# Lesson: Responsive Type

## Notes

### Create Maintainable Responsive Type with `em`

- One of the best ways to create maintainable type is through relative measurements such as _em_. Em values are relative to the current `font-size`. Because it is a relative measurement, it is very useful for keeping type proportional.
- By declaring the `font-size` of one element (for instance, the `body`) using % or px and declaring the `font-size` of all other elements using em values, all elements will adjust in proportion to each other all while only having to adjust the body's `font-size` value.
- Em values can be used in width and height properties, so this measurement can be used for the divs and elements making up your web page structure, and would also adjust in proportion based on `font-size`.

### Create Maintainable Responsive Type with Column Count

- Another tip for adjusting type is when you might want to wrap text into separate columns. This is especially true on larger screen sizes where you have big bodies of text content.
- Designers suggest that for optimum readability, you want the measure of your text lines to be between 40 to 80 characters. Anything smaller or larger becomes a bit awkward to read. To tackle this, we use the `column-count` property.
- The default `column-count` is one, meaning text is contained within one column. When our screens get bigger, it might be good to adjust the text into multiple columns.
