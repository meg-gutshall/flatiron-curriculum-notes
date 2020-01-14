# Lab: Removing, Altering, and Inserting HTML

## Creating DOM Elements Programmatically

### `document.createElement()`

Creating an element in JavaScript is an easy process. Simply call `document.createElement("tagName")`, where `tagName` is the name of any valid HTML tag.

```js
let element = document.createElement("div");
```

## Adding Elements to the DOM

To get an element to appear in the DOM, we have to `append` it to an existing DOM node. We can start as high up in the tree as `document.body`, or we can find a more specific element using any of the methods we've learned for traversing the DOM.

### `appendChild()`

Let's append `element` to `body` to start.

```js
document.body.appendChild(element);
```

We can continue to update `element` since we have reference to it.

```js
let ul = document.createElement("ul");

for (let i = 0; i < 3; i++) {
  let li = document.createElement("li");
  li.innerHTML = (i + 1).toString();
  ul.appendChild(li);
}

element.appendChild(ul);
```

## Adding Elements to the DOM via `innerHTML`

Creating elements and then appending them into the DOM is a multi-step process. It's also the safest and most reliable. Most repeated code can be removed by using functions and loops. It's "The Right Way."

That said, there's another route which is commonly used: `Element.innerHTML`. If you can get a node with `getElementById` or `querySelector` or any of the modes you've learned thus far, you can imagine that you have that node's opening and closing HTML tag. You can update the node's `innerHTML` property with a string of HTML and it will be _just as if_ you changed the HTML source for that node.

```js
let element = document.querySelector("p#greeting");
element.innerHTML = "Hello, DOM!"
```

There are dangers with using `innerHTML`, however. If you put user-driven data into the DOM using `innerHTML`, someone could do something nasty. Consider the following code:

```js
content = someTextArea.value;
node.innerHTML = `Hi, ${content}!`;
```

We might have intended for `someTextArea` to contain something like a person's name that we're going to echo back out to the screen. But what if the person typing in `someTextArea` is a nasty person and submits:

```html
<a href="#" onclick="doSomethingNastyLikeStealCookies">click here to claim your prize</a>
```

While you're not familiar with events (_yet!_), it should be clear that `doSomethingNasty` when clicking on a link that promises a prize is

## Changing Properties on DOM Nodes

We can change properties on DOM nodes to change their appearance.

```js
element.style.backgroundColor = "#27647B";
```

Perhaps the most common way to change how things appear in the DOM is by changing an element's `class` attribute. As you know from CSS, we often change the way a bit of rendered HTML appears by changing its `class` attribute: adding a name or removing a name. It's very common, therefore, to grab an element with JavaScript and update its `className` property—which is the same as setting the `class` property in the HTML. The `className` property expects a `String` where each class name is separated by a space.

```js
element.className = "dog"
element.className = "pet-listing dog"
```

Sometimes it's easier to add classes programmatically instead of creating a long string first. JavaScript makes this friendly by having elements provide a `classList` [property](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList) which has `.add()` and `.remove()` methods. So provided the CSS rules for `.this-is-fine` and `.the-room-is-on-fire` exist, you could change the display of `element` like so:

```js
element.classList.remove("this-is-fine");
element.classList.add("the-room-is-on-fire");
```

Why go through the trouble of defining appearance in a stylesheet which is applied by [`classList`](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList) versus simply using JavaScript to change the appearance? Again, this goes back to a fundamental programming concept about separating concerns between technologies:

- HTML defines the structure of the website (not appearance nor functionality)
- JavaScript defines functionality of the website (not structure nor styling)
- CSS defines the visualization and style of the website (not structure nor functionality)

## Removing Elements from the DOM

### `removeChild()`

Let's really use the power of `querySelector` and method chaining. The `removeChild()` method requires us to find a parent and tell it to remove its already-found child.

```js
ul.removeChild(ul.querySelector("li:nth-child(2)"));
```

### `element.remove()`

We can just call `remove()` on the element itself as well.

```js
ul.remove();
```

## Resources

- [`document.createElement()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
- [`appendChild()`](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)
- [`removeChild()`](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)
- [`element.remove()`](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove)
- [`classList` Property](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
- [`innerHTML` Property](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)
- [`innerText` HTML Property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText)
- [`innerContent` Node Property](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)
