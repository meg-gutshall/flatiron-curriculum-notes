# Lesson: Context and Explicit Setting (JavaScript Advanced Functions)

We learned that when we invoke functions, JavaScript will make a context available inside the function. That context will be set to "whatever's to the left of the dot: or, when there's nothing to the left of the dot, the global object. JavaScript provides other means for specifying what _we_ want the context to be. These are the _explicit_ methods of setting execution context: `call()`, `apply()`, and `bind()`.

## Explicitly Override Context with `call()` and `apply()`

The methods on functions called `call()` and `apply()` allow us to override the _execution context_. We'll invoke the following functions in the way we already know, but also show how we could achieve the equivalent behavior by using `call()` and `apply()`:

```js
let asgardianBrothers = [
  {
    firstName: "Thor",
    lastName: "Odinsson"
  },
  {
    firstName: "Loki",
    lastName: "Laufeysson-Odinsson"
  }
];

function intro(person, line) {
  return `${person.firstName} ${person.lastName} says: ${line}`;
}

function introWithContext(line) {
  return `${this.firstName} ${this.lastName} says: ${line}`;
}

let phrase = "I like this brown drink very much, bring me another!";
intro(asgardianBrothers[0], phrase);
//=> LOG: Thor Odinsson says: I like this brown drink vary much, bring me another!
//=> undefined
intro(asgardianBrothers[0], phrase) === introWithContext.call(asgardianBrothers[0], phrase);
//=> true
intro(asgardianBrothers[0], phrase) === introWithContext.call(asgardianBrothers[0], [phrase]);
//=> true

let complaint = "I was falling for thirty minutes!";
intro(asgardianBrothers[1], complaint);
//=> LOG: Loki Laufeysson-Odinsson says: I was falling for thirty minutes!
//=> undefined
intro(asgardianBorthers[1], complaint) === introWithContext.call(asgardianBrothers[1], complaint);
//=> true
intro(asgardianBrothers[1], complaint) === introWithContext.apply(asgardianBrothers[1], [complaint]);
//=> true
```

When we first wrote a record-oriented program, we wrote functions in the style of `intro`. They took the record _as an argument_.

What if we told JavaScript that instead of the record being a _parameter_ (in addition to a phrase), it could be assumed as a _context_ and thus accessible via `this`. That's what we're doing above with the function `introWithContext` as invoked with either `call()` or `apply()`.

The `introWithContext` function expects only a catchphrase as an argument. Both `call()` and `apply()` take a `thisArg` argument as their first argument. That becomes the `this` _inside_ the function. In the case of `call()`, anything after `thisArg` gets passed to the function like arguments inside of a `()`. In the case of `apply()`, the contents in the array get destructured and passed to the function like arguments inside of a `()`.

>**ES6 ALERT**: Some might wonder: if we have destructuring of arrays, why do we need both `call()` and `apply()` since a destructured array, as required by `apply()`, could simply be destructured and fed to `call()`? Destructuring is a relatively new arrival to JavaScript, so before then JavaScript relied on two separate methods.

## Explicitly Lock Context for a Function with `bind()`

Let's supposed that we want to create the `introWithContext()` function, but have it permanently bound to `asgardianBrothers[0]`. As the adjective "bound" suggests, we use `bind()`:

```js
let asgardianBrothers = [
  {
    firstName: "Thor",
    lastName: "Odinsson"
  },
  {
    firstName: "Loki",
    lastName: "Laufeysson-Odinsson"
  }
];

function introWithContext(line) {
  return `${this.firstName} ${this.lastName} says: ${line}`;
}

let thorIntro = introWithContext.bind(asgardianBrothers[0]);
thorIntro("Hi, Jane");
//=> LOG: Thor Odinsson says: Hi, Jane
//=> undefined
thorIntro("I love snakes");
//=> LOG: Thor Odinsson says: I love snakes
//=> undefined
```

The `bind()` method **_returns a function that needs to be called_**, but wherever the function that `bind()` was called on had a `this` reference, the `this` is "hard set" to what was passed in to `bind()`.

## Conclusion

To sum up the explicit overrides:

1. Execution context is set in a function by invoking `call()` on the function and passing, as the first argument, a `thisArg` which is accessed via `this` in the function. Additional parameters to the function are listed after `,`.
2. Execution context is set in a function by invoking `apply()` on the function and passing, as first argument, a `thisArg` which is accessed via `this` in the function. Additional parameters to the function are stored in the second argument: as array containing arguments to the function.
3. Execution context can be locked in a function by invoking `bind()` on it and passing it a `thisArg`. The `bind()` function makes a copy of the functionality of its function but with all the `this` stuff locked in place and returns that function. That _new_ function can have arguments passed to it during its call with `()` as usual.

### Resources

- [`call()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/call)
- [`apply()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/apply)
- [`bind()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
