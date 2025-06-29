# Async JavaScript - fetch() API

## 🌟 Introduction

The **fetch() API** is a modern, powerful, built-in browser feature in JavaScript used to make HTTP requests to servers — like getting data from an API (e.g., TMDB or GitHub) or sending data to a backend.

Think of it like asking a waiter (browser) to go get some data (like food) from the kitchen (server), and bring it back to you.

It's the successor to the older XMLHttpRequest and provides a cleaner, more flexible interface for network requests.

**Why fetch() API?**

- **Promise-based**: Works seamlessly with async/await
- **Modern syntax**: Clean and readable code
- **Flexible**: Supports all HTTP methods
- **Built-in**: Available in all modern browsers
- **Stream-based**: Better handling of large responses

---

## 🔍 What is fetch() API?

**Definition**: The fetch() API is a web standard that provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses.

**Key Characteristics:**

- Returns a Promise that resolves to the Response object
- Does NOT reject on HTTP error status codes (404, 500, etc.)
- Only rejects on network failures or request setup issues
- Supports streaming responses
- Can be cancelled using AbortController

<details>
<summary>🧠 Knowledge Check: What does fetch() return?</summary>

**Answer**: fetch() returns a Promise that resolves to a Response object representing the response to the request.

</details>

---

## 📝 fetch() API Syntax

### Basic Syntax

```javascript
fetch(url, options)
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

### Parameters

- **url** (required): The resource URL
- **options** (optional): Configuration object with properties like:
  - `method`: HTTP method (GET, POST, PUT, DELETE, etc.)
  - `headers`: Request headers
  - `body`: Request body data
  - `mode`: CORS mode
  - `credentials`: Include credentials or not

### Basic Example

```javascript
// Simple GET request
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

### Example 2:👇

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "Hello",
    body: "This is a test post",
    userId: 1,
  }),
})
  .then((res) => res.json())
  .then((data) => console.log("Posted:", data))
  .catch((err) => console.log("Error:", err));
```

### 🔍 What's Happening? (Line-by-Line Breakdown)

#### 1. The URL

```js
fetch("https://jsonplaceholder.typicode.com/posts", { ... })

```

- This is a fake test API that accepts dummy post requests.

- You are telling the browser: **“Send a request to this address and try to create (POST) a new post there.”**

#### 2. The options object

This object tells the fetch() function what kind of request you want to send, and what data is going with it.

##### a. method: "POST"

```js
headers: {
  "Content-Type": "application/json"
}

```

- You are telling the server:

> “I’m sending JSON data in the request body.”

- If you don’t send this header, the server may not understand your data properly.

##### c. `body`

```js
body: JSON.stringify({
  title: "Hello",
  body: "This is a test post",
  userId: 1,
});
```

- body is the actual data you're sending to the server.

- It's an object like this:

```js
{
  title: "Hello",
  body: "This is a test post",
  userId: 1
}

```

- But it must be converted to a string before sending. That’s why we use `JSON.stringify()`.

##### 3. The Response Handling

```js
.then(res => res.json())

```

- The server sends back a **response** (like: “Hey, I received your data”).

- That response is in **JSON** format, so we convert it to a JavaScript object using `.json()`.

##### 4. The Final Result

```js
.then(data => console.log("Posted:", data))

```

- After conversion, we get the final data from the server — usually `it echoes back the data you sent`.

- This line logs it in the console.

✅ You’ll see:

```js
Posted: {
  title: "Hello",
  body: "This is a test post",
  userId: 1,
  id: 101
}

```

`Note:` It adds an `id: 101` — meaning the server accepted your post and assigned an ID to it.

##### 5. Catching Errors

```js
.catch(err => console.log("Error:", err));

```

- If the request fails (e.g., no internet or wrong URL), this block will catch the error and print it.

#### 🔁 Summary of the Flow

```vbnet

1. fetch() sends data to the server
2. We tell it the method is POST
3. We set headers to say we're sending JSON
4. We send a JS object (converted to JSON)
5. The server responds with a success message
6. We log the result to the console
7. We handle any possible errors

```

✅ Output in Console

```js
Posted: {
  title: "Hello",
  body: "This is a test post",
  userId: 1,
  id: 101
}

