# Lab: Destructuring Assignment

As developers sometimes we receive information in a collection like an `Object` and we want to "pick and choose" elements out of the collection. It's a major pain to extract each property/value pair out of an `Object` and then assign it to a variable.

Destructuring lets us type less and be more clear about what we want to pull out of an `Object`. Not only does destructuring help when working with data in your application, it's essential for understanding how to get JavaScript to include third-party code (like you find on [npm](https://www.npmjs.com/)).

## Use Destructuring to Assign Data to Variables

In JavaScript, when we want to assign data to single variables from a top level object such as this, we normally do it individually like so:

```js
const doggie = {
  first: 'Buzz,
  breed: 'Great Pyrenees',
  fur_color: 'black and white',
  activity_level: 'sloth-like',
  favorite_food: 'hot_dogs'
};

const first = doggie.first; // Buzz
const breed = doggie.breed; // Great Pyrenees
```

This is repetitive code. The algorithm at play is:

1. Declare a variable with a name (e.g., `first` or `breed`)
2. Use that variable's name to point to an attribute in the `Object` whose name matches the name of the variable (e.g., `doggie.breed` or `doggie.first`)
3. Assign the attribute's value to the created variable

JavaScript gives us the ability to perform this algorithm with _one_ simple line of code.

```js
const doggie = {
  first: 'Buzz,
  breed: 'Great Pyrenees',
  fur_color: 'black and white',
  activity_level: 'sloth-like',
  favorite_food: 'hot_dogs'
};

const { first, breed } = doggie;
console.log(first); // Buzz
console.log(breed); // Great Pyrenees
```

We can also use it to destructure a nested syntax:

```js
const doggie = {
  first: 'Buzz,
  breed: 'Great Pyrenees',
  fur_color: 'black and white',
  activity_level: 'sloth-like',
  favorite_foods: {
    meats: {
      ham: 'smoked',
      hot_dog: 'oscar_meyer',
    },
    cheeses: {
      american: 'kraft'
    }
  }
};

const { ham, hot_dog } = doggie.favorite_foods.meats;
console.log(ham); // smoked
console.log(hot_dog); // oscar_meyer
```

### Destructuring Assignment with Arrays

Destructuring does not work only on objects—we can use the same syntax with arrays as well.

```js
const dogs = ['Great Pyrenees', 'Pug', 'Bull Mastiff'];
const [medium, small, giant] = dogs;
console.log(medium, small, giant); // Great Pyrenees, Pug, Bull Mastiff
```

The cool part is we can pick the parts of the array that we want to assign!

```js
const dogs = ['Great Pyrenees', 'Pug', 'Bull Mastiff'];
const [, small, giant] = dogs;
console.log(small, giant); // Pug, Bull Mastiff
```

Destructuring Assignment with Strings

We can also destructure with strings, as a whole...

```js
const dogsName = 'Sir Woody BarksALot';
const [title, firstName, lastName] = 'Sir Woody BarksALot'.split(' ');
console.log(title, firstName, lastName); // Sir Woody BarksALot
```

...and in parts, just as we did with the arrays above:

```js
const dogsName = 'Sir Woody BarksALot';
const [title, , lastName] = 'Sir Woody BarksALot'.split(' ');
console.log(title, lastName); // Sir BarksALot
```

## Conclusion

"Destructuring assignment" is a fast and efficient way to assign data to variables from objects, arrays, and strings. It allows us to pick and choose the pieces of data the we want to assign and gives us lots of freedom to manipulate the data as it is coming in.

### Resources

- [Destructuring Assignment (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
