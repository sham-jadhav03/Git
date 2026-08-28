# JS  God Mode Phase 1 Practice Sheet Revised

# Phase 1 — Foundations Practice Questions

## Question 1 — Variables + Template Literals

Create variables for a student’s `name`, `age`, `city`, and `isStudent`.

Print exactly this kind of sentence using a template literal:

```
Aman is 22 years old, lives in Bhopal, and student status is true.
```

Use `const` wherever the value does not need to change.

---

## Question 2 — Declaration, Initialization and Reassignment

Write code that does all of the following:

1. Declare a variable `score` without assigning a value.
2. Print its value.
3. Assign `10` to it.
4. Increase it to `25`.
5. Create a `const` variable named `country` with value `"India"`.
6. Try to reassign `country` and observe what happens.

---

## Question 3 — `typeof` Practice

Create one value for each of these primitive types:

- string
- number
- boolean
- undefined
- null
- bigint
- symbol

Print the value and its `typeof`.

Also observe the result of:

```jsx
typeof null
```

---

## Question 4 — User Input and Explicit Type Conversion

Take two values from the user using `prompt()`.

Convert them into numbers and print:

- sum
- difference
- product
- division
- remainder
- first number raised to the power of second number

If the user enters `10` and `3`, the program should perform actual mathematical operations instead of string concatenation.

---

## Question 5 — Type Coercion Output Challenge

Without running the code first, predict the output of every line. Then run it and verify your answers.

```jsx
console.log("5" + 3);
console.log("5" - 3);
console.log("5" * "2");
console.log(true + 1);
console.log(false + 1);
console.log(null + 1);
console.log(undefined + 1);
```

After checking the output, add a comment beside every line explaining which conversion JavaScript performed.

---

## Question 6 — Pre-Increment vs Post-Increment

Predict the final values of `x`, `a`, and `b`, then verify them by running the code.

```jsx
let x = 5;

let a = x++;
let b = ++x;

console.log(x);
console.log(a);
console.log(b);
```

After that, write another example yourself using decrement operators `--`.

---

## Question 7 — Assignment Operators

Start with:

```jsx
let balance = 1000;
```

Perform these operations using assignment operators only:

1. Add `500`
2. Subtract `200`
3. Multiply the remaining value by `2`
4. Divide it by `4`
5. Store the remainder after dividing it by `300`

Print `balance` after every operation.

Do not write expressions like:

```jsx
balance = balance + 500;
```

Use `+=`, `-=`, `*=`, `/=`, `%=`.

---

## Question 8 — `==` vs `===`

Predict and then print the result of:

```jsx
5 == "5"
5 === "5"
0 == false
0 === false
"" == false
"" === false
null == undefined
null === undefined
```

For every comparison, write a comment explaining why the result is `true` or `false`.

---

## Question 9 — Truthy, Falsy and Short-Circuiting

Create these variables:

```jsx
let userName = "";
let enteredAge = 0;
let customTheme = null;
```

Using `||`, create fallback values:

```
userName → "Guest"
enteredAge → 18
customTheme → "light"
```

Then predict the output of:

```jsx
console.log("hello" && "world");
console.log(0 && "hello");
console.log("" || "default");
console.log("user" || "guest");
```

---

## Question 10 — Ternary Operator

Take a user’s age using `prompt()`.

Using only a ternary operator, store:

```
"Adult"
```

if age is `18` or above, otherwise store:

```
"Minor"
```

Print the final result.

---

## Question 11 — String Cleanup

Take this value:

```jsx
let text = "   JavaScript God Mode   ";
```

Without manually changing the original text, print:

1. original length
2. trimmed string
3. trimmed string length
4. uppercase version
5. lowercase version

---

## Question 12 — String Search and Extraction

Use:

```jsx
let text = "JavaScript is powerful";
```

Write code to:

1. Check whether `"Script"` exists.
2. Find the index of `"is"`.
3. Extract `"JavaScript"` using `slice()`.
4. Extract `"powerful"` using `substring()`.
5. Replace `"powerful"` with `"awesome"`.
6. Check whether the string starts with `"Java"`.
7. Check whether it ends with `"powerful"`.
8. Print the first character using both `charAt()` and bracket notation.

---

## Question 13 — Number Conversion and Validation

Given:

```jsx
let price = "499px";
let rating = "4.8stars";
let invalidValue = "hello";
```

Use the appropriate methods to produce:

```
499
4.8
NaN
```

Also check:

```jsx
Number.isInteger(499)
Number.isInteger(4.8)
```

Print all results.

---

## Question 14 — Math Methods

