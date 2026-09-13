# JavaScript Technical Paper

## 1. Different Data Types in JavaScript

JavaScript has **primitive** and **non-primitive** data types.

### Primitive

```js
let name = "Raghvendra";   // String
let age = 25;              // Number
let isActive = true;       // Boolean
let value;                 // Undefined
let data = null;           // Null
let id = 123n;             // BigInt
let symbol = Symbol("id"); // Symbol
```

### Non-primitive

```js
let numbers = [10, 20, 30];       // Array
let user = { name: "Raghvendra" };// Object
function greet() {}               // Function
```

---

# 2. Scope in JavaScript

Scope determines where a variable can be accessed.

### Global Scope

```js
let name = "John";

function greet() {
    console.log(name);
}
```

### Function Scope

```js
function test() {
    let age = 25;
}

console.log(age); // Error
```

### Block Scope

`let` and `const` are block scoped.

```js
if (true) {
    let x = 10;
    const y = 20;
}

console.log(x); // Error
```

---

# 3. let, var, const

```js
let age = 25;
age = 26;        // Allowed

const name = "John";
// name = "Mike"; // Error

var city = "Delhi";
city = "Mumbai"; // Allowed
```

| Keyword | Reassign | Redeclare | Block Scope |
| ------- | -------- | --------- | ----------- |
| `let`   | Yes      | No        | Yes         |
| `const` | No       | No        | Yes         |
| `var`   | Yes      | Yes       | No          |

---

# 4. Why We Must Not Use `var`

`var` is function scoped, can be redeclared, and is hoisted in confusing ways.

```js
if (true) {
    var x = 10;
}

console.log(x); // 10
```

With `let`:

```js
if (true) {
    let x = 10;
}

console.log(x); // Error
```

Prefer:

```js
const name = "John";
let age = 25;
```

Use `const` by default and `let` when reassignment is required.

---

# 5. Why Global Variables Are Bad

Global variables can be changed from anywhere and can cause unexpected side effects.

```js
let total = 0;

function add(price) {
    total += price;
}

function reset() {
    total = 0;
}
```

Both functions can modify the same variable.

Prefer local variables:

```js
function calculateTotal(prices) {
    let total = 0;

    for (const price of prices) {
        total += price;
    }

    return total;
}
```

---

# 6. Truthy and Falsy Values

Falsy values:

```js
false
0
-0
0n
""
null
undefined
NaN
```

Everything else is generally truthy.

```js
if ("hello") {
    console.log("Runs");
}

if (0) {
    console.log("Does not run");
}
```

---

# 7. Function Hoisting

Function declarations are hoisted.

```js
greet();

function greet() {
    console.log("Hello");
}
```

This works.

Function expressions are different:

```js
greet(); // Error

const greet = function () {
    console.log("Hello");
};
```

---

# 8. Function Without a Return Statement

A function without `return` returns `undefined`.

```js
function greet() {
    console.log("Hello");
}

const result = greet();

console.log(result); // undefined
```

---

# 9. Different Ways of Declaring Functions

### Function Declaration

```js
function add(a, b) {
    return a + b;
}
```

### Function Expression

```js
const add = function (a, b) {
    return a + b;
};
```

### Arrow Function

```js
const add = (a, b) => {
    return a + b;
};
```

Short arrow function:

```js
const add = (a, b) => a + b;
```

---

# 10. Pass by Value and Reference

JavaScript passes arguments **by value**.

For primitives, the value itself is copied.

```js
let a = 10;

function change(value) {
    value = 20;
}

change(a);

console.log(a); // 10
```

Objects contain a reference value.

```js
const user = {
    name: "John"
};

function change(user) {
    user.name = "Mike";
}

change(user);

console.log(user.name); // Mike
```

The object itself wasn't copied; the reference value was copied.

Reassigning the parameter does not replace the original object:

```js
function change(user) {
    user = { name: "Mike" };
}

change(user);

console.log(user.name); // John
```

---

# 11. Different Types of `for` Loops

### Traditional `for`

Useful when controlling an index/count.

```js
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

### `for...of`

Iterates over values.

```js
const numbers = [10, 20, 30];

for (const number of numbers) {
    console.log(number);
}
```

### `for...in`

Iterates over object keys.

```js
const user = {
    name: "John",
    age: 25
};

for (const key in user) {
    console.log(key, user[key]);
}
```

Avoid `for...in` for arrays.

### `forEach`

```js
numbers.forEach((number) => {
    console.log(number);
});
```

### `while`

```js
let i = 0;

