---
description: 'Version 8: Module 14: Section 2: Lesson'
---

# Calling Methods (JS Fundamentals)

## Defining a JavaScript Method

Let's consider the `document.querySelector` method. This code _calls_ the _method_ `querySelector`. The method is said to be "defined in" the object `document`.

_Calling_ is the same as _running_. We do that when we write:

```javascript
document.querySelector(); // Notice the addition of ()
```

When we _call_ `document.querySelector()`, we provide it an [_argument_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments), a bit of text, a `String` that goes inside the `()`. The method `document.querySelector()` expects us to provide a CSS identifier that will help us find the node we want as an _argument_. If the `document` object finds an `HTMLElement` in its representation of the page, it _returns_ it. Otherwise the methos returns `null`.

The thing `document.querySelector()` return is _also_ an object. It too has both information and methods, state and behavior, properties and methods (they all mean the same thing). This `HTMLElement` [_instance_](https://developer.mozilla.org/en-US/docs/Glossary/Instance) has methods like `remove()`.

## Conclusion

JavaScript methods are actions that can be performed on objects. Objects have many useful methods that help us modify and iterate through them. The DOM selection method `document.querySelector()` is a powerful tool for finding elements needed to make updates and changes to the DOM using methods like `remove()`.

## Resources

* [JavaScript Object Methods (W3 Schools)](https://www.w3schools.com/js/js\_object\_methods.asp)
