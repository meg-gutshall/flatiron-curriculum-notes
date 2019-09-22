# Lesson: Display

## Notes

### Block

- Displays one above the other and by default expands (100%) to fill the width of the screen
  - Able to specify width as well as top and bottom margins, however the margins on the top and bottom overlap other block element top and bottom margins
- Elements that display block by default are: `div`, `p`, `h1...h6`

### Inline

- Displays side-by-side on the same line
  - Does not accept width nor top and bottom margins — they're as wide as the content inside of them
- Elements that display inline by default are: `span`, `a`, `img`

### Inline-block

- Displays side-by-side and by default expands (100%) to fill the width of the screen
  - Able to specify width as well as top and bottom margins

### Table-cell

- Does not have the ability to have margin (acts as cells in a table)

### Floating

- Any time you float an element, elements that come after it try to nest upwards which is why you have to `clear` elements.

### Clearfix

- Styles the height of the parent element of child float elements so it doesn't collapse.

### Centering

- To center content, create a wrapper (`<div class="wrapper">`), then set its margin to `margin: 0 auto;`.

### Column Structure

- Use the IE `box-sizing: border-box;` attribute when working with columns since it includes padding and border.
- Or set padding, border, and margin in percentages and subtract the appropriate percentage from each section to add up to 100% width.

## Code Examples

### Floating & Clearing

```css
p {
  float: right;
}

footer {
  clear: both;
}
```

### Clearfix CSS Hack

```css
.clearfix:after {
  content: ".";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
  line-height: 0;
}
```