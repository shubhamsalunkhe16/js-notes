# Falsy & Truthy values

- A falsy value is a value that is considered `false` when encountered in a Boolean context

- all values are `truthy` - `except falsy` values

| Value      | Description                                                                                           |
| ---------- | ----------------------------------------------------------------------------------------------------- |
| false      | The keyword false.                                                                                    |
| 0          | The Number zero (so, also 0.0, etc., and 0x0).                                                        |
| -0         | The Number negative zero (so, also -0.0, etc., and -0x0).                                             |
| 0n         | The BigInt zero (so, also 0x0n). Note that there is no BigInt negative zero the negation of 0n is 0n. |
| "", '', `` | Empty string value.                                                                                   |
| null       | null — the absence of any value.                                                                      |
| undefined  | undefined — the primitive value.                                                                      |
| NaN        | NaN — not a number.                                                                                   |

---

# Comparisons

- strings are compared letter-by-letter

```js
alert("Z" > "A"); // true
alert("Glow" > "Glee"); // true
alert("Bee" > "Be"); // true
```

- comparing values of different types, JavaScript converts the values to numbers

```js
alert("2" > 1); // true, string '2' becomes a number 2
alert("01" == 1); // true, string '01' becomes a number 1

// For boolean values, true becomes 1 and false becomes 0
alert(true == 1); // true
alert(false == 0); // true
```

---

## Strict equality

- A strict equality operator `===` checks the equality without type conversion
- checks value and data type both

```js
alert(0 == false); // true
alert(0 === false); // false, because the types are different
```

---

# Logical operators

| Operator | Description        |
| -------- | ------------------ |
| &&       | logical and        |
| \| \|    | logical or         |
| !        | logical not        |
| ??       | Nullish Coalescing |

## || (OR)

- If any of its arguments are `true`, it returns `true`, otherwise it returns `false`.

```js
alert(true || true); // true
alert(false || true); // true
alert(true || false); // true
alert(false || false); // false
```

- `||` finds the `first truthy value`

```js
alert(1 || 0); // 1 (1 is truthy)
alert(null || 1); // 1 (1 is the first truthy value)
alert(null || 0 || 1); // 1 (the first truthy value)
```

- if `all falsy`, returns the `last value`

```js
alert(undefined || null || 0); // 0 (all falsy, returns the last value)

let firstName = "";
let lastName = "";
let nickName = "SuperCoder";

alert(firstName || lastName || nickName || "Anonymous"); // SuperCoder

// If all variables were falsy, "Anonymous" would show up.
```

- `Short-circuit evaluation`

```js
true || alert("not printed"); // true (not alert)
false || alert("printed"); // (alert shown)
```

---

## && (AND)

- AND returns `true` if `both operands are truthy` and `false otherwise`

```js
alert(true && true); // true
alert(false && true); // false
alert(true && false); // false
alert(false && false); // false
```

- If the result is `false`, `stops and returns the original value of that operand`
- `AND` returns the `first falsy value`

```js
alert(1 && 2 && null && 3); // null
```

- When `all values are truthy`, the `last value` is returned

```js
alert(1 && 2 && 3); // 3, the last one
```

- difference in `||` and `&&`is that `AND returns the first falsy value` while `OR returns the first truthy one`

```js
// if the first operand is truthy,
// AND returns the second operand:
alert(1 && 0); // 0
alert(1 && 5); // 5

// if the first operand is falsy,
// AND returns it. The second operand is ignored
alert(null && 5); // null
alert(0 && "no matter what"); // 0
```

#### NOTE :

- The precedence of `&&` operator is `higher than` `||`

- So the code `a && b || c && d` is essentially the same as if the && expressions were in parentheses: `(a && b) || (c && d)`

---

## Nullish coalescing operator '??'

- returns the `first argument if it’s not null/undefined`. Otherwise, the second one.

```js
// The result of a ?? b is:

// if a is defined, then a,
// if a isn’t defined, then b.

result = a !== null && a !== undefined ? a : b;
// same as
result = a ?? b;
```

- The common use case for ?? is `to provide a default value`

```js
let user;
alert(user ?? "Anonymous"); // Anonymous (user not defined)

let user = "John";
alert(user ?? "Anonymous"); // John (user defined)

let firstName = null;
let lastName = null;
let nickName = "Supercoder";
// shows the first defined value:
alert(firstName ?? lastName ?? nickName ?? "Anonymous"); // Supercoder
```

### Comparison with ||

- `||` returns the `first truthy value`
- `??` returns the `first defined value`

