# Looping Methods

## Code Examples

### The `loop` Method

```ruby
# Will loop infinitely until you press Ctrl + C
loop do
  # Code block here  
end

# Loop will end at break point
loop do
  # Code block here
  break
end

# Can use a counter in the loop as well
counter = 0
loop do
  counter += 1
  # Code block here
  break
end
```

### The `times` Method

```ruby
integer.times do
  # Code block here
end

#=> Will run code block integer number of times
#=> return value equals integer
```

### The `while` Method

```ruby
counter = 0
while counter < integer
  # Code block here
  counter += 1
end
```

### The `until` Method

```ruby
counter = 0
until counter == integer
  # Code block here
  counter += 1
end
```
