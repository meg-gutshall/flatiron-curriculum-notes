---
description: 'Version 8: Module 14: Section 2: Lesson'
---

# Arrays (JS Fundamentals)

A _data structure_ is a means for associating and organizing information. Outside of the programming world, we use data structures all the time! Some examples are shopping lists and address books. If we have a lot of related data, it's best to represent it in a related system.

## Collections and Arrays

We know that `getElementById()` returns a **singular** element, whereas `getElementsByClassName()` and `getElementsByTagName()` return **all elements** that match the tag or class name.

```javascript
document.getElementsByClassName() => [...multiple elements...]
document.getElementsByTagName() => [...multiple elements...]
document.getElementById() => single element
```

The first two methods' name hint, with the part **Elements** plural, that they can return multiple matches—a _collection_. This is a collection that we're going to call an `Array`.

_**NOTE:**_ These methods don't actually return an `Array`. An `HTMLCollection` is _actually_ what is returned from the first two methods. This is a major point of confusion in JavaScript! The `HTMLCollection` knows its length like an `Array` and we can iterate across it with a `for... in...` loop, but it's not _technically_ an `Array`. More on this later.

We can ask a DOM to give us a collection by asking it to do:

```javascript
document.getElementsByTagName("p")
```

We can get a single member of a collection by providing an element number or, _index_ `[]`, after the collection. This is done as follows:

```javascript
document.getElementsByTagName("main")[0]
```

## How to Create an Array

An `Array` is a list, with the items listed in a particular order, surrounded by square brackets (`[]`):

```javascript
["This", "is", "an", "array", "of", "strings."];
//=> ["This", "is", "an", "array", "of", "strings."]
```

The _members_ or _elements_ in an array can be data of any type in JavaScript:

```javascript
["Hello, world!", 42, null, NaN];
//=> ["Hello, world!", 42, null, NaN]
```

> In some other languages arrays _cannot be of multiple types_. In C, C++, Java, and Swift are just a few languages in which you cannot mix types. JavaScript, Python, Ruby, and Lisp are some that permit this behavior.

Arrays are _ordered_, meaning that the elements in them will always appear in the same order. For example, the array `[1, 2, 3]` is different from the array `[3, 2, 1]`.

Just like any other type of JavaScript data, we can assign an `Array` to a variable:

```javascript
const primeNumbers = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37];
const tvShows = ["Game of Thrones", "True Detective", "The Good Wife", "Empire"];
```

We can find out how many elements an array contains by checking the array's built-in `length` property:

```javascript
const myArray = ["This", "array", "has", 5, "elements];
myArray.length;
//=> 5
```

We defined the arrays above using the _array literal_ syntax—that is, we literally typed out the array that we wanted to create, square brackets and all. There are other ways to create new arrays, but they are only necessary for very rare circumstances. For now, we'll just use array literals.

Arrays provide organization, and we only have to remember _one_ identifier (the variable) instead of multiple (each element in the array). We call arrays _expressive_ because putting elements in a shared data structure communicates to other programmers "Hey, these things go together!" in a way that naming them individually _does not_. Arrays offer a simple syntax for accessing the individual members stored within.

## How to Access the Elements in an Array

Every element in an array is assigned a unique index value that corresponds to its place within the collection. The first element in the array is at index `0` and it increments from there. To access an element, we use the _computed member access operator_, aka "square brackets."

```javascript
const winningNumbers = [32, 9, 14, 33, 48, 5];

winningNumbers[0];
//=> 32

winningNumbers[3];
//=> 33
```

_**NOTE:**_ Most people just call it _bracket notation_ or the _bracket operator_, so don't worry too much about remembering the term _computed member access operator_.

How would we access the **last** element in our array?

```javascript
const alphabet = ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"];

alphabet.length
//=> 26

alphabet[alphabet.length - 1];
//=> "z"
```

This is why it's called the _**computed** member access operator_. We put an expression (`alphabet.length - 1`) inside the square brackets, and the JavaScript engine _computed_ the value of that expression to determine which element we were trying to access.

## Adding Elements to an Array

JavaScript allows us to manipulate the members in an array in a number of ways.

### `.push()` and `.unshift()`

With the `.push()` method, we can add elements to the end of an array.

```javascript
const superheroes = ["Catwoman", "Miss Marvel", "She-Hulk", "Jessica Jones"];

superheroes.push("Wonder Woman");
//=> 5

superheroes;
//=> ["Catwoman", "Miss Marvel", "She-Hulk", "Jessica Jones", "Wonder Woman"]
```

We can also `.unshift()` elements onto the beginning of an array.

