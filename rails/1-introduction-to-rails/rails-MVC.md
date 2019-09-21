# Lesson: Rails MVC

## Model View Controller Overview

- **Model**: The model manages the critical aspects of the application. It has direct access to specific database records and it's where your logic should mainly reside.
- **Controller**: The controller transmits data requests from the user to the model, adn then delivers data that is rendered in the view to the user.
- **View**: The view shouldn't contain any programming logic; only render what the controller sends it.

## Routing, File Naming Conventions, and Data Flow

- **Rails was created with the concept of convention over configuration.**
- View files correspond directly to controller files, which speak directly with models.
- For example, imagine you have a blog that has a database table called `posts`. You will have the following set of files:
  - A `post.rb` model file that will contain: validations, database relationships, callbacks, and any custom logic for posts.
  - A `post_controller.rb` file that will have methods to manage data flow for the Post behavior, including the full set of CRUD features. The standard methods are: `index`, `new`, `create`, `show`, `edit`, `update`, and `destroy`.
  - A `views/` directory that will contain a corresponding view for each of the pages that the end user will access. For a CRUD-based model, a few of the standard views would include: an `index` view to show all records, a `show` page that shows a specific record, and then `new` and `edit` pages that each render a form.

## Request Flow

![Flatiron's request flow graphic](https://github.com/meg-gutshall/flatiron-curriculum-notes/blob/master/public/images/rails/mvc_flow_updated.png)

## Roles and Responsibilities

### Models

- At the end of the day, the model file is a Ruby class.
- If it has a corresponding database table, it will inherit from the `ActiveRecord::Base` class.
  - This means that you can use the Active Record database helper methods with the model as well as treat it like a regular Ruby class (i.e. create methods, use data attributes, etc.)
- It is important to remember to follow the single responsibility principle for your model class files.
  - If any of the methods that you place in the model perform tasks outside the scope of that specific model, they should probably be moved to their own class.

### Controllers

- As mentioned before, the controllers connect the models, views, and routes.
  - The view looks to the controller adn only has access to the instance variables that the controller makes available. Those instance variables will contain any/all data coming in from the database.
  - The routes file looks to the controller and ensures that the methods in the controller match the items in the routes file.

### Views

- In a Rails application, the view files should contain the least amount of logic of any of the files in the model-view-controller architecture. The role of the view is to simply render whatever it is sent from the database.
- Rails supplies built-in ActionView helper methods that you can implement to efficiently code the views.

#### ActionView Method

The following erb code:

```erb
<%= div_for(@post, class: "post-index-page") do %>
  <p><%= @post.title %> <%= @post.summary %></p>
<% end %>
```

Translated to the following HTML markup:

```html
<div id="post_42" class="post post-index-page">
  <p><strong>My Amazing Blog Post</strong> With an incredible summary</p>
</div>
```