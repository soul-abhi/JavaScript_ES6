# JavaScript Data Types — Interview Revision

> **Goal:** Be able to answer JavaScript datatype questions quickly and explain *why*, not just memorize outputs.

---

# 1. The Big Picture

JavaScript has **8 data types**.

## Primitive Data Types — 7

1. `String`
2. `Number`
3. `BigInt`
4. `Boolean`
5. `Undefined`
6. `Null`
7. `Symbol`

## Non-Primitive / Reference Type

8. `Object`

Important:

```text
Primitive
├── String
├── Number
├── BigInt
├── Boolean
├── Undefined
├── Null
└── Symbol

Non-Primitive
└── Object
    ├── Array
    ├── Function
    ├── Date
    ├── RegExp
    └── ...many others
```

### Interview statement

> JavaScript has 7 primitive data types and one non-primitive type, Object.

---

# 2. Primitive vs Reference Types

## Primitive

Primitive values are **immutable**.

Examples:

```js
let x = 10;
let name = "Abhi";
let flag = true;
```

If you appear to modify a primitive value, JavaScript creates/uses another value rather than mutating the original primitive.

```js
let x = "hello";

x[0] = "H";

console.log(x); // "hello"
```

Strings are immutable.

---

## Objects

Objects are mutable.

```js
let user = {
    name: "Abhi"
};

user.name = "Rahul";

console.log(user.name); // Rahul
```

---

# 3. The 7 Primitive Types

---

## 3.1 String

Used for textual data.

```js
let name = "Abhi";
let city = 'Delhi';
let message = `Hello ${name}`;
```

Three common ways:

```js
"Hello"
'Hello'
`Hello`
```

Template literals allow interpolation:

```js
let age = 21;

console.log(`I am ${age} years old`);
```

### Important

Strings are immutable.

```js
let str = "hello";

str[0] = "H";

console.log(str); // hello
```

---

# 3.2 Number

JavaScript uses one `Number` type for:

* Integers
* Floating-point numbers
* Positive infinity
* Negative infinity
* `NaN`

```js
let a = 10;
let b = 10.5;
let c = Infinity;
let d = NaN;
```

Unlike languages such as Java:

```text
Java:
int
float
double
long

JavaScript:
Number
```

### Important limitation

JavaScript's `Number` uses IEEE-754 double-precision floating point.

Therefore:

```js
console.log(0.1 + 0.2);
```

Output:

```text
0.30000000000000004
```

This is a floating-point precision issue.

---

# 3.3 BigInt

Used for integers larger than the safe integer range of `Number`.

```js
let x = 123456789012345678901234567890n;
```

Notice the `n`.

```js
typeof 10n;
```

Output:

```text
"bigint"
```

### Important

You cannot directly mix `Number` and `BigInt` in arithmetic.

```js
10n + 5;
```

This throws an error.

You must convert explicitly:

```js
10n + BigInt(5);
```

or:

```js
Number(10n) + 5;
```

Be careful: converting a huge BigInt to Number can lose precision.

---

# 3.4 Boolean

Has only two values:

```js
true
false
```

Commonly used in conditions:

```js
let loggedIn = true;

if (loggedIn) {
    console.log("Welcome");
}
```

---

# 3.5 Undefined

`undefined` generally means:

> A variable exists but has not been assigned a value.

```js
let x;

console.log(x);
```

Output:

```text
undefined
```

Also:

```js
function test() {}

console.log(test());
```

Output:

```text
undefined
```

A missing object property also returns `undefined`:

```js
let user = {};

console.log(user.name);
```

Output:

```text
undefined
```

---

# 3.6 Null

`null` represents an intentional absence of a value.

```js
let user = null;
```

Think:

```text
undefined → value was not provided / not initialized

null → intentionally empty
```

---

# 3.7 Symbol

A `Symbol` creates a unique primitive value.

```js
let a = Symbol("id");
let b = Symbol("id");

console.log(a === b);
```

Output:

```text
false
```

Even though both have the same description, they are different symbols.

Symbols are often used as unique object property keys.

```js
const id = Symbol("id");

const user = {
    [id]: 101
};
```

---

# 4. The Weird `typeof` Questions

This is one of the most important interview areas.

Memorize this table:

