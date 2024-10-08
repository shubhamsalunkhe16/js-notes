# Variables

- used to `store information` and use them later

```js
let message = "Hello";

alert(message); // Hello
```

- `declare multiple variables` in one line
  <br/>

```js
let user = "John",
  age = 25,
  message = "Hello";
```

## Variable naming

- name must contain `only letters`, `digits`, or the symbols `$ and _`

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

- `var`, `let`, and `const` are all used to declare variables,
- but they have some differences in terms of how they behave and the scope they have:

  1.**`var`**:

- Variables declared with var can be `re-declared` and `updated` anywhere in the program.

```js
function example() {
  var x = 10;
  if (true) {
    var x = 20; // this will overwrite the previous declaration of x
    console.log(x); // output: 20
  }
  console.log(x); // output: 20
}
```

- Varibles declared with var are `hoisted`. `Hoisting` is moving declarations to the top of the current scope.

```js
x = 5; //intilize x (assign value to x)
console.log(x); //output: 5
var x; //declaring x with var

//the previous code is similar to:
var y; // declare y with var
y = 5; // intilize y (assign value to y)
console.log(y); //output: 5
```

- var is a `function-scoped`, variables declared with var inside a function can be used anywhere witin a function.

```js
function sayHello() {
  a = "hello";
  console.log(a);
  var a;
}

//'a' is hoisted to the "top of the function" and become "local variable"
sayHello(); //output: 'hello'

console.log(a); //ERROR: a is not defined cause
//'a' is only accessible inside the function and doesn't become a global variable cause it is declared with var
```

- Redeclaring a varible with var in a block scope will change the value too in the outer scope. A block is any code surrounded by curly braces `{ }`.

```js
var c = 5;
console.log(c); //output: 5
{
  var c = 10;
  console.log(c); //output: 10
}
console.log(c); //output: 10
```

- When a variable declared with var in a loop, the value of that variable is changed.

```js
for (var y = 0; y < 3; y++) {
  //processing some data
}
console.log(y); //output: 3
```

#

2.**`let`**:

- Variables declared with let `can be updated` but `not re-declared`

```js
function example() {
  let x = 10;
  if (true) {
    let x = 20; // this will create a new variable x that only exists inside the block
    console.log(x); // output: 20
  }
  console.log(x); // output: 10
}
```

- Varibles declared with let are `not hoisted`. In other words cannot be used untill they are declared.

```js
x = 5; //intilize x (assign value to x)
console.log(x); //ERROR: Cannot access 'x' before initialization
let x; //declaring x with let
```

- let is `block-scoped`, which means that if you declare a variable with let inside a block, it's only accessible within that block.

```js
let c = 5;
console.log(c); //output: 5
{
  let c = 10;
  console.log(c); //output: 10
}
console.log(c); //output: 5
```

- When a variable declared with let in a loop, the value of that variable doesn't change cause let is blocked scope.

```js
let y = 100;
for (let y = 0; y < 3; y++) {
  //processing some data
}
console.log(y); //output: 100
```

#

3.**`const`**:

- Like let, const is also block-scoped.
- Variables declared with const cannot be re-declared or updated.

```js
const x = 100;
x = 200; //ERROR: Assignment to constant variable.
console.log(x);
```

|                  | var                                            | let                                            | const                                               |
| ---------------- | ---------------------------------------------- | ---------------------------------------------- | --------------------------------------------------- |
| `Redeclaration`  | YES                                            | NO                                             | NO                                                  |
| `Reassignment`   | YES                                            | YES                                            | NO                                                  |
| `Initialization` | NO<br/>var name;<br/>name = 'Shubham'; //valid | NO<br/>let name;<br/>name = 'Shubham'; //valid | YES<br/>const PI;<br/>PI = 3.14159265359; //invalid |
| `Scope`          | Functional Scope                               | Block Scope                                    | Block Scope                                         |
| `Hoisting`       | Yes (but initialized as undefined)             | Yes (with Temporal Dead Zone)                  | Yes (with Temporal Dead Zone)                       |

# scope

- A variable can be declared at `different scope`
- determines the `accessibility of variables`
- there are 4 kinds of scope in Javascript - `Block Scope`, `Global Scope`, `Function Scope`, `Module Scope`

- Anything declared `without let, var or const` is scoped at `global level`

```js
// Global Scope
let cart = []; // Available globally throughout the program

function addToCart(item) {
  // Function Scope
  let itemDetails = `Added ${item} to the cart`; // Only accessible inside this function
  console.log(itemDetails);

  cart.push(item); // cart is global, so we can modify it here

  // Nested block scope
  if (cart.length > 0) {
    let cartStatus = "Cart has items"; // Block-scoped variable
    console.log(cartStatus); // Accessible inside the block
  }

  // console.log(cartStatus); // Uncaught ReferenceError: cartStatus is not defined
}

addToCart("Phone");
console.log(cart); // Accessible because 'cart' is global
// console.log(itemDetails); // Uncaught ReferenceError: itemDetails is not defined
```

## Module scope

- In modern javascript, a `file can be considered as module`
- defined variable can only be `accessed in that particular module`

```js
<script src="index.js" type="module"></script>;
export { someVar, someFunc };
import { someVar } from "./app.js";
```

## Shadowing

### Variable Shadowing

```js
function func() {
  let a = "John";

  if (true) {
    let a = "Wick"; // New value assigned => Variable Shadowing
    console.log(a); // Wick
  }

  console.log(a); // John
}
func();
```

### Illegal Shadowing

- if we try to shadow `let variable by var variable`, it is known as Illegal Shadowing

```js
function func() {
  var a = "Rohit";
  let b = "Sharma";

  if (true) {
    let a = "Virat"; // Legal Shadowing
    var b = "Kohli"; // Illegal Shadowing
    console.log(a); // It will print 'Virat'
    console.log(b); // It will print error
  }
}
func();
```
