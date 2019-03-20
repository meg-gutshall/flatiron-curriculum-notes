# Lesson: `gets` CLI Input

## Notes

- Use the `gets` method and the Command Line Interface (CLI) to receive and process input from the user when running a method that accepts an argument.
- We first greet the user, then ask them for input (in this case, their name).
- We capture that input using `#gets` and use it to do something else in another method.
  - In this case, we are passing the user's input into the `#greeting` method as an argument. The greeting method then uses string interpolation to `#puts` out a personalized message.
- The return value of `gets` is the text typed into the terminal.
- Most often `gets` is followed by `.strip` or `.chomp`.
  - The `#chomp` method removes any new lines at the end of a string while the `#strip` method removes whitespace (leading and trailing) and new lines.

## Code Examples

### The CLI Pattern When Using the `#gets` Method

```ruby
puts "Hello! Welcome to the world of Ruby programming!"
puts "Please enter your name so that we can greet you more personally:"
name = gets.strip
greeting(name)
```