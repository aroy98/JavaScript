# Map Object

> A focused, practical document to teach, demonstrate, and test mastery of the `Map` object in JavaScript. Contains explanations, runnable examples, performance notes, common pitfalls, and practice problems with full solutions.

---

## Table of Contents

1. Introduction
2. When to use Map vs Object
3. Creating Maps
4. Core API (methods & properties)
5. Iteration patterns
6. Advanced usage

   * Objects as keys
   * WeakMap vs Map
   * Chaining & fluent patterns
   * Using Map for memoization & caches
7. Converting Map ↔ Object ↔ Array
8. Performance considerations
9. Common pitfalls & gotchas
10. Real-world examples
11. Interview-style questions (with solutions)
12. Quick reference
13. Further reading

---

## 1. Introduction

The `Map` object in JavaScript is a collection of key-value pairs where keys can be of any type (primitives, objects, functions). Maps preserve insertion order and expose a rich API that is ideal for cases where you need reliable key typing and frequent additions/removals.

```js
// Minimal example
const m = new Map();
m.set('a', 1);
m.set({}, 2);
console.log(m.size); // 2
```

---

## 2. When to use Map vs Object

Use `Map` when:

* Keys are not strings or symbols (e.g., objects, functions).
* You need reliable iteration order (insertion order).
* You frequently add/remove key-value pairs.

Use plain `Object` when:

* You need simple JSON-like serializable data structures.
* You rely on the object prototype or want to use JSON.stringify on it.

Quick comparison:

| Feature   |                       Map | Object                                                                                                 |
| --------- | ------------------------: | ------------------------------------------------------------------------------------------------------ |
| Key types |                       Any | String / Symbol only                                                                                   |
| Order     | Maintains insertion order | Not guaranteed historically (now insertion order for string keys in many engines, but Map is explicit) |
| Size      |                   `.size` | `Object.keys(obj).length`                                                                              |
| Iteration |         Directly iterable | Requires `Object.keys/values/entries`                                                                  |

---

## 3. Creating Maps

```js
// Empty
const map1 = new Map();

// With initial entries
const map2 = new Map([ ['x', 10], ['y', 20] ]);

// From object
const fromObj = new Map(Object.entries({ name: 'Akash', role: 'Dev' }));
```

---

## 4. Core API (methods & properties)

### set(key, value)

Adds or updates a key-value pair. Returns the Map to allow chaining.

```js
map.set('a', 1).set('b', 2);
```

### get(key)

Returns the value for the key, or `undefined` if not present.

### has(key)

Checks presence of a key.

### delete(key)

Removes a key-value pair; returns `true` if an element existed and was removed.

### clear()

Removes all entries.

### size

Number of entries.

Examples:

```js
const m = new Map();
m.set('name', 'Akash');
console.log(m.get('name'));
console.log(m.has('age'));
```

---

## 5. Iteration patterns

Because Map is iterable, you can use `for...of`, `forEach`, or the iterator-producing methods: `.keys()`, `.values()`, `.entries()`.

```js
const m = new Map([['a',1], ['b',2]]);

for (const [k,v] of m) console.log(k, v);

m.forEach((v,k) => console.log(k, v));

console.log([...m.keys()]);
console.log([...m.values()]);
```

**Note:** `.forEach` callback order follows insertion order.

---

## 6. Advanced usage

### Objects as keys

```js
const u1 = {id:1};
const u2 = {id:2};
const visits = new Map();
visits.set(u1, 5);
visits.set(u2, 3);
console.log(visits.get(u1)); // 5
```

Important: the object identity matters — two object literals with identical shape are different keys.

### WeakMap vs Map

* `WeakMap` keys must be objects and are held weakly: they do not prevent garbage collection.
* Use `WeakMap` for per-object metadata where you don't want the map to keep objects alive.

### Chaining & fluent patterns

`Map.prototype.set` returns the Map, enabling chaining:

```js
const m = new Map();
m.set('a',1).set('b',2);
```

### Using Map for memoization / caches

```js
function memoize(fn) {
  const cache = new Map();
  return function(arg) {
    if (cache.has(arg)) return cache.get(arg);
    const result = fn(arg);
    cache.set(arg, result);
    return result;
  };
}
```

Be careful when `arg` is an object — you may want a `WeakMap`.

---

## 7. Converting Map ↔ Object ↔ Array

```js
const map = new Map([['a', 1], ['b', 2]]);

// Map -> Object
const obj = Object.fromEntries(map);

// Object -> Map
const map2 = new Map(Object.entries({ x: 10, y: 20 }));

// Map -> Array of entries
const arr = [...map]; // [['a',1], ['b',2]]

// Array -> Map
const map3 = new Map(arr);
```

---

## 8. Performance considerations

* Maps are usually more performant than objects for frequent additions/deletions and non-string keys.
* For small static lookup tables with string keys, plain objects are fine and easier to serialize.
* Avoid iterations on huge Maps in tight loops; profile if performance-sensitive.

---

## 9. Common pitfalls & gotchas

1. **Object key identity** — two objects with same contents are different keys.
2. **JSON.stringify** — Maps are not serialized to JSON by default. Convert with `Object.fromEntries`.
3. **Using NaN as key** — `NaN` is treated as the same key as itself in Maps (consistent with `Object.is`).

