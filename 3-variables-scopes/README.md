# Variables

- used to `store information` and use them later

- can `change` information later (var, let)

```js
let message; // undefined

message = "Hello"; // Hello

message = "World"; // value changed to `World`

alert(message); // World
```

- `declare multiple variables` in one line
  <br/>

```js
let user = "John",
  age = 25,
  message = "Hello";
```

---

## Variable naming

- name `must contain` only `letters`, `digits`, or the symbols `$ and \_`

```js
let userName;
let test123;

let $ = 1; // declared a variable with the name "$"
let _ = 2; // and now a variable with the name "_"
alert($ + _); // 3
```

- `first` character must `not be a digit`

```js
let 1a;
```

- hyphens `-` are `not allowed` in the name

```js
let my-name;
```

- `Case sensitive`

```js
// both variables are different
let apple = "...";
let APPLE = "...";
```

- `Non-Latin` letters are `allowed`, but `not recommended`

```js
let имя = "...";
```

- `can't use reserved words`

```js
let let = 5;
let return = 5;
```

---

## 🔄 Comparison Table: `var` vs `let` vs `const`

| Feature                 | `var`                                               | `let`                                   | `const`                                                                |
| ----------------------- | --------------------------------------------------- | --------------------------------------- | ---------------------------------------------------------------------- |
| Scope                   | Function scope                                      | Block scope `{}`                        | Block scope `{}`                                                       |
| Hoisting                | Hoisted & initialized as `undefined`                | Hoisted but in Temporal Dead Zone (TDZ) | Hoisted but in Temporal Dead Zone (TDZ)                                |
| Attached to `window`?   | ✅ Yes                                              | ❌ No                                   | ❌ No                                                                  |
| Can be Re-declared?     | ✅ Yes                                              | ❌ No                                   | ❌ No                                                                  |
| Can be Reassigned?      | ✅ Yes                                              | ✅ Yes                                  | ❌ No                                                                  |
| Initial Value Required? | ❌ No                                               | ❌ No                                   | ✅ Yes (Must be initialized)                                           |
| Mutability              | Mutable                                             | Mutable                                 | Immutable (Can't be reassigned but mutable if it's an object or array) |
| Use in Loops            | Allowed but not recommended (function scope issues) | ✅ Recommended                          | ❌ Not recommended for changing values                                 |

- If you re-declare with `var` only, it will not lose its value.

```js
var carName = "Volvo";
var carName; // Volvo

-----------------------

let message = "This";
let message = "That"; // SyntaxError: 'message' has already been declared
```

---

# Scope

- A variable can be declared at `different scope`
- Variables scopes can be:

  1. `Global`
  2. `Local`

- Anything declared `without let, var or const` is scoped at `global level`

```js
//scope.js
a = "JavaScript"; // declaring a variable without let or const make it available in window object and this found anywhere
b = 10; // this is a global scope variable and found in the window object
function letsLearnScope() {
  console.log(a, b); // JavaScript 10
  if (true) {
    console.log(a, b); // JavaScript 10
  }
}
console.log(a, b); // JavaScript 10
```

## 1.Global scope

A globally declared variable can be `accessed every where in the same file`

```js
//scope.js
let a = "JavaScript"; // is a global scope it will be found anywhere in this file
let b = 10; // is a global scope it will be found anywhere in this file
function letsLearnScope() {
  console.log(a, b); // JavaScript 10, accessible
  if (true) {
    let a = "Python";
    let b = 100;
    console.log(a, b); // Python 100
  }
  console.log(a, b);
}
letsLearnScope();
console.log(a, b); // JavaScript 10, accessible
```

#### ⚔️ Var vs Let/Const in Global Scope

- Variables declared with `var` in the global scope are attached to the global object (`window` in browsers)
- Variables declared with `let` or `const` in the global scope are not attached to the global object

```javascript
var x = 10;
let y = 20;
const z = 30;

console.log(window.x); // 10
console.log(window.y); // undefined
console.log(window.z); // undefined
```

## 2. 🧩 Function Scope

