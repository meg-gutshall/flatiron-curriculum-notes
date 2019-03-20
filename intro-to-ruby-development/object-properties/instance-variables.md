# Lesson: Instance Variables

## Notes

- Local variables can only be accessed in a specific, local environment.
  - A local variable that is defined inside one method cannot be accessed by another method.
  - We get around this limitation by using instance variables inside of our Ruby classes.
- An instance variable is a variable that is accessible in any instance method is a particular instance class.
  - We define an instance variable by prefacing the variable name with an `@` symbol.
- Instance variables hold information about an instance and can be called on throughout the class, without needing to be passed into other methods as arguments (as would be the case with local variables).

## Code Examples

```ruby
class Dog
  
  def name = (dogs_name)
    @this_dogs_name = dogs_name
  end
  
  def name
    @this_dogs_name
  end
end

lassie = Dog.new
lassie.name = "Lassie"

puts lassie.name
```