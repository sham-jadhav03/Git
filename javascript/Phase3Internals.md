# Phase 3 — The HOW Begins (Execution Context, Scope, Closures)

**Goal:** Understand what is actually happening when JavaScript runs your code. This is the phase that separates good developers from average ones.

---

## How JavaScript Works Under the Hood

- **Single-threaded:** One call stack, one thing at a time
- **Synchronous:** Code runs line by line (until async)
- **JIT Compiled:** Just-In-Time compilation (V8 compiles hot code to machine code)

### JavaScript Engines

| Engine | Used By |
|--------|---------|
| V8 | Chrome, Node.js, Edge, Electron |
| SpiderMonkey | Firefox |
| JavaScriptCore | Safari |
| Chakra | Legacy Edge |

---

## Execution Context

**Execution Context** = The environment in which JavaScript code is evaluated and executed. Every piece of code runs inside an execution context.

### Two Phases of Execution Context

```
┌─────────────────────────────────────┐
│     CREATION PHASE (Memory)         │
│  • Create Variable Object (VO)      │
│  • Create Scope Chain               │
│  • Determine `this` value           │
│  • Hoist declarations               │
└─────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────┐
│     EXECUTION PHASE (Code)          │
│  • Assign values                    │
│  • Execute code line by line        │
│  • Function calls create new ECs    │
└─────────────────────────────────────┘
```

### Global Execution Context (GEC)

- Created when script starts
- `this` = `window` (browser) / `global` (Node)
- Only one per program

### Function Execution Context (FEC)

- Created **each time** a function is called
- Has its own Variable Object, Scope Chain, `this`
- Includes `arguments` object (in regular functions)

---

## Call Stack

**Call Stack** = LIFO stack that tracks function calls.

```jsx
function first() {
    console.log("First");
    second();
    console.log("Back to first");
}

function second() {
    console.log("Second");
    third();
}

function third() {
    console.log("Third");
}

first();
```

**Stack trace:**
```
1. first() called          → Stack: [first]
2. first() calls second()  → Stack: [first, second]
3. second() calls third()  → Stack: [first, second, third]
4. third() finishes        → Stack: [first, second]
5. second() finishes       → Stack: [first]
6. first() finishes        → Stack: []
```

**Stack Overflow:** When call stack exceeds limit (too deep recursion).

---

## Hoisting

**Hoisting** = JavaScript's behavior of moving declarations to the top of their scope during the Creation Phase.

### `var` Hoisting

```jsx
console.log(x);  // undefined (not ReferenceError!)
var x = 5;

// Interpreted as:
var x;           // Declaration hoisted, initialized to undefined
console.log(x);  // undefined
x = 5;           // Assignment stays in place
```

### `let` and `const` Hoisting (TDZ)

```jsx
console.log(y);  // ReferenceError: Cannot access 'y' before initialization
let y = 10;

// Temporal Dead Zone (TDZ): from start of scope to declaration
// Variables exist but are uninitialized
```

### Function Hoisting

```jsx
// Function Declaration — fully hoisted
foo();  // Works! "Hello"

function foo() {
    console.log("Hello");
}

// Function Expression — NOT hoisted (only variable declaration)
bar();  // TypeError: bar is not a function
var bar = function() {
    console.log("World");
};
```

---

## Scope

**Scope** = Where variables are accessible.

### Scope Types

| Scope | Description | Variables |
|-------|-------------|-----------|
| **Global** | Outside all functions/blocks | `var`, `let`, `const` at top level |
| **Function** | Inside a function | `var`, `let`, `const` in function |
| **Block** | Inside `{ }` (if, for, etc.) | `let`, `const` only |

```jsx
var globalVar = "I'm global";

function example() {
    var funcVar = "I'm function scoped";
    let blockVar = "I'm block scoped";

    if (true) {
        var stillFunc = "var ignores blocks";
        let trulyBlock = "let respects blocks";
        const alsoBlock = "const respects blocks";
    }

    console.log(stillFunc);      // Works
    // console.log(trulyBlock);  // ReferenceError
}
```

### Lexical Scope

**Lexical Scope** = Scope determined by **where code is written**, not where it's called.

```jsx
const global = "global";

function outer() {
    const outerVar = "outer";

    function inner() {
        const innerVar = "inner";
        console.log(global);    // ✓ Global scope
        console.log(outerVar);  // ✓ Parent (lexical) scope
        console.log(innerVar);  // ✓ Own scope
    }

    inner();
}

outer();
```

