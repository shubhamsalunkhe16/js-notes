## Prototypes and Inheritance

### What is a Prototype?

- **Prototype** is a mechanism in JavaScript used to enable inheritance. Every object in JavaScript has an internal property called `[[Prototype]]`, which is accessed through `__proto__` or `Object.getPrototypeOf()`.

### Prototype Chain

- Objects in JavaScript inherit properties and methods from their prototype. This forms a prototype chain.
- If a property is not found in the object, JavaScript looks for it in the prototype chain until it finds the property or reaches `null`.

### Prototype Inheritance Example

```javascript
const animal = {
  eat() {
    console.log("Animal eats");
  },
};

const dog = Object.create(animal); // dog inherits from animal
dog.bark = function () {
  console.log("Dog barks");
};

dog.eat(); // Animal eats
dog.bark(); // Dog barks
```

### Constructor Functions and Prototypes

- Constructor functions are used to create new objects and can be used to define methods on their prototypes.

```javascript
function Animal(name) {
  this.name = name;
}

Animal.prototype.sayHello = function () {
  console.log("Hello, " + this.name);
};

const dog = new Animal("Buddy");
dog.sayHello(); // Hello, Buddy
```

### ES6 Classes and Prototypes

- Classes in JavaScript are syntactic sugar over prototypes. They work the same way but are cleaner.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log("Hello, " + this.name);
  }
}

const dog = new Animal("Buddy");
dog.sayHello(); // Hello, Buddy
```

---

## Generators and Advanced Iteration

### What is a Generator?

- A generator is a special type of function that can pause its execution and resume later, returning multiple values as needed.
- Created using the `function*` syntax, a generator function returns a generator object.

### Generator Syntax

```javascript
function* countUpTo(max) {
  let count = 0;
  while (count <= max) {
    yield count;
    count++;
  }
}

const counter = countUpTo(5);
console.log(counter.next().value); // 0
console.log(counter.next().value); // 1
```

### `yield` Keyword

- The `yield` keyword pauses the execution of the generator function, returning a value. The function execution can be resumed by calling `next()` on the generator object.

### Using Generators for Iteration

- **Iterators**: Generators are iterators that can be used to produce values one at a time.

```javascript
function* colors() {
  yield "red";
  yield "green";
  yield "blue";
}

for (let color of colors()) {
  console.log(color); // red, green, blue
}
```

### Advanced Iteration with Generators

- Generators are useful for managing complex iteration logic, such as iterating over large datasets or infinite sequences.
- You can create an infinite sequence of numbers:

```javascript
function* infiniteNumbers() {
  let count = 0;
  while (true) {
    yield count++;
  }
}

const gen = infiniteNumbers();
console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
```

### The `return` Statement in Generators

- The `return` statement is used to terminate the generator. It also provides a final value.

```javascript
function* example() {
  yield 1;
  yield 2;
  return 3;
}

const gen = example();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

### Using `for...of` with Generators

- You can loop over a generator using the `for...of` loop to get all the yielded values until the generator is done.

```javascript
function* numbers() {
  yield 1;
  yield 2;
  yield 3;
}

for (let num of numbers()) {
  console.log(num); // 1, 2, 3
}
```

### Asynchronous Generators

- Asynchronous generators allow you to pause and resume execution asynchronously, typically used for handling streams or async data.

```javascript
async function* fetchData() {
  const data = await fetch("url");
  yield data;
}

for await (let data of fetchData()) {
  console.log(data);
}
```
