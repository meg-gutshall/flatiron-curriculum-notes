# Lesson: Objects (JavaScript Fundamentals)

Arrays are great for representing simple, ordered data sets, but they're generally not so great at modeling a more complex structure. For that, we need the `Object` data type.

## JavaScript Objects

### What Is an Object?

We briefly touched on the syntax for an `Object` back in the data types lesson:

> A JavaScript `Object` is a collection of properties bounded by curly braces (`{}`), similar to the hash in Ruby. The properties can point to values of any data type—even another `Object`.

We can have empty Objects:

```js
{};
```

Or Objects can have a single _key-value_ pair:

```js
{ key: value };
```

When we have to represent multiple key-value pairs in the same Object (which is most of the time), we use commas to separate them out:

```js
{
  key1: value1,
  key2: value2
};
```

For a real example, let's see our address as an Object:

```js
const address = {
  street1: "11 Broadway",
  street2: "2nd Floor",
  city: "New York",
  state: "NY",
  zipCode: 10004
};
```

The real data in an `Object` is stored in the _value_ half of the key-value pairings. The _key_ is what lets us access that value. In the same way we use _identifiers_ to name variables and functions, inside an `Object` we assign each value a key. We can then refer to that key and the JavaScript engine knows exactly which value we're trying to access.

## Access a Value Stored in an Object

There are two ways to access values in an `Object`, one of which we already learned about in the `Array` lesson: dot notation and bracket notation.

### Dot Notation

With _dot notation_, we use the _member access operator_ (a single period) to access values in an `Object`. For example, we can grab the individual pieces of our address as follows:

```js
address.street1;
//=> "11 Broadway"

address.street2;
//=> "2nd Floor"

address.city;
//=> "New York"

address.state;
//=> "NY"

address.zipCode;
//=> 10004
```

Dot notation is fantastic for readability, as we can just reference the bare key name (e.g., `street1` or `zipCode`). Because of this simple syntax, it should be your go-to strategy for accessing the properties of an `Object`.

#### Accessing Nonexistent Properties

If we try to access the `country` property of our `address` Object, what will happen?

```js
address.country;
//=> undefined
```

It returns `undefined` because there is no matching key on the Object. JavaScript is too nice to throw and error, so it lets us down gently. Keep this in mind though: if you're seeing `undefined` when trying to access an Object's property, it's a good indicator that you should recheck which properties actually exist on that particular Object (along with your spelling and camelcasing)!

### Bracket Notation

With _bracket notation_ we use the _computed member access operator_, which is a pair of square brackets (`[]`). To access the same properties as above, we need to represent them as strings inside the operator:

```js
address["street1"];
//=> "11 Broadway"

address["street2"];
//=> "2nd Floor"

address["city"];
//=> "New York"

address["state"];
//=> "NY"

address["zipCode"];
//=> 10004
```

Bracket notation is a bit harder to read than dot notation, so we always default to the latter. However, there are two main situations in which to use bracket notation.

#### With Nonstandard Keys

If (for whatever reason) you need to use a nonstandard string as an Object's key, you'll only be able to access the properties with bracket notation. For example, the following is a valid Object:

```js
const wildKeys = {
  "Cash rules everything around me.": "Wu",
  "C.R.E.A.M.": "Tang",
  "Get the money.": "For",
  "$ $ bill, y'all!": "Ever"
};
```

It's impossible to access those properties with dot notation, but bracket notation works just fine.

In order to access a property via dot notation, **the key must follow the same naming rules applied to the variables and functions**. It's also important to note that under the hood, **all keys are strings**. Don't waste too much time worrying whether or not a key is accessible via dot notation. If you follow these rules when naming your keys, everything will work out:

- camelCaseEverything
- Start the key with a lowercase letter
- No spaces or punctuation

If you follow those three rules, you'll be able to access all of an Object's properties via bracket notation **or** dot notation.

