# ECMASCRIPT.md

# ECMAScript — Interview Preparation Guide

> **Goal:** Understand what ECMAScript actually is, how JavaScript relates to it, how the language evolves, and the core concepts that are commonly tested in interviews.

---

## 1. What is ECMAScript?

### Short interview answer

**ECMAScript is the standardized specification that defines the core language features of JavaScript. JavaScript is an implementation of ECMAScript, along with additional host APIs provided by environments such as browsers and Node.js.**

The important distinction is:

```text
ECMAScript
   │
   ├── Defines the language
   │     ├── Variables
   │     ├── Data types
   │     ├── Operators
   │     ├── Functions
   │     ├── Objects
   │     ├── Classes
   │     ├── Promises
   │     ├── Modules
   │     └── etc.
   │
   ├── JavaScript engines implement it
   │     ├── V8
   │     ├── SpiderMonkey
   │     └── JavaScriptCore
   │
   └── Host environments add APIs
         ├── Browser → DOM, fetch, localStorage
         └── Node.js → fs, process, Buffer
```

### ECMAScript vs JavaScript

These terms are related but not identical.

**ECMAScript** is the language specification.

**JavaScript** is the programming language commonly used to refer to implementations of that specification, plus environment-specific capabilities.

For example:

```javascript
let x = 10;
const user = { name: "Abhi" };

console.log(user.name);
```

The language constructs such as `let`, `const`, objects, property access, and `console` do not all belong to exactly the same layer.

`let`, `const`, objects, and property access are ECMAScript language features.

`console` is generally supplied by the host/runtime rather than being the fundamental ECMAScript language itself.

### Browser JavaScript is more than ECMAScript

A browser provides:

```text
Browser
├── ECMAScript
├── DOM API
├── BOM
├── Web APIs
└── JavaScript Engine
```

Examples of browser APIs:

```javascript
document.querySelector("#app");
window.alert("Hello");
fetch("/api/users");
localStorage.setItem("theme", "dark");
```

These APIs are not simply "ECMAScript syntax". They are capabilities exposed by the browser environment.

Similarly, Node.js provides APIs such as:

```javascript
const fs = require("fs");

fs.readFile("data.txt", "utf8", callback);
```

`fs` is a Node.js API, not a core ECMAScript feature.

---

# 2. Why is it called ECMAScript?

JavaScript was originally created by Netscape. JavaScript was later standardized through **Ecma International**.

The standardized language specification became known as **ECMAScript**.

The name "JavaScript" itself is associated with trademark history, while ECMAScript became the formal standardized name.

For interviews, remember:

```text
JavaScript → practical language name
ECMAScript → standardized language specification
```

Do not say:

> "ECMAScript and JavaScript are completely different languages."

That is incorrect.

A better answer:

> "ECMAScript defines the standardized core language, while JavaScript is the common name for implementations of that language, usually together with environment-specific APIs."

---

# 3. ECMAScript Versions

ECMAScript has evolved through standardized editions.

Important versions:

| Version | Year | Important Features |
|---|---:|---|
| ES1 | 1997 | First edition |
| ES3 | 1999 | Major early standard |
| ES5 | 2009 | Strict mode, JSON, array methods |
| ES6 / ES2015 | 2015 | Major modernization |
| ES2016 | 2016 | `Array.prototype.includes`, exponentiation |
| ES2017 | 2017 | `async/await` |
| ES2018 | 2018 | Object spread/rest, async iteration |
| ES2019 | 2019 | `flat`, `flatMap`, optional improvements |
| ES2020 | 2020 | Optional chaining, nullish coalescing, BigInt, modules improvements |
| ES2021 | 2021 | Logical assignment operators, `replaceAll` |
| ES2022 | 2022 | Class fields, private fields, top-level `await` |
| ES2023 | 2023 | `findLast`, `findLastIndex`, array copy methods |
| ES2024 | 2024 | New language/platform improvements |
| ES2025+ | 2025 onward | Continued annual standardization |

### The most important version: ES6

**ES6**, also called **ES2015**, was one of the largest updates to JavaScript.

It introduced or standardized many features that are now fundamental:

