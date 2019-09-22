# Lesson: Debugging with Pry

## Notes

- Pry is a Ruby REPL (Read, Evaluate, Print, Loop), much like IRB
  - Pry is far more flexible than IRB.
- Once you install the Pry library, you cna use the following line `binding.pry` anywhere in your code.
  - Binding is a built-in Ruby class whose objects can encapsulate the context of your current scope (variable, methods, etc.), and retain them for use outside of that context.
- Calling `binding.pry` is essentially 'prying' into the current binding or context of the code, from outside your file.
- Insert the line `binding.pry` in your code and, when run, the program will freeze at that line and turn into a REPL.
- You must write `require 'pry'` on the first line of your code to use Pry.
- Type `exit` to leave the REPL and the program will continue to execute.