Given:

```jsx
let value = -4.7;
```

Print:

- absolute value
- rounded value
- floor value
- ceil value

Then print:

- maximum of `12, 45, 7, 31`
- minimum of `12, 45, 7, 31`
- square root of `144`
- `2` raised to power `10` using `Math.pow()`

---

## Question 15 — Random Integer Generator

Generate a random integer between `1` and `6`, inclusive, to simulate a dice roll.

Then modify the same logic so that it can generate a random integer between any two variables:

```jsx
let min = 20;
let max = 30;
```

The result must include both `20` and `30` as possible values.

---

## Question 16 — Grade Calculator

Take marks from the user.

Use `if / else if / else` and print:

```
90–100  → A
80–89   → B
70–79   → C
60–69   → D
Below 60 → F
```

If marks are below `0` or above `100`, print:

```
Invalid marks
```

---

## Question 17 — Nested `if`

Take the user’s age and whether they have a driving licence.

Rules:

- If age is below `18`, print `Not eligible to drive`.
- If age is `18` or above:
    - if they have a licence, print `You can drive`.
    - otherwise print `You need a licence`.

Use a nested `if`.

---

## Question 18 — `switch` and Fall-Through

Take a number from `1` to `7`.

Print the corresponding day:

```
1 → Monday
2 → Tuesday
3 → Wednesday
4 → Thursday
5 → Friday
6 → Saturday
7 → Sunday
```

Additionally:

- For Monday to Friday, print `Weekday`.
- For Saturday and Sunday, print `Weekend`.

Use `switch`. Try to use intentional fall-through for Saturday and Sunday where appropriate.

---

## Question 19 — Loop Practice

Take a number from the user and print its multiplication table from `1` to `10` using a `for` loop.

Example for `5`:

```
5 x 1 = 5
5 x 2 = 10
...
5 x 10 = 50
```

Use template literals for the output.

---

## Question 20 — `while`, `do...while`, `for...of`, `break`, `continue`

Complete all four tasks:

### A. `while`

Print numbers from `1` to `10` using a `while` loop.

### B. `do...while`

Start with:

```jsx
let x = 10;
```

Run a `do...while` whose condition is false from the beginning, but prove that the body still executes once.

### C. `for...of`

Loop through:

```jsx
let word = "JavaScript";
```

and print every character separately.

### D. `break` and `continue`

Print numbers from `1` to `20`:

- skip multiples of `3` using `continue`
- completely stop the loop when the number reaches `17` using `break`

---

## Question 21 — Mini Project: Simple Calculator

Take:

- first number
- operator (`+`, , , `/`)
- second number

from the user.

Perform the selected operation.

Requirements:

- Convert numeric inputs correctly.
- Handle all four operators.
- Do not allow division by zero.
- Print `Invalid operator` for unsupported operators.

---

## Question 22 — Mini Project: FizzBuzz

Print numbers from `1` to `50`.

Rules:

- multiple of `3` → `Fizz`
- multiple of `5` → `Buzz`
- multiple of both `3` and `5` → `FizzBuzz`
- otherwise print the number

Make sure `15`, `30`, and `45` print `FizzBuzz`, not just `Fizz` or `Buzz`.

---

## Question 23 — Mini Project: Number Guessing Game

Generate a random secret integer between `1` and `100`.

Repeatedly ask the user to guess the number.

After every wrong guess print:

```
Too high!
```

or:

```
Too low!
```

When the user guesses correctly, print how many attempts were required.

Use a `do...while` loop.

---

## Question 24 — Mini Project: Temperature Converter

Take:

1. a temperature
2. its unit, either `C` or `F`

If the user enters Celsius, convert it to Fahrenheit.

If the user enters Fahrenheit, convert it to Celsius.

Formulas:

```
F = (C × 9/5) + 32
C = (F - 32) × 5/9
```

Print the converted result with exactly two decimal places.

Accept lowercase `c` and `f` too.

---

## Question 25 — Mini Project: Count Vowels

Take a string from the user.

Count how many vowels it contains:

```
a, e, i, o, u
```

The solution should work with uppercase and lowercase letters.

Use:

- `toLowerCase()`
- `for...of`
- `includes()`

Example:

```
Input: JavaScript
Output: 3
```

---

# Solutions — Practice Questions

## Solution 1

```jsx
const name = "Aman";
const age = 22;
const city = "Bhopal";
const isStudent = true;

console.log(
  `${name} is${age} years old, lives in${city}, and student status is${isStudent}.`
);
```

