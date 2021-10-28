---
description: 'Version 8: Module 14: Section 4: Lab'
---

# Fetch Lab

## What's an API?

An API, or application programming interface, is a manner in which companies and organizations expose their data and/or functionality to the public for use. APIs allow us to add important data and functionality to the applications we build. You can think of an API as one way in which data is exposed to us developers for use in our own programs.

Just like we can use JavaScript to send a web request for a web page that is written in HTML, and receive a response that is full of HTML, we can use JavaScript to send a web request to an API and receive a collection of JSON in return.

## What's JSON?

JSON is a language-agnostic way of formatting data. If we send a web request to an API, it will return to us a JSON collection of data. With just one easy line of code, we can tell JavaScript to treat that JSON as a nested `Object`. In this way, large and complicated amounts of data can be shared across platforms.

## Game of Thrones Example

Getting data from the [Game of Thrones API](https://anapioficeandfire.com) with `fetch()` is a pretty easy process. If we're just trying to `GET` some JSON, we can add the following code to our JavaScript console in the browser:

```javascript
fetch("https://anapioficeandfire.com/api/books")
  .then(resp => resp.json())
  .then(json => console.log(json));
```

Remember that we can use the `json()` method of the `Body` mixin to render the API's response as JSON. We then pass the arrow function's result to the _next_ `then()`. Thus in the second `then()`, we receive a JSON `String` that, when we pass it to `console.log()`, prints a JavaScript object to our console.

Then response from the API contains all ten books currently existing in the Game of Thrones series, in JSON format.

APIs have many different variations and can be as customizable as the developer wants them to be. If you're really lucky, there will be robust documentation to go along with the API to help you out and give you a road map to help you figure out how to format your request for information.
