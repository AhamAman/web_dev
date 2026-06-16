# React Lifecycle Methods & useEffect Mastery Checklist

## Beginner → Veteran (First-Principles Roadmap)

> Core First Principle:
>
> A React component has a life:
>
> **Mount → Update → Unmount**
>
> Everything in React lifecycles and `useEffect` exists to manage these three phases.

---

# Phase 0: Foundation

## Understand Why Lifecycles Exist

* [ ] Explain why UI is dynamic
* [ ] Explain why React needs lifecycle management
* [ ] Define a React component lifecycle
* [ ] Explain Mounting, Updating, and Unmounting
* [ ] Explain lifecycle using the "birth → life → death" analogy
* [ ] Explain the difference between rendering and side effects

### Milestone

* [ ] Explain React lifecycle without looking at notes

---

# Phase 1: Mounting Fundamentals

## Learn What Mounting Means

* [ ] Define Mounting
* [ ] Identify when a component mounts
* [ ] Understand Virtual DOM creation during mounting
* [ ] Understand DOM insertion during mounting

## Class Component Lifecycle

* [ ] Learn `constructor()`
* [ ] Learn `render()`
* [ ] Learn `componentDidMount()`

## Practice

* [ ] Log a message when component mounts
* [ ] Fetch data in `componentDidMount`
* [ ] Start a timer in `componentDidMount`
* [ ] Add event listeners in `componentDidMount`

### Milestone

* [ ] Explain execution order:

```text
constructor()
↓
render()
↓
componentDidMount()
```

---

# Phase 2: Updating Fundamentals

## Learn What Updating Means

* [ ] Define Updating
* [ ] Understand state-triggered updates
* [ ] Understand prop-triggered updates
* [ ] Understand parent-triggered updates

## Class Lifecycle Updates

* [ ] Learn `componentDidUpdate()`
* [ ] Understand previous props
* [ ] Understand previous state

## Practice

* [ ] Detect prop changes
* [ ] Detect state changes
* [ ] Log updates correctly
* [ ] Trigger API request after prop change

## Avoid Problems

* [ ] Understand infinite render loops
* [ ] Learn safe update patterns
* [ ] Compare previous and current values before updating

### Milestone

* [ ] Explain:

```text
State Change
↓
render()
↓
componentDidUpdate()
```

---

# Phase 3: Unmounting Fundamentals

## Learn What Unmounting Means

* [ ] Define Unmounting
* [ ] Understand when React removes components
* [ ] Identify common unmount scenarios

## Class Lifecycle Cleanup

* [ ] Learn `componentWillUnmount()`
* [ ] Understand cleanup responsibilities

## Practice

* [ ] Remove event listeners
* [ ] Clear timers
* [ ] Close WebSocket connections
* [ ] Cancel subscriptions

## Memory Management

* [ ] Understand memory leaks
* [ ] Understand orphaned timers
* [ ] Understand lingering listeners

### Milestone

* [ ] Explain why cleanup is necessary

---

# Phase 4: Master Class Component Lifecycles

## Lifecycle Flow

* [ ] Memorize mounting lifecycle
* [ ] Memorize updating lifecycle
* [ ] Memorize unmount lifecycle

## Draw Lifecycle Diagram From Memory

* [ ] Draw lifecycle without references

```text
Mount
├─ constructor
├─ render
└─ componentDidMount

Update
├─ render
└─ componentDidUpdate

Unmount
└─ componentWillUnmount
```

### Milestone

* [ ] Teach lifecycle methods to another developer

---

# Phase 5: Introduction to Hooks

## Understand Why Hooks Exist

* [ ] Learn problems with class components
* [ ] Learn why React introduced hooks
* [ ] Understand function component architecture

## Learn useEffect Basics

* [ ] Define `useEffect`
* [ ] Understand effect execution timing
* [ ] Understand side effects

### Milestone

* [ ] Explain why `useEffect` replaced multiple lifecycle methods

---

# Phase 6: Side Effects Mastery

## Understand Side Effects

### Learn What Counts as Side Effects

* [ ] API requests
* [ ] Logging
* [ ] Timers
* [ ] Local storage
* [ ] DOM updates
* [ ] Event listeners
* [ ] WebSocket connections

### Learn What Is NOT a Side Effect

* [ ] Rendering JSX
* [ ] Computing values
* [ ] Returning UI

### Milestone

* [ ] Categorize any operation as side effect or non-side effect

---

# Phase 7: useEffect Lifecycle Mapping

## Mount Equivalent

* [ ] Use empty dependency array

```jsx
useEffect(() => {}, []);
```

* [ ] Explain why it runs once

## Update Equivalent

* [ ] Use dependency array

```jsx
useEffect(() => {}, [count]);
```

* [ ] Explain why it runs on dependency changes

## Every Render Equivalent

* [ ] Use effect without dependency array

```jsx
useEffect(() => {});
```

