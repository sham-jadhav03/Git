# JavaScript Arrays Practice Sheet | JS God Mode | 25 Questions + Solutions

**Goal:** This sheet is designed to make you *use* JavaScript arrays, not just remember method names. It starts simple and gradually combines arrays with functions, callbacks, loops, conditionals, spread/rest and reference behavior.

## How to Use This Sheet

1. Solve every question without looking at the solution first.
2. Run your code and test it with more than one input.
3. If your answer works, ask yourself: **Does this mutate the original array?**
4. Open the solution only after you have attempted the question.
5. For the final questions, try to explain your approach out loud. If you can explain it clearly, you probably understand it.

**Difficulty Guide:** `Foundation` • `Intermediate` • `Challenge`

---

## Part 1: Practice Questions

### Q1. Create, Access and Update `Foundation`

Create an array called `languages` containing `"JavaScript"`, `"Python"`, `"Java"` and `"C++"`.

1. Print the first element.
2. Print the third element.
3. Change `"Java"` to `"TypeScript"`.
4. Print the final array.

---

### Q2. Get the Last Element `Foundation`

Given:

```jsx
let cities = ["Bhopal", "Indore", "Delhi", "Bengaluru", "Pune"];
```

Print the last element in **two different ways** without hardcoding the last index.

---

### Q3. Understanding `length` `Foundation`

Given:

```jsx
let numbers = [10, 20, 30, 40, 50];
```

1. Print its length.
2. Print the last valid index using `length`.
3. Set the array's length to `3`.
4. Predict and then print the resulting array.

---

### Q4. Build a Queue Using Array Methods `Foundation`

Start with:

```jsx
let queue = ["Aman", "Riya"];
```

Perform these operations in order:

1. Add `"Karan"` to the end.
2. Add `"Sarthak"` to the beginning.
3. Remove the first person and store that name in `servedPerson`.
4. Remove the last person and store that name in `cancelledPerson`.
5. Print the final queue and both removed names.

---

### Q5. Remove Items with `splice` `Foundation`

Given:

```jsx
let topics = ["HTML", "CSS", "JavaScript", "React", "Node.js"];
```

Remove `"JavaScript"` and `"React"` using **one** `splice()` call.

---

### Q6. Insert and Replace with `splice` `Intermediate`

Given:

```jsx
let roadmap = ["HTML", "CSS", "React"];
```

1. Insert `"JavaScript"` between `"CSS"` and `"React"` without removing anything.
2. Then replace `"CSS"` with `"Tailwind CSS"` using `splice()`.

---

### Q7. Numeric Sorting `Intermediate`

Given:

```jsx
let prices = [499, 99, 1299, 299, 999];
```

Create:
- An ascending numeric sort
- A descending numeric sort

Also explain why plain `prices.sort()` is not reliable for numeric sorting.

---

### Q8. `slice()` vs `splice()` `Intermediate`

Given:

```jsx
let arr = [10, 20, 30, 40, 50];
```

Write code that:
1. Extracts `[20, 30, 40]` **without changing** `arr`.
2. Then **removes** `[20, 30, 40]` from the original array.

Use the correct method for each operation.

---

### Q9. Search and Join `Foundation`

Given:

```jsx
let skills = ["HTML", "CSS", "JavaScript", "React"];
```

1. Check whether `"JavaScript"` exists.
2. Find the index of `"React"`.
3. Find the index of `"Node.js"`.
4. Convert the array into the string `"HTML -> CSS -> JavaScript -> React"`.

---

### Q10. `forEach()` and Side Effects `Foundation`

Given:

```jsx
let marks = [45, 67, 89, 32, 76];
```

Use `forEach()` to print:

```
Student 1: 45
Student 2: 67
...
```

Then store the return value of `forEach()` in a variable and print it. **What do you get, and why?**

---

### Q11. Transform Prices with `map()` `Foundation`

An online store has these base prices:

```jsx
let prices = [100, 250, 500, 1000];
```

Create a **new array** containing prices after adding **18% GST** to each value. Do not modify the original array.

**Expected:**
```jsx
[118, 295, 590, 1180]
```

---

### Q12. Filter Passing Students `Foundation`

Given:

```jsx
let scores = [23, 45, 67, 34, 89, 90, 12];
```

1. Create a new array containing only scores **greater than or equal to 40**.
2. Create another array containing only scores **greater than or equal to 80**.

---

### Q13. Find the First Eligible User `Intermediate`

Given:

```jsx
let users = [
  { name: "Aman", age: 17 },
  { name: "Riya", age: 19 },
  { name: "Karan", age: 22 }
];
```

1. Use `find()` to get the first user whose age is at least 18.
2. What would `find()` return if nobody matched?

---

### Q14. Find the Position of the First Expensive Item `Intermediate`

Given:

```jsx
let prices = [199, 499, 799, 1299, 299];
```

1. Use `findIndex()` to find the index of the first price greater than 500.
2. Also test the same logic for a price greater than 5000. What will be returned?

---

### Q15. Validate Data with `some()` and `every()` `Intermediate`

Given:

```jsx
let ages = [19, 22, 17, 24, 30];
```

Use array methods to answer:

1. Is **at least one** person under 18?
2. Is **every** person 18 or older?
3. Is **every** age greater than 0?

---

### Q16. Shopping Cart Total with `reduce()` `Intermediate`

A cart contains item prices:

```jsx
let cart = [499, 1299, 299, 799];
```

1. Use `reduce()` to calculate the total bill.
2. Then calculate the final amount after applying a **flat discount of 500** to the total.

---

### Q17. Destructuring Practice `Intermediate`

Given:

```jsx
let profile = ["Sarthak", 23, "Developer", "Bhopal"];
```

