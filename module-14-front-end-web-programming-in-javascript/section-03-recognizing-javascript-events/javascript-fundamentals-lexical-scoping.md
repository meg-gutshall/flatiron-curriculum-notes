# Lesson: Lexical Scoping (JavaScript Fundamentals)

How does JavaScript decide which outer scope to place into the scope chain for a new function?

## The Concept of Lexical Scoping

In JavaScript, each declared function creates its own scope. _Lexical scope_ is scope that is based on where variables and blocks of scope are defined by the programmer at the time it's written, and solidified by the time the code is processed.

The _lexing_ phase of code compilation determines where and how all identifiers are declared, and how they will be looked up during execution. This mechanism also plays a role in being able to access certain variables throughout the code.

For example, the statement `let foo = "bar"` is split into **two** separate steps at lexing time:

1. `let foo` declares the variable in the scope before code execution.
2. `foo = "bar"` assigns the value `"bar"` to the variable `foo`, if it is found in the available scope.

## Lexical Scoping Informs the Scope Chain of a Function

Take a look at the following code snippet:

```js
const myVar = "Foo";

function first() {
  console.log("Inside first()");

  console.log("myVar is currently equal to:", myVar);
}

function second() {
  const myVar = "Bar";

  first();
}
```

JavaScript looks up the scope chain to perform identifier resolution. Given that information, what do you think  will get logged out to the console when we invoke `second()`? Let's try it out:

```js
second();
// LOG: Inside first()
// LOG: myVar is currently equal to: Foo
//=> undefined
```

At first glance, it might seem like `"Bar"` should get printed out. Inside `second()`, that string is assigned to the `myVar` variable right before `first()` is invoked:

```js
function second() {
  const myVar = "Bar";

  first();
}
```

However, the assignment of `myVar` as `"Bar"` is **not visible** to `first()`. This is because `second()` is **not** the parent scope of `first()`.

In the following diagram, the red `myVar` is declared in the global scope, and the green `myVar` is declared inside `second()`:

![JavaScript lexical scope](/public/images/front-end-web-programming-in-javascript/lexical-scope.png)

No variable named `myVar` exists inside `first()`. When the JavaScript engine reaches the second line of code inside the function, it has to consult the scope chain to figure out what `myVar` is:

```js
console.log("myVar is currently equal to:", myVar);
```

The engine's first (and only) stop in the scope chain is the global scope, where it finds a variable named `myVar`. The reference to `myVar` inside `first()` is pointed at that external variable, so `console.log()` prints out `myVar is currently equal to: Foo`.

`first()` is declared in the global scope and, when it comes to the scope chain, JavaScript functions don't care where they are invoked. **The only thing that matters is where they are declared.** When we declare a new function, the function asks, "Where was I created?" The answer to that question is the outer environment (the outer scope) that gets stored in the new function's scope chain.

In the example above, we typed our declaration for `first()` in the global scope, which gets stored in `first()`'s scope chain. When `first()` is invoked, the JavaScript engine can't find anything matching `myVar` locally, so it looked up the scope chain. The engine finds `myVar` in the outer scope—the global scope—with a value of `"Foo"`, which is what then gets printed out to the console.

By contrast, if we declare `first()` **_inside_** of `second()`, then `first()`'s reference to its outer scope points at `second()` instead of at the global scope:

```js
const myVar = "Foo";

function second() {
  function first() {
    console.log("Inside first()");

    console.log("myVar is currently equal to:", myVar);
  }

  const myVar = "Bar";

  first();
}
```

When we invoke `second()` this time, it creates a local `myVar` variable set to "Bar". Then, it invokes `first()`:

```js
second();
// LOG: Inside first()
// LOG: myVar is currently equal to: Bar
//=> undefined
```

While `first()` is executing, it again encounters the reference to `myVar` and realizes it doesn't have a local variable or function with that name. `first()` looks up the scope chain again, but this time `first()`'s outer scope isn't the global scope. It's the scope of `second()` because `first()` was declared **_inside_** of `second()`. So `first()` uses the copy of `myVar` from the `second()` scope, which contains the string `"Bar"`.

## Conclusion

Lexical scope is the scope defined by author-time decisions of where functions are declared. The lexing phase of compilation knows where and how all identifiers are declared, and determine how they will be looked-up during execution.

When a variable contains an unexpected value, understanding the scope chain will save you hours of painful debugging. When you're wondering where to declare a function so that it can access the proper variables, your familiarity with JavaScript's lexical scoping will be useful.

## Resources

- [JavaScript: Understanding the Weird Parts — The First 3.5 Hours](https://www.youtube.com/watch?v=Bv_5Zv5c-Ts) (Video)
- [What Is a Closure?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)
- [What Is Lexical Scope Anyway?](http://astronautweb.co/javascript-lexical-scope/)
