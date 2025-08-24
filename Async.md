# Lecture 37

### Q1. JS is Single Threaded and Synchronous

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# 📚 JavaScript is Single Threaded and Synchronous

- JavaScript is designed as a single-threaded and synchronous language.

### 🧵 JavaScript is Single-Threaded

Single-threaded means that JavaScript has:

- One call stack: Executes one function at a time.
- One memory heap: Stores variables and objects.
- Since there's only one thread, JavaScript can execute only one task at a time.
- This design simplifies concurrency — no race conditions or thread collisions within the language.

### ⏱️ JavaScript is Synchronous by Nature

- JavaScript code runs line by line, in the order it appears.
- A statement must complete its execution before the next one starts.

### ⚙️ Asynchronous Capabilities (via Runtime APIs)

While JavaScript is synchronous and single-threaded at its core, it can handle asynchronous operations using features provided by its runtime environment (e.g., browsers or Node.js):

These environments provide:

- Web APIs in browsers (e.g., setTimeout, fetch, event listeners)
- C++ APIs in Node.js (e.g., file system access, timers)

These APIs run operations outside the main thread.
Once completed, they send results back via:

- Callbacks
- Promises
- async/await

This enables non-blocking I/O, which is crucial for performance in web applications.

</div>

---

### Q2. Blocking vs Non-Blocking Code

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# 🔃 Blocking vs Non-Blocking in JavaScript (Node.js)

In JavaScript—particularly in **Node.js**—the terms **blocking** and **non-blocking** refer to **how operations affect the flow of execution** in your code.

JavaScript is **single-threaded**, so managing these two types of operations efficiently is key to building responsive and performant applications.

---

## Blocking Operations

A **blocking operation** halts the execution of further JavaScript code **until the operation completes**.

### 🚨 Impact

- **Freezes the main thread**.
- No other operations can execute in the meantime.
- Can cause performance issues and unresponsiveness in your app.

### 🧪 Examples

```js
const fs = require("fs");

const data = fs.readFileSync("file.txt", "utf-8"); // Blocking
console.log(data); // This won't run until the file is completely read
console.log("This will wait!");
```

- `fs.readFileSync` blocks the thread until the file is read.
- CPU-intensive loops (e.g., calculating large prime numbers) are also blocking.

## Non Blocking Operations

A **non-blocking** operation allows the program to continue executing subsequent code while the operation runs in the background.

### 🚨 Impact

- Keeps the event loop free to handle other tasks.
- Makes apps faster and more responsive, especially for I/O operations.

### 🧪 Examples

```js
const fs = require("fs");

fs.readFile("file.txt", "utf-8", (err, data) => {
  if (err) throw err;
  console.log(data); // This runs after the file is read
});
console.log("This runs without waiting!");
```

- `fs.readFile` is asynchronous and doesn’t block the thread.
- Non-blocking patterns include: - Callbacks - Promises - async/await
</div>

---

### Q3. Event Loop

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# 🔁 Event Loop in JavaScript

The **event loop** is the heart of JavaScript’s asynchronous behavior. It is a mechanism that handles the execution of code, enabling asynchronous operations and ensuring that JavaScript’s single-threaded nature does not block the entire program.

---

## 🧩 Components of the Event Loop

### 🧮 Call Stack

The **call stack** keeps track of the functions being executed. When a function is called, it is pushed onto the top of the stack. Once the function finishes execution, it is popped off. It follows the **LIFO (Last-In-First-Out)** principle.

---

### 🌐 Web APIs / Node.js APIs

Asynchronous operations such as timers, HTTP requests, and file I/O are handled by **Web APIs** in browsers or **C++ APIs** in Node.js. These run in separate threads and allow time-consuming tasks to execute without blocking the call stack.

---

### 📦 Task Queue / Macrotask Queue / Callback Queue

This queue holds **macrotasks**, which include callbacks from operations like timers, I/O events, and UI interactions. When the call stack is empty, the event loop pushes the first task from this queue onto the call stack.

---

### ⚡ Microtask Queue

Microtasks have **higher priority** than macrotasks and are executed immediately after the currently executing script finishes, but **before the next macrotask**. These include:

- Promise callbacks (`then`, `catch`, `finally`)
- `async/await` resolutions
- `queueMicrotask`
- `MutationObserver` callbacks

---

## 🔄 Event Loop Operation Order

