# Lesson: Communicating with the Server

## The Process of Communicating with the Server

In our Simple Liker app example, "favoriting" is a click event on a hear icon that updates the user's DOM to show a full heart.

This event kicks off a sequence of actions to notify the server, so that the original poster can be notified that you favorited it. JavaScript needs to send a message to the server when the `click` event runs, and the server needs to indicate success so that the DOM can update accordingly.

The user doesn't see this entire process happening. Ideally, the process moves quickly enough that the user barely even notices that it's taken place. All they know is that the little heart icon is now reflecting their clicked appreciation. To keep the user experience fast and smooth, we use something called the _AJAX technique_.

## What Is AJAX?

_AJAX_ is the shortened version of "asynchronous JavaScript and XML," and it's the general way we make requests to the server without reloading the web page, and then work with data we receive from the server. We give the user HTML and CSS first, then JavaScript, behind the scenes, fills in the rest of the action we want the page to offer. There are a few different ways to do this technically, and next we'll take a look at one of the most efficient ways: `fetch()`.

The data that comes back from the server is not sent in HTML. While (once) sent back in XML, it's now most often sent back in a format known as JSON. JavaScript Object Notation (JSON) is a `String` that JavaScript knows how to turn into an `Object`.

## Conclusion

The last skill we need to be effective JavaScript web developers is communication with the server, which links together what we've learned about how to manipulate the DOM and how to work with events. With the AJAX technique, we'll learn how to send and receive data quickly so that we keep our users' experience a positive one.
