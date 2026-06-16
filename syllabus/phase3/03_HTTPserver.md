# 🚀 Node.js Mastery Roadmap

## Phase 3: Creating a Basic HTTP Server

---

# 🎯 Mission of This Phase

Before learning Express.js, databases, authentication, or REST APIs, you must understand:

> How the web actually works underneath.

Most developers use frameworks.

Veteran engineers understand what frameworks are hiding.

This phase teaches how to build an HTTP server directly using Node.js Core Modules.

---

# 🧠 First Principles Understanding

## What Problem Does a Server Solve?

A server exists for one purpose:

> Receive requests and send responses.

Everything else is an abstraction.

Examples:

* Browser requests a webpage
* Mobile app requests user data
* Frontend requests product information
* API receives form submissions

---

## First Principle

```text
Client → Request → Server
Server → Response → Client
```

The web is simply machines exchanging messages.

---

# 🌐 Understanding HTTP

## What is HTTP?

HTTP stands for:

```text
HyperText Transfer Protocol
```

It defines rules for communication between:

* Browsers
* Servers
* APIs
* Mobile Applications

---

## HTTP Communication Flow

```text
Browser
    ↓
HTTP Request
    ↓
Server
    ↓
HTTP Response
    ↓
Browser
```

---

## Real Example

### Request

```http
GET /users HTTP/1.1
Host: localhost:3000
```

### Response

```http
HTTP/1.1 200 OK

Users Data
```

---

# 1️⃣ Introduction to the HTTP Module

## Core Understanding

Node.js includes a built-in module:

```js
const http = require("http");
```

No installation required.

---

## Why It Exists

The HTTP module allows Node.js to:

* Listen for requests
* Process requests
* Send responses

Without frameworks.

---

## Checklist

* [ ] Understand what the HTTP module does.
* [ ] Import the HTTP module.
* [ ] Learn how Node.js listens for requests.
* [ ] Understand server lifecycle.

---

## Veteran Insight

* [ ] Express, NestJS, and Fastify ultimately rely on Node's HTTP capabilities.
* [ ] Understanding HTTP removes framework dependency.

---

# 2️⃣ Creating Your First HTTP Server

## Basic Server Example

```js
const http = require("http");

const server = http.createServer((req, res) => {
    res.end("Hello World");
});

server.listen(3000, () => {
    console.log("Server running");
});
```

---

## Execution Flow

```text
Client Request
       ↓
HTTP Server Receives Request
       ↓
Request Handler Executes
       ↓
Response Sent
```

---

## Checklist

* [ ] Create a server.
* [ ] Listen on a port.
* [ ] Return plain text.
* [ ] Access localhost from browser.

---

## Veteran Understanding

* [ ] One server handles many requests.
* [ ] Every request triggers the callback function.

---

# 3️⃣ Understanding Request and Response Objects

## Request Object (req)

Represents incoming client data.

---

### Important Properties

```js
req.url
req.method
req.headers
```

---

## Checklist

* [ ] Access request URL.
* [ ] Access HTTP method.
* [ ] Access request headers.
* [ ] Log request information.

---

## Response Object (res)

Represents outgoing server response.

---

### Important Methods

```js
res.write()
res.end()
res.setHeader()
res.statusCode
```

---

## Checklist

* [ ] Send text response.
* [ ] Send JSON response.
* [ ] Set headers.
* [ ] Set status codes.

---

## Veteran Insight

* [ ] Every framework wraps req and res.
* [ ] Understanding them makes debugging easier.

---

# 4️⃣ Understanding Routing

## What is Routing?

Routing determines:

> Which code executes for a specific URL.

---

## Example

```text
/           → Home
/users      → Users List
/products   → Products
/about      → About Page
```

---

## Manual Routing Example

```js
if (req.url === "/") {
    res.end("Home");
}
else if (req.url === "/users") {
    res.end("Users");
}
```

---

## Routing Flow

```text
Request URL
      ↓
Route Matching
      ↓
Execute Handler
      ↓
Send Response
```

---

## Checklist

* [ ] Create multiple routes.
* [ ] Return different responses.
* [ ] Handle unknown routes.

---

## Veteran Understanding

* [ ] Express Router is built on this concept.
* [ ] Routing is pattern matching.

---

# 5️⃣ HTTP Methods

## Why HTTP Methods Exist

URLs identify resources.

Methods define actions.

---

## GET

Retrieve data.

```http
GET /users
```

---

## POST

Create data.

```http
POST /users
```

---

## PUT

Update data.

```http
PUT /users/1
```

---

## DELETE

Delete data.

```http
DELETE /users/1
```

---

## CRUD Mapping

```text
Create → POST
Read   → GET
Update → PUT
Delete → DELETE
```

---

## Checklist

* [ ] Detect request methods.
* [ ] Handle GET requests.
* [ ] Handle POST requests.
* [ ] Handle PUT requests.
* [ ] Handle DELETE requests.

---

## Example

```js
if (req.method === "GET") {
    res.end("Fetching Data");
}
```

---

## Veteran Insight

* [ ] REST APIs rely heavily on HTTP methods.
* [ ] Method misuse creates poor API design.

---

# 6️⃣ Sending Data to Clients

