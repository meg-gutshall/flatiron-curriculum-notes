---
description: 'Version 8: Module 14: Section 2: Lesson'
---

# Changing the DOM with Dev Tools and JavaScript

## Delete an Element with Chrome DevTools

Once you open Chrome DevTools and navigate to the **Elements** tab, select an element. You'll notice that element is highlighted on the web page. Press the delete button on your keyboard and the element will vanish from the browser's rendered page.

Now let's view the page source. Click on "View" from Chrome's menu bar, select "Developer," then "View Source." The HTML is unchanged even though you just deleted an element! Why is that?

Changes in the DOM do not affect the HTML file on the server. If that were true, anyone could change carefully-written HTML. The HTML, which lives on the server, is unchanged. Refresh the page and your deleted element will reappear. That's because you're reloading the DOM _from the source_.

## Using the DevTools' JavaScript Console

We can do the same deletion by selecting elements and deleting them using the DevTools with JavaScript. In DevTools, select the **Console** tab.

At the bottom you will see a cursor. There, type the word `document` and press "Enter." You'll get a `#document` returned. If you click the disclosure triangle, you'll see that it's the exact HTML that you would find in the **Elements** tab.

_Note: `disclosure triangle` is the triangle on the left side of the returned `#document`. It is hiding the HTML that wouldn't normally be shown. It is good information to have is you wanted more details about what is going on behind the scenes. Those triangles are standard for hiding more information throughout Chrome DevTools. If you want to see more, feel free to click on the triangle—you won't break anything!_

Since `document` is an `object`, which means that it has properties and `methods` we can imagine that by calling `methods` on it, it can return DOM elements. Let's find, or `select`, an element by speaking JavaScript with the DOM.

### How to Select an Element with JavaScript

In the **Console** type:

```javascript
document.querySelector('header');
```

This will return something like this: `<header class="site-header">...</header>`. Go ahead and click on that disclosure triangle to see more. This is the DOM Node, a JavaScript `object`. This means that it, in turn, can have methods called on it! This is called _method chaining_. Let's use _method chaining_ to remove our node from the DOM.

### How to Delete an Element with JavaScript

Now type:

```javascript
document.querySelector('header').remove();
```

The header is gone! We called `document.querySelector('header')` in order to get the node onto which we _chained_ the call to `remove()`. We use dot-notation to _chain_ the calls.

Just the same as before, the source file has not been changed. Reload the DOM by refreshing the page and the header will be restored.

## Preview JavaScript Variables

JavaScript variables let us refer to a calculation, a process, or a value by giving it a name.
