# Lesson: Sinatra Basics

## Notes

- Web applications tend to require a certain degree of complexity. To handle this, Sinatra is more commonly used through the Modular Sinatra Pattern.
- The first new convention this pattern introduces is a `config.ru` file whose purpose is to detail the Rack environment requirements of the application and start the application.
  - In the first line we load the Sinatra library.
  - The second line requires our application file, defined in `app.rb`.
  - The last line uses `run` to start the application represented by the Ruby class defined in `app.rb`.
- `config.ru` requires a valid Sinatra Controller to `run`. A Sinatra Controller is simply a Ruby class that inherits from `Sinatra::Base`. This inheritance transforms into a web application by giving it a Rack-compatible interface behind the scenes via the Sinatra framework.
- The final step in creating a controller is mounting it in `config.ru`. Mounting a controller means telling Rack that part of your web application is defined within the following class. We do this in `config.ru` by using `run Application` where `run` is the mounting method and `Application` is the controller class that inherits from `Sinatra::Base` and is defined in a previously required file.
