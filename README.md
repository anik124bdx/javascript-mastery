<div align="center">

# 🚀 Modern JavaScript Mastery
### *A comprehensive, step-by-step curriculum from core fundamentals to advanced concepts*

<br/>

[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Author](https://img.shields.io/badge/Curated_By-ANIK124BD-6366f1?style=for-the-badge&logo=github)](https://github.com/anik124bdx)
[![Status](https://img.shields.io/badge/Status-Active_Learning-10b981?style=for-the-badge)](README.md)

<br/>

<p align="center">
  A clean, practical, and hands-on guide designed to take you from core JavaScript fundamentals to modern frontend application architecture. Every topic includes clear explanations, syntax breakdowns, common pitfalls, and practical exercises.
</p>

</div>

## 🗺️ Chapter Roadmap

Follow the chapters in order or jump directly to what you're working on:

| Chapter | Topic | Level | Key Concepts Covered | Link |
| :---: | :--- | :---: | :--- | :---: |
| **01** | **Variables & Data Types** | `Beginner` | `let`, `const`, `var`, 7 Primitives, Objects, Arrays, `typeof`, Type Coercion | [Open Chapter 1](chapters/chapter-01-variables-and-datatypes.md) |
| **02** | **Operators & Conditionals** | `Beginner` | Arithmetic, Strict Equality (`===`), Logical Operators, `if/else`, `switch`, Truthy/Falsy | [Open Chapter 2](chapters/chapter-02-operators-and-conditionals.md) |
| **03** | **Loops & Strings** | `Intermediate` | `for`, `while`, `do-while`, `for...of`, `break`/`continue`, Template Literals, String Methods | [Open Chapter 3](chapters/chapter-03-loops-and-strings.md) |
| **04** | **Arrays & Methods** | `Intermediate` | Indexing, Mutating Methods, ES6 Iterators (`map`, `filter`, `reduce`), Spread & Destructuring | [Open Chapter 4](chapters/chapter-04-arrays-and-methods.md) |
| **05** | **Functions & Scope** | `Intermediate` | Declarations vs Expressions, Arrow Functions, Rest/Default Params, Callbacks, Closures | [Open Chapter 5](chapters/chapter-05-functions-and-scope.md) |
| **06** | **Objects & OOP Basics** | `Advanced` | Dot/Bracket Access, `this` Keyword, Deep vs Shallow Copy, Object Static Methods, Classes | [Open Chapter 6](chapters/chapter-06-objects-and-oop.md) |
| **07** | **DOM & Events** | `Advanced` | `querySelector`, Content Updates, Style & `classList`, Element Creation, Event Delegation | [Open Chapter 7](chapters/chapter-07-dom-and-events.md) |
| **08** | **Async JS & API Calls** | `Advanced` | Event Loop, Promises, `async`/`await`, JSON, HTTP Requests (`fetch`), Error Handling | [Open Chapter 8](chapters/chapter-08-async-js-and-apis.md) |

## 💻 Getting Started Locally

To run and experiment with the code examples:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/anik124bdx/javascript-mastery.git
   cd javascript-mastery
   ```

2. **Run with an HTML entry point:**
   Create an `index.html` file and link your script:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>JavaScript Mastery</title>
   </head>
   <body>
       <h1>Open the DevTools Console (F12)</h1>
       <script src="script.js"></script>
   </body>
   </html>
   ```

3. **Open Developer Tools:**
   - Press **`F12`** or **`Ctrl + Shift + I`** in your browser.
   - Switch to the **Console** tab to inspect live outputs and test code.

## 📌 Core Engineering Principles

| Principle | Recommendation |
| :--- | :--- |
| **Prefer `const` over `let`** | Declare variables with `const` by default. Only use `let` when reassignment is required, and avoid `var` entirely. |
| **Enforce Strict Equality** | Always use `===` and `!==`. Loose equality (`==`) performs implicit type conversions that cause unexpected bugs. |
| **Verify Network Responses** | Always check `response.ok` when calling `fetch()` because it does not reject on 4xx or 5xx HTTP errors. |

<br/>

<div align="center">
  <sub>Curated by <b><a href="https://github.com/anik124bdx">ANIK124BD</a></b> • Modern JavaScript Mastery</sub>
</div>
