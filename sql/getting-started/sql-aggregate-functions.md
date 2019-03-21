# Lesson: SQL Aggregate Functions

## Notes

- Aggregate functions perform a calculation on specified values, queried from a database table. We'll craft queries that select a desired set of values from a table and then aggregate that data, in addition to clauses that will group and or order the returned data based on various conditions.

### Using Aggregators

- The average function returns the average value of a column:

```sql
SELECT AVG(column_name) FROM table_name;
```

  - Use the `AS` keyword to rename the returned column. (This is called "aliasing the return value".)
- The sum function returns the sum of all of the values in a particular column:

```sql
SELECT SUM(column_name) FROM table_name;
```

- The minimum and maximum aggregator functions return the minimum and maximum values from a specified column respectively:

```sql
SELECT MIN|MAX(column_name) FROM table_name;
```

- The count function returns the number of rows that meet a certain condition:

```sql
SELECT COUNT(column_name) FROM table_name;
```

  - We can use the `COUNT()` function to calculate the total number of rows in a table that are not `NULL`, or empty. `COUNT(*)` means count everything and will count the rows where at least one column has data in it.