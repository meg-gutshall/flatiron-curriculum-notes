# Lesson: Ternary Operators and Statement Modifiers

## Notes

### Ternary Operator

- The ternary operator (`?:`) is another type of comparison operator that is used in the context of `if` and `else` statements.
  - Not the best choice for an `if` statement that requires `elsif`.
- The code before the `?` is evaluated as a boolean expression. If it return true, the code on the left side of the `:` will run, otherwise the code on the right will run.
- Example: `conditional ? action_if_true : action_if_false`
- The ternary operator shortens simple `if` statements.

### Statement Modifier

- A statement modifier allows you to put a conditional at the end of a statement.
- Accepts `if`, 'while', and `unless` (plus any other conditionals).