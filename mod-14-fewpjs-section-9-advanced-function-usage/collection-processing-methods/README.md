---
description: 'Version 8: Module 14: Section 9: Lesson'
---

# Collection Processing Methods (JS Advanced Functions)

As programmers, we wonder about the world, come up with questions, and then ask a computer to help us manipulate data to find answers. Many of those questions can be resolved by "polling" every member in a collection. We'd typically "poll" each number in the collection and feed that value to a calculation _or_ aggregate that value into a running value (like a total).

The questions involve:

1. Finding a collection of data, typically stored in an array or object
2. Visiting each element (array) or pair (object) in the collection
3. Doing some "work" with that element or pair
4. Returning a new collection **or** a new value based on the "work" that touched that element

When we say "work," we mean the evaluation of some expression that uses the "current element." In JavaScript, you guessed it, that "work" is stored in a function definition—be it a function declaration, a function expression, or a function returned by invoking another function.

"Collection-processing method" is what we call a method provided by JavaScript that:

1. "Visits" each element or pair in a collection
2. Tests those elements or pairs with "work"
3. Returns a new collection **or** a value

Methods that behave in this way we'll say have the "Character of Collection Processing."

**NOTE:** In Ruby, all the methods that behave like this are called "Enumerable." There's no official collective term for methods that do this "polling each member" operation. "Collection-processing methods" isn't a hard-and-fast term that programmers use in daily practice, but all JavaScript programmers know that there's something similar to the methods we're about to introduce, so nobody would look at you too strangely for speaking of "JavaScript's collection methods."

## Consult JavaScript's Collection-Processing Method Documentation

JavaScript provides us _lots_ of collection-processing methods. You can find them listed in the [Array reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array) documentation at MDN.

We'll demonstrate two of the most important collection-processing methods, but you should familiarize yourself with others. Since they all follow the same _character_, once you learn one or two, the rest will be easy.

### Enumeration Versus Collection-Processing Methods

The trouble comes in when we talk about _coding_ with JavaScript's collection-processing methods. Specifically, the code can get confusing when we need to _abstract_ out the "work" that we should apply to each element. To feel truly comfortable with Enumerable methods, we have to understand the challenging coding ideas of:

* Capturing work (but not _doing_ it) using (anonymous) functions.
* Doing the work and passing it arguments based on visiting each element or pair in the collection. This is called invoking the method. As a surprising monkey-wrench that causes tons of bugs, we'll need to reckon with JavaScript's "execution context" when we do the work.
* Gathering a new collection **or** combining the individual results into an aggregate result.

## Conclusion

A wide number of problems have a solution that involves following the "character of collection processing." Process a collection by visiting each element and do "work" on it in order to return a new collection **or** aggregate value. Understanding collection processing in the big picture is the first step to understanding collection-processing methods.
