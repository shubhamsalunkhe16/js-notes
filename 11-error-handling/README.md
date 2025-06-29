# Error handling

## 📌 1. Why Error Handling?

Error handling is a critical aspect of programming that allows your code to gracefully respond to unexpected situations rather than crashing completely. Without proper error handling:

- ❌ A single error can crash your entire application
- ❌ Users may see confusing technical messages
- ❌ Debugging becomes more difficult
- ❌ Critical operations might be left incomplete

**Benefits of good error handling:**

- ✅ Improves user experience by showing helpful messages
- ✅ Enhances application reliability and stability
- ✅ Makes debugging easier by providing clear error information
- ✅ Allows your program to recover from errors and continue running

> 💡 **Knowledge Check:** What might happen if you don't implement error handling in your code?

---

## 📌 2. Errors in JavaScript

Before diving into specific error types, it's important to understand the two main categories of errors:

### 1. 🔠 Parsing Errors (Syntax Errors)

- Occur during code parsing, before execution even begins
- Caused by invalid JavaScript syntax that the engine cannot understand
- `Examples:` **missing parentheses**, **invalid variable names**, or **unclosed string literals**
- These errors cannot be caught with try-catch because the code never runs

### 2. 🔄 Runtime Errors

- Occur during program execution (while your code is running)
- The syntax is valid, but something goes wrong when the code executes
- Examples: trying to access properties of null, dividing by zero, or calling undefined functions
- These are the errors we can catch with try-catch blocks

### JavaScript has several built-in error types:

|      Error Type       | Description                                           | Example                                             |
| :-------------------: | ----------------------------------------------------- | --------------------------------------------------- |
|  **🔤 SyntaxError**   | Occurs when the code structure is invalid             | `console.log("hello"` (missing closing parenthesis) |
| **🔍 ReferenceError** | Occurs when referencing an undefined variable         | `console.log(undefinedVariable)`                    |
|   **🔠 TypeError**    | Occurs when a value is not of the expected type       | `null.toString()`                                   |
|   **📏 RangeError**   | Occurs when a value is outside the allowed range      | `new Array(-1)`                                     |
|    **🔗 URIError**    | Occurs with incorrect URI encoding/decoding           | `decodeURIComponent('%')`                           |
|   **⚙️ EvalError**    | Occurs with the `eval()` function (rare in modern JS) | `eval('var a = ;')`                                 |

> 💡 **Knowledge Check:** What type of error would you expect if you tried to call a method on `null`?

---

## 📌 3. Handling Errors With try and catch

The `try...catch` statement lets you handle errors gracefully:

```javascript
try {
  // 🧪 Code that might cause an error
  console.log("Start of try block");
  // Potentially problematic code here
  console.log("End of try block");
} catch (error) {
  // 🧯 Code to handle the error
  console.error("An error occurred:", error.message);
}
```

**How it works:**

1. ▶️ Code inside the `try` block is executed normally
2. ⏭️ If no errors occur, the `catch` block is skipped
3. ⚠️ If an error occurs in the `try` block, execution jumps to the `catch` block
4. 📦 The error object is passed to the `catch` block

**Example:**

```javascript
try {
  console.log("Starting calculation...");
  let result = 10 / 0; // This won't cause an error in JS (returns Infinity)
  console.log(undefinedVariable); // This WILL cause an error
  console.log("This line never runs");
} catch (error) {
  console.error("Caught an error:", error.message);
}
console.log("Program continues running");
```

### try...catch works synchronously

- If an exception happens in “scheduled” code, like in setTimeout, then try...catch won’t catch it

```js
try {
  setTimeout(function () {
    noSuchVariable; // script will die here
  }, 1000);
} catch (err) {
  alert("won't work");
}
```

- That’s because the function itself is executed later, when the engine has already left the try...catch construct.

- To catch an exception inside a scheduled function, try...catch must be inside that function

```js
setTimeout(function () {
  try {
    noSuchVariable; // try...catch handles the error!
  } catch {
    alert("error is caught here!");
  }
}, 1000);
```