### Scope Chain

When looking up a variable, JS checks:
1. Current scope
2. Parent scope (lexical parent)
3. Grandparent scope...
4. Global scope
5. **ReferenceError** if not found

---

## Closures

### What is a Closure?

> **A closure is a function bundled together with its lexical environment.**

In simpler terms: **A function remembers the variables from where it was created, even when executed elsewhere.**

### Step-by-Step Trace

```jsx
function createCounter() {
    let count = 0;  // This variable is "closed over"

    return function() {
        count++;
        return count;
    };
}

const counter = createCounter();

console.log(counter());  // 1
console.log(counter());  // 2
console.log(counter());  // 3
```

**What happens:**
1. `createCounter()` runs, creates local `count = 0`
2. Returns inner function — this function **closes over** `count`
3. `counter` holds reference to inner function + its lexical environment
4. Each call accesses the **same** `count` variable

### Practical Use Cases

#### 1. Data Privacy (Encapsulation)

```jsx
function createBankAccount(initialBalance) {
    let balance = initialBalance;  // Private!

    return {
        deposit(amount) {
            balance += amount;
            return balance;
        },
        withdraw(amount) {
            if (amount > balance) return "Insufficient funds";
            balance -= amount;
            return balance;
        },
        getBalance() {
            return balance;
        }
    };
}

const account = createBankAccount(100);
account.deposit(50);    // 150
account.getBalance();   // 150
// account.balance;     // undefined — truly private!
```

#### 2. Function Factories

```jsx
function createGreeter(greeting) {
    return function(name) {
        console.log(`${greeting}, ${name}!`);
    };
}

const sayHello = createGreeter("Hello");
const sayHi = createGreeter("Hi");

sayHello("Aman");  // "Hello, Aman!"
sayHi("Aman");     // "Hi, Aman!"
```

#### 3. Currying

```jsx
function multiply(a) {
    return function(b) {
        return function(c) {
            return a * b * c;
        };
    };
}

const multiplyBy2 = multiply(2);
const multiplyBy2And3 = multiplyBy2(3);
multiplyBy2And3(4);  // 24

// Or: multiply(2)(3)(4) === 24
```

#### 4. Memoization

```jsx
function memoize(fn) {
    const cache = new Map();

    return function(...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) return cache.get(key);

        const result = fn(...args);
        cache.set(key, result);
        return result;
    };
}

const factorial = memoize(function(n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
});

factorial(50);  // Computes
factorial(50);  // Instant (cached)
```

### Common Closure Interview Questions

#### Q1: The Loop Problem

```jsx
// PROBLEM: var is function-scoped
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
}
// Output: 3, 3, 3 (not 0, 1, 2!)

// FIX 1: Use let (block-scoped, new binding per iteration)
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
}
// Output: 0, 1, 2

// FIX 2: IIFE to capture value
for (var i = 0; i < 3; i++) {
    ((j) => setTimeout(() => console.log(j), 100))(i);
}
// Output: 0, 1, 2
```

#### Q2: What does this print?

```jsx
function outer() {
    let x = 10;
    function inner() {
        console.log(x);
    }
    return inner;
}

const fn = outer();
fn();  // 10 (closure remembers x)
```

#### Q3: Module Pattern

```jsx
const Counter = (function() {
    let count = 0;
    return {
        increment() { return ++count; },
        decrement() { return --count; },
        getCount() { return count; }
    };
})();

Counter.increment();  // 1
Counter.increment();  // 2
Counter.getCount();   // 2
```

---

## Phase 3 Checklist

- [ ] Explain Execution Context (Creation + Execution phases)
- [ ] Draw Call Stack for nested function calls
- [ ] Explain `var` hoisting vs `let/const` TDZ
- [ ] Explain function declaration vs expression hoisting
- [ ] Define Global, Function, Block scope
- [ ] Explain Lexical Scope vs Dynamic Scope
- [ ] Trace Scope Chain lookup
- [ ] **Define Closure in your own words**
- [ ] Trace a closure step-by-step
- [ ] Implement: Data privacy, Factory, Currying, Memoization
- [ ] Explain the `var` in loop problem and 2 fixes
- [ ] Solve closure output prediction problems

---

*Revisit Phase 1 & 2 examples with this new lens. The "aha" moments here are what make this phase special.*