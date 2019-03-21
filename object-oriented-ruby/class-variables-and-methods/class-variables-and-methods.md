# Lesson: Class Variables and Methods

## Notes

- All objects are bundles of data and logic—or attributes and behavior.
  - We understand this to be true of instances of a class.
  - Each instance contains attributes or properties as well as methods that can enact behaviors.
- When a class has its own variables and methods, they're called class variables and class methods.
- An instance variable is responsible for holding information regarding an instance of a class and is accessible only to that instance of the class. A class variable is accessible to the entire class—it has class scope.
  - A class method is a method that is called on the class itself, not on the instances of that class.
  - Class variables store information regarding the class as a whole and class methods enact behaviors that belong to the whole class, not just to individual instances of that class.
- A class variable looks like this: `@@variable_name`
- A class method is defined like this: `def self.class_method_name #some code end`
  - The `self` keyword refers to the entire class itself, not to an instance of the class. In this case, we are inside the class only, not inside an instance method of the class. We are in the class scope, not the instance scope.