| Value          | `typeof`      |
| -------------- | ------------- |
| `"hello"`      | `"string"`    |
| `10`           | `"number"`    |
| `10n`          | `"bigint"`    |
| `true`         | `"boolean"`   |
| `undefined`    | `"undefined"` |
| `null`         | `"object"`    |
| `Symbol()`     | `"symbol"`    |
| `{}`           | `"object"`    |
| `[]`           | `"object"`    |
| `function(){}` | `"function"`  |

## Biggest trap

```js
typeof null
```

Output:

```text
"object"
```

This is a historical JavaScript behavior/legacy quirk.

### Interview question

**Q: Is `null` actually an object?**

**A:** No. `null` is a primitive value. The fact that `typeof null` returns `"object"` is a historical language quirk.

---

# 5. Arrays and `typeof`

This is another classic question.

```js
typeof [];
```

Output:

```text
"object"
```

Therefore:

```js
typeof [1, 2, 3] === "object"
```

is `true`.

To properly determine whether something is an array:

```js
Array.isArray(value);
```

Example:

```js
Array.isArray([]);
```

Output:

```text
true
```

---

# 6. Functions and `typeof`

Functions are technically objects in JavaScript's object model, but:

```js
typeof function() {}
```

returns:

```text
"function"
```

Example:

```js
function hello() {}

console.log(typeof hello);
```

Output:

```text
function
```

This is another special behavior worth remembering.

---

# 7. `typeof` — Must-Know Interview Questions

### Q1

```js
typeof null
```

Answer:

```text
object
```

### Q2

```js
typeof []
```

Answer:

```text
object
```

### Q3

```js
typeof {}
```

Answer:

```text
object
```

### Q4

```js
typeof function(){}
```

Answer:

```text
function
```

### Q5

```js
typeof NaN
```

Answer:

```text
number
```

### Q6

```js
typeof Infinity
```

Answer:

```text
number
```

### Q7

```js
typeof undefined
```

Answer:

```text
undefined
```

### Q8

```js
typeof 10n
```

Answer:

```text
bigint
```

---

# 8. NaN

`NaN` means:

> Not-a-Number

But there is an important trap:

```js
typeof NaN
```

returns:

```text
"number"
```

Because `NaN` is a special numeric value in JavaScript.

---

## NaN is not equal to itself

```js
NaN === NaN
```

Output:

```text
false
```

Even:

```js
NaN == NaN
```

Output:

```text
false
```

Use:

```js
Number.isNaN(value);
```

Example:

```js
Number.isNaN(NaN); // true
```

---

# 9. Infinity

JavaScript supports:

```js
Infinity
-Infinity
```

Example:

```js
console.log(10 / 0);
```

Output:

```text
Infinity
```

And:

```js
typeof Infinity
```

returns:

```text
number
```

---

# 10. Safe Integer Range

JavaScript `Number` can represent integers safely only up to:

```js
Number.MAX_SAFE_INTEGER
```

which is:

```text
9007199254740991
```

And:

```js
Number.MIN_SAFE_INTEGER
```

is:

```text
-9007199254740991
```

Check:

```js
Number.isSafeInteger(100);
```

---

# 11. Number Precision Trap

Classic interview question:

```js
console.log(0.1 + 0.2 === 0.3);
```

Answer:

```text
false
```

Because floating-point values are represented approximately in binary.

For precision-sensitive calculations, especially financial calculations, do not blindly rely on binary floating-point arithmetic.

---

# 12. Type Coercion

JavaScript can automatically convert one type into another.

This is called:

> Type coercion

Example:

```js
let x = "10";
let y = 5;

console.log(x + y);
```

Output:

```text
"105"
```

Why?

Because `+` with a string causes string concatenation.

---

# 13. `+` vs Other Operators

This is extremely important.

```js
"10" + 5
```

Output:

```text
"105"
```

But:

```js
"10" - 5
```

Output:

```text
5
```

Because `-` converts the string to a number.

Similarly:

```js
"10" * 2 // 20
"10" / 2 // 5
```

---

# 14. Explicit Type Conversion

You can manually convert types.

## String

```js
String(123);
```

Result:

```text
"123"
```

## Number

```js
Number("123");
```

Result:

```text
123
```

## Boolean

```js
Boolean(1);
```

Result:

```text
true
```

---

# 15. `parseInt()` vs `Number()`

Important interview distinction.

```js
Number("123abc");
```

Result:

