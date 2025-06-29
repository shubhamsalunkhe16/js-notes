# Hoisting

- hoisting is a behavior where `variable and function declarations` are moved ("hoisted") to the `top of their containing scope` during the `compilation phase`, before the code is executed.
- `Functions` and `variables` are stored in `memory` for an `execution context` before we execute our code. This is called `hoisting`.

## Hoisting Behavior:

1. Variables declared with `var are hoisted` but `initialized with undefined`.
2. Variables declared with `let and const are hoisted` but `not initialized` (they exist in the "temporal dead zone" until their declaration is encountered).
3. Function declarations are `hoisted along with their definitions`, meaning you can call the function before the actual declaration.

```js
console.log(orderDetails); // Output: undefined (because of hoisting)

// console.log(paymentMethod); // Error: Cannot access 'paymentMethod' before initialization
// TDZ prevents access until the declaration is encountered.

// processOrder(); // This will work fine because of function hoisting

var orderDetails = "Pizza, 2 sodas";
let paymentMethod = "Credit Card";

function processOrder() {
  console.log("Processing order for:", orderDetails);
}

processOrder(); // Works fine because function declarations are hoisted
```

![Hoisting](./images/hoisting/hoisting1.gif)
![Hoisting](./images/hoisting/hoisting2.gif)
![Hoisting](./images/hoisting/hoisting3.gif)
![Hoisting](./images/hoisting/hoisting4.gif)
![Hoisting](./images/hoisting/hoisting5.gif)
![Hoisting](./images/hoisting/hoisting6.gif)
![Hoisting](./images/hoisting/hoisting7.gif)
