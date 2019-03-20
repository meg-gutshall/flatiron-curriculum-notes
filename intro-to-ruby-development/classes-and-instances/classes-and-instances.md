# Lesson: Classes and Instances

## Notes

- A class is like a blueprint that defines how to build an object.
- A Ruby class both contains the instructions for creating new objects and has the ability to create those objects.
- Class names begin with capital letters because they are stored as Ruby constants.
  - If your class name contains two words, the name should be CamelCased.
- Once a class is defined, we can create instantiate, or create, new objects from that class.
  - Each specific version of our class is called an instance. An instance refers to the individual object produced from the class.
- Every time a new instance of a class is created, you get a return value called Ruby Object Notation.
  - The part inside the carats tells you which class your object is an instance of.
  - The part following the semicolon is called its object identifier and it basically means this is where the object lives inside your computer.
- Each instance is totally unique.

## Code Examples

```ruby
class ClassName
end

object = ClassName.new
object #=> #<ClassName:0x007fc52c2cc588>

# Ruby Object Notation: #<ClassName:0x007fc52c2cc588>
# Tells us this is an instance of ClassName
# Object Identifier: 0x007fc52c2cc588
# This is where the object lives in the computer.
```