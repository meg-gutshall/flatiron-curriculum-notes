# Lesson: Responsive Media

## Notes

- With CSS, we can create _fluid_ content. Using percent (%) measurements on our media's CSS allows them to fluidly fill the size of their container. In most cases our media is contained within the columns and rows of our layouts.

### Use Percent Measurements

- By setting our media to expand `width: 100%;`, we're setting them to be as wide as the parent element they are inside of. Then, by setting `max-width: 100%;`, we prevent them from getting any larger than their parent.
- Using both these properties will ensure that they scale fluidly in all browsers. Having them fill their containers will allow us to write fewer media queries overall as they will squish and expand until we set a fixed size for their parent elements. This also allows us to focus sizing the parent element of the media content, which will often be a column of sibling elements.

## Code Examples

```html
img, form, input, table, video, audio, iframe {
  width: 100%;
  max-width: 100%;
}
```