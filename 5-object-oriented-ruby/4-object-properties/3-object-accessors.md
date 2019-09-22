# Lesson: Object Accessors

## Notes

- In Ruby, a macro is like a method that instead of returning a Ruby datatype, returns more Ruby code. This code will get executed along with all the other code you have written when you run your program.
  - "Macro" is the programmer word for shortcut.
- The implementation of macros is considered metaprogramming—the writing of programs that operate on other programs.
  - Macros can be used to automate repetitive tasks.
- The usage of macros is preferred over the explicit definition of setter and getter methods, unless you need to customize the implementation of a method (i.e. defining `.name` as returning the first and last name variable combined).

### Attribute Readers, Writers, and Accessors

- The `attr_reader` macro, followed by the attribute name `:name`, creates a getter method (instead of `.name`).
- The `attr_writer` macro, followed by the attribute name `:name`, creates a setter method (instead of `.name=`).
- The `attr_accessor` can be used in place of the attribute reader (`attr_reader`) and attribute writer (`attr_writer`).

## Code Examples

### Macros vs. Explicit Methods

```ruby
# Method
class Person
  attr_writer :name
  attr_reader :name
end

# Explicit Method Definition
class Person
  
  def name=(name)
    @name = name
  end
  
  def name
    @name
  end
  
end
```

### Attribute Accessors

```ruby
class Person
  attr_writer :name
  attr_reader :name
end

# Can be rewritten as

class Person
  attr_accessor :name
end
```
