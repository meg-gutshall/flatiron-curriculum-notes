# Lesson: Introduction to the DOM to Get Started

## Identify the Document Object Model (DOM)

Your DNA represents a code-based version of _you_. The DOM represents a code-based version of _a web page_. If something edits you DNA, changes will be made in your body. Similarly, if something changes the DOM, what's displayed in the browser _changes as well_.

## View a Web Page's Source to See How the DOM Is Created

The DOM is created when the page loads from the HTML that the web server provides the browser. Let's examine this process step by step:

1. In a Google Chrome browser, copy the current URL and open it in another tab.
2. To see the HTML of this page, add `view-source:` to the front of the URL in the new tab. By using the `view-source` URL prefix, all the page's source HTML appears.
3. The browser reads the HTML, along with CSS and JavaScript defined in `<script>` or `<link>` tags, to create the DOM inside the browser. At this point, nothing is displayed on the screen, however, it is so brief, our human eyes never really catch it.
4. The browser then uses the DOM object to create the rendered page. While we often learn that browsers "display HTML" that's not exactly accurate. Browsers use HTML to create a "middleman" that they in turn use to display the structured and styled content.

## Identify the DOM as Accessed by JavaScript Objects

Recall that JavaScript is object-oriented. The DOM is available inside Chrome through two _variables_: `window` and `document`.

The `window` variable points to an _object_ that represents Chrome's information about the browser "window." It has many functions, but the main one is "it's a place where everything is." A browser without a `window` is like the universe before the Big Bang; there's just _nothing_. It's in the `window` that the data types are defined (`Array`, `String`, and `Number`).

In the `window`, JavaScript also tracks operating system browser information like:

```javascript
window.innerHeight;
// returns the inner height of the browser window
```

Like all object, `window` also has _methods_. We won't use them too much. We don't want to mess with the container of everything that is or operating system stuff. Instead, we want to change content. To do that, we're going to focus on an object called `document`.

As an _object_, `document` has _properties_:

```javascript
document.URL //=> https://www.flatironschool.com
```

As an _object_, `document` also has _methods_:

```javascript
document.write("Moof");
// removes all existing DOM content and replaces it with "Moof"
```

The _methods_ and _properties_ that the DOM provides via its objects is called the DOM's "Application Programming Interface," or "API." It's a programming word that means "the things that these objects know how to do."

## Resources

[CSS Tricks – What Is the DOM?](https://css-tricks.com/dom/)<br>
[MDN – The DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
