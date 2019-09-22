# Lesson: Yield and Blocks

## Notes

- The `yield` keyword, when used inside the body of a method, will allow you to call that method with a block of code and pass the torch to that block.
- The `yield` keyword can take parameters (or an argument) similar to the `each` method.

## Code Examples

### Example Yield Method with Arguments

```ruby
def yielding_with_arguments(num)
  puts "the program is executing the code inside the method"
  yield(num) { |i| puts i * 2 }
  puts "now we are back in the method"
end

# Output
the program is executing the code inside the method
4
now we are back in the method
```
