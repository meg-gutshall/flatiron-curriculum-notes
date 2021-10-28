---
description: 'Version 8: Module 14: Section 6: Lesson'
---

# Creating a Rails API from Scratch

Rails is flexible enough to be able to respond to different formats, and is ready to do so out of the box. For the purposes of building applications in JavaScript and frameworks like React, though, we specifically need it to act as an API that responds with JSON.

## Using the `--api` Flag

To create an API-only Rails build from scratch, include the `--api` flag after the Rails application name upon creation:

```bash
rails new bird-watcher-api --api
```

By using the `--api` flag, Rails will remove a lot of default features and middleware, mostly related to the browser, since it won't be needed. Controllers will inherit from `ActionController::API` rather than `ActionController::Base` and generators will skip generating views.

One noticeable change—some browser errors will disappear. Normally, when a Rails server is running, it produces an error message in browser when something goes wrong while attempting to render. Since there is not way to render views in the API-only build, if the Rails API fails and we visit it in browser, it will just show a blank screen.

No changes are required when setting up resources for an API-only Rails build.

## From Beginning to End

After we create the API-only Rails build:

```bash
rails new bird-watcher-api --api
```

We navigate into the new Rails application. Rather than create _everything_ by hand, we can use a generator to help us out with our resources:

```bash
rails g resource bird name:string species:string
rails g resource location latitude:float longitude:float
rails g resource sighting bird:belongs_to location:belongs_to
```

This will create three migrations, three models, and three empty controllers. The three controller actions we want in the API will need to be added:

```ruby
def index
  sightings = Sighting.all
  render json: sightings, include: [:bird, :location]
end
```

Since the resource generator was used, it would be good to be diligent and clean up `config/routes.rb` once we've decided what endpoints the API should have.

## Dealing with CORS

While working on your own APIs, you'll typically want to have your Rails server running while also trying out various endpoints using `fetch()`. In order to do this, though, you will need to deal with [Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS), or CORS.

CORS is designed to prevent scripts like `fetch()` from one origin accessing a resource from a different origin unless that resource specifically states that it expects to share. So for instance, if you have run the command `rails server` with your server running at `http://localhost:3000`, the go to "www.google.com," open the console, and attempt to send a `fetch()` to your server, the browser considers these two different origins and will _refuse_ your request.

A solution is already provided though! By using the `--api` flag, the `Gemfile` was altered to include the [`rack-cors`](https://github.com/cyu/rack-cors) gem. This gem will be commented out initially:

```ruby
# Use Rack CORS for handling Cross-Origin Resource Sharing (CORS), making cross-origin AJAX possible
# gem 'rack-cors'
```

To get `rack-cors` working, uncomment the gem and run `bundle install`. Then, add the following to `config/application.rb`:

```ruby
class Application < Rails::Application
  config.middleware.insert_before 0, Rack::Cors do
    allow do
      origins '*'
      resource '*', headers: :any, methods: [:get, :post]
    end
  end
end
```

This shouldn't replace anything else inside `class Application < Rails::Application`, just be included in addition. This will allow you to test your APIs while developing them locally.

**WARNING:** Disabling CORS altogether in the long term can leave your server unsecure. Check out the documentation on [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) and [`rack-cors`](https://github.com/cyu/rack-cors) for additional information.

## Conclusion

With CORS enabled and your resources configured, you should be able to now run `rails server`, start up your API, and begin sending requests to it. You have all that you need to get you own API-only Rails builds into development. If you can think of something that can be turned into an API, you now have the power to spin one up in short order.

## Resources

* [Using Rails for API-only Applications (RailsGuides)](https://guides.rubyonrails.org/api\_app.html)
* [CORS (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