while (i < 5) {
    console.log(i);
    i++;
}
```

---

# 12. Searching MDN

MDN is the primary reference for JavaScript and Web APIs.

Search examples:

```text
MDN Array.map
MDN Array.splice
MDN String.includes
MDN Object.entries
```

Check:

* Syntax
* Parameters
* Return value
* Examples
* Browser/Node compatibility
* Whether the method mutates the original value

[MDN Web Docs](https://developer.mozilla.org/?utm_source=chatgpt.com)

---

# 13. Popular Array Utility Methods

Assume:

```js
const numbers = [1, 2, 3, 4];
```

## `pop()`

Removes the last element.

**Mutable**

```js
numbers.pop();

console.log(numbers); // [1, 2, 3]
```

## `push()`

Adds elements to the end.

**Mutable**

```js
numbers.push(5);

console.log(numbers); // [1, 2, 3, 4, 5]
```

## `concat()`

Combines arrays.

**Immutable**

```js
const result = numbers.concat([5, 6]);

console.log(result);
```

## `slice()`

Returns part of an array.

**Immutable**

```js
const result = numbers.slice(1, 3);

console.log(result); // [2, 3]
```

## `splice()`

Adds/removes elements.

**Mutable**

```js
numbers.splice(1, 2);

console.log(numbers);
```

## `join()`

Converts array elements into a string.

**Immutable**

```js
const result = numbers.join("-");

console.log(result); // "1-2-3-4"
```

## `flat()`

Flattens nested arrays.

**Immutable**

```js
const numbers = [1, [2, 3], [4, [5]]];

console.log(numbers.flat(2));
// [1, 2, 3, 4, 5]
```

---

# 14. Array Finding Methods

## `find()`

Returns the first matching element.

```js
const numbers = [10, 20, 30];

const result = numbers.find(number => number > 15);

console.log(result); // 20
```

## `indexOf()`

Returns the index of a value.

```js
numbers.indexOf(20); // 1
```

## `includes()`

Checks whether a value exists.

```js
numbers.includes(20); // true
```

## `findIndex()`

Returns the index of the first matching element.

```js
numbers.findIndex(number => number > 15); // 1
```

These methods do not mutate the array.

---

# 15. Higher-Order Array Methods

A higher-order function accepts another function as an argument or returns a function.

## `forEach()`

**No new array**

```js
numbers.forEach(number => {
    console.log(number);
});
```

## `filter()`

Creates an array containing matching elements.

**Immutable**

```js
const even = numbers.filter(number => number % 2 === 0);
```

## `map()`

Creates a transformed array.

**Immutable**

```js
const doubled = numbers.map(number => number * 2);
```

## `reduce()`

Reduces an array to one value.

**Immutable**

```js
const total = numbers.reduce(
    (sum, number) => sum + number,
    0
);
```

## `sort()`

Sorts the array.

**Mutable**

```js
numbers.sort((a, b) => a - b);
```

Always provide a comparator for numeric sorting.

---

# 16. Array Method Chaining

Methods can be combined.

```js
const result = numbers
    .filter(number => number > 10)
    .map(number => number * 2)
    .reduce((sum, number) => sum + number, 0);
```

Flow:

```text
filter → map → reduce
```

Keep chains readable rather than creating unnecessarily complex chains.

---

# 17. Popular String Utility Methods

Strings are **immutable** in JavaScript.

```js
const text = "Hello World";
```

### `toUpperCase()`

```js
text.toUpperCase();
// "HELLO WORLD"
```

**Immutable**

### `toLowerCase()`

```js
text.toLowerCase();
```

**Immutable**

### `includes()`

```js
text.includes("World");
// true
```

### `startsWith()`

```js
text.startsWith("Hello");
// true
```

### `endsWith()`

```js
text.endsWith("World");
// true
```

### `indexOf()`

```js
text.indexOf("World");
// 6
```

### `slice()`

```js
text.slice(0, 5);
// "Hello"
```

### `substring()`

```js
text.substring(0, 5);
// "Hello"
```

### `split()`

```js
const words = text.split(" ");

console.log(words);
// ["Hello", "World"]
```

### `trim()`

```js
const name = "  John  ";

