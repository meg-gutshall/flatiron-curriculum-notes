# Lesson: Array Basics

## Notes

- An array is like a list, but in code form. It stores pieces of data as a collection and can contain any data types in any combination (but it’s encouraged that you keep it to one data type per array).
- Arrays are declared by listing variable names or literals separated by commas (`,`) and wrapped in square brackets `[]`.
- Two ways to create an array:
  - The Literal Constructor: `my_array = []`
  - The Class Constructor: `my_array = Array.new`
- Items in an array are associated with a number called an index. The first item in the array will always be “at index `0`”. In other words, indexes will always be one less than the count.
  - Access a specific element in an array by using its index: `array[index]`
    - The last item of an array is considered to be stored at an index of `-1`.
  - If you try to access an array at an index that doesn't exist, it returns `nil`.
- Find the index number of an element in an array by using the `.index()` method: `array.index(element)`

### Assigning new values to an array

- To re-assign a value to an index in an array we use the `[ ] =` syntax. We must supply an index we want to re-assign and then a value for that index.
- Re-assigning a value to an index of an array looks a lot like variable definition and that is by design.

### Adding items to an array

- The shovel method: employs the "shovel" operator `<<` and allows you to add ("shovel") items onto the end of an array (this is the preferred syntax for adding elements to an array)
- The `.push` method: calling `.push` on an array will also allow you to add items onto the end of an array, however, you can add more than one item at a time with this method
- The `.unshift` method: call the `.unshift` method to add an item to the front of the array

### Removing items from an array

- The `.pop` method: removes the last item from the end of an array and supplies that item as its return
- The `.shift` method: removes the first item from the front of an array and supplies that item as its return

### Operating on arrays

- The `.reverse` method: reverses an array
- The `.include?` method: returns a boolean of whether or not the array contains (or includes) the element submitted to it inside the parentheses

### Using methods on arrays

- We can use the `#first` method on an array to access the first element: `array.first`
- We can use the `#last` method on an array to access the last element: `array.last`