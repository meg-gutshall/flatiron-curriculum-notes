# Lesson: Modifying Nested Resources

Continuing with our blog application, we're going to extend our nested resources to allow for creating and modifying blog posts by author.

## Creating A New Post For An Author

The first thing we want to do is to create a new post that is automatically link to an `Author`. We could set up a select box on the post page and make the author choose, however, if we're already on the author's page, we know who the author is, so why not do it without forcing the user to choose?

We already used nested resources to view posts by author, so now let's look at nested resources to create posts by author. As usual, we want to start with the route. We want to add `:new` to our nested `:posts` resource:

```ruby
# config/routes.rb

resources :authors, only: [:show, :index] do
  resources :posts, only: [:show, :index, :new]
end
```

This gives us access to `/authors/:id/posts/new`, and a `new_author_post_path` helper.

We have the route, so now we need to update our `posts_controller#new` action to handle the `:author_id` parameter.

```ruby
# app/controllers/posts_controller.rb

def new
  @post = Post.new(author_id: params[:author_id])
end
```

Notice that we're passing the `params[:author_id]` into `Post.new()`. We want to make sure that, if we capture an `author_id` through a nested route, we keep track of it and assign the post to that author. We'll actually be carrying this `id` with us for the next few steps, babysitting it through the server request/response cycle.

Now let's get into our author `show` template and add a link to the nested new post page for that author.

```erb
<!-- app/views/authors/show.html.erb -->

<h1><%= @author.name %></h1>

<h2><%= link_to "New Post", new_author_post_path(@author) %></h2>

<h3>Posts:</h3>
<% @author.posts.each do |post| %>
  <p><%= post.title %></p>
<% end %>
```

Let's launch the app (don't forget to `rake db:seed`), browse to `/authors`, click on an author's name, and then click the new post link. Once there, let's make a post.

But where's our author? We set it up in the `new` action, but it never made it to the view so that it could get submitted back to the server. Let's fix that. Open up the post form partial and add a hidden field for the `:author_id`.

```erb
<!-- app/views/posts/_form.html.erb -->

<%= form_for @post do |f| %>
  <label>Post Title:</label><br>
  <%= f.text_field :title %><br>

  <%= f.hidden_field :author_id %>

  <label>Post Description:</label><br>
  <%= f.text_area :description %><br>

  <%= f.submit %>
<% end %>
```

If we reload the new post page for the author and inspect the source, we should see something like this:

```html
<input type="hidden" value="1" name="post[author_id]" id="post_author_id">
```

That part's working, but we need to carry that `author_id` with us even further. Remember [Strong Parameters](http://guides.rubyonrails.org/action_controller_overview.html#strong-parameters)? We need to update our `PostsController` to accept `:author_id` as a parameter for a post. So let's get in there and modify our `post_params` method.

```ruby
# app/controllers/posts_controller.rb

...

private
  def post_params
    params.require(:post).permit(:title, :description, :author_id)
  end
```

Now we know the `author_id` will be allowed for mass-assignment in the `create` action.

Why didn't we have to make a nested resource for `:create` in addition to `:new`? The `form_for(@post)` helper in `posts/_form.html.erb` will automatically route to `POST posts_controller#create` for a new `Post`. By carrying the `author_id` as we did and allowing it through strong parameters, the existing `create` route and action can be used without needing to do anything else.

## Editing An Author's Posts

We can use the same technique to allow us to directly edit an author's posts. First, we allow the `:edit` action in the nested route:

```ruby
# config/routes.rb

resources :authors, only: [:show, :index] do
  resources :posts, only: [:show, :index, :new, :edit]
end
```

We don't have to change any views because `new` and `edit` both use the same `_form` partial that already has the `author_id`.

Now we need to update our post `show` view to give us the new nested link to edit the post for the author.

```erb
<!-- app/views/posts/show.html.erb -->

<h1><%= @post.title %></h1>
<h2>by <%= link_to @post.author.name, author_path(@post.author) if @post. author %> (<%= link_to "Edit Post", edit_author_post_path(@post.author, @post) if @post.author %>)</h2>
<p><%= @post.description %></p>
```

And if we try it out, everything _should_ work just fine. Reload the page, click the edit link, and edit the post...

## Handling Mischief and Errors in Our URLs

But now we've opened ourselves up to a couple of potential bugs, or worse, opportunities for our more playful users to make a mess of our data. Let's work backward, starting with our recent changes to `edit`.

