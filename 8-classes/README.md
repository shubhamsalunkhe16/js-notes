# Classes and OOP Concepts

## `Classes`

- A class is a `blueprint for creating objects.`
- It `encapsulates data` (properties) and `methods` (functions) that operate on the data.

### Syntax:

```javascript
class ClassName {
  constructor(parameters) {
    // Initialize properties
  }

  // Methods
  method1() {
    // Method logic
  }
}
```

### Example:

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const person1 = new Person("Alice", 25);
person1.greet(); // "Hello, my name is Alice"
```

---

## `Key Features of Classes`

### a. `Constructor Method`

- The `constructor` is a special method `used for initializing new objects.`

### b. `Methods`

- Methods define `behavior for the objects` created from the class.

### c. `Static Methods`

- Static methods `belong to the class itself` and are `not accessible from instances.`

```javascript
class MathUtils {
  static add(a, b) {
    return a + b;
  }
}

console.log(MathUtils.add(2, 3)); // 5
```

### d. `Getters and Setters`

Getters and setters allow controlled access to properties.

```javascript
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  get area() {
    return this.width * this.height;
  }

  set updateWidth(newWidth) {
    this.width = newWidth;
  }
}

const rect = new Rectangle(10, 20);
console.log(rect.area); // 200
rect.updateWidth = 15;
console.log(rect.area); // 300
```

---

## `Inheritance`

- Classes `can inherit properties and methods from other classes` using the `extends` keyword.

### Example:

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog("Rex");
dog.speak(); // "Rex barks."
```

---

## `Encapsulation`

- Encapsulation is the practice of `bundling data and methods within a class` and `restricting direct access to some components`.

### Example:

```javascript
class BankAccount {
  #balance = 0; // Private field (ES6+)

  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
    }
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount();
account.deposit(100);
console.log(account.getBalance()); // 100
```

---

## `Polymorphism`

- Polymorphism allows `methods in derived classes to override methods` in the base class.

### Example:

```javascript
class Shape {
  draw() {
    console.log("Drawing a shape");
  }
}

class Circle extends Shape {
  draw() {
    console.log("Drawing a circle");
  }
}

const shapes = [new Shape(), new Circle()];
shapes.forEach((shape) => shape.draw());
// Output:
// "Drawing a shape"
// "Drawing a circle"
```

---

## `Abstraction`

- Abstraction `hides implementation details` and shows only the necessary features of an object.

### Example:

- `JavaScript doesn’t have true abstract classes`, but we can simulate them using base classes and `throw` statements.

```javascript
class AbstractVehicle {
  startEngine() {
    throw new Error("This method must be implemented by a subclass");
  }
}

class Car extends AbstractVehicle {
  startEngine() {
    console.log("Car engine started");
  }
}

const myCar = new Car();
myCar.startEngine(); // "Car engine started"
```

---
