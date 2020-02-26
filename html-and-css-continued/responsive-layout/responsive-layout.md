# Lesson: Responsive Layout

## Notes

### Construct Alternate Wrapper Sizes Between Fixed and Fluid Layouts

- One common way to handle this adjustment in CSS is to use a _wrapper_ class, one class that wraps and and all core content of our site. If we want to make changes that affect all of that content using a media query, we can simply modify the one _wrapper_ class.
- A popular strategy when using a wrapper class is to first make a layout for large screens that is centered and stays within a fixed pixel size on the screen, so that our content doesn't get stretched out too wide. On smaller devices, we switch to a liquid (fluid) size using percents so our content will squish and expand on many different small and medium sized devices, taking up the maximum amount of space available.
  - There's also the option to go with the opposite, mobile-first, approach.

### Construct Adjustable Column Properties for Different Screen Sizes

- One common issue we battle when building responsive sites is handling multi-column layouts on smaller devices. Usually it's best to change the multi-column layout into a single column layout. This can be achieved easily by changing floating columns to `float: none;` on smaller devices and adjusting their widths accordingly.
