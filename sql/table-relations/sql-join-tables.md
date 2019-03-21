# Lesson: SQL Join Tables

## Notes

- Relational databases allow us to categorize the type of relationship that exists between the data we are storing.

### The "has many"/"belongs to" Relationship

- The "has many"/"belongs to" relationship is created through the use of foreign keys.
- The table that contains the foreign key column is the table that contains the entities that "belong to" another entity. The table that is reference via the foreign key is the parent owner entity that "has many" of something else. This relationship works because multiple entities in the "belonging" or child table can have the same foreign key.

### Join Tables and The "many-to-many" Relationship

- A join table contains common fields from two or more other tables. In this way, it creates a "many-to-many" relationship between data.
- It is conventional to name your join tables using the names of the tables you are creating the "many-to-many" relationship between.
- Each row in the join tables represents one relationship.

### Querying the Join Table

- Example that utilizes a JOIN statement to query a join table: `SELECT column(s) FROM table_one INNER JOIN table_two ON table_one.column_name = table_two.column_name WHERE table_two.column_name = condition;`