# Lesson: Collect and Return Values

## Notes

- The most important thing to remember about `.each` is that it does not change the return value. It implicitly returns the original array.
  - To change what's being returned, we have to create an empty array and push elements into that array.
- `.map` (also known as `.collect`) is an abstraction of our `.each` method.
  - An abstraction is the process of taking away or removing characteristics from something in order to reduce it to a set of essential characteristics.
  - These methods will return an array based on the block of code between `do` and `end` (unless the block includes `puts` which always returns `nil`.)