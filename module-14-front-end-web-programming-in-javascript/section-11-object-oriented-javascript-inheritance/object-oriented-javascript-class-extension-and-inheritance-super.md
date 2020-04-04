# Lesson: Class Extension and Inheritance Super (Object-Oriented JavaScript)

In addition to simply extending classes, JavaScript provides an additional keyword, `super`, for directly working with a parent class constructor and inherited models.

## Recognize How to Use the `super` Method

In the code below, we have two JavaScript classes: `Pet` and `Dog`. The `Dog` class is a _child_ class of `Pet` and it uses the `extends` keyword to inherit methods from the parent class:

```js
class Pet {
  constructor(name) {
    this._name = name;
    this._owner = null;
  }

  get name() {
    return this._name;
  }

  get owner() {
    return this._owner;
  }

  set owner(owner) {
    this._owner = owner;
  }

  get speak() {
    return `${this.name} speaks.`;
  }
}

// Inherits from Pet
class Dog extends Pet {
  constructor(name, breed) {
    super(name); // new
    this.breed = breed;
  }
}

let creature = new Pet("The Thing");
let dog = new Dog("Spot", "Foxhound");

dog;
//=> Dog { _name: "Spot", _owner: null, breed: "Foxhound" }
```

Above, there is something new. The `Pet` class takes in a name parameter, assigns it to the `name` property, and also creates an `_owner` property, setting it to `null`. The `Dog` class takes in **name and breed** properties, calls `super`, passing in the name, then sets `this.breed` to the provided breed.

What is happening? On our `Dog` constructor, we are able to use `super` to call the `Pet` constructor. Doing this will set up the `name` and `owner` properties. Then, once complete, the `Dog` constructor continues to execute, setting `breed`.

In a child class constructor, `super` is used as a `method` and calls the parent class constructor before continuing with the child. This lets us extend a parent's constructor inside a child. If we need to define custom behavior in a child constructor, we can do so without having to override or ignore the parent.

## Recognize How to Use the `super` Object

Outside of the constructor, the `super` keyword is also used, but this time as an object. When used, it refers to parent class' properties or methods.

For instance, we could use `super.owner` in our `Dog` class:

```js
// Inherits from Pet
class Dog extends Pet {
  constructor(name, breed) {
    super(name); // new
    this._breed = breed;
  }

  get breed() {
    return this._breed;
  }

  get info() {
    if (super.owner) {
      return `${this.name} is a ${this.breed} owned by ${super.owner}`;
    }
    return `${this.name} is a ${this.breed}`;
  }
}

let charlie = new Dog("Charlie B. Barkin", "Mutt");
dog.info;
//=> "Charlie B. Barkin is a Mutt"

let lady = new Dog("Lady", "Cocker Spaniel");
lady.owner = "Darling Dear";
lady.info;
//=> "Lady is a Cocker Spaniel owned by Darling Dear"
```

In the above code, we've added an `info` getter that uses `super.owner` in a conditional statement. This accesses the `owner` getter from the parent.

**However**, since instance methods and properties are _already_ inherited, this _will be the same as using_ `this.owner`.

Using `super` as an object is useful in situations where a parent class contains a static method that we want to expand on in a child class:

```js
class Pet {
  constructor(name) {
    this.name = name;
    this._owner = null;
  }

  get owner() {
    return this._owner;
  }

  set owner(owner) {
    this._owner = owner;
  }

  static definition() {
    return "A pet is an animal kept primarily for a person's company.";
  }
}

// Inherits from Pet
class Dog extends Pet {
  constructor(name, breed) {
    super(name);
    this.breed = breed;
  }

  static definition() {
    return (
      super.definition() + " Dogs are one of the most common types of pets."
    );
  }
}

let creature = new Pet("The Thing");
let dog = new Dog("Spot", "Foxhound");

Pet.definition();
//=> "A pet is an animal kept primarily for a person's company."
Dog.definition();
//=> "A pet is an animal kept primarily for a person's company. Dogs are one of the most common types of pets."
```

In the `Pet` class above, we've included a static method, `definition()`, for what a pet is. In `Dog`, we are able to use `super.definition()` to access that static method, then _add_ to it, in this case extending the definition to specifically reference dogs.

## Conclusion

In combination with `extends`, `super` allows a child class to access a parent's constructor from within a child's constructor. It also allows a child class to access methods and properties from a parent class, but as most of these are already inherited, this is only useful for when modifying static methods from the parent class.

### Resources

- [Inheritance in JavaScript (MDN)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)
- ["Super" and "Extends" in JavaScript ES6 — Understanding the Tough Parts (Beginner's Guide to Mobile Web Development)](https://medium.com/beginners-guide-to-mobile-web-development/super-and-extends-in-javascript-es6-understanding-the-tough-parts-6120372d3420)
- [Class Inheritance (JavaScript.info)](https://javascript.info/class-inheritance)
