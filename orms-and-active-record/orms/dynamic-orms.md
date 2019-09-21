# Lesson: Dynamic ORMs

## Notes

- With a dynamic ORM, we can abstract all of our conventional ORM methods into flexible, abstract, and shareable methods.
- A dynamic ORM allows us to map an existing database table to a class and write methods that can use nothing more than information regarding a specific database table to:
  - Create `attr_accessors` for a Ruby class.
  - Create shareable methods for inserting, updating, selecting, and deleting data from the database table.
  - The pattern—first creating the database table and having your program do all the work of writing your ORM methods for you, based on that table—is exactly how we will develop web applications in Sinatra and Rails.

### Setting Up the Database

- In `config/environment.rb` we create the database, drop `songs` to avoid an error, then create a `songs` table.
- Use the `#results_as_hash` method to return database rows as a hash with the column names as keys instead of as an array when a `SELECT` statement is executed.

### Building `attr_accessor`s from Column Names

- The next step of building our dynamic ORM is to use the column names of the `songs` tables to dynamically create the `attr_accessor`s of our `Song` class. In order to do that, we first need to collect the column names from our `songs` table.
  - The `#pluralize` method is provided by the `active_support/inflector` code library, required at the top of `lib/song.rb`.

### Building an Abstract `#initialize` Method

- Define the `#initialize` method to take in an argument of `options`, which defaults to an empty hash. We expect `#new` to be called with a hash, so when we refer to `options` inside the `#initialize` method, we expect to be operating on a hash.
- Then we use the `#send` method to interpolate the name of each hash key as a method that we set equal to that key's value. As long as each `property` has a corresponding `attr_accessor`, this `#initialize` method will work.

### Writing Our ORM Methods

#### Saving Records in A Dynamic Manner

- In order to write a method that can `INSERT` any record to any table, we need to be able to craft the above SQL statement without explicitly referencing the `songs` table or column names and without explicitly referencing the values of a given `Song` instance.
- Therefore, we need to abstract the table name, column names, and values to use in the SQL `INSERT` statement.

## Code Examples

### Dynamic ORM Methods

```ruby
class Song

  #Create table name based on Ruby class name
  def self.table_name
    self.to_s.downcase.pluralize
  end
  
  #Identify column names from the table
  def self.column_names
    DB[:conn].results_as_hash = true

    sql = "PRAGMA table_info('#{table_name}')"

    table_info = DB[:conn].execute(sql)
    column_names = []

    table_info.each do |column|
      column_names << column["name"]
    end

    column_names.compact
  end
  
  #Create attr_accessors from the table's column names
  self.column_names.each do |col_name|
    attr_accessor col_name.to_sym
  end
  
  def initialize(options = {})
    options.each do |property, value|
      self.send("#{property}=", value)
    end
  end
  
  def table_name_for_insert
    self.class.table_name
  end
  
  def col_names_for_insert
    self.class.column_names.delete_if {|col| col == "id"}.join(", ")
  end
  
  def values_for_insert
    values = []

    self.class.column_names.each do |col_name|
      values << "'#{send(col_name)}'" unless send(col_name).nil?
    end
    values.join(", ")
  end
  
  def save
    sql = "INSERT INTO #{table_name_for_insert} (#{col_names_for_insert}) VALUES (#{values_for_insert})"

    DB[:conn].execute(sql)

    @id = DB[:conn].execute("SELECT last_insert_rowid() FROM #{table_name_for_insert}")[0][0]
  end
  
  def self.find_by_name(name)
    sql = "SELECT * FROM #{self.table_name} WJHERE name = '#{name}'"

    DB[:conn].execute(sql)
  end
  
end
```