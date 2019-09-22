# Lesson: Mapping Database Tables to Ruby Objects

## Notes

- We don't store Ruby objects in the database, and we don't get Ruby objects back from the database. We store raw data describing a given Ruby object in a table row and when we want to reconstruct a Ruby object from the stored data, we select that same row in the table.
- When we query the database, it is up to us to write the code that takes that data and turns it back into an instance of the appropriate class. We will be responsible for translating the raw data that the database sends into Ruby objects that are instances of a particular class.
- Three methods are needed to access data and convert it into Ruby objects.

### `.new_from_db`

- The first thing we need to do is convert what the  database gives us into a Ruby object.
  - The database will return an array of data for each row.

### `Song.all`

- Now we return all the songs in the database by storing the `SELECT * FROM songs` SQL query to a variable called `sql` and then making  call to the database using `DB[:conn]` with the `execute` method that accepts the `sql` variable as an argument.
- This will return an array of rows from the database that match our query. Now all we have to do is iterate over each row and use the `self.new_from_db` method to create a new Ruby object for each row.

### `Song.find_by_name`

- This one is similar to `Song.all` with the small exception being that we have to include a name in our SQL statement. To do this, we use a question mark where we want the `name` parameter to be passed in, and we include `name` as the second argument to the `execute` method.

## Code Examples

```ruby
class Song
  
  def self.new_from_db(row)
    new_song = self.new #same as running Song.new
    new_song.id = row[0]
    new_song.name = row[1]
    new_song.length = row[2]
    new_song #return the newly created instance
  end
  
  def self.all
    sql = "SELECT * FROM songs"

    DB[:conn].execute(sql).map do |row|
      self.new_from_db(row)
    end
  end

  def self.find_by_name(name)
    sql = "SELECT * FROM songs WHERE name = ? LIMIT 1"

    DB[:conn].execute(sql, name).map do |row|
      self.new_from_db(row)
    end.first
  end

end
```
