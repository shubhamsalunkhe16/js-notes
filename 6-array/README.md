# Arrays

- `indexed collection of different data types` which are `ordered` and `mutable`(modifiable)
- can store `multiple values`
- index of an array starts from `zero`
- allows storing `duplicate elements` and `different data types`

### Array can have items of `different data types`

```js
const arr = [
  "Asabeneh",
  250,
  true,
  { country: "Finland", city: "Helsinki" },
  { skills: ["HTML", "CSS", "JS", "React", "Python"] },
]; // arr containing different data types
console.log(arr);
```

#### Creating an array using `split`

```js
let companiesString = "Facebook, Google, Microsoft, Apple, IBM, Oracle, Amazon";
const companies = companiesString.split(",");

console.log(companies); // ["Facebook", " Google", " Microsoft", " Apple", " IBM", " Oracle", " Amazon"]
```

#### Accessing array items using index `[index]`

```js
const fruits = ["banana", "orange", "mango", "lemon"];
let firstFruit = fruits[0]; // we are accessing the first item using its index
console.log(firstFruit); // banana

let lastIndex = fruits.length - 1;
lastFruit = fruits[lastIndex];

console.log(lastFruit); // lemon
```

#### Modifying array element

- An array is mutable(modifiable).

```js
const numbers = [1, 2, 3, 4, 5];
numbers[0] = 10; // changing 1 at index 0 to 10
numbers[1] = 20; // changing  2 at index 1 to 20

console.log(numbers); // [10, 20, 3, 4, 5]
```

#### Methods to manipulate array

- These are some of the available methods to deal with arrays:`Array`,`length`,`concat`,`indexOf`,`slice`,`splice`,`join`,`toString`,`includes`,`lastIndexOf`,`isArray`,`fill`,`push`,`pop`,`shift`,`unshift`

##### Array Constructor : `Array()`

```js
const arr = Array(); // creates an an empty array
console.log(arr);

const eightEmptyValues = Array(8); // it creates eight empty values
console.log(eightEmptyValues); // [empty x 8]
```

##### Creating static values with `fill`

- `fill all the array elements` with a static value

```js
const arr = Array(); // creates an an empty array
console.log(arr);

const eightXvalues = Array(8).fill("X"); // it creates eight element values filled with 'X'
console.log(eightXvalues); // ['X', 'X','X','X','X','X','X','X']
```

##### Concatenating array using `concat`

- To `concatenate two arrays`

```js
const firstList = [1, 2, 3];
const secondList = [4, 5, 6];
const thirdList = firstList.concat(secondList);

console.log(thirdList); // [1, 2, 3, 4, 5, 6]
```

##### Getting array `length`

- To know the `size` of the array

```js
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.length); // -> 5 is the size of the array
```

##### Getting index of an element in an array `indexOf`/`lastIndexOf`

- To `check if an item exist` in an array
- If it exists it returns the index else it returns `-1`

```js
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.indexOf(5)); // -> 4
console.log(numbers.indexOf(0)); // -> -1
console.log(numbers.lastIndexOf(4)); // -> 3
```

##### Getting last index of an element in array

- It gives the `position of the last item` in the array
- If it exist, it returns the index else it returns `-1`

```js
const numbers = [1, 2, 3, 4, 5, 3, 1, 2];

console.log(numbers.lastIndexOf(2)); // 7
console.log(numbers.lastIndexOf(0)); // -1
```

##### includes method in array :

- To check if an `item exist in an array`
- If it exist it returns the `true` else it returns `false`

```js
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.includes(5)); // true
console.log(numbers.includes(0)); // false
```

##### Checking array

- To check if the `data type is an array`

```js
const numbers = [1, 2, 3, 4, 5];
console.log(Array.isArray(numbers)); // true

const number = 100;
console.log(Array.isArray(number)); // false
```

##### Converting array to string : `toString`

- converts `array to string`

```js
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.toString()); // 1,2,3,4,5

const names = ["Asabeneh", "Mathias", "Elias", "Brook"];
console.log(names.toString()); // Asabeneh,Mathias,Elias,Brook
```

##### `Join` array elements

- It is used to `join the elements` of the array
- the `argument` we passed in the join method will be `joined in the array` and return as a `string`

