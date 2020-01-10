# Events and Functions Intro

So far, we've used code like:

```js
const input = document.getElementById("input");
input.addEventListener("click", function(event)) {
  alert("I was clicked!");
});
```

to find DOM elements and attach event listeners to them.

Now we'll dig deeper into JavaScript functions—the part of the code that looks like:

```js
function(event) {
  alert("I was clicked!");
}
```

JavaScript's functions work differently from other languages. Understanding their _syntax_ (what the code look like) and _semantics_ (what the code means) is critical to writing event-based code. We'll cover:

- functions as "first class" data
- function scope
- hoisting

First, we'll use functions to "wrap up" the behavior that should happen when an event fires. Later, we'll see that functions are used to wrap up and name any behavior or code that we'd like to reuse.
