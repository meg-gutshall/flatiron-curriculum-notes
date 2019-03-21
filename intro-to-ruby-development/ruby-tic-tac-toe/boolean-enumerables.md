# Lesson: Boolean Enumerables

## Notes

- When you use `#each` on a collection, the return value is always the original collection.

### The `#all?` Method

- The rule for the `#all?` enumerator is that the block passed to it must return `true` for every iteration for the entire `#all?` expression or method to return `true`.

### The `#none?` Method

- The opposite of `#all?` where we are interested in none of the elements in a collection producing a true expression.
- If any of the elements in the collection evaluate to `true` when passed to the block, `#none?` will return `false`. If none of the elements evaluate to `true`, `#none?` will return `true`.

### The `#any?` Method

- Ensures that at least one element within the block of code will return `true`.
  - Will evaluate to `false` if no elements return `true`.

### The `#include?` Method

- Whereas `#any?` is useful for evaluating the truthiness of the logic of a block, `#include?` is helpful if you'd like to merely compare actual contents of a known value.
- `#include?` will return `true` if the given object exists in the element. If it doesn't find a match, it will return `false`.