# Phase 4 — Objects Deeper & `this`

**Goal:** Understand JavaScript's object model — how inheritance really works, and why `this` confuses everyone.

---

## The `this` Keyword

`this` is determined by **how a function is called** (call-site), not where it's defined.

### `this` in Different Contexts

```jsx
// 1. Global Scope
console.log(this);  // Browser: window | Node: globalThis (or module.exports in modules)

// 2. Regular Function (non-strict)
function regular() {
    console.log(this);  // window (or global)
}
regular();

// 3. Regular Function (strict mode)
"use strict";
function strict() {
    console.log(this);  // undefined
}
strict();

// 4. Method (object.function())
const obj = {
    name: "Aman",
    greet() {
        console.log(this.name);  // "Aman" — obj is the call-site
    }
};
obj.greet();

// 5. Arrow Function (lexical this)
const arrow = {
    name: "Arrow",
    greet: () => {
        console.log(this.name);  // window/global — inherits from enclosing scope
    }
};
arrow.greet();  // undefined (or global name)

// 6. Event Handler
button.addEventListener("click", function() {
    console.log(this);  // button element (the element that fired)
});

// 7. Arrow in Event Handler
button.addEventListener("click", () => {
    console.log(this);  // window/global (lexical!)
});
```

### `this` Rules Summary

| Call Pattern | `this` Value |
|--------------|--------------|
| `func()` | `window` / `global` / `undefined` (strict) |
| `obj.method()` | `obj` |
| `new Constructor()` | New instance |
| `func.call(obj, ...)` | `obj` |
| `func.apply(obj, [...])` | `obj` |
| `func.bind(obj)()` | `obj` |
| Arrow function | Lexical (enclosing scope) |

---

## Explicit Binding: `call`, `apply`, `bind`

### `call(thisArg, arg1, arg2, ...)`

```jsx
function greet(greeting, punctuation) {
    console.log(`${greeting}, ${this.name}${punctuation}`);
}

const user = { name: "Aman" };

greet.call(user, "Hello", "!");  // "Hello, Aman!"
```

### `apply(thisArg, [argsArray])`

```jsx
greet.apply(user, ["Hi", "?"]);  // "Hi, Aman?"

// Useful for arrays
const numbers = [1, 2, 3];
Math.max.apply(null, numbers);  // 3
Math.max(...numbers);           // Modern alternative
```

### `bind(thisArg, arg1, arg2, ...)`

**Returns a NEW function with `this` permanently bound.**

```jsx
const boundGreet = greet.bind(user, "Hey");
boundGreet(".");  // "Hey, Aman."

// Partial application
const sayHello = greet.bind(user, "Hello");
sayHello("!");    // "Hello, Aman!"
sayHello("?");    // "Hello, Aman?"
```

### Practical Example: Borrowing Methods

```jsx
const arrayLike = { 0: "a", 1: "b", length: 2 };

// Borrow Array methods
const arr = Array.prototype.slice.call(arrayLike);  // ["a", "b"]
const arr2 = [...arrayLike];  // Modern spread (if iterable)
```

---

## Prototypes

### What is a Prototype?

Every object has a hidden `[[Prototype]]` link (exposed as `__proto__`) to another object. When you access a property, JS looks:
1. On the object
2. On its prototype
3. On prototype's prototype...
4. Until `null`

### `__proto__` vs `prototype` — The Confusing Pair

| Property | On | Purpose |
|----------|-----|---------|
| `prototype` | **Constructor functions** | Blueprint for instances created with `new` |
| `__proto__` | **Instances (objects)** | Actual link to prototype object |

```jsx
function User(name) {
    this.name = name;
}

User.prototype.greet = function() {
    console.log(`Hi, I'm ${this.name}`);
};

const user1 = new User("Aman");
const user2 = new User("Riya");

user1.greet();  // "Hi, I'm Aman"
user2.greet();  // "Hi, I'm Riya"

// Diagram:
/*
User.prototype = { greet: ƒ, constructor: User }
       ↑
       │ __proto__
       │
user1 = { name: "Aman" }
user2 = { name: "Riya" }
*/
```

### Prototype Chain

```jsx
const arr = [1, 2, 3];

