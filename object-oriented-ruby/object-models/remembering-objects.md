# Lesson: Remembering Objects

## Notes

- The class itself is responsible for keeping track of every instance of the class. To do this, we create a class variable.
  - Example: `@@all = []`
- The class should store an instance of itself on instantiation—when a new instance is created.
  - We can implement this by simply adding the new instance that gets created into the array stored in `@@all` inside our `#initialize` method.
- In `#initialize` we use the `self` keyword to refer to the new object that has just been created by `#new`.
  - Remember that when `#new` is called, it creates a new instance of the class and then calls `#initialize` on that new instance.
- You need to build a class method to access the contents of `@@all`.
  - Recall that to define a class method we use the `def self.method_name` syntax.

## Code Examples

### Storing Instances of A Class

```ruby
class Song          #create the class
  
  @@all = []        #create the class variable
  
  attr_accessor :name
  
  def initialize(name)
    @name = name
    @@all << self   #add instance to the class variable
  end
  
  #create a method to access the class variable
  def self.all
    @@all.each do |song|
      puts song.name
    end
  end
  
end
```