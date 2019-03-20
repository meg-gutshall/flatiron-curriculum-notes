# Instance Methods

- We send objects messages asking them to perform an operation or task through a syntax known as "Dot Notation".
  - This separates the object and the message with a dot (`.`).
  - When we send an object a message through dot notation, we are evoking the corresponding method on the object.
- In dot notation, we call the object that received the method message the "receiver" and we call the method the "message".
- All objects respond to methods and messages.
- The `#methods` method returns an array of all the methods and messages an object responds to.
- If we place a method definition within the body of a class, that method becomes a specific behavior of instances of that class, not a generic procedure we can just call whenever we want.
  - We call the methods defined within the object's class Instance Methods because they are methods that belong to any instance of the class.
- Instance methods are not globally evocable like procedural methods. They cannot be called without an instance.