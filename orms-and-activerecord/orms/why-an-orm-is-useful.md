# Lesson: Why an ORM is Useful

## Notes

- Object Relational Mapping (ORM) is the technique of accessing a relational database using an object-oriented programming language.
- Object Relational Mapping is a way for our Ruby programs to manage database data by "mapping" database tables to classes and instances of classes to rows in those tables.
- An ORM is really just a design pattern, a conventional way for us to organize our programs when we want those programs to connect on a database.
  - The convention is this: When "mapping" our program to a database, we equate classes with database tables and instances of those classes with table rows.
  - You may also see this referred to as "wrapping" a database, because we are writing Ruby code that "wraps" or handles SQL.
- ORM cuts down on repetitious code by writing methods to abstract common behaviors.
- ORM implements conventional patterns that are organized and sensible.
  - Classes are mapped or equated with tables and instances of a class are equated to table rows.