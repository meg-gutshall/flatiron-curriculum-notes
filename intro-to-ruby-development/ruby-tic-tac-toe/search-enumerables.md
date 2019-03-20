# Search Enumerables

- Often we want to search for elements in a collection based on a condition.
- When you evoke `#select` on a collection, the return value will be a new array containing all the elements of the collection that cause the block passed to `#select` to return true.
  - If no element makes the block evaluate to `true`, an empty array is returned.
- `detect` and `find` are two names for the same method.
- Whereas `#select` will return all elements from the original collection that cause the block to evaluate to true, `#detect` will only return the first element that makes the block true.
- `#detect` will always return a single object, whereas `#select` will always return an array.
- `#reject` will return an array with the elements for which the block is false.

## Search Enumerables Example

```ruby
[1, 2, 3, 4, 5].select do |number|
  number.even?
end #=> [2, 4]

# In the first iteration of the block above, number will be
# assigned the value 1. Because 1.even? will return false,
# 1 will not be in the return array for this call to #select
# (same for 3 and 5). In the second iteration, number will be
# 2. Because 2.even? will return true, 2 will be in the return
# array (same for 4).

# short block form
[1, 2, 3, 4, 5].select{|i| i.even?} #=> [2, 4]
```