# React Context API Mastery Checklist

## Beginner → Veteran (First-Principles Roadmap)

> Core First Principle:
>
> Data should be available where it is needed.
>
> When many components need the same data, passing props through every level becomes inefficient.
>
> ```text
> Shared Data
> ↓
> Global Access
> ↓
> Consistent UI
> ```
>
> Context API exists to solve the problem of **prop drilling** and provide **global state access**.

---

# Phase 0: Foundation

## Understand Why Context Exists

### First Principle

Every component can have its own state.

```text
Component A
Own State

Component B
Own State

Component C
Own State
```

Problem:

Sometimes many components need the same data.

Examples:

* Authentication user
* Theme settings
* Language preferences
* Shopping cart
* Notifications

---

## Understand Shared State

### Without Shared State

```text
App
↓
Header
↓
Navbar
↓
Menu
↓
Profile
```

Pass user data through every level.

This is called:

* [ ] Prop Drilling

---

### With Shared State

```text
Context
↓
Any Component
```

### Milestone

* [ ] Explain why prop drilling becomes a problem

---

# Phase 1: Prop Drilling Fundamentals

## Understand Prop Drilling

### Learn Data Flow

```text
Parent
↓
Child
↓
GrandChild
↓
GreatGrandChild
```

### Practice

* [ ] Pass user data through 3 levels
* [ ] Pass theme data through 4 levels
* [ ] Pass cart data through 5 levels

### Identify Problems

* [ ] Repeated props
* [ ] Unnecessary coupling
* [ ] Difficult maintenance
* [ ] Poor scalability

### Milestone

* [ ] Identify when prop drilling becomes problematic

---

# Phase 2: Introduction to Context API

## Learn Context Fundamentals

### What Context Provides

```text
Provider
↓
Stores Value
↓
Consumer Reads Value
```

### Core Concepts

* [ ] Context
* [ ] Provider
* [ ] Consumer
* [ ] Shared State
* [ ] Global Access

### Understand Context Flow

```text
Provider
↓
React Tree
↓
Consumer
```

### Milestone

* [ ] Explain Context without using React code

---

# Phase 3: Creating Context

## Learn Context Creation

### Create Context

```jsx
const UserContext =
  createContext();
```

* [ ] Create UserContext
* [ ] Create ThemeContext
* [ ] Create CartContext

### Understand Purpose

* [ ] Context definition
* [ ] Context identity
* [ ] Default values

### Milestone

* [ ] Create contexts independently

---

# Phase 4: Providing Context

## Learn Providers

### First Principle

Data must originate somewhere.

Provider acts as the source.

```jsx
<UserContext.Provider value={user}>
```

### Practice

* [ ] Wrap App with Provider
* [ ] Provide authentication data
* [ ] Provide theme settings

### Understand Scope

```text
Provider
├── Child A
├── Child B
└── Child C
```

All children can access context.

### Milestone

* [ ] Explain Provider scope

---

# Phase 5: Consuming Context

## Learn Context Consumption

### Using useContext

```jsx
const user =
  useContext(UserContext);
```

### Practice

* [ ] Read user data
* [ ] Read theme data
* [ ] Read cart data

### Understand Consumption

```text
Provider
↓
Stores Data
↓
Consumer Reads Data
```

### Milestone

* [ ] Access context anywhere within provider tree

---

# Phase 6: Updating Global State

## Understand Global Updates

### First Principle

Global state should be readable and writable.

### Provide State + Actions

```jsx
<UserContext.Provider
  value={{
    user,
    setUser
  }}
>
```

### Practice

* [ ] Login user
* [ ] Logout user
* [ ] Update profile
* [ ] Change theme

### Milestone

* [ ] Update global state from any component

---

# Phase 7: Authentication Context

## Build Real Authentication

### Store

* [ ] User
* [ ] Login state
* [ ] Logout actions

### Features

* [ ] Login
* [ ] Logout
* [ ] Protected UI
* [ ] User display

### Practice Project

```text
AuthContext
├── Login
├── Logout
├── User Profile
└── Protected Routes
```

### Milestone

* [ ] Build authentication using Context

---

# Phase 8: Theme Management Context

## Build Theme System

### State

* [ ] Light Theme
* [ ] Dark Theme

### Actions

* [ ] Toggle theme
* [ ] Persist theme

### Practice Project

```text
ThemeContext
├── Navbar
├── Sidebar
├── Footer
└── Dashboard
```

### Milestone

* [ ] Build complete theme switching system

---

# Phase 9: Shopping Cart Context

## Build Shared Business State

### Store

* [ ] Products
* [ ] Cart Items
* [ ] Quantities
* [ ] Totals

### Actions

* [ ] Add Item
* [ ] Remove Item
* [ ] Update Quantity
* [ ] Clear Cart

### Milestone

* [ ] Build cart state using Context

---

# Phase 10: Context + useReducer

## Understand Scaling Problems

