# Phase 0: Web Warriors ⚔️
## Topic 2: DNS Magic and Internals

> **First Principle:** Every device on the internet is identified by a number (IP address). Humans remember names, not numbers. DNS is the globally distributed system that bridges that gap — translating `google.com` into `142.250.190.46` in milliseconds.

---

## 1. What is DNS (Domain Name System)?

### The Core Problem DNS Solves
Without DNS, to visit Google you'd have to type `142.250.190.46` into your browser. DNS lets you type `google.com` instead and handles the translation automatically.

### DNS in One Sentence
**DNS is a globally distributed, hierarchical database that maps human-readable domain names to machine-readable IP addresses.**

### Real-World Analogy
Think of DNS like a **contacts app on your phone:**
```
Contact Name  →  Phone Number
google.com    →  142.250.190.46
github.com    →  140.82.112.4
```
Just like you don't memorize phone numbers — you look up the name — your browser uses DNS to look up IP addresses from domain names.

### Why "Distributed"?
There is no single DNS server that knows everything. The system is split across thousands of servers worldwide, each responsible for a piece of the namespace. This makes it:
- **Fast** — Servers are geographically distributed, reducing latency
- **Resilient** — No single point of failure
- **Scalable** — Billions of queries per day handled globally

---

## 2. How DNS Resolves Domain Names to IP Addresses

### The Full Resolution Journey (Step by Step)

When you type `www.example.com` in your browser:

```
Step 1: Browser Cache
  → "Have I looked up example.com recently?"
  → Yes? Use cached IP. No? Continue.

Step 2: OS Cache
  → Checks the local machine's DNS cache
  → Yes? Use cached IP. No? Continue.

Step 3: /etc/hosts file (Linux/Mac) or hosts file (Windows)
  → Local override file checked first before any network query
  → No match? Continue.

Step 4: Recursive Resolver (your ISP or Google's 8.8.8.8)
  → Your machine asks: "What's the IP for www.example.com?"
  → The resolver does the heavy lifting on your behalf

Step 5: Root Name Server
  → Resolver asks: "Where do I find .com domains?"
  → Root server replies: "Ask the .com TLD servers"

Step 6: TLD Name Server (.com)
  → Resolver asks: "Where do I find example.com?"
  → TLD server replies: "Ask example.com's authoritative server"

Step 7: Authoritative Name Server
  → Resolver asks: "What's the IP for www.example.com?"
  → Authoritative server replies: "It's 93.184.216.34"

Step 8: Response returned
  → Resolver sends IP back to your browser
  → Browser caches the result (for TTL duration)
  → Browser connects to 93.184.216.34
```

### Visual Flow
```
Browser
  │
  ├─── Cache hit? ──Yes──→ Done ✓
  │
  No
  │
  ↓
Recursive Resolver (ISP / 8.8.8.8 / 1.1.1.1)
  │
  ├─── Cache hit? ──Yes──→ Return IP ✓
  │
  No
  │
  ↓
Root Name Server (13 sets worldwide)
  "Go ask .com TLD servers"
  │
  ↓
TLD Name Server (.com / .org / .in / etc.)
  "Go ask example.com's own name server"
  │
  ↓
Authoritative Name Server (for example.com)
  "www.example.com = 93.184.216.34" ✓
  │
  ↓
Answer travels back up the chain → Browser → Page loads
```

### Two Types of DNS Queries

| Query Type | Who Does It | Description |
|---|---|---|
| **Recursive** | Recursive Resolver | "Find me the full answer, I'll wait" — does all the work |
| **Iterative** | Resolver asking each server | "Who should I ask next?" — each server gives a referral |

Your browser makes a **recursive** query to the resolver. The resolver makes **iterative** queries to root → TLD → authoritative servers.

---

## 3. Types of DNS Records

DNS records are entries in a DNS zone file. Each record type serves a specific purpose.

### A Record — Address Record (Most Common)
Maps a domain name to an **IPv4** address.

```
example.com.     IN  A     93.184.216.34
www.example.com. IN  A     93.184.216.34
```

- One domain can have **multiple A records** (load balancing)
- When a browser resolves a domain, it ultimately needs an A (or AAAA) record

