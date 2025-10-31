# 🧠 Array — Complete Mastery Guide

## 📘 Table of Contents

1. Introduction to Arrays
2. Creating Arrays
3. Accessing and Modifying Elements
4. Array Properties
5. Core Array Methods
6. Iteration and Transformation Methods
7. Searching, Filtering, and Reducing
8. Sorting and Flattening
9. Advanced Techniques
10. Real-World Examples with Explanations
11. Interview Problems with Solutions

---

## 1. 🔍 Introduction to Arrays

An **Array** in JavaScript is an ordered collection of elements that can store multiple values of any type — numbers, strings, objects, or even functions.

```js
const fruits = ["Apple", "Banana", "Mango"];
console.log(fruits[0]); // Output: Apple
```

🧩 **Explanation:** Arrays in JavaScript are zero-indexed, meaning the first element has an index of `0`. You can access any element using its index.

---

## 2. 🏗️ Creating Arrays

### ✅ Using Array Literals

```js
const numbers = [1, 2, 3, 4];
```

### ✅ Using Array Constructor

```js
const arr = new Array(5); // Creates an empty array with 5 slots
```

### ✅ Using `Array.of()`

```js
const arr = Array.of(5, 10, 15); // [5, 10, 15]
```

### ✅ Using `Array.from()`

```js
const chars = Array.from('Hello'); // ['H','e','l','l','o']
```

🧩 **Explanation:** `Array.from()` converts iterable objects like strings or sets into arrays.

---

## 3. 🎯 Accessing and Modifying Elements

```js
const colors = ["Red", "Green", "Blue"];
colors[1] = "Yellow";
console.log(colors); // ["Red", "Yellow", "Blue"]
```

🧩 **Explanation:** Arrays are mutable — you can update, insert, or remove elements easily.

You can also access the last element:

```js
console.log(colors.at(-1)); // "Blue"
```

---

## 4. ⚙️ Array Properties

| Property | Description                 | Example               |
| -------- | --------------------------- | --------------------- |
| `length` | Number of elements in array | `[1,2,3].length // 3` |

```js
const arr = [10, 20, 30];
console.log(arr.length); // 3
```

🧩 **Explanation:** `.length` dynamically updates when elements are added or removed.

---

## 5. 🧩 Core Array Methods

### ➕ `push()` and `pop()`

```js
const nums = [1, 2];
nums.push(3); // Adds at the end → [1, 2, 3]
nums.pop();   // Removes last → [1, 2]
```

### ↔️ `shift()` and `unshift()`

```js
const fruits = ["Apple", "Banana"];
fruits.unshift("Mango"); // Add at start
fruits.shift();           // Remove first
console.log(fruits); // ["Apple", "Banana"]
```

### 🧠 `concat()`

```js
const arr1 = [1, 2];
const arr2 = [3, 4];
const result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]
```

🧩 **Explanation:** `concat()` returns a new array — it doesn’t modify the originals.

---

## 6. 🔁 Iteration and Transformation Methods

### 🚀 `map()`

```js
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2);
console.log(doubled); // [2, 4, 6]
```

🧩 **Explanation:** `map()` creates a new array by applying a function to every element.

### 🔍 `forEach()`

```js
const items = ["Pen", "Pencil", "Eraser"];
items.forEach(item => console.log(item));
```

🧩 **Explanation:** `forEach()` executes a function for each element but doesn’t return anything.

### 💡 `filter()`

```js
const ages = [10, 18, 21, 15];
const adults = ages.filter(age => age >= 18);
console.log(adults); // [18, 21]
```

🧩 **Explanation:** `filter()` returns only those elements that satisfy a condition.

---

## 7. 🔎 Searching, Filtering, and Reducing

### 🔸 `find()` and `findIndex()`

```js
const users = [{id: 1}, {id: 2}];
const user = users.find(u => u.id === 2);
console.log(user); // {id: 2}
```

### 🔸 `reduce()`

```js
const nums = [1, 2, 3, 4];
const sum = nums.reduce((acc, n) => acc + n, 0);
console.log(sum); // 10
```