name.trim();
// "John"
```

All of these create/return values without modifying the original string.

---

# 18. Popular Object Utility Methods

Assume:

```js
const user = {
    name: "John",
    age: 25
};
```

### `Object.keys()`

```js
Object.keys(user);
// ["name", "age"]
```

### `Object.values()`

```js
Object.values(user);
// ["John", 25]
```

### `Object.entries()`

```js
Object.entries(user);
// [["name", "John"], ["age", 25]]
```

These do not mutate the object.

### `Object.assign()`

**Can mutate the target object**

```js
Object.assign(user, {
    city: "Delhi"
});
```

Safer copy:

```js
const copy = Object.assign({}, user);
```

### Spread

```js
const copy = { ...user };
```

### `Object.fromEntries()`

```js
const entries = [
    ["name", "John"],
    ["age", 25]
];

const user = Object.fromEntries(entries);
```

---

# 19. When to Use `forEach`, `map`, `filter`, `reduce`

### `forEach`

Use when you simply want to perform an action.

```js
users.forEach(user => {
    console.log(user.name);
});
```

### `map`

Use when you want a transformed array.

```js
const names = users.map(user => user.name);
```

### `filter`

Use when you want selected elements.

```js
const adults = users.filter(user => user.age >= 18);
```

### `reduce`

Use when converting an array into one result.

```js
const total = prices.reduce(
    (total, price) => total + price,
    0
);
```

Mental model:

```text
forEach → do something
map     → transform
filter  → select
reduce  → combine
```

---

# 20. Mutable vs Immutable Methods

### Mutable

Changes the original array/object.

```js
push()
pop()
splice()
sort()
reverse()
```

Example:

```js
const numbers = [3, 1, 2];

numbers.sort();

console.log(numbers); // [1, 2, 3]
```

### Immutable

Does not change the original value.

```js
map()
filter()
slice()
concat()
flat()
join()
find()
includes()
```

Example:

```js
const numbers = [1, 2, 3];

const doubled = numbers.map(x => x * 2);

console.log(numbers); // [1, 2, 3]
```

---

# 21. Error Handling — `try...catch`

Use `try...catch` to handle runtime errors.

```js
try {
    JSON.parse("invalid json");
} catch (error) {
    console.error(error.message);
}
```

The program can handle the error instead of unexpectedly terminating.

---

# 22. Throwing Errors

```js
function withdraw(balance, amount) {
    if (amount > balance) {
        throw new Error("Insufficient balance");
    }

    return balance - amount;
}
```

Handle it:

```js
try {
    withdraw(100, 200);
} catch (error) {
    console.error(error.message);
}
```

---

# 23. `throw new Error()` vs `throw "message"`

Prefer:

```js
throw new Error("Something went wrong");
```

Instead of:

```js
throw "Something went wrong";
```

`Error` provides useful properties such as:

```js
error.name
error.message
error.stack
```

Example:

```js
try {
    throw new Error("Invalid age");
} catch (error) {
    console.log(error.name);
    console.log(error.message);
    console.log(error.stack);
}
```

---

# 24. Reading Error Messages and Stack Traces

Example:

```text
TypeError: user.getName is not a function
    at login (/app/user.js:10:15)
    at start (/app/app.js:5:1)
```

Read it from the top:

```text
Error type → TypeError
Message    → user.getName is not a function
File       → user.js
Line       → 10
Column     → 15
```

Then trace the call chain:

```text
start()
  ↓
login()
  ↓
user.getName()
  ↓
ERROR
```

### Daily practice

For 2 weeks:

```text
1. Create a small bug.
2. Run the program.
3. Read the error.
4. Find the file and line.
5. Trace the stack.
6. Explain why it happened.
7. Fix it.
8. Run again.
```

Do not immediately search for the solution. First understand the stack trace.

---

# 25. Importance of the `catch` Block

`catch` gives us access to the error.

```js
try {
    riskyOperation();
} catch (error) {
    console.error(error.message);
}
```

Without handling the error:

```js
try {
    riskyOperation();
}
```

the error can propagate to the caller.

---

# 26. Spread Operator

Spread expands iterable/object values.

### Array

```js
const first = [1, 2];
const second = [3, 4];

const result = [...first, ...second];

console.log(result);
// [1, 2, 3, 4]
```

### Object

```js
const user = {
    name: "John",
    age: 25
};

const updatedUser = {
    ...user,
    city: "Delhi"
};
```

### Function arguments

```js
const numbers = [10, 20, 30];

