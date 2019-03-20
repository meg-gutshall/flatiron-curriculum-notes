# Lesson: Default Arguments

## Notes

- In order to define a method that optionally takes in an argument, we define our method to take in an argument with a default value. By defining our method with default arguments, we make it possible to call the method with optional arguments, i.e. with or without arguments.
- It is possible to use multiple default arguments in the same method or a combination of required and default arguments in the same method.

## Code Examples

```ruby
def greeting(name)
  "Hello #{name}"
end
```