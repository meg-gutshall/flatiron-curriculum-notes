# Lesson: Constructor Functions (Object-Oriented JavaScript)

JavaScript is sometimes a bit confusing. It has a native type `Object`. How does that relate to object orientation and how does the desire to avoid repeating ourselves relate to them both?

## Create a Constructor Function

It's sometimes handy to represent data with objects, which give us key/value pairs. For example, we may represent a user as the following:

```js
const bobby = { name: "Bobby", age: 20, hometown: "Philly" }
```

Now imagine that we had a couple of users:

```js
const bobby = {
  name: "Bobby",
  age: 20,
  hometown: "Philly"
}

const susan = {
  name: "Susan",
  age: 28,
  hometown: "Boston"
}
```

Note, that with both objects sharing exactly the same keys, and only the values differing, we are [_repeating ourselves_](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). We would like a mechanism to construct objects with the same attributes (that is, keys), while assigning different values to those keys. The name for what kind of function does this varies across many popular programming languages, but we'll call it a **factory function** because it spits out new instances:

```js
function User(name, age, hometown) {
  return {
    name,
    age,
    hometown
    // Don't forget ES6 powertools --> this is the same as `name: name`
  }
}

let byronPoodle = User("Karbit's Byron By the Bay", 5, "Manhattan");
byronPoodle.age;
//=> 5
```

Interestingly, `typeof` confirms `byronPoodle` is an `Object`:

```js
typeof byronPoodle;
//=> "object"
```

However, something's not quite as clear as we might like it to be. If we ask `byronPoodle` what made it, the answer is...

```js
byronPoodle.constructor;
//=> [Function: Object]
```

`byronPoodle` is certainly an `Object`, but it's more specific than that: it's a `User`. We'd really like for this special kind of object to be reflected when we ask it what it is. We'd like for a mystical process to come along and say, "You are not merely an `Object`, you are a `User` or a `Dog`." We tell JavaScript to bless the thing created by the constructor function into being something more specific than `Object` by using the keyword `new`. Using `new` requires that we evolve our _factory function_ into a _constructor function_. It's the same idea, but with a few subtle additions.

## Explain What `new` Is and How It Works with the Constructor Function

Let's create a _constructor function_. Constructor functions must be paired with the `new` keyword:

```js
function User(name, email) {
  this.name = name;
  this.email = email;
}
```

What's `this` here? It refers to the function's context. Since functions in JavaScript are also objects, a function can say "on me, set a property." What we ultimately want to do is say something like, "Hey constructor function! When you run, create a new copy of yourself, leaving the original unchanged, and on that _particular copy_, set the properties based on the arguments passed into the function." The keyword `new` tells the constructor function to do exactly that.

We just need to put the two together like so:

```js
function User(name, email) {
  this.name = name;
  this.email = email;
}

let lauren = new User("Lauren", "lauren@example.com");
lauren.name;
//=> "Lauren"
```

What's happening here hinges on the `new` keyword. When we invoke the function with `new` before it, you can picture an imaginary JavaScript `Object` being copied for use in the `User` function. The constructor function **is not changed**; the freshly-created, new context **is** changed.

Here's the above code again, but with comments per JavaScript's execution phase:

```js
function User(name, email) {
  this.name = name;     // 2. Set the new context's property name to the argument that was passed into the first parameter (name).
  this.email = email;   // 3. Set the new context's property name to the argument that was passed into the second parameter (email).
}

// 1. Create a new context (what `new` does) and use that new context inside of the execution of the `User()` function while passing in the arguments "Lauren" and "lauren@example.com".

let lauren = new User("Lauren", "lauren@example.com");    // 4. Assign the new context's newly-created object to the variable `lauren`.
lauren.name;    // 5. Ask the new context for the value stored in its `.name` property.
//=> "Lauren"
```

You can ask interesting questions about the `lauren` variable. Building on the previous code:

```js
typeof lauren;
//=> "object"

lauren.constructor;
//=> [Function: User]
```

This makes sense: the function that constructed `lauren`, or the `constructor`, is `User`. The instance `lauren` is an `Object`.

Since we know one object-oriented pattern, we might be wondering how to add methods to the `User` instances. It should be obvious that if we can set a property to point to a value like `"Lauren"` or `"lauren@example.com"`, we should be able to set an anonymous function to a property. That function would have access to the `this` context created when the instance was created:

```js
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

## Conclusion

There is one problem with creating the constructor function and using the `new` keyword in a factory: it's incredibly memory inefficient.
