# Lesson: Nested Arrays

## Notes

- Arrays are declared as a comma-separated list of variable names or literal values wrapped in square brackets.
- A nested, or multidimensional array, is an array whose individual elements are also arrays.
- Nested arrays are useful for storing groups of similar data.
- To access data from and add data to (i.e., "read and write") a nested array, we use the same methods we've been using to deal with one-dimensional arrays.
  - To access a value from a nested array, we double up on bracket notation to drill down into the second, nested level (i.e. `array[index][index]`).
    - The first `index` is the nested array. The second is the value in the nested array.
- To add data to a nested array, we can use the same `<<`, or shovel, method we use to add data to a one-dimensional array.
  - To add an element to an array that is nested inside of another array, we first use the same bracket notation as above to dig down to the nested array, and then we can use the `<<` on it (i.e. `array[index] << value`).
- To iterate through nested arrays, we add a second layer of iteration inside the first.
- Multidimensional arrays, like the deeply nested one above, are useful for storing hierarchical data. Any collection of information that you can picture like a tree is a good candidate for a nested array.
  - The data structure is considered hierarchical.
  - A useful tactic is to format the array such that each nested level is placed on its own line.
  - Don't go more than four levels deep when constructing a multidimensional array, use the has instead.

## Code Examples

### Iteration in Nested Arrays

```ruby
nested_students = [
  ["Mike", "Grade 10", "A average"],
  ["Tim", "Grade 10", "C average"],
  ["Monique", "Grade 11", "B average", "Class President"]
]

nested_students.each do |student_array|
  student_array.each do |student_detail|
    puts student_detail
  end
end
```
