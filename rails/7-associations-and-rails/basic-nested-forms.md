# Lesson: Basic Nested Forms

## Data Model

Let's say we're writing an address book. Each `Person` can have multiple addresses. Each `Address` has a bunch of address info fields. Our data models looks like this:

- `Person`
  - has many `addresses`
  - has a `name` (string)
- `Address`
  - has one `person`
  - has the first line of the street address stored as `street_address_1` (string)
  - has the second line of the street address stored as `street_address_2` (string)
  - has a `city` (string)
  - has a `state` (string)
  - has a `zipcode` (string)
  - has an `address_type` (string)

## Creating People

How do we write our `Person` form? We don't want to require our user to first create an `Address`, then create that `Person`. That's annoying. We want a single form for a `Person` containing several slots for their `addresses`.

Previously, we wrote setters like `Song#artist_name=` to find or create an `Artist` and connect them to the song.

That won't work here, because an address contains more than one field. In the `Artist` case we were just doing the `name`. With `Address`, it's "structured data". All that really means is it has multiple fields attached to it. When we build a form for it, the form will send a different key for each field in each address. This can get a bit unwieldy so we generally try to group a hash within the `params` hash, which makes things much neater. Spoiler alert: Rails has a way to send this across as a hash.

The complete `params` object for creating a `Person` will look like the following. Using "0" and "1" as keys can seem a bit odd, but it makes everything else work moving forward. This hash is now more versatile. You can access nested values the standard way, with `params[:person][:addresses_attributes]["0"]` returning all of the information about the first address.

Notice the `addresses_attributes` key. That key is similar to the `artist_name` key we used previously. Last time, we handled that by writing a `artist_name=` method. In this case, we're going to do something _super_ similar. Instead of writing our own `addresses_attributes=` method, we'll let Rails take care of it for us. We're going to use `accepts_nested_attributes_for` and the `fields_for` FormHelper.

Last time, we first wrote our setter method in the model. This time let's modify our `Person` model to include an `accepts_nested_attributes_for :addresses` line.

```ruby
# app/models/person.rb

class Person < ActiveRecord::Base
  has_many :addresses
  accepts_nested_attributes_for :addresses
end
```

Now open up `rails c` and run our `addresses_attributes` method that was created for us by `accepts_nested_attributes_for`. You'll notice that we have a method called `addresses_attributes=`. You didn't write that; `accepts_nested_attributes_for` wrote that. Then when we called `new_person.save` it created both the `Person` object and the two `Address` objects.

Now, we just need to get our form to create a `params` hash like that. Easy peasy. We are going to use `fields_for` to make this happen.

```erb
<!-- app/views/people/new.html.erb -->

<%= form_for @person do |f| %>
  <%= f.label :name %>
  <%= f.text_field :name %><br>

  <%= f.fields_for :addresses do |addr| %>
    <%= addr.label :street_address_1 %>
    <%= addr.text_field :street_address_1 %><br>

    <%= addr.label :street_address_2 %>
    <%= addr.text_field :street_address_2 %><br>

    <%= addr.label :city %>
    <%= addr.text_field :city %><br>

    <%= addr.label :state %>
    <%= addr.text_field :state %><br>

    <%= addr.label :zipcode %>
    <%= addr.text_field :zipcode %><br>

    <%= addr.label :address_type %>
    <%= addr.text_field :address_type %>
  <% end %>

  <%= f.submit %>
<% end %>
```

The `fields_for` line gives something nice and English-y. In that block are the fields for the addresses. Love Rails.

## Creating Stubs

We're asking Rails to generate `fields_for` each of the `Person`'s addresses. However, when we first create a `Person`, they have no addresses. Just like `f.text_field :name` will have nothing in the text field if there is no name, `f.fields_for :addresses` will have no address fields if there are no addresses.

We'll take the most straightforward way out: when we create a `Person` in the `PeopleController`, we'll add two empty addresses to fill out. The final controller looks like this:

```ruby
# app/controllers/people_controller.rb

class PeopleController < ApplicationController
  def new
    @person = Person.new
    @person.addresses.build(address_type: 'work')
    @person.addresses.build(address_type: 'home')
  end

  def create
    person = Person.create(person_params)
    redirect_to people_path
  end

  def index
    @people = Person.all
  end

  private
    def person_params
      params.require(:person).permit(:name)
    end
end
```

Now, refresh the page and you'll see two lovely address forms. Try to hit submit, and it isn't going to work. One last hurdle. We have new `params` keys, which means we need to modify our `person_params` method to accept them. Your `person_params` method should now look like this:

```ruby
# app/controllers/people_controller.rb

def person_params
  params.require(:person).permit(
    :name,
    addresses_attributes: [
      :street_address_1,
      :street_address_2,
      :city,
      :state,
      :zipcode,
      :address_type
    ]
  )
end
```

## Avoiding Duplicates

One situation we can't use `accepts_nested_attributes_for` is when we want to avoid duplicates of the row we're creating. In some instances we'll want duplicate rows, but say we have a database of songs and artists. We would want `Artist` rows to be unique, so that `Artist.find_by(name: 'Tori Amos').songs` returns what we'd expect. If we want to be able to create artists _while_ creating songs, we'll need to use `find_or_create_by` in our `artist_attributes=` method:

```ruby
# app/models/song.rb

class Song < ActiveRecord::Base
  def artist_attributes=(artist)
    self.artist = Artist.find_or_create_by(name: artist.name)
    self.artist.update(artist)
  end
end
```

This looks up existing artists by name. If no matching artist if found, on is created. Then we update the artist's attributes with the ones we were given. We could also choose to do something else if we didn't want to allow bulk assigning of an artist's information through a song.

Note that `accepts_nested_attributes_for` and setter methods (e.g., `artist_attributes=`) aren't necessarily mutually exclusive. It's important to evaluate the needs of your specific use case and choose the approach that makes the most sense. Keep in mind, too, that setter methods are useful for more than just avoiding duplicates—that's just one domain where they come in handy.