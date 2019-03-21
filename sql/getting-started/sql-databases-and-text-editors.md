# Lesson: SQL Databases and Text Editors

## Notes

- To write SQL in our text editor and execute that SQL against a specific database, we'll create files in our text editor that have the `.sql` extension. These files will contain valid SQL code. Then, we can execute these files against our database in the command line.

### Creating A Database and Table

- Create a database in the terminal, then exit the sqlite prompt with the `.quit` command.
- Open a text editor and write your create statement. Save that file as a `.sql` extension.
- Execute that file in the command line: `sqlite3 database_name.db < create_statement.sql`
- To carry out any subsequent actions on this database, we can create new `.sql` files in the text editor and execute them in the same way as above.