1. JavaScript starts by executing all **synchronous code**, pushing function calls onto the call stack.
2. When an **asynchronous operation** is encountered, it is offloaded to the **Web APIs** or **Node.js APIs**.
3. Once the async operation is completed, its **callback** is placed into the **task queue** (macrotask queue) or **microtask queue**, depending on its type.
4. The **event loop** checks if the **call stack is empty**:
   - If yes, it first processes **all microtasks** in the microtask queue.
   - Then it picks the **next macrotask** from the task queue and pushes it onto the call stack.
5. This cycle continues indefinitely.

---

## ✅ Conclusion

The event loop is fundamental to JavaScript’s **non-blocking**, **asynchronous** behavior. It allows JavaScript to handle multiple operations efficiently, despite being single-threaded, by delegating tasks to external APIs and managing callbacks through queues.

> Understanding the event loop is essential for writing performant and responsive JavaScript applications.

</div>
</br>

# Lecture 38

### Q1. setTimeout() vs setInterval() vs clearTimeout() vs clearInterval()

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## ⏱ JavaScript Timers: `setTimeout`, `clearTimeout`, `setInterval`, `clearInterval`

JavaScript provides built-in timing functions to schedule the execution of code at specific time intervals or after a delay. These are useful for creating delays, animations, polling, and more.

---

## 📌 `setTimeout`

- `setTimeout` is used to schedule the execution of a function **once** after a specified delay (in milliseconds).
- It returns a **timer ID**, which can be used to cancel the timeout using `clearTimeout`.

---

## ❌ `clearTimeout`

- `clearTimeout` cancels a timer that was previously created using `setTimeout`.
- It requires the **timer ID** returned by `setTimeout` to identify which timeout to cancel.

---

## 🔁 `setInterval`

- `setInterval` is used to execute a function **repeatedly at fixed intervals** (in milliseconds).
- Like `setTimeout`, it also returns a **timer ID** that can be used to stop the repeated execution.

---

## ✋ `clearInterval`

- `clearInterval` stops an interval that was created with `setInterval`.
- It requires the **interval ID** returned by `setInterval` to cancel it.

---

```js
// ✅ setTimeout Example
let timeoutId = setTimeout(() => {
  console.log("This will run after 2 seconds");
}, 2000);

// ❌ clearTimeout Example
clearTimeout(timeoutId); // Cancels the above timeout, so the message won't show
timeoutId = null; // Best practice to free the variable
```

```js
// ✅ setInterval Example
let intervalId = setInterval(() => {
  console.log("This message repeats every second");
}, 1000);

// ❌ clearInterval Example
setTimeout(() => {
  clearInterval(intervalId); // Stops the interval after 5 seconds
  intervalId = null; // Best practice to reset the ID
}, 5000);
```

</div>

---

### Q2. Best practices for setTimeout() and setInterval()

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## ⚠️ Best Practice: Manage Timer IDs Safely

- It is a good practice to **store timer IDs in a variable**.
- Before creating a new timer (timeout or interval), check if the ID already exists.
- To **avoid creating multiple timers unintentionally**, always **clear the existing timer and set its ID to `null`** before creating a new one.
- This ensures that:
  - You don’t leave timers running unnecessarily.
  - You avoid memory leaks and unintended behavior.

---

## ✅ Timer Control Rule

> Before creating a new `setTimeout` or `setInterval`, make sure:
>
> - The existing timer is cleared using `clearTimeout` or `clearInterval`.
> - The timer ID variable is set to `null`.

This pattern avoids overlapping timers and keeps timer logic predictable and efficient.

```js
// Reusable function to start interval only if not already running
let clockInterval = null;

function startClock() {
  if (clockInterval !== null) {
    clearInterval(clockInterval); // Clear previous interval
    clockInterval = null;
  }

  clockInterval = setInterval(() => {
    console.log("Tick at", new Date().toLocaleTimeString());
  }, 1000);
}

// Later, you can stop it
function stopClock() {
  if (clockInterval !== null) {
    clearInterval(clockInterval);
    clockInterval = null;
  }
}
```

</div>
</br>

# Lecture 39

### Q1. AJAX and XMLHttpRequest

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 🌐 AJAX & XMLHttpRequest in JavaScript

AJAX (Asynchronous JavaScript and XML) allows web pages to communicate with servers **asynchronously**—meaning data can be requested or sent without reloading the entire page. One of the earliest and most widely used tools for AJAX in JavaScript is the `XMLHttpRequest` object.

---

## 🔄 What is `XMLHttpRequest`?

`XMLHttpRequest` is a built-in browser object that allows JavaScript to send HTTP requests to a server and receive data in response, **without refreshing the page**.

It supports:

- Sending GET, POST, PUT, DELETE requests
- Receiving responses as text, XML, or JSON
- Handling asynchronous communication

