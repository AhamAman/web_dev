# 4. Asynchronous JavaScript – Handling Time-Sensitive Code ✅ Checklist

> Goal: Understand how JavaScript handles operations that take time without blocking the application.

---

# Phase 1: Foundations

## 1. Introduction to Asynchronous JavaScript

### Core Concepts

* [ ] Understand synchronous execution
* [ ] Understand asynchronous execution
* [ ] Learn why asynchronous programming exists
* [ ] Understand blocking vs non-blocking operations
* [ ] Understand real-world asynchronous tasks

### First-Principles Understanding

* [ ] Understand that JavaScript runs on a single thread
* [ ] Understand why long-running tasks freeze applications
* [ ] Understand how asynchronous programming prevents blocking
* [ ] Understand that JavaScript delegates work to browser APIs

### Real-World Examples

* [ ] Fetching API data
* [ ] Uploading files
* [ ] Downloading files
* [ ] Waiting for user interaction
* [ ] Running timers
* [ ] Reading databases

### Practice

* [ ] Explain synchronous execution in your own words
* [ ] Explain asynchronous execution in your own words
* [ ] Identify 5 asynchronous operations from daily web usage

---

# Phase 2: JavaScript Runtime Fundamentals

## 2. Understanding the Call Stack

### Concepts

* [ ] Understand what the Call Stack is
* [ ] Understand function execution
* [ ] Understand LIFO (Last In First Out)

### Practice

* [ ] Trace nested function execution
* [ ] Draw Call Stack diagrams
* [ ] Predict stack behavior

---

## 3. Understanding Web APIs

### Concepts

* [ ] Understand what Web APIs are
* [ ] Understand browser-provided functionality
* [ ] Understand delegation of asynchronous tasks

### Examples

* [ ] setTimeout
* [ ] setInterval
* [ ] Fetch API
* [ ] DOM Events
* [ ] Geolocation API

### Practice

* [ ] Identify which tasks run inside Web APIs
* [ ] Explain the role of Web APIs

---

## 4. Understanding the Event Loop

### Concepts

* [ ] Understand why the Event Loop exists
* [ ] Understand Callback Queue
* [ ] Understand task scheduling
* [ ] Understand Event Loop responsibilities

### First-Principles Understanding

* [ ] Understand Call Stack
* [ ] Understand Web APIs
* [ ] Understand Callback Queue
* [ ] Understand Event Loop interaction

### Practice

* [ ] Predict output order of asynchronous code
* [ ] Explain Event Loop flow step-by-step

### Mastery Test

Predict the output:

```javascript
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

console.log("C");
```

* [ ] Explain why output is:

```text
A
C
B
```

---

# Phase 3: Timers

## 5. setTimeout()

### Concepts

* [ ] Understand delayed execution
* [ ] Learn syntax
* [ ] Execute code after a delay

### Example

```javascript
setTimeout(() => {
  console.log("Hello");
}, 2000);
```

### Practice

* [ ] Show message after 3 seconds
* [ ] Delay function execution
* [ ] Build countdown logic

---

## 6. clearTimeout()

### Concepts

* [ ] Understand timeout cancellation
* [ ] Store timeout IDs
* [ ] Cancel scheduled tasks

### Practice

* [ ] Create timeout
* [ ] Cancel timeout before execution

---

## 7. setInterval()

### Concepts

* [ ] Understand repeated execution
* [ ] Learn interval scheduling
* [ ] Understand use cases

### Example

```javascript
setInterval(() => {
  console.log("Running...");
}, 1000);
```

### Practice

* [ ] Create a digital clock
* [ ] Print numbers every second
* [ ] Build a stopwatch

---

## 8. clearInterval()

### Concepts

* [ ] Stop repeated execution
* [ ] Manage interval IDs

### Practice

* [ ] Start interval
* [ ] Stop interval
* [ ] Create self-stopping countdown

---

# Phase 4: Callbacks

## 9. Understanding Callbacks

### Concepts

* [ ] Understand callback functions
* [ ] Pass functions as arguments
* [ ] Execute callback functions

### Example

```javascript
function greet(name, callback) {
  console.log(`Hello ${name}`);
  callback();
}
```

### Practice

* [ ] Create greeting callback
* [ ] Create calculator callback
* [ ] Pass multiple callbacks

---

## 10. Callback Hell

### Concepts

* [ ] Understand nested callbacks
* [ ] Understand readability issues
* [ ] Understand maintenance problems

### Example

```javascript
loginUser(() => {
  getProfile(() => {
    getPosts(() => {
      getComments();
    });
  });
});
```

### Practice

* [ ] Identify callback hell
* [ ] Refactor nested callbacks

---

# Phase 5: Promises

## 11. Introduction to Promises

### Concepts

* [ ] Understand why Promises were created
* [ ] Understand Promise lifecycle
* [ ] Understand asynchronous flow control

### Promise States

* [ ] Pending
* [ ] Fulfilled
* [ ] Rejected

### First-Principles Understanding

* [ ] Understand Promise as a future value
* [ ] Understand Promise as a placeholder for work that completes later

---

## 12. Creating Promises

### Concepts

* [ ] Create Promises manually
* [ ] Use resolve()
* [ ] Use reject()

### Example

```javascript
const promise = new Promise((resolve, reject) => {
  resolve("Success");
});
```

### Practice

* [ ] Create successful Promise
* [ ] Create rejected Promise
* [ ] Simulate API requests

---

## 13. Consuming Promises

### then()

* [ ] Handle successful results

### catch()

* [ ] Handle errors

### finally()

* [ ] Execute cleanup logic

### Example