```js
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

### Using ?? with && or ||

- Due to safety reasons, JavaScript forbids using ?? together with && and || operators, unless the precedence is explicitly specified with parentheses.

---

## Logical Assignment Operators (ES2021)

These operators combine logical operations with assignment.

### Logical AND assignment (`&&=`)

Assigns the right operand to the left only if the left operand is truthy.

```javascript
// Equivalent to: x = x && y
let x = 10;
x &&= 5; // x becomes 5 (since x was truthy)

let y = 0;
y &&= 5; // y remains 0 (since y was falsy)

// Practical example
function updateUserSettings(settings) {
  // Only update if 'darkMode' setting exists
  settings.darkMode &&= { enabled: true, contrast: "high" };
}
```

### Logical OR assignment (`||=`)

Assigns the right operand to the left only if the left operand is falsy.

```javascript
// Equivalent to: x = x || y
let x = 0;
x ||= 5; // x becomes 5 (since x was falsy)

let y = 10;
y ||= 5; // y remains 10 (since y was truthy)

// Practical example
function ensureDefaultSettings(settings) {
  // Set defaults only if properties are falsy
  settings.theme ||= "light";
  settings.fontSize ||= "medium";
}
```

### Nullish coalescing assignment (`??=`)

Assigns the right operand to the left only if the left operand is null or undefined.

```javascript
// Equivalent to: x = x ?? y
let x = undefined;
x ??= 5; // x becomes 5 (since x was undefined)

let y = 0;
y ??= 5; // y remains 0 (since y was not null/undefined)

// Practical example
function initializeConfig(config) {
  // Only initialize if properties are null or undefined
  // This preserves falsy values like 0 or ""
  config.timeout ??= 3000;
  config.maxRetries ??= 5;
  config.autoSave ??= true;
}
```

---

> 🔍 **Advanced Feature: Short-circuit evaluation** 🚀
>
> ```javascript
> // && returns the first falsy value or the last value if all are truthy
> let result1 = 5 && 0 && "hello"; // result1 = 0
>
> // || returns the first truthy value or the last value if all are falsy
> let result2 = null || 0 || "hello" || 42; // result2 = 'hello'
> ```

---

### Conditional (Ternary) Operator 🔀🤔

The only JavaScript operator that takes three operands.

```javascript
condition ? valueIfTrue : valueIfFalse;

// Example
let age = 20;
let status = age >= 18 ? "adult" : "minor";
// status = 'adult'
```

> 💫 **Pro Tip**: Ternary operators can be nested, but use carefully for readability!
>
> ```javascript
> let result = age < 13 ? "child" : age < 18 ? "teenager" : "adult";
> ```

---

### Bitwise Operators 🔢🔧

Perform operations on binary representations of numbers.

| Operator |     Description      |  Example   |    Result    |
| :------: | :------------------: | :--------: | :----------: |
|   `&`    |     Bitwise AND      |  `5 & 3`   |     `1`      |
|   `\|`   |      Bitwise OR      |  `5 \| 3`  |     `7`      |
|   `^`    |     Bitwise XOR      |  `5 ^ 3`   |     `6`      |
|   `~`    |     Bitwise NOT      |    `~5`    |     `-6`     |
|   `<<`   |      Left shift      |  `5 << 1`  |     `10`     |
|   `>>`   |     Right shift      |  `5 >> 1`  |     `2`      |
|  `>>>`   | Unsigned right shift | `-5 >>> 1` | `2147483645` |

> 📊 **Visual Explanation** 🖼️
>
> ```javascript
> // Bitwise operations (visualized in binary)
> // 5 in binary is 101
> // 3 in binary is 011
> 5 & 3; // 001 in binary = 1 in decimal (bits that are 1 in BOTH)
> 5 | 3; // 111 in binary = 7 in decimal (bits that are 1 in EITHER)
> 5 ^ 3; // 110 in binary = 6 in decimal (bits that are 1 in ONE BUT NOT BOTH)
> ```

---

```js
let x = 1 && 2 ?? 3; // Syntax error

let x = (1 && 2) ?? 3; // Works
alert(x); // 2
```

---

# 🌟 Introduction to Control Flow

## 🔍 if-else Statements

The `if-else` statement is a fundamental control structure that lets your code make decisions based on conditions.

### ✨ Basic Syntax

```javascript
if (condition) {
  // Code to execute when condition is true
} else {
  // Code to execute when condition is false
}
```

### 🗳️ The Voting Problem Example

```javascript
const age = 18;

