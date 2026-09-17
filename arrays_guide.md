# 📚 Arrays & Methods: Storing Lists Like a Senior Engineer

Arrays are the backbone of any real app. Feeds, playlists, shopping carts, follower lists—all of them are arrays under the hood. Let's make sure you're manipulating them with precision.

---

## 📑 Table of Contents
1. [What is an Array?](#1-what-is-an-array)
2. [Access & Mutability (Arrays Can Actually Change)](#2-access--mutability)
3. [The Core Arsenal](#3-the-core-arsenal)
   - [Push, Pop, Shift, Unshift](#-push-pop-shift-unshift)
   - [`slice` vs `splice` (Don't Get These Confused)](#-slice-vs-splice)
   - [Searching & Converting to Strings](#-searching--converting)
4. [The Holy Trinity: `map`, `filter`, `reduce`](#4-the-holy-trinity-map-filter-reduce)
   - [`.map()`: Transform Every Single Item](#-map-transform-every-item)
   - [`.filter()`: Drop the Garbage](#-filter-drop-the-garbage)
   - [`.reduce()`: Boil It All Down to One Value](#-reduce-boil-it-all-down)
   - [`.find()` and `.findIndex()`](#-find-and-findindex)
5. [The Spread Operator (`...`) & Destructuring](#5-spread-operator----destructuring)
6. [Boss Fight Challenges](#6-boss-fight-challenges)

---

## 1. What is an Array?

An **array** is an ordered list. In JavaScript, arrays can hold any mix of data: strings, numbers, objects, booleans, and even other arrays.

```javascript
const inventory = ["Potion", 3, true, { type: "Legendary" }];
```

---

## 2. Access & Mutability

Arrays are **0-indexed**. The first element is `0`.

```javascript
const squad = ["Anik", "Rahim", "Karim"];

console.log(squad[0]); // "Anik"
console.log(squad.length); // 3

// Quick trick to grab the last item:
console.log(squad[squad.length - 1]); // "Karim"
```

Unlike strings, **arrays are mutable in place**:

```javascript
squad[1] = "Tanvir";
console.log(squad); // ["Anik", "Tanvir", "Karim"]
```

> [!NOTE]
> Even if you declare an array with `const`, you can still add, remove, and change the items inside! `const` only stops you from overwriting the variable name with a completely new array (`squad = [1, 2]` ❌).

---

## 3. The Core Arsenal

### 🎯 Push, Pop, Shift, Unshift

```
               unshift(item)  ┌──────────────────┐  push(item)
   Adds to Front ───────────► │                  │ ◄─────────── Adds to Back
                              │      ARRAY       │
 Removes from Front ◄──────── │                  │ ───────────► Removes from Back
                shift()       └──────────────────┘   pop()
```

```javascript
let queue = ["Player1", "Player2"];

// Add to the end:
queue.push("Player3"); // ["Player1", "Player2", "Player3"]

// Remove from the end:
let kicked = queue.pop(); // kicked = "Player3"

// Add to the front:
queue.unshift("VIP_Player"); // ["VIP_Player", "Player1", "Player2"]

// Remove from the front:
queue.shift(); // removes "VIP_Player"
```

---

### ✂️ `slice` vs `splice`

One of the most famous interview questions:

| Method | Mutates the original array? | What it does |
| :--- | :---: | :--- |
| **`.slice(start, end)`** | ❌ **No** | Makes a clean cut and hands you a copy. Original is untouched. |
| **`.splice(start, count, ...add)`** | ✅ **Yes** | Reaches in, cuts out items, and can inject new items in place. |

```javascript
let games = ["Valorant", "CS2", "Apex", "Overwatch", "Fortnite"];

// slice(start, endExclusive)
let favorites = games.slice(0, 2);
console.log(favorites); // ["Valorant", "CS2"]
console.log(games);     // Original is 100% untouched!

// splice(start, howManyToDelete, ...itemsToInsert)
// Delete 1 item at index 2 ("Apex") and insert "Minecraft"
games.splice(2, 1, "Minecraft");
console.log(games); // ["Valorant", "CS2", "Minecraft", "Overwatch", "Fortnite"]
```

---

### 🔎 Searching & Converting

```javascript
const badges = ["Gold", "Silver", "Bronze"];

console.log(badges.includes("Gold"));   // true
console.log(badges.indexOf("Bronze"));  // 2
console.log(badges.indexOf("Diamond")); // -1 (not found!)

// Turn array into a string:
console.log(badges.join(" | ")); // "Gold | Silver | Bronze"
```

---

## 4. The Holy Trinity: `map`, `filter`, `reduce`

Once you master these three, you will never write a messy loop over an array again.

### 🌟 `.map()`: Transform Every Item
Loops through every element, applies a function to it, and **returns a brand new array**.

```javascript
const prices = [10, 25, 50];

// Double every price:
const doubled = prices.map((price) => price * 2);

console.log(doubled); // [20, 50, 100]
```

---

### 🛡️ `.filter()`: Drop the Garbage
Runs a condition on every item and **only keeps the ones that return `true`**.

```javascript
const scores = [88, 42, 95, 33, 75];

// Keep only passing scores (60 and up):
const passed = scores.filter((score) => score >= 60);

console.log(passed); // [88, 95, 75]
```

---

### 🧱 `.reduce()`: Boil It All Down
Takes an entire array and reduces it down into a **single value** (like a sum, average, or single object).

```javascript
const cart = [15, 30, 45, 10];

// array.reduce((accumulator, currentItem) => ..., startValue)
const total = cart.reduce((acc, price) => acc + price, 0);

console.log(`Cart total: $${total}`); // $100
```

---

### 🎯 `.find()` & `.findIndex()`

```javascript
const members = [
    { id: 101, user: "Anik" },
    { id: 102, user: "Rahman" }
];

// Returns the first item that matches:
const match = members.find((m) => m.id === 101);
console.log(match); // { id: 101, user: "Anik" }
```

---

## 5. Spread Operator (`...`) & Destructuring

### Unpacking with Spread (`...`)
```javascript
const frontEnd = ["HTML", "CSS", "JS"];
const backEnd = ["Node", "Express", "Mongo"];

// Merge arrays without awkward concat:
const fullStack = [...frontEnd, ...backEnd];

// Clone an array safely without sharing references:
const copy = [...frontEnd];
```

### Destructuring: Unpack directly into variables
```javascript
const scores = [100, 85, 70];

const [firstPlace, secondPlace, thirdPlace] = scores;
console.log(firstPlace);  // 100
console.log(secondPlace); // 85
```

---

## 6. Boss Fight Challenges

### ⚔️ Challenge 1: Flash Sale (20% Off Everything)
Given an array of item prices: `[150, 400, 25, 80]`, use `.map()` to create a new array with a 20% discount applied to each.

<details>
<summary>👀 Show Solution</summary>

```javascript
const prices = [150, 400, 25, 80];

const discounted = prices.map(price => price * 0.80);
console.log(discounted); // [120, 320, 20, 64]
```
</details>

---

### ⚔️ Challenge 2: Find the Highest Value with `.reduce()`
Given `[12, 85, 4, 99, 53]`, use `.reduce()` to find the maximum number.

<details>
<summary>👀 Show Solution</summary>

```javascript
const nums = [12, 85, 4, 99, 53];

const highest = nums.reduce((max, current) => {
    return current > max ? current : max;
}, nums[0]);

console.log(highest); // 99
```
</details>
