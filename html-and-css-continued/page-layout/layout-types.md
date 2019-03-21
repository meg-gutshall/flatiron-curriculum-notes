# Lesson: Layout Types

## Notes

### Scaling Elements

- Sizing units:
  - Fixed (px)
  - Elastic (em)
  - Fluid (%)
  - Min/Max (media query)

#### Fixed (px)

- Pros: Widths are the same for all screens.
- Cons: May create excessive white space for users with larger screen resolutions. Smaller screen resolutions may require a horizontal scroll bar, depending on the fixed layout's width (i.e. not responsive).

#### Elastic (em)

- Pros: In responsive design, upscaling and downscaling the text will keep the containers in proportion with their text content.
- Cons: Parent elements may crowd each other if the text gets too large in size.

#### Fluid (%)

- Pros: Makes full use of the screen and can eliminate horizontal scroll bars in smaller screen resolutions.
- Cons: The designer has less control over what the user sees with regard to container sizes and where type and media wraps.

### Content Overflow

- The `overflow` attribute can be set to `visible`, `hidden`, `scroll`, or `auto`.
- If you want to set an `overflow` attribute on an element, you must first set a fixed height.

### Fluid Height

- In the browser, the body element is always 100% wide but not necessarily 100% high.
- To set a height of 100%, you have to first set the `body` and `html` element heights to 100%.
  - Example: [100% Fluid Height](:note:96f7ae73-a1f8-4818-bf67-770118280e8f)

## Code Examples

### 100% Fluid Height

```css
body, html {
  height: 100%;
  min-height: 100%;
}
```