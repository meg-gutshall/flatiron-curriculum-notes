# Lesson: Array Element Finding

As developers, one of the things we need to do on a regular basis is locate thing in arrays. It's all well and good to be able to store data as developers, but it's pretty useless unless we're able to get it back out again. In JavaScript, there are two different methods that we use to locate data in arrays. For a more simple solution, we use `Array.prototype.indexOf()`. For more complex calculations, we use `Array.prototype.find()`.

## Find Elements in a Simple Array with `Array.prototype.indexOf()`

`Array.prototype.indexOf()` depends on one required parameter and one optional parameter. It compares the elements using the strict equality operator (`===`) and returns the index of the matching element:

```js
let cards = ['queen of hearts', 'jack of clubs', 'ten of diamonds', 'ace of spades'];
console.log(cards.indexOf('jack of clubs'));
//=> 1
```

The first parameter, the _item_ that you are looking for, is required. You can also pass in the _start_ postition like so:

```js
let cards = ['queen of hearts', 'jack of clubs', 'ten of diamonds', 'ace of spades'];
console.log(cards.indexOf('jack of clubs', 2));
//=> -1
```

However, if you pass in a start position that is after the element that you are looking for, or if the element that you are looking for is not in the array, `Array.prototype.indexOf()` will return `-1` to let you know.

## Find Elements in a More Complex Array with `Array.prototype.find()`

`Array.prototype.find()` refers to a function to execute on each value in the array, taking in three arguments:

```js
function isOdd(element, index, array) {
  return (element % 2 === 1);
};

console.log([4, 6, 8, 10].find(isOdd)); //=> undefined (not found)
console.log([4, 5, 8, 10].find(isOdd)); //=> 5
console.log([4, 5, 7, 8, 10].find(isOdd)); //=> 5
console.log([4, 7, 5, 8, 10].find(isOdd)); //=> 7
```

`Array.prototype.find()` takes in the element we'd like to find, the index at which we'd like to start, and the array, and returns the first element in the array that satisfies the condition specified by the function.

## Conclusion

Both `Array.prototype.indexOf()` and `Array.prototype.find()` can be very useful in different situations.

### Resources

- [`Object.prototype` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)
- [`Array.prototype.indexOf()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
- [`Array.prototype.find()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
