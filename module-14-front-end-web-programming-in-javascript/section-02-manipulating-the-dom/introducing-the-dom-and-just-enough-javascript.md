# Lesson: Introducing the DOM and Just Enough JavaScript

JavaScript can do many kinds of work—from building web servers, to creating infinite scroll effects—but it was originally designed to do a type of programming called **Document-Object Model (DOM) programming**. Understanding DOM programming is the foundation of front-end development.

DOM programming is using JavaScript to:

- Ask the DOM to find or `select` an HTML element or elements in the rendered page
- Remove and/or insert an element or elements
- Adjust a property of the selected element or elements

## JavaScript and the DOM: A Learning Catch-22

JavaScript changes are made through a middle layer called the DOM, or the Document Object Model, and the DOM only understands JavaScript. Unfortunately, this gives us a chicken-and-egg situation. Because the two are inseparable, learning about the DOM will require us to write some JavaScript and learning JavaScript won't tell us anything about the DOM. To get around this problem, we start by learning some basic structures of JavaScript called "sight words", which are JavaScript reserved words you can identify at a glance. We're going to learn "just enough JavaScript" so that we can start working with the DOM—the best way to understand it.

## The Concept of "Just Enough JavaScript"

We call the approach of learning JavaScript sight words "just enough JavaScript." We learn so much better working with technology than by merely reading words.

## Using the Console and Chrome DevTools

As you learn JavaScript, you should almost always have a browser console open, either on the lessons page or in a separate window. Code along with every example. Get used to the syntax and familiarize yourself with the errors that arise when you mistype something. Clear the console or simply refresh the page whenever you need a clean slate. Every major browser comes with a built-in set of developer tools that you can use to inspect, modify, and debug the content of a web page.

