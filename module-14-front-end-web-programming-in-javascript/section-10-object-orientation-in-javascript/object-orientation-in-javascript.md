# Lesson: Object Orientation in JavaScript

So far in JavaScript, we've discussed the "Three Pillars of Web Programming," **recognizing JavaScript events**, **manipulating the DOM**, and **communicating with the server**, and we saw how these pillars are incorporated into web applications.

The process we've learned so far has been:

1. An HTML page renders on the screen
2. JavaScript is executed when the page loads
3. In the JavaScript, event listeners are created pointing to 'free-standing' function, listed out in the JavaScript file

In that process, we have three primary takeaways:

- Some of these functions handle DOM manipulation
- Some functions handle server communication
- Still other functions may serve as 'helper' functions to others

These functions can be invoked in whatever order we set, or from within each other. This setup works great when just getting off the ground; with a handful of functions, we can get an interactive website up and running. What happens though when we want to go beyond a small website?

**The more complicated our code gets, the harder it is to understand and change it.**

In larger applications, we might be dealing with hundreds of functions, DOM elements, and events, all tied together, forming a web of relationships. It becomes increasingly difficult to follow the flow of actions in your code as more and more functions are introduced. Changes to one function may have unforeseen affects on functions _'downstream'_.

This web of dependent, free-standing functions can be improved with organization. We do things like group functions together, arrange code in a readable way. Our options, however, are still limited—it's a big web!

Let's take a look at an alternative way to structure our code called object orientation. By understanding and using object orientation, we can _design_ our code to be easier to read, understand, and change.

## Define Object Orientation

With object orientation, instead of a web, we can think of our code as a collection of _cells_. These cells are separated from each other and can contain _information_ bits of data (like variables) as well as _behaviors_ (like functions) directly related to that data.

Consider what we know so far: any sort of data we had to store and manipulate has been either stored in variables or passed to functions as arguments, like so:

```js
let name = "Evan";
let age = 34;

function sayHello(nameOfPerson) {
  console.log(`Hello, my name is ${nameOfPerson}.`);
};

function sayAge(age) {
  console.log(`I am ${age} years old.`);
};

function haveBirthday(age) {
  return age + 1;
};

sayHello(name);
//=> Hello, my name is Evan.
sayAge(age);
//=> I am 34 years old.
age = haveBirthday(age);
sayAge(age);
//=> I am 35 years old.
```

Here, we've got some data, a string and an integer assigned variables, and a few functions for using and reading that data. The functions and data are closely related. Combined, they convey information about a _person_. While we, as human beings, might be able to interpret the above code as all related, as far as code structure, **there isn't anything structurally that actually _encodes_ those relationships**. The _names_ of our functions and variables are the only indicators that they are related.

Object orientation grants us the ability to write code that **structurally** establishes the relationships between data and functions. If we rewrite our first code snippet applying object orientation, we could write something like this:

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  };

  sayHello() {
    console.log(`Hello, my name is ${this.name}.`);
  };

  sayAge() {
    console.log(`I am ${this.age} years old.`);
  };

  haveBirthday(age) {
    console.log("It's my birthday!");
    this.age += 1;
  };
};

let evan = new Person("Evan", 34);

