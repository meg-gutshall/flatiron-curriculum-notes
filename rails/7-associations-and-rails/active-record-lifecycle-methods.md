# Lesson: Active Record Lifecycle Methods

## Callbacks

Now that you are integrating Active Record into Rails, we must first have a quick discussion about how developers can control the "lifecycle" of our object. This means that it can be nice to inject our code every time Active Record does something to our model. There are a ton of different places we can inject our code. In this reading we are going to discuss the most common ones. Before we begin, some quick terminology. Everything we cover here is called "Active Record Lifecycle Callbacks". Many people just call them callbacks. It's a bit shorter.

Take a look at the blog app that is included. It's pretty simple. We have a `Post` model and a few views. The `Post` `belongs_to` an `Author`. Also in the `Post` model you'll notice a validation to make sure that post titles are in title case. Title case means every word starts with a capital letter.

We are going to use our first callback by calling a method provided by Rails called `#titlecase` that will take care of the title casing for us. We'll implement the callback similarly to how we use `has_many` or `validates` by writing it at the top of our model file. First let's write our method to actually run `#titlecase`.

```ruby
# app/models/post.rb

def make_title_case
  self.title = self.title.titlecase
end
```

### `before_validation`

Ok, now we want to run this whenever someone tries to save to the database, but which callback do we use?

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base
  belongs_to :author
  validate :is_title_case
  before_validation :make_title_case

  private

  def is_title_case
    if.title.split.any?{|w| w[0].upcase != w[0]}
      errors.add(:title, "Title must be in title case")
    end
  end

  def make_title_case
    self.title = self.title.titlecase
  end

end
```

We use the `before_validation` callback here to run our `#make_title_case` method first, _then_ run the `:is_title_case` validation, which will pass and save into our database.

### `before_save`

We use `before_save` for actions that need to occur that aren't modifying the model itself. For example, whenever you save to the database, let's send an email to the `Author` alerting them that the post was just saved.

This is a perfect `before_save` action. It doesn't modify the model so there is no validation weirdness, and we don't want to email the user if the `Post` is invalid. So if you had some method called `email_author_about_post`, you would modify your `Post` model to look like this:

```ruby
# app/models/post.rb

class Post < ActiveRecord::Base
  belongs_to :author
  validate :is_title_case
  before_validation :make_title_case
  before_save :email_author_about_post

  private

  def is_title_case
    if.title.split.any?{|w| w[0].upcase != w[0]}
      errors.add(:title, "Title must be in title case")
    end
  end

  def make_title_case
    self.title = self.title.titlecase
  end

end
```

Here's a rule of thumb: **Whenever you are modifying an attribute of the model, use `before_validation`. If you are doing some other action, the use `before_save`.**

### `before_create`

Let's cover one last callback that is super useful. `before_create` is very close to `before_save` with one major difference: it only gets called when a model is created for the first time. This means not every time the object is persisted, just when it is **new**.

For more information on all of the callbacks available to you, check out [this amazing Rails guide](https://guides.rubyonrails.org/active_record_callbacks.html).