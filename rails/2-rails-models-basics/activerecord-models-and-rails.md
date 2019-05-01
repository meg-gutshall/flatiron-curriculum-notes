# Lesson: ActiveRecord Models and Rails

## Active Record's Role

- Active Record is the built-in ORM that Rails utilizes to manage the model aspects of an application.
  - An ORM (Object Relational Mapping system) enables your application to manage data in a method-driven structure, meaning that you are able to run queries, add records, and perform all of the traditional database processes by leveraging methods as opposed to writing SQL manually.
- By using Active Record, you are also able to perform advanced query tasks, such as method chaining and scoping, which typically require less code and make for a more readable query.

## Active Record Models

- By using model files, we are able to create an organized layer of abstraction for our data.
- An important thing to remember is that **at the end of the day the model file is a Ruby class**.
  - If it has a corresponding database table, it will inherit from the `ActiveRecord::Base` class, which means that it has access to a number of methods that assist in working with the database.
  - You can also treat it like a regular Ruby class, allowing you to create methods, data attributes, etc.
- A typically data file will contain code such as but not limited to the following:
  - [Custom scopes](https://api.rubyonrails.org/classes/ActiveRecord/Scoping/Named/ClassMethods.html)
  - Model instance methods
  - Default settings for database columns
  - [Validations](https://api.rubyonrails.org/classes/ActiveModel/Validations/ClassMethods.html)
  - [Model-to-model relationships](https://api.rubyonrails.org/classes/ActiveRecord/Associations/ClassMethods.html)
  - [Callbacks](https://api.rubyonrails.org/classes/ActiveRecord/Callbacks.html)
  - Custom algorithms

## Creating an Active Record Model

As a professional Rails developer, you will be expected to build applications by leveraging a BDD (behavior-driven development) process, so we will walk through how to build each feature with a test-first approach so that the tests can lead our development.

### Generate a New Rails App

```bash
# The -T flag tells the Rails project generator not to include TestUnit, the default testing framework:

rails new my-blog-post-app -T

# The Rails project generator created our directory:

cd my-blog-post-app

# We modified the Gemfile to include
# gem 'rspec-rails', '~> 3.0'
# in the :development, :test group, then ran:

bundle install

# Finally, we created the initial RSpec config:

rails g rspec:install
```

### Creating an RSpec Test

Create a new file `spec/models/post_spec.rb` and within place the following code:

```ruby
# spec/models/post_spec.rb

require 'rails_helper'

describe Post do

  it 'can be created' do
    post = Post.create!(title: "My title", description: "The post description")
    expect(post).to be_valid
  end

  it 'has a summary' do
    post = Post.create!(title: "My title", description: "The post description")
    expect(post.post_summary).to eq("My title - The post description")
  end

end
```

The first block tests for a `Post` being created. The second block tests to see if the `post` object has a summary.

### Creating the `Post` Model

In order for our RSpec to have anything to test, we need to create a `Post` model in the `app/models` directory called `post.rb`, and add the following code:

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base

  def post_summary
    self.title + " - " + self.description
  end

end
```

### Creating the Post Database Table

Since we're testing to see if a `Post` can be created, the `Post` model will need to have an associated database table in which `ActiveRecord` can use its built-in `#create` method to store a new object. To do this, we'll need to make a new directory in the `db/` directory called `migrate`, and add a new file called `001_create_posts.rb`. To that file, add the following code:

```ruby
# db/migrate/001_create_posts.rb

class CreatePosts < ActiveRecord::Migration
  def change
    create_table :posts do |t|
      t.string :title
      t.text :description

      t.timestamps null: false
    end
  end
end
```

After creating the above file, run `rake db:migrate` and you should see that our `db/schema.rb` file has been updated with our new posts table.

#### Table Migration Naming Conventions

- The table's name should reflect the migration's class name.
  - This is then reiterated by the argument passed to the `create_table` method.
- The filename needs to be unique, and when you generate a migration automatically through a model of scaffold generator, you will notice that the migration file name is prepended with a timestamp value to make sure there are no duplicate migration files.
- For a refresher on migrations, see [this documentation](https://edgeguides.rubyonrails.org/active_record_migrations.html).

## Resources

[Creating an Active Record Model Code Along](https://github.com/meg-gutshall/rails-activerecord-models-and-rails-readme-v-000)