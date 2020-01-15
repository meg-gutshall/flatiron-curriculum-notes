# Lesson: Scope (JavaScript Fundamentals)

## How Scope Works in JavaScript

Scope is the concept of **where something is available**. In JavaScript, scope is defined by where declared variables and methods are available within our code.

Every piece of JavaScript code is run in an _execution context_. In a JavaScript execution context, we have access to all of the variables and functions declared in that context. Within an execution context, we can write an expression that references a variable or invokes a function declared in the same context.

## Identifying Different Types of Scope

### Global Scope

Up to this point, almost all of the JavaScript code we've written has lived in the _global execution context_. Variables and functions declared in the global execution context—in the _global scope_—are accessible everywhere in your JavaScript code.

![JavaScript global execution context](/public/images/front-end-web-programming-in-javascript/global-scope-01.png)

Here's what that looks like in JavaScript:

```js
// `myFunc` is declared in the global scope and available everywhere in your code
function myFunc() {
  return 42;
}
//=> undefined

// `myVar` is able to reference and invoke `myFunc` because both are declared in the same scope (the global execution context)
const myVar = myFunc() * 2;
//=> undefined

myVar;
//=> 84
```

![JavaScript global execution context (continued)](/public/images/front-end-web-programming-in-javascript/global-scope-02.png)

**_Top Tip:_** If a variable or function is **not** declared inside a function or block, it's in the global execution context.

### Function Scope

When we declare a new function and write some code in the function body, we're no longer in the global execution context. The function creates a new execution context with its own scope. Inside the function body, we can reference variables and functions declared in the function's scope.

```js
function myFunc() {
  const myVar = 42;

  return myVar * 2;
}
//=> undefined

myFunc();
//=> 84
```

However, from outside the function, we can't reference anything declared inside of it.

```js
function myFunc() {
  const myVar = 42;
}
//=> undefined

myVar * 2;
// Uncaught ReferenceError: myVar is not defined
```

### Block Scope

A block statement also creates its own scope... kind of. As of ES2015, JavaScript has partial support for block scoping.

Variables declared with `var` are **not** block-scoped.

```js
if (true) {
  var myVar = 42;
}

myVar;
//=> 42
```

However, variables created with `const` and `let` **are** block-scoped.

```js
if (true) {
  const myVar = 42;

  let myOtherVar = 9001;
}

myVar;
// Uncaught ReferenceError: myVar is not defined

myOtherVar;
// Uncaught ReferenceError: myOtherVar is not defined
```

This is yet another reason to **never use** `var`. As long as you stick to declaring variables with `const` and `let`, what happens in block stays in block.

## Best Practices in Defining Scope

In a perfect world, you'd always remember to declare new variables with `const` and `let` and you'd never run into any scoping issues. However, it's inevitable that at some point, you're going to forget the `const` or `let` and accidentally do something like:

```js
firstName = "Ada";
```

Variables created without a `const`, `let`, or `var` keyword are **always globally-scoped**, regardless of where they sit in your code. Even if you create it inside of a function or a block, it will still be globally-scoped without that `const`, `let`, or `var` keyword.

Declaring global variables and functions should only be used as a last resort if you absolutely need access to something **everywhere** in your program. In general, it's best practice to make variables and functions available only where they're needed—and nowhere else. Making a variable available in a place that shouldn't have access to it can only lead to bad things and make your debugging process more complex. The more pieces of code that can access a given variable, the more places you have to check for bugs if/when that variable contains an unexpected value... So keep your scopes small and specific!

## Conclusion

We've now covered how scope works in JavaScript. We talked about how our declared variables and methods have their own execution contexts and global-, function-, and block-level scopes. We also discussed that it's best practice to make variables and functions available only where they're needed.

