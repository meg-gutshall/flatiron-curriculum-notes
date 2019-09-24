# Lesson: Rails URL Helpers

## Paths vs Route Helpers

Why would we want to use route helper methods as opposed to hard coding paths into the application? There are a number of reasons. Below are a few of the key rationales:

- Route helpers are more dynamic since they are methods and not simply strings. This means that if something changes with the route, there are many cases where the code itself won't need to be changed at all.
- Route helper methods help clean up the view and controller code and assist with readability. (_However, you cannot use these helper methods in your model files._)
- It's more natural to be able to pass arguments into a method as opposed to using string interpolation.
- Route helpers translate directly into HTML-friendly paths. In other words, if you have any weird characters in your URLs, the route helpers will convert them so they can be read properly by browsers. This includes items such as spaces or characters such as `&`, `%`, etc.

## Implementing Route Helpers

Using the `resources` method to draw your routes will create routing methods that we can utilize in our views and controllers. For example:

```ruby
# config/routes.rb

resources :posts, only: [:index, :show]
```

Running `rake routes` in the terminal will give the following output:

| Prefix | Verb | URI Pattern | Controller#Action |
| --- | --- | --- | --- |
| posts | GET | /posts(.:format) | posts#index |
| post | GET | /posts/:id(.:format) | posts#show |

These four columns tell us everything that we'll need in order to use the route helper methods. The breakdown is below:

- **Column 1**: This column gives the prefix for the route helper methods. In the current application, `posts` and `post` are the prefixes for the methods that you can use throughout your applications. The two most popular method types are `_path` and `_url`. So if we want to render a relative link path to our posts' index page, the method would be `posts_path` or `posts_url`. The difference between `_path` and `_url` is that `_path` gives the relative path and `_url` renders the full URL. **In general, it's best to use the `_path` version so that nothing breaks if your server domain changes.**
- **Column 2**: This is the HTTP verb.
- **Column 3**: This column shows what the path for the route will be and what parameters need to be passed to the route. As you may notice, the second row for the show route calls for an ID. When you pass the `resources` method to the `:show` argument, it will automatically create this route and assume that you will need to pass the `id` into the URL string. Whenever you have `id` parameters listed in the path like this, you will need to pass the route helper method an ID.
- **Column 4**: This column shows the controller and action with a syntax of `controller#action`.

One of the nice things about utilizing route helper methods is that they create predictable names for the methods. Once to get into "day-to-day Rails development", you will only need to run `rake routes` to find custom paths.

## The `link_to` Method

Instead of using the HTML anchor tag to create a hyperlink, Rails provides us with the handy `link_to` method. Just call `link_to` and pass in the body and URL arguments.

- The body refers to the text that will be hyperlinked.
- The URL represents a `String`. You can use route helpers (or URL helpers) here.

Rails is smart enough to know that if you pass in an object as the argument to a route helper method, it will automatically use the `id` attribute. For example:

```erb
<!-- app/views/posts/show.html.erb -->

<% @posts.each do |post| %>
  <div><%= link_to post.title, post_path(post) %></div>
<% end %>
```

## Using the `:as` Option

If for any reason you don't like the naming structure for the methods or paths, you can customize them quite easily. A common change is updating the path users go to in order to register for a site. Out of the box, the standard path would be `/users/new`. However, we want something a little more readable, like `/register`. In order to make this change, let's update the `routes.rb` file, adding the following line:

```ruby
# config/routes.rb

get '/register', to: 'users#new', as: 'register'
```

Now the application lets users navigate to `/register` to sign up, and you, the developer, can utilize your own custom `register_path` route helper throughout the app.
