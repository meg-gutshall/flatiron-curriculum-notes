# Lesson: Inspecting the Web with Rack

## Notes

- Rack is a Ruby gem that helps us to create a web server and it is what Rails is built on top of.

### Setting Up Rack

- To work with Rack, we need to create a new class that responds to a single method: `#call`. All this method needs to do is return a response which consists of the status code, any headers, and the body. This can all be done using the `Rack::Response` object.
  - This is run whenever a request is received.
- We have one more step. We actually have to set up an HTTP web server that will receive the HTTP request, send it through the `#call` method, and then serve the response to the browser. We do this using a `config.ru` file and the `rackup` command.
  - To execute this code, we then run `rackup config.ru`.
- It should return some lines of code, part of which will say something like `port=9292`. If you open your browser and go to `http://localhost:9292/` you should see `Hello World!`.
  - `localhost` is the server name of your own computer.
- To exit the running web server and get back to your terminal, press CTRL-C. **You will have to do this every time you change your code.**

## Code Examples

### Rack's `#call` Method

```ruby
class Application
  
  def call(env)
    resp = Rack::Response.new
    resp.write "Hello World!"
    resp.finish
  end
  
end
```

### `config.ru`

```ruby
#config.ru

require_relative "./application.rb"

run Application.new
```
