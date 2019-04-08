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

The model generator creates the core code needed to create a model and associated database table without adding a lot of bloat to the application. Let's add a new model to the app called `Author` with columns `name`, `genre`, and `bio`. We can use the model generator with the following CLI command:

```bash
rails generate model Author name:string genre:string bio:text
```

Running the generator will create the following files for us:

```bash
invoke  active_record
create    db/migrate/20151127225446_create_authors.rb
create    app/models/author.rb
```

At a high level, the has created:

- A database migration that will add a table and add the columns `name`, `genre`, and `bio`
- A model file that will inherit from `ActiveRecord::Base`

After running `rake db:migrate`, it will add the table to the database schema.

### Controller Generators

Controller generators are great if you are creating static views or non-CRUD-related features. Let's create an `admin` controller that will manage the data flow and view rendering for our admin dashboard pages:

```bash
rails generate controller admin dashboard stats financials settings
```

This will create a ton of code! Below is the full list:

```bash
create  app/controllers/admin_controller.rb
route   get 'admin/settings'
route   get 'admin/financials'
route   get 'admin/stats'
route   get 'admin/dashboard'
invoke  erb
create    app/views/admin
create    app/views/admin/dashboard.html.erb
create    app/views/admin/stats.html.erb
create    app/views/admin/financials.html.erb
create    app/views/admin/settings.html.erb
invoke  helper
create    app/helpers/admin_helper.rb
invoke  assets
invoke    coffee
create      app/assets/javascripts/admin.js.coffee
invoke    scss
create      app/assets/stylesheets/admin.css.scss
```

Here's a high level list of what was created:

- A controller file that will inherit from `ApplicationController`
- A set of routes to each of the generator arguments: `dashboard`, `stats`, `financials`, and `settings`
- A new directory for all of the view templates along with a view template file for each of the controller actions that we declared in the generator command
- A view helper method
- A Coffeescript file for specific JavaScripts for that controller
- A `scss` file for the styles for the controller

Controller generators shouldn't be used for creating CRUD-based features because it would automatically create wasted code. The view templates for `create`, `update`, and `destroy` would need to be removed immediately and they would also be setup with `get` HTTP requests, which would not work at all.

### Resource Generators

If you are building an API, using a frontend MVC framework, or simply want to manually create your views, the `resource` generator is a great option for creating the code. Let's build the `Account` controller here:

```bash
rails generate resource Account name:string payment_status:string
```

This creates quite a bit of code for us. Below is the full list:

```bash
invoke  active_record
create    db/migrate/20170712011124_create_accounts.rb
create    app/models/account.rb
invoke  controller
create    app/controllers/accounts_controller.rb
invoke    erb
create      app/views/accounts
invoke    helper
create      app/helpers/accounts_helper.rb
invoke    assets
invoke      coffee
create        app/assets/javascripts/accounts.js.coffee
invoke      scss
create        app/assets/stylesheets/accounts.css.scss
invoke  resource_route
route     resources :accounts
```

Below is a list of what our app now contains:

- A migration file that will create a new database table for the attributes passed to the generator
- A model file that inherits from `ActiveRecord::Base`
- A controller file that inherits from `ApplicationController`
- A view directory, but no view template files
- A view helper file
- A Coffeescript file for specific JavaScripts for that controller
- A `scss` file for the styles for the controller
- A full `resources` call in the `routes.rb` file

The `resource` generator is a smart generator that creates some of the core functionality needed for a full featured resource without much code bloat.

## Code Examples

### Boilerplate: Generate New Migration

To generate a new migration, you can use:

```bash
rails generate migration MyNewMigration
```

where "MyNewMigration" is the name of your migration. The generator will create an empty migration file `timestamp_my_new_migration.rb` in the `db/migrate` directory where `timestamp` is the UTC formatted date and time that the migration was generated.

### Boilerplate: Add Column to Migration

There is a special syntactic shortcut to generate migrations that add field to a table:

```bash
rails generate migration add_fieldname_to_tablename fieldname:string
```

This will generate the file `timestamp_add_fieldname_to_tablename.rb`, which will look like this:

```ruby
class AddFieldnameToTablename < ActiveRecord::Migration[5.0]
  def change
    add_column :tablenames, :fieldname, :string
  end
end
```

## Resources

- [Rails::Generators](https://api.rubyonrails.org/classes/Rails/Generators.html)
- [ActiveRecord::Migration](https://api.rubyonrails.org/classes/ActiveRecord/Migration.html)