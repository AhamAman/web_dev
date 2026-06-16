# Phase 0: Web Warriors ⚔️
## Topic 1: How the Internet Works

> **First Principle:** Before writing a single line of code, understand the infrastructure your code runs on. The internet is not magic — it's a global system of physical machines talking to each other through agreed-upon rules.

---

## 1. Introduction to the Concept of the Internet

### What is the Internet?
The internet is a **global network of interconnected computers and devices** that communicate with each other using standardized protocols. Think of it as a massive postal system — but instead of letters, it sends packets of digital data.

### Key Mental Model
```
Your Device → Local Network → ISP → Internet Backbone → Destination Server
```

### First Principles Breakdown
- At its core, the internet is just **wires + agreed-upon rules (protocols)**
- Every device connected to the internet has a unique address (IP address)
- Data is broken into small chunks called **packets**, sent independently, and reassembled at the destination
- No single entity "owns" the internet — it's a decentralized network of networks

### Why This Matters for Web Dev
Every time your browser loads a page, fetches an API, or submits a form — it's using this infrastructure. Understanding it helps you debug latency issues, understand security boundaries, and optimize performance.

---

## 2. Overview of the World Wide Web (WWW)

### WWW vs The Internet — They Are NOT the Same
| | Internet | World Wide Web |
|---|---|---|
| **What it is** | The physical + logical network infrastructure | A service that runs ON TOP of the internet |
| **Think of it as** | The highway system | Cars and roads (HTTP, HTML, URLs) |
| **Invented by** | ARPANET (1960s–70s) | Tim Berners-Lee (1989) |
| **Examples** | Email, FTP, DNS, VoIP | Websites, web apps, REST APIs |

### How the WWW Works (First Principles)
1. A user types a URL into a browser
2. The browser uses **DNS** to resolve the domain name to an IP address
3. The browser sends an **HTTP/HTTPS request** to that IP address
4. The server responds with **HTML, CSS, JS** (or data like JSON)
5. The browser **renders** the response into what you see on screen

### Core WWW Technologies
- **HTTP/HTTPS** — The protocol for sending and receiving web content
- **HTML** — The structure/content of a web page
- **CSS** — The styling and visual presentation
- **JavaScript** — The behavior and interactivity
- **URLs** — The addressing system for web resources

---

## 3. How Data Is Transferred Across Networks

### Packet Switching (First Principles)
The internet doesn't send data as one continuous stream. It breaks data into small **packets** and sends them independently.

```
Large File (e.g., an image)
    ↓
Split into Packets [P1][P2][P3][P4][P5]
    ↓
Each packet travels independently through the network
(may take different routes!)
    ↓
Reassembled at destination → Original File
```

### Why Packets?
- **Efficiency:** Multiple people can share the same network simultaneously
- **Resilience:** If one route fails, packets find another route
- **Error recovery:** If a packet is lost, only that packet is re-sent (not the whole file)

### The OSI Model (Simplified — 4 Layers You Need to Know)
| Layer | Name | What it Does | Example |
|---|---|---|---|
| 4 | Application | What the app sends/receives | HTTP, HTTPS, DNS, FTP |
| 3 | Transport | Breaks data into packets, ensures delivery | TCP, UDP |
| 2 | Network | Routes packets across the internet | IP addresses, routers |
| 1 | Physical | Actual hardware transmission | Fiber optic, WiFi, Ethernet |

### TCP vs UDP — Two Transfer Protocols
| | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
|---|---|---|
| **Reliability** | Guaranteed delivery, in order | No guarantee |
| **Speed** | Slower (handshake required) | Faster |
| **Use cases** | Web pages, file downloads, emails | Video streaming, gaming, DNS |
| **Error handling** | Re-sends lost packets | Drops lost packets |

### The TCP Handshake (3-Way)
```
Client → Server : SYN ("I want to connect")
Server → Client : SYN-ACK ("Acknowledged, ready")
Client → Server : ACK ("Let's go!")
             ↓
        Connection Established
```
This happens every time your browser loads a website over HTTP.

---

## 4. Understanding IP Addresses, Domain Names, and Routing

### IP Addresses
An **IP (Internet Protocol) address** is a unique numerical label assigned to every device on a network.

#### IPv4 (Current Standard)
```
192.168.1.1
```
- 4 numbers separated by dots
- Each number: 0–255
- Total possible addresses: ~4.3 billion (running out!)

#### IPv6 (New Standard)
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```
- 128-bit address
- Virtually unlimited addresses

#### Public vs Private IP
| | Public IP | Private IP |
|---|---|---|
| **Assigned by** | Your ISP | Your router |
| **Visible to** | The entire internet | Only your local network |
| **Example** | `203.0.113.42` | `192.168.1.5` |

### Domain Names
Humans remember names, not numbers. Domain names map to IP addresses.

```
google.com  →  142.250.190.46
```

#### Anatomy of a URL
```
https://www.example.com:443/path/to/page?query=value#section
  │       │      │       │       │             │         │
