# JavaScript Fundamentals: Conditionals

In programming, the logic of a code let's us dictate that we only want an action to happen _if_ a certain condition is met. This is called **control flow**.

## The Makeup of an Expression in JavaScript

A JavaScript expression is **a unit of code that returns a value**. Primitive values are expressions because they resolve to a value:

```js
9;
//=> 9

('Hello, world!');
//=> "Hello, world!"

false;
//=> false
```

So are arithmetic and string operations. This code resolves to the number `64`:

```js
8 * 8;
//=> 64
```

This resolves to the string `"Hello, world!"`:

```js
'Hello, ' + 'world!';
//=> "Hello, world!"
```

Same for comparison and assignment operations. The comparison resolves to the boolean `true`:

```js
2 > 1;
//=> true
```

Variable declarations are **NOT** expressions...

```js
let answer;
```

Variable assignments **ARE**, resolving to the assigned value (`42`, in this case):

```js
answer = 42;
//=> 42
```

Finally, references to variables are also expressions, resolving to the value contained in the variable:

```js
const fullName = 'Ada Lovelace';

fullName;
//=> "Ada Lovalace"
```

## Organize Code Using Block Statements

A _block statement_ is a pair of curly braces (`{ }`) used to group JavaScript statements. It plays a role in conditional statements, loops, and functions.

```js
{
  ('This line is a JavaScript statement nested inside a block statement!');

  // This is also a statement nested inside a block:
  5 * 5 - 5;

  // And so are these:
  const weCan = 'group multiple statements';

  const suchAs = 'these variable declarations';

  const insideA = 'block statement.';
}
//=> 20
```

Block statements return the value of the last evaluated expression inside the curly braces. Remember, the variable declarations are _not_ expressions, so the values of `5 * 5 - 5` is returned.

**Note:** The statement above _implicitly_ returns `20`, the value returned by `5 * 5 - 5`, when evaluated. The **implicit return is something unique to block statements** like the ones we use for `if...else` and loop statements. In the case of functions, we need to _explicitly_ use the word `return` to tell JavaScript what we want the output to be (if we want one at all).

## The Difference Between Truthy and Falsy Values

_Truthiness_ and _falsiness_ indicate what happens when the value is converted into a boolean. If, upon conversion, the value becomes `true`, we say that it's a **truthy** value. If it becomes `false`, we say that it's **falsy**.

In JavaScript, the following values are **falsy**:

- `false`
- `null`
- `undefined`
- `0`
- `NaN`
- An empty string (` `, `''`, `""`)

**_Every other value is truthy._**

To check whether a value is truthy or falsy in our browser's JS console, we can pass it to the global `Boolean` object, which converts the value into its boolean equivalent:

```js
Boolean(false);
//=> false

Boolean(null);
//=> false

Boolean(undefined);
//=> false

Boolean(0);
//=> false

Boolean(NaN);
//=> false

Boolean('');
//=> false

Boolean(true);
//=> true

Boolean(42);
//=> true

Boolean('Hello, world!');
//=> true

Boolean({ firstName: 'Brendan', lastName: 'Eich' });
//=> true
```

**Note:** `document.all` is also falsy, but don't worry about that too much—it's an imperfect solution for legacy code compatibility.

## Using Conditional Statements

In JavaScript, we use three structures for implementing condition-based control flow: the `if...else` statement, `switch` statement, and ternary operator.

### `if` Statement

`if` statements are the most common type of conditional, and they're pretty straightforward:

```js
if (condition) {
  // Block of code
}
```

If the condition returns a **truthy** value, run the code inside the **block**:

```js
const age = 30;

let isAdult;

if (age >= 18) {
  isAdult = true;
}

isAdult;
//=> true
```

If the condition returns a **falsy** value, do nothing:

```js
const age = 14;

let isAdult;

if (age >= 18) {
  isAdult = true;
}

isAdult;
//=> undefined
```

### `else` Clause

If we want to run some code when condition returns a **falsy** value, we can use an `else` clause:

```js
const age = 14;

let isAdult;

if (age >= 18) {
  isAdult = true;
} else {
  isAdult = false;
}

isAdult;
//=> false
```

