# Lecture 1

### Q1. What is JavaScript?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">
JavaScript is a high-level, interpreted programming language primarily used to create dynamic and interactive effects within web browsers. It is a core technology of the World Wide Web, alongside HTML and CSS.
</div>

---

### Q2. What is the difference between compiler and interpreter?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">
A **compiler** translates the entire code into machine code before execution, which generally makes execution faster. An **interpreter**, on the other hand, translates and executes the code line-by-line, which can be slower but useful for dynamic execution and easier debugging.
</div>

---

### Q3. Is JavaScript a compiled language or interpreted language?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">
Traditionally, JavaScript is an interpreted language. However, modern JavaScript engines like V8 use Just-In-Time (JIT) compilation, which combines interpretation and compilation to improve performance.
</div>

</br>

# Lecture 4

### Q1. What is the difference between var, let, and const?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">
# var vs let vs const in JavaScript

| Feature                          | `var`                                                | `let`                                                              | `const`                                                            |
| -------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| **Scope**                        | Function-scoped or globally scoped                   | Block-scoped (`{}`)                                                | Block-scoped (`{}`)                                                |
| **Hoisting**                     | Yes, hoisted and initialized to `undefined`          | Yes, hoisted but in **Temporal Dead Zone (TDZ)** until initialized | Yes, hoisted but in **Temporal Dead Zone (TDZ)** until initialized |
| **Access Before Initialization** | ✅ Allowed (returns `undefined`)                     | ❌ Not allowed — gives `ReferenceError`                            | ❌ Not allowed — gives `ReferenceError`                            |
| **Initialization Requirement**   | Optional (can be declared without assigning a value) | Optional (can be declared without assigning a value)               | Mandatory — must be initialized at the time of declaration         |
| **Re-declaration**               | ✅ Allowed in the same scope                         | ❌ Not allowed in the same scope                                   | ❌ Not allowed in the same scope                                   |
| **Reassignment**                 | ✅ Allowed                                           | ✅ Allowed                                                         | ❌ Not allowed                                                     |
| **Binding to Global Object**     | ✅ Yes (if declared globally, non-strict mode)       | ❌ No                                                              | ❌ No                                                              |
| **Use Case**                     | Legacy code or for function-wide variables           | Preferred for block-scoped, mutable variables                      | Use for constants or when reassignment should be disallowed        |

---

### 🔍 Notes:

- **TDZ (Temporal Dead Zone):** A phase where a `let` or `const` variable is hoisted but not yet initialized, causing `ReferenceError` if accessed before declaration.
- **Best Practices:**
  - Use `let` for variables that will change.
  - Use `const` for variables that should never be reassigned.
  - Avoid `var` unless working with legacy code.
  </div>

---

### Q2 . console.log() vs console.table()

```js
const user1 = "Hitesh" ;
console.log(user1); // will display the output in the string/text format

const user = "Hitesh" ;
const user2 = "Himanshu" ;
const user3 = "Ashu" ;
console.table([user, user2, user3]); // will display the output in the table format

Output:

Hitesh

┌─────────┬───────────┐
│ (index) │   Values  │
├─────────┼───────────┤
│    0    │ 'Hitesh'  │
│    1    │ 'Himanshu'│
│    2    │ 'Ashu'    │
└─────────┴───────────┘

```

</br>

# Lecture 5

### Q1. Datatypes in JS

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# JavaScript Data Types

JavaScript has **eight basic (primitive) data types**, plus complex types like `Object`.

---

## 🔢 Primitive Data Types

Primitive types are **immutable** and stored **by value**.

### 1. Number

Represents both integers and floating-point numbers.

```js
let a = 42;
let b = 3.14;
```

---

### 2. String

