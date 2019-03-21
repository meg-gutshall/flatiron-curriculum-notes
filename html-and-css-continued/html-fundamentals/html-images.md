# Lesson: HTML Images

## Notes

- The way we insert images is using the `<img>` element which has two main attributes: `<src>`, the source of the image, and `<alt>`, the _alternate_ text.
- To add a source to our image, we can provide either a relative path to a file we have locally, or provide a URL to an existing image on the Internet.
  - An image file in the same directory would just need the filename, and if we were leaving the current folder, moving up to a parent directory, we would use `../` at the beginning of the path.
- We should add an `alt` text to this image which will be displayed if the image fails to load. The alt text is also important for screen readers for the visually impaired, as the alt text will be read aloud. It is necessary to provide a source for an image to load, and while it isn't required, it is strongly advised to add an alternate text as well.
- Content added to the `title` attribute will display when we hover over the image with our mouse.