Math.max(...numbers);
```

---

# 27. Template Literals

Use backticks for strings containing variables or expressions.

```js
const name = "John";
const age = 25;

const message = `My name is ${name} and I am ${age}.`;
```

Multiline:

```js
const message = `
Hello ${name},
Welcome!
`;
```

---

# 28. Default Parameters

Provide a default value when an argument is `undefined`.

```js
function greet(name = "Guest") {
    console.log(`Hello ${name}`);
}

greet();
// Hello Guest

greet("John");
// Hello John
```

---

# 29. Destructuring

Extract values from arrays or objects.

### Object

```js
const user = {
    name: "John",
    age: 25
};

const { name, age } = user;
```

### Array

```js
const numbers = [10, 20, 30];

const [first, second] = numbers;
```

### Function parameter

```js
function greet({ name }) {
    console.log(name);
}

greet({ name: "John" });
```

---

# 30. Closures

A closure occurs when an inner function remembers variables from its outer function.

```js
function counter() {
    let count = 0;

    return function () {
        count++;
        return count;
    };
}

const increment = counter();

console.log(increment()); // 1
console.log(increment()); // 2
console.log(increment()); // 3
```

The inner function still has access to `count`.

---

# 31. Arrow Functions vs Regular Functions

### Syntax

```js
function add(a, b) {
    return a + b;
}

const add = (a, b) => a + b;
```

### `this`

Regular functions get `this` based on how they are called.

Arrow functions don't create their own `this`; they use the surrounding `this`.

```js
const user = {
    name: "John",

    regular() {
        console.log(this.name);
    },

    arrow: () => {
        console.log(this.name);
    }
};
```

For object methods, prefer regular method syntax when you need `this`.

### Constructor

Regular functions can be used with `new`.

```js
function User(name) {
    this.name = name;
}

const user = new User("John");
```

Arrow functions cannot be constructors.

---

# 32. `===` vs `==`

`===` checks value **and type**.

```js
5 === "5";
// false
```

`==` performs type coercion.

```js
5 == "5";
// true
```

Prefer:

```js
===
```

because it avoids unexpected type conversions.

---

# 33. Why `value === undefined` Is Better Than `!value`

`!value` also matches other falsy values.

```js
const value = 0;

if (!value) {
    console.log("Runs");
}
```

But `0` is not undefined.

If we specifically want to check for undefined:

```js
if (value === undefined) {
    console.log("Value is undefined");
}
```

This clearly expresses the intention.

---

# 34. `null` vs `undefined`

### `undefined`

Usually means a value has not been assigned.

```js
let value;

console.log(value);
// undefined
```

### `null`

Usually means an intentional absence of a value.

```js
let user = null;
```

Comparison:

```js
undefined === null;
// false
```

---

# 35. Modules — `require` and `module.exports`

### Export

`math.js`

```js
function add(a, b) {
    return a + b;
}

module.exports = {
    add
};
```

### Import

`app.js`

```js
const { add } = require("./math");

console.log(add(2, 3));
```

Another form:

```js
module.exports = add;
```

Then:

```js
const add = require("./math");
```

Modules help separate code into reusable files.

---

# 36. Console Methods

### `console.log()`

General information.

```js
console.log("Hello");
```

### `console.error()`

Errors.

```js
console.error("Something failed");
```

### `console.warn()`

Warnings.

```js
console.warn("Deprecated method");
```

### `console.info()`

Information.

```js
console.info("Server started");
```

### `console.table()`

Useful for arrays/objects.

```js
console.table([
    { name: "John", age: 25 },
    { name: "Mike", age: 30 }
]);
```

### `console.dir()`

Useful for inspecting objects.

```js
console.dir(user);
```

### `console.time()` / `console.timeEnd()`

Measure execution time.

```js
console.time("loop");

for (let i = 0; i < 100000; i++) {}

console.timeEnd("loop");
```

---

# 37. JavaScript Best Practices

### Indentation

```js
if (age >= 18) {
    console.log("Adult");
}
```

### Meaningful variable names

Bad:

```js
let x = 100;
```

Good:

```js
let totalPrice = 100;
```

### Loop variable names

Bad:

```js
for (const x of users) {}
```

Good:

```js
for (const user of users) {}
```

### Prefer `const`

```js
const name = "John";
let age = 25;
```

### Small functions

Bad:

```js
function processEverything() {
    // hundreds of lines
}
```

Prefer:

```js
function validateUser() {}
function calculateTotal() {}
function saveUser() {}
```

### Avoid unnecessary nesting

Prefer early returns:

```js
function login(user) {
    if (!user) {
        return;
    }

    if (!user.isActive) {
        return;
    }

    // login
}
```

### Avoid magic values

Bad:

```js
if (age > 18) {}
```

Better when reused:

```js
const ADULT_AGE = 18;

