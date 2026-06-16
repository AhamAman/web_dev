# Phase 0: Web Warriors ⚔️
## Topic 3: Server-Client Architecture

> **First Principle:** Every interaction on the web is a conversation between two parties — one that asks (client) and one that answers (server). Understanding this conversation, its structure, and its rules is the foundation of everything in web development.

---

## 1. What is the Client-Server Model?

### The Core Idea
The client-server model is an **architectural pattern** where responsibilities are divided between two types of programs:

- **Client** — the one that *requests* resources or services
- **Server** — the one that *provides* resources or services in response

This is not unique to the web. It's a universal computing pattern:

```
ATM Machine         ←→  Bank's Server
Your Email App      ←→  Gmail's Mail Server
A Video Game        ←→  Game Server
Your Browser        ←→  Web Server
Mobile Banking App  ←→  Bank's API Server
```

### First Principles Breakdown
Before the client-server model, computers either ran everything locally (standalone) or shared resources chaotically. The client-server model introduced:

1. **Separation of concerns** — client handles presentation, server handles data/logic
2. **Centralized resources** — one server can serve many clients
3. **Scalability** — add more servers when demand grows
4. **Security** — sensitive data stays on the server, never exposed to the client

### The Simplest Mental Model
```
Client: "Hey server, can I have the homepage?"
Server: "Sure, here's the HTML for it."
Client: "Thanks, I'll display it to the user."
```

That exchange — multiplied billions of times per day — is the entire web.

---

## 2. Differences Between Client and Server

### Side-by-Side Comparison

