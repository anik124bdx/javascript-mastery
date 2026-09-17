# 📖 Chapter 06: Objects & OOP Basics

[⏮️ Prev: Chapter 05 (Functions & Scope)](chapter-05-functions-and-scope.md) • [🏠 Home (Roadmap)](../README.md) • [Next: Chapter 07 (DOM & Events) ⏭️](chapter-07-dom-and-events.md)

---

Objects represent real-world entities through structured key-value pairs, encapsulate behavior through methods, and serve as the core paradigm for state representation.

---

## 📑 Table of Contents
1. [What is an Object?](#1-what-is-an-object)
2. [Accessing Properties: Dot vs Bracket Notation](#2-accessing-properties-dot-vs-bracket-notation)
3. [Adding, Modifying & Deleting Properties](#3-adding-modifying--deleting-properties)
4. [Methods & The `this` Keyword](#4-methods--the-this-keyword)
5. [Pass by Reference & Cloning (Don't Mutate by Accident)](#5-pass-by-reference--cloning)
6. [Object Static Methods](#6-object-static-methods)
7. [Modern Object Superpowers](#7-modern-object-superpowers)
   - [Destructuring & Renaming](#-destructuring--renaming)
   - [Optional Chaining (`?.`)](#-optional-chaining-)
   - [Nullish Coalescing (`??`)](#-nullish-coalescing-)
8. [Classes Primer (Blueprints for Objects)](#8-classes-primer)
9. [Boss Fight Challenges](#9-boss-fight-challenges)

---

## 1. What is an Object?

An **Object** is a bundle of `key: value` pairs that describe an entity's properties (stats) and methods (actions).

```javascript
const player = {
    username: "ANIK124BD",
    rank: "Diamond",
    level: 42,
    isOnline: true,
    inventory: ["Sword", "Shield", "Health Potion"]
};
```

---

## 2. Accessing Properties: Dot vs Bracket Notation

```javascript
const car = {
    brand: "Tesla",
    "top speed": 250, // Keys with spaces need quotes
    model: "Model S"
};

// 1. Dot Notation: Quick, clean, standard
console.log(car.brand); // "Tesla"

// 2. Bracket Notation: Required when key has spaces or comes from a variable
console.log(car["top speed"]); // 250

let propertyToLookup = "model";
console.log(car[propertyToLookup]); // "Model S"
```

---

## 3. Adding, Modifying & Deleting Properties

```javascript
const pc = {
    cpu: "Ryzen 7",
    ram: "16GB"
};

// Add new property:
pc.gpu = "RTX 4070";

// Modify existing property:
pc.ram = "32GB";

// Delete a property:
delete pc.cpu;

console.log(pc); // { ram: "32GB", gpu: "RTX 4070" }
```

---

## 4. Methods & The `this` Keyword

A function stored inside an object is called a **method**.
Inside a normal method, **`this`** points to the object currently executing it.

```javascript
const streamer = {
    handle: "ANIK124BD",
    followers: 1200,
    gainFollower() {
        this.followers++;
        console.log(`${this.handle} now has ${this.followers} followers!`);
    }
};

streamer.gainFollower(); // "ANIK124BD now has 1201 followers!"
```

> [!WARNING]
> Never use **arrow functions** for object methods if you need `this`! Arrow functions don't bind their own `this`, meaning `this` will point to the outer global `window` instead of the object itself.

---

## 5. Pass by Reference & Cloning

Objects are stored by reference. Copying a variable does **not** create a new object; it just gives you a second pointer to the exact same memory address!

```javascript
let player1 = { name: "Anik", hp: 100 };
let player2 = player1; // Just copying the pointer!

player2.hp = 0;
console.log(player1.hp); // 0 (Oops! Both changed!)
```

### 🧬 How to Actually Clone an Object
```javascript
// Shallow Clone (top-level properties only):
let safeCopy = { ...player1 };

// Deep Clone (clones deeply nested objects and arrays too):
let deepCopy = structuredClone(player1); // Native modern standard!
```

---

## 6. Object Static Methods

| Method | What It Returns |
| :--- | :--- |
| `Object.keys(obj)` | Array of all property names (keys) |
| `Object.values(obj)` | Array of all property values |
| `Object.entries(obj)` | Array of nested `[key, value]` pairs |
| `Object.freeze(obj)` | Locks the object so nothing can be added, changed, or deleted |

```javascript
const stats = { kills: 14, deaths: 2, assists: 8 };

console.log(Object.keys(stats));   // ["kills", "deaths", "assists"]
console.log(Object.values(stats)); // [14, 2, 8]
console.log(Object.entries(stats));// [["kills", 14], ["deaths", 2], ["assists", 8]]
```

---

## 7. Modern Object Superpowers

### 📦 Destructuring & Renaming
Extract properties straight into variables without repetitive typing:

```javascript
const config = {
    port: 8080,
    host: "localhost",
    isSecure: true
};

// Destructure:
const { port, host } = config;

// Destructure with renaming & default value:
const { isSecure: httpsEnabled, timeout = 5000 } = config;

console.log(port);         // 8080
console.log(httpsEnabled); // true
console.log(timeout);      // 5000
```

---

### ❓ Optional Chaining (`?.`)
Prevents your entire app from crashing when checking nested properties that might be `null` or `undefined`.

```javascript
const user = {
    name: "Anik",
    contact: null
};

// Without ?.:
// console.log(user.contact.email); // ❌ TypeError: Cannot read properties of null (CRASH!)

// With ?.:
console.log(user.contact?.email); // undefined (Safe! No crash.)
```

---

### 🛡️ Nullish Coalescing (`??`)
Fallback operator that ONLY kicks in if the value is `null` or `undefined` (unlike `||`, it does NOT treat `0` or `""` as missing data).

```javascript
let currentScore = 0;

let result1 = currentScore || 10; // 10 (0 is falsy, unwanted fallback!)
let result2 = currentScore ?? 10; // 0 (0 is kept because it's a real score!)
```

---

## 8. Classes Primer

Classes are blueprints for creating multiple objects that share the same properties and methods.

```javascript
class Hero {
    constructor(name, weapon) {
        this.name = name;
        this.weapon = weapon;
    }

    attack() {
        console.log(`${this.name} strikes with ${this.weapon}!`);
    }
}

const warrior = new Hero("Knight", "Claymore");
warrior.attack(); // "Knight strikes with Claymore!"
```

---

## 9. Boss Fight Challenges

### ⚔️ Challenge 1: Shopping Cart Total
Calculate the total price of all items in a cart object array:

```javascript
const cart = [
    { name: "Mousepad", price: 20, qty: 2 },
    { name: "Keycaps", price: 35, qty: 1 }
];
```

<details>
<summary>👀 Show Solution</summary>

```javascript
const total = cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
console.log(`Total: $${total}`); // $75
```
</details>

---

### ⚔️ Challenge 2: Frequency Counter
Count how many times each tag appears in this array: `["tech", "gaming", "tech", "anime", "tech", "gaming"]`.

<details>
<summary>👀 Show Solution</summary>

```javascript
const tags = ["tech", "gaming", "tech", "anime", "tech", "gaming"];
const count = {};

for (let tag of tags) {
    count[tag] = (count[tag] || 0) + 1;
}

console.log(count); // { tech: 3, gaming: 2, anime: 1 }
```
</details>
