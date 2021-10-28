---
description: 'Version 8: Module 14: Section 9: Lab'
---

# Map Lab (Iterators Drill)

As developers, we find ourselves responsible for all sorts of common, but tedious, tasks, such as iterating over arrays. Although a `for` loop or nesting in lists and collections will complete the task, we can take advantage of a method like `map()` to organize and optimize our code into building blocks of functions, which we can then chain together to create more readable and understandable functions.

## How the `map()` Method Works

`Array.prototype.map()` is an array method that iterates over all elements, allowing you to apply a function to each element in that array, and changing them into something else. The result is then returned as a _new array_, leaving the original array unmodified (but remember, **not** the elements we modify, that requires defensive copying). This is super important because it saves us from having to create a new array ourselves to copy stuff into there, **or** modifying the original elements in the array, which we may need later.

## Demonstrate `map()` with Arrays

We use `map()` when we want to perform an action on each element in the collection and "gather" the results into a new array.

We'll also use this as a chance to demonstrate some of the power of functions in JavaScript. We'll write `map()` **four times** so you can see how the iterator functions allow us to write more _expressive_ code.

### `for` and `for...of`

In this example, we are using a standard bit of iteration code. Because `for` and `for...of` are _general_ functions that can be used to do lots of things, another programmer won't be sure if the inner workings return values are important or not. For example:

```javascript
let students = ["harry", "ron", "hermione", "ginevra"];
let rollCall = [];

for (const student of students) {
  rollCall.push( student + " the wizard" );
};

//=> rollCall = ["harry the wizard", "ron the wizard", "hermione the wizard", "ginevra the wizard"];
```

When we write `.map()`, we are saying to other programmers: "Expect a new array to come out of this after each element is touched."

### `map()` with a Function Declaration

```javascript
function studentRollCall(student) {
  return student + " the wizard";
};

let students = ["harry", "ron", "hermione", "ginevra"];
let rollCall = students.map(studentRollCall);
//=> rollCall = ["harry the wizard", "ron the wizard", "hermione the wizard", "ginevra the wizard"];
```

With `map()`, we have a list of _n_ things and want that list of _n_ things to be transformed. Here, we're passing a function _as an argument_. Arguments can be things like numbers or strings, and, in JavaScript, **they can also be work.** Very few other programming languages allow that!

The iterator function `map()` expects to be _passed a function as an argument_ which they will hand each of their elements off to. In the case of `map()`, it hands each element to the function and stores the return value of the function into a new array.

This code is more _expressive_ because it lives up to the promise of `map()`. It creates a new array after each element is "touched" be a function.

One drawback to this code is that the `studentRollCall` function doesn't do much work. It just returns something that the `student` _already_ knew how to do. What if we use a function expression ("anonymous function") instead?

### `map()` with a Function Expression

```javascript
let students = ["harry", "ron", "hermione", "ginevra"];
let rollCall = students.map(function(student) {
  return student + " the wizard";
});
//=> rollCall = ["harry the wizard", "ron the wizard", "hermione the wizard", "ginevra the wizard"];
```

That's much shorter and it has all the same advantages of the previous version.

### `map()` with an Arrow Function

Thanks to arrow functions, we can shorten up the function expression to:

```javascript
// When the parameter list is only one element, we can drop ()!
let students = ["harry", "ron", "hermione", "ginevra"];
let rollCall = students.map( student => student + " the wizard" )
//=> rollCall = ["harry the wizard", "ron the wizard", "hermione the wizard", "ginevra the wizard"];
```

The code now fits on one line! This is much less noisy JavaScript code, so the _expressiveness_ has increased: `rollCall` is the resulting of mapping `students`.

## Using `map()` with Complex Data Structures

Let's use the `map()` function on a trickier data structure—a list of robots. To start things off, we have an array of robots. Now, let's activate all of them. An activated robot needs to be marked as such using the `isActivated` boolean, as well as have its number of modes doubled:

```javascript
const robots = [
  { name: "Johnny 5", modes: 5, isActivated: false },
  { name: "C3PO", modes: 3, isActivated: false },
  { name: "Sonny", modes: 2.5, isActivated: false },
  { name: "Baymax", modes: 1.5, isActivated: false }
];

const activatedRobots = robots.map(function (robot) {
  return Object.assign({}, robot, {
    modes: robot.modes * 2,
    isActivated: true
  });
});

console.log(activatedRobots);

/* Expected Output:
  [
    { name: "Johnny 5", modes: 10, isActivated: true },
    { name: "C3PO", modes: 6, isActivated: true },
    { name: "Sonny", modes: 5, isActivated: true },
    { name: "Baymax", modes: 3, isActivated: true }
  ]
*/
```

With the native `map()` function that is a property of the array's prototype, it gives us the exact same result! Now that we know how `map()` is implemented, it holds no more secrets for us. We can discard our own `map()` function and just use the `map()` property on arrays.

## Conclusion

`map()` takes two arguments: a callback and the optional context. The callback runs for each value in an array and returns each new value in the resulting array. It returns a new array that is the same length as the original array and saves time while making the code simpler and easy to read.

## Resources

* [`Array.prototype.map()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/map)