Variables declared inside a function are only accessible within that function. They are not visible outside the function.

```javascript
function calculateTax() {
  // Function-scoped variable
  let taxRate = 0.07;
  let amount = 100;
  let tax = amount * taxRate;

  console.log(`Tax: ${tax}`);
}

calculateTax(); // Output: "Tax: 7"
console.log(taxRate); // ❌ ReferenceError: taxRate is not defined
```

## 3. 📦 Block Scope

Variables declared with `let` or `const` inside a block (denoted by curly braces `{}`) are only accessible within that block. This includes blocks in `if` statements, `for` loops, `while` loops, etc.

```javascript
if (true) {
  // Block-scoped variable
  let blockVar = "I'm in a block";
  const blockConst = "I'm also in a block";

  console.log(blockVar); // "I'm in a block"
  console.log(blockConst); // "I'm also in a block"
}

console.log(blockVar); // ❌ ReferenceError: blockVar is not defined
```

```js
//scope.js
let a = "JavaScript"; // is a global scope it will be found anywhere in this file
let b = 10; // is a global scope it will be found anywhere in this file
// Function scope
function letsLearnScope() {
  console.log(a, b); // JavaScript 10, accessible
  let value = false;
  // block scope
  if (true) {
    // we can access from the function and outside the function but
    // variables declared inside the if will not be accessed outside the if block
    let a = "Python";
    let b = 20;
    let c = 30;
    let d = 40;
    value = !value;
    console.log(a, b, c, value); // Python 20 30 true
  }
  // we can not access c because c's scope is only the if block
  console.log(a, b, value); // JavaScript 10 true
}
letsLearnScope();
console.log(a, b); // JavaScript 10, accessible
```

---

# understanding of scope

- A variable declared with `var` only scoped to `function`
- variable declared with `let` or `const` is `block scope`(function block, if block, loop block, etc)
- Block in JavaScript is a code in between `two curly brackets` ({}).

```js
//scope.js
function letsLearnScope() {
  var gravity = 9.81;
  console.log(gravity);
}
// console.log(gravity), Uncaught ReferenceError: gravity is not defined

if (true) {
  var gravity = 9.81;
  console.log(gravity); // 9.81
}
console.log(gravity); // 9.81

for (var i = 0; i < 3; i++) {
  console.log(i); // 0, 1, 2
}
console.log(i); // 3
```

- When we use `let/const`, our variable is block scoped and it will not infect other parts of our code

```js
//scope.js
function letsLearnScope() {
  // you can use let or const, but gravity is constant I prefer to use const
  const gravity = 9.81;
  console.log(gravity);
}
// console.log(gravity), Uncaught ReferenceError: gravity is not defined

if (true) {
  const gravity = 9.81;
  console.log(gravity); // 9.81
}
// console.log(gravity), Uncaught ReferenceError: gravity is not defined

for (let i = 0; i < 3; i++) {
  console.log(i); // 0, 1, 2
}
// console.log(i), Uncaught ReferenceError: i is not defined
```

- Let's take a look at the following code

```js
const name = "Lydia";
const age = 21;
const city = "San Francisco";

function getPersonInfo() {
  const name = "Sarah";
  const age = 22;

  return `${name} is ${age} and lives in ${city}`;
}

console.log(getPersonInfo());
```

- First, `memory space` is set up for the different contexts
- We have the default `global context` (window in a browser, global in Node)
- and a `local context for the getPersonInfo function` which has been invoked
- Each context also has a `scope chain`

![scope](./images/scope/scope-1.png)
![scope](./images/scope/scope-2.gif)

- In order to find the value for city the engine `goes to outer scopes`
- You can go to `outer scopes`, but `not to more inner`

![scope](./images/scope/scope-3.gif)
![scope](./images/scope/scope-4.png)

- if variable not found in any scope, it throws `ReferenceError`

![scope](./images/scope/scope-5.gif)

# ⛓️ Scope Chain

The scope chain is how JavaScript looks for variables. When you try to access a variable, JavaScript will:

1. First look in the current scope
2. If not found, it looks in the outer scope
3. This process continues until it reaches the global scope
4. If the variable is not found in the global scope, a ReferenceError is thrown