if (age >= 18) {
  console.log("You can vote! 🎉");
} else {
  console.log("You cannot vote yet. ⏳");
}
```

### ⚠️ Omitting Brackets

For single statements, you can omit the curly brackets (but this is generally not recommended for readability):

```javascript
if (age >= 18) console.log("You can vote! 🎉");
else console.log("You cannot vote yet. ⏳");
```

### 📊 Multiple if-else (else if)

```javascript
const score = 85;

if (score >= 90) {
  console.log("Grade: A 🌟");
} else if (score >= 80) {
  console.log("Grade: B ✨");
} else if (score >= 70) {
  console.log("Grade: C 👍");
} else {
  console.log("Grade: F 📚");
}
```

### 🪆 Nesting if-else

You can place if-else statements inside other if-else statements:

```javascript
const hasLicense = true;
const age = 19;

if (age >= 18) {
  if (hasLicense) {
    console.log("You can drive a car. 🚗");
  } else {
    console.log("You need to get a license first. 📝");
  }
} else {
  console.log("You're too young to drive. ⏳");
}
```

## 🔄 Switch-Case Statements

The `switch` statement evaluates an expression and matches it against multiple possible cases.

### ✨ Basic Syntax

```javascript
switch (expression) {
  case value1:
    // Code to execute when expression equals value1
    break;
  case value2:
    // Code to execute when expression equals value2
    break;
  default:
  // Code to execute when no cases match
}
```

### 📅 Example

```javascript
const day = 3;
let dayName;

switch (day) {
  case 1:
    dayName = "Monday";
    break;
  case 2:
    dayName = "Tuesday";
    break;
  case 3:
    dayName = "Wednesday";
    break;
  case 4:
    dayName = "Thursday";
    break;
  case 5:
    dayName = "Friday";
    break;
  case 6:
    dayName = "Saturday";
    break;
  case 7:
    dayName = "Sunday";
    break;
  default:
    dayName = "Invalid day";
}

console.log(dayName); // Output: Wednesday
```

### 🪜 Fall Through

Without the `break` statement, code execution "falls through" to the next case:

```javascript
const month = 2;
let season;

switch (month) {
  case 12:
  case 1:
  case 2:
    season = "Winter ❄️";
    break;
  case 3:
  case 4:
  case 5:
    season = "Spring 🌱";
    break;
  case 6:
  case 7:
  case 8:
    season = "Summer ☀️";
    break;
  case 9:
  case 10:
  case 11:
    season = "Fall 🍂";
    break;
  default:
    season = "Invalid month ⚠️";
}

console.log(season); // Output: Winter ❄️
```

---

## 🔄 Ternary Operator

The ternary operator is a shorthand way to write simple if-else statements:

### ✨ Syntax

```javascript
condition ? expressionIfTrue : expressionIfFalse;
```

### 🎯 Example

```javascript
const age = 20;
const canVote = age >= 18 ? "Yes, can vote ✓" : "No, cannot vote ✗";
console.log(canVote); // Output: Yes, can vote ✓
```

You can also nest ternary operators, though this can reduce readability:

```javascript
const score = 85;
const grade =
  score >= 90 ? "A 🌟" : score >= 80 ? "B ✨" : score >= 70 ? "C 👍" : "F 📚";
console.log(grade); // Output: B ✨
```

---

## 🔍 Comparison: if-else vs. switch-case

| Feature          | if-else                                        | switch-case                                            |
| ---------------- | ---------------------------------------------- | ------------------------------------------------------ |
| 🎯 Purpose       | Good for testing multiple different conditions | Best for comparing a single value against many options |
| 📏 Range Testing | Can test ranges (>, <, >=, <=)                 | Tests only for equality (===)                          |
| 🧩 Flexibility   | More flexible for complex conditions           | More concise for multiple equality checks              |
| ⚡ Performance   | Slower for many equality checks                | More efficient for multiple equality comparisons       |
| 📊 Usage         | More commonly used in general                  | Better for enumerations and discrete values            |

### 🕒 When to use if-else

- When you need to test different conditions
- When you need comparison operators (>, <, >=, <=)
- When conditions are complex (using logical operators &&, ||)

### 🕒 When to use switch

- When comparing a single variable against multiple values
- When you have many conditions based on the same variable
- When the conditions are simple equality checks

---

# 🚀 JavaScript Loops & Logic Building

## 🧠 Logic Building and DSA

**Logic Building** is the foundation of programming that helps you transform problems into step-by-step solutions. It involves:

- 🧩 Breaking down complex problems into smaller, manageable parts
- 📝 Creating algorithms (step-by-step procedures) to solve problems
- 🔧 Using programming constructs like loops, conditionals, and functions

**Data Structures and Algorithms (DSA)** are essential tools for efficient problem-solving:

- 📊 **Data Structures**: Organized ways to store and access data (arrays, objects, sets)
- ⚙️ **Algorithms**: Step-by-step procedures to solve specific problems

## 🔄 Loops in JavaScript

Loops allow you to execute code repeatedly based on a condition. JavaScript offers several types of loops:

### 📋 Types of Loops

JavaScript provides several loop types for different scenarios:

1. 🔂 **`for loop`** - Used when the number of iterations is known
2. 🔁 **`while loop`** - Used when the number of iterations depends on a condition
3. 🔄 **`do-while loop`** - Similar to while loop but guarantees at least one execution
4. 🔠 **`for...in loop`** - Used to iterate over object properties
5. 📦 **`for...of loop`** - Used to iterate over iterable objects (arrays, strings, etc.)
6. 🔄 **`forEach() method`** - Array method that executes a provided function for each array element
7. 🔁 **`map(), filter(), reduce()`** - Functional iteration methods that transform data

---

### 1. 🔂 `The for Loop`

The `for` loop is used when you know how many times you want to execute a block of code.

**Syntax:**

```javascript
for (initialization; condition; update) {
  // code to be executed
}
```

**Components:**

1. 🏁 **Initialization**: Executed once before the loop starts (e.g., `let i = 0`)
2. ✅ **Condition**: Checked before each iteration; loop continues if true
3. 🔄 **Update**: Executed after each iteration (e.g., `i++`)

### 📊 The for Loop Flow Chart

```
┌─────────────────┐
│  Initialization │
└────────┬────────┘
         │
         ▼
