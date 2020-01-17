# Lab: Basic Functions Review Lab (JavaScript Advanced Functions)

## Define a Function Using Function Declaration

In JavaScript, the most common way to define functions is with **function declaration**:

```js
function razzle() {
  console.log("You've been razzled!");
}
```

The word `razzle` becomes a _pointer_ to some stored, potential, not-yet-actually-run bit of work (the function). We use the _pointer_ to _call_ or _invoke_ the function. We _call_ the function by adding `()` after the _pointer_.

```js
function razzle() {
  console.log("You've been razzled!");
}

razzle();
//=> "You've been razzled!"
```

Interestingly, you can write function declarations _after_ you call them:

```js
razzle();
//=> "You've been razzled!"

function razzle() {
  console.log("You've been razzled!");
}
```

Functions can be passed arguments, given default arguments, etc. Here's a brief code synopsis:

```js
function razzle(lawyer="Billy", target="'em") {
  console.log(`${lawyer} razzle-dazzles ${target}!`);
}

razzle();
//=> Billy razzle-dazzles 'em!
razzle("Methuselah", "T'challah");
//=> Methuselah razzle-dazzles T'challah!
```

## Define the Term Hoisting

JavaScript's ability to call functions _before_ they appear in the code is called _hoisting_. For hoisting to work, **the function must be defined as a function declaration.**

## Define a Function Using a Function Expression

Early in your programming career, you probably learned that programming languages feature _expressions_: arrangements of constants, variables, and symbols that, when interpreted by the language, produce a _value_.

```js
1 + 1; //=> 2
"Razzle " + "dazzle!"; //=> "Razzle dazzle!"
```

By analogy, if we agree that JavaScript has function _expressions_ that look like this:

```js
function() {
  console.log("Yet more razzling");
}
```

...what is in the variable `fn` at the end of this block of code?

```js
let fn = function() {
  console.log("Yet more razzling");
}
```

This **function expression** evaluates to "stored work." Instead of the value `2` when `1 + 1` is evaluated, in `fn` JavaScript stores _work_—something that's much harder to visualize than `2`! If we ask JavaScript what's in `fn`, it says:

```js
let fn = function() {
  console.log("Yet more razzling");
} //=> undefined

fn; //=> ƒ () { console.log("Yet more razzling") }
```

Here, Chrome tells us that `fn` points to an unexecuted function, a "frozen" function, a "potential" function, a "recipe" for work. The Chrome console symbolizes this "frozen work" by putting the function definition after the `ƒ` character.

Here, `fn` is a _pointer_ to the stored block of work. But the work is merely _potential_, it hasn't been _done_ yet. Just as with **function declaration**, we need to _invoke_ or _call_ the function.

To **do** to work, to make the potential real, we add `()` to the end, optionally adding arguments:

```js
let fn = function() {
  console.log("Yet more razzling");
} //=> undefined

fn; //=> ƒ () { console.log("Yet more razzling") }
fn(); //=> "Yet more razzling"
```

In any case, a **function expression** comes about when we write `function() {...}` and assign it to a variable. Very importantly, **_function expressions are not hoisted_**. Since we assign these expressions to variables, we'd expect things to operate in the same way they do when we assign a string to a variable or the result of an arithmetic expression to a variable. Those assignments are not hoisted, thus neither is a function expression.

## Define the Term Anonymous Function

We also call the expression that produces a function that uses the template `function() {...}` an **anonymous function.** In the previous example, the following was the anonymous function:

```js
function() {
  console.log("Yet more razzling");
}
```

Unlike a **_function declaration_**, there's no function name in front of the `()`. Since anonymous means, "without a name," this function is called, sensibly enough, an anonymous function.

## Define an IIFE: Instantly-Invoked Function Expression

As a thought experiment, what happens here:

```js
(function(baseNumber) { return baseNumber + 3 })(2); //=> ?
```

We recognize the first `()` as being those that we might use from arithmetic to make something happen first in terms of order-of-operations. In the example below, `*` should happen first, but instead, it happens after `-` since the `()` evaluation is performed earlier:

```js
( 3 - 4 ) * 2 //=> -2
```

So in the IIFE statement, the first parentheses return an anonymous function. It's like we assigned an anonymous function to a variable name, but didn't do the actual assignment and are instead left the right-hand side of the assignment: a thing that can be invoked (instantly).

The second `()` are the `()` of function invocation like `sayHello()` having `()` after the `o`. It means, do the work in the function identified by the name `sayHello`.

Put these two components together and we're "invoking" the function immediately after defining it. That would make the function we're doing that upon an "Instantly-Invoked Function Expression" (IIFE, for short).

```js
(function(baseNumber) { return baseNumber + 3 })(2); //=> 5
```

Interestingly, any variables, functions, arrays, etc. that are defined _inside_ of the function expression's body _can't_ be seen _outside_ of the IIFE. It's like openings up a micro-dimension, a bubble-universe, doing all the work you could ever want to do there, and then closing the space-time rift.

## Define the Term Function-level Scope

JavaScript exhibits function-level scope. This means that if a function is defined _inside another_ function, the inner function has access to all the parameters (variables passed in) as well as any variables defined in the function. This moves backward recursively too. Each of the enclosing parents' scopes are made available via the _scope chain_.

Consider this code:

