# Lesson: The HTTP Request

## Notes

- An HTTP request that our browser sends to the server contains two main sections of information: headers and the resource, or path requested.

### The Path

- The path that is requested is the source that the client wants. Since your server can contain a lot of functionality, the path signifies which specific part of your server it wants.
- The path lives in the HTTP request, and to get to it we have to inspect the `env` part of our `#call` function. In the `env` variable is all of the information contained in the request. Thankfully, Rack has a great way of parsing all this information for us called `Rack::Request`
  - Built into the `Rack::Request` instance is the `#path` method, which will return the path that was requested.
- Can display different content based on path

### User Input Via the Path

- What happens when a user wants to execute a search? If we go to GitHub and type in "apples" in the search query, we get a URL that looks like this: `https://github.com/search?q=apples`.
  - The section after the `?` is called the `GET` parameters and they come in key/value pairs. The matching Ruby data structure that is also a key.value store would be a `Hash`. Rack provides the mechanism to parse the `GET` params and return them to us in a standard `Hash`.

## Code Examples

### `Rack::Request`

```ruby
class Application
  
  def call(env)
    resp = Rack::Response.new
    req = Rack::Request.new(env)
    resp.finish
  end
  
end
```

### The `#path` Method

```ruby
class Application
  
  def call(env)
    resp = Rack::Response.new
    req = Rack::Request.new(env)

    if req.path.match(/eagles/)
      resp.write "Fly, Eagles fly!"
    elsif req.path.match(/phillies/)
      resp.write "Go Phils!"
    elsif req.path.match(/flyers/)
      resp.write "Gritty rules!"
    elsif req.path.match(/sixers/)
      resp.write "Trust the process."
    else
      resp.write "Path not found"
    end

    resp.finish
  end
  
end
```