🧩 **Explanation:** `reduce()` combines all elements into a single value (sum, average, object, etc.).

---

## 8. 🔢 Sorting and Flattening

### 📊 `sort()`

```js
const arr = [5, 2, 10, 1];
arr.sort((a, b) => a - b);
console.log(arr); // [1, 2, 5, 10]
```

### 🧩 `flat()` and `flatMap()`

```js
const arr = [1, [2, [3, 4]]];
console.log(arr.flat(2)); // [1, 2, 3, 4]
```

---

## 9. 🧠 Advanced Techniques

### Removing Duplicates

```js
const arr = [1, 1, 2, 3, 3];
const unique = [...new Set(arr)];
console.log(unique); // [1, 2, 3]
```

### Destructuring

```js
const [first, ...rest] = [10, 20, 30];
console.log(first); // 10
console.log(rest);  // [20, 30]
```

### Merging Arrays

```js
const merged = [...[1, 2], ...[3, 4]];
console.log(merged); // [1, 2, 3, 4]
```

---

## 10. 🌍 Real-World Examples with Explanations

### 🧮 Example 1 — Calculate Average

```js
const scores = [80, 90, 100, 70];
const average = scores.reduce((a, b) => a + b, 0) / scores.length;
console.log(average); // 85
```

🧩 **Explanation:** `reduce()` calculates the total sum, and then we divide by the length.

### 🔤 Example 2 — Capitalize First Letter

```js
const names = ["john", "mike", "sarah"];
const capitalized = names.map(n => n[0].toUpperCase() + n.slice(1));
console.log(capitalized); // ["John", "Mike", "Sarah"]
```

🧩 **Explanation:** Each string’s first letter is converted to uppercase using `map()`.

### 📦 Example 3 — Group by Property

```js
const people = [
  { city: "NY", name: "Alice" },
  { city: "LA", name: "Bob" },
  { city: "NY", name: "Carol" }
];

const grouped = people.reduce((acc, person) => {
  acc[person.city] = acc[person.city] || [];
  acc[person.city].push(person);
  return acc;
}, {});

console.log(grouped);
```

🧩 **Explanation:** `reduce()` is used to group data by a key.

---

## 11. 💼 Interview Problems with Explanations

### 🔸 Problem 1 — Reverse an Array

```js
const arr = [1, 2, 3];
const reversed = arr.reduceRight((acc, n) => (acc.push(n), acc), []);
console.log(reversed); // [3, 2, 1]
```

🧩 **Explanation:** `reduceRight()` traverses from right to left, reversing the order.

### 🔸 Problem 2 — Find Duplicates

```js
const arr = [1, 2, 3, 2, 1];
const duplicates = arr.filter((item, index) => arr.indexOf(item) !== index);
console.log(duplicates); // [2, 1]
```

🧩 **Explanation:** Checks if the first occurrence of an element is different from the current index.

### 🔸 Problem 3 — Flatten Deeply Nested Array

```js
function flattenArray(arr) {
  return arr.flat(Infinity);
}
console.log(flattenArray([1, [2, [3, [4]]]])); // [1,2,3,4]
```

🧩 **Explanation:** Using `flat(Infinity)` removes all levels of nesting.

---

## 🏁 Summary

| Category   | Method                                      | Description                       |
| ---------- | ------------------------------------------- | --------------------------------- |
| Add/Remove | `push`, `pop`, `shift`, `unshift`, `splice` | Modify arrays                     |
| Iterate    | `map`, `forEach`, `filter`, `reduce`        | Transform and loop through arrays |
| Search     | `find`, `includes`, `indexOf`               | Locate elements                   |
| Transform  | `flat`, `concat`, `flatMap`                 | Combine or reshape arrays         |
| Utility    | `sort`, `reverse`, `join`                   | Miscellaneous helpers             |

---

✅ **Final Tip:** Use immutable methods (`map`, `filter`, `reduce`) whenever possible to write clean, predictable, and side-effect-free code.
