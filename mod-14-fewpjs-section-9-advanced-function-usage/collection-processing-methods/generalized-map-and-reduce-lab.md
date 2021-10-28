---
description: 'Version 8: Module 14: Section 9: Lab'
---

# Generalized Map and Reduce Lab (JS Advanced Functions)

## Define the Term Callback

When we pass a function expression (an anonymous function) or the _pointer_ (variable name, declared function name) to a function as an argument, the passed function is known as a _callback_. Since the receiving function will execute, or _call_ that function at a later time; that is, it will _call_ it back, it is called a callback.

## Identify Duplication that Can Be Avoided with Callbacks

Let's look at this solution code from the previous lesson:

```javascript
function mapToNegativize(sourceArray) {
  let newArray = [];
  for (const el of sourceArray) {
    newArray.push(el * -1); // Unique work
  }
  return newArray;
};

function mapToNoChange(sourceArray) {
  let newArray = [];
  for (const el of sourceArray) {
    newArray.push(el); // Unique work
  }
  return newArray;
};

function mapToDouble(sourceArray) {
  let newArray = [];
  for (const el of sourceArray) {
    newArray.push(el * 2); // Unique work
  }
  return newArray;
};

function mapToSquare(sourceArray) {
  let newArray = [];
  for (const el of sourceArray) {
    newArray.push(el ** 2); // Unique work
  }
  return newArray;
};
```

As you can see, the only thing that varies between these functions is the line which we've labeled `// Unique work`. We want to get rid of that duplicated "noise" around those lines.

When you learned to create functions, you learned that the way to _abstract_ the function is to pass in the stuff that varies as an _argument_ in the _call_ of the function. We'd _like_ to do the same thing here. Fortunately, since JavaScript considers functions to be first-class, we can pass functions in as arguments _just like_ we pass strings and arrays.

## Pass a Callback to a Function

We pass a callback to a function, adding it to the arguments list inside the `()`:

```javascript
function sayHello(name = "") {
  console.log(`Hello${name}`);
};

let sayHola = function(name = "") {
  console.log(`Hola${name}`);
};

functionUsingCallback(sayHello, sayHola, function(name = "") {
  console.log(`Ni Hao${name}`);
})

function functionUsingCallback(en, es, zh, name) {
  ...
};
```

In this case, `functionUsingCallback` will receive each of the three functions passed to it and will store those functions in `en`, `es`, and `zh`. Now let's call those functions.

## Invoke a Callback from Within a Function

```javascript
function sayHello(name = "") {
  console.log(`Hello${name}`);
};

let sayHola = function(name = "") {
  console.log(`Hola${name}`);
};

functionUsingCallback(sayHello, sayHola, function(name = "") {
  console.log(`Ni Hao${name}`);
})

function functionUsingCallback(en, es, zh, name) {
  en();
  es();
  zh();
};

// Prints
Hello
Hola
Ni Hao
```

As we're familiar with, we _call_ the function by typing its _pointer_ name and adding `()`.

## Pass Data Between Functions and Callbacks

We can pass arguments when we invoke functions by putting them inside the `()`. By doing so, we can share knowledge from within the function to its passed-in callback(s).

```javascript
function sayHello(name = "") {
  console.log(`Hello${name}`);
};

let sayHola = function(name = "") {
  console.log(`Hola${name}`);
};

functionUsingCallback(sayHello, sayHola, function(name = "") {
  console.log(`Ni Hao${name}`);
}, " Gary")

function functionUsingCallback(en, es, zh, name) {
  en(name);
  es(name);
  zh(name);
};

// Prints
Hello Gary
Hola Gary
Ni Hao Gary
```

## Identify JavaScript's Non-enforcement of Arity

One interesting point about calling functions in JavaScript is that JavaScript doesn't require you to provide the number of arguments to the function that the function's parameters expect:

```javascript
function accidentProneMen(larry, curly, moe) {
  return `${larry}, ${curly}, and ${moe} are an insurance risk.`
};

accidentProneMen();
//=> undefined, undefined, and undefined are an insurance risk.
accidentProneMen("Fine");
//=> Fine, undefined, and undefined are an insurance risk.
accidentProneMen("Fine", undefined, "Howard");
//=> Fine, undefined, and Howard are an insurance risk.
```

In JavaScript (and many other disciplines/languages), the correspondence to the number of parameters specified _**is not enforced**_ as it is in C, Java, or Ruby. Notice, in JavaScript, you don't even have to define default values? JavaScript just thinks, 'Oh, you meant to call this function with nothing? Cool!'

The number of "how many arguments are expected" is called _arity_. Keep this in mind as you write your own `reduce`.
