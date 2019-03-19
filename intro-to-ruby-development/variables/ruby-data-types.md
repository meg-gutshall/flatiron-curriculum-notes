# Ruby Data Types

- Ruby has six data types: booleans, symbols, numbers, strings, arrays, and hashes.
  - Call `.class` on any object to find out what type of data it is (i.e. `“hello”.class` returns a value of `=> String`)

## Strings

- A string is a sequence of characters enclosed in double or single quotes that represents textual data.
- Two ways to create a string:
  - The Literal Constructor: typing between two quotation marks (i.e. `“hello”`)
  - The Class Constructor: `String.new` creates an empty string (or you can add the value by typing `String.new(“hello”)`)

## Booleans

- In Ruby, there is no such thing as a Boolean class. Instead, every appearance, or instance, of `true` and `false` in your program are instances of TrueClass and FalseClass respectively.

## Numbers

- In Ruby, there are two types of numbers:
  - Fixnums: whole numbers
  - Floats: decimal numbers

## Symbols

- A symbol is a representation of a piece of data.
- If symbols are used multiple times in code, they will refer to the same area of memory (as opposed to strings, which which take up new areas of memory every time they are used).
- You write symbols by placing a `:` in front of the symbol name (`:this_is_a_symbol`).

## Arrays

- Arrays are collections of Ruby objects in which you can store any type of data.
- Two ways to create an array:
  - The Literal Constructor: typing any set of comma separated data enclosed in brackets (i.e. `[1, 2, 3, 4]`)
  - The Class Constructor: typing `Array.new` will create an empty array (`=> []`)

## Hashes

- Hashes are like arrays, but operate like dictionaries. Instead of a simple comma separated list, hashes are composed of key/value pairs. Each key points to a specific value––just like a word and a definition in a regular dictionary.
  - Hashes look like this: `{"i'm a key" => "i'm a value!", "key2" => "value2"}`
- Again, there are two ways to create hashes:
  - The Literal Constructor: write key/value pairs enclosed in curly braces
  - The Class Constructor: type `Hash.new`, creating an empty hash, `{}`