A sequence of characters, enclosed in single (`'`), double (`"`), or backticks (`` ` ``).

```js
let name = "Alice";
let greeting = "Hello";
let message = `Welcome, ${name}`;
```

---

### 3. Boolean

Represents a logical value: `true` or `false`.

```js
let isLoggedIn = true;
let isAdmin = false;
```

---

### 4. Undefined

A variable that has been declared but not assigned a value.

```js
let x;
console.log(x); // undefined
```

---

### 5. Null

Represents the **intentional absence** of a value.

```js
let data = null;
```

---

### 6. Symbol (ES6)

A **unique and immutable** value used as the key for object properties.

```js
let sym = Symbol("id");
```

---

### 7. BigInt (ES11)

Used to represent **very large integers** beyond the `Number` limit.

```js
let big = 1234567890123456789012345678901234567890n;
```

---

## 🧱 Non-Primitive (Reference) Type

Stored **by reference**.

### 8. Object

Used to store collections of data and more complex entities.

```js
let person = {
  name: "John",
  age: 30,
};
```

> Arrays, functions, and dates are all special types of objects:

```js
let arr = [1, 2, 3]; // Array
let func = function () {}; // Function
let now = new Date(); // Date
```

---

## ✅ Summary Table

| Type      | Example                    | `typeof` result           |
| --------- | -------------------------- | ------------------------- |
| Number    | `42`, `3.14`               | `"number"`                |
| String    | `"hello"`                  | `"string"`                |
| Boolean   | `true`, `false`            | `"boolean"`               |
| Undefined | `let x;`                   | `"undefined"`             |
| Null      | `null`                     | `"object"` _(quirk)_      |
| Symbol    | `Symbol("id")`             | `"symbol"`                |
| BigInt    | `123n`                     | `"bigint"`                |
| Object    | `{}`, `[]`, `function(){}` | `"object"` / `"function"` |

</div>

</br>

# Lecture 6

### Q1. To number conversoin

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# `Number()` Conversion Examples

| Input       | Code Example        | Output |
| ----------- | ------------------- | ------ |
| `"33"`      | `Number("33")`      | `33`   |
| `"33acr"`   | `Number("33acr")`   | `NaN`  |
| `true`      | `Number(true)`      | `1`    |
| `false`     | `Number(false)`     | `0`    |
| `undefined` | `Number(undefined)` | `NaN`  |
| `null`      | `Number(null)`      | `0`    |

</div>

---

### Q2. To Boolean conversion

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# `Boolean()` Conversion Examples in

| Input      | Code Example        | Output  | Explanation                     |
| ---------- | ------------------- | ------- | ------------------------------- |
| `1`        | `Boolean(1)`        | `true`  | Non-zero number → true          |
| `0`        | `Boolean(0)`        | `false` | Zero is falsy → false           |
| `""`       | `Boolean("")`       | `false` | Empty string → false            |
| `"Hitesh"` | `Boolean("Hitesh")` | `true`  | Non-empty string → true         |
| `" "`      | `Boolean(" ")`      | `true`  | Non-empty string (space) → true |

</div>

---

### Q3. To String conversion

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# `String()` Conversion Examples

| Input       | Code Example        | Output        |
| ----------- | ------------------- | ------------- |
| `33`        | `String(33)`        | `"33"`        |
| `true`      | `String(true)`      | `"true"`      |
| `false`     | `String(false)`     | `"false"`     |
| `undefined` | `String(undefined)` | `"undefined"` |
| `null`      | `String(null)`      | `"null"`      |
| `NaN`       | `String(NaN)`       | `"NaN"`       |
| `[]`        | `String([])`        | `""`          |
| `[1, 2, 3]` | `String([1, 2, 3])` | `"1,2,3"`     |

</div>

</br>

# Lecture 7

### Q1. Arithmetic Operators

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# 🧮 Arithmetic Operators

| Operator | Name                | Description                                | Example  | Result |
| -------- | ------------------- | ------------------------------------------ | -------- | ------ |
| `+`      | Addition            | Adds two numbers or concatenates strings   | `5 + 2`  | `7`    |
| `-`      | Subtraction         | Subtracts second number from the first     | `5 - 2`  | `3`    |
| `*`      | Multiplication      | Multiplies two numbers                     | `5 * 2`  | `10`   |
| `/`      | Division            | Divides first number by the second         | `5 / 2`  | `2.5`  |
| `**`     | Exponentiation      | Raises first number to the power of second | `5 ** 2` | `25`   |
| `%`      | Modulus (Remainder) | Remainder after division                   | `5 % 2`  | `1`    |

</div>

---

### Q2. Addition Rules in the JavaScript language

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# ➕ Addition Rules in JavaScript

In JavaScript, the `+` operator is used for both:

- **Numerical addition** (if both operands are numbers)
- **String concatenation** (if either operand is a string)

## 📘 Examples & Explanations

| Expression                  | Output                                | Explanation                                                            |
| --------------------------- | ------------------------------------- | ---------------------------------------------------------------------- |
| `2 + 2`                     | `4`                                   | Both operands are numbers → numeric addition                           |
| `"2" + 2`                   | `"22"`                                | String + number → number is coerced to string → concatenation          |
| `2 + "2"`                   | `"22"`                                | Number + string → number is coerced to string → concatenation          |
| `1 + 2 + 3 + "2" + "3" + 3` | `"62" + "3" + 3 → "623" + 3 → "6233"` | Left to right: numbers first, then strings make everything concatenate |
| `"2" + 1 + 2`               | `"21"` + 2 → `"212"`                  | First string forces concatenation of all following values              |

</div>

</br>

# Lecture 8

### Q1. Null behave in comparison and equality checks

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# `null` Behavior in Comparison and Equality Checks

In JavaScript, `null` behaves differently in equality (`==`) and comparison (`<`, `>`, `>=`, `<=`) operations.

| Expression   | Result  |
| ------------ | ------- |
| `null > 0`   | `false` |
| `null < 0`   | `false` |
| `null === 0` | `false` |
| `null >= 0`  | `true`  |
| `null <= 0`  | `true`  |
| `null == 0`  | `false` |
| `null != 0`  | `true`  |

## 🧠 Important Notes

- In relational comparisons (`<`, `>`, `>=`, `<=`), `null` is **converted to a number** (`0`).
- In loose equality (`==`), `null` is **only equal to `undefined`**, and not to `0` or any number.
- Always use `===` for safer comparisons.

</div>

</br>

# Lecture 9

### Q1. Call by value vs call by reference

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

# 📚 Call by Value vs Call by Reference

## 🔢 Call by Value (Primitives)

- Data types: `Number`, `String`, `Boolean`, `null`, `undefined`, `Symbol`, `BigInt`
- A **copy** of the value is passed
- Changes inside the function **do not affect** the original

### Example:

```js
function modifyValue(x) {
  x = x + 10;
  console.log("Inside function:", x);
}

let num = 5;
modifyValue(num); // Inside function: 15
console.log("Outside:", num); // Outside: 5
```

## 📦 Call by Reference (for Non-Primitive Types)

Data types: Object, Array, Function

- A reference to the original value is passed to the function.
- Changes inside the function do affect the original variable.

### Example:

```js
function modifyObject(obj) {
  obj.name = "Hitesh";
}

let user = { name: "Ravi" };
modifyObject(user);
console.log(user.name); // Hitesh
```

</div>

---

### Q2. Is JS dynamically typed or statically typed?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

- **JavaScript is a dynamically typed language.**
- You **do not need to declare variable types** explicitly.
- The type of a variable is **determined at runtime** based on the value assigned.
- A single variable can store **different types of values** at different times.

</div>
</br>

# Lecture 10

### Q1. Stack memory vs Heap memory

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

### 📝 Stack vs Heap Memory – Description Table

| **Aspect**              | **Stack Memory**                                  | **Heap Memory**                                   |
| ----------------------- | ------------------------------------------------- | ------------------------------------------------- |
| **Used For**            | Primitive data types, function calls              | Non-primitive data types (objects, arrays, etc.)  |
| **Storage**             | Direct value storage                              | Reference stored in stack, actual data in heap    |
| **Speed**               | Fast (LIFO structure)                             | Slower (needs reference lookup)                   |
| **Memory Size**         | Small                                             | Large                                             |
| **Management**          | Automatic (by system/compiler)                    | Manual or by Garbage Collector (e.g., in Java/JS) |
| **Lifetime**            | Ends when function/method ends                    | Persists until explicitly deleted or unreferenced |
| **Example (Primitive)** | `let a = 10;` (value `10` stored in stack)        | N/A                                               |
| **Example (Object)**    | `let obj = {name: "Hitesh"}` (reference in stack) | `{name: "Hitesh"}` stored in heap                 |

</div>

</br>

# Lecture 11

### Q1. If I declare a string like `const str = new String("Hello")` in JavaScript, where is it stored in memory? And how is it different from `const str = "Hello"`?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

In JavaScript:

#### 📌 `const str = new String("Hello")`

- This creates a **String object**, not a primitive string.
- **Memory storage**:
  - The **reference `str`** is stored in the **stack**.
  - The **actual object** (containing the string `"Hello"`) is stored in the **heap**.

#### 📌 `const str = "Hello"`

- This creates a **primitive string**.
- The primitive value is stored **directly in the stack** (or in a shared internal string pool, depending on the JS engine).

#### ⚠️ Key Difference:

- `typeof "Hello"` → `"string"` (primitive)
- `typeof new String("Hello")` → `"object"` (boxed object)
- `new String("Hello") !== "Hello"` → `true` (different types)

</div>

---

### Q2. Why do string methods in JavaScript not change the original string?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

Because **strings in JavaScript are immutable**.  
This means that once a string is created, it **cannot be changed**.

When you call a method like `.toUpperCase()`, `.replace()`, or `.slice()`:

- JavaScript creates a **new string** with the requested change.
- The **original string remains unchanged**.
- And all string methods in JavaScript are functions that **return a new string** and **do not modify the original string**.

</div>

---

### Q3. Javascript String Methods

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

### 📚 JavaScript String Methods: Functions, Uses & Examples

| Method                      | Use / Description                                     | Example                                         |
| --------------------------- | ----------------------------------------------------- | ----------------------------------------------- |
| `toLocaleUpperCase()`       | Converts to uppercase (locale-aware)                  | `"hello".toLocaleUpperCase()` → `"HELLO"`       |
| `toLocaleLowerCase()`       | Converts to lowercase (locale-aware)                  | `"HELLO".toLocaleLowerCase()` → `"hello"`       |
| `toLowerCase()`             | Converts string to lowercase                          | `"JS".toLowerCase()` → `"js"`                   |
| `toUpperCase()`             | Converts string to uppercase                          | `"js".toUpperCase()` → `"JS"`                   |
| `length`                    | Returns the length of the string                      | `"hello".length` → `5`                          |
| `slice(start, end)`         | Extracts part of a string                             | `"abcdef".slice(1, 4)` → `"bcd"`                |
| `substring(start, end)`     | Similar to slice, but doesn't accept negative indices | `"abcdef".substring(1, 4)` → `"bcd"`            |
| `charAt(index)`             | Returns the character at a given index                | `"hello".charAt(1)` → `"e"`                     |
| `charCodeAt(index)`         | Returns the UTF-16 code of character at index         | `"A".charCodeAt(0)` → `65`                      |
| `indexOf(search, start)`    | Returns first index of match or `-1`                  | `"banana".indexOf("a")` → `1`                   |
| `trim()`                    | Removes whitespace from both ends                     | `"  test  ".trim()` → `"test"`                  |
| `trimStart()`               | Removes whitespace from start only                    | `"  test".trimStart()` → `"test"`               |
| `trimEnd()`                 | Removes whitespace from end only                      | `"test  ".trimEnd()` → `"test"`                 |
| `replace(search, value)`    | Replaces first occurrence                             | `"hi hi".replace("hi", "bye")` → `"bye hi"`     |
| `replaceAll(search, value)` | Replaces all occurrences                              | `"hi hi".replaceAll("hi", "bye")` → `"bye bye"` |
| `includes(search, start)`   | Checks if string contains substring                   | `"apple".includes("p")` → `true`                |
| `split(separator)`          | Splits string into array by separator                 | `"a,b,c".split(",")` → `["a", "b", "c"]`        |
| `concat(str1, str2)`        | Joins strings together                                | `"Hi".concat(" there")` → `"Hi there"`          |
| `padStart(length, padStr)`  | Pads string at the start to reach target length       | `"5".padStart(3, "0")` → `"005"`                |
| `padEnd(length, padStr)`    | Pads string at the end to reach target length         | `"5".padEnd(3, "0")` → `"500"`                  |
| `strike()`                  | Deprecated; wraps text in `<strike>` HTML tag         | `"Hello".strike()` → `"<strike>Hello</strike>"` |

</div>

</br>

# Lecture 12

### Q1. Number methods in JavaScript

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 📊 Number Methods and Properties Table

| Method / Property         | Description                                                                | Example                                | Output                    |
| ------------------------- | -------------------------------------------------------------------------- | -------------------------------------- | ------------------------- |
| `toString()`              | Converts a number to a string.                                             | `(123).toString()`                     | `"123"`                   |
| `toFixed(n)`              | Formats a number using fixed-point notation with `n` digits after decimal. | `(5.6789).toFixed(2)`                  | `"5.68"`                  |
| `toPrecision(n)`          | Formats a number to `n` significant digits.                                | `(5.6789).toPrecision(3)`              | `"5.68"`                  |
| `toLocaleString()`        | Converts a number to a locale-sensitive string representation.             | `(1234567.89).toLocaleString("en-IN")` | `"12,34,567.89"`          |
| `Number.MAX_VALUE`        | Returns the largest possible number in JS.                                 | `Number.MAX_VALUE`                     | `1.7976931348623157e+308` |
| `Number.MIN_VALUE`        | Returns the smallest positive number (closest to 0, not most negative).    | `Number.MIN_VALUE`                     | `5e-324`                  |
| `Number.MAX_SAFE_INTEGER` | Largest integer accurately represented in JS.                              | `Number.MAX_SAFE_INTEGER`              | `9007199254740991`        |
| `Number.MIN_SAFE_INTEGER` | Smallest integer accurately represented in JS.                             | `Number.MIN_SAFE_INTEGER`              | `-9007199254740991`       |
| `Number.isNaN(x)`         | Determines whether the passed value is NaN and of type Number.             | `Number.isNaN("abc"/2)`                | `true`                    |
| `Number.isFinite(x)`      | Checks if the value is a finite number.                                    | `Number.isFinite(100)`                 | `true`                    |
| `Number.isInteger(x)`     | Checks if the value is an integer.                                         | `Number.isInteger(10.5)`               | `false`                   |
| `Number.parseInt(x)`      | Parses a string and returns an integer.                                    | `Number.parseInt("123abc")`            | `123`                     |
| `Number.parseFloat(x)`    | Parses a string and returns a floating-point number.                       | `Number.parseFloat("123.45abc")`       | `123.45`                  |
| `Number()`                | Converts a value to a number.                                              | `Number("123")`                        | `123`                     |
| `isNaN(x)`                | Global function that checks if a value is NaN.                             | `isNaN("hello")`                       | `true`                    |
| `isFinite(x)`             | Global function that checks if a value is finite.                          | `isFinite(1/0)`                        | `false`                   |

</div>

---

### Q2. Math Object

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 📊 Math Methods and Examples

| Method                | Description                                                    | Example                 | Output           |
| --------------------- | -------------------------------------------------------------- | ----------------------- | ---------------- |
| `Math.abs(x)`         | Returns the absolute (positive) value of a number              | `Math.abs(-7.25)`       | `7.25`           |
| `Math.round(x)`       | Rounds a number to the nearest integer                         | `Math.round(4.7)`       | `5`              |
| `Math.ceil(x)`        | Rounds a number **up** to the nearest integer                  | `Math.ceil(4.2)`        | `5`              |
| `Math.floor(x)`       | Rounds a number **down** to the nearest integer                | `Math.floor(4.9)`       | `4`              |
| `Math.sqrt(x)`        | Returns the square root of a number                            | `Math.sqrt(16)`         | `4`              |
| `Math.pow(x, y)`      | Returns the value of `x` raised to the power `y`               | `Math.pow(2, 3)`        | `8`              |
| `Math.min(a, b, ...)` | Returns the lowest-valued number in a list                     | `Math.min(5, 2, 8, -1)` | `-1`             |
| `Math.max(a, b, ...)` | Returns the highest-valued number in a list                    | `Math.max(5, 2, 8, -1)` | `8`              |
| `Math.random()`       | Returns a random float between 0 (inclusive) and 1 (exclusive) | `Math.random()`         | `0.0 - 0.999...` |
| `Math.log(x)`         | Returns the natural logarithm (base e) of a number             | `Math.log(Math.E)`      | `1`              |
| `Math.log10(x)`       | Returns the base-10 logarithm of a number                      | `Math.log10(100)`       | `2`              |
| `Math.log2(x)`        | Returns the base-2 logarithm of a number                       | `Math.log2(8)`          | `3`              |
| `Math.exp(x)`         | Returns e^x (Euler’s number to the power of x)                 | `Math.exp(1)`           | `2.718...`       |
| `Math.PI`             | Returns the value of PI                                        | `Math.PI`               | `3.14159...`     |

</div>

---

### Q3. Generation random number in the range

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

```js
Math.floor(Math.random() * (max - min + 1)) + min;
```

</div>

</br>

# Lecture 13

### Q1. Date Object

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## ✅ 1. Creating Dates

```js
new Date(); // Current date and time
new Date(0); // Jan 1, 1970
new Date("2025-06-10"); // Parses string to date
new Date(2025, 5, 10, 12, 30); // June 10, 2025, 12:30 PM (month is 0-indexed)
```

## ✅ 2. Date Get Methods

```js
date.getFullYear(); // Returns 4-digit year
date.getMonth(); // Month (0–11)
date.getDate(); // Day of the month (1–31)
date.getDay(); // Day of the week (0–6, Sun = 0)
date.getHours(); // Hour (0–23)
date.getMinutes(); // Minutes (0–59)
date.getSeconds(); // Seconds (0–59)
date.getMilliseconds(); // Milliseconds (0–999)
date.getTime(); // Milliseconds since Jan 1, 1970
date.getTimezoneOffset(); // Timezone difference in minutes
```

## ✅ 3. Date Set Methods

```js
date.setFullYear(2026); // Set full year
date.setMonth(6); // Set month (July = 6)
date.setDate(15); // Set day of the month
date.setHours(10); // Set hours
date.setMinutes(45); // Set minutes
date.setSeconds(30); // Set seconds
date.setMilliseconds(500); // Set milliseconds
date.setTime(1672531200000); // Set time in milliseconds
```

## ✅ 4. Date Formatting Methods

```js
date.toString(); // Full date and time string
date.toDateString(); // Date only (e.g., "Tue Jun 10 2025")
date.toTimeString(); // Time only (e.g., "19:00:00 GMT+0530")
date.toISOString(); // ISO format (e.g., "2025-06-10T13:30:00.000Z")
date.toUTCString(); // UTC format
date.toLocaleString(); // Locale date and time
date.toLocaleDateString(); // Locale date only
date.toLocaleTimeString(); // Locale time only
```

</div>

---

### Q2. Genral questions about Date Object

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 1. What Is a Timestamp?

- A **timestamp** is the number of **milliseconds since the Unix Epoch** (Jan 1, 1970 UTC).
- In JavaScript, `Date` objects internally store time as timestamps.

---

## 2. Getting the Current Timestamp

- Use `Date.now()` to get the current timestamp:

```js
const now = Date.now(); // milliseconds since Jan 1, 1970
```

## 3. Convert Date to Timestamp

- Use .getTime() on a Date object:

```js
const date = new Date("2025-06-10");
const timestamp = date.getTime(); // returns milliseconds
```

## 4. Convert Timestamp to Date

- Pass the timestamp to the Date constructor:

```js
const timestamp = 1750000000000;
const date = new Date(timestamp);
```

## 5. Adding or Subtracting Time

- Timestamps are in milliseconds, so you can add/subtract time directly:

```
1 second = 1000 ms
1 minute = 60 * 1000 ms
1 hour   = 60 * 60 * 1000 ms
```

```js
const now = Date.now();
const oneHourLater = now + 60 * 60 * 1000; // add 1 hour
const oneDayEarlier = now - 24 * 60 * 60 * 1000; // subtract 1 day
```

## 6. Calculating Differences Between Dates

- Subtract timestamps to find duration:

```js
const start = new Date("2025-06-10T00:00:00").getTime();
const end = new Date("2025-06-12T00:00:00").getTime();
const diff = end - start; // in ms
const days = diff / (1000 * 60 * 60 * 24); // in days
```

## 7. Converting Milliseconds to Human Units

```js
function msToTime(duration) {
  const seconds = Math.floor((duration / 1000) % 60);
  const minutes = Math.floor((duration / (1000 * 60)) % 60);
  const hours = Math.floor((duration / (1000 * 60 * 60)) % 24);
  const days = Math.floor(duration / (1000 * 60 * 60 * 24));

  return `${days}d ${hours}h ${minutes}m ${seconds}s`;
}

console.log(msToTime(172800000)); // Output: 2d 0h 0m 0s
```

</div>
</br>

# Lecture 14

### Q1. Array Declaration

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

```js
// Using square brackets
let arr1 = [1, 2, 3];

// Using Array constructor
let arr2 = new Array(1, 2, 3);

// Empty array
let empty = [];
```

</div>

---

### Q2. Array Methods

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

| Method     | What It Does                                                 | What It Returns               | Changes Original Array? | Example                                                                |
| ---------- | ------------------------------------------------------------ | ----------------------------- | ----------------------- | ---------------------------------------------------------------------- |
| push()     | Adds item(s) to the end of the array                         | New length of the array       | Yes                     | `[1, 2].push(3)` → returns `3`, array becomes `[1, 2, 3]`              |
| pop()      | Removes the last item                                        | The removed last item         | Yes                     | `[1, 2, 3].pop()` → returns `3`, array becomes `[1, 2]`                |
| unshift()  | Adds item(s) to the beginning                                | New length of the array       | Yes                     | `[1, 2].unshift(0)` → returns `3`, array becomes `[0, 1, 2]`           |
| shift()    | Removes the first item                                       | The removed first item        | Yes                     | `[1, 2, 3].shift()` → returns `1`, array becomes `[2, 3]`              |
| splice()   | Adds/removes/replaces elements                               | An array of removed items     | Yes                     | `[1, 2, 3].splice(1, 1, 4)` → returns `[2]`, array becomes `[1, 4, 3]` |
| slice()    | Extracts a section of the array                              | A new array (sliced portion)  | No                      | `[1, 2, 3].slice(1, 3)` → returns `[2, 3]`                             |
| concat()   | Merges arrays                                                | A new array (combined arrays) | No                      | `[1, 2].concat([3, 4])` → returns `[1, 2, 3, 4]`                       |
| join()     | Joins elements into a string                                 | A string of array elements    | No                      | `[1, 2, 3].join("-")` → returns `"1-2-3"`                              |
| toString() | Converts array to string                                     | A string of array elements    | No                      | `[1, 2, 3].toString()` → returns `"1,2,3"`                             |
| includes() | Checks if value is present                                   | `true` or `false`             | No                      | `[1, 2, 3].includes(2)` → returns `true`                               |
| indexOf()  | Gets index of item                                           | Index or `-1` if not found    | No                      | `[1, 2, 3].indexOf(3)` → returns `2`                                   |
| reverse()  | Reverses the array order                                     | The reversed array            | Yes                     | `[1, 2, 3].reverse()` → returns `[3, 2, 1]`                            |
| sort()     | Sorts the array                                              | The sorted array              | Yes                     | `[3, 1, 2].sort()` → returns `[1, 2, 3]`                               |
| find()     | Finds first matching element                                 | The found item or `undefined` | No                      | `[1, 2, 3].find(x => x > 1)` → returns `2`                             |
| flat()     | Flattens nested arrays (can give the degree of nesting also) | A new flattened array         | No                      | `[1, [2, 3]].flat()` → returns `[1, 2, 3]`                             |

</div>

---

### Q3. Shallow Copy vs Deep Copy

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 🧬 Shallow Copy

- Copies **only the top-level properties** of an object or array.
- **Nested objects or arrays are still shared (referenced)**.
- Changes to nested values affect both original and copy.

### ✅ Example:

```js
let original = {
  name: "Alice",
  address: {
    city: "New York",
  },
};

let shallowCopy = { ...original }; // Shallow copy
shallowCopy.address.city = "London";

console.log(original.address.city); // "London" → affected
```

## 🧬 Deep Copy

- Creates a **completely independent copy**, including all nested objects/arrays.
- Changes in the copy do **not affect** the original.

### ✅ Example:

```js
let original = {
  name: "Alice",
  address: {
    city: "New York",
  },
};

let deepCopy = JSON.parse(JSON.stringify(original));
deepCopy.address.city = "London";

console.log(original.address.city); // "New York" → unaffected
```

---

## 🧠 Reference Assignment (Not a Copy)

When you do:

```js
let obj2 = obj1;
```

- `obj2` and `obj1` point to the **same object in memory**.
- Any changes to `obj2` will affect `obj1`.

### ✅ Example:

```js
let employee = {
  name: "Jack",
  salary: 50000,
};

let newEmployee = employee; // Reference assignment
newEmployee.name = "Beck";

console.log(employee.name); // "Beck" → changed
```

### 🧠 Why it happens:

Because `newEmployee` is just another name for the same object. No actual copying is done.

---

## 📦 Shallow Copy with Spread Operator

```js
let obj2 = { ...obj1 };
```

- Creates a **shallow copy**.
- Top-level values (like strings, numbers) are copied.
- Nested objects/arrays are **still shared**.

### ✅ Example:

```js
let obj1 = {
  name: "Alice",
  details: {
    city: "Paris",
  },
};

let obj2 = { ...obj1 };
obj2.name = "Bob"; // Doesn't affect obj1
obj2.details.city = "London"; // Affects obj1

console.log(obj1);
// { name: "Alice", details: { city: "London" } }
```

---

## 🧾 Array Copy Operations Create Shallow Copies

When copying arrays using:

- `slice()`
- `concat()`
- Spread operator `[...arr]`

These create **shallow copies**, meaning:

- Top-level elements are copied
- **Nested arrays/objects inside the array are still referenced**

### ✅ Example:

```js
let arr1 = [1, 2, [3, 4]];
let arr2 = [...arr1];

arr2[2][0] = 99;

console.log(arr1); // [1, 2, [99, 4]] → original modified
```

---

## 🔚 Conclusion

- Use **shallow copy** (`{...obj}`, `slice()`, `concat()`, `[...arr]`) for flat structures.
- Use **deep copy** (`JSON.parse(JSON.stringify(obj))` or `structuredClone()`) for nested structures.
- **Assignment (`=`)** only shares references — no copy is made.
</div>

---

### Q4. Sorting Arrays

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## ✅ Default Sorting (Lexicographical Order)

```js
let fruits = ["banana", "apple", "cherry"];
fruits.sort();

console.log(fruits); // Output: ["apple", "banana", "cherry"]
```

- ⚠️ Note: .sort() treats all elements as strings by default — even numbers.

## ⚠️ Incorrect Numeric Sort

```js
let numbers = [10, 5, 2, 30];
numbers.sort();

console.log(numbers); // Output: [10, 2, 30, 5] ❌
```

## ✅ Correct Numeric Sort

```js
//Ascending Order
let numbers = [10, 5, 2, 30];
numbers.sort((a, b) => a - b);

console.log(numbers); // Output: [2, 5, 10, 30]

//Descending Order
let numbers = [10, 5, 2, 30];
numbers.sort((a, b) => b - a);

console.log(numbers); // Output: [30, 10, 5, 2]
```

</div>
</br>

# Lecture 15

### Q1. Spread Operator

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

The **spread operator (`...`)** allows you to "spread" the elements of an array or properties of an object into another array or object.

```js
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];

