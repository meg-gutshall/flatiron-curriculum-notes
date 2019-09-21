# Lesson: Has Many Through in Forms

## Join Model Forms

Sometimes, it may be appropriate for a user to create an instance of our join model directly. Think back to the hospital domain from our previous lab. It makes perfect sense that a user would go to `appointments/new` and fill out a form to create a new appointment.

```erb
<!-- app/views/appointments/new.html.erb -->

<%= form_for @appointment do |f| %>
  <%= f.datetime_select :appointment_datetime %>
  <%= f.collection_select :doctor, Doctor.all, :id, :name %>
  <%= f.collection_select :patient, Patient.all, :id, :name %>
  <%= f.submit %>
<% end %>
```

In this example, a user is filling out a form, entering the date and time they'd like to come, and choosing their doctor and their name from a dropdown. We're assigning these properties directly to the appointment as it's created.

Other times, we need to be more abstract. Let's return to our blog example, but this time we'll say that a post can have many categories and categories can have many posts. For this, we'll need a join table—let's call it `post_categories`. If our user wants to associate a post with a category, it doesn't make sense for them to go to `/post_categories/new` and fill out a "new post category form". That's confusing! Let's look at a more abstract way that we can do this thanks to the magic of Active Record.

## Setting Up Our Posts and Categories

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base
  has_many :post_categories
  has_many :categories, through: :post_categories
end
```

```ruby
# app/models/category.rb

class Category < ActiveRecord::Base
  has_many :post_categories
  has_many :posts, through: :post_categories
end
```

```ruby
# app/models/post_category.rb

class PostCategory < ActiveRecord::Base
  belongs_to :post
  belongs_to :category
end
```

Now, let's make it so that our user can assign categories to a post when the post is created. We did this in a previous example with a join table. Our post was directly related to its category, and the `posts` table has the foreign key for its category. Because of this, instances of our `Post` class responded to a method called `category_ids=`. We called upon this method from our form helpers to build out a nested form. Luckily, `has_many, through` functions exactly the same as a `has_many` relationship. Instances of our `Post` class still respond to a method called `category_ids=`. We'll use a helper method very similar to the `collection_select` we used previously.

```erb
<!-- app/views/posts/_form.html.erb -->

<%= form_for @post do |f| %>
  <%= f.label "Title" %>
  <%= f.text_field :title %>

  <%= f.label "Content" %>
  <%= f.text_area :content %>

  <%= f.collection_check_boxes :category_ids, Category.all, :id, :name %>

  <%= f.submit %>
<% end %>
```

This will create a checkbox field for each `Category` in our database. The HTML generated looks something link this:

```html
<input type="checkbox" value="1" name="post[category_ids][]" id="post_category_ids_1">
```

In our controller, we've set up our `post_params` to expect a key of `:category_ids` with a value of an array.

```ruby
# app/controllers/post_controller.rb

class PostController < ApplicationController

  ...

  private
    def post_params
      params.require(:post).permit(:title, :content, category_ids: [])
    end
end
```

When we submit a new post, first, we're creating a new row in our `posts` table with `title` and `content`. Next, we create a row in our `post_categories` table dor each ID number that was stored in our `category_ids` array. This functions just like it did with a `has_many` relationship, but, instead of creating a new record in our `categories` table, Active Record is creating two new rows in our `post_categories` table. This means that we can interact with out higher-level models directly without having to think too much at all about our join table—Active Record will manage that relationship for us behind the scenes.

## Creating New Categories

We can now associate categories with our posts, but what about creating new categories? First, we want a text field to enter the name of our new category. The value of the name should be nested under our `post_params`, so we don't have to add too much code to our controller. We can use the `fields_for` helper to do this very easily.

```erb
<!-- app/views/posts/_form.html.erb -->

<%= form_for @post do |f| %>
  <%= f.label "Title" %>
  <%= f.text_field :title %>

  <%= f.label "Content" %>
  <%= f.text_area :content %>

  <%= f.collection_check_boxes :category_ids, Category.all, :id, :name %>
  <%= f.fields_for :categories, post.categories.build do |categories_fields| %>
    <%= categories_fields.text_field :name %>
  <% end %>

  <%= f.submit %>
<% end %>
```

The `fields_for` helper takes two arguments: the associated model that we're creating and an object to wrap around. In this case, we've passed in the `:categories` association and built an empty category associated with the post.

Let's look at the HTML that this generated for us:

```html
<input type="text" name="post[categories_attributes][0][name]" id="post_categories_attributes_0_name">
```

Our params hash will now have a key of `:categories_attributes` nested under the key of `post`. Let's add that to our strong params and tell it to expect a key of `name` inside for the category's name.

```ruby
# app/controllers/posts_controller.rb

class PostsController < ApplicationController

  ...

  private
    def post_params
      params.require(:post).permit(:title, :content, category_ids: [], categories_attributes: [:name])
    end
end
```

Now, when we do mass assignment, our `Post` model will call a method called `categories_attributes=`. Let's add that method to our model using the `accepts_nested_attributes_for` macro.

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base
  has_many :post_categories
  has_many :categories, through: :post_categories
  accepts_nested_attributes_for :categories
end
```

We can now create categories that are automatically associated with our new post, but there's a problem. We're creating a new category each time, regardless of whether or not it already exists. In this case, we need to customize the way our category is created. Luckily, we can easily do this by creating our own `categories_attributes=` method.

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base
  has_many :post_categories
  has_many :categories, through: :post_categories
  accepts_nested_attributes_for :categories

  def categories_attributes=(category_attributes)
    category_attributes.values.each do |category_attribute|
      category = Category.find_or_create_by(category_attribute)
      self.categories << category
    end
  end
end
```

Now, we're only creating a new category if it doesn't already exist with the current name. We're also using a cool method called `categories <<`. What's great about this is you can mentally think of it as two steps. First, we call `self.categories`, which returns an array of `Category` objects, and then we call the shovel (`<<`) method to add our newly found or created `Category` object to the array. We could imagine later calling `save` on the `Post` object and this then creating the `post_categories` join record for us. In reality, this is syntactic sugar for the `categories <<` method. That's the actual method name, and behind the scenes it will create the join record for us. It's one of the methods dynamically created for us whenever we use a `has_many` association. The end result is this method doing exactly what Active Record was doing for us before; we're just customizing the behavior a little bit.