**Explanation:** Yahan values change nahi ho rahi hain, isliye `const` sahi choice hai. Template literal backticks ke andar `${variable}` se values directly string mein insert ho jaati hain. Isse `+` se unnecessary concatenation karne ki zarurat nahi padti.

---

## Solution 2

```jsx
let score;

console.log(score); // undefined

score = 10;
console.log(score);

score = 25;
console.log(score);

const country = "India";

// country = "USA"; // TypeError
```

**Explanation:** `let score;` sirf declaration hai. Abhi value assign nahi hui, isliye value `undefined` hai. `score = 10` initialization/assignment karta hai aur baad mein `score = 25` reassignment hai.

`const country = "India"` ko reassign nahi kar sakte. Agar `country = "USA"` run karoge to JavaScript error dega because constant binding ko dobara assign nahi kiya ja sakta.

---

## Solution 3

```jsx
const stringValue = "JavaScript";
const numberValue = 42;
const booleanValue = true;
let undefinedValue;
const nullValue = null;
const bigintValue = 9007199254740993n;
const symbolValue = Symbol("id");

console.log(stringValue, typeof stringValue);
console.log(numberValue, typeof numberValue);
console.log(booleanValue, typeof booleanValue);
console.log(undefinedValue, typeof undefinedValue);
console.log(nullValue, typeof nullValue);
console.log(bigintValue, typeof bigintValue);
console.log(symbolValue, typeof symbolValue);
```

**Explanation:** JavaScript mein 7 primitive types hain. Important interview quirk ye hai:

```jsx
typeof null
```

`"object"` return karta hai. `null` actually primitive hai. Ye JavaScript ka old historical bug hai, isliye `typeof null` dekhkar `null` ko object mat samajhna.

---

## Solution 4

```jsx
const first = Number(prompt("Enter first number:"));
const second = Number(prompt("Enter second number:"));

console.log("Sum:", first + second);
console.log("Difference:", first - second);
console.log("Product:", first * second);
console.log("Division:", first / second);
console.log("Remainder:", first % second);
console.log("Power:", first ** second);
```

**Explanation:** `prompt()` hamesha string return karta hai. Agar input `"10"` aur `"3"` ho aur `Number()` na lagao, to `+` ke case mein result `"103"` aa sakta hai. Isliye pehle explicit conversion karna important hai.

`%` remainder deta hai aur `**` exponentiation ke liye use hota hai.

---

## Solution 5

```jsx
console.log("5" + 3);       // "53"
console.log("5" - 3);       // 2
console.log("5" * "2");     // 10
console.log(true + 1);      // 2
console.log(false + 1);     // 1
console.log(null + 1);      // 1
console.log(undefined + 1); // NaN
```

**Explanation:** `+` special hai. Agar ek operand string hai, JavaScript concatenation kar sakti hai, isliye `"5" + 3` becomes `"53"`.

Baaki mathematical operators numeric operation try karte hain. Isliye `"5" - 3` mein `"5"` number `5` mein coerce ho jaata hai.

Numeric context mein:

```
true      → 1
false     → 0
null      → 0
undefined → NaN
```

---

## Solution 6

```jsx
let x = 5;

let a = x++;
let b = ++x;

console.log(x); // 7
console.log(a); // 5
console.log(b); // 7
```

Decrement example:

```jsx
let n = 10;

let p = n--;
let q = --n;

console.log(n); // 8
console.log(p); // 10
console.log(q); // 8
```

**Explanation:** Post-increment `x++` pehle old value expression ko deta hai, uske baad `x` increase hota hai. Pre-increment `++x` pehle value increase karta hai, phir updated value expression ko deta hai.

Isi logic ka reverse decrement operators ke saath hota hai.

---

## Solution 7

```jsx
let balance = 1000;

balance += 500;
console.log(balance); // 1500

balance -= 200;
console.log(balance); // 1300

balance *= 2;
console.log(balance); // 2600

balance /= 4;
console.log(balance); // 650

balance %= 300;
console.log(balance); // 50
```

**Explanation:** Assignment operators existing value par operation karke result wapas same variable mein store kar dete hain.

For example:

```jsx
balance += 500;
```

same idea hai as:

```jsx
balance = balance + 500;
```

Bas syntax shorter hai.

---

## Solution 8

```jsx
console.log(5 == "5");          // true
console.log(5 === "5");         // false

console.log(0 == false);        // true
console.log(0 === false);       // false

console.log("" == false);       // true
console.log("" === false);      // false

console.log(null == undefined); // true
console.log(null === undefined);// false
```

**Explanation:** `==` loose equality hai aur comparison se pehle type coercion kar sakta hai. Isi wajah se surprising results milte hain.

