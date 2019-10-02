# Lesson: SQL Joins

## Notes

- A SQL JOIN clause is a way to combine rows from two or more tables, based on a common column between them.
- Relational databases allow us not only to store data that is interconnected, but to retrieve that data in ways that reflect said interconnectivity.

### Join Types

The following JOIN keywords will be crafted into `SELECT` statements to achieve the described return values:

- INNER JOIN: Returns all rows when there is at least one match in BOTH tables

```sql
SELECT column_name(s) FROM first_table INNER JOIN second_table ON first_table.column_name = second_table.column_name;
```

- LEFT JOIN: Returns all rows from the left table, and matched rows from the right table

```sql
SELECT column_name(s) FROM first_table LEFT JOIN second_table ON first_table.column_name = second_table.column_name;
```

- RIGHT JOIN: Returns all rows from the right table, and the matched rows from the left table

```sql
SELECT column_name(s) FROM first_table RIGHT JOIN second_table ON first_table.column_name = second_table.column_name;
```

- FULL JOIN: Returns all rows when there is a match in ONE of the tables

```sql
SELECT column_name(s) FROM first_table FULL OUTER JOIN second_table ON first_table.column_name = second_table.column_name;
```
