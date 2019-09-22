# Lesson: Document Structure

## Notes

### `<!DOCTYPE html>`

At the top of every HTML document, you're always going to start off with the sale element, `DOCTYPE`. The `DOCTYPE` element starts with a `<`, followed by an `!` and `DOCTYPE`, then specifies which version of HTML we want to use. In HTML5, we just say `html`, and the browser will interpret the rest of the document as HTML5. To close the element, add a `>` at the end.

### `<html> </html>`

The next element is also always required: `<html>`. This tells the browser that everything that falls between the opening and closing `html` tags is to be interpreted as HTML code.
One attribute that is important to include in the `<html>` tag is `lang`, which declares what language the webpage is written in. In our case, writing in English, we use `lang="en"`. This helps search engines to know what language a page is written in.

### `<!-- Comments -->`

Inside our HTML, sometimes we want to leave notes wither for ourselves or for other developers. An example might be a brief explanation of what some part of the code is doing, or an important message or reminder. We can write comments by wrapping the text we want like so: `<!-- This is a comment! -->`. Text included in the comment will not be visible in the webpage, but will be visible in the browser console and `.html` file.

### `<head> </head>`

Inside our `<html` tags, we divide the page into two main sections, `<head>` and `<body>`, which both play unique roles. Before we get to adding viewable content, there are some additional bits of information we need to declare about our webpage, and this information will be stored in the `<head>`.

- The `<meta>` tag provides metadata about the document, including what character set to use, a description of the content, specific keywords, and the author. Adding metadata on the content of the page helps search engines to know what the page contains. There is also a `viewport` method, which instructs the browser on how to control the page's dimensions and scaling.
- The `<link>` tag is also used here, and is for importing external files. Most commonly, we'll see this being used to import in CSS stylesheets as well as fonts.
- Another common tag in the `<head>` is `<title>`. The `<title>` is where the title of the webpage would be entered. Text added inside the `<title>` tags will appear up on your browser tab.

## Code Examples

### Examples of `<meta>` tags we can add into our `head` section

```html
<meta charset="UTF-8">
<meta name="description" content="Exceptional Realty Group, your real estate agent for buying, selling, and renting throughout New York City">
<meta name="keywords" content="Exceptional Realty Group, real estate, houses, property">
<meta name="author" content="Jon Grover">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
