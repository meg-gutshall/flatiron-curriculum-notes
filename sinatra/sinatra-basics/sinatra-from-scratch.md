# Lesson: Sinatra from Scratch

## Notes

- The first thing you need to do in any Sinatra app is run `bundle install`, which will lock in the current versions of the gems for your applications so if any updates happen, your app won't break. It keeps the version locked in a file called `Gemfile.lock` that is created for you.
- The `app.rb` file is our application controller, which handles all incoming requests to our app, and sends back the appropriate responses to the client.
  - The first line of `app.rb` requires the Sinatra gem.
  - the next line defines the class and inherits from `Sinatra::Base` so it will have all of the functionality of the Sinatra class (i.e. `App < Sinatra::Base`).
  - Inside our class we have a Sinatra method define our controller action.
- Sinatra relies on Rack for its middleware, the software that bridges the connection between our Ruby application and the database. Therefore, to check if our app is working in the browser, we type `rackup app.rb` into the terminal and visit `localhost:9292` to see if it displays the content called for in our controller.