`===` strict equality hai. Ye value ke saath type bhi compare karta hai.

Example:

```jsx
5 === "5"
```

false hai because ek `number` hai aur doosra `string`.

Isi reason se normal code mein `===` aur `!==` prefer karna better hai.

---

## Solution 9

```jsx
let userName = "";
let enteredAge = 0;
let customTheme = null;

userName = userName || "Guest";
enteredAge = enteredAge || 18;
customTheme = customTheme || "light";

console.log(userName);    // Guest
console.log(enteredAge);  // 18
console.log(customTheme); // light

console.log("hello" && "world"); // world
console.log(0 && "hello");       // 0
console.log("" || "default");    // default
console.log("user" || "guest");  // user
```

**Explanation:** `||` first truthy value return karta hai. `""`, `0`, aur `null` falsy hain, isliye fallback values choose ho jaati hain.

`&&` first falsy value return karta hai. Agar sab truthy hain to last value return karta hai.

Important point: `&&` aur `||` hamesha sirf `true` ya `false` return nahi karte. Ye actual operand values bhi return kar sakte hain.

---

## Solution 10

```jsx
const age = Number(prompt("Enter your age:"));

const status = age >= 18 ? "Adult" : "Minor";

console.log(status);
```

**Explanation:** Ternary operator ka syntax hai:

```jsx
condition ? valueIfTrue : valueIfFalse
```

Agar `age >= 18` true hai to `"Adult"` milega, otherwise `"Minor"`.

---

## Solution 11

```jsx
let text = "   JavaScript God Mode   ";

console.log("Original length:", text.length);

const trimmed = text.trim();

console.log("Trimmed:", trimmed);
console.log("Trimmed length:", trimmed.length);
console.log("Uppercase:", trimmed.toUpperCase());
console.log("Lowercase:", trimmed.toLowerCase());
```

**Explanation:** `trim()` beginning aur ending ke extra spaces remove karta hai. Original string directly change nahi hoti. Method ek new string return karta hai.

Isi tarah `toUpperCase()` aur `toLowerCase()` bhi transformed string return karte hain.

---

## Solution 12

```jsx
let text = "JavaScript is powerful";

console.log(text.includes("Script"));       // true
console.log(text.indexOf("is"));            // 11
console.log(text.slice(0, 10));             // JavaScript
console.log(text.substring(14, 22));        // powerful
console.log(text.replace("powerful", "awesome"));
console.log(text.startsWith("Java"));        // true
console.log(text.endsWith("powerful"));      // true
console.log(text.charAt(0));                 // J
console.log(text[0]);                        // J
```

**Explanation:** Har method ka different purpose hai.

- `includes()` presence check karta hai.
- `indexOf()` starting index deta hai.
- `slice()` aur `substring()` string ka portion extract karte hain.
- `replace()` matching text ko replace karke new string return karta hai.
- `startsWith()` aur `endsWith()` boolean return karte hain.
- `charAt(0)` aur `text[0]` dono first character access kar sakte hain.

---

## Solution 13

```jsx
let price = "499px";
let rating = "4.8stars";
let invalidValue = "hello";

console.log(parseInt(price));          // 499
console.log(parseFloat(rating));       // 4.8
console.log(Number(invalidValue));     // NaN

console.log(Number.isInteger(499));    // true
console.log(Number.isInteger(4.8));    // false
```

**Explanation:** `Number("499px")` `NaN` deta because poori string valid number nahi hai.

`parseInt("499px")` beginning ka integer part parse kar leta hai. `parseFloat("4.8stars")` decimal part parse kar leta hai.

`Number.isInteger()` check karta hai ki given value integer number hai ya nahi.

---

## Solution 14

```jsx
let value = -4.7;

console.log(Math.abs(value));   // 4.7
console.log(Math.round(value)); // -5
console.log(Math.floor(value)); // -5
console.log(Math.ceil(value));  // -4

console.log(Math.max(12, 45, 7, 31)); // 45
console.log(Math.min(12, 45, 7, 31)); // 7
console.log(Math.sqrt(144));           // 12
console.log(Math.pow(2, 10));          // 1024
```

**Explanation:** `Math.floor()` hamesha lower integer ki taraf jaata hai, isliye negative numbers ke case mein ye beginners ko confuse kar sakta hai.

For example:

```jsx
Math.floor(-4.7)
```

- `5` deta hai, `4` nahi.

`Math.ceil()` upper integer ki taraf jaata hai, so result `-4` hai.

---

## Solution 15

```jsx
const dice = Math.floor(Math.random() * 6) + 1;

console.log(dice);
```

