# Phase 6 — Modern & Practical JavaScript Practice Questions

*To be created — scaffold for practice questions matching Phase6Modern.md*

---

## Modern ES6+ Features (Q1-Q8)

### Q1. Advanced Destructuring
```jsx
const user = {
    name: "Aman",
    address: { city: "Bhopal", zip: 462001 },
    skills: ["JS", "React", "Node"]
};

// Destructure: name, city (renamed to hometown), first skill, third skill
// With defaults for missing properties
```

### Q2. Spread/Rest Advanced
```jsx
const defaults = { theme: "light", lang: "en" };
const userPrefs = { theme: "dark", fontSize: 16 };
const settings = { ...defaults, ...userPrefs, lang: "hi" };

// What is settings?
// What if userPrefs had nested objects?
const a = [1, 2], b = [3, 4];
const combined = [0, ...a, ...b, 5];
// Result?
```

### Q3. Tagged Template Literals
Write `sql` tag that escapes values for SQL queries:
```jsx
const id = 1; const name = "Aman'; DROP TABLE users;--";
const query = sql`SELECT * FROM users WHERE id = ${id} AND name = ${name}`;
// Should safely escape
```

### Q4. Optional Chaining
```jsx
const user = { profile: { settings: { theme: "dark" } } };
// Safely access user.profile.settings.theme
// Safely access user.profile.avatar.url (doesn't exist)
// Safely call user.getPreferences?.()
```

### Q5. Nullish Coalescing vs ||
```jsx
const name = "";
const count = 0;
const flag = false;

// For each, what does ?? return vs || ?
name ?? "Guest";  // ?
name || "Guest";  // ?
```

### Q6. Logical Assignment Operators
```jsx
let a = 1, b = 0, c = null, d = "";
a ||= 10;  // a = ?
b ||= 10;  // b = ?
c ??= 10;  // c = ?
d ??= 10;  // d = ?

obj.prop ??= "default";
// When does this assign?
```

### Q7. Short-Circuit Patterns
```jsx
// Rewrite using short-circuit:
if (user) renderProfile(user);
if (!cache) cache = computeExpensive();
if (isLoggedIn && hasPermission) showAdminPanel();
```

### Q8. Modern Feature Detection
Write feature detection for: optional chaining, nullish coalescing, logical assignment, top-level await.

---

## Modules (Q9-Q12)

### Q9. ESM Named & Default Exports
```jsx
// math.js
export const PI = 3.14;
export function add(a, b) { return a + b; }
export default function subtract(a, b) { return a - b; }

// main.js - import all variations
```

### Q10. Re-exports & Barrel Files
Create `index.js` that re-exports from `math.js`, `string.js`, `date.js`.

### Q11. Dynamic Imports
```jsx
// Load module only when needed
async function loadFeature() {
    const { heavyFunction } = await import("./heavy.js");
    return heavyFunction();
}
```

### Q12. CommonJS Interop
```jsx
// How to import CommonJS module in ESM?
// How to import ESM in CommonJS?
```

---

## Error Handling (Q13-Q16)

### Q13. try/catch/finally
```jsx
async function fetchData() {
    try {
        const response = await fetch(url);
        if (!response.ok) throw new Error("Failed");
        return response.json();
    } catch (err) {
        // Handle different error types
    } finally {
        // Cleanup
    }
}
```

### Q14. throw with Custom Data
```jsx
function validateEmail(email) {
    if (!email.includes("@")) {
        throw {
            code: "INVALID_EMAIL",
            field: "email",
            value: email
        };
    }
}
```

### Q15. Built-in Error Types
Match error to scenario:
- `TypeError` — `null.toString()`
- `ReferenceError` — `console.log(x)` (x not defined)
- `SyntaxError` — `JSON.parse("{")`
- `RangeError` — `new Array(-1)`
- `URIError` — `decodeURIComponent("%")`

### Q16. Custom Error Classes
```jsx
class AppError extends Error {
    constructor(message, code, statusCode) {
        // Implement properly with Error.captureStackTrace
    }
}

class ValidationError extends AppError { /* 400 */ }
class NotFoundError extends AppError { /* 404 */ }
class UnauthorizedError extends AppError { /* 401 */ }

// Throw and catch with instanceof checks
```

---

## Useful Built-ins (Q17-Q20)

