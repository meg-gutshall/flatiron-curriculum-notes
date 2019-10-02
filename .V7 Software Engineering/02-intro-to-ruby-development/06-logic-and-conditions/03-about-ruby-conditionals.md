# Lesson: About Ruby Conditionals

## Notes

- Control flow lets you tell your program what code to execute conditionally.
- There are a number of ways to tell your program to conditionally execute certain code, the basic forms of which are:
  - `if`, `else`, and `elsif` statements
  - `case` statements
  - loops
- One of the most common ways to enact control flow is the `if` statement. Whatever block of code that follows the `if` statement will get evaluated—i.e. read and enacted by the computer. If this evaluation of the `if` statement results in `true`, then the code through to the associated end statement will run.
- An `else` statement sets a "default" condition for when your `if` statement's conditional evaluates as `false`. Every condition that doesn't evaluate as `true` will instead pass through the `else` statement.
- We can cascade as many `elsif` statements as we wish, however `elsif` statements can only be used following an `if` statement, and must precede the associated `else` statement (if used).