### First Principle

As state grows:

```jsx
setUser()
setCart()
setTheme()
setOrders()
```

becomes difficult.

---

## Learn Reducer Pattern

```text
Action
↓
Reducer
↓
New State
```

### Practice

* [ ] Combine Context + useReducer
* [ ] Centralize updates
* [ ] Manage complex state

### Milestone

* [ ] Build Redux-like architecture with Context

---

# Phase 11: Multiple Contexts

## Understand Context Separation

### Bad

```text
MegaContext
Everything
```

### Good

```text
AuthContext
ThemeContext
CartContext
LanguageContext
```

### Practice

* [ ] Split responsibilities
* [ ] Create focused contexts

### Milestone

* [ ] Design scalable context architecture

---

# Phase 12: Context Performance

## Understand Re-rendering

### First Principle

Context updates trigger consumer re-renders.

```text
Provider Update
↓
Consumers Re-render
```

### Learn Optimization

* [ ] Split contexts
* [ ] Memoize values
* [ ] Reduce unnecessary updates

### Practice

```jsx
useMemo()
```

### Milestone

* [ ] Prevent unnecessary re-renders

---

# Phase 13: Common Context Mistakes

## Architecture Mistakes

* [ ] Using Context for local state
* [ ] Creating giant contexts
* [ ] Overusing global state

## Performance Mistakes

* [ ] Frequent updates in Context
* [ ] Unmemoized provider values

## Design Mistakes

* [ ] Poor context boundaries
* [ ] Business logic inside components

### Milestone

* [ ] Identify Context anti-patterns

---

# Phase 14: Context Best Practices

## State Design

* [ ] Keep context focused
* [ ] Separate concerns
* [ ] Store only shared data

## Provider Design

* [ ] Wrap only necessary components
* [ ] Avoid global provider overload

## Consumer Design

* [ ] Create custom hooks
* [ ] Encapsulate access logic

Example:

```jsx
function useAuth() {
  return useContext(AuthContext);
}
```

### Milestone

* [ ] Write production-grade Context architecture

---

# Phase 15: Advanced Context Patterns

## Build Enterprise Systems

### Projects

* [ ] Authentication Framework
* [ ] Theme Framework
* [ ] Shopping Cart System
* [ ] Notification System
* [ ] Feature Flags System

### Advanced Patterns

* [ ] Context Composition
* [ ] Context Modules
* [ ] Provider Factories

### Milestone

* [ ] Design reusable Context libraries

---

# Phase 16: React Internals

## Understand Context Internals

### Learn

* [ ] How Provider stores values
* [ ] How Consumers subscribe
* [ ] How React detects updates
* [ ] Context propagation process

### Rendering

```text
Provider Update
↓
React Tree Traversal
↓
Consumer Re-render
```

### Milestone

* [ ] Explain Context update flow internally

---

# Phase 17: Context vs Other Solutions

## Learn State Management Choices

### Context API

Best For:

* [ ] Theme
* [ ] Authentication
* [ ] Language
* [ ] User Preferences

### Not Ideal For

* [ ] High-frequency updates
* [ ] Complex business workflows
* [ ] Massive enterprise state

### Compare

* [ ] Context API
* [ ] Redux
* [ ] Zustand
* [ ] Jotai
* [ ] Recoil

### Milestone

* [ ] Choose correct state management solution

---

# Phase 18: Veteran-Level Understanding

## First-Principles Thinking

Stop thinking:

```text
I need Context.
```

Think:

```text
Who owns this data?
↓
Who needs this data?
↓
How often does it change?
↓
How many components consume it?
↓
Should it be local or global?
```

---

## Veteran Questions

* [ ] Why does Context exist?
* [ ] What problem does prop drilling create?
* [ ] When should Context NOT be used?
* [ ] Why can Context cause re-render issues?
* [ ] Why combine Context with useReducer?
* [ ] When should Redux or Zustand replace Context?
* [ ] How does Context work internally?
* [ ] How should large applications organize Context?

---

# Final Veteran Checklist

## Core Concepts

* [ ] Context API
* [ ] Provider
* [ ] Consumer
* [ ] useContext
* [ ] Global State
* [ ] Prop Drilling

## Practical Skills

* [ ] Authentication Context
* [ ] Theme Context
* [ ] Cart Context
* [ ] Notification Context

## Advanced Skills

* [ ] Context + useReducer
* [ ] Context Composition
* [ ] Performance Optimization
* [ ] Custom Context Hooks

## Internal Understanding

* [ ] Context Propagation
* [ ] Consumer Subscription
* [ ] Re-render Mechanics

## Veteran Outcome

* [ ] Can eliminate prop drilling effectively
* [ ] Can design global state architecture
* [ ] Can build authentication systems
* [ ] Can build scalable Context solutions
* [ ] Can optimize Context performance
* [ ] Can explain Context internals
* [ ] Can choose between Context, Redux, and Zustand intelligently
