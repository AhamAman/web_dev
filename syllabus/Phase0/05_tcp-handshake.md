# Topic 5: TCP Handshakes and the 3-Way Handshake (First Principles)

## 0. The problem this exists to solve

Before touching the handshake itself, sit with the actual problem TCP was built to solve, because the handshake only makes sense as a consequence of it.

The internet's base layer (IP) gives you almost nothing. It moves packets from one address to another on a "best effort" basis: packets can get lost, arrive out of order, arrive duplicated, or get corrupted, and IP itself does not care or tell you. If two programs on different machines want to exchange a stream of bytes and be *sure* the other side received everything, in order, exactly once, something has to sit on top of IP and manufacture that guarantee out of an unreliable substrate.

That something is TCP. And to manufacture reliability over an unreliable channel, both sides first need to agree on some shared state before any real data moves: a starting point to count from, and confirmation that both ends are actually present and willing to talk. That agreement step is the handshake. It is not bureaucracy for its own sake — it is the minimum negotiation required before "reliable, ordered delivery" can mean anything at all.

## 1. What is a 3-way handshake in TCP?

It's the three-message exchange a client and server perform to open a TCP connection before any application data (like an HTTP request) is sent. The three messages are conventionally called **SYN**, **SYN-ACK**, and **ACK**.

The deeper purpose: each side of a TCP connection maintains its own independent byte counter, called a **sequence number**, used to track exactly which bytes have been sent and received. Two machines that have never spoken can't assume anything about each other's counters. The handshake is how they introduce these counters to each other and confirm receipt, in both directions, before trusting the connection enough to send real data.

## 2. Walking through the three phases

**Phase 1 — SYN (synchronize):**
The client picks a random 32-bit starting number for its own counter — its **Initial Sequence Number (ISN)**. It sends a TCP segment with the SYN flag set and `seq = ISN_client`. Nothing else is in this packet; it carries no application data. This says, in effect, "I'd like to open a connection, and I'm going to start counting my bytes from this number."

**Phase 2 — SYN-ACK (synchronize-acknowledge):**
The server, if it's listening on that port, replies with two flags set at once: SYN and ACK. It picks its own random ISN (`ISN_server`) for its own counter, and acknowledges the client's SYN by setting `ack = ISN_client + 1`. So this single packet does two jobs simultaneously: "I confirm I received your starting number" (the ACK part) and "here is my own starting number" (the SYN part). That's why it's one combined step rather than two separate ones.

**Phase 3 — ACK (acknowledge):**
The client confirms it received the server's ISN by replying with `ack = ISN_server + 1`. At this point, both machines have exchanged and confirmed each other's starting sequence numbers. The connection moves into the `ESTABLISHED` state on both ends, and the client is now free to send real application data (in practice, this ACK can even be combined with the first chunk of data — more on that in the expert section).

A small but important detail: each side's acknowledgment number is the peer's ISN *plus one*. That's because the SYN flag itself is treated as consuming one sequence number, even though it carries no payload. This convention lets the receiving side unambiguously confirm "I got your SYN" rather than something that could be confused with acknowledging real data.

## 3. Why three messages, not two or four?

This is where reasoning from first principles really pays off, because the number three isn't arbitrary.

**Why not two?** If the handshake stopped after SYN and SYN-ACK, the server would never know whether its SYN-ACK actually arrived. The client received the server's ISN, but the server has no confirmation of that fact. It would be forced to guess, or to start accepting data optimistically without certainty the client agrees on its sequence numbering. Two messages establish trust in only one direction.

**Why is three enough?** After the third message, both sides have positive confirmation: the client knows the server received its ISN (because the server's SYN-ACK acknowledged it), and the server knows the client received its ISN (because the client's final ACK acknowledged it). Three is the minimum number of messages needed to confirm both directions, because the second message is allowed to do double duty (acknowledge one direction while introducing the other).

This is closely related to a classic problem in distributed systems called the **Two Generals Problem**: over a channel where messages can be lost, you can never achieve perfect, simultaneous certainty for both parties using a finite number of messages. TCP's handshake doesn't violate that — it doesn't aim for perfect certainty, it aims for *practical* mutual agreement that's good enough to start exchanging data, with the reliability mechanisms that come after (timeouts, retransmission) cleaning up if any of these three packets get lost along the way.

## 4. The state machine underneath

It helps to see this as a state transition on each side, because "ESTABLISHED" doesn't happen instantly — it's reached at different moments for client and server.

Server side: `CLOSED → LISTEN` (waiting for a SYN) `→ SYN_RECEIVED` (got the SYN, sent SYN-ACK, waiting for final ACK) `→ ESTABLISHED` (got the final ACK).

