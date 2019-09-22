# Lesson: A Peek Behind the "Link", the Web's Superpower

## Notes

- In addition to being freely accessible and distributable for virtually no cost, texts created on the web can refer to one another, a process that's so common we might miss how special it is. On the Web, HTML documents can organically relate (link) to one another, allowing pieces of information to reference one another without the constraint of a hierarchical structure.
- The idea for hyperlinks was discovered by the inventor of the World Wide Web, Tim Berners-Lee.
- A hyperlink consists of two parts: an "address" and a "trigger" (a word or idea to suggest the reason for the link).
  - To achieve these two goals, we need to describe the data in the document using the same technology ("text") that makes up the document. In other words, we need to provide "metadata"—data about data.
- Tim Berners-Lee developed an annotation language named Hypertext Markup Language (HTML). HTML is a language to create content as well as describe the meaning of certain blocks of text.
- "Meaning" is denoted by "wrapping" the text in "tags" or built-in content classifications. Each tag broadly defines the marked-up content. Slight variations between usages of a tag can be captured by providing a specific tag with an attribute.
- One of the most fundamental features of the web is the ability to relate information to one another.
- A simple pattern applies to all HTML elements:
  - Tags classify the type of data
  - Attributes describe the specific occurrence of an HTML element

## Code Examples

### Anatomy of an HTML Tag

```html
<opening tag content-attribute=attribute value>
  Content
</closing tag> <!-- Its a closing tag because the tag name begins with a `/`. By the way, this is an HTML comment. -->
```
