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

- `ES6` introduced Promises
- A `promise` is a `placeholder for a value` that can either `resolve or reject` at some time in the `future`

```js
new Promise(() => {});
```

- it returns

```sh
Promise {<pending>}
[[Prototype]]: Promise
[[PromiseState]]: "pending"
[[PromiseResult]]: undefined
```

- A Promise is an `object` that contains a `status`, ([[PromiseStatus]]) and a `value` ([[PromiseValue]])

### The value of the PromiseStatus, `the state`, can be one of three values:

- ✅ `fulfilled`: The promise has been `resolved`. Everything `went fine`, no errors occurred within the promise 🥳

```js
new Promise((res, rej) => {
  res("yay!");
});
```

```sh
Promise {<fulfilled>}
[[Prototype]]: Promise
[[PromiseState]]: "fulfilled"
[[PromiseResult]]: "yay!"
```

- ❌ `rejected` : The promise has been `rejected`. Argh, something `went wrong`

```js
new Promise((res, rej) => {
  rej("oh no!");
});
```

```sh
Promise {<rejected>}
[[Prototype]]: Promise
[[PromiseState]]: "rejected"
[[PromiseResult]]: "oh no!"
```

- ⏳ `pending`: The promise has `neither resolved nor rejected` (yet), the promise is still `pending`

![resolve-reject-params](./images/promises/resolve-reject-params.png)

- lets see previous image example

![promise-image-example](./images/promises/promise-image-example.png)

### there are built-in methods to get a promise's value. To a promise, we can attach 3 methods

- `.then()` : Gets called after a promise `resolved`
- `.catch()` : Gets called after a promise `rejected`
- `.finally()` : `Always gets called`, whether the promise resolved or rejected

#### `IF RESOLVE`

![promise-image-example-resolve](./images/promises/promise-image-example-resolve.gif)

#### `IF REJECT`

![promise-image-example-reject](./images/promises/promise-image-example-reject.gif)

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

- used when we want `many promises to execute in parallel` and `wait until all of them are ready`

```js
let urls = [
  "https://api.github.com/users/iliakan",
  "https://api.github.com/users/remy",
  "https://api.github.com/users/jeresig",
];

// map every url to the promise of the fetch
let requests = urls.map((url) => fetch(url));

// Promise.all waits until all jobs are resolved
Promise.all(requests).then((responses) =>
  responses.forEach((response) => alert(`${response.url}: ${response.status}`))
);
```

#### **Scenarios**

- Scenario 1: `All passed-in Promises get fulfilled`
  ![Promise.all](./images/promises/methods/Promise.all-1.gif)
- Scenario 2: ⚡️ `One or more of the passed-in Promise(s) rejects`
  ![Promise.all](./images/promises/methods/Promise.all-2.gif)
  - In case of an `error`, other `promises are ignored`
  ```js
  Promise.all([
    new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
    new Promise((resolve, reject) =>
      setTimeout(() => reject(new Error("Whoops!")), 2000)
    ),
    new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000)),
  ]).catch(alert); // Error: Whoops!
  ```
- Scenario 3: ⚡️ `All passed-in Promises get rejected`
  ![Promise.all](./images/promises/methods/Promise.all-3.gif)
- Scenario 4: `Passing an Empty iterable`
  ![Promise.all](./images/promises/methods/Promise.all-4.gif)

### 2. `Promise.allSettled`

- `Promise.all` rejects as a whole if any promise rejects. when we need `all results successful` to proceed:
- `Promise.allSettled` just waits for `all promises to settle`, `regardless of the result`. The resulting array has:

  - {status:"fulfilled", value:result} for successful responses,
  - {status:"rejected", reason:error} for errors.

```js
let urls = [
  "https://api.github.com/users/iliakan",
  "https://api.github.com/users/remy",
  "https://no-such-url",
];

Promise.allSettled(urls.map((url) => fetch(url))).then((results) => {
  // (*)
  results.forEach((result, num) => {
    if (result.status == "fulfilled") {
      alert(`${urls[num]}: ${result.value.status}`);
    }
    if (result.status == "rejected") {
      alert(`${urls[num]}: ${result.reason}`);
    }
  });
});
```

**_output_**

```sh
[
  {status: 'fulfilled', value: ...response...},
  {status: 'fulfilled', value: ...response...},
  {status: 'rejected', reason: ...error object...}
]
```

#### **Scenarios**

Scenario 1: `All passed-in Promises get fulfilled`
![Promise.allSettled](./images/promises/methods/Promise.allSettled-1.gif)
Scenario 2: `One or more of the passed-in Promise(s) rejects`
![Promise.allSettled](./images/promises/methods/Promise.allSettled-2.gif)
Scenario 3: `All passed-in Promises get rejected`
![Promise.allSettled](./images/promises/methods/Promise.allSettled-3.gif)
Scenario 4: `Passing an Empty iterable`
![Promise.allSettled](./images/promises/methods/Promise.allSettled-4.gif)

### 3. `Promise.race`

- Similar to `Promise.all`, but waits only for the first `settled promise` and gets its result (or error).

