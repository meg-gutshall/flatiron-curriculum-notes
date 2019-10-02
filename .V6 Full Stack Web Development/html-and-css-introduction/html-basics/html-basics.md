# Lesson: HTML Basics

## Notes

- HTML, or HyperText Markup Language, is a markup language which describes the structure and semantic meaning of web pages. Web browsers interpret the HTML code and use it to render output.
- Unlike Ruby, JavaScript, and other programming languages, markup languages like HTML don't have any logic behind them. Instead, they simply surround the content to convey structure and meaning.
- HTML consists of different elements and each element consists of tags, which wrap around content.
  - The tags "affect how the content is rendered by the browser."
- We can also nest elements inside of each other.

### Basic HTML Document Structure

- All HTML documents begin with a "doctype declaration" tag, which tells our web browser which version of HTML to use.
  - Since it's not wrapping any content, our doctype declaration doesn't require a closing tag.
- Next, we add an opening adn closing `html` tag. This tells the web browser to interpret everything inside the tags as HTML code.
- Every HTML page is made up of two primary sections: a `head` and a `body`. The `head` element contains metadata about the HTML document and other information for the browser, while the `body` element contains the actual content.
- Common HTML elements include: links (`a`), paragraphs (`p`), headers (`h1` through `h6`), images (`img`), and lists (`ul`, `ol`, and `li`)
  - In addition to changing how the text is displayed, search engines use headers to help determine what a web page is about. A well-structured article will generally have its principle arguments bracketed by low-number header tags.
  - The `img` element doesn't have a closing tag. The `src` attribute tells the browser where to find the image. The `alt` attribute will be displayed if an image can't be loaded, and also describes the image to search engines and screen readers.

## Code Examples

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- metadata about the HTML document as a whole -->

  </head>
  <body>
    <!-- content of our page will be here -->

  </body>
</html>
```