---

## 📤 `XMLHttpRequest.open()`

### **Syntax**:

```js
xhr.open(method, url, async);
```

- method: HTTP method ("GET", "POST", etc.)
- url: URL to send the request to
- async (optional): true for asynchronous (default), false for synchronous
  > This method prepares the request but does not send it yet.

## 📩 `XMLHttpRequest.send()`

Syntax:

```js
xhr.send(body);
```

- Sends the request to the server.
- If the request method is "POST" or "PUT", you can include a request body.
- If using "GET", the body should be null.

## 📊 `XMLHttpRequest.readyState`

The .readyState property returns the current state of the request:

| Value | State              | Description                                |
| ----- | ------------------ | ------------------------------------------ |
| 0     | `UNSENT`           | Request not initialized                    |
| 1     | `OPENED`           | `open()` has been called                   |
| 2     | `HEADERS_RECEIVED` | `send()` has been called, headers received |
| 3     | `LOADING`          | Downloading response body (partial data)   |
| 4     | `DONE`             | Operation is complete                      |

Typically, we wait for readyState === 4 and status === 200 to know the request succeeded.

</div>

---

### Q2. JSON.parse() vs JSON.stringify()

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

1. `JSON.parse()` is a built-in JavaScript function that convert a JSON formatted string and returns the corresponding JavaScript object.

```js
const jsonString = '{"name": "John", "age": 30, "city": "New York"}';
const person = JSON.parse(jsonString);

console.log(person.name); // John
console.log(person.age); // 30
console.log(person.city); // New York
```

2. `JSON.stringify()` is a built-in JavaScript function that converts a JavaScript object or value to a JSON formatted string.

```js
const person = {
  name: "John",
  age: 30,
  city: "New York",
};

const jsonString = JSON.stringify(person);

console.log(jsonString); // {"name":"John","age":30,"city":"New York"}
```

> Both `JSON.parse()` and `JSON.stringify()` are synchronous functions, meaning they will block the main thread until the operation is complete.

</div>
</br>

# Lecture 40

### Q1. Promises

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

A **Promise** is an object in JavaScript that represents the **eventual completion or failure** of an asynchronous operation and its resulting value.

---

## 🔍 What Is a Promise?

A Promise is a placeholder for a value that is **not immediately available**, but will be resolved (fulfilled or rejected) in the **future**.

Promises have **three states**:

| State       | Description                                   |
| ----------- | --------------------------------------------- |
| `pending`   | Initial state; neither fulfilled nor rejected |
| `fulfilled` | Operation completed successfully              |
| `rejected`  | Operation failed                              |

---

## 🛠️ How to Create a New Promise

A new Promise is created using the `Promise` constructor:

```js
const promise = new Promise((resolve, reject) => {
  // async logic
});
```

- `resolve(value)`: Marks the promise as fulfilled and returns a value.
- `reject(error)`: Marks the promise as rejected and returns an error or reason.

## 🔗 Promise Chaining with .then()

Promises can be chained using .then() to run asynchronous operations in sequence.

- .then() handles a fulfilled result.
- Returns a new Promise, enabling chaining.
- .catch() handles any rejection in the chain.
- .finally() runs regardless of success or failure.

## 🧪 Error Handling: try / catch / finally

While promises themselves use .catch() for errors, if you’re using async/await (which is built on Promises), you can use try...catch...finally blocks.

### try

- Used to wrap code that might throw an error or reject a Promise.

### catch

- Handles the error or rejection that occurs in the try block.

### finally

- Runs code after the try and catch blocks — regardless of the outcome. Useful for cleanup logic.

</div>

---

### Q2. What is callback hell?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 😖 What is Callback Hell in JavaScript?

**Callback Hell** refers to a situation in JavaScript where **multiple nested callbacks** are used to handle asynchronous operations, leading to **code that is difficult to read, debug, and maintain**.

---

## 🔁 Why Does Callback Hell Happen?

JavaScript is **asynchronous and single-threaded**, so developers often use **callbacks** to handle the result of time-consuming operations (e.g., file reading, database queries, API calls). When multiple asynchronous tasks depend on each other, callbacks are nested inside one another, forming a **pyramid or staircase** shape in the code.

---

## 📉 Problems with Callback Hell

| Problem             | Description                                                               |
| ------------------- | ------------------------------------------------------------------------- |
| 😵 Poor Readability | Deep nesting makes code look messy and hard to follow                     |
| 🧩 Hard to Maintain | Updating or modifying logic in deeply nested blocks is error-prone        |
| 🐛 Debugging Issues | Stack traces become difficult to trace through layers of nested functions |
| 🤯 Inflexibility    | Reusing or refactoring logic becomes more complicated                     |