```

<details>
<summary>🧠 Knowledge Check: What are the two main parameters of fetch()?</summary>

**Answer**:

1. **url** (required) - The resource URL you want to fetch
2. **options** (optional) - Configuration object for the request
</details>

---

## ⚡ Using fetch() with async/await

The async/await syntax makes fetch() requests more readable and easier to handle.

### Basic Pattern

```javascript
async function fetchData(url) {
  try {
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error("Error:", error);
    throw error;
  }
}
```

### Why Use async/await?

- **Cleaner code**: Eliminates callback chains
- **Better error handling**: Use try/catch blocks
- **Sequential execution**: Easy to read flow
- **Return values**: Can return processed data

### 🔄 Comparison: Promises vs async/await

<table>
<tr>
<th>🔗 Promise Chain</th>
<th>🚀 async/await</th>
</tr>
<tr>
<td>

```javascript
fetch("/api/user/1")
  .then((response) => {
    if (!response.ok) {
      throw new Error("Network error");
    }
    return response.json();
  })
  .then((user) => {
    console.log(user);
    return fetch(`/api/posts/${user.id}`);
  })
  .then((response) => response.json())
  .then((posts) => {
    console.log(posts);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

</td>
<td>

```javascript
async function getUserAndPosts() {
  try {
    const userResponse = await fetch("/api/user/1");
    if (!userResponse.ok) {
      throw new Error("Network error");
    }

    const user = await userResponse.json();
    console.log(user);

    const postsResponse = await fetch(`/api/posts/${user.id}`);
    const posts = await postsResponse.json();
    console.log(posts);
  } catch (error) {
    console.error("Error:", error);
  }
}
```

</td>
</tr>
</table>

<details>
<summary>🧠 Knowledge Check: What's the advantage of using async/await with fetch()?</summary>

**Answer**: async/await makes the code more readable, allows better error handling with try/catch, eliminates callback chains, and makes asynchronous code look like synchronous code.

</details>

<details>
<summary>❓ Question: What happens if you forget to use 'await' with fetch()?</summary>

**💡 Answer:** Without `await`, fetch() returns a Promise object instead of the actual response:

```javascript
// ❌ Wrong - returns Promise<Response>
const response = fetch("/api/data");
console.log(response); // Promise { <pending> }

// ✅ Correct - returns Response object
const response = await fetch("/api/data");
console.log(response); // Response { status: 200, ... }

// ❌ This will cause errors
const data = fetch("/api/data").json(); // TypeError!

// ✅ Correct way
const data = await (await fetch("/api/data")).json();
```

</details>

---

## 🌐 HTTP Methods Overview

Understanding HTTP methods is crucial for API interactions:

<div style="background: linear-gradient(45deg, #fa709a 0%, #fee140 100%); padding: 20px; border-radius: 10px; color: #333; margin: 15px 0;">

### 🎯 Understanding HTTP Methods

HTTP methods define the **intent** of your request. Each method has a specific purpose and semantic meaning.

</div>

### 📊 HTTP Methods Reference

<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr style="background: #f8f9fa;">
<th>🌊 Method</th>
<th>🎯 Purpose</th>
<th>📦 Body</th>
<th>🔒 Safe</th>
<th>🔄 Idempotent</th>
<th>💡 Use Case</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>GET</strong></td>
<td>Retrieve data</td>
<td>❌ No</td>
<td>✅ Yes</td>
<td>✅ Yes</td>
<td>Fetch user profile</td>
</tr>
<tr>
<td><strong>POST</strong></td>
<td>Create resource</td>
<td>✅ Yes</td>
<td>❌ No</td>
<td>❌ No</td>
<td>Create new user</td>
</tr>
<tr>
<td><strong>PUT</strong></td>
<td>Replace resource</td>
<td>✅ Yes</td>
<td>❌ No</td>
<td>✅ Yes</td>
<td>Update entire profile</td>
</tr>
<tr>
<td><strong>PATCH</strong></td>
<td>Partial update</td>
<td>✅ Yes</td>
<td>❌ No</td>
<td>❌ No</td>
<td>Update email only</td>
</tr>
<tr>
<td><strong>DELETE</strong></td>
<td>Remove resource</td>
<td>🔸 Optional</td>
<td>❌ No</td>
<td>✅ Yes</td>
<td>Delete user account</td>
</tr>
<tr>
<td><strong>HEAD</strong></td>
<td>Get headers only</td>
<td>❌ No</td>
<td>✅ Yes</td>
<td>✅ Yes</td>
<td>Check if file exists</td>
</tr>
<tr>
<td><strong>OPTIONS</strong></td>
<td>Get allowed methods</td>
<td>❌ No</td>
<td>✅ Yes</td>
<td>✅ Yes</td>
<td>CORS preflight</td>
</tr>
</tbody>
</table>

### Key Concepts:

- **Idempotent**: Multiple identical requests have the same effect
- **Safe**: Doesn't modify server state
- **Cacheable**: Response can be cached

<details>
<summary>🧠 Knowledge Check: Which HTTP method should you use to partially update a resource?</summary>

**Answer**: **PATCH** - It's designed for partial updates, unlike PUT which replaces the entire resource.

</details>

---

## 📥 GET Resources with fetch()

GET is the most common HTTP method for retrieving data.

GET is the most fundamental HTTP method. It's used to retrieve data from a server without modifying anything. Every time you type a URL in your browser or click a link, you're making a GET request.

### 🔍 Analogy:

Imagine you’re ordering from Zomato.
You click `"View Menu"` — you're asking the server,

> **“Hey, send me the food list (but I’m not changing anything)!”**

That's a `GET request`. You're just **viewing** (not adding, editing, or deleting).

### Basic GET Request

```javascript
async function fetchPosts() {
  const API_URL = "https://jsonplaceholder.typicode.com/posts";

  try {
    const response = await fetch(API_URL);

    // Check if request was successful
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    // Check content type
    const contentType = response.headers.get("content-type");
    if (!contentType || !contentType.includes("application/json")) {
      throw new TypeError("Response is not JSON!");
    }

    const data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error("Fetch error:", error);
    throw error;
  }
}
```

### Response Properties

- `response.ok`: Boolean indicating success (status 200-299)
- `response.status`: HTTP status code
- `response.statusText`: Status message
- `response.headers`: Headers object
- `response.url`: Final URL after redirects

## 🔍 4. Key Characteristics of GET:

| Property    | Value                         |
| ----------- | ----------------------------- |
| Purpose     | Read/Fetch data               |
| Body        | ❌ No body allowed            |
| Cacheable   | ✅ Often cached by browser    |
| Safe?       | ✅ Yes (no data change)       |
| Idempotent? | ✅ Same request = same result |

### 🧠 Knowledge Check

<details>
<summary>Q: What does response.ok indicate?</summary>

**Answer**: response.ok is a boolean that indicates whether the response was successful (status codes 200-299). It's false for 4xx and 5xx status codes.

</details>

<details>
<summary>Q: Why do we need to check response.ok even for GET requests?</summary>

**💡 Answer:**

fetch() **only rejects** for network errors, not HTTP error status codes:

```javascript
// ❌ This will NOT throw an error for 404, 500, etc.
try {
  const response = await fetch("/api/nonexistent");
  // response.status = 404, but no error thrown
  const data = await response.json(); // This might fail
} catch (error) {
  // Only catches network errors, not HTTP errors
}

// ✅ Proper error handling
try {
  const response = await fetch("/api/nonexistent");

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }

  const data = await response.json();
} catch (error) {
  // Catches both network AND HTTP errors
}
```

**🎯 Key Point:** Always check `response.ok` or `response.status` to handle HTTP errors properly.

</details>

---

## 🔍 Query Parameters

### 🧠 What is a Query Parameter?

A **query parameter** is extra information added to a URL to:

- Filter
- Search
- Sort
- Customize the response from the server

Query parameters allow you to filter, sort, or modify API responses.

### 🧾 Basic Syntax

```txt
https://example.com/api?key=value
```

- `?` — starts the query section
- `key=value` — one filter
- `&` — separates multiple filters

### 📌 Real Example

```txt
https://jsonplaceholder.typicode.com/posts?userId=1
```

👉 This tells the server:

> “Give me **only the posts** where `userId` is `1`.”

### 🔍 Anatomy of Query Parameters

```txt
URL: https://api.com/products?category=shoes&sort=price
              └────────┬────────┘ └────┬────┘
                  key=value         key=value
```

📝 This URL means:

- `category=shoes` → filter products to show only shoes
- `sort=price` → sort them by price

### ✅ Using Query Parameters in `fetch()`

```js
fetch("https://jsonplaceholder.typicode.com/posts?userId=1")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

📦 This will get all posts made by user with ID = 1.

## 🔁 More Examples

| URL with Query Params            | Meaning                        |
| -------------------------------- | ------------------------------ |
| `/products?category=shoes`       | Filter to only show shoes      |
| `/users?age=25`                  | Get users aged 25              |
| `/posts?userId=1&id=5`           | Get post with ID 5 from user 1 |
| `/movies?genre=action&year=2023` | Get action movies from 2023    |

### 🧠 Query Params vs Path Params

| Feature          | Query Parameter       | Path Parameter          |
| ---------------- | --------------------- | ----------------------- |
| URL Example      | `/users?age=25`       | `/users/25`             |
| Purpose          | Filters, search, sort | Exact lookup by ID      |
| Flexibility      | ✅ Flexible           | ❌ Strict structure     |
| Mostly used with | `GET` requests        | Resource identification |

### 🛠 Building Query Strings Dynamically

```js
const userId = 1;
const postId = 5;

const url = `https://jsonplaceholder.typicode.com/posts?userId=${userId}&id=${postId}`;

fetch(url)
  .then((res) => res.json())
  .then((data) => console.log(data));
```

### 🎯 When to Use Query Parameters

- ✅ Filtering by category or type
- ✅ Searching by keyword
- ✅ Sorting by price, rating, etc.
- ✅ Paginating results (page=1, limit=10)

### 🧪 Try This Example

```js
fetch("https://jsonplaceholder.typicode.com/comments?postId=2")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

✅ This returns all comments for **post ID = 2**

### ✅ Summary Table

| Concept     | Explanation                            |
| ----------- | -------------------------------------- |
| `?`         | Starts query section of URL            |
| `key=value` | One filter or parameter                |
| `&`         | Separates multiple key-value pairs     |
| Used in     | Mostly in `GET` requests               |
| Common use  | Filters, searches, sorting, pagination |

---

> 💡 **Pro Tip:** Always use `encodeURIComponent()` when building dynamic query strings with user input.

```js
const search = "smart phones";
const url = `https://api.com/search?q=${encodeURIComponent(search)}`;
```

### Manual Query String

```javascript
const url = "https://api.example.com/posts?userId=1&_limit=5";
```

### Using URLSearchParams

```javascript
async function fetchPostsWithComments() {
  const API_URL = "https://jsonplaceholder.typicode.com/posts";

  // Create query parameters object
  const queryParams = {
    userId: 1,
    _limit: 10,
    _sort: "title",
    _order: "asc",
  };

  try {
    // Build query string
    const queryString = new URLSearchParams(queryParams).toString();
    const url = `${API_URL}?${queryString}`;

    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error("Error:", error);
  }
}
```

## How the above code Works:

#### 🔍 Goal of the Code

We want to **fetch a list of posts** from an API, but with:

- Only from `userId = 1`
- Only 10 posts
- Sorted by `title`
- In **ascending** (`asc`) order

### ✅ Step 1: Function Setup

```js
async function fetchPostsWithComments() {
```

- Declares an **async function** so we can use `await` inside.
- Function name describes the task clearly.

### ✅ Step 2: API Base URL

```js
const API_URL = "https://jsonplaceholder.typicode.com/posts";
```

- This is the **endpoint** we’ll fetch data from.
- JSONPlaceholder is a free fake API often used for learning.

### ✅ Step 3: Create Query Parameter Object

```js
const queryParams = {
  userId: 1,
  _limit: 10,
  _sort: "title",
  _order: "asc",
};
```

We are defining filters here:

| Key      | Meaning                               |
| -------- | ------------------------------------- |
| `userId` | Get posts only by user with ID `1`    |
| `_limit` | Limit results to 10 posts only        |
| `_sort`  | Sort the results by the `title` field |
| `_order` | Use ascending order (`asc`)           |

### ✅ Step 4: Convert Object to Query String

```js
const queryString = new URLSearchParams(queryParams).toString();
```

- `URLSearchParams(queryParams)` takes your object and builds:

  ```js
  userId=1&_limit=10&_sort=title&_order=asc
  ```

- `.toString()` turns it into a query string for the URL.

### ✅ Step 5: Combine Full URL

```js
const url = `${API_URL}?${queryString}`;
```

- Combines base API and query string:

  ```js
  https://jsonplaceholder.typicode.com/posts?userId=1&_limit=10&_sort=title&_order=asc
  ```

### ✅ Step 6: Fetch the Data

```js
const response = await fetch(url);
```

- Sends a **GET** request to the built URL
- `await` waits until the server sends back a response

### ✅ Step 7: Parse JSON Response

```js
const data = await response.json();
```

- Converts the raw HTTP response into usable **JavaScript object/array**
- Now you can access it like `data[0].title` etc.

### ✅ Step 8: Log the Result

```js
console.log(data);
return data;
```

- Shows the fetched posts in the console
- Returns the data so you can use it elsewhere if needed

### ✅ Step 9: Handle Errors

```js
} catch (error) {
    console.error('Error:', error);
}
```

- If something fails (like no internet or invalid URL), this block runs
- Prevents your app from crashing

### 📦 Final Output (You’ll see 10 posts from user 1 sorted by title)

```js
[
  {
    userId: 1,
    id: 3,
    title: "adipisicing elit",
    body: "..."
  },
  {
    userId: 1,
    id: 7,
    title: "aliquid rerum mollitia",
    body: "..."
  },
  ...
]
```

### 🧠 Summary Flow

1. ✅ Create a base API URL
2. ✅ Build a query filter object
3. ✅ Convert it to query string using `URLSearchParams`
4. ✅ Combine URL + query
5. ✅ Fetch the data
6. ✅ Parse it into JSON
7. ✅ Use it or log it

---

## 🔍 URLSearchParams Methods

### 🧠 What is `URLSearchParams` ?

It’s a JavaScript object that lets you **easily read, write, update, or delete query parameters** in a URL.

### 🔧 Commonly Used `URLSearchParams` Methods

| Method                                 | What it does                                    |
| -------------------------------------- | ----------------------------------------------- |
| `.get(key)`                            | Get the value of a specific parameter           |
| `.getAll(key)`                         | Get **all values** of a parameter (if repeated) |
| `.set(key, value)`                     | Set or update the value of a parameter          |
| `.append(key, value)`                  | Add another value to an existing parameter      |
| `.delete(key)`                         | Remove a parameter from the URL                 |
| `.has(key)`                            | Check if a parameter exists                     |
| `.toString()`                          | Convert the object into a query string          |
| `.keys()` / `.values()` / `.entries()` | Loop through all params                         |

---

## ✅ 1. `.get(key)`

Get a value of a query parameter.

```js
const url = new URLSearchParams("userId=5&sort=desc");
console.log(url.get("userId")); // "5"
console.log(url.get("sort")); // "desc"
```

---

## ✅ 2. `.getAll(key)`

Returns **all values** for a key (when key appears multiple times).

```js
const params = new URLSearchParams("tag=js&tag=react&tag=node");
console.log(params.getAll("tag")); // ["js", "react", "node"]
```

---

## ✅ 3. `.set(key, value)`

Set or update the value of a key. If it exists, it's overwritten.

```js
const params = new URLSearchParams("page=1&sort=desc");
params.set("page", 2);
console.log(params.toString()); // "page=2&sort=desc"
```

---

## ✅ 4. `.append(key, value)`

Adds a **new value** without replacing existing one. Useful for multi-select filters.

```js
const params = new URLSearchParams();
params.append("tag", "js");
params.append("tag", "node");
console.log(params.toString()); // "tag=js&tag=node"
```

---

## ✅ 5. `.delete(key)`

Removes a parameter completely.

```js
const params = new URLSearchParams("search=js&sort=asc");
params.delete("sort");
console.log(params.toString()); // "search=js"
```

---

## ✅ 6. `.has(key)`

Checks if a parameter exists.

```js
const params = new URLSearchParams("q=hello");
console.log(params.has("q")); // true
console.log(params.has("page")); // false
```

---

## ✅ 7. `.toString()`

Converts `URLSearchParams` back into a proper query string.

```js
const params = new URLSearchParams({ userId: 1, sort: "asc" });
console.log(params.toString()); // "userId=1&sort=asc"
```

You can use this in a fetch URL:

```js
fetch(`https://api.com/posts?${params.toString()}`);
```

---

## ✅ 8. `.keys()`, `.values()`, `.entries()`

These are for looping.

### Loop over keys

```js
for (let key of params.keys()) {
  console.log(key);
}
```

### Loop over values

```js
for (let value of params.values()) {
  console.log(value);
}
```

### Loop over key-value pairs

```js
for (let [key, value] of params.entries()) {
  console.log(`${key} = ${value}`);
}
```

---

## 🎯 Summary Table

| Method                      | What it Does                            |
| --------------------------- | --------------------------------------- |
| `get("key")`                | Get single value of a parameter         |
| `getAll("key")`             | Get all values for repeated keys        |
| `set("key", val)`           | Set or update value (replaces existing) |
| `append("key", val)`        | Add extra value (does not replace)      |
| `delete("key")`             | Remove a parameter                      |
| `has("key")`                | Check if the key exists                 |
| `toString()`                | Turn into a real query string           |
| `keys()/values()/entries()` | Loop through all parameters             |

---

## 🚀 Real Use Case Example:

```js
const filters = new URLSearchParams();

filters.append("category", "shoes");
filters.append("category", "bags");
filters.set("sort", "price");
filters.set("order", "asc");

console.log(filters.toString());
// category=shoes&category=bags&sort=price&order=asc
```

👉 You can now send this in a GET request!

<details>
<summary>🧠 Knowledge Check: What's the benefit of using URLSearchParams?</summary>

**Answer**: URLSearchParams automatically handles URL encoding, provides methods to manipulate parameters, and creates properly formatted query strings without manual string concatenation.

</details>

---

## 📤 CREATE Resources (POST)

POST requests are used to create new resources on the server.

> **Think of POST like filling a form and submitting it.**

### Basic POST Request

```javascript
async function createPost(postData) {
  const API_URL = "https://jsonplaceholder.typicode.com/posts";

  try {
    const response = await fetch(API_URL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(postData),
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const result = await response.json();
    console.log("Created:", result);
    return result;
  } catch (error) {
    console.error("Creation error:", error);
    throw error;
  }
}

// Usage
const newPost = {
  title: "My New Post",
  body: "This is the content of my post",
  userId: 1,
};

createPost(newPost);
```

### ✅ Goal:

Send a **POST request** to an API and **create a new post** with some data.

### 💡 Step-by-Step Explanation:

#### 🔹1. **Function Declaration**

```js
async function createPost(postData) {
```

- `async`: This means the function will use `await` and return a **Promise**.
- `postData`: This is the data (like title, body, userId) you want to send to the server.

#### 🔹2. **API URL**

```js
const API_URL = "https://jsonplaceholder.typicode.com/posts";
```

- This is the URL of the fake API (JSONPlaceholder) where you're sending the post.

### 🔹3. **Try-Catch Block for Safety**

```js
try {
  // do something
} catch (error) {
  // handle error
}
```

- Used to **handle errors gracefully** — for example, if the server is down.

#### 🔹4. **Sending the POST request**

```js
const response = await fetch(API_URL, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(postData),
});
```

Let’s break this fetch call:

| Part                             | Meaning                                        |
| -------------------------------- | ---------------------------------------------- |
| `await fetch(...)`               | Waits for the server to respond                |
| `method: "POST"`                 | We're sending data to create something         |
| `headers`                        | Tell the server we're sending JSON             |
| `body: JSON.stringify(postData)` | Convert the `postData` object to a JSON string |

**Why JSON.stringify?**
Because the HTTP body must be a **string**, not a JS object.

#### 🔹5. **Checking the Response Status**

```js
if (!response.ok) {
  throw new Error(`HTTP error! status: ${response.status}`);
}
```

- `response.ok` is true if status is 200–299.
- If the server returns an error (like 400 or 500), we throw a custom error.

#### 🔹6. **Convert the Response to JSON**

```js
const result = await response.json();
```

- The server responds with some JSON data.
- `await response.json()` converts it into a JavaScript object.

#### 🔹7. **Log the Created Post**

```js
console.log("Created:", result);
return result;
```

- Shows the server’s response in the console.
- Returns the result so it can be used later.

#### 🔹8. **Catch Block (Error Handling)**

```js
} catch (error) {
    console.error('Creation error:', error);
    throw error;
}
```

- If anything fails above (network issue, invalid response), it logs the error.

### 🧪 Usage Example:

```js
const newPost = {
  title: "My New Post",
  body: "This is the content of my post",
  userId: 1,
};

createPost(newPost);
```

You are passing this `newPost` object into the function.
It gets sent as a POST request to the API.

### 📦 What Happens Behind the Scenes?

1. You call `createPost(newPost)`
2. It sends a **POST** request to the API
3. The server "creates" a new post and sends back the created data
4. You log and return that data

## Important Points

- Always set `Content-Type` header for JSON data
- Use `JSON.stringify()` to convert objects to JSON strings
- Server typically returns the created resource with an ID

<details>
<summary>🧠 Knowledge Check: Why do we need to set Content-Type header in POST requests?</summary>

**Answer**: The Content-Type header tells the server what format the request body is in. For JSON data, we set it to "application/json" so the server knows how to parse the incoming data.

</details>

---

## 🔄 UPDATE Resources (PUT/PATCH)

### ✍️ Imagine This Real-Life Analogy:

You have a **profile form** with these fields:

```json
{
  "name": "Neeraj",
  "email": "neeraj@gmail.com",
  "location": "Delhi"
}
```

Let’s say you want to update your profile.

## 🔁 1. **PUT – Replace Everything**

> **PUT is like rewriting the entire profile** even if you're just changing one thing.

If you update just the `location` using PUT:

```json
{
  "name": "Neeraj",
  "email": "neeraj@gmail.com",
  "location": "Mumbai"
}
```

You must **send the whole object** again — not just the changed part.

- If you forget to send `email`, it will be **erased**.
- It's a **full replacement**.

---

### ✅ Use Case:

- Replacing a blog post
- Updating the full user profile

---

## 🩹 2. **PATCH – Update Partially**

> **PATCH is like editing just one field** in your profile without touching others.

To update just the location:

```json
{
  "location": "Mumbai"
}
```

- PATCH updates only the given fields.
- The rest of the data **remains unchanged**.

---

### ✅ Use Case:

- Updating just one property (like username or status)
- Partial profile changes
- Toggle a boolean field (e.g., completed: true)

---

## 📊 Comparison Table

| Feature              | PUT                                 | PATCH                   |
| -------------------- | ----------------------------------- | ----------------------- |
| Purpose              | Full update (replace)               | Partial update          |
| Sends entire object? | ✅ Yes                              | ❌ Only changed fields  |
| Risk                 | Can accidentally delete data        | Safer for minor changes |
| Idempotent           | ✅ Yes (same request = same result) | ✅ Yes                  |
| Used for             | Full record update                  | Single field change     |

---

## 🧠 Simple Example in Code:

### PUT - Complete Resource Replacement

```javascript
async function updatePost(postId, postData) {
  const API_URL = `https://jsonplaceholder.typicode.com/posts/${postId}`;

  try {
    const response = await fetch(API_URL, {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(postData),
    });

    const result = await response.json();
    console.log("Updated:", result);
    return result;
  } catch (error) {
    console.error("Update error:", error);
  }
}

// Complete replacement
const updatedPost = {
  id: 1,
  title: "Updated Title",
  body: "Updated content",
  userId: 1,
};

updatePost(1, updatedPost);
```

### PATCH - Partial Update

```javascript
async function updateViews(postId, viewData) {
  const API_URL = `https://jsonplaceholder.typicode.com/posts/${postId}`;

  try {
    const response = await fetch(API_URL, {
      method: "PATCH",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(viewData),
    });

    const result = await response.json();
    console.log("Partially updated:", result);
    return result;
  } catch (error) {
    console.error("Partial update error:", error);
  }
}

// Only update specific fields
updateViews(1, { views: 150 });
```

## 🧠 Key Rule to Remember:

- **PUT = Paint the entire wall again**
- **PATCH = Just fix the cracked spot**

<details>
<summary>🧠 Knowledge Check: What's the difference between PUT and PATCH?</summary>

**Answer**:

- **PUT**: Replaces the entire resource with new data
- **PATCH**: Updates only the specified fields, leaving others unchanged
</details>

---

## 🗑️ DELETE Resources

The DELETE method is used to delete/remove a resource from the server.

> Like clicking a trash-can icon to remove a post, a comment, or an account.

### 🧠 Real-Life Analogy:

Imagine you posted a comment on Instagram.

Now you want to **delete** it.

When you hit `🗑 Delete`:

- Your browser sends a `DELETE` request to the server.

- The server removes that comment.

- You don’t get anything new in return — maybe just a `Deleted Successfully` message.

```javascript
async function deletePost(postId) {
  const API_URL = `https://jsonplaceholder.typicode.com/posts/${postId}`;

  try {
    const response = await fetch(API_URL, {
      method: "DELETE",
    });

    if (!response.ok) {
      throw new Error(`Failed to delete: ${response.status}`);
    }

    // Some APIs return empty response for DELETE
    const result =
      response.status === 204
        ? { message: "Deleted successfully" }
        : await response.json();

    console.log("Deleted:", result);
    return result;
  } catch (error) {
    console.error("Delete error:", error);
    throw error;
  }
}

// Usage
deletePost(1);
```

### DELETE Response Codes

- **200**: Success with response body
- **204**: Success with no content
- **404**: Resource not found

### 🔐 Do You Send Data in DELETE?

Usually NO.

You just send the ID in the URL like:

```bash
DELETE /posts/1
```

Sometimes, for advanced APIs, you may send some extra data (rarely), but standard DELETEs are clean.

### 🧾 What Does the Server Return?

Most APIs respond with:

```json
{ "message": "Deleted successfully" }
```

Or they just send back status 204 No Content, meaning deletion is done and there’s nothing else to show.

### 📊 Quick Summary Table:

| Feature     | DELETE                                      |
| ----------- | ------------------------------------------- |
| Purpose     | Remove a resource                           |
| Data sent   | Usually just the ID in URL                  |
| Response    | Often empty or confirmation                 |
| Safe?       | ❌ No (it changes the server)               |
| Idempotent? | ✅ Yes (deleting again has no extra effect) |

<details>
<summary>🧠 Knowledge Check: What HTTP status code indicates successful deletion with no response body?</summary>

**Answer**: **204 No Content** - indicates the request was successful but there's no content to return.

</details>

---

## 🏷️ Custom Headers

Headers provide metadata about the request or response.

### Common Headers

```javascript
async function authenticatedRequest() {
  const API_URL = "https://api.example.com/protected";

  try {
    const response = await fetch(API_URL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer your-token-here",
        "X-API-Key": "your-api-key",
        Accept: "application/json",
        "User-Agent": "MyApp/1.0",
        "X-Custom-Header": "custom-value",
      },
      body: JSON.stringify({
        username: "user123",
        action: "getData",
      }),
    });

    const result = await response.json();
    return result;
  } catch (error) {
    console.error("Request error:", error);
  }
}
```

### Important Headers

- **Content-Type**: Format of request body
- **Authorization**: Authentication credentials
- **Accept**: Expected response format
- **User-Agent**: Client identification
- **X-\*\*\***: Custom headers (prefix with X-)

<details>
<summary>🧠 Knowledge Check: What header is used for authentication?</summary>

**Answer**: **Authorization** header is commonly used for authentication, often with formats like "Bearer token" or "Basic credentials".

</details>

---

## 📋 Creating Request Objects

A Request object is an instance of the Request class that holds all details of an HTTP request:

- Method (GET, POST, etc.)

- Headers

- Body

- URL

- Mode (CORS, no-cors, same-origin)

- Credentials, etc.

`Request objects provide reusable, configurable request templates`.

### Basic Request Object

```javascript
const request = new Request("https://api.example.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "New Post",
    content: "Post content",
  }),
});

