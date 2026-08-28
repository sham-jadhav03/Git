# Phases Quick Reference Card

One-page summary of all 6 phases — print this or keep it open while learning.

---

## Phase 1: Foundations ✅
**Goal:** Write JS without fear. Master syntax and basic building blocks.

| Concept | Key Points |
|---------|------------|
| **Environment** | Browser Console, VS Code, Node.js (`node file.js`) |
| **Output** | `console.log`, `warn`, `error`, `table` |
| **Variables** | `const` (default), `let` (reassign), avoid `var` |
| **Types** | 7 primitives: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint` + `object` |
| **Typeof** | `typeof null === "object"` (bug from 1995) |
| **Coercion** | `"5" + 3 = "53"` (concat), `"5" - 3 = 2` (math) |
| **Equality** | **Always `===`** — `==` does surprise coercion |
| **Truthy/Falsy** | 6 falsy: `false`, `0`, `""`, `null`, `undefined`, `NaN` |
| **Operators** | `+ - * / % **`, `+= -= *= /= %=`, `&&` `||` `!`, `? :` |
| **Strings** | Template literals `` `Hi ${name}` ``, immutable, methods return new strings |
| **Numbers** | `Math.random()`, `toFixed()`, `parseInt()`, `parseFloat()` |
| **Conditionals** | `if/else if/else`, `switch` (strict `===`, don't forget `break`) |
| **Loops** | `for`, `while`, `do...while`, `for...of` |
| **Control** | `break` (exit), `continue` (skip) |
| **Input** | `prompt()` → always string → convert with `Number()` |

**Mini Projects:** Calculator, FizzBuzz, Guessing Game, Temp Converter, Count Vowels

---

## Phase 2: Functions, Arrays & Objects 🔄
**Goal:** Organize logic and data. Write "real" programs.

### Functions
| Concept | Key Points |
|---------|------------|
| **Declaration vs Expression** | `function foo() {}` vs `const foo = function() {}` |
| **Arrow Functions** | `const add = (a, b) => a + b` (implicit return) |
| **Parameters** | Default: `(x = 10)`, Rest: `(...args)` |
| **First-Class** | Pass functions, return functions |
| **Callbacks** | Functions passed to other functions |
| **Higher-Order** | Functions that take/return functions |
| **Pure vs Impure** | Pure: same input → same output, no side effects |
| **Recursion** | Function calls itself (base case required) |

### Arrays
| Method Category | Methods |
|-----------------|---------|
| **Mutating** | `push`, `pop`, `shift`, `unshift`, `splice`, `sort`, `reverse` |
| **Non-Mutating** | `slice`, `concat`, `map`, `filter`, `reduce`, `find`, `findIndex`, `some`, `every`, `forEach` |
| **Search** | `indexOf`, `includes`, `find`, `findIndex` |
| **Transform** | `map` (1→1), `filter` (subset), `reduce` (→ single value) |
| **Iteration** | `forEach` (side effects), `for...of` (values) |
| **Destructuring** | `const [a, , c] = arr`, `const [first, ...rest] = arr` |
| **Spread/Rest** | `[...arr]`, `[...a, ...b]`, `const [first, ...rest] = arr` |
| **2D Arrays** | `matrix[row][col]`, nested loops |

### Objects
| Concept | Key Points |
|---------|------------|
| **Creation** | `{ key: value }`, `new Object()` |
| **Access** | `obj.key`, `obj["key"]` (bracket for dynamic) |
| **Methods** | Functions as properties: `obj.method = function() {}` |
| **Destructuring** | `const { name, age: years } = obj` |
| **Spread** | `{ ...obj, newKey: val }` |
| **Static Methods** | `Object.keys()`, `values()`, `entries()`, `assign()`, `freeze()`, `seal()` |
| **Looping** | `for...in` (keys), `Object.entries().forEach()` |

**Mini Projects:** To-do list, Grade Tracker, Shopping Cart, Word Frequency Counter

---

## Phase 3: The HOW Begins 🔄
**Goal:** Understand what happens when JS runs. Separates good from average.

| Concept | Key Points |
|---------|------------|
| **Single-Threaded** | One thing at a time |
| **Execution Context** | Wrapper for running code: Creation (memory) → Execution (code) |
| **Global EC** | Created first, `this` = `window`/`global` |
| **Function EC** | Created per call, has `arguments`, `this` |
| **Call Stack** | LIFO stack of ECs, overflow = too deep recursion |
| **Hoisting** | `var` → `undefined`, `let/const` → TDZ (ReferenceError), functions → full declaration |
| **Scope** | Global, Function, Block — `let/const` are block-scoped |
| **Lexical Scope** | Scope determined by where code is *written*, not where called |
| **Scope Chain** | Look up → parent → grandparent → global |
| **Closure** | Function + its lexical environment (remembers variables from birth) |
| **Closure Uses** | Data privacy, factories, counters, currying |
| **Classic Bug** | `for (var i...)` in setTimeout → all see final `i` (fixed with `let`) |

**Mental Model:** Draw the stack, trace the scopes, see the closure.

---

## Phase 4: Objects Deeper & `this` 🔄
**Goal:** Master JS's object model and the most confusing keyword.

### `this` Keyword
| Context | `this` Value |
|---------|--------------|
| **Global (browser)** | `window` |
| **Global (Node)** | `globalThis` / module exports |
| **Regular Function** | Depends on *how called* (default: `window`/`undefined` strict) |
| **Method** | Object before the dot: `obj.method()` → `obj` |
| **Arrow Function** | Lexical — inherits from enclosing scope |
| **Event Handler** | The element that fired the event |
| **Strict Mode** | `undefined` (not `window`) |

### Explicit Binding
| Method | Use Case |
|--------|----------|
| `call(thisArg, arg1, arg2...)` | Invoke immediately, pass args individually |
| `apply(thisArg, [args])` | Invoke immediately, pass args as array |
| `bind(thisArg, arg1...)` | Returns **new function** with bound `this` |

### Prototypes
| Concept | Key Points |
|---------|------------|
| **`prototype`** | Property on *constructor functions* — shared methods live here |
| **`__proto__`** | Hidden link on *instances* — points to constructor's `prototype` |
| **Prototype Chain** | `obj.__proto__ → Constructor.prototype → Object.prototype → null` |
| **`Object.create(proto)`** | Creates object with given prototype (no constructor needed) |
| **Inheritance** | `Child.prototype = Object.create(Parent.prototype)` |

### ES6 Classes
| Feature | Syntax |
|---------|--------|
| **Class** | `class User { constructor(name) { this.name = name } }` |
| **Extends** | `class Admin extends User { constructor(name, role) { super(name); this.role = role } }` |
| **Static** | `static count = 0`, `static create() {}` |
| **Getters/Setters** | `get name() {}`, `set name(v) {}` |
| **Private** | `#field` (truly private) |
| **Reveal** | Classes = syntactic sugar over prototypes |