```javascript
promise
  .then(result => console.log(result))
  .catch(error => console.log(error))
  .finally(() => console.log("Done"));
```

### Practice

* [ ] Chain multiple then() calls
* [ ] Handle Promise errors
* [ ] Use finally()

---

## 14. Promise Chaining

### Concepts

* [ ] Understand sequential async operations
* [ ] Pass values through chains
* [ ] Replace callback hell

### Practice

* [ ] Build login → profile → posts flow
* [ ] Create three-step Promise chain

---

## 15. Promise Utility Methods

### Promise.all()

* [ ] Execute multiple Promises simultaneously
* [ ] Handle multiple results

### Promise.race()

* [ ] Return fastest Promise

### Promise.allSettled()

* [ ] Handle mixed success/failure

### Promise.any()

* [ ] Return first successful Promise

### Practice

* [ ] Compare all utility methods
* [ ] Simulate multiple API requests

---

# Phase 6: Async / Await

## 16. Async Functions

### Concepts

* [ ] Understand async keyword
* [ ] Understand returned Promises
* [ ] Convert Promise chains

### Example

```javascript
async function getData() {
  return "Data";
}
```

### Practice

* [ ] Create async functions
* [ ] Return values from async functions

---

## 17. Await

### Concepts

* [ ] Understand await keyword
* [ ] Pause execution inside async functions
* [ ] Handle asynchronous values cleanly

### Example

```javascript
async function fetchData() {
  const result = await getData();
  console.log(result);
}
```

### Practice

* [ ] Await one Promise
* [ ] Await multiple Promises
* [ ] Build sequential workflows

---

## 18. Error Handling with Async/Await

### try...catch

* [ ] Handle async errors
* [ ] Understand exception flow

### Example

```javascript
async function fetchData() {
  try {
    const result = await getData();
    console.log(result);
  } catch (error) {
    console.log(error);
  }
}
```

### Practice

* [ ] Handle failed requests
* [ ] Simulate API failures
* [ ] Implement fallback logic

---

# Phase 7: Advanced Async

## 19. Microtasks vs Macrotasks

### Concepts

* [ ] Understand Microtask Queue
* [ ] Understand Macrotask Queue
* [ ] Understand execution priority

### Practice

Predict:

```javascript
Promise.resolve().then(() => console.log("Promise"));

setTimeout(() => console.log("Timeout"), 0);

console.log("Sync");
```

* [ ] Explain output order

```text
Sync
Promise
Timeout
```

---

## 20. Concurrency Concepts

### Concepts

* [ ] Concurrency vs Parallelism
* [ ] Request batching
* [ ] Rate limiting
* [ ] Retry mechanisms
* [ ] Debouncing
* [ ] Throttling

### Practice

* [ ] Build search debounce
* [ ] Build API retry system
* [ ] Build request queue

---

# Mini Projects

## Project 1: Countdown Timer

* [ ] Use setInterval()
* [ ] Display remaining time
* [ ] Stop automatically

---

## Project 2: Digital Clock

* [ ] Display current time
* [ ] Update every second
* [ ] Format correctly

---

## Project 3: Fake Login System

* [ ] Simulate API delay
* [ ] Use Promises
* [ ] Convert to Async/Await
* [ ] Handle errors

---

## Project 4: Weather App Simulator

* [ ] Simulate API requests
* [ ] Show loading state
* [ ] Handle success
* [ ] Handle failure

---

## Project 5: Sequential Task Runner

* [ ] Execute multiple async tasks
* [ ] Preserve execution order
* [ ] Handle failures gracefully

---

# Veteran-Level Challenges

* [ ] Explain Event Loop without notes
* [ ] Explain Microtask Queue vs Macrotask Queue
* [ ] Build your own Promise implementation
* [ ] Build an async task scheduler
* [ ] Simulate Event Loop behavior
* [ ] Understand Node.js Event Loop
* [ ] Understand V8 execution model

---

# Common Mistakes

* [ ] Confusing synchronous and asynchronous execution
* [ ] Forgetting to return Promises
* [ ] Forgetting await
* [ ] Using await outside async functions
* [ ] Ignoring Promise rejections
* [ ] Creating callback hell
* [ ] Misusing setInterval()
* [ ] Misunderstanding Event Loop execution order

---

# Completion Criteria ✅

You can move to DOM Manipulation & Browser APIs when you can:

* [ ] Explain synchronous vs asynchronous execution
* [ ] Explain Call Stack
* [ ] Explain Web APIs
* [ ] Explain Event Loop
* [ ] Use setTimeout() and setInterval()
* [ ] Create callback-based programs
* [ ] Explain callback hell
* [ ] Create and consume Promises
* [ ] Use Promise utility methods
* [ ] Use Async/Await confidently
* [ ] Handle async errors using try...catch
* [ ] Explain Microtasks vs Macrotasks
* [ ] Complete all 5 projects independently

---

# Key Concepts Mastery

* [ ] Call Stack
* [ ] Web APIs
* [ ] Event Loop
* [ ] Callback Queue
* [ ] Microtask Queue
* [ ] Macrotask Queue
* [ ] Callbacks
* [ ] Callback Hell
* [ ] Promises
* [ ] Promise States
* [ ] Promise Chaining
* [ ] Promise Utilities
* [ ] Async Functions
* [ ] Await
* [ ] Error Handling
* [ ] setTimeout()
* [ ] clearTimeout()
* [ ] setInterval()
* [ ] clearInterval()

🎯 Final Goal: Reach the point where you can reason about any asynchronous JavaScript code, predict its execution order, design reliable async workflows, and explain exactly what happens behind the scenes inside the JavaScript runtime.
