# 🚀 React Mastery Roadmap

## Phase 2: Components and Props – The Building Blocks of React

---

# 🎯 Mission of This Phase

In Phase 1, you learned:

```text
React = UI = f(State)
```

Now you'll learn how React applications are built.

React applications are not pages.

They are:

```text
Trees of Components
```

Every button, card, navbar, modal, sidebar, and dashboard is a component.

This phase teaches the most important React idea:

> Building complex UIs by combining small reusable pieces.

---

# 🧠 First Principles Understanding

## Why Components Exist

Imagine building a website without components.

```html
Navbar
Navbar
Navbar

Footer
Footer
Footer

Card
Card
Card
Card
```

Massive duplication.

---

## Component Solution

Create once:

```jsx
<Navbar />
```

Use everywhere.

---

## First Principle

A component is simply:

```text
A Function
That Returns UI
```

---

## Example

```jsx
function Welcome() {
    return (
        <h1>Hello</h1>
    );
}
```

---

## Input → Output

```text
Data
 ↓
Component
 ↓
UI
```

---

## Veteran Insight

React components are closer to mathematical functions than traditional UI elements.

---

# 🌳 Understanding Component Architecture

## Real Application

```text
App
│
├── Navbar
│
├── Sidebar
│
├── Dashboard
│   ├── StatsCard
│   ├── Chart
│   └── Table
│
└── Footer
```

---

## Component Tree

Applications are:

```text
Nested Components
```

---

## Benefits

* Reusability
* Maintainability
* Scalability
* Testability

---

## Checklist

* [ ] Explain component trees.
* [ ] Explain component composition.
* [ ] Explain UI decomposition.

---

## Veteran Understanding

Large applications are composed of hundreds or thousands of small components.

---

# 1️⃣ Functional Components

## What is a Functional Component?

A JavaScript function that returns JSX.

---

## Example

```jsx
function Welcome() {
    return (
        <h1>Hello React</h1>
    );
}
```

---

## Arrow Function Version

```jsx
const Welcome = () => {
    return (
        <h1>Hello React</h1>
    );
};
```

---

## Rendering

```jsx
<Welcome />
```

---

## Execution Flow

```text
React
 ↓
Calls Function
 ↓
Receives JSX
 ↓
Renders UI
```

---

## Checklist

* [ ] Create functional components.
* [ ] Render components.
* [ ] Return JSX.

---

## Veteran Insight

Modern React development primarily uses functional components.

---

# 2️⃣ Class Components (Legacy)

## Before React Hooks

React used class-based components.

---

## Example

```jsx
class Welcome
extends React.Component {
    render() {
        return (
            <h1>Hello</h1>
        );
    }
}
```

---

## Why Learn Them?

You will encounter them in:

* Legacy codebases
* Older tutorials
* Enterprise projects

---

## Comparison

| Feature         | Functional | Class |
| --------------- | ---------- | ----- |
| Simpler         | ✅          | ❌     |
| Modern          | ✅          | ❌     |
| Hooks Support   | ✅          | ❌     |
| Preferred Today | ✅          | ❌     |

---

## Checklist

* [ ] Recognize class components.
* [ ] Understand legacy React.

---

## Veteran Understanding

Know class components, but build with functional components.

---

# 3️⃣ Understanding Props

## What Are Props?

Props stands for:

```text
Properties
```

Props allow data to flow into components.

---

## First Principle

Components are functions.

Functions receive arguments.

Props are component arguments.

---

## Example

```jsx
function Welcome(props) {
    return (
        <h1>
            {props.name}
        </h1>
    );
}
```

---

## Usage

```jsx
<Welcome name="John" />
```

---

## Output

```html
<h1>John</h1>
```

---

## Flow

```text
Parent Component
        ↓
Props
        ↓
Child Component
```

---

## Checklist

* [ ] Pass props.
* [ ] Read props.
* [ ] Explain one-way data flow.

---

## Veteran Insight

Props make components reusable.

---

# 4️⃣ Props Destructuring

## Basic Approach

```jsx
function Welcome(props) {
    return (
        <h1>
            {props.name}
        </h1>
    );
}
```

---

## Preferred Approach

```jsx
function Welcome({ name }) {
    return (
        <h1>{name}</h1>
    );
}
```

---

## Multiple Props

```jsx
function User({
    name,
    age
}) {
    return (
        <p>
            {name} - {age}
        </p>
    );
}
```

---

## Usage

```jsx
<User
    name="John"
    age={25}
/>
```

---

## Checklist

* [ ] Destructure props.
* [ ] Use multiple props.

---

## Veteran Understanding

Destructuring improves readability and maintainability.

---

# 5️⃣ One-Way Data Flow

## React Principle

Data flows:

```text
Parent
 ↓
Child
```

Only.

---

## Example

```text
App
 ↓
Profile
 ↓
Avatar
```

---

## Not

```text
Child
 ↑
Parent
```

---

## Benefits

* Predictability
* Easier debugging
* Better architecture

---

## Checklist

* [ ] Explain one-way data flow.
* [ ] Explain parent-child relationships.

---

## Veteran Insight

Most React architecture decisions stem from one-way data flow.

---

# 6️⃣ Reusable Components

## Problem

Duplicate UI.

---

## Example

```jsx
<Card title="Product 1" />
<Card title="Product 2" />
<Card title="Product 3" />
```

---

## Single Component

```jsx
function Card({ title }) {
    return (
        <div>
            {title}
        </div>
    );
}
```

