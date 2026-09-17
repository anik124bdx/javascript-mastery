# ⚡ Operators & Conditionals: Teaching Your Code to Make Decisions

Computers are fast, but by default they are completely clueless. Operators let you do math and compare values, and conditionals let your code make decisions instead of mindlessly running down in a straight line.

---

## 📑 Table of Contents
1. [Operators: What Are We Working With?](#1-operators-what-are-we-working-with)
   - [Math Operators](#-math-operators)
   - [Quick Level-Ups: `++` and `--`](#-quick-level-ups----and---)
   - [Assignment Shortcuts](#-assignment-shortcuts)
   - [Comparison: `===` vs `==` (Avoid Heartbreak)](#-comparison-operators)
   - [Logical Operators: `&&`, `||`, `!`](#-logical-operators)
   - [The Ternary Operator: One-Line Flex](#-the-ternary-operator)
2. [Truthy vs Falsy: The Secret Test](#2-truthy-vs-falsy-the-secret-test)
3. [Conditionals: Branching Realities](#3-conditionals-branching-realities)
   - [`if` and `if-else`](#-if-and-if-else)
   - [`else-if` Ladders](#-else-if-ladders)
   - [`switch` Statements](#-switch-statements)
4. [Rookie Mistakes That Will Embarrass You](#4-rookie-mistakes-that-will-embarrass-you)
5. [Boss Fight Challenges](#5-boss-fight-challenges)

---

## 1. Operators: What Are We Working With?

### 🧮 Math Operators

| Operator | Action | Example | Result |
| :--- | :--- | :--- | :--- |
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `4 * 3` | `12` |
| `/` | Division | `20 / 4` | `5` |
| `%` | Modulo (The Remainder) | `10 % 3` | `1` |
| `**` | Exponent (Power) | `2 ** 4` (2⁴) | `16` |

> [!TIP]
> The `%` operator is your go-to whenever you need to check if a number is even or odd:
> `number % 2 === 0` ➔ Even!

---

### 🚀 Quick Level-Ups: `++` and `--`

- `num++` (Post-increment): Uses the current number first, then adds 1.
- `++num` (Pre-increment): Adds 1 first, then hands you the new number.

```javascript
let energy = 10;
console.log(energy++); // 10 (hands you 10, then bumps to 11 in the background)
console.log(energy);   // 11

let aura = 10;
console.log(++aura);   // 11 (bumps to 11 immediately!)
```

---

### ⚡ Assignment Shortcuts

Stop writing `x = x + 5`. Save your keystrokes:

```javascript
let xp = 100;

xp += 25; // xp is now 125
xp -= 10; // xp is now 115
xp *= 2;  // xp is now 230
xp /= 5;  // xp is now 46
```

---

### ⚖️ Comparison Operators

Comparison operators always return a boolean: `true` or `false`.

| Operator | Check | Example | Result |
| :--- | :--- | :--- | :--- |
| `===` | **Strict Equal** (checks value **AND** type) | `5 === "5"` | `false` ✅ (Clean!) |
| `==` | **Loose Equal** (ignores type completely) | `5 == "5"` | `true` 🚩 (Dangerous!) |
| `!==` | **Strict Not Equal** | `10 !== "10"` | `true` ✅ |
| `!=` | Loose Not Equal | `10 != "10"` | `false` 🚩 |
| `>` | Greater than | `10 > 5` | `true` |
| `<` | Less than | `3 < 2` | `false` |
| `>=` | Greater than or equal | `5 >= 5` | `true` |
| `<=` | Less than or equal | `4 <= 5` | `true` |

> [!WARNING]
> Always stick to `===` and `!==`. Using `==` lets JS do unhinged things like `"" == 0` evaluating to `true`. Don't let your code do that to you.

---

### 🧠 Logical Operators

Used to chain conditions together.

#### 1. Logical AND (`&&`)
Needs **EVERY single condition** to be `true`. If even one fails, the whole thing is `false`.
```javascript
let hasTicket = true;
let isVip = false;

console.log(hasTicket && isVip); // false
```

#### 2. Logical OR (`||`)
Only needs **ONE condition** to be `true`. It only gives up if everything is `false`.
```javascript
let hasWifi = false;
let hasMobileData = true;

console.log(hasWifi || hasMobileData); // true (we're online!)
```

#### 3. Logical NOT (`!`)
Flips the truth. Turns `true` into `false` and vice-versa.
```javascript
let isSleeping = false;
console.log(!isSleeping); // true
```

---

### 🎯 The Ternary Operator

When an `if-else` is too bulky for a simple one-liner, pull out the ternary:

```javascript
// Syntax: condition ? ifTrue : ifFalse

let battery = 12;
let status = battery < 20 ? "Low Battery" : "All Good";

console.log(status); // "Low Battery"
```

---

## 2. Truthy vs Falsy: The Secret Test

When JavaScript evaluates a value inside an `if` statement, it converts it to a boolean behind the scenes.

### The 7 Falsy Values (Everything else is Truthy!)
Memorize these seven. If it's not on this list, JS treats it as `true`:
1. `false`
2. `0` (and `-0`)
3. `""` (empty string)
4. `null`
5. `undefined`
6. `NaN`
7. `0n` (BigInt zero)

```javascript
// Empty string is falsy:
if ("") {
    console.log("Never runs");
}

// Any string with characters is truthy (even "0" or "false"):
if ("ANIK") {
    console.log("Runs every time!");
}

// Empty array or object is ALSO truthy!
if ([]) {
    console.log("Empty arrays are truthy in JS!");
}
```

---

## 3. Conditionals: Branching Realities

---

### 🚦 `if` and `if-else`

```javascript
let isFollowed = false;

if (isFollowed) {
    console.log("Showing: Following (Unfollow)");
} else {
    console.log("Showing: Follow Button");
}
```

---

### 🪜 `else-if` Ladders

For when you have multiple stages or tiers:

```javascript
let ping = 45;

if (ping < 30) {
    console.log("Connection: Flawless");
} else if (ping < 80) {
    console.log("Connection: Playable");
} else if (ping < 150) {
    console.log("Connection: Laggy");
} else {
    console.log("Connection: Disconnected");
}
```

---

### 🎛️ `switch` Statements

Great when checking one variable against a list of exact matching cases:

```javascript
let command = "start";

switch (command) {
    case "start":
        console.log("Game initiated!");
        break;
    case "pause":
        console.log("Game frozen.");
        break;
    case "exit":
        console.log("Closing game...");
        break;
    default:
        console.log("Command not recognized.");
        break;
}
```

> [!CAUTION]
> Don't forget `break;`! If you forget it, the code will fall through and execute every case underneath it regardless of whether it matches.

---

## 4. Rookie Mistakes That Will Embarrass You

### ❌ The Single Equals Trap
```javascript
let isMuted = false;

// ❌ WRONG: '=' is assignment! This forces isMuted to true and ALWAYS executes!
if (isMuted = true) {
    console.log("Always muted!");
}

// ✅ RIGHT:
if (isMuted) {
    console.log("Proper check");
}
```

### ❌ String Math Glitches
```javascript
console.log("10" + 5); // "105" (Glued together!)
console.log("10" - 5); // 5 (Did math!)
```

---

## 5. Boss Fight Challenges

### ⚔️ Challenge 1: The Toggle Switch
You have a profile object:
```javascript
const profile = {
    username: "ANIK124BD",
    followers: 10,
    isFollowed: false
};
```
Write an `if-else` block that toggles `isFollowed`. If already followed, drop followers by 1 and set to `false`. If not followed, increase followers by 1 and set to `true`.

<details>
<summary>👀 Show Solution</summary>

```javascript
if (profile.isFollowed) {
    profile.isFollowed = false;
    profile.followers--;
    console.log(`Unfollowed ${profile.username}. Total: ${profile.followers}`);
} else {
    profile.isFollowed = true;
    profile.followers++;
    console.log(`Followed ${profile.username}! Total: ${profile.followers}`);
}
```
</details>

---

### ⚔️ Challenge 2: The Bouncer Check
Check if a user is allowed into an event:
- Must be age 18 or older
- Must have either an `isVip` pass OR an `isInvited` pass
- Cannot be on the `isBanned` list

Write a single `if` statement using logical operators (`&&`, `||`, `!`).

<details>
<summary>👀 Show Solution</summary>

```javascript
let age = 20;
let isVip = false;
let isInvited = true;
let isBanned = false;

if (age >= 18 && (isVip || isInvited) && !isBanned) {
    console.log("Access Granted. Come on in!");
} else {
    console.log("Access Denied.");
}
```
</details>