```javascript
let
const
arrow functions
classes
template literals
destructuring
default parameters
rest parameters
spread syntax
Map
Set
Promises
modules
Symbols
generators
```

Interviewers frequently use "ES6" as shorthand for modern JavaScript fundamentals.

---

# 4. ECMAScript Specification

ECMAScript is not simply a list of syntax examples.

It is a formal specification describing how the language behaves.

The specification defines concepts such as:

- lexical grammar
- syntax
- execution contexts
- environments
- values
- types
- objects
- functions
- operators
- statements
- modules
- asynchronous mechanisms
- iteration
- promises

A useful mental model is:

```text
Source Code
    ↓
Lexing / Parsing
    ↓
ECMAScript semantics
    ↓
JavaScript Engine
    ↓
Execution
```

The specification tells an engine **what behavior should occur**.

The engine decides **how to implement that behavior efficiently**.

For example, two engines may internally implement objects differently while still producing behavior consistent with the ECMAScript specification.

---

# 5. JavaScript Engine

A JavaScript engine executes JavaScript code.

Common engines include:

| Engine | Used by |
|---|---|
| V8 | Chrome, Node.js, Deno |
| SpiderMonkey | Firefox |
| JavaScriptCore | Safari |
| Chakra | Historically used by Microsoft |

A simplified execution pipeline:

```text
JavaScript source
       ↓
Tokenization
       ↓
Parsing
       ↓
AST / internal representation
       ↓
Bytecode / machine code
       ↓
Execution
```

Modern engines use techniques such as:

- JIT compilation
- inline caching
- optimization
- deoptimization
- garbage collection

### Important interview distinction

**ECMAScript is the specification.**

**V8 is an implementation/engine.**

**Node.js is a runtime environment built around a JavaScript engine and additional APIs.**

Therefore:

```text
ECMAScript ≠ V8 ≠ Node.js
```

---

# 6. ECMAScript Types

ECMAScript has **language types**.

The commonly discussed primitive types are:

```text
Primitive
├── Undefined
├── Null
├── Boolean
├── Number
├── BigInt
├── String
└── Symbol

Non-primitive
└── Object
```

Examples:

```javascript
let a;                  // undefined
let b = null;           // null
let c = true;           // boolean
let d = 42;             // number
let e = 123n;           // bigint
let f = "hello";        // string
let g = Symbol("id");   // symbol
let h = {};             // object
```

### Important interview question

**Is `null` an object?**

The famous result is:

```javascript
typeof null;
```

Output:

```text
"object"
```

But conceptually, `null` represents the absence of an object value.

So say:

> "`typeof null` returns `"object"` because of a historical language behavior, but `null` is a primitive value."

---

# 7. Number and BigInt

ECMAScript `Number` uses IEEE 754 double-precision floating-point representation.

```javascript
let x = 10;
let y = 10.5;
```

This creates an important precision issue:

```javascript
0.1 + 0.2 === 0.3;
```

Result:

```text
false
```

Why?

Binary floating-point representation cannot represent many decimal fractions exactly.

For very large integers, ECMAScript provides `BigInt`:

```javascript
const n = 9007199254740993n;
```

Notice the `n`.

Do not freely mix:

```javascript
1n + 1;
```

This throws a `TypeError`.

Use:

```javascript
1n + 1n;
```

---

# 8. Equality

There are two operators you must know very well:

```javascript
==
===
```

### Loose equality

`==` performs type conversion in many situations.

```javascript
5 == "5";     // true
0 == false;   // true
```

### Strict equality

`===` checks value and type without the normal coercion performed by `==`.

```javascript
5 === "5";    // false
0 === false;  // false
```

### Interview rule

Prefer:

```javascript
===
```

unless you specifically understand and want the semantics of `==`.

---

# 9. Type Coercion

JavaScript frequently converts values from one type to another.

Example:

```javascript
"5" + 2;
```

Result:

```text
"52"
```

Because `+` can perform string concatenation.

But:

```javascript
"5" - 2;
```

Result:

```text
3
```

because subtraction performs numeric coercion.

Important examples:

