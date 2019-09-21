# Lesson: Dynamic ORMs with Inheritance

## Notes

- We can define all of the dynamic ORM methods in a super class and have a child class inherit from it so we can keep programs DRY.
- The only code that the child class needs to contain is the code to create the `attr_accessor`s specific to itself. Even that uses a method, `#column_names`, inherited from the super class.