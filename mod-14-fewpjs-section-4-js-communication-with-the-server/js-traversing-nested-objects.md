---
description: 'Version 8: Module 14: Section 4: Lesson'
---

# Traversing Nested Objects (JS Fundamentals)

When we're looking for occurrences of a word or concept in a book, we often turn to the index. The index tells us where we can find more information on that concept by giving us a list (or page numbers) that we can use to loop up more information in the book. Additionally, it might include information that is related to the heading that we looked up in a _sublist_ (e.g. Animals > Vertebrate; Animals > Invertebrate). We link the connections between these lists in our heads, and it doesn't cause any issues to think of one list containing other lists. The index itself, after all, is a kind of list.

## Nested Objects: Objects in Objects

Remember when we said the values in an Object can be _anything_? Well, like the lists in the index in the example above, the values in an Object **can also be other Objects**.

```javascript
const person = {
  name: "Eileen Gutshall",
  occupation: {
    title: "Math Teacher",
    yearsHeld: 11
  },
  pets: [{
    species: "cat",
    name: "Dill"
  }, {
    species: "cat",
    name: "Pepper"
  }]
};
```

If you look closely, you can see that we've kind of seen this before when we looped over an array containing objects—so it should be familiar.

## How to Access Inner Properties

How would you imagine we'd access the `yearsHeld` field?

```javascript
person.yearsHeld;
```

We should see `undefined`. However, we can see that `yearsHeld` is a property of `occupation`, which in turn is a property of `person`. If we try `occupation.yearsHeld`, that will throw an error because `occupation` is not defined globally. It's only a property of `person`. Instead, let's try this:

```javascript
person.occupation;
//=> { title: "Math Teacher", yearsHeld: 11 }
```

Great! Now we're getting somewhere. Let's take it a step further:

```javascript
person.occupation.yearsHeld;
//=> 11
```

Now we get the value we want.

### Arrays in Arrays

Let's get a bit more abstract. In the above example, we had a name for each field that we wanted to access. If we had wanted to access the second pet's name, we could have done `person.pets[1].name`. Notice that we need to specify the _index_ in the `pets` array of the pet that we want (`[1]`).

Working with Arrays isn't all that different. It's just that instead of named properties of objects (and sub-objects), we have indexes of Arrays (and sub-arrays). And, of course, JavaScript is flexible enough that we can mix the two:

```javascript
const numberCollections = [1, [2, [4, [5, [6]], 3]]];
// Get number 6

[1, [2, [4, [5, [6]], 3]]]  // numberCollections;
[2, [4, [5, [6]], 3]]       // numberCollections[1];
[4, [5, [6]], 3]            // numberCollections[1][1];
[5, [6]]                    // numberCollections[1][1][1];
[6]                         // numberCollections[1][1][1][1];
6                           // numberCollections[1][1][1][1][0];
```

## Finding an Element in a Nested Array

### Use `for`

What is we have criteria for finding an element that we know is in a nested data structure? Let's implement a simple `find` function that takes two arguments: an Array (which can contain sub-arrays) and a function that returns `true` for the thing that we're looking for.

```javascript
function find(array, criteriaFn) {
  for (let i = 0; i < array.length; i++) {
    if (criteriaFn(array[i])) {
      return array[i];
    }
  }
};
```

**NOTE:** In JavaScript, functions are "first-class data", just like Numbers. In fact, writing functions that test a condition (also known as a "criteria function") is _**so**_ common, JavaScript even has an advanced syntax for writing functions that do one evaluation and return the value: _the arrow function syntax_. The example code below would do something like find all the members in the array that are even.

```javascript
// Regular function syntax
find([1, 2, ["a", "b"]], function(someNumber) { return someNumber % 2 === 0 })

// Arrow function syntax
find([1, 2, ["a", "b"]], someNumber => someNumber % 2 === 0 )
```

The above will work for a flat Array, but what if `array` looks like the `numberCollections` nested array and we want to find the first element that's `>5`? We'll need some way to move down the levels of the Array (like we described above). Let's figure this out step-by-step:

```javascript
function find(array, criteriaFn) {
  // Step 1 below
  let current = array;
  let next = [];

  // Step 2 below
  while (current || current === 0) {
    if (criteriaFn(current)) {
      // Step 3 below
      return current;
    }
    // Step 4 below
    if (Array.isArray(current)) {
      for (let i = 0; i < current.length; i++) {
        next.push(current[i]);
      }
    }
    // Step 5 below
    current = next.shift();
  }
  return null;
};
```

Our step-by-step process of finding a nested element as displayed in the code above:

1. Initialize two variables: `current` and `next`. `current` keeps track of the element that we're currently on; `next` is itself an Array that keeps track of the elements that we haven't looked at yet.
2. Use a `while` loop. This loop will only trigger if `current` is truthy, so when we exhaust `next` and then attempt to `shift()` `undefined` (when `next` is empty) onto `current`, we'll exit this loop.
3. Inside the `while` loop: If `current` satisfies the `criteriaFn`, then return it. This will then exit the entire function.
4. If `current` is an Array, we want to push all of its elements onto `next`.
5. After pushing any children (if there are any) of `current` onto `next`, we want to take the first element of `next` and make it the new `current` for the next pass of the `while` loop.

### Breadth-first Search

A [breadth-first search](https://en.wikipedia.org/wiki/Breadth-first\_search) is one of the main algorithms used to search through nested Objects. It earned its name because it looks at the the siblings of an Object (the elements that are on the same level) before looking at the children (the elements that are one or more levels down).