```js
const m = new Map();
m.set(NaN, 'not a number');
console.log(m.get(NaN)); // 'not a number'
```

4. **Prototype collision** — Maps don't suffer prototype property collisions like plain objects do.

---

## 10. Real-world examples

### Counting occurrences (word frequency)

```js
function wordFrequency(text) {
  const map = new Map();
  for (const word of text.split(/\s+/).filter(Boolean)) {
    const w = word.toLowerCase();
    map.set(w, (map.get(w) || 0) + 1);
  }
  return map;
}
```

### LRU cache (simple)

```js
class LRUCache {
  constructor(limit = 50) {
    this.limit = limit;
    this.map = new Map();
  }

  get(key) {
    if (!this.map.has(key)) return undefined;
    const val = this.map.get(key);
    // Move to end (most recently used)
    this.map.delete(key);
    this.map.set(key, val);
    return val;
  }

  set(key, value) {
    if (this.map.has(key)) this.map.delete(key);
    else if (this.map.size === this.limit) {
      // delete least-recent (first entry)
      const firstKey = this.map.keys().next().value;
      this.map.delete(firstKey);
    }
    this.map.set(key, value);
  }
}
```

---

## 11. Interview-style questions (with full solutions)

### Q1 — Swap keys and values (assume values are unique strings)

**Problem:** Given a `Map` with unique string values, create a new Map with keys and values swapped.

**Solution:**

```js
function invertMap(m) {
  const inverted = new Map();
  for (const [k,v] of m) inverted.set(v, k);
  return inverted;
}

// Example
const m = new Map([['a','1'], ['b','2']]);
console.log(invertMap(m)); // Map { '1' => 'a', '2' => 'b' }
```

**Explanation:** iterate and set reversed pairs. O(n) time.

---

### Q2 — Deep merge two Maps (key conflict => keep max value)

**Problem:** Merge two maps `m1` and `m2`. If a key exists in both, keep the larger numeric value.

**Solution:**

```js
function mergeMax(m1, m2) {
  const out = new Map(m1);
  for (const [k,v] of m2) {
    if (!out.has(k) || v > out.get(k)) out.set(k, v);
  }
  return out;
}
```

**Explanation:** copy `m1`, iterate `m2`, compare and set.

---

### Q3 — Find k most frequent items

**Problem:** Given an array of values, return top `k` values by frequency using `Map`.

**Solution:**

```js
function topK(arr, k) {
  const freq = new Map();
  for (const x of arr) freq.set(x, (freq.get(x) || 0) + 1);
  // convert to array and sort
  return [...freq.entries()]
    .sort((a,b) => b[1] - a[1])
    .slice(0,k)
    .map(([val]) => val);
}
```

**Explanation:** build frequency map (O(n)), sort entries (O(n log n)).

---

### Q4 — Serialize Map safely

**Problem:** JSON-serialize a Map so it can be restored later.

**Solution:**

```js
function serializeMap(map) {
  return JSON.stringify([...map.entries()]);
}

function deserializeMap(str) {
  return new Map(JSON.parse(str));
}
```

---

### Q5 — Implement `groupBy` using Map

**Problem:** Group an array of objects by a key and return a Map.

**Solution:**

```js
function groupBy(arr, keyFn) {
  const map = new Map();
  for (const item of arr) {
    const key = keyFn(item);
    if (!map.has(key)) map.set(key, []);
    map.get(key).push(item);
  }
  return map;
}

// Example
const users = [ {id:1, team:'A'}, {id:2, team:'B'}, {id:3, team:'A'} ];
console.log(groupBy(users, u => u.team));
```

---

## 12. Quick reference

* Create: `new Map(entries)`
* Add: `map.set(k,v)`
* Read: `map.get(k)`
* Check: `map.has(k)`
* Delete: `map.delete(k)`
* Clear: `map.clear()`
* Size: `map.size`
* Iterate: `for (const [k,v] of map)` or `map.forEach()`
* Convert: `Object.fromEntries(map)` / `new Map(Object.entries(obj))`

---

## 13. Further reading

* MDN `Map` docs
* ECMAScript specification (Map)

---

## Appendix — Practice problems (short)

1. Remove entries from a Map where value is falsy. (Write an in-place solution.)
2. Given a Map of user→timestamp, return users inactive for > 30 days.
3. Using Map, implement a simple pub/sub registry keyed by event name.

**Solutions**

1.

```js
for (const key of [...map.keys()]) {
  if (!map.get(key)) map.delete(key);
}
```

2.

```js
function inactiveUsers(map, now=Date.now(), days=30) {
  const cutoff = now - days*24*60*60*1000;
  return [...map.entries()].filter(([u,t]) => t < cutoff).map(([u]) => u);
}
```

3.

```js
class PubSub {
  constructor() { this.topics = new Map(); }
  subscribe(topic, fn) {
    if (!this.topics.has(topic)) this.topics.set(topic, new Set());
    this.topics.get(topic).add(fn);
    return () => this.topics.get(topic).delete(fn);
  }
  publish(topic, data) {
    if (!this.topics.has(topic)) return;
    for (const fn of this.topics.get(topic)) fn(data);
  }
}
```

---

*End of document.*