```javascript
let global = "I'm global";

function outer() {
  let outerVar = "I'm in outer function";

  function inner() {
    let innerVar = "I'm in inner function";

    console.log(innerVar); // Finds in current scope
    console.log(outerVar); // Finds in outer scope
    console.log(global); // Finds in global scope
  }

  inner();
}

outer();
```

![ScopeChain](./images/scope/scope-3.gif)
![ScopeChain](./images/scope/scope-5.gif)

---

## 🧪 Practice Question to Test Knowledge

**Question**: What will be the output of the following code?

```javascript
let x = 10;

function first() {
  let y = 20;

  function second() {
    let z = 30;
    console.log(x + y + z);
  }

  second();
}

first();
```

<details>
  <summary>👉 Click to see answer</summary>
  
  **Answer**: `60` (10 + 20 + 30)
  
  This demonstrates the scope chain. The `second()` function can access:
  - Its own variable `z`
  - The variable `y` from its parent function `first()`
  - The global variable `x`
</details>

---

# Lexical Scope

- lexical scope means that the `visibility of variables` is determined by `where they are written in the code`, `not where or how they are executed`.

- In other words, an item's lexical scope is the `place in which the item got created`

- `Inner functions` can access variables from their `own scope` and any `outer scope`, but `not vice versa`

- Real-Life Example: `Office Building (Lexical Scope)`

- Imagine an office building with multiple floors:

1. `Each floor represents a scope`
2. Employees on each floor can access files that are `located on their floor` (local scope).
3. Employees can also access files on the `floors above them` (outer scope), but `not on the floors below them`

```js
// Top floor (Global Scope)
let topFloorDocument = "Global Document";

function middleFloor() {
  // Middle floor (Function Scope)
  let middleFloorDocument = "Middle Floor Document";

  function basement() {
    // Basement (Inner Function Scope)
    let basementDocument = "Basement Document";

    // Employees in the basement can access all documents
    console.log(topFloorDocument); // Accessible
    console.log(middleFloorDocument); // Accessible
    console.log(basementDocument); // Accessible
  }

  // Employees on the middle floor can access their own and top floor documents
  console.log(topFloorDocument); // Accessible
  console.log(middleFloorDocument); // Accessible
  // console.log(basementDocument); // Error: Not accessible from middle floor

  basement();
}

middleFloor();
```

---

# 🌑 What is Variable Shadowing?

- **Variable Shadowing** occurs when a **variable declared within a certain scope (e.g., function or block)** has the **same name** as a variable in an **outer scope**.
- The inner variable _“shadows”_ the outer one — making the outer variable **inaccessible** in that scope.

---

## 🧠 Step-by-Step Explanation

### 1. **Basic Shadowing**

```js
let a = 10;

function test() {
  let a = 20; // Shadows the outer 'a'
  console.log(a); // 20
}

test();
console.log(a); // 10
```

- Inside `test()`, the outer `a` is shadowed by the inner `a`.
- The outer `a` remains unchanged.

---

### 2. **Function vs Block Scope**

```js
let x = 1;

{
  let x = 2; // Shadows outer 'x' only inside this block
  console.log(x); // 2
}

console.log(x); // 1
```

- `let` and `const` are block-scoped, so the outer `x` is unaffected outside the block.

---

### 3. **`var` and Function Scope Shadowing**

```js
var y = 100;

function testVar() {
  var y = 200; // Shadows outer 'y'
  console.log(y); // 200
}

testVar();
console.log(y); // 100
```

- `var` is **function-scoped**, so it behaves like shadowing inside a function.

---

### 4. **Illegal Shadowing**

> ⚠️ Shadowing a `let/const` with `var` in the **same block** causes an error.

```js
let z = 5;

{
  var z = 10; // ❌ SyntaxError: Identifier 'z' has already been declared
}
```

- Because `var` gets hoisted to function or global scope, it conflicts with `let`.

---

### 5. **Legal Shadowing Example**

