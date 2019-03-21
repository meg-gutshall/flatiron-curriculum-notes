# Lesson: Basic SQL Queries

## Notes

### What Is A SQL Query?

The term "query" refers to any SQL statement that retrieves data from your database.

- Format the output of your select statements with options (see example below)

### `ORDER BY`

This modifier allows us to order the table rows returned by a certain `SELECT` statement: `SELECT column_name FROM table_name ORDER BY column_name ASC|DESC;`

- When using `ORDER BY`, the default is to order in ascending order.

### `LIMIT`

`LIMIT` is used to determine the number of records you want to return from a dataset. It can be used in conjunction with `ORDER BY` to select extremes from a database table.

- Example: `SELECT * FROM cats ORDER BY age DESC LIMIT 1;`

### `BETWEEN`

Selects data between specified values: `SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2;`

### `NULL`

Add missing values using the `NULL` keyword: `INSERT INTO cats (name, age, breed) VALUES (NULL, NULL, "Tabby");`

### `COUNT`

SQL aggregate functions are SQL statements that retrieve minimum and maximum values from a column, sum values in a column, get the average of a column's values, or count a number of records that meet certain conditions. `COUNT` will count the number of records that meet a certain condition: `SELECT COUNT([column name]) FROM [table name] WHERE [column name] = [value];`

### `GROUP BY`

`GROUP BY` groups your results by a given column.

### A Note on `SELECT`

SQLite allows us to explicitly state the tableName.columnName we want to select. This is particularly useful when we want data from two different tables.

## Code Examples

### Format Query Output

```sql
.headers on       # output the name of each column
.mode column     # now we are in column mode, enabling us to run the next two .width commands
.width auto      # adjusts and normalizes column width
# or
.width NUM1, NUM2 # customize column width
```