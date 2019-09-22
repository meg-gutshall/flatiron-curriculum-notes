# Lesson: Private Methods

## Notes

- Public methods are called by an explicit receiver. We can call them from outside the scope of the class declaration, like on the instance of the class or the class itself.
- Private methods cannot be called by an explicit receiver. That means we can only call private methods within the context of the defining class: the receiver of a private method is always `self`.
- Private methods are a way of encapsulating functionality within a class.
- Private methods also signal to other developers that this method is depended on by other methods in your program. It signals that they should beware of removing such a method for fear of breaking other parts of the program that they may not realize rely on it.
- `initialize` is a private method.
  - Private methods, aside from `#initialize`, are usually written with the word `private` above them.
- Since private methods are called without explicit receivers, Ruby sees the missing receiver and assumes it to be self, or the current object.
