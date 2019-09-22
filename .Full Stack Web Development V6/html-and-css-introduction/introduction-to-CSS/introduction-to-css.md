# Lesson: Introduction to CSS

## Notes

- Browsers combine the content (HTML) and presentation (CSS) layers to display web pages. CSS is the language for styling web pages.
- CSS instructions live apart from the HTML elements and have a different look and feel ("syntax").
- For each presentation rule, there are three things to keep in mind:
  - What is the specific HTML we want to style?
  - What are the qualities we want to modify?
  - How do we want to modify the qualities of the element?
- CSS selectors are a way of declaring which HTML elements you wish to style.
- Selectors can appear in a few different ways:
  - The type of HTML element
  - The value of an element's `id` or `class`
  - The value of an element's attributes
  - The element's relationship with surrounding elements
- Class selectors are used to select all elements that share a given class name.
  - The class selector syntax is: `.classname`
- You can also use the `id` selector to style elements. However, there should be only one element with a given id in an HTML document. This can make styling with the ID selector ideal for one-off styles.
  - The `id` selector syntax is: `#idvalue`
- CSS property values are directly related to property names.
  - Some properties have their values set with words, others with numbers, and some can take both.
- A CSS property name with a CSS property value is a CSS declaration.
  - To apply a CSS declaration to an HTML element, you need to combine it with a CSS selector.
- The association between one or more CSS declarations and a CSS selector is called a CSS declaration block.
  - CSS declarations that are applied to a specific selector are wrapped by curly braces (`{}`).
  - Each declaration inside a declaration block must be separated by a semi-colon (`;`).

## Code Examples

```css
selector {
  property-name-1: property value 1;
  property-name-2: property value 2;
}
```
