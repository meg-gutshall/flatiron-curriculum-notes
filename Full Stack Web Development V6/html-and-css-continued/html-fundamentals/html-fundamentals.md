# Lesson: HTML Fundamentals

## Notes

### Identify Ordered, Unordered, and Definition Lists

- When we want to present a list of items in a clear, readable format, we turn to the HTML unordered list, represented by the `ul` tag.
- If it's important to distinguish a particular order for the items (as for a recipe or ranking), we use an ordered list, or the `ol` tag.
  - We nest our items within the lists. Each `li` is a list item contained in the larger `ul` or `ol` container.
- Another list we can use is a definition list, which defines specific types of items.

### Identify Images

- To include an image in our page, we use an `img` tag.
- There are two notable things about the `img` tag.
  - The first is that it has no closing tag-this tag closes itself!
  - Secondly, it handles a lot of attributes. Our `alt` attribute provides descriptive text the browser can display if it can't find the image file. The browser can also display the `title` text to give the user more information about the image. The `width` and `height` attributes define the size of the image that shows up in the browser.

### Identify Links

- We can create links other than the basic link structure:
  - To link an image, we can replace the text within the `a` tags with our image tag.
  - To link an email, set `a href` equal to `"mailto:email@email.com"`.
  - Sometimes we might want to link to another, specific location on the same webpage. We can target an element that we identified or classified earlier. This is called an Anchor Link. It uses an `id` attribute to identify the content or the section of the page to which we want to link, then sets `a href` equal to `#id`.
- When considering what location links point to, you will choose between relative or absolute links.
  - A relative link directs to content within the same website.
  - An absolute link directs to external content and requires a fully defined URL path. This is likely the type of link you see most often.

## Code Examples

### Definition List

```html
<dl>
  <dt>First term</dt>
  <dd>Term definition</dd>
</dl>
```

### Anchor Link

```html
<p id="tips">Useful Tips Section</p>
<a href="#tips">Jump to the Useful Tips Section</a>
```