---

## 🛠 How to Avoid Callback Hell

### ✅ Use Named Functions

Break nested functions into separate, named functions to improve readability.

### ✅ Use Promises

Promises allow chaining of async operations without nesting.

### ✅ Use Async/Await

With `async/await`, asynchronous code can be written in a linear, readable fashion similar to synchronous code.

---

## ✅ Summary

| Term              | Description                                                 |
| ----------------- | ----------------------------------------------------------- |
| **Callback Hell** | Overuse of nested callbacks in asynchronous JavaScript code |
| **Caused By**     | Chaining many async tasks using inline callbacks            |
| **Drawbacks**     | Messy structure, harder debugging, poor readability         |
| **Solutions**     | Named functions, Promises, and `async/await`                |

---

> ⚠️ Callback hell is a common pain point in asynchronous JavaScript. The modern solution is to use Promises or `async/await` for cleaner, more manageable code.

</div>

---

### Q3. Does making delay = 0 in setTimeout() make it synchronous?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

No, setting `delay = 0` in `setTimeout` **does not make it synchronous code**. It still behaves asynchronously.

Here's why:

1.  **Event Loop and Task Queue (or Callback Queue):** JavaScript is single-threaded. When you call `setTimeout(callback, delay)`, the `callback` function is not executed immediately, even if `delay` is 0. Instead, it's placed onto a **task queue** (also known as the callback queue).

2.  **Call Stack Priority:** The JavaScript engine always prioritizes the **call stack**. Any code currently executing on the call stack must complete before the event loop can check the task queue for pending tasks.

3.  **"Minimum Delay" Concept:** Even with `delay = 0`, `setTimeout` effectively means "execute this `callback` as soon as the current call stack is empty, but not before." It's more like a "defer" than an "execute now." This is often referred to as a "minimum delay" or "zero-delay timeout."

**Example:**

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Inside setTimeout (delay 0)");
}, 0);

console.log("End");
```

**Output:**

```
Start
End
Inside setTimeout (delay 0)
```

**Explanation of the output:**

- console.log("Start") executes immediately and synchronously.
- setTimeout(() => { ... }, 0) is encountered. The callback function () => { console.log("Inside setTimeout (delay 0)"); } is put into the task queue. The JavaScript engine moves on.
- console.log("End") executes immediately and synchronously because the call stack is not yet empty (it's still processing the initial script).
- Only after the entire initial script finishes (i.e., the call stack becomes empty), the event loop picks up the callback from the task queue and pushes it onto the call stack for execution. That's when "Inside setTimeout (delay 0)" is logged.

</div>

---

### Q4. Common Promise API's

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

### 1. `Promise.resolve(value)`

**Purpose:** Returns a `Promise` object that is resolved with the given `value`. If the `value` is already a Promise, it's returned directly. If the `value` is a `thenable` (an object with a `then` method), the returned Promise will "follow" that thenable, adopting its eventual state. Otherwise, the returned Promise will be fulfilled with the `value`.

---

### 2. `Promise.reject(reason)`

**Purpose:** Returns a `Promise` object that is rejected with the given `reason`.

---

### 3. `Promise.all(iterable)`

**Purpose:** Takes an iterable (e.g., an array) of Promises as input. It returns a single Promise that **resolves** when _all_ of the input Promises have resolved. The resolved value is an array containing the resolved values of the input Promises, in the same order as the input. It **rejects** as soon as _any_ of the input Promises rejects. The rejected value is the reason of the first Promise that rejected.

---

### 4. `Promise.race(iterable)`

**Purpose:** Takes an iterable of Promises as input. It returns a single Promise that **resolves** or **rejects** as soon as _any_ of the input Promises resolves or rejects. The resolved/rejected value is the value/reason of the first Promise to settle.

---

### 5. `Promise.allSettled(iterable)`

**Purpose:** Takes an iterable of Promises as input. It returns a single Promise that **resolves** when _all_ of the input Promises have either resolved or rejected (i.e., settled). The resolved value is an array of objects, each describing the outcome of a Promise (either `{ status: 'fulfilled', value: resolvedValue }` or `{ status: 'rejected', reason: rejectedReason }`).

---

### 6. `Promise.any(iterable)`

**Purpose:** Takes an iterable of Promises as input. It returns a single Promise that **resolves** as soon as _any_ of the input Promises resolves. The resolved value is the value of the first Promise that resolved. It **rejects** if _all_ of the input Promises reject. The rejected value is an `AggregateError` containing an array of all the rejection reasons.

</div>
</br>

# Lecture 41

### Q1. Fetch API

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 🌐 Fetch API in JavaScript

The Fetch API is a built-in JavaScript API that provides an interface for making HTTP requests and handling responses. It's Promise-based, meaning it returns a Promise that resolves or rejects depending on the network request's outcome.

The fetch() function takes one mandatory argument, the path/URL to the resource you want to fetch.

## Fetch Options

| Option      | Description                                                                     |
| ----------- | ------------------------------------------------------------------------------- |
| method      | HTTP method (GET, POST, PUT, DELETE, etc.)                                      |
| headers     | Object containing request headers such as 'Content-Type', 'Authorization', etc. |
| body        | Request body (e.g., JSON, form data)                                            |
| mode        | Specifies the mode of the request (e.g., cors, no-cors, same-origin)            |
| credentials | Specifies whether or not cookies are sent with the request                      |

---

## Fetch Response

The fetch() function returns a Promise that resolves to a Response object. The Response object contains information about the response, such as the status code, headers, and body.

---

### Example

```js
fetch("https://api.example.com/profile", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer YOUR_USER_TOKEN",
  },
  body: JSON.stringify({
    username: "newUsername123",
    email: "new.email@example.com",
  }),
  mode: "cors", // Allow cross-origin requests
  credentials: "include", // Send cookies with the request
})
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => {
    console.log("Profile updated:", data);
  })
  .catch((error) => {
    console.error("Error updating profile:", error);
  });