```js
var a = 5;

{
  let a = 10; // ✅ Legal shadowing — inner block scoped with 'let'
  console.log(a); // 10
}

console.log(a); // 5
```

- `let` and `const` can safely shadow `var` variables if used in a different scope.

---

### 6. **Function Parameter Shadowing**

```js
let num = 30;

function shadow(num) {
  console.log(num); // shadows outer 'num', prints argument passed
}

shadow(50); // 50
```

- Function parameter `num` shadows the global `num`.

---

## ⚠️ Potential Pitfalls of Shadowing

1. **Debugging becomes harder** — it’s easy to confuse which variable is being accessed.
2. **Accidental overwrites** if you forget variable scoping rules.
3. Can lead to **bugs in closures**, especially in loops or nested functions.

---

## 🧪 Best Practices

- ❌ Avoid using the same variable names in nested scopes unless necessary.
- ✅ Use **meaningful, distinct names**.
- ✅ Prefer `let` and `const` over `var` to avoid hoisting-related shadowing issues.

---

## 🧠 Summary

| Aspect           | Description                                                                        |
| ---------------- | ---------------------------------------------------------------------------------- |
| What             | Declaring a variable in an inner scope with the same name as one in an outer scope |
| Scope Types      | Global, Function, Block                                                            |
| Safe Shadowing   | `let`/`const` shadowing `var` in a different scope                                 |
| Unsafe Shadowing | `var` shadowing `let`/`const` in the same scope (SyntaxError)                      |
| Common in        | Functions, Loops, Blocks, Parameters                                               |

## 🧪 Practice Question to Test Shadowing Knowledge

**Question**: What will be the output of the following code?

```javascript
let value = 10;

function test() {
  let value = 20;

  function innerTest() {
    let value = 30;
    console.log("A:", value);
  }

  innerTest();
  console.log("B:", value);
}

test();
console.log("C:", value);
```