## Sending Text

```js
res.end("Hello");
```

---

## Sending HTML

```js
res.setHeader("Content-Type", "text/html");

res.end("<h1>Hello</h1>");
```

---

## Sending JSON

```js
res.setHeader("Content-Type", "application/json");

res.end(
    JSON.stringify({
        message: "Success"
    })
);
```

---

## Checklist

* [ ] Send plain text.
* [ ] Send HTML.
* [ ] Send JSON.
* [ ] Set correct content types.

---

## Veteran Understanding

* [ ] Content-Type tells clients how to interpret data.
* [ ] APIs primarily return JSON.

---

# 7️⃣ Receiving Data from Clients

## Why Receive Data?

Clients often send:

* User registration data
* Login credentials
* Form submissions
* API payloads

---

## Request Body Flow

```text
Client
   ↓
JSON Data
   ↓
HTTP Request
   ↓
Server Reads Body
   ↓
Process Data
```

---

## Basic Body Parsing

```js
let body = "";

req.on("data", chunk => {
    body += chunk;
});

req.on("end", () => {
    console.log(body);
});
```

---

## Checklist

* [ ] Receive POST data.
* [ ] Parse JSON requests.
* [ ] Handle malformed input.
* [ ] Validate request body.

---

## Veteran Insight

* [ ] Express body-parser exists because this process is repetitive.
* [ ] Input validation is a security requirement.

---

# 8️⃣ Status Codes

## Why Status Codes Exist

They communicate result outcomes.

---

## Common Codes

### Success

```text
200 OK
201 Created
```

---

### Client Errors

```text
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
```

---

### Server Errors

```text
500 Internal Server Error
```

---

## Example

```js
res.statusCode = 404;

res.end("Not Found");
```

---

## Checklist

* [ ] Return 200 responses.
* [ ] Return 404 responses.
* [ ] Return 500 responses.
* [ ] Use proper status codes.

---

## Veteran Understanding

* [ ] Status codes are part of API contracts.
* [ ] Proper status codes simplify frontend development.

---

# 9️⃣ Building a Mini REST API

## Project Goal

Create:

```text
/users
```

Supporting:

```text
GET
POST
PUT
DELETE
```

---

## API Flow

```text
Client Request
      ↓
Route Matching
      ↓
Method Matching
      ↓
Business Logic
      ↓
Response
```

---

## Checklist

* [ ] GET all users.
* [ ] POST a user.
* [ ] UPDATE a user.
* [ ] DELETE a user.
* [ ] Return JSON responses.

---

## Veteran Understanding

* [ ] REST APIs are simply HTTP servers with structured routes.

---

# 🔥 Core Concepts Master Checklist

## HTTP

* [ ] Explain HTTP from memory.
* [ ] Explain request-response lifecycle.

---

## Server Creation

* [ ] Create server from scratch.
* [ ] Listen on custom ports.

---

## Request Object

* [ ] Read URL.
* [ ] Read method.
* [ ] Read headers.

---

## Response Object

* [ ] Send text.
* [ ] Send HTML.
* [ ] Send JSON.
* [ ] Send status codes.

---

## Routing

* [ ] Build manual routing.
* [ ] Handle unknown routes.

---

## HTTP Methods

* [ ] Explain CRUD mapping.
* [ ] Handle GET, POST, PUT, DELETE.

---

# 🧪 Veteran-Level Exercises

## Beginner

* [ ] Hello World server.
* [ ] About page route.
* [ ] Contact page route.

---

## Intermediate

* [ ] JSON API server.
* [ ] Simple notes API.
* [ ] User management API.

---

## Advanced

* [ ] Build mini Express clone.
* [ ] Build custom router.
* [ ] Build REST API without frameworks.

---

# ⚠️ Common Beginner Mistakes

* [ ] Forgetting res.end().
* [ ] Not setting Content-Type.
* [ ] Ignoring status codes.
* [ ] Hardcoding responses.
* [ ] Not validating request bodies.
* [ ] Not handling 404 routes.

---

# 🏆 Veteran Thinking Questions

* [ ] Why do frameworks exist if Node.js already has an HTTP module?
* [ ] What performance overhead do frameworks add?
* [ ] How does Express simplify routing?
* [ ] How does a browser interpret HTTP responses?
* [ ] Why is JSON the dominant API format?

---

# 📚 Learning Sequence

```text
HTTP Fundamentals
      ↓
HTTP Module
      ↓
Request Object
      ↓
Response Object
      ↓
Routing
      ↓
HTTP Methods
      ↓
JSON APIs
      ↓
REST Architecture
```

---

# ✅ Phase Completion Criteria

You have mastered this phase when you can:

* [ ] Build an HTTP server without frameworks.
* [ ] Explain request-response lifecycle.
* [ ] Handle GET, POST, PUT, DELETE requests.
* [ ] Send JSON responses.
* [ ] Receive client data.
* [ ] Create manual routing logic.
* [ ] Build a small REST API from scratch.

---

# 🚀 Next Phase

```text
Node Core Modules
      ↓
File System Module (fs)
      ↓
Path Module
      ↓
OS Module
      ↓
Process Module
      ↓
Streams & Buffers
      ↓
Building Production Applications
```
