# Lesson: Mapping Ruby Classes to Database Tables

## Notes

### Mapping A Class to A Table

- When building an ORM to connect our Ruby program to a database, we equate a class with a database table and the instances that the class produces to rows in that table.
  - In building an ORM, it is conventional to pluralize the name of the class to create the name of the table.

#### Creating the Database

- It is the responsibility of our program as a whole to create and establish the database. Accordingly, you'll see our Ruby programs set up such that they have a `config` directory that contains an `environment.rb` file.
  - In the `environment.rb` file, we set up a constant that is equal to a hash that contains our connection to the database: `DB = {conn: SQLite3::Database.new("db/music.db")}`
  - In the `lib/song.rb` file, we can access the `DB` constant and the database connection it holds: `DB[:conn]`

#### Creating the Table

- To create a songs tables, we'll write a class method in our `Song` class.
- To "map" our class to a database table, we will create a table with the same name as our class and give that table column names that match the `attr_accessor`s of our class.
- **The `id` Attribute**
  - When we create a new song with the `Song.new` method, we do not set that song's id. A song gets an `id` only when it gets saved in the database. We therefore set the default value of the `id` argument that the `#initialize` method takes equal to `nil`, so that we can create new song instances that do not have an `id` value.
- **The `.create_table` Method**
  - A class method is used to create the table because it's the job of the class as a whole to create the table that it is mapped to.
  - Use a heredoc to create a string that runs on multiple lines: `<<-` + `special word meaning "End of Document"` + `the string, on multiple lines` + `special word meaning "End of Document"`

### Mapping Class Instances to Table Rows

- We are not saving Ruby objects in our database, we are going to take the individual attributes of a given instance and save those attributes that describe an individual song to the database as one, single row.

#### Inserting Data into A Table with the `#save` Method

- Let's build an instance method, `#save`, that saves a given instance of our `Song` class into the songs table of our database. In order to `INSERT` data into our songs table, we need to craft a SQL `INSERT` statement.
- Bound parameters protect our program from getting confused by SQL injections and special characters. Instead of interpolating variables into a string of SQL, we are using the `?` characters as placeholders. Then, the special magic provided to us by the SQLite3-Ruby gem's `#execute` method will take the values we pass in as an argument and apply them as the values of the question marks.
- In doing this, our `#save` method inserts a record into our database that has the name and album values of the song instance we are trying to save. We are not saving the Ruby object itself, we are creating a new row in our songs table that had the values that characterize that song instance.
  - Notice that we didn't insert an ID number into the table with the above statement. Remember that the `INTEGER PRIMARY KEY` datatype will assign and auto-increment the id attribute of each record that gets saved.

### Creating Instances vs. Creating Table Rows

- The moment in which we create a new `Song` instance with the `#new` method is different than the moment in which we save a representation of that song to our database.
  - The `#new` method creates a new instance of the song class—a new Ruby object. The `#save` method takes the attributes that characterize a given song and saves them in a new row of the songs table in our database.
  - We don't want to force our objects to be saved every time they are created, or make the creation of an object dependent upon/always coupled with saving a record to the database.

#### Giving Our `Song` Instance an `id`

- When we `INSERT` the data concerning a particular `Song` instance into our database table, we create a new row in that table.
- As each record gets inserted into the database, it is given an ID number automatically.
- We want our instance to completely reflect the database row it is associated with so that we can retrieve it from the table later on with ease. Once the new row with the instance's data is inserted into the table, let's grab the `ID` of that newly inserted row and assign it to be the value of the instance's `id` attribute.
  - At the end of our `save` method, we use a SQL query to grab the value of the `ID` column of the last inserted row, and set that equal to the given song instance's `id` attribute.

#### The `#create` Method

- Any time we see the same code being used again and again, we think about abstracting that code into a method, which is why we'll write the `#create` method to wrap the code to create a new `Song` instance and save it.
  - The `#create` method uses keyword arguments.

If you delete the Ruby object, the database will not change at all until the record is deleted and vice versa.

## Code Examples

### Mapping Ruby Classes to Database Tables

```ruby
class Song
  attr_accessor :name, :album, :id
  
  #Create new Song instance
  def initialize(name, album, id = nil)
    @id = id
    @name = name
    @album = album
  end
  
  #Create songs table in database
  def self.create_table
    sql = "CREATE TABLE IF NOT EXISTS songs (id INTEGER PRIMARY KEY, name TEXT, album TEXT)"

    DB[:conn].execute(sql)
  end

  #Save Song instance's data into songs table row
  def save
    sql = "INSERT INTO songs (name, album) VALUES (?, ?)"

    DB[:conn].execute(sql, self.name, self.album)

    #Assign id attribute to Song instance
    @id = DB[:conn].execute("SELECT last_insert_rowid() FROM songs")[0][0]
  end

  def self.create(name:, album:)
    song = Song.new(name, album)
    song.save
    song
  end

end
```