### AAAA Record — IPv6 Address Record
Maps a domain name to an **IPv6** address.

```
example.com.  IN  AAAA  2606:2800:220:1:248:1893:25c8:1946
```

### CNAME Record — Canonical Name (Alias)
Maps one domain name to **another domain name** (not directly to an IP).

```
www.example.com.   IN  CNAME  example.com.
blog.example.com.  IN  CNAME  example.com.
```

**Key Rule:** A CNAME cannot point to an IP address — only to another domain name. The resolver follows the chain until it hits an A record.

```
www.example.com
  → CNAME → example.com
              → A → 93.184.216.34  ✓
```

**When to use CNAME:** Aliases, subdomains, CDN integration (e.g., pointing your domain to Cloudflare or Vercel).

### MX Record — Mail Exchange
Tells email servers where to deliver email for a domain.

```
example.com.  IN  MX  10  mail1.example.com.
example.com.  IN  MX  20  mail2.example.com.
```

- The number (`10`, `20`) is the **priority** — lower number = higher priority
- Multiple MX records = fallback if the primary mail server is down

### TXT Record — Text Record
Stores arbitrary text. Used for verification and security.

```
example.com.  IN  TXT  "v=spf1 include:_spf.google.com ~all"
example.com.  IN  TXT  "google-site-verification=abc123xyz"
```

**Common uses:**
| Use Case | What It Does |
|---|---|
| **SPF** | Specifies which servers can send email for your domain |
| **DKIM** | Cryptographic signature for email authentication |
| **DMARC** | Policy for handling emails that fail SPF/DKIM |
| **Domain Verification** | Proving you own a domain to Google, GitHub, etc. |

### NS Record — Name Server
Specifies which DNS servers are **authoritative** for the domain.

```
example.com.  IN  NS  ns1.exampledns.com.
example.com.  IN  NS  ns2.exampledns.com.
```

When you buy a domain and set it up with a hosting provider, you update the NS records to point to their DNS servers.

### PTR Record — Pointer Record (Reverse DNS)
Maps an **IP address back to a domain name** (opposite of A record).

```
34.216.184.93.in-addr.arpa.  IN  PTR  example.com.
```

Used for: email spam filtering, network diagnostics, logging.

### SOA Record — Start of Authority
Contains administrative information about a DNS zone.

```
example.com.  IN  SOA  ns1.example.com. admin.example.com. (
                          2024010101  ; Serial number
                          3600        ; Refresh (1 hour)
                          900         ; Retry (15 min)
                          604800      ; Expire (7 days)
                          300 )       ; Minimum TTL (5 min)
```

### SRV Record — Service Record
Specifies the location of services (host + port).

```
_http._tcp.example.com.  IN  SRV  10  5  80  www.example.com.
```

Used by: SIP (VoIP), XMPP (chat), game servers.

### Complete DNS Record Cheat Sheet

| Record | Maps | Example Use |
|---|---|---|
| **A** | Domain → IPv4 | `example.com → 93.184.216.34` |
| **AAAA** | Domain → IPv6 | `example.com → 2606:...` |
| **CNAME** | Domain → Domain | `www → example.com` |
| **MX** | Domain → Mail server | Email delivery |
| **TXT** | Domain → Text string | SPF, DKIM, verification |
| **NS** | Domain → Name server | Who is authoritative? |
| **PTR** | IP → Domain | Reverse lookup |
| **SOA** | Zone metadata | Admin info, serial number |
| **SRV** | Service → Host:Port | VoIP, game servers |
| **CAA** | Domain → Allowed CA | Which CAs can issue SSL certs |

---

## 4. DNS Hierarchy

DNS is structured as an **inverted tree**. Understanding this hierarchy is key to understanding how DNS resolution works.

### The Hierarchy (Top to Bottom)

```
                        . (Root)
                        │
          ┌─────────────┼─────────────┐
         .com          .org          .in   ← TLDs
          │             │
     ┌────┴────┐    ┌───┴───┐
  google    example  wikipedia       ← Second-Level Domains
     │
  ┌──┴──┐
 www   mail                          ← Subdomains
```

### Level 1: Root DNS Servers

