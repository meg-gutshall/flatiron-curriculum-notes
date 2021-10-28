---
description: 'Version 8: Module 14: Section 9: Lesson'
---

# Collection Processing Methods Family Tree (JS Advanced Functions)

Now that you have written `map` and `reduce`, here's the big reveal: JavaScript _already_ has these methods built into its array data type!

## Use `map` to Transform an Array

```javascript
[10, 20, 30, 40].map(function(a) {
  return a * 2;
});
//=> [20, 40, 60, 80]
```

## Use `reduce` to Reduce an Array to a Value

```javascript
[10, 20, 30, 40].reduce(function(memo, i) { return memo + i }) //=> 100
[10, 20, 30, 40].reduce(function(memo, i) { return memo + i }, 100) //=> 200
```

Remember, _**JavaScript loves functions.**_ By being able to pass functions around comfortably, we can take advantage of methods that JavaScript gives us! Given what you know about writing your own `map` and `reduce` functions, read the JavaScript documentation and make sure you know how to use the versions JavaScript provides you:

* [`map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/map)
* [`reduce`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/Reduce)

## Use JavaScript Documentation to Learn More About Other Variations on `map` and `reduce`

Now that we understand the "character of collection processing," we are ready to use other methods to unleash its full power!

## `filter`

Look at the documentation for [`filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/filter). The syntax snippet is provided as:

```javascript
let newArray = arr.filter(callback(element[, index[, array]])[, thisArg]);
```

Here, we're told that on an array (`arr`), we add a `.filter` and then, between `()`, we provide a `callback` and a `thisArg`.

> **Remember:** Because of JavaScript's non-enforcement of _arity_, we don't **have** to provide all the arguments.

Possible parameter that support the `callback`:

1. `element`
2. `index` (optional)
3. `array` (optional)

JavaScript will move through the array that `filter()` was invoked on and pass the `element`, the `index` of that element, and the whole darn `array` to the callback (called in the documentation, "`callback`").

Yet again, because of _arity_ non-enforcement, we don't _have_ to add parameters for `index` or `array`, or `element` even. Furthermore, in our callbacks, we can name our parameters whatever we like. JavaScript always makes those 3 arguments _available_ to our callback. What to call them and whether to use them is entirely up to us.

Now what happens in `callback`? The documentation tells us:

> Function is a predicate, to test each element of the array. Return true to keep the element, false otherwise. It accepts three arguments...

This function runs and has access to the parameters we just explained. If the _call_ to `callback` returns `true`, that element will be added to an invisible "keeper" array; else, it's left out. We can use the `element` of the `array` of the `index` or (more typically) some interaction between them to create an expression that will return a boolean values from `callback`:

```javascript
[10, 20, 30, 40].filter(function() {
  return true;
});
//=> [10, 20, 30, 40] (map, basically)

[10, 20, 30, 40].filter(function(e) {
  return e < 30;
});
//=> [10, 20]

[10, 20, 30, 40].filter(function(e, index) {
  return index % 2 === 0;
});
//=> [10, 30] (elements with an even-numbered index)
```

1. Map a collection
2. Only accumulate the elements that return a truthy value from the callback

Obviously, how we adjust the return value of the callback will decide whether data we want is preserved of data we don't want is rejected.

## Memorize These Methods!

These are the collection-processing methods you should _**memorize**_ and practice heavily. They're going to be your friends every day in JavaScriptopia. There are other collection-processing methods that you might not memorize, but it's pretty common for a developer to realize when they're working in the "character of collection processing" and go back to the documentation to find the best function for the job.

* [`every`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/every): Check if all elements in the array satisfy the callback
* [`find`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/find): Find the first element in the array that satisfies the callback
* [`findIndex`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/findIndex): Find the first element in the array that satisfies the callback's index
* [`map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/map): Transform every element in the array to create a new array
* [`reduce`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/Reduce): Reduce every element in the array into a new value
* [`some`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/some): Check if any element in the array satisfies the callback
