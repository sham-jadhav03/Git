# Phase 2 — Functions, Arrays & Objects

**Goal:** Learn how to organize logic and data. This is where you start writing "real" programs.

---

## Functions

### Function Declaration vs Function Expression

```jsx
// Declaration (hoisted)
function add(a, b) {
    return a + b;
}

// Expression (not hoisted)
const subtract = function(a, b) {
    return a - b;
};

// Arrow Function (modern, lexical `this`)
const multiply = (a, b) => a * b;

// Block body with explicit return
const divide = (a, b) => {
    if (b === 0) return "Cannot divide by zero";
    return a / b;
};
```

### Parameters vs Arguments

- **Parameters:** Names in function definition
- **Arguments:** Values passed when calling

```jsx
function greet(name, greeting = "Hello") {  // Default parameter
    console.log(`${greeting}, ${name}!`);
}

greet("Aman");           // "Hello, Aman!"
greet("Aman", "Hi");     // "Hi, Aman!"
```

### Rest Parameters

```jsx
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0);
}

sum(1, 2, 3);        // 6
sum(10, 20, 30, 40); // 100
```

### Return Values

```jsx
function findUser(users, id) {
    for (const user of users) {
        if (user.id === id) return user;  // Early return
    }
    return null;  // Implicit return undefined if not found
}
```

### Functions as First-Class Citizens

```jsx
// Pass function as argument
function operate(a, b, fn) {
    return fn(a, b);
}

operate(5, 3, (x, y) => x + y);  // 8
operate(5, 3, (x, y) => x * y);  // 15

// Return function from function (factory)
function createMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

### Callback Functions

```jsx
function fetchData(callback) {
    setTimeout(() => {
        const data = { user: "Aman" };
        callback(data);
    }, 1000);
}

fetchData((result) => {
    console.log("Got data:", result);
});
```

### Higher-Order Functions

Functions that take functions as arguments or return functions.

```jsx
// map, filter, reduce are higher-order functions
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map(n => n * 2);        // [2, 4, 6, 8, 10]
const evens = numbers.filter(n => n % 2 === 0); // [2, 4]
const sum = numbers.reduce((a, b) => a + b, 0); // 15
```

### Pure vs Impure Functions

| Pure | Impure |
|------|--------|
| Same input → Same output | Depends on external state |
| No side effects | Modifies external state |
| Predictable, testable | Harder to test |

```jsx
// Pure
const add = (a, b) => a + b;

// Impure (modifies external array)
let total = 0;
function addToTotal(x) {
    total += x;  // Side effect!
    return total;
}
```

### Recursion Basics

```jsx
function factorial(n) {
    if (n <= 1) return 1;  // Base case
    return n * factorial(n - 1);  // Recursive case
}

factorial(5); // 120
```

### IIFE (Immediately Invoked Function Expression)

```jsx
// Creates private scope
(function() {
    const secret = "hidden";
    console.log(secret);
})();

// Arrow IIFE
(() => {
    const temp = "temporary";
})();
```

---

## Arrays

### Creating & Accessing

```jsx
const fruits = ["apple", "banana", "mango"];
const mixed = [1, "hello", true, null, [1, 2]];

console.log(fruits[0]);        // "apple"
console.log(fruits.length);    // 3
console.log(fruits[fruits.length - 1]);  // Last element
```

### Mutating vs Non-Mutating Methods

| Mutating (changes original) | Non-Mutating (returns new) |
|-----------------------------|----------------------------|
| `push`, `pop` | `slice`, `concat` |
| `shift`, `unshift` | `map`, `filter`, `reduce` |
| `splice`, `sort`, `reverse` | `find`, `findIndex`, `some`, `every` |
| | `forEach`, `join` |

### Common Methods

```jsx
const arr = [1, 2, 3];

// Adding
arr.push(4);           // [1, 2, 3, 4] - end
arr.unshift(0);        // [0, 1, 2, 3, 4] - start

// Removing
arr.pop();             // [0, 1, 2, 3] - end
arr.shift();           // [1, 2, 3] - start
arr.splice(1, 1);      // [1, 3] - remove 1 at index 1

// Slicing (non-mutating)
arr.slice(1, 3);       // [2, 3] - copy portion

// Searching
arr.indexOf(2);        // 1
arr.includes(3);       // true
arr.find(n => n > 2);  // 3
arr.findIndex(n => n > 2); // 2

// Transforming
arr.map(n => n * 2);       // [2, 4, 6]
arr.filter(n => n > 1);    // [2, 3]
arr.reduce((a, b) => a + b, 0); // 6

// Joining
arr.join("-");           // "1-2-3"
```

### Iteration Methods Comparison

| Method | Returns | Use When |
|--------|---------|----------|
| `forEach` | `undefined` | Side effects (logging, DOM) |
| `map` | New array | Transform each element 1:1 |
| `filter` | New array (subset) | Keep only matching elements |
| `reduce` | Single value | Aggregate to one value |
| `find` | First match | Need first matching element |
| `findIndex` | Index of first match | Need position |
| `some` | `boolean` | At least one matches |
| `every` | `boolean` | All match |

### Array Destructuring

```jsx
const [first, second, ...rest] = [1, 2, 3, 4, 5];
console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4, 5]

// With defaults
const [a = 10, b = 20] = [5];
console.log(a, b);  // 5, 20

// Swapping
let x = 1, y = 2;
[x, y] = [y, x];
```

### Spread & Rest with Arrays

```jsx
const a = [1, 2];
const b = [3, 4];

