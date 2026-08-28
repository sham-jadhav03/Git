# Phase 6 — Modern & Practical JavaScript

**Goal:** Round out your toolkit with everything modern JavaScript offers, and prepare for real-world development.

---

## Modern ES6+ Features (Deep Dive)

### Advanced Destructuring

```jsx
// Nested destructuring
const user = {
    name: "Aman",
    address: { city: "Bhopal", zip: 462001 },
    skills: ["JS", "React", "Node"]
};

const {
    name,
    address: { city, zip: pincode },  // Renaming nested
    skills: [firstSkill, , thirdSkill]  // Array destructuring with skip
} = user;

// Defaults with renaming
const { country = "India", theme: uiTheme = "dark" } = user;

// Function parameter destructuring with defaults
function greet({ name = "Guest", age = 18, city = "Unknown" } = {}) {
    console.log(`${name}, ${age}, ${city}`);
}
greet();  // "Guest, 18, Unknown"
```

### Spread & Rest (Advanced)

```jsx
// Object spread (shallow merge)
const defaults = { theme: "light", lang: "en", notifications: true };
const userPrefs = { theme: "dark", fontSize: 16 };
const settings = { ...defaults, ...userPrefs, lang: "hi" };

// Array spread for concatenation
const all = [...arr1, ...arr2, newItem, ...arr3];

// Rest in destructuring
const [head, ...tail] = [1, 2, 3, 4];
const { a, b, ...rest } = { a: 1, b: 2, c: 3, d: 4 };
```

### Tagged Template Literals

```jsx
function highlight(strings, ...values) {
    return strings.reduce((result, str, i) => {
        return result + str + (values[i] ? `<mark>${values[i]}</mark>` : "");
    }, "");
}

const name = "Aman";
const role = "Developer";
const html = highlight`Name: ${name}, Role: ${role}`;
// "Name: <mark>Aman</mark>, Role: <mark>Developer</mark>"

// Real use: Styled Components, SQL sanitization, i18n
```

### Optional Chaining (`?.`)

```jsx
const user = {
    address: { city: "Bhopal" }
};

// Safe nested access
user?.address?.city;        // "Bhopal"
user?.address?.street;      // undefined (no error)
user?.profile?.avatar?.url; // undefined

// With function calls
user.getSettings?.();       // Calls if exists, else undefined

// With arrays
const arr = [1, 2];
arr?.[0];                   // 1
arr?.[5];                   // undefined
```

### Nullish Coalescing (`??`)

```jsx
// Only falls back for null/undefined (not "", 0, false)
const name = userName ?? "Guest";
const count = items?.length ?? 0;
const theme = userTheme ?? "light";

// vs || (falls back for ALL falsy)
const bad = userName || "Guest";  // Falls back for "" too!
```

### Short-Circuit Evaluation Patterns

```jsx
// && as guard (execute if truthy)
isLoggedIn && renderDashboard();
user && console.log(user.name);

// || as default (legacy, prefer ??)
const displayName = userName || "Guest";

// &&= (logical AND assignment) - ES2021
obj && (obj.prop = value);  // Only assign if obj truthy

// ??= (nullish assignment) - ES2021
obj.prop ??= defaultValue;  // Only assign if null/undefined

// ||= (logical OR assignment) - ES2021
obj.prop ||= defaultValue;  // Only assign if falsy
```

### Logical Assignment Operators (ES2021)

```jsx
let a = 1, b = 0, c = null, d = "";

a ||= 10;  // a stays 1 (truthy)
b ||= 10;  // b becomes 10 (falsy)
c ??= 10;  // c becomes 10 (nullish)
d ??= 10;  // d stays "" (not nullish)

// Compound with property access
obj.prop ||= defaultVal;
obj.prop ??= defaultVal;
obj.prop &&= newVal;  // Only if truthy
```

---

## Modules

### ES Modules (ESM) — Standard

```jsx
// math.js
export const PI = 3.14159;
export function add(a, b) { return a + b; }
export function multiply(a, b) { return a * b; }

// Default export
export default function subtract(a, b) { return a - b; }

// Re-export
export { PI as PI_CONSTANT } from "./constants.js";
```

```jsx
// main.js
import { add, multiply, PI } from "./math.js";
import subtract from "./math.js";  // Default
import * as MathUtils from "./math.js";  // Namespace

// Dynamic import (code splitting)
const module = await import("./math.js");
```

### CommonJS — Node.js Legacy

```jsx
// math.js
const PI = 3.14159;
function add(a, b) { return a + b; }
module.exports = { PI, add };

// Or default
module.exports = function subtract(a, b) { return a - b; };
```

```jsx
// main.js
const { add, PI } = require("./math.js");
const subtract = require("./math.js");  // Default
```

### Key Differences

| Feature | ESM | CommonJS |
|---------|-----|----------|
| Syntax | `import`/`export` | `require`/`module.exports` |
| Loading | Static (compile-time) | Dynamic (runtime) |
| Top-level await | ✅ | ❌ (needs wrapper) |
| Tree shaking | ✅ | ❌ |
| Default export | `export default` | `module.exports =` |
| File extension | `.js` (with `"type": "module"`) | `.js` (default Node) |

