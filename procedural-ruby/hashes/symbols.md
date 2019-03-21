# Lesson: Symbols

## Notes

- A symbol is a keyword that starts with a colon (`:`) and can't be changed.

- Symbols vs. strings
  - Strings are mutable, meaning that we can manipulate them in various ways by adding, removing, or replacing characters. Every time you create a new string, it creates a new object in memory, even if the string text is identical to another one you've already created.
  - The symbol is immutable, meaning that its state can't be modified after it is created and it will always be the same size in memory.
    - Unlike the string, the same symbol can be referenced many times and will always point to the same object, using less memory than a string.
- Since keys do not need to be mutable, and since mutable objects like strings take up more space in memory, we use immutable, memory-saving symbols as hash keys.
- When writing key/value pairs when the key is a symbol, use the following syntax: `my_hash = {symbol_key: "New value"}`