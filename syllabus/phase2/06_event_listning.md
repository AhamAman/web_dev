# Event Handling – Making Web Pages Interactive ✅ Checklist

> Goal: Learn how JavaScript responds to user actions and browser events to create interactive web pages.

---

# 1. Introduction to Events

## Understanding Events

* [ ] Understand what an event is
* [ ] Understand event-driven programming
* [ ] Understand how browsers generate events
* [ ] Understand the relationship between user actions and JavaScript execution

### First-Principles Understanding

* [ ] Understand that web pages are waiting for user interactions
* [ ] Understand that events act as signals sent by the browser
* [ ] Understand that JavaScript listens and responds to these signals

### Common Events

#### Mouse Events

* [ ] `click`
* [ ] `dblclick`
* [ ] `mouseenter`
* [ ] `mouseleave`
* [ ] `mousemove`

#### Keyboard Events

* [ ] `keydown`
* [ ] `keyup`

#### Form Events

* [ ] `submit`
* [ ] `input`
* [ ] `change`
* [ ] `focus`
* [ ] `blur`

#### Window Events

* [ ] `load`
* [ ] `resize`
* [ ] `scroll`

### Practice

* [ ] Identify events on your favorite websites
* [ ] List 10 user actions that generate browser events

---

# 2. Event Listeners

## Understanding Event Listeners

* [ ] Understand what an event listener is
* [ ] Understand why event listeners exist
* [ ] Understand callback functions in event handling

### First-Principles Understanding

* [ ] Understand that listeners wait for specific events
* [ ] Understand that callbacks run only when events occur

---

## addEventListener()

### Syntax

```javascript
element.addEventListener("event", callback);
```

### Example

```javascript
const button = document.querySelector("button");

button.addEventListener("click", () => {
  console.log("Button clicked");
});
```

### Practice

* [ ] Add click listener to a button
* [ ] Add hover listener to a div
* [ ] Add keydown listener to an input
* [ ] Add submit listener to a form

---

## removeEventListener()

* [ ] Understand why listeners are removed
* [ ] Understand listener cleanup

### Practice

* [ ] Add and remove a click listener dynamically
* [ ] Disable interactions after an action

---

# 3. Event Object

## Understanding the Event Object

* [ ] Understand that every event generates an event object
* [ ] Access event information

### Example

```javascript
button.addEventListener("click", (event) => {
  console.log(event);
});
```

### Important Properties

* [ ] `event.target`
* [ ] `event.currentTarget`
* [ ] `event.type`
* [ ] `event.key`
* [ ] `event.clientX`
* [ ] `event.clientY`

### Practice

* [ ] Display clicked element
* [ ] Display pressed key
* [ ] Display mouse position

---

# 4. Event Propagation

## Understanding Event Propagation

### Concepts

* [ ] Understand what event propagation is
* [ ] Understand how events travel through the DOM
* [ ] Understand parent-child event relationships

### First-Principles Understanding

* [ ] Understand that events move through the DOM tree
* [ ] Understand that events don't remain on one element

---

## Event Bubbling

### Concepts

* [ ] Understand bubbling phase
* [ ] Understand child → parent event flow

### Example

```javascript
child.addEventListener("click", () => {
  console.log("Child");
});

parent.addEventListener("click", () => {
  console.log("Parent");
});
```

### Practice

* [ ] Create nested divs
* [ ] Observe bubbling behavior
* [ ] Predict event order

---

## Event Capturing

### Concepts

* [ ] Understand capturing phase
* [ ] Understand parent → child event flow

### Example

```javascript
parent.addEventListener(
  "click",
  () => {
    console.log("Parent");
  },
  true
);
```

### Practice

* [ ] Compare capturing and bubbling
* [ ] Explain event order

---

## Event Flow Mastery

* [ ] Understand Capturing Phase
* [ ] Understand Target Phase
* [ ] Understand Bubbling Phase

### Practice

* [ ] Draw event flow diagrams
* [ ] Explain event propagation without notes

---

# 5. Preventing Default Behavior

## event.preventDefault()

### Concepts

* [ ] Understand browser default actions
* [ ] Prevent unwanted browser behavior

### Example

```javascript
form.addEventListener("submit", (event) => {
  event.preventDefault();
});
```

### Common Use Cases

* [ ] Prevent form submission
* [ ] Prevent link navigation
* [ ] Create custom validation

### Practice

* [ ] Prevent page refresh on form submit
* [ ] Prevent navigation on link click
* [ ] Build custom form validation

---

# 6. Stopping Event Propagation

## event.stopPropagation()

### Concepts

* [ ] Understand stopping propagation
* [ ] Prevent parent listeners from executing

### Example

```javascript
button.addEventListener("click", (event) => {
  event.stopPropagation();
});
```

### Practice

* [ ] Stop bubbling events
* [ ] Compare behavior with and without stopPropagation()
* [ ] Create nested click handlers

---

# 7. Event Delegation (Recommended)

## Understanding Event Delegation

### Concepts

* [ ] Understand event delegation
* [ ] Understand why delegation improves performance
* [ ] Understand dynamic element handling

### First-Principles Understanding

* [ ] Understand that events bubble upward
* [ ] Understand that one parent listener can manage many child elements

### Example

```javascript
list.addEventListener("click", (event) => {
  if (event.target.matches("li")) {
    console.log("Item clicked");
  }
});
```

### Practice

* [ ] Handle clicks on dynamic lists
* [ ] Build delegated menu navigation
* [ ] Handle dynamically created buttons

---

# Mini Projects

## Project 1: Click Counter

* [ ] Increase count on button click
* [ ] Display total clicks
* [ ] Add reset button

---

## Project 2: Live Character Counter

* [ ] Listen to input events
* [ ] Count typed characters
* [ ] Display remaining characters

---

## Project 3: Form Validation

* [ ] Prevent default submission
* [ ] Validate user input
* [ ] Show validation messages

---

## Project 4: Interactive Color Changer

* [ ] Change colors on click
* [ ] Change colors on hover
* [ ] Reset styles

---

## Project 5: Dynamic To-Do List

* [ ] Add tasks
* [ ] Remove tasks
* [ ] Use event delegation
* [ ] Handle dynamically added elements

---

# Common Mistakes

* [ ] Forgetting to attach event listeners
* [ ] Confusing `target` and `currentTarget`
* [ ] Ignoring event propagation
* [ ] Overusing `stopPropagation()`
* [ ] Forgetting `preventDefault()`
* [ ] Creating unnecessary event listeners
* [ ] Not using event delegation for dynamic elements

---

# Completion Criteria ✅

You can move to the next module when you can:

* [ ] Explain event-driven programming
* [ ] Use common browser events confidently
* [ ] Attach listeners using `addEventListener()`
* [ ] Access and use the event object
* [ ] Explain event bubbling
* [ ] Explain event capturing
* [ ] Use `preventDefault()`
* [ ] Use `stopPropagation()`
* [ ] Implement event delegation
* [ ] Build all 5 projects independently

---

# Key Concepts Mastery

* [ ] Events
* [ ] Event Handling
* [ ] Event Listener
* [ ] addEventListener()
* [ ] removeEventListener()
* [ ] Event Object
* [ ] event.target
* [ ] event.currentTarget
* [ ] Event Bubbling
* [ ] Event Capturing
* [ ] Event Propagation
* [ ] Event Delegation
* [ ] preventDefault()
* [ ] stopPropagation()

🎯 Goal: Reach the point where you can build interactive web pages that respond intelligently to user actions while understanding exactly how events flow through the browser and DOM.
