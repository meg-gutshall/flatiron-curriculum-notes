# Lesson: Converting Data Types

## Notes

### The `.split` Method

- The `.split` method will convert a string into an array.
- The `.split` method takes the an argument of the character in the string on which you want to split it (i.e. a comma or a space).
- Example: `"1,2,3,4".split(",") => ["1", "2", "3", "4"]`

### The `.to_a` Method

- The `.to_a` method, when called on a range, can convert a range of numbers to an array.
- Example: `(1..4).to_a => [1, 2, 3, 4]`

### The `.join` Method

- The `.join` method, when called on an array, will convert it into a string.
- This method takes an optional argument containing either a character or set of characters that will be inserted between each array element, as they are assembled into a string.
- Example without argument: `["a", "b", "c"].join => "abc"`
- Example with argument: `["a", "b", "c"].join(, ) => "a, b, c"`
