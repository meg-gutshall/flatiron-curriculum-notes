---
description: 'Version 8: Module 14: Section 6: Code-along'
---

# Rendering Related Object Data in JSON

Using `only` and `except`, we can be selective in what attributes we want to render to JSON in our basic Rails API. But what if we want to be _inclusive_ rather than selective? With Rails models, we're often dealing with many different related objects. Using `include` when rendering JSON, our API can send data about one resource along with data about its associated resources.

## Setting Up Additional Related Resources to Include

In our birdwatching app, we already have the `Bird` resource created with `name` and `species` attributes. It seems that the next logical step would be to create a location-based _bird sighting_ system so next, let's build the `Location` resource to connect specific birds to specific locations. We'll use the built-in Rails model generator and give `Location` the `latitude` and `longitude` attributes:

```bash
rails g model location latitude:float longitude:float
```

Now, we'll create the `Sighting` resource to connect a specific bird and location. A bird sighting in real life is an event that ties birds to their locations at a specific time. Similarly, a `Sighting` will do the same by tying one `Bird` to one `Location`. Let's use Rails' built-in resource generator to create `Sighting` and add its associations:

```bash
rails g resource sighting bird:belongs_to location:belongs_to
```

This generates a migration with associations:

```ruby
class CreateSightings < ActiveRecord::Migration[5.2]
  def change
    create_table :sightings do |t|
      t.belongs_to :bird, foreign_key: true
      t.belongs_to :location, foreign_key: true

      t.timestamps
    end
  end
end
```

Running `rails db:migrate` now will produce a slightly different schema, but if we look at the file, we see it still connects the `"birds"` and `"locations"` tables to the `"sightings"` table by id:

```ruby
create_table "sightings", force: :cascade do |t|
  t.integer "bird_id"
  t.integer "location_id"
  t.datetime "created_at", null: false
  t.datetime "updated_at", null: false
  t.index ["bird_id"], name: "index_sightings_on_bird_id"
  t.index ["location_id"], name: "index_sightings_on_location_id"
end
```

The other effect of using `belongs_to` in the generator is that it will add relationships automatically to the generated model:

```ruby
class Sighting < ApplicationRecord
  belongs_to :bird
  belongs_to :location
end
```

The other models will remain unaltered, so we'll have to update them. A bird may show up many times so it could be argued that a bird _has many_ sightings. The same would apply for a location. Through sightings, birds have many locations, and vice versa, so we would update our models to reflect these. Add the following relationships to the `Bird` and `Location` models:

```ruby
class Bird < ApplicationRecord
  has_many :sightings
  has_many :locations, through: :sightings
end
```

```ruby
class Location < ApplicationRecord
  has_many :sightings
  has_many :birds, through: :sightings
end
```

## Including Related Models in a Single Controller Action

In the `SightingsController`, now that the resources are created and connected, we should be able to confirm our data has been created by including a basic `show` action:

```ruby
def show
  sighting = Sighting.find_by(id: params[:id])
  render json: sighting
end
```

With the Rails server running, visiting `http://localhost:3000/sightings/1` should produce an object representing a _sighting_:

```javascript
{
  "id": 1,
  "bird_id": 1,
  "location_id": 2,
  "created_at": "2020-03-15T16:38:37.225z",
  "updated_at": "2020-03-15T16:38:37.225z"
}
```

> **NOTE:** Notice that the object includes its own `"id"` as well as the related `"bird_id"` and `"location_id"`. That is useful data. We _could_ use these values to send additional requests using JavaScript to get bird and location data if needed.

To include bird and location information in the controller action, now that our models are connected, the most direct way would be to build a custom hash like we did in the previous lesson:

```ruby
def show
  sighting = Sighting.find_by(id: params[:id])
  render json: { id: sighting.id, bird: sighting.bird, location: sighting.location }
end
```

This produces nested objects in our rendered JSON for `"birds"` and `"location"`:

```javascript
{
  "id": 2,
  "bird": {
    "id": 2,
    "name": "Grackle",
    "species": "Quiscalus Quiscula",
    "created_at": "2020-03-15T16:38:37.225z",
    "updated_at": "2020-03-15T16:38:37.225z"
  },
  "location": {
    "id": 2,
    "latitude": 30.26715,
    "longitude": -97.74306,
    "created_at": "2020-03-15T16:38:37.225z",
    "updated_at": "2020-03-15T16:38:37.225z"
  }
}
```

Often this works perfectly fine to get yourself started and is more than enough to begin testing with `fetch()` requests on a frontend.

## Using `include`

An alternative is to use the `include` option to indicate which models you want to nest:

```ruby
def show
  sighting = Sighting.find_by(id: params[:id])
  render json: sighting, include: [:bird, :location]
end
```

This produces similar JSON as the previous custom configuration:

```javascript
{
  "id": 2,
  "bird_id": 2,
  "location_id": 2,
  "created_at": "2020-03-15T16:38:37.225z",
  "updated_at": "2020-03-15T16:38:37.225z",
  "bird": {
    "id": 2,
    "name": "Grackle",
    "species": "Quiscalus Quiscula",
    "created_at": "2020-03-15T16:38:37.225z",
    "updated_at": "2020-03-15T16:38:37.225z"
  },
  "location": {
    "id": 2,
    "latitude": 30.26715,
    "longitude": -97.74306,
    "created_at": "2020-03-15T16:38:37.225z",
    "updated_at": "2020-03-15T16:38:37.225z"
  }
}
```

All attributes of included objects will be listed by default. Using `include` also works fine when dealing with an action that renders an array, like when we use `all` in `index` actions:

```ruby
def index
  sightings = Sighting.all
  render json: sightings, include: [:bird, :location]
end
```

As before with `only` and `except`, `include` is actually just another option that we can pass into the `to_json` method. Rails is just _obscuring_ this part:

```ruby
def index
  sightings = Sighting.all
  render json: sightings.to_json(include: [:bird, :location])
end

def show
  sighting = Sighting.find_by(id: params[:id])
  render json: sighting.to_json(include: [:bird, :location])
end
```

And adding some error handling on our `show` action:

```ruby
def show
  sighting = Sighting.find_by(id: params[:id])
  if sighting
    render json: sighting.to_json(include: [:bird, :location])
  else
    render json: { message: 'No sighting found with that id' }
  end
end
```

## Conclusion

We see now that within a single controller action, it is possible to render related models as nested JSON data! When nesting models in JSON, it is entirely possible to use `include` in conjunction with `only` and `exclude`:

```ruby
def show
  sighting = Sighting.find_by(id: params[:id])
  render json: sighting, include: [:bird, :location], except: [:updated_at]
end
```

But this begins to complicate things significantly as we work with nested resources and try to limit with _they_ display.

For example, to _also_ remove all instances of `created_at` and `updated_at` from the nested bird and location data in the above example, we'd have to add nesting into the _options_, so the included bird and location data can have their own options listed. Using the fully written `to_json` render statement can help keep thing a bit more readable here:

```ruby
def show
  sighting = Sighting.find_by(id: params[:id])
  render json: sighting.to_json(:include => {
    :bird => { :only => [:name, :species] },
    :location => { :only => [:latitude, :longitude] }
  }, :except => [:updated_at])
end
```

This does produce a more specific set of data:

```javascript
{
  "id": 2,
  "bird_id": 2,
  "location_id": 2,
  "created_at": "2020-03-15T16:38:37.225z",
  "bird": {
    "id": 2,
    "name": "Grackle",
    "species": "Quiscalus Quiscula"
  },
  "location": {
    "id": 2,
    "latitude": 30.26715,
    "longitude": -97.74306
  }
}
```

While it's neat, it seems silly to have to include such a complicated render line in our action. In addition, in this example we're only dealing with three models. Customizing what is rendered in a larger set of nested data could quickly turn into a major headache.

Now that we have covered how to customize and shape Rails model data into JSON, we can start to look at options for keeping data well-organized when building more complicated APIs.
