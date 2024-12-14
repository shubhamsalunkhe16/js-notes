# Events in JavaScript

---

## 1. `Event Flow in JavaScript`

The flow of events in the DOM is divided into three phases:

1. `Capturing Phase`:

   - The event starts from the root (`document`) and travels down to the target element.
   - This is also called the "capture phase."
   - Flow direction : `Parent → Child`

2. `Target Phase`:

   - The event reaches the target element (the element where the event occurred).

3. `Bubbling Phase`:
   - The event bubbles back up from the target element to the root.
   - Flow direction : `Child → Parent`

![Event Flow Diagram](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events/event_flow.svg)

By default, most events are registered in the bubbling phase, but developers can choose to handle events in the capturing phase.

---

## 2. `Event Bubbling`

Event bubbling means that an event propagates from the target element upwards through its ancestors in the DOM tree.

- Example:

  ```html
  <div id="parent">
    <button id="child">Click Me</button>
  </div>
  <script>
    document.getElementById("parent").addEventListener("click", () => {
      console.log("Parent clicked");
    });

    document.getElementById("child").addEventListener("click", () => {
      console.log("Child clicked");
    });
  </script>
  ```

  `Output when button is clicked:`

  - "Child clicked"
  - "Parent clicked" (bubbles up to the parent)

- To stop event bubbling, use `event.stopPropagation()`:
  ```javascript
  document.getElementById("child").addEventListener("click", (event) => {
    event.stopPropagation();
    console.log("Bubbling stopped at child.");
  });
  ```

---

## 3. `Event Capturing`

Event capturing, also known as the "trickle-down phase," means that an event is first captured by the root element and then propagates to the target element.

- To register an event listener in the capturing phase, set the third parameter of `addEventListener` to `true`:

  ```javascript
  document.getElementById("parent").addEventListener(
    "click",
    () => {
      console.log("Parent clicked (capturing phase)");
    },
    true
  );
  ```

- Example:

  ```html
  <div id="parent">
    <button id="child">Click Me</button>
  </div>
  <script>
    document.getElementById("parent").addEventListener(
      "click",
      () => {
        console.log("Parent clicked (capturing phase)");
      },
      true
    );

    document.getElementById("child").addEventListener("click", () => {
      console.log("Child clicked");
    });
  </script>
  ```

  `Output when button is clicked:`

  - "Parent clicked (capturing phase)"
  - "Child clicked"

---

## 4. `Event Delegation`

Event delegation is a technique where a `single event listener is attached to a parent element to handle events for its child elements.`

- `Why Use Event Delegation?`

  - `Reduces the number of event listeners` in your application, improving performance.
  - Handles `dynamically added child elements.`

- Example:
  ```html
  <ul id="list">
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
  <script>
    document.getElementById("list").addEventListener("click", (event) => {
      if (event.target.tagName === "LI") {
        console.log("List item clicked:", event.target.textContent);
      }
    });
  </script>
  ```
  `Output when an `<li>` is clicked:`
  - "List item clicked: Item 1" or "Item 2"

---

## 5. `Prevent Default Behavior`

To stop the default action associated with an event (e.g., link navigation, form submission), use `event.preventDefault()`.

- Example:
  ```html
  <a href="https://example.com" id="link">Click Me</a>
  <script>
    document.getElementById("link").addEventListener("click", (event) => {
      event.preventDefault();
      console.log("Default behavior prevented");
    });
  </script>
  ```

---

## 6. `Other Important Events`

### Mouse Events

- `click`: Fired when an element is clicked.
- `dblclick`: Fired when an element is double-clicked.
- `mousemove`: Fired when the mouse moves over an element.
- `mouseover`: Fired when the mouse enters an element.
- `mouseout`: Fired when the mouse leaves an element.

### Keyboard Events

- `keydown`: Fired when a key is pressed down.
- `keypress`: Fired when a key is pressed (deprecated, use `keydown` or `keyup`).
- `keyup`: Fired when a key is released.

Example:

```javascript
window.addEventListener("keydown", (event) => {
  console.log("Key pressed:", event.key);
});
```

### Form Events

- `submit`: Fired when a form is submitted.
- `change`: Fired when an input value changes.
- `focus`: Fired when an input gains focus.
- `blur`: Fired when an input loses focus.

Example:

```javascript
const form = document.querySelector("form");
form.addEventListener("submit", (event) => {
  event.preventDefault();
  console.log("Form submitted");
});
```

### Load Events

- `load`: Fired when the entire page or an image is fully loaded.
- `DOMContentLoaded`: Fired when the initial HTML document is completely loaded and parsed, without waiting for stylesheets, images, etc.

Example:

```javascript
window.addEventListener("DOMContentLoaded", () => {
  console.log("DOM fully loaded and parsed");
});
```

---

## 7. `Event Listeners Best Practices`

- Always remove event listeners when no longer needed to prevent memory leaks.

  ```javascript
  const handler = () => console.log("Event fired");
  document.addEventListener("click", handler);
  document.removeEventListener("click", handler);
  ```

- Use `event delegation` for better performance and flexibility.
- Use `once: true` in the options to make an event listener execute only once.
  ```javascript
  document.addEventListener("click", () => console.log("Clicked!"), {
    once: true,
  });
  ```