```text
NaN
```

But:

```js
parseInt("123abc");
```

Result:

```text
123
```

`parseInt()` parses an integer from the beginning of a string.

Better practice:

```js
parseInt("123", 10);
```

---

# 16. Truthy and Falsy Values

JavaScript converts values to Boolean in conditions.

## Falsy Values

Memorize these:

```text
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

Example:

```js
if ("hello") {
    console.log("Runs");
}
```

It runs because `"hello"` is truthy.

---

# 17. Important Truthy Traps

### Empty array

```js
Boolean([])
```

Result:

```text
true
```

### Empty object

```js
Boolean({})
```

Result:

```text
true
```

Therefore:

```js
if ([]) {
    console.log("yes");
}
```

prints:

```text
yes
```

And:

```js
if ({}) {
    console.log("yes");
}
```

also prints:

```text
yes
```

### Important

```text
[] is truthy
{} is truthy
```

---

# 18. `==` vs `===`

## `==`

Loose equality.

It performs type coercion.

```js
5 == "5"
```

Result:

```text
true
```

## `===`

Strict equality.

It checks both:

1. Type
2. Value

```js
5 === "5"
```

Result:

```text
false
```

### Interview rule

Prefer:

```js
===
```

unless you specifically understand and require loose equality semantics.

---

# 19. Famous Equality Traps

Memorize these:

```js
0 == false        // true
0 === false       // false

1 == true         // true
1 === true        // false

"" == false       // true
"" === false      // false

null == undefined // true
null === undefined // false
```

But:

```js
null == 0
```

is:

```text
false
```

And:

```js
undefined == 0
```

is:

```text
false
```

---

# 20. `null` vs `undefined`

This question appears frequently.

| `undefined`                      | `null`                      |
| -------------------------------- | --------------------------- |
| Usually means value not assigned | Intentional absence         |
| Primitive                        | Primitive                   |
| `typeof` → `"undefined"`         | `typeof` → `"object"`       |
| Often produced automatically     | Usually assigned explicitly |

Example:

```js
let a;
let b = null;
```

---

# 21. Primitive Assignment

Primitive values behave like independent values.

```js
let a = 10;
let b = a;

b = 20;

console.log(a);
```

Output:

```text
10
```

Because:

```text
a → 10
b → 10
```

Then changing `b` does not change `a`.

---

# 22. Object Assignment

Objects behave differently.

```js
let a = {
    value: 10
};

let b = a;

b.value = 20;

console.log(a.value);
```

Output:

```text
20
```

Why?

Both variables refer to the same object.

Conceptually:

```text
a ─────┐
       ↓
    { value: 20 }
       ↑
b ─────┘
```

---

# 23. Arrays Behave Like Objects

```js
let a = [1, 2, 3];

let b = a;

b.push(4);

console.log(a);
```

Output:

```text
[1, 2, 3, 4]
```

Because both refer to the same array object.

---

# 24. Important Interview Terminology

You will often hear:

> "Primitive types are passed by value and objects are passed by reference."

This is useful shorthand, but the technically precise explanation is:

> JavaScript is pass-by-value. For objects, the value being passed is a reference to the object.

Example:

```js
let obj = {
    x: 10
};

function change(o) {
    o.x = 20;
}

change(obj);

console.log(obj.x);
```

Output:

```text
20
```

---

# 25. Mutation vs Reassignment

Very important distinction.

```js
let obj = {
    x: 10
};

function test(o) {
    o.x = 20;       // mutation
    o = { x: 30 };  // reassignment
}

test(obj);

console.log(obj.x);
```

Output:

```text
20
```

Why?

The reassignment:

```js
o = { x: 30 };
```

only changes the local variable `o`.

It does not change what `obj` points to.

---

# 26. Mutable vs Immutable

## Immutable Primitive Values

```text
String
Number
BigInt
Boolean
Undefined
Null
Symbol
```

These are primitive and immutable.

## Mutable Objects

Objects can generally be mutated:

```js
let user = {
    age: 20
};

user.age = 21;
```

Arrays are mutable:

```js
let arr = [1, 2];