┌─────────────────┐     false
│    Condition    ├─────────────► Exit Loop
└────────┬────────┘
         │ true
         ▼
┌─────────────────┐
│  Execute Code   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│     Update      │
└────────┬────────┘
         │
         └─────────────► Return to Condition
```

### ✨ for Loop Examples

**Example 1: Basic counter**

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(`Count: ${i}`);
}
// Output: Count: 1, Count: 2, Count: 3, Count: 4, Count: 5
```

**Example 2: Sum of numbers**

```javascript
let sum = 0;
for (let i = 1; i <= 10; i++) {
  sum += i;
}
console.log(`Sum: ${sum}`); // Output: Sum: 55
```

**Example 3: Iterating through an array**

```javascript
const fruits = ["Apple", "Banana", "Cherry"];
for (let i = 0; i < fruits.length; i++) {
  console.log(`Fruit ${i + 1}: ${fruits[i]}`);
}
```

### 🔄➿ Nested Loop

A nested loop is a loop inside another loop. The inner loop completes all its iterations for each iteration of the outer loop.

```javascript
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 3; j++) {
    console.log(`i: ${i}, j: ${j}`);
  }
}
```

**Practical example: Creating a multiplication table**

```javascript
for (let i = 1; i <= 5; i++) {
  let row = "";
  for (let j = 1; j <= 5; j++) {
    row += i * j + "\t";
  }
  console.log(row);
}
```

### ⏹️ The break and continue

**break**: Terminates the loop completely

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    break; // Exit the loop when i equals 5
  }
  console.log(i);
}
// Output: 1, 2, 3, 4
```

**continue**: Skips the current iteration and continues with the next one

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) {
    continue; // Skip iteration when i equals 3
  }
  console.log(i);
}
// Output: 1, 2, 4, 5
```

### 📊 Handling Multiple Counters

You can manage multiple variables within a single `for` loop:

```javascript
// Counting up and down simultaneously
for (let i = 1, j = 10; i <= 5; i++, j--) {
  console.log(`i: ${i}, j: ${j}`);
}
// Output: i: 1, j: 10 → i: 2, j: 9 → i: 3, j: 8 → i: 4, j: 7 → i: 5, j: 6
```

---

### 2. `🔁 The while Loop`

The `while` loop executes a block of code as long as a specified condition is true.

**Syntax:**

```javascript
while (condition) {
  // code to be executed
}
```

**Example:**

```javascript
let i = 1;
while (i <= 5) {
  console.log(`Number: ${i}`);
  i++;
}
```

## **When to use:** 🤔 When you don't know in advance how many times the loop should run.

### 3. `🔄 The do-while Loop`

The `do-while` loop is similar to the `while` loop, but it executes the code block at least once before checking the condition.

**Syntax:**

```javascript
do {
  // code to be executed
} while (condition);
```

**Example:**

```javascript
let i = 1;
do {
  console.log(`Number: ${i}`);
  i++;
} while (i <= 5);
```

**Key difference from while loop:** ⚠️ The code always executes at least once, even if the condition is initially false:

