# JavaScript Fundamentals: Data Types

In JavaScript, _concrete_ instances of data can be categorized into _abstract_ names called "data type" or, more simply, "type."

## What Is a Data Type?

**_Everything in JavaScript is data_** except:

1. **Operators**: `+`, `!`, `<=`, etc.
2. **Reserved words**: `function`, `for`, `debugger`, etc.

Every piece of data falls into one of JavaScript's seven data types: numbers, strings, booleans, symbols, objects, `null`, and `undefined`.

## Basic Type Checking Using the `typeof` Operator

The `typeof` operator gives us an idea of what data types we're dealing with. `typeof` accepts one argument, the piece of data that we'd like to know the _type of_.

> `typeof` is an operator, just like `+` or `!`. We get used to operators being only one character, but JavaScript (and many other languages) have operators with **_more than one_** character. As such, **we don't need parentheses with `typeof`**. That said, JavaScript also supports `()` after `typeof`, but it's commonly not done.

## JavaScript's Seven Basic Types

### Numbers

Some programming languages divide numbers up into integers, decimals, doubles, floats, and so on. They do this so that they can have higher _precision_ in their calculations. In a banking application or airplane wing engineering application we want our interest rate or the curve of the wing to be **_as accurate as possible_**. For good reason: we want to make sure we get paid of have a safe plane! When JavaScript was created, this level of precision was not thought to be a thing that would be needed, so JavaScript only has a single, all-encompassing `number` type:

```js
typeof 42;
//=> "number"

typeof 3.141592653589793;
//=> "number"

typeof 5e-324;
//=> "number"

typeof -Infinity;
//=> "number"
```

### Strings

Strings are how we represent text in JavaScript. A string consists of a matching pair of `'single quotes'`, `"double quotes"`, or `` `backticks` `` with zero or more characters in between:

```js
typeof 'I am a string.';
//=> "string"

typeof "Me too!";
//=> "string"

typeof `Me three!`;
//=> "string"
```

Even empty strings are strings:

```js
typeof '';
//=> "string"
```

### Booleans

A boolean can only be one of two possible values: `true` or `false`. Booleans play a big role in `if` statements and looping in JavaScript.

```js
typeof true;
//=> "boolean"

typeof false;
//=> "boolean"
```

### Objects

JavaScript objects are a collection of properties bound by curly braces (`{ }`), similar to a hash in Ruby or a dictionary in Python.

The properties can point to values of any data type—even other objects:

```js
{
  "name": "JavaScript",
  "createdBy": {
    "firstName": "Brendan",
    "lastName": "Eich"
  },
  "firstReleased": 1995,
  "isAwesome": true
}

typeof {};
//=> "object"
```

From JavaScript's perspective, what we call "arrays" are just special cases of an object where the keys are all numbers. So while JavaScript has arrays like `let dogs = ["Byron", "Cubby", "Boo Radley", "Luca"]`, JavaScript really thinks that `typeof dogs` is `"object"`.

```js
let dogs = ["Byron", "Cubby", "Boo Radley", "Luca"];
typeof dogs;
//=> "object"
```

### `null`

The `null` data type represents an intentionally absent object. For example, is a piece of code returns an object when it successfully executes, we could have it return `null` in the event of an error. Confusingly, the `typeof` operator returns `"object"` when called with `null`:

```js
typeof null;
//=> "object"
```

### `undefined`

The bane of many JavaScript developers, `undefined` is a bit of a misnomer. Instead of "not defined," it actually means something more like "not yet assigned a value."

```js
typeof undefined;
//=> "undefined"

let unassignedVariable;
typeof unassignedVariable;
//=> "undefined"

unassignedVariable = '';
typeof unassignedVariable;
//=> "string"
```

Any variable declared but not defined will be `undefined` until a value is assigned.

### Symbols

Symbols are a relatively new data type (introduced in ES2015) that's primarily used as an alternative way to add properties to objects.

### Primitive Types

Six of seven JavaScript data types—everything except `Object`—are **primitive**. All this means is that they represent _single_ values, such as `7` or `"hello"` or `false`, instead of a collection of values.

## How Different JavaScript Data Types Interact

Every programming language has its own rules governing the ways in which we can operate on data of a given type. For example, it's rather uncontroversial that numbers can be subtracted from other numbers...

```js
3 - 2;
//=> 1
```

...and that strings can be added to other strings:

```js
'Hello' + ", " + `world!`;
//=> "Hello, world!"
```

But what happens if you mix them?

Some programming languages, such as Python, are strict about how data of different types can interact, and they will refuse to compile a program that blends types. Well, that's rather strict.

Other Languages, such as Ruby, will attempt to handle the interaction by converting one of the data types so all data is of the same type. For example, instead of throwing an error when an integer (`3`) is added to a floating-point number (`0.14159`), Ruby will simply convert the integer into a floating-point number and correctly calculate the sum:

```ruby
3 + 0.14159
#=> 3.14159
```

Ruby throws errors when some stranger cases come up:

```ruby
> "THX-" + 1138
TypeError: no implicit conversion of FixNum into String
```

This seems pretty reasonable: I don't know how to make the `Integer`, `1138`, a `String` without being directly told that you want it to be a `String` (same as Python's rule).

That seems like a good baseline. However, JavaScript is a little _too_ nice when handling conflicting data types. **No matter what weird combination of types you give it, JavaScript won't throw an error and will return _something_ (though that _something_ might make no sense at all).**

Sometimes this makes _some_ sense:

```js
'High ' + 5 + '!';
//=> "High 5!"
```

...to the [comical](https://www.destroyallsoftware.com/talks/wat):

```js
null ** 2; // null to the power of 2
//=> 0

undefined ** null; // undefined to the power of null
//=> 1

{}+{}; // empty object plus empty object
//=> "[object Object][object Object]" <-- That's a string!
```

Why JavaScript returns a string when we ask it to add two empty objects is anyone's guess, but its heart is in the right place. The language always tries to bend over backwards for its human masters, returning actionable data instead of throwing errors. However, JavaScript's eagerness occasionally results in data type issues that surprise both novice and expert programmers alike.

Try to follow along with what's happening here:

```js
1 + 2 + 3 + 4 + 5;
//=> 15

'1' + 2 + 3 + 4 + 5;
//=> "12345"

1 + '2' + 3 + 4 + 5;
//=> "12345"

1 + 2 + '3' + 4 + 5;
//=> "3345"

1 + 2 + 3 + '4' + 5;
//=> "645"

1 + 2 + 3 + 4 + '5';
//=> "105"
```

As long as we are only adding numbers to other numbers, JavaScript performs the expected addition. However, as soon as we throw a strong in the mix, we stop adding and start concatenating everthing together into a string.

You'll encounter a lot of these weird data type behaviors throughout your JavaScript programming, but fear not: they'll trip you up less and less often as you gain experience.

## Conclusion

Data types are representation of pieces of information and JavaScript defines seven different types: numbers, strings, booleans, symbols, objects, `null`, and `undefined`.

## Resources

- [JavaScript Data Types and Data Structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [Types](https://www.destroyallsoftware.com/compendium/types?share_key=baf6b67369843fa2): A cross-language examination of type in various languages
- [Wat](https://www.destroyallsoftware.com/talks/wat): A beloved **_and hilarious_** talk in which JavaScript's friendliness when mixing types is discussed at a feverish pace—with awesome slides
