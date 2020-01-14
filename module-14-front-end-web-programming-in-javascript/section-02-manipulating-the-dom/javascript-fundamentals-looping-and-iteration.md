# Code-along: Looping and Iteration (JavaScript Fundamentals)

Sometimes, we have to run the same code repeatedly. Instead of calling the same function over and over again, we use a loop! With a loop, we can write the repeated action **once** and perform the action on **every item in the collection**. Loops are used to execute the same block of code a specified number of times. In JavaScript, loops come in different flavors, but the main two are `for` and `while` loops.

## The `for` Loop

Of the loops in JavaScript, the `for` loop is the most common. The `for` loop is made up of four statements in the following structure:

```js
for ([initialization]; [condition]; [iteration]) {
  [loop body]
}
```

- Initialization
  - Typically used to initialize a **counter** variable
- Condition
  - An expression evaluated before each pass through the loop
    - If the expression evaluates to `true`, the statements in the loop body are executed
    - If the expression evaluates to `false`, the loop exits
- Iteration
  - A statement executed at the end of each iteration
  - Typically this will involve incrementing or decrementing a counter, bringing the loop ever closer to completion
- Loop body
  - Code that run on each pass through the loop

Use a `for` loop when you know exactly how many times you want the loop to run (for example, when you have an array of known size). The `for` loop is often used to iterate over every element in an array. Here's an example of a gift wrapping action using a `for` loop:

```js
const gifts = ["teddy bear", "drone", "doll"];

function wrapGifts(gifts) {
  for (let i = 0; i < gifts.length; i++) {
    console.log(`Wrapped ${gifts[i]} and added a bow!`);
  }

  return gifts;
}

wrapGifts(gifts);
// LOG: Wrapped teddy bear and added a bow!
// LOG: Wrapped drone and added a bow!
// LOG: Wrapped doll and added a bow!
//=> ["teddy bear", "drone", "doll"]
```

We started our counter, `i` at `0` because arrays have zero-based indexes. Our condition states that we should run the code in the loop body while `i` is less than `gifts.length` (`3` in the above example). Our iteration, `i++`, increments our counter by `1` at the end of each pass through the loop.

In our loop body, notice that we reference `gifts[i]`. Since `i` starts out as `0` during the first pass through the loop, `gifts[i]` is `gifts[0]` which returns `teddy bear`. Each loop `i` increments by one, therefore returning the next element in the array. After the third pass through the loop, we increment `i` to `3`, which is no longer less than `gifts.length`. Our condition evaluates to `false` and we exit the loop.

## The `while` Loop

The `while` loop is similar to a `for` loop, repeating an action in a loop based on a condition. Both will continue to loop until that condition evaluates to `false`. Unlike `for`, `while` only requires condition and loop statements.

```js
while ([condition]) {
  [loop body]
}
```

The initialization and iteration statements of the `for` loop have not disappeared though. In fact, we could rewrite out original `for` loop gift wrapping example using a `while` loop and achieve the exact same result:

```js
const gifts = ["teddy bear", "drone", "doll"];

function wrapGifts(gifts) {
  let i = 0; // The initialization moves OUTSIDE the body of the loop!
  while (i < gifts.length) {
    console.log(`Wrapped ${gifts[i]} and added a bow!`);
    i++; // The iteration moves INSIDE the body of the loop!
  }

  return gifts;
}

wrapGifts(gifts);
// LOG: Wrapped teddy bear and added a bow!
// LOG: Wrapped drone and added a bow!
// LOG: Wrapped doll and added a bow!
//=> ["teddy bear", "drone", "doll"]
```

Notice that we've just moved the initialization and iteration statements—declaring the `i` variable outside the loop and now incrementing it _inside_ the loop.

**CAUTION:** When using `while` loops, it is easy to forget to involve iteration. Leaving iteration out can result in a condition that _always_ evaluates to `true`, causing an infinite loop!

Because of their design, `while` loops are sometimes used when we _want_ a loop to run an indeterminate amount of times. If we were pseudocoding out a program for planting a garden, we could use a `while` loop to organize the work.

```js
function plantGarden() {
  let keepWorking = true;
  while (keepWorking) {
    chooseSeedLocation();
    plantSeed();
    waterSeed();
    keepWorking = checkForMoreSeeds();
  }
}
```

We can imagine that _while_ we have seeds, we take the same steps over and over.

## When to Use `for` and `while`

JavaScript, like many programming languages, provides a variety of looping options. Loops like `for` and `while` are actually just slight variations of the same process. By providing a variety, we as programmers have a larger vocabulary to work with. Often, you will see `while` loops simply being used as an alternative to `for` loops.

```js
let countup = 0;
while (countup < 10) {
  console.log(countup++);
}
```

This is perfectly fine as an alternative way to describe:

```js
for (let countup = 0; countup < 10; countup++) {
  console.log(countup);
}
```

Most of the time, a regular `for` loop will suffice. It's by far the most common looping construct in JavaScript. A general heuristic for choosing which loop to use is to first try a `for` loop. If that doesn't serve your purposes, then go ahead and try a `while` or [`do...while`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration#do...while_statement) loop. Also, remember that you can always refer to the [documentation on these loops](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration) at any time. Just don't forget: with `while`, make sure you are updating the condition on each loop so that the loop eventually terminates!

## Resources

- Codecademy
  - [`for` loop](http://www.codecademy.com/glossary/javascript/loops#for-loops)
  - [`while` loop](http://www.codecademy.com/glossary/javascript/loops#while-loops)
- MDN
  - [`for` loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)
  - [`while` loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)