```javascript
Number("42");      // 42
String(42);        // "42"
Boolean(1);        // true
Boolean(0);        // false
```

### Truthy and falsy values

Common falsy values:

```javascript
false
0
-0
0n
""
null
undefined
NaN
```

Almost everything else is truthy.

Example:

```javascript
if ("hello") {
    console.log("runs");
}
```

---

# 10. `Object` and Prototype System

Objects are fundamental to ECMAScript.

```javascript
const user = {
    name: "Abhi",
    age: 21
};
```

Properties can be accessed using:

```javascript
user.name;
user["age"];
```

Objects can inherit behavior through the **prototype chain**.

Example:

```javascript
const user = {
    name: "Abhi"
};

console.log(user.toString());
```

Where did `toString()` come from?

It is available through the object's prototype chain.

Conceptually:

```text
user
  ↓
Object.prototype
  ↓
null
```

When JavaScript cannot find a property directly on an object, it searches its prototype chain.

---

# 11. Prototype vs `__proto__` vs `prototype`

This is a very common interview topic.

### `prototype`

Functions that can act as constructors have a `prototype` property.

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.sayHello = function () {
    console.log("Hello");
};
```

### `__proto__`

`__proto__` historically provides access to an object's prototype.

```javascript
const person = new Person("Abhi");

person.__proto__ === Person.prototype;
```

This is generally not the preferred modern API.

Use:

```javascript
Object.getPrototypeOf(person);
```

### Key distinction

```text
Constructor function
        │
        └── prototype ──→ prototype object

Created object
        │
        └── internal prototype ──→ prototype object
```

---

# 12. Functions

Functions are first-class objects in JavaScript.

This means a function can be:

- stored in a variable
- passed as an argument
- returned from another function
- stored as an object property

Example:

```javascript
function greet() {
    return "Hello";
}

const fn = greet;
console.log(fn());
```

A function can also be passed as an argument:

```javascript
function execute(callback) {
    callback();
}

execute(function () {
    console.log("Running");
});
```

This is the basis of callbacks and many higher-order functions.

---

# 13. Arrow Functions

ES6 introduced arrow functions.

```javascript
const add = (a, b) => {
    return a + b;
};
```

Short form:

```javascript
const add = (a, b) => a + b;
```

### Major interview point: `this`

Arrow functions do **not** create their own `this`.

They capture `this` from the surrounding lexical scope.

```javascript
const obj = {
    name: "Abhi",

    normal() {
        console.log(this.name);
    },

    arrow: () => {
        console.log(this.name);
    }
};
```

Do not treat arrow functions as simply "shorter functions".

Their `this` behavior is fundamentally different.

---

# 14. Scope

JavaScript has different kinds of scope.

### Global scope

```javascript
var x = 10;
```

### Function scope

`var` is function-scoped.

```javascript
function test() {
    var x = 10;
}

console.log(x); // ReferenceError
```

### Block scope

`let` and `const` are block-scoped.

```javascript
if (true) {
    let x = 10;
    const y = 20;
}
```

Outside the block:

```javascript
console.log(x); // ReferenceError
```

### Interview comparison

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Function scoped | Yes | No | No |
| Block scoped | No | Yes | Yes |
| Redeclaration in same scope | Yes | No | No |
| Reassignment | Yes | Yes | No |
| Hoisted | Yes | Yes* | Yes* |

`let` and `const` are hoisted but remain inaccessible in the **Temporal Dead Zone (TDZ)** until execution reaches their declaration.

---

# 15. Hoisting

Hoisting describes how declarations are processed before normal execution of code.

Example:

```javascript
console.log(x);

var x = 10;
```

Result:

```text
undefined
```

Conceptually:

```javascript
var x;
console.log(x);
x = 10;
```

But:

```javascript
console.log(x);

let x = 10;
```

throws a `ReferenceError`.

The reason is the **Temporal Dead Zone**.

### Function declarations

Function declarations are available before their textual position:

```javascript
hello();