Generic version:

```jsx
let min = 20;
let max = 30;

const randomNumber =
  Math.floor(Math.random() * (max - min + 1)) + min;

console.log(randomNumber);
```

**Explanation:** `Math.random()` `0` inclusive aur `1` exclusive ke beech decimal deta hai.

Range ko inclusive banane ke liye common formula hai:

```jsx
Math.floor(Math.random() * (max - min + 1)) + min
```

`+1` important hai because maximum value ko bhi possible banana hai.

---

## Solution 16

```jsx
const marks = Number(prompt("Enter marks:"));

if (marks < 0 || marks > 100) {
  console.log("Invalid marks");
} else if (marks >= 90) {
  console.log("A");
} else if (marks >= 80) {
  console.log("B");
} else if (marks >= 70) {
  console.log("C");
} else if (marks >= 60) {
  console.log("D");
} else {
  console.log("F");
}
```

**Explanation:** Sabse pehle invalid input handle kiya gaya hai. Uske baad conditions highest range se lowest range tak check ho rahi hain.

Agar marks `84` hain, `marks >= 90` false hoga aur `marks >= 80` true hote hi `"B"` print ho jayega. Baaki chain skip ho jaayegi.

---

## Solution 17

```jsx
const age = Number(prompt("Enter your age:"));
const hasLicence =
  prompt("Do you have a driving licence? yes/no").toLowerCase() === "yes";

if (age >= 18) {
  if (hasLicence) {
    console.log("You can drive");
  } else {
    console.log("You need a licence");
  }
} else {
  console.log("Not eligible to drive");
}
```

**Explanation:** Outer `if` pehle age eligibility decide kar raha hai. Sirf agar user `18+` hai tab inner `if` licence check karta hai.

Ye nested `if` ka clear use case hai: second condition ko tabhi check karna hai jab first condition satisfy ho.

---

## Solution 18

```jsx
const day = Number(prompt("Enter day number from 1 to 7:"));

switch (day) {
  case 1:
    console.log("Monday");
    console.log("Weekday");
    break;

  case 2:
    console.log("Tuesday");
    console.log("Weekday");
    break;

  case 3:
    console.log("Wednesday");
    console.log("Weekday");
    break;

  case 4:
    console.log("Thursday");
    console.log("Weekday");
    break;

  case 5:
    console.log("Friday");
    console.log("Weekday");
    break;

  case 6:
    console.log("Saturday");
    console.log("Weekend");
    break;

  case 7:
    console.log("Sunday");
    console.log("Weekend");
    break;

  default:
    console.log("Invalid day");
}
```

Alternative grouping example:

```jsx
const type = Number(prompt("Enter 6 for Saturday or 7 for Sunday:"));

switch (type) {
  case 6:
  case 7:
    console.log("Weekend");
    break;

  default:
    console.log("Not weekend");
}
```

**Explanation:** `switch` exact values compare karta hai aur comparison strict hota hai. `break` matching case ke baad switch ko stop karta hai.

Second example mein `case 6` ke baad deliberately `break` nahi hai. Execution `case 7` ke shared code tak fall through karta hai. Ye intentional fall-through hai.

---

## Solution 19

```jsx
const number = Number(prompt("Enter a number:"));

for (let i = 1; i <= 10; i++) {
  console.log(`${number} x${i} =${number * i}`);
}
```

**Explanation:** `for` loop mein initialization, condition aur update ek jagah clearly visible hain.

```jsx
let i = 1
```

se start hota hai, `i <= 10` tak chalta hai aur har iteration ke baad `i++` hota hai.

---

## Solution 20

### A. `while`

```jsx
let i = 1;

while (i <= 10) {
  console.log(i);
  i++;
}
```

### B. `do...while`

```jsx
let x = 10;

do {
  console.log(x);
  x++;
} while (x < 5);
```

### C. `for...of`

```jsx
let word = "JavaScript";

for (let character of word) {
  console.log(character);
}
```

### D. `break` and `continue`

```jsx
for (let n = 1; n <= 20; n++) {
  if (n === 17) {
    break;
  }

  if (n % 3 === 0) {
    continue;
  }

  console.log(n);
}
```

**Explanation:** `while` condition pehle check karta hai. `do...while` body ko pehle execute karta hai, isliye false condition ke bawajood ek baar run hota hai.

`for...of` iterable ki values deta hai, yahan string ka har character.

`continue` sirf current iteration skip karta hai. `break` complete loop terminate kar deta hai.

---

## Solution 21