- There are **13 root server IP addresses** (named A through M)
- In reality, these are **clusters of hundreds of servers** worldwide using anycast routing
- They know nothing about specific domains — only **which TLD servers to ask**
- Operated by ICANN, NASA, VeriSign, and others

```
Root servers:
a.root-servers.net  →  198.41.0.4
b.root-servers.net  →  199.9.14.201
...
m.root-servers.net  →  202.12.27.33
```

### Level 2: TLD (Top-Level Domain) Servers

TLD servers are authoritative for their top-level domain.

| TLD Type | Examples | Managed By |
|---|---|---|
| **Generic (gTLD)** | `.com`, `.org`, `.net`, `.io` | ICANN-accredited registries |
| **Country Code (ccTLD)** | `.in`, `.uk`, `.jp`, `.de` | Country-specific organizations |
| **New gTLD** | `.app`, `.dev`, `.cloud` | Various registries |

TLD servers know which **authoritative name servers** are responsible for each domain registered under them.

### Level 3: Authoritative Name Servers

These are the **source of truth** for a specific domain. When you register `example.com` and configure DNS:

- Your domain registrar (GoDaddy, Namecheap, etc.) stores NS records pointing to your authoritative servers
- Your authoritative servers hold all the DNS records for your domain (A, CNAME, MX, TXT, etc.)
- Common authoritative DNS providers: Cloudflare, AWS Route 53, Google Cloud DNS

```
Who owns what:
example.com's NS records → point to → ns1.cloudflare.com
ns1.cloudflare.com → stores → all DNS records for example.com
```

### Level 4: Recursive Resolvers

Not part of the hierarchy but critical to the process. These are the **middlemen** that do the work of querying the hierarchy on your behalf.

| Provider | IP Addresses | Notes |
|---|---|---|
| Google Public DNS | `8.8.8.8`, `8.8.4.4` | Fast, widely used |
| Cloudflare DNS | `1.1.1.1`, `1.0.0.1` | Privacy-focused, very fast |
| Your ISP's DNS | Varies | Default, may log queries |
| OpenDNS | `208.67.222.222` | Filtering options |

---

## 5. How Browsers Query DNS to Load Websites

### The Full Browser Journey

When you hit Enter on `https://www.github.com`:

```
1. URL Parsing
   → Browser extracts: protocol=https, host=www.github.com, path=/

2. DNS Resolution (detailed above)
   → www.github.com → 140.82.112.4

3. TCP Connection
   → Browser opens TCP connection to 140.82.112.4:443

4. TLS Handshake (because HTTPS)
   → Browser and server agree on encryption
   → Server presents SSL certificate
   → Secure channel established

5. HTTP Request
   → GET / HTTP/2
   → Host: www.github.com

6. Server Response
   → HTML, CSS, JS, images sent back

7. Rendering
   → Browser parses and displays the page
```

### Where DNS Fits in Page Load Time

```
Total Page Load Time
├── DNS Resolution          →  0–200ms  (cached: ~0ms)
├── TCP Connection          →  1 RTT
├── TLS Handshake           →  1–2 RTTs
├── HTTP Request + Response →  1+ RTTs
└── Rendering               →  varies
```

DNS is often the **first bottleneck**. That's why DNS caching and fast resolvers matter for web performance.

### DNS Pre-fetching (Web Dev Optimization)
Browsers can resolve DNS for links on a page **before the user clicks them**:

```html
<!-- Tell browser to pre-resolve DNS for this domain -->
<link rel="dns-prefetch" href="//cdn.example.com">

<!-- Even more aggressive: pre-connect (DNS + TCP + TLS) -->
<link rel="preconnect" href="https://cdn.example.com">
```

### Checking DNS in Browser DevTools
1. Open DevTools → Network tab
2. Click any request
3. Look at "Timing" → **DNS Lookup** row
4. Cached DNS = 0ms; uncached = 10–200ms

---

## 6. Key Concepts Deep Dive

### Recursive Queries

A **recursive query** is when a client (your browser) asks a resolver: *"Give me the final answer, do all the work for me."*

The resolver is obligated to:
1. Check its own cache
2. If not cached, query the DNS hierarchy (root → TLD → authoritative)
3. Return the final IP address to the client

