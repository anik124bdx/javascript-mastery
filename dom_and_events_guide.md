# 🌐 DOM & Events: Making Your Web Pages Actually Do Stuff

HTML is the skeleton, CSS is the drip, but JavaScript is the nervous system. Without the **DOM (Document Object Model)**, your web page is just a static picture. With it, you can respond to clicks, create animations, build dark mode toggles, and craft full web apps.

---

## 📑 Table of Contents
1. [What is the DOM?](#1-what-is-the-dom)
2. [Targeting Elements (Selectors That Actually Work)](#2-targeting-elements)
3. [Changing Text & HTML](#3-changing-text--html)
4. [Styling & The Power of `classList`](#4-styling--the-power-of-classlist)
5. [Spawning & Destroying Elements](#5-spawning--destroying-elements)
6. [Events: Listening for User Actions](#6-events-listening-for-user-actions)
   - [Event Listeners](#-event-listeners)
   - [The Event Object (`e`) & `preventDefault()`](#-the-event-object-e)
   - [Event Bubbling & Event Delegation](#-event-bubbling--event-delegation)
7. [Hands-On Builds (Interactive Counter & Dark Mode)](#7-hands-on-builds)

---

## 1. What is the DOM?

When a browser reads your HTML file, it translates it into a giant, living tree of JavaScript objects called the **Document Object Model**.

```
                  window (The Browser Tab)
                          │
                       document (The Web Page)
                          │
                        <html>
                    ┌─────┴─────┐
                 <head>       <body>
                   │            │
                <title>      <nav>, <h1>, <button>
```

Through the `document` object, JavaScript can inspect, rewrite, add, or delete any element on the screen in real-time.

---

## 2. Targeting Elements

Forget outdated methods like `getElementsByTagName`. Modern JS uses the exact same selectors you already know from CSS:

| Selector | What It Grabs | What It Returns |
| :--- | :--- | :--- |
| `document.querySelector(".card")` | Grabs the **first** element that matches | Single DOM Element (or `null`) |
| `document.querySelectorAll(".card")` | Grabs **every single** element that matches | NodeList (can loop with `.forEach`) |
| `document.getElementById("btn")` | Fast lookup by unique ID | Single DOM Element |

```javascript
const heading = document.querySelector("#title");
const primaryBtn = document.querySelector(".btn-action");
const allCards = document.querySelectorAll(".card");

allCards.forEach((card) => {
    card.style.opacity = "0.9";
});
```

---

## 3. Changing Text & HTML

```javascript
const banner = document.querySelector(".banner");

// 1. innerText: Changes visible text (respects CSS hidden/shown rules)
banner.innerText = "New Drop Coming Soon!";

// 2. textContent: Raw text content (faster, best for plain text)
banner.textContent = "Flash Sale Live!";

// 3. innerHTML: Actually renders HTML elements inside
banner.innerHTML = "<strong>CRITICAL:</strong> System update starting.";
```

> [!CAUTION]
> Never insert untrusted user input directly into `.innerHTML`! If someone types `<script>maliciousCode()</script>`, it could run on your page (XSS Attack). For plain user text, always stick to `.textContent`.

---

## 4. Styling & The Power of `classList`

### 🎨 Changing Inline Styles Directly
```javascript
const badge = document.querySelector(".badge");

// CSS property names become camelCase:
badge.style.backgroundColor = "#6366f1";
badge.style.color = "#ffffff";
badge.style.padding = "8px 16px";
```

### 🏷️ The Clean Way: Toggling Classes with `classList`
Keep all your styling in CSS classes, and let JavaScript just turn them on and off:

```javascript
const modal = document.querySelector(".modal");

modal.classList.add("active");       // Adds the class
modal.classList.remove("hidden");    // Removes the class
modal.classList.toggle("dark-mode"); // Flips it: adds if missing, removes if present!
console.log(modal.classList.contains("active")); // true or false
```

---

## 5. Spawning & Destroying Elements

```javascript
// 1. Create a brand new element in memory:
const newNotification = document.createElement("div");
newNotification.textContent = "You've got a new follower!";
newNotification.classList.add("toast-alert");

// 2. Insert it into the actual page:
const feed = document.querySelector("#feed");
feed.append(newNotification);   // Sticks it to the bottom
// feed.prepend(newNotification); // Sticks it to the very top!

// 3. Delete an element:
newNotification.remove();
```

---

## 6. Events: Listening for User Actions

An **event** happens whenever something occurs on the page: a click, mouse hover, key press, page scroll, or form submit.

### 🔔 Event Listeners
The gold standard for handling user interaction:

```javascript
const followBtn = document.querySelector("#follow-btn");

followBtn.addEventListener("click", () => {
    console.log("Follow button clicked!");
});
```

---

### 📦 The Event Object (`e`) & `preventDefault()`
When an event fires, JS automatically passes an object `e` packed with details:

```javascript
const loginForm = document.querySelector("#login-form");

loginForm.addEventListener("submit", (e) => {
    // Stop the browser from refreshing the page automatically:
    e.preventDefault();

    console.log("Form intercepted by JS. No page reload!");
});
```

---

### 🫧 Event Bubbling & Event Delegation

- **Bubbling**: When you click a child button, the click event triggers on the button, then bubbles up to its parent `<div>`, then `<section>`, then `<body>`.
- **Event Delegation**: Instead of putting 50 click listeners on 50 separate list items, put **ONE listener on the parent container**:

```javascript
const messageList = document.querySelector("#message-container");

messageList.addEventListener("click", (e) => {
    // Check if the actual thing clicked was a delete button:
    if (e.target.classList.contains("delete-btn")) {
        e.target.parentElement.remove(); // Delete that message card!
    }
});
```

---

## 7. Hands-On Builds

### 🎯 Build 1: The Interactive Counter

#### HTML:
```html
<div class="counter-card">
    <h1 id="count-val">0</h1>
    <div class="btn-group">
        <button id="minus-btn">-</button>
        <button id="reset-btn">Reset</button>
        <button id="plus-btn">+</button>
    </div>
</div>
```

#### JavaScript:
```javascript
let count = 0;
const countDisplay = document.querySelector("#count-val");
const plusBtn = document.querySelector("#plus-btn");
const minusBtn = document.querySelector("#minus-btn");
const resetBtn = document.querySelector("#reset-btn");

function updateUI() {
    countDisplay.textContent = count;
    countDisplay.style.color = count > 0 ? "#10b981" : count < 0 ? "#ef4444" : "#1e293b";
}

plusBtn.addEventListener("click", () => {
    count++;
    updateUI();
});

minusBtn.addEventListener("click", () => {
    count--;
    updateUI();
});

resetBtn.addEventListener("click", () => {
    count = 0;
    updateUI();
});
```

---

### 🎯 Build 2: Instant Theme Switcher
```javascript
const themeToggle = document.querySelector("#theme-toggle");

themeToggle.addEventListener("click", () => {
    document.body.classList.toggle("dark");
});
```