async function sendRequest(request) {
  try {
    const response = await fetch(request);
    const result = await response.json();
    console.log("Success:", result);
    return result;
  } catch (error) {
    console.error("Error:", error);
  }
}

sendRequest(request);
```

### Why use Request instead of fetch directly?

| Use Case                       | `fetch(url, options)` | `new Request()` |
| ------------------------------ | --------------------- | --------------- |
| Simple requests                | ✅                    | ❌              |
| Reusable request object        | ❌                    | ✅              |
| Better readability for configs | ❌                    | ✅              |
| Can inspect or clone request   | ❌                    | ✅              |

### Cloning and Modifying Requests

Useful if you want to reuse the same request in multiple fetch() calls (because requests are one-time use):

```javascript
const baseRequest = new Request("https://api.example.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
});

// Create a new request based on the first one
const modifiedRequest = new Request(baseRequest, {
  body: JSON.stringify({
    title: "Different Post",
    content: "Different content",
  }),
});
```

### Benefits of Request Objects

- **Reusability**: Create templates for common requests
- **Immutability**: Original request isn't modified when cloned
- **Consistency**: Ensure similar requests have same configuration

### Common Properties

| Property      | Description                         |
| ------------- | ----------------------------------- |
| `method`      | HTTP method like GET, POST          |
| `url`         | Request URL                         |
| `headers`     | Headers sent with the request       |
| `body`        | Request body (for POST/PUT/PATCH)   |
| `mode`        | `cors`, `no-cors`, or `same-origin` |
| `credentials` | `include`, `same-origin`, or `omit` |

<details>
<summary>🧠 Knowledge Check: Why would you use Request objects instead of passing options directly to fetch()?</summary>

**Answer**: Request objects provide reusability, allow you to create templates for similar requests, ensure consistency across requests, and can be cloned and modified without affecting the original.

</details>

---

## 🛠️ Handling Responses & Errors

Proper error handling is crucial for robust applications.

### Complete Response Handling

```javascript
async function robustFetch(url, options = {}) {
  try {
    const response = await fetch(url, options);

    // Check if request was successful
    if (!response.ok) {
      // Handle different error types
      switch (response.status) {
        case 400:
          throw new Error("Bad Request - Check your data");
        case 401:
          throw new Error("Unauthorized - Check your credentials");
        case 403:
          throw new Error("Forbidden - Access denied");
        case 404:
          throw new Error("Not Found - Resource doesn't exist");
        case 500:
          throw new Error("Server Error - Try again later");
        default:
          throw new Error(`HTTP Error: ${response.status}`);
      }
    }

    // Check content type
    const contentType = response.headers.get("content-type");

    if (contentType && contentType.includes("application/json")) {
      return await response.json();
    } else if (contentType && contentType.includes("text/")) {
      return await response.text();
    } else {
      return await response.blob();
    }
  } catch (error) {
    // Network errors, parsing errors, etc.
    if (error.name === "TypeError") {
      console.error("Network error:", error.message);
    } else {
      console.error("Request error:", error.message);
    }
    throw error;
  }
}
```

### Response Methods

- `response.json()`: Parse JSON data
- `response.text()`: Get text content
- `response.blob()`: Get binary data
- `response.arrayBuffer()`: Get array buffer
- `response.formData()`: Get form data

### Error Types

1. **Network Errors**: No internet, server down
2. **HTTP Errors**: 4xx, 5xx status codes
3. **Parsing Errors**: Invalid JSON, etc.
4. **Timeout Errors**: Request takes too long

<details>
<summary>🧠 Knowledge Check: Does fetch() automatically throw an error for 404 status codes?</summary>

**Answer**: **No**. fetch() only rejects on network errors. HTTP error status codes (like 404, 500) are considered successful requests, so you need to check `response.ok` manually.

</details>

---

## ❌ Canceling fetch() Requests

AbortController allows you to cancel ongoing requests.

### Why cancel a fetch?

You might want to cancel a request:

- When user navigates away

- To avoid race conditions (e.g., live search)

- To prevent unnecessary network calls

### Basic Cancellation

```javascript
let controller;