// Using spread operator
let arr3 = [...arr1, ...arr2];

console.log(arr3); // Output: [1, 2, 3, 4, 5, 6]
```

- ℹ️ Spread creates a shallow copy, not a deep one.
</div>

---

### Q2. Spread Operator Key Overwriting Behavior

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

### 🧠 Spread Operator – Key Overwriting Behavior

When using the **spread operator** (`...`) to merge objects, if there are **common/shared keys**, the **last object in the spread order** will **override** the previous values.

---

#### 📌 Example:

```js
const obj1 = { a: 1 };
const obj2 = { b: 2, a: 3 };

const mergedObj = { ...obj2, ...obj1 };

console.log(mergedObj); // { b: 2, a: 1 }
```

</div>

---

### Q3. Array Static Methods

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

### JavaScript provides several static methods to create or check arrays. Here's a summary of three important ones:

## 🔹 Array.isArray()

### ✅ Purpose:

Determines whether a given value is an array.

`Array.isArray(value)`

```js
Array.isArray([1, 2, 3]); // true
Array.isArray("hello"); // false
Array.isArray({}); // false
```

🔍 Returns:

- true if the value is an array
- false otherwise

## 🔹 Array.from()

### ✅ Purpose:

Creates a new array instance from an array-like or iterable object, such as a string, Set, or NodeList.

`Array.from(arrayLike, mapFn, thisArg)`

```js
Array.from("hello"); // ['h', 'e', 'l', 'l', 'o']