---

## Error Handling

### try / catch / finally

```jsx
try {
    const data = await fetchData();
    process(data);
} catch (error) {
    // Handle error
    console.error("Failed:", error.message);
    // Can re-throw
    throw error;
} finally {
    // Cleanup (always runs)
    loadingSpinner.hide();
}
```

### throw

```jsx
function divide(a, b) {
    if (b === 0) throw new Error("Cannot divide by zero");
    return a / b;
}

// Custom error data
throw {
    code: "VALIDATION_ERROR",
    field: "email",
    message: "Invalid email format"
};
```

### Built-in Error Types

```jsx
new Error("Generic error");
new TypeError("Expected string, got number");
new ReferenceError("x is not defined");
new SyntaxError("Invalid JSON");
new RangeError("Array length invalid");
new URIError("Invalid URI");
new EvalError("Eval error (rare)");
```

### Custom Error Classes

```jsx
class AppError extends Error {
    constructor(message, code, statusCode = 500) {
        super(message);
        this.name = this.constructor.name;
        this.code = code;
        this.statusCode = statusCode;
        Error.captureStackTrace(this, this.constructor);
    }
}

class ValidationError extends AppError {
    constructor(message, field) {
        super(message, "VALIDATION_ERROR", 400);
        this.field = field;
    }
}

class NotFoundError extends AppError {
    constructor(resource) {
        super(`${resource} not found`, "NOT_FOUND", 404);
    }
}

// Usage
throw new ValidationError("Email required", "email");
throw new NotFoundError("User");
```

---

## Useful Built-ins

### Date Object

```jsx
const now = new Date();           // Current date/time
const specific = new Date("2024-01-15T10:30:00Z");
const fromParts = new Date(2024, 0, 15);  // Month is 0-indexed!

// Getters
now.getFullYear();    // 2024
now.getMonth();       // 0-11
now.getDate();        // 1-31
now.getDay();         // 0-6 (Sun-Sat)
now.getHours();       // 0-23
now.getTime();        // Timestamp (ms since epoch)
Date.now();           // Same as new Date().getTime()

// Formatting
now.toISOString();       // "2024-01-15T10:30:00.000Z"
now.toLocaleString();    // "1/15/2024, 10:30:00 AM"
now.toLocaleDateString(); // "1/15/2024"

// Calculations
const diff = date2 - date1;  // Difference in ms
const future = new Date(now.getTime() + 86400000);  // +1 day
```

### Regular Expressions (Basics)

```jsx
// Creation
const regex1 = /pattern/flags;
const regex2 = new RegExp("pattern", "flags");

// Flags
// g = global, i = case-insensitive, m = multiline, s = dotAll, u = unicode

// Methods
const str = "Hello World";

regex.test(str);        // true/false
str.match(regex);       // Array or null
str.replace(regex, "X"); // New string
str.split(regex);       // Array

// Common patterns
/^\d+$/              // Only digits
/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-z]{2,}$/  // Email (basic)
/\b\w{5,}\b/g        // Words 5+ chars
```

### Iterators & Generators (Intro)

```jsx
// Iterable protocol
const iterable = {
    [Symbol.iterator]() {
        let step = 0;
        return {
            next() {
                return step < 3 ? { value: step++, done: false } : { done: true };
            }
        };
    }
};

for (const x of iterable) console.log(x);  // 0, 1, 2

// Generator function
function* countTo(n) {
    for (let i = 1; i <= n; i++) {
        yield i;  // Pause and return value
    }
}

const gen = countTo(3);
gen.next();  // { value: 1, done: false }
gen.next();  // { value: 2, done: false }
gen.next();  // { value: 3, done: false }
gen.next();  // { value: undefined, done: true }

// Async generators (for await...of)
async function* fetchPages() {
    for (let page = 1; page <= 3; page++) {
        yield await fetchPage(page);
    }
}

for await (const page of fetchPages()) {
    process(page);
}
```

---

## Storage & Persistence

### localStorage (Persistent)

```jsx
// Save (strings only!)
localStorage.setItem("user", JSON.stringify({ name: "Aman" }));

// Load
const user = JSON.parse(localStorage.getItem("user"));

// Remove
localStorage.removeItem("user");
localStorage.clear();  // All items

// Storage event (cross-tab sync)
window.addEventListener("storage", (e) => {
    console.log(e.key, e.oldValue, e.newValue);
});
```

### sessionStorage (Tab Session)

```jsx
// Same API as localStorage
// Cleared when tab closes
sessionStorage.setItem("temp", "data");
```

### Cookies (Brief)

```jsx
// Set (via document.cookie)
document.cookie = "token=abc123; max-age=3600; path=/; Secure; SameSite=Strict";

// Read (manual parsing)
const cookies = document.cookie.split("; ").reduce((acc, c) => {
    const [key, val] = c.split("=");
    acc[key] = decodeURIComponent(val);
    return acc;
}, {});
```

