# Lesson: Arrays and Methods

## Notes

- The `.sort` method rearranges the contents of the array by sorting them. For string, this means alphabetically, for numerical values, this means from smallest to largest number.
  - `array.sort`
- This method does not change the return value of the array, it is meant to return a new array to be stored into another variable.
- To permanently change the unsorted array into the sorted array, you can call `sort!`: `array.sort!`
  - It's a Ruby convention that a method with the `!` will do the operation in place and then modify the receiver of the method (aka the thing to the left of the `.`).
- The `.reverse` method reverses an array.
- The `.include?` method will return a boolean of whether or not the array contains the element submitted to it inside the parentheses.
  - `array.include?(element)`
- The `.first` method will return the first element of the array.
- The `.last` method will return the last element of the array.
- The `.size` method will return the number of elements in the array.

## Code Examples

### Ruby Methods

#### String Methods

```ruby
“hello”.size => 5
“hello”.upcase => “HELLO”
“hello”.reverse => “olleh”
```

#### Number Methods

```ruby
7.5.floor => 7 # (Rounds the float down to the nearest fixnum)
7.5.ceil => 8 # (Rounds the float up to the nearest fixnum)
10.next => 11
```

#### Array Methods

```ruby
[5, 100, 234, 7, 2].sort => [2, 5, 7, 100, 234]
[1, 2, 3].reverse => [3, 2, 1]
```

### Manipulating Arrays

#### Reassigning Values

```ruby
speed_dial = [mom, dad, sister, brother]
speed_dial[2] #=> “sister”
speed_dial[2] = “boyfriend”
speed_dial #=> [mom, dad, boyfriend, brother]
```

#### Adding Items

```ruby
array = ["object1", "object2", "object3"]

# The shovel method
array << "item"
array #=> ["object1", "object2", "object3", "item"]

# The .push method
array.push("item1", "item2")
array #=> ["object1", "object2", "object3", "item1", "item2"]

# The .unshift method
array.unshift("item")
array #=> ["item", "object1", "object2", "object3"]
```

#### Removing Items

```ruby
# The .pop method
array = ["object1", "object2", "object3"]
object3 = array.pop

array #=> ["object1", "object2"]
object3 #=> object3

# The .shift method
array = ["object1", "object2", "object3"]
object1 = array.pop

array #=> ["object2", "object3"]
object1 #=> object1
```

#### Operating on Arrays

```ruby
array = ["eenie", "meenie", "miney"]

# The .reverse method
array.reverse #=> ["miney", "meenie", "eenie"]

# The .includes? method
array.include?("moe") #=> false
array.include?("eenie") #=> true
```