function hello() {
    console.log("Hello");
}
```

---

# 16. Closures

A closure occurs when a function retains access to variables from its lexical environment even after the outer function has finished executing.

Example:

```javascript
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
```

The inner function remembers `count`.

### Interview definition

> **A closure is a function together with the lexical environment in which it was created.**

Common uses:

- data privacy
- function factories
- callbacks
- memoization
- maintaining state
- event handlers

---

# 17. Execution Context

An **execution context** represents the environment in which JavaScript code is evaluated.

Commonly discussed contexts:

```text
Global Execution Context
Function Execution Context
Eval Execution Context
```

A simplified mental model:

```text
Execution Context
├── Lexical Environment
├── Variable Environment
└── This binding
```

When a function is called, a new function execution context is created.

The call stack tracks active execution contexts.

Example:

```javascript
function one() {
    two();
}

function two() {
    three();
}

function three() {
    console.log("Hello");
}

one();
```

Conceptually:

```text
| three() |
| two()   |
| one()   |
| global  |
------------
 Call Stack
```

---

# 18. `this` Keyword

`this` is one of the most frequently asked JavaScript interview topics.

Its value depends on **how a function is called**, except for arrow functions, which use lexical `this`.

Example:

```javascript
const user = {
    name: "Abhi",

    greet() {
        console.log(this.name);
    }
};

user.greet();
```

Here:

```text
this → user
```

### Explicit binding

JavaScript provides:

```javascript
call()
apply()
bind()
```

Example:

```javascript
function greet(city) {
    console.log(this.name, city);
}

const user = {
    name: "Abhi"
};

greet.call(user, "Delhi");
```

`call` invokes immediately.

`apply` invokes immediately but accepts arguments as an array-like value.

`bind` returns a new function with a bound `this`.

---

# 19. Destructuring

ES6 introduced destructuring.

Object destructuring:

```javascript
const user = {
    name: "Abhi",
    age: 21
};

const { name, age } = user;
```

Array destructuring:

```javascript
const nums = [10, 20];

const [a, b] = nums;
```

It is frequently used in modern JavaScript and React.

---

# 20. Rest and Spread

Both use `...`, but their purposes differ.

### Rest

Collects multiple values.

```javascript
function sum(...nums) {
    return nums.reduce((a, b) => a + b, 0);
}
```

### Spread

Expands an iterable or object.

```javascript
const a = [1, 2];
const b = [...a, 3, 4];
```

Object spread:

```javascript
const user = {
    name: "Abhi"
};

const updated = {
    ...user,
    age: 21
};
```

Remember:

```text
Rest   → collect
Spread → expand
```

---

# 21. Classes

ES6 introduced class syntax.

```javascript
class Person {
    constructor(name) {
        this.name = name;
    }

    greet() {
        console.log(`Hello ${this.name}`);
    }
}

const p = new Person("Abhi");
p.greet();
```

Classes provide a cleaner syntax for working with JavaScript's prototype-based object model.

Important interview point:

> JavaScript classes do not replace the prototype system. Class methods are still associated with prototypes.

Inheritance:

```javascript
class Student extends Person {
    constructor(name, branch) {
        super(name);
        this.branch = branch;
    }
}
```

---

# 22. Promises

A Promise represents the eventual result of an asynchronous operation.

States:

```text
Pending
   ↓
Fulfilled

or

Pending
   ↓
Rejected
```

Example:

```javascript
const promise = new Promise((resolve, reject) => {
    resolve("Success");
});
```

Consuming it:

```javascript
promise
    .then(result => console.log(result))
    .catch(error => console.log(error));
```

Important terms:

- pending
- fulfilled
- rejected
- resolved
- rejected
- then
- catch
- finally

---

# 23. `async` / `await`

`async/await` was introduced to make Promise-based asynchronous code easier to read.

```javascript
async function getData() {
    const response = await fetch("/api/data");
    const data = await response.json();

    return data;
}
```

An `async` function always returns a Promise.

```javascript
async function test() {
    return 10;
}
```

Conceptually:

```javascript
test().then(console.log);
```

prints:

```text
10
```

### Important interview point

`await` does not make JavaScript synchronous globally.

It pauses the execution of the current async function until the awaited Promise settles, while the runtime can continue processing other work.

---

# 24. Event Loop

The event loop is critical for JavaScript interviews.

JavaScript execution is commonly described as using a single main call stack, while asynchronous work is coordinated with the host environment and job/task queues.

Simplified model:

```text
        ┌──────────────┐
        │ Call Stack   │
        └──────┬───────┘
               │
        ┌──────▼───────┐
        │ Host APIs    │
        └──────┬───────┘
               │
      ┌────────┴────────┐
      │                 │
      ▼                 ▼
 Task Queue        Promise Jobs
      │                 │
      └────────┬────────┘
               ▼
          Event Loop
