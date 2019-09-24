# Lesson: Login Required

## First Pass: Manual Checks

Let's say we have a `DocumentsController`. Its `show` method looks like this:

```ruby
# app/controller/documents_controller.rb

class DocumentsController < ApplicationController
  def show
    @document = Document.find(params[:id])
  end
end
```

Now let's add a new requirement: documents should only be shown to users when they're logged in. From a technical perspective, what does it actually mean for a user to _log in_? When a user logs in, all we are doing is using cookies to add their `:user_id` to their `session`.

The first thing you might do is to just add some code into `DocumentsController#show`:

```ruby
# app/controller/documents_controller.rb

class DocumentsController < ApplicationController
  def show
    return head(:forbidden) unless session.include? :user_id
    @document = Document.find(params[:id])
  end
end
```

The first line is a return guard. Unless the session includes `:user_id`, we return an error. `head(:forbidden)` is a controller method that returns the specified HTTP status code—in this case, if a user isn't logged in, we return `403 Forbidden`.

## Refactor

This code works fine, so you use it in a few places. Now your `DocumentsController` looks like this:

```ruby
# app/controller/documents_controller.rb

class DocumentsController < ApplicationController
  def show
    return head(:forbidden) unless session.include? :user_id
    @document = Document.find(params[:id])
  end

  def index
    return head(:forbidden) unless session.include? :user_id
  end

  def create
    return head(:forbidden) unless session.include? :user_id
    @document = Document.create(author_id: user_id)
  end

  def update
    return head(:forbidden) unless session.include? :user_id
    @document = Document.find(params[:id])
    # code to update a document
  end
end
```

That doesn't look so DRY. Fortunately, Rails gives us [`before_action`](http://guides.rubyonrails.org/action_controller_overview.html#filters). We can refactor our code like so:

```ruby
# app/controller/documents_controller.rb

class DocumentsController < ApplicationController
  before_action :require_login

  def show
    @document = Document.find(params[:id])
  end

  def index
  end

  def create
    @document = Document.create(author_id: user_id)
  end

  def update
    @document = Document.find(params[:id])
    # code to update a document
  end

  private
    def require_login
      return head(:forbidden) unless session.include? :user_id
    end
end
```

Let's look at the code we've added: `before_action :require_login`. This is a call to the ActionController class method `before_action`. `before_action` registers a filter. A filter is a method which runs before, after, or around a controller's action. In this case, the filter runs before all `DocumentsContoller`'s actions, and kicks requests out with `403 Forbidden` unless they're logged in.

## Skipping Filters for Certain Actions

What if we wanted to let anyone see a list of documents, but keep the `before_action` filter for other `DocumentsController` methods? We could do this:

```ruby
# app/controllers/documents_controller.rb

class DocumentsController < ApplicationController
  before_action :require_login
  skip_before_action :require_login, only: [:index]

  ...

end
```

The `skip_before_action` class method tells Rails to skip the `require_login` filter only on the `index` action.

## Resources

[Action Controller Overview — 8, Filters](http://guides.rubyonrails.org/action_controller_overview.html#filters)
