# Lesson: Class Extension and Inheritance Extends (Object-Oriented JavaScript)

In JavaScript, as in other object-oriented languages, we can create classes and build methods that can perform actions on instance data, or specific to the class. What if you have classes that exhibit many of the same behaviors, such as `Cat`, `Dog`, and `Bird`, which all have a method for `speak()`?

```js
class Dog {
  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} says woof!`;
  }
}

class Cat {
  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} says meow!`;
  }
}

class Bird {
  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} says squawk!`;
  }
}
```

In this code snippet, `Dog`, `Cat`, and `Bird` all accept `name` and have a method called `speak()`, thus repeating code. In JavaScript, we can create "child" object classes that inherit methods and properties from their "parent" classes, allowing us to reuse some class methods while building in additional functionality.

## Use the `extends` Keyword

To get started with inheriting class functionality, we utilize the `extends` keyword. `extends` is used in class declarations to create a class which is a _child_ of another class:

```js
class Pet {
  constructor(name, sound) {
    this.name = name;
    this.sound = sound;
  }

  speak() {
    return `${this.name} says ${this.sound}!`;
  }
}

class Dog extends Pet {
  // inherits constructor from Pet
}

class Cat extends Pet {
  // inherits constructor from Pet
}

class Bird extends Pet {
  // inherits constructor from Pet
  fly() {
    return `${this.name} flies away!`;
  }
}

let dog = new Dog("Shadow", "woof");
let cat = new Cat("Missy", "meow");
let bird = new Bird("Tiki", "squawk");

dog.speak();
//=> Shadow says woof!
cat.speak();
//=> Missy says meow!
bird.speak();
//=> Tiki says squawk!
bird.fly();
//=> Tiki flies away!
```

In addition to _inheriting_ the functionality of the `Pet` class, each "child" class extends the functionality of the parent. For example, `Bird` has an additional method called `fly()` that is unique to it and not present on `Pet`, but `Bird` can still call `speak()`.

## Conclusion

Class extensions and inheritance in JavaScript allow us to leverage object-orientation concepts. With `extends` we can create new classes that are capable of utilizing all of the same methods as its parent. Leveraging inheritance and `extends` is vital in object-oriented programming. It keeps code bases maintainable by sharing and reusing code in a beneficial manner.

### Resources

- [Inheritance in JavaScript (MDN)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)
- [`extends` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends)
- [`getter` (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)
- ["Super" and "Extends" in JavaScript ES6 — Understanding the Tough Parts (Beginner's Guide to Mobile Web Development)](https://medium.com/beginners-guide-to-mobile-web-development/super-and-extends-in-javascript-es6-understanding-the-tough-parts-6120372d3420)