```
Browser ────recursive query────→ Recursive Resolver
Browser ←───final IP answer───── Recursive Resolver
                                      │
                          (iterative queries internally)
                                      ↓
                              Root → TLD → Authoritative
```

Contrast with an **iterative query**, where each server just gives a referral ("ask that server over there") and the client does the follow-up work itself. Recursive resolvers use iterative queries when talking to root/TLD/authoritative servers.

### Caching

DNS caching happens at multiple levels to speed up subsequent lookups:

```
Level 1: Browser cache       (Chrome: chrome://net-internals/#dns)
Level 2: OS cache            (Windows: ipconfig /displaydns | Mac: sudo dscacheutil -cachedump)
Level 3: Recursive Resolver  (ISP or 8.8.8.8 caches results)
Level 4: Authoritative NS    (never caches — always authoritative)
```

**Why caching matters:**
- First lookup: ~50–300ms (full resolution chain)
- Subsequent lookups: ~0ms (served from cache)
- Reduces load on DNS infrastructure globally

**Cache invalidation problem:** If you change your server's IP and update your A record, old IPs are still cached everywhere until TTL expires. This is DNS propagation delay.

### TTL (Time-to-Live)

TTL is a value (in seconds) attached to every DNS record that tells resolvers **how long to cache the record**.

```
example.com.  IN  A  93.184.216.34  TTL: 3600
                                         ↑
                                  Cache for 3600 seconds = 1 hour
```

#### TTL Strategy Guide for Web Devs

| Scenario | Recommended TTL | Reason |
|---|---|---|
| Stable production site | 86400 (24h) | Minimize DNS load, faster for users |
| Before a planned migration | 300 (5 min) | Lower TTL first, then change IP |
| During active migration | 60–300 (1–5 min) | Fast failover if something breaks |
| After migration complete | 86400 (24h) | Return to normal |

**The Golden Rule:** Lower your TTL 24–48 hours BEFORE changing DNS records. Then after the change, raise it back.

#### TTL in Practice
```bash
# Check TTL on a DNS record
dig example.com A

# Output:
;; ANSWER SECTION:
example.com.    3571  IN  A  93.184.216.34
                ↑
        Seconds remaining in cache (was 3600, now 3571)
```

### DNS Security Concerns

| Attack | Description | Defense |
|---|---|---|
| **DNS Spoofing / Cache Poisoning** | Injecting fake DNS records into a resolver's cache | DNSSEC |
| **DNS Hijacking** | Redirecting DNS queries to malicious servers | DNSSEC, DoH |
| **DNS Amplification (DDoS)** | Using open resolvers to amplify attack traffic | Rate limiting, BCP38 |
| **DNS Snooping** | ISP or network watching your DNS queries | DNS over HTTPS (DoH), DNS over TLS (DoT) |

**DNSSEC** — DNS Security Extensions
- Adds cryptographic signatures to DNS records
- Resolvers can verify records haven't been tampered with
- Does NOT encrypt DNS traffic (just signs it)

**DoH (DNS over HTTPS)**
- Encrypts DNS queries inside HTTPS traffic
- Hides DNS queries from network observers
- Enabled in: Firefox, Chrome, Windows 11

---

## 7. Practical Commands

```bash
# Basic DNS lookup
nslookup example.com
dig example.com

# Look up a specific record type
dig example.com A
dig example.com MX
dig example.com TXT
dig example.com NS
dig example.com AAAA

# Use a specific DNS server (not your default)
dig @8.8.8.8 example.com
dig @1.1.1.1 example.com

# Trace the full DNS resolution chain
dig +trace example.com

# Reverse DNS lookup (IP → domain)
dig -x 93.184.216.34
nslookup 93.184.216.34

# Check TTL remaining
dig example.com | grep -i ttl

# Flush DNS cache
# Mac:
sudo dscacheutil -flushcache && sudo killall -HUP mDNSResponder
# Windows:
ipconfig /flushdns
# Linux:
sudo systemd-resolve --flush-caches

# View all cached DNS (Windows)
ipconfig /displaydns

# View Chrome's DNS cache
# Open: chrome://net-internals/#dns
```

