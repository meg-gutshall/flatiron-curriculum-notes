---
description: 'Version 8: Module 14: Section 4: Lab'
---

# Sending Data with Fetch Lab

If you think about it, `fetch()` is a little browser in your browser. You tell `fetch()` to go to a URL by passing it an argument and it makes a network request. You chain calls to `fetch()` with `then()`. Each `then()` call takes a callback function as its argument. Based on actions in the callback function, we can display the content, update it, or inject it into the DOM.

This is a lot like browsing the web. You change the URL in the address bar, or you follow a link and those actions tell the browser to go somewhere else and get the data. Technical descriptions are as follows:

* The browser implements an HTTP GET to retrieve the content at a URL
* `fetch()` uses an HTTP GET to retrieve the content specified by a URL

The browser also provides a helpful model for understanding what _sending_ data from the browser looks like. We know that as an HTML _form_. Technically speaking, HTML forms use an HTTP POST to send content gathered in `<input>` elements to a specified URL. Another way to say this is that is that `fetch()` uses as HTTP `POST` to send content gathered in a JavaScript `Object`.

With `fetch()`, we have more detailed controle of our HTML forms; we can actually _override_ the normal behavior of an HTML form, capturing any user input, packaging it up with the appropriate request information, and sending it out.

## The JSON Server

