# Lesson: `form_for` on Edit

## Recap of `form_tag`

To review, the `form_tag` helper method allows us to automatically generate HTML form code and integrate date to both auto fill the values as well as have the form submit data that the controller can use to either create or update a record in the database. It allows for you to pass in: the route for where the parameters for the form will be sent, the HTTP method that the form will utilize, and the attributes for each field.

## Issues with Using `form_tag`

Before we get into the benefits and features of the `form_for` method, let's first discuss some of the key drawbacks to utilizing `form_tag`:

- Our form must be manually passed to the route where the form parameters will be submitted
- The form has no knowledge of the form's goal; it doesn't know if the form is mean to create or update a record
- You're forced to have duplicate code throughout the form; it's hard to adhere to DRY principles when utilizing the `form_tag`

## Difference Between `form_for` and `form_tag`

The differences between `form_for` and `form_tag` are subtle, but important. We'll start with talking about them at a high level perspective and then get into each one of the aspects on a practical/implementation basis:

- The `form_for` method accepts the instance of the model as an argument. Using this argument, `form_for` is able to make a bunch of assumptions for you.
- `form_for` yields an object of class `FormBuilder`
- `form_for` automatically knows the standard route (it follows RESTful conventions) for the form data as opposed to having to manually declare it
- `form_for` gives the option to dynamically change the `submit` button text (this comes in very handy when you're using a form partial and the `new` and `edit` pages will share the same form)

A good rule of thumb for when to use one approach over the other is below:

- Use `form_for` when your form is directly connected to a model.
- Use `form_tag` when you simply need an HTML form generated. Examples of this would be: a search form field or a contact form.

## Implementation of `form_for`

Below is an example `edit` form for a `post` object:

```erb
<h3>Edit Post</h3>

<%= form_for @post do |f| %>
  <%= f.label 'Post title: ' %><br>
  <%= f.text_field :title %><br>

  <%= f.label 'Post description: ' %><br>
  <%= f.text_area :description %><br>

  <%= f.submit %>
<% end %>
```

- `form_for` is smart enough to know that since it's dealing with a pre-existing record, we want to utilize `PUT` or `PATCH` over `POST` for the HTTP method.

Because `form_for` is bound directly with the `Post` model, we need to pass the model name into the ActiveRecord `update` method in the controller. We can do this two ways:

```ruby
# Option 1
def update
  @post = Post.find(params[:id])
  @post.update(params.require(:post))
  redirect_to post_path(@post)
end

# Option 2
def update
  @post = Post.find(params[:id])
  @post.update(title: params[:post][:title], description: params[:post][:description])
  redirect_to post_path(@post)
end
```