```

Example:

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

Promise.resolve().then(() => {
    console.log("C");
});

console.log("D");
```

Typical output:

```text
A
D
C
B
```

Why?

1. Synchronous code runs first.
2. Promise reactions are scheduled as jobs/microtasks.
3. Timer callbacks are tasks/macrotasks.
4. The runtime processes the relevant queues according to its event-loop rules.

For interviews, remember the practical ordering:

```text
Synchronous code
      ↓
Microtasks / Promise jobs
      ↓
Tasks such as timer callbacks
```

Do not oversimplify this into "JavaScript has a microtask queue and macrotask queue" without acknowledging that exact event-loop behavior is specified across ECMAScript and the host environment.

---

# 25. Modules

Modern ECMAScript supports modules.

Export:

```javascript
export const name = "Abhi";

export function greet() {
    console.log("Hello");
}
```

Import:

```javascript
import { name, greet } from "./user.js";
```

Default export:

```javascript
export default function App() {
    console.log("App");
}
```

Import:

```javascript
import App from "./App.js";
```

Modules provide:

- encapsulation
- dependency management
- reusable code
- separate module scope

A major interview point:

> ES modules are statically analyzable, which enables tooling such as tree shaking.

---

# 26. Map and Set

### Set

Stores unique values.

```javascript
const set = new Set([1, 2, 2, 3]);

console.log(set);
// Set { 1, 2, 3 }
```

Useful for removing duplicates:

```javascript
const unique = [...new Set([1, 2, 2, 3])];
```

### Map

Stores key-value pairs.

```javascript
const map = new Map();

map.set("name", "Abhi");
map.set("age", 21);

console.log(map.get("name"));
```

Unlike ordinary objects, `Map` keys can be values of many types, including objects.

```javascript
const key = {};

map.set(key, "value");
```

---

# 27. Iterators and Generators

An iterator provides a standard way to produce values one at a time.

The iterator protocol uses:

```javascript
next()
```

A generator function is declared using `function*`.

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = numbers();

console.log(gen.next());
console.log(gen.next());
```

Output resembles:

```javascript
{ value: 1, done: false }
{ value: 2, done: false }
```

Generators are useful for controlled/lazy iteration.

---

# 28. Symbols

`Symbol` creates unique primitive values.

```javascript
const id1 = Symbol("id");
const id2 = Symbol("id");

console.log(id1 === id2);
```

Result:

```text
false
```

Symbols are often used as unique property keys.

```javascript
const id = Symbol("id");

