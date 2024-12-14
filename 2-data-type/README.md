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

// Template String
alert(`Hello, ${firstName}!`); // Hello, John!
```

#### **Escape Sequences in Strings**

- `\` followed by some characters is an escape sequence.
- Let's see the most common escape characters:
  - `\n`: new line
  - `\t`: Tab, means 8 spaces
  - `\\`: Back slash
  - `\'`: Single quote (')
  - `\"`: Double quote (")

#### **String Methods**

1. `_length_`: returns the `number of characters`

```js
let js = "JavaScript";
console.log(js.length); // 10
```

2. `_Accessing characters in a string_`: We can access each character in a string using its `index`.

```js
let string = "JavaScript";
let firstLetter = string[0];
console.log(firstLetter); // J
let lastIndex = string.length - 1;
console.log(lastIndex); // 9
console.log(string[lastIndex]); // t
```

3. `_toUpperCase()_`: changes the string to `uppercase` letters

```js
let string = "JavaScript";
console.log(string.toUpperCase()); // JAVASCRIPT
```

4. `_toLowerCase()_`: changes the string to `lowercase` letters.

```js
let string = "JavasCript";
console.log(string.toLowerCase()); // javascript
```

5. `_substr()_`: It takes `two arguments`, the `starting index` and `number of characters to slice`.

```js
const str = "substr";

console.log(str.substr(1, 2)); // (1, 2): ub
console.log(str.substr(1)); // (1): ubstr

/* can pass negative start index */
console.log(str.substr(-3, 2)); // (-3, 2): st
console.log(str.substr(-3)); // (-3): str
```

6. `slice()_`: It takes `two arguments`, the `starting index` and the `stopping index`. can pass negative indices for both args

```js
const str = "The quick brown fox jumps over the lazy dog.";

console.log(str.slice(31)); // expected output: "the lazy dog."

console.log(str.slice(4, 19)); // expected output: "quick brown fox"

console.log(str.slice(-4)); // expected output: "dog."

console.log(str.slice(-9, -5)); // expected output: "lazy"
```

7. `_substring()_`: It takes `two arguments`, the `starting index` and the `stopping index` but it `doesn't include` the character at the `stopping index`.

```js
let string = "JavaScript";
console.log(string.substring(0, 4)); // Java
console.log(string.substring(4, 10)); // Script
console.log(string.substring(4)); // Script
```

| method                | selects…                                  | negatives              |
| --------------------- | ----------------------------------------- | ---------------------- |
| slice(start, end)     | from start to end (not including end)     | allows negatives       |
| substring(start, end) | between start and end (not including end) | negative values mean 0 |
| substr(start, length) | from start get length characters          | allows negative start  |

8. `_split()_`: `splits` a string at a specified place.

```js
let string = "30 Days Of JavaScript";
let firstName = "Asabeneh";
console.log(firstName.split()); // Change to an array - > ["Asabeneh"]
console.log(firstName.split("")); // Split to an array at each letter ->  ["A", "s", "a", "b", "e", "n", "e", "h"]
let countries = "Finland, Sweden, Norway, Denmark, and Iceland";
console.log(countries.split(",")); // split to any array at comma -> ["Finland", " Sweden", " Norway", " Denmark", " and Iceland"]
console.log(countries.split(", ")); //  ["Finland", "Sweden", "Norway", "Denmark", "and Iceland"]
```

9. `_trim()_`: `Removes trailing space` in the `beginning` or the `end` of a string.

```js
let string = "   30 Days Of JavaScript   ";
console.log(string);
console.log(string.trim(" "));
```

```sh
   30 Days Of JavasCript
30 Days Of JavasCript
```

10. `_includes()_`: returns a `boolean`. If a `substring exist` in a string, it returns `true`, otherwise it returns `false`.

```js
let string = "30 Days Of JavaScript";
console.log(string.includes("Days")); // true
console.log(string.includes("days")); // false - it is case sensitive!
```

11. `_replace()_`: takes as a parameter the old substring and a new substring.

```js
string.replace(oldsubstring, newsubstring);
```

```js
let string = "30 Days Of JavaScript";
console.log(string.replace("JavaScript", "Python")); // 30 Days Of Python
```

12. `_charAt()_`: Takes `index` and it returns the `value at that index`

```js
string.charAt(index);
```

```js
let string = "30 Days Of JavaScript";
console.log(string.charAt(0)); // 3
let lastIndex = string.length - 1;
console.log(string.charAt(lastIndex)); // t
```

13. `_charCodeAt()_`: Takes `index` and it returns `char code (ASCII number)` of the value at that index

```js
string.charCodeAt(index);
```

```js
let string = "30 Days Of JavaScript";
console.log(string.charCodeAt(3)); // D ASCII number is 68
let lastIndex = string.length - 1;
console.log(string.charCodeAt(lastIndex)); // t ASCII is 116
```

14. `_indexOf()_`: Takes a `substring` and if the substring `exists` in a string it returns the `first position` of the substring if `does not exist` it returns `-1`

```js
string.indexOf(substring);
```

```js
let string = "30 Days Of JavaScript";
console.log(string.indexOf("D")); // 3
console.log(string.indexOf("Days")); // 3
console.log(string.indexOf("days")); // -1
```

15. `_lastIndexOf()_`: Takes a `substring` and if the substring `exists` in a string it returns the `last position` of the substring if it `does not exist` it returns `-1`

```js
//syntax
string.lastIndexOf(substring);
```

```js
let string =
  "I love JavaScript. If you do not love JavaScript what else can you love.";
console.log(string.lastIndexOf("love")); // 67
console.log(string.lastIndexOf("you")); // 63
console.log(string.lastIndexOf("JavaScript")); // 38
```

16. `_concat()_`: it takes many substrings and joins them.

```js
string.concat(substring, substring, substring);
```

```js
let string = "30";
console.log(string.concat("Days", "Of", "JavaScript")); // 30DaysOfJavaScript
```

17. `_startsWith_`: it takes a `substring` as an argument and it checks if the string `starts with that specified substring`. It returns a `boolean`.

```js
//syntax
string.startsWith(substring);
```

```js
let string = "Love is the best to in this world";
console.log(string.startsWith("Love")); // true
console.log(string.startsWith("love")); // false
```

18. `_endsWith_`: it takes a `substring` as an argument and it checks if the string `ends with that specified substring`. It returns a `boolean`.

```js
string.endsWith(substring);
```

```js
let string = "Love is the most powerful feeling in the world";
console.log(string.endsWith("world")); // true
console.log(string.endsWith("love")); // false
console.log(string.endsWith("in the world")); // true
```

19. `_search_`: it takes a `substring` as an argument and it returns the `index` of the first match. The search value can be a `string` or a `regular expression pattern`.

```js
string.search(substring);
```

```js
let string =
  "I love JavaScript. If you do not love JavaScript what else can you love.";
console.log(string.search("love")); // 2
console.log(string.search(/javascript/gi)); // 7
```

20. `_match_`: it takes a `substring` or `regular expression pattern` as an argument and it returns an `array` if there is `match` if `not` it returns `null`. Let us see how a regular expression pattern looks like. It starts with / sign and ends with / sign.

```js
let string = "love";
let patternOne = /love/; // with out any flag
let patternTwo = /love/gi; // g-means to search in the whole text, i - case insensitive
```

Match syntax

```js
// syntax
string.match(substring);
```

```js
let string =
  "I love JavaScript. If you do not love JavaScript what else can you love.";
console.log(string.match("love"));
```

```sh
["love", index: 2, input: "I love JavaScript. If you do not love JavaScript what else can you love.", groups: undefined]
```

21. `_repeat()_`: it takes a `number` as argument and it returns the `repeated version of the string`.

```js
string.repeat(n);
```

```js
let string = "love";
console.log(string.repeat(10)); // lovelovelovelovelovelovelovelovelovelove
```

21. `pad...()_`: adds `extra character` to get required length.

```js
var s = "10";
console.log(s.padStart("5", "0"));
//00010

console.log(s.padEnd("5", "0"));
//10000
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

// special methods
alert(Number.isNaN(NaN)); // true
alert(Number.isNaN("str" / 2)); // true

// Note the difference:
alert(Number.isNaN("str")); // false, because "str" belongs to the string type, not the number type
alert(isNaN("str")); // true, because isNaN converts string "str" into a number and gets NaN as a result of this conversion

alert(Number.isFinite(123)); // true
alert(Number.isFinite(Infinity)); // false
alert(Number.isFinite(2 / 0)); // false

// Note the difference:
alert(Number.isFinite("123")); // false, because "123" belongs to the string type, not the number type
alert(isFinite("123")); // true, because isFinite converts string "123" into a number 123
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

#### **Math Object**

```js
const PI = Math.PI;
console.log(PI); // 3.141592653589793
// Rounding to the closest number
// if above .5 up if less 0.5 down rounding
console.log(Math.round(PI)); // 3 to round values to the nearest number
console.log(Math.round(9.81)); // 10
console.log(Math.floor(PI)); // 3 rounding down
console.log(Math.ceil(PI)); // 4 rounding up
console.log(Math.min(-5, 3, 20, 4, 5, 10)); // -5, returns the minimum value
console.log(Math.max(-5, 3, 20, 4, 5, 10)); // 20, returns the maximum value
const randNum = Math.random(); // creates random number between 0 to 0.999999
console.log(randNum);
// Let us  create random number between 0 to 10
const num = Math.floor(Math.random() * 11); // creates random number between 0 and 10
console.log(num);
//Absolute value
console.log(Math.abs(-10)); // 10
//Square root
console.log(Math.sqrt(100)); // 10
console.log(Math.sqrt(2)); // 1.4142135623730951
// Power
console.log(Math.pow(3, 2)); // 9
console.log(Math.E); // 2.718
// Logarithm
// Returns the natural logarithm with base E of x, Math.log(x)
console.log(Math.log(2)); // 0.6931471805599453
console.log(Math.log(10)); // 2.302585092994046
// Returns the natural logarithm of 2 and 10 respectively
console.log(Math.LN2); // 0.6931471805599453
console.log(Math.LN10); // 2.302585092994046
// Trigonometry
Math.sin(0);
Math.sin(60);
Math.cos(0);
Math.cos(60);
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

## Checking Data Types and Casting

### Checking Data Types

- To check the data type of a certain variable we use the `_typeof_` method.
  **Example:**

```js
console.log(typeof "Asabeneh"); // string
console.log(typeof 10); // number
console.log(typeof 3.14); // number
console.log(typeof true); // boolean
console.log(typeof false); // boolean
console.log(typeof NaN); // number
console.log(typeof undefined); // undefined
console.log(typeof null); // object
```

### Changing Data Type (Casting)

- `Casting`: `Converting one data type to another data type`. We use _parseInt()_, _parseFloat()_, _Number()_, _+ sign_, _str()_
- `Type coercion` is the `automatic or implicit conversion` of values from one data type to another (such as strings to numbers).

```js
const value1 = "5";
const value2 = 9;
let sum = value1 + value2; //59

sum = Number(value1) + value2; //14

alert(6 - "2"); // 4, converts '2' to a number
alert("6" / "2"); // 3, converts both operands to numbers
```

#### String to Int

- parseInt()
- Number()
- Plus sign(+)

```js
let num = "10";
let numInt = parseInt(num);
console.log(numInt); // 10
```

```js
let num = "10";
let numInt = Number(num);
console.log(numInt); // 10
```

```js
let num = "10";
let numInt = +num;
console.log(numInt); // 10
```

#### String to Float

- parseFloat()
- Number()
- Plus sign(+)

```js
let num = "9.81";
let numFloat = parseFloat(num);
console.log(numFloat); // 9.81
```

```js
let num = "9.81";
let numFloat = Number(num);
console.log(numFloat); // 9.81
```

```js
let num = "9.81";
let numFloat = +num;
console.log(numFloat); // 9.81
```

#### Float to Int

- parseInt()

```js
let num = 9.81;
let numInt = parseInt(num);
console.log(numInt); // 9
```
