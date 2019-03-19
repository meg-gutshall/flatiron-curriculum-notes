# Methods and Arguments

- To add arguments to a method, you specify them in the method signature––the line that starts with `def`. Simply add parentheses after the name of the method and create a placeholder name for your argument.
- Arguments create new local variables that can be used within the method.
- You can define a method to accept as many arguments as you want.
- Once you define arguments for a method, they become required when you invoke or call the method. If you define a method that accepts a singular argument, when you call that method, you must supply a value for that argument, otherwise, you get an `ArgumentError`.
- In Ruby, all arguments are required when you invoke the method. Additionally, a method defined to accept one argument will raise an error if called with more than one argument.
- Even though we don’t have the value of the argument when creating a method, the bareword that we use as the argument's name in the method signature becomes a local variable within the method. Through that variable we can reference the value of the argument supplied at invocation.