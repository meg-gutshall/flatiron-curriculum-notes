# Lesson: The Lost Context Bug (JavaScript Advanced Functions)

We've already learned about record-oriented programming and how, by using methods like `call()`, `apply()`, and `bind()`, we can change the default context of a function from the global context (`window` in the browser, `global` in NodeJS) as we see fit.

However, sometimes the rules of function execution interact in a way that leads to **_one particularly surprising bug_**: "the lost context bug." It's impossible to list _all_ the places where this bug could be triggered, but if you encounter something "strange" like what we're about to describe, you'll know how to proceed.

## Scenario

It's the All-Father Odin's birthday. His sons, Thor and Loki, would like to print him a birthday greeting using JavaScript. They know how to define objects and functions, so they've written a simple function that takes a configuration object as the _execution context_ and prints a JavaScript greeting card. The object looks like this:

```js
let configuration = {
  frontContent: "Happy Birthday, Odin One-Eye!",
  insideContent: "From Asgard to Nifelheim, you're the best all-father ever.\n\nLove,",
  closing: {
    "Thor": "Admiration, respect, and love",
    "Loki": "Your son"
  },
  signatories: ["Thor", "Loki"]
};
```

To display this, they wrote the following function:

```js
let printCard = function() {
  console.log(this.frontContent);
  console.log(this.insideContent);

  this.signatories.forEach(function(signatory) {
    let message = `${this.closing[signatory]}, ${signatory}`;
    console.log(message);
  });
};

printCard.call(configuration);
```

This doesn't work as planned. A quick debug shows that there **very much** is a property called `"Thor"` in `configuration.closing`:

```js
console.log(configuration.closing.Thor);
//=> LOG: Admiration, respect, and love
//=> undefined
```

Here is one of the most boggling problems in JavaScript: a bug created in the shadow of the all-too-easy-to-forget fact that function expressions and declarations **_inside_** of other functions **_do not automatically_** use the same context as the outer function.

## Debugging: Discovering the Nature of the Lost Context Bug

As a first step in getting this code working, let's add some `console.log()` calls so we can see what `this` is:

```js
let configuration = {
  frontContent: "Happy Birthday, Odin One-Eye!",
  insideContent: "From Asgard to Nifelheim, you're the best all-father ever.\n\nLove,",
  closing: {
    "Thor": "Admiration, respect, and love",
    "Loki": "Your son"
  },
  signatories: ["Thor", "Loki"]
};

let printCard = function() {
  console.log(this.frontContent);
  console.log(this.insideContent);

  console.log("Debug before forEach: " + this);
  this.signatories.forEach(function(signatory) {
    console.log("Debug inside: " + this);
    // let message = `${this.closing[signatory]}, ${signatory}`;
    console.log(message);
  });
};

printCard.call(configuration);

/* BEGIN LOG OUTPUT
/* Happy Birthday, Odin One-Eye!
/* From Asgard to Nifelheim, you're the best all-father ever.
/*
/* Love,
/* Debug before forEach: [object Object]
/* Debug inside: [object Window]
/* Debug inside: [object Window]
/* END LOG OUTPUT */
```

The `console.log()` statements reveal the bug. _Inside_ the `forEach`, the execution context **is not** the `configuration` object we used as a `this` arguments when calling the function `printCard()`. Instead, the `this` _inside_ the function expression passed to `forEach` is the global object (`window` or `global`).

## Solutions to the Lost Context Bug

Remember the rules of function invocation. A function defaults to getting the global scope as _execution context_ when it is called without "anything to the left of a dot." It **does not** get its parent function's _execution context_ automatically. There are many ways for programmers to solve this problem. The three most common are:

1. Pass a `thisArg`
2. Use a closure
3. Use the arrow function expression

### Solution 1: Avoid It!

Use a `thisArg` to avoid the lost context bug completely. Per the [`forEach` documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach), we could pass a `thisArg` argument to `forEach` as its second argument, after the function expression. This explicitly provides a context for the function used inside `forEach`. Doing so fixes our bug!

>**ASIDE**: This pattern works for `forEach` as well as `map` and other collection-processing methods. Consult their documentation to see where a `thisArg` is expected.

```js
let printCard = function() {
  console.log(this.frontContent);
  console.log(this.insideContent);

  this.signatories.forEach(function(signatory) {
    let message = `${this.closing[signatory]}, ${signatory}`;
    console.log(message);
  }, this);
};

printCard.call(configuration);

/* BEGIN LOG OUTPUT
/* Happy Birthday, Odin One-Eye!
/* From Asgard to Nifelheim, you're the best all-father ever.
/*
/* Love,
/* Admiration, respect, and love, Thor
/* Your son, Loki
/* END LOG OUTPUT */
```

In the call to `forEach`, we tell it to use (for its own context) the context the `printCard()` has at `this`. A slight variation on this idea would be to invoke `bind()` on the function expression in the `forEach`:

```js
let printCard = function() {
  console.log(this.frontContent);
  console.log(this.insideContent);

  let contextBoundForEachExpr = function(signatory) {
    let message = `${this.closing[signatory]}, ${signatory}`;
    console.log(message);
  }.bind(this);

  this.signatories.forEach(contextBoundForEachExpr);
};

printCard.call(configuration);

/* BEGIN LOG OUTPUT
/* Happy Birthday, Odin One-Eye!
/* From Asgard to Nifelheim, you're the best all-father ever.
/*
/* Love,
/* Admiration, respect, and love, Thor
/* Your son, Loki
/* END LOG OUTPUT */
```

### Solution 2: Closures

Use a closure to regain access to the lost context. Since we have the ability to "point to" our `this` context, we could assign that value to a variable and leverage function-level scope and _closures_ to regain access to the outer context.

```js
let printCard = function() {
  console.log(this.frontContent);
  console.log(this.insideContent);

  let outerContext = this;

  this.signatories.forEach(function(signatory) {
    let message = `${outerContext.closing[signatory]}, ${signatory}`;
    console.log(message);
  });
};

printCard.call(configuration);

/* BEGIN LOG OUTPUT
/* Happy Birthday, Odin One-Eye!
/* From Asgard to Nifelheim, you're the best all-father ever.
/*
/* Love,
/* Admiration, respect, and love, Thor
/* Your son, Loki
/* END LOG OUTPUT */
```

Many JavaScript developers define the variable we called `outerContext` by the name `self` which sure is confusing for Ruby programmers! In any case, by using an assignment with `let`, `var`, or `const`, we put the original context within the function-level scope that the inner function encloses as a closure. This means inside the inner function, we can get "back" to the outer function's context.

What we would _really_ like is for there to be a way to tell the `function` inside of `forEach` to:

1. _Not_ declare its own context **but also**
2. _Not_ require us to do some extra work with using `bind()` or a `thisArg`

In ES6, JavaScript gave us an answer: the "arrow function expression." This is our third and most-preferred option. Nevertheless, you will see all the other approaches used in framework code and in other codebases.

### Solution 3: Arrow Functions

Use an arrow function expression to create a function without its own context. The arrow function expression (often simply called an "arrow function") is yet another way of writing a function expression. They look different from "old style" function expressions, but the **_most important difference_** is that the arrow function is **_automatically bound_** to its parent's context and does not create a context of its own.

Many programmers think arrow functions are much more predictable since they do not create their own `this` during execution and instead "absorb" the context of their enclosing environment.

Since _the whole point_ of an arrow function is to **_not have its own execution context_**, we should not use `call()`, `bind()`, or `apply()` when executing them. Most of the time, you'll see them used like anonymous functions passed as first-class data into another function. See the typical `reduce()` example below.

An arrow function look like this:

```js
// The let greeter is merely the assignment, the expression begins at `(`
let greeter = (nameToGreet) => {
  let message = `Good morning ${nameToGreet}`;
  console.log(message);
  return "Greeted: " + nameToGreet;
};
let result = greeter("Max");
//=> LOG: Good morning Max
//=> Greeted: Max
```

Which, excluding context-switching differences, is the exact same as:

```js
let greeter = function(nameToGreet) {
  let message = `Good morning ${nameToGreet}`;
  console.log(message);
  return "Greeted: " + nameToGreet;
}.bind(this);
let result = greeter("Max Again");
//=> LOG: Good morning Max Again
//=> Greeted: Max Again
```

Because arrow functions are _so often used_ to take a value, do a single operation with it, and return the result, they have two shortcuts:

1. If you pass only one argument, you don't have to wrap the single parameter in `()`.
2. If there is only one expression, you don't need to wrap it in `{}` and the result of that expression is automatically returned.

>**Anti-shortcut**: If you _DO_ use `{}`, you must explicitly `return` the return value.

Thus, Thor and Loki can fix their problem and wish their father a happy birthday most elegantly with the following code:

```js
let printCard = function() {
  console.log(this.frontContent);
  console.log(this.insideContent);

  this.signatories.forEach(signatory =>
    console.log(`${this.closing[signatory]}, ${signatory}`)
  );
};

printCard.call(configuration);

/* BEGIN LOG OUTPUT
/* Happy Birthday, Odin One-Eye!
/* From Asgard to Nifelheim, you're the best all-father ever.
/*
/* Love,
/* Admiration, respect, and love, Thor
/* Your son, Loki
/* END LOG OUTPUT */
```

## Conclusion

The arrow function expression is a very important piece of syntax. While it lets us type less, its most important feature is that **_it carries its parent's context as its own_**.

### Resources

- [`forEach` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [Arrow Function Expressions (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [How Arrow Functions Leverage `this` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#No_separate_this)