```

</div>

---

### Q2. HTTP Status Codes

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 📊 HTTP Status Codes

HTTP status codes are used to indicate the outcome of a request. They provide information about the request's success or failure.

Here's a list of common HTTP status codes:

- 1XX - Informational
- 2XX - Success
- 3XX - Redirection
- 4XX - Client Error
- 5XX - Server Error

| Status Code | Category              | Description                                                   |
| ----------- | --------------------- | ------------------------------------------------------------- |
| 200         | OK                    | Request successful                                            |
| 201         | Created               | Resource created successfully                                 |
| 202         | Accepted              | Request accepted for processing                               |
| 204         | No Content            | Request successful, but no content                            |
| 301         | Moved Permanently     | Resource has been moved to a new URL permanently              |
| 302         | Found                 | Resource has been moved to a new URL temporarily              |
| 303         | See Other             | Resource is available at a different URL                      |
| 304         | Not Modified          | Resource has not been modified since last request             |
| 400         | Bad Request           | Request is invalid or cannot be fulfilled                     |
| 401         | Unauthorized          | Request requires authentication                               |
| 403         | Forbidden             | Server refuses to authorize the request                       |
| 404         | Not Found             | Requested resource not found                                  |
| 405         | Method Not Allowed    | Request method is not allowed for the resource                |
| 408         | Request Timeout       | Server timed out waiting for the request                      |
| 409         | Conflict              | Request conflicts with the current state of the resource      |
| 429         | Too Many Requests     | Server refuses to process the request due to rate limiting    |
| 500         | Internal Server Error | Server fails to fulfill the request due to an internal error  |
| 501         | Not Implemented       | Server does not support the requested method                  |
| 502         | Bad Gateway           | Server fails to fulfill the request due to an invalid gateway |
| 503         | Service Unavailable   | Server is unavailable due to maintenance or capacity issues   |

</div>

---

### Q3. Axios

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# Axios 📦

Axios is a **promise-based HTTP client** for the browser and Node.js. It simplifies making HTTP requests to REST endpoints and handling their responses.

---

## Common Methods

| Method                          | Description          |
| ------------------------------- | -------------------- |
| `axios.get(url, config)`        | Perform GET request  |
| `axios.post(url, data, config)` | Perform POST request |
| `axios.put(url, data, config)`  | Update data          |
| `axios.delete(url, config)`     | Delete a resource    |

## Response Format

```js
response = {
  data: {}, // response payload
  status: 200, // HTTP status code
  statusText: "OK",
  headers: {}, // response headers
  config: {}, // request config
  request: {}, // raw request
};
```

- Axios automatically parses JSON responses and sets the `data` property to the parsed object. If the response is not JSON, Axios sets the `data` property to the raw response string. Also do the same at the time of sending the request.

</div>
 
---

### Q4. Fetch Promise Rejection

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## ⚠️ Understanding `fetch()` and HTTP Errors

The `fetch()` API **only rejects** a promise when a **network error** occurs (e.g., no internet, DNS failure, CORS issues).

It **does not reject** on HTTP errors like `404 Not Found` or `500 Internal Server Error`. Instead, it resolves the promise and you need to manually check the `response.ok` property.

</div>
</br>

# Lecture 42, 43, 45

### Q1. Prototype in JavaScript

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

In JavaScript, a **prototype** is an object that acts as a blueprint for other objects. In JavaScript, a **prototype** is an object from which other objects inherit properties and methods. When you try to access a property or method on an object, and that property or method isn't found directly on the object itself, JavaScript automatically looks it up in the object's prototype. This forms a chain of objects, known as the **prototype chain**, which is how JavaScript achieves inheritance. 🧬

## How it Works

Every JavaScript object has an associated prototype. This prototype object, in turn, can have its own prototype, and so on, forming a chain that eventually ends with `null`. When you access a property or method:

1.  JavaScript first checks if the property/method exists directly on the object.
2.  If not, it looks for it on the object's prototype.
3.  If still not found, it continues up the prototype chain until it either finds the property/method or reaches `null`.
4.  If it reaches `null` without finding the property/method, it returns `undefined` (for properties) or throws an error (for method calls).

---

## The `prototype` Property of Functions

Every **function** in JavaScript automatically gets a `prototype` property. This `prototype` property is an object that's intended to hold properties and methods that you want to be inherited by instances created using that function as a constructor.

When you create a new object using the `new` keyword with a constructor function, the new object's internal `[[Prototype]]` (which you can often access via `.__proto__`) is set to point to the constructor function's `prototype` object.

---

## Prototype in Classes

ES6 Classes are largely **syntactic sugar** over JavaScript's existing prototype-based inheritance. When you define a class, the methods defined within the class body are automatically placed on the class's `prototype` object.

---

## Why Prototypes Are Important

- **Inheritance:** Prototypes are the fundamental mechanism for inheritance in JavaScript, allowing objects to inherit properties and methods from other objects.
- **Memory Efficiency:** Methods defined on the prototype are shared among all instances, rather than being duplicated for each instance. This saves memory, especially when you have many objects of the same type.
- **Dynamic Nature:** You can add new properties and methods to a prototype **after** objects have been created, and those existing objects will immediately gain access to the new members.

</div>

---

### Q2. `new` keyword and Constructor Functions

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

In JavaScript, the `new` keyword and constructor functions are **fundamental to object-oriented programming (OOP)**. They serve as the primary mechanism to:

- Create instances of objects
- Establish prototype-based inheritance

---

## 🔨 The `new` Keyword

The `new` keyword is an **operator** used to create an instance of:

- A **user-defined** object type (via constructor functions)
- A **built-in** object type (like `Date`, `Object`, etc.)

When placed before a function call, it **transforms that function into a constructor call**.

---

## ⚙️ What Happens When You Use `new`?

When you call a function with `new`, JavaScript performs the following steps:

1. **Create a new empty object**

   - A plain JavaScript object `{}` is created.

2. **Set the `[[Prototype]]` of the new object**

   - The new object's `__proto__` is set to the **constructor's `.prototype`**.
   - This links the instance to the constructor’s prototype, enabling **inheritance**.

3. **Execute the constructor function**

   - The constructor is called with `this` bound to the new object.
   - Inside the function, `this` refers to the new instance.
   - Properties and methods can now be added using `this`.

4. **Return the object**
   - If the constructor **returns an object**, that object is returned.
   - If it **returns a primitive** or nothing, the newly created object is returned.

---

# Constructor Functions in JavaScript

A **constructor function** is a **regular JavaScript function** that is intended to be called using the `new` keyword. It is used to create and initialize new object instances.

---

## 📌 Purpose

- To **create and initialize** new objects (instances) with specific properties and methods.
- Context of this: When called with new, the this keyword inside a constructor function refers to the newly created instance.
- Return Value: Typically, constructor functions do not explicitly return a value. If they do, and the returned value is a non-primitive object, that object is returned instead of the newly created instance. If a primitive value (like a number, string, boolean) or nothing is returned, the new instance is returned.
- Prototype Linkage: The prototype property of the constructor function is essential. Any properties or methods added to Constructor.prototype will be inherited by all instances created using that constructor.

---

## ✍️ Naming Convention

By convention, constructor function names **start with a capital letter** to distinguish them from regular functions.

</div>

---

### Q3. `__proto__` vs `Prototype`

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

`.__proto__` and `.prototype` are both related to JavaScript's prototype-based inheritance, but they serve different roles and are accessed on different types of entities.

---

## `.__proto__` (Internal Property)

The `.__proto__` property is an **internal property** of an **object instance** that points to its **prototype object**. It's the actual link in the prototype chain that JavaScript traverses when looking for properties or methods that aren't directly on the object itself.

- **Who has it:** Every JavaScript **object instance**.
- **What it points to:** The actual prototype object from which the instance inherits.
- **Role:** It's the mechanism by which an object "looks up" properties and methods in its inheritance chain.
- **Usage Note:** While widely supported, `.__proto__` is a legacy, non-standard way to access an object's prototype. It's generally recommended to use `Object.getPrototypeOf()` to read an object's prototype and `Object.setPrototypeOf()` to set it, as these are standard and often more performant.

---

## `.prototype` (Property of Functions/Classes)

The `.prototype` property is a property of **constructor functions** and **classes** (which are syntactic sugar over constructor functions). It is the object that will become the `.__proto__` of any instances created by that constructor or class.

- **Who has it:** Only **functions** (specifically, those intended to be used as constructors) and **classes**.
- **What it points to:** An object that serves as the "blueprint" for new instances. You define shared methods and properties on this object.
- **Role:** It's where you define the properties and methods that you want all instances created by that constructor/class to inherit.
- **Usage Note:** This is the standard and recommended way to add methods and properties that are shared among all instances of a particular type, improving memory efficiency.

</div>

---

### Q4. Classes in JavaScript

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

Classes in JavaScript are **syntactic sugar** over the existing prototype-based inheritance model. They provide a cleaner, more familiar object-oriented syntax for creating objects and handling inheritance, making JavaScript look and feel more like traditional class-based languages (like Java or C++), while still operating on the same underlying prototype mechanisms. 🍰

---

## Defining a Class

You define a class using the `class` keyword, followed by the class name (conventionally capitalized) and a pair of curly braces.

---

## `constructor` Method

The `constructor` is a special method within a class that gets called automatically when a new object (instance) of the class is created using the `new` keyword. Its primary purpose is to **initialize the object's state** by setting its properties. A class can only have **one `constructor` method**. If you don't define a `constructor`, JavaScript provides a default empty one. The `this` keyword inside the constructor refers to the newly created instance.

---

## Instance Properties and Methods

Properties defined directly within the `constructor` using `this.` are **instance properties**. Each instance gets its own copy of these. Methods defined outside the `constructor` but within the class body are **prototype methods**. These methods are automatically added to the class's `prototype` object and are shared among all instances, promoting memory efficiency.

---

## Creating Class Instances

You create new objects (instances) of a class using the `new` keyword, similar to how you would with constructor functions.

---

## Inheritance with `extends` and `super`

Classes support inheritance using the `extends` keyword. A **child class** can `extend` a **parent class** (or base class), inheriting its properties and methods. In the constructor of a child class, `super()` must be called before `this` can be used. It calls the constructor of the parent class, ensuring that the parent's initialization logic runs. In a child class method, `super.methodName()` allows you to call a method from the parent class.

---

## Static Methods

Static methods are methods that belong to the **class itself**, not to any specific instance of the class. They are defined using the `static` keyword and are called directly on the class name. They cannot access instance properties (i.e., they don't have access to `this` referring to an instance). They're useful for utility functions, factory methods, or operations that don't depend on the state of a particular instance.

---

## Private Class Features (ES2022)

Modern JavaScript (ES2022 and later) introduced private class fields and methods, prefixed with a `#` (hash) symbol. These members are truly private and are not accessible from outside the class or from subclasses (except through public methods of the class itself).