---

## 8. DNS in Web Development — Real-World Scenarios

### Scenario 1: Deploying a New Website
```
1. Buy domain: example.com (via Namecheap/GoDaddy)
2. Set up hosting (Vercel/Netlify/AWS)
3. Hosting provider gives you: 76.76.21.21
4. Add A record: example.com → 76.76.21.21
5. Add CNAME: www.example.com → example.com
6. Wait for TTL to expire across the internet (DNS propagation)
7. Verify: dig example.com A
```

### Scenario 2: Setting Up Email (Gmail / Google Workspace)
```
Add MX records:
example.com  MX  1   aspmx.l.google.com.
example.com  MX  5   alt1.aspmx.l.google.com.
example.com  MX  10  alt2.aspmx.l.google.com.

Add TXT record for SPF:
example.com  TXT  "v=spf1 include:_spf.google.com ~all"
```

### Scenario 3: Using a CDN (Cloudflare)
```
1. Sign up for Cloudflare, add your domain
2. Cloudflare gives you NS records:
   ns1.cloudflare.com
   ns2.cloudflare.com
3. Update NS records at your registrar to point to Cloudflare
4. All DNS is now managed through Cloudflare
5. Cloudflare proxies traffic → hides your origin IP
```

### Scenario 4: Zero-Downtime Server Migration
```
Day -2: Lower TTL from 86400 → 300
Day -1: Wait for old TTL to expire everywhere
Day  0: Change A record to new server IP
        (propagates in max 300 seconds now)
Day +1: Verify everything works
Day +2: Raise TTL back to 86400
```

---

## 9. Summary — What to Remember

| Concept | One-Line Summary |
|---|---|
| **DNS** | Translates domain names → IP addresses |
| **Recursive Resolver** | Does the full lookup work on your behalf (8.8.8.8, 1.1.1.1) |
| **Root Servers** | 13 IPs, know where to find TLD servers |
| **TLD Server** | Knows which NS servers own a domain (.com, .org, .in) |
| **Authoritative NS** | The source of truth for a specific domain's records |
| **A Record** | Domain → IPv4 |
| **CNAME** | Domain → another domain (alias) |
| **MX** | Email delivery routing |
| **TXT** | Verification, SPF, DKIM |
| **TTL** | How long a record is cached (in seconds) |
| **DNS Propagation** | Time for TTL to expire globally after a change |
| **DNSSEC** | Cryptographic verification of DNS records |
| **DoH** | Encrypts DNS queries inside HTTPS |

---

## 10. Interview / Knowledge Check Questions

1. What is DNS and why does it exist?
2. Walk me through every step of DNS resolution when you visit `www.github.com`
3. What is the difference between a recursive and iterative DNS query?
4. What's the difference between an A record and a CNAME record? When would you use each?
5. What is TTL and why should you lower it before changing DNS records?
6. What are the 13 root name servers and what do they actually do?
7. What is the difference between a TLD server and an authoritative name server?
8. How would you set up DNS for a new domain with a website and email?
9. What is DNS cache poisoning and how does DNSSEC prevent it?
10. What is DNS over HTTPS and why does it matter for privacy?
11. What `dig` command would you use to trace the full DNS resolution chain?
12. Why does DNS propagation take time even after you've updated a record?

---

## 11. Resources to Go Deeper

- **Visual:** [howdns.works](https://howdns.works) — Comic-strip DNS explanation
- **Tool:** [DNS Checker](https://dnschecker.org) — Check propagation worldwide
- **Tool:** `dig +trace example.com` — Live DNS resolution trace in your terminal
- **Spec:** RFC 1034 & RFC 1035 — Original DNS specifications
- **Article:** Cloudflare's DNS Learning Center — [cloudflare.com/learning/dns](https://www.cloudflare.com/learning/dns/what-is-dns/)
- **Tool:** [MXToolbox](https://mxtoolbox.com) — Debug MX, SPF, DKIM records
- **Browser:** `chrome://net-internals/#dns` — See Chrome's live DNS cache

---

*Next up → Phase 0, Topic 3: HTTP & HTTPS — the protocol browsers and servers speak*