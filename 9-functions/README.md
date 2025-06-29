# 🔧 Functions

## 📘 Introduction to Functions

Functions are one of the fundamental building blocks in JavaScript. They allow you to encapsulate a block of code that can be used and reused throughout your program. Think of functions as "code recipes" that you can call whenever you need them.

## 🎯 What is a Function?

A function is a reusable block of code designed to perform a specific task. Functions help:

- 📦 Organize your code into manageable pieces
- 🔄 Make your code reusable (write once, use many times)
- 📝 Keep your code maintainable and easier to understand
- 🏗️ Build modular applications

---

## 🛠️ Defining a Function

Functions can be defined (created) in several ways in JavaScript:

### Function Declaration

```javascript
function greet() {
  console.log("Hello, Neeraj!");
}
```

**Key components:**

- `function` keyword
- Function name (`greet`)
- Parentheses `()`
- Function body enclosed in curly braces `{}`

### Function with Parameters

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}
```

## 📞 Invoking (Calling) a Function

To use a function after it's defined, you need to invoke/call it:

```javascript
// Define function
function sayHello() {
  console.log("Hello!");
}

// Invoke function
sayHello(); // Output: Hello!
```

When invoking a function with parameters:

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet("John"); // Output: Hello, John!
```

## 🛠️ Function Declaration

Function declaration (also called function statement) defines a named function using the `function` keyword:

```javascript
function multiply(a, b) {
  return a * b;
}
```

**Key characteristics:**

- Begins with the `function` keyword
- Followed by the function name (`multiply` in this example)
- Parameters in parentheses (`a, b`)
- Function body enclosed in curly braces `{}`
- Can include a `return` statement (not required, but often used)

**Important:** Function declarations are hoisted to the top of their scope, meaning you can call them before they appear in your code:

```javascript
// This works!
console.log(square(5)); // Output: 25

// Function declaration is hoisted
function square(number) {
  return number * number;
}
```

---

## 🔢 Function as Expression

A function expression assigns a function to a variable:

```javascript
// Function expression
const greet = function (name) {
  console.log(`Hello, ${name}!`);
};

// Invoke function
greet("Sarah"); // Output: Hello, Sarah!
```

**Key differences from function declarations:**

- Function expressions are not hoisted (can't be used before they're defined)
- Can be anonymous (no name) or named
- Often used for callbacks and IIFE

## 📫 Parameters and Arguments

- **Parameters** are variables listed in the function definition
- **Arguments** are the values passed to the function when it's called

```javascript
// 'name' and 'age' are parameters
function introduce(name, age) {
  console.log(`I am ${name} and I am ${age} years old.`);
}

// 'Alice' and 25 are arguments
introduce("Alice", 25);
```

## 🛡️ Default Parameters

Default parameters allow you to specify default values for parameters if no argument is provided:

```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet(); // Output: Hello, Guest!
greet("Tom"); // Output: Hello, Tom!
```

---

## 📦 Rest Parameter

The rest parameter syntax (`...`) allows a function to accept an indefinite number of arguments as an array:

```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2)); // Output: 3
console.log(sum(1, 2, 3, 4, 5)); // Output: 15
```

**Key points:**

- Must be the last parameter in the function definition
- Collects all remaining arguments into an array
- Only one rest parameter allowed per function.

---

## 🪆 Nested Functions

Functions can be defined inside other functions:

```javascript
function outer() {
  console.log("I am the outer function");

  function inner() {
    console.log("I am the inner function");
  }

  // Call the inner function
  inner();
}

outer();
// Output:
// I am the outer function
// I am the inner function
```

### How to Execute Inner Functions

There are several ways to execute inner functions:

1. **Call directly from inside the outer function** (as shown above)

2. **Return the inner function and call it later**:

```javascript
function createGreeter(greeting) {
  function greet(name) {
    console.log(`${greeting}, ${name}!`);
  }

  return greet; // Return the inner function
}

const sayHello = createGreeter("Hello");
sayHello("Maria"); // Output: Hello, Maria!
```

3. **Immediately invoke the inner function**:

```javascript
function outer() {
  console.log("Outer function");

  (function inner() {
    console.log("Inner function executed immediately");
  })();
}

outer();
```

---

## 🔄 Callback Functions

A callback function is a function passed as an argument to another function, which is then invoked inside the outer function:

```javascript
function processInput(input, callback) {
  // Process the input
  const processed = input.toUpperCase();

  // Call the callback function with the processed input
  callback(processed);
}

// Define callback function
function displayResult(result) {
  console.log(`The processed result is: ${result}`);
}

// Pass the callback function to processInput
processInput("hello", displayResult);
// Output: The processed result is: HELLO
```

**Common use cases:**

- Event handlers
- Asynchronous operations (setTimeout, API calls)
- Array methods (forEach, map, filter, etc.)

---

## ✨ Pure Functions

A pure function is a function that:

1. Always returns the same output for the same input
2. Has no side effects (doesn't modify external state)

```javascript
// Pure function
function add(a, b) {
  return a + b;
}

// Not a pure function (uses external state)
let total = 0;
function addToTotal(value) {
  total += value; // Side effect: modifies external variable
  return total;
}
```

**Benefits of pure functions:**

- 🔍 Easier to test and debug
- 🔄 More predictable behavior
- 🔒 Safer for concurrent operations
- 📦 More reusable and modular

---

## 🚀 Higher-Order Functions

A higher-order function is a function that:

- Takes one or more functions as arguments, and/or
- Returns a function as its result

```javascript
// Higher-order function that takes a function as argument
function calculate(operation, a, b) {
  return operation(a, b);
}

// Functions to pass as arguments
function add(x, y) {
  return x + y;
}
function subtract(x, y) {
  return x - y;
}

console.log(calculate(add, 5, 3)); // Output: 8
console.log(calculate(subtract, 5, 3)); // Output: 2
```

**Higher-order function that returns a function:**

```javascript
function multiplier(factor) {
  return function (number) {
    return number * factor;
  };
}

const double = multiplier(2);
const triple = multiplier(3);

console.log(double(5)); // Output: 10
console.log(triple(5)); // Output: 15
```

---

## 🏹 Arrow Functions

Arrow functions provide a shorter syntax for writing functions and do not bind their own `this` value:

```javascript
// Regular function
function add(a, b) {
  return a + b;
}

// Equivalent arrow function
const addArrow = (a, b) => a + b;

console.log(addArrow(5, 3)); // Output: 8
```

**Syntax variations:**

- With multiple parameters: `(a, b) => expression`
- With single parameter: `a => expression` (parentheses optional)
- With no parameters: `() => expression`
- Multiple statements: `(a, b) => { statements; return value; }`

**Key differences from regular functions:**

- No `this` binding of their own (inherits from parent scope)
- No `arguments` object
- Can't be used as constructors (no `new` keyword)
- No `super` or `new.target`

---

## 🔄 IIFE (Immediately Invoked Function Expression)

An IIFE is a function that runs as soon as it is defined:

```javascript
(function () {
  console.log("This function runs immediately!");
})();
// Output: This function runs immediately!
```

**With parameters:**

```javascript
(function (name) {
  console.log(`Hello, ${name}!`);
})("Alice");
// Output: Hello, Alice!
```

**Arrow function IIFE:**

```javascript
(() => {
  console.log("Arrow function IIFE");
})();
```

**Use cases:**

- Creating private scopes to avoid polluting the global namespace
- Avoiding variable hoisting issues
- Module patterns (before ES6 modules)

---

## 📚 Call Stack

The call stack is a mechanism that JavaScript uses to keep track of function calls:

- When a function is called, it's added to the stack (pushed)
- When a function returns, it's removed from the stack (popped)
- The stack follows the Last In, First Out (LIFO) principle

```javascript
function first() {
  console.log("First function");
  second();
  console.log("First function again");
}

function second() {
  console.log("Second function");
  third();
  console.log("Second function again");
}

function third() {
  console.log("Third function");
}

first();
/* Output:
First function
Second function
Third function
Second function again
First function again
*/
```

Call stack sequence:

1. Push `first()`
2. Execute `first()` and push `second()`
3. Execute `second()` and push `third()`
4. Execute `third()` and pop it
5. Continue executing `second()` and pop it
6. Continue executing `first()` and pop it

**Stack overflow** occurs when the call stack exceeds its size limit, often due to infinite recursion.

---

## 🔄 Recursion

Recursion is when a function calls itself:

```javascript
function countdown(n) {
  // Exit criteria (base case)
  if (n <= 0) {
    console.log("Done!");
    return;
  }

  console.log(n);

  // Recursive call with progress toward exit criteria
  countdown(n - 1);
}

countdown(3);
/* Output:
3
2
1
Done!
*/
```

### Key Components of Recursion:

1. **Exit Criteria (Base Case)**: The condition that stops the recursion

   ```javascript
   if (n <= 0) {
     console.log("Done!");
     return;
   }
   ```

2. **Fetch Condition (Recursive Case)**: The part where the function calls itself with modified parameters
   ```javascript
   countdown(n - 1);
   ```

**Common example: Factorial calculation**

```javascript
function factorial(n) {
  // Base case
  if (n <= 1) {
    return 1;
  }

  // Recursive case
  return n * factorial(n - 1);
}

console.log(factorial(5)); // Output: 120 (5 * 4 * 3 * 2 * 1)
```

**Best practices:**

- Always define a clear base case
- Ensure progress toward the base case
- Be mindful of stack overflow for deep recursion
- Consider tail-call optimization for better performance

---

## Unlimited number of parameters in arrow function

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

---

## 🧩 Advanced Function Patterns

# Closures

- A closure in JavaScript occurs when a function is able to `remember the variables` from its `lexical scope`, even when that `function is executed outside of that scope`.
- In other words, a closure allows a function to `access variables from an outer function` even after the `outer function has finished executing`.
- Closures are formed when inner functions maintain access to the outer function's scope
- Closures provide data privacy and state persistence between function calls
- Each closure has its own "memory" of the variables it captures
- Closures are widely used in real-world JavaScript for:
  - Data encapsulation
  - Function factories
  - Callbacks and event handling
  - Module patterns
  - Memoization (caching)
- Care must be taken to avoid memory leaks with closures
- Example: `Bank Account Using Closures`

```js
function createBankAccount(initialBalance) {
  // The `balance` is private
  let balance = initialBalance;

  return {
    // Function to deposit money into the account
    deposit: function (amount) {
      if (amount > 0) {
        balance += amount;
        console.log(`Deposited: $${amount}. New balance: $${balance}`);
      } else {
        console.log("Invalid deposit amount");
      }
    },

    // Function to withdraw money from the account
    withdraw: function (amount) {
      if (amount > 0 && amount <= balance) {
        balance -= amount;
        console.log(`Withdrew: $${amount}. New balance: $${balance}`);
      } else {
        console.log("Insufficient funds or invalid amount");
      }
    },

    // Function to check the current balance
    checkBalance: function () {
      console.log(`Current balance: $${balance}`);
      return balance;
    },
  };
}

// Creating a new bank account with an initial balance of $1000
const myAccount = createBankAccount(1000);

// Using the closure to interact with the bank account
myAccount.deposit(500); // Deposits $500
myAccount.withdraw(200); // Withdraws $200
myAccount.checkBalance(); // Prints the current balance
```

### debounce example

```js
function debounce(fn, delay) {
  let timeId;
  return function (...args) {
    let context = this;
    !!timeId && clearTimeout(timeId);
    timeId = setTimeout(() => {
      fn.apply(context, args);
    }, delay);
  };
}
```

### throttle example

```js
function throttle(fn, delay) {
  let timeId = null;
  return function (...args) {
    let context = this;
    if (timeId) return;
    fn.apply(context, args);
    timeId = setTimeout(() => {
      timeId = null;
    }, delay);
  };
}
```

### Simple Addition with Memoization

```js
function memoizeAdd() {
  const cache = {};

  return function (a, b) {
    const key = `${a},${b}`; // Use a string key to store result for inputs a and b

    if (key in cache) {
      console.log("Fetching from cache:", key);
      return cache[key];
    }

    console.log("Calculating result:", key);
    const result = a + b;
    cache[key] = result;

    return result;
  };
}

const add = memoizeAdd();

console.log(add(3, 5)); // Output: 8 (calculated)
console.log(add(3, 5)); // Output: 8 (fetched from cache)
console.log(add(10, 15)); // Output: 25 (calculated)
console.log(add(10, 15)); // Output: 25 (fetched from cache)
```

### Memoization with Closures Example

```js
// Fibonacci Function Without Memoization (Inefficient)
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(10)); // 55

// Fibonacci Function With Memoization (efficient)
function memoizedFibonacci() {
  // This cache object stores the results of the previous Fibonacci calculations.
  const cache = {};

  // This function uses the cache to avoid recalculating values.
  return function fib(n) {
    // Check if the result is already in the cache
    if (n in cache) {
      return cache[n];
    }

    // Base cases: Fibonacci(0) = 0, Fibonacci(1) = 1
    if (n <= 1) {
      cache[n] = n;
      return n;
    }

    // Recursively calculate the Fibonacci value and store it in the cache
    cache[n] = fib(n - 1) + fib(n - 2);

    // Return the cached result
    return cache[n];
  };
}

const fib = memoizedFibonacci();

console.log(fib(10)); // 55
console.log(fib(50)); // 12586269025 (computed much faster)
```

**[Interview questions](https://roadsidecoder.hashnode.dev/closures-javascript-interview-questions)**

---

# Currying

- Instead of taking all arguments at once, the function takes the `first argument`, `returns a new function` that takes the `second argument`, and so on, `until all arguments have been provided`
- Real-Life Example: `Coffee Shop Order`

Imagine you're at a `coffee shop ordering a customized drink`. Instead of giving all your preferences at once, the barista asks for your choices `step by step`.

1. First, you choose the type of drink (e.g., latte, cappuccino).
2. Next, you specify the size (e.g., small, medium, large).
3. Finally, you choose any extra options (e.g., extra shot of espresso, syrup).

At each step, the barista asks for more information and finalizes the order only after you've provided all the details.

```js
// Currying function for placing a coffee order
function orderCoffee(drinkType) {
  return function (size) {
    return function (extra) {
      return `Order placed: ${size} ${drinkType} with ${extra}`;
    };
  };
}

// Placing the order step by step
const orderLatte = orderCoffee("Latte");
const orderMediumLatte = orderLatte("Medium");
const finalOrder = orderMediumLatte("an extra shot of espresso");
// can be called by another way
const anotherFinalOrder = orderCoffee("cappuccino")("Large")(
  "an extra shot of espresso"
);

console.log(finalOrder); // Output: Order placed: Medium Latte with an extra shot of espresso
console.log(anotherFinalOrder); // Output: Order placed: Large cappuccino with an extra shot of espresso
```

- Benefits of Currying:
- `Reuse Functions`: You can reuse parts of the function. For example, you can create a partially applied function like `orderLatte` for all latte orders, without needing to specify the drink type every time.

- `Customization`: Currying allows you to break down the `logic into smaller pieces`, making it easier to compose and customize function behavior.

```js
function sum(a, b, c) {
  return a + b + c;
}
sum(1, 2, 3); // 6

function sum(a) {
  return (b) => {
    return (c) => {
      return a + b + c;
    };
  };
}

const add = (a) => (b) => (c) => a + b + c;

console.log(sum(1)(2)(3)); // 6
console.log(add(1)(2)(3)); // 6
```

- It helps you avoid passing the same variable again and again
- It helps to create a higher order function

```js
// Another Example of a curried function

const multiply = (x, y) => x * y;

const curriedMultiply = x => y => x * y;

console.log(multiply(2, 3));

console.log(curriedMultiply(2));  // y => x * y
console.log(curriedMultiply(2)(3)); // 6


// Partially applied functions are a common use of currying
const timesTen = curriedMultiply(10);

console.log(timesTen); // y => x * y
console.log(timesTen(8)); // 80

// Another example

const updateElemText = id => content => document.querySelector(`#${id}`).
textContent = content;

Const updateHeaderText = updateElemText("header");
updateHeaderText("Hello Dave!");

// Another example
let log = (time) => (type) => (msg) =>
  `At ${time.toLocaleString()}: severity ${type} => ${msg}`;

log(new Date())("error")("power not sufficient");

let logNow = log(new Date());

logNow("warning")("temp high");

let logErrorNow = log(new Date())("error");

logErrorNow("unknown error");
```

- normal function to curried function

```js
const curry = (fn) => {
  return (curried = (...args) => {
    if (fn.length !== args.length) {
      return curried.bind(null, ...args);
    }
    return fn(...args);
  });
};

const total = (a, b, c) => a + b + c;
const curriedTotal = curry(total);
curriedTotal(10)(20)(30); //60
```

## 📝 Summary & Best Practices

- ✅ Use function declarations for main functions and hoisting benefits
- ✅ Use arrow functions for short callbacks and lexical this binding
- ✅ Use default parameters for more robust functions
- ✅ Follow pure function principles when possible
- ✅ Document your functions with clear comments
- ✅ Name functions clearly to describe what they do, not how they do it
- ✅ Keep functions focused on a single task (Single Responsibility)
- ✅ Limit function parameters (ideally 3 or fewer)
- ✅ Use early returns to avoid deep nesting

## 🔍 Key Terms Reference

| Term                  | Description                                                           |
| --------------------- | --------------------------------------------------------------------- |
| Function              | A reusable block of code that performs a specific task                |
| Parameter             | Variables listed in function definition                               |
| Argument              | Actual values passed to a function when called                        |
| Function Expression   | Assigning a function to a variable                                    |
| Return Value          | Data sent back from a function                                        |
| Arrow Function        | Shorthand syntax for writing functions                                |
| Callback              | Function passed as argument to another function                       |
| Pure Function         | Function with no side effects that returns same output for same input |
| Higher-Order Function | Function that takes or returns other functions                        |
| IIFE                  | Function that runs as soon as it's defined                            |
| Recursion             | Function that calls itself                                            |
| Call Stack            | Mechanism to track function execution order                           |

---

# Most asked interview questions

### Task 1: What will the following code output?

```javascript
function outer() {
  var x = 10;

  function inner() {
    console.log(x);
  }

  x = 20;
  return inner;
}

var result = outer();
result();
```

<details>
<summary>Click for answer</summary>
<p>Output: <code>20</code></p>
<p>Although the inner function is created when <code>x</code> is 10, it captures a reference to <code>x</code>, not its value at that time. By the time <code>inner</code> is called, <code>x</code> has been changed to 20.</p>
</details>

### Task 2: Implement a counter with increment, decrement, and reset functions using closures.

<details>
<summary>Click for solution</summary>
<pre><code>function createCounter() {
    let count = 0;
    
    return {
        increment: function() {
            count++;
            return count;
        },
        decrement: function() {
            count--;
            return count;
        },
        reset: function() {
            count = 0;
            return count;
        },
        getCount: function() {
            return count;
        }
    };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.decrement()); // 1
console.log(counter.reset()); // 0
</code></pre>

</details>

### Task 3: What will be the output of this code?

```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

<details>
<summary>Click for answer</summary>
<p>Output:</p>
<pre>4
4
4</pre>
<p>This happens because <code>var</code> creates a function-scoped variable. By the time the timeout callbacks execute, the loop has completed and <code>i</code> is 4. All three callbacks reference the same <code>i</code>.</p>
</details>

### Task 4: Fix the code in Task 3 using closures to output 1, 2, 3.

<details>
<summary>Click for solution</summary>
<p>Option 1: Using IIFE (Immediately Invoked Function Expression):</p>
<pre><code>for (var i = 1; i <= 3; i++) {
    (function(j) {
        setTimeout(function() {
            console.log(j);
        }, 1000);
    })(i);
}
</code></pre>
<p>Option 2: Using let (ES6):</p>
<pre><code>for (let i = 1; i <= 3; i++) {
    setTimeout(function() {
        console.log(i);
    }, 1000);
}
</code></pre>
</details>

### Task 5: Create a function `createMultiplier` that returns a function which multiplies a number by a specified multiplier.

<details>
<summary>Click for solution</summary>
<pre><code>function createMultiplier(multiplier) {
    return function(value) {
        return value * multiplier;
    };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
</code></pre>

</details>

### Task 6: Implement a function `memoize` that caches the results of expensive function calls.

<details>
<summary>Click for solution</summary>
<pre><code>function memoize(fn) {
    const cache = {};
    
    return function(...args) {
        const key = JSON.stringify(args);
        
        if (key in cache) {
            console.log("Cached result");
            return cache[key];
        }
        
        console.log("Calculating result");
        const result = fn(...args);
        cache[key] = result;
        return result;
    };
}

// Example usage
function expensiveCalculation(a, b) {
// Simulate expensive operation
console.log("Performing expensive calculation...");
return a \* b;
}

const memoizedCalc = memoize(expensiveCalculation);

console.log(memoizedCalc(4, 5)); // Performs calculation
console.log(memoizedCalc(4, 5)); // Uses cached result
console.log(memoizedCalc(3, 7)); // Performs calculation
</code></pre>

</details>

### Task 7: What would the following code snippet output?

```javascript
function createFunctions() {
  var result = [];

  function createFunction(i) {
    return function () {
      return i;
    };
  }

  for (var i = 0; i < 3; i++) {
    result.push(createFunction(i));
  }

  return result;
}

var functions = createFunctions();
console.log(functions[0]());
console.log(functions[1]());
console.log(functions[2]());
```

<details>
<summary>Click for answer</summary>
<p>Output:</p>
<pre>0
1
2</pre>
<p>This code correctly uses a separate function <code>createFunction</code> to create a closure for each value of <code>i</code>.</p>
</details>

### Task 8: Create a private counter module using the module pattern and closures.

<details>
<summary>Click for solution</summary>
<pre><code>const counterModule = (function() {
    // Private variables
    let count = 0;
    
    // Private functions
    function validateCount(newCount) {
        return Number.isInteger(newCount);
    }
    
    // Public API
    return {
        increment: function() {
            count++;
            return count;
        },
        decrement: function() {
            count--;
            return count;
        },
        getCount: function() {
            return count;
        },
        setCount: function(newCount) {
            if (validateCount(newCount)) {
                count = newCount;
                return true;
            }
            return false;
        }
    };
})();

console.log(counterModule.getCount()); // 0
counterModule.increment();
counterModule.increment();
console.log(counterModule.getCount()); // 2
counterModule.setCount(10);
console.log(counterModule.getCount()); // 10
console.log(counterModule.setCount("not a number")); // false (validation failed)
</code></pre>

</details>

### Task 9: Create a function that generates unique IDs using closure.

<details>
<summary>Click for solution</summary>
<pre><code>function createIdGenerator() {
    let id = 0;
    
    return function(prefix = '') {
        id++;
        return `${prefix}${id}`;
    };
}

const generateUserId = createIdGenerator();
const generateProductId = createIdGenerator();

console.log(generateUserId('USER-')); // "USER-1"
console.log(generateUserId('USER-')); // "USER-2"
console.log(generateProductId('PROD-')); // "PROD-1" (separate counter)
console.log(generateUserId('USER-')); // "USER-3"
</code></pre>

</details>

### Task 10: Implement a "once" function that ensures a function is only called once using closures.

<details>
<summary>Click for solution</summary>
<pre><code>function once(fn) {
    let called = false;
    let result;
    
    return function(...args) {
        if (called) {
            return result;
        }
        
        called = true;
        result = fn.apply(this, args);
        return result;
    };
}

// Example usage
function initializeApp(config) {
console.log("App initialized with:", config);
return `App started with ${config.name}`;
}

const initialize = once(initializeApp);

console.log(initialize({name: "MyApp", version: "1.0"})); // Initializes and returns
console.log(initialize({name: "AttemptedRestart", version: "2.0"})); // Returns previous result, doesn't initialize again
</code></pre>

</details>
