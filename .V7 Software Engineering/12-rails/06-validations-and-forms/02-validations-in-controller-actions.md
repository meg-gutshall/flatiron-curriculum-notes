# Lesson: Validations in Controller Actions

Now that we know Rails automatically performs validations defined on models, let's use this information to help users fix typos or other problems in their form submissions. At this point, we'll be covering step two of the following flow:

1. User fills out the form and hits "Submit", transmitting the form data via a POST request.
2. **The controller sees that validations have failed, and re-renders the form.**
3. The view displays the errors to the user.

## Manually Checking Validation

Up until this point, our `create` action has looked something like this:

```ruby
# app/controllers/posts_controller.rb

def create
  @post = Post.create(post_params)

  redirect_to post_path(@post)
end
```

However, we have two problems now:

1. If the post is invalid, there will be no `show` path to redirect to. The post was never saved to the database, so the `post_path` will result in a 404.
2. If we redirect, we start a new page load, which will lost all of the feedback from the validations.

## A Note About Page Loads

When a form is submitted, a **full page load** occurs, as if you had navigated to a completely new URL. This means that all of the variables set by the controller's `new` action (like `@post`) _disappear_ and are unavailable to the `create` action.

- The browser throws everything out after each request, except for cookies.
- Rails throws everything out after each request, except for the `session` hash.
- You're probably used to validation happening almost instantaneously on websites that you interact with on a daily basis. When you get validation feedback _without_ a full page load, that's JavaScript at work, sneakily performing requests in the background without throwing away the current page.

For now, let's use `valid?` to see what's going on before deciding how to respond:

```ruby
# app/controllers/posts_controller.rb

def create
  # Create a brand new, unsaved, not-yet-validated Post object from the form.
  @post = Post.new(post_params)

  # Run the validations WITHOUT attempting to save to the database, returning
  # true if the Post is valid, and false if it's not.
  if @post.valid?
    # If--and only if--the post is valid, do what we usually do.
    @post.save
    # This returns a new status code of 302, which instructs the browser to
    # perform a NEW REQUEST! (AKA: throw @post away and let the show action
    # worry about re-reading it from the database)
    redirect_to post_path(@post)
  else
    # If the post is invalid, hold on to @post, because it is not full of
    # useful error messages, and re-render the :new page, which knows how
    # to display them alongside the user's entries.
    render :new
  end
end
```

`render` can be instructed to render the templates from other actions. In the above code, since we want the `:new` template from the same controller, we don't have to specify anything except the template name. You can read more about this (and other) creative use(s) of `render` in Section 2.2.2 of the Rails Guides on [Layout and Rendering](https://guides.rubyonrails.org/layouts_and_rendering.html#using-render).