async function fetchWithCancel(url) {
  // Create new controller for this request
  controller = new AbortController();
  const signal = controller.signal;

  try {
    const response = await fetch(url, { signal });
    const data = await response.json();
    console.log("Data received:", data);
    return data;
  } catch (error) {
    if (error.name === "AbortError") {
      console.log("Request was cancelled");
    } else {
      console.error("Fetch error:", error);
    }
  }
}

// To cancel the request
function cancelRequest() {
  if (controller) {
    controller.abort("User cancelled the request");
    console.log("Request cancelled");
  }
}
```

### 🧠 Key Concepts

| Concept              | Meaning                                          |
| -------------------- | ------------------------------------------------ |
| `AbortController()`  | Creates a controller to cancel requests          |
| `controller.signal`  | A signal passed to `fetch()` to listen for abort |
| `controller.abort()` | Cancels the request immediately                  |
| `AbortError`         | Error thrown when fetch is aborted               |

### Timeout Implementation

```javascript
async function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();
  const signal = controller.signal;

  // Set timeout
  const timeoutId = setTimeout(() => {
    controller.abort("Request timeout");
  }, timeout);

  try {
    const response = await fetch(url, { signal });
    clearTimeout(timeoutId); // Clear timeout if request succeeds
    return await response.json();
  } catch (error) {
    clearTimeout(timeoutId);
    if (error.name === "AbortError") {
      throw new Error("Request timed out");
    }
    throw error;
  }
}
```

### Use Cases for Cancellation

- **User Navigation**: Cancel when user leaves page
- **Search Debouncing**: Cancel previous search when typing
- **Timeouts**: Prevent hanging requests
- **Component Unmounting**: Cancel in React/Vue cleanup

<details>
<summary>🧠 Knowledge Check: What happens when you call controller.abort()?</summary>

**Answer**: When you call controller.abort(), the fetch request is immediately cancelled and throws an AbortError. Any ongoing network activity is stopped.

</details>

---

## 🎯 Interview Questions

<details>
<summary>1. What is the difference between fetch() and XMLHttpRequest?</summary>

**Answer:**

- **fetch()**: Promise-based, modern syntax, better error handling, supports streaming, built-in JSON parsing
- **XMLHttpRequest**: Callback-based, older API, more verbose, requires manual parsing
- fetch() is the modern standard and preferred approach
</details>

<details>
<summary>2. Why doesn't fetch() reject HTTP error status codes?</summary>

**Answer:**
fetch() only rejects on network failures (no internet, server unreachable). HTTP status codes like 404, 500 are considered valid responses from the server's perspective. You need to check `response.ok` or `response.status` manually to handle HTTP errors.

</details>

<details>
<summary>3. How do you handle CORS errors with fetch()?</summary>

**Answer:**
CORS errors occur when making cross-origin requests. Solutions include:

- Configure server to allow cross-origin requests
- Use `mode: 'cors'` in fetch options
- Use a proxy server for development
- Implement proper CORS headers on the server
</details>

<details>
<summary>4. What's the difference between no-cors and cors mode?</summary>

**Answer:**

- **cors mode**: Default mode, allows cross-origin requests with proper CORS headers
- **no-cors mode**: Makes opaque requests, you can't read the response, mainly for fire-and-forget requests
</details>

<details>
<summary>5. How do you upload files using fetch()?</summary>

**Answer:**

```javascript
const formData = new FormData();
formData.append("file", fileInput.files[0]);