evan.sayHello();
//=> Hello, my name is Evan.
evan.sayAge();
//=> I am 34 years old.
evan.haveBirthday();
//=> It's my birthday.
evan.sayAge();
//=> I am 35 years old.
evan;
//=> Person { name: "Evan", age: 35 }
```

Where did our variables go? Now we just have one: `evan`. Instead of being assigned to a data type like a string or and integer, `evan` is assigned to a `Person` object that _contains_ our data.

This `Person` object is a `class`, the fundamental structure underlying all object-oriented code in JavaScript. The line:

```js
let evan = new Person("Evan", 34);
```

...initializes a copy, a single **_instance_** of the `Person` class. Two arguments are passed in (`"Evan"` and `34`), and the resulting instance is assigned to a variable.

The instance we just created contains the functions that were previously free-standing, `sayHello`, `sayAge`, and `haveBirthday`. Notice here that we're no longer passing data as arguments to these functions when we call them.

>For clarity, functions that are contained within a `class` or `class` instance are referred to as 'methods.' The word _'function'_ is used when referring to functions outside of any `class` object.

Instead of receiving arguments, our _methods_ have access to the data as `this.name` and `this.age`! These are referred to as _properties_, and are both assigned when a new instance of the `Person` class is created.

With our data and _methods_ captured in the `Person` instance, we've **_encapsulated_** all the information and behaviors that represent a _person_ in our code!

## The Benefits of Object Orientation

The end result of our code example hasn't changed—we are still able to perform the same actions with minor modifications. However, by designing and creating classes like this, we can gain some important benefits:

### Easier to Change

If we want to add more code related to a _person_, instead of just adding it in to a long list of functions, we now have a clear, logical place to put it. This makes it easier to extend code, and encourages good organization in the future.

### Offers Better Data Control

By encapsulating our data in a class, we can protect that data from unexpected changes. When using local variables like `let name = "Evan"`, the variable is vulnerable to change from any function. Functions, meanwhile, will do what they are programmed to do, regardless of the data they are given. They are oblivious.

```js
function sayHello(nameOfPerson) {
  console.log(`Hello, my name is ${nameOfPerson}.`);
};

sayHello([23, "Golden Apple"]);
//=> Hello, my name is 23,Golden Apple.
```

In a class, however, we can design out code so that methods with a specific purpose only interact with and change the data they are supposed to. We don't need a stand alone `sayHello` function that takes in any argument and tries to log it, we just need it for saying a particular person's name.

```js
let sarah = new Person("Sarah", 31);
sarah.sayHello();
//=> Hello, my name is Sarah.
```

Equally, using a class to encapsulate our data allows us to be specific in how that data is used. The `sarah` variable in the code snippet above points to an entire _instance_ of the `Person` class. Wherever `sarah` goes, `sarah` will always carry its properties and methods with it. If we need to access data stored on the instance, we can get property values directly:

```js
sarah.name;
//=> "Sarah"
```

Or use the built-in methods _we've_ defined to access the information however we choose:

```js
sarah.sayAge();
//=> I am 31 years old.
```

### Easy to Replicate

Every time we initialize a new instance of the `Person` class, we create a unique object:

```js
let sarah = new Person("Sarah", 31);
let evan = new Person("Evan", 34);
```

Since each instance of `Person` has unique data, our instance methods will behave accordingly and only use _their_ data:

```js
evan.sayHello();
//=> Hello, my name is Evan.
sarah.sayHello();
//=> Hello, my name is Sarah.
```

This turns out to be a fantastic help when dealing with many collections of similar data. For example, comments on a blog post—while the data is unique to each, comments should always "behave" the same way and all display the same way on the page. With object orientation, we can write a `Comment` class and create an "instance" for each unique comment.

Once we establish the data and methods for a class, we can create as many copies as we need.

### Improves Understanding by Adding Meaning

By encapsulating related information and behavior, we have organized our code in a more meaningful way. It _makes sense_ to us as humans to group related things like this. Object orientation works well for representing real world systems and relationships in code, which makes it easier to comprehend.

```js
let sarah = new Person("Sarah", 31);
let evan = new Person("Evan", 34);
let restaurant = new Restaurant("La Villa", "261 5th Avenue, Brooklyn, NY");

evan.sayHello();
//=> Hello, my name is Evan.
sarah.sayHello();
//=> Hello, my name is Sarah.

restaurant.addGuest(evan);
restaurant.addGuest(sarah);
restaurant.serveGuest(evan, new Drink("Water"));
restaurant.serveGuest(sarah, new Drink("Water"));

evan.saySmallTalk();
//=> How about this weather?
```

All classes are structured in a consistent way, so even though we don't know the details of the `Restaurant` class, we can still infer how the `Restaurant`, `Person`, and `Drink` classes might interact.

Many systems of interrelated things can be represented as objects interacting with one another, and being able to visualize these relationships helps when designing complex applications. Even the more abstract concepts of web programming can be easier to understand using object orientation, though it takes some practice to think in the object-oriented mindset.

## Conclusion

Object orientation can fundamentally change the way we design our code, but as we explore, we will see how proper design encourages code that is easier to use, understand, change, and maintain.

### Resources

- [Object-oriented JavaScript for Beginners (MDN)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS)
