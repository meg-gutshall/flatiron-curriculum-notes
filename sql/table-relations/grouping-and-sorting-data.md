# Lesson: Grouping and Sorting Data

## Notes

- We can tell our SQL queries and aggregate functions to group and sort our data using a number of clauses to narrow our search criteria as well as to order and group it.
- `ORDER BY()` will automatically sort the returned values in ascending order. Use the `DESC` keyword to sort in descending order.
- The `LIMIT` keyword specifies how many of the records resulting from the query you'd like to actually return.
- The `GROUP BY()` keyword is very similar to `ORDER BY()`. The only difference is that `ORDER BY()` sorts the resulting data set of basic queries while `GROUP BY()` sorts the result sets of aggregate functions.

```sql
SELECT column_name, aggregate_function(column_name) FROM table_name WHERE column_name operator value GROUP BY column_name;
```

- The `HAVING` clause compares aggregates to other values, just how the `WHERE` clause can be used with non-aggregates.
  - The difference between the `HAVING` and `WHERE` clause in SQL is that the `WHERE` clause can not be used with aggregates but the `HAVING` clause can. `HAVING` filters out groups of rows created by `GROUP BY` and `WHERE` filters out rows. Another way to think of it is that the `HAVING` clause is an additional filter to the `WHERE` clause.
  - Also note syntax differences: `HAVING` is after `GROUP BY` and `WHERE` is before `GROUP BY`.
- Changing this order will produce a syntax error:

```sql
SELECT, FROM, JOIN, ON, WHERE, GROUP BY, HAVING, ORDER BY, LIMIT
```