#### Accessing Properties Dynamically

The other situation in which bracket notation is required is if we want to dynamically access properties. Remember, we can place any expression inside our _computed member access operator_ and JavaScript will _compute_ its value to figure out which property to access. For example, we can access the `zipCode` property from our `address` Object like so:

```js
address[ "zip" + "Code"];
//=> 10004
```

However, the real strength of bracket notation lies in its ability to compute the value of variables on the fly. For example:

```js
const meals = {
  breakfast: "Oatmeal",
  lunch: "Caesar salad",
  dinner: "Chimichangas"
};

let mealName = "lunch";

meals[mealName];
//=> "Caesar salad"
```

If we try to use the `mealName` variable with dot notation, it doesn't work:

```js
mealName = "dinner";
//=> "dinner"

meals.mealName;
//=> undefined
```

With dot notation, JavaScript doesn't treat `mealName` as a variable—it checks whether a property exists with a key of `mealName`, only finds properties named `breakfast`, `lunch`, and `dinner`, and so returns `undefined`. Essentially, dot notation is for when you know the exact name of the property in advance, and bracket notation is for when you need to computer it when the program runs.

The need for bracket notation doesn't stop at dynamically setting properties on an already-created Object. We can also use bracket notation to dynamically set properties _during the creation of a new Object_. For example:

```js
const morningMeal = "breakfast";
const middayMeal = "lunch";
const eveningMeal = "dinner";

const meals = {
  [morningMeal]: "French toast",
  [middayMeal]: "Personal pizza",
  [eveningMeal]: "Fish and chips"
};

meals;
//=> { breakfast: "French toast", lunch: "Personal pizza", dinner: "Fish and chips" }
```

Let's try doing the same without square brackets:

```js
const morningMeal = "breakfast";
const middayMeal = "lunch";
const eveningMeal = "dinner";

const meals = {
  morningMeal: "French toast",
  middayMeal: "Personal pizza",
  eveningMeal: "Fish and chips"
};

meals;
//=> { morningMeal: "French toast", middayMeal: "Personal pizza", eveningMeal: "Fish and chips" }
```

Without the square brackets, JavaScript treated each key as a literal identifier instead of a variable. Bracket notation—the _computed member access operator_—once again shows its powers of computation! Bracket notation really comes in handy when iterating over Objects and programmatically accessing and assigning properties.

## Adding a Property to an Object

To add properties to an `Object`, we can use either dot notation or bracket notation:

```js
const circle = {};

circle.radius = 5;

circle["diameter"] = 10;

circle.circumference = circle.diameter * Math.PI;
//=> 31.41592653589793

circle["area"] = Math.PI * circle.radius ** 2;
//=> 78.53981633974483

circle;
//=> { radius: 5, diameter: 10, circumference: 31.41592653589793, area: 78.53981633974483 }
```

Multiple properties can have the same value:

```js
const meals = {
  breakfast: "Avocado toast",
  lunch: "Avocado toast",
  dinner: "Avocado toast"
};

meals.breakfast;
//=> "Avocado toast"

meals.dinner;
//=> "Avocado toast"
```

But keys must be unique. If the same key is used for multiple properties, only the final value will be retained. The rest will be overwritten:

```js
const meals = {
  breakfast: "Avocado toast",
  breakfast: "Oatmeal",
  breakfast: "Scrambled eggs"
};

meals;
//=> { breakfast: "Scrambled eggs" }
```

We can update or overwrite existing properties by assigning a new value to an existing key:

```js
const mondayMenu = {
  cheesePlate: {
    soft: "Chèvre",
    semiSoft: "Gruyère",
    hard: "Manchego"
  },
  fries: "Curly",
  salad: "Cobb"
};

mondayMenu.fries = "Sweet potato";

mondayMenu;
//=> { cheesePlate: { soft: "Chèvre", semiSoft: "Gruyère", hard: "Manchego" }, fries: "Sweet potato", salad: "Cobb" }
```