---

## 📌 4. The Error Object

When an error occurs, JavaScript creates an `Error` object with useful properties:

|   Property   | Description                                  |
| :----------: | -------------------------------------------- |
|  `📛 name`   | The type of error (e.g., "ReferenceError")   |
| `💬 message` | Human-readable description of the error      |
|  `📚 stack`  | Stack trace showing where the error occurred |

**Example:**

```javascript
try {
  nonExistentFunction();
} catch (error) {
  console.log(error.name); // "ReferenceError"
  console.log(error.message); // "nonExistentFunction is not defined"
  console.log(error.stack); // Full stack trace with line numbers
}
```

> 💡 **Knowledge Check:** What three properties can you access from an error object?

---

## 📌 5. Rethrowing Errors

Sometimes you want to handle an error partially but pass it up to a higher-level handler:

```javascript
function validateUsername(username) {
  try {
    if (!username) {
      throw new Error("Username is required");
    }
    if (username.length < 3) {
      throw new Error("Username must be at least 3 characters");
    }
    return true;
  } catch (error) {
    console.error("Username validation failed:", error.message);
    throw error; // ↗️ Rethrow the error
  }
}

try {
  validateUsername("");
  console.log("Username is valid");
} catch (error) {
  console.error("Form submission failed:", error.message);
  // Display error to user
}
```

**When to rethrow:**

- 📝 When you want to log the error but still have higher-level code handle it
- 🧹 When you need to perform cleanup but can't fully recover from the error
- ℹ️ When you want to add information to the error but still treat it as an error

> 💡 **Knowledge Check:** What happens when you rethrow an error in a catch block?

---

## 📌 6. The finally Block

The `finally` block contains code that will always execute, regardless of whether an error occurred:

```javascript
function processFile() {
  let file = null;

  try {
    file = openFile("data.txt");
    // Process file data
    return "Processing successful";
  } catch (error) {
    console.error("Error processing file:", error.message);
    return "Processing failed";
  } finally {
    // This will run even if there's a return statement
    // in either the try or catch blocks
    if (file) {
      closeFile(file); // Always close the file
    }
    console.log("Cleanup complete");
  }
}
```

**The `finally` block is perfect for:**

- 🗃️ Closing database connections
- 🔓 Releasing resources (files, network connections)
- 📝 Completing logging
- 🧹 Any cleanup operations that should happen regardless of success or failure

```javascript
try {
  // Code that may throw an error
} catch (error) {
  // Handle the error
} finally {
  // Always runs ✨
}
```

> 💡 **Knowledge Check:** If you have a `return` statement in both the `try` and `catch` blocks, will the `finally` block still execute?

---

## 📌 7. Custom Errors

You can create your own error types by extending the built-in Error class:

**Using ES6 class syntax (modern approach):**

```javascript
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}

try {
  throw new ValidationError("Form data is invalid");
} catch (error) {
  if (error instanceof ValidationError) {
    console.error("Validation failed:", error.message);
  } else {
    console.error("Other error:", error.message);
  }
}
```

**Using function constructor (older approach):**

```javascript
function DatabaseError(message) {
  this.name = "DatabaseError";
  this.message = message;
  this.stack = new Error().stack;
}
DatabaseError.prototype = Object.create(Error.prototype);
```

**Benefits of custom errors:**

- 🔍 You can check for specific error types using `instanceof`
- 📝 Errors are more descriptive and meaningful
- 🛠️ You can add custom properties relevant to the error

> 💡 **Knowledge Check:** What's the advantage of creating custom error types instead of using generic Error objects?

---

## 8. Global catch

- in the browser we can assign a function to the special window.onerror property, that will run in case of an uncaught error.

```js
window.onerror = function (message, url, line, col, error) {
  // ...
};
```

- `message`
  - Error message.
- `url`
  - URL of the script where error happened.
- `line, col`
  - Line and column numbers where error happened.
- `error`
  - Error object.
