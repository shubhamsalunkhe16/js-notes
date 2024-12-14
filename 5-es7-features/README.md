# Destructuring

## Array destructuring

```js
// we have an array with the name and surname
let arr = ["John", "Smith"];

// destructuring assignment
// sets firstName = arr[0]
// and surname = arr[1]
let [firstName, surname] = arr;

alert(firstName); // John
alert(surname); // Smith
```

- `Ignore elements` using commas

```js
// second element is not needed
let [firstName, , title] = ["Julius", "Caesar", "Consul"];

alert(title); // Consul
```

- Works with any `iterable` on the `right-side`

```js
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);
```

- `Swap` variables trick

```js
let guest = "Jane";
let admin = "Pete";

// Let's swap the values: make guest=Pete, admin=Jane
[guest, admin] = [admin, guest];

alert(`${guest} ${admin}`); // Pete Jane (successfully swapped!)
```

- The rest `…`

```js
let [name1, name2, ...rest] = [
  "Julius",
  "Caesar",
  "Consul",
  "of the Roman Republic",
];

// rest is array of items, starting from the 3rd one
alert(rest); // ["Consul","of the Roman Republic"]
alert(rest[0]); // Consul
alert(rest[1]); // of the Roman Republic
alert(rest.length); // 2
```

- `Default values`

```js
// default values
let [name = "Guest", surname = "Anonymous", age] = ["Julius"];

alert(name); // Julius (from array)
alert(surname); // Anonymous (default used)
alert(age); // undefined
```

## Object destructuring

```js
let options = {
  title: "Menu",
  width: 100,
};

let { title, width } = options;

alert(title); // Menu
alert(width); // 100
```

- `order does not matter`.

```js
// changed the order in let {...}
let { width, title } = { title: "Menu", width: 100 };
```

- `rename variables`

```js
// { sourceProperty: targetVariable }
let { width: w, title } = { width: 100, title: "Menu" };

// width -> w
// title -> title

alert(title); // Menu
alert(w); // 100
```

- `default values`

```js
let options = {
  title: "Menu",
};

let { width = 100, height, title } = options;

alert(title); // Menu
alert(width); // 100
alert(height); // undefined
```

- can `combine` both the `colon and equality`

```js
let { width: w = 100, height: h = 200, title } = options;
```

- The rest pattern `…`

```js
let options = {
  title: "Menu",
  height: 200,
  width: 100,
};

// title = property named title
// rest = object with the rest of properties
let { title, ...rest } = options;

// now title="Menu", rest={height: 200, width: 100}
alert(rest.height); // 200
alert(rest.width); // 100
```

- `Nested destructuring`

```js
let options = {
  size: {
    width: 100,
    height: 200,
  },
  items: ["Cake", "Donut"],
  extra: true,
};

// destructuring assignment split in multiple lines for clarity
let {
  size: {
    // put size here
    width,
    height,
  },
  items: [item1, item2], // assign items here
  title = "Menu", // not present in the object (default value is used)
} = options;

alert(title); // Menu
alert(width); // 100
alert(height); // 200
alert(item1); // Cake
alert(item2); // Donut
```

# Modules

- A module is a `file`.
- To make `import/export` work, browsers need `<script type="module">`.

```js
<!doctype html>
<script type="module">
  import {sayHi} from './say.js';

  document.body.innerHTML = sayHi('John');
</script>
```

- Modules have several differences:
  - `Deferred` by default.
  - `Async` works on inline scripts.
  - `Duplicate external scripts are ignored`.
- Modules have their own, `local top-level scope` and `interchange functionality via import/export`.

```html
<script type="module">
  // The variable is only visible in this module script
  let user = "John";
</script>

<script type="module">
  alert(user); // Error: user is not defined
</script>
```

- Modules always `use strict`.
- Module code is `executed only once`. Exports are `created once` and `shared between importers`.

```js
// 📁 alert.js
alert("Module is evaluated!");

// Import the same module from different files

// 📁 1.js
import `./alert.js`; // Module is evaluated!

// 📁 2.js
import `./alert.js`; // (shows nothing)
```

## Export

### Export before declarations

```js
// export an array
export let months = [
  "Jan",
  "Feb",
  "Mar",
  "Apr",
  "Aug",
  "Sep",
  "Oct",
  "Nov",
  "Dec",
];

// export a constant
export const MODULES_BECAME_STANDARD_YEAR = 2015;

// export a class
export class User {
  constructor(name) {
    this.name = name;
  }
}
```

### Export apart from declarations

```js
// 📁 say.js
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

export { sayHi, sayBye }; // a list of exported variables
```

### Export “as”

```js
export { sayHi as hi, sayBye as bye };
```

### Export default

- `one thing per module` can export default

```js
export default class User {
  // just add "default"
  constructor(name) {
    this.name = name;
  }
}

// 📁 main.js
import User from "./user.js"; // not {User}, just User
```

- A module has either `named exports or the default one`

```js
export default class { // no class name
  constructor() { ... }
}

export default function(user) { // no function name
  alert(`Hello, ${user}!`);
}

// export a single value, without making a variable
export default ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

// Without default, such an export would give an error:
export class { // Error! (non-default export needs a name)
  constructor() {}
}
```

- The `default` name

```js
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

// same as if we added "export default" before the function
export { sayHi as default, sayBye };
```

## Import

