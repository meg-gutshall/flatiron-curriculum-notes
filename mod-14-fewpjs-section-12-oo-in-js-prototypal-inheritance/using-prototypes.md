---
description: 'Version 8: Module 14: Section 12: Lesson'
---

# Using Prototypes (OOJS)

```javascript
function User(name, email) {
  this.name = name;
  this.email = email;
  this.sayHello = function() {
    console.log(`Hello everybody, my name is ${this.name} whom you've been mailing at ${this.email}!`);
  };
}

let lauren = new User("Lauren", "lauren@example.com");
lauren.sayHello();
//=> Hello everybody, my name is Lauren whom you've been mailing at lauren@example.com!
```

Given the code above, let's assume the following:

* The `name` property costs 32 bytes of space
* The `email` property costs 32 bytes of space
* The function costs 64 bytes of space

That means, to create our `lauren` instance, we pay a cost of 128 bytes (32 + 32 + 64 = 128)! If we want to create a million `User` instances, that would add up to 128 million bytes of space! While memory and disk space are constantly growing larger and cheaper, we'd like to be efficient whenever possible.

The key to gaining efficiency is the _prototype_.

## Identify Inefficiency in Constructor Function Object Orientation

In our example, the `name` and `email` properties vary, so we can't economize there. However, the method `sayHello()` is the same in every instance: "in my current context, return a template string with this current context's values."

We want to tell al instances of `User` that they have a shared place to find methods. That place is called the "prototype."

## Recognize the Prototype as a Means for Reducing Inefficiency

We access the prototype of a constructor function by typing the constructor function's name, and adding the attribute `.prototype`. So for `User` it's `User.prototype`. Attributes that point to functions in the JavaScript `Object` will be shared to all instances made by that constructor function:

```javascript
function User(name, email) {
  this.name = name;
  this.email = email;
}

User.prototype.sayHello = function() {
  console.log(`Hello everybody, my name is ${this.name}!`);
};

let sarah = new User("Sarah", "sarah@example.com");
let lauren = new User("Lauren", "lauren@example.com");

sarah.sayHello();
//=> Hello everybody, my name is Sarah!
lauren.sayHello();
//=> Hello everybody, my name is Lauren!
```

The prototype is just a JavaScript `Object`:

```javascript
User.prototype;
//=> { sayHello: ƒ, constructor: ƒ }
typeof User.prototype;
//=> "object"
```

To prove the efficiency of sharing methods via prototype:

```javascript
lauren.sayHello === sarah.sayHello;
//=> true
```

## Conclusion

The constructor prototype can be used to share functionality between instances.