```javascript
const cities = ["New York", "San Francisco"];

cities.push("Los Angeles");
//=> 3

cities;
//=> ["New York", "San Francisco", "Los Angeles"]
```

Notice the value returned by both methods is the `length` of the updated array.

### Destructive vs. Nondestructive

Both `.push()` and `.unshift()` update or _mutate_ the original array, adding elements directly to it. Operations that modify the original collection are _destructive_ and those that leave the original collection intact are _nondestructive_. Mutating the original array isn't necessarily a bad thing, but there's also a way to add elements nondestructively, leaving the original array intact.

### Spread Operator

ES2015 introduced the _spread operator_, which looks like an ellipsis (`...`). The spread operator allows us to spread out the contents of an existing array into a new array, adding new elements while at the same time preserving the original.

```javascript
const coolCities = ["New York", "San Francisco"];
const allCities = ["Los Angeles", ...coolCities];

coolCities;
//=> ["New York", "San Francisco"]

allCities;
//=> ["Los Angeles", "New York", "San Francisco"]
```

We created a new array instead of modifying the original one—our `coolCities` array was untouched. We can also use the spread operator to add a new item to the end of an array without modifying the original.

```javascript
const coolCats = ["Hobbes", "Felix", "Tom"];
const allCats = [...coolCats, "Garfield"];

coolCats;
//=> ["Hobbes", "Felix", "Tom"]

allCats;
//=> ["Hobbes", "Felix", "Tom", "Garfield"]
```

## Removing Elements from an Array

As compliments for `.push()` and `.unshift()`, respectively, we have `.pop()` and `.shift()`.

### `.pop()` and `.shift()`

The `.pop()` method removes the last element in an array, destructively updating the original array.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.pop();
//=> "Sun"

days;
//=> ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
```

The `.shift()` method removes the first element in an array, also mutating the original.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.shift();
//=> "Mon"

days;
//=> ["Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
```

Notice that the return value for the `.pop()` and `.shift()` methods is the element that was removed.

### `.slice()`

To remove elements from an array nondestructively, we can use the `.slice()` method. Just as the name implies, the `.slice()` method returns a portion, or slice, of an array.

#### Without Arguments

If we don't provide any arguments, `.slice()` will return a copy of the original array with all elements intact.

```javascript
const primes = [2, 3, 5, 7];
const copyOfPrimes = primes.slice();

primes;
//=> [2, 3, 5, 7]

copyOfPrimes;
//=> [2, 3, 5, 7]
```

Note that the array returned by `.slice()` has the same elements as the original, but it's a copy—**the two arrays point to different objects in memory.** If you add an element to one of the arrays, it does not get added to the other.

#### With Arguments

We can provide two arguments to `.slice()`: the index where the slice should begin and the index **before which** it should end.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.slice(2, 5);
//=> ["Wed", "Thu", "Fri"]
```

If no second argument is provided, the slice will run from the index specified bt the first argument to the end of the array.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.slice(5);
//=> ["Sat", "Sun"]
```

To remove the first element and return a new array, we call `.slice(1)`.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.slice(1);
//=> ["Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
```

And we can remove the last element in a way that will look familiar from earlier in this lesson.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.slice(0, days.length - 1);
//=> ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
```

In fact, `.slice()` provides an easier syntax for grabbing the last element in an array.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.slice(-1);
//=> ["Sun"]

days.slice(-3);
//=> ["Fri", "Sat", "Sun"]
```

When we provide a negative index, the JavaScript engine know to start counting from the last element in the array instead of the first. **`.slice` is used everywhere in JavaScript code so familiarize yourself with this method and its parameters!**

### `.splice()`

While `.slice()` allows us to return a piece of an array without mutating the original (nondestructive), `.splice()` performs destructive actions. There are three different ways to use `.splice()`.

#### With a Single Argument

```javascript
array.splice(start)
```

The first argument expected by `.splice()` is the index at which to begin the splice. If we only provide one argument, `.splice()` will destructively remove a chunk of the original array beginning at the provided index and continuing to the end of the array.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.splice(2);
//=> ["Wed", "Thu", "Fri", "Sat", "Sun"]

days;
//=> ["Mon", "Tue"]
```

Notice that `.splice()` returns the removed chunk and leaves the remaining elements in the original array. With a negative start index, the opposite happens.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

days.splice(-2);
//=> ["Sat", "Sun"]

days;
//=> ["Mon", "Tue", "Wed", "Thu", "Fri"]
```

#### With Two Arguments

```javascript
array.splice(start, deleteCount)
```

When we provide two arguments to `.splice()`, the first is still the index at which to begin splicing, and the second dictates how many elements we want to remove from the array.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

// Remove `3` elements, starting with the element at index `2`

days.splice(2, 3);
//=> ["Wed", "Thu", "Fri"]

days;
//=> ["Mon", "Tue", "Sat", "Sun"]
```

