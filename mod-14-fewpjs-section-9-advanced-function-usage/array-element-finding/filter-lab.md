---
description: 'Version 8: Module 14: Section 9: Lab'
---

# Filter Lab (Iterators Drill)

We've all probably had the experience of filtering a selection of choices online. When shopping for clothing, we might have selected a single size so that we can consider only the search results we need. Or when ordering food online, we could have customized our results to only show restaurants currently open of offering delivery in our neighborhoods. Since it's such a common need for a user, it's also a common function for a programmer to run. There are many ways to filter in programming, but the easiest is to use `filter()`.

## How the `filter()` Method Works

If you have an array but only want some of the elements in it, that's where `filter()` comes in. You can think of `filter()` as a `for` loop that specifically keeps or sifts out certain values from an array. Consider the following code:

```javascript
let arr = [1, 2, 3, 4, 5, 6];
let even = [];
for(var i = 0; i < arr.length; i++) {
  if (arr[i] % 2 === 0) even.push(arr[i]);
};
//=> even = [2, 4, 6]
```

This code checks all of the values in the array. If the value can be divided by 2 with no remainder, it is considered an even number. Those values are then pushed onto the even array. This works, but now we have the `filter()` method to achieve the same result much more easily.

## Demonstrate `filter()`

The `filter()` method creates a new array with all elements that pass certain tests implemented by the provided function. The callback functions for both `filter()` and `map()` receive the same arguments (current item, index, and entire array), and work very similarly. The only difference is that the `filter()` method's callback needs to return either _true_ or _false_. If it returns _true_, the array keeps that element. If it returns _false_, the element is filtered out.

Here is the earlier example written with `filter()`:

```javascript
let arr = [1, 2, 3, 4, 5, 6];
let even = arr.filter(n => {
  return n % 2 === 0;
});
//=> even = [2, 4, 6]
```

This code's function returns _true_ if the element can be divided by 2 with no remainder (i.e. is even).

## Conclusion

The `filter()` method returns a new array created from all elements in the original array that meet certain conditions. When we use methods like `filter()`, we work directly with the current value instead of accessing it through an index (i.e. `array[i]`), avoid mutation of the original array (minimizing side-effects), and there's no need to manage a `for` loop with an empty array to push values into.

## Resources

* [Array.prototype.filter() (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/filter)
