# 7. Object-Oriented JavaScript – Mastering Objects and Classes ✅ Checklist

> Goal: Learn how to model real-world entities using objects, classes, inheritance, and prototypes while understanding how JavaScript's object system works behind the scenes.

---

# Phase 1: OOP Fundamentals

## 1. Introduction to Object-Oriented Programming (OOP)

### Core Concepts

* [ ] Understand what Object-Oriented Programming (OOP) is
* [ ] Understand why OOP exists
* [ ] Understand procedural vs object-oriented programming
* [ ] Understand how OOP models real-world entities

### First-Principles Understanding

* [ ] Understand that programs manage data and behavior
* [ ] Understand that objects group related data and behavior together
* [ ] Understand that OOP helps reduce complexity in large applications

### Real-World Examples

* [ ] User Object
* [ ] Product Object
* [ ] Bank Account Object
* [ ] Car Object
* [ ] Student Object

### Practice

* [ ] Identify objects in a shopping app
* [ ] Identify objects in a social media app
* [ ] Convert real-world entities into objects

---

# Phase 2: Objects

## 2. Creating Objects

### Concepts

* [ ] Create objects using object literals
* [ ] Define properties
* [ ] Define methods

### Example

```javascript
const user = {
  name: "John",
  age: 25,

  greet() {
    console.log("Hello");
  }
};
```

### Practice

* [ ] Create a student object
* [ ] Create a product object
* [ ] Create a car object

---

## 3. Understanding Object Properties

### Concepts

* [ ] Access properties using dot notation
* [ ] Access properties using bracket notation
* [ ] Add properties dynamically
* [ ] Update existing properties
* [ ] Delete properties

### Practice

* [ ] Create user profile object
* [ ] Update user information
* [ ] Remove object properties

---

## 4. Understanding Object Methods

### Concepts

* [ ] Understand methods
* [ ] Understand object behavior
* [ ] Call methods correctly

### Practice

* [ ] Create calculator object
* [ ] Create bank account object
* [ ] Create shopping cart object

---

# Phase 3: Constructors and this

## 5. Understanding Constructor Functions

### Concepts

* [ ] Understand why constructors exist
* [ ] Create multiple objects from one blueprint
* [ ] Understand reusable object creation

### Example

```javascript
function User(name, age) {
  this.name = name;
  this.age = age;
}
```

### Practice

* [ ] Create User constructor
* [ ] Create Product constructor
* [ ] Create Employee constructor

---

## 6. Understanding the this Keyword

### Concepts

* [ ] Understand what `this` refers to
* [ ] Understand context
* [ ] Understand object ownership

### First-Principles Understanding

* [ ] Understand that `this` points to the current object context
* [ ] Understand that `this` changes depending on how a function is called

### Practice

* [ ] Use `this` inside objects
* [ ] Use `this` inside constructors
* [ ] Compare regular functions and object methods

---

# Phase 4: Classes

## 7. Introduction to Classes

### Concepts

* [ ] Understand ES6 Classes
* [ ] Understand class syntax
* [ ] Understand why classes were introduced

### Example

```javascript
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```

### Practice

* [ ] Create User class
* [ ] Create Product class
* [ ] Create Student class

---

## 8. Creating Objects from Classes

### Concepts

* [ ] Understand object instantiation
* [ ] Use the `new` keyword

### Example

```javascript
const user1 = new User("John", 25);
```

### Practice

* [ ] Create multiple instances
* [ ] Compare instance values

---

## 9. Class Methods

### Concepts

* [ ] Define methods inside classes
* [ ] Use instance methods
* [ ] Understand shared behavior

### Example

```javascript
class User {
  greet() {
    console.log("Hello");
  }
}
```

### Practice

* [ ] Create greeting methods
* [ ] Create calculator methods
* [ ] Create shopping cart methods

---

# Phase 5: Inheritance

## 10. Understanding Inheritance

### Concepts

* [ ] Understand code reuse
* [ ] Understand parent-child relationships
* [ ] Understand inheritance hierarchy

### First-Principles Understanding

* [ ] Understand inheritance prevents duplicated code
* [ ] Understand child classes extend parent functionality

---

## 11. Extending Classes

### Concepts

* [ ] Use `extends`
* [ ] Create child classes

### Example

```javascript
class User {}

class Admin extends User {}
```

### Practice

* [ ] Create Employee from Person
* [ ] Create Admin from User
* [ ] Create Dog from Animal

---

## 12. Using super()

### Concepts

* [ ] Understand parent constructor access
* [ ] Initialize inherited properties

### Example

```javascript
class Admin extends User {
  constructor(name, age) {
    super(name, age);
  }
}
```

### Practice

* [ ] Create inherited constructors
* [ ] Pass data to parent classes

---

# Phase 6: Prototype Chain

## 13. Understanding Prototypes

### Concepts