</div>
</br>

# Lecture 44, 46

### Q1. Call vs Apply vs Bind

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

`call`

- The `call()` method invokes a function immediately with a specified `this` context. Arguments are passed individually as a comma-separated list.

---

`apply`

- The `apply()` method invokes a function immediately with a specified `this` context and argument are passed as an array.

---

`bind`

- The `bind()` method does not invoke the function immediately. Instead, it returns a new function with the `this` context permanently bound to the specified value. Any arguments provided to bind after the `this` context are pre-filled (curried) into the new function.

---

```js
const person = {
  name: "Alice",
  greet: function (city, country) {
    console.log(`Hello, my name is ${this.name} from ${city}, ${country}.`);
  },
};

const anotherPerson = {
  name: "Bob",
};

// Bind the greet function to anotherPerson, pre-filling 'Paris'
const boundGreet = person.greet.bind(anotherPerson, "Paris");

// The boundGreet function can now be called later
boundGreet("France"); // Output: Hello, my name is Bob from Paris, France.
// Notice 'France' is the second argument, after the pre-filled 'Paris'
```

</div>
</br>

# Lecture 49

### Q1. Lexical Scope and Closures

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## Lexical Scope

Lexical scoping in JS defines the accessibility of variables and functions based on their location in the source code. Also known as static scoping.

