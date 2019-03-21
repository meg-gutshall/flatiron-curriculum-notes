# Lesson: Intro to Nested Hashes

## Notes

- Hashes can be multi-dimensional, or nested.
  - A key in a hash can point to a value that is a collection of objects, like an array or another hash.
  - This allows us to store data that is associated to other data via categories and subcategories.
  - You'll find them in APIs ("Application Programming Interfaces").
- Hashes and arrays can store any type of data.
- Iteration can be used on nested hashes as well by nesting the iterations.
- The `#values` method lets you collect all of the values in a hash.
- The `#keys` method lets you collect all of the keys in a hash.
- The `#min` method returns the key/value pair whose key has the lowest value.
- The `#flatten` method will take nested arrays and convert them into one array.