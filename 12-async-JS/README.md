# Promise

## callbacks intro

- we often have to deal with `tasks that rely on other tasks`

```js
function loadScript(src, callback) {
  let script = document.createElement("script");
  script.src = src;
  script.onload = () => callback(script);
  document.head.append(script);
}

loadScript(
  "https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js",
  (script) => {
    alert(`Cool, the script ${script.src} is loaded`);
    alert(_); // _ is a function declared in the loaded script
  }
);
```

- That’s the idea: the second argument is a `function` (usually anonymous) that `runs when the action is completed`

### Callback in callback

- another eg. we want to `get an image`, `compress it`, `apply a filter`, and `save it` 📸
- In the end, we'll end up with something like this:

![callback hell](./images/promises/callback-hell.png)

- Although it's... fine, it's `not great`
- because it has `many nested callback functions` called `callback hell`
- that make the code quite `difficult to read`
- `promises can help` us in situations like these

## Promise Syntax

- represents an operation that `hasn't completed yet`, but is expected to in the future.
- It's a placeholder for the `result of an asynchronous operation`, providing a way to handle `success or failure` after the task is `finished`

A **real-life example** of a promise would be something like **ordering a pizza**.

- There are three possible outcomes:

1. The pizza is successfully delivered (fulfilled).
2. There is a problem with the order, and it cannot be delivered (rejected).
3. You're still waiting for the pizza to be delivered (pending).

### Pizza Order Example: Promise in JavaScript

Let’s model this using JavaScript promises.

```javascript
// Function to simulate ordering a pizza
function orderPizza(pizzaType) {
  return new Promise((resolve, reject) => {
    console.log(`Order placed for a ${pizzaType} pizza.`);

    setTimeout(() => {
      const isSuccessful = Math.random() > 0.2; // 80% chance the order will succeed

      if (isSuccessful) {
        resolve(`${pizzaType} pizza delivered! Enjoy!`);
      } else {
        reject(`Sorry, we couldn't deliver your ${pizzaType} pizza.`);
      }
    }, 3000); // Simulate a 3 second pizza delivery time
  });
}

// Placing the order
orderPizza("Margherita")
  .then((message) => {
    console.log(message); // Success handler: Pizza delivered!
  })
  .catch((error) => {
    console.log(error); // Error handler: Pizza not delivered
  })
  .finally(() => {
    console.log("Thank you for ordering with us."); // Final statement
  });
```

## `.then` chain

- `.then` handlers can `solve callback hell problem`
- result of `.then` itself is a `promise value`
- can chain many as we want
- the result of the `previous then callback` will be `passed` as an `argument to the next then callback`

![then-chain](./images/promises/then-chain.png)

- for image example,

![then-chain](./images/promises/promise-image-example-then-chain.png)

## Promise API

- There are `6 static methods` in the Promise class

### 1. `Promise.all`

- This method takes an `array of promises` and `returns a single promise` that `resolves when all the promises` in the array have resolved, or `rejects if any promise fails`

#### Real-Life Example: Ordering Multiple Pizzas

- Imagine you and your friends order several pizzas at the same time. You want to `start the party only after all pizzas are delivered`.

```js
// Simulating pizza orders with promises
const orderPizza1 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 1 delivered"), 3000)
);
const orderPizza2 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 2 delivered"), 2000)
);
const orderPizza3 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 3 delivered"), 1000)
);

// Waiting for all pizzas to be delivered
Promise.all([orderPizza1, orderPizza2, orderPizza3])
  .then((pizzas) => {
    console.log("All pizzas delivered:", pizzas);
    // Output: All pizzas delivered: ['Pizza 1 delivered', 'Pizza 2 delivered', 'Pizza 3 delivered']
  })
  .catch((error) => {
    console.log("One of the pizza orders failed:", error);
  });
```

### 2. `Promise.allSettled`

- This method `returns a promise that resolves` when `all promises have either resolved or rejected`, with an array of objects that describes the `outcome of each promise`.

#### Real-Life Example: Status of Multiple Pizza Orders

- You order several pizzas and you want to know the status of all of them, even if some deliveries fail

```js
const pizza1 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 1 delivered"), 3000)
);
const pizza2 = new Promise((_, reject) =>
  setTimeout(() => reject("Pizza 2 failed to deliver"), 2000)
);
const pizza3 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 3 delivered"), 1000)
);

// Checking the status of all pizza deliveries
Promise.allSettled([pizza1, pizza2, pizza3]).then((results) => {
  console.log("All pizza statuses:", results);
  // Output:
  // [
  //   { status: 'fulfilled', value: 'Pizza 1 delivered' },
  //   { status: 'rejected', reason: 'Pizza 2 failed to deliver' },
  //   { status: 'fulfilled', value: 'Pizza 3 delivered' }
  // ]
});
```

### 3. `Promise.race`

- This method `returns a promise that resolves or rejects as soon as one of the promises in the array resolves or rejects`. The result of the `first completed promise` is returned.

#### Real-Life Example: Pizza Delivery Race

- You and your friends are racing to see which pizza is delivered first.

```js
const pizza1 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 1 delivered"), 3000)
);
const pizza2 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 2 delivered"), 2000)
);
const pizza3 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 3 delivered"), 1000)
);

// Racing to see which pizza is delivered first
Promise.race([pizza1, pizza2, pizza3])
  .then((winner) => {
    console.log("The first pizza delivered is:", winner);
    // Output: The first pizza delivered is: Pizza 3 delivered
  })
  .catch((error) => {
    console.log("One of the pizza orders failed:", error);
  });
```

### 4. `Promise.any`

- This method returns a `single promise that resolves as soon as any of the promises resolves`. If all promises reject, it returns a rejection.

#### Real-Life Example: First Pizza that Successfully Delivers

- You order multiple pizzas, and you just want to know as soon as any pizza arrives, ignoring any failed deliveries.

```js
const pizza1 = new Promise((_, reject) =>
  setTimeout(() => reject("Pizza 1 failed to deliver"), 3000)
);
const pizza2 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 2 delivered"), 2000)
);
const pizza3 = new Promise((resolve) =>
  setTimeout(() => resolve("Pizza 3 delivered"), 1000)
);

// Getting the first successfully delivered pizza
Promise.any([pizza1, pizza2, pizza3])
  .then((firstDelivered) => {
    console.log("First pizza delivered is:", firstDelivered);
    // Output: First pizza delivered is: Pizza 3 delivered
  })
  .catch((error) => {
    console.log("No pizza was delivered:", error);
  });
```

# Async/Await

- introduced in `ES7`
- `async` and `await` keywords, we can create `async` functions which implicitly return a promise

![async-await](./images/async-await.gif)