fetch("/upload", {
  method: "POST",
  body: formData, // Don't set Content-Type header manually
});
```

</details>

<details>
<summary>6. Can you use fetch() in Node.js?</summary>

**Answer:**
Yes, fetch() is available in Node.js 18+ natively. For older versions, you can use packages like `node-fetch` or `isomorphic-fetch`.

</details>

<details>
<summary>7. How do you implement retry logic with fetch()?</summary>

**Answer:**

```javascript
async function fetchWithRetry(url, options, retries = 3) {
  for (let i = 0; i < retries; i++) {
    try {
      const response = await fetch(url, options);
      if (response.ok) return response;
    } catch (error) {
      if (i === retries - 1) throw error;
      await new Promise((resolve) => setTimeout(resolve, 1000 * i));
    }
  }
}
```

</details>

---

## 📝 Practice Tasks

### Task 1: Basic API Interaction

Create functions to interact with JSONPlaceholder API:

1. Fetch all posts
2. Fetch posts by specific user ID
3. Create a new post
4. Update an existing post
5. Delete a post

<details>
<summary>Solution</summary>

```javascript
const API_BASE = "https://jsonplaceholder.typicode.com";

// 1. Fetch all posts
async function getAllPosts() {
  const response = await fetch(`${API_BASE}/posts`);
  return await response.json();
}

