# Object Initialization

- The `#initialize` method is used to create instances of our class with certain attributes.
  - An `#initialize` method is a method that is called automatically whenever `#new` is used.
- The initialize method is a constructor method, which is invoked upon the creation of an instance of a class and used to help define the instance of that class.

## Example of Defining an Initialize Method

```ruby
class Dog
  def initialize(breed)
    @breed = breed
  end
  
  def breed=(breed)
    @breed = breed
  end
  
  def breed
    @breed
  end
end

# Calling a new method
lassie = Dog.new("Collie")

lassie.breed #=> "Collie"
```