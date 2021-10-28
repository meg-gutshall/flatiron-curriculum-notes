---
description: 'Version 8: Module 14: Section 6: Code-along'
---

# Rendering Different Content Types Using Rails

## Overriding the Default Rails View

Rails doesn't restrict us to displaying ERB. We can indicate which type of content we want to render.

### Render Plain Text from a Controller

To render plain text from a Rails controller, you specify `plain:`, followed by the text you want to display:

```ruby
class BirdsController < ApplicationController
  def index
    @birds = Bird.all
    render plain: "Hello #{@birds[3].name}"
  end
end
```

In the browser, this displays as:

```
Hello Mourning Dove
```

This isn't very fancy, but _**this is actually enough for us to start using our JavaScript skills and access with a `fetch()` request**_.

### Render JSON from a Controller

To render JSON from a Rails controller, you specify `json:` followed by data that can be converted to valid JSON:

```ruby
class BirdsController < ApplicationController
  def index
    @birds = Bird.all
    render json: 'Remember that JSON is just object notation converted to string data, so strings also work here'
  end
end
```

We can pass strings as we see above as well as hashes, arrays, and other data types:

```ruby
class BirdsController < ApplicationController
  def index
    @birds = Bird.all
    render json: { message: 'Hashes of data will get converted to JSON' }
  end
end
```

```ruby
class BirdsController < ApplicationController
  def index
    @birds = Bird.all
    render json: ['As', 'well', 'as', 'arrays']
  end
end
```

In our bird watching case, we actually already have a collection of data, `@birds`, so we can write:

```ruby
class BirdsController < ApplicationController
  def index
    @birds = Bird.all
    render json: @birds
  end
end
```

You may often see more detailed nesting in the `render json:` statement:

```ruby
class BirdsController < ApplicationController
  def index
    @birds = Bird.all
    render json: { birds: @birds, messages: ['Hello Birds', 'Goodbye Birds'] }
  end
end
```

Notice that the above would alter the structure of the data being rendered. Rather than an array of four birds, an object with two keys (each pointing to an array) would be rendered instead.

With the intent of constructing an API, we always want to be thinking about data. The purpose of an API is to be an accessible _interface_, in our case, to a JavaScript frontend, so we want to always be thoughtful in how we structure data and how that data will be utilized.

Well structured API data can make frontend code simpler. Poorly structured API data can lead to complicated nests of JavaScript enumerables.

## Where Is Our Data Being Converted to JSON?

When we include an array or hash after `render json:`, it turns out that Rails is actually being accommodating to us and implicitly handling the work of converting that array or hash to JSON.

We can choose to explicitly convert our array or hash, without any problem by adding `to_json` to the end:

```ruby
class BirdsController < ApplicationController
  def index
    @birds = Bird.all
    render json: { birds: @birds, messages: ['Hello Birds', 'Goodbye Birds'] }.to_json
  end
end
```

This will produce the same result as it did before. The `to_json` method is made available to both [arrays](https://apidock.com/rails/Array/to\_json) and [hashes](https://apidock.com/rails/Hash/to\_json) in Rails, but is not natively available to them in Ruby. It does exactly what it says—it takes whatever array or hash it is called on and converts it to JSON.

Rails favors convention as well as a clean and clutter-free controller, so it has some built-in "magic" to handle things like this and keep us from having to write `to_json` on the same line as `render json:` in every action we write.

## Say Goodbye to Instance Variables

So far in controller actions, we've typically seen instance variables being used. However, we really only needed instance variables when we were rendering to ERB. Now that we a directly rendering to JSON in the same action, we no longer need to deal with instance variables and can instead just use a local variable:

```ruby
class BirdsController < ApplicationController
  def index
    birds = Bird.all
    render json: birds
  end
end
```

## Conclusion

Let's take a step back and consider what all this means because this is actually huge! Now that you know that Rails can render JSON, you have the ability to create entirely independent JavaScript frontends that can communicate with Rails backends!
