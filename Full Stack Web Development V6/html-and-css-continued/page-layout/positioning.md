# Lesson: Positioning

## Notes

### Relative

When an element's declaration is set to `position: relative;`, you can set `top`, `right`, `bottom`, or `left` attributes that will "push" the element from the set direction according to its original positioning.

### Absolute

When an element's declaration is set to `position: absolute;`, you can set `top`, `right`, `bottom`, or `left` attributes that will position the element the specified distance from the selected edge of the browser window or relatively positioned parent element.

### Fixed

When an element's declaration is set to `position: fixed;`, it acts much like an absolutely positioned element, except the element will stay in place when the browser window scrolls.

### Z-Index

- Allows us to layer elements on top of one another.
- By default, everything in the browser starts with a z-index of 0.
  - Setting an element to a negative z-index moves it back (behind). The lower the z-index number, the further away from the viewer the element will be.
  - Setting an element to a positive z-index moves it forward (in front). The higher the z-index number, the closer to the viewer the element will be.
  