## Replacing Elements in an Array

### `.splice()` with 3+ Arguments

```javascript
array.splice(start, deleteCount, item1, item2, ...)
```

After the first two, every additional argument passed to `.splice()` will be inserted into the array at the position indicated by the first argument. We can replace a single element in an array as follows, discarding a card and drawing a new one:

```javascript
const cards = ["Ace of Spades", "Jack of Clubs", "Nine of Clubs", "Nine of Diamonds", "Three of Hearts"];

cards.splice(2, 1, "Ace of Clubs");
//=> ["Nine of Clubs"]

cards;
//=> ["Ace of Spades", "Jack of Clubs", "Ace of Clubs", "Nine of Diamonds", "Three of Hearts"]
```

Or we can remove two elements and insert three new ones as our restaurant expands its vegetarian options:

```javascript
const menu = ["Jalapeño Poppers", "Cheeseburger", "Fish and Chips", "French Fries", "Onion Rings"];

menu.splice(1, 2, "Veggie Burger", "House Salad", "Teriyaki Tofu");
//=> ["Cheeseburger", "Fish and Chips"]

menu;
//=> ["Jalapeño Poppers", "Veggie Burger", "House Salad", "Teriyaki Tofu", "French Fries", "Onion Rings"]
```

We aren't required to remove anything with `.splice()`—we can use it to insert elements anywhere within an array. Here we're adding new books to our library in alphabetical order:

```javascript
const books = ["Bleak House", "David Copperfield", "Our Mutual Friend"];

books.splice(2, 0, "Great Expectations", "Oliver Twist");
//=> []

books;
//=> ["Bleak House", "David Copperfield", "Great Expectations", "Oliver Twist", "Our Mutual Friend"]
```

Notice that `.splice()` returns an empty array when we provide a second argument of `0`. This makes sense because the return value is the set of elements that were removed, and we're telling it to remove `0` elements.

### Using the Computer Member Access Operator to Replace Elements

If we only need to replace a single elements in an array, there's a simpler solution than `.splice()`.

```javascript
const cards = ["Ace of Spades", "Jack of Clubs", "Nine of Clubs", "Nine of Diamonds", "Three of Hearts"];

cards[2] = "Ace of Clubs";
//=> "Ace of Clubs"

cards;
//=> ["Ace of Spades", "Jack of Clubs", "Ace of Clubs", "Nine of Diamonds", "Three of Hearts"]
```

However, using that computed member access operator (`[]`) is still _destructive_—it modifies the original array. There's a _nondestructive_ way to replace or add items at arbitrary points withing an array, and it involves two of the concepts we learned earlier.

### Slicing and Spreading

Combining `.slice()` and the spread operator allows us to replace elements _nondestructively_, leaving the original array unharmed.

```javascript
const menu = ["Jalapeño Poppers", "Cheeseburger", "Fish and Chips", "French Fries", "Onion Rings"];

const newMenu = [...menu.slice(0, 1), "Veggie Burger", "House Salad", "Teriyaki Tofu", ...menu.slice(3)];

menu;
//=> ["Jalapeño Poppers", "Cheeseburger", "Fish and Chips", "French Fries", "Onion Rings"]

newMenu;
//=> ["Jalapeño Poppers", "Veggie Burger", "House Salad", "Teriyaki Tofu", "French Fries", "Onion Rings"]
```

## Identify Nested Arrays

An array can contain elements of **any** data type, including **other arrays**. In general, try to keep your arrays to no more than two levels deep. Two levels is perfect for representing two-dimensional things like a tic-tac-toe board:

```javascript
const board = [
  ["X", "O", " "],
  [" ", "X", "O"],
  ["X", " ", "O"]
];

board;
//=> [["X", "O", " "], [" ", "X", "O"], ["X", " ", "O"]]
```

The cool thing about representing a game board like this is in how we can access the different squares by specifying coordinates. The first `[]` operator grabs the row that we want: top (`board[0]`), middle (`board[1]`), or bottom (`board[2]`). The second `[]` operator specifies the square within that row: left (`board[1][0]`), middle (`board[1][1]`), or right (`board[1][2]`). Effectively, we're using X and Y coordinates to refer to data within a two-dimensional structure.

## Conclusion

We dove into data structures and the `Array`, including how to create an `Array`, access elements in an `Array`, add elements to an `Array`, remove elements from an `Array`, and replace elements in an `Array`. We also covered the difference between destructive and non-destructive `Array` manipulation.

## Resources

* [Array (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array)
* [`.slice()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/slice)
* [`.splice()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/splice)
