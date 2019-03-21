# Lesson: Hash Iteration

## Notes

### The `#each` Method

- We can use `#each` to iterate over key/value pairs.
- When we iterate over a hash, the `#each` method yields the key/value pair together into the block. Inside that block, you have access to the key and the value, and can manipulate either one or both.
  - Remember: `#each` returns the original collection on which you are calling the method.

### The `#collect` Method

- We use `#collect` to iterate over a collection of data and return a collection of data therein.
  - `#collect` and `#map` can be used interchangeably.
- When working with hashes, we'll most often see `#collect` used to collect the values of the hash's keys and/or collect data that we've operated on over the course of an iteration.

## Code Examples

### The `each` Method with Hashes

```ruby
hash = {key1: "value1", key2: "value2"}

hash.each do |key, value|
  puts "#{key}: #{value}"
end

# When run:
key1: value1
key2: value2
=> {:key1 => "value1", :key2 => "value2"}
```