# Lesson: Object Assign

In JavaScript, we have access to a global `Object` that comes with several helpful methods ready for us to use. One of these methods is `Object.assign()`, which allows us to combine properties from multiple objects into a single object.

## Identify `Object.assign()`

The first argument passed to `Object.assign()` is the first object into which all properties are merged. Every additional argument is an object whose properties we want to merge into the first object:

```js
Object.assign(firstObject, secondObject, thirdObject, ...);
```

The return value of `Object.assign()` is the first object after all of the additional objects' properties have been merged in:

```js
Object.assign({ eggs: 3 }, { flour: '1 cup' });
//=> { eggs: 3, flour: "1 cup" }

Object.assign({ eggs: 3 }, { chocolateChips: '1 cup', flour: '2 cups' }, { flour: '1/2 cup' });
//=> { eggs: 3, chocolateChips: "1 cup", flour: "1/2 cup" }
```

Let's look at the `flour` property in the above example. **If multiple objects have a property with the same key, the last key to be defined wins out.** Essentially, the last call to `Object.assign()` in the above snippet is wrapping all of the following assignments into a single line of code:

```js
const recipe = { eggs: 3 };

recipe.chocolateChips = '1 cup';

recipe.flour = '2 cups';

recipe.flour = '1/2 cup';
```

## Non-Destructively Assign New Data with `Object.assign()`

A common pattern for `Object.assign()` is to provide an empty object as the first argument. That way we're providing an entirely new object instead of modifying or overwriting the properties of an existing object.

```js
function nondestructivelyUpdateObject(obj, key, value) {
  return Object.assign({}, obj, { [key]: value });
};

const recipe = { eggs: 3 };

const newRecipe = nondestructivelyUpdateObject(recipe, 'chocolate', '1 cup');
//=> { eggs: 3, chocolate: "1 cup" }

newRecipe;
//=> { eggs: 3, chocolate: "1 cup" }

recipe;
//=> { eggs: 3 }
```

In other languages (like Ruby), this behavior is called "merging." You take an original base object (maybe with some typical "standard" attribute/value pairs already set), and then you "merge" in additional object(s).

It's important that we merge everything into a new, empty object. Otherwise, we would be modifying the original object, which would be destructive behavior.

## Non-Destructive Updates == Performance Gains

Doing non-destructive updates (i.e. "creating new things and merging on top") is a really important pattern. It turns out that, in many places, non-destructive updates are _more performant_. The main reason on this is when you add something to an existing object, the computer has to make sure that the object has enough room to add what you're saying to add. If it doesn't, the computer needs to do cleanup work, find some more space, copy the old thing over, add the new thing, and then resume work, etc. That "accounting" process is actually quite slow.

`Object.assign()`, however, avoids all that and says: "Hey, I created a thing that looks like this, give me space for it!" This is faster.

Furthermore, in the cloud-based world of programming we're moving more and more to, we can't be sure that two computers will share the same memory. They might be servers separated be centimeters or kilometers. When a design like this is used, we'll need to make sure the functions have "all they need" to run a function call _independently_ (i.e. they have their own copy of the data they need and aren't sharing memory with other machines).

## Conclusion

Depending on how you use it, `Object.assign()` can be useful in both destructive and non-destructive ways.

### Resources

- [`Object.assign() (MDN)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