---

## Phase 5: Asynchronous JavaScript 🔄
**Goal:** Master async. Understand the Event Loop. Stop fearing `async`/`await`.

| Concept | Key Points |
|---------|------------|
| **Sync vs Async** | Sync blocks, async delegates (timer, network, file) |
| **Callbacks** | `setTimeout(cb, ms)`, `setInterval`, callback hell = pyramid of doom |
| **Promises** | States: `pending` → `fulfilled` / `rejected` |
| **Promise Methods** | `.then()`, `.catch()`, `.finally()`, chaining |
| **Static Methods** | `Promise.all()`, `race()`, `allSettled()`, `any()` |
| **async/await** | Syntactic sugar over promises, looks synchronous |
| **Error Handling** | `try/catch/finally` with `await` |
| **Parallel vs Sequential** | `await Promise.all([p1, p2])` vs `await p1; await p2` |

### The Event Loop (The "Wow" Moment)
```
┌─────────────────────────────────────┐
│           Call Stack                │  ← Currently executing
└─────────────────────────────────────┘
                    │
                    ▼ (when async op completes)
┌─────────────────────────────────────┐
│        Web APIs / Browser APIs      │  ← setTimeout, fetch, DOM events
│  (timer, HTTP, DOM, etc.)           │
└─────────────────────────────────────┘
                    │
         ┌──────────┴──────────┐
         ▼                     ▼
┌─────────────────┐   ┌─────────────────┐
│  Microtask Q    │   │  Macrotask Q    │  ← Promises go here    ← setTimeout, events
│ (Promise .then) │   │ (setTimeout)    │
└─────────────────┘   └─────────────────┘
         │                     │
         └──────────┬──────────┘
                    ▼
        ┌─────────────────────┐
        │    Event Loop       │  ← 1. Run all microtasks
        │  (while stack empty)│      2. Run one macrotask
        └─────────────────────┘      3. Repeat
```

**Prediction Problems:** Know the exact order of `console.log`, `setTimeout`, `Promise.resolve().then()`, `queueMicrotask()`.

### Fetch & HTTP
| Method | Purpose |
|--------|---------|
| `fetch(url)` | Returns `Promise<Response>` |
| `res.json()` | Parse JSON body |
| `JSON.parse/stringify` | String ↔ Object |

