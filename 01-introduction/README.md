# What is JavaScript?

- created to `make web pages alive`

- `lightweight`, `prototype - based`, `single - threaded`, `dynamic language`, `object - oriented`, `interpreted` or `just-in-time compiled` programming language

- can execute not only in the `browser`, but also on the `server` <br/>eg.`Node.js`,`Apache CouchDB`

- JavaScript engines :
  - ` "V8" – in Chrome, Opera and Edge`
  - `"SpiderMonkey" – in Firefox`
  - `"Chakra" - in IE`
  - `"JavaScriptCore", "Nitro" and "SquirrelFish" - in Safari`, etc

# Why is it called JavaScript?

- It initially had another name: `LiveScript`

* But `Java` was very popular at that time, so it was decided that positioning a new language as a `younger brother of Java` would help

# How do engines (translator) work?

```
parse(read)  =>  compiles(translate)  =>  run
```

# How to link with HTML ?

- for `inline` js

  ```html
  <a href="#" onclick="alert(this)">Click Me</a>
  ```

- for `internal` file

  ```html
  <script>
    ....
  </script>
  ```

- for `external` file

  ```html
  <script src="path/to/script.js"></script>
  ```

# Async Vs Defer In Javascript

## Normal `<script>` tag

```html
<html>
<head> ... </head>
<body>
    ...
    <script src="script.js">
    ....
</body>
</html>
```

- JS `blocks` the parsing of HTML
- `fetches` the script from the network
- `Executes` the script
- HTML parsing is started only after the `script is fully executed`

![asyncVSdefer](./images/async-defer/async-defer-1.png)

## The async Attribute

```html
<script async src="script.js">
```

- `HTML parsing` and `script fetched` from the network goes asynchronously

- As soon as scripts are `fetched`, HTML parsing `stops` & scripts start `executing`

- Once the scripts are executed, the HTML parsing continues like regular

![asyncVSdefer](./images/async-defer/async-defer-2.png)

## The defer Attribute

```html
<script defer src="script.js">
```

- HTML parsing goes on and scripts are fetched in `parallel`

- Scripts are only `executed` once the HTML `parsing is complete`

![asyncVSdefer](./images/async-defer/async-defer-3.png)

## Which one to use?

- `async` attribute does not guarantee the order of execution of scripts but `defer` does

- So for this, we can use an alternative solution which is to use the `<script>` tag just before the `<body>` tag of the HTML file.

# What is “use strict” ?

- always at the `top` of your scripts

- with Strict mode you cannot use any variable before initializing it.

```js
// note: no "use strict" in this example

num = 5; // the variable "num" is created if it didn't exist

alert(num); // 5
```

```js
"use strict";

num = 5; // error: num is not defined
```

- Declared inside a `function`, it has `local scope` (only the code inside the function is in strict mode)

```js
x = 3.14; // This will not cause an error.
myFunction();

function myFunction() {
  "use strict";
  y = 3.14; // This will cause an error
}
```

- `Modern JS` supports “classes” and “modules” – advanced language structures, that `enable use strict automatically`. So we don’t need to add the "use strict" directive, if we use them.

# Alert, Prompt and Confirm

## alert

- `shows a message` and waits for the user to press “OK”

```js
alert("Hello");
```

## prompt

- `takes input` from user
- The function prompt accepts `two` arguments:

```js
result = prompt(title, [default]);

let age = prompt('How old are you?', 100);

alert(`You are ${age} years old!`); // You are 100 years old!
```

## confirm

- The function confirm `shows a modal` window with a question and two buttons: `OK` and `Cancel`

- The result is `true if OK` is pressed and `false otherwise`

```js
let isBoss = confirm("Are you the boss?");

alert(isBoss); // true if OK is pressed
```

# Data types

- We can put `any type` in a variable

- hence it is `dynamically typed`

```js
// no error
let message = "hello";
message = 123456;
```

## _Primitive Data Type_

- They are called `primitive` because their `values can contain only a single thing` (be it a string or a number or whatever)

- `String`, `Number`, `Boolean`, `Undefined`, `Null`, `BigInt` and `Symbol`

### 1. String

- A string is any `series of characters` enclosed with `single` quotes, `double` quotes or `backticks`

```js
let firstName = "John";
let lastName = "Cena";

// Template String
alert(`Hello, ${firstName} ${lastName}!`); // Hello, John Cena!
```

### 2. Number

- The number type represents both `integer and floating point` numbers

- There are many `operations` for numbers

  | Operator | Description             |
  | -------- | ----------------------- |
  | +        | Addition                |
  | -        | Subtraction             |
  | \*       | Multiplication          |
  | \*\*     | Exponentiation (ES2016) |
  | /        | Division                |
  | %        | Modulus (Remainder)     |
  | ++       | Increment               |
  | --       | Decrement               |

- `special numeric values` - `Infinity`, `-Infinity` and `NaN`.

```js
alert(1 / 0); // Infinity
alert("not a number" / 2); // NaN, such division is erroneous

alert(NaN + 1); // NaN
alert(3 * NaN); // NaN
alert("not a number" / 2 - 1); // NaN
```

- `Increment` ++ /`decrement` -- (PRE/POST)

```js
let counter = 0;
alert(++counter); // 1

let counter = 0;
alert(counter++); // 0

let counter = 5;
alert(--counter); // 4

let counter = 5;
alert(counter--); // 5

let counter = 0;
counter++;
++counter;
alert(counter); // 2, the lines above did the same
```

