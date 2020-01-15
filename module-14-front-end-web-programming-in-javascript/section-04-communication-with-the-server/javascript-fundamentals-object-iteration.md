# Lesson: Object Iteration (JavaScript Fundamentals)

## Loopings vs. Iteration

There's a pretty fine line separating the concepts of _looping_ and _iteration_, and only the truly pedantic will call you out if you use one in place of the other. Looping is the process of executing a set of statements **repeatedly until a condition is met**. It's great for when we want to do something a specific number of times (`for` loop) or unlimited times until the condition is met (`while` loop). Iteration is the process of executing a set of statements **once for each element in a collection**.

## `for...of`

ES2015 introduced the `for...of` statement:

```javascript
const myArray = ["a", "b", "c", "d", "e", "f", "g"];

for (const element of myArray) {
  console.log(element);
}
```

It's so much cleaner than the looping solutions—no initialization of a counter, no condition, no incrementing the counter, and no bracket notation to access elements in the array (`myArray[i]`).

## `const` vs. `let`

As you might have noticed, `for...of` allows us to use `const` instead of `let`. In `for` and `while` statements, `let` is required because we are incrementing a counter variable. The `for...of` statement involves no such reassignment. On each trip into the loop body (which is a _block_—not the curly braces), we assign the next element in the collection to a **new** `element` variable. Upon reaching the end of the block, the block-scoped variable vanishes, and we return to the top. Then we repeat the process, assigning the next element in the collection to a **new** `element` variable.

### Iterating Over... Strings?

A string is effectively an ordered collection (an array) of characters, which `for...of` is more than happy to iterate over:

```javascript
for (const char of "Hello, world!") {
  console.log(char);
}

// LOG: H
// LOG: e
// LOG: l
// LOG: l
// LOG: o
// LOG: ,
// LOG:  
// LOG: w
// LOG: o
// LOG: r
// LOG: l
// LOG: d
// LOG: !
```

### Usage

Use a `for...of` statement anytime you want to iterate over an array.

## Iterating Over Objects

The `for...in` statement had been around for a long time, and it's usually used for iterating over the properties in an object. The statement follows this syntax:

```javascript
for (const <KEY> in <OBJECT>) {
  // Code in the statement body
}
```

The `for...in` statement iterates over the properties in an object, but it doesn't pass the entire property into the block. Instead, it only passes in the _keys_:

```javascript
const address = {
  street1: "11 Broadway",
  street2: "2nd Floor",
  city: "New York",
  state: "NY",
  zipCode: 10004
};

for (const key in address) {
  console.log(key);
}

// LOG: street1
// LOG: street2
// LOG: city
// LOG: state
// LOG: zipCode
```

Accessing the object's values is as simple as combining the passed-in key with the _bracket operator_:

```javascript
const address = {
  street1: "11 Broadway",
  street2: "2nd Floor",
  city: "New York",
  state: "NY",
  zipCode: 10004
};

for (const key in address) {
  console.log(address[key]);
}

// LOG: 11 Broadway
// LOG: 2nd Floor
// LOG: New York
// LOG: NY
// LOG: 10004
```

We **cannot use** the _dot operator_ in this instance, only the _bracket operator_. Remember, variables don't work with the dot operator because it treats the variable name as a literal key—that is, `address.key` would be trying to access the property on `address` with a key of `key`. Since there is no `key` property in `address`, it returns `undefined`.

### Usage

Use a `for...in` statement whenever you want to enumerate the properties of an object.

### `for...in` and Order

As a general rule, don't use `for...in` with arrays. When iterating over an array, an **ordered** collection, we would expect the elements in the array to be dealt with **in order**. However, because of how `for...in` works under the hood, there's no guarantee of order. From the MDN documentation:

> A `for...in` loop iterates over the properties of an object in an **arbitrary order** ... one cannot depend on the seeming orderliness of iteration, at least in a cross-browser setting.

Additionally, in the pre-ES2015 days, using `for...in` would often result in different browsers iterating over the same object's properties in different orders. Cross-browser consistency is very important. A lot of progress has been made towards standardizing the behavior of `for...in` across all major browsers, but there's still no reason to use `for...in` with arrays when we have the wonderfully consistent `for...of` tailor-made for the job.

### Resources

- [`for...of` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- [`for...in` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
