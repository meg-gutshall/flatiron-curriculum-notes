# Lesson: Box Model

## Notes

- Padding: spacing inside an element
- Margin: spacing outside an element
- Border
  - Takes three values: thickness, style, color

### Sizing for Padding and Margin

- One value: all sides
- Two values: top/bottom, left/right
- Three values: top, left/right, bottom
- Four values: top, right, bottom, left

### Two Types of Box Models

- W3C box model only uses content when setting the width
  - Need to account for padding, border, and margin when calculating content area
- Internet Explorer uses content, padding, and border when setting the width
  - Only need to account for margin when calculating content area

## Code Examples

### Box-Sizing Property

Tells all browsers to use the specified box model

```css
div {
  box-sizing: border-box;
}

/*
IE model = border-box
W3C model = content-box
*/
```
