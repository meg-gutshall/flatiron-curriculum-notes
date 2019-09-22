# Lesson: Partial with Locals

Partials help us break our code up into reusable chunks. They also often have implicit dependencies that can lead to bugs. To make the implicit explicit, use locals whenever you partials depend on data to work. In the following example, we'll unpack exactly what locals are and how they're used.

Take a look at the [included repo](https://github.com/learn-co-students/partial-locals-reading-v-000). You should notice the same piece of code in a few places:

```erb
<ul>
  <li><%= @author.name %></li>
  <li><%= @author.hometown %></li>
</ul>
```

You'll find that code (or very similar code) in the following pages: `app/views/authors/show.html.erb`, `app/views/authors/index.html.erb`, and `app/views/posts/show.html.erb`.

Let's move that chunk of code into a partial and call the partial in each of those files instead. So our partial will look like:

```erb
<!-- app/views/authors/_author.html.erb -->

<ul>
  <li><%= @author.name %></li>
  <li><%= @author.hometown %></li>
</ul>
```

And our `authors/show` page will look like:

```erb
<!-- app/views/authors/show.html.erb -->

<%= render 'author' %>
```

Now let's take a look at the `posts/show` page. It currently looks like the following:

```erb
<!-- app/views/posts/show.html.erb -->

<h1>Information About the Post</h1>
<ul>
  <li><%= @author.name %></li>
  <li><%= @author.hometown %></li>
</ul>
<h2><%= @post.title %></h2>
<p><%= @post.content %></p>
```

You can see the first two lines are exactly the same as the code in our `authors/author` partial. Let's remove the repetition in our codebase by using that partial instead. By using the partial, our code will look like the following:

```erb
<!-- app/views/posts/show.html.erb -->

<h1>Information About the Post</h1>
<%= render 'authors/author' %>
<h2><%= @post.title %></h2>
<p><%= @post.content %></p>
```

Note that, because we are calling a partial from outside the current `app/views/posts` folder, we must specify the folder that our author partial is coming from by calling `render 'authors/author'`.

This code may look okay at first, but it poses some problems. When we render the partial `authors/author`, we are not being explicit about that partial's dependencies. A dependency is data that the code requires in order to work (like passing a variable into a method). In this case, the dependency of the author partial is the instance variable `@author`. Without that instance variable, the code won't work. Unfortunately, that dependency is defined far away in the controller. If we end up deleting the partial, we might forget to delete the dependency in the controller as well. This mistake likely can be avoided if, whenever we call the partial, we also specify the data that the code relies on by passing through local variables.

Let's see how local variables make our code more explicit:

```erb
<!-- app/views/posts/show.html.erb -->

<h1>Information About the Post</h1>
<%= render partial: "authors/author", locals: {post_author: @author} %>
<h2><%= @post.title %></h2>
<p><%= @post.content %></p>
```

Notice a few things. First, we are no longer passing the render method a string; we're passing a hash with two key-value pairs.

The first key-value pair tells Rails the name of the partial to render. The second key-value pair contains a key of `locals` pointing to a hash of variables to pass into the partial. Within that nested hash, the key is the name of the variable and its value is the value you'd like it to have in the partial. For the values of your locals, you can use instance variables set in the controller. When we use locals, we need to make sure that the variables we refer to in our partial have the same names as the keys in our locals hash.

So now, our `authors/author` partial should look like:

```erb
<!-- app/views/authors/_author.html.erb -->

<ul>
  <li><%= post_author.name %></li>
  <li><%= post_author.hometown %></li>
</ul>
```

In other words, the way we use locals with a partial is similar to how we pass arguments into a method. In the locals hash, the `post_author:` key is the argument name, and the value of that argument, `@author`, is the corresponding value stored as `post_author` and passed into the method. We can name the keys whatever we want (and would probably name this one `author` in a real application), but here the intent was demonstrating that the name of the keys has no special powers.

Now notice that, if we choose to delete the line `<%= render partial: "authors/author", locals: {post_author: @author} %>` from the `posts/show` view, the `@author = @post.author` line in our `PostsController` may no longer be needed because calling the partial requires us to pass in data about the author.

In fact, with locals, we can completely eliminate the `@author = @post.author` line in the `posts#show` controller action, instead only accessing that data where we need it—in the partial.

Let's remove that line of code in our controller and in the view pass through the author information be changing our code to the following:

```ruby
# app/controllers/posts_controller.rb

...
def show
  @post = Post.find(params[:id])
end
```

```erb
<!-- app/views/posts/show.html.erb -->

<h1>Information About the Post</h1>
<%= render partial: "authors/author", locals: {post_author: @post.author} %>
<h2><%= @post.title %></h2>
<p><%= @post.content %></p>
```

This code is much better. We are being more explicit about our dependencies, reducing line of code in our codebase, and reducing the scope of the author variable.
