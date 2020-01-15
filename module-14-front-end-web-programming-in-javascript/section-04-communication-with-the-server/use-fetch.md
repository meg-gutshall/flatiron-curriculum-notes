# Lesson: Use Fetch

Browsers won't show anything until they've processed all of their received data. To speed up this process as well as provide other great features, we use a technique called AJAX.

In AJAX we:

1. Deliver an initial, engaging page using HTML and CSS which browsers render _quickly_
2. _Then_ we use JavaScript to add more to the DOM, behind the scenes

AJAX relies on several technologies:

- Something called a `Promise`
- Something called a `XMLHttpRequestObject`
- A [serialization format](https://en.wikipedia.org/wiki/Serialization) called JSON (JavaScript Object Notation)
- [Asynchronous Input/Output](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)
- [The event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

Part of what makes AJAX complicated to learn is that to understand it _thoroughly_, you need to understand _all_ these components. It just so happens that modern browsers have _abstracted_ all those components into a single function called `fetch()`. Let's learn to use `fetch()` to apply the AJAX technique: a way to load additional data _after_ information is presented to the user.

## Explain How to Fetch Data with `fetch()`

The `fetch()` function retrieves data. It's a global _method_ on the `window` object. That means you can simply use it with `fetch()` in DevTools.

Here's the skeleton for using `fetch()`:

```js
fetch("string representing a URL to a data source")
  .then(function(response) {
    return response.json();
  })
  .then(function(json) {
    // Use this data inside of `json` to do DOM manipulation
  })
```

### `fetch()` Step-By-Step

The function above returns an object that represents what the data source sent back. It does **not** return the actual content.

We have to call the `then()` method on the object that comes back. The argument of `then()` is a function that receives the response as its argument.

Inside of the function, we do whatever processing we need, but at the end, we **have to return** the content that we've gotten out of the response.

The response has some basic functions on it for the most common data types. The most important ones are `.json()` and `.text()`.

This callback function is usually only one line: returning the content from the response. What we return from this function will be used in the _next_ `then()` function.

Then next `then()` function returns the content from the response. We can use that content inside of the callback function that's passed into the _next_ `then()` function.

Finally, we can use the data inside of `json` to do DOM manipulation.

### Fleshing Out Our Skeleton

First, we'll provide a `String` argument to `fetch()`. JSON is a way to send a collection of data across the Internet. It just so happens that this `String` is written in a way that would be valid JavaScript syntax for an `Object` instance. Thus, the name "JavaScript Object" notation, or JSON.

The `then()` take a function. Here is wear you tell JavaScript to ask the network response to be turned into JSON. When you first start using `fetch()` most of your first `then()` methods are going to look like this:

```js
function(response) {
  return response.json();
}
```

Then final `then()` is when you actually get some JSON passed in. You can then do something with the JSON. The easiest options are:

- `alert()` the JSON
- `console.log()` the JSON
- hand the JSON off to another function

Here's a completed example:

```js
fetch("http://api.open-notify.org/astros.json")
  .then(function(response) {
    return response.json();
  })
  .then(function(json) {
    console.log(json)
  });
```

## Working Around Backwards Compatibility Issues

`fetch()` has only recently arrived in browsers. Older code may use `jquery.ajax`, `$.ajax`, or an object called an `XMLHttpRequestObject`. These are considered legacy code.

## Examples of the AJAX Technique on Popular Websites

The AJAX technique opens up a lot of uses!

1. It allows us to pull in dynamic content. The same "framing" HTML page remains on screen for a cooking website. The recipe on display updates _without_ page load. This approach with pioneered by GMail whose navigation area is swapped for mail content swiftly—thanks to AJAX!
2. It allows us to get data from multiple sources. We could make a website that displays the current weather forecast and the current price of bitcoin side by side. This approach is used by most sites to render ads. Your content loads while JavaScript gets the ad to show and injects it into your page (sometimes AJAX can be used in a way that we don't _entirely_ like).

## Conclusion

Many pages use AJAX to provide users fast and engaging sites. It's certainly not required in all sites. Using it for every site is a step backward when simple HTML would suffice. However, as sites have more and more material, the AJAX technique is a great tool to have.

Using `fetch()`, we can include requests for data wherever we need to in our code. We can `fetch()` data on the click of a button or the expansion of an accordion display. There are many older methods for fetching data, but `fetch()` is the future.

### Resources

- [Fetch API (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
