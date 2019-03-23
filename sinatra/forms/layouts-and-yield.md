# Lesson: Layouts and Yield

## Notes

- It's a common practice to create a single `layout.erb` file for elements that stay consistent across every page in a website.
- Inside `layout.erb`, we need to add a `yield` wherever we want the additional page content to be loaded.
- When a controller action is triggered and the `erb` method is called, it automatically looks to see if there is a view titled `layout.erb`. If that file exists, it loads that content around the desired erb file.