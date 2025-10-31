# 🧠 Object

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

In JavaScript, **objects** are collections of **key-value pairs**. Keys are strings (or Symbols), and values can be of any type — even functions or other objects.

```js
const person = {
  name: "John",
  age: 30,
  isEmployed: true
};
```

🧩 **Explanation:** Objects store structured data. They are the foundation of most JS constructs — including arrays, classes, and functions.

---

## 2. 🏗️ Creating Objects

### ✅ Object Literal Syntax

```js
const car = {
  brand: "Tesla",
  model: "Model 3",
  year: 2023
};
```

### ✅ Using the `Object` Constructor

```js
const user = new Object();
user.name = "Alice";
user.age = 25;
```

### ✅ Using a Factory Function

```js
function createUser(name, age) {
  return { name, age };
}

const user1 = createUser("Bob", 22);
console.log(user1); // { name: 'Bob', age: 22 }
```

### ✅ Using a Constructor Function

```js
function User(name, age) {
  this.name = name;
  this.age = age;
}
const user2 = new User("Carol", 27);
```

---

## 3. 🎯 Accessing and Modifying Properties

### Dot Notation

```js
console.log(car.brand); // 'Tesla'
```

### Bracket Notation

```js
console.log(car["model"]); // 'Model 3'
```

### Adding or Updating Properties

```js
car.color = "Red";
car.year = 2024; // update
```

### Deleting a Property

```js
delete car.model;
```

🧩 **Explanation:** Bracket notation is useful when keys are dynamic or contain special characters.

---

## 4. ⚙️ Object Methods and `this`

You can define functions inside objects — called **methods**.

```js
const user = {
  name: "John",
  greet() {
    console.log(`Hello, ${this.name}!`);
  }
};

user.greet(); // Hello, John!
```

🧩 **Explanation:** The `this` keyword refers to the object the method belongs to.

---

## 5. 🔒 Property Descriptors

Every object property has attributes like `writable`, `enumerable`, and `configurable`.

```js
const obj = {};
Object.defineProperty(obj, 'id', {
  value: 101,
  writable: false
});

console.log(obj.id); // 101
obj.id = 202;        // Ignored in strict mode
```

🧩 **Explanation:** This allows fine-grained control over how properties behave.

---

## 6. 🔁 Iterating Over Objects

### Using `for...in`

```js
const student = { name: 'Alice', grade: 'A' };
for (let key in student) {
  console.log(key, student[key]);
}
```

### Using `Object.keys()`, `Object.values()`, `Object.entries()`

```js
const product = { id: 1, name: 'Book', price: 200 };

console.log(Object.keys(product));   // ['id','name','price']
console.log(Object.values(product)); // [1,'Book',200]
console.log(Object.entries(product)); // [['id',1],['name','Book'],['price',200]]
```

🧩 **Explanation:** `Object.entries()` is handy for looping with `for...of`.

---

## 7. 🧠 Object Utility Methods

| Method            | Description                                                |
| ----------------- | ---------------------------------------------------------- |
| `Object.assign()` | Copy properties from one object to another                 |
| `Object.freeze()` | Make an object immutable                                   |
| `Object.seal()`   | Prevent adding/removing properties, but allow modification |
| `Object.create()` | Create an object with a specific prototype                 |

### Example:

```js
const target = { a: 1 };
const source = { b: 2 };
Object.assign(target, source);
console.log(target); // { a: 1, b: 2 }
```

🧩 **Explanation:** `Object.assign()` merges two or more objects.

---

## 8. 🔗 Cloning and Merging Objects

### Shallow Clone

```js
const clone = { ...car };
```

### Deep Clone

```js
const deepClone = JSON.parse(JSON.stringify(car));
```

### Merging Multiple Objects

```js
const merged = { ...car, ...user };
```

🧩 **Explanation:** The spread operator (`...`) merges or copies enumerable properties.

---

## 9. 🧩 Nested and Dynamic Objects

### Accessing Nested Properties

```js
const company = {
  name: 'TechCorp',
  address: {
    city: 'New York',
    zip: 10001
  }
};
console.log(company.address.city); // 'New York'
```

### Optional Chaining

```js
console.log(company.location?.city); // undefined (no error)
```

### Dynamic Keys

```js
const key = 'salary';
const employee = {
  name: 'Mike',
  [key]: 50000
};
console.log(employee.salary); // 50000
```

🧩 **Explanation:** Dynamic properties are defined using square brackets around a variable.

---

## 10. 🌍 Real-World Examples

### 📦 Example 1 — Grouping Data

```js
const users = [
  { role: 'admin', name: 'John' },
  { role: 'user', name: 'Bob' },
  { role: 'admin', name: 'Sarah' }
];

const grouped = users.reduce((acc, user) => {
  acc[user.role] = acc[user.role] || [];
  acc[user.role].push(user.name);
  return acc;
}, {});

console.log(grouped);
// { admin: ['John', 'Sarah'], user: ['Bob'] }
```

🧩 **Explanation:** `reduce()` groups items by a specific property.

### 🧮 Example 2 — Counting Occurrences

```js
const votes = ['A', 'B', 'A', 'C', 'B', 'A'];
const tally = votes.reduce((acc, v) => {
  acc[v] = (acc[v] || 0) + 1;
  return acc;
}, {});
console.log(tally); // { A: 3, B: 2, C: 1 }
```

---

## 11. 💼 Interview-Level Problems

### 🔸 Problem 1 — Compare Two Objects

```js
function isEqual(obj1, obj2) {
  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);
  if (keys1.length !== keys2.length) return false;
  return keys1.every(key => obj1[key] === obj2[key]);
}

console.log(isEqual({a:1,b:2}, {a:1,b:2})); // true
```

🧩 **Explanation:** Compares all keys and values for equality.

### 🔸 Problem 2 — Convert Object to Query String

```js
const params = { name: 'John', age: 25 };
const query = Object.entries(params).map(([k, v]) => `${k}=${v}`).join('&');
console.log(query); // 'name=John&age=25'
```

### 🔸 Problem 3 — Invert Key-Value Pairs

```js
const obj = { a: 1, b: 2 };
const inverted = Object.fromEntries(Object.entries(obj).map(([k,v]) => [v,k]));
console.log(inverted); // { 1: 'a', 2: 'b' }
```

🧩 **Explanation:** `Object.entries()` + `map()` transforms pairs and `Object.fromEntries()` rebuilds the object.

---

## 🏁 Summary Table

| Category  | Method                               | Description            |
| --------- | ------------------------------------ | ---------------------- |
| Create    | `{}`, `new Object()`                 | Make new objects       |
| Access    | `.`, `[]`                            | Retrieve values        |
| Iterate   | `for...in`, `Object.keys()`          | Loop over keys/values  |
| Utility   | `assign`, `freeze`, `seal`, `create` | Manage objects         |
| Transform | `entries`, `fromEntries`, `values`   | Convert and manipulate |

---

✅ **Final Tip:** Use **destructuring**, **spread syntax**, and **functional methods** (`map`, `reduce`, `entries`) for elegant and immutable object manipulation.
