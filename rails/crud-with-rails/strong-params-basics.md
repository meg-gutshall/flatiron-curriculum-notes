# Lesson: Strong Params Basics

## Notes and Code Examples

### What Are Strong Params?

Parameters that are whitelisted as permitted when sending form data from a Rails application to the database.

### Code Implementation

- To enable Strong Params, open up `config/application.rb` and delete the line that says: `config.action_controller.permit_all_parameters = true`.
- Now when we submit a form, we get a `ForbiddenAttributesError`.
  - This means that Rails needs to be told what parameters are allowed to be submitted through the form to the database because now, the default is to let _nothing_ through.
    - The same error would occur if you were trying to update a record.
- We use the `permit` method chained on to the `require` method (which is chained on to the `params`) to specify which attributes are allowed to be submitted.

#### Permit vs. Require

The `#require` method is the most restrictive. It means that the `params` that gets passed in **must** contain a key called "post". If it's not included, then it fails and the user gets an error. The `#permit` method is a bit looser. It means that the `params` hash **may** have whatever keys are in it. So in the `create` case, it may have the `:title` and `:description` keys. If it doesn't have one of those keys, it's no problem—the hash just won't accept any other keys.

### DRYing Up Strong Params

It's standard Rails practice to remove code repetition, so let's abstract the strong parameter call into its own method in the controller:

```ruby
# app/controllers/posts_controller.rb

def create
  @post = Post.new(post_params(:title, :description))
  @post.save
  redirect_to post_path(@post)
end

def update
  @post = Post.find(params[:id])
  @post.update(post_params(:title))
  redirect_to post_path(@post)
end

private
  def post_params(*args)
    params.require(:post).permit(*args)
  end
```

Now, both our `create` and `update` methods in the `posts` controller can simply call `post_params`.