Note that modifying an Object's properties in the way we did above is _destructive_. This means that we're making changes directly to the original Object. Instead, there are other methods we can use to make _non-destructive_ changes to our Objects called _convenience methods_. We can call a convenience method on an Object and save it to a variable to create a whole new Object!

## Using Convenience Methods

We can create a method that accepts the old menu and the proposed change:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  // Code to return new, updated menu object
}
```

Then, with the _spread operator_, we can copy all of the old menu Object's properties into a new Object:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  const newObj = { ...obj };

  // Code to return new, updated menu object
}
```

And finally, we can update the new menu Object with the proposed change and return the updated menu:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  const newObj = { ...obj };
  
  newObj[key] = value;

  return newObj;
}

const sundayMenu = nondestructivelyUpdateObject(tuesdayMenu, "fries", "Shoestring");

tuesdayMenu.fries;
//=> "Sweet potato"

sundayMenu.fries;
//=> "Shoestring"
```

**NOTE:** You may notice that we're using `const` here, but _adding_ a key and value; but that can't be right, since `const` means **_constant_**, the variable can't change. The _data_ in a `const` pointing to an `Array` or `Object` can still be changed, but a new value _cannot_ be assigned to the name. For example, given `const x = {}`, it's okay to say `x.dog = "Poodle"`, but it is **_not_** okay to say `x = [1, 2, 3]`.

Anyway, back to nondestructively returning Objects. We've got our code written, but it's quite a bit to write, and it's not very extensible. If we want to modify more than a single property, we'll have to completely rewrite our function. This is where convenience methods come into play.

### `Object.assign()`

JavaScript provides us access to a global `Object` of data type `Object` that has a bunch of helpful methods we can use. One of those methods is `Object.assign()`, which allows us to combine properties from multiple `Object` instances into a single `Object`. The first argument passed to `Object.assign()` is the initial `Object` into which all properties are merged. Every additional argument is an `Object` whose properties we want to merge into the first `Object`:

```js
Object.assign(initialObject, additionalObject, additionalObject, ...);
```

The return value of `Object.assign()` is the initial `Object` after the properties of each additional `Object` have been merged in. Here's an example:

```js
Object.assign({ eggs: 3 }, { flour: "1 cup" });
//=> { eggs: 3, flour: "1 cup" }

Object.assign({ eggs: 3 }, { chocolateChips: "1 cups", flour: "2 cups" }, { flour: "1/2 cup" })
//=> { eggs: 3, chocolateChips: "1 cup", flour: "1/2 cup" }
```

Pay attention to the `flour` property in the above example. **If multiple Objects have a property with the same key, the last key to be defined wins out.** Essentially, the last call to `Object.assign()` in the above snippet is wrapping all of the following assignments into a single line of code:

```js
const recipe = { eggs: 3 };

recipe.chocolateChips = "1 cup";

recipe.flour = "2 cups";

recipe.flour = "1/2 cup";
```

A common pattern for `Object.assign()` is to provide an empty Object as the first argument. That way we're composing an entirely new Object instead of modifying or overwriting the properties of an existing Object. This pattern allows us to rewrite the above `destructivelyUpdateObject()` function in a nondestructive way:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  return Object.assign({}, obj, { [key]: value });
}

const recipe = { eggs: 3 };

const newRecipe = nondestructivelyUpdateObject(recipe, "chocolate", "1 cup");
//=> { eggs: 3, chocolate: "1 cup" }

newRecipe;
//=> { eggs: 3, chocolate: "1 cup" }

recipe;
//=> { eggs: 3 }
```

It's important that we merge everything into a new, empty Object. Otherwise, we would be modifying the original Object.

Let's write a function for our restaurant that accepts an old menu and some changes we want to make and returns a new menu **without modifying the old menu**:

```js
function createNewMenu(oldMenu, menuChanges) {
  return Object.assign({}, oldMenu, menuChanges);
}

const tuesdayMenu = {
  cheesePlate: {
    soft: "Chèvre",
    semiSoft: "Gruyère",
    hard: "Manchego"
  },
  fries: "Sweet potato",
  salad: "Caesar"
};

const newOfferings = {
  cheesePlate: {
    soft: "Brie",
    semiSoft: "Fontina",
    hard: "Provolone"
  },
  salad: "Southwestern"
};

const wednesdayMenu = createNewMenu(tuesdayMenu, newOfferings);

wednesdayMenu;
//=> { cheesePlate: { soft: "Brie", semiSoft: "Fontina", hard: "Provolone" }, fries: "Sweet potato", salad: "Southwestern" }

tuesdayMenu;
//=> { cheesePlate: { soft: "Chèvre", semiSoft: "Gruyère", hard: "Manchego" }, fries: "Sweet potato", salad: "Caesar" }
```

For deep cloning, we need to use other alternatives because `Object.assign()` copies property values. For example, if `newOfferings` did not have an updated value for `hard` cheese such as:

```js
const newOfferings = {
  cheesePlate: {
    soft: 'Brie',
    semiSoft: 'Fontina'
  },
  salad: 'Southwestern'
};
```

Our output for `const wednesdayMenu = createNewMenu(tuesdayMenu, newOfferings);` would look like this:

```js
wednesdayMenu;
//=> { cheesePlate: { soft: "Brie", semiSoft: "Fontina" }, fries: "Sweet potato", salad: "Southwestern" }
```

Instead of the desired outcome we saw above.

### `Object.keys()`

Another convenience method available on the global `Object` of data type `Object` is `Object.keys()`. When an `Object` is passed as an argument to `Object.keys()`, the return value is an `Array` containing all of the keys at the top level of the `Object`:

```js
const wednesdayMenu = {
  cheesePlate: {
    soft: "Brie",
    semiSoft: "Fontina",
    hard: "Provolone"
  },
  fries: "Sweet potato",
  salad: "Southwestern"
};

Object.keys(wednesdayMenu);
//=> ["cheesePlate", "fries", "salad"]
```

Notice that it didn't pick up the keys in the nested `cheesePlate` Object, just the keys from the properties declared at the top level within `wednesdayMenu`.

**NOTE:** The sequence in which keys are ordered in the returned Array is not consistent across browsers and should not be relied upon. All of the Object's keys will be in the Array, but you can't count on `keyA` always being at index `0` of the Array and `keyB` always being at index `1`.

## Removing a Property from an Object

We just ran out of Southwestern dressing, so we have to take the salad off the menu. In JavaScript, that's as easy as:

```js
const wednesdayMenu = {
  cheesePlate: {
    soft: "Brie",
    semiSoft: "Fontina",
    hard: "Provolone"
  },
  fries: "Sweet potato",
  salad: "Southwestern"
};

delete wednesdayMenu.salad;
//=> true

wednesdayMenu;
//=> { cheesePlate: { soft: "Brie", semiSoft: "Fontina", hard: "Provolone" }, fries: "Sweet potato" }
```

We pass the property that we'd like to remove to the `delete` operator, and JavaScript takes care of the rest.

## The Relationship Between Arrays and Objects

Remember an earlier lesson where we discussed the fundamental data types in JavaScript. We listed off seven types into which all data falls: `Number`, `String`, `Boolean`, `Symbol`, `Object`, `null`, and `undefined`. Why isn't an `Array` a fundamental data type in JavaScript? The answer is that it's _actually_ a special type of `Object`. Yes, that's right: **Arrays are Objects**. To underscore this point, check out what the `typeof` operator returns when we use it on an `Array`:

```js
typeof [];
//=> "object"
```

We can set properties on an `Array` just like a regular `Object`:

```js
const myArray = [];

myArray.summary = "Empty array!";

myArray;
//=> [summary: "Empty array!"]
```

