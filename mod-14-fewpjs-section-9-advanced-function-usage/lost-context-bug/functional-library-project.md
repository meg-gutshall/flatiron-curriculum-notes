---
description: 'Version 8: Module 14: Section 9: Lab'
---

# Functional Library Project (JS Advanced Functions)

"Functional programming" is a style of programming like record-oriented or object-oriented programming. It's very popular in languages that _**LOVE**_ functions, like JavaScript.

## Creating a Functional Library

The entire `fi` library should be wrapped in an [Immediately Invoked Function Expression (IIFE)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE), like the example below:

```javascript
let fi = (function() {
  return {
    libraryMethod: function() {
      return "Start by reading the article!";
    },
    each: function() {
      // TODO
    }
  };
})();

fi.libraryMethod();
```

Wrapping a library in code is sometimes called "[The Module Pattern](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript)."

## Collection Functions (Arrays or Objects)

### fi.each

`fi.each(collection, callback)`

Iterates over a **collection** of elements, passing each element in turn to a **callback** function. Each invocation of `callback` is called with three arguments: an `element`, the `index` of the `element`, and a reference to the entire `collection`. If `collection` is a JavaScript object, the arguments for `callback` will be: the `value`, the `key` to the corresponding `value`, and once again a reference to the entire `collection`. **Returns the original collection for chaining.**

```javascript
fi.each([1, 2, 3], alert);
//=> Alerts each number in turn and returns the original collection

fi.each({one: 1, two: 2, three: 3}, alert);
//=> Alerts each number value in turn and returns the original collection
```

### fi.map

`fi.map(collection, callback)`

Produces a new array of values by mapping each value in `collection` through a transformation function (`callback`). The `callback` is passed three arguments: an `element`, the `index` of the `element`, and a reference to the entire `collection`. If `collection` is a JavaScript object, the arguments for `callback` will be: the `value`, the `key` to the corresponding `value`, and once again a reference to the entire `collection`. **Returns a new collection for chaining without modifying the original.**

```javascript
fi.map([1, 2, 3], function(num){ return num * 3; });
//=> [3, 6, 9]

fi.map({one: 1, two: 2, three: 3}, function(num, key){ return num * 3; });
//=> [3, 6, 9]
```

### fi.reduce

`fi.reduce(collection, callback, acc)`

Boils down a **collection** of values into a single value. `acc` (short for accumulator) starts as the initial state of the reduction, and with each successive step it should accumulate the return value of `callback`. The `callback` is passed three arguments: the `acc`, the current value in our iteration (the element array), and finally a reference to the entire `collection`.

```javascript
var sum = fi.reduce([1, 2, 3], function(acc, val, collection){ return acc + val; }, 0);
//=> 6
```

### fi.find

`fi.find(collection, predicate)`

Looks through each value in the `collection`, returning the first one that passes a truth test (`predicate`), or `undefined` if no value passes the test. The function returns as soon as it finds an acceptable element, ceasing traversal of the collection.

```javascript
var even = fi.find([1, 2, 3, 4, 5, 6], function(num){ return num % 2 === 0; });
//=> 2
```

### fi.filter

`fi.filter(collection, predicate)`

Looks through each value in the `collection`, returning an array of all the values that pass a truth test (`predicate`).

```javascript
var evens = fi.filter([1, 2, 3, 4, 5, 6], function(num){ return num % 2 === 0; });
//=> [2, 4, 6]
```

### fi.size

`fi.size(collection)`

Returns the number of values in the `collection`.

```javascript
fi.size({one: 1, two: 2, three: 3});
//=> 3
```

## Array Functions

### fi.first

`fi.first(array, [n])`

Returns the first element of an **array**. Passing `n` will return the first `n` elements of the array.

```javascript
fi.first([5, 4, 3, 2, 1]);
//=> 5

fi.first([5, 4, 3, 2, 1], 3);
//=> [5, 4, 3]
```

### fi.last

`fi.last(array, [n])`

Returns the last element of an **array**. Passing `n` will return the last `n` elements of the array.

