# Lesson: Rails Generators

## Notes

A primary goal of the Rails team was to make it efficient to build core application functionality. The Rails system has a number of generators that will do some of the manual work for us. As nice as it is to use the generators to save time, they also provide some additional extra benefits:

- They can setup some basic specs for an application's test suite. They won't write our complex logic tests for us, but they will provide some basic examples.
- They are setup to work the same way each time. This helps standardize your code and enables your development to be more efficient since you don't have to worry as much about bugs related to spelling, syntax errors, or anything else that can occur when writing code manually.
- They follow Rails best practices, which includes RESTful naming patterns, removing duplicate code, using partials, and a number of other best of breed design patterns.

### Abusing Generators

Great tools are only great tools if they are matched with the right task. Generators should only be used when they are needed, or else there will be an abundance of unneeded code that clutters the app.

### Rails Generate

All of the Rails generators are entered as commands into the terminal and will follow this syntax: `rails generate <name of generator> <options> --no-test-framework`

- `--no-test-framework` is a flag that tells the generator not to create any tests for the newly-generated models, controllers, etc.
  - This is necessary for Learn.co labs because we don't want Rails adding additional tests on top of the test suite that already comes with the lesson.

### Different Types of Generators

Below are the main generators that Rails offers:

- Migrations
- Models
- Controllers
- Resources

### Migration Generators

Rails has a great set of migration generators with conventions that can help make managing the database schema very efficient.

#### Generate A New Migration

To generate a new migration, you can use:`rails generate migration CreatePosts` where CreatePosts is the name of your migration. The generator will create an empty migration file `timestamp_create_posts.rb` in the `db/migrate/` directory where `timestamp` is the UTC formatted date and time that the migration was generated.

- Add the posts table to the migration file:

```ruby
class CreatePosts <ActiveRecord[5.0]
  def change
    create_table :posts do |t|
      t.string :title
      t.string :description

      t.timestamps null: false
    end
  end
end
```

#### Add A Column to A Migration Table

There is a special syntactic shortcut to generate migrations that add field to a table: `rails generate migration add_published_status_to_create_posts published_status:string`

- This will generate the file `timestamp_add_published_status_to_create_posts.rb`, which will look like:

```ruby
class AddPublishedStatusToCreatePosts < ActiveRecord::Migration[5.0]
  def change
    add_column :posts, :published_status, :string
  end
end
```

#### Remove A Column from A Migration Table

We can also get rid of a column with another migration: `rails generate migration remove_published_status_from_create_posts published_status:string`

- If you open up this migration file, you will see the following code:

```ruby
class RemovePublishedStatusFromCreatePosts < ActiveRecord::Migration
  def change
    remove_column :posts, :published_status, :string
  end
end
```

- By prepending the `add_` text to the name it gave a signal to the migration generator that the purpose of this schema change will be to add a column(s) to the table.
- By appending the `_posts` text to the end of the migration name it tells Rails that the table we want to change is the `posts` table.
- After running `rake db:migrate`, our schema will be updated.

### Model Generators

