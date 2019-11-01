# JavaScript Document Onload

An important part of working with JavaScript is ensuring that your code runs at the right time. Every now and then, you may have to run some extra code to ensure you code doesn't run before the page is ready. There are many factors that go into determining the "right time." There are two events that represent two important milestones in terms of page load:

1. The `DOMContentLoaded` event fires when your page's DOM is fully parsed
2. The `load` event fires when a resource and its dependent resources (CSS, JavaScript) have finished loading

## Why Is `DOMContentLoaded` Important?

The `DOMContentLoaded` event is the browser's built-in way to indicate when a page is loaded. It isn't possible to manipulate HTML elements that haven't rendered yet, so trying to manipulate the DOM before the page fully loads can potentially lead to problems.

We need to make sure to wait until _after_ the `DOMContentLoaded` event is trigged to safely execute our code. By creating an event listener, we can keep our code from immediately firing when `index.js` is loaded.

## Set Up an Event Listener for `DOMContentLoaded`

As always, `addEventListener` takes a `String` with the name of the event and a callback function.

```javascript
document.addEventListener("DOMContentLoaded", function() {
  console.log("The DOM has loaded");
});
```

## `DOMContentLoaded` Does Not Wait for Stylesheets and Images to Load

It is important to note that the `DOMContentLoaded` event fires once the initial HTML document finishes loading, but does not wait for CSS or images to load. In situations where you need _everything_ to completely load, use the `load` event instead.

While both will work, it is often the case that we only need the HTML content to fully load in order to execute our JavaScript. Since images can take some time to load, using the `load` event means visitors of a web page may see your web pages in its original state for a couple of seconds before any JavaScript fires and updates the DOM.

For a comparison of the difference between `DOMContentLoaded` and `loaded` events, [check out this example](http://web.archive.org/web/20150405114023/http://ie.microsoft.com/testdrive/HTML5/DOMContentLoaded/Default.html).

## Conclusion

JavaScript provides us the powerful ability to update web page content **without** refreshing the browser. We can now have a page with some basic HTML structure and use JavaScript to fill in the content, enabling the possibility of dynamic web pages.

Keep in mind, this sort of action will only work if the HTML content is actually loaded on the page. The `DOMContentLoaded` event ensures that our JavaScript code is being executed immediately after the HTML is finished loading.

## Addendum

The `DOMContentLoaded` event is now a widely accepted standard. However, modern web development provides us with additional choices for setting up when we want our JavaScript to execute. For example, HTML5 now has a [`defer`](https://www.w3schools.com/tags/att_script_defer.asp) attribute for use in `<script>` tags:

```html
<script src="index.js" defer></script>
```

This functions in a similar way to `DOMContentLoaded`. The JavaScript code stored in `index.js` will be loaded up but won't execute until the HTML page completely loads.

## Resources

- [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/API/Window/DOMContentLoaded_event)
- [Running Your Code at the Right Time](https://www.kirupa.com/html5/running_your_code_at_the_right_time.htm)