scheme  subdomain domain  port   path        query    fragment
```

### DNS — The Domain Name System
DNS is the internet's **phone book**. It translates human-readable domain names into IP addresses.

#### How DNS Resolution Works (Step by Step)
```
1. You type: www.example.com
2. Your browser checks its cache → Not found
3. OS checks its cache → Not found
4. Query sent to Recursive Resolver (usually your ISP)
5. Resolver asks Root Name Server → "Try .com servers"
6. Resolver asks .com TLD Server → "Try example.com's server"
7. Resolver asks Authoritative Name Server → "The IP is 93.184.216.34"
8. IP returned to browser → Connection established
```

#### DNS Record Types
| Record | Purpose | Example |
|---|---|---|
| **A** | Domain → IPv4 address | `example.com → 93.184.216.34` |
| **AAAA** | Domain → IPv6 address | `example.com → 2606:2800:...` |
| **CNAME** | Alias to another domain | `www.example.com → example.com` |
| **MX** | Mail server for domain | `mail.example.com` |
| **TXT** | Verification/misc text | SPF, DKIM for email security |

### Routing
Once the IP address is known, the data must be **routed** to its destination.

```
Your Device → Home Router → ISP → Internet Exchange Point → Destination ISP → Server
```

- **Routers** are devices that forward packets toward their destination
- Each router only knows the **next hop**, not the full path
- The **BGP (Border Gateway Protocol)** is what makes large-scale internet routing work
- Tools to trace routing: `traceroute` (Linux/Mac) or `tracert` (Windows)

```bash
# See every router hop between you and google.com
traceroute google.com
```

---

## 5. Key Concepts Deep Dive

### Internet Service Providers (ISPs)

ISPs are companies that provide internet access. They operate at different tiers:

| Tier | Description | Examples |
|---|---|---|
| **Tier 1** | Own backbone infrastructure, peer with each other for free | AT&T, NTT, Tata Communications |
| **Tier 2** | Regional networks, buy transit from Tier 1 | BSNL, Airtel, regional telcos |
| **Tier 3** | Local ISPs, buy from Tier 2 | Your local internet provider |

**The chain:**
```
Tier 1 (global backbone)
    ↕ (peering/transit)
Tier 2 (regional)
    ↕ (transit)
Tier 3 (local ISP)
    ↕ (last mile connection)
Your Home/Office
```

### Routers
A router's job is to **forward packets toward their destination** based on routing tables.

- **Home Router:** Connects your local network (LAN) to your ISP (WAN)
- **Core Routers:** Handle massive amounts of traffic across the internet backbone
- **Routing Table:** A map of "if packet is going to X, send it to Y next"

```
Simplified Routing Table:
Destination     Next Hop        Interface
192.168.1.0/24  directly        eth0 (local network)
0.0.0.0/0       203.0.113.1     eth1 (to ISP — default route)
```

### DNS (Expanded)

#### DNS Caching — Why It Matters
DNS responses are cached to speed things up. The cache duration is controlled by **TTL (Time To Live)** in seconds.

```
example.com  A  93.184.216.34  TTL: 3600
                                    ↑
                              Cache for 1 hour
```

**Implication for web devs:** When you change a domain's IP address (e.g., moving servers), it takes time to propagate because of caching. This is called **DNS propagation** and can take up to 48 hours.

#### HTTPS and DNS Security
- Regular DNS queries are **unencrypted** — someone on your network can see what sites you visit
- **DNS over HTTPS (DoH)** and **DNS over TLS (DoT)** encrypt DNS queries
- **DNSSEC** adds cryptographic signatures to prevent DNS spoofing

---

## 6. Practical Tools to Explore These Concepts

```bash
# Find the IP address of a domain
nslookup google.com
dig google.com

# Trace the route packets take
traceroute google.com       # Linux/Mac
tracert google.com          # Windows

# Check your own public IP
curl ifconfig.me

# See DNS records
dig google.com ANY

# Ping a server (basic connectivity test)
ping google.com

# Check what's listening on your machine
netstat -tuln
```

---

## 7. Summary — What to Remember

| Concept | One-Line Summary |
|---|---|
| **Internet** | Global network of connected computers |
| **WWW** | A service (websites) that runs on the internet |
| **IP Address** | Unique ID for every device on a network |
| **DNS** | Phone book that converts domain names → IP addresses |
| **Packets** | Data broken into small chunks for efficient transmission |
| **TCP** | Reliable, ordered delivery protocol (used by HTTP) |
| **UDP** | Fast, unreliable protocol (used by video streaming) |
| **ISP** | Company that sells you internet access |
| **Router** | Device that forwards packets toward their destination |
| **TTL** | How long a DNS record is cached |

---

## 8. Interview / Knowledge Check Questions

1. What is the difference between the internet and the World Wide Web?
2. What happens step-by-step when you type `https://google.com` in your browser?
3. What is an IP address, and what's the difference between IPv4 and IPv6?
4. Explain DNS resolution from scratch — what is a recursive resolver?
5. What is packet switching and why does the internet use it?
6. What is the difference between TCP and UDP? When would you use each?
7. What is a TTL in DNS and why does it matter?
8. What is the difference between a public and private IP address?
9. What does a router actually do?
10. What is BGP?

---

## 9. Resources to Go Deeper

- **Article:** [How DNS Works (dnsimple.com)](https://howdns.works/) — comic-style explanation
- **Tool:** [Wireshark](https://www.wireshark.org/) — see actual network packets in real time
- **Tool:** [DNS Checker](https://dnschecker.org/) — check DNS propagation globally
- **Video:** "How the Internet Works in 5 Minutes" by Aaron Titus
- **RFC 791** — The original IP specification (primary source)
- **RFC 793** — The original TCP specification
- **Book:** *Computer Networks* by Andrew Tanenbaum (deep reference)

---

*Next up → Phase 0, Topic 2: HTTP & HTTPS — the language browsers and servers speak*