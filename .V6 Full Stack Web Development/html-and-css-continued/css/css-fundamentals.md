# Lesson: CSS Fundamentals

## Notes

- We create a CSS rule by defining the selector, which matches the HTML element we want to style. Inside the curly braces we declare the properties we want to change and after the colon, we set the value we want to change that property to.
  - Example: `selector {property: value;}`

### CSS Use Formats

#### Inline

- Inline includes the styles directly into the HTML element with the `style` attribute.
  - Example: `<p style="color: blue;"></p>`
- This is generally not the best practice because it only affects that single element and it breaks out principle of separation of content and presentation.

#### Internal

- Internal CSS is inside of `style` tags in the HTML document's `head` section.
  - This applies the styling to that single document.

#### External

- If we want our CSS to carry across various pages, we can use an external stylesheet. This is a separate CSS file that we link in the `head` of HTML documents.
  - Example: `<link rel="stylesheet" href="css/styles.css">`

### Utilize Various Types of CSS Selectors

#### ID and Class Selectors

- ID selectors target all elements with a specific ID attribute value. The way we specify an ID selector in a CSS rule is to follow the element name with a hash tag and then the ID attribute value we want to match (no spaces).
- Class selectors target all elements with a class attribute value matching the selector name. We specify a class selector using the period symbol followed by the name of the value (no spaces).
- The difference between IDs and classes is the IDs are meant for one element on the page that has unique identity where class selectors are meant to be spread throughout the page across multiple elements.

#### Compound Selectors

- Compound selectors let us apply the same CSS rules to multiple elements at once by separating the elements with commas. This eliminates the need to rewrite a new CSS rule containing the same styles for different elements.

#### Descendant Selectors

- Descendant selectors target elements that are descendants of the matching selector name. A descendant selector is indicated by a space in between one selector and another selector.

#### Child Selectors

- The child selector targets all elements that are the immediate children of a specified element, using the `>` symbol.

#### Adjacent Sibling Selector

- The adjacent sibling selector target elements that appear directly after the matching selector name, using the `+` symbol.

#### General Sibling Selector

- The general sibling selector (sometimes called the preceded selector) will style all matched elements after the preceding selector name, using the `~` symbol.

#### Universal

- The universal selector matches any elements and will apply to elements that are not targeted by other rules. It's indicated by the `*` symbol.

#### Attribute Selectors

- The `attribute` selector can target elements with a particular attribute. We can also define exactly which attribute we want to match.
  - Example: `element[attribute="value"]`

#### Pseudo-class Selectors

- Pseudo-class selectors target elements based on a particular state of an element or relationship to other elements, using the `:` symbol (no spaces).

### Color Values in CSS

#### Hexadecimal Color Values

- Most often developers use hexadecimals, which represents a wide range of colors. Hex colors begin with `#` and are followed by, generally, 6 numbers or letters.
  - Hexadecimal Numbers: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9,a, b, c, d, e, f, 10
- Hex colors work by creating Red, Green, Blue (RGB) values. Traditional RGB colors are on a scale of 0 to 255 for each of the three colors in the spectrum. `#000000` translates to black since 0 reds, 0 greens, and 0 blues represents the absence of all colors, and `#ffffff` makes white since 255 reds, 255 greens, and 255 blues equal the maximum of each of the colors.
- Hex colors can be shortened to just three numbers when each RGB values is the same for each digit.

#### RGB Color Values

- We can also work directly with RGB values.
- You can add an extra channel to your RGB color by setting an "a" value, which represents opacity.

### CSS Comments

- Everything in between `/* */` is a CSS comment. The browser will not pay attention to these comments, but they can be useful for us to add explanations or reminders alongside our CSS code.