```js
// 📁 main.js
import { sayHi, sayBye } from "./say.js";

sayHi("John"); // Hello, John!
sayBye("John"); // Bye, John!

// OR

// 📁 main.js
import * as say from "./say.js";

say.sayHi("John");
say.sayBye("John");
```

### Import `as`

```js
// 📁 main.js
import { sayHi as hi, sayBye as bye } from "./say.js";

hi("John"); // Hello, John!
bye("John"); // Bye, John!
```

- import the default export along with a named one:

```js
// 📁 main.js
import { default as User, sayHi } from "./user.js";
// OR
import User, { sayHi } from "./user.js";
new User("John");
```

- if importing everything `*` as an object, then the `default property is exactly the default export`

```js
// 📁 main.js
import * as user from "./user.js";

let User = user.default; // the default export
new User("John");
```

- `Named exports` force us to use `exactly the right name` to import

```js
import { User } from "./user.js";
// import {MyUser} won't work, the name must be {User}
```

- While for a `default export`, we `always choose the name when importing`:

```js
import User from "./user.js"; // works
import MyUser from "./user.js"; // works too
// could be import Anything... and it'll still work
```

| Named export            | Default export                  |
| ----------------------- | ------------------------------- |
| export class User {...} | export default class User {...} |
| import {User} from ...  | import User from ...            |

## Dynamic imports

- we can’t` dynamically generate` any parameters of import

```js
import ... from getModuleName(); // Error, only from "string" is allowed
```

- we can’t import `conditionally` or at `run-time`

```js
if(...) {
  import ...; // Error, not allowed!
}

{
  import ...; // Error, we can't put import in any block
}
```

- But how can we import a module dynamically, on-demand?

### The import() expression

- The `import(module)` expression loads the `module` and returns a `promise` that resolves into a `module object` that contains all its `exports`.
- It can be `called` from `any place in the code`.

```js
let modulePath = prompt("Which module to load?");

import(modulePath)
  .then((obj) => `<module object>`)
  .catch((err) => `<loading error, e.g. if no such module>`);

// OR

let module = await import(modulePath);
```

**Example**

```js
// 📁 say.js
export function hi() {
  alert(`Hello`);
}

export function bye() {
  alert(`Bye`);
}

let { hi, bye } = await import("./say.js");

hi();
bye();
```

- Or, if say.js has the default export:

```js
// 📁 say.js
export default function () {
  alert("Module loaded (export default)!");
}

let obj = await import("./say.js");
let say = obj.default;
// or, in one line: let {default: say} = await import('./say.js');

say();
```

# Rest parameters

- used to create functions that accept `any number of arguments`.

```js
function sumAll(...args) {
  // args is the name for the array
  let sum = 0;

  for (let arg of args) sum += arg;

  return sum;
}

alert(sumAll(1)); // 1
alert(sumAll(1, 2)); // 3
alert(sumAll(1, 2, 3)); // 6

/////*******************************************/////

function showName(firstName, lastName, ...titles) {
  alert(firstName + " " + lastName); // Julius Caesar

  // the rest go into titles array
  // i.e. titles = ["Consul", "Imperator"]
  alert(titles[0]); // Consul
  alert(titles[1]); // Imperator
  alert(titles.length); // 2
}

showName("Julius", "Caesar", "Consul", "Imperator");
```

- `must` be `at the end`

```js
function f(arg1, ...rest, arg2) { // arg2 after ...rest ?!
  // error
}
```

# Spread syntax

- used to pass an `array` to functions that normally require a `list of many arguments`

```js
alert(Math.max(3, 5, 1)); // 5

let arr = [3, 5, 1];

alert(Math.max(arr)); // NaN
alert(Math.max(...arr)); // 5
```

- can pass `multiple iterable`s this way

```js
let arr1 = [1, -2, 3, 4];
let arr2 = [8, 3, -8, 1];

alert(Math.max(1, ...arr1, 2, ...arr2, 25)); // 25
```

- `Copy` an array/object

```js
let arr = [1, 2, 3];

let arrCopy = [...arr]; // spread the array into a list of parameters
// then put the result into a new array

// do the arrays have the same contents?
alert(JSON.stringify(arr) === JSON.stringify(arrCopy)); // true

// are the arrays equal?
alert(arr === arrCopy); // false (not same reference)

// modifying our initial array does not modify the copy:
arr.push(4);
alert(arr); // 1, 2, 3, 4
alert(arrCopy); // 1, 2, 3

/////*************************************************/////

let obj = { a: 1, b: 2, c: 3 };

let objCopy = { ...obj }; // spread the object into a list of parameters
// then return the result in a new object

// do the objects have the same contents?
alert(JSON.stringify(obj) === JSON.stringify(objCopy)); // true

// are the objects equal?
alert(obj === objCopy); // false (not same reference)

// modifying our initial object does not modify the copy:
obj.d = 4;
alert(JSON.stringify(obj)); // {"a":1,"b":2,"c":3,"d":4}
alert(JSON.stringify(objCopy)); // {"a":1,"b":2,"c":3}
```

### There’s an easy way to distinguish between them:

- When ... is at the `end of function parameters`, it’s “rest parameters” and gathers the rest of the `list of arguments` into an `array`.
- When ... occurs `in a function call or alike`, it’s called a “spread syntax” and `expands` an array into a `list`.
