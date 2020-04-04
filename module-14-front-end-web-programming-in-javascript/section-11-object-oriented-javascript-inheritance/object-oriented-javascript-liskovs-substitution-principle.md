# Lesson: Liskov's Substitution Principle (Object-Oriented JavaScript)

Much work has been done in the field of object-oriented programming, and over the last few decades engineers have developed design patterns and principles that are meant to help keep object-oriented code easier to understand and maintain. One principle in particular applies to inheritance and extension: Liskov's substitution principle.

## Recognize the Meaning of Strong Behavioral Subtyping

Liskov's substitution principle, also known as strong behavioral subtyping, is the 'L' in [SOLID](https://en.wikipedia.org/wiki/SOLID), a popular set of object-oriented design principles.

**Liskov's substitution principle**: Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.

In terms of JavaScript inheritance, **an instance of a parent class should be replaceable with an instance of a child class.**

If we follow this principle, the consequence is that properties and methods that exist on the parent will never be modified in any child. Child classes can _expand_ upon what they inherited, adding methods or extra properties, and do not modifying what they inherited.

If you need to modify a child's inherited properties or methods, why are we inheriting them in the first place?

Below are two examples; one that violates Liskov's substitution principle, and one the upholds it:

### Violates Liskov's Substitution Principle

```js
class Reptile {
  constructor(name) {
    this.name = name;
  }

  get move() {
    return `${this.name} crawls away`;
  }
}

// Lizard inherits `move()` because it crawls
class Lizard extends Reptile {}

// Snake overrides `move()` because it cannot crawl
class Snake extends Reptile {
  get move() {
    return `${this.name} slithers away`;
  }
}
```

The `Snake` class is a subtype of class `Reptile`, but overrides the `move()` getter because the original doesn't apply. If we created an instance of `Reptile`:

```js
let tricky = new Reptile("Tricky");
//=> Reptile { name: "Tricky" }
```

And an instance of `Snake`:

```js
let basilisk = new Snake("Basilisk");
//=> Snake { name: "Basilisk" }
```

We see that `tricky` cannot be replaced with `basilisk` without changing behavior:

```js
tricky.move();
//=> "Tricky crawls away"
basilisk.move();
//=> "Basilisk slithers away"
```

## Upholds Liskov's Substitution Principle

So how do we stop violating Liskov's substitution principle? We can either choose to not inherit from the same parent, _or_ we can create a grandparent `Reptile` class. This grandparent class can still contain all shared data and behavior for all parent and child classes. Since the definition of `move()` is _not_ shared by all, we can move these definitions down a level, defining them in two new parent classes:

```js
// All reptiles have a name
class Reptile {
  constructor(name) {
    this.name = name;
  }
}

// Legless reptiles slither
class LeglessReptile extends Reptile {
  move() {
    return `${this.name} slithers away`;
  }
}

// Legged reptiles crawl
class LeggedReptile extends Reptile {
  move() {
    return `${this.name} crawls away`;
  }
}

class Lizard extends LeggedReptile;
class Snake extends LeglessReptile;
```

Now we've got two levels of inheritance. `Reptile` sets up the `constructor` that all children and grandchildren inherit. Because `move()` needs to behave differently for legged and legless reptiles, it is defined differently in both `LeglessReptile` and `LeggedReptile`.

With this structure, if an instance of `Lizard` replaced an instance of `LeggedReptile` _or_ `Reptile`, it will work correctly. The same goes for an instance of `Snake`.

>Why does this work? We've removed some of the behavior from `Reptile`. An instance of `Reptile` will never be required to utilize a method it hasn't defined or inherited.

## Recognize the Benefits of Upholding Liskov's Substitution Principle

Both of the above examples _work_. There is no syntax error if you choose to ignore Liskov's substitution principle. This is considered a purely _semantic_ design choice.

The benefit of following this principle is that no matter how complicated inheritance gets, you can always assume that whetever a parent class has, a child class will have too. Looking at a parent class should give us some insight into the functionality of any children, grandchildren, great grandchildren, etc...

If we have chains of inheritance where children fundamentally change the data behaviors they inherit, we can potentially introduce bugs. More importantly, this can also make your code much more complicated that it need to be, which will make it harder to change and understand.

As per Liskov's substitution principle, a child class may include _more_ properties or use the data _differently_. If you do find that a child class meed to overwrite a method or property it inherited from its parent, consider other options – perhaps don't inherit at all!

**NOTE:** In general, when dealing with inheritance, the fewer levels of inheritance, the better. If you've got great grandparent, grandparent, parent, and child classes, it can be difficult to figure out which class contributes what to a child. It also makes our code more difficult to change. You may not be able to modify code on a grandparent class without fundamentally changing how a parent or child class functions. Too much inheritance can make our code inflexible.

Upholding Liskov's substitution principle limits what we can do with inheritance, discouraging largar chains of inherited classes. AS a side effect, our code is easier to understand and change later on.

## Conclusion

Liskov's substitution principle ensures that all subtypes may replace their types without altering the behavior of the program. An instance of a parent class should be replacement be an instance of any of its child classes and still work as expected. The result of this pattern is a clearer, consistence inheritance pattern that leads to more organized, easier to change code.
