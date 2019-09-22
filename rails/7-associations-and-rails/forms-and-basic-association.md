# Lesson: Forms and Basic Association

## The Problem

Let's say we have a simple blogging system. Our models are `Post` and `Category`. A `Post` `belongs_to` a `Category`.

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base
  belongs_to :category
end
```

```ruby
# app/models/category.rb

class Category < ActiveRecord::Base
  has_many :posts
end
```

Now we need to build the functionality for a user to create a `Post`. We're going to need a form for the `Post`'s content, and some way to represent what `Category` the `Post` belongs to.

## Defining A Custom Setter and Getter (Convenience Attributes on Models)

Since our Active Record models are still just Ruby classes, we can define our own setter and getter methods:

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base
  def category_name=(name)
    self.category = Category.find_or_create_by(name: name)
  end

  def category_name
    self.category ? self.category.name : nil
  end
end
```

The setter method `#category_name=` is called whenever a `Post` is initialized with a `category_name` field. We can expand `Post.create(post_params)` to:

```ruby
Post.create({
  category_name: params[:post][:category_name],
  content: params[:post][:content]
})
```

So, you can see that `#category_name=` will indeed be called. Since we have defined this setter ourselves, `Post.create` does not try to fall back to setting `category_name` through Active Record. You can think of `#category_name=` as intercepting the call to the database and instead shadowing the attribute `category_name` by, one, making sure the `Category` exists; and, two, providing it in-memory for the `Post` model. We sometimes call these in-memory attributes "virtuals".

Now we can set `category_name` on a post. We can do it when creating a post too, so our controller becomes quite simple again:

```ruby
# app/controllers/posts_controller.rb

class PostsController < ApplicationController
  def create
    Post.create(post_params)
  end

  private
    def post_params
      params.require(:post).permit(:category_name, :content)
    end
end
```

Notice the difference—we're now accepting a category name, rather than a category ID. Even though there's no Active Record field for `category_name`, the `category_name` key in the `post_params` hash prompts a call to the `category_name=` method.

Now we can build our form:

```erb
<!-- app/views/posts/new.html.erb -->

<%= form_for @post do |f| %>
  <%= f.label :category_name %>
  <%= f.text_field :category_name %>
  <%= f.text_field :content %>
  <%= f.submit %>
<% end %>
```

Now the user can enter a category by name (instead of needing look up its ID), and we handle finding or creating the `Category` in the black box of the server. This results in a much friendlier experience for the user.

## Selecting from Existing Categories

If we want to let the user pick from existing categories, we can use a [Collection Select](https://apidock.com/rails/ActionView/Helpers/FormOptionsHelper/collection_select) helper to render a `<select>` tag:

```erb
<!-- app/views/posts/new.html.erb -->

<%= form_for @post do |f| %>
  <%= f.collection_select :category_name, Category.all, :name, :name %>
  <%= f.text_field :content %>
  <%= f.submit %>
<% end %>
```

This will create a drop down selection input where the user can pick a category. However, we've list the ability for users to create their own categories.

That might be what you want. For example, the content management system for a magazine would probably want to enforce that the category of an article is one of the sections actually printed in the magazine.

In our case, however, we want to give users the flexibility to create a new category _or_ pick an existing one. What we want is autocompletion, which we can get with a [`datalist`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist):

```erb
<!-- app/views/posts/new.html.erb -->

<%= form_for @post do |f| %>
  <%= f.text_field :category_name, list: "categories_autocomplete" %>
  <datalist id="categories_autocomplete">
    <% Category.all.each do |category| %>
      <option value="<%= category.name %>">
    <% end %>
  </datalist>
  <textarea name="post[content]"></textarea>
  <%= f.submit %>
<% end %>
```

`datalist` is a new element in the HTML5 spec that allows for easy autocomplete.

## Updating Multiple Rows

Let's think about the reverse association. Categories have many posts.

```ruby
# app/models/category.rb

class Category < ActiveRecord::Base
  has_many :posts
end
```

Given a category, how do we let a user specify many different posts to categorize? We can't do it with just one `<select>` because we can have many posts in that category.

### Using Array Parameters

Rails uses a [naming convention](https://guides.rubyonrails.org/v3.2.13/form_helpers.html#understanding-parameter-naming-conventions) to let you submit an array of values to a controller.

If you put this in a view, it looks like this:

```erb
<%= form_for @category do |f| %>
  <input name="category[post_ids][]">
  <input name="category[post_ids][]">
  <input name="category[post_ids][]">
  <input type="submit" value="Submit">
<% end %>
```

When the form is submitted, your controller will have access to a `post_ids` param, which will be an array of strings.

We can write a setter method for this, just like we did for `category_name`:

```ruby
# app/models/category.rb

class Category < ActiveRecord::Base
  def post_ids=(ids)
    ids.each do |id|
      post = Post.find(id)
      self.posts << post
    end
  end
end
```

Now we can use the same wiring in the controller to set `post_ids` from `params`:

```ruby
# app/controllers/categories_controller.rb

class CategoriesController < ApplicationController
  def create
    Category.create(category_params)
  end

  private
    def category_params
      params.require(:category).permit(:name, post_ids: [])
    end
end
```
