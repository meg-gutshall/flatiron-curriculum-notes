# JavaScript Fundamentals: Hoisting

In JavaScript, "hoisting" deals with how function and variable declarations get raised to the top of the current scope. While it can cause problems, you can avoid these problems by following standard rules for where and how declarations should happen within your code.

## How Function and Variable Declarations Are Hoisted

Because the JavaScript engine reads a JavaScript file from top to bottom, it would make sense if we had to define a function before we invoked it:

```javascript
function myFunc() {
  return "Hello, world!";
}

myFunc();
//=> "Hello, world!"
```

However, we can invert those two steps and everything works fine:

```javascript
myFunc();

function myFunc() {
  return "Hello, world!";
}
//=> "Hello, world!"
```

This reads as though we're invoking the function prior to declaring it, but we're forgetting about the two-phase nature of the JavaScript engine. During the compilation phase, the engine skips right over the invocation and stores the declared function in memory:

```javascript
// The engine ignores all function invocations during the compilation phase.
myFunc();

function myFunc() {
  return "Hello, world!";
}
//=> "Hello, world!"
```

By the time the JavaScript engine reaches the execution phase, `myFunc()` has already been created in memory. The engine starts over at the top of the code and begins executing it line-by-line:

```javascript
// During the execution phase, the engine invokes myFunc(), which was already initialized during the compilation phase.
myFunc();

// During the execution phase, the engine will simply ignore this function declaration that was already carried out in the compilation phase.
function myFunc() {
  return "Hello, world!";
}
//=> "Hello, world!"
```

This process is called _hoisting_ because it feels like your declarations are being hoisted, or raised, to the top of the current scope. Your declarations **are** being evaluated before the rest of your code gets run, but hoisting is a bit of a misnomer: the physical location of the code isn't actually changing at all.

**_Top Tip:_** The best way to avoid any confusion brought on by function hoisting is to simply declare your functions at the very top of your code.

## Variable Declaration Best Practices

We're going to look at some of the hoisting issues caused by `var` because you will encounter this weirdness in legacy code. However, the fix is straightforward: use `const` and `let` and you'll have no variable hoisting issues.

Look at the following code:

```javascript
function myFunc() {
  console.log(hello);

  var hello = "World!";
}

myFunc();
// LOG: undefined
//=> undefined
```

In JavaScript, hoisting only applies to variables _declarations_; not variables _assignments_. As a quick refresher on that terminology:

```javascript
// Declaration:
let hello;

// Assignment:
hello = "World!";

// Declaration and assignment on the same line:
let goodnight = "Moon";
```

During the compilation phase, the JavaScript engine initializes the variable `hello`, storing it in memory. At this point, however, **no value is assigned to the variable**. As far as the JavaScript engine is concerned, the variable `hello` exists, but it contains `undefined`.

The variable will contain `undefined` until it's assigned a different value during the execution phase. Because of this odd behavior, you'll often see variable hoisting explained by taking some sample code...

```javascript
function myFunc() {
  console.log(hello);

  var hello = "World!";
}
```

and rearranging it to better indicate the order of events.

```javascript
function myFunc() {
  var hello;
  
  console.log(hello);

  hello = "World!";
}
```

When rearranged, it's clear that the variable it initialized as `undefined`, that is still contains `undefined` when it's logged out to the console, and that only after the logging event is it assigned the value of `"World!"`. However, armed with knowledge of what's going on under the surface (the distinct compilation and execution phases), we don't need to move the code around. When we invoke the following function, five things happen:

```javascript
function myFunc() {
  console.log(hello);

  var hello = "World!";

  return hello;
}

myFunc();
// LOG: undefined
//=> "World!"
```

1. The declaration of `hello` (`var hello`) is evaluated during the compilation phase, and the identifier, `hello`, is stored in memory as `undefined`.
2. The execution phase starts, and the JavaScript engine begins stepping through the code, executing each line in turn.
3. At the first line, `console.log(hello);`, the value `hello` is still `undefined`, and that's exactly what gets logged out to the console.
4. At the second line, the value `"World!"` is assigned to the variable `hello`. From this point on, all references to `hello` in this scope will evaluate to `"World!"`.
5. At the final line, we `return` the value of `hello`, which by now has been assigned and evaluates to `"World!"`.

### Avoiding the Confusion of `var` Hoisting

There are two ways to keep the JavaScript engine from "hoisting" your variables:

1. If, for whatever reason, your current project requires that you use `var`, follow our rule for function declarations and declare everything at the **top** of its scope. For example, if you need to declare a variable within a function, declare it at the **top** of that function:

    ```javascript
    // BAD
    function myBadFunc() {
      console.log("Just doing some other stuff before we get around to variable declarations.");

      var myVar = 42;
    }

    // GOOD
    function myGoodFunc() {
      var myVar = 42;

      console.log("Much better! The variable declaration is at the top of the scope created by 'myGoodFunc()', so there's no chance it gets 'hoisted'.");
    }

2. The most important thing to keep in mind is: **_don't use `var`_**. Variables declared with `const` and `let` do technically get "hoisted", but the JavaScript engine doesn't allow them to be referenced before they've been initialized.

Recommended:

```javascript
const myOtherVar = "Gotta assign a value for our beloved 'const'.";

myOtherVar;
//=> "Gotta assign a value for our beloved 'const'."
```

Not recommended:

```javascript
myVar;

let myVar = "Assignment is optional since we used 'let'.";
// ERROR: Uncaught ReferenceError: myVar is not defined
```

Since we can't even reference them, the whole problem of hoisted variables evaluating to `undefined` prior to assignment is unimportant.

## Resources

- [Back to Basics: JavaScript Hoisting](https://www.sitepoint.com/back-to-basics-javascript-hoisting/)
- [`var` Hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting)
