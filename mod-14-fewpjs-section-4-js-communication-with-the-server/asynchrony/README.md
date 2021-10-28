---
description: 'Version 8: Module 14: Section 4: Lesson'
---

# Asynchrony

Browsers use an _asynchronous_ execution model, or "they do little bits of lots of tasks until the tasks are done."

## A Synchronous Code Block

So far in JavaScript, we've written _synchronous_ code and the execution model didn't matter.

```javascript
let sum = 1 + 1; // Line 1
let lis = document.querySelectorAll("li"); // Line 2
```

In this case, when we hit the definition of `sum`, this work doesn't rely on any "questionable" or "unknowably long" process. As soon as the work of Line 1 is done, JavaScript will then go to work finding elements and assigning them to `lis` in Line 2.

But let's consider a "blocking" operation. Imagine we had a synchronous function called `synchronousFetch("URL STRING")` that fetches data from the network.

```javascript
let tooMuchData = synchronousFetch("https://genome.example.com/..."); // Line 1
let lis = document.querySelectorAll("li"); // Line 2
console.log(tooMuchData);
```

That work in Line 1 could take a long time (e.g. slow network), or might fail (e.g. failed login), or might retrieve a _**huge**_ amount of data (e.g. The Human Genome).

It's possible that the `let lis` in Line 2 _will never execute_! While JavaScript is executing `synchronousFetch` it will appear "locked up."

## An Asynchronous Code Block

Asynchronous code in JavaScript looks a lot like event handlers. And if we think about it, that makes sense. You tell JavaScript:

> Hey, do this thing _and then_ go do whatever maintenance you need, but when that first thing has an "I'm done" event, go **back** to it and do some work that I defined in a function when I called it.

Let's imagine a function called `asynchronousFetch` that takes as arguments:

1. A URL String
2. An arrow function that will have the fetched data passed into it as its first arguments when the `asynchronousFetch` work is done

```javascript
asynchronousFetch("https://genome.example.com/...", tonOfGeneticData => sequenceClone(tonOfGeneticData)); // Line 1
let lis = document.querySelectorAll("li"); // Line 2
```

In this case, JavaScript _starts_ the `asynchronousFetch` in Line 1, and then sets `lis` in Line 2. Some time later, the fetch of data finishes and _that_ data is passed into the "callback" function as `tonOfGeneticData` back on Line 1.

Most asynchronous functions in JavaScript have this quality of "being passed a callback function." It's a helpful tool for spotting asynchronous code "in the wild."

## Conclusion

JavaScript in the browser has an asynchronous execution model. This fact has little impact when you're writing simple code, but when you start doing work that might block the browser, you'll need to leverage asynchronous functions. Remember, these functions can be surprising and nearly every JavaScript developer sooner or later forgets to reckon with asynchrony.

While working asynchronously can be a bit of a headache for developers, it allows JavaScript to do other work whenever it has the opportunity. Important methods which require us to think asynchronously are `setTimeout()` and `fetch()`, among others.
