# Lesson: Viewport

## Notes

- Unless the user specifically overrides the browser by zooming in or out on their mobile device, we get control of the default size of elements by using the viewport meta tag inside of our HTML head section: `<meta name="viewport" content="width=device-width, initial-scale-1.0">`
- You will want to specify that the width of our viewport should only be _exactly_ as wide as the device. Set its initial scale to 1.0, indicating that the device's initial scale is set to a normal scale, and not to zoom in or out on this content.
- There are other options that can be added, such as `minimum-scale=1.0` and `maximum-scale=1.0`, or, _alternatively_, `user-scalable-false`. Adding these along with setting width and initial scale will prevent users from zooming in or out. Doing this _can_ give you greater control over how a site looks, but it's generally best not to limit scaling, as this may affect screen readers that need to zoom in users who are visually impaired.
