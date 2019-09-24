# Lesson: Preventing Record Duplication

## Notes

- To prevent record duplication, we should first check to see if the object we are trying to save already has an equivalent record in the database. If it does, we should update it. Otherwise, we can save it.

### The `#find_or_create_by` Method

- First we query the database.
  - If the record exists, the `!song.empty?` statement will return `true` and we'll use the returned values to make a new Ruby object but not save it to the database.
  - If the record does not exist, we'll save a new object instance with the `#create` method.

## Code Examples

```ruby
class Song
  
  def self.find_or_create_by(name:, album:)
    sql = "SELECT * FROM songs WHERE name = ? AND album = ?, name, album"
    song = DB[:conn].execute(sql)
    if !song.empty?
      song_data = song[0]
      song = Song.new(song_data[0], song_data[1], song_data[2])
    else
      song = self.create(name: name, album: album)
    end
    song
  end
  
end
```
