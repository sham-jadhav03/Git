# Phase 3 — Execution Context, Hoisting, Scope, Closures Practice Questions

*To be created — scaffold for practice questions matching Phase3Internals.md*

---

## Execution Context & Call Stack (Q1-Q5)

### Q1. Execution Context Phases
Given this code, what happens in Creation vs Execution phase?
```jsx
var x = 10;
function foo() {
    var y = 20;
    console.log(x + y);
}
foo();
```

### Q2. Call Stack Trace
Trace the call stack for:
```jsx
function a() { b(); }
function b() { c(); }
function c() { console.log("Hi"); }
a();
```

### Q3. Stack Overflow
Write a recursive function without base case. What error occurs?

### Q4. Global vs Function EC
How many ECs created? What's in each VO?
```jsx
var global = "G";
function outer() {
    var outerVar = "O";
    function inner() {
        var innerVar = "I";
    }
    inner();
}
outer();
```

### Q5. `this` in Global EC
What is `this` in browser global scope? In Node module scope?

---

## Hoisting (Q6-Q10)

### Q6. `var` Hoisting
Predict output:
```jsx
console.log(a);
var a = 5;
console.log(a);
```

### Q7. `let`/`const` TDZ
Predict output:
```jsx
console.log(b);
let b = 10;
```

### Q8. Function Declaration Hoisting
```jsx
foo();
function foo() { console.log("Hello"); }
```

### Q9. Function Expression Hoisting
```jsx
bar();
var bar = function() { console.log("World"); };
```

### Q10. Mixed Hoisting
```jsx
console.log(x);
var x = 1;
let y = 2;
console.log(y);
function x() {}
var x = 3;
```

---

## Scope & Scope Chain (Q11-Q15)

### Q11. Scope Types
Identify scope of each variable:
```jsx
var global = 1;
function fn() {
    let funcScoped = 2;
    if (true) {
        const blockScoped = 3;
    }
}
```

### Q12. Lexical vs Dynamic Scope
Explain why this logs "outer":
```jsx
const x = "global";
function outer() {
    const x = "outer";
    inner();
}
function inner() {
    console.log(x);
}
outer();
```

### Q13. Scope Chain Lookup
Trace variable lookup for `z`:
```jsx
const z = 1;
function a() {
    const z = 2;
    function b() {
        function c() {
            console.log(z);  // Which z?
        }
        c();
    }
    b();
}
a();
```

### Q14. Block Scope in Loops
Why does this work with `let` but not `var`?
```jsx
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
}
```

### Q15. Function Scope vs Block Scope
```jsx
if (true) {
    var a = 1;
    let b = 2;
    const c = 3;
}
console.log(a, b, c);  // What prints? Errors?
```

---

## Closures (Q16-Q25)

### Q16. Closure Definition
Define closure in your own words. What two things make a closure?

### Q17. Basic Closure Trace
Trace step-by-step:
```jsx
function createCounter() {
    let count = 0;
    return function() {
        return ++count;
    };
}
const counter = createCounter();
counter();  // 1
counter();  // 2
```

### Q18. Closure with Parameters
```jsx
function multiplier(factor) {
    return function(number) {
        return number * factor;
    };
}
const double = multiplier(2);
const triple = multiplier(3);
double(5);  // ?
triple(5);  // ?
```

### Q19. Data Privacy (Module Pattern)
Create a counter with private `count` using IIFE. Expose `increment`, `decrement`, `getCount`.

### Q20. Function Factory
Write `createGreeter(greeting)` returning function that greets a name.

### Q21. Currying
Implement `add(a)(b)(c)` returning sum of three numbers.

### Q22. Memoization
Write `memoize(fn)` that caches results. Test with slow Fibonacci.

### Q23. Closure in Loop (Classic Bug)
```jsx
// Problem
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
}
// Fix 1: let
// Fix 2: IIFE
// Explain both
```

### Q24. Closure + Event Listener
```jsx
for (let i = 1; i <= 3; i++) {
    btn.addEventListener("click", () => console.log(i));
}
// What does each button log?
```

### Q25. Advanced: Closure Memory Leak
```jsx
function createBigData() {
    const bigArray = new Array(1000000).fill("x");
    return function() {
        return bigArray.length;
    };
}
const getSize = createBigData();
// When can bigArray be GC'd?
```

---

## Solutions

*Solutions to be added after Phase 3 content is finalized.*

---

## Interview Questions (Phase 3)

1. What are the two phases of Execution Context?
2. Draw the Call Stack for nested function calls.
3. Explain hoisting for `var`, `let`, `const`, function declarations, function expressions.
4. What is TDZ? Which declarations have it?
5. What is Lexical Scope? How does it differ from Dynamic Scope?
6. How does the Scope Chain work?
7. **Define Closure.** (The real definition)
8. Trace a closure step-by-step showing the environment record.
9. Implement: private counter, function factory, curried function, memoize.
10. The `var` in loop problem — explain and give 2 fixes.
11. Can a closure cause memory leaks? When?
12. What's the difference between `var`, `let`, `const` in terms of scope and hoisting?