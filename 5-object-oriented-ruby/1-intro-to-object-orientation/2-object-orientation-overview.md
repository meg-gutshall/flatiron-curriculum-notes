# Lesson: OO Ruby Video: Object Orientation Overview

## Notes

- When a method is automatically fired upon initialization, it's called a hook (or callback or life cycle event).
- You can only call methods on objects in Ruby.
- Instance variables have an `@` in front of them, signifying that the scope of the variable is to the instance itself.
- When you assign the instance variable the value of a local variable, it's called casting.
- Use an attribute accessor to quickly define reader and writer methods
  - Example: `attr_accessor :name, :age, :location, :job`
  - Attribute accessors always define methods in pairs (read and write).
- Make a new class method by using `self` with a class variable, defined by `@@` in front of the variable.
- The element to the left of the dot in a method is always the receiver of that method.
  - Sometimes there is no element to the left of the method. This is called an implicit receiver.
    - Explicit receiver: `self.method`
    - Implicit receiver: `method`
- The downside of using the implicit receiver is that local variables always take precedence over method calls so if there's a value assigned to your method, the program may run it as a local variable instead of a method.
  - In these cases, use `self.method`.
- The scope accessor (`::`) allows you to reach inside a class and pull out a constant. This is called a Class Constant.
  - Example: `Class::CONSTANT`
  - If you need to display the constant a lot, build it into a method instead of using the scope accessor.
- Whatever code is located in your class body gets executed at runtime as Ruby is reading it unless it is a method, which will only run when it's evoked.
- You can define a method on an object itself explicitly.
  - Example: `def object.method #code end`
  