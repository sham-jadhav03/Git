# Phase 5 — Asynchronous JavaScript

**Goal:** Master async code. Understand the event loop. Stop being afraid of `async`/`await`.

---

## Synchronous vs Asynchronous

| Synchronous | Asynchronous |
|-------------|--------------|
| Blocks execution | Non-blocking |
| Line by line | Delegates + continues |
| `console.log(1); console.log(2);` | `setTimeout(() => console.log(1), 0); console.log(2);` |
| Predictable order | Order depends on timing |

---

## Callbacks

### `setTimeout` & `setInterval`

```jsx
// Runs once after delay
const timeoutId = setTimeout(() => {
    console.log("Runs after 1 second");
}, 1000);

// Runs repeatedly
const intervalId = setInterval(() => {
    console.log("Every 2 seconds");
}, 2000);

// Cancel
clearTimeout(timeoutId);
clearInterval(intervalId);
```

### Callback Patterns

```jsx
// Node-style (error-first)
function readFile(filename, callback) {
    // ... async work
    if (error) callback(error, null);
    else callback(null, data);
}

readFile("data.txt", (err, data) => {
    if (err) return console.error(err);
    console.log(data);
});
```

### Callback Hell (Pyramid of Doom)

```jsx
getData(a, (a) => {
    getData(b, (b) => {
        getData(c, (c) => {
            getData(d, (d) => {
                // Deep nesting — hard to read, hard to handle errors
            });
        });
    });
});
```

---

## Promises

### What is a Promise?

A **Promise** represents a value that may be available now, later, or never.

```
┌─────────────────────────────────────────────┐
│              PENDING                        │
│  (initial state, waiting for result)        │
└──────────────┬──────────────────────────────┘
               │
       ┌───────┴───────┐
       ▼               ▼
┌─────────────┐  ┌─────────────┐
│  FULFILLED  │  │  REJECTED   │
│  (success)  │  │  (failure)  │
└─────────────┘  └─────────────┘
```

### Creating Promises

```jsx
const promise = new Promise((resolve, reject) => {
    // Async work here
    const success = true;

    if (success) {
        resolve("Data received!");  // Fulfill
    } else {
        reject(new Error("Failed"));  // Reject
    }
});
```

### Consuming Promises

```jsx
promise
    .then((value) => {
        console.log(value);  // "Data received!"
        return "Next value";
    })
    .then((value) => {
        console.log(value);  // "Next value"
    })
    .catch((error) => {
        console.error(error);  // Handles any rejection above
    })
    .finally(() => {
        console.log("Cleanup");  // Always runs
    });
```

### Promise Chaining

```jsx
fetchUser(1)
    .then(user => fetchPosts(user.id))
    .then(posts => fetchComments(posts[0].id))
    .then(comments => console.log(comments))
    .catch(err => console.error("Chain failed:", err));
```

### Error Propagation

```jsx
Promise.resolve(1)
    .then(x => { throw new Error("Oops"); })  // Rejects
    .then(x => console.log("Skipped"))        // Skipped
    .catch(err => console.log("Caught:", err.message));  // "Caught: Oops"
```

### Static Promise Methods

| Method | Behavior |
|--------|----------|
| `Promise.all([p1, p2])` | Resolves when **all** resolve, rejects if **any** rejects |
| `Promise.race([p1, p2])` | Resolves/rejects as **first** settles |
| `Promise.allSettled([p1, p2])` | Waits for **all** to settle, never rejects |
| `Promise.any([p1, p2])` | Resolves when **first** fulfills, rejects if **all** reject |

```jsx
const p1 = Promise.resolve(1);
const p2 = Promise.reject(new Error("Fail"));
const p3 = new Promise(r => setTimeout(() => r(3), 100));

Promise.all([p1, p3]).then(console.log);  // [1, 3] after 100ms
Promise.race([p2, p3]).catch(console.log);  // Error: Fail (immediate)
Promise.allSettled([p1, p2]).then(console.log);
// [{status: "fulfilled", value: 1}, {status: "rejected", reason: Error}]
```

---

## async / await

**Syntactic sugar over promises.** Makes async code look synchronous.

### Basic Syntax

```jsx
async function fetchData() {
    try {
        const user = await fetchUser(1);
        const posts = await fetchPosts(user.id);
        return posts;
    } catch (error) {
        console.error("Failed:", error);
        throw error;  // Re-throw if needed
    }
}
```

### Rules

1. `await` only works inside `async` functions
2. `await` pauses function until promise settles
3. `await` unwraps resolved value (or throws rejected reason)
4. `async` functions **always return a promise**

### Sequential vs Parallel

```jsx
// Sequential (slower — waits for each)
async function sequential() {
    const a = await fetchA();  // 100ms
    const b = await fetchB();  // 100ms
    return { a, b };
}
// Total: ~200ms

// Parallel (faster — runs together)
async function parallel() {
    const [a, b] = await Promise.all([fetchA(), fetchB()]);
    return { a, b };
}
// Total: ~100ms
```

### Common Mistakes

