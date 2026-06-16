# 🚀 Node.js Mastery Roadmap

## Phase 5: RESTful API Design – Building APIs with Express

---

# 🎯 Mission of This Phase

Most developers learn how to create API routes.

Few learn how to design APIs.

A poorly designed API becomes difficult to:

* Scale
* Maintain
* Secure
* Document
* Integrate

A well-designed API feels predictable.

---

## First Principle

A REST API is not about Express.

A REST API is about:

> Exposing business resources through standardized HTTP communication.

Think:

```text
Users
Products
Orders
Payments
Comments
```

Not:

```text
getUsersData
fetchProductInfo
deleteOrderNow
```

Veteran engineers design APIs around resources, not actions.

---

# 🧠 First Principles Understanding

## Why Do APIs Exist?

Without APIs:

```text
Frontend
   ↓
Direct Database Access
```

Problems:

* Security Risks
* Tight Coupling
* No Validation
* No Business Rules

---

## API Architecture

```text
Client
   ↓
API Layer
   ↓
Business Logic
   ↓
Database
```

The API acts as a contract.

---

## REST Philosophy

REST stands for:

```text
Representational State Transfer
```

---

### Core REST Principle

Everything is treated as a resource.

Examples:

```text
/users
/products
/orders
/comments
```

---

# 1️⃣ Understanding REST Architecture

## REST Characteristics

### Resource-Based

Good:

```text
/users
/products
/orders
```

Bad:

```text
/getUsers
/createUser
/deleteUser
```

---

### Stateless

Every request contains all required information.

Example:

```text
Request A
```

Does not depend on:

```text
Request B
```

---

### Uniform Interface

Same rules everywhere.

Example:

```text
GET     → Read
POST    → Create
PUT     → Update
DELETE  → Delete
```

---

## Checklist

* [ ] Understand resources.
* [ ] Understand stateless communication.
* [ ] Understand uniform interfaces.
* [ ] Explain REST from memory.

---

## Veteran Insight

* [ ] REST is a communication philosophy.
* [ ] Express is merely an implementation tool.

---

# 2️⃣ Designing RESTful Endpoints

## Resource Naming Rules

Use nouns.

---

### Good Examples

```text
/users
/products
/orders
```

---

### Bad Examples

```text
/getUsers
/deleteUser
/createProduct
```

---

## Collection vs Single Resource

### Collection

```text
/users
```

Returns:

```json
[
  {
    "id": 1
  }
]
```

---

### Single Resource

```text
/users/1
```

Returns:

```json
{
  "id": 1
}
```

---

## Checklist

* [ ] Design resource endpoints.
* [ ] Separate collections and resources.
* [ ] Follow naming conventions.

---

## Veteran Understanding

* [ ] URL structure communicates intent.
* [ ] Predictable APIs reduce documentation requirements.

---

# 3️⃣ CRUD Operations

## CRUD Mapping

```text
Create → POST
Read   → GET
Update → PUT
Delete → DELETE
```

---

## GET

Retrieve data.

```http
GET /users
```

```http
GET /users/1
```

---

## POST

Create data.

```http
POST /users
```

Request:

```json
{
  "name": "John"
}
```

---

## PUT

Replace existing resource.

```http
PUT /users/1
```

---

## PATCH

Partial update.

```http
PATCH /users/1
```

---

## DELETE

Remove resource.

```http
DELETE /users/1
```

---

## Checklist

* [ ] Build all CRUD routes.
* [ ] Understand method semantics.
* [ ] Use correct methods.

---

## Veteran Insight

* [ ] Many APIs misuse POST for everything.
* [ ] Correct HTTP methods improve API clarity.

---

# 4️⃣ Building REST APIs with Express

## Example Structure

```js
app.get("/users", handler);

app.get("/users/:id", handler);

app.post("/users", handler);

app.put("/users/:id", handler);

app.delete("/users/:id", handler);
```

---

## Request Lifecycle

```text
Request
   ↓
Middleware
   ↓
Validation
   ↓
Controller
   ↓
Database
   ↓
Response
```

---

## Checklist

* [ ] Create resource routes.
* [ ] Create CRUD handlers.
* [ ] Return JSON responses.

---

## Veteran Understanding

* [ ] Route handlers should remain thin.
* [ ] Business logic belongs elsewhere.

---

# 5️⃣ Query Parameters

## Why Query Parameters Exist

Query parameters modify responses.

---

## Examples

### Pagination

```http
GET /users?page=1&limit=10
```

---

### Sorting

```http
GET /users?sort=name
```

---

### Filtering

```http
GET /users?role=admin
```

---

## Express Access

```js
req.query
```

---

## Checklist

* [ ] Implement pagination.
* [ ] Implement sorting.
* [ ] Implement filtering.

---

## Veteran Insight

* [ ] Query parameters should never identify resources.
* [ ] Query parameters modify collections.

---

# 6️⃣ Request Body Handling

## Why Request Bodies Exist

Clients send data to servers.

Examples:

* Registration
* Login
* Product creation
* Order placement

---

## Example

```json
{
  "name": "John",
  "email": "john@example.com"
}
```

---

## Express Access

```js
req.body
```

---

## JSON Middleware