```jsx
const num1 = Number(prompt("Enter first number:"));
const operator = prompt("Enter operator (+, -, *, /):");
const num2 = Number(prompt("Enter second number:"));

let result;

if (operator === "+") {
  result = num1 + num2;
} else if (operator === "-") {
  result = num1 - num2;
} else if (operator === "*") {
  result = num1 * num2;
} else if (operator === "/") {
  result = num2 !== 0 ? num1 / num2 : "Cannot divide by zero";
} else {
  result = "Invalid operator";
}

console.log("Result:", result);
```

**Explanation:** Numbers ko `Number()` se convert karna zaroori hai because `prompt()` strings deta hai.

Division ke case mein `num2 !== 0` check kiya hai. Ternary se valid division aur divide-by-zero case dono handle ho gaye.

Operator comparisons ke liye strict equality `===` use ki gayi hai.

---

## Solution 22

```jsx
for (let i = 1; i <= 50; i++) {
  if (i % 3 === 0 && i % 5 === 0) {
    console.log("FizzBuzz");
  } else if (i % 3 === 0) {
    console.log("Fizz");
  } else if (i % 5 === 0) {
    console.log("Buzz");
  } else {
    console.log(i);
  }
}
```

**Explanation:** Sabse important part condition order hai.

`15` both `3` and `5` se divisible hai. Agar pehle sirf `i % 3 === 0` check karoge to `"Fizz"` print ho jayega aur `FizzBuzz` case kabhi nahi milega.

Isliye most specific condition:

```jsx
i % 3 === 0 && i % 5 === 0
```

sabse pehle aani chahiye.

---

## Solution 23

```jsx
const secret = Math.floor(Math.random() * 100) + 1;

let attempts = 0;
let guess;

do {
  guess = Number(prompt("Guess a number between 1 and 100:"));
  attempts++;

  if (guess > secret) {
    console.log("Too high!");
  } else if (guess < secret) {
    console.log("Too low!");
  }
} while (guess !== secret);

console.log(`You got it in${attempts} attempts!`);
```

**Explanation:** Secret number `1` se `100` inclusive generate ho raha hai.

`do...while` yahan natural choice hai because user ko kam se kam ek guess to dena hi padega.

Har iteration mein `attempts++` count increase karta hai. Loop tab tak chalta hai jab tak:

```jsx
guess !== secret
```

true hai.

---

## Solution 24

```jsx
const temp = Number(prompt("Enter temperature:"));
const unit = prompt("Is it in C or F?").toUpperCase();

if (unit === "C") {
  const fahrenheit = (temp * 9) / 5 + 32;
  console.log(`${temp}°C =${fahrenheit.toFixed(2)}°F`);
} else if (unit === "F") {
  const celsius = ((temp - 32) * 5) / 9;
  console.log(`${temp}°F =${celsius.toFixed(2)}°C`);
} else {
  console.log("Invalid unit");
}
```

**Explanation:** `.toUpperCase()` ki wajah se user `c`, `C`, `f`, ya `F` enter kare, comparison consistent ho jaata hai.

`toFixed(2)` result ko two decimal places mein format karta hai. Important: `toFixed()` ka return value string hota hai.

---

## Solution 25

```jsx
const str = prompt("Enter a string:").toLowerCase();

const vowels = "aeiou";
let count = 0;

for (let character of str) {
  if (vowels.includes(character)) {
    count++;
  }
}

console.log("Vowels:", count);
```

**Explanation:** Pehle poori input lowercase mein convert kar di, isliye uppercase vowels ke liye separate conditions ki zarurat nahi hai.

`for...of` har character deta hai. `vowels.includes(character)` check karta hai ki current character `"aeiou"` mein present hai ya nahi. Match milne par counter increase hota hai.

---

# Interview / Conceptual Questions

## Question 1

What is JavaScript, where can it run, and what is a JavaScript engine?

---

## Question 2

What is the difference between `var`, `let`, and `const`?

---

## Question 3

What is the difference between declaration, initialization, assignment, reassignment, and redeclaration?

---

## Question 4

What are the seven primitive data types in JavaScript? What is the main non-primitive category?

---

## Question 5

What is the difference between `null` and `undefined`? Why does `typeof null` return `"object"`?

---

## Question 6

What is the difference between explicit type conversion and implicit type coercion? Explain why `"5" + 3` and `"5" - 3` behave differently.

---

## Question 7

What are truthy and falsy values? Name all six falsy values covered in this phase.

---

## Question 8

What is the difference between `==` and `===`? Why is `===` generally preferred?

---

## Question 9

What is the difference between pre-increment and post-increment?

Explain:

```jsx
let x = 5;
let a = x++;
let b = ++x;
```

---

## Question 10

How do `&&` and `||` actually work in JavaScript? Do they always return boolean values?

---

## Question 11

Are strings mutable in JavaScript? What happens when methods like `toUpperCase()`, `trim()`, or `replace()` are called?

---

## Question 12

What is the difference between `Number()`, `parseInt()`, and `parseFloat()`? What is `NaN`?

---

## Question 13

When would you use `if / else if / else` instead of `switch`? What is fall-through, and why is `break` important in a `switch`?

---

## Question 14

Explain the difference between `for`, `while`, `do...while`, and `for...of`.

---

## Question 15

What is the difference between `break` and `continue` inside a loop?

---

# Solutions — Interview / Conceptual Questions

## Solution 1

JavaScript ek programming language hai jo originally web pages mein interactivity add karne ke liye create hui thi. Aaj JavaScript browser ke andar websites ke logic ke liye, Node.js ke through servers par, React Native jaise tools ke through mobile apps mein, aur Electron jaise tools ke through desktop apps mein bhi use hoti hai.

JavaScript engine wo software component hai jo JavaScript code ko execute karta hai.

Examples:

```
Chrome  → V8
Firefox → SpiderMonkey
Safari  → JavaScriptCore
Node.js → V8
```

Browser ke andar engine JavaScript run karta hai. Node.js V8 engine ko browser ke bahar JavaScript execute karne ke liye use karta hai.

---

## Solution 2

`var`, `let`, aur `const` teeno variable declaration keywords hain, but behaviour different hai.

```
var   → reassign ho sakta hai, redeclare bhi ho sakta hai
let   → reassign ho sakta hai, same scope mein redeclare nahi
const → reassign nahi ho sakta, same scope mein redeclare nahi
```

`let` aur `const` block scoped hain. `var` function scoped hota hai.

Modern JavaScript mein general rule:

```
const → default choice
let   → jab value actually change hogi
var   → generally avoid
```

`var` ki deeper scoping aur hoisting behaviour Phase 3 mein zyada clearly samajh aayegi.

---

## Solution 3

**Declaration** means variable create karna:

```jsx
let score;
```

**Initialization** means pehli baar value dena:

```jsx
score = 10;
```

Declaration aur initialization ek saath bhi ho sakte hain:

```jsx
let score = 10;
```

**Assignment** means variable ko value dena.

**Reassignment** means existing variable ki value change karna:

```jsx
score = 20;
```

**Redeclaration** means same scope mein same naam se variable ko dobara declare karna.

```jsx
var x = 10;
var x = 20;
```

`var` ke saath allowed hai, but `let` aur `const` ke saath same scope mein allowed nahi hai.

---

## Solution 4

JavaScript ke seven primitive types hain:

```
string
number
boolean
null
undefined
symbol
bigint
```

Examples:

```jsx
"hello"
42
true
null
undefined
Symbol("id")
123n
```

Main non-primitive category `object` hai. Objects, arrays, dates etc. object system ka part hain. Inhe Phase 2 mein detail mein study kiya jaata hai.

---

## Solution 5

`undefined` normally indicate karta hai ki value abhi assign nahi hui.

```jsx
let x;
console.log(x); // undefined
```

`null` developer intentionally assign karta hai to represent “currently no value”.

```jsx
let selectedUser = null;
```

Simple mental model:

```
undefined → value nahi di gayi
null      → intentionally empty rakha gaya
```

Interesting JavaScript quirk:

```jsx
typeof null
```

returns:

```
"object"
```

Lekin `null` actually primitive value hai. Ye JavaScript ka historical bug hai jo compatibility reasons ki wajah se change nahi kiya gaya.

---

## Solution 6

**Explicit conversion** tab hota hai jab developer khud type convert karta hai:

```jsx
Number("42");
String(100);
Boolean("hello");
```

**Implicit coercion** tab hota hai jab JavaScript automatically conversion karti hai.

```jsx
"5" + 3
```

gives:

```
"53"
```

because `+` ke saath string present hone par concatenation ho sakti hai.

But:

```jsx
"5" - 3
```

gives:

```
2
```

because subtraction numeric operation hai, so JavaScript `"5"` ko number `5` mein coerce karti hai.

Isi wajah se `+` operator coercion questions mein special attention deserve karta hai.

---

## Solution 7

Boolean context mein values truthy ya falsy behave karti hain.

Phase 1 ke six falsy values:

```jsx
false
0
""
null
undefined
NaN
```

Inke alawa almost every normal value truthy hoti hai.

