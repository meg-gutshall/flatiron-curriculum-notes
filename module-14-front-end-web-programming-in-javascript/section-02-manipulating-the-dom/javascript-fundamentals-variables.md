# JavaScript Fundamentals: Variables

"Saving" information to a variable allows us to _save_ a result so we can use it again later. Storing calculations to _temporary storage places_ is the heart of making efficient programs. It's a simple idea that has powerful consequences.

## Define a Variable

A variable is a container in which we can store values for later retrieval. Imagine a box that can hold any type of data: a `number`, `string`, `boolean`, `object`—even an `undefined`. We take some data that we want to store, place it inside the box, and hand the box off to the JavaScript engine, which stores it in memory. Now our data is safely cached until we need to access it again.

But how do we get the data back? How will the JavaScript engine know _which_ box to retrieve? We need to assign a name to our variable—a label for our box—so that we can tell the engine exactly which piece of stored data we want to access.

## Names Variables in JavaScript

Variable names in JavaScript can sometimes be complicated, but if you follow these three rules you'll be fine:

- Start every variable name with a lowercase letter. Variable names starting with a number are not valid.
- Don't use spaces. `camelCaseYourVariableNames` instead of `snake_casing_them`.
- Don't use JavaScript [reserved words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Reserved_keywords_as_of_ECMAScript_2015) or [future reserved words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Future_reserved_keywords).

It's important to note that case matters, so `javaScript`, `javascript`, `JavaScript`, and `JAVASCRIPT` are four different variables.

## Initialize Variables in JavaScript

The `var` reserved word is the classic way to declare a variable. It's been around since the inception of JavaScript, and it's what you will encounter in any pre-ES2015 code.

Creating new variables in JavaScript is really a two-step process. First, we declare the variable:

```js
var pi;
//=> undefined
```

The JavaScript engine sets aside a chunk of memory to store the declared variable. Then, we assign a value to that variable:

```js
pi = 3.14159;
//=> 3.14159
```

We can package both of the initialization steps—declaration and assignment—in a single line of code:

```js
var pi = 3.14159;
//=> undefined
```

### Multi-line Variable Assignment

You can easily declare multiple variables. Instead of repeating `var` over and over again, JavaScript allows us to do multi-line variable assignment. Every variable must be separated with a comma and the entire line must end with a semicolon.

Let's condense the below code into one line:

```js
var a = 5;
var b = 2;
var c = 3;
var d = {};
var e = [];
```

The above is equivalent to:

```js
var a = 5,
    b = 2,
    c = 3,
    d = {},
    e = [];
```

Which can be converted to:

```js
var a = 5, b = 2, c = 3, d = {}, e = [];
```

### Retrieving Variables

To retrieve a declared variable, refer to its name:

```js
pi;
//=> 3.14159
```

### Reassigning Variable Value

Changing the value of a variable in JavaScript works as follows:

```js
var pi = 3.14159;
pi;
//=> 3.14159
pi = 3.14;
pi;
//=> 3.14
```

### Variable Values

Upon declaration, all variables are automatically assigned the value of `undefined`. It's only after we assign a new value that the variable will contain something other than undefined. We can use the `typeof` operator to check the data type of the value currently stored in a variable:

```js
var language;
//=> undefined

typeof language;
//=> "undefined"

language = "JavaScript";
//=> "JavaScript"

typeof language;
//=> "string"
```

**_Top Tip:_** When writing JavaScript code, it's good practice to **_never_** set a variable equal to `undefined`. Variables will be `undefined` until we explicitly assign a value, so encountering an `undefined` variable is a strong signal that the variable was declared but not assigned prior to reference. That's valuable information that we can use while debugging, and it comes at no additional cost to us.

Once a variable has been created with `var`, we can reassign it to our heart's content:

```js
var pi = 3.14159;
//-> undefined

typeof pi;
//=> "number"

pi = "the ratio between a circle's circumference and diameter";
//=> "the ratio between a circle's circumference and diameter"

typeof pi;
//=> "string"
```

The data that's stored in our variable might change over time, but at any moment we can retrieve its current contents.

## Identify when to Use `const`, `let`, and `var` for Declaring Variables

Because of its ubiquity in legacy code and StackOverflow posts, it's important to get to know `var`. However, as we alluded to earlier, there is almost no reason to use `var` with the features JavaScript has post-2015. `var` comes with a ton of baggage in the form of scope issues, and allows developers to play a little too fast and loose with variable declarations.

### `let`

ES2015 introduced two new ways to create variables: `let` and `const`. Both solve all of `var`'s scope issues. Both also throw an error if you try to declare the same variable a second time:

```js
let pi = 3.14159;
//-> undefined

let pi = "the ratio between a circle's circumference and diameter";
//=> Uncaught SyntaxError: Identifier 'pi' has already been declared
```

Just like with `var`, we can still reassign a variable declared with `let`:

```js
let pi = 3.14159;
//-> undefined

pi = "the ratio between a circle's circumference and diameter";
//=> "the ratio between a circle's circumference and diameter"

typeof pi;
//=> "string"
```

### `const`

Using `let` instead of `var` will help you avoid silly errors like declaring the same variable at two different places within your code, but there's an even better option to use as your default: `const`. Declaring a variable with the `const` reserved word means that not only can it not be redeclared but it also **_cannot be reassigned_**. This is a good thing for three reasons:

1. When we assign a primitive value (any type of data _except_ an object) to a variable declared with `const`, we know that variable with _always_ contain the same value.
2. When we assign an object to a variable declared with `const`, we know that variable will _always_ point to the same object (though the object's properties can still be modified).
3. When another developer looks at our code and sees a `const` declaration, they immediately know that variable points to the same object or has the same value every other time it's referenced in the program. For variables declared with `let` or `var`, the developer cannot be so sure and will have to keep track of how those variables change throughout the program. The extra information provided by `const` is valuable, and it comes at no extra cost to you! Just use `const` as much as possible and reap the benefits.

```js
const pi = 3.14159;
//=> undefined

pi = 2.71828;
//=> Uncaught TypeError: Assignment to constant variable.
```

**_NOTE:_** With `let`, it's possible to declare a variable without assigning a value, just like `var`:

```js
let pi;
//=> undefined

pi = 3.14159;
//=> 3.14159
```

However, because `const` doesn't allow reassignment after the variable is initialized, we **must** assign a value right away:

```js
const pi;
//=> Uncaught SyntaxError: Missing initializer in const declaration

const pi = 3.14159;
//=> undefined
```

As your JavaScript powers increase with experience, you'll develop a more nuanced understanding of what to use where. However, now for, this is a good rule of thumb:

- **Use `var` ...** never.
- **Use `let` ...** when you know the value of a variable will change.
- **Use `const` ...** for _every_ other variable.

Best practice is to always declare variables with `const` and then, if you later realize that the value has to change over the course of your program, circle back to change it to `let`.

## Resources

- [Language basics crash course: Variables](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics#Variables)
- [Valid JavaScript variable names in ECMAScript 6](https://mathiasbynens.be/notes/javascript-identifiers-es6)
- [`var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [JavaScript ES6+: `var`, `let`, or `const`?](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75)
