# Lesson: SQL Intro and Installation

## Notes

Create a new database file:

```sql
sqlite3 [db_name].db
```

The terminal should then display:

```sql
SQLite version X.X.X yyyy-mm-dd hh:mm:ss
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
```

This is the sqlite prompt.

Create a database table:

```sql
sqlite> create table [table_name](id);
sqlite> .quit
```

**Tip:** All SQL statements that you write in your terminal, inside the sqlite prompt, `sqlite3>`, must be terminated with a semi-colon `;`. If you hit enter without adding a semi-colon to the end of your line, you must add `;` on the new line and hit enter again. The only command the doesn't require, and in face doesn't even work with, a `;` is the `.quit` command.

`.help` gives you a complete list of commands.