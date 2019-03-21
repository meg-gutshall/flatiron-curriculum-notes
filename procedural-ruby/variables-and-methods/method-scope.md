# Lesson: Method Scope

## Notes

- Scope means that not all variables exist everywhere in a program.
- Methods in Ruby create their own scope.
  - Scope refers to the areas of your program in which certain data is available to you.
- Any local variable created outside of a method will be unavailable inside of a method. In addition, local variables created inside of a method 'fall out of scope' once you're outside the method.
- A method can't access a variable outside of the scope unless we pass it as an argument.