# 🚀 Node.js Mastery Roadmap

## Phase 7: Authentication and Authorization – Securing Your Application

---

# 🎯 Mission of This Phase

A backend application without security is merely a public database.

This phase teaches how modern applications answer two critical questions:

```text
Who are you?
```

and

```text
What are you allowed to do?
```

These two questions form the foundation of every secure system.

Examples:

* Banking Apps
* E-Commerce Platforms
* SaaS Products
* Social Networks
* Enterprise Systems

---

# 🧠 First Principles Understanding

## Authentication vs Authorization

Most beginners confuse them.

---

## Authentication

Authentication answers:

```text
Who are you?
```

Example:

```text
Email + Password
```

Result:

```text
User Identity Verified
```

---

## Authorization

Authorization answers:

```text
What can you do?
```

Example:

```text
User
```

Allowed:

```text
View Profile
```

Not Allowed:

```text
Delete All Users
```

---

## First Principle

```text
Authentication
       ↓
Identity
       ↓
Authorization
       ↓
Permissions
```

Authorization cannot happen without authentication.

---

# 🔐 Security Architecture Overview

```text
User
  ↓
Login
  ↓
Verify Credentials
  ↓
Generate JWT
  ↓
Store Token
  ↓
Protected Route
  ↓
Verify JWT
  ↓
Check Permissions
  ↓
Grant Access
```

---

# 1️⃣ Understanding Authentication

## What is Authentication?

Authentication proves a user is who they claim to be.

---

## Common Authentication Methods

### Username & Password

```text
Most Common
```

---

### OAuth

Examples:

* Google Login
* GitHub Login
* Facebook Login

---

### Multi-Factor Authentication (MFA)

```text
Password
    +
OTP
```

---

### Biometric Authentication

* Face ID
* Fingerprint

---

## Checklist

* [ ] Explain authentication.
* [ ] Explain identity verification.
* [ ] Compare authentication methods.

---

## Veteran Insight

Authentication is about trust.

The server must verify identity without blindly trusting the client.

---

# 2️⃣ Understanding Authorization

## What is Authorization?

Authorization determines what actions a user can perform.

---

## Example

User:

```json
{
  "id": 1,
  "role": "user"
}
```

Allowed:

```text
Read Profile
Update Profile
```

---

Not Allowed:

```text
Delete Users
Manage Payments
```

---

## Authorization Flow

```text
User Authenticated
        ↓
Permission Check
        ↓
Allow / Deny
```

---

## Checklist

* [ ] Explain authorization.
* [ ] Understand permission systems.
* [ ] Understand role systems.

---

## Veteran Understanding

Authentication answers:

```text
Who are you?
```

Authorization answers:

```text
What can you do?
```

---

# 3️⃣ Password Security Fundamentals

## Why Password Hashing Exists

Never store:

```json
{
  "password": "mypassword123"
}
```

This is catastrophic.

---

## First Principle

Passwords should never be recoverable.

---

## Hashing

Input:

```text
mypassword123
```

Output:

```text
$2b$10$...
```

One-way transformation.

---

## Benefits

* Cannot reverse hash
* Database breach becomes less damaging
* Protects user credentials

---

## Checklist

* [ ] Understand hashing.
* [ ] Understand salting.
* [ ] Understand one-way functions.

---

## Veteran Insight

A secure system never stores raw passwords.

---

# 4️⃣ Password Hashing with bcrypt

## Why bcrypt?

bcrypt provides:

* Salt generation
* Slow hashing
* Brute-force resistance

---

## Installation

```bash
npm install bcrypt
```

---

## Hash Password

```js
const bcrypt = require("bcrypt");

const hash =
await bcrypt.hash(
    password,
    10
);
```

---

## Compare Password

```js
const isValid =
await bcrypt.compare(
    password,
    user.password
);
```

---

## Checklist

* [ ] Hash passwords.
* [ ] Verify passwords.
* [ ] Understand salt rounds.

---

## Veteran Understanding

Hash speed is intentionally slow.

Slower hashes increase attacker cost.

---

# 5️⃣ Introduction to JWT

## What is JWT?

JWT stands for:

```text
JSON Web Token
```

JWT allows stateless authentication.

---

## Traditional Session Authentication

```text
User Login
      ↓
Server Creates Session
      ↓
Session Stored
      ↓
User Sends Session ID
```

Server must store sessions.

---

## JWT Authentication

```text
User Login
      ↓
Server Creates Token
      ↓
Client Stores Token
      ↓
Token Sent With Requests
```

Server remains stateless.

---

## JWT Structure

```text
Header
   .
Payload
   .
Signature
```

Example:

```text
xxxxx.yyyyy.zzzzz
```

---

## Checklist

* [ ] Understand JWT purpose.
* [ ] Understand token structure.
* [ ] Understand stateless authentication.

---

## Veteran Insight

JWT is not security.

JWT is a transport mechanism for identity.

Security depends on implementation.

---

# 6️⃣ Creating JWT Tokens

## Installation

```bash
npm install jsonwebtoken
```

---

## Generate Token

```js
const jwt =
require("jsonwebtoken");

const token =
jwt.sign(
    {
        id: user.id
    },
    process.env.JWT_SECRET,
    {
        expiresIn: "1d"
    }
);
```

---

## Verify Token

```js
jwt.verify(
    token,
    process.env.JWT_SECRET
);
```

---

## Token Flow

```text
Login
  ↓
Generate JWT
  ↓
Send To Client
  ↓
Store Token
  ↓
Protected Requests
```

---

## Checklist

* [ ] Generate JWT.
* [ ] Verify JWT.
* [ ] Add expiration.
* [ ] Use environment variables.

---

## Veteran Understanding