```js
function outer(greeting, msg="It's a fine day to learn") { // 2
  let innerFunction = function(name, lang="Python") { // 3
    return `${greeting}, ${name}! ${msg} ${lang}`; // 4
  }
  return innerFunction("student", "JavaScript"); // 5
}

outer("Hello"); // 1
//=> "Hello, student! It's a fine day to learn JavaScript"
```

1. We call `outer`, passing `"Hello"` as an argument.
2. The argument (`"Hello"`) is saved in `outer`'s `greeting` parameter. The other parameter, `msg`, is set to default value.
3. Here's our old friend the function expression. It expects two arguments which it stores in the parameters `name` and `lang` with `lang` being set as a default to `"Python"`. This expression is saved in the local variable `innerFunction`.
4. Inside `innerFunction`, we make use of both the parameters `name` and `lang` **_as well as_** the parameters of `innerFunction`'s containing (parent) function, `outer`. `innerFunction` gets access to `outer`'s variables.
5. Inside `outer`, we invoke `innerFunction`.

This might look a little bit weird, but it generally make sense to our intuition about scopes: inner thing can see their parent outer things. But with a simple change, something miraculous can happen:

```js
function outer(greeting, msg="It's a fine day to learn") { // 2
  let innerFunction = function(name, lang="Python") { // 3
    return `${greeting}, ${name}! ${msg} ${lang}`; // 4
  }
  return innerFunction
}

outer("Hello")("student", "JavaScript"); // 1, 5
//=> "Hello, student! It's a fine day to learn JavaScript"
```

Amazingly, this code work **_the exact same._** Even if the inner function `innerFunction` is invoked **outside** the parent function, it **_still_** has access to those parent function's variables. It's like a little wormhole in space-time to the `outer`'s scope!

Let's tighten this code up once more instead of assigning the function expression to `innerFunction`, let's just return the function expression:

```js
function outer(greeting, msg="It's a fine day to learn") {
  return function(name, lang="Python") {
    return `${greeting}, ${name}! ${msg} ${lang}`;
  }
}

outer("Hello")("student", "JavaScript");
//=> "Hello, student! It's a fine day to learn JavaScript"
```

Our "inner" function is now a returned **anonymous function.** To repeat: When it came into existence, it inherited the values in `outer`'s parameters `greeting` and `msg`. When we invoked `outer` we provided the arguments for `greeting` and left `msg` as the default. `outer` then returned an anonymous function that had its uses of `greeting` and `msg` set. It was almost as if `outer` returned:

```js
return function(name, lang="Python") { // The "inner" function
  return `Hello, ${name}! It's a fine day to learn ${lang}`;
}
```

We invoked the returned of "inner" function by adding `()` and passing the arguments `"student"` and `"JavaScript"` which we then loaded into `name` and `lang` inside the inner function. This filled in the final two values inside of the template string and effectively returned:

```js
return `Hello, student! It's a fine day to learn JavaScript`;
//=> "Hello, student! It's a fine day to learn JavaScript"
```

Keep in mind, it's not the case that we have to invoke functions like this:

```js
outer("Hello")("student", "JavaScript");
```

We could:

```js
let storedFunction = outer("Hello");
// ...lots of other code
storedFunction("student", "JavaScript");
//=> "Hello, student! It's a fine day to learn JavaScript"
```

## Define the Term Closure

In the previous example, we could call the "inner" function, the **anonymous function** a "closure." It "encloses" the function-level scope of its parent. And, like a backpack, it can carry out the knowledge that it saw—_even when you're out of the parent's scope._

Recall the IIFE discussion, since what's inside an IIFE can't be seen, if we wanted to let just tiny bits of information leak back out, we might want to pass that information back out, through a closure.

**Note:** We're also using destructuring assignment. Don't forget your ES6 tools!

```js
let [answer, theBase] = (
  function(thingToAdd) {
    let base = 3;
    return [
      function() { return base + thingToAdd },
      function() { return base }
    ];
  }
)(2);

answer(); //=> 5
console.log(`The base was ${theBase()}`);
//=> The base was 3
```

## Define the Term Scope Chain

The mechanism behind all the cool stuff we just saw is the _scope chain_ which allows functions defined in functions to access all their parent scopes' variables. Here's a simple example:

```js
function demoChain(name) {
  let part1 = 'hi';
  return function() {
    let part2 = 'there';
    return function() { // Innermost
      console.log(`${part1.toUpperCase()} ${part2} ${name}`);
    }
  }
}

demoChain("Dr. Stephen Strange")()();
//=> HI there Dr. Stephen Strange
```

Through the _scope chain_, the function labeled `// Innermost` has access to `name`, `part1`, and `part2` when it is called and runs the `console.log()` statement.

## Conclusion

This was just a recap of the basics of function declaration, invocation, and function scope.

### Resources

- [First-class Function (Wikipedia)](https://en.wikipedia.org/wiki/First-class_function)
- [What Is Meant by 'First Class Object'? (StackOverflow)](https://stackoverflow.com/questions/705173/what-is-meant-by-first-class-object)
- [Functions Are First Class Objects in JavaScript (Helephant via the Wayback Machine)](https://web.archive.org/web/20170606141950/http://helephant.com/2008/08/19/functions-are-first-class-objects-in-javascript/)
- [Expressions Versus Statements in JavaScript (2ality)](http://2ality.com/2012/09/expressions-vs-statements.html)
- [Functions (MDN)](https://developer.mozilla.org/en-US/docs/web/JavaScript/Reference/Operators/function)
- [Statements and Declarations (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements)
