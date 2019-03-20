# Intro to Ruby Iterators

- `each` is a common iteration method.
  - Example: `array.each do |element|`
  - This executes the following block of code once for each element of the array
  - Enclosing an element in pipes (`||`) also acts as a declaration of a variable.
    - The variable's value is automatically assigned the element from the array for the current iteration.
- Iterators like `#each` are smart—they don't need a separate counter variable and manual incrementing of that variable to know how many times to do something. They use the number of items in the collection on which they are called to determine how many times they will do something.
- The `#each` method will always return the original collection on which it was called.
- Another way of establishing a code block that you may encounter is to use curly brackets, `{ }`, instead of the `do`/`end` keywords.
  - It is appropriate to use the `{ }` syntax when the code in the block is short and can fit on one line.