const user = {
    name: "Abhi",
    [id]: 123
};
```

---

# 29. Optional Chaining and Nullish Coalescing

Optional chaining:

```javascript
const city = user?.address?.city;
```

It avoids errors when an intermediate value is `null` or `undefined`.

Nullish coalescing:

```javascript
const name = user.name ?? "Guest";
```

`??` uses the right side only when the left side is `null` or `undefined`.

Compare:

```javascript
0 || 10;     // 10
0 ?? 10;     // 0
```

This difference is a common interview question.

---

# 30. Modern Array Methods

Important methods to know:

```javascript
map()
filter()
reduce()
find()
findIndex()
some()
every()
includes()
forEach()
sort()
slice()
splice()
flat()
flatMap()
```

### `map`

Transforms every element:

```javascript
const result = [1, 2, 3].map(x => x * 2);
```

### `filter`

Keeps matching elements:

```javascript
const result = [1, 2, 3, 4].filter(x => x % 2 === 0);
```

### `reduce`

Combines values:

```javascript
const sum = [1, 2, 3].reduce((a, b) => a + b, 0);
```

Remember:

```text
map    → transform
filter → select
reduce → accumulate
```

---

# 31. Important Interview Traps

## `typeof`

```javascript
typeof undefined;     // "undefined"
typeof null;          // "object"
typeof 10;            // "number"
typeof 10n;           // "bigint"
typeof "hello";       // "string"
typeof true;          // "boolean"
typeof Symbol();      // "symbol"
typeof {};            // "object"
typeof function(){};  // "function"
```

---

## `NaN`

```javascript
typeof NaN;
```

Result:

```text
"number"
```

`NaN` means **Not-a-Number**, but it is still part of the Number type.

Also:

```javascript
NaN === NaN;
```

is:

```text
false
```

Use:

```javascript
Number.isNaN(value);
```

for a precise NaN check.

---

## `Object.is`

`Object.is` provides SameValue comparison.

Important examples:

```javascript
Object.is(NaN, NaN);   // true
Object.is(+0, -0);     // false
```

This differs from `===`.

---

# 32. Shallow Copy vs Deep Copy

Spread syntax creates a shallow copy.

```javascript
const user = {
    name: "Abhi",
    address: {
        city: "Meerut"
    }
};

const copy = { ...user };
```

The nested object is still shared:

```javascript
copy.address.city = "Delhi";

console.log(user.address.city);
```

Result:

```text
Delhi
```

because both objects reference the same nested object.

For structured data, one modern option is:

```javascript
const copy = structuredClone(user);
```

But deep-copy strategy should be chosen based on the data types and requirements.

---

# 33. Garbage Collection

JavaScript automatically manages memory.

A simplified model:

```text
Reachable objects
      ↓
Kept in memory

Unreachable objects
      ↓
Eligible for garbage collection
```

Example:

```javascript
let user = {
    name: "Abhi"
};

user = null;
```

If no other references exist, the previous object can eventually become eligible for garbage collection.

Important:

> Garbage collection is automatic, but developers can still create memory leaks by unintentionally retaining references.

Common sources:

- forgotten event listeners
- long-lived timers
- global references
- closures retaining unnecessary objects
- caches without eviction

---

# 34. Strict Mode

Strict mode enables stricter semantics.

```javascript
"use strict";
```

Examples of behavior that becomes stricter include certain accidental global assignments.

```javascript
"use strict";

x = 10;
```

This causes an error instead of silently creating/using an accidental global in the relevant context.

ES modules are automatically strict mode code.

---

# 35. Lexical Environment

The lexical environment is a key specification concept.

It stores bindings such as:

```javascript
let x = 10;
const y = 20;
```

When nested functions are created, they can access bindings from their surrounding lexical environments.

That is the foundation of closures.

Conceptually:

```text
Global Lexical Environment
        │
        ├── x
        └── function outer
                 │
                 ▼
          Outer Lexical Environment
                 │
                 ├── count
                 └── inner function