| Aspect | Client | Server |
|---|---|---|
| **Who initiates?** | Always initiates requests | Always responds to requests |
| **Examples** | Browser, mobile app, curl, Postman | Apache, Nginx, Node.js, Django |
| **Where it runs** | User's device | Data center / cloud |
| **Resources** | Limited (user's hardware) | Powerful (dedicated hardware) |
| **Trust level** | Untrusted (user can manipulate it) | Trusted (you control it) |
| **Can it be offline?** | Yes, temporarily | No (defeats the purpose) |
| **Language examples** | HTML, CSS, JavaScript | Python, Node.js, Java, PHP, Go, Ruby |
| **Access to DB?** | Never directly | Yes |
| **User sees the code?** | Yes (View Source) | No (runs privately) |

### Critical Security Implication
```
❌ WRONG thinking:
"I'll validate the form on the client side (JavaScript), that's enough."

✅ CORRECT thinking:
"I'll validate on the client side for UX, but ALWAYS validate again
on the server side. The client can never be trusted — anyone can
bypass client-side JavaScript."
```

### Multiple Clients, One Server
A server doesn't talk to just one client — it handles many simultaneously:

```
Browser (Chrome)     ─┐
Browser (Firefox)    ─┤
Mobile App (iOS)     ─┼──→  Web Server  ──→  Database
Mobile App (Android) ─┤
curl / API client    ─┘
```

### A Client Can Also Be a Server
In complex systems, a server for one service is a client of another:

```
Browser → Web Server → Database Server
            ↑               ↑
     (server to browser) (client of DB)
```

This is the foundation of **microservices architecture**.

---

## 3. The HTTP Request-Response Cycle

### What is HTTP?
**HTTP (HyperText Transfer Protocol)** is the agreed-upon language clients and servers use to communicate on the web. It's a **stateless, text-based, request-response protocol**.

- **Stateless** — Every request is independent. The server doesn't remember previous requests (cookies/sessions solve this)
- **Text-based** — HTTP messages are human-readable text (until HTTP/2 which uses binary)
- **Request-Response** — Every interaction is a pair: one request, one response

### Anatomy of an HTTP Request

```
GET /products/shoes?color=red HTTP/1.1
Host: www.example.com
Accept: text/html,application/json
Accept-Language: en-US
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)
Cookie: session_id=abc123
Connection: keep-alive
                                       ← blank line (end of headers)
                                       ← body (empty for GET requests)
```

**Breaking it down:**
```
[Method] [Path][Query String] [HTTP Version]
GET      /products/shoes?color=red HTTP/1.1

[Headers]
Host: www.example.com          ← Required: which domain is being requested
Accept: text/html              ← What formats client can handle
User-Agent: Mozilla/5.0        ← What client is making the request
Cookie: session_id=abc123      ← State sent with every request

[Body]                         ← Empty for GET, has data for POST/PUT/PATCH
```

### Anatomy of an HTTP Response

```
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 3421
Cache-Control: max-age=3600
Set-Cookie: session_id=abc123; HttpOnly; Secure
Date: Tue, 16 Jun 2026 09:30:00 GMT
Server: nginx/1.24.0
                                       ← blank line (end of headers)
<!DOCTYPE html>
<html>
  <head><title>Products - Shoes</title></head>
  <body>
    <h1>Red Shoes</h1>
    ...
  </body>
</html>
```

**Breaking it down:**
```
[HTTP Version] [Status Code] [Status Text]
HTTP/1.1       200           OK

[Response Headers]
Content-Type: text/html        ← What format is the body in?
Content-Length: 3421           ← How many bytes in the body?
Cache-Control: max-age=3600    ← How long can client cache this?
Set-Cookie: session_id=abc123  ← Server setting a cookie on client

[Body]
<!DOCTYPE html>...             ← The actual content
```

### The Full Request-Response Cycle (Step by Step)

```
1. User types URL / clicks link in browser
         ↓
2. DNS Resolution (domain → IP address)
         ↓
3. TCP Connection established (3-way handshake)
         ↓
4. TLS Handshake (if HTTPS) — encryption negotiated
         ↓
5. HTTP Request sent by client
   GET /index.html HTTP/1.1
   Host: example.com
         ↓
6. Server receives and parses request
         ↓
7. Server processes request
   - Static file? Read from disk and return it
   - Dynamic? Run code (PHP/Python/Node), query DB, build response
         ↓
8. Server sends HTTP Response
   HTTP/1.1 200 OK
   Content-Type: text/html
   [HTML body]
         ↓
9. Client receives response
         ↓
10. Browser parses HTML
    - Finds <link> for CSS → new HTTP request
    - Finds <script> for JS → new HTTP request
    - Finds <img> tags → new HTTP requests (one per image)
         ↓
11. Browser renders the page
```

### HTTP Methods (Verbs)

HTTP methods define **what action** the client wants to perform:

| Method | Action | Has Body? | Idempotent? | Safe? |
|---|---|---|---|---|
| **GET** | Retrieve a resource | No | Yes | Yes |
| **POST** | Create a new resource | Yes | No | No |
| **PUT** | Replace a resource entirely | Yes | Yes | No |
| **PATCH** | Partially update a resource | Yes | No | No |
| **DELETE** | Remove a resource | No | Yes | No |
| **HEAD** | Like GET but no body returned | No | Yes | Yes |
| **OPTIONS** | What methods does this endpoint support? | No | Yes | Yes |

**Idempotent** — Calling it multiple times gives the same result
**Safe** — Does not modify any data on the server

### REST Convention (How Methods Map to Actions)
```
GET    /users          → List all users
POST   /users          → Create a new user
GET    /users/42       → Get user with ID 42
PUT    /users/42       → Replace user 42 entirely
PATCH  /users/42       → Update specific fields of user 42
DELETE /users/42       → Delete user 42
```

---

## 4. How Browsers Act as Clients

### The Browser's Job
A browser is the most sophisticated HTTP client ever built. It doesn't just send one request — loading a single webpage triggers **dozens to hundreds** of HTTP requests:

```
GET /          → HTML (1 request)
GET /style.css → CSS (1 request per stylesheet)
GET /app.js    → JavaScript (1 request per script)
GET /logo.png  → Image (1 request per image)
GET /font.woff → Font (1 request per font)
GET /api/user  → API data (via JavaScript fetch/XHR)
...
```

Open DevTools → Network tab on any website and watch this happen in real time.

### Browser Rendering Pipeline
After receiving the HTML response:

```
HTML received
     ↓
Parse HTML → Build DOM (Document Object Model)
     ↓
Encounter <link rel="stylesheet"> → Fetch CSS
     ↓
Parse CSS → Build CSSOM (CSS Object Model)
     ↓
Combine DOM + CSSOM → Render Tree
     ↓
Encounter <script> → Fetch + Execute JS
(JS can modify the DOM dynamically)
     ↓
Layout → Calculate positions and sizes
     ↓
Paint → Draw pixels on screen
     ↓
Composite → Final visible page
```

### Browser Caching
The browser caches responses to avoid re-downloading unchanged resources:

```
First visit:
  GET /style.css → 200 OK (full response, 15KB)
  Browser caches it with Cache-Control: max-age=86400

Second visit (same day):
  → Browser uses cached version, NO network request
  → Instant load

After 24 hours (cache expired):
  GET /style.css → 304 Not Modified (server says "use cache")
  OR
  GET /style.css → 200 OK (new version)
```

### Types of HTTP Clients (Not Just Browsers)

| Client | Use Case | Example Tool |
|---|---|---|
| **Browser** | Human-facing web apps | Chrome, Firefox, Safari |
| **curl** | Command line HTTP requests | `curl https://api.example.com` |
| **Postman / Insomnia** | API testing and development | GUI tools for developers |
| **fetch / axios** | JavaScript HTTP in browser/Node | `fetch('https://api.example.com')` |
| **HTTP libraries** | Server-to-server requests | Python requests, Go net/http |
| **Mobile apps** | Native app → backend API | iOS URLSession, Android OkHttp |
| **Web scrapers** | Automated data extraction | Scrapy, Puppeteer, Playwright |

---

## 5. Introduction to Web Servers and Web Hosting

### What is a Web Server?
A **web server** is software that:
1. Listens for incoming HTTP requests (on port 80 for HTTP, 443 for HTTPS)
2. Processes those requests
3. Returns HTTP responses

```
          HTTP Request
Client ──────────────→ Web Server Software (Nginx/Apache)
                              │
                    ┌─────────┴──────────┐
                    ↓                    ↓
              Static Files        Dynamic Request
              (HTML, CSS, JS,     (PHP, Python, Node)
               images)                   │
                    │                    ↓
                    │             App Server / Framework
                    │             (Django, Express, Laravel)
                    │                    │
                    │                    ↓
                    │               Database
                    │             (MySQL, PostgreSQL)
                    │                    │
                    └──────────┬─────────┘
                               ↓
                          HTTP Response
Client ←──────────────────────────────────
```

### Apache vs Nginx — The Two Giants

#### Apache HTTP Server
- Created in 1995, the original dominant web server
- **Process/thread-based** — spawns a new process or thread per connection
- Very mature, extensive module ecosystem
- Excellent for shared hosting (`.htaccess` per-directory config)
- Slower under very high concurrency

```
# Apache config example (httpd.conf or .htaccess)
<VirtualHost *:80>
    ServerName example.com
    DocumentRoot /var/www/html
    DirectoryIndex index.html index.php
</VirtualHost>
```

#### Nginx (pronounced "Engine-X")
- Created in 2004, designed for high concurrency
- **Event-driven, non-blocking** — one worker handles thousands of connections
- Faster at serving static files
- Widely used as a **reverse proxy** in front of app servers
- Used by Netflix, Airbnb, GitHub, WordPress.com

```nginx
# Nginx config example (nginx.conf)
server {
    listen 80;
    server_name example.com;
    root /var/www/html;
    index index.html;

    location /api/ {
        proxy_pass http://localhost:3000;  # Forward to Node.js app
    }
}
```

#### Apache vs Nginx Comparison

| Feature | Apache | Nginx |
|---|---|---|
| **Architecture** | Thread/process per connection | Event-driven, async |
| **Static files** | Good | Excellent (faster) |
| **High concurrency** | Struggles | Handles thousands easily |
| **Config style** | `.htaccess` per directory | Centralized config files |
| **Dynamic content** | Built-in PHP module | Via proxy to app server |
| **Use as reverse proxy** | Possible but complex | Native, simple config |
| **Market share** | ~30% | ~34% |
| **Best for** | Shared hosting, legacy PHP | Modern apps, high traffic |

### Other Web Servers Worth Knowing

| Server | Language | Best For |
|---|---|---|
| **Node.js (Express)** | JavaScript | APIs, real-time apps |
| **Gunicorn / uWSGI** | Python | Django/Flask apps |
| **Puma / Unicorn** | Ruby | Rails apps |
| **Caddy** | Go | Automatic HTTPS, modern simplicity |
| **IIS** | C++ | Windows/.NET environments |
| **Tomcat** | Java | Java web applications |

### Nginx as Reverse Proxy (Common Pattern)

A **reverse proxy** sits in front of your app server and forwards requests to it:

```
Internet → Nginx (port 80/443) → Node.js App (port 3000)
                 ↑
         Handles: SSL termination
                  Static file serving
                  Load balancing
                  Compression (gzip)
                  Rate limiting
                  Caching
```

This is the standard production setup for most web applications.

### Web Hosting Types

| Type | Description | Best For | Examples |
|---|---|---|---|
| **Shared Hosting** | Multiple sites share one server | Small sites, beginners | Hostinger, Bluehost |
| **VPS (Virtual Private Server)** | Dedicated virtual machine slice | Growing sites, more control | DigitalOcean, Linode |
| **Dedicated Server** | Entire physical server | High-traffic sites | Hetzner, OVH |
| **Cloud Hosting** | Scalable, pay-per-use | Modern apps, variable traffic | AWS, GCP, Azure |
| **PaaS** | Platform manages infrastructure | Developers who don't want DevOps | Heroku, Railway, Render |
| **Serverless** | Functions, no server management | Event-driven APIs | Vercel, Netlify, AWS Lambda |
| **Static Hosting** | Serves pre-built files only | Portfolios, static sites | GitHub Pages, Netlify, Vercel |

---

## 6. Key Concepts Deep Dive

### Request Headers

Headers are **metadata** sent with every HTTP request or response. They tell the other side important information about the message.

#### Common Request Headers

| Header | Purpose | Example |
|---|---|---|
| `Host` | Which domain is being requested (required in HTTP/1.1) | `Host: www.example.com` |
| `User-Agent` | Identifies the client software | `User-Agent: Mozilla/5.0 ...` |
| `Accept` | What content types the client understands | `Accept: text/html, application/json` |
| `Accept-Encoding` | What compression formats are supported | `Accept-Encoding: gzip, deflate, br` |
| `Accept-Language` | Preferred language | `Accept-Language: en-US, hi;q=0.9` |
| `Authorization` | Credentials for authenticated requests | `Authorization: Bearer eyJhbG...` |
| `Content-Type` | Format of the request body | `Content-Type: application/json` |
| `Content-Length` | Size of request body in bytes | `Content-Length: 348` |
| `Cookie` | Sends stored cookies to server | `Cookie: session_id=abc123` |
| `Referer` | The page that linked to this request | `Referer: https://google.com/` |
| `Origin` | Where the request originated (CORS) | `Origin: https://app.example.com` |
| `Cache-Control` | Caching directives | `Cache-Control: no-cache` |
| `Connection` | Connection management | `Connection: keep-alive` |

#### Common Response Headers

| Header | Purpose | Example |
|---|---|---|
| `Content-Type` | Format of the response body | `Content-Type: application/json` |
| `Content-Length` | Size of response body in bytes | `Content-Length: 1234` |
| `Cache-Control` | How long to cache the response | `Cache-Control: max-age=86400` |
| `Set-Cookie` | Set a cookie on the client | `Set-Cookie: session=abc; HttpOnly` |
| `Location` | URL for redirects (3xx responses) | `Location: https://example.com/new` |
| `Server` | Server software info | `Server: nginx/1.24.0` |
| `Strict-Transport-Security` | Force HTTPS (HSTS) | `max-age=31536000; includeSubDomains` |
| `X-Content-Type-Options` | Prevent MIME sniffing | `X-Content-Type-Options: nosniff` |
| `Access-Control-Allow-Origin` | CORS permission | `Access-Control-Allow-Origin: *` |
| `ETag` | Resource version identifier (caching) | `ETag: "33a64df551..."` |

### HTTP Response Status Codes

Status codes are **three-digit numbers** that tell the client what happened with their request.

#### The Five Classes

```
1xx — Informational  (processing, continue)
2xx — Success        (request succeeded)
3xx — Redirection    (go somewhere else)
4xx — Client Error   (you did something wrong)
5xx — Server Error   (we did something wrong)
```

#### 2xx — Success Codes

| Code | Name | Meaning |
|---|---|---|
| **200** | OK | Request succeeded, response body contains the data |
| **201** | Created | Resource was created (after POST) |
| **204** | No Content | Success, but no body to return (after DELETE) |
| **206** | Partial Content | Partial content returned (video streaming, downloads) |

#### 3xx — Redirection Codes

| Code | Name | Meaning |
|---|---|---|
| **301** | Moved Permanently | Resource has permanently moved — update your bookmarks |
| **302** | Found | Temporary redirect — keep the original URL |
| **304** | Not Modified | Cached version is still valid — use it |
| **307** | Temporary Redirect | Like 302 but preserves HTTP method |
| **308** | Permanent Redirect | Like 301 but preserves HTTP method |

**301 vs 302 — SEO Matters:**
```
301 → "This page is gone forever, update your links"
      (Search engines transfer ranking to the new URL)

302 → "Temporarily moved, keep linking to the old one"
      (Search engines keep the old URL in the index)
```

#### 4xx — Client Error Codes

| Code | Name | Meaning |
|---|---|---|
| **400** | Bad Request | Malformed request syntax |
| **401** | Unauthorized | Not authenticated — need to log in |
| **403** | Forbidden | Authenticated but not authorized — no permission |
| **404** | Not Found | Resource doesn't exist |
| **405** | Method Not Allowed | Wrong HTTP method for this endpoint |
| **408** | Request Timeout | Client took too long to send request |
| **409** | Conflict | Resource conflict (e.g., duplicate username) |
| **410** | Gone | Resource existed but is permanently deleted |
| **422** | Unprocessable Entity | Validation errors (commonly used in APIs) |
| **429** | Too Many Requests | Rate limit exceeded |

**401 vs 403 — Important Distinction:**
```
401 Unauthorized → "Who are you? Please log in."
403 Forbidden    → "I know who you are, but you can't access this."
```

#### 5xx — Server Error Codes

| Code | Name | Meaning |
|---|---|---|
| **500** | Internal Server Error | Generic server crash / unhandled exception |
| **501** | Not Implemented | Server doesn't support this feature |
| **502** | Bad Gateway | Upstream server (e.g., app server) returned an invalid response |
| **503** | Service Unavailable | Server is overloaded or down for maintenance |
| **504** | Gateway Timeout | Upstream server didn't respond in time |

**502 vs 504 in Nginx:**
```
502 Bad Gateway  → Nginx reached the app server, but got garbage back
504 Gateway Timeout → Nginx reached out to app server, but it never replied
```

### Client-Side vs Server-Side — Where Does Code Run?

#### Client-Side
Code runs in the **user's browser**. The user can see and modify it.

```javascript
// This runs in the browser (client-side)
document.getElementById('btn').addEventListener('click', () => {
    console.log('Button clicked!');
    fetch('/api/data').then(res => res.json()).then(data => {
        document.getElementById('output').textContent = data.value;
    });
});
```

- Languages: HTML, CSS, JavaScript (only)
- Frameworks: React, Vue, Angular, Svelte
- Can access: DOM, browser APIs, localStorage
- Cannot access: Database, filesystem, secrets/API keys

#### Server-Side
Code runs on the **server**. Users never see it.

```python
# This runs on the server (Python/Django)
def get_user(request, user_id):
    user = User.objects.get(id=user_id)  # Database query
    return JsonResponse({'name': user.name, 'email': user.email})
```

- Languages: Python, Node.js, PHP, Ruby, Go, Java, Rust
- Frameworks: Django, Express, Laravel, Rails, Gin, Spring
- Can access: Database, filesystem, environment variables, secrets
- Cannot access: The user's browser or DOM

#### The Golden Rule
```
✅ Put on the SERVER: business logic, database access,
   authentication, sensitive operations, API keys

✅ Put on the CLIENT: UI rendering, user interactions,
   form validation (for UX), animations

❌ NEVER put on the CLIENT: Database credentials, API secret keys,
   passwords, critical business logic that can be bypassed
```

---

## 7. HTTP Versions — Evolution

| Version | Year | Key Feature |
|---|---|---|
| **HTTP/0.9** | 1991 | Only GET, only HTML |
| **HTTP/1.0** | 1996 | Headers, status codes, multiple content types |
| **HTTP/1.1** | 1997 | Persistent connections, chunked transfer, `Host` header required |
| **HTTP/2** | 2015 | Binary (not text), multiplexing, header compression, server push |
| **HTTP/3** | 2022 | Built on QUIC (UDP), faster connection setup, better mobile performance |

**HTTP/1.1 problem (head-of-line blocking):**
```
Request 1 ────→ Wait for response ────→ Response 1
Request 2 ──────────────────────────────────────────→ (must wait)
Request 3 ─────────────────────────────────────────────────────→ (must wait)
```

**HTTP/2 solution (multiplexing):**
```
Request 1 ──→    Response 1 ←──
Request 2 ──→    Response 2 ←──   (all at once, interleaved)
Request 3 ──→    Response 3 ←──
```

---

## 8. Practical Tools

```bash
# Make HTTP requests from the terminal
curl https://example.com
curl -I https://example.com                    # Headers only (HEAD request)
curl -v https://example.com                    # Verbose (see full request + response)
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Alice", "email": "alice@example.com"}'

# Check response status code only
curl -o /dev/null -s -w "%{http_code}" https://example.com

# Follow redirects
curl -L https://example.com

# Check response headers
curl -D - https://example.com -o /dev/null

# See what web server a site uses
curl -I https://example.com | grep -i server

# Check HTTP/2 support
curl --http2 -I https://example.com | head -1
```

```javascript
// Fetch API (browser & Node.js 18+)
// GET request
const response = await fetch('https://api.example.com/users');
console.log(response.status);         // 200
console.log(response.headers.get('content-type')); // application/json
const data = await response.json();

// POST request
const res = await fetch('https://api.example.com/users', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name: 'Alice' })
});
```

---

## 9. Real-World Architecture Patterns

### Simple Static Site
```
User → CDN (Cloudflare) → Static Files (HTML/CSS/JS)
```

### Typical Web Application
```
User → Load Balancer → Nginx → Node.js / Python App → Database
                          ↓
                    Static Files (served by Nginx directly)
```

### Modern Decoupled Architecture (SPA + API)
```
User → CDN → React/Vue SPA (client-side rendering)
               ↓ (API calls via fetch)
            API Gateway → Microservices → Database(s)
```

### Serverless / Edge
```
User → Vercel/Netlify Edge → Serverless Function → Database
(Function spins up on demand, no persistent server)
```

---

## 10. Summary — What to Remember

| Concept | One-Line Summary |
|---|---|
| **Client** | Initiates requests, runs on user's device, cannot be trusted |
| **Server** | Responds to requests, runs in data center, trusted |
| **HTTP** | The text-based, stateless protocol clients and servers speak |
| **Request** | Method + Path + Headers + Body |
| **Response** | Status Code + Headers + Body |
| **GET** | Read data — no body, safe, idempotent |
| **POST** | Create data — has body, not idempotent |
| **2xx** | Success |
| **3xx** | Redirect |
| **4xx** | Client made an error |
| **5xx** | Server made an error |
| **401 vs 403** | Not authenticated vs not authorized |
| **Apache** | Thread-based, great for shared hosting, `.htaccess` |
| **Nginx** | Event-driven, great for static files + reverse proxy |
| **Reverse Proxy** | Nginx sits in front of app server, handles SSL + routing |
| **Client-side** | Runs in browser, user can see it — never put secrets here |
| **Server-side** | Runs on server, user can't see it — safe for secrets and DB |

---

## 11. Interview / Knowledge Check Questions

1. Explain the client-server model. What are the roles of each?
2. Walk through every step of what happens when you click a link on a webpage
3. What is the difference between GET and POST? When would you use each?
4. What does HTTP status code 200, 201, 301, 302, 400, 401, 403, 404, 500 mean?
5. What is the difference between 401 and 403?
6. What are HTTP headers? Give 5 examples of request headers and what they do
7. What is a reverse proxy and why is Nginx commonly used as one?
8. What is the difference between Apache and Nginx architecturally?
9. What is the difference between client-side and server-side code? What should never go on the client?
10. What is HTTP/2 and how does multiplexing solve a problem in HTTP/1.1?
11. What does "stateless" mean in the context of HTTP? How do sessions solve this?
12. What is a `304 Not Modified` response and when does it occur?

---

## 12. Resources to Go Deeper

- **MDN Web Docs:** [HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) — authoritative reference
- **Tool:** Browser DevTools → Network tab — watch every HTTP request/response live
- **Tool:** `curl -v` — see raw HTTP requests and responses in terminal
- **Tool:** [Postman](https://www.postman.com/) — GUI for making and testing HTTP requests
- **Book:** *HTTP: The Definitive Guide* by David Gourley — deep reference
- **Spec:** RFC 7230–7235 — HTTP/1.1 specifications
- **Interactive:** [httptoolkit.tech](https://httptoolkit.tech) — intercept and debug HTTP traffic
- **Nginx Docs:** [nginx.org/en/docs](https://nginx.org/en/docs/) — official reference

---

*Next up → Phase 0, Topic 4: How Browsers Work — parsing, rendering, and the DOM*