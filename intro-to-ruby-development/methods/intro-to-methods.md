# Lesson: Intro to Methods

## Notes

Methods define a new thing that your program can do. Variables are a mechanism to teach your Ruby program about data; methods teach your Ruby program about a new routine or behavior it can use. Variables are like nouns, methods are like verbs.

- You can define a method in Ruby with the `def` keyword. A method's name can begin with any lowercase letter.
- The first line, called the method signature, defines the basic properties of the method, including the name.
- Once you open a method definition with the `def` keyword, all subsequent lines in your program are considered the method's body, the actual procedure or code that your method will run every time it's called.
- You must terminate every opening `def` of a method with a corresponding `end` in order to close the method body. If you don't correctly end a method, your program will have unexpected results or break entirely because of a syntax error.
- It’s good practice is to define the method and then immediately close it before programming anything into the method as well as use indentation for the body code.
- Once you define a method, you can execute the method whenever you want by using the method name in your code.
- A common syntax convention for Ruby methods is to preface them with a # so it can be identified as a method instead an object or variable. This only applies to in writing, not in actual code.