arr.__proto__ === Array.prototype;        // true
Array.prototype.__proto__ === Object.prototype;  // true
Object.prototype.__proto__ === null;      // true (end of chain)
```

### `Object.create(proto)`

Creates object with specified prototype — **no constructor needed.**

```jsx
const animal = {
    breathe() { console.log("Breathing..."); }
};

const dog = Object.create(animal);
dog.bark = function() { console.log("Woof!"); };

dog.breathe();  // Inherited from animal
dog.bark();     // Own method

// animal is dog's prototype
dog.__proto__ === animal;  // true
```

### Prototype Inheritance (Pre-ES6)

```jsx
function Animal(name) {
    this.name = name;
}

Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound`);
};

function Dog(name, breed) {
    Animal.call(this, name);  // Call parent constructor
    this.breed = breed;
}

// Set up inheritance
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;  // Fix constructor

Dog.prototype.speak = function() {
    console.log(`${this.name} barks`);
};

const dog = new Dog("Buddy", "Labrador");
dog.speak();  // "Buddy barks"
```

---

## ES6 Classes

**Classes are syntactic sugar over prototypes.** Same behavior, cleaner syntax.

### Basic Class

```jsx
class User {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hi, I'm ${this.name}, ${this.age}`);
    }

    // Getter
    get birthYear() {
        return new Date().getFullYear() - this.age;
    }

    // Setter
    set birthYear(year) {
        this.age = new Date().getFullYear() - year;
    }
}

const user = new User("Aman", 25);
user.greet();           // "Hi, I'm Aman, 25"
console.log(user.birthYear);  // 1999 (getter)
user.birthYear = 2000;  // Sets age to 24 (setter)
```

### Inheritance with `extends` and `super`

```jsx
class Animal {
    constructor(name) {
        this.name = name;
    }

    speak() {
        console.log(`${this.name} makes a sound`);
    }
}

class Dog extends Animal {
    constructor(name, breed) {
        super(name);  // Call parent constructor
        this.breed = breed;
    }

    speak() {
        super.speak();  // Call parent method
        console.log(`${this.name} barks`);
    }
}

const dog = new Dog("Buddy", "Labrador");
dog.speak();
// "Buddy makes a sound"
// "Buddy barks"
```

### Static Methods & Properties

```jsx
class MathUtils {
    static PI = 3.14159;

    static add(a, b) {
        return a + b;
    }

    static createAdder(x) {
        return (y) => x + y;
    }
}

MathUtils.PI;           // 3.14159
MathUtils.add(2, 3);    // 5
const add5 = MathUtils.createAdder(5);
add5(10);               // 15
```

### Private Fields (`#`)

```jsx
class BankAccount {
    #balance = 0;  // Truly private

    deposit(amount) {
        this.#balance += amount;
    }

    getBalance() {
        return this.#balance;
    }
}

const acc = new BankAccount();
acc.deposit(100);
acc.getBalance();  // 100
// acc.#balance;   // SyntaxError: Private field
```

### Classes = Syntactic Sugar (Proof)

```jsx
// This class:
class User {
    constructor(name) {
        this.name = name;
    }
    greet() { console.log(this.name); }
}

// Is roughly equivalent to:
function User(name) {
    this.name = name;
}
User.prototype.greet = function() {
    console.log(this.name);
};

// Proof:
class User {}
typeof User;           // "function"
User.prototype.constructor === User;  // true

const u = new User();
u instanceof User;    // true
```

---

## Phase 4 Checklist

- [ ] Explain what `this` refers to in 5+ contexts
- [ ] Use `call`, `apply`, `bind` correctly
- [ ] Explain difference between `prototype` and `__proto__`
- [ ] Draw prototype chain for `[]`, `{}`, custom objects
- [ ] Use `Object.create` for prototype-based inheritance
- [ ] Implement prototype inheritance (pre-ES6 pattern)
- [ ] Write ES6 classes with constructor, methods, getters/setters
- [ ] Use `extends` and `super` for inheritance
- [ ] Use static methods/properties
- [ ] Use private fields (`#`)
- [ ] Prove classes are syntactic sugar over prototypes

---

*Next: Phase 5 — Asynchronous JavaScript (Promises, async/await, Event Loop)*