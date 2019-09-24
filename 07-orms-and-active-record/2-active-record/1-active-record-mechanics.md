# Lesson: Active Record Mechanics

## Notes

- Active Record is a Ruby gem, meaning we get an entire library of code just by running `gem install activerecord` or by including it in our `Gemfile`.
- To execute sql code, now we write it like this: `ActiveRecord::Base.connection.execute(sql)`
- To add Active Record's `Base` methods to your class, inherit from `ActiveRecord::Base`. Now your class has a whole bunch of new methods available to it that are built into Active Record.
  - `.column_names`: Retrieve a list of all the columns in the table
  - `.create`: Create a new entry of your class in the database (aka add a row)
  - `.find`: Retrieve an entry from the database by `id`
  - `.find_by`: Find by any attribute
  - `attr_accessors`: You can get or set attributes of an instance of your class once you've retrieved said attribute
  - `#save`: Save changes to the database

## Code Examples

## Connect to A Database

```ruby
connection = ActiveRecord::Base.establish_connection(
  :adapter => "sqlite3",
  :database => "db/students.sqlite"
)
```
