---
description: 'Version 8: Module 14: Section 10: Lesson'
---

# Classes and Instances (OOJS)

In object-oriented JavaScript, objects share a similar structure: the class. Each class has the ability to generate copies of itself, referred to as _instances_. Each of these class instances can contain unique data, often set when the instance is created.

## A Basic Class

The class syntax was introduced in [ECMAScript 2015](https://www.w3schools.com/js/js\_es6.asp) and it's important to note that the `class` keyword is just syntactic sugar, or a nice abstraction, over JavaScript's existing prototypal object structure.

{% hint style="warning" %}
**REMINDER:** All JavaScript objects inherit properties and methods from a prototype. This includes standard objects like functions and data types.
{% endhint %}

A basic, empty class can be written on one line:

```javascript
class Fish {};
```

With only a name and brackets, we can ne create instances of the "Fish" class by using `new`:

```javascript
let oneFish = new Fish();
let twoFish = new Fish();

oneFish; //=> Fish {}
twoFish; //=> Fish {}

oneFish == twoFish; //=> false
```

These two fish are unique class instances, event though they have no information encapsulated within them.

## Using the `constructor` Method

Typically, when we create an instance of class, we want it to contain some bit of unique information from the beginning. To do this, we use a special method called `constructor`:

```javascript
class Fish {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  };
};
```

The `constructor` method allows us to pass arguments in when we use the `new` syntax:

```javascript
let redFish = new Fish('Red', 3);
let blueFish = new Fish('Blue', 1);

redFish; //=> Fish { name: 'Red', age: 3 }
blueFish; //=> Fish { name: 'Blue', age: 1 }
```

Now our instances are each carrying unique data. It is possible to add and change data using other means _after_ an instance is created using custom methods, but the `constructor` is where any initial data is defined.

## Assigning Instance Properties

We see that our fish have data, but what is happening exactly inside the `constructor`?

```javascript
constructor(name, age) {
  this.name = name;
  this.age = age;
};
```

Two arguments, `name` and `age`, are passed in and then assigned to something new: `this`.

For now, think of `this` as a reference to the object it is inside. Since we're calling `constructor` when we create a new instance, `this` is referring to the _instance we've created_. _This_ fish.

{% hint style="info" %}
**NOTE:** In class methods, `this` acts similarly to Ruby's `self` keyword. `this` can be used to refer to properties of an instance, like `name` and `age`, or methods of an instance, like `this.sayName()`. There is more to `this` than meets the eye, however, and we'll go into more detail later on.
{% endhint %}

## Accessing Instance Properties

If we've assigned an instance variable, we can access properties using the variable object:

```javascript
let oldFish = new Fish('George', 19);
let newFish = new Fish('Clyde', 1);

oldFish.name; //=> 'George'
oldFish.age; //=> 19
newFish.name; //=> 'Clyde'
newFish.age; //=> 1
```

By using `this.name` and `this.age` to define properties in our `constructor` method, we can also refer to these properties within other methods of our class:

```javascript
class Fish {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  };

  sayName() {
    return `Hi! My name is ${this.name}!`;
  };
};
```

This allows us to return dynamic information based on the unique properties we assigned back when an instance was created. Another example:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = sideLength;
  };

  area() {
    return this.sideLength ** 2;
  };
};

let square = new Square(5);
square; //=> Square { sideLength: 5 }
square.sideLength; //=> 5
square.area(); //=> 25
```

### Private Properties

All properties are accessible from outside an instance, as well as from within class methods.

This is not always desirable. Sometimes, we want to protect the data from being modified after being set, or we want to use methods to control the exact ways our data should be changed.

For example, say we had a `Transaction` class that we are using to represent individual bank transactions. When a new `Transaction` instance is created, it has `amount`, `date`, and `memo` properties:

```javascript
class Transaction {
  constructor(amount, date, memo) {
    this.amount = amount;
    this.date = date;
    this.memo = memo;
  };
};
```

The `amount`, `date`, and `memo` properties represent fixed values for each time a `Transaction` instance is created and probably shouldn't be altered. However, it is still possible to change these properties after they're assigned:

```javascript
let transaction = new Transaction(100.24, '03/04/2018', 'Grocery Shopping');
transaction.amount; //=> 100.24
transaction.amount = 100000.24;
transaction.amount; //=> 100000.24
```

Currently, there is no official way to make a property private; all class and object properties are exposed as we see above. One common convention, however, is to include an underscore at the beginning of the property name to indicate those properties are not intended to be accessed outside the class:

```javascript
class Transaction {
  constructor(amount, date, memo) {
    this._amount = amount;
    this._date = date;
    this._memo = memo;
  };
};
```

Now, it is _still_ possible to modify these properties, the `amount` property name just changed to `_amount`. The above class setup, however, _suggests_ that these properties should only be accessed or changed through class methods, not directly.

Implementing private properties is planned in [future versions of JavaScript](https://www.sitepoint.com/javascript-private-class-fields/), and will use a `#` symbol to indicate a property is private.

## Conclusion

We can define a class simply by writing class, a name, and a set of curly brackets. We can then use this class to create unique instances. These instances can contain their own data, which we typically set using the `constructor` method, passing in arguments and assigning them to properties we've defined. With these properties, class instances can carry data around with them wherever they go. While there are no private properties (yet), it is possible to set up classes to emphasize using methods over directly changing properties.

## Resources

* [Classes (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
