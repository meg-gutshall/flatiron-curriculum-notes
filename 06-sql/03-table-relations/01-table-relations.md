# Lesson: Table Relations

## Notes

### Relational Databases

- A relational database is a database structured to recognize relations among stored items of information.
- A relational database will allow us to store representations of our Ruby objects and preserve the relationships between those objects when we store them.

### Relational Database Structure

- Different objects are stored in their own tables.
- Relationships between tables are established by using a foreign key column, which uses the primary key of a different table to refer to a member of that table.
  - Primary keys are used as foreign keys in other tables because they're always unique.

### Relating Tables with Foreign Keys

- Since SQL doesn't have an array data type, relations are in one direction.
- The thing that "has many" is considered to be the parent. The thing that "belongs to" we'll call the child. The child table gets the foreign key column, the value of which is the primary key of that data's/row's parent.