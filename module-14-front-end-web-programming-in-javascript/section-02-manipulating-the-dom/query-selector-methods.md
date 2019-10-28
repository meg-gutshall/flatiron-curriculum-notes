# querySelector Methods

One of the most essential skills in our web development toolbox is finding elements in the DOM.

While `document.getElementById()` and `document.getElementsByClassName()` are good, we can improve our search when we use document structure (tag, `id`, and `class`) **and** the tree structure of the DOM. It turns out CSS is a _great_ language for expressing those relationships! With the following methods we provide a CSS selector as argument and we get back the collections _or_ specific node we want.

To practice finding elements in the DOM, we're going to make use of two methods that are useful for navigating the DOM: `document.querySelector()` and `document.querySelectorAll()`.

## Use `document.querySelector()` and `document.querySelectorAll()` to Find Nested Nodes

### `querySelector()`

`querySelector()` takes one argument, a string of CSS-compatible [selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors), and returns the first element that matches these selectors.

Given a document like:

```html
<body>
  <div>
    Hello!
  </div>

  <div>
    Goodbye!
  </div>
</body>
```

If we called `document.querySelector("div")`, the method would return the first `div` (whose content is "Hello!").

Selectors aren't limited to using one tag name in their argument though, otherwise why not just use `document.getElementsByTagName("div")[0]`? We can get very specific.

```html
<body>
  <div>
    <ul class="ranked-list">
      <li>1</li>
      <li>
        <div>
          <ul>
            <li>2</li>
          </ul>
        </div>
      </li>
      <li>3</li>
    </ul>
  </div>

  <div>
    <ul class="ranked-list">
      <li>6</li>
      <li>2</li>
      <li>
        <div>4</div>
      </li>
    </ul>
  </div>
</body>
```

```javascript
const li2 = document.querySelector("ul.ranked-list li ul li");
li2;
// => <li>2</li>

const div4 = document.querySelector("ul.ranked-list li div");
div4;
// => <div>4</div>
```

### `querySelectorAll()`

`querySelectorAll()` works a lot like `querySelector()`—it accepts a selector as its argument and it searches starting from the element that it's called on (or from the `document`)—but instead of returning the first match, it returns a `NodeList` collection (which, remember, is not _technically_ an `Array`) of matching elements.

Given a document like:

```html
<main id="app">
  <ul class="ranked-list">
    <li>1</li>
    <li>2</li>
  </ul>

  <ul class="ranked-list">
    <li>10</li>
    <li>11</li>
  </ul>
</main>
```

If we called:

```javascript
document.getElementById("app").querySelectorAll("ul.ranked-list li")
```

We'd get back a list of Nodes corresponding to: `<li>1</li>, <li>2</li>, <li>10</li>, <li>11</li>`.

## Resources

- [Reference Table of CSS Selectors](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors#Reference_table_of_selectors)
- [`querySelector()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [`querySelectorAll()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