```

---

# 36. Common ECMAScript Interview Questions

### Q1. What is ECMAScript?

**Answer:**

ECMAScript is the standardized specification defining the core JavaScript language.

---

### Q2. Is JavaScript the same as ECMAScript?

**Answer:**

Not exactly. ECMAScript defines the core language standard. JavaScript is the commonly used language name for implementations of that standard, together with environment-specific APIs.

---

### Q3. What is ES6?

**Answer:**

ES6 is ECMAScript 2015, a major version that introduced features such as `let`, `const`, arrow functions, classes, destructuring, modules, Promises, Map, Set, and more.

---

### Q4. What is the difference between ECMAScript and Node.js?

**Answer:**

ECMAScript defines the language. Node.js is a runtime environment that uses a JavaScript engine and provides additional APIs for server-side development.

---

### Q5. What is a JavaScript engine?

**Answer:**

A JavaScript engine is software that parses and executes JavaScript, such as V8, SpiderMonkey, or JavaScriptCore.

---

### Q6. Why does `typeof null` return `"object"`?

**Answer:**

It is a historical behavior preserved for compatibility. Conceptually, `null` is a primitive value representing the absence of an object.

---

### Q7. Difference between `var`, `let`, and `const`?

Remember:

```text
var   → function scoped
let   → block scoped
const → block scoped + cannot be reassigned
```

---

### Q8. What is a closure?

**Answer:**

A closure is a function together with access to the lexical environment in which the function was created.

---

### Q9. Does an arrow function have its own `this`?

**Answer:**

No. Arrow functions capture `this` lexically from their surrounding scope.

---

### Q10. Is JavaScript single-threaded?

Interview-safe answer:

> JavaScript execution on the main thread is commonly described as single-threaded, but modern runtimes can use additional threads internally and expose concurrency mechanisms such as Web Workers or Node.js worker threads. The ECMAScript language itself defines execution semantics, while the host environment provides many concurrency facilities.

---

# 37. One-Minute ECMAScript Revision

Before an interview, remember this hierarchy:

```text
ECMAScript
│
├── Specification
│
├── Types
│   ├── Undefined
│   ├── Null
│   ├── Boolean
│   ├── Number
│   ├── BigInt
│   ├── String
│   ├── Symbol
│   └── Object
│
├── Scope
│   ├── Global
│   ├── Function
│   └── Block
│
├── Functions
│   ├── Regular
│   ├── Arrow
│   ├── Callback
│   ├── Higher-order
│   └── Closure
│
├── Objects
│   ├── Prototype
│   ├── Prototype Chain
│   └── Classes
│
├── Execution
│   ├── Execution Context
│   ├── Call Stack
│   ├── Hoisting
│   └── `this`
│
├── Async
│   ├── Promise
│   ├── async/await
│   └── Event Loop / Host Tasks
│
├── Modern Syntax
│   ├── Destructuring
│   ├── Rest / Spread
│   ├── Optional Chaining
│   └── Nullish Coalescing
│
└── Collections
    ├── Map
    ├── Set
    ├── Iterator
    └── Generator
```

---

# 38. Final Interview Checklist

Before saying you are comfortable with ECMAScript, make sure you can explain these without memorizing definitions:

- [ ] ECMAScript vs JavaScript
- [ ] ECMAScript vs Node.js
- [ ] JavaScript engine
- [ ] ES5 vs ES6
- [ ] Primitive vs object values
- [ ] `null` vs `undefined`
- [ ] `==` vs `===`
- [ ] Type coercion
- [ ] Truthy and falsy values
- [ ] `NaN`
- [ ] `Number` vs `BigInt`
- [ ] `var` vs `let` vs `const`
- [ ] Scope
- [ ] Hoisting
- [ ] Temporal Dead Zone
- [ ] Closures
- [ ] Lexical environment
- [ ] Execution context
- [ ] Call stack
- [ ] `this`
- [ ] `call`, `apply`, `bind`
- [ ] Prototype
- [ ] Prototype chain
- [ ] `prototype` vs `__proto__`
- [ ] Classes and inheritance
- [ ] Arrow functions
- [ ] Destructuring
- [ ] Rest vs spread
- [ ] Promises
- [ ] `async/await`
- [ ] Event loop
- [ ] Microtasks / Promise jobs
- [ ] Modules
- [ ] Map vs Object
- [ ] Set
- [ ] Iterators
- [ ] Generators
- [ ] Symbols
- [ ] Optional chaining
- [ ] Nullish coalescing
- [ ] Shallow vs deep copy
- [ ] Garbage collection
- [ ] Strict mode

---

# 39. The Core Mental Model

If an interviewer asks something unexpected about JavaScript, return to this model:

```text
ECMAScript = LANGUAGE SPECIFICATION

JavaScript Engine = IMPLEMENTATION

Runtime / Host = ENGINE + APIs + EVENT/CONCURRENCY FACILITIES

Browser = JavaScript Engine + Web APIs + DOM + Browser Environment

Node.js = JavaScript Engine + Node APIs + Node Runtime
```

And remember the most important interview principle:

> **Do not learn JavaScript as a collection of syntax tricks. Understand the language model: values, types, bindings, lexical environments, objects, prototypes, execution contexts, functions, asynchronous jobs, and host interaction.**

Once those concepts are clear, most "tricky" JavaScript interview questions become predictable rather than mysterious.