// Spread: expand
const combined = [...a, ...b];  // [1, 2, 3, 4]
const copy = [...a];            // Shallow copy

// Rest: collect
const [head, ...tail] = [1, 2, 3, 4];
console.log(head);  // 1
console.log(tail);  // [2, 3, 4]
```

### Multi-Dimensional Arrays

```jsx
const matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

console.log(matrix[1][2]);  // 6 (row 1, col 2)

// Nested loops
for (const row of matrix) {
    for (const cell of row) {
        console.log(cell);
    }
}

// Flatten
const flat = matrix.flat();  // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

## Objects

### Creating Objects

```jsx
// Literal (most common)
const user = {
    name: "Aman",
    age: 25,
    isStudent: true,
    greet() {
        console.log(`Hi, I'm ${this.name}`);
    }
};

// Constructor
const user2 = new Object();
user2.name = "Riya";

// Object.create (prototype-based)
const user3 = Object.create(user);
```

### Accessing Properties

```jsx
const user = { name: "Aman", age: 25 };

// Dot notation (static keys)
user.name;      // "Aman"

// Bracket notation (dynamic keys)
const key = "age";
user[key];      // 25
user["full-name"];  // Works with special chars

// Optional chaining (ES2020)
user?.address?.city;  // undefined instead of error
```

### Adding, Updating, Deleting

```jsx
const user = { name: "Aman" };

user.age = 25;           // Add
user.name = "Aman K";    // Update
delete user.age;         // Delete

// Check existence
"name" in user;          // true
user.hasOwnProperty("name"); // true
```

### Methods (Functions in Objects)

```jsx
const calculator = {
    value: 0,
    add(n) {
        this.value += n;
        return this;  // Chaining
    },
    multiply(n) {
        this.value *= n;
        return this;
    },
    getResult() {
        return this.value;
    }
};

calculator.add(5).multiply(2).getResult();  // 10
```

### Nested Objects

```jsx
const user = {
    name: "Aman",
    address: {
        city: "Bhopal",
        pincode: 462001,
        coordinates: {
            lat: 23.2599,
            lng: 77.4126
        }
    }
};

user.address.city;                    // "Bhopal"
user.address.coordinates.lat;         // 23.2599
```

### Object Destructuring

```jsx
const user = { name: "Aman", age: 25, city: "Bhopal" };

// Basic
const { name, age } = user;

// Renaming
const { name: userName, age: userAge } = user;

// Defaults
const { country = "India" } = user;  // "India"

// Nested
const { address: { city } } = user;

// In function parameters
function greet({ name, age = 18 }) {
    console.log(`${name} is ${age}`);
}
greet(user);
```

### Spread with Objects

```jsx
const defaults = { theme: "light", lang: "en" };
const userPrefs = { theme: "dark" };

const settings = { ...defaults, ...userPrefs };
// { theme: "dark", lang: "en" }

// Shallow copy
const copy = { ...user };
```

### Useful Static Methods

```jsx
const user = { name: "Aman", age: 25, city: "Bhopal" };

Object.keys(user);      // ["name", "age", "city"]
Object.values(user);    // ["Aman", 25, "Bhopal"]
Object.entries(user);   // [["name", "Aman"], ["age", 25], ["city", "Bhopal"]]

// Merge
Object.assign({}, user, { country: "India" });

// Freeze (immutable)
Object.freeze(user);
user.age = 30;  // Silently fails (strict mode throws)

// Seal (can't add/remove, can modify)
Object.seal(user);
```

### Looping Through Objects

```jsx
const user = { name: "Aman", age: 25, city: "Bhopal" };

// for...in (keys only)
for (const key in user) {
    console.log(key, user[key]);
}

// Object.entries (modern, preferred)
for (const [key, value] of Object.entries(user)) {
    console.log(key, value);
}

// Object.keys + forEach
Object.keys(user).forEach(key => {
    console.log(key, user[key]);
});
```

---

## End-of-Phase Mini Projects

### 1. To-Do List (In-Memory)
- Add, remove, toggle complete
- Filter: all / active / completed
- Persist to `localStorage` (bonus)

### 2. Student Grade Tracker
- Array of student objects: `{ name, scores: [] }`
- Add student, add score, calculate average
- Letter grades (A-F)

### 3. Shopping Cart Logic
- Array of items: `{ name, price, quantity }`
- Add item, update quantity, remove item
- Calculate subtotal, tax, total
- Apply discount codes

### 4. Word Frequency Counter
- Input: string of text
- Output: object/array of `{ word, count }` sorted by frequency
- Handle punctuation, case-insensitive

---

## Phase 2 Checklist

- [ ] Write function declarations, expressions, and arrows
- [ ] Use default parameters, rest parameters
- [ ] Pass functions as arguments, return functions
- [ ] Identify pure vs impure functions
- [ ] Write recursive functions with base cases
- [ ] Use all major array methods correctly
- [ ] Choose right iteration method (`map` vs `filter` vs `reduce`)
- [ ] Destructure arrays with rest, defaults, swapping
- [ ] Use spread for copying and merging arrays
- [ ] Work with 2D arrays (access, nested loops)
- [ ] Create objects with methods
- [ ] Access properties with dot and bracket notation
- [ ] Destructure objects with renaming, defaults, nesting
- [ ] Use spread for object copying/merging
- [ ] Use `Object.keys`, `values`, `entries`
- [ ] Loop objects with `for...in` and `Object.entries`
- [ ] Build all 4 mini projects

---

*Next: Phase 3 — The HOW Begins (Execution Context, Scope, Closures)*