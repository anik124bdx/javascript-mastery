# 📖 Chapter 03: Loops & Strings

[⏮️ Prev: Chapter 02 (Operators & Conditionals)](chapter-02-operators-and-conditionals.md) • [🏠 Home (Roadmap)](../README.md) • [Next: Chapter 04 (Arrays & Methods) ⏭️](chapter-04-arrays-and-methods.md)

---

Loops allow you to repeat operations cleanly, and strings provide the foundational tools to inspect, format, and manipulate textual data.

---

## 📑 Table of Contents
1. [Loops: Don't Do It Manually](#1-loops-dont-do-it-manually)
   - [The Classic `for` Loop](#-the-classic-for-loop)
   - [The `while` Loop](#-the-while-loop)
   - [The `do-while` Loop](#-the-do-while-loop)
   - [The `for...of` Loop (The Modern Favorite)](#-the-forof-loop-the-modern-favorite)
   - [The `for...in` Loop (For Objects Only)](#-the-forin-loop-for-objects-only)
   - [`break` vs `continue`: Taking Control](#-break-vs-continue-taking-control)
   - [Infinite Loops: Instant Tab Crash](#-infinite-loops-instant-tab-crash)
2. [Strings: Handling Text Like a Pro](#2-strings-handling-text-like-a-pro)
   - [Template Literals (Backtick Superiority)](#-template-literals-backtick-superiority)
   - [Indexing & Length](#-indexing--length)
   - [Strings Are Immutable (They Don't Change In Place)](#-strings-are-immutable)
   - [The String Toolkit (Essential Methods)](#-the-string-toolkit-essential-methods)
3. [Boss Fight Challenges](#3-boss-fight-challenges)

---

## 1. Loops: Don't Do It Manually

A loop takes a block of code and repeats it until you tell it to stop.

---

### 🏎️ The Classic `for` Loop
Best when you know **exactly how many times** you want something to run.

```javascript
// for (start; stopCondition; step)
for (let i = 1; i <= 5; i++) {
    console.log(`Loot drop #${i}`);
}
// Outputs 1 through 5
```

---

### ⏳ The `while` Loop
Best when you want something to run until a condition changes, but you don't know the exact count upfront.

```javascript
let bossHealth = 100;

while (bossHealth > 0) {
    console.log(`Attacking boss! Current HP: ${bossHealth}`);
    bossHealth -= 25; // DON'T FORGET THIS or it runs forever!
}
console.log("Boss defeated!");
```

---

### 🚪 The `do-while` Loop
The wildcard. It runs the code block **at least once** before it even checks if the condition is true.

```javascript
let attempts = 0;

do {
    console.log("This will always execute at least once.");
    attempts++;
} while (attempts < 0); // Condition is already false, but it already ran!
```

---

### 🔥 The `for...of` Loop (The Modern Favorite)
The cleanest way to step through strings and arrays one item at a time without managing index numbers.

```javascript
let tech = "JAVASCRIPT";

for (let letter of tech) {
    console.log(letter);
}
// Prints each letter individually
```

---

### 🔍 The `for...in` Loop (For Objects Only)
Used to peek at the keys inside an object:

```javascript
const player = {
    tag: "ANIK124BD",
    role: "Duelist",
    level: 75
};

for (let prop in player) {
    console.log(`${prop} -> ${player[prop]}`);
}
```

---

### 🛑 `break` vs `continue`: Taking Control

- **`break`**: Hard stop. Shuts down the entire loop immediately.
- **`continue`**: Skip. Skips whatever is left of the current turn and jumps to the next one.

```javascript
// Example: Skipping the number 3
for (let i = 1; i <= 5; i++) {
    if (i === 3) {
        continue; // Skip 3!
    }
    if (i === 5) {
        break; // Stop completely at 5!
    }
    console.log(i); // Prints 1, 2, 4
}
```

---

### 💥 Infinite Loops: Instant Tab Crash
If your condition never becomes `false`, your browser will freeze and fans will spin up like a jet engine.

```javascript
// ❌ CRASH ALERT:
// let count = 1;
// while (count > 0) {
//     console.log("Never ending..."); // count never changes!
// }
```

---

## 2. Strings: Handling Text Like a Pro

### ✨ Template Literals (Backtick Superiority)

Stop chaining strings with `+` signs like it's 2008. Backticks (`` ` ``) let you embed expressions cleanly:

```javascript
let username = "ANIK124BD";
let rank = "Gold";

// Old and messy:
let oldWay = "Welcome " + username + ", your rank is " + rank + "!";

// Modern:
let cleanWay = `Welcome ${username}, your rank is ${rank}!`;
console.log(cleanWay);

// Multi-line works out of the box:
let message = `Hey team,
Servers are going down for maintenance.
Be back in 10 mins.`;
```

---

### 🎯 Indexing & Length

Strings start at index `0`.

```javascript
let tag = "CODING";

console.log(tag.length); // 6
console.log(tag[0]);     // "C" (First letter)
console.log(tag[tag.length - 1]); // "G" (Last letter shortcut!)
```

---

### 🔒 Strings Are Immutable

You cannot mutate a string character directly. JS will simply ignore it:

```javascript
let word = "Rain";
word[0] = "P"; // ❌ Does nothing!
console.log(word); // Still "Rain"

// To change it, overwrite the variable:
word = "Pain"; // ✅ Valid
```

---

### 🛠️ The String Toolkit (Essential Methods)

> [!NOTE]
> String methods **never** modify the original string; they always return a shiny new string!

| Method | What It Does | Example | Output |
| :--- | :--- | :--- | :--- |
| `.toUpperCase()` | All caps | `"hello".toUpperCase()` | `"HELLO"` |
| `.toLowerCase()` | All lowercase | `"HEY".toLowerCase()` | `"hey"` |
| `.trim()` | Cuts whitespace from both sides | `"  text  ".trim()` | `"text"` |
| `.slice(start, end)` | Cuts out a segment (end is excluded) | `"Frontend".slice(0, 5)` | `"Front"` |
| `.replace(old, new)` | Replaces the first match | `"cat dog cat".replace("cat", "owl")` | `"owl dog cat"` |
| `.replaceAll(old, new)` | Replaces every single match | `"cat dog cat".replaceAll("cat", "owl")` | `"owl dog owl"` |
| `.includes(str)` | Checks if a substring is inside | `"JavaScript".includes("Script")` | `true` |
| `.startsWith(str)` | Checks the beginning | `"https://".startsWith("https")` | `true` |
| `.endsWith(str)` | Checks the end | `"avatar.png".endsWith(".png")` | `true` |

```javascript
// Method Chaining:
let input = "   ANIK124BD   ";
let cleaned = input.trim().toLowerCase();
console.log(cleaned); // "anik124bd"
```

---

## 3. Boss Fight Challenges

### ⚔️ Challenge 1: The Auto-Handle Generator
Take a user's full name, strip out any spaces, make it all lowercase, prefix it with `@`, and tack the character count to the end.

*Example:* `"Anik Rahman"` ➔ `"@anikrahman10"`

<details>
<summary>👀 Show Solution</summary>

```javascript
let rawName = "Anik Rahman";

let noSpaces = rawName.replaceAll(" ", "").toLowerCase();
let handle = `@${noSpaces}${noSpaces.length}`;

console.log(handle); // "@anikrahman10"
```
</details>

---

### ⚔️ Challenge 2: Count the Letter "e"
Write a loop that counts how many times the letter `"e"` (case-insensitive) appears in a sentence.

<details>
<summary>👀 Show Solution</summary>

```javascript
let sentence = "Everything Everywhere All At Once";
let count = 0;

for (let char of sentence) {
    if (char.toLowerCase() === "e") {
        count++;
    }
}

console.log(`Total 'e' occurrences: ${count}`); // 7
```
</details>
