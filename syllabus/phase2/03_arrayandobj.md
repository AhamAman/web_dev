# Arrays and Objects – Working with Data ✅ Checklist

## 1. Introduction to Arrays and Objects

* [ ] Understand why data structures exist
* [ ] Understand when to use Arrays
* [ ] Understand when to use Objects
* [ ] Learn the difference between indexed data and key-value data

### First-Principles Understanding

* [ ] Understand that arrays organize **lists of related values**
* [ ] Understand that objects organize **related information about a single entity**
* [ ] Understand that data structures help programs manage complexity

### Examples

```javascript
// Array
const colors = ["red", "green", "blue"];

// Object
const user = {
  name: "John",
  age: 25
};
```

---

# Arrays

## 2. Creating Arrays

* [ ] Create empty arrays
* [ ] Create arrays with values
* [ ] Store different data types in arrays
* [ ] Access elements using index positions

### Practice

* [ ] Create an array of favorite movies
* [ ] Create an array of numbers
* [ ] Access first element
* [ ] Access last element

---

## 3. Array Properties

### Length

* [ ] Understand `.length`
* [ ] Find total elements in an array

### Practice

```javascript
const fruits = ["Apple", "Banana", "Mango"];

console.log(fruits.length);
```

* [ ] Use `.length` in exercises

---

## 4. Adding and Removing Elements

### push()

* [ ] Add element to end of array

```javascript
fruits.push("Orange");
```

### pop()

* [ ] Remove element from end

```javascript
fruits.pop();
```

### unshift()

* [ ] Add element to beginning

```javascript
fruits.unshift("Apple");
```

### shift()

* [ ] Remove element from beginning

```javascript
fruits.shift();
```

### Practice

* [ ] Add 3 items using `push()`
* [ ] Remove items using `pop()`
* [ ] Add items using `unshift()`
* [ ] Remove items using `shift()`

---

## 5. Iterating Through Arrays

### for Loop

* [ ] Understand traditional `for` loop
* [ ] Loop through arrays using index

```javascript
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

### for...of Loop

* [ ] Understand `for...of`
* [ ] Iterate without indexes

```javascript
for (const fruit of fruits) {
  console.log(fruit);
}
```

### Practice

* [ ] Print all array elements
* [ ] Print only even numbers
* [ ] Find largest number in an array

---

## 6. Array Methods

### map()

* [ ] Understand transformation
* [ ] Create new arrays using `map()`

```javascript
const doubled = numbers.map(num => num * 2);
```

### Practice

* [ ] Double all numbers
* [ ] Convert names to uppercase
* [ ] Add tax to product prices

---

### filter()

* [ ] Understand filtering
* [ ] Return matching elements

```javascript
const adults = ages.filter(age => age >= 18);
```

### Practice

* [ ] Filter even numbers
* [ ] Filter adults from age list
* [ ] Filter expensive products

---

### reduce()

* [ ] Understand accumulation
* [ ] Combine array values into one result

```javascript
const total = numbers.reduce(
  (sum, num) => sum + num,
  0
);
```

### Practice

* [ ] Calculate total sum
* [ ] Calculate average
* [ ] Find maximum value

---

## 7. Chaining Array Methods

* [ ] Combine `filter()` and `map()`
* [ ] Combine `map()` and `reduce()`
* [ ] Understand method chaining

### Practice

```javascript
const result = numbers
  .filter(num => num > 10)
  .map(num => num * 2);
```

* [ ] Create your own chained operations

---

# Objects

## 8. Understanding Objects

* [ ] Understand key-value pairs
* [ ] Understand object structure
* [ ] Understand real-world object modeling

### Example

```javascript
const person = {
  name: "John",
  age: 25,
  city: "Mumbai"
};
```

### Practice

* [ ] Create a student object
* [ ] Create a product object
* [ ] Create a car object

---

## 9. Accessing Object Properties

### Dot Notation

* [ ] Access properties using dot notation

```javascript
person.name;
```

### Bracket Notation

* [ ] Access properties using brackets

```javascript
person["name"];
```

### Practice

* [ ] Retrieve multiple properties
* [ ] Compare dot vs bracket notation

---

## 10. Modifying Object Properties

### Update Existing Properties

```javascript
person.age = 30;
```

* [ ] Update object values

### Add New Properties

```javascript
person.country = "India";
```

* [ ] Add new properties

### Delete Properties

```javascript
delete person.city;
```

* [ ] Remove properties

---

## 11. Object Methods

### What is a Method?

* [ ] Understand methods as functions inside objects

```javascript
const person = {
  name: "John",
  greet() {
    console.log("Hello");
  }
};
```

### Practice

* [ ] Create greeting method
* [ ] Create calculator object
* [ ] Create student object with methods

---

## 12. Understanding Prototypes

### Foundations

* [ ] Understand prototype inheritance
* [ ] Understand why prototypes exist
* [ ] Understand code reuse

### First-Principles Understanding

* [ ] Understand that JavaScript objects inherit behavior from other objects
* [ ] Understand prototype chains

### Example

```javascript
const person = {
  greet() {
    console.log("Hello");
  }
};