```javascript
fi.last([5, 4, 3, 2, 1]);
//=> 1

fi.last([5, 4, 3, 2, 1], 3);
//=> [3, 2, 1]
```

### fi.compact

`fi.compact(array)`

Returns a copy of `array` with all falsy values removed. In JavaScript, quotations, `false`, `null`, `0`, `undefined`, and `NaN` are all falsy.

```javascript
fi.compact([0, 1, false, 2, '', 3]);
//=> [1, 2, 3]
```

### fi.sortBy

`fi.sortBy(array, callback)`

Returns a sorted copy of `array`, ranked in ascending order by the results of running each value through `callback`. The values from the original array should be retained within the sorted copy, just in ascending order.

```javascript
fi.sortBy([1, 2, 3, 4, 5, 6], function(num){ return Math.sin(num); });
//=> [5, 4, 6, 3, 1, 2]

var stooges = [{name: 'moe', age: 40}, {name: 'larry', age: 50}, {name: 'curly', age: 60}];
fi.sortBy(stooges, function(stooge){ return stooge.name; });
//=> [{name: 'curly', age: 60}, {name: 'larry', age: 50}, {name: 'moe', age: 40}]
```

### fi.flatten

`fi.flatten(array, [shallow])`

Flattens a nested **array** (the nesting can be to any depth).

If you pass `true` for the second argument, the array will only be flattened a single level.

```javascript
fi.flatten([1, [2], [3, [[4]]]]);
//=> [1, 2, 3, 4]

fi.flatten([1, [2], [3, [[4]]]], true);
//=> [1, 2, 3, [[4]]]
```

### fi.uniq

`fi.uniq(array, [isSorted], [callback])`

Produces a duplicate-free version of `array`, using `===` to test object equality. In particular, only the first occurrence of each value is kept.

```javascript
fi.uniq([1, 2, 1, 4, 1, 3]);
//=> [1, 2, 4, 3]
```

If you know in advance that `array` is sorted, passing `true` for `isSorted` will run a much faster algorithm.

```javascript
fi.uniq(['a', 'a', 'b', 'c', 'e', 'e', 'e', 'e'], true);
//=> ['a', 'b', 'c', 'e'] // Faster than unsorted
```

If you want to compute unique items based on a transformation, pass a callback function.

Specifically, if the callback function returns the same value that a previous execution of the `callback` also returned, we don't include that item in the return array -- _even if the elements from the original `array` are different_. The output array will be made up of a subset of the values from the original `array`, not the transformed values.

```javascript
fi.uniq([1, 2, 3, 6], false, (x => x % 3));
//=> [1, 2, 3]

fi.uniq([4, 8, 6, 5, 7], false, (x => x % 3));
//=> [4, 8, 6]
```

## Object Functions

### fi.keys

`fi.keys(object)`

Retrieves all the names of the enumerable properties of `object`.

```javascript
fi.keys({one: 1, two: 2, three: 3});
//=> ["one", "two", "three"]
```

### fi.values

`fi.values(object)`

Returns all of the values of the properties of `object`.

```javascript
fi.values({one: 1, two: 2, three: 3});
//=> [1, 2, 3]
```

### fi.functions

`fi.functions(object)`

Returns a sorted collection of the names of every function in `object`—that is to say, the name of every property whose value is a function.

```javascript
fi.functions(fi);
//=> ["compact", "each", "filter", "find", "first", "functions", "last", "map", "reduce", "size", "sortBy"]
```

## Conclusion

Building a functional library is a great experience for learning to see how many functions can build off of each other.

Expand your vocabulary by visiting a library like [Lodash](https://lodash.com) or [Ramda](https://ramdajs.com). Look a methods like Ramda's [filter](https://ramdajs.com/docs/#filter) or [flip](https://ramdajs.com/docs/#flip). Can you imagine how to write that?

## Resources

* [Lodash](https://lodash.com): A modern JavaScript utility library delivering modularity, performance & extras
* [Ramda](https://ramdajs.com): A practical functional library for JavaScript programmers
* [Master the JavaScript Interview: What is Functional Programming? (JavaScript Scene)](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)