### Nested Conditionals

If we have multiple overlapping conditions, we can employ nested conditional statements. For example, instead of just deciding whether the passed-in `age` meets the criteria for `isAdult`, let's add in some other examples of American adulthood: `canWork`, `canEnlist`, and `canDrink`. Let's use these conditions in a nesting example:

```js
const age = 17;

let isAdult, canWork, canEnlist, canDrink;

if (age >= 16) {
  canWork = true;

  if (age >= 18) {
    isAdult = true;
    canEnlist = true;

    if (age >= 21) {
      canDrink = true;
    }
  }
}

isAdult;
//=> undefined

canDrink;
//=> undefined

canEnlist;
//=> undefined

canWork;
//=> true
```

### `else if` Clause

Another way to represent multiple possible conditions is with `else if` clauses:

```js
const age = 20;

let isAdult, canWork, canEnlist, canDrink;

if (age >= 21) {
  isAdult = true;
  canDrink = true;
  canEnlist = true;
  canWork = true;
} else if (age >= 18) {
  isAdult = true;
  canEnlist = true;
  canWork = true;
} else if (age >= 16) {
  canWork = true;
}

isAdult;
//=> true

canDrink;
//=> undefined

canEnlist;
//=> true

canWork;
//=> true
```

As soon as one of the conditions returns a **truthy** value, the attached code block runs and the conditional exits. If none of the conditions evaluate to a **truthy** value, then the `else` code block runs (or, in the absence of an `else` clause, the conditional simply exits). Note that unlike the nested `if` statements above, **at most one code block will run**. In the absence of an `else` statement, it's possible that none of the `if` conditions return a **truthy** value and **no block is run**. However, it's impossible for more than one block in a linked `if...else if...else` control flow to run.

### `switch` Statement

Running multiple blocks in the same control flow is one of the many talents of the `switch` statement. The general structure is as follows:

```js
switch (expression) {
  case value1:
    // Statements
    break;
  case value2:
    // Statements
    break;
  default:
    // Statements
    break;
}
```

The JavaScript engine evaluates the expression and then compares the returned value against each of the `case` values _using strict equality_ (`===`):

```js
const hunger = 'famished';

let food;

switch (hunger) {
  case 'light':
    food = 'grapes';
    break;
  case 'moderate':
    food = 'sushi';
    break;
  case 'famished':
    food = 'lasagna';
    break;
}

food;
//=> "lasagna"
```

Generally, we use a `switch` statement if we need a conditional that hinges on a single value but requires a separate handler for each potential case. For example, the `switch` statement here doesn't require us to repeat the `if (order === ______) line for each possibility:

```js
const order = 'cheeseburger';

let ingredients;

switch (order) {
  case 'cheeseburger':
    ingredients = 'bun, burger, cheese, lettuce, tomato, onion';
    break;
  case 'hamburger':
    ingredients = 'bun, burger, lettuce, tomato, onion';
    break;
  case 'malted':
    ingredients = 'milk, ice cream, malted milk powder';
    break;
  default:
    console.log("Sorry, that's not on the menu right now.");
    break;
}
```

If we'd like to write out the same code with an `if` conditional, it will look like this:

```js
const order = 'cheeseburger';

let ingredients;

if (order === 'cheeseburger') {
  ingredients = 'bun, burger, cheese, lettuce, tomato, onion';
} else if (order === 'hamburger') {
  ingredients = 'bun, burger, lettuce, tomato, onion';
} else if (order === 'malted') {
  ingredients = 'milk, ice cream, malted milk powder';
} else {
  console.log("Sorry, that's not on the menu right now.");
}
```

We can also assign the same set of statements to multiple cases. In the following example, if the `age` variable contains any number between `13` and `19`, the `isTeenager` variable will be set to `true`. If it contains anything other than a number between `13` and `19`, none of our cases will hit and it will end up at the `default`, which sets `isTeenager` to `false`:

```js
const age = 15;

let isTeenager;

switch (age) {
  case 13:
  case 14:
  case 15:
  case 16:
  case 17:
  case 18:
  case 19:
    isTeenager = true;
    break;
  default:
    isTeenager = false;
}
```

