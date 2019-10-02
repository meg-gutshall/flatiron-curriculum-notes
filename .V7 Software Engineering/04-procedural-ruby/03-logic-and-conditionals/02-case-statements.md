# Lesson: Case Statements

## Notes

- A case statement is a powerful tool to run multiple conditions against one value.
- We need three things to create a case statement:
  - A value
  - One or more conditions to compare to the value
  - The code we want to run if that condition is met
- This is used when an `if` statement becomes too complex.

## Code Examples

### Writing A Case Statement

```ruby
case greeting
  when "unfriendly_greeting"
    puts "What do you want!?"
  when "friendly_greeting"
    puts "Hi! How are you?"
end
```
