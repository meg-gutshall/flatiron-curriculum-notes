# Lab: DOM Editing

We've started looking at the DOM and its structure, now it's time to see what we can do with it.

## Identify that DOM Nodes Are Written as HTML

When viewing the DOM through DevTools' **Elements** tab, we see HTML that is a clone of the HTML found in the source HTML file. DOM nodes represent all components that make up a web page.

DOM nodes most often have a starting tag and an ending tag. Because of this, something else could nest inside. This inner node is called a child node. The outer node is called a parent node. To nest items in a normal tag, we simply add the child node HTML element content between its parent's starting and ending tags:

```html
<body>
  <main>
    <p>I am a nest paragraph, inside the main element, inside the body!</p>
  </main>
</body>
```

Some nodes only have a starting tag. Those are called self-closing elements. These elements do not have any content nested inside of them. More technically, they are called void elements. Void elements cannot be parent nodes. In self-closing tags, the trailing `/` is optional. An example of a self-closing tag is an image:

```html
<img src="http://gph.is/1mPQEB0" alt="Mr.Rogers 'Roger that'">

<!-- Or use the optional trailing backslash(/) -->

<img src="http://gph.is/1mPQEB0" alt="Mr.Rogers 'Roger that'" />
```

Every HTML element has a `display` value. Since these are known by modern browsers, you don't have to worry about specifying the value unless you want to change it. That value can be many things (including `none`, which hides the element), but the default value for most elements is either [`block`](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements) or [`inline`](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements). For the image above, the value is `inline`.

### Resources

- [HTML Block Elements (MDN)](https://developer.mozilla.org/en/docs/Web/HTML/Block-level_elements)
- [HTML Inline Elements (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)
