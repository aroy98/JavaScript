# 🧠  WeakMap & WeakSet — Complete Mastery Guide

## 📘 Table of Contents

1. Introduction
2. What is WeakMap?
3. WeakMap vs Map
4. Common WeakMap Methods
5. WeakMap Examples
6. What is WeakSet?
7. WeakSet vs Set
8. Common WeakSet Methods
9. WeakSet Examples
10. Memory Management and Garbage Collection
11. Practical Use Cases
12. Summary

---

## 🔹 Introduction

In JavaScript, **WeakMap** and **WeakSet** are special types of collections that hold **weak references** to their keys (for `WeakMap`) or values (for `WeakSet`).
They allow **automatic garbage collection** of objects when there are no other references to them.

Unlike `Map` or `Set`, **WeakMap** and **WeakSet**:

* Can only store **objects** (not primitives).
* Are **not iterable**.
* Do **not have a `size` property**.

They are primarily used for **memory-efficient data management** and **object caching**.

---

## 🔹 What is WeakMap?

A **WeakMap** is a collection of **key/value pairs** where:

* **Keys must be objects.**
* **Values can be anything.**
* If the key object is no longer referenced elsewhere, it is **automatically removed** from memory.

### Example

```js
let user = { name: 'Alice' };
const weakMap = new WeakMap();
weakMap.set(user, 'Admin');

console.log(weakMap.get(user)); // 'Admin'

user = null; // Remove reference to user
// The entry in weakMap will be garbage collected automatically.
```

✅ **Key takeaway:** You don’t have to manually delete entries — JavaScript’s garbage collector handles it.

---

## 🔹 WeakMap vs Map

| Feature            | Map                                 | WeakMap                       |
| ------------------ | ----------------------------------- | ----------------------------- |
| Key Type           | Any (object or primitive)           | Objects only                  |
| Iteration          | Iterable (`for...of`, `.forEach()`) | ❌ Not iterable                |
| `size` Property    | ✅ Available                         | ❌ Not available               |
| Garbage Collection | ❌ Manual                            | ✅ Automatic (weak references) |
| Use Case           | Persistent data                     | Temporary/cached data         |

---

## 🔹 Common WeakMap Methods

| Method             | Description                  | Example               |
| ------------------ | ---------------------------- | --------------------- |
| `.set(key, value)` | Add a new key-value pair     | `wm.set(obj, 'data')` |
| `.get(key)`        | Retrieve the value for a key | `wm.get(obj)`         |
| `.has(key)`        | Check if the key exists      | `wm.has(obj)`         |
| `.delete(key)`     | Remove a key-value pair      | `wm.delete(obj)`      |

### Example:

```js
const wm = new WeakMap();
let obj = {};

wm.set(obj, 'Secret Data');
console.log(wm.has(obj)); // true
console.log(wm.get(obj)); // 'Secret Data'

wm.delete(obj);
console.log(wm.has(obj)); // false
```

---

## 🔹 WeakMap Example: Private Data Storage

WeakMaps are often used to store **private data** in objects, preventing direct access.

```js
const privateData = new WeakMap();

class User {
  constructor(name, password) {
    this.name = name;
    privateData.set(this, { password });
  }
  getPassword() {
    return privateData.get(this).password;
  }
}

const user1 = new User('John', '12345');
console.log(user1.getPassword()); // 12345

// password data can't be accessed directly
console.log(user1.password); // undefined
```

---

## 🔹 What is WeakSet?

A **WeakSet** is similar to a `Set`, but it only stores **objects**, and they are **weakly held**.

* No duplicates allowed.
* Objects in a WeakSet can be **garbage collected** if no other references exist.

### Example

```js
let obj1 = { id: 1 };
let obj2 = { id: 2 };

const weakSet = new WeakSet([obj1, obj2]);
console.log(weakSet.has(obj1)); // true

obj1 = null; // object is no longer referenced
// obj1 is automatically garbage collected from the WeakSet
```

---

## 🔹 WeakSet vs Set

| Feature            | Set                     | WeakSet               |
| ------------------ | ----------------------- | --------------------- |
| Value Type         | Any type                | Objects only          |
| Iteration          | ✅ Iterable              | ❌ Not iterable        |
| `size` Property    | ✅ Available             | ❌ Not available       |
| Garbage Collection | ❌ Manual                | ✅ Automatic           |
| Use Case           | Unique value collection | Track object presence |

---

## 🔹 Common WeakSet Methods

| Method           | Description            | Example          |
| ---------------- | ---------------------- | ---------------- |
| `.add(value)`    | Add a new object       | `ws.add(obj)`    |
| `.has(value)`    | Check if object exists | `ws.has(obj)`    |
| `.delete(value)` | Remove an object       | `ws.delete(obj)` |

### Example:

```js
const ws = new WeakSet();
let car = { model: 'Tesla' };

ws.add(car);
console.log(ws.has(car)); // true

ws.delete(car);
console.log(ws.has(car)); // false
```

---

## 🔹 WeakSet Example: Track Active Objects

```js
const activeUsers = new WeakSet();

class User {
  constructor(name) {
    this.name = name;
    activeUsers.add(this);
  }
  logout() {
    activeUsers.delete(this);
  }
}

let john = new User('John');
console.log(activeUsers.has(john)); // true

john.logout();
console.log(activeUsers.has(john)); // false
```

---

## 🔹 Memory Management and Garbage Collection

Both `WeakMap` and `WeakSet` are **memory-safe** — they don’t prevent their objects from being garbage collected.
When the only remaining references to an object are weak (inside a WeakMap or WeakSet), the object is **automatically removed** from memory.

This makes them **ideal for caching, storing metadata, or tracking state**.

---

## 🔹 Practical Use Cases

### ✅ Use Case 1: Caching

```js
const cache = new WeakMap();

function fetchData(obj) {
  if (cache.has(obj)) {
    return cache.get(obj); // return cached data
  }
  const result = expensiveOperation(obj);
  cache.set(obj, result);
  return result;
}
```

### ✅ Use Case 2: DOM Element Metadata

```js
const elementData = new WeakMap();

function trackElement(el, info) {
  elementData.set(el, info);
}

const button = document.querySelector('button');
trackElement(button, { clicked: 0 });

button.addEventListener('click', () => {
  const data = elementData.get(button);
  data.clicked++;
  console.log(data.clicked);
});
```

### ✅ Use Case 3: Object Tracking

```js
const weakSet = new WeakSet();
const obj = {};
weakSet.add(obj);

console.log(weakSet.has(obj)); // true
```

---

## 🔹 Summary

| Feature            | WeakMap               | WeakSet                  |
| ------------------ | --------------------- | ------------------------ |
| Stores             | Key-value pairs       | Object values            |
| Keys/Values        | Keys: Objects only    | Values: Objects only     |
| Iteration          | ❌ No                  | ❌ No                     |
| Garbage Collection | ✅ Automatic           | ✅ Automatic              |
| Use Case           | Private data, caching | Object presence tracking |

---

**In short:**

* Use **WeakMap** for mapping data to objects privately.
* Use **WeakSet** for tracking object membership.
* Both improve **memory efficiency** and avoid **memory leaks**.

---

**Next Step:** Explore [`FinalizationRegistry`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/FinalizationRegistry) to handle cleanup logic when objects are garbage collected.
