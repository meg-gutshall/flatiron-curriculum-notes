---
description: 'Version 8: Module 14: Section 7: Lesson'
---

# Logical Operators (JS Fundamentals)

Logical operators in JavaScript are the powerful backbone on which most website logic is based. Using JavaScript's three logical operators, NOT (`!`), AND (`&&`), and OR (`||`), we'll learn how to negate and combine expressions.

## How to Use `!` to Negate an Expression

### NOT (`!`)

The logical NOT operator (`!`), also called the _bang operator_, operates on an expression, returning the opposite of the expression's truthiness. If `x` resolves to a truthy value, `!x` returns `false`. If `x` is falsy, `!x` returns `true`:

```javascript
const truthyValue = 'This value is truthy.';

!truthyValue;
//=> false

const falsyValue = 0;

!falsyValue;
//=> true
```

## Convert an Expression to a Boolean Using `!!`

### Double Bang (`!!`)

In the lesson on conditional statements, we passed values into the `Boolean()` _constructor function_ to check their truthiness. For now, think of this constructor function as a function that takes in some input, creates a new boolean for that input, and outputs the created boolean.

A shorter way to convert any value into a boolean is to use two NOT operators:

```javascript
const truthyValue = 'This value is truthy.';

!truthyValue;
// => false

!!truthyValue;
// => true
```

Reading from left-to-right, the JavaScript engine sees the first `!` and looks to the right to check what we're asking it to invert (`!truthyValue`). It then sees the second `!` and look to the right _again_, this time finding our `truthyValue` variable. The engine resolves `truthyValue` to `"This value is truthy."` and then executes the second `!` operator on it. `!truthyValue` returns `false`, so instead of `!!truthyValue` we're now looking at `!false`. The remaining `!` operator then executes on `false`, inverting the falsy value and evaluating to `true`.

## The AND (`&&`) and OR (`||`) Operators

### AND (`&&`)

The logical AND (`&&`) operator takes two expressions:

```javascript
expression1 && expression2;
```

The return value of the `&&` operator is always **one of the two expressions**. If the first expression is falsy, `&&` returns the value of the first expression. If the first expression is truthy, `&&` returns the value of the second expression. That means, if the first expression is falsy, `&&` returns that value and exits _without ever checking the second expression_:

```javascript
false && 'Anything';
//=> false

4 * 0 && 'Anything';
//=> 0
```

If the first expression is truthy, `&&` then returns whatever the second expression evaluates to:

```javascript
true && false;
//=> false

1 + 1 && 'Whatever';
//=> "Whatever"

'The truthiest of truthy strings' && 9 * 9;
//=> 81
```

There are three different ways the `&&` operator can be evaluated:

| Left side | Right side     | Return value | Truthiness of return value |
| --------- | -------------- | ------------ | -------------------------- |
| Falsy     | Doesn't matter | Left side    | Falsy                      |
| Truthy    | Falsy          | Right side   | Falsy                      |
| Truthy    | Truthy         | Right side   | Truthy                     |

1. If the left-side expression is falsy, the right-side expression doesn't matter at all. The `&&` operator returns the left side's falsy value and finishes.
2. If the left-side expression is truthy, the `&&` operator returns the right side's value (whether it's truthy or falsy) and finishes.

### OR (`||`)

The logical OR (`||`) operator also takes two expressions:

```javascript
expression1 || expression2
```

The return value of the `||` operator is always **one of the two expressions**. If the first expression is truthy, `||` returns the value of the first expression. If the first expression is falsy, `||` returns the value of the second expression.

If the first expression is truthy, that value is immediately returned and the second expression is never evaluated:

```javascript
true || 'Whatever';
//=> true

1 + 1 || 'Whatever';
//=> 2
```

If the first expression is falsy, `||` returns whatever the second expression evaluates to:

```javascript
false || 'Whatever';
//=> "Whatever"

1 === 2 || 8 * 8;
//=> 64

'' || 'Not ' + 'an ' + 'empty ' + 'string';
//=> "Not an empty string"
```

There are three different ways the `||` operator can be evaluated:

| Left side | Right side     | Return value | Truthiness of return value |
| --------- | -------------- | ------------ | -------------------------- |
| Truthy    | Doesn't matter | Left side    | Truthy                     |
| Falsy     | Truthy         | Right side   | Truthy                     |
| Falsy     | Falsy          | Right side   | Falsy                      |

1. If the left-side expression is truthy, the right-side expression doesn't matter at all. The `||` operator returns the life side's truthy value and completes.
2. If the left-side expression is falsy, the `||` operator returns the right side's value (regardless of whether it's truthy or falsy) and completes.

## How to Link Conditions Using the `&&` and `||` Operators

The `&&` and `||` operators are often used to link multiple conditions in a conditional statement:

```javascript
let user = 'Charles Babbage';
let friendCount = 3;
let message, messageColor;

if (user && friendCount) {
  message = `Hi ${user}! You have ${friendCount} ${friendCount === 1 ? 'friend' : 'friends'}!`;
} else if (user) {
  message = 'Link up with your friends to get the most out of Flatbook!';
} else {
  message = 'Please sign in.';
}
//=> "Hi Charles Babbage! You have 3 friends!"

if (message = 'Please sign in.' || message = 'Link up with your friends to get the most out of Flatbook!') {
  messageColor = 'red';
} else if (friendCount >= 1 && friendCount <= 10) {
  messageColor = 'blue';
} else if (friendCount >= 11 && friendCount <= 50) {
  messageColor = 'purple';
} else {
  messageColor = 'rainbow';
}
//=> "blue"
```

## Conclusion

Logical operators are used to determine the logic between variables or values. Although they are called "logical," they can be applied to values of any type—not just boolean. The result can also be of any type. If a value can be converted to `true`, to value is so-called truthy; and if a value can be converted to `false`, the value is so-called falsy.

## Resources

* [Logical Operators (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical\_Operators)
* [Review of Conditionals, Comparisons, and Logical Operators (MDN)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building\_blocks/conditionals)