We find out that if we change the `author_id` in the URL, it will still load the same page even though the author may not even exist, let alone own the particular post we're editing. Remember how we didn't have to change the controller when we added the nested resource route for `:edit`? Well, this is the price we pay for taking shortcuts. What we should do is check to make sure that 1) the `author_id` is valid and 2) the post matches the author. So let's fix that now.

```ruby
# app/controllers/posts_controller.rb

def edit
  if params[:author_id]
    author = Author.find_by(id: params[:author_id])
    if author.nil?
      redirect_to authors_path, alert: "Author not found."
    else
      @post = author.posts.find_by(id: params[:id])
      redirect_to author_posts_path(author), alert: "Post not found." if @post.nil?
    end
  else
    @post = Post.find(params[:id])
  end
end
```

Here we're looking for the existence of `params[:author_id]`, which we know would come from our nested route. If it's there, we want to make sure that we find a valid author. If we can't, we redirect them to the `authors_path` with a `flash[:alert]`.

If we do find the author, we next want to find the post by `params[:id]`, but, instead of directly looking for `Post.find()`, we need to filter the query through our `author.posts` collection to make sure we find it in that author's posts. It may be a valid post `id`, but it might not belong to that author, which makes this an invalid request.

**Top-tip:** One of the downsides of RESTful URL schemes is that curious users can edit the URLs to try to explore the system further. This is how we discovered [all the hidden Netflix genres](http://mashable.com/2016/01/11/netflix-search-codes/#LM6QcfeksZqG). However, this could also lead to security holes in your system, allowing users to potentially mismatch ID parameters and wreak havoc in your database, so always guard against that by doing what we've done above.

While we're at it, we should fix up our `new` action to ensure that we're creating a new post for a valid author. Let's make it look like this:

```ruby
# app/controllers/posts_controller.rb

def new
  if params[:author_id] && !Author.exists?(params[:author_id])
    redirect_to authors_path, alert: "Author not found."
  else
    @post = Post.new(author_id: params[:author_id])
  end
end
```

Here we check for `params[:author_id]` and then for `Author.exists?` to see if the author is real.

Why aren't we doing a `find_by` and getting the author instance? Because we don't need a whole instance for `Post.new`; we just need the `author_id`. And we don't need to check against the `posts` of the author because we're just creating a new one. So we use `exists?` to quickly check the database in the most efficient way.

But what if `params[:author_id]` is `nil` in the example above? If we just did `Post.new` without the `(author_id: params[:author_id])` argument, the `author_id` attribute of the new `Post` would be initialized as `nil` anyway. So we don't have to do anything special to handle it. It works for us if there is or isn't an `author_id` present.

## Missing Authors

When someone creates a new post via our nested route, we automatically assign an author, and everything works great. But what about when they create a new post from the regular old `new_post_path`?

We could just eliminate that route and only allow post creation through the nest resource. That might be a valid choice in some applications. But we've decided we want to be able to select an author at the time of posting if we haven't used the nested route.

Since we're already set up to handle `author_id` on the controller, all we have to do is augment our `posts/_form.html.erb` partial to present a list of authors when none is present.

```erb
<!-- app/views/posts/_form.html.erb -->

<%= form_for @post do |f| %>
  <label>Post Title:</label><br>
  <%= f.text_field :title %><br>

  <% if @post.author.nil? %>
    <%= f.select :author_id, options_from_collection_for_select(Author.all, :id, :name) %><br>
  <% end %>
  <%= f.hidden_field :author_id %>

  <label>Post Description:</label><br>
  <%= f.text_area :description %><br>

  <%= f.submit %>
<% end %>
```

That gives us a select control if we don't have an author, but we have a problem. We can only have one `:author_id` field. We could put that `hidden_field` in an `else`, which would work, but then we would have a whole bunch of logic cluttering up our view. So let's dump it in our `posts_helper` and clean up that form.

```ruby
# app/helpers/posts_helper.rb

module PostsHelper
  def author_id_field(post)
    if post.author.nil?
      select_tag "post[author_id]", options_from_collection_for_select(Author.all, :id, :name)
    else
      hidden_field_tag "post[author_id]", post.author_id
    end
  end
end
```

And back in our form partial:

```erb
<!-- app/views/posts/_form.html.erb -->

<%= form_for @post do |f| %>
  <label>Post Title:</label><br>
  <%= f.text_field :title %><br>

  <%= author_id_field(@post) %><br>

  <label>Post Description:</label><br>
  <%= f.text_area :description %><br>

  <%= f.submit %>
<% end %>
```

Now we should have a selector when we browse to `/posts/new` and a hidden `author_id` field when we browse to `/authors/1/posts/new`.
