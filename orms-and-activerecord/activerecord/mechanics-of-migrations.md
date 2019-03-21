# Lesson: Mechanics of Migrations

## Notes

- Migrations are a convenient way for you to alter your database in a structured and organized manner. They also allow you to describe these transformations using Ruby. The great thing about this is that (like most of ActiveRecord's functionality) it is database independent.
- Another way to think of migrations is like version control for your database. You might create a table, add some data to it, and then make some changes to it later on. By adding a new migration for each change you make to the database, you wont lose any data you don't want to, and you can easily revert changes.
  - Executed migrations are tracked by ActiveRecord in your database so that they aren't used twice.

### Setting Up Your Migration

1. Create a directory called `db` at the top level, then `cd` into the `db` directory and use the `mkdir` command to create a `migrate` directory.
2. In the `db/migrate` directory, create a file called `01_create_artists.rb`.

### ActiveRecord Migration Methods

- We create a class called `CreateArtists` that inherits from ActiveRecord's `ActiveRecord::Migration` module. Within the class we have an `up` method to define the code to execute when the migration is run and a `down` method to define the code to execute when the migration is rolled back.
  - Think of it like "do" and "undo".
- However, another method, `change`, is more common for basic migrations. It works for the majority of cases, where ActiveRecord knows how to reverse the migration automatically.

### Creating A Table

- Just use the `create_table` method and pass it the name of the table we want to create as a symbol.
- Create columns by declaring the data type of the column followed by the name of the column as a symbol.
  - ActiveRecord generates the id column and primary key as well as auto-increments each row.

### Running Migrations

- The simplest way to run our migrations is through a Rake task that we're given through the `activerecord` gem.
- Use the `establish_connection` method from `ActiveRecord::Base` to connect to our `artists` database, which will be created in the migration via SQLite3 (the adapter). Then run `rake db:migrate`.

### Using Migrations to Manipulate Existing Tables

- Generally, the best practice for database management is creating new migrations to modify existing tables. That way, we have a clear, linear record of all of the changes that have led to our current database structure.
- ActiveRecord executes files in alpha-numerical order. We add numbering at the beginning of each filename to make sure that our migrations execute in order.