The `default` and `break` keywords are both optional in basic `switch` statements, but useful. In more complicated statements, they become necessary to ensure the correct flow.

### `break` Statement

In the previous example, `break` is used to stop the `switch` statement from continuing to look at case statements. If instead, we wrote the following:

```js
const age = 15;

let isTeenager;

switch (age) {
  case 13:
  case 14:
  case 15:
  case 16:
  case 17:
  case 18:
  case 19:
    isTeenager = true;
    console.log('case 19: ', isTeenager);
  default:
    isTeenager = false;
    console.log('default: ', isTeenager);
}
```

...the switch statement would get to a match at `case 15` and continue on through to `case 19`, setting `isTeenager` to `true`. It would then get to `default` and set `isTeenager` to `false`. You will often see switch statements where `break` is used in every case as a way to ensure there is no unexpected behavior from multiple cases executing.

However, sometimes we do want to potentially match multiple cases, and we will need to leave out `break` in order to do this. That's a neat little trick we can employ that allows us to use comparisons for `case` statements. Let's rewrite the above `if...else` chain as a more compact, less repetitious `switch` statement:

```js
const age = 20;

let isAdult, canWork, canEnlist, canDrink;

switch (true) {
  case age >= 21:
    canDrink = true;
  case age >= 18:
    isAdult = true;
    canEnlist = true;
  case age >= 16:
    canWork = true;
}

isAdult;
//=> true

canDrink;
//=> undefined

canEnlist;
//=> true

canWork;
//=> true
```

We specified `true` as the value to switch on. All of our cases are comparisons, and if the comparison returns `true`, its statements will be run. Because we did not include any `break` statements, once _one_ case statement matches, all subsequent statements will execute.

### `default`

The `default` keyword specifies a set of statements to run after all of the `switch` statement's cases have been checked. The only time the `default` statement do _not_ run is if the engine hits a `break` in one of the case statements:

```js
const mood = 'quizzical';

let response;

switch (mood) {
  case 'happy':
    response = 'Heck yea; be happy!';
  case 'sad':
    response = "You're awesome; keep your head up!";
  default:
    response = "Sorry, I don't know how to respond to that mood.";
}

response;
//=> "Sorry, I don't know how to response to that mood."
```

It's typically safer to include `break` statements because it helps avoid bugs like this:

```js
const mood = 'happy';

let response;

switch (mood) {
  case 'happy':
    response = 'Heck yea; be happy!';
  case 'sad':
    response = "You're awesome; keep your head up!";
  default:
    response = "Sorry, I don't know how to respond to that mood.";
}

response;
//=> "Sorry, I don't know how to respond to that mood."
```

The `'happy'` case matches and assigns the string `'Heck yea; be happy!'` to `response`. However, since we didn't `break` after that assignment, the `default` case _also_ runs and reassigns `"Sorry, I don't know how to respond to that mood."` to `response`. Whoops!

#### Ternary Operator

The ternary operator, the final piece of the conditional puzzle, is a good way to represent an `if...else` statement in a single line of code:

```js
condition ? expression1 : expression2;
```

If the condition returns a **truthy** value, run the code in `expression1`. If the condition returns a **falsy** value, run the code in `expression2`.

```js
const age = 45;

let isAdult;

age >= 18 ? (isAdult = true) : (isAdult = false);

isAdult;
//=> true
```

We can simplify the above example a bit and assign the result of the ternary directly to a variable:

```js
const age = 60;

const isAdult = age >= 18 ? true : false;

isAdult;
//=> true
```

If it helps to visualize what's going on, you can wrap the condition, the expressions, or the entire ternary in parentheses:

```js
const age = 17;

const isAdult = (age >= 18) ? true : false;

const canWork = age >= 16 ? ( 1 === 1 ) : ( 1 !== 1 );

const canEnlist = (isAdult ? true : false);

isAdult;
//=> false

canWork;
//=> true

canEnlist;
//=> false
```

## Resources

- [Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions)
- [Block Statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block)
- [Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) and [Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
- [Conditional Statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Conditional_statements)
- [`if...else` Statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
- [Conditional (Ternary) Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
- [`switch` Statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
