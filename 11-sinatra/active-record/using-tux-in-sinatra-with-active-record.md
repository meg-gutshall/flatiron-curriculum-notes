# Lesson: Using Tux in Sinatra with Active Record

## Notes

- Tux is an incredible Ruby gem that lets you access your database and perform all CRUD operations on it through the terminal. It also loads a full environment in the console that allows you to see all routes and views. Primarily, you'll use Tux to make sure your database is set up properly, play around with Ruby objects, and make sure your Active Record associations are working properly.

### Setup

- Include `tux` in your Gemfile and run `bundle install` in terminal.

### Using Tux

- Set up your `User` model and migration-and make sure you actually run the migration to create the user table.
- To use Tux, enter `tux` into the terminal. Once Tux is loaded, regular terminal commands won't work, but you cna use Ruby and Active Record methods.
- Once you're done, just exit Tux by typing `exit`.