| Feature | localStorage | sessionStorage | Cookies |
|---------|--------------|----------------|---------|
| Capacity | ~5-10 MB | ~5 MB | ~4 KB |
| Expires | Never | Tab close | Configurable |
| Sent to server | No | No | Yes (auto) |
| Access | Sync | Sync | Sync |

---

## Best Practices

### Clean Code Principles

```jsx
// ❌ Bad: Magic numbers, unclear names
function calc(x, y) { return x * y * 0.18; }

// ✅ Good: Named constants, descriptive names
const GST_RATE = 0.18;
function calculatePriceWithGST(basePrice, quantity) {
    return basePrice * quantity * (1 + GST_RATE);
}

// ❌ Bad: Long function, multiple responsibilities
function processUser(data) {
    validate(data);
    saveToDB(data);
    sendEmail(data);
    logAnalytics(data);
}

// ✅ Good: Small, single-purpose functions
function processUser(data) {
    const validated = validateUser(data);
    saveUser(validated);
    notifyUser(validated);
    trackUser(validated);
}
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Variables/Functions | camelCase | `userName`, `calculateTotal` |
| Classes/Constructors | PascalCase | `User`, `ApiClient` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRIES`, `API_URL` |
| Private (convention) | _prefix | `_internalMethod` |
| Boolean | is/has/can/should | `isActive`, `hasPermission` |

### Common Pitfalls to Avoid

```jsx
// ❌ Mutating arguments
function addItem(items, item) {
    items.push(item);  // Mutates caller's array!
}

// ✅ Return new array
function addItem(items, item) {
    return [...items, item];
}

// ❌ == instead of ===
if (value == "5")  // Type coercion!

// ✅ Strict equality
if (value === "5")

// ❌ Forgetting await
const user = fetchUser(1);  // Promise!

// ✅ Always await
const user = await fetchUser(1);

// ❌ Var in loops
for (var i = 0; i < 3; i++) { ... }

// ✅ Let/const in loops
for (let i = 0; i < 3; i++) { ... }
```

### Debugging with DevTools

1. **Sources Panel:** Set breakpoints (click line number)
2. **Watch Expressions:** Monitor variables during pause
3. **Call Stack:** See how you got here
4. **Scope:** Inspect local, closure, global variables
5. **Console:** `debugger` statement pauses execution

```jsx
function trickyFunction() {
    const x = 1;
    debugger;  // Pauses here if DevTools open
    const y = 2;
    return x + y;
}
```

### Reading Error Messages

```
Error: Cannot read property 'map' of undefined
    at processData (app.js:15)
    at handleRequest (app.js:42)
    at Object.<anonymous> (app.js:50)
```

1. **Error type & message:** `Cannot read property 'map' of undefined`
2. **Stack trace:** Bottom = origin, Top = where it crashed
3. **Look for YOUR code** in stack (not node_modules)
4. **Line numbers** point to exact location

---

## Capstone Project Ideas

### 1. Weather App (Fetch API)
- Search city → show current weather + 5-day forecast
- Use OpenWeatherMap API
- Cache results in localStorage
- Loading states, error handling

### 2. Expense Tracker (localStorage)
- Add/edit/delete expenses
- Categories, date filtering
- Monthly summaries, charts (Chart.js)
- Data persists across sessions

### 3. Quiz App
- Multiple choice questions
- Timer, score tracking
- High scores in localStorage
- Categories/difficulty

### 4. Kanban Board
- Columns: Backlog, Todo, In Progress, Done
- Drag & drop (native HTML5 or library)
- LocalStorage persistence
- Multiple boards

### 5. Your Own Idea
- Build something you'd actually use
- Apply 3+ phases of knowledge
- Deploy (Netlify, Vercel, GitHub Pages)

---

## Phase 6 Checklist

- [ ] Use advanced destructuring (nested, defaults, renaming)
- [ ] Use spread/rest for objects and arrays
- [ ] Write tagged template literals
- [ ] Use optional chaining (`?.`) and nullish coalescing (`??`)
- [ ] Use logical assignment operators (`??=`, `||=`, `&&=`)
- [ ] Create ES modules with named/default exports
- [ ] Use dynamic imports for code splitting
- [ ] Write try/catch/finally with proper error handling
- [ ] Create custom error classes
- [ ] Work with Date, Regex, Generators
- [ ] Use localStorage/sessionStorage correctly
- [ ] Follow clean code practices
- [ ] Debug effectively with DevTools
- [ ] Build and deploy 2+ capstone projects

---

## Final Note

> **By the end of this course, you won't just *know* JavaScript. You'll *understand* it.**

The phases build on each other:
- Phase 1: Syntax & basics
- Phase 2: Data structures & functions
- Phase 3: **How JS works** (the mental model)
- Phase 4: **Object system** (prototypes, classes, `this`)
- Phase 5: **Async model** (event loop, promises)
- Phase 6: **Modern tools** + real projects

Revisit earlier phases with later knowledge. That's where mastery lives.

---

*Congratulations on completing the roadmap. Now go build things.*