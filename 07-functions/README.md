# Functions

- A function is a `reusable block` of code or programming statements designed
- Function makes code:

  - `clean and easy to read`
  - `reusable`
  - `easy to test`

- A function can be declared or created in couple of ways:

  - _Declaration function_
  - _Expression function_
  - _Anonymous function_
  - _Arrow function_

### Function Declaration

- If the function is declared as a `separate statement in the main code flow`, that’s called a `Function Declaration`
- Function Declarations are `processed before the code block is executed`. They are visible everywhere in the block.(`Hoisted`)

```js
//declaring a function without a parameter
function functionName() {
  // code goes here
}
functionName(); // calling function by its name and with parentheses
```

### Parameters

- We can pass arbitrary data to functions using parameters.

```js
function showMessage(from, text) {
  // parameters: from, text
  alert(from + ": " + text);
}

showMessage("Ann", "Hello!"); // Ann: Hello! (*)
showMessage("Ann", "What's up?"); // Ann: What's up? (**)
```

### Function returning value

- Function can also `return values`
- if a function `does not return values` the value of the function is `undefined`

```js
function printFullName() {
  let firstName = "Asabeneh";
  let lastName = "Yetayeh";
  let space = " ";
  let fullName = firstName + space + lastName;
  return fullName;
}
console.log(printFullName()); // Asabeneh Yetayeh
```

### Function with unlimited number of parameters

- Sometimes `we do not know how many arguments` the user going to pass.
- The way we do it has a significant `difference` between a function `declaration`(regular function) and `arrow` function

### Unlimited number of parameters in regular function

- A function declaration provides a function scoped `arguments array like object`.

```js
// Let us access the arguments object
​
function sumAllNums() {
 console.log(arguments)
}

sumAllNums(1, 2, 3, 4)
// Arguments(4) [1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]

```

```js
// function declaration
​
function sumAllNums() {
  let sum = 0
  for (let i = 0; i < arguments.length; i++) {
    sum += arguments[i]
  }
  return sum
}

console.log(sumAllNums(1, 2, 3, 4)) // 10
console.log(sumAllNums(10, 20, 13, 40, 10))  // 93
console.log(sumAllNums(15, 20, 30, 25, 10, 33, 40))  // 173
```

### Unlimited number of parameters in arrow function

- Arrow function does not have the function scoped arguments object.
- can use spread operator

```js
// Let us access the arguments object
​
const sumAllNums = (...args) => {
 // console.log(arguments), arguments object not found in arrow function
 // instead we use a parameter followed by spread operator (...)
 console.log(args)
}

sumAllNums(1, 2, 3, 4)
// [1, 2, 3, 4]

```

```js
// function declaration
​
const sumAllNums = (...args) => {
  let sum = 0
  for (const element of args) {
    sum += element
  }
  return sum
}

console.log(sumAllNums(1, 2, 3, 4)) // 10
console.log(sumAllNums(10, 20, 13, 40, 10))  // 93
console.log(sumAllNums(15, 20, 30, 25, 10, 33, 40))  // 173
```

### Anonymous Function

- Anonymous function or `without name`

```js
const anonymousFun = function () {
  console.log(
    "I am an anonymous function and my value is stored in anonymousFun"
  );
};
```

### Function expression

- If the function is created as a part of an `expression`, it’s called a `Function Expression`
- Function Expressions are `created when the execution flow reaches them`.
- After we create a `function without a name` and we `assign it to a variable`.
- To return a value from the function we should call the variable. Look at the example below.

```js
// Function expression
const square = function (n) {
  return n * n;
};

console.log(square(2)); // -> 4
```

### Arrow Function

- Arrow function uses `arrow` instead of the keyword _`function`_ to declare a function

```js
// This is how we write normal or declaration function
// Let us change this declaration function to an arrow function
function square(n) {
  return n * n;
}

console.log(square(2)); // 4

const square = (n) => {
  return n * n;
};

console.log(square(2)); // -> 4

// if we have only one line in the code block, it can be written as follows, explicit return
const square = (n) => n * n; // -> 4
```

### Function with default parameters

```js
// syntax
// Declaring a function
function functionName(param = value) {
  //codes
}

// Calling function
functionName();
functionName(arg);
```

**Example:**

```js
function greetings(name = "Peter") {
  let message = `${name}, welcome to 30 Days Of JavaScript!`;
  return message;
}

console.log(greetings());
console.log(greetings("Asabeneh"));
```

### Self Invoking Functions ( Immediately Invoked Function Expression - IIFE )

- are `anonymous functions` which do not need to be called to return a value.
- it called `Immediately`

```js
(function (n) {
  console.log(n * n);
})(2); // 4, but instead of just printing if we want to return and store the data, we do as shown below

let squaredNum = (function (n) {
  return n * n;
})(10);

console.log(squaredNum);
```