And we can modify and access those properties too:

```js
myArray["summary"] = "This array is totally empty.";

myArray;
//=> [summary: "This array is totally empty."]

myArray.summary;
//=>  "This array is totally empty."
```

In fact, _everything_ we just learned how to do to `Object` data types can also be done to an `Array` because **Arrays are Objects**; just special ones. To see the special stuff, let's `.push()` some values into our Array:

```js
myArray.push(2, 3, 5, 7);
//=> 4

myArray;
//=> [2, 3, 5, 7, summary: "This array is totally empty."]

myArray.length;
//=> 4

myArray[0];
//=> 2

myArray[myArray.length - 1];
//=> 7
```

Above, we pushed four items into our Array, which already had the `summary` property with some text. However, when we called `.length` on our Array, we got back `4`, as in four items exist in our Array. Our first item from our Array returned `2` and our last item from our Array returned `7`; so where did `summary` go?

You see, one of the "special" features of an `Array` is that **its Array-style elements are stored separately from its Object-style properties**. The `.length` property of an `Array` describes how many items exist in its special list of elements. Its Object-style properties are not included in that calculation.

This brings up an interesting question: if we add a new property to an `Array` that has a key of `0`, how does the JavaScript engine know whether it should be an Object-style property or an Array-style element?

```js
const myArray = [];

myArray[0] = "Will this be an `Object` property or an `Array` element?";
//=> "Will this be an `Object` property or an `Array` element?"

myArray.length;
//=> 1
```

JavaScript used that assignment operation to add a new Array-style element. What happens if we enclose the integer in quotation marks, turning it into a string?

```js
myArray["0"] = "What about this one?";
//=> "What about this one?"

myArray.length;
//=> 1

myArray;
//=> ["What about this one?"]
```

This is hitting on a fundamental truth: **all keys in Objects and indexes in Arrays are actually strings**. In `myArray[0]` we're using the integer `0`, but under the hood the JavaScript engine automatically converts that to the string `"0"`. When we access elements or properties of an `Array`, the engine routes all integers and integers masquerading as strings to the Array's special list of elements, and it treats everything else as a simple `Object` property. For example:

```js
const myArray = [2, 3, 5, 7];

myArray["1"] = "Hi";
//=> "Hi"

myArray;
//=> [2, "Hi", 5, 7]

myArray["01"] = "Ho";
//=> "Ho"

myArray;
//=> [2, "Hi", 5, 7, 01: "Ho"]

myArray[01];
//=> "Hi"

myArray["01"];
//=> "Ho"
```

After adding our `"01"` property, the `.length` property still returns `4`:

```js
myArray.length;
//=> 4
```

So it would stand to reason that `Object.keys()` would only return `"01"`, right?

```js
Object.keys(myArray);
//=> ["0", "1", "2", "3", "01"]
```

Unfortunately not. The reason why Arrays have this behavior would take us deep inside the JavaScript source code, and it's frankly not that important. Just remember these simple guidelines and you'll be fine:

- **For accessing elements in an Array, always use integers.**
- **Be wary of setting Object-style properties on an Array.** There's rarely any reason to and it's usually more trouble than it's worth.
- **Remember that all Object keys, including Array indexes, are strings.** This will really come into play when we learn how to iterate over Objects, so keep it in the back of your mind.

## Conclusion

We identified what an `Object` is and how to access values stored in it. We also covered how to add and remove properties, and use the convenience methods `Object.assign()` and `Object.keys()`. We also traced the link between the `Object` data type and `Array` data type.

### Resources

- [`Object.assign()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
- [`Object.keys()` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
- [`delete` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)
- [Object Basics (MDN)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics)
- [Objects in JavaScript: `Object.assign()`/Deep Copy](https://medium.com/@tkssharma/objects-in-javascript-object-assign-deep-copy-64106c9aefab)
