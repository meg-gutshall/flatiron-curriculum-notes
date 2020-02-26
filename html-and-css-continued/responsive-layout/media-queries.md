# Lesson: Media Queries

## Notes

- Media queries are a feature of CSS. They are sets of styles that are applied when the medium satisfies specific conditions. media queries most frequently decide whether a group of CSS rules applies based on the device "viewport" (or, "screen") size. The points at which the layout adjusts, based on some media property (or properties!), is called a "breakpoint".
- Media queries automatically inherit all of the styles written outside of the `{}` braces so inside the media query we only need to write the CSS for the properties we wish to change.
- Let your content determine where break points should fall.

### Media Query Syntax

When defining a media query, we use the `@media` keyword followed by conditional statements that trigger the media query to apply or not.

#### `not`, `only`

The logical keywords `not` or `only` can be used optionally to include or exclude specific media types or screen sizes.

#### `mediatype`

Currently, the only well-supported media types are: screen, print, or all (meaning all devices). Mobile, tablet, and desktop devices all fall within the _screen_ media type, while _print_ is used for displaying content in a "print preview" mode. Most commonly we are concerned only with _screen_.

#### `and`, `,`

We can use `and` and `,` to separate or combine conditions.

- Using `and` requires that both conditions on each side of the `and` are true in order for the query to apply.
- Using `,` stand for _or_, meaning that only one of the conditions on either side of the comma has to be true for the query to trigger.

#### (expression)

We define conditional expressions by writing the test and wrapping it in parentheses. The expression must evaluate to true in order for the query to trigger unless using a `,`. These expressions are followed by a set of `{}` curly braces that enclose the CSS selectors and rules that will be applied when the media query is triggered.

## Code Examples

### Media Query Statements

```html
@media (max-width: 960px) {
  body {
    background-color: #fff;
  }
}

@media screen and (max-width: 992px) {
  body {
    background-color: #000;
  }
}

@media screen only and (max-width: 1080px) {
  body {
    background-color: #eee;
  }
}
```