### 3. BigInt

- In JS, the `Number` type cannot safely represent integer values larger than (253-1) (that’s 9007199254740991)`Number.MAX_SAFE_INTEGER`, or less than -(253-1) for negatives `Number.MIN_SAFE_INTEGER`.

```js
// For example, these two numbers (right above the safe range) are the same :

console.log(9007199254740991 + 1); // 9007199254740992
console.log(9007199254740991 + 2); // 9007199254740992
```

- `to get more precise results` we use bigint

```js
// the "n" at the end means it's a BigInt
const bigInt = 1234567890123456789012345678901234567890n;

let myNumber = BigInt(12);
let sameMyNumber = 123n;

console.log(myNumber + sameMyNumber);
// for math operation both values must be of bigint type
```

### 4. Boolean (logical type)

- The boolean type has only two values: `true` and `false`

```js
let nameFieldChecked = true; // yes, name field is checked
let ageFieldChecked = false; // no, age field is not checked

let isGreater = 4 > 1;
alert(isGreater); // true (the comparison result is "yes")
```

- Comparison Operators

| Operator | Description                       |
| -------- | --------------------------------- |
| ==       | equal to                          |
| ===      | equal value and equal type        |
| !=       | not equal                         |
| !==      | not equal value or not equal type |
| >        | greater than                      |
| <        | less than                         |
| >=       | greater than or equal to          |
| <=       | less than or equal to             |
| ?        | ternary operator                  |

### 5. Null

- In JS, null is `not` a `reference to a non-existing object` or a `null pointer` like in some other languages

- special value - `nothing`, `empty` or `value unknown`

- `typeof null` is `object` <=== `bug`

```js
let age = null;
// The code above states that age is unknown.
```

### 6 .Undefined

- The meaning of `undefined` is `value is not assigned`.

- If a variable is `declared`, but `not assigned`, then its value is `undefined`

```js
let age;
alert(age); // shows "undefined"
```

### Null vs Undefined

| --        | --                                         |
| --------- | ------------------------------------------ |
| Undefined | used for `unintentionally` missing values. |
| Null      | used for `intentionally` missing values.   |

```js
console.log(null == undefined); // true
console.log(null === undefined); // false

console.log(typeof null); // Object
console.log(typeof undefined); // undefined

let a = null;
console.log(a); // null

let c;
let d = undefined;
console.log(c, d); // undefined undefined
```

### Strange result: null vs 0

```js
alert(null > 0); //  false
alert(null == 0); //  false
alert(null >= 0); //  true
```

### An incomparable undefined

```js
alert(undefined > 0); // false
alert(undefined < 0); // false
alert(undefined == 0); // false
```

### 7 .Symbols

- represents a `unique identifier`
- created with Symbol() call with an `optional description` (name)

```js
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

## _# Non-Primitive Data Type (object/array)_

- All other types are called `primitive` because their values can `contain only a single thing` (be it a string or a number or whatever)

- used to store `collections of data` and `more complex entities`

# The typeof operator

- The `typeof` operator returns the `type of the argument`

```js
typeof undefined; // "undefined"
typeof 0; // "number"
typeof 10n; // "bigint"
typeof true; // "boolean"
typeof "foo"; // "string"
typeof Symbol("id"); // "symbol"
typeof Math; // "object"  (1)
typeof null; // "object"  (2)
typeof alert; // "function"  (3)
```

# Type Conversion

### String Conversion

```js
let value = true;
alert(typeof value); // boolean

value = String(value); // now value is a string "true"
alert(typeof value); // string
```

### Numeric Conversion

- Numeric conversion happens in mathematical functions and expressions automatically.

```js
alert("6" / "2"); // 3, strings are converted to numbers
```

- We can use the Number(value) function to explicitly convert a value to a number

```js
let str = "123";
alert(typeof str); // string

let num = Number(str); // becomes a number 123

alert(typeof num); // number
```

### Boolean Conversion

```js
Boolean(1); // true
Boolean(0); // false

Boolean("hello"); // true
Boolean(""); // false

Boolean("0"); // true
Boolean(" "); // spaces, also true (any non-empty string is true)
```

### Numeric Methods

```js
Number("3.14"); // returns 3.14
Number(" 10 "); // returns 10
Number("123z"); // NaN (error reading a number at "z")
Number(""); // returns 0
Number("John"); // returns NaN
Number("99 88"); // returns NaN
Number(true); // returns 1
Number(false); // returns 0

let string1 = "17";
let string2 = "10";

let newString = +string1 + +string2; //27
console.log(typeof newString); //Number

let y = 5; // y is a number
let x = y + ""; // x is a string

let x = 123;
x.toString(); //'123'
(100 + 23).toString(); //'123'

let x = 9.656;
x.toFixed(0); //10
x.toFixed(2); //9.66

let x = 9.656;
x.toPrecision(); //9.656
x.toPrecision(2); //9.7

parseInt("-10.33"); // returns 10
parseInt("10"); // returns 10
parseInt("10.33"); // returns 10
parseInt("10 6"); // returns 10
parseInt("10 years"); // returns 10
parseInt("years 10"); // returns NaN
```

# Type coercion

- Type coercion is the `automatic or implicit conversion` of values from one data type to another (such as strings to numbers).

```js
const value1 = "5";
const value2 = 9;
let sum = value1 + value2; //59

sum = Number(value1) + value2; //14

alert(6 - "2"); // 4, converts '2' to a number
alert("6" / "2"); // 3, converts both operands to numbers
```
