# Integrating Models for A Full MVC

## Notes

A full Model-View-Controller application in Sinatra uses input (usually from a form) to create an instance of a model, and then sends that instance back to a view to be displayed to the user.

### Creating A Model

- Instead of analyzing the data in our application controller, we create a new class inside of our `models` directory to do so.
- In general, our models are agnostic about the rest of our application. We could drop this class into a Command Line or Ruby on Rails app and it would function in the exact same way.

### Using A Model in the Controller

- In order to use the model we've created in our controller, we need to connect the two. To do this, we'll use the `require_relative` keyword to bring in the code from the model we've created. At the top of `app.rb`, add `require_relative "models/class_name.rb"`. This now gives us the ability to create new instances of our model class from within our controller.
