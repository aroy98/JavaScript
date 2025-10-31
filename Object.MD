# 🧠  Object

## 📘 Table of Contents

1. Introduction to Objects
2. Creating Objects
3. Accessing and Modifying Properties
4. Object Methods and the `this` Keyword
5. Property Descriptors
6. Iterating Over Objects
7. Object Utility Methods
8. Cloning and Merging Objects
9. Nested and Dynamic Objects
10. Real-World Examples with Explanations
11. Interview-Level Problems and Solutions

---

## 1. 🔍 Introduction to Objects

Objects in JavaScript are **key-value pairs** where keys are strings (or Symbols) and values can be any data type — even arrays or functions.

### Example:

```js
const person = {
  name: "Alice",
  age: 25,
  isStudent: true
};
```

🧩 **Explanation:** Here, `name`, `age`, and `isStudent` are keys (also known as properties). Each holds a value. Objects group related data together.

---

## 2. 🏗️ Creating Objects

There are multiple ways to create objects in JavaScript.

### (a) Object Literal

```js
const car = {
  brand: "Toyota",
  model: "Camry",
  year: 2022
};
```

🧩 **Explanation:** The easiest and most common way — defines key-value pairs directly.

### (b) Using the `Object` Constructor

```js
const user = new Object();
user.name = "Bob";
user.age = 30;
```

🧩 **Explanation:** Creates an empty object using a constructor, then adds properties.

### (c) Using a Factory Function

```js
function createPerson(name, age) {
  return { name, age };
}
const person = createPerson("Charlie", 28);
```

🧩 **Explanation:** Factory functions allow reusable object creation with custom values.

### (d) Constructor Function

```js
function User(name, age) {
  this.name = name;
  this.age = age;
}
const user1 = new User("David", 35);
```

🧩 **Explanation:** Using `new` creates an instance of an object based on a constructor.

---

## 3. 🎯 Accessing and Modifying Properties

### Example:

```js
const laptop = { brand: "HP", price: 60000 };
console.log(laptop.brand);     // Access via dot notation
console.log(laptop["price"]);  // Access via bracket notation

laptop.price = 65000;          // Modify property
laptop.color = "Silver";       // Add new property
```

🧩 **Explanation:** Dot notation is simpler, but bracket notation is useful when property names are dynamic or contain spaces.

---

## 4. ⚙️ Object Methods and `this`

Objects can include functions — these are called **methods**.

### Example:

```js
const user = {
  name: "Emma",
  greet() {
    console.log(`Hi, I'm ${this.name}!`);
  }
};
user.greet(); // Hi, I'm Emma!
```

🧩 **Explanation:** `this` refers to the current object where the function is defined.

---

## 5. 🔒 Property Descriptors

You can control how object properties behave using descriptors.

### Example:

```js
const car = {};
Object.defineProperty(car, 'engine', {
  value: 'V8',
  writable: false, // cannot be changed
  enumerable: true
});

