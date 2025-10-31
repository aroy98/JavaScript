# 🧠 `Set` — Complete Mastery Guide

## 📘 Table of Contents

1. Introduction
2. Creating a Set
3. Adding and Deleting Elements
4. Checking for Values
5. Iterating through a Set
6. Set Size and Clearing
7. Working with Arrays and Sets
8. Set Operations (Union, Intersection, Difference)
9. Common Use Cases
10. Set vs Array vs Map
11. Summary

---

## 🔹 Introduction

A **`Set`** in JavaScript is a **collection of unique values** — it automatically removes duplicates.
It can store **any type of value**, whether primitive or object references.

### Example

```js
const fruits = new Set(["apple", "banana", "apple"]);
console.log(fruits); // Set(2) { 'apple', 'banana' }
```

---

## 🔹 Creating a Set

### Syntax

```js
const mySet = new Set();
```

### Example with Initialization

```js
const numbers = new Set([1, 2, 3, 3, 4]);
console.log(numbers); // Set(4) { 1, 2, 3, 4 }
```

You can also initialize an empty Set and then add items:

```js
const colors = new Set();
colors.add("red");
colors.add("green");
colors.add("blue");
console.log(colors); // Set(3) { 'red', 'green', 'blue' }
```

---

## 🔹 Adding and Deleting Elements

### Add Elements

```js
const ids = new Set();
ids.add(101);
ids.add(102).add(103); // method chaining
console.log(ids); // Set(3) { 101, 102, 103 }
```

### Delete Elements

```js
ids.delete(102);
console.log(ids); // Set(2) { 101, 103 }
```

### Check if Value Exists

```js
console.log(ids.has(103)); // true
console.log(ids.has(999)); // false
```

---

## 🔹 Iterating through a Set

You can iterate over a `Set` just like an array.

### Using `for...of`

```js
const languages = new Set(["JavaScript", "Python", "Go"]);
for (const lang of languages) {
  console.log(lang);
}
```

### Using `forEach()`

```js
languages.forEach(value => console.log(value));
```

### Using Spread Operator

```js
console.log([...languages]); // [ 'JavaScript', 'Python', 'Go' ]
```

---

## 🔹 Set Size and Clearing

### Getting the Size

```js
const pets = new Set(["cat", "dog", "parrot"]);
console.log(pets.size); // 3
```

### Clearing All Elements

```js
pets.clear();
console.log(pets.size); // 0
```

---

## 🔹 Working with Arrays and Sets

Sets are often used to **remove duplicates** from arrays.

### Remove Duplicates from an Array

```js
const arr = [1, 2, 2, 3, 4, 4, 5];
const uniqueArr = [...new Set(arr)];
console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

### Convert Set Back to Array

```js
const mySet = new Set([10, 20, 30]);
const arrFromSet = Array.from(mySet);
console.log(arrFromSet); // [10, 20, 30]
```

---

## 🔹 Set Operations

Mathematical operations like **Union**, **Intersection**, and **Difference** can be implemented using Sets.

### 1. Union (A ∪ B)

```js
const setA = new Set([1, 2, 3]);
const setB = new Set([3, 4, 5]);
const union = new Set([...setA, ...setB]);
console.log(union); // Set(5) { 1, 2, 3, 4, 5 }
```

### 2. Intersection (A ∩ B)

```js
const intersection = new Set([...setA].filter(x => setB.has(x)));
console.log(intersection); // Set(1) { 3 }
```

### 3. Difference (A − B)

```js
const difference = new Set([...setA].filter(x => !setB.has(x)));
console.log(difference); // Set(2) { 1, 2 }
```

---

## 🔹 Common Use Cases

### ✅ Removing Duplicates

```js
const emails = ["a@gmail.com", "b@gmail.com", "a@gmail.com"];
const uniqueEmails = [...new Set(emails)];
console.log(uniqueEmails);
```

### ✅ Checking for Unique Inputs

```js
const seen = new Set();
function isUnique(value) {
  if (seen.has(value)) return false;
  seen.add(value);
  return true;
}
console.log(isUnique('apple')); // true
console.log(isUnique('apple')); // false
```

### ✅ Storing Unique DOM Elements

```js
const nodes = new Set(document.querySelectorAll('div'));
console.log(nodes.size);
```

---

## 🔹 Set vs Array vs Map

| Feature               | Set               | Array                   | Map                   |
| --------------------- | ----------------- | ----------------------- | --------------------- |
| Stores Unique Values  | ✅                 | ❌                       | ❌                     |
| Key-Value Pairs       | ❌                 | ❌                       | ✅                     |
| Order Preserved       | ✅                 | ✅                       | ✅                     |
| Supports Index Access | ❌                 | ✅                       | ❌                     |
| Common Use            | Remove Duplicates | Store Data Sequentially | Store Key-Value Pairs |

---

## 🔹 Summary

* `Set` is ideal for storing **unique values**.
* Great for **removing duplicates** from arrays.
* Supports powerful operations like **Union**, **Intersection**, and **Difference**.
* Does **not** support index-based access.
* Often used in performance-critical areas to track **seen** or **processed** items.

---

**Next Step:** Learn about [`WeakSet`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet) for storing objects **without preventing garbage collection**.