## Closures

Closures is the combination of a function and the lexical scope within which that function was declared. Closures are the functions that have access to the outer scope function, even after the outer function has returned.

## Example

```js
function createCounter() {
  let count = 0; // 'count' is in the lexical environment of createCounter

  // This inner function forms a closure
  return function increment() {
    count++; // 'increment' accesses 'count' from its outer scope
    console.log(count);
  };
}

const counter1 = createCounter(); // counter1 is the returned 'increment' function
counter1(); // Output: 1
counter1(); // Output: 2

const counter2 = createCounter(); // createCounter runs again, creating a *new* 'count'
counter2(); // Output: 1 (This 'count' is independent of counter1's 'count')
counter2(); // Output: 2
```

</div>
</br>

# Lecture 48, 49

### Q1. Object.getOwnPropertyDescriptors()

### Q2. Object.defineProperty()

### Q3. Math.PI value change example

### Q4. Object Iterators

### Q5. Getters and Setters

</br>

# Lecture 50

### Q1. Local Storage and Session Storage

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 📦 Local Storage

- Local Storage allows you to store data persistently, meaning the data remains even after the browser tab or window is closed, or the computer is restarted. The data has no expiration date and will stay until explicitly deleted by the user or by the web application. Both are web storage APIs.

- Lifespan: Persistent. Data remains until cleared manually or programmatically.

