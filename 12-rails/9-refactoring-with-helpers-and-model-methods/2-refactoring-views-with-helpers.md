# Lesson: Refactoring Views with Helpers

## A Story as Old as `strftime`

Let's imagine we're working on a blog application. We've already added the presentation logic to show a blog post:

```erb
<!-- app/views/posts/show.html.erb -->

<h1><%= @post.title %></h1>
<p><%= @post.description %></p>
```

However, our readers really want to know _when_ the post was posted or edited. We know our `Post` model has a timestamp field called `updated_at`, so we decide to display that using the `strftime` method.

```erb
<!-- app/views/posts/show.html.erb -->

<h1><%= @post.title %></h1>
<p><%= @post.updated_at.strftime("Last update %A, %b %e, at %l:%M %p") %></p>
<p><%= @post.description %></p>
```

**Top tip:** Notice how we included the text and punctuation in the argument to `strftime`. It will very nicely ignore anything that isn't one of the format directives and pass it through as part of the final string. This is helpful because it saves us from the awkward business of having to try to parse out the time string and concatenate parts of it together with other strings in order to create more readable output.

Now people know when a blog entry was last updated. Except they only know it on the `show` template. What if they also need to see that date on the post list page, in line with each post title? We can add it to the `index` template.

```erb
<!-- app/views/posts/index.html.erb -->

<% @posts.each do |post| %>
  <div>
    <p><%= post.title %> - <%= post.updated_at.strftime("Last update %A, %b %e, at %l:%M %p") %></p>
  </div>
<% end %>
```

Now it's on the `show` and `index` views. But now we're thinking that it would be nice to see this when we are editing a blog post, just for our reference, so let's add it to the `edit` template.

```erb
<!-- app/views/posts/edit.html.erb -->

<%= form_for @post do |f| %>
  <label><%= @post.updated_at.strftime("Last update %A, %b %e, at %l:%M %p") %></label><br>

  <%= f.label :post_title %><br>
  <%= f.text_field :title %><br>

  <%= f.label :post_description %><br>
  <%= f.text_area :description %><br><br>

  <%= f.submit %>
<% end %>
```

At this point there may be little red flags shooting up in your head, but let's go one step further. A few weeks after making this change, we decide that the format should be in military (24-hour) time and that we don't want to display the day of the week anymore.

But now we have a problem. WE have to remember (or worse, search for) every place we wrote that code to display the last updated date and time, and then we have to make the _same_ change in all of those places. We have a small application with only a few views right now but, as your app grows in size, this kind of repetition is a productivity _killer_. It's also a great way to introduce bugs into the system if we forget to make changes in all of the correct places.

## Don't Repeat Yourself (DRY)

DRY is a software design principle that, like Separation of Concerns, helps us make decisions about how to organize our code. The formal, very dry statement of DRY is: "Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."

How do we DRY up our views for this last updated feature? If we have a goal of manipulating the `updated_at` field in only a single place, where can we do that? What about the model? We only ever get `updated_at` from the model, so it's tempting to do something like:

```ruby
# app/models/post.rb

def last_updated
  updated_at.strftime("Last updated %A, %b %e, at %l:%M %p")
end
```

Then we can call `@post.last_updated` on the view. That would certainly solve our DRY problem, but if we think back on MVC and Separation of Concerns, we've created a new problem. Model code isn't concerned with _presentation logic_. Displaying a formatted string isn't the job of the component that talks to the database and handles the business logic. It's the job of the view. So we need a way to keep that code in the view but also make it DRY.

## Helpers Are Here To, Well, Help

Rails provides us with a great way to extract common presentation logic from multiple views: helpers! Helpers are methods that are available to your views and encapsulate a common bit of code. If you've used a `link_to` or a `text_field` then you've already come across helpers. Rails has a ton of them built-in to help keep you from having to repeat all the code necessary to build a link to a given route, display an image, or create a form.

We can also create our own helpers to solve our own problems.

For our post's last updated label, we want to create a method that executes the `strftime` bit so that we can use it in our three views. But where do we put it?

