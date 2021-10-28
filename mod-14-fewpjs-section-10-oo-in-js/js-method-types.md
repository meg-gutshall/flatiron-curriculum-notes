---
description: 'Version 8: Module 14: Section 10: Lesson'
---

# Method Types (OOJS)

So far, we've seen some examples of classes that have their own custom methods:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = sideLength;
  }

  area() {
    return this.sideLength ** 2;
  }
}
```

It turns out, however, there are four different types of methods we can write in a class: the standard "instance method" we've seen already, static, getter, and setter methods. Each of these behaves differently, and this variety provides us with flexibility in how we design the behaviors of our classes.

## Standard Methods

Most class methods you will see use the following, standard syntax:

```javascript
area() {
  return this.sideLength * this.sideLength;
}
```

These methods are available to any instance of the class they belong to, as we've seen:

```javascript
let square = new Square(5);
square.area();
//=> 25
```

Methods can be called from inside other methods, just like properties:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = side.Length;
  }

  area() {
    return this.sideLength * this.sideLength;
  }

  areaMessage() {
    return `The area of this square is ${this.area()}`;
  }
}

let square = new Square(5);
square.area();
//=> 25
square.areaMessage();
// LOG: The area of this square is 25
```

In the class above, we can access `area()` directly, or use it to provide dynamic content for other methods. These methods are the most common—they act as the 'behaviors' of a class instance.

## Static Methods

Static methods are class-level methods; they can only be called on the class itself. These are often used in "utility" classes, or classes that encapsulate a set of related methods but don't need to be made into instances. For example, we could write a `CommonMath` class that stores a series of math-related methods:

```javascript
class CommonMath {
  static cubed(number) {
    return number * number * number;
  }

  static findHypotenuse(a, b) {
    return Math.sqrt(a * a + b * b);
  }
}
```

To access these static methods:

```javascript
let num = CommonMath.cubed(3);
num;
//=> 27

let c = CommonMath.findHypotenuse(3, 4);
c;
//=> 5
```

This sort of class might be useful in many different situations, but we don't ever need an _instance_ of it.

## Define `get` Keyword in JavaScript Class Context

Often, when writing methods for a class, we want to return information derived from that instance's properties. In modern JavaScript, new syntax, `get` has been introduced. The `get` keyword is used in classes for methods which serve the specific purpose of retrieving data from an instance.

The `get` keyword turns a method into a pseudo-property; it allows us to write a method that interacts like a property. To use `get`, write a class method like normal, preceded by `get`:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = sideLength;
  }

  get area() {
    return this.sideLength ** 2;
  }
}
```

As a result of this, `area` will now be available as though it is a property just like `sideLength`:

```javascript
let square = new Square(5);
square.sideLength;
//=> 5
square.area;
//=> 25
```

If you try to use `this.area()`, you'll receive a TypeError—`area` is no longer considered a function!

You could also just write the following code a achieve the same result:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = sideLength;
    this.area = sideLength * sideLength;
  }
}
```

This is valid code, but what we've done is load our `constructor` with more calculations.

The main benefit of using `get` is that your `area` calculation isn't actually run until it is accessed. The "cost" of calculating is offset, and may not be called at all. While our computers can make short work of this example, these are times when we need to perform calculations that are CPU intensive, sometimes referred to as "costly" or "expensive" processes.

If included in the `constructor`, an expensive process will be called every time a new instance of a class is created. When dealing with many instanced, this can result in decreased performance. Using `get`, an expensive process can be delayed, distributing the workload more evenly.

Even if your process is not expensive, using `get` is useful in general when deriving or calculating data from properties. Since properties can changes, any values dependent on them should be calculated based on the current property values, otherwise we will run into issues like this:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = sideLength;
    this.area = sideLength * sideLength;
  }
}

let square = new Square(5);
square.area;
//=> 25
square.sideLength = 10;
square.area;
//=> 25
```

If `area` is only calculated in the beginning, and `sideLength` is then modified, `area` will no longer be accurate.

## Define `set` Keyword in JavaScript Class Context

Using `get` to create a pseudo-property is only half the story, since it is only used for retrieving data from an instance. To change data, we have `set`.

The `set` keyword allows us to write a method that interacts like a property being assigned a value. By adding it in conjunction with a `get`, we can create a reassignable pseudo-property.

For example, in the previous section we used `get` in the `Square` class:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = sideLength;
  }

  get area() {
    return this.sideLength ** 2;
  }
}
```

This allowed us to retrieve the area of a `Square` instance like so:

```javascript
let square = new Square(5);
square.sideLength;
//=> 5
square.area;
//=> 25
```

If we change `square.sideLength`, `square.area` will update accordingly:

```javascript
square.sideLength = 10;
square.area;
//=> 100
```

However, we can't _assign_ `area` a new value. To `area` fully act like a real property, we create both `get` and `set` methods for it:

```javascript
class Square {
  constructor(sideLength) {
    this.sideLength = sideLength;
  }

  get area() {
    return this.sideLength ** 2;
  }

  set area(newArea) {
    this.sideLength = Math.sqrt(newArea);
  }
}
```

