# Lesson: ActiveRecord Associations

## Notes

### What Are ActiveRecord Associations?

- ActiveRecord associations allow us to associate models and their analogous database tables without having to write tons of code.
  - ActiveRecord associations make working with our associate objects even quicker, neater, and easier.

### How Do We Use ActiveRecord Associations?

- ActiveRecord makes it easy to implement the following relationships between models:
  - `belongs_to`
  - `has_one`
  - `has_many`
  - `has_many:through`
  - `has_one:through`
  - `has_and_belongs_to_many`
- In order to implement these relationships, we will need to do two things:
  - Write a migration that creates tables with associations.
  - Use ActiveRecord macros in the models.

### Overview of Our Example

- We'll have three models: Artists, Songs, and Genres. By writing a few migrations and making use of the appropriate ActiveRecord macros, we will be able to:
  - ask an Artist about its songs and genres
  - ask a Song about its genre and artist
  - ask a Genre about its songs and artists
- The relationships between artists, songs, and genres will be enacted as follows:
  - Artists have many songs and a song belongs to an artist
  - Artists have many genres through songs
  - Songs belong to a genre
  - A genre has many songs
  - A genre has many artists through songs

### Building Our Migrations

#### The `Song` Model

- A song will belong to an artist and belong to a genre, which means that in addition to `id` and `name` columns, it will also include `artist_id` and `genre_id` columns.
  - We will give a given song an `artist_id` value of the artist it belongs to. The same goes for genre.
  - These foreign keys, in conjunction with the ActiveRecord association macros, will allow us to write queries to get an artist's songs or genres, a song's artist or genre, adn a genre's songs and artists, entirely through ActiveRecord-provided methods on our class.

#### The `Artist` Model

- An artist will have many songs and it will have many genres through songs.
  - The songs table is the `JOIN` table.

#### The `Genre` Model

- A genre will have many songs and it will have many artists through songs.

### Building Our Associations Using ActiveRecord Macros

- A macro is a method that writes code for us (think metaprogramming).
- The class must inherit from `ActiveRecord::Base` to be able to access the macros.
- Use one of the relationship macros followed by the other class with which this one has a relationship (written as a symbol).
  - Example: `belongs_to :artist` or `has_many :genres, through: :songs`
- **The model that `has_many` is considered the parent. The model that `belongs_to` is considered the child. If you tell the child that it belongs to the parents, the parent won't know about that relationship. If you tell the parent that a certain child object has been added to its collection, both the parent and the child will know about the association.**
  - In this example, it is better to push song objects into `artist.songs` instead of assign artist objects to `song.artist`.