Helpers are generally organized by controller. If you use `rails g scaffold` or `rails g controller`, Rails will create a helper for your controller and put it in the `app/helpers` directory. If we look in our helpers directory, we'll see `application_helper.rb`, `authors_helper.rb`, and `posts_helper.rb`. This matches what we have in our `controllers` directory—`application_controller.rb`, `authors_controller.rb`, and `posts_controller.rb`.

Let's use Separation of Concerns to decide where to make our helper. Displaying the date of the last time the post was updated isn't an application-wide concern; it's only a post concern. So let's put it in the `PostsHelper`.

```ruby
# app/helpers/posts_helper.rb

def last_updated(post)
  post.updated_at.strftime("Last updated %A, %b %e, at %l:%M %p")
end
```

Why are we passing `post` as an argument to the helper? If you look back at our three views, you'll see that sometimes we're dealing with an instance variable (`@post`), and sometimes we're dealing with a local variable (`post`). Our helper doesn't know anything that we don't directly tell it, so it can't assume a specific variable name. We will need to tell it which post we want it to act on.

**Note:** Helpers can get a lot more advanced, encapsulating more logic and even HTML. In this case, we just want to get the value and not output any markup—we'll let the view template handle that part. It's not the helper;s _concern_.

Now that we have our helper, let's DRY up those views.

```erb
<!-- app/views/posts/show.html.erb -->

<h1><%= @post.title %></h1>
<p><%= last_updated @post %></p>
<p><%= @post.description %></p>
```

```erb
<!-- app/views/posts/index.html.erb -->

<% @posts.each do |post| %>
  <div>
    <p><%= post.title %> - <%= last_updated post %></p>
  </div>
<% end %>
```

```erb
<!-- app/views/posts/edit.html.erb -->

<%= form_for @post do |f| %>
  <label><%= last_updated @post %></label><br>

  <%= f.label :post_title %><br>
  <%= f.text_field :title %><br>

  <%= f.label :post_description %><br>
  <%= f.text_area :description %><br><br>

  <%= f.submit %>
<% end %>
```

Now we have encapsulated the formatting logic into a single method, but notice how much more readable our views are now.

## Using Another Controller's Helpers

Our blog also has an author page that lists the posts by that author. What do we do we do if we want to also show the last updated time on that page? The answer is: the same thing we just did!

```erb
<!-- app/views/authors/show.html.erb -->

<h1><%= @author.name %></h1>

<p>Posts:</p>
<% @author.posts.each do |post| %>
  <div><%= post.title %> - <%= last_updated post %></div>
<% end %>
```

Helpers are _organized_ by controller, but they aren't _restricted_ to a single controller. Just like you can use a Rails `link_to` helper in any view, you can also use any of your own helpers in any view. Our `last_updated` helper is still a `Post` concern (so we know to look for it in the `PostsHelper`), but if an author page or any other page needs to use it, they can. Just like our models, views, and controllers, helpers are separated by concern to help us keep our codebase organized.

## Application Helpers

What about thing that aren't the concern of a single controller and are applicable to the entire application? For these cases, we have the `application_helper`. This helper is created automatically with your Rails project and is where you keep helpers that are related to the application itself rather than any given model or controller.

In applications where users can log in, the application helper will often have a method to expose a `current_user`, something which gets used on almost every view in the system.

For our blog application, we decide we want to dynamically change the `<title>` of each page based on what the user is looking at. On an author's show page, it might be the author name. On a blog post page, it might be the post's title. Since we already know we're going to be repeating the same basic snippet of code across many views, we're going to jump right to creating a helper.

The page `title` isn't strictly the concern of a `Post` or an `Author`, even though it may use data from either of those things. Since it's a broader concern then just one controller/model, it's a prime candidate for the `ApplicationHelper`.

```ruby
# app/helpers/application_helper.rb

def title(text)
  content_for :title, text
end
```

**Note:** We use the Rails `content_for` helper within our custom helper here. What this will do is send our `text` to the place in our application layout that is expecting some content for the `:title`.

```erb
<!-- app/views/layout/application.html.erb -->

<head>
  <title><%= yield :title %></title>
</head>
```

You can read more about `content_for` in the [Layouts and Rendering](https://guides.rubyonrails.org/layouts_and_rendering.html) RailsGuide.

Now that we have our `title` helper, we can use it everywhere to change the page title based on the content.
