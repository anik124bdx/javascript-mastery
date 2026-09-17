# 📦 Variables & Data Types: Storing Your Data Without Looking Clueless

Before you can build anything insane, you gotta understand how JavaScript holds onto information. Variables are just memory boxes with labels on them. Let's make sure you're using the right ones.

---

## 📑 Table of Contents
1. [The Holy Trinity: `var` vs `let` vs `const`](#1-the-holy-trinity-var-vs-let-vs-const)
   - [Why `var` is an Immediate Red Flag](#-why-var-is-an-immediate-red-flag)
   - [Scope Check: Who Can See What?](#-scope-check-who-can-see-what)
   - [The Cheat Sheet](#-the-cheat-sheet)
2. [Naming Things (Without Causing Chaos)](#2-naming-things-without-causing-chaos)
3. [Data Types: What Can You Actually Store?](#3-data-types-what-can-you-actually-store)
   - [Primitives: Stored by Value](#-primitives-stored-by-value-the-immutables)
   - [Non-Primitives: Stored by Reference](#-non-primitives-stored-by-reference-the-mutables)
4. [The `typeof` Operator (And That One 1995 Glitch)](#4-the-typeof-operator-and-that-one-1995-glitch)
5. [Type Coercion: When JS Tries to Help (And Fails)](#5-type-coercion-when-js-tries-to-help-and-fails)
6. [Passing by Value vs Passing by Reference](#6-passing-by-value-vs-passing-by-reference)
7. [Boss Fight Challenges](#7-boss-fight-challenges)

---

## 1. The Holy Trinity: `var` vs `let` vs `const`

Back in the day (pre-2015), developers only had `var`. It was chaotic. Then ES6 dropped `let` and `const` to save everyone's sanity.

### 🚩 Why `var` is an Immediate Red Flag

1. **You can re-declare it accidentally and JS won't even warn you:**
   ```javascript
   var salary = 50000;
   // 300 lines of code later...
   var salary = 0; // Oops, overwritten without any warning!
   ```
2. **It leaks out of blocks:**
   `var` ignores curly braces `{}` inside `if` statements and loops. It just escapes into the wild.

---

### 🔍 Scope Check: Who Can See What?

- **Global Scope**: Everyone can access it.
- **Function Scope**: Locked inside a function.
- **Block Scope**: Trapped between `{}` (like inside an `if` block or a loop).

```javascript
{
    let lockedLet = "Trapped in here";
    const lockedConst = "Also trapped";
    var sneakyVar = "I snuck out lol";
}

// console.log(lockedLet);   // ❌ ReferenceError (safely trapped)
// console.log(lockedConst); // ❌ ReferenceError (safely trapped)
console.log(sneakyVar);      // ⚠️ "I snuck out lol" (Leaked out!)
```

---

### 📊 The Cheat Sheet

| Keyword | Re-assignable? | Re-declarable? | Block Scoped? | When to use |
| :--- | :---: | :---: | :---: | :--- |
| `const` | ❌ No | ❌ No | ✅ Yes | **Your default choice.** Use 90% of the time. |
| `let` | ✅ Yes | ❌ No | ✅ Yes | When you **know** the value will change (loops, counters). |
| `var` | ✅ Yes | ✅ Yes | ❌ No | **Never.** Delete it from your vocabulary. |

```javascript
const birthYear = 2004;
// birthYear = 2005; // ❌ TypeError: Assignment to constant variable

let followers = 120;
followers = 121; // ✅ Totally fine
```

> [!NOTE]
> `const` locks the **binding**, not the insides! If you put an object or array in a `const`, you can still modify the contents inside:
> ```javascript
> const user = { name: "Anik" };
> user.name = "Rahman"; // ✅ Legal!
> // user = { name: "Someone Else" }; // ❌ ILLEGAL (can't reassign the whole variable)
> ```

---

## 2. Naming Things (Without Causing Chaos)

Don't name variables like a villain (`x`, `data2`, `temp_final_v3_reallyfinal`).

- **Use camelCase**: `isUserLoggedIn`, `totalCartPrice`, `followerCount`.
- **Can start with**: letters, `_`, or `$`.
- **Cannot start with**: numbers (`let 1stPlace = 1;` ❌).
- **Reserved words**: Don't use words JS already owns (`let`, `class`, `function`).

---

## 3. Data Types: What Can You Actually Store?

JavaScript handles types dynamically—meaning you don't declare whether something is a number or string; JS figures it out at runtime.

---

### 🧱 Primitives (Stored by Value, Immutable)

There are 7 primitive types. When you assign them, JS makes an independent copy of the actual value.

#### 1. Number
Integers, floats, negative numbers, decimals—all just `number`.
```javascript
let balance = 1500.75;
let temp = -5;
let infinity = Infinity;
let notANumber = NaN; // Happens when math goes horribly wrong, e.g. "abc" / 2
```

#### 2. BigInt
When numbers get ridiculously huge beyond $2^{53} - 1$:
```javascript
let superHuge = 9007199254740991123456789n; // ends with 'n'
```

#### 3. String
Text data wrapped in quotes or backticks.
```javascript
let single = 'Single quote';
let double = "Double quote";

// Template literals (backticks) let you plug in variables directly:
let user = "ANIK124BD";
let welcome = `What's good, ${user}! You have ${3 + 2} unread pings.`;
```

#### 4. Boolean
Just two states. Pure truth or pure cap.
```javascript
let hasWifi = true;
let isBroke = false;
```

#### 5. Undefined
A variable was declared, but nobody gave it a value yet. JS is just waiting.
```javascript
let mysteryBox;
console.log(mysteryBox); // undefined
```

#### 6. Null
Intentional emptiness. You are explicitly saying: "there is nothing here right now."
```javascript
let currentRelationship = null; // deliberately set to empty
```

#### 7. Symbol
Guaranteed 100% unique identifier, even if they have the exact same label.
```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");
console.log(id1 === id2); // false (never equal!)
```

---

### 📦 Non-Primitives (Stored by Reference, Mutable)

These hold complex structures. The variable doesn't hold the actual data—it holds a pointer (address) to where that data lives in memory.

#### 1. Object
Key-value pairs representing an entity:
```javascript
const gamer = {
    handle: "ANIK124BD",
    rank: "Immortal",
    hoursPlayed: 450
};
```

#### 2. Array
An ordered list of items:
```javascript
const playlist = ["Song A", "Song B", "Song C"];
```

#### 3. Function
Callable blocks of logic:
```javascript
const ping = () => "Pong!";
```

---

## 4. The `typeof` Operator (And That One 1995 Glitch)

Use `typeof` to inspect what you're dealing with:

```javascript
console.log(typeof 42);          // "number"
console.log(typeof "hello");     // "string"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof { a: 1 });    // "object"
console.log(typeof [1, 2, 3]);   // "object" (Arrays are objects under the hood!)
console.log(typeof (() => {}));  // "function"
```

> [!WARNING]
> ```javascript
> console.log(typeof null); // "object" 💀
> ```
> `null` is a primitive, NOT an object. This is a bug from the first release of JavaScript in 1995. It was never fixed because fixing it would break legacy sites across the entire internet. It lives rent-free in the engine forever.

---

## 5. Type Coercion: When JS Tries to Help (And Fails)

JS tries to be smart and auto-convert types behind your back. Sometimes it's hilarious; sometimes it causes bugs.

```javascript
console.log("5" + 2);   // "52" (number got turned into text and glued together)
console.log("5" - 2);   // 3    (string got converted into a number!)
console.log("10" * "2");// 20   (both became numbers)
console.log(true + 1);  // 2    (true becomes 1)
console.log(false + 1); // 1    (false becomes 0)
```

### The Move: Explicit Conversion (Do it on purpose)
```javascript
let strScore = "450";

let numScore = Number(strScore); // 450 (as a real number)
let backToString = String(numScore); // "450"
let isNonZero = Boolean(numScore); // true
```

---

## 6. Passing by Value vs Passing by Reference

This trips up almost everyone when starting out.

### Primitives copy the actual value:
```javascript
let a = 10;
let b = a; // b gets its own copy of 10
b = 99;

console.log(a); // 10 (untouched, unaffected)
console.log(b); // 99
```

### Objects share the same reference (memory address):
```javascript
let profile1 = { name: "Anik" };
let profile2 = profile1; // profile2 points to the EXACT SAME object

profile2.name = "Ghost";

console.log(profile1.name); // "Ghost" (Both changed because they share 1 brain!)
```

To make an actual independent clone:
```javascript
let safeClone = { ...profile1 }; // shallow clone
let deepClone = structuredClone(profile1); // full deep clone
```

---

## 7. Boss Fight Challenges

### ⚔️ Challenge 1: Predict the Output
Without peeking, what does each log print?
```javascript
console.log(typeof NaN);
console.log(NaN === NaN);
console.log(typeof (1 + "1"));
console.log(typeof (1 - "1"));
```

<details>
<summary>👀 Show Answers</summary>

```javascript
// 1. "number" (NaN literally means "Not-a-Number", but its data type is number lol)
// 2. false (NaN is the only value in JS that isn't even equal to itself)
// 3. "string" ("11")
// 4. "number" (0)
```
</details>

---

### ⚔️ Challenge 2: Fix the Broken Profile
You want a user object where settings can be toggled, but the user ID can never be reassigned or modified.

```javascript
// Fix this setup:
var userID = "USR_9921";
var userSettings = { darkMode: true };

// Try changing them properly
```

<details>
<summary>👀 Show Solution</summary>

```javascript
const USER_ID = "USR_9921"; // Never changes, locked with const
const userSettings = { darkMode: true }; // Reference locked, properties editable

// Toggle setting:
userSettings.darkMode = false; // ✅ Works!
// USER_ID = "USR_0000"; // ❌ Throws error immediately!
```
</details>