console.log(car.engine); // V8
car.engine = 'V6';       // No effect
```

🧩 **Explanation:** Property descriptors help protect object integrity by locking values or preventing modifications.

---

## 6. 🔁 Iterating Over Objects

### Example 1: Using `for...in`

```js
const person = { name: 'Alice', age: 25, city: 'Delhi' };
for (let key in person) {
  console.log(`${key}: ${person[key]}`);
}
```

🧩 **Explanation:** `for...in` iterates over all enumerable keys in the object.

### Example 2: Using `Object.keys()` and `Object.entries()`

```js
const item = { id: 1, name: 'Book', price: 150 };
console.log(Object.keys(item));   // ['id','name','price']
console.log(Object.values(item)); // [1,'Book',150]
console.log(Object.entries(item));// [['id',1],['name','Book'],['price',150]]
```

🧩 **Explanation:** `Object.entries()` is great for converting objects into iterable arrays.

---

## 7. 🧠 Object Utility Methods

| Method            | Description                                                 |
| ----------------- | ----------------------------------------------------------- |
| `Object.assign()` | Copies values from one object to another                    |
| `Object.freeze()` | Prevents any modification                                   |
| `Object.seal()`   | Allows modification but prevents adding/removing properties |
| `Object.create()` | Creates an object with a given prototype                    |

### Example:

```js
const target = { a: 1 };
const source = { b: 2 };
Object.assign(target, source);
console.log(target); // { a: 1, b: 2 }
```

🧩 **Explanation:** `Object.assign()` is useful for merging or extending objects.

---

## 8. 🔗 Cloning and Merging Objects

### Shallow Copy:

```js
const obj1 = { a: 1, b: 2 };
const clone = { ...obj1 };
```

### Deep Copy:

```js
const deepClone = JSON.parse(JSON.stringify(obj1));
```

### Merging:

```js
const merged = { ...{x: 1}, ...{y: 2} };
console.log(merged); // { x: 1, y: 2 }
```

🧩 **Explanation:** Spread syntax `...` is the modern way to clone or merge objects.

---

## 9. 🧩 Nested and Dynamic Objects

### Example 1: Nested Objects

```js
const company = {
  name: 'TechCorp',
  address: { city: 'Bangalore', zip: 560001 }
};
console.log(company.address.city); // Bangalore
```

### Example 2: Optional Chaining

```js
console.log(company.location?.city); // undefined
```

### Example 3: Dynamic Properties

```js
const prop = 'salary';
const employee = { name: 'Arjun', [prop]: 75000 };
console.log(employee.salary); // 75000
```

🧩 **Explanation:** Use `[ ]` to dynamically assign property names at runtime.

---

## 10. 🌍 Real-World Examples with Explanations

### Example 1: Counting Votes

```js
const votes = ['A', 'B', 'A', 'C', 'A', 'B'];
const tally = votes.reduce((acc, vote) => {
  acc[vote] = (acc[vote] || 0) + 1;
  return acc;
}, {});
console.log(tally); // { A: 3, B: 2, C: 1 }
```

🧩 **Explanation:** The accumulator keeps track of counts for each unique key.

### Example 2: Grouping by Role

```js
const users = [
  { role: 'admin', name: 'John' },
  { role: 'user', name: 'Bob' },
  { role: 'admin', name: 'Sara' }
];

const grouped = users.reduce((acc, u) => {
  acc[u.role] = acc[u.role] || [];
  acc[u.role].push(u.name);
  return acc;
}, {});
console.log(grouped);
// { admin: ['John','Sara'], user: ['Bob'] }
```

🧩 **Explanation:** Useful for grouping data in dashboards or reports.

---

## 11. 💼 Interview-Level Problems with Explanations

### Problem 1: Compare Two Objects

```js
function isEqual(obj1, obj2) {
  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);
  if (keys1.length !== keys2.length) return false;
  return keys1.every(key => obj1[key] === obj2[key]);
}
console.log(isEqual({a:1,b:2}, {a:1,b:2})); // true
```

🧩 **Explanation:** Compares the key count and values for equality.

### Problem 2: Invert Key-Value Pairs

```js
const obj = { a: 1, b: 2 };
const inverted = Object.fromEntries(Object.entries(obj).map(([k,v]) => [v,k]));
console.log(inverted); // { 1: 'a', 2: 'b' }
```

🧩 **Explanation:** `Object.entries()` helps swap key-value pairs easily.

### Problem 3: Convert to Query String

```js
const params = { name: 'John', age: 30 };
const query = Object.entries(params).map(([k,v]) => `${k}=${v}`).join('&');
console.log(query); // name=John&age=30
```

🧩 **Explanation:** Commonly used in building URL query parameters.

---

## 🏁 Summary

| Concept     | Method                           | Description                   |
| ----------- | -------------------------------- | ----------------------------- |
| Creation    | `{}`, `new Object()`             | Create new objects            |
| Access      | `.`, `[]`                        | Retrieve or modify properties |
| Iterate     | `for...in`, `Object.keys()`      | Loop through properties       |
| Clone/Merge | `assign`, `spread`, `JSON.parse` | Copy or combine objects       |
| Protect     | `freeze`, `seal`                 | Control object mutability     |

---

✅ **Final Tip:** Objects are the building blocks of JavaScript. Use modern techniques like destructuring, spread syntax, and `Object.entries()` for clean, readable, and efficient code.
