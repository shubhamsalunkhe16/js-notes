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

- Ignore elements using commas

```js
// second element is not needed
let [firstName, , title] = ["Julius", "Caesar", "Consul"];

alert(title); // Consul
```

- Works with any iterable on the right-side

```js
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);
```

- Swap variables trick

```js
let guest = "Jane";
let admin = "Pete";

// Let's swap the values: make guest=Pete, admin=Jane
[guest, admin] = [admin, guest];

alert(`${guest} ${admin}`); // Pete Jane (successfully swapped!)
```

- The rest ‘…’

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

- Default values

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

- The order does not matter.

```js
// changed the order in let {...}
let { width, title } = { title: "Menu", width: 100 };
```

- to assign a property to a variable with another name

```js
// { sourceProperty: targetVariable }
let { width: w, title } = { width: 100, title: "Menu" };

// width -> w
// title -> title

alert(title); // Menu
alert(w); // 100
```

- default values

```js
let options = {
  title: "Menu",
};

let { width = 100, height, title } = options;

alert(title); // Menu
alert(width); // 100
alert(height); // undefined
```

- can combine both the colon and equality

```js
let { width: w = 100, height: h = 200, title } = options;
```

- The rest pattern “…”

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

- Nested destructuring

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
