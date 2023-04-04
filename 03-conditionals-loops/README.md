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

## Strict equality

- A strict equality operator `===` checks the equality without type conversion
- checks value and data type both

```js
alert(0 == false); // true
alert(0 === false); // false, because the types are different
```

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

```js
let x = 1 && 2 ?? 3; // Syntax error

let x = (1 && 2) ?? 3; // Works
alert(x); // 2
```

# if else condition

```js
let age = 3;

if (age >= 5) {
  console.log("coffee");
} else {
  console.log("milk");
}
// milk
```

# ternary operator

```js
let age = 3;
let drink = age >= 5 ? "coffee" : "milk";
console.log(drink); //milk
```

### Multiple ‘?’

```js
let age = prompt("age?", 18);

let message =
  age < 3
    ? "Hi, baby!"
    : age < 18
    ? "Hello!"
    : age < 100
    ? "Greetings!"
    : "What an unusual age!";

alert(message);
```

# if - else if - else

```js
let age = 23;
if (age < 3) {
  message = "Hi, baby!";
} else if (age < 18) {
  message = "Hello!";
} else if (age < 100) {
  message = "Greetings!";
} else {
  message = "What an unusual age!";
}

// Greetings!
```

# Switch case

```js
let day = 9;

switch (day) {
  case 0:
    console.log("Sunday");
    break;
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  case 4:
    console.log("Thrusday");
    break;
  case 5:
    console.log("Friday");
    break;
  case 6:
    console.log("Saturday");
    break;
  default:
    console.log("Invalid Day");
}
```

### Examples to use conditions in the cases

```js
let num = prompt("Enter number");
switch (true) {
  case num > 0:
    console.log("Number is positive");
    break;
  case num == 0:
    console.log("Numbers is zero");
    break;
  case num < 0:
    console.log("Number is negative");
    break;
  default:
    console.log("Entered value was not a number");
}
```

# while loop

```js
let num = 10;
let total = 0;
let i = 0;

while (i <= num) {
  total = total + i;
  i++;
}

console.log(total); //55
```

# for loop

```js
for (let i = 0; i <= 9; i++) {
  console.log(i); // "0", "1", "2", "3", "4", "5", "6", "7", "8","9"
}
```

# for-in and for-of loop

- Both `for..of` and `for..in` statements `iterate` over lists
- the `values iterated on are different though`
- only `for..in` used to iterate object
- `for..in` returns a `keys for object` and return `index of array`
- `for..of` returns a list of `values`

```js
let list = [4, 5, 6];

for (let i in list) {
  console.log(i); // "0", "1", "2",
}

for (let i of list) {
  console.log(i); // "4", "5", "6"
}
```

# break keyword

```js
for (let i = 1; i <= 10; i++) {
  if (i === 4) {
    break;
  }
  console.log(i); //1,2,3
}
```

# continue keyword

```js
for (let i = 1; i <= 10; i++) {
  if (i === 4) {
    continue;
  }
  console.log(i); //1,2,3,5,6,7,8,9,10
}
```

# do while loop

```js
let i = 10;
do {
  console.log(i); //10
  i++;
} while (i <= 9);

console.log("value of i is ", i); //11
```