arr.push(3);
```

---

# 27. `Object` Is the Base Category for Many Things

Examples:

```js
{}
[]
new Date()
new Map()
new Set()
function test() {}
```

Arrays, dates, maps, sets, and functions are objects in JavaScript's broader object model.

But `typeof` has special behavior for functions:

```js
typeof function() {}
// "function"
```

---

# 28. `typeof` Is Not Enough

Bad:

```js
typeof []
```

gives:

```text
object
```

If you want to determine an array:

```js
Array.isArray([]);
```

If you want to determine whether something is `null`:

```js
value === null
```

Do not rely on:

```js
typeof value === "object"
```

to mean "this is a normal object."

It also includes arrays, dates, maps, sets, and `null`.

---

# 29. `Object.prototype.toString`

Another way to inspect types:

```js
Object.prototype.toString.call([]);
```

Result:

```text
[object Array]
```

Examples:

```js
Object.prototype.toString.call({});
// [object Object]

Object.prototype.toString.call(null);
// [object Null]

Object.prototype.toString.call(new Date());
// [object Date]
```

This can be useful when you need more specific runtime type information.

---

# 30. `const` Does NOT Make Objects Immutable

Classic interview trap.

```js
const user = {
    name: "Abhi"
};

user.name = "Rahul";
```

This is allowed.

But:

```js
user = {};
```

is not allowed.

Why?

`const` prevents reassignment of the binding. It does not freeze the object.

For actual immutability:

```js
Object.freeze(user);
```

---

# 31. String Conversion

Remember:

```js
String(null)
```

gives:

```text
"null"
```

```js
String(undefined)
```

gives:

```text
"undefined"
```

```js
String(true)
```

gives:

```text
"true"
```

---

# 32. Number Conversion

Important:

```js
Number("")
```

returns:

```text
0
```

```js
Number(" ")
```

returns:

```text
0
```

```js
Number("123")
```

returns:

```text
123
```

```js
Number("abc")
```

returns:

```text
NaN
```

```js
Number(null)
```

returns:

```text
0
```

```js
Number(undefined)
```

returns:

```text
NaN
```

---

# 33. Boolean Conversion

Remember:

```js
Boolean(0)          // false
Boolean("")         // false
Boolean(null)       // false
Boolean(undefined)  // false
Boolean(NaN)        // false
```

But:

```js
Boolean("0")        // true
Boolean("false")    // true
Boolean([])         // true
Boolean({})         // true
```

Why?

Because non-empty strings and objects are truthy.

---

# 34. Common Interview Output Questions

Before looking at the answer, predict the output.

### Question 1

```js
console.log(typeof null);
```

Answer:

```text
object
```

---

### Question 2

```js
console.log(typeof NaN);
```

Answer:

```text
number
```

---

### Question 3

```js
console.log([] == false);
```

Answer:

```text
true
```

---

### Question 4

```js
console.log([] === false);
```

Answer:

```text
false
```

---

### Question 5

```js
console.log("" == 0);
```

Answer:

```text
true
```

---

### Question 6

```js
console.log("" === 0);
```

Answer:

```text
false
```

---

### Question 7

```js
console.log(null == undefined);
```

Answer:

```text
true
```

---

### Question 8

```js
console.log(null === undefined);
```

Answer:

```text
false
```

---

### Question 9

```js
console.log(Boolean([]));
```

Answer:

```text
true
```

---

### Question 10

```js
console.log(Boolean({}));
```

Answer:

```text
true
```

---

### Question 11

```js
console.log(0.1 + 0.2);
```

Answer:

```text
0.30000000000000004
```

---

### Question 12

```js
console.log("5" + 2);
```

Answer:

```text
52
```

---

### Question 13

```js
console.log("5" - 2);
```

Answer:

```text
3
```

---

### Question 14

```js
console.log(typeof []);
```

Answer:

```text
object
```

---

### Question 15

```js
console.log(typeof function(){});
```

Answer:

```text
function
```

---

# 35. Rapid Revision Table

| Concept                 | Remember                |
| ----------------------- | ----------------------- |
| Primitive types         | 7                       |
| Non-primitive           | Object                  |
| `typeof null`           | `"object"`              |
| `typeof NaN`            | `"number"`              |
| `typeof []`             | `"object"`              |
| `typeof function(){}`   | `"function"`            |
| `typeof 10n`            | `"bigint"`              |
| Array detection         | `Array.isArray()`       |
| `NaN === NaN`           | `false`                 |
| `null == undefined`     | `true`                  |
| `null === undefined`    | `false`                 |
| `5 == "5"`              | `true`                  |
| `5 === "5"`             | `false`                 |
| `[]`                    | truthy                  |
| `{}`                    | truthy                  |
| `""`                    | falsy                   |
| `0`                     | falsy                   |
| `NaN`                   | falsy                   |
| `null`                  | falsy                   |
| `undefined`             | falsy                   |
| `0n`                    | falsy                   |
| `const object`          | object can still mutate |
| Strings                 | immutable               |
| Objects                 | mutable                 |
| BigInt suffix           | `n`                     |
| Number safe integer max | `9007199254740991`      |

---

# 36. Interview Mental Model

When an interviewer gives you a datatype question, mentally ask:

```text
1. What is the actual value?
        ↓
