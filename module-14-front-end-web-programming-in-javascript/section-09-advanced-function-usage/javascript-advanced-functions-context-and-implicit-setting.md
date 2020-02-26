# Lesson: Context and Implicit Setting (JavaScript Advanced Functions)

## Execution Context

When a function in JavaScript **_is called_**, it is provided an _execution context_. The _execution context_ is a JavaScript object that is either implicitly or explicitly passed at the time of the function's call. The implicit way of passing a context with a function is something we have to memorize and accept as part of the nature of JavaScript. The tools for explicitly passing a context at function call-time are the methods: `call()`, `apply()`, and `bind()`.

## Define `this`

The JavaScript keyword `this` returns the current _execution context_ while the function is being run. Whether that context was passed explicitly or implicitly, `this` returns it.

Some people think that `this` is a strange thing to call such an important concept. But pronouns like "this," "he," or "here" all refer to a _context_.

## Access Implicitly-Set Context in an Object-Contained Function Expression

When a function is called, it gets an execution context passed in. That context will be whatever the function was 'called on'—the object to the left og the `.` where it's called. In the below example, `byronPoodle` is the the left of the `.`. In `byronPoodle.warn()`, `warn` gets `byronPoodle` as its context:

```js
let byronPoodle = {
  name: "Byron",
  sonicAttack: "ear-rupturing atomic bark",
  mostHatedThing: "noises in the apartment hallway",
  warn: function() {
    console.log(`${this.name} issues an ${this.sonicAttack} when he hears ${this.mostHatedThing}.`)
  }
}
bryonPoodle.warn();

// LOG: Bryon issues an ear-rupturing atomic bark when he hears noises in the apartment hallway.
```

As you can see, when you call `someObject.someFunction()`, the context inside of `someFunction` will be the thing to the left of the `.`: `someObject`.

Here's another interesting example:

```js
let speak = function() { return `It ain't easy being ${this.name}.` };
let frog = { name: "Kermit" };
let pig = { name: "Miss Piggy" };
frog.speak = speak;
pig.speak = speak;
frog.speak === pig.speak
//=> true
frog.speak();
//=> "It ain't easy being Kermit."
pig.speak();
//=> "It ain't easy being Miss Piggy."
```

Again, the crucial realization is that the context used _inside_ the function `speak` is defined by what's "left of the dot." This is the general behavior for understanding context-setting in JavaScript.

## Access Implicitly-Set Global Object in a Function Expression

What happens if we invoke a function and it's **not** defined inside an object:

```js
let contextReturner = function() {
  return this;
}

contextReturner();
//=> window
contextReturner() === window;
//=> true
```

When no object is to the left of the function, JavaScript invisibly adds **the global object**. Thus `contextReturner` is, from JavaScript's point of view, the same as `window.contextReturner`.

A simple way of saying it: when you call `someFunction()`, the context inside of `someFunction` will be the thing to the left of the `.`. Since there's nothing there, JavaScript swaps in the global object.

In the browser-based JavaScript environment (or "JavaScript runtime"), the global object is called `window`. In NodeJS, it's called `global`.

Thus, in Chrome:

```js
let locationReturner = function() {
  return this.location.host;
}

locationReturner();
//=> URL host serving this page (e.g. developer.mozilla.org)
// Implicitly: window.locationReturner(); --> This will be `window` in the function
```

It's worth noting that even in a function inside of another function, the inner function's default context is still in the global object:

```js
function a() {
  return function b() {
    return this;
  }
}

a()() === window;
//=> true
```

## Prevent Implicitly Setting a Global Object in Function Call with `use strict`

We wish we could say that the default context was **always** the global object. It'd make things simple.

However, in JavaScript, if the engine see the string "use strict" inside the function, it will _stop_ passing the implicit _execution context_ of the global object. If JavaScript sees `"use strict"` at the top of a JavaScript code file, it will apply this rule (and other strict behaviors) to _all functions_.

```js
function looseyGoosey() {
  return this;
}

function noInferringAllowed() {
  "use strict"
  return this;
}

looseyGoosey() === window;
//=> true
noInferringAllowed() === undefined;
//=> true
```

There are really no guidelines as to which you'll see more. Some programmers think `strict` prevents confusing bugs; others think it's an obvious rule of the language and squelching it is against the language's love of functions. Generally, we advise you to think of the "default mode" as the one that permits an _implicit_ presumption of context.

### Access Implicitly-Set New Object in Object-Oriented Programming Constructor

An important place when `this` is implicitly set is when new instances of classes are created. Class definition and instance creation are hallmarks of object-oriented programming, a style you might not be familiar with in JavaScript. Rather than ignore this important case until later, we're going to cover it now, even though you might not be familiar with object-oriented programming.

It's for convenience and feels "natural" from a linguistic point of view: "The thing we're setting up should be the default context for work during its construction in its own function that's called `constructor`."

```js
class Poodle {
  constructor(name, pronoun) {
    this.name = name;
    this.pronoun = pronoun;
    this.sonicAttack = "ear-rupturing atomic bark";
    this.mostHatedThing = "noises in the apartment hallway";
  }

  warn() {
    console.log(`${this.name} issues an ${this.sonicAttack} when ${this.pronoun} hears ${this.mostHatedThing}.`);
  }
}
let b = new Poodle("Byron", "he");
b.warn();
// LOG: Bryon issues an ear-rupturing atomic bark when he hears noises in the apartment hallway.
```

## Use Available JavaScript Runtimes to Validate Understanding

There are two main JavaScript environments you'll encounter as you get started with JavaScript. Those environments are also called runtimes. They are:

1. In the browser
2. In the "shell" when running the NodeJS program

## Conclusion

To sum up the discussion so far:

1. Execution context is set at function call-time, implicitly or explicitly.
2. In "bare" function calls, the context is automatically set to the global object unless prevented by `"use strict"`.
3. In "non-bare" function calls, the context is automatically set to the "object to the left of the dot."
4. For object-oriented JavaScript, execution context defaults to the new thing being created in a class's `constructor`.

This covers the _implicit_ context-setting rules.

### Resources

- [Strict mode (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
