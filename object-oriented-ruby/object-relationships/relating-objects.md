# Lesson: Relating Objects

## Notes

- Object-oriented programming is meant to model real-world environments.
- A "belongs to" relationship sets up a one-to-one connection with another Class, such that each instance of the declaring Class "belongs to" one instance of the other Class.
- A "has many" relationship indicates a one-to-many connection with another Class. This relationship is often found on the "other side" of a "belongs to" relationship. This relationship indicates that each instance of the Class has zero or more instances of another Class.
- The inverse of the "belongs to" relationship is the "has many" relationship.

### The `has many` Relationship

- Use an array to store a collection of data in a "has many" relationship.
  - The given instance should be initialized with an empty array (in the form of an instance variable)
    - Example: `@array = []`
- Write a method that adds the associated instances to the array.

### Object Reciprocity

- When the "belongs to" instance is added to the "has many" array, there need to be reciprocity. In other words, the "belongs to" instance needs to be told it belongs to that particular "has many" instance. This is often accomplished by using `self`.

### Collaborating Objects

- Two classes don't need to have a relationship to collaborate.

## Code Examples

### The `has many` Relationship: Song and Artist

```ruby
# Songs belong to artists

class Song
  attr_accessor :title, :artist
  
  def initialize(title)
    @title = title
  end
  
  # Access artist name
  def artist_name
    self.artist.name
  end
  
end

roses.artist_name
#=> "Kanye West"
```

```ruby
# Artists have many songs

class Artist
  attr_accessor :name, :genre
  
  def initialize(name, genre)
    @name = name
    @genre = genre
    # Use an array to store song instances
    @songs = []
  end
  
  # Create a new song and add to the artist's collection
  def add_song_by_name(name, genre)
    song = Song.new(name, genre)
    @songs << song
    song.artist = self
  end
  
  # Add songs to the array
  def add_song(song)
    @songs << song
    # Assign artist to the song
    song.artist = self
  end
  
  # Show songs
  def songs
    @songs
  end
  
end

kanye = Artist.new("Kanye West")

roses = Song.new("Roses", "rap")
gone = Song.new("Gone", "rap")

kanye.add_song("Roses")
kanye.add_song("Gone")

kanye.songs
#=> [#<Song:id @name="Roses", @genre="rap">, #<Song:id @name="Gone", @genre="rap">]

roses.artist.name
#=> "Kanye West"
```

### The `belongs to` Relationship: Song and Artist

```ruby
# Songs belong to artists

class Song
  attr_accessor :title, :artist
  
  def initialize(title)
    @title = title
  end
  
end
```

```ruby
# Artists have many songs

class Artist
  attr_accessor :name, :genre
  
  def initialize(name, genre)
    @name = name
    @genre = genre
  end
  
end

sublime = Artist.new("Sublime", "ska punk")
wrong_way = Song.new("Wrong Way")

wrong_way.artist = sublime

wrong_way.artist.genre
#=> "ska punk"
wrong_way.artist.name
#=> "Sublime"
```

### Collaborating Objects: Song and Artist

```ruby
class Song
  attr_accessor :title
  
  def self.new_by_filename(filename)
    song = self.new
    song.title = filename.split(" - ")[1]
    song
  end
  
  def artist_name=(name)
    if (self.artist.nil?)
      self.artist = Artist.new(name)
    else
      self.artist.name = name
    end
  end
  
end
```

```ruby
class Artist
  attr_accessor :name
  
  def initialize(name)
    @name = name
  end
  
end
```

```ruby
class MP3Importer
  
  def import(list_of_filenames)
    list_of_filenames.each do |filename|
      Song.new_by_filename(filename)
    end
  end
  
end
```