<details>
  <summary>👉 Click to see answer</summary>
  
  **Answer**:
  - A: 30 (from innerTest's local scope)
  - B: 20 (from test's local scope)
  - C: 10 (from global scope)
  
  Each scope has its own `value` variable that shadows the outer ones.
</details>

---

## 🔄 Loop with Var and Let

Using `var` vs `let` in loops shows an important difference in scoping behavior:

### 🔁 Using var in a loop

```javascript
function varLoop() {
  for (var i = 0; i < 3; i++) {
    // i is function-scoped
  }
  console.log(i); // 3 - i is still accessible!
}

varLoop();
```

### 🔂 Using let in a loop

```javascript
function letLoop() {
  for (let j = 0; j < 3; j++) {
    // j is block-scoped to the for loop
  }
  console.log(j); // ❌ ReferenceError: j is not defined
}

letLoop();
```

---

### 🎭 Special Case: Closures in Loops

This classic example shows the difference between `var` and `let` in loops when using closures:

```javascript
// Using var
function createFunctionsVar() {
  var funcs = [];

  for (var i = 0; i < 3; i++) {
    funcs.push(function () {
      console.log(i);
    });
  }

  return funcs;
}

var functionsVar = createFunctionsVar();
functionsVar[0](); // 3
functionsVar[1](); // 3
functionsVar[2](); // 3 - All reference the same i!

// Using let
function createFunctionsLet() {
  var funcs = [];

  for (let i = 0; i < 3; i++) {
    funcs.push(function () {
      console.log(i);
    });
  }

  return funcs;
}

var functionsLet = createFunctionsLet();
functionsLet[0](); // 0
functionsLet[1](); // 1
functionsLet[2](); // 2 - Each has its own copy of i!
```

With `var`, all functions share the same `i` (which ends up as 3).
With `let`, each iteration creates a new block-scoped `i` that is captured by the closure.

---

## 🧠 Additional Practice Questions

### Question 1: Scope Chain & Shadowing

What will be the output of the following code?

```javascript
let x = 5;

function outer() {
  let x = 10;

  function inner() {
    let x = 15;
    console.log("A:", x);

    {
      let x = 20;
      console.log("B:", x);
    }

    console.log("C:", x);
  }

  inner();
  console.log("D:", x);
}

outer();
console.log("E:", x);
```

<details>
  <summary>👉 Click to see answer</summary>
  
  **Answer**:
  - A: 15 (from inner's local scope)
  - B: 20 (from block scope inside inner)
  - C: 15 (back to inner's scope)
  - D: 10 (from outer's scope)
  - E: 5 (from global scope)
  
  This demonstrates both the scope chain and variable shadowing at multiple levels.
</details>

### Question 2: Hoisting with Different Variable Types

What will be the output of the following code?

```javascript
console.log("A:", x);
console.log("B:", y);
console.log("C:", z);

var x = 1;
let y = 2;
const z = 3;
```

<details>
  <summary>👉 Click to see answer</summary>
  
  **Answer**:
  - A: undefined (var is hoisted and initialized with undefined)
  - B: ReferenceError: Cannot access 'y' before initialization (let is hoisted but in TDZ)
  - C: The code won't reach here due to the error in B
  
  This demonstrates the difference in hoisting behavior between var, let, and const.
</details>

### Question 3: Block Scoping with Functions

What will be the output of this code?

```javascript
function example() {
  if (true) {
    var varVariable = "I'm var";
    let letVariable = "I'm let";
    function innerFunc() {
      console.log("Inside function");
    }
  }

  console.log(varVariable); // A
  console.log(letVariable); // B
  innerFunc(); // C
}

example();
```

<details>
  <summary>👉 Click to see answer</summary>
  
  **Answer**:
  - A: "I'm var" (var is function-scoped)
  - B: ReferenceError: letVariable is not defined (let is block-scoped)
  - C: The behavior depends on the JavaScript environment!
  
  In strict mode (ES2015+), function declarations are block-scoped in most browsers, causing a ReferenceError. In non-strict mode or older environments, the function might be hoisted to the containing function scope.
  
  This shows how functions can have complex scoping rules that differ from variables.
</details>

### Question 4: Loop Closures Challenge

What will each alert display in this code?

```javascript
const buttons = [];

// Using var
for (var i = 0; i < 3; i++) {
  const button = document.createElement("button");
  button.innerText = "Button " + i;
  button.onclick = function () {
    alert("Button " + i + " clicked");
  };
  buttons.push(button);
}

// What alerts will be shown when clicking each button?
```

<details>
  <summary>👉 Click to see answer</summary>
  
  **Answer**:
  All three buttons will alert "Button 3 clicked"
  
  This is because var is function-scoped, and by the time any button is clicked, the loop has finished and i has the value 3. All onclick callbacks reference the same variable i, which by then has the value 3.
  
  To fix this, you would use let instead of var:
  
  ```javascript
  for (let i = 0; i < 3; i++) {
    // Now each iteration creates its own i
  }
  ```
  
  Then each button would correctly alert its number (0, 1, or 2).
</details>

### Question 5: Global vs Window Object

Consider this code running in a browser:

```javascript
var globalVar = "I'm a var";
let globalLet = "I'm a let";
const globalConst = "I'm a const";

function checkGlobals() {
  console.log("A:", window.globalVar);
  console.log("B:", window.globalLet);
  console.log("C:", window.globalConst);

  console.log("D:", window.hasOwnProperty("globalVar"));
  console.log("E:", window.hasOwnProperty("globalLet"));
  console.log("F:", window.hasOwnProperty("globalConst"));
}

checkGlobals();
```

<details>
  <summary>👉 Click to see answer</summary>
  
  **Answer**:
  - A: "I'm a var" 
  - B: undefined
  - C: undefined
  - D: true
  - E: false
  - F: false
  
  This demonstrates that variables declared with var at the global level become properties of the window object, while those declared with let and const are in the global scope but don't get attached to the window object.
</details>

# Most asked interview questions

---

```js
console.log(a);
var a = 10;
```

**Output:** `undefined`
**Explanation:** `var` declarations are **hoisted**, but not initialized.

---

```js
console.log(b);
let b = 10;
```

**Output:** `ReferenceError`
**Explanation:** `let` is hoisted but in **Temporal Dead Zone (TDZ)** until declared.

---

```js
const x = 5;
x = 10;
console.log(x);
```

**Output:** `TypeError`
**Explanation:** Cannot reassign a `const` variable.

---

```js
const user = { name: "Shubham" };
user.name = "Salunkhe";
console.log(user.name);
```

**Output:** `"Salunkhe"`
**Explanation:** `const` prevents reassignment, **not mutation**.

---

```js
let x = 10;
{
  let x = 20;
  console.log(x);
}
console.log(x);
```

**Output:**

```
20
10
```

**Explanation:** `let` is **block scoped**.

---

```js
let a = 1;
function outer() {
  let b = 2;
  function inner() {
    let c = 3;
    console.log(a, b, c);
  }
  inner();
}
outer();
```

**Output:** `1 2 3`
**Explanation:** Inner functions can access variables from outer scopes – **Scope Chain**.

---

```js
function foo() {
  if (true) {
    var x = 10;
  }
  console.log(x);
}
foo();
```

**Output:** `10`
**Explanation:** `var` is function-scoped, not block-scoped.

---

```js
function test() {
  console.log(x);
  var x = 5;
}
test();
```

**Output:** `undefined`
**Explanation:** `var x` is hoisted, but not initialized.

---

```js
function foo() {
  console.log(x);
}
let x = 10;
foo();
```

**Output:** `10`
**Explanation:** Global `x` is accessible inside `foo()` due to **scope chain**.

---

```js
{
  var a = 10;
}
console.log(a);
```

**Output:** `10`
**Explanation:** `var` is not block-scoped; it leaks out.

---

```js
{
  let a = 10;
}
console.log(a);
```

**Output:** `ReferenceError`
**Explanation:** `let` is block-scoped.

---

```js
let a = 10;
function test() {
  console.log(a);
  let a = 20;
}
test();
```

**Output:** `ReferenceError`
**Explanation:** `a` is in **TDZ** inside `test()` even though it's declared later.

---

Here are the most commonly asked **output-based JavaScript interview questions** on **Variable Shadowing**, with concise explanations.

---

```js
let a = 100;
function test() {
  let a = 50;
  console.log(a);
}
test();
```

**Output:** `50`
**Explanation:** Inner `let a` **shadows** outer `a` within the function scope.

---

```js
var a = 1;
function outer() {
  var a = 2;
  function inner() {
    console.log(a);
  }
  inner();
}
outer();
```

**Output:** `2`
**Explanation:** Inner function accesses the **closest scoped variable**—`a = 2`.

---

```js
let x = 10;
{
  let x = 20;
  {
    let x = 30;
    console.log(x);
  }
}
```

**Output:** `30`
**Explanation:** Each block creates a new scope, and inner variables **shadow** the outer ones.

---

```js
let b = 1;
function example() {
  console.log(b);
  let b = 2;
}
example();
```

**Output:** `ReferenceError`
**Explanation:** `b` is in the **Temporal Dead Zone (TDZ)**. Accessing it before declaration throws an error.

---

```js
var x = 10;
function shadow() {
  if (true) {
    var x = 20;
  }
  console.log(x);
}
shadow();
```

**Output:** `20`
**Explanation:** `var` is function-scoped. Inner `x` **re-declares** and **overwrites** the outer one.

---

```js
let x = 5;
function foo() {
  var x = 10;
  console.log(x);
}
foo();
```

**Output:** `10`
**Explanation:** `var x` inside `foo` **shadows** the outer `let x`.

---

```js
let a = 10;
function outer() {
  let a = 20;
  function inner() {
    console.log(a);
  }
  return inner;
}
const fn = outer();
fn();
```

**Output:** `20`
**Explanation:** `inner()` closes over `outer()`'s `a` — this is **shadowing + closure**.

---

```js
var a = 1;
function test() {
  console.log(a);
  var a = 2;
}
test();
```

**Output:** `undefined`
**Explanation:** `var a` is hoisted inside the function and shadows the outer `a`, but is **undefined** until initialized.

---
