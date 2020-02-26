# Lesson: Rails Dynamic Request

## Dynamic Requests

A breakdown of the dynamic route process flow is below:

1. The `routes.rb` file takes in the request and processes it like normal, except this time it also parses the `id` as a parameter and passes it to the posts controller.
2. From that point, the controller action that you write will parse the `id` parameter and run a query on the model, storing the result in an instance variable.
3. Finally, the controller passes the instance variable to the associated view, which renders details of that specific record for the client.

In review, what's the difference between static and dynamic routes?

- Static routes render pages that have a hard coded path connected to them.
- Dynamic routes will render different data based on the parameters passed to the route.

## Code Implementation

In order to set up a dynamic request feature, we will start by writing a test to verify that the page exists:

```ruby
# spec/features/post_spec.rb

require 'rails_helper'

describe 'navigate' do
  before do
    @post = Post.create(title: "My Post", description: "My post desc")
  end

  it 'loads the show page' do
    visit "/posts/#{@post.id}"
    expect(page.status_code).to eq(200)
  end
end
```

To get this test to pass, we need to draw a route in `config/routes.rb` that maps to a show action in the `PostsController`:

```ruby
# config/routes.rb

get 'posts/:id', to: 'posts#show'
```

We will also need to create the `PostsController` and define a `show` action:

```ruby
# app/controllers/posts_controller.rb

class PostsController < ApplicationController
  def show
    @post = Post.find(params[:id])
  end
end
```

Lastly, we'll need to add a `posts` folder in the `views` directory and create a `show.html.erb` file inside the new `views/posts` directory.

### Resource Routing

Instead of using our `get` route, we can use Ruby's RESTful defaults and the `resources` method with the `only` option:

```ruby
# config/routes.rb

resources :posts, only: :show
```