```jsx
// ❌ Forgetting await
async function bad() {
    const user = fetchUser(1);  // Returns Promise, not user!
    console.log(user.name);     // undefined
}

// ✅ Correct
async function good() {
    const user = await fetchUser(1);
    console.log(user.name);     // Works
}

// ❌ Missing try/catch
async function risky() {
    const data = await fetchData();  // If rejects → unhandled rejection
}

// ✅ With error handling
async function safe() {
    try {
        const data = await fetchData();
    } catch (err) {
        // Handle error
    }
}

// ❌ Await in loop (sequential by accident)
async function slow() {
    for (const id of ids) {
        const item = await fetchItem(id);  // One by one!
    }
}

// ✅ Parallel in loop
async function fast() {
    const promises = ids.map(id => fetchItem(id));
    const items = await Promise.all(promises);
}
```

### Top-Level Await (Modules)

```jsx
// In ES Modules (.mjs or "type": "module")
const data = await fetchData();  // Works at top level
```

---

## The Event Loop (The Second "Wow" Moment)

### Components

```
┌─────────────────────────────────────────────────────────────┐
│                        CALL STACK                             │
│  (Currently executing function)                               │
└─────────────────────────┬─────────────────────────────────────┘
                          │
              ┌───────────┴───────────┐
              ▼                       ▼
    ┌─────────────────┐       ┌─────────────────┐
    │   WEB APIs      │       │  NODE APIs      │
    │ (setTimeout,    │       │ (fs, http,      │
    │  fetch, DOM,   │       │  timers, etc.)  │
    │  events)       │       │                 │
    └────────┬────────┘       └────────┬────────┘
             │                         │
     ┌───────┴───────┐           ┌─────┴─────┐
     ▼               ▼           ▼           ▼
┌───────────┐  ┌───────────┐ ┌────────┐ ┌──────────┐
│ MICROTASK │  │ MACROTASK │ │ nextTick│ │ setImmed │
│  QUEUE    │  │  QUEUE    │ │ (Node)  │ │ (Node)   │
│ (Promises,│  │(setTimeout,│ │         │ │          │
│ queueMicro│  │ setInterval,│ │         │ │          │
│ task)     │  │  I/O, UI  │ │         │ │          │
│           │  │  rendering)│ │         │ │          │
└───────────┘  └───────────┘ └────────┘ └──────────┘
             │               │
             └───────┬───────┘
                     ▼
         ┌─────────────────────┐
         │    EVENT LOOP       │
         │  (while stack empty)│
         │ 1. Run ALL microtasks│
         │ 2. Run ONE macrotask │
         │ 3. Render (browser)  │
         │ 4. Repeat            │
         └─────────────────────┘
```

### Execution Order

```jsx
console.log("1. Sync");

setTimeout(() => console.log("2. Macrotask"), 0);

Promise.resolve()
    .then(() => console.log("3. Microtask"));

queueMicrotask(() => console.log("4. Microtask"));

console.log("5. Sync");

// Output:
// 1. Sync
// 5. Sync
// 3. Microtask
// 4. Microtask
// 2. Macrotask
```

### Tricky Prediction Problems

```jsx
// Problem 1
async function foo() {
    console.log("A");
    await Promise.resolve();
    console.log("B");
}
foo();
console.log("C");
// Output: A, C, B

// Problem 2
setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));
console.log("Sync");
// Output: Sync, Promise, Timeout

// Problem 3
async function bar() {
    await Promise.resolve();
    console.log("After await");
}
bar();
console.log("End");
// Output: End, After await
```

---

## Fetch API & HTTP

### Basic Fetch

```jsx
async function getUser(id) {
    const response = await fetch(`https://api.example.com/users/${id}`);

    if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
    }

    const user = await response.json();
    return user;
}
```

### POST Request

```jsx
async function createUser(userData) {
    const response = await fetch("/api/users", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(userData)
    });
    return response.json();
}
```

### Error Handling

```jsx
async function safeFetch(url) {
    try {
        const response = await fetch(url);
        if (!response.ok) throw new Error(`Status: ${response.status}`);
        return await response.json();
    } catch (error) {
        if (error instanceof TypeError) {
            // Network error
            console.error("Network failed");
        } else {
            // HTTP error or parsing error
            console.error("Request failed:", error.message);
        }
        throw error;
    }
}
```

### JSON

```jsx
const obj = { name: "Aman", age: 25 };
const json = JSON.stringify(obj);  // '{"name":"Aman","age":25}'
const parsed = JSON.parse(json);   // { name: "Aman", age: 25 }
```

---

## Phase 5 Checklist

- [ ] Explain sync vs async with examples
- [ ] Use `setTimeout`, `setInterval`, `clearTimeout`, `clearInterval`
- [ ] Identify callback hell and why it's problematic
- [ ] Create promises with `new Promise`
- [ ] Consume promises with `.then`, `.catch`, `.finally`
- [ ] Chain promises correctly
- [ ] Use `Promise.all`, `race`, `allSettled`, `any`
- [ ] Write `async`/`await` functions
- [ ] Handle errors with `try`/`catch`/`finally`
- [ ] Choose sequential vs parallel execution correctly
- [ ] **Draw the Event Loop** (Call Stack, Web APIs, Micro/Macro queues)
- [ ] Predict output of event loop puzzles
- [ ] Make fetch requests (GET, POST)
- [ ] Handle fetch errors (network, HTTP, parsing)
- [ ] Use `JSON.parse` / `stringify`

---

*Next: Phase 6 — Modern & Practical JavaScript*