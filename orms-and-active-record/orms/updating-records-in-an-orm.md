# Lesson: Updating Records in an ORM

## Notes

- In our Ruby ORM, where attributes of given Ruby objects are stored as an individual row in a database table, we will need to retrieve these attributes, reconstitute them into a Ruby object, make changes to that object using Ruby methods, and then save those (newly updated) attributes back into the database.
- In order to update a record, we must first find it, then use the `#update` method.

### The `#update` Method

- The best way to update a record is to update all the attributes. That way, we will catch any changed attributes, while the unchanged ones will stay the same.
- We do this through using the primary key ID of a database record and the `id` attribute of its analogous Ruby object.

### Identifying Objects and Records Using ID

- We need a way to select a Ruby object's analogous table row using some fixed and unique attribute. Song records in the database table have a unique `id`, and our `Song` instances have an `id` attribute. Recall that we have been setting the `id` attribute of individual songs directly after the data regarding that song gets inserted into the database table, right at the end of our `#save` method.
- The unique `id` number of a `Song` instance should come from the database. When a song record gets inserted into the database, that row automatically gets assigned a unique ID number. We need to grab that ID number from the database record and assign it to the `Song` instance's `id` attribute.

#### Assigning Unique IDs on `#save`

- The `Song` instance gets assigned a unique `id` right after we `INSERT` it into the database. At that point, its equivalent database record will have a unique ID in the ID column. We want to grab that ID and use it to assign the `Song` object its `id` value.

### Using `id` to Update Records

- Our `#update` method should identify the correct record to update based in the unique ID that both the song Ruby object and the songs table row share.

### Refactoring our `#save` Method to Avoid Duplication

- We need our `#save` method to check to see if the object it is being called on has already been persisted. If so, don't `INSERT` a new row into the database, simply update an existing one.
  - We know that an object has already been persisted if it has an `id` that is not `nil`.

## Code Examples

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

  #Save Song instance's data into songs table row if not already saved
  def save
    if self.id
      self.update
    else
      sql = "INSERT INTO songs (name, album) VALUES (?, ?)"

      DB[:conn].execute(sql, self.name, self.album)

      #Assign id attribute to Song instance
      @id = DB[:conn].execute("SELECT last_insert_rowid() FROM songs")[0][0]
    end
  end

  def self.create(name:, album:)
    song = Song.new(name, album)
    song.save
    song
  end
  
  #Update a database record
  def update
    sql = "UPDATE songs SET name = ?, album = ? WHERE id = ?"
    DB[:conn].execute(sql, self.name, self.album, self.id)
  end

end
```