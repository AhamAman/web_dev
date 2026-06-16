# Next.js Mastery Checklist

## Beginner → Veteran (First-Principles Roadmap)

> Core First Principle:
>
> React solves UI.
>
> Next.js solves application architecture.
>
> ```text
> React
> ↓
> Components
>
> Next.js
> ↓
> Routing
> Rendering
> Data Fetching
> Backend APIs
> Deployment
> SEO
> Performance
> ```
>
> Next.js exists because large applications need more than components.

---

# Phase 0: Foundation

## Understand Why Next.js Exists

### First Principle

React alone provides:

* [ ] Components
* [ ] State
* [ ] UI Logic

React does NOT provide:

* [ ] Routing
* [ ] SEO
* [ ] Server Rendering
* [ ] Backend APIs
* [ ] Full-stack Architecture

### Problems Next.js Solves

* [ ] SEO limitations
* [ ] Slow initial load
* [ ] Complex routing setup
* [ ] Backend integration
* [ ] Production architecture

### Milestone

* [ ] Explain why Next.js was created

---

# Phase 1: Understanding Modern Web Rendering

## Learn Rendering Strategies

### Client-Side Rendering (CSR)

```text
Browser
↓
Downloads JS
↓
React Renders
↓
UI Appears
```

### Server-Side Rendering (SSR)

```text
Request
↓
Server Generates HTML
↓
Browser Receives HTML
↓
Hydration
```

### Static Site Generation (SSG)

```text
Build Time
↓
Generate HTML
↓
Serve Instantly
```

### Incremental Static Regeneration (ISR)

```text
Static Page
↓
Background Updates
↓
Fresh Content
```

### Milestone

* [ ] Explain CSR vs SSR vs SSG vs ISR

---

# Phase 2: Setting Up Next.js

## Create Project

### Learn

* [ ] Create Next.js app

```bash
npx create-next-app@latest
```

* [ ] Project structure
* [ ] Development server

### Explore

```text
app/
public/
components/
lib/
```

### Milestone

* [ ] Create Next.js projects from memory

---

# Phase 3: Understanding App Router

## Learn Modern Next.js Architecture

### First Principle

Folders become routes.

Example:

```text
app/
├── page.tsx
├── about/
│   └── page.tsx
```

Produces:

```text
/
about
```

### Learn

* [ ] app directory
* [ ] page.tsx
* [ ] layout.tsx
* [ ] loading.tsx
* [ ] error.tsx

### Milestone

* [ ] Explain file-based routing

---

# Phase 4: File-Based Routing

## Understand Routing

### First Principle

Filesystem = URL Structure

```text
app/
├── page.tsx
├── products/
│   └── page.tsx
```

Creates:

```text
/
/products
```

### Practice

* [ ] Home page
* [ ] About page
* [ ] Contact page
* [ ] Dashboard page

### Milestone

* [ ] Create routes without React Router

---

# Phase 5: Dynamic Routing

## Understand Dynamic URLs

### First Principle

One page can serve many resources.

Example:

```text
/products/1
/products/2
/products/3
```

### Learn Dynamic Segments

```text
app/
└── products/
    └── [id]/
        page.tsx
```

### Learn

* [ ] params
* [ ] dynamic segments
* [ ] catch-all routes

### Practice

* [ ] Product detail page
* [ ] User profile page
* [ ] Blog posts

### Milestone

* [ ] Build dynamic applications

---

# Phase 6: Layout System

## Understand Layouts

### First Principle

Pages share common UI.

```text
Navbar
Sidebar
Footer
```

Should not repeat.

### Learn

```text
layout.tsx
```

### Practice

* [ ] Root layout
* [ ] Dashboard layout
* [ ] Admin layout

### Milestone

* [ ] Create reusable layouts

---

# Phase 7: Navigation

## Learn Navigation System

### Learn

* [ ] Link component
* [ ] useRouter
* [ ] Programmatic navigation

### Practice

* [ ] Navigation menus
* [ ] Dashboard navigation
* [ ] Redirect flows

### Milestone

* [ ] Navigate applications without page reloads

---

# Phase 8: Server Components

## Understand Server Components

### First Principle

Not all components need JavaScript.

Server Components:

```text
Run On Server
↓
Send HTML
```

### Benefits

* [ ] Faster load
* [ ] Smaller bundles
* [ ] Better SEO

### Learn

* [ ] Default Server Components
* [ ] Server rendering model

### Milestone

* [ ] Explain why Server Components exist

---

# Phase 9: Client Components

## Understand Interactive Components

### First Principle

Interactivity requires JavaScript.

### Learn

```jsx
"use client";
```

### Practice

* [ ] Counters
* [ ] Forms
* [ ] Search inputs

### Learn

* [ ] Server vs Client Components

### Milestone

* [ ] Choose correct component type

---

# Phase 10: Data Fetching

## Understand Data Sources

### First Principle

Applications exist to display data.

### Learn

```jsx
fetch()
```

inside Server Components.

### Practice

* [ ] Fetch products
* [ ] Fetch users
* [ ] Fetch blog posts

### Learn

* [ ] Async Server Components
* [ ] Fetch caching

### Milestone

* [ ] Build data-driven applications

---

# Phase 11: Server-Side Rendering (SSR)

