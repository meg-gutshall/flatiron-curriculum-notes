# Lesson: SQL Data Types

## Notes

- We've learned that when we create a table, we need to include a name for it as well as define at least one column. We define the columns in a `CREATE` statement by including a name and a datatype to let SQL know the kind of data we will be storing there. The practice of explicitly declaring a type is known as "typing".
  - Typing not only informs our database of the kind of data we plan to store in a column but it also restricts it.
- Because databases are designed to store large amounts of data, they are very concerned with storing, accessing, and acting upon that data as efficiently and normally as possible.
- Typing gives us the ability to perform all kinds of operations with predictable results.

### Data Types

- Different database systems have different data types available.
- SQLite only has four basic categories of data types:
  - TEXT: Any alphanumeric characters which we want to represent as plain text
  - INTEGER: Anything we want to represent as a whole number
  - REAL: Anything that's a decimal (up to 15 characters long)
    - In other database systems this is called "double precision".
  - BLOB: Binary data
- To increase its compatibility with other engines, SQLite allows the programmer to use other common data types outside of the four mentioned above.