if (age >= ADULT_AGE) {}
```

### Use strict equality

```js
if (age === 18) {}
```

### Keep one responsibility per function

```js
function calculateTotal(items) {
    return items.reduce((total, item) => total + item.price, 0);
}
```

---

# 38. Passing Functions to Other Functions

Functions can be passed as values.

```js
function greet(name) {
    console.log(`Hello ${name}`);
}

function execute(callback) {
    callback("John");
}

execute(greet);
```

Here:

```js
execute(greet);
```

passes the function.

```js
callback("John");
```

invokes it.

Do not do this when you want to pass the function itself:

```js
execute(greet());
```

because `greet()` executes immediately.

---

# 39. Named vs Anonymous Functions

### Named

```js
function calculateTotal() {
    return 100;
}
```

The function has a name.

Useful for debugging and stack traces.

### Anonymous

```js
const calculateTotal = function () {
    return 100;
};
```

The function itself has no explicit name.

Commonly used as callbacks:

```js
numbers.forEach(function (number) {
    console.log(number);
});
```

Arrow functions are also commonly used as callbacks:

```js
numbers.forEach(number => {
    console.log(number);
});
```

---

# 40. Variable Number of Arguments

Use rest parameters.

```js
function sum(...numbers) {
    return numbers.reduce(
        (total, number) => total + number,
        0
    );
}

console.log(sum(1, 2, 3));
console.log(sum(10, 20, 30, 40));
```

`numbers` becomes an array.

```js
function show(first, ...rest) {
    console.log(first);
    console.log(rest);
}

show(10, 20, 30, 40);

// first → 10
// rest  → [20, 30, 40]
```

---

# 41. Debugging Strategies

## 1. Read the Error First

Do not immediately change code.

```text
Error type
↓
Error message
↓
File
↓
Line
↓
Call stack
```

## 2. Reproduce the Bug

Create the smallest input that causes the problem.

```js
const result = calculateTotal([]);
console.log(result);
```

## 3. Use `console.log`

```js
console.log("input:", input);
console.log("result:", result);
```

## 4. Inspect Types

```js
console.log(typeof value);
```

Especially useful for:

```js
"10" // string
10   // number
```

## 5. Use Breakpoints

Pause execution and inspect:

```text
variables
call stack
scope
values
```

## 6. Check Assumptions

Instead of assuming:

```js
user.name
```

inspect:

```js
console.log(user);
```

## 7. Trace Data Flow

```text
input
  ↓
validation
  ↓
transformation
  ↓
calculation
  ↓
output
```

Find where the value first becomes incorrect.

## 8. Change One Thing at a Time

Bad debugging:

```text
change 10 lines → run → still broken
```

Better:

```text
hypothesis → one change → run → observe
```

## 9. Use Stack Traces

```text
app.js
  ↓
service.js
  ↓
calculator.js
  ↓
ERROR
```

Start at the error and move upward through the call stack.

## 10. Verify the Fix

After fixing:

```text
normal input
edge case
invalid input
empty input
```

should all be tested.

---

# Quick Revision

```text
const          → default variable choice
let            → reassignment required
var            → avoid
===            → strict comparison
==             → type coercion
undefined      → value not assigned
null           → intentional absence
map()          → transform
filter()       → select
reduce()       → combine
forEach()      → perform an action
for...of       → iterate values
for...in       → iterate object keys
push/pop       → mutable
splice/sort    → mutable
slice/map      → immutable
...            → spread/rest
`${value}`     → template literal
try/catch      → handle errors
throw new Error→ create proper error
require        → import CommonJS module
module.exports → export CommonJS module
```

# Daily Practice

For debugging practice, spend **2 weeks** creating and fixing small JavaScript bugs.

Each day:

```text
1. Write a small program.
2. Introduce one bug.
3. Run it.
4. Read the complete error message.
5. Locate the file and line.
6. Read the stack trace.
7. Explain the root cause.
8. Fix it.
9. Test the fix.
10. Repeat with another bug.
```

The goal is not just to fix errors, but to become comfortable **reading errors and tracing how execution reached the failure**.