We can now "set" the pseudo-property, `area`, and modify `this.sideLength` based on a reverse of the calculation we used in `get`:

```javascript
let square = new Square(5);
square.sideLength;
//=> 5
square.area;
//=> 25
square.area = 64;
square.sideLength;
//=> 8
square.area;
//=> 64
```

We can now interact with `area` as though it is a modifiable property, even though `area` is derived.

From the outside, it looks like a property is being set, but behind the scenes, we can define what we want to happen, including applying conditional statements:

```javascript
set area(newArea) {
  if (newArea > 0) {
    this.sideLength = Math.sqrt(newArea);
  } else {
    console.warn("Area cannot be less than 0");
  }
}
```

Creating pseudo-properties this way enables us to finely tune how data can be both accessed and modified. In using `get` and `set`, we are designing the interface for our class.

## Using `get` and `set` with "Private" Properties

You may remember that in JavaScript, properties are exposed. That is, any property can be reassigned from outside its class. Here is where `get` and `set` really shine. Although there is no official "private" property yet, an underscore at the beginning of a property is commonly used to indicate that method should not be directly modified. With `get` and `set`, we can define the "public"-facing methods for updating a "private" property:

```javascript
class Square {
  constructor(sideLength) {
    this._sideLength = sideLength;
  }

  get sideLength() {
    this._sideLength;
  }

  set sideLength(sideLength) {
    this._sideLength;
  }
}
```

A square's side can't have negative length. Now with our pseudo-property in place, we write code to make sure that `_sideLength` is always valid, both when an instance property is created and when it is modified:

```javascript
class Square {
  constructor(sideLength) {
    if (sideLength > 0) {
      this._sideLength = sideLength;
    } else {
      throw new Error("A square cannot have negative side length");
    }
  }

  get sideLength() {
    this._sideLength;
  }

  set sideLength(sideLength) {
    if (sideLength > 0) {
      this._sideLength = sideLength;
    } else {
      throw new Error("A square cannot have negative side length");
    }
  }
}
```

We could always extract that duplicate code into a helper method, but the takeaway here is the design. We've designed our `Square` classes to be a little more resistant to unwanted changes that might introduce bugs.

Stepping away from `Squares` for a moment, let's consider an example with string properties. Imagine we want to build a `Student` class. The class takes in a student's first and last name. We are tasked with making sure names do not have any non-alphanumeric characters except for those that appear in names. This is sometimes referred to a _sanitizing_ text.

With `set`, we can make sure that we sanitize input text both when an instance is created, as well as later, if the property needs to change:

```javascript
class Student {
  constructor(firstName, lastName) {
    this._firstName = this.sanitize(firstName);
    this._lastName = this.sanitize(lastName);
  }

  get firstName() {
    return this.capitalize(this._firstName);
  }

  set firstName(firstName) {
    this._firstName = this.sanitize(firstName);
  }

  capitalize(string) {
    // capitalizes first letter
    return string.charAt(0).toUpperCase() + string.slice(1);
  }

  sanitize(string) {
    // removes any non-alphanumeric characters except dash and apostrophe
    return string.replace(/[^A-Za-z0-9-']+/g, '');
  }
}

let student = new Student("Carr@ol-Ann", ")Freel*ing");
student;
//=> Student { _firstName: 'Carrol-Ann', _lastName: 'Freeling' }
student.firstName = "Hea@)@(!$)ther";
student.firstName;
//=> 'Heather'
```

In this `Student` class, we've set up a pseudo-property, `firstName`, which refers to a "private" property `_firstName`. We've also included a `sanitize()` method that removes any non-alphanumeric characters except `-` and `'`.

Because we are using `set` and a "private" property, we can call `sanitize when a`Student`instance is constructed, _or_ when we try to modify`\_firstName\`.

## When to Use Methods Over `get` and `set`

Although `get` and `set` change the way in which we interact with a class, normal instance methods can do everything that `get` and `set` can do. So, which should we use and when? JavaScript itself is indifferent.

With `get` and `set`, while we don't gain any sort of extra functionality, we gain the ability to _differentiate_ between behaviors. **We can use `get` and `set` whenever we are handling input or output of a class.** We are, in essence, creating the _public interface_ of the class. We can treat this interface as a menu of sorts. `get` and `set` methods are the ways in which _other_ classes and code _should_ utilize this class.

Using this design, all remaining methods can be considered _private_. They don't deal with input and output; they are only used internally as helper methods.

It is important to note that in JavaScript currently, we can _always_ order off the menu. All class methods and properties are exposed for use "publicly." Using `get` and `set` in this way is purely design. In designing this way, however, we produce better organized, easier to understand classes.

## Conclusion

In the object-oriented JavaScript world, we have a variety of ways to build our classes. Flexibility is important. It allows us to design many classes that work together, each serving their own specific purpose that we have defined.

## Resources

* [Static Methods (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static)
* [Classes: Static Methods (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#Static\_methods)
* [`get` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)
* [`set` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set)
* [Property Getters and Setters (The Modern JavaScript Tutorial)](https://javascript.info/property-accessors)