Using array destructuring:

1. Store the first value in `name`.
2. **Skip** the age.
3. Store the third value in `profession`.
4. Store the fourth value in `city`.

Then swap these variables **without creating a third variable**:

```jsx
let first = "frontend";
let second = "backend";
```

---

### Q18. Spread: Copy and Merge `Intermediate`

Given:

```jsx
let frontend = ["HTML", "CSS", "JavaScript"];
let backend = ["Node.js", "Express"];
```

1. Create an **independent top-level copy** of `frontend` using spread.
2. Add `"React"` to the copy and **prove that the original is unchanged**.
3. Create a `fullStack` array containing all frontend and backend technologies using spread.

---

### Q19. Shallow Copy Gotcha `Challenge`

Predict the output before running this code:

```jsx
let original = [[1, 2], [3, 4]];
let copy = [...original];

copy[0].push(99);

console.log(original);
console.log(copy);
```

**Explain** why spreading an array does not create a fully independent deep copy when nested arrays are present.

---

### Q20. Rest Parameters + `reduce()` `Intermediate`

Create a function called `average` that accepts any number of numeric arguments:

```jsx
average(10, 20, 30);       // 20
average(5, 10, 15, 20);    // 12.5
```

Use a **rest parameter** to collect arguments and `reduce()` to calculate the result.

---

### Q21. Work with a 2D Array `Intermediate`

Given:

```jsx
let matrix = [
  [10, 20, 30],
  [40, 50, 60],
  [70, 80, 90]
];
```

1. Print `50` using indexes.
2. Print `90` using indexes.
3. Use **nested loops** to print every value in the matrix.

---

### Q22. Calculate the Sum of a Matrix `Intermediate`

Using the same matrix:

```jsx
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];
```

1. Calculate the sum of all values. Try solving it first with **nested loops**.
2. **Bonus:** Solve it using `reduce()` inside another `reduce()`.

---

### Q23. Reference Behavior `Challenge`

Predict the output and explain each line:

```jsx
let arr1 = [1, 2, 3];
let arr2 = arr1;
let arr3 = [...arr1];

arr2.push(4);
arr3.push(5);

console.log(arr1);
console.log(arr2);
console.log(arr3);
console.log(arr1 === arr2);
console.log(arr1 === arr3);
```

---

### Q24. Compare Two Arrays by Values `Challenge`

JavaScript gives:

```jsx
[1, 2, 3] === [1, 2, 3] // false
```

Write a function:

```jsx
arraysEqual(a, b)
```

that returns `true` when two arrays of primitive values contain the same values in the same order, otherwise `false`.

**Examples:**

```jsx
arraysEqual([1, 2, 3], [1, 2, 3]); // true
arraysEqual([1, 2, 3], [1, 3, 2]); // false
arraysEqual([1, 2], [1, 2, 3]);    // false
```

---

### Q25. Final Challenge: Build a Leaderboard Pipeline `Challenge`

You receive raw student scores:

```jsx
let scores = [72, 91, 38, 88, 45, 99, 67, 83, 29];
```

Without modifying the original `scores` array, create a final array that:

1. Keeps only students who passed (score >= 40).
2. Adds 5 grace marks to every passing score, but **no score may exceed 100**.
3. Sorts the resulting scores from highest to lowest.
4. Keeps only the top 3 scores.

**Expected result:**

```jsx
[100, 96, 93]
```

Try to solve it as a **clean method chain**.

---

## Part 2: Solutions and Explanations

> **Do not speed-run the solutions.** The value of this sheet comes from struggling with the question first and then comparing your thinking with the solution.

### Solution 1: Create, Access and Update

### Solution 2: Get the Last Element

### Solution 3: Understanding length

### Solution 4: Build a Queue

### Solution 5: Remove Items with splice

### Solution 6: Insert and Replace with splice

### Solution 7: Numeric Sorting

### Solution 8: slice vs splice

### Solution 9: Search and Join

### Solution 10: forEach and Side Effects

### Solution 11: Transform Prices with map

### Solution 12: Filter Passing Students

### Solution 13: Find the First Eligible User

### Solution 14: Find the First Expensive Item

### Solution 15: Validate Data with some and every

### Solution 16: Shopping Cart Total with reduce

### Solution 17: Destructuring Practice

### Solution 18: Spread Copy and Merge

### Solution 19: Shallow Copy Gotcha

### Solution 20: Rest Parameters + reduce

### Solution 21: Work with a 2D Array

### Solution 22: Sum of a Matrix

### Solution 23: Reference Behavior

### Solution 24: Compare Arrays by Values

### Solution 25: Final Leaderboard Challenge

---

## Final Revision Checklist

Before moving ahead, make sure you can answer these without notes:

- [ ] I understand why array indexes start at 0.
- [ ] I can get the last array element without hardcoding an index.
- [ ] I know which methods mutate the original array.
- [ ] I can explain `slice()` vs `splice()`.
- [ ] I know why numeric `sort()` needs a compare function.
- [ ] I understand the difference between `forEach()` and `map()`.
- [ ] I can decide when to use `map()`, `filter()`, `reduce()`, `find()`, `some()` and `every()`.
- [ ] I can use destructuring with skipping and defaults.
- [ ] I understand spread vs rest.
- [ ] I know that spread creates a shallow copy.
- [ ] I can access and loop through a 2D array.
- [ ] I understand why assigning one array to another variable copies the reference.
- [ ] I understand why `[] === []` is false.
- [ ] I can combine multiple array methods to solve a real problem.

> If you can solve Q21 to Q25 without copying the solutions, your array fundamentals are in a very solid place. Now don't memorize the methods. Build things with them.