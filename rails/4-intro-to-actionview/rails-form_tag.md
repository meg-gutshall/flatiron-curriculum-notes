# Lesson: Rails `form_tag`

## Rendering the Form View

In order to render the new post form, we have to add code to a few other files. First, we'll need to add a `new_post_path` method to our `routes.rb` file:

```ruby
# config/routes.rb

resources :posts, only: [:index, :new]
```

Next, we need to add the `new` action to our `PostsController`:

```ruby
# app/controllers/posts_controller.rb

def new
end
```

Lastly, we have to create the actual template to hold our form at `app/views/posts/new.html.erb`.

## Submitting the Form

In order to submit the new post form, we have to draw a `create` route so that the routing system knows what to do when a `POST` request is sent to the `/posts` resource:

```ruby
# config/routes.rb

resources :posts, only: [:index, :new, :create]
```

If you run `rake routes`, you'll see we now have a `posts#create` action:

| Prefix | Verb | URI Pattern | Controller#Action |
| --- | --- | --- | --- |
| posts | GET | /posts(.:format) | posts#index |
|  | POST | /posts(.:format) | posts#create |
| new_post | GET | /posts/new(.:format) | posts#new |

Next, we need to add a `create` action to our `PostsController` and have it create a new `Post` object with the values from `params` and then redirect to the index page:

```ruby
# app/controllers/posts_controller.rb

def create
  Post.create(title: params[:post][:title], description: params[:post][:description])
  redirect_to posts_path
end
```

## What Is CSRF

"CSRF" stands for Cross-Site Request Forgery. Let's walk through a real-life example of a Cross-Site Request Forgery hack:

1. You go to your banking website and log in. After checking your balance, you open up a new tab in the browser and go to your favorite meme site.
2. Unbeknownst to you, the meme site is actually a hacking site that has scripts running in the background as soon as you land on their page.
3. One of the scripts on the site hijacks the banking session that's open in the other browser tab and submits a form request to transfer money to their account.
4. The banking form can't tell that the form request wasn't made by you, so it goes through the process as if you were the one who made the request.

One site making a request to another site via a form is the general flow of a Cross-Site Request Forgery. Rails blocks this from happening by default by requiring that a unique authenticity token be submitted with each form. This authenticity token is stored in the session and can't be hijacked by hackers. It performs a match check when the form is submitted, and it will throw an error if the token isn't there or doesn't match.

## Building the Form in HTML Using Form Helpers

- Just like Sinatra, Rails takes the user input entered into form field and stores it in the `params` hash. The `name` attribute for a given `input` field is used as the key within `params` at which the entered data is stored.
  - Traditionally, Rails apps use that `model[attribute]` syntax for `name` attributes.

`ActionView`, a sub-gem of Rails, provides a number of helper methods to assist with streamlining view template code.

### Pure HTML Form

```erb
<!-- app/views/posts/new.html.erb -->

<form action="<%= posts_path %>" method="POST">
  <label>Post title:</label><br>
  <input type="text" id="post_title" name="post[title]"><br>

  <label>Post description:</label><br>
  <textarea id="post_description" name="post[description]"></textarea><br>

  <input type="hidden" name="authenticity_token" value="<%= form_authenticity_token %>">
  <input type="submit" value="Submit Post">
</form>
```

### HTML Form with `ActionView` Helper Methods

```erb
<!-- app/views/posts/new.html.erb -->

<%= form_tag posts_path do %>
  <label>Post title:</label><br>
  <%= text_field_tag :'post[title]' %><br>

  <label>Post description:</label><br>
  <%= text_area_tag :'post[description]' %><br>

  <%= submit_tag "Submit Post" %>
<% end %>
```

- The `form_tag` Rails helper is smart enough to know that we want to submit the form via the `POST` method, and it automatically renders the HTML that we were writing by hand before. The `form_tag` method also automatically generates the necessary authenticity token, so we can remove the now-redundant `hidden_field_tag`.
- The form helpers are simply Ruby methods that accept arguments, such as the `name` attribute and any additional parameters related to the form's elements.
  - The `form_tag` points the action to the URL (or URL helper) that follows. The method for the form defaults to `POST`. If `PATCH` or `DELETE`is used, a hidden input with name `_method` is added to simulate the verb over `POST` and the `method: :PATCH` or `method: :DELETE` argument is passed to `form_tag`.
  - The `submit_tag` creates a submit button with the text `value` as the caption which can be passed in as a string.
  - Other form helpers include:
    - `button_tag`: By default, it will create a button tag with type `submit`, if type is not given.
    - `check_box_tag`: Creates a checkbox form input tag.
    - `color_field_tag`: Creates a text field of type "color".
    - `date_field_tag`: Creates a text field of type "date".
    - `datetime_field_tag`: Creates a text field of type "datetime-local".
    - `email_field_tag`: Creates a text field of type "email".
    - `field_set_tag`: Creates a field set for grouping HTML form elements.
    - `file_field_tag`: Creates a file upload field.
    - `hidden_field_tag`: Creates a hidden form input field used to transmit data that would be lost due to HTTP's statelessness or data that should be hidden from the user.
    - `image_submit_tag`: Displays an image which when clicked will submit the form.
    - `label_tag`: Creates a label element. Accepts a block.
    - `month_field_tag`: Creates a text field of type "month".
    - `number_field_tag`: Creates a number field.
    - `password_field_tag`: Creates a password field, a masked text field that will hide the user's input behind a mask character.
    - `radio_button_tag`: Creates a radio button; use groups of radio buttons named the same to allow users to select from a group of options.
    - `range_field_tag`: Creates a range form element.
    - `search_field_tag`: Creates a text field of type "search".
    - `select_tag`: Creates a dropdown selection box, or if the `:multiple` option is set to true, a multiple choice selection box.
    - `telephone_field_tag`: Creates a text field of type "tel".
    - `text_area_tag`: Creates a text input area; use a textarea for longer text inputs, such as blog posts or descriptions.
    - `text_field_tag`: Creates a standard text field; use these text fields to input smaller chunks of text like a username or a search query.
    - `time_field_tag`: Creates a text field of type "time".
    - `url_field_tag`: Creates a text field of type "url".
    - `week_field_tag`: Creates a text field of type "week".
