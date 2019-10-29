# JavaScript Eventing

Most web apps are _not_ used by people editing the DOM. Instead, people _do something_ and then _work happens_. "Doing work" in response to "something happening" is known as _event handling_. _Events_ are the "something that happens" and the "_callback function_" is the work that will happen in response to the event being triggered. When JavaScript recognizes an event that applies to an "event handler" that has been set up, it will execute that "handler's" work, which is stored in a _callback function_. For now, we'll focus on the first half of that relationship: the event.

## What Is a JavaScript Event?

JavaScript has the ability to "listen" for things that happen inside the browser. It can listen for events like whether the browser resized, or whether someone clicked on a specific image on the screen. The Event you're probably most familiar with is "click."

Here's a few common types of events:

### Mouse Click

The mouse/trackpad is a primary pointing device when working with browsers. In response to click, double-click, right-click, etc. we can do work like, changing the background of the document to a random color every time someone clicks on the page.

### Key Press

While click events make up the majority of event's you'll use, keyboard is _also_ an important source of events. We can listen for `keypress`, `keydown`, and `keyup`. When these events are handled, we can find out which keys were pressed (like if a space was hit to make the character jump over the hole).

### Form Submission

HTML pages often use a submit button to submit a form to a server. When a user submits a form, the `submit` event is fired. An event handler here might pop up a thank you overlay, play a song, or provide some other sort of interactivity depending on what values were entered in the form.

### Other Events

As you seek to build more complicated applications, you'll need to handle and trigger work on more events. Some other commons events are `scroll`, `mouseenter` and `mouseleave`, `focus`, `blur`, and `onchange`. Here's a list of a [ton of browser events](http://help.dottoro.com/larrqqck.php).

## Resources

- [Web Events](https://developer.mozilla.org/en-US/docs/Web/Events)
- [Bubbling and Capturing](http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)
- [Event Order](http://www.quirksmode.org/js/events_order.html)
