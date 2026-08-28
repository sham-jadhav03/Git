# Phase 5 — Asynchronous JavaScript Practice Questions

*To be created — scaffold for practice questions matching Phase5Async.md*

---

## Callbacks (Q1-Q5)

### Q1. `setTimeout` Basics
Log numbers 1-3 with 1 second delay between each using `setTimeout`.

### Q2. `setInterval` & Cleanup
Start interval logging "Tick" every 500ms. Stop after 5 ticks.

### Q3. Callback Pattern
Write `fetchUser(id, callback)` that simulates async with `setTimeout`. Use error-first callback.

### Q4. Callback Hell
Write 3 nested async operations with callbacks. Then refactor to avoid nesting.

### Q5. `Promise` Constructor from Callback
Convert `setTimeout` callback to a Promise-returning function `delay(ms)`.

---

## Promises (Q6-Q15)

### Q6. Create Promise
Create promise that resolves after 1s with "Done", or rejects with Error.

### Q7. `.then` / `.catch` / `.finally`
Chain: delay(100) → log "A" → delay(100) → log "B" → catch errors → finally log "End".

### Q8. Promise Chaining
```jsx
fetchUser(1)
    .then(user => fetchPosts(user.id))
    .then(posts => posts[0])
    .then(post => fetchComments(post.id))
    .then(comments => console.log(comments.length))
    .catch(err => console.error(err));
```
Explain what each `.then` receives.

### Q9. Error Propagation
```jsx
Promise.resolve(1)
    .then(x => { throw new Error("Oops"); })
    .then(x => console.log("A"))
    .catch(err => console.log("Caught:", err.message))
    .then(x => console.log("B"));
// Output?
```

### Q10. `Promise.all`
Run 3 async operations in parallel. Wait for all. Handle if one fails.

### Q11. `Promise.race`
Race: fast promise (100ms) vs slow promise (1000ms). Log winner.

### Q12. `Promise.allSettled`
Run 3 promises: 2 resolve, 1 reject. Log all results with status.

### Q13. `Promise.any`
Run 3 promises: 2 reject fast, 1 resolves slow. Log first success.

### Q14. Sequential vs Parallel
```jsx
// Sequential
async function seq() {
    const a = await fetchA();
    const b = await fetchB();
    return { a, b };
}

// Parallel
async function par() {
    const [a, b] = await Promise.all([fetchA(), fetchB()]);
    return { a, b };
}
// If each takes 100ms, how long does each function take?
```

### Q15. Custom Promise Implementation (Challenge)
Implement a minimal `MyPromise` with `resolve`, `reject`, `then`, `catch`.

---

## async/await (Q16-Q22)

### Q16. Basic async/await
Rewrite Promise chain from Q8 using `async`/`await`.

### Q17. try/catch/finally
Wrap async function in try/catch. Log error, return fallback in catch, cleanup in finally.

### Q18. Forgetting await
```jsx
async function foo() {
    const user = fetchUser(1);  // Missing await!
    console.log(user.name);
}
// What prints? How to fix?
```

### Q19. Missing Error Handling
```jsx
async function risky() {
    const data = await fetchData();  // If rejects?
}
// What happens? How to fix?
```

### Q20. Await in Loop (Sequential vs Parallel)
```jsx
const ids = [1, 2, 3];

// Sequential
for (const id of ids) {
    const item = await fetchItem(id);
}

// Parallel
const promises = ids.map(id => fetchItem(id));
const items = await Promise.all(promises);
```
If each fetch takes 100ms, how long for each?

### Q21. Top-Level Await
In ES Module, write top-level `await fetchData()`.

### Q22. Parallel with Limited Concurrency (Challenge)
Write `mapWithConcurrency(tasks, fn, limit)` that runs max `limit` promises at once.

---

## Event Loop (Q23-Q30)

### Q23. Execution Order
```jsx
console.log("A");
setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));
queueMicrotask(() => console.log("D"));
console.log("E");
// Predict output
```

### Q24. Async Function Order
```jsx
async function foo() {
    console.log("1");
    await Promise.resolve();
    console.log("2");
}
foo();
console.log("3");
// Output?
```

### Q25. Nested Microtasks
```jsx
Promise.resolve()
    .then(() => {
        console.log("A");
        return Promise.resolve();
    })
    .then(() => console.log("B"));
queueMicrotask(() => console.log("C"));
// Output?
```

### Q26. setTimeout vs Promise
```jsx
setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));
// Which runs first? Why?
```

### Q27. Multiple setTimeouts
```jsx
setTimeout(() => console.log("A"), 0);
setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));
// Output?
```

### Q28. Async/Await in Loop
```jsx
async function test() {
    for (let i = 0; i < 3; i++) {
        await Promise.resolve();
        console.log(i);
    }
}
test();
console.log("Done");
// Output?
```

### Q29. Microtask Queue Drain
```jsx
Promise.resolve().then(() => {
    console.log("A");
    queueMicrotask(() => console.log("B"));
});
queueMicrotask(() => console.log("C"));
// Output? (All microtasks drain before next macrotask)
```

### Q30. Complex Prediction (Challenge)
```jsx
console.log("1");

setTimeout(() => {
    console.log("2");
    Promise.resolve().then(() => console.log("3"));
}, 0);

Promise.resolve().then(() => {
    console.log("4");
    setTimeout(() => console.log("5"), 0);
});

console.log("6");
// Full output in order?
```

---

## Fetch & HTTP (Q31-Q35)

### Q31. Basic GET
Write `fetchUser(id)` that GETs `/api/users/:id`, checks `response.ok`, returns JSON.

### Q32. POST Request
Write `createUser(data)` that POSTs JSON to `/api/users`.

### Q33. Error Handling
Handle: network error, 404, 500, invalid JSON response.

### Q34. JSON Parsing
```jsx
const json = '{"name":"Aman","age":25}';
const obj = JSON.parse(json);
const back = JSON.stringify(obj);
// What are types at each step?
```

### Q35. Fetch with Timeout (Challenge)
Write `fetchWithTimeout(url, ms)` that rejects if fetch takes longer than `ms`.

---

## Solutions

*Solutions to be added after Phase 5 content is finalized.*

---

## Interview Questions (Phase 5)

1. What's the difference between synchronous and asynchronous code?
2. Explain callback hell and how Promises solve it.
3. What are the three states of a Promise?
4. How does `.then` chaining work? What does it return?
5. Difference between `Promise.all`, `race`, `allSettled`, `any`?
6. How does `async`/`await` relate to Promises?
7. What are the rules for `await`?
8. Common mistakes with `async`/`await`?
9. **Draw the Event Loop** with Call Stack, Web APIs, Microtask Queue, Macrotask Queue.
10. Explain the Event Loop algorithm (microtasks drain before macrotask).
11. Predict output of event loop puzzles (macrotask vs microtask).
12. How does `fetch` work? How to handle errors properly?