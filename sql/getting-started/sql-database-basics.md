# Lesson: SQL Database Basics

## Notes

### Database Structure

- Relational Databases store data in a structure we refer to as a table. We define specific columns in our table, and then we store any number of what we refer to as 'records' as rows in our database.
  - A record is information referring to one specific entity.
- Conventions when naming columns in a database:
  - Use lowercase letters
  - Use "snake_case" if the column name is multiple words

### Database Tables

- Create a database using the `sqlite3 database_name.db` command
- [Create a table with columns and data types](:note:fd11cb68-1c03-42a0-9622-c85b546d3a12)
  - First, we use the `CREATE TABLE` command to create a new table called "cats".
  - In parentheses after that, we list our columns starting with the column name (in lowercase) followed by the type of data they will be storing. Capitalizing the datatype is another SQL convention to help separate it from the name of the column.
  - **Every table we create, regardless of the other column names and data types, should be defined with an `id INTEGER PRIMARY KEY` column, including data type and primary key designation.** This indexes the table rows by number.
    - Primary keys are unique and auto-incrementing.
- Use the `.tables` command to make sure your new table was properly created.
- The `.schema` command shows the structure of the database.

### Altering A Table

- Add or remove columns with the `ALTER TABLE` statement.
  - Add a column: `ALTER TABLE cats ADD COLUMN breed TEXT;`

### Deleting A Table

- Delete a table using the `DROP TABLE` statement followed by the table name.

## Code Examples

### Create a table with columns and data types

```sql
CREATE TABLE cats (
id INTEGER PRIMARY KEY,
name TEXT,
age INTEGER
);
```