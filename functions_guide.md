# ⚡ Functions & Scope: Reusable Logic Without Copy-Pasting

If code was cooking, functions are your recipes. Instead of writing 20 lines of repetitive logic every time a user logs in, likes a post, or buys an item, you write it once, wrap it in a function, and call it whenever you need it.

---

## 📑 Table of Contents
1. [The Anatomy of a Function](#1-the-anatomy-of-a-function)
2. [3 Ways to Write Functions](#2-3-ways-to-write-functions)
   - [Function Declaration (The Classic)](#-a-function-declaration)
   - [Function Expression (Assigned to a Variable)](#-b-function-expression)
   - [Arrow Functions (The Clean Modern Way)](#-c-arrow-functions)
3. [Parameters vs Arguments](#3-parameters-vs-arguments)
   - [Default Parameters](#-default-parameters)
   - [Rest Parameters: Catching Everything (`...args`)](#-rest-parameters-args)
4. [The `return` Statement & Early Exits](#4-the-return-statement--early-exits)
5. [Callbacks & Higher-Order Functions](#5-callbacks--higher-order-functions)
6. [Closures: When Functions Remember Their Past](#6-closures-when-functions-remember-their-past)
7. [Boss Fight Challenges](#7-boss-fight-challenges)

---

## 1. The Anatomy of a Function

```javascript
// Defining the function:
function levelUp(user, currentLevel) {
    console.log(`Congrats ${user}! You just reached Level ${currentLevel + 1}!`);
}

// Calling (invoking) it:
levelUp("ANIK124BD", 4);
```

---

## 2. 3 Ways to Write Functions

### 📜 A. Function Declaration
Hoisted completely to the top of the file. You can call it before it’s even declared in the code!

```javascript
greet("Anik"); // ✅ Works even though the code is written below!

function greet(name) {
    console.log(`Hey ${name}!`);
}
```

---

### 📦 B. Function Expression
Assigning an anonymous function directly to a variable. Not hoisted.

```javascript
const add = function(a, b) {
    return a + b;
};

console.log(add(5, 10)); // 15
```

---

### 🏹 C. Arrow Functions
The sleek ES6 syntax. If your function only does one thing, you don't even need curly braces or a `return` keyword!

```javascript
// Full syntax:
const calculateTax = (price) => {
    return price * 0.15;
};

// One-liner with implicit return:
const double = (x) => x * 2;

// Single parameter doesn't even need parentheses:
const square = n => n * n;

console.log(double(21)); // 42
```

> [!NOTE]
> Arrow functions do **not** have their own `this` keyword. They inherit `this` from the code surrounding them. Keep that in mind when working inside objects!

---

## 3. Parameters vs Arguments

- **Parameter**: The label you define in the function signature.
- **Argument**: The actual real data you pass in when calling it.

```javascript
function sendPing(receiver, priority) { // receiver & priority are parameters
    console.log(`Sending ping to ${receiver} with priority ${priority}`);
}

sendPing("Server_1", "High"); // "Server_1" and "High" are arguments
```

---

### 🛟 Default Parameters
Provide fallback values so your code doesn't explode when someone forgets an argument:

```javascript
function createProfile(name, role = "Member") {
    console.log(`User: ${name} | Role: ${role}`);
}

createProfile("Anik"); // "User: Anik | Role: Member" (Used fallback!)
createProfile("Rahman", "Admin"); // "User: Rahman | Role: Admin"
```

---

### 🎣 Rest Parameters (`...args`)
Collect an unlimited number of arguments into an array:

```javascript
function sumTotal(...numbers) {
    return numbers.reduce((acc, curr) => acc + curr, 0);
}

console.log(sumTotal(10, 20));          // 30
console.log(sumTotal(5, 10, 15, 20, 25)); // 75
```

---

## 4. The `return` Statement & Early Exits

When a function hits a `return`, it stops executing **immediately**. Anything underneath it is dead code.

Use this pattern for **early exits** (guard clauses) to avoid messy nested `if` statements:

```javascript
function verifyAccess(age, hasTicket) {
    // Guard Clause 1:
    if (age < 18) {
        return "Too young!";
    }

    // Guard Clause 2:
    if (!hasTicket) {
        return "No ticket!";
    }

    // Happy path:
    return "Welcome in!";
}
```

---

## 5. Callbacks & Higher-Order Functions

In JavaScript, functions are **first-class citizens**. That means you can pass a function into another function just like a regular variable!

- A function passed as an argument is a **Callback**.
- A function that accepts another function is a **Higher-Order Function**.

```javascript
function downloadFile(filename, onComplete) {
    console.log(`Downloading ${filename}...`);
    // Simulated finish:
    onComplete(filename);
}

downloadFile("game_update.zip", (file) => {
    console.log(`${file} installed and ready to play!`);
});
```

---

## 6. Closures: When Functions Remember Their Past

A **closure** happens when an inner function remembers variables from its outer function, even after that outer function has already finished running.

Think of it like a backpack the inner function carries around with the variables inside it:

```javascript
function makeVault() {
    let secretCode = "8821"; // Private variable trapped inside!

    return {
        checkCode(input) {
            return input === secretCode ? "Access Granted" : "Wrong Code";
        }
    };
}

const vault = makeVault();
// You can't access secretCode directly:
console.log(vault.secretCode); // undefined

// But the inner function still remembers it:
console.log(vault.checkCode("0000")); // "Wrong Code"
console.log(vault.checkCode("8821")); // "Access Granted"
```

---

## 7. Boss Fight Challenges

### ⚔️ Challenge 1: Arrow Function Vowel Counter
Write an arrow function `countVowels(text)` that returns how many vowels are inside any string.

<details>
<summary>👀 Show Solution</summary>

```javascript
const countVowels = (text) => {
    const vowels = "aeiouAEIOU";
    let count = 0;
    for (let char of text) {
        if (vowels.includes(char)) count++;
    }
    return count;
};

console.log(countVowels("JavaScript")); // 3
```
</details>

---

### ⚔️ Challenge 2: The Multiplier Factory (Closure Practice)
Create a function `createMultiplier(factor)` that returns a new function multiplying any number given to it by that factor.

<details>
<summary>👀 Show Solution</summary>

```javascript
function createMultiplier(factor) {
    return (number) => number * factor;
}

const triple = createMultiplier(3);
console.log(triple(10)); // 30
console.log(triple(7));  // 21
```
</details>