### Q17. Date Manipulation
```jsx
const now = new Date();
// Get: year, month (1-12), day, day of week, timestamp
// Create: specific date, date + 7 days
// Format: ISO, locale string, custom "YYYY-MM-DD"
```

### Q18. Regular Expressions
Write regex for:
- Email validation (basic)
- Phone number (10 digits, optional formatting)
- URL detection
- Password strength (8+ chars, upper, lower, number, special)
- Extract all hashtags from string

### Q19. Iterators
```jsx
// Make object iterable
const range = {
    from: 1,
    to: 5,
    [Symbol.iterator]() { /* return iterator */ }
};
for (const n of range) console.log(n);  // 1,2,3,4,5
```

### Q20. Generators
```jsx
function* fibonacci() {
    let [a, b] = [0, 1];
    while (true) {
        yield a;
        [a, b] = [b, a + b];
    }
}
const fib = fibonacci();
fib.next();  // ?
// Get first 10 Fibonacci numbers
```

---

## Storage (Q21-Q24)

### Q21. localStorage CRUD
```jsx
// Save object (stringify)
// Load object (parse)
// Update single property
// Delete item
// Clear all
// Listen for cross-tab changes
```

### Q22. sessionStorage vs localStorage
When to use each? What happens on tab close? Browser close?

### Q23. Cookie Parsing
```jsx
document.cookie = "user=Aman; max-age=3600; Secure";
document.cookie = "theme=dark; max-age=86400";
// Parse all cookies into object
```

### Q24. Storage Quotas & Limits
- localStorage limit?
- What happens when exceeded?
- How to check available space?

---

## Best Practices (Q25-Q28)

### Q25. Clean Code Refactoring
```jsx
// Refactor this:
function processUserData(data) {
    if (data && data.user && data.user.profile && data.user.profile.settings) {
        const theme = data.user.profile.settings.theme || "light";
        const lang = data.user.profile.settings.lang || "en";
        applyTheme(theme);
        applyLang(lang);
    }
}
// Use optional chaining, nullish coalescing, early returns
```

### Q26. Naming Conventions
Fix naming:
```jsx
const user_name = "Aman";  // ?
const MAXCOUNT = 100;      // ?
function getUserData() {}  // ?
class userService {}       // ?
const isvalid = true;      // ?
```

### Q27. Common Pitfalls
Identify bugs:
```jsx
// 1
const arr = [1,2,3];
const copy = arr;
copy.push(4);

// 2
if (value == "5") { }

// 3
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
}

// 4
async function foo() {
    fetchData();  // Missing await
}

// 5
const user = { name: "Aman" };
const greet = user.greet;
greet();
```

### Q28. Debugging Workflow
Given this error:
```
TypeError: Cannot read property 'map' of undefined
    at processData (app.js:15)
    at handleRequest (app.js:42)
```
- What's the error?
- Where to look first?
- How to debug with breakpoints?

---

## Capstone Projects (Q29+)

### Q29. Weather App
- Search city → current weather + 5-day forecast
- API: OpenWeatherMap
- Cache in localStorage (10 min TTL)
- Loading, error states

### Q30. Expense Tracker
- Add/edit/delete expenses (name, amount, category, date)
- Filter by month/category
- Monthly totals, category breakdown
- Chart.js visualization
- localStorage persistence

### Q31. Quiz App
- Questions from JSON/localStorage
- Timer per question
- Score, high scores
- Categories, difficulty
- Review answers at end

### Q32. Kanban Board
- Columns: Backlog, Todo, In Progress, Done
- Drag & drop tasks
- Add/edit/delete tasks
- Multiple boards
- localStorage persistence

### Q33. Your Project
Build something solving your own problem. Use 3+ phases of knowledge.

---

## Solutions

*Solutions to be added after Phase 6 content is finalized.*

---

## Interview Questions (Phase 6)

1. What's the difference between `??` and `||`? When to use each?
2. How does optional chaining (`?.`) work? What does it prevent?
3. Explain tagged template literals with a real use case.
4. What are logical assignment operators (`??=`, `||=`, `&&=`)?
5. ESM vs CommonJS — key differences?
6. How do dynamic imports enable code splitting?
7. How do you create custom error classes properly?
8. What's the difference between `localStorage`, `sessionStorage`, cookies?
9. How do you make an object iterable?
10. What are generators? When would you use them?
11. What are the clean code principles you follow?
12. How do you debug effectively with DevTools?