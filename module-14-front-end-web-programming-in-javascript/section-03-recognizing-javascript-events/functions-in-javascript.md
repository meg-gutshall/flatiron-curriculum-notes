# Functions in JavaScript

Functions are the single most important unit of code in JavaScript. Much like a `<div>` or a `<section>` in HTML, functions serve as ways to group together related bits of JavaScript code. Grouped code is easier to read, debug, and improve.

## Abstraction

Abstraction comes from Latin roots, meaning "to pull away." It's the "take-away" or "impression" of a whole thing. As humans, we often take sets of single action or things and _abstract them_ into another word. That word that we "pull away" is the "abstraction." We also use abstractions to decide what does or doesn't fit into a group. Abstractions help us think about complex activities. Humans brought the pattern of "abstracting work" to JavaScript. Abstractions that hold work are called _functions_.

## Functions Are Abstractions

Functions combine series of steps under a new name. That's why they're _abstractions_. We'll call that the _function name_. More formally: **A function is an object that contains a sequence of JavaScript statements. We can execute or _call_ it multiple times.** To _call_ a function means to run the independent pieces that make it. Synonyms to call that you might see are _execute_ and _invoke_.

Let's describe a series of single, non-abstract tasks:

```javascript
console.log("Wake Byron the poodle");
console.log("Leash Byron the poodle");
console.log("Walk to the park with Byron the poodle");
console.log("Throw the frisbee for Byron the poodle");
console.log("Walk home with Byron the poodle");
console.log("Unleash Byron the poodle");
```

To abstract these single action into a collective name, we do:

```javascript
function exerciseByronThePoodle() {
  console.log("Wake Byron the poodle");
  console.log("Leash Byron the poodle");
  console.log("Walk to the park with Byron the poodle");
  console.log("Throw the frisbee for Byron the poodle");
  console.log("Walk home with Byron the poodle");
  console.log("Unleash Byron the poodle");
}
```

The code above is a _function declaration_. We've abstracted 6 different actions into 1 activity: `exerciseByronThePoodle`. Abstractions themselves can be lumped together _as if_ they were single things.

## How to Call a Function

To execute or call a function, you add `()` after its name. To execute the function we just defined in JavaScript, you run: `exerciseByronThePoodle()`. That `()` is also known as the _invocation operator_ because it tells JavaScript to invoke the function. A function must be _declared_ before it can be called.

## Generalization

Looking at our abstraction, `exerciseByronThePoodle()`, it's pretty concrete—the opposite of abstract. It's concrete because it only works for Byron the Poodle. Our function would be more abstract if it were written for _all dogs_, since Byron falls under the "all dogs" category. The process of moving from _concrete_ to _abstract_ is called "generalization" (or "abstraction" by some).

Let's make `exerciseByronThePoodle()` more general. Looking at the `console.log()` statements, we repeatedly refer to a dog's name and a dog's breed, which are both of type `String`. If we were to write them as JavaScript variables inside the function, we might write `dogName` and `dogBreed`.

Let's use string interpolation to generalize the body of our function.

```javascript
function exerciseByronThePoodle() {
  let dogName = "Byron";
  let dogBreed = "poodle";
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park with ${dogName} the ${dogBreed}`);
  console.log(`Throw the frisbee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
}
```

If we call this function, we'll get to same result as the original `exerciseByronThePoodle()`. Our problem now is that our function has the `dogName` and `dogBreed` locked in. If we could make is possible to tell each call of the function "Use these strings instead," we could get more general.

That's the purpose of _parameters_. Parameters are locally-scoped variables that are usable ("scoped") to inside the function. In our example, our variables `dogName` and `dogBreed` should become parameters. They're defined inside of the function declaration's `()`, like so:

```javascript
function exerciseDog(dogName, dogBreed) {
  ...
}
```

JavaScript will assign the _arguments_ of "Byron" and "poodle" to the parameters `dogName` and `dogBreed` when this function is called.

```javascript
function exerciseDog("Byron", "poodle");
```

The full function declaration for `exerciseDog` is:

```javascript
function exerciseDog(dogName, dogBreed) {
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park with ${dogName} the ${dogBreed}`);
  console.log(`Throw the frisbee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
}
```

Now, the parameters are usable inside the function body as if they had been set with `let` inside the function.

If expected arguments aren't given, the parameters won't be set. The parameters' values will be `undefined`. This is just like non-initialized variables; set them or else they're `undefined`. **This will not cause an error in JavaScript.**

We can assign default arguments to our parameters. While it's not as attention-grabbing as a real error, it's a helpful signal that we've run off the rails.

```javascript
function exerciseDog(dogName = "ERROR the Broken Dog", dogBreed = "Sick Puppy") {
  ...
}
```

## Return Values

Sometimes it's helpful to send something _back_ to the place where the function was called, kind of like a "summary" of what happened in the function.

```javascript
let weatherToday = "Rainy";

function exerciseDog(dogName, dogBreed) {
  if (weatherToday === "Rainy") {
    return `${dogName} did not exercise due to rain`;
  }
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park with ${dogName} the ${dogBreed}`);
  console.log(`Throw the frisbee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
  return `${dogName} is happy and tired!`;
}

let result = exerciseDog("Byron", "poodle");
console.log(result);
// => "Byron did not exercise due to rain"
```

When a function is called in JavaScript and encounters a `return` statement, it "returns" the value of the thing that appears to the right of the word. The thing could be a `String`, a `Number`, or an expression like `1 + 1`. When a `return` is reached in the code, no further code behavior happens. Above, if `weatherToday` is `truthy` **the only thing that happens** is the evaluation of the `String`. Return values can be saved to variables or used as inputs to other functions.

## Boilerplate Function Definition

JavaScript functions are defined:

```javascript
function functionName(argument1, argument2, argument3) {
  body code goes here
}
```

## Resources

- [Functions: Reusable Blocks of Code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions)
- [Function Return Values](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Return_values)
- [Function Declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
