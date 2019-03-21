# Lesson: Reading Error Messages

## Notes

### Error messages have three parts:

1. The location of the error, the “where”, which includes the file the error occurred in, the line of code with the error, and the scope of the error
2. The description of the error, the “why”,
3. And the type of error, the “who”.

### Four common error types are:

1. Name errors: Caused when a given name is invalid or undefined
2. Syntax errors: A result of incorrect syntax
3. Type errors: Happens when you try to do a mathematical operation on two objects of a different type
4. Division errors: Caused when a given number is divided by 0

- Tests are programs, written using the RSpec testing library, that are written to make sure your program is running properly.
  - Found inside the spec directory
- Each error prints out a stack trace, which points to where the code failed and attempts to follow it up the stack—that is, through the bits of code that ran leading up to the failure. You can use these stack traces to pinpoint which line(s) of code need your attention.

## Code Examples

### Example Error Message

```bash
lib/a_name_error.rb:3:in `<main>': undefined local variable or method `hello_world' for main:Object (NameError)

# The location of the error
lib/a_name_error.rb:3:in `<main>':

# The description of the error
undefined local variable or method `hello_world' for main:Object

# The type of error
(NameError)
```