```js
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.join()); // 1,2,3,4,5

const names = ["Asabeneh", "Mathias", "Elias", "Brook"];

console.log(names.join()); // Asabeneh,Mathias,Elias,Brook
console.log(names.join(" ")); //Asabeneh Mathias Elias Brook
console.log(names.join(", ")); //Asabeneh, Mathias, Elias, Brook
console.log(names.join(" # ")); //Asabeneh # Mathias # Elias # Brook
```

##### `Slice` array elements

- To `cut out a multiple items in range`
- It takes `two parameters` : `starting` and `ending` position.
- It `doesn't include the ending position`.

```js
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.slice()); // -> it copies all  item
console.log(numbers.slice(0)); // -> it copies all  item
console.log(numbers.slice(0, numbers.length)); // it copies all  item
console.log(numbers.slice(1, 4)); // -> [2,3,4] // it doesn't include the ending position
```

##### `Splice` method in array

- takes `three parameters`:`Starting position`, `number of times to be removed` and `items to be added`.

```js
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.splice()); // -> remove all items
```

```js
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.splice(0, 1)); // remove the first item
```

```js
const numbers = [1, 2, 3, 4, 5, 6];
console.log(numbers.splice(3, 3, 7, 8, 9)); // -> [1, 2, 3, 7, 8, 9] //it removes three item and replace three items
```

##### Adding item to an array using `push`

- adding item in the end

```js
// syntax
const arr = ["item1", "item2", "item3"];
arr.push("new item");

console.log(arr);
// ['item1', 'item2','item3','new item']
```

##### Removing the end element using `pop`

- Removing item in the end

```js
const numbers = [1, 2, 3, 4, 5];
numbers.pop(); // -> remove one item from the end

console.log(numbers); // -> [1,2,3,4]
```

##### Removing an element from the beginning

- Removing first element the array

```js
const numbers = [1, 2, 3, 4, 5];
numbers.shift(); // -> remove one item from the beginning

console.log(numbers); // -> [2,3,4,5]
```

##### Add an element from the beginning

- Adding array element in the beginning of the array

```js
const numbers = [1, 2, 3, 4, 5];
numbers.unshift(0); // -> add one item from the beginning

console.log(numbers); // -> [0,1,2,3,4,5]
```

##### `Reverse` array order

```js
const numbers = [1, 2, 3, 4, 5];
numbers.reverse(); // -> reverse array order

console.log(numbers); // [5, 4, 3, 2, 1]
```

##### `Sort` elements in array

```js
const webTechs = [
  "HTML",
  "CSS",
  "JavaScript",
  "React",
  "Redux",
  "Node",
  "MongoDB",
];

webTechs.sort();
console.log(webTechs); // ["CSS", "HTML", "JavaScript", "MongoDB", "Node", "React", "Redux"]

webTechs.reverse(); // after sorting we can reverse it
console.log(webTechs); // ["Redux", "React", "Node", "MongoDB", "JavaScript", "HTML", "CSS"]
```

##### Sort Numeric Array

```js
let arr = [12, 25, 31, 23, 75, 81, 100];
console.log(arr.sort());
```

```sh
// code shows this output
Wrong Output   : [100, 12, 23, 25, 31, 75, 81]

// Correct Output
Correct Output : [12, 23, 25, 31, 75, 81, 100]
```

```js
let arr = [12, 25, 31, 23, 75, 81, 100];
console.log(arr.sort((a, b) => a - b));
// 12,23,25,31,75,81,100
```

```
Negative Value ( a < b) => a will be placed before b
zero value (a == b) => No Change
Positive Value (a > b ) => a will be placed after b
```

# Set

- `collection of unique values`.
- insertion `order` is preserved

### Its main methods are:

- `new Set([iterable])` – creates the set, and if an iterable object is provided (usually an array), copies values from it into the set.
- `set.add(value)` – adds a value, returns the set itself.
- `set.delete(value)` – removes the value, returns true if value existed at the moment of the call, otherwise false.
- `set.has(value)` – returns true if the value exists in the set, otherwise false.
- `set.clear()` – removes everything from the set.
- `set.size` – is the elements count.

```js
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// visits, some users come multiple times
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// set keeps only unique values
alert(set.size); // 3
```

### Iteration over Set

- either with `for..of` or using `forEach`

```js
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// the same with forEach:
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```