```javascript
let i = 6;
do {
  console.log(`This runs once even though i > 5`);
  i++;
} while (i <= 5);
```

---

### 4. `♾️ Infinite Loop`

An infinite loop occurs when the loop condition always evaluates to true, causing the loop to run indefinitely.

**Example of an infinite loop:**

```javascript
// ⚠️ WARNING: Don't run this without a way to stop execution
for (let i = 1; i > 0; i++) {
  console.log(i); // This will run forever
}
```

**Common causes:**

1. 🚫 Forgetting to update the counter variable
2. ⛔ Setting a condition that will never be false
3. 🔄 Accidentally resetting the counter inside the loop

**How to avoid:**

1. ✅ Always ensure the condition will eventually become false
2. 🔍 Double-check counter updates
3. 🛑 Use a backup exit condition (like a counter limit)

## 💪 Practice Problems for Reinforcement

1. ✏️ Write a loop that prints even numbers from 0 to 20
2. 🌟 Create a nested loop to generate a simple pattern of asterisks
3. 🧮 Use a loop to find the sum of all numbers in an array
4. 🔢 Write a program to find factorial of a number using loops
5. 🔤 Create a loop that iterates through a string and counts vowels

> 💡 **Remember**: The key to mastering loops is practice. Try building different solutions and analyze how loops can make your code more efficient.

## 📝 Quick Reference Table

| Loop Type    | Syntax                          | Best Used When                | Special Notes                              |
| ------------ | ------------------------------- | ----------------------------- | ------------------------------------------ |
| for          | `for (init; condition; update)` | Known number of iterations    | Most versatile loop                        |
| while        | `while (condition)`             | Unknown number of iterations  | Checks condition first                     |
| do-while     | `do { } while (condition);`     | At least one execution needed | Checks condition after execution           |
| for...in     | `for (key in object)`           | Iterating object properties   | Don't use for arrays                       |
| for...of     | `for (value of iterable)`       | Iterating array values        | Modern alternative to traditional for loop |
| Nested loops | loops inside loops              | 2D structures, matrices       | Watch performance!                         |

# Most asked interview questions

```js
if ("false") {
  console.log("Yes");
} else {
  console.log("No");
}
```

**Output:** `"Yes"`
**Explanation:** `"false"` is a **non-empty string**, hence **truthy**.

---

```js
let x = 5;
if (x > 3) {
  if (x < 10) {
    console.log("Valid");
  }
}
```

**Output:** `"Valid"`
**Explanation:** Both conditions are `true`.

---

```js
let val = 2;
switch (val) {
  case 1:
    console.log("One");
  case 2:
    console.log("Two");
  case 3:
    console.log("Three");
}
```

**Output:**

```
Two
Three
```

**Explanation:** No `break` causes **fallthrough** behavior.

---

```js
let result = 10 > 5 ? "A" : "B";
console.log(result);
```

**Output:** `"A"`
**Explanation:** Simple ternary.

---

```js
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

**Output:**

```
0
1
2
```

**Explanation:** Standard `for` loop iteration.

---

```js
let i = 0;
while (i < 2) {
  console.log(i);
  i++;
}
```

**Output:**

```
0
1
```

---

```js
let i = 3;
do {
  console.log(i);
  i++;
} while (i < 3);
```

**Output:** `3`
**Explanation:** Executes at least once regardless of condition.

---

```js
const arr = [10, 20];
arr.foo = "bar";
for (let key in arr) console.log(key);
```

**Output:**

```
0
1
foo
```

**Explanation:** `for...in` iterates **over keys**, including **custom properties**.

---

```js
const arr = [10, 20];
arr.foo = "bar";
for (let val of arr) console.log(val);
```

**Output:**

```
10
20
```

**Explanation:** `for...of` iterates **only over values**, not custom properties.

---

```js
for (let i = 0; i < 3; i++) {
  if (i === 1) continue;
  console.log(i);
}
```

**Output:**

```
0
2
```

**Explanation:** `continue` skips the current iteration.

---

```js
let i = 0;
while (i < 5) {
  if (i === 3) break;
  console.log(i);
  i++;
}
```

**Output:**

```
0
1
2
```

**Explanation:** `break` exits the loop when `i === 3`.

---

```js
for (let i = 0; i < 3; ) {
  console.log("Looping");
}
```

**Output:** _(Infinite loop)_
**Explanation:** No increment (`i++`) causes infinite loop.

---

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```

**Output:**

```
3
3
3
```

**Explanation:** `var` is function-scoped. All callbacks share the same `i`.

---

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```

**Output:**

```
0
1
2
```

**Explanation:** `let` is block-scoped — each loop gets a fresh `i`.

---