To open the [dev tools in Chrome](https://developers.google.com/web/tools/chrome-devtools/console/#open_as_panel), press `Ctrl+Shift+J` (Windows/Linux) or `Cmd+Opt+J` (Mac). Chrome ships with a whole suite of useful dev tools, but the only one we care about for now is the JavaScript console.

The console is an environment in the browser where we can type and run arbitrary JavaScript code in the context of the current browser window. The console is _sandboxed_, meaning the only resources it has access to are those loaded on the current page. Once we start declaring variables and functions in separate JavaScript files, we'll be able to access and play around with them in the console. The console is the single best tool for debugging JavaScript in the browser, so start familiarizing yourself with it now.

## Coding in JavaScript

In JavaScript, an **[expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions)** is a valid unit of code that returns a value. The value an expression returns is aptly referred to as the **return value** of the expression.

When writing text, wrap it in quotation marks to signal to JavaScript that we're writing literal text.

## JavaScript Has Data Types

JavaScript has data types. One kind of data type is a `Number`, which can be whole or decimal. Another kind of data type is an arrangement of characters called a `String`, which can be a single word, a phrase, a few letters, a sentence, etc. A `String` is surrounded by either single (`'`) or double(`"`) quotes as to avoid JavaScript confusing regular text for a _reserved word_. A reserved word is a word that has meaning in JavaScript. For example, `if` is used regularly in both the English language and JavaScript code, so to distinguish the reserved word from plain text, JavaScript uses quotation marks.

## JavaScript Has Variables

Sometimes you want to hold a `String` or a `Number` under another name. You can easily do this by going to your console and typing either `var`, `let`, or `const` followed by the name of your new variable, the equal sign (`=`), and the value you want to assign your new variable, closing it off with a semi-colon (`;`).

**NOTE:** The `//=>` means "what JavaScript would return back."

```javascript
3.14; //=> 3.14
var pi = 3.14; //=> 'undefined'
pi; //=> 3.14

3.14; //=> 3.14
let pi = 3.14; //=> 'undefined'
pi; //=> 3.14

3.14; //=> 3.14
const pi = 3.14; //=> 'undefined'
pi; //=> 3.14
```

### Mathematic Operations Can Be Performed on Numbers

`Number` data types can be added, subtracted, multiplied, and divided. The results of these operations can be stored in variables.

```javascript
1 + 1; //=> 2
let result = 1 + 1; //=> 'undefined'
result; //=> 2
let pi = 3.14; //=> 'undefined'
let radius = 2; //=> 'undefined'
let circumference = pi * (radius * 2); //=> 'undefined'
circumference; //=> 12.56
10 / 4; //=> 2.5
```

JavaScript also has a symbol for finding the remainder when one `Number` is divided by another (`%`).

```javascript
10 % 4 //=> 2
13 % 5 //=> 3
```

### Strings Can Be Manipulated

Just as `Number` data types can be added together, it is possible to add `String` data types together as well.

```javascript
'Ya got trouble, folks, right here in ' + 'River City';
//=> 'Ya got trouble, folks, right here in River City'

let poolTable = 'Trouble';
poolTable + ' with a capital T';
//=> 'Trouble with a capital T'
```

Dynamically combining `String` data types and variables is very common in JavaScript, so much so that multiple methods exist for this purpose. One is called `concat`:

```javascript
'And that rhymes with '.concat('P');
//=> 'And that rhymes with P'

let lyric = 'And that stands for ';
let trouble = 'pool!';
lyric.concat(trouble);
//=> 'And that stands for pool!'
```

You can also use [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals). To use Template Literals in your `String` data types, you _must_ wrap the entire `String` in _backticks_, not quotation marks. Instead of using `+` to combine, a variable is wrapped in brackets preceded by a dollar sign, `${}`, then included _within_ the backticks. Inside these brackets, you can include variables or any other data types that can be converted into a `String`.

```javascript
let pool = 'trouble';
//=> 'undefined'

`Ya got ${pool}, ${pool}, ${pool}, ${pool}, ${pool}...`;
//=> 'Ya got trouble, trouble, trouble, trouble, trouble...'

`Adding two and two equals ${2 + 2}`;
//=> 'Adding two and two equals 4'
```

## JavaScript Can Compare Data Types

```javascript
1 < 3; //=> true
3 == 3; //=> true
3 != 4; //=> true
5 > 2; //=> true
```

Be careful here! `=` means "assign to," like we just did with `var` above. For comparison we use `==` and `===`. We can build on our previous example:

```javascript
3.14; //=> 3.14
const pi = 3.14; //=> 'undefined'
pi; //=> 3.14
pi == 3.14; //=> true
```

## JavaScript Has Conditionals

With the ability to compare data types, we can build logic into our code using `if` statements:

```javascript
let test = 1;
test; //=> 1

if (test < 2) {
  // Test is less than 2.
  // This statement is true so the code within the brackets is executed.
  test = test + 1;
}

test; //=> 2

if (test < 2) {
  // Test NOT is less than 2.
  // This statement is false so the code within the brackets is ignored.
  test = test + 1;
}

test; //=> 2
```

The code inside an `if` statement's brackets will only be executed if the statement is `true`. We can expand our `if` statement to do one thing or another using `else`:

```javascript
let test = 1;
test; //=> 1

if (test < 2) { // Test is less than 2.
  test = test + 1; // This code is executed.
} else {
  test = 0; // This code is ignored.
}

test; //=> 2

if (test < 2) { // Test NOT is less than 2.
  test = test + 1; // This code is ignored.
} else {
  test = 0; // This code is executed.
}

test; //=> 0
```

## JavaScript Has Collections

Sometimes a `variable` may point to a data type which has many data types inside of it. In programming vocabulary, these collection-data types are called `Array`s. So technically, `Array` belongs with `String` and `Number`.

## JavaScript Is Object-Oriented

When working with the DOM is JavaScript, many of the data types you encounter are objects. `Objects` are bits of code you can talk to that know state and behavior. `Objects` should round out our universe of JavaScript data types, along with `Array`s, `String`s, and `Number`s.

When talking to an `Object`, you can ask it for a bit of state by using a `.` and then that state's name. You can trigger behavior by using a `.` and then the behavior's name, followed by `()`. Due to the `.` being the separator between the object-name and the state or behavior name, we call writing cade this way "dot-notation." The thing that holds a bit of state is known as a property.

### An Object-Oriented JavaScript Example

To ask a poodle its `name` state, you would do it like so:

```javascript
poodle.name; //=> "Byron"
```

If you ask an object for a property if doesn't have, JavaScript says `undefined`.

```javascript
poodle.favoritePainter; //=> undefined
```

When asking an object to do something (a behavior), you use a `.` and a behavior-name (usually a verb) followed by `()`. Behaviors on objects are called methods.

```javascript
poodle.bark(); //=> An ear-splitting bark is heard
```

An `Object`'s methods have access to all of that `Object`'s properties.

```javascript
poodle.introduceYourselfFormally();
//=> "Hello, my name is Byron the poodle"
```

In this case, the method `introduceYourselfFormally` presumably looks at `poodle`'s `name` property and adds some text around it. We might imagine that it's making `"Hello, my name is " + this.name + " the poodle"`. As it turns out, the is entirely valid JavaScript and it is probably what's happening!

Finally, methods can take arguments. Arguments change the method's operation.

```javascript
poodle.eat(1); //=> "Byron eats 1 can of food"
poodle.eat(2); //=> "Byron eats 2 cans of food"
```

`Methods` can take multiple arguments.

```javascript
poodle.eyeEnviously('Shack Burger', '$', 9.57);
//=> "Byron eyes your Shack Burger enviously, hoping you will drop some, not caring the least that it cost you $9.57."
```

**A very important object when working with the DOM is called `document`.**

## JavaScript Has Loops

Sometimes you don't want to manually type something out multiple times, but you want to perform some action "for each" element in a collection. That's where looping comes in.

### An Example of the "For" Loop in JavaScript

"For each" character in the `slytherin` collection (or `Array`), we would like the `harry_potter` object to invoke its `expelliarmus` method on the wizard or witch who is passed in as an argument:

```javascript
for (let i = 0; i < slytherins.count; i += 1) {
  harry_potter.expelliarmus(slytherins[i])
}
```

The important thing to take away is the ability to "sight read" that `for` invokes the idea of doing some repeating action for each element in a collection.

## JavaScript Logs with `console.log`

The JavaScript method `console.log()` is used to print something. Often it's used to print out a `variable` or some bit of data to make a point or to debug something.

### An Example of `console.log`

Building on the loop example, let's say we want to know who `harry_potter` is defending against:

```javascript
for (let i = 0; i < slytherins.count; i += 1 ) {
  console.log(`Harry is about to disarm ${slytherins[i]}`);
  harry_potter.expelliarmus(slytherins[i]);
  console.log(`${slytherins[i]} is defenseless!`);
}
```
