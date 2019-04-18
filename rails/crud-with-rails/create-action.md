# Lesson: Create Action

## The Difference Between `save` and `create`

Both the `save` and `create` methods generate a SQL script that inserts a new record into the database; each of the object's attributes is passed into the SQL statement. However, the `save` method returns `true` upon a successful save, whereas the `create` method returns the object itself.

## The `create` Controller Action

To build the `create` action in our `PostsController`, we'll first create a new `post` object, populate its attributes with data grabbed from the `params` hash received through the user-submitted 'New Post' form, and then save the object, successfully persisting the new record to our database. Then, per convention, we will redirect to the new resource's `show` page. See the controller action here:

```ruby
# app/controllers/posts_controller.rb

def create
  @post = Post.new
  @post.title = params[:title]
  @post.description = params[:description]
  @post.save
  redirect_to post_path(@post)
end
```

## Checking for A Successfully Persisted Record

There are a few ways to check to see if your record was successfully created in the database:

1. Type `Post.last` into the Rails console, and it will display the most recently created record. We can look at the record's `created_at` attribute to ensure the timestamp is current.
2. We can simply scroll up through the Rails server logs. All SQL statements are printed out in the log, so it's just a matter of locating the correct `INSERT` statement.

### Example `INSERT` Statement

```bash
1     (0.1ms)   begin transaction
2   SQL (0.7ms)   INSERT INTO "posts" ("title", "description", "created_at", "updated_at") VALUES (?, ?, ?, ?) [["title", "My Post"], ["description", "My desc"], ["created_at", "2015-12-26 18:00:31.393419"], ["updated_at", "2015-12-26 18:00:31.393419"]]
3    (2.2ms)    commit transaction
```