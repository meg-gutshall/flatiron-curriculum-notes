# Lesson: Active Record Setup in Sinatra

## Notes

### Adding Gems

- First, we'll add three gems to allow us to use Active Record:
  - `activerecord` (version `4.2.5`) gives us access to database mapping and association methods
  - `sinatra-activerecord` gives us access to Rake tasks
  - `rake`, short for "ruby make", is a package that lets us quickly create files and folders, and automate tasks such as database creation
- We'll add two gems to our development group:
  - `sqlite3` is our database adapter gem which allows our Ruby application to communicate with a SQL database
  - `tux` will give us an interactive console that pre-loads our database and Active Record relationships for us

### Setting Up A Database Connection

- Write a block of code in the `environment.rb` file that configures the environment's database to direct to a specific file we set (see database connection example below).

### Making A Rakefile

- We define our Rake tasks in our `Rakefile`, stored in the root of our project directory and required in our `environment.rb` file.
  - Also require `sinatra/activerecord/rake` in the environment file in order to retrieve the Rake tasks from the `sinatra-activerecord` gem.

## Code Examples

### Database Connection

```ruby
configure :development do
  set :database, 'sqlite3:db/database.db'
end
```