```js
app.use(express.json());
```

---

## Checklist

* [ ] Parse JSON bodies.
* [ ] Validate request payloads.
* [ ] Reject invalid data.

---

## Veteran Understanding

* [ ] Validation is mandatory.
* [ ] Never trust client input.

---

# 7️⃣ JSON Responses

## Why JSON?

JSON is:

* Lightweight
* Human-readable
* Language-independent

---

## Example

```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "John"
  }
}
```

---

## Express Example

```js
res.json({
    success: true,
    data: user
});
```

---

## Checklist

* [ ] Return structured JSON.
* [ ] Standardize response formats.
* [ ] Return meaningful data.

---

## Veteran Insight

Consistency matters more than structure choice.

---

### Good API Response Pattern

```json
{
  "success": true,
  "data": {}
}
```

---

### Error Response Pattern

```json
{
  "success": false,
  "message": "User not found"
}
```

---

# 8️⃣ HTTP Status Codes

## Why Status Codes Matter

They communicate outcomes.

---

## Success Codes

### 200 OK

```text
Request Successful
```

---

### 201 Created

```text
Resource Created
```

---

### 204 No Content

```text
Successful Without Response Body
```

---

## Client Errors

### 400 Bad Request

```text
Invalid Input
```

---

### 401 Unauthorized

```text
Authentication Required
```

---

### 403 Forbidden

```text
Access Denied
```

---

### 404 Not Found

```text
Resource Not Found
```

---

## Server Errors

### 500 Internal Server Error

```text
Unexpected Failure
```

---

## Express Example

```js
res.status(404).json({
    success: false,
    message: "User not found"
});
```

---

## Checklist

* [ ] Use correct status codes.
* [ ] Return meaningful errors.
* [ ] Avoid always returning 200.

---

## Veteran Understanding

* [ ] Status codes form part of the API contract.
* [ ] Frontends rely heavily on proper status handling.

---

# 9️⃣ API Versioning

## Why Version APIs?

Changes break clients.

---

## Example

```text
/api/v1/users
/api/v2/users
```

---

## Benefits

* Backward compatibility
* Controlled migrations
* Safer deployments

---

## Checklist

* [ ] Understand versioning strategies.
* [ ] Design versioned routes.

---

## Veteran Insight

* [ ] Most production APIs eventually require versioning.

---

# 🔥 REST API Design Rules

## Follow These Rules

* [ ] Use nouns.
* [ ] Use proper HTTP methods.
* [ ] Use plural resource names.
* [ ] Return JSON.
* [ ] Use status codes correctly.
* [ ] Keep APIs predictable.
* [ ] Validate all input.

---

# 🔥 Core Concepts Master Checklist

## REST

* [ ] Explain REST architecture.
* [ ] Explain statelessness.

---

## Routing

* [ ] Design resource endpoints.
* [ ] Follow naming conventions.

---

## CRUD

* [ ] Build Create APIs.
* [ ] Build Read APIs.
* [ ] Build Update APIs.
* [ ] Build Delete APIs.

---

## Query Parameters

* [ ] Build filtering.
* [ ] Build sorting.
* [ ] Build pagination.

---

## JSON

* [ ] Return structured responses.
* [ ] Return consistent errors.

---

## Status Codes

* [ ] Use appropriate status codes.
* [ ] Explain code meanings.

---

# 🧪 Veteran-Level Exercises

## Beginner

* [ ] Users API.
* [ ] Products API.
* [ ] Notes API.

---

## Intermediate

* [ ] Pagination system.
* [ ] Filtering system.
* [ ] Search API.

---

## Advanced

* [ ] Full Blog API.
* [ ] E-Commerce API.
* [ ] API versioning implementation.

---

# ⚠️ Common Beginner Mistakes

* [ ] Using verbs in URLs.
* [ ] Returning 200 for every request.
* [ ] Ignoring validation.
* [ ] Inconsistent response structures.
* [ ] Mixing route and business logic.
* [ ] Using query strings incorrectly.

---

# 🏆 Veteran Thinking Questions

* [ ] Why is REST resource-oriented?
* [ ] Why are APIs stateless?
* [ ] Why does versioning become necessary?
* [ ] What makes an API intuitive?
* [ ] How do large companies maintain API compatibility?

---

# 📚 Learning Sequence

```text
REST Principles
      ↓
Resource Design
      ↓
CRUD Operations
      ↓
Express Routes
      ↓
Query Parameters
      ↓
Request Bodies
      ↓
JSON Responses
      ↓
Status Codes
      ↓
Versioning
      ↓
Production API Design
```

---

# ✅ Phase Completion Criteria

You have mastered this phase when you can:

* [ ] Explain REST architecture from memory.
* [ ] Design resource-oriented APIs.
* [ ] Build CRUD APIs using Express.
* [ ] Handle query parameters and request bodies.
* [ ] Return standardized JSON responses.
* [ ] Use HTTP status codes correctly.
* [ ] Design versioned APIs.

---

# 🚀 Next Phase

```text
Project Architecture
      ↓
MVC Pattern
      ↓
Controllers
      ↓
Services
      ↓
Repository Pattern
      ↓
Validation
      ↓
Error Handling
      ↓
Production Backend Development
```
