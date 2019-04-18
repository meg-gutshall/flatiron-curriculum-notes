# Lesson: Edit/Update Action

## Rails Controller Conventions

There is a trend in Rails conventions where the logic for rendering a form is separate from the action that manages the database record alteration. For example:

- The `new` action in the controller simply renders the `new` form
- The `create` action is what actually handles the process of inserting the form data into the database

In like fashion, the `edit` and `update` actions have a similar convention:

- The `edit` action will handle rendering the `edit` form
- The `update` action will be the method that updates the database record itself

## Rendering the `edit` Form

### Routes

To start off, let's draw a `get` route for our edit form. Since the form will need to know which record is being edited, this will need to be a dynamic route that accepts an `:id` as a parameter that the controller can access:

```ruby
get 'articles/:id/edit', to: 'articles#edit', as: :edit_article
```

We still need to draw one additional route to handle the `update` action. This second route will also need to be dynamic, accepting the same `:id` as a parameter so that the action will know which record is being altered.

```ruby
patch 'articles/:id', to: 'articles#update'
```

**NOTE:** `PUT` is meant to be used when replacing a whole resource. `PATCH` is used for sending a set of changes to a resource.

### Controllers

With our routes in place, let's add the controller actions to `app/controllers/articles_controller.rb`:

```ruby
def edit
  @article = Article.find(params[:id])
end

def update
  @article = Article.find(params[:id])
  @article.update(title: params[:article][:title], description: params[:article][:description])
  redirect_to article_path(@article)
end
```

### Views

Create a new view template in `app/views/articles/edit.html.erb`. Since the `edit` view template has access to the `Article` object (stored in `@article`), we need to refactor the form so that it auto-fills the form fields with the corresponding data from `@article`. We'll also use a different form helper, `form_for`, which will automatically set up the url where the form will be sent, as seen below:

```erb
  <%= form_for @article do |f| %>
    <%= f.label 'Article Title' %><br>
    <%= f.text_field :title %><br>

    <%= f.label 'Article Description' %><br>
    <%= f.text_area :description %><br>

    <%= f.submit "Submit Article" %>
  <% end %>
```

In this case, `form_for` takes care of some work for us. Using the object `@article` we've provided, `form_for` determines that `@article` is **not a _new_ instance** of the `Article` class. Because of this, `form_for` knows to automatically send to the _update_ path. Since `@article` is not a new instance of `Article`, the inputs on this form will be populated with the corresponding object values. When submitted, the form will be routed to the `update` action.