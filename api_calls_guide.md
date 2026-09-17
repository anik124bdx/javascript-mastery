# 🚀 Async JS & APIs: Fetching Data from the Outside World

Your frontend looks great, but right now it's running on hardcoded fake data. In the real world, you need to pull live stats, query user profiles from databases, and talk to external servers. That's where **Asynchronous JavaScript** and **APIs** come into play.

---

## 📑 Table of Contents
1. [Synchronous vs Asynchronous (Don't Block the Thread)](#1-synchronous-vs-asynchronous)
   - [The Event Loop Simplified](#-the-event-loop-simplified)
2. [The Progression: Callbacks ➔ Promises ➔ `async/await`](#2-the-evolution-of-async-code)
   - [Callbacks & The Pyramid of Doom](#-a-callbacks--the-pyramid-of-doom)
   - [Promises (A Guarantee for the Future)](#-b-promises)
   - [`async` / `await` (Modern Clean Code)](#-c-async--await)
3. [What is an API & JSON?](#3-what-is-an-api--json)
   - [`JSON.parse()` vs `JSON.stringify()`](#-jsonparse-vs-jsonstringify)
4. [Mastering `fetch()`](#4-mastering-fetch)
   - [GET Requests (Pulling Data)](#-get-requests)
   - [The `response.ok` Trap (Check Your Errors!)](#-the-responseok-trap)
   - [POST Requests (Sending Data)](#-post-requests)
5. [Complete Real-World Build: Live GitHub Profile Fetcher](#5-complete-real-world-build-live-github-profile-fetcher)
6. [Boss Fight Challenges](#6-boss-fight-challenges)

---

## 1. Synchronous vs Asynchronous

JavaScript is **single-threaded**—it has one brain and can only do one calculation at a time.

- **Synchronous**: Runs line-by-line. If one operation takes 5 seconds (like a heavy database query), your entire browser tab freezes until it's done.
- **Asynchronous**: Starts the slow task in the background (via the browser engine) and immediately moves on with the rest of your script. When the slow task is finished, JS handles the result.

```javascript
console.log("1. Starting engine");

setTimeout(() => {
    console.log("2. Delayed ping (after 2 seconds)");
}, 2000);

console.log("3. Ready to rumble!");

// Output order:
// 1. Starting engine
// 3. Ready to rumble!
// 2. Delayed ping (after 2 seconds)
```

---

### 🎡 The Event Loop Simplified

1. **Call Stack**: Where your active JS code runs.
2. **Web APIs**: The browser handles background work (timers, network requests).
3. **Callback Queue**: When the background work finishes, its callback waits in line here.
4. **Event Loop**: Constantly checks if the Call Stack is empty. As soon as the stack is clear, it pushes the waiting callback from the queue into the stack.

---

## 2. The Evolution of Async Code

### 💀 A. Callbacks & The Pyramid of Doom
In old JavaScript, nesting callbacks inside callbacks led to deeply indented, unreadable code:

```javascript
// ❌ Avoid this callback nightmare:
getUser(userId, (user) => {
    getPosts(user.id, (posts) => {
        getComments(posts[0].id, (comments) => {
            console.log(comments);
        });
    });
});
```

---

### 🤝 B. Promises
A **Promise** represents a task that hasn't completed yet, but promises to give you a result later.

**3 States of a Promise:**
1. `Pending`: Still working on it...
2. `Fulfilled` (`resolve`): Succeeded! Handed you the data.
3. `Rejected` (`reject`): Something blew up. Threw an error.

```javascript
const orderPizza = new Promise((resolve, reject) => {
    let ovenWorking = true;
    if (ovenWorking) {
        resolve("🍕 Hot pizza delivered!");
    } else {
        reject("❌ Oven broke down.");
    }
});

// Chaining with .then() and .catch():
orderPizza
    .then((food) => console.log(food))
    .catch((err) => console.error(err));
```

---

### ⚡ C. `async` / `await`
The modern standard. It makes asynchronous code look and feel like clean, synchronous code:

- Add `async` to declare an asynchronous function.
- Use `await` to pause execution until the promise finishes.
- Wrap everything in `try...catch` for rock-solid error handling.

```javascript
async function deliverFood() {
    try {
        const result = await orderPizza;
        console.log(result);
    } catch (err) {
        console.error("Order failed:", err);
    }
}

deliverFood();
```

---

## 3. What is an API & JSON?

- **API (Application Programming Interface)**: A waiter between your client app and the server database. You ask for data; the API delivers it.
- **JSON (JavaScript Object Notation)**: The universal text format data is wrapped in when traveling across the internet.

### 🔄 `JSON.parse()` vs `JSON.stringify()`

```javascript
const player = { username: "ANIK124BD", score: 999 };

// 1. To send across the web, stringify it into JSON text:
const jsonPayload = JSON.stringify(player);
console.log(jsonPayload); // '{"username":"ANIK124BD","score":999}'

// 2. When receiving JSON text from a server, parse it back into a JS object:
const restoredObj = JSON.parse(jsonPayload);
console.log(restoredObj.username); // "ANIK124BD"
```

---

## 4. Mastering `fetch()`

### 📥 A. GET Requests

```javascript
async function getRandomFact() {
    const URL = "https://catfact.ninja/fact";

    const response = await fetch(URL); // 1. Wait for server response
    const data = await response.json(); // 2. Parse the JSON body

    console.log("Fact:", data.fact);
}
```

---

### ⚠️ B. The `response.ok` Trap
Here's the catch: `fetch()` will **not** throw an error if the server sends back a `404 Not Found` or `500 Server Crash`. It only throws if there is no internet connection at all!

You must check `response.ok` yourself:

```javascript
async function safeFetch(url) {
    try {
        const response = await fetch(url);

        // Check if status is between 200 and 299:
        if (!response.ok) {
            throw new Error(`Server returned error: ${response.status} ${response.statusText}`);
        }

        const data = await response.json();
        return data;
    } catch (error) {
        console.error("Fetch failed:", error.message);
    }
}
```

---

### 📤 C. POST Requests

Sending new data up to a server:

```javascript
async function submitData(payload) {
    try {
        const res = await fetch("https://jsonplaceholder.typicode.com/posts", {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify(payload)
        });

        const result = await res.json();
        console.log("Saved to server:", result);
    } catch (err) {
        console.error("Post failed:", err);
    }
}

submitData({ title: "Mastering JS", body: "Coding every day!" });
```

---

## 5. Complete Real-World Build: Live GitHub Profile Fetcher

Put this in your script to pull live GitHub stats for any username:

```javascript
async function getGitHubStats(username) {
    const URL = `https://api.github.com/users/${username}`;

    try {
        console.log(`Connecting to GitHub for @${username}...`);
        const res = await fetch(URL);

        if (!res.ok) {
            if (res.status === 404) {
                throw new Error("User does not exist on GitHub!");
            }
            throw new Error(`Failed with status: ${res.status}`);
        }

        const user = await res.json();

        console.log("=== GITHUB PROFILE ===");
        console.log(`Handle: @${user.login}`);
        console.log(`Name: ${user.name || "Anonymous"}`);
        console.log(`Public Repos: ${user.public_repos}`);
        console.log(`Followers: ${user.followers}`);
        console.log(`Avatar URL: ${user.avatar_url}`);
    } catch (err) {
        console.error("Error:", err.message);
    }
}

// Test it with your handle:
getGitHubStats("ANIK124BD");
```

---

## 6. Boss Fight Challenges

### ⚔️ Challenge 1: Convert `.then()` to `async/await`
Refactor this snippet:

```javascript
function loadStatus() {
    fetch("https://api.github.com")
        .then(res => res.json())
        .then(data => console.log(data.current_user_url))
        .catch(err => console.error(err));
}
```

<details>
<summary>👀 Show Solution</summary>

```javascript
async function loadStatus() {
    try {
        const res = await fetch("https://api.github.com");
        const data = await res.json();
        console.log(data.current_user_url);
    } catch (err) {
        console.error("Failed:", err);
    }
}
```
</details>

---

### ⚔️ Challenge 2: Render Live API Data into the DOM
Hook up a button with ID `#fetch-quote-btn` so that clicking it fetches a quote from an API and inserts it into `<h3 id="quote-box"></h3>`.

<details>
<summary>👀 Show Solution</summary>

```javascript
const quoteBox = document.querySelector("#quote-box");
const fetchBtn = document.querySelector("#fetch-quote-btn");

async function displayQuote() {
    quoteBox.textContent = "Loading quote...";
    try {
        const response = await fetch("https://api.quotable.io/random");
        const data = await response.json();
        quoteBox.textContent = `"${data.content}" — ${data.author}`;
    } catch (err) {
        quoteBox.textContent = "Couldn't fetch quote. Try again!";
    }
}

fetchBtn?.addEventListener("click", displayQuote);
```
</details>
