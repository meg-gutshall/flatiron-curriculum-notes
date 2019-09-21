# Lesson: Model Class Methods

Let's add more features to our blog application!

## Filtering Posts by Author and Date

We have our list of blogs, but our readers would like to be able to filter the list by author.

We want to start by adding some controls to our view to do the filtering:

```erb
<!-- app/views/posts/index.html.erb -->

<h1>FlatBlog</h1>

<!-- add the new filter code above the @posts.each loop -->
<div class="filter">
  <h3>Filter posts:</h3>
  <%= form_tag @posts, method: :get do %>
    <%= select_tag :author, options_from_collection_for_select(@authors, :id, :name), include_blank: true %>
    <%= select_tag :date, options_for_select(["Today", "Old News"]), include_blank: true %>
    <%= submit_tag "Filter" %>
  <% end %>
</div>
<!-- end filter code -->

<% @posts.each do |post| %>
  <div class="post">
    <h2><%= post.title %></h2>
    <h3>by: <%= link_to post.author.name, author_path(post.author) %></h3>
    <p><%= post.description %></p>
  </div>
<% end %>
```

## Refactoring Out of the View

Remember, a view's concern is _presentation_. The controller should give it all the data it needs. That's why in our filter code, instead of passing `Author.all` to the `select_tag` and allowing the view to query the database, we pass it the `@authors` variable which is declared in the `PostController`.

Now let's get into our `PostController` and write our filter code in the `index` method so our view can render. **Note:** You can use `helper_method` in a controller to expose, or make available, a controller method in your view, but this isn't always such a great idea.

```ruby
# app/controllers/posts_controller.rb

def index
  # provide a list of authors to the view for the filter control
  @authors = Author.all

  # filter the @posts list based on user input
  if !params[:author].blank?
    @posts = Post.where(author: params[:author])
  elsif !params[:date].blank?
    if params[:date] == "Today"
      @posts = Post.where("created_at >= ?", Time.zone.today.beginning_of_day)
    else
      @posts = Post.where("created_at < ?", Time.zone.today.beginning_of_day)
    end
  else
    # if no filters are applied, show all posts
    @posts = Post.all
  end
end
```

## Refactoring Database Logic Out of the Controller

This is looking much better. Our view is back to dealing with presentation logic, and our controller is providing the right data. But we're still not there yet.

If we think about Separation of Concerns, is the controller concerned with having deep knowledge of the database so that it can make queries directly? No. All a controller wants to do is ask a model for what it needs in the simplest way possible.

So having something that looks like this...

```ruby
@posts = Post.where("created_at >= ?", Time.zone.today.beginning_of_day)
```

...isn't the best application of MVC and Separation of Concerns. We want the model to know things like `"created_at >= ?", Time.zone.today.beginning_of_day` and the controller to just ask for something more like `from_today`.

So we need to move this into the model. Now, the question becomes: is this a _class method_ on the `Post` model itself, or is it an _instance method_ on a specific `post`? Since we are going to be asking for multiple `post` instances from the database, we won't have an instance to begin with, so we'll need to use a class method. Class methods are commonly used on Active Record models to encapsulate this type of custom query functionality, so let's do that now.

First, we want to add one for the author filter. Let's dive into `post.rb` and get to work.

```ruby
# app/models/post.rb

def self.by_author(author_id)
  where(author: author_id)
end
```

You'll notice that this is essentially the same code that we had in the controller, but it's now properly encapsulated in the model. This way, a controller doesn't have to query the database—it just has to ask for posts `by_author`. So let's do that. Get back in the `PostsController`, and change the code to use our new class method:

```ruby
# app/controllers/posts_controller.rb

if !params[:author].blank?
  @posts = Post.by_author(params[:author])
elsif !params[:date].blank?

  ...
```

**Top-tip:** There are always more ways to accomplish the same thing. You may be wondering why we didn't just `find` the author and return `author.posts`. That also would work. But when we think about constructing an application in a logical way, using principles like Separation of Concerns to guide us, we can conclude that the `PostsController` is concerned with the `Post` model, so almost everything that controller does will probably flow through that model.

Next, let's give the same treatment to our date filter. We want to move the database code from the controller to the model, so let's add a couple more class method to the `Post` model:

```ruby
# app/models/post.rb

  ...

def self.from_today
  where("created_at >= ?", Time.zone.today.beginning_of_day)
end

def self.old_news
  where("created_at < ?", Time.zone.today.beginning_of_day)
end
```

And then let's update our controller to use them. Our final `index` method should look like this:

```ruby
# app/controllers/posts_controller.rb

def index
  # provide a list of authors to the view for the filter control
  @authors = Author.all

  # filter the @posts list based on user input
  if !params[:author].blank?
    @posts = Post.by_author(params[:author])
  elsif !params[:date].blank?
    if params[:date] == "Today"
      @posts = Post.from_today
    else
      @posts = Post.old_news
    end
  else
    # if no filters are applied, show all posts
    @posts = Post.all
  end
end
```