Important examples:

```jsx
Boolean("0")       // true
Boolean("false")   // true
Boolean([])        // true
Boolean({})        // true
```

`"false"` ka content word false hai, but ye non-empty string hai. Isliye value truthy hai.

---

## Solution 8

`==` loose equality hai. Ye comparison se pehle type coercion kar sakta hai.

```jsx
5 == "5" // true
```

`===` strict equality hai. Ye value aur type dono compare karta hai.

```jsx
5 === "5" // false
```

Ek `number` hai aur doosra `string`, isliye strict comparison false.

`===` generally preferred hai because implicit coercion ke surprising results avoid hote hain aur code ka behaviour zyada predictable hota hai.

---

## Solution 9

Post-increment:

```jsx
x++
```

pehle current value expression ko deta hai, phir variable increment hota hai.

Pre-increment:

```jsx
++x
```

pehle variable increment karta hai, phir updated value expression ko deta hai.

Example:

```jsx
let x = 5;

let a = x++; // a = 5, x = 6
let b = ++x; // x = 7, b = 7
```

Final:

```
x = 7
a = 5
b = 7
```

---

## Solution 10

`&&` aur `||` sirf boolean operators samajhna incomplete understanding hai. JavaScript mein ye actual operand values return kar sakte hain.

`&&` first falsy value return karta hai. Agar sab truthy hain to last value return karta hai.

```jsx
"hello" && "world" // "world"
0 && "hello"       // 0
```

`||` first truthy value return karta hai. Agar sab falsy hain to last value return hoti hai.

```jsx
"" || "Guest"      // "Guest"
"user" || "Guest"  // "user"
```

Is behaviour ko short-circuiting kehte hain.

---

## Solution 11

JavaScript strings immutable hoti hain. Matlab existing string ke characters ko directly modify nahi kiya jaata.

Example:

```jsx
let text = "hello";

const upper = text.toUpperCase();

console.log(text);  // hello
console.log(upper); // HELLO
```

`toUpperCase()`, `trim()`, `replace()` jaise methods original string ko mutate nahi karte. Ye transformed **new string** return karte hain.

Agar transformed result preserve karna hai to usse variable mein assign karna padta hai.

---

## Solution 12

`Number()` poori value ko valid number mein convert karne ki try karta hai.

```jsx
Number("42")   // 42
Number("42px") // NaN
```

`parseInt()` beginning se integer part parse karta hai:

```jsx
parseInt("42px") // 42
```

`parseFloat()` decimal number parse kar sakta hai:

```jsx
parseFloat("4.8stars") // 4.8
```

`NaN` ka meaning `Not-a-Number` hai. Ye invalid numeric result ko represent karta hai.

Interesting point:

```jsx
typeof NaN
```

returns:

```
"number"
```

---

## Solution 13

`if / else if / else` tab better hota hai jab:

- ranges check karni ho
- multiple different conditions ho
- logical operators use ho rahe hon

Example:

```jsx
if (marks >= 90) {
  // ...
} else if (marks >= 80) {
  // ...
}
```

`switch` tab readable hota hai jab ek expression ko multiple exact values ke against compare karna ho.

```jsx
switch (day) {
  case 1:
    // ...
    break;
}
```

`switch` strict equality style comparison use karta hai.

Agar matching case ke baad `break` nahi hai, execution next case mein continue kar sakta hai. Is behaviour ko **fall-through** kehte hain.

Kabhi fall-through intentionally useful hota hai, but accidentally ho to bug create kar sakta hai.

---

## Solution 14

### `for`

Jab iterations ka structure clear ho:

```jsx
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

### `while`

Jab loop primarily condition ke basis par chalna ho aur iterations pehle se fixed na hon:

```jsx
while (condition) {
  // ...
}
```

### `do...while`

Body kam se kam ek baar execute hoti hai because condition baad mein check hoti hai:

```jsx
do {
  // runs first
} while (condition);
```

### `for...of`

Iterable ki values par iterate karne ke liye:

```jsx
for (let character of "JS") {
  console.log(character);
}
```

Phase 1 level par strings aur basic iterable examples ke liye ye useful hai.

---

## Solution 15

`break` complete loop ko immediately terminate kar deta hai.

```jsx
for (let i = 1; i <= 10; i++) {
  if (i === 5) break;
  console.log(i);
}
```

Output:

```
1
2
3
4
```

`continue` sirf current iteration ka remaining code skip karta hai aur next iteration par move karta hai.

```jsx
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

Output:

```
1
2
4
5
```

Short version:

```
break    → loop khatam
continue → current round skip
```