* [ ] Understand prototype-based inheritance
* [ ] Understand object linking
* [ ] Understand method sharing

### First-Principles Understanding

* [ ] Understand JavaScript is prototype-based
* [ ] Understand classes are syntactic sugar over prototypes

### Practice

* [ ] Inspect object prototypes
* [ ] Use Object.getPrototypeOf()
* [ ] Explore browser prototype chains

---

## 14. Prototype Chain

### Concepts

* [ ] Understand inheritance lookup
* [ ] Understand prototype traversal

### Example

```javascript
const user = {};

console.log(user.toString());
```

### Practice

* [ ] Trace prototype chains
* [ ] Explain method lookup

---

# Phase 7: Encapsulation

## 15. Understanding Encapsulation

### Concepts

* [ ] Understand data protection
* [ ] Understand controlled access
* [ ] Understand information hiding

### First-Principles Understanding

* [ ] Understand objects should protect internal state
* [ ] Understand exposing only necessary functionality

---

## 16. Private Fields

### Concepts

* [ ] Use private properties
* [ ] Restrict direct access

### Example

```javascript
class BankAccount {
  #balance = 0;
}
```

### Practice

* [ ] Create private balance
* [ ] Create private password
* [ ] Restrict data access

---

# Phase 8: Polymorphism

## 17. Understanding Polymorphism

### Concepts

* [ ] Understand multiple implementations
* [ ] Understand method overriding
* [ ] Understand flexible interfaces

### Example

```javascript
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  speak() {
    console.log("Bark");
  }
}
```

### Practice

* [ ] Override methods
* [ ] Create multiple animal classes
* [ ] Create multiple payment systems

---

## 18. Method Overriding

### Concepts

* [ ] Replace inherited behavior
* [ ] Extend inherited behavior

### Practice

* [ ] Override greeting methods
* [ ] Override calculator methods

---

# Phase 9: Advanced OOP Concepts

## 19. Static Methods

### Concepts

* [ ] Understand class-level methods
* [ ] Understand utility methods

### Example

```javascript
class MathHelper {
  static add(a, b) {
    return a + b;
  }
}
```

### Practice

* [ ] Create utility classes
* [ ] Create helper functions

---

## 20. Getters and Setters

### Concepts

* [ ] Understand controlled property access
* [ ] Validate data

### Example

```javascript
class User {
  get name() {
    return this._name;
  }

  set name(value) {
    this._name = value;
  }
}
```

### Practice

* [ ] Create validated properties
* [ ] Create protected fields

---

# Mini Projects

## Project 1: Student Management System

* [ ] Create Student class
* [ ] Store student information
* [ ] Add methods
* [ ] Create multiple students

---

## Project 2: Bank Account System

* [ ] Create BankAccount class
* [ ] Use encapsulation
* [ ] Deposit money
* [ ] Withdraw money
* [ ] Check balance

---

## Project 3: Employee Management System

* [ ] Create Person class
* [ ] Create Employee class
* [ ] Create Manager class
* [ ] Implement inheritance

---

## Project 4: E-Commerce Product System

* [ ] Create Product class
* [ ] Create DigitalProduct class
* [ ] Create PhysicalProduct class
* [ ] Implement polymorphism

---

## Project 5: Animal Simulator

* [ ] Create Animal class
* [ ] Create Dog class
* [ ] Create Cat class
* [ ] Override methods
* [ ] Demonstrate polymorphism

---

# Common Mistakes

* [ ] Confusing classes with objects
* [ ] Misunderstanding `this`
* [ ] Forgetting `new`
* [ ] Overusing inheritance
* [ ] Ignoring composition alternatives
* [ ] Misunderstanding prototypes
* [ ] Confusing instance methods and static methods
* [ ] Breaking encapsulation unnecessarily

---

# Completion Criteria ✅

You can move to **Modules, ES6+, and Design Patterns** when you can:

* [ ] Explain OOP principles
* [ ] Create objects confidently
* [ ] Use constructors correctly
* [ ] Explain `this`
* [ ] Create ES6 classes
* [ ] Instantiate objects using `new`
* [ ] Implement inheritance
* [ ] Explain prototype chains
* [ ] Use encapsulation
* [ ] Implement polymorphism
* [ ] Build all 5 projects independently

---

# Key Concepts Mastery

* [ ] Objects
* [ ] Properties
* [ ] Methods
* [ ] Constructors
* [ ] this
* [ ] Classes
* [ ] Instances
* [ ] Inheritance
* [ ] extends
* [ ] super
* [ ] Prototypes
* [ ] Prototype Chain
* [ ] Encapsulation
* [ ] Private Fields
* [ ] Polymorphism
* [ ] Method Overriding
* [ ] Static Methods
* [ ] Getters
* [ ] Setters

🎯 Final Goal: Reach the point where you can model complex real-world systems using objects and classes while understanding the prototype-based foundations that power JavaScript's object-oriented features.
