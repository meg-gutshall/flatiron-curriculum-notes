# Lab: Custom JSON Rendering Using Rails

By using `render json:` in our Rails controller, we can take entire models or even collections of models, have Rails convert them to JSON, and send them out on request.

The way we structure our data matters—it can lead to better, simpler code in the future. By specifically defining what data is being sent via a Rails controller, we have full control over what data our frontend has access to.

## Adding Additional Routes to Separate JSON Data

The simplest way to make data more useful to us is to provide more routes and actions that help to divide and organize our data. For instance, we could add a `show` action to allow us to send specific record/model instances. First, we'd add a route:

```ruby
Rails.application.routes.draw do
  get '/birds' => 'birds#index'
  get '/birds/:id' => 'birds#show'
end
```

Then we could add an additional action:

```ruby
class BirdsController < ApplicationController
  def index
    birds = Bird.all
    render json: birds
  end

  def show
    bird = Bird.find_by(id: params[:id])
    render json: bird
  end
end
```

>**Reminder:** No need for instance variables anymore since we're immediately rendering `birds` and `bird` to JSON and are not going to be using ERB.

Now, visiting `http://localhost:3000/birds` will produce an array of `Bird` objects, but `http://localhost:3000/birds/2` will produce just one:

```json
{
  "id": 2,
  "name": "Grackle",
  "species": "Quiscalus Quiscula",
  "created_at": "2020-03-14T19:51:41.543z",
  "updated_at": "2020-03-14T19:51:41.543z"
}
```

We can use multiple routes to differentiate between specific requests. In an API, these are typically referred to as endpoints. A user of the API uses endpoints to access specific pieces of data. Just like a normal Rails app, we can create full CRUD-based controllers that only render JSON.

>**NOTE:** If you've ever tried using `rails generate scaffold` to create a resource, you'll find that this is the case. Rails has favored convention over configuration and will set up JSON rendering for you almost immediately out of the box.

In terms of communicating with JavaScript, even when sending POST requests, we do not need to change anything in our controller to handle a `fetch()` request compared to a normal user visiting a page. This means that you could go back to _any_ existing Rails project and all you would need to do is change the rendering portion of the controller to make it render JSON. And bam! You have a rudimentary Rails API!

Even though we are no longer serving up views the same way, maintaining RESTful conventions is still a HUGE plus here for your API end user (mainly yourself at the moment).

## Removing Context When Rendering

Sometimes when sending JSON data, such as an entire model, we don't want or need to send the entire thing. Some data is sensitive, for instance. An API that sends user information might contain details of a user internally that it does not want to ever share externally. Sometimes, data is just extra clutter we don't need. Consider the last piece of data:

```json
{
  "id": 2,
  "name": "Grackle",
  "species": "Quiscalus Quiscula",
  "created_at": "2020-03-14T19:51:41.543z",
  "updated_at": "2020-03-14T19:51:41.543z"
}
```

For our birdwatching purposes, we probably don't need bits of data like `created_at` and `updated_at`. Rather than send this unnecessary info when rendering, we could just pick and choose what we want to send:

```ruby
def show
  bird = Bird.find_by(id: params[:id])
  render json: {id: bird.id, name: bird.name, species: bird.species}
end
```

Here, we've created a new hash out of three keys, assigning the keys manually with the attributes of `bird`. The result is that when we visit a specific bird's endpoint, like `http://localhost:3000/bird/3`, we'll see just the id, name, and species:

```json
{
  "id": 3,
  "name": "Common Starling",
  "species": "Sturnus Vulgaris"
}
```

Another option would be to use Ruby's built-in `slice` method. On the `show` action, that would look like this:

```ruby
def show
  bird = Bird.find_by(id: params[:id])
  render json: bird.slice(:id, :name, :species)
end
```

This achieves the same result but in a slightly different way. Rather than having to spell out each key, the hash [`slice` method](https://ruby-doc.org/core-2.7.0/Hash.html#method-i-slice) returns a _new_ hash with only the keys that are passed into `slice`. In this case, `id`, `name`, and `species` were passed in, so `created_at` and `updated_at` get left out, just like before.

```json
{
  "id": 3,
  "name": "Common Starling",
  "species": "Sturnus Vulgaris"
}
```

While `slice` works fine for a single hash, it won't work for an array of hashes like the one we have in our `index` action:

```ruby
def index
  birds = Bird.all
  render json: birds
end
```

In this case, we can add in the `only:` option directly after listing an object we want to render to JSON:

```ruby
def index
  birds = Bird.all
  render json: birds, only: [:id, :name, :species]
end
```

Visiting or fetching `http://localhost:3000/birds` will now produce our array of bird objects and each object will _only_ have the `id`, `name`, and `species` values, leaving out everything else:

```json
[
  {
    "id": 1,
    "name": "Black-Capped Chickadee",
    "species": "Poecile Atricapillus"
  },
  {
    "id": 2,
    "name": "Grackle",
    "species": "Quiscalus Quiscula"
  },
  {
    "id": 3,
    "name": "Common Starling",
    "species": "Sturnus Vulgaris"
  },
  {
    "id": 4,
    "name": "Mourning Dove",
    "species": "Zenaida Macroura"
  }
]
```

Alternatively, rather than specifically listing every key we want to include, we could also exclude particular content using the `except:` option, like so:

```ruby
def index
  birds = Bird.all
  render json: birds, except: [:created_at, :updated_at]
end
```

The above code would achieve the same result, producing only `id`, `name`, and `species` for each bird. All the keys _except_ `created_at` and `updated_at`.

## Drawing Back the Curtain on Rendering JSON Data

The `only` and `except` keywords are actually parameters of the `to_json` method, obscured by Rails magic. The last code snippet can be rewritten in full to show what is actually happening:

```ruby
def index
  birds = Bird.all
  render json: birds.to_json(except: [:created_at, :updated_at])
end
```

As customization becomes more complicated, writing in full sometimes helps to clarify what is happening.

## Basic Error Messaging When Rendering JSON Data

With the power to create our own APIs, we also have the power to define what to do when things go wrong. In our `show` action, we are currently using `Bird.find_by`, passing in `id: params[:id]`:

```ruby
def show
  bird = Bird.find_by(id: params[:id])
  render json: { id: bird.id, name: bird.name, species: bird.species }
end
```

When using `find_by`, if the record is not found, `nil` is returned. As we have it set up, if `params[:id]` does not match a valid id, `nil` will be assigned to the `bird` variable.

As `nil` is a _falsy_ value in Ruby, this gives us the ability to write our own error messaging in the event that a request is made for a record that doesn't exist:

```ruby
def show
  bird = Bird.find_by(id: params[:id])
  if bird
    render json: { id: bird.id, name: bird.name, species: bird.species }
  else
    render json: { message: 'Bird not found' }
  end
end
```

Now, if we were to send a request to an invalid endpoint, rather than receiving a general HTTP error, we would still receive a response from the API:

```json
{
  "message": "Bird not found"
}
```

From here, we could build a more complex response, including additional details about what might have occurred.