---

## Phase 6: Modern & Practical JS 🔄
**Goal:** Complete toolkit for real-world development.

### Modern ES6+ Features
| Feature | Syntax | Use Case |
|---------|--------|----------|
| **Optional Chaining** | `obj?.user?.name` | Safe nested access |
| **Nullish Coalescing** | `x ?? default` | Default only for `null/undefined` |
| **Logical Assignment** | `x ??= y`, `x ||= y`, `x &&= y` | Conditional assignment |
| **Tagged Templates** | `fn`strings`` | Custom string processing |
| **Destructuring Advanced** | Nested, defaults, renaming | Clean extraction |

### Modules
| System | Syntax |
|--------|--------|
| **ES Modules** | `export const x = 1`, `import { x } from './file.js'` |
| **Default Export** | `export default fn`, `import fn from './file.js'` |
| **Dynamic Import** | `const mod = await import('./file.js')` |
| **CommonJS** | `module.exports = x`, `require('./file')` (Node) |

### Error Handling
| Concept | Key Points |
|---------|------------|
| **try/catch/finally** | `catch (err) {}` catches any thrown error |
| **throw** | `throw new Error("msg")`, `throw new TypeError()` |
| **Built-in Errors** | `Error`, `TypeError`, `ReferenceError`, `SyntaxError`, `RangeError` |
| **Custom Errors** | `class MyError extends Error { constructor(msg) { super(msg); this.name = "MyError" } }` |

### Useful Built-ins
| Feature | Key Points |
|---------|------------|
| **Date** | `new Date()`, `toISOString()`, `getTime()`, `Date.now()` |
| **Regex** | `/pattern/flags`, `.test()`, `.match()`, `.replace()` |
| **Iterators/Generators** | `function* gen() { yield 1 }`, `for (const x of gen())` |

### Storage
| API | Persistence | Scope |
|-----|-------------|-------|
| `localStorage` | Until cleared | Origin (domain) |
| `sessionStorage` | Tab session | Origin |
| Cookies | Expires | Domain + path |

### Best Practices
- **Naming:** `camelCase` vars/functions, `PascalCase` classes, `UPPER_SNAKE` constants
- **Functions:** Small, single responsibility, pure when possible
- **Debugging:** Breakpoints > `console.log`, use DevTools Sources panel
- **Errors:** Read the stack trace, find the *first* line in *your* code

---

## Learning Order Checklist

```
☐ Phase 1: Foundations (complete)
    ☐ Read Phase1Foundation.md
    ☐ Solve Phase1Q.md (all 25 + 15 interview)
    ☐ Build 5 mini projects
    ☐ Can explain all 15 interview answers

☐ Phase 2: Functions, Arrays, Objects
    ☐ Read Phase2Functions.md (when ready)
    ☐ Solve Phase2Q.md
    ☐ Build 4 mini projects

☐ Phase 3: Internals (Execution Context, Scope, Closures)
    ☐ Read Phase3Internals.md
    ☐ Solve Phase3Q.md
    ☐ Trace closure examples on paper

☐ Phase 4: Objects & this
    ☐ Read Phase4Objects.md
    ☐ Solve Phase4Q.md
    ☐ Build prototype chain diagrams

☐ Phase 5: Async & Event Loop
    ☐ Read Phase5Async.md
    ☐ Solve Phase5Q.md
    ☐ Predict event loop output problems

☐ Phase 6: Modern JS & Capstone
    ☐ Read Phase6Modern.md
    ☐ Solve Phase6Q.md
    ☐ Build 2+ capstone projects
```

---

## Time Estimates (Self-Paced)

| Phase | Reading | Practice | Projects | Total |
|-------|---------|----------|----------|-------|
| 1 | 3-4 hrs | 4-6 hrs | 2-3 hrs | ~10 hrs |
| 2 | 4-5 hrs | 6-8 hrs | 3-4 hrs | ~15 hrs |
| 3 | 3-4 hrs | 4-6 hrs | 1-2 hrs | ~10 hrs |
| 4 | 3-4 hrs | 4-5 hrs | 2 hrs | ~10 hrs |
| 5 | 4-5 hrs | 6-8 hrs | 3 hrs | ~15 hrs |
| 6 | 3-4 hrs | 4-6 hrs | 4-6 hrs | ~15 hrs |
| **Total** | | | | **~75 hrs** |

> **Tip:** Spend more time on Phases 3 and 5 — they're where the deep understanding lives.

---

*Keep this card handy. Revisit after each phase.*