```js
Promise.race([
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) =>
    setTimeout(() => reject(new Error("Whoops!")), 2000)
  ),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000)),
]).then(alert); // 1
```

- The first promise here was `fastest`, so it became the `result`
- After the first settled promise `wins the race`, all further `results/errors are ignored`.

#### **Scenarios**

Scenario 1: ⚡️ `All passed-in Promises get fulfilled`
![Promise.race](./images/promises/methods/Promise.race-1.gif)
Scenario 2: ⚡️ `One or more of the passed-in Promise(s) rejects`
![Promise.race](./images/promises/methods/Promise.race-2.gif)
Scenario 3: ⚡️ `All passed-in Promises get rejected`
![Promise.race](./images/promises/methods/Promise.race-3.gif)
Scenario 4: `Passing an Empty iterable`
![Promise.race](./images/promises/methods/Promise.race-4.gif)

### 4. `Promise.any`

- similar to promise.race, waits only for the first `fulfilled promise`
- If `all of the given promises are rejected`, then the returned promise is rejected with `AggregateError` – a special error object that stores all promise errors in its errors property.

```js
Promise.any([
  new Promise((resolve, reject) =>
    setTimeout(() => reject(new Error("Ouch!")), 1000)
  ),
  new Promise((resolve, reject) =>
    setTimeout(() => reject(new Error("Error!")), 2000)
  ),
]).catch((error) => {
  console.log(error.constructor.name); // AggregateError
  console.log(error.errors[0]); // Error: Ouch!
  console.log(error.errors[1]); // Error: Error!
});
```

#### **Scenarios**

Scenario 1: ⚡️ `All passed-in Promises get fulfilled`
![Promise.any](./images/promises/methods/Promise.any-1.gif)
Scenario 2: ⚡️ `One or more of the passed-in Promise(s) rejects`
![Promise.any](./images/promises/methods/Promise.any-2.gif)
Scenario 3: `All passed-in Promises get rejected`
![Promise.any](./images/promises/methods/Promise.any-3.gif)
Scenario 4: `Passing an Empty iterable`
![Promise.any](./images/promises/methods/Promise.any-4.gif)

### 5. `Promise.resolve`

- Promise.resolve(value) – makes a resolved promise with the given value.

![Promise.resolve](./images/promises/methods/Promise.resolve-1.gif)

### 6. `Promise.reject`

- Promise.reject(error) – makes a rejected promise with the given error.

![Promise.reject](./images/promises/methods/Promise.reject-1.gif)

# Event Loop

- JS is `single-threaded` : `only one` task can `run at a time`
- if a task which takes 30 seconds..During that task we’re waiting for 30 seconds before anything else can happen😬
- results a `slow`, `unresponsive website`
- Luckily, the `browser` gives us some features that the `JavaScript engine itself doesn’t provide`: a `WEB API`
- This includes the `DOM API`, `setTimeout`, `HTTP requests`, and so on...
- This can help us create some `async`, `non-blocking` behavior 🚀

![event-loop](./images/promises/event-loop/event-loop-1.gif)
![event-loop](./images/promises/event-loop/event-loop-2.gif)
![event-loop](./images/promises/event-loop/event-loop-3.gif)
![event-loop](./images/promises/event-loop/event-loop-4.gif)
![event-loop](./images/promises/event-loop/event-loop-5.gif)

- lets see one example

```js
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"), 500);
const baz = () => console.log("Third");

bar();
foo();
baz();
```

![event-loop](./images/promises/event-loop/event-loop-6.gif)

# Microtasks and (Macro)tasks

| (Macro)task  |      Microtask      |
| :----------- | :-----------------: |
| setTimeout   |  process.nextTick   |
| setInterval  |  Promise callback   |
| setImmediate | queueMicrotask neat |

### The event loop gives a different priority to the tasks:

1. All `functions` in that are currently in the call stack get `executed`. When they `returned a value`, they get `popped off the stack`. eg.`Task1`

2. `event loop` checks if `call stack is empty`. if empty, all queued up `microtasks` are `popped` onto the callstack `one by one`, and get `executed`. eg.`Task2`,`Task3`, `Task4`

3. `event loop` checks if both the `call stack and microtask queue are empty`.if empty, all queued up `macrotasks` are `popped` onto the callstack `one by one`, and get `executed`. eg.`Task5`,`Task6`

```
- Microtasks has higher priority than (Macro)tasks
- Microtasks will execute first
- Microtasks > (Macro)tasks
```

![task-queue](./images/promises/task-queue/micro-macro-2.gif)

- lets see with the example

![taskQueue](./images/promises/task-queue/micro-macro-3.gif)
![task-queue](./images/promises/task-queue/micro-macro-4.gif)
![task-queue](./images/promises/task-queue/micro-macro-5.gif)
![task-queue](./images/promises/task-queue/micro-macro-6.gif)
![task-queue](./images/promises/task-queue/micro-macro-7.gif)
![task-queue](./images/promises/task-queue/micro-macro-8.gif)

# Async/Await

- introduced in `ES7`
- `async` and `await` keywords, we can create `async` functions which implicitly return a promise

![async-await](./images/promises/async-await.gif)