// 2. Fetch posts by user ID
async function getPostsByUser(userId) {
  const response = await fetch(`${API_BASE}/posts?userId=${userId}`);
  return await response.json();
}

// 3. Create new post
async function createPost(postData) {
  const response = await fetch(`${API_BASE}/posts`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(postData),
  });
  return await response.json();
}

// 4. Update post
async function updatePost(id, postData) {
  const response = await fetch(`${API_BASE}/posts/${id}`, {
    method: "PUT",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(postData),
  });
  return await response.json();
}

// 5. Delete post
async function deletePost(id) {
  const response = await fetch(`${API_BASE}/posts/${id}`, {
    method: "DELETE",
  });
  return response.ok;
}
```

</details>

### Task 2: Error Handling Wrapper

Create a robust fetch wrapper that handles all types of errors and provides meaningful error messages.

<details>
<summary>Solution</summary>

```javascript
async function safeFetch(url, options = {}) {
  try {
    const response = await fetch(url, options);

    if (!response.ok) {
      const errorData = await response.text();
      throw new Error(`HTTP ${response.status}: ${errorData}`);
    }

    const contentType = response.headers.get("content-type");
    if (contentType?.includes("application/json")) {
      return await response.json();
    }
    return await response.text();
  } catch (error) {
    if (error.name === "TypeError") {
      throw new Error("Network error: Check your internet connection");
    }
    throw error;
  }
}
```

</details>

### Task 3: Search with Debouncing

Implement a search function that cancels previous requests when new searches are made.

<details>
<summary>Solution</summary>

```javascript
let searchController = null;

