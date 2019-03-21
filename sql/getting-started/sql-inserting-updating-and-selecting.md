# Lesson: SQL Inserting, Updating, and Selecting

## Notes

### The `INSERT INTO` Command

We use the `INSERT INTO` command, followed by the name of the table to which we want to add data. Then, in parentheses, we put the column names that we will be filling with data. This is followed by the `VALUES` keyword, which is accompanied by a parentheses enclosed list of values that correspond to each column name.<br>
**Important:** Note that we didn't specify the "id" column name or value. Since we created the table with an "id" column whose type is `INTEGER PRIMARY KEY`, we don't have to specify the id column values when we insert data. Primary Key columns are auto-incrementing. As long as you have defined an id column with a data type of `INTEGER PRIMARY KEY`, a newly inserted row's id column will be automatically given the correct value.

### Selecting Data

We use the `SELECT` statement to retrieve database data, or rows. A basic `SELECT` statement works like this:

```sql
SELECT [names of columns we are going to select] FROM [table we are selecting from];
```

- To get data from every column in the table, use a special selector known as the "wildcard" `*` (ex. `SELECT * FROM cats`)
- To select only unique values, use the `DISTINCT` keyword (ex. `SELECT DISTINCT name FROM cats`)

### Selecting Data Based on Conditions

We can use the `WHERE` keyword to select data based on specific conditions:

```sql
SELECT * FROM [table name] WHERE [column name] = [some value];
```

- We can also use comparison operators, like `<` or `>` to select specific data.

### Updating Data

To update or change data in our table rows, we use the `UPDATE` keyword:

```sql
UPDATE [table name] SET [column name] = [new value] WHERE [column name] = [value];
```

- The `UPDATE` statement uses a `WHERE` clause to grab the row you want to update.

### Deleting Data

To delete table rows, we use the `DELETE` keyword:

```sql
DELETE FROM [table name] WHERE [column name] = [value];
```