- Scope: Data is available across all tabs and windows from the same origin (same protocol, host, and port).

- Capacity: Typically offers a larger storage capacity, usually around 5MB to 10MB per origin, depending on the browser.

- Accessibility: Accessible via the window.localStorage object.

## Methods:

- `localStorage.setItem(key, value)`: Stores a key-value pair.

- `localStorage.getItem(key)`: Retrieves the value for a given key.

- `localStorage.removeItem(key)`: Removes a specific key-value pair.

- `localStorage.clear()`: Clears all key-value pairs for the current origin.

- `localStorage.key(index)`: Gets the key at a specific index.

- `localStorage.length`: Returns the number of stored items.

---

## 📦 Session Storage

- Session Storage allows you to store data only for the duration of a single browser session. The data is cleared when the browser tab or window is closed. If the user opens a new tab or window to the same website, a new, separate session storage is created for that tab/window. Web Storage APIs.

- Lifespan: Ephemeral. Data is cleared when the Browse session (tab/window) ends.

- Scope: Data is specific to the tab or window that created it. It's not shared between multiple tabs/windows, even if they are from the same origin.

- Capacity: Similar to Local Storage, typically 5MB to 10MB per origin per tab.

- Accessibility: Accessible via the window.sessionStorage object.

### Note:

- JSON.stringify() while storing data and JSON.parse() while retrieving data.
- Depends on browser profile as well.
- Vulnerable to XSS attacks.
</div>

---

### Q2. Cookies

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 📦 Cookies

Cookies are small pieces of data that are stored on the user's computer by the web browser. They are sent to the server with each request, and the server can send them back to the browser. Cookies are often used to store user preferences, login information, and other settings.

### How to set a cookie:

```js
document.cookie =
  "name=value; expires=date; path=path; domain=domain; secure; httponly";
```

| Parameter | Description                                                                                                     |
| --------- | --------------------------------------------------------------------------------------------------------------- |
| name      | Name of the cookie.                                                                                             |
| value     | Value of the cookie.                                                                                            |
| expires   | Expiration date of the cookie. It's a date string in the format "YYYY-MM-DD HH:MM:SS GMT/UTC".                  |
| path      | Path of the cookie. It's a URL path. If not specified, the cookie is sent to all pages on the domain.           |
| domain    | Domain of the cookie. It's a domain name. If not specified, the cookie is sent to all subdomains of the domain. |

---

## 📦 Cookie Storage

- In JS you can access cookies using the document.cookie property.

- It will return a string containing all the cookies separated by semicolons.

- 4KB limit per cookie.

- Send with every HTTP request results in overhead.

</div>

---

### Q3. Currying

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

Currying is a technique in functional programming where a function with multiple arguments is transformed into a sequence of functions, each taking a single argument. This allows for partial application of the function, where some arguments are fixed and others are left to be provided later.

```js
function curried(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}
console.log(curried(1)(2)(3)); // Output: 6
```

</div>
</br>