## Learn SSR

### First Principle

Generate HTML per request.

```text
Request
↓
Server
↓
HTML
↓
Browser
```

### Benefits

* [ ] SEO
* [ ] Personalization
* [ ] Fresh data

### Practice

* [ ] User dashboard
* [ ] News page
* [ ] Analytics page

### Milestone

* [ ] Know when SSR is appropriate

---

# Phase 12: Static Site Generation (SSG)

## Learn SSG

### First Principle

Generate pages during build.

```text
Build
↓
HTML Generated
↓
Serve Instantly
```

### Practice

* [ ] Blog
* [ ] Documentation site
* [ ] Marketing site

### Learn

* [ ] generateStaticParams

### Milestone

* [ ] Build static websites

---

# Phase 13: Incremental Static Regeneration (ISR)

## Understand Hybrid Rendering

### First Principle

Static pages can become stale.

ISR solves:

```text
Static
↓
Background Refresh
↓
Updated Content
```

### Learn

* [ ] revalidate
* [ ] cache strategies

### Practice

* [ ] Product catalog
* [ ] News site

### Milestone

* [ ] Build scalable content systems

---

# Phase 14: API Routes

## Understand Backend Functionality

### First Principle

Applications often need APIs.

Next.js provides backend endpoints.

### Learn

```text
app/api/
```

### Practice

* [ ] User API
* [ ] Contact Form API
* [ ] Product API

### Build

* [ ] CRUD endpoints

### Milestone

* [ ] Build full-stack applications

---

# Phase 15: Authentication Architecture

## Learn Authentication

### Practice

* [ ] Login
* [ ] Logout
* [ ] Protected routes
* [ ] Session management

### Learn

* [ ] Cookies
* [ ] JWT
* [ ] Auth providers

### Milestone

* [ ] Build authentication systems

---

# Phase 16: Environment Variables

## Learn Configuration

### Practice

```env
DATABASE_URL=
API_KEY=
```

### Learn

* [ ] Server variables
* [ ] Public variables
* [ ] Deployment configuration

### Milestone

* [ ] Manage environments safely

---

# Phase 17: Performance Optimization

## Learn Next.js Performance

### Features

* [ ] Image Optimization
* [ ] Font Optimization
* [ ] Code Splitting
* [ ] Streaming

### Components

* [ ] Image
* [ ] Script

### Milestone

* [ ] Optimize production applications

---

# Phase 18: Deployment

## Learn Production Delivery

### Practice

* [ ] Vercel deployment
* [ ] Environment setup
* [ ] Production builds

### Learn

```bash
npm run build
```

### Milestone

* [ ] Deploy Next.js applications confidently

---

# Phase 19: Application Architecture

## Build Real Systems

### Projects

* [ ] Blog Platform
* [ ] E-Commerce Store
* [ ] SaaS Dashboard
* [ ] Learning Platform

### Architecture

* [ ] Features
* [ ] Services
* [ ] Components
* [ ] API layer

### Milestone

* [ ] Design scalable Next.js applications

---

# Phase 20: Next.js Internals

## Understand How Next.js Works

### Learn

* [ ] Routing engine
* [ ] Rendering pipeline
* [ ] Hydration
* [ ] Server Components architecture

### Understand

```text
Request
↓
Route Match
↓
Server Render
↓
Hydration
↓
Interactive UI
```

### Milestone

* [ ] Explain Next.js internals

---

# Phase 21: Veteran-Level Understanding

## First-Principles Thinking

Stop thinking:

```text
Should I use SSR?
```

Think:

```text
What problem am I solving?
↓
SEO?
↓
Performance?
↓
Fresh data?
↓
Static content?
↓
Personalized content?
```

Then choose:

```text
SSG
SSR
ISR
CSR
Server Components
```

---

## Veteran Questions

* [ ] Why does Next.js exist?
* [ ] Why is file-based routing powerful?
* [ ] When should SSR be used?
* [ ] When should SSG be used?
* [ ] When should ISR be used?
* [ ] Why are Server Components important?
* [ ] How do API Routes work?
* [ ] How does hydration work?
* [ ] How does Next.js improve React performance?

---

# Final Veteran Checklist

## Core Concepts

* [ ] Next.js
* [ ] File-Based Routing
* [ ] Layouts
* [ ] Dynamic Routes

## Rendering

* [ ] CSR
* [ ] SSR
* [ ] SSG
* [ ] ISR

## Full-Stack Features

* [ ] API Routes
* [ ] Authentication
* [ ] Environment Variables

## Advanced Skills

* [ ] Server Components
* [ ] Client Components
* [ ] Data Fetching
* [ ] Performance Optimization

## Architecture

* [ ] Scalable Structure
* [ ] Feature-Based Design
* [ ] Deployment

## Internal Understanding

* [ ] Hydration
* [ ] Rendering Pipeline
* [ ] Routing Engine

## Veteran Outcome

* [ ] Can build full-stack Next.js applications
* [ ] Can choose correct rendering strategies
* [ ] Can create API routes and backend logic
* [ ] Can optimize performance using Server Components
* [ ] Can deploy production applications
* [ ] Can architect enterprise-grade Next.js systems
* [ ] Can explain Next.js from first principles
