# Phase 4 — Objects, `this`, Prototypes, Classes Practice Questions

*To be created — scaffold for practice questions matching Phase4Objects.md*

---

## The `this` Keyword (Q1-Q5)

### Q1. `this` in Global Scope
What is `this` in browser console? In Node REPL? In ES module?

### Q2. `this` in Regular Functions
```jsx
function foo() { console.log(this); }
foo();           // ?
const obj = { foo };
obj.foo();       // ?
new foo();       // ?
```

### Q3. `this` in Methods
```jsx
const user = {
    name: "Aman",
    greet() { console.log(this.name); }
};
user.greet();           // ?
const fn = user.greet;
fn();                   // ?
```

### Q4. `this` in Arrow Functions
```jsx
const obj = {
    name: "Obj",
    regular() { console.log(this.name); },
    arrow: () => console.log(this.name)
};
obj.regular();  // ?
obj.arrow();    // ?
```

### Q5. `this` in Event Handlers
```jsx
btn.addEventListener("click", function() { console.log(this); });
btn.addEventListener("click", () => console.log(this));
// What is `this` in each?
```

---

## Explicit Binding (Q6-Q10)

### Q6. `call` vs `apply` vs `bind`
Given `fn.call(obj, 1, 2)`, `fn.apply(obj, [1,2])`, `fn.bind(obj, 1, 2)`:
- Which invokes immediately?
- Which returns new function?
- Which takes array of args?

### Q7. Borrowing Methods
Use `call` to borrow `Array.prototype.slice` on array-like `{0: 'a', 1: 'b', length: 2}`.

### Q8. Partial Application with `bind`
Create `add5` from `add(a, b)` using `bind`.

### Q9. Fixing `this` in Callbacks
```jsx
const user = {
    name: "Aman",
    greet() { console.log(this.name); }
};
setTimeout(user.greet, 1000);  // Loses `this`
// Fix with bind, arrow, or wrapper
```

### Q10. `this` in Strict Mode
```jsx
"use strict";
function foo() { console.log(this); }
foo();  // ?
```

---

## Prototypes (Q11-Q15)

### Q11. `prototype` vs `__proto__`
```jsx
function User(name) { this.name = name; }
User.prototype.greet = function() { console.log(this.name); };
const u = new User("Aman");

// What is:
User.prototype;
u.__proto__;
u.__proto__ === User.prototype;
User.prototype.__proto__;
```

### Q12. Prototype Chain
Trace the chain for `[]`, `{}`, `new Date()`, `new User()`.

### Q13. `Object.create`
```jsx
const animal = { breathe() { console.log("breathing"); } };
const dog = Object.create(animal);
dog.bark = () => console.log("woof");
dog.breathe();  // Works? Why?
```

### Q14. Prototype Inheritance (Pre-ES6)
Implement `Animal` → `Dog` inheritance without classes. Use `Object.create` and `call`.

### Q15. Prototype Pollution
```jsx
Object.prototype.custom = "hacked";
const obj = {};
console.log(obj.custom);  // ?
// Why is this dangerous?
```

---

## ES6 Classes (Q16-Q25)

### Q16. Basic Class
Write `class User` with constructor, `greet()` method, getter `isAdult` (age >= 18), setter for `age`.

### Q17. Inheritance with `extends`/`super`
Create `Animal` → `Dog` → `Puppy`. Each overrides `speak()` and calls `super.speak()`.

### Q18. Static Methods
Add `static createAnonymous()` to `User` returning `new User("Anonymous")`.

### Q19. Private Fields
```jsx
class Counter {
    #count = 0;
    increment() { this.#count++; }
    getCount() { return this.#count; }
}
// Can you access #count from outside?
```

### Q20. Getters/Setters
Create `Temperature` class with `celsius` getter/setter and `fahrenheit` getter/setter that convert.

### Q21. Classes = Syntactic Sugar
Prove that `class` is a function and `prototype` methods exist.

### Q22. `instanceof` with Classes
```jsx
class A {} class B extends A {}
const b = new B();
b instanceof B;  // ?
b instanceof A;  // ?
b instanceof Object;  // ?
```

### Q23. Method Definition Shorthand
```jsx
class C {
    method1() {}      // On prototype
    static method2() {}  // On constructor
    get prop() {}     // Getter
    set prop(v) {}    // Setter
}
```

### Q24. Subclassing Built-ins
Create `class MyArray extends Array` with custom `first()` method.

### Q25. Mixins / Composition
Implement `canFly`, `canSwim` mixins. Compose into `Duck`, `Fish`, `Penguin`.

---

## Solutions

*Solutions to be added after Phase 4 content is finalized.*

---

## Interview Questions (Phase 4)

1. What determines `this` in JavaScript? Explain all 5 call patterns.
2. Difference between `call`, `apply`, `bind`? When to use each?
3. What is `prototype`? What is `__proto__`? How do they relate?
4. Draw the prototype chain for an array.
5. How does `Object.create` differ from `new Constructor()`?
6. Implement prototype inheritance without `class` syntax.
7. How does `extends`/`super` work under the hood?
8. What are static methods? Where do they live?
9. What are private fields (`#`) and how are they different from `_` convention?
10. Prove that `class` is syntactic sugar over prototypes.