// With mapping function
Array.from([1, 2, 3], (x) => x * 2); // [2, 4, 6]
```

🔍 Returns:

- A new array instance from the provided input.

## 🔹 Array.of()

### ✅ Purpose:

Creates a new array with the passed arguments as elements, regardless of their number or type.

`Array.of(element0, element1, ..., elementN)`

```js
Array.of(7); // [7]
Array.of(1, 2, 3); // [1, 2, 3]

Array(7); // Creates an empty array of length 7 (not the same as [7])
```

🔍 Returns:

- A new array with the specified elements.
</div>
</br>

# Lecture 16

### Q1. Object Literal Declaration vs Object Constructor Declaration

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

## 🔹Using Object Literal
The simplest and most common way to create an object.

```js
const person = {
  name: "Alice",
  age: 25,
  greet: function() {
    console.log(`Hello, I'm ${this.name}`);
  }
};

person.greet(); // Hello, I'm Alice
```
## 🔹Using Object Constructor

Using the Object constructor or custom constructors (functions or classes).

### a) Built-in Object constructor:
```js
const person = new Object();
person.name = "Bob";
person.age = 30;
person.greet = function() {
  console.log(`Hello, I'm ${this.name}`);
};

person.greet(); // Hello, I'm Bob
```
### b) Custom constructor function:
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.greet = function() {
    console.log(`Hello, I'm ${this.name}`);
  };
}

const person1 = new Person("Charlie", 35);
person1.greet(); // Hello, I'm Charlie
```
</div>  

---

### Q2. What is a Singleton Object?

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

A **singleton object** in JavaScript is an object that is created only once and used globally throughout your code. It ensures that there is only one instance of that object during the application's lifecycle.
</div>

---

### Q3. Object Access 

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">
JavaScript allows you to access object properties in two ways:

## ✅ 1. Dot Notation (`.`)

- Used when you know the exact property name.
- Cleaner and more readable.
- Property name must be a valid identifier (no spaces, special characters, etc.)

### Example:
```js
const person = {
  name: "Alice",
  age: 25
};

console.log(person.name); // Output: Alice
console.log(person.age);  // Output: 25
```

## ✅ 2. Bracket Notation ([])
- Used when the property name is stored in a variable or includes special characters or spaces.
- Property name must be a string or expression that resolves to a string.
### Example:
```js
const person = {
  name: "Alice",
  "favorite color": "blue"
};

console.log(person["name"]);             // Output: Alice
console.log(person["favorite color"]);   // Output: blue

const key = "name";
console.log(person[key]); // Output: Alice
```
</div>

---

### Q4. Symbol as a key in Object

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

```js
const symKey = Symbol("userId");

const user = {
  name: "Alice",
  [symKey]: 12345
};

console.log(user.name);         // "Alice"
console.log(user[symKey]);      // 12345
```
</div>

---

### Q5. Object Methods 

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

| Method                        | Changes Original? | What It Returns                 | What It Does                                                                 | 🧪 Example                                                                 |
|------------------------------|-------------------|----------------------------------|------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `Object.keys(obj)`           | ❌ No             | Array of keys                    | Returns an array of all **enumerable property names**                        | `Object.keys({a:1, b:2})` → `["a", "b"]`                                   |
| `Object.values(obj)`         | ❌ No             | Array of values                  | Returns an array of all **enumerable property values**                       | `Object.values({a:1, b:2})` → `[1, 2]`                                     |
| `Object.entries(obj)`        | ❌ No             | Array of `[key, value]` pairs    | Returns an array of **[key, value] pairs**                                   | `Object.entries({a:1, b:2})` → `[["a", 1], ["b", 2]]`                      |
| `Object.assign(target, src)` | ✅ Yes (if target) | Modified target object           | Copies properties from source to target and returns updated target           | `Object.assign({x:1}, {y:2})` → `{x:1, y:2}`                               |
| `Object.freeze(obj)`         | ✅ Yes (locks it)  | The frozen object                | Prevents **adding, removing, or changing** any properties                    | `let a = Object.freeze({x:10}); a.x = 5;` → `x` stays `10`                |
| `Object.seal(obj)`           | ✅ Yes (locks shape)| The sealed object               | Prevents adding/removing props, **but allows modifying existing ones**       | `let a = Object.seal({x:10}); a.x = 20;` → valid, but can't add `a.y = 5` |
| `obj.hasOwnProperty(key)`    | ❌ No             | Boolean (`true` / `false`)       | Checks if the object has the property directly (not via prototype chain)     | `{a:1}.hasOwnProperty("a")` → `true`                                      |
</div>

---

### Q6. this keyword in the object

<div style="background-color:black; color:white; padding: 10px; border-radius: 5px;">

The `this` keyword refers to the **object that is calling the function**.

When a function is a method of an object, `this` refers to the object itself.

---


```js
const person = {
  name: "Alice",
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

person.greet(); // Output: Hello, my name is Alice
```
- Arrow functions do not have their own `this`. They inherit `this` from their surrounding (lexical) scope.
</div>
</br>

# Lecture 17
