# The DOM Tree

DOM programming is using JavaScript to:

1. Ask the DOM to find an HTML element or elements in the rendered page
2. Remove the selected element(s) or add a new element next to the selected element
3. Adjust a property of the selected element(s)

Remember, the command to find the HTML element we want is:

```javascript
document.querySelector(selector)
```

The _selector_ is like a query string that lets us find things within an HTML page. It's like how SQL finds records in a database. So what is the syntax of this _selector_? How does the _selector_ navigate through our document to find the DOM nodes that we want to work with (update, move, even delete)? To understand these queries, or "_selectors_", we first need to talk about how the DOM tree (i.e. what we see in the **Elements** tab of our DevTools) is used to help the DOM `methods` find the right nodes.

## The Computer Science Version of "Tree"

What do we mean when we say the DOM is like a tree? Well, trees are thicker at the bottom—starting with the trunk and roots, then the heavy branches, then smaller and smaller branches and leaves splitting off the further they get from the trunk—and the thicker the branch, the more it can hold.

This is exactly how the DOM works, except that the trunk and roots begin at the top and the branches continue downward, symbolizing nested HTML elements. Basically, it's like imagining a tree upside down.

![Example of the JavaScript querySelector method](/public/images/front-end-web-programming-in-javascript/dom-tree.png)

The HTML for this "tree" would be:

```html
<!DOCTYPE HTML>
<html>
  <head>
    <title>My Title</title>
  </head>
  <body>
    <h1>A heading</h1><a href="http://example.com">Link text</a>
  </body>
</html>
```

Not only does providing more information about a node via HTML metadata make it more useful, it also makes the node and its children easier to find.

## How the DOM Works as a Tree

Every tree can contain subtrees, which we can treat independently of their parent trees. Despite just being a small part of a larger tree, they repeat the pattern and appearance of the full tree—like branches! Practically speaking, the DOM begins at `<html>`, but for now we should avoid changing what's between the `<head> </head>` tags. Most of the time, we will look at the DOM subtree with its root at `<body>` and only change things that will be visible on the page. We might also deal with subtrees.

## Finding a Node

JavaScript exposes a few ways of finding DOM nodes directly, or via other ways, courtesy of the `document` object.

### `document.getElementById()`

This method provides the quickest access to a node, but it requires that we know a very specific piece of information—its `id`. This method can only return one element, since CSS `id`s are expected to be unique.

Given the following DOM tree:

```html
<div>
  <h5 id="greeting">Hello!</h5>
</div>
```

We could find the `h5` element with `document.getElementById('greeting')`. Notice how the `id` we pass to `getElementById` is identical to the `id` in `<h5 id="greeting">`.

_**Note:** You can use either single (' ') or double (" ") quotes around the `id` within the `id` in `document.getElementById('yourIdGoesHere')`, as long as you use the same kind to open and close them._

### `document.getElementByClassName()`

This one is also very commonly used in DOM programming. This method finds elements by their `className`. Unlike the previous method, class names do not need to be unique, so this method returns an `HTMLCollection` of the elements with the given class. You can iterate over an `HTMLCollection` with a simple `for` loop.

Given the following DOM tree:

```html
<!-- The `className` attribute is called `class` in HTML -->

<div>
  <div class="banner">
    <h1>Hello!</h1>
  </div>

  <div class="banner">
    <h1>Sup?</h1>
  </div>

  <div class="banner">
    <h5>Tinier heading</h5>
  </div>
</div>
```

We could find all of the elements with the class name "banner" by calling `document.getElementByClassName("banner")`. We can use the `.length` property on the returned object to find out how many elements came back.

If you recall the `for` loop syntax, you might try to write a loop which prints out the `innerHTML` property of every element in the collection. You might find doing so much easier if you save the results of `document.getElementByClassName()` to a variable: `var elements = document.getElementByClassName("yourClassNameHere")`.

### `document.getElementByTagName()`

If you _don't_ know an element's `id` or `class`, but you _do_ know its tag name (the tag name is the thing between the `<>`, e.g., `div`, `h1`, `header`, `article`, etc.). Since tag names aren't unique, this method returns an `HTMLCollection` also.

### Finding a Node with Little to No Information

What if we know next to nothing about an element? Or what if we're just interested in finding out more about the child nodes of a given element? This is where our knowledge tree comes in handy!

Given the following DOM tree:

```html
<main>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
</main>
```

How would we go about changing only the second "Hello!" to "Goodbye!"? We're going to use a mix of different `methods` to accomplish the goal.

Let's start by getting the `<main>` element:

```javascript
const main = document.getElementByTagName("main")[0]
```

Then we can get the children of `main` using `main.children`; so we can get the second child with `main.children[1]`.

```javascript
const div = main.children[1]
```

We can get and update our `<p>` element with:

```javascript
// We can call `getElementByTagName() on an element to constrain the search to its children!

const p = div.getElementByTagName("p")[0]
```

And lastly, we can change an attribute on the node:

```javascript
p.textContent = "Goodbye!"
```

Obviously, this way of accessing that text isn't efficient and won't work on all pages, but it does a good job of demonstrating the basic tools available to us for finding and manipulating HTML elements.

## Resources

- [MDN — Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
