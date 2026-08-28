# Phase 2 — Functions, Arrays & Objects Practice Questions

*To be created — scaffold for practice questions matching Phase2Functions.md*

---

## Functions (Q1-Q10)

### Q1. Function Declaration vs Expression vs Arrow
Write the same function `add(a, b)` three ways. Explain hoisting differences.

### Q2. Default Parameters
Create `greet(name, greeting = "Hello")`. Call with 1 and 2 arguments.

### Q3. Rest Parameters
Write `sum(...nums)` that returns sum of all arguments.

### Q4. Return Values & Early Return
Write `findUser(users, id)` that returns user or `null`. Use early return.

### Q5. Functions as Arguments (Callbacks)
Write `operate(a, b, fn)` that applies `fn` to `a` and `b`.

### Q6. Functions Returning Functions (Factories)
Create `createMultiplier(factor)` that returns a function multiplying by factor.

### Q7. Higher-Order Functions
Use `map`, `filter`, `reduce` on `[1,2,3,4,5]` to get sum of doubled evens.

### Q8. Pure vs Impure
Identify which are pure: `add(a,b)`, `pushToArray(arr, x)`, `Math.random()`, `Date.now()`.

### Q9. Recursion
Write `factorial(n)` and `fibonacci(n)` recursively with base cases.

### Q10. IIFE
Create an IIFE that logs a private counter, incrementing each call.

---

## Arrays (Q11-Q20)

### Q11. Mutating vs Non-Mutating
Given `arr = [1,2,3]`, show mutating (`push`, `splice`) vs non-mutating (`slice`, `map`) equivalents.

### Q12. Map/Filter/Reduce Choice
For each task, pick the right method:
- Double all numbers
- Keep only numbers > 10
- Sum all numbers
- Find first even number
- Check if any number > 100
- Check if all numbers positive

### Q13. Array Destructuring
Destructure `[a, b, ...rest]` from `[1,2,3,4,5]`. Swap two variables with destructuring.

### Q14. Spread for Copy/Merge
Create independent copy of `arr`. Merge `arr1` and `arr2` with spread.

### Q15. Shallow Copy Gotcha
Predict: `const a = [[1,2],[3,4]]; const b = [...a]; b[0].push(99); console.log(a);`

### Q16. 2D Array Access
Access `matrix[1][2]` from `[[1,2,3],[4,5,6],[7,8,9]]`. Print all with nested loops.

### Q17. Matrix Sum
Sum all values in 2D array. Bonus: `reduce` inside `reduce`.

### Q18. Reference Behavior
Explain: `const a = [1]; const b = a; b.push(2); console.log(a);` vs spread copy.

### Q19. Compare Arrays by Value
Write `arraysEqual(a, b)` returning true if same values in same order.

### Q20. Pipeline Challenge
From `scores = [72, 91, 38, 88, 45, 99, 67, 83, 29]`:
- Keep >= 40
- Add 5 grace marks (max 100)
- Sort descending
- Take top 3
- Chain methods

---

## Objects (Q21-Q30)

### Q21. Object Creation & Access
Create `user` with `name`, `age`, `greet()` method. Access with dot and bracket.

### Q22. Property Operations
Add `email`, update `age`, delete `city`. Check if `name` exists.

### Q23. Object Destructuring
Destructure `{ name, age: years, city = "Unknown" }` from user object.

### Q24. Spread with Objects
Merge `defaults` and `userPrefs` with spread. Create shallow copy.

### Q25. Object.keys/values/entries
Print all keys, values, and key-value pairs of an object.

### Q26. Object.freeze/seal
Freeze an object, try to modify. Seal an object, add/delete/modify.

### Q27. Looping Objects
Loop with `for...in` and `Object.entries().forEach()`. Compare.

### Q28. Nested Objects
Access `user.address.city.zip` safely with optional chaining.

### Q29. Method `this` Context
Create object with method using `this`. Call directly vs extract to variable.

### Q30. Mini Project: Shopping Cart
Array of `{ name, price, qty }`. Functions: add, remove, updateQty, getTotal, applyDiscount(code).

---

## Solutions

*Solutions to be added after Phase 2 content is finalized.*

---

## Interview Questions (Phase 2)

1. Difference between function declaration, expression, arrow function?
2. What is a higher-order function? Give 3 examples.
3. What makes a function pure? Why does it matter?
4. When to use `map` vs `filter` vs `reduce`?
5. What does spread do with nested arrays? How to deep copy?
6. How does `this` work in object methods vs arrow functions?
6. What's the difference between `Object.freeze` and `Object.seal`?
7. How do you loop over object properties?
8. What is the prototype chain?
9. How does `extends`/`super` work under the hood?