<div align="center">

# 🚀 Modern JavaScript Mastery
### *A comprehensive, step-by-step curriculum from core fundamentals to advanced concepts*

<br/>

[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![GitHub Repo](https://img.shields.io/badge/Repository-anik124bdx%2Fjavascript--mastery-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/anik124bdx/javascript-mastery)
[![Author](https://img.shields.io/badge/Curated_By-ANIK124BD-6366f1?style=for-the-badge&logo=github)](https://github.com/anik124bdx)
[![Status](https://img.shields.io/badge/Status-Active_Learning-10b981?style=for-the-badge)](README.md)

<br/>

<p align="center">
  A clean, practical, and hands-on guide designed to take you from core JavaScript fundamentals to modern frontend application architecture. Every topic includes clear explanations, syntax breakdowns, common pitfalls, and practical exercises.
</p>

</div>

---

## 🗺️ Curriculum Roadmap

Follow the modules sequentially or jump directly into any topic:

| Module | Topic | Level | Key Concepts Covered | Link |
| :---: | :--- | :---: | :--- | :---: |
| **01** | **Variables & Data Types** | `Beginner` | `let`, `const`, `var`, 7 Primitives, Objects, Arrays, `typeof`, Type Coercion | [View Guide](variables_and_datatypes_guide.md) |
| **02** | **Operators & Conditionals** | `Beginner` | Arithmetic, Strict Equality (`===`), Logical Operators, `if/else`, `switch`, Truthy/Falsy | [View Guide](operators_and_conditionals_guide.md) |
| **03** | **Loops & Strings** | `Intermediate` | `for`, `while`, `do-while`, `for...of`, `break`/`continue`, Template Literals, String Methods | [View Guide](loops_and_strings_guide.md) |
| **04** | **Arrays & Methods** | `Intermediate` | Indexing, Mutating Methods, ES6 Iterators (`map`, `filter`, `reduce`), Spread & Destructuring | [View Guide](arrays_guide.md) |
| **05** | **Functions & Scope** | `Intermediate` | Declarations vs Expressions, Arrow Functions, Rest/Default Params, Callbacks, Closures | [View Guide](functions_guide.md) |
| **06** | **Objects & OOP Basics** | `Advanced` | Dot/Bracket Access, `this` Keyword, Deep vs Shallow Copy, Object Static Methods, Classes | [View Guide](objects_guide.md) |
| **07** | **DOM & Events** | `Advanced` | `querySelector`, Content Updates, Style & `classList`, Element Creation, Event Delegation | [View Guide](dom_and_events_guide.md) |
| **08** | **Async JS & API Calls** | `Advanced` | Event Loop, Promises, `async`/`await`, JSON, HTTP Requests (`fetch`), Error Handling | [View Guide](api_calls_guide.md) |

---

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
   - Press **`F12`** or **`Ctrl + Shift + I`** in Chrome, Edge, or Firefox.
   - Switch to the **Console** tab to inspect live outputs, test expressions, and debug.

---

## 📌 Core Engineering Principles

> [!TIP]
> **Prefer `const` over `let`**: Declare variables with `const` by default. Only switch to `let` when you explicitly need reassignment. Avoid `var` entirely in modern projects.

> [!IMPORTANT]
> **Enforce Strict Equality**: Always use `===` and `!==`. Loose equality (`==`) performs implicit type conversions that often introduce unexpected bugs.

> [!WARNING]
> **Handle Network Responses Explicitly**: `fetch()` only rejects on network failures. Always verify `response.ok` or check the HTTP status code before processing payload data.

---

## 👤 Author

- **ANIK124BD** — [@anik124bdx](https://github.com/anik124bdx)

---

<div align="center">
  <sub>Modern JavaScript Mastery • Designed for clean code and structured learning.</sub>
</div>