2. What is its primitive/reference category?
        ↓
3. What does typeof return?
        ↓
4. Is type coercion happening?
        ↓
5. Is this == or ===?
        ↓
6. Is the value truthy/falsy?
        ↓
7. Is the value mutable?
        ↓
8. Is this a special JavaScript edge case?
```

This mental sequence solves a huge percentage of datatype output questions.

---

# 37. Must-Know Interview Questions

You should be able to answer these without notes:

### Fundamentals

1. What are JavaScript's primitive data types?
2. What is the difference between primitive and non-primitive types?
3. Is JavaScript statically or dynamically typed?
4. What is dynamic typing?
5. What does `typeof` do?
6. Why does `typeof null` return `"object"`?
7. Why does `typeof []` return `"object"`?
8. Why does `typeof NaN` return `"number"`?
9. Why does `typeof function(){}` return `"function"`?

### Conversion

10. What is type coercion?
11. Difference between implicit and explicit conversion?
12. Difference between `Number()` and `parseInt()`?
13. What happens when `"10" + 5` is evaluated?
14. What happens when `"10" - 5` is evaluated?
15. What is the result of `Number("")`?
16. What is the result of `Number(null)`?
17. What is the result of `Number(undefined)`?

### Equality

18. Difference between `==` and `===`?
19. Why is `0 == false` true?
20. Why is `0 === false` false?
21. Why is `null == undefined` true?
22. Why is `null === undefined` false?
23. Why is `NaN === NaN` false?

### Truthiness

24. What are all falsy values?
25. Is `[]` truthy or falsy?
26. Is `{}` truthy or falsy?
27. Is `"false"` truthy or falsy?
28. Is `"0"` truthy or falsy?

### Objects

29. Are objects mutable?
30. Are primitive values mutable?
31. What happens when one object variable is assigned to another?
32. What is the difference between mutation and reassignment?
33. Does `const` make an object immutable?
34. How do you check whether a value is an array?

### Numbers

35. What is `NaN`?
36. What is `Infinity`?
37. Why does `0.1 + 0.2` produce an unexpected result?
38. What is `Number.MAX_SAFE_INTEGER`?
39. When should you use `BigInt`?
40. Can `BigInt` and `Number` be directly mixed?

---

# 38. 30-Second Final Revision

Before an interview, remember this:

```text
JS = 7 primitives + Object

Primitive:
String
Number
BigInt
Boolean
Undefined
Null
Symbol

Major traps:
typeof null → "object"
typeof [] → "object"
typeof NaN → "number"
typeof function → "function"

Falsy:
false
0
-0
0n
""
null
undefined
NaN

Equality:
==  → coercion
=== → strict

NaN:
NaN !== NaN

Objects:
mutable
reference-valued
const does not freeze them

Array:
typeof [] → "object"
Array.isArray([]) → true

Number:
IEEE-754
0.1 + 0.2 !== 0.3
MAX_SAFE_INTEGER = 9007199254740991

BigInt:
123n
Cannot directly mix with Number
```

---

# 39. The Most Important Rule

Do not memorize only the outputs.

For every tricky question, learn the **reason behind the output**.

For example:

```js
console.log("5" + 2); // "52"
```

Do not remember:

> `"5" + 2 = "52"`

Remember:

> `+` has special string concatenation behavior, so the number is converted to a string.

Similarly:

```js
console.log(null == undefined); // true
```

Do not just memorize `true`.

Remember:

> Loose equality has a special rule that treats `null` and `undefined` as equal to each other, but not equal to ordinary values such as `0` or `false`.

That distinction is what separates **memorization from interview-level understanding**.
