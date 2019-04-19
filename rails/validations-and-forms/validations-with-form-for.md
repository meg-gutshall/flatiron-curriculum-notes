# Lesson: Validations with `form_for`

Now that we know Rails automatically performs validations defined on models, let's use this information to easily display validation errors to the user.

## The Differences Between `form_for` and `form_tag`

This step will make heavy usage of `form_for`, the high-powered alternative to `form_tag`. The biggest difference between these two helpers is that `form_for` creates a form specifically **for** a model object. `form_for` is full of convenient features.

In the example below, `@post` is the model object that needs a form. `form_for` automatically performs a route lookup to find the right URL for post.

`form_for` takes a block. It passes an instance of FormBuilder as a parameter to the block, which is what `f` is below.

`form_tag` doesn't know what action we're going to use it for, because it has no model object to check. `form_for` knows that an empty, unsaved model object needs a `new` form and a populated object needs an `edit` form. This means we get to skip all of these steps:

1. Setting the `name` and `id` of the `<form>` element.
2. Setting the method to `patch` on edits.
3. Setting the text of the `<submit>` element.
4. Specifying the root parameter name (`post[whatever]`) for every field.
5. Choosing the attribute (`@post.whatever`) to fill for every field.

## Using `form_for` to Generate Empty Forms

To wire up an empty form in our `new` view, we need to create a blank object:

```ruby
# app/controllers/posts_controller.rb

def new
  @post = Post.new
end
```

Here's our usual vanilla `create` action:

```ruby
# app/controllers/posts_controller.rb

def create
  @post = Post.create(post_params)

  redirect_to post_path(@post)
end
```

We still have to solve the dual problem of what to do when there's no valid model object to redirect to, and how to hold on to our error messages while re-rendering the same form.

## Re-Rendering with Errors

Remember from a few lessons ago how CRUD methods return `false` when validation fails? We can use that to our advantage here and branch our actions based on the result:

```ruby
# app/controllers/posts_controller.rb

def create
  @post = Post.net(post_params)

  if @post.save
    redirect_to post_path(@post)
  else
    render :new
  end
end
```

## Full Messages with Prepopulated Fields

Because of `form_for`, Rails will automatically prepopulate the `new` form with the values the user entered on the previous page.

To get some extra verbosity, we can add the snippet from the previous lesson to the top of the form:

```erb
<!-- app/views/posts/new.html.erb //-->

<% if @post.errors.any? %>
  <div id="error_explanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited the post from being saved: </h2><br>
    <ul>
    <% @post.errors.full_messages.each do |msg| %>
      <li><%= msg %></li>
    <% end %>
    </ul>
  </div>
<% end %>
```

## More Freebies: `field_with_errors`

Let's look at another nice feature of `FormBuilder`. Here's our `form_for` code again:

```erb
<!--- app/views/posts/edit.html.erb //-->

<%= form_for @post do |f| %>
  <%= f.text_field :title %>
  <%= f.text_area :content %>
  <%= f.submit %>
<% end %>
```

The `text_field` call generates this tag:

```html
<input type="text" name="post[title]" id="post_title" value="Existing Post Title">
```

Not only will `FormBuilder` pre-fill an existing `Post` object's data, it will also wrap the tag in a `div` with an error class if the field has failed validations(s):

```html
<div class="field_with_errors">
  <input type="text" name="post[title]" id="post_title" value="Existing Post Title">
</div>
```

This can also result in some unexpected styling changes because `<div>` is a blocking tag (which takes up the entires width of its container) while `<input>` is an inline tag. If your layout suddenly gets messed up when a field has errors, this is probably why.

## Recap

When in doubt, **read the HTML.** Get used to hitting the "View Source" and "Open Inspector" hotkeys in your browser (`Ctrl-u` and `Ctrl-Shift-i` on Chrome Windows; `Option-Command-u` and `Option-Command-i` on Chrome Mac), and remember that most browsers let you [examine `POST` data in their developer network tools](https://superuser.com/questions/395919/where-is-the-post-tab-in-chrome-developer-tools-network).