async function searchPosts(query) {
  // Cancel previous request
  if (searchController) {
    searchController.abort();
  }

  // Create new controller
  searchController = new AbortController();

  try {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/posts?q=${query}`,
      { signal: searchController.signal }
    );
    const results = await response.json();
    return results;
  } catch (error) {
    if (error.name !== "AbortError") {
      console.error("Search error:", error);
    }
  }
}

// Debounced search
function debounce(func, delay) {
  let timeoutId;
  return (...args) => {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}

const debouncedSearch = debounce(searchPosts, 300);
```

</details>

### Task 4: File Upload with Progress

Create a function to upload files with progress tracking.

<details>
<summary>Solution</summary>

```javascript
async function uploadFile(file, onProgress) {
  const formData = new FormData();
  formData.append("file", file);

  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();

    xhr.upload.addEventListener("progress", (event) => {
      if (event.lengthComputable) {
        const percentComplete = (event.loaded / event.total) * 100;
        onProgress(percentComplete);
      }
    });

    xhr.addEventListener("load", () => {
      if (xhr.status === 200) {
        resolve(JSON.parse(xhr.responseText));
      } else {
        reject(new Error(`Upload failed: ${xhr.status}`));
      }
    });

    xhr.addEventListener("error", () => {
      reject(new Error("Upload failed"));
    });

    xhr.open("POST", "/upload");
    xhr.send(formData);
  });
}
```

</details>

### Task 5: API Rate Limiting

Implement a rate-limited fetch function that ensures you don't exceed API limits.

<details>
<summary>Solution</summary>

```javascript
class RateLimiter {
  constructor(requestsPerMinute = 60) {
    this.requests = [];
    this.limit = requestsPerMinute;
  }

  async rateLimitedFetch(url, options) {
    await this.waitForRateLimit();
    this.requests.push(Date.now());
    return fetch(url, options);
  }

  async waitForRateLimit() {
    const now = Date.now();
    const oneMinuteAgo = now - 60000;

    // Remove requests older than 1 minute
    this.requests = this.requests.filter((time) => time > oneMinuteAgo);

    if (this.requests.length >= this.limit) {
      const oldestRequest = this.requests[0];
      const waitTime = 60000 - (now - oldestRequest);
      await new Promise((resolve) => setTimeout(resolve, waitTime));
      return this.waitForRateLimit();
    }
  }
}

const limiter = new RateLimiter(30); // 30 requests per minute
```

</details>

### Task 6: Comprehensive Quiz

**Question 1:** What will happen if you don't check `response.ok` before parsing JSON?

<details>
<summary>Answer</summary>

If the server returns an error status (like 404 or 500) but with a JSON error message, the code might still work. However, if the server returns HTML error pages or non-JSON content, `response.json()` will throw a parsing error. Always check `response.ok` first.

</details>

**Question 2:** How would you implement request/response interceptors similar to Axios?

<details>
<summary>Answer</summary>

```javascript
class FetchInterceptor {
  constructor() {
    this.requestInterceptors = [];
    this.responseInterceptors = [];
  }

  addRequestInterceptor(interceptor) {
    this.requestInterceptors.push(interceptor);
  }

  addResponseInterceptor(interceptor) {
    this.responseInterceptors.push(interceptor);
  }

  async fetch(url, options = {}) {
    // Apply request interceptors
    for (const interceptor of this.requestInterceptors) {
      options = await interceptor(options);
    }

    let response = await fetch(url, options);

    // Apply response interceptors
    for (const interceptor of this.responseInterceptors) {
      response = await interceptor(response);
    }

    return response;
  }
}
```

</details>

**Question 3:** What's the difference between `response.json()` and `JSON.parse(response)`?

<details>
<summary>Answer</summary>

- `response.json()` is a method that reads the response stream and parses it as JSON
- `JSON.parse()` only works on strings, so you'd need `JSON.parse(await response.text())`
- `response.json()` can only be called once per response due to stream consumption
- `response.json()` handles encoding and other response details automatically
</details>

---

## 🎓 Summary

Today you mastered the **fetch() API**, a powerful tool for making HTTP requests in modern JavaScript. Key takeaways:

✅ **Understood fetch() fundamentals** - Promise-based, flexible API

✅ **Learned HTTP methods** - GET, POST, PUT, PATCH, DELETE and their purposes

✅ **Mastered async/await pattern** - Clean, readable asynchronous code

✅ **Implemented CRUD operations** - Create, Read, Update, Delete resources

✅ **Handled errors properly** - Network errors, HTTP errors, parsing errors

✅ **Used query parameters** - URLSearchParams for clean URL building

✅ **Added custom headers** - Authentication, content types, custom metadata

✅ **Created Request objects** - Reusable request templates

✅ **Implemented cancellation** - AbortController for request management

✅ **Built robust applications** - Error handling, timeouts, retries
