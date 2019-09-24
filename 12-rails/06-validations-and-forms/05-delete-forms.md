# Lesson: Delete Forms

So far, we've worked with three pieces of the CRUD puzzle:

- Creating records, using HTTP `POST` requests.
- Reading records, using HTTP `GET` requests.
- Updating records, using HTTP `PATCH` requests.

One piece remains:

- Deleting records, using HTTP `DELETE` requests.

In many cases, sending a request with the `PATCH` or `DELETE` method will not work. In this lesson, we'll focus on `DELETE`, but many of the same issues arise with `PATCH` requests as well.

## Setting Up Our Routes and Forms

Before we dive into the problem with `DELETE` (and `PATCH`) requests, let's proceed as if we were none the wiser, setting up our route and form as usual:

```ruby
# config/routes.rb

delete '/people/:id', to: 'people#destroy', as: 'person'
```

```erb
<!-- app/views/people/show.html.erb -->

<h2><%= @person.name %></h2>
<%= @person.email %>
<%= form_tag person_path(@person.id), method: "delete" do %>
  <%= submit_tag "Delete #{@person.name}" %>
<% end %>
```

Now our HTML output:

```html
<!-- app/views/people/show.html.erb -->

<h2>Caligula</h2>
caligula@rome-circe-40-AD.com
<form accept-charset="UTF-8" action="/people/1" method="POST">
  <input name="_method" type="hidden" value="DELETE">
  <input name="utf8" type="hidden" value="&#x2713;">
  <input name="authenticity_token" type="hidden" value="f755bb0ed134b76c432144748a6d4b7a7ddf2b71">
  <input name="commit" type="submit" value="Delete Caligula">
</form>
```

## Rails Magic at Work

As of HTML5, forms officially do not support `DELETE` and `PATCH` for their methods.

What you're seeing in the above `#form_tag()` behavior is a **workaround** implemented for us by Rails itself. With this in mind, we get the best of both worlds:

- We get to be **good HTTP-abiding citizens** who use the correct request methods for their corresponding goals (`GET` for read, `PATCH` for update, and so on).
- We get to **maintain our sanity** and not worry about W3C drama while writing views.

Thus enlightened, we can (finally) proceed with our original goal:

```ruby
# app/controllers/people_controller.rb

def destroy
  Person.find(params[:id]).destroy
  redirect_to people_url
end
```

Nothing too special happening here except for a bit of method-chaining to immediately destroy the found instance.

## Fancy JavaScript Helper

As shown, you have to go to a user's `show` page to delete them. What if we want an admin control panel where users can be deleted from a list?

```erb
<!-- app/views/people/show.html.erb -->

<% @people.each do |person| %>
<div class="person">
  <span><%= person.name %></span>
  <%= link_to "Delete", person, method: :delete, data: {confirm: "Really?"} %>
</div>
<% end %>
```

[`link_to`](http://api.rubyonrails.org/classes/ActionView/Helpers/UrlHelper.html#method-i-link_to) is a method of `UrlHelper` that has a number of convenient features.

The HTML generated at that call to `link_to` looks like this:

```html
<a data-confirm="Really?" rel="nofollow" data-method="delete" href="/people/1">Delete</a>
```

The `data-confirm` attribute and the `data-method` attribute rely on some JavaScript built into Rails.

`data-method` will "submit" a `DELETE` request as if a form had been submitted. It will use `GET` (the default method used by all browsers for HTML links) if the user has JavaScript disabled.

`data-confirm` pops up a confirmation window before the link is followed, allowing the user to make sure they're ready to delete someone forever.