* [ ] Explain why it runs after every render

### Milestone

* [ ] Map all class lifecycle methods to `useEffect`

---

# Phase 8: Dependency Array Mastery

## Learn Dependency Tracking

* [ ] Understand dependency comparison
* [ ] Understand reference equality
* [ ] Understand primitive comparison

## Practice

* [ ] Track state changes
* [ ] Track prop changes
* [ ] Track multiple dependencies

```jsx
useEffect(() => {}, [count, user, theme]);
```

## Advanced Understanding

* [ ] Explain dependency graph thinking
* [ ] Explain effect re-execution logic

### Milestone

* [ ] Predict exactly when an effect will run

---

# Phase 9: Cleanup Function Mastery

## Learn Cleanup Mechanics

* [ ] Understand cleanup execution
* [ ] Understand cleanup timing

```jsx
useEffect(() => {
  return () => {};
}, []);
```

## Practice

* [ ] Clear intervals
* [ ] Remove listeners
* [ ] Close sockets
* [ ] Disconnect observers

### Milestone

* [ ] Explain how cleanup replaces `componentWillUnmount`

---

# Phase 10: Real-World Lifecycle Applications

## Data Fetching

* [ ] Fetch data on mount
* [ ] Refetch when dependencies change
* [ ] Handle loading state
* [ ] Handle error state

## DOM Manipulation

* [ ] Update page title
* [ ] Focus input fields
* [ ] Measure DOM elements

## Timers

* [ ] Create interval timer
* [ ] Create countdown timer
* [ ] Properly clean up timer

## Event Handling

* [ ] Window resize listener
* [ ] Keyboard listener
* [ ] Scroll listener

### Milestone

* [ ] Build a complete dashboard using lifecycle concepts

---

# Phase 11: Common Mistakes

## Infinite Loops

* [ ] Recognize infinite loops
* [ ] Prevent infinite loops

## Missing Dependencies

* [ ] Understand stale closures
* [ ] Understand stale state bugs

## Unnecessary Effects

* [ ] Remove derived-state effects
* [ ] Calculate values directly during render

## Missing Cleanup

* [ ] Detect memory leaks
* [ ] Detect resource leaks

### Milestone

* [ ] Debug lifecycle issues confidently

---

# Phase 12: Advanced useEffect

## React Internals Awareness

* [ ] Understand render phase
* [ ] Understand commit phase
* [ ] Understand effect phase

## Advanced Dependency Concepts

* [ ] Function dependencies
* [ ] Object dependencies
* [ ] Array dependencies

## Optimization

* [ ] Learn `useCallback`
* [ ] Learn `useMemo`
* [ ] Prevent unnecessary effects

### Milestone

* [ ] Explain effect execution in terms of React rendering

---

# Phase 13: Expert-Level Understanding

## Learn Custom Hooks

* [ ] Create `useFetch`
* [ ] Create `useTimer`
* [ ] Create `useLocalStorage`
* [ ] Create `useWindowSize`

## Lifecycle Abstraction

* [ ] Encapsulate side effects
* [ ] Share effect logic
* [ ] Build reusable hooks

### Milestone

* [ ] Build custom hooks without tutorials

---

# Phase 14: Veteran-Level Understanding

## React Architecture Knowledge

* [ ] Understand reconciliation
* [ ] Understand Fiber architecture
* [ ] Understand concurrent rendering
* [ ] Understand Strict Mode effect behavior
* [ ] Understand effect scheduling

## First-Principles Thinking

* [ ] Stop thinking in lifecycle methods
* [ ] Think in synchronization problems
* [ ] Think in side-effect systems
* [ ] Think in state transitions

### Veteran Questions You Should Answer

* [ ] Why does `useEffect` exist?
* [ ] Why are effects executed after rendering?
* [ ] Why are dependencies required?
* [ ] Why is cleanup necessary?
* [ ] When should effects NOT be used?
* [ ] How does React schedule effects internally?

---

# Final Veteran Checklist

## Knowledge

* [ ] Mounting
* [ ] Updating
* [ ] Unmounting
* [ ] Lifecycle methods
* [ ] Side effects
* [ ] Dependency arrays
* [ ] Cleanup functions
* [ ] React rendering cycle

## Practical Skills

* [ ] Data fetching
* [ ] Event listeners
* [ ] Timers
* [ ] DOM manipulation
* [ ] Cleanup management
* [ ] Custom hooks

## Advanced Skills

* [ ] Performance optimization
* [ ] Effect debugging
* [ ] Hook architecture
* [ ] React internals understanding

## Veteran Outcome

* [ ] Can explain React lifecycle from first principles
* [ ] Can design side-effect systems confidently
* [ ] Can debug complex effect bugs
* [ ] Can create reusable custom hooks
* [ ] Can teach React lifecycle concepts to others
* [ ] Can reason about React behavior without memorizing APIs