---

## Result

```text
One Component
Many Uses
```

---

## Checklist

* [ ] Create reusable components.
* [ ] Avoid duplication.

---

## Veteran Understanding

If you're copying JSX repeatedly, you probably need a component.

---

# 7️⃣ Understanding Children

## What is children?

Special prop automatically provided by React.

---

## Example

```jsx
<Card>
    Hello World
</Card>
```

---

## Component

```jsx
function Card({
    children
}) {
    return (
        <div>
            {children}
        </div>
    );
}
```

---

## Output

```html
<div>Hello World</div>
```

---

## Advanced Example

```jsx
<Card>
    <h1>Title</h1>
    <p>Description</p>
</Card>
```

---

## Checklist

* [ ] Use children.
* [ ] Build wrapper components.

---

## Veteran Insight

children enables highly flexible component composition.

---

# 8️⃣ Default Props

## Problem

Missing props.

---

## Example

```jsx
<Welcome />
```

---

## Solution

Provide defaults.

---

## Modern Approach

```jsx
function Welcome({
    name = "Guest"
}) {
    return (
        <h1>{name}</h1>
    );
}
```

---

## Result

```html
<h1>Guest</h1>
```

---

## Checklist

* [ ] Use default values.
* [ ] Handle missing props.

---

## Veteran Understanding

Components should fail gracefully.

---

# 9️⃣ Props vs State

## Props

Received from parent.

```text
External Data
```

---

## State

Managed internally.

```text
Internal Data
```

---

## Props Example

```jsx
<User
    name="John"
/>
```

---

## State Example

```jsx
const [count,
setCount] =
useState(0);
```

---

## Comparison

| Feature            | Props  | State         |
| ------------------ | ------ | ------------- |
| Owned By           | Parent | Component     |
| Mutable            | ❌      | ✅             |
| Purpose            | Input  | Internal Data |
| Triggers Re-render | ✅      | ✅             |

---

## Checklist

* [ ] Explain props.
* [ ] Explain state.
* [ ] Compare both.

---

## Veteran Insight

Props describe data.

State manages behavior.

---

# 🔟 Breaking Down UIs

## Example Page

```text
E-Commerce Homepage
```

---

## Decomposition

```text
App
│
├── Navbar
│
├── Hero
│
├── ProductGrid
│   ├── ProductCard
│   ├── ProductCard
│   └── ProductCard
│
└── Footer
```

---

## Rule

If a UI section can stand alone:

```text
Make It A Component
```

---

## Checklist

* [ ] Break UI into components.
* [ ] Identify reusable sections.

---

## Veteran Understanding

Good React architecture starts with good component decomposition.

---

# 🔥 Component Communication Model

```text
Parent Component
       ↓
Props
       ↓
Child Component
       ↓
Rendered UI
```

---

# 🔥 React Component Lifecycle (Simplified)

```text
Render Component
        ↓
Receive Props
        ↓
Generate JSX
        ↓
Render UI
```

---

# 🔥 Core Concepts Master Checklist

## Components

* [ ] Create functional components.
* [ ] Explain component trees.

---

## Props

* [ ] Pass props.
* [ ] Destructure props.
* [ ] Use default values.

---

## Children

* [ ] Use children prop.
* [ ] Create wrapper components.

---

## Reusability

* [ ] Identify repeated UI.
* [ ] Build reusable components.

---

## Architecture

* [ ] Break pages into components.
* [ ] Explain one-way data flow.

---

## State vs Props

* [ ] Compare both concepts.
* [ ] Identify when each should be used.

---

# 🧪 Veteran-Level Exercises

## Beginner

* [ ] Welcome component.
* [ ] User profile component.
* [ ] Product card component.

---

## Intermediate

* [ ] Blog card system.
* [ ] Dashboard widget system.
* [ ] Reusable modal component.

---

## Advanced

* [ ] Design system components.
* [ ] UI component library.
* [ ] Layout composition framework.

---

# ⚠️ Common Beginner Mistakes

* [ ] Creating huge components.
* [ ] Mutating props.
* [ ] Confusing props with state.
* [ ] Passing unnecessary props.
* [ ] Ignoring component reuse.
* [ ] Not using children effectively.

---

# 🏆 Veteran Thinking Questions

* [ ] Why are components considered functions?
* [ ] Why does React enforce one-way data flow?
* [ ] Why should props be immutable?
* [ ] What makes a component truly reusable?
* [ ] How would you break a complex dashboard into components?

---

# 📚 Learning Sequence

```text
Components
     ↓
Functional Components
     ↓
Class Components
     ↓
Props
     ↓
Props Destructuring
     ↓
One-Way Data Flow
     ↓
Children
     ↓
Default Props
     ↓
Reusable Components
     ↓
State vs Props
     ↓
Component Architecture
```

---

# ✅ Phase Completion Criteria

You have mastered this phase when you can:

* [ ] Build functional components confidently.
* [ ] Explain class components and their legacy role.
* [ ] Pass and destructure props.
* [ ] Use children effectively.
* [ ] Create reusable UI components.
* [ ] Explain one-way data flow.
* [ ] Distinguish between props and state.
* [ ] Break large UIs into maintainable component trees.

---

# 🚀 Next Phase

```text
State
  ↓
useState
  ↓
Event Handling
  ↓
Forms
  ↓
Controlled Components
  ↓
Conditional Rendering
  ↓
Lists & Keys
  ↓
Interactive React Applications
```