const student = Object.create(person);
```

### Practice

* [ ] Create objects using `Object.create()`
* [ ] Inspect prototype chain
* [ ] Explain inheritance in simple terms

---

# Iterating Over Objects

## 13. for...in Loop

* [ ] Understand `for...in`
* [ ] Iterate through object properties

```javascript
for (const key in person) {
  console.log(key);
}
```

### Practice

* [ ] Print all keys
* [ ] Print all values
* [ ] Print key-value pairs

---

## 14. Object Utility Methods

### Object.keys()

* [ ] Retrieve object keys

```javascript
Object.keys(person);
```

### Object.values()

* [ ] Retrieve object values

```javascript
Object.values(person);
```

### Object.entries()

* [ ] Retrieve key-value pairs

```javascript
Object.entries(person);
```

### Practice

* [ ] Loop through keys
* [ ] Loop through values
* [ ] Loop through entries

---

# Combining Arrays and Objects

## 15. Array of Objects

* [ ] Understand real-world data structures

```javascript
const users = [
  { name: "John", age: 25 },
  { name: "Jane", age: 30 }
];
```

### Practice

* [ ] Create a product catalog
* [ ] Create student records
* [ ] Create employee database

---

## 16. Working with Array of Objects

* [ ] Use `map()` on objects
* [ ] Use `filter()` on objects
* [ ] Use `reduce()` on objects

### Practice

* [ ] Get all names
* [ ] Filter active users
* [ ] Calculate total sales
* [ ] Find highest-paid employee

---

# Mini Projects

## Project 1: Student Management System

* [ ] Create student objects
* [ ] Store students in an array
* [ ] Add new students
* [ ] Remove students
* [ ] Display all students

---

## Project 2: Shopping Cart

* [ ] Store products in array
* [ ] Add products
* [ ] Remove products
* [ ] Calculate total price using `reduce()`

---

## Project 3: Expense Tracker

* [ ] Store expenses
* [ ] Filter expenses by category
* [ ] Calculate total spending

---

## Project 4: Employee Directory

* [ ] Create employee objects
* [ ] Search employees
* [ ] Filter employees by department
* [ ] Display employee information

---

# Common Mistakes

* [ ] Confusing arrays with objects
* [ ] Forgetting array indexes start at 0
* [ ] Mutating arrays accidentally
* [ ] Using `map()` when `filter()` is needed
* [ ] Forgetting `return` inside `map()`
* [ ] Using `for...in` on arrays unnecessarily
* [ ] Confusing object properties and methods
* [ ] Misunderstanding prototypes

---

# Completion Criteria ✅

You can move to **DOM Manipulation** when you can:

* [ ] Create and manipulate arrays confidently
* [ ] Use `push`, `pop`, `shift`, and `unshift`
* [ ] Use `map`, `filter`, and `reduce` without examples
* [ ] Create and modify objects confidently
* [ ] Access properties using both notations
* [ ] Create object methods
* [ ] Explain prototypes at a beginner level
* [ ] Loop through arrays and objects
* [ ] Build all 4 mini-projects independently

---

# Key Concepts Mastery

* [ ] Arrays
* [ ] Objects
* [ ] Properties
* [ ] Methods
* [ ] Prototypes
* [ ] Loops
* [ ] `for`
* [ ] `for...of`
* [ ] `for...in`
* [ ] `push()`
* [ ] `pop()`
* [ ] `shift()`
* [ ] `unshift()`
* [ ] `map()`
* [ ] `filter()`
* [ ] `reduce()`
* [ ] Object Utility Methods

🎯 Goal: Reach the point where you naturally think of arrays as **collections of data** and objects as **models of real-world entities**, while confidently transforming, filtering, and organizing data using modern JavaScript techniques.