JWT secrets are critical infrastructure.

Never expose them.

---

# 7️⃣ Building Registration Endpoint

## Registration Flow

```text
User Registration
       ↓
Validate Input
       ↓
Check Existing User
       ↓
Hash Password
       ↓
Store User
       ↓
Return Success
```

---

## Validation Requirements

* Email required
* Password required
* Password strength rules

---

## Checklist

* [ ] Validate registration input.
* [ ] Hash passwords.
* [ ] Prevent duplicate users.
* [ ] Store user securely.

---

## Veteran Insight

Validation is part of security.

Never trust client data.

---

# 8️⃣ Building Login Endpoint

## Login Flow

```text
Email Submitted
      ↓
Find User
      ↓
Compare Password
      ↓
Generate JWT
      ↓
Return Token
```

---

## Example Response

```json
{
  "token": "jwt-token"
}
```

---

## Checklist

* [ ] Verify email.
* [ ] Verify password.
* [ ] Generate JWT.
* [ ] Return secure response.

---

## Veteran Understanding

Authentication failures should reveal minimal information.

Avoid:

```text
User Exists
Wrong Password
```

Instead:

```text
Invalid Credentials
```

---

# 9️⃣ Protecting Routes with Middleware

## Why Middleware?

Every protected route needs verification.

---

## Authentication Middleware

```text
Request
   ↓
Check Token
   ↓
Verify Token
   ↓
Allow Access
```

---

## Example Flow

```text
GET /profile
```

Without token:

```text
401 Unauthorized
```

With valid token:

```text
200 OK
```

---

## Checklist

* [ ] Create auth middleware.
* [ ] Verify tokens.
* [ ] Attach user data.
* [ ] Protect routes.

---

## Veteran Insight

Middleware centralizes security.

Never duplicate authentication logic.

---

# 🔟 Role-Based Access Control (RBAC)

## What is RBAC?

Permissions are assigned through roles.

---

## Example Roles

```text
Admin
Manager
User
Guest
```

---

## Example User

```json
{
  "id": 1,
  "role": "admin"
}
```

---

## Access Rules

| Action       | User | Admin |
| ------------ | ---- | ----- |
| View Profile | ✅    | ✅     |
| Edit Profile | ✅    | ✅     |
| Delete Users | ❌    | ✅     |
| Manage Roles | ❌    | ✅     |

---

## Authorization Middleware

```text
Request
    ↓
Authenticated?
    ↓
Role Check
    ↓
Allow / Deny
```

---

## Checklist

* [ ] Create role system.
* [ ] Create permission middleware.
* [ ] Restrict routes.

---

## Veteran Understanding

RBAC scales better than individual permissions.

---

# 🔥 JWT Best Practices

## Always

* [ ] Use HTTPS.
* [ ] Use strong secrets.
* [ ] Add expiration.
* [ ] Validate tokens.
* [ ] Store secrets in environment variables.

---

## Never

* [ ] Store passwords in plain text.
* [ ] Trust client roles.
* [ ] Expose JWT secrets.
* [ ] Use weak passwords.

---

# 🔥 Security Layers

```text
Input Validation
       ↓
Password Hashing
       ↓
Authentication
       ↓
JWT Verification
       ↓
Authorization
       ↓
Protected Resources
```

---

# 🔥 Core Concepts Master Checklist

## Authentication

* [ ] Explain authentication.
* [ ] Build login flow.
* [ ] Build registration flow.

---

## Authorization

* [ ] Explain authorization.
* [ ] Build role system.

---

## bcrypt

* [ ] Hash passwords.
* [ ] Verify passwords.

---

## JWT

* [ ] Generate tokens.
* [ ] Verify tokens.
* [ ] Protect routes.

---

## Middleware

* [ ] Create auth middleware.
* [ ] Create role middleware.

---

# 🧪 Veteran-Level Exercises

## Beginner

* [ ] User registration API.
* [ ] Login API.
* [ ] Protected profile endpoint.

---

## Intermediate

* [ ] JWT authentication system.
* [ ] Password reset flow.
* [ ] Refresh token system.

---

## Advanced

* [ ] Multi-role SaaS authentication.
* [ ] Enterprise RBAC system.
* [ ] OAuth integration (Google/GitHub).

---

# ⚠️ Common Beginner Mistakes

* [ ] Storing plain passwords.
* [ ] Hardcoding JWT secrets.
* [ ] Missing token expiration.
* [ ] Trusting user-provided roles.
* [ ] Returning sensitive data.
* [ ] Weak validation.

---

# 🏆 Veteran Thinking Questions

* [ ] Why is hashing one-way?
* [ ] Why are JWTs stateless?
* [ ] When should sessions be preferred over JWT?
* [ ] How do large companies implement RBAC?
* [ ] What happens if a JWT secret leaks?

---

# 📚 Learning Sequence

```text
Authentication Fundamentals
          ↓
Password Security
          ↓
bcrypt
          ↓
JWT
          ↓
Registration
          ↓
Login
          ↓
Auth Middleware
          ↓
Authorization
          ↓
RBAC
          ↓
Production Security
```

---

# ✅ Phase Completion Criteria

You have mastered this phase when you can:

* [ ] Explain authentication and authorization.
* [ ] Hash passwords securely.
* [ ] Build registration and login APIs.
* [ ] Generate and verify JWTs.
* [ ] Protect routes with middleware.
* [ ] Implement role-based access control.
* [ ] Design secure authentication systems.

---

# 🚀 Next Phase

```text
Error Handling
      ↓
Validation
      ↓
Logging
      ↓
API Security
      ↓
Rate Limiting
      ↓
Production Best Practices
      ↓
Enterprise Backend Architecture
```