To help us practice sending `fetch()` requests, this lab comes with a dependency called [`json-server`](https://github.com/typicode/json-server). The JSON Server allows us to start a fake RESTful API within our lab folder, giving us the ability to send both GET and POST requests and to persist and receive data.

Install it be executing `npm install -g json-server`. To start up JSON Server, run `json-server --watch db.json` in your terminal.

Once the server is running, you'll see a list of available resource paths:

```bash
Resources
  http://localhost:3000/dogs
  http://localhost:3000/cats
  http://localhost:3000/users
  http://localhost:3000/robots

Home
  http://localhost:3000/
```

These endpoints each provide different sets of data. Some example data is already present, stored in `db.json`. If the JSON server is running, you can also visit any of the above resources in a browser to see the data.

## Analyze Data Sent in an HTML Form

Let's take a look at a `<form>`:

```markup
<form action="http://localhost:300/dogs" method="POST">
  <label>Dog Name:</label><input type="text" name="dogName" id="dogName" /><br />
  <label>Dog Breed:</label><input type="text" name="dogBreed" id="dogBreed" /><br />
  <input type="submit" name="submit" id="submit value="Submit" />
</form>
```

The key components as far as sending data to the server are:

* The destination URL as defined in the `action` attribute of the `<form>` tag
* The HTTP verb to use as defined in the `method` attribute of the `<form>` tag
* The key/value data about the inputs in the fields `dogName` and `dogBreed`

We should expect that our "mini-browser" `fetch()` will need those same bits of information in order to send data to the server. Let's place this data inside our `fetch()` skeleton.

## Construct a POST Request Using `fetch()`

Sending a POST request with `fetch()` is more complicated than what we've seen up to this point. It still takes a URL in the form of a String as the first argument, but as we will see below, `fetch()` can also take a JavaScript Object as the _second_ argument. This Object can be given certain [properties](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters) with certain values in order to change the default behavior for `fetch()`.

```javascript
fetch(destinationURL, configurationObject);
```

The `configurationObject` contains three core components that are needed for standard POST requests.

### Add the HTTP Verb

So far, comparing to an HTML form, we've only got the destination URL. The next thing we need is to include the HTTP verb. By default, the verb is GET, which is why we can send simple GET requests with _only_ a destination URL. To tell `fetch()` that this is a POST request, we need to add a `method` key to our `configurationObject`:

```javascript
configurationObject = {
  method: "POST"
};
```

### Add Headers

The second piece we need to include is some _metadata_ about the actual data we want to send. This metadata is in the form of _headers_. Headers are sent just ahead of the actual data payload of our POST request. They contain information about the data being sent.

One very common header is [`"Content-Type"`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type). `"Content-Type"` is used to indicate what format the data being sent is in. With JavaScript's `fetch()`, [JSON](https://www.json.org/json-en.html) is the most common format we will be using. We want to make sure that the destination of our POST request knows this. To do this, we'll include the `"Content-Type"` header:

```javascript
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  }
};
```

Each individual header is stored as a key/value pair inside an object. This object is assigned to the `headers` key as seen above.

When sending data, the server destination URL will send back a response, often including data that the sender of the `fetch()` request might find useful. Just like `"Content-Type"` tells the destination server what type of data we're sending, it is also good practice to tell the server what data format we _accept_ in return.

To do this, we add a second header, [`"Accept"`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept), and assign it to `"application/json"` as well:

```javascript
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  }
};
```

There are many other [headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) available for particular uses. Some are used to send credentials or user authentication keys. Others are used to send cookies containing user info. `"Content-Type"` and `"Accept"` are two that we'll see the most. Servers may reject requests without the specific headers the server is configured to expect.

### Add Data

We now have the destination URL, our HTTP verb, and headers that include information about the data we're sending. The last thing to add is the _data_ itself.

Data being sent in `fetch()` must be stored in the `body` of the `configurationObject`:

```javascript
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: /* Your data goes here */
};
```

There is a catch here to be aware of: When data is exchanged between a client (your browser, for instance), and a server, the data is sent as _text_. Whatever data we're assigning to the `body` of our request needs to be a String.

### Use `JSON.stringify()` to Convert Objects to Strings

When sending data using `fetch()`, we often send multiple pieces of information in one request. In our code, we often organize this information using Objects. However, we can't just assign our Object to `body`, as it isn't a String. Instead, we convert it to JSON. Consider the following:

```javascript
// A JavaScript Object
{
  dogName: "Byron",
  dogBreed: "Poodle"
}

// JSON
"{"dogName":"Byron","dogBreed":"Poodle"}"
```

Here, using JSON has enabled us to preserve the key/value pairs of our Object within the String. When sent to a server, the server will be able to take this String and convert it back into key/value pairs in whatever language the server is written in.

Fortunately, JavaScript comes with a built-in method for converting Objects to Strings, `JSON.stringify()`. By passing an object in, `JSON.stringify()` will return a String, formatted and ready to send in our request:

```javascript
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify({
    dogName: "Byron",
    dogBreed: "Poodle"
  })
};
```

## Send the POST Request

We've got all the pieces we need, but we don't have to define everything inside of one anonymous Object. We could also write:

```javascript
let formData = {
  dogName: "Byron",
  dogBreed: "Poodle"
};

let configObj = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify(formData)
};

fetch("http://localhost:3000/dogs", configObj);
```

## Handling What Happens After

Just like when we use `fetch()` to send GET requests, we have to handle responses to `fetch()`. As mentioned before, servers will send a [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response) that might include useful information. To access this information, we use a series of calls to `then()` which are given function _callbacks_. Building on the previous implementation, we might write the following:

```javascript
let formData = {
  dogName: "Byron",
  dogBreed: "Poodle"
};

let configObj = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify(formData)
};

fetch("http://localhost:3000/dogs", configObj)
  .then(function(response) {
    return response.json();
  })
  .then(function(object) {
    console.log(object);
  });
```

Notice that the first `then()` is passed a callback function that takes in `response` as an argument. The is a `Response` object, representing what the destination server sent back to us. This Object has a built-in method, `json()`, that converts the _body_ of the response from JSON to a plain old JavaScript object. The result of `json()` us returned and made available in the _second_ `then()`. In this example, whatever `response.json()` returns will be logged in `console.log(object)`.

Sending the example above to our JSON server, once the request is successfully resolved, we would see the following log:

```javascript
{dogName: "Byron", dogBreed: "Poodle", id: 6}
```

The JSON server is sending back the data we sent, along with a new piece of data, an `id`, created by the server.

### When Thing Go Wrong: Using `catch()`

When something goes wrong in a `fetch()` request, JavaScript will look down the chain of `.then()` calls for something very similar to a `then()` called a `catch()`.

When something goes wrong in a `fetch()`, the next `catch()` is called so that error work can be performed. By including a `catch()` statement, JavaScript doesn't fail silently:

```javascript
let formData = {
  dogName: "Byron",
  dogBreed: "Poodle"
};

let configObj = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify(formData)
};

fetch("http://localhost:3000/dogs", configObj)
  .then(function(response) {
    return response.json();
  })
  .then(function(object) {
    console.log(object);
  })
  .catch(function(error) {
    alert("Bad things! Ragnarõk!");
    console.log(error.message);
  });
```

Sent to our JSON server from a page like `index.html`, we would receive an alert window pop-up and logged message:

```bash
Failed to execute 'fetch' on 'Window': Request with GET/HEAD method cannot have body.
```

While `catch()` may not stop _all_ silent errors, it is useful to have as a way to gracefully handle unexpected results. We can use it, for instance, to display a message in the DOM for a user, rather than leave them with nothing.

## Conclusion

You can now use `fetch()`, the browser inside your browser's JavaScript environment, to both:

* Read data using HTTP GET (whose response you can put in the DOM)
* Send data using HTTP POST (whose response you can put in the DOM)

With this, we're ready to stitch server updates (reads **and** updates) with DOM updating and event handling.
