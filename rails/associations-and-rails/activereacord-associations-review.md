# Lesson: ActiveRecord Associations Review

ActiveRecord associations are an iconic Rails feature. They allow developers to work with complex networks of related models without having to write a single line of SQL—as long as all of the names line up!

## Foreign Keys

It all starts in the database. **Foreign keys** are columns that refer to the primary key of another table. Conventionally, foreign keys in ActiveRecord are comprised of the name of the model you're referencing, and `_id`. So for example if the foreign key was for a `posts` table, it would be `post_id`.

Like any other column, foreign keys are accessible through instance methods of the same name. For example, a migration that looks like this:

```ruby
class AddAuthorIdToPosts < ActiveRecord::Migration
  def change
    change_table :posts do |t|
      t.integer :author_id
    end
  end
end
```

Would mean you could find a post's author with the following ActiveRecord query:

```ruby
Author.find(@post.author_id)
```

Which is equivalent to the SQL:

```bash
SELECT * FROM authors WHERE id = #{@post.author_id}
```

And you could look up an author's posts like this:

```ruby
Post.where("author_id = ?", @author.id)
```

Which is equivalent to the SQL:

```bash
SELECT * FROM posts WHERE author_id = #{@author.id}
```

This is all great, but Rails is always looking for ways to save us keystrokes.

## Many-to-One Relationships

By using ActiveRecord's macro-style association class methods, we can add some convenient instance methods to our models. The most common relationship is **many-to-one**, and it is declared in ActiveRecord with `belongs_to` and `has_many`.

### `belongs_to`

Each `Post` is associated with **one** `Author`.

```ruby
class Post < ActiveRecord::Base
  belongs_to :author
end
```

We now have access to some new instance methods, like `author`. This will return the actual `Author` object that is attached to that `@post`.

```ruby
@post.author_id = 5
@post.author  # => #<Author id=5>
```

### `has_many`

In the opposite direction, each `Author` might be associated with zero, one, or many `Post` objects. We haven't changes the schema of the `authors` table at all; ActiveRecord is just going to use `posts.author_id` to do all of the lookups.

```ruby
class Author < ActiveRecord::Base
  has_many :posts
end
```

Now we can look up an author's posts just as easily:

```ruby
@author.posts  # => [#<Post id=3>, #<Post id=8>]
```

Remember, ActiveRecord uses its [Inflector](https://api.rubyonrails.org/classes/ActiveSupport/Inflector.html) to switch between the singular and plural forms of your models.

| Name | Data |
| --- | --- |
| Model | `Author` |
| Table | `authors` |
| Foreign Key | `author_id` |
| `belongs_to` | `:author` |
| `has_many` | `:authors` |

Like many other ActiveRecord class methods, the symbol you pass determines the name of the instance method that will be defined. So `belongs_to :author` will give you `@post.author`, and `has_many :posts` will give you `@author.posts`.

## Convenience Builders

### Building A New Item in A Collection

If you want to add a new post for an author, you might start this way:

```ruby
new_post = Post.new(author_id: @author.id, title: "Web Development for Cats")
new_post.save
```

But the association macros save the day again, allowing this instead:

```ruby
new_post = @author.posts.build(title: "Web Development for Cats")
new_post.save
```

This will return a new `Post` object with the `author_id` already set for you! We use this one as much as possible because it's just easier. `build` works just like `new`. So the instance that is returned isn't quite saved to the database just yet. You'll need to `#save` the instance when you want it to be persisted to the database.

### Setting A Singular Association

The setup process is a little bit less intuitive for singular associations. Remember, a post `belongs_to` an author. The verbose way of creating this association would be like so:

```ruby
@post.author = Author.new(name: "Leeroy Jenkins")
```

Remember, if you used the `build_` option, you'll need to persist your new `author` with `#save`.

These methods are also documented in the [Rails Associations Guide](https://guides.rubyonrails.org/association_basics.html).

### Collection Convenience

If you add an existing object to a collection association, ActiveRecord will conveniently take care of setting the foreign key for you:

```ruby
@author = Author.find_by(name: "Leeroy Jenkins")
@author.posts
# => []
@post = Post.new(title: "Web Development for Cats")
@post.author
# => nil
@author.posts << @post
@post.author
# => #<Author @name="Leeroy Jenkins">
```

## One-to-One Relationships

Profiles can get pretty complex, so in large applications it can be a good idea to give them their own model. In this case:

- Every author would have one, and only one, profile.
- Every profile would have one, and only one, author.

`belongs_to` makes another appearance in this relationship, but instead of `has_many` the other model is declared with `has_one`.

If you're not sure which model should be declared with which macro, it's usually a safe bet to put `belongs_to` on whichever model has the foreign key column in its database table.

## Many-to-Many Relationships and Join Tables

Each author has many posts, each post has one author. So let's shake things up and think about tags.

- One-to-One doesn't work because a post can have multiple tags.
- Many-to-One doesn't work because a tag can appear on multiple posts.

Because there is no "owner" model in this relationship, there's also no right place to put the foreign key column. Enter the join table.

ActiveRecord has a migration method for creating join tables:

```ruby
create_join_table :posts, :tags
```

This will create a table called `posts_tags`.

### `has_many :through`

To work with the join table, both our `Post` and `Tag` models will have a `has_many` association with the `posts_tags` table. We also still need to associate `Post` and `Tag` themselves. Ideally, we'd like to be able to call a `@my_post.tags` method, right? That's where `has_many :through` comes in. First, let's add the `has_many :posts_tags` line to our `Post` and `Tag` models:

```ruby
class Post
  has_many :posts_tags
end

class PostsTags
  belongs_to :post
  belongs_to :tag
end

class Tag
  has_many :posts_tags
end
```

So now we can run code like `@post.posts_tags` to get all the join entries. This is kinda sorta what we want. What we really want is to be able to call `@post.tags`, so we need one more `has_many` relationship to complete the link between tags and posts: `has_many :through`. Essentially, our `Post` model has many `tags` _through_ the `posts_tags` table, and vice versa. Let's write that out:

```ruby
class Post
  has_many :posts_tags
  has_many :tags, through: :posts_tags
end

class PostsTags
  belongs_to :post
  belongs_to :tag
end

class Tag
  has_many :posts_tags
  has_many :posts, through: :posts_tags
end
```

Great, we've unlocked out `@post.tags` and `@tag.posts` methods!

## Summary

For every relationship, there is a foreign key somewhere. Foreign keys correspond to the `belongs_to` macro on the model.

One-to-one and many-to-one relationships only require a single foreign key, which is stored in the 'subordinate' or 'owned' model. The other model declares its relationship via a `has_one` or `has_many` statement, respectively.

Many-to-many relationships require a join table containing a foreign key for both models. The models are joined using `has_many :through` statements.

You can see the entire [list of class methods](https://api.rubyonrails.org/classes/ActiveRecord/Associations/ClassMethods.html) in the Rails API docs.