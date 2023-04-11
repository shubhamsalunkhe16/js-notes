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

## `var` vs `let` vs `const`

|                                         | var                                            | let                                            | const                                               |
| --------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | --------------------------------------------------- |
| Redeclaration                           | YES                                            | NO                                             | NO                                                  |
| Reassignment</br>(can change its value) | YES                                            | YES                                            | NO                                                  |
| Must be Assigned                        | NO<br/>var name;<br/>name = 'Shubham'; //valid | NO<br/>let name;<br/>name = 'Shubham'; //valid | YES<br/>const PI;<br/>PI = 3.14159265359; //invalid |
| Block Scope                             | NO<br/>(functional scope)                      | YES                                            | YES                                                 |

- If you re-declare with `var` only, it will not lose its value.

```js
var carName = "Volvo";
var carName; // Volvo

-----------------------

let message = "This";
let message = "That"; // SyntaxError: 'message' has already been declared
```

# scope

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

## Global scope

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

## Local scope

- A variable declared as local can be accessed only in certain block code
  1. `Block Scope`
  2. `Function Scope`

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

## understanding of scope

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

# Lexical Scope

- Lexical scope is the `definition area of an expression`

- In other words, an item's lexical scope is the `place in which the item got created`

```js
// Define a variable in the global scope:
const myName = "Oluwatobi";

// Call myName variable from a function:
function getName() {
  return myName;
}
```

- notice that we defined the `myName` variable in the global scope and called it in the `getName()` function
- Remember that lexical scope means definition space — not invocation space
- hence, `myName`’s lexical scope is the `global scope` because we defined myName in the global environment

# Hoisting

- `Functions` and `variables` are stored in `memory` for an `execution context` before we execute our code. This is called `hoisting`.
- `Functions` are stored with a `reference to the entire functions`,
- `Variables` with the `var` keyword with the value of `undefined`, and variables with the `let` and `const` keyword are stored `uninitialized`.

![Hoisting](./images/hoisting/hoisting1.gif)
![Hoisting](./images/hoisting/hoisting2.gif)
![Hoisting](./images/hoisting/hoisting3.gif)
![Hoisting](./images/hoisting/hoisting4.gif)
![Hoisting](./images/hoisting/hoisting5.gif)
![Hoisting](./images/hoisting/hoisting6.gif)
![Hoisting](./images/hoisting/hoisting7.gif)

## let and const hoisting

- Variables declared with let and const are `also hoisted` but, `unlike var, are not initialized with a default value`. An `exception` will be thrown in a case of let and const

- A let or const variable is said to be in a `temporal dead zone (TDZ)` from the start of the block until code execution reaches the line where the variable is declared.

```js
{
  // TDZ starts at beginning of scope
  console.log(bar); // undefined
  console.log(foo); // ReferenceError
  var bar = 1;
  let foo = 2; // End of TDZ (for foo)
}
```

## class hoisting

- Classes defined using a `class` declaration are hoisted, which means that JavaScript has a reference to the class. However the class is not initialized by default, so any code that uses it before the line in which it is initialized is executed will throw a `ReferenceError`.

# How JavaScript Works

- Everything in JavaScript happens `inside an Execution Context`
- assume this Execution context to be a `big container`
- In this container, there are two components

  1. `Memory component`
  2. `Code component`

### Memory component

- `variables and functions are stored as key-value pairs`
- also known as `variable environment`

### Code component

- is a place in the container where `code is executed one line at a time`
- also known as `Thread of Execution`

![execution-context](./images/execution-context/execution-context-1.png)

## Execution of the code

- Let's take a simple example,

```js
var a = 2;
var b = 4;

var sum = a + b;

console.log(sum);
```

![execution-context](./images/execution-context/execution-context-2.gif)
![execution-context](./images/execution-context/execution-context-3.gif)

## How Functions Are Called In Execution Context?

- Let's see the example,

```js
var n = 2;

function square(num) {
  var ans = num * num;
  return ans;
}

var square2 = square(n);
var square4 = square(4);
```

![execution-context](./images/execution-context/execution-context-4.gif)
![execution-context](./images/execution-context/execution-context-5.gif)
![execution-context](./images/execution-context/execution-context-6.gif)
![execution-context](./images/execution-context/execution-context-7.gif)
![execution-context](./images/execution-context/execution-context-8.gif)

# Call Stack

- When a function is `invoked` in JavaScript, JavaScript creates an `execution context`
- JavaScript manages `code execution context creation` and `deletion` with the the help of Call Stack

```js
function a() {
  function insideA() {
    return true;
  }
  insideA();
}
a();
```

![call-stack](./images/call-stack/call-stack-2.gif)
