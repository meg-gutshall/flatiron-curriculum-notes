---
description: 'Version 8: Module 14: Section 9: Lab'
---

# Find Lab (Iterators Drill)

In any programming language, you'll perform operations on arrays. Looking in an array for a substring or set of characters is a common task. Sometimes you need to look for a _specific_ item in the array and return it. Given a string or array, you can iterate over its elements and perform actions. ES6 introduced a few new array methods, one of them being `find()`.

## Demonstrate `find()`

The `find` function behaves similar to others in JavaScript (like `filter`) that want a truthy/falsy result. `find()` returns the **first** element for which the function returns true—a single element:

```javascript
[1, 3, 5, 6, 8].find( e => e % 2 === 0);
```

**Note:** You could have multiple matches, but `find()` returns _only the first element_. This could lead to some bugs if you're not careful:

```javascript
let roommates = ["jess", "winston", "winston", "nick"];

roommates.find( s => s === "winston");
//=> winston

roommates.filter( s => "winston");
//=> [winston, winston]
```

## Conclusion

`Array.find()` is a built-in function in JavaScript which is used to get the value of the first element in the array that satisfies the provided condition. With this, you can quickly check all the elements of the array and return the first match.

## Resources

* [`Array.prototype.find()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/find)