Client side: `CLOSED → SYN_SENT` (sent the SYN, waiting for SYN-ACK) `→ ESTABLISHED` (got the SYN-ACK, sent the final ACK — it doesn't wait for confirmation of that last ACK to consider itself established).

Notice the asymmetry: the client reaches `ESTABLISHED` one message earlier than it can be *certain* the server has too. This is exactly why the connection is sometimes described as reaching agreement "good enough to proceed" rather than perfect simultaneous certainty — it's the practical resolution of the Two Generals tension mentioned above.

## 5. How data flows after the handshake completes

Once both sides are in `ESTABLISHED`, sequence numbers keep doing the same job they did during the handshake, just now for real payload bytes instead of the SYN itself. Every byte sent gets a sequence number continuing on from the ISN, and the receiver sends back acknowledgments stating the next byte number it expects, which is how the sender learns what successfully arrived.

TCP doesn't wait for an acknowledgment after every single segment, since that would be painfully slow. Instead it uses a **sliding window**: the sender can have multiple unacknowledged segments in flight at once, up to a size advertised by the receiver (its available buffer space), and acknowledgments are cumulative — one ACK can confirm a whole batch of bytes at once. If an expected acknowledgment doesn't arrive within a calculated retransmission timeout, TCP assumes loss and resends, which is the actual mechanism that makes the "reliable" in "reliable, ordered delivery" true. The handshake just sets the starting line; this windowing-and-acknowledgment machinery is the ongoing engine of reliability.

## 6. Key concepts, tied together

- **Reliable connection establishment** — the handshake exists so that no application data is ever sent into a connection whose state isn't mutually confirmed by both endpoints first.
- **Sequence numbers** — independent 32-bit counters per direction, randomized at connection start (not starting at zero) specifically so that old, lingering packets from a previous, already-closed connection between the same two ports can't be mistaken for new data on a fresh connection.
- **Acknowledgments** — confirmations of "I received up to byte N," used both to finish the handshake and, afterward, to drive retransmission and flow control for the life of the connection.

## 7. Expert-level nuances worth knowing as a web developer

**Latency cost.** The handshake is one full round trip (RTT) before a single byte of your actual HTTP request can go out. For HTTPS, a TLS handshake stacks on top of that (one or two more RTTs depending on TLS version), meaning a "cold" HTTPS connection can cost two to three round trips before your server even sees the request. This is the real reason browser DevTools shows separate "Connecting" and "TLS" timing bars before "Waiting (TTFB)" even starts — and it's why keep-alive connections, connection pooling, and HTTP/2's single shared connection per origin all exist: to amortize this fixed cost across many requests instead of paying it repeatedly.

**HTTP/3 and QUIC.** This handshake cost is exactly the problem QUIC (the transport HTTP/3 runs on) was designed to attack. QUIC runs over UDP and merges the transport handshake with the cryptographic handshake into a single round trip, and on reconnecting to a known server it can send data with effectively zero extra round trips (0-RTT). Knowing why the classic TCP handshake costs what it costs is what makes QUIC's design make sense rather than feeling like an arbitrary optimization.

**SYN floods.** Because the server allocates state the moment it receives a SYN and replies with SYN-ACK (entering `SYN_RECEIVED`), an attacker can send many SYNs and never complete the third step, leaving the server holding many half-open connections and exhausting its resources — a classic denial-of-service technique. The common defense, **SYN cookies**, encodes the connection state into the SYN-ACK's own sequence number cryptographically instead of storing it in memory, so the server doesn't have to commit resources until the final ACK actually arrives.

**TCP Fast Open (TFO).** For repeat connections to a server you've connected to before, TFO allows a small amount of data to ride along inside the very first SYN packet, using a cookie issued during an earlier handshake — shaving off the wait for the handshake to fully complete before sending the first request. It's a niche but real optimization used by some CDNs and browsers.

## 8. A note on what comes next

Opening a connection is only half the lifecycle — closing one is its own four-step process involving FIN and ACK flags, with its own subtleties (like the `TIME_WAIT` state), which is worth covering as its own topic when you get there in your syllabus.

## How to actually see this, not just read about it

Reading the theory only goes so far — open your browser's DevTools Network tab on any HTTPS site and look at the "Connecting" timing breakdown, or run `curl -v https://example.com` and watch the connection-then-TLS sequence in the output, or capture traffic with Wireshark on a local request and filter for `tcp.flags.syn==1` to watch the actual SYN, SYN-ACK, ACK sequence with your own eyes. Seeing the three packets and their sequence numbers in a real capture will cement this far better than any explanation can.