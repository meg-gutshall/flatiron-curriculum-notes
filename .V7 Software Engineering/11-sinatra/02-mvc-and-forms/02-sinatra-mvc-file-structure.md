# Lesson: Sinatra MVC File Structure

## Notes

### Keeping Code Organized

- Keeping our code organized is crucial when developing complex applications. This concept is called `separation of concerns` and `single responsibility`. Each file in our application will have a different responsibility and we'll keep these responsibilities split up into reasonable chunks.

#### `Gemfile`

- This holds a list of all gems needed to run the application. The bundler gem provides us access to a terminal command: `bundle install`. Bundler will look in the Gemfile and install any gems, as well as any dependencies for this application.
- This command will create a `Gemfile.lock` file, which is just a documentation of the specific gems version that should be installed.

#### `app` Directory

- This folder holds our MVC directories. We spend most of our time coding in this directory.

#### `models` Directory

- This directory holds the logic behind our application. Typically these files represent either a component of your application, such as a User, Post, or Comment, or a unit of work. Each file in models typically contains a different class.
- Models represent the data and object logic of our application.

#### `controllers` Directory

- The controllers are where the application configurations, routes, and controller actions are implemented.
- There is typically a class that represents an instance of your application when the server is up and running.
- Controllers represent the application logic-the interface and flow of our application.

#### `views` Directory

- This directory holds the code that will be displayed in the browser.
- In a Sinatra app, we use `.erb` files instead of `.html` files because `.erb` files allow us to include HTML tags and special erb tags which contain Ruby code.
- By convention, our file names should match up with the action that renders them.

#### `config` Directory

- This directory holds an `environment.rb` file, which we use to connect all our application files and gem to each other. This `environment.rb` file loads Bundler and thus all the gems in our Gemfile, as well as the `app` directory.

#### `public` Directory

- The `public` directory holds our front-end assets (CSS, HTML, JavaScript, images, etc.).

#### `spec` Directory

- The `spec` directory contains any tests for our applications. These tests set up any expectations for the rest of the project. These are often broken down into unit tests for models, controller tests for routes, and feature tests, which check the actual behavior for users.
