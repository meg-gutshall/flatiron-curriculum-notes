# Truthiness

- In Ruby, the boolean types are expressed directly as `true` and `false`.
  - These values help to implement flow control, which is the idea that we can tell our program to execute certain lines of code based upon certain conditions.
- The adjectives "truthy" and "falsey" are a programming convention for describing the state of being true and the state of being false.
  - In Ruby only `false` and `nil` are falsey. Everything else is truthy (yes, even `0` and an empty string (`" "`)).
- Determining truthiness: A "double-bang operator" (`!!`) will return `true` or `false` based on whether a value is truthy or falsey to begin with.