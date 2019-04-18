# Lesson: Rails Static Request

## Routing

- Routes tells your application which views to render to users.
- The differences between a static and a dynamic route:
  - A **static route** will render a view that does not change. Typically, you will not send parameters to it.
  - A **dynamic route** is a page that accepts parameters and renders different content based on those parameters.

## Implementing A Static Route

To draw a route, we need to open the `config/routes.rb` file and add the route inside of the `draw` block:

```ruby
get 'about', to: 'static#about'
```

- Let's look at the components that make up this route code:
  - The HTTP verb: In this case we're using the `get` HTTP verb.
  - The path: `'about'` represents the path in the URL bar that the route will be mapped to.
  - The controller action: `'static#about'` tells the Rails routing system that this route should be passed through the `static` controller's `about` action. If the term `action` sounds foreign, actions are just Ruby speak for a method in a controller. So in the `StaticController`, there will be a method called `about` that gets called when a user goes to `/about`.
- We must refresh the server to reflect any changes we make to this file.

We must also add a new controller for our static pages (`app/controllers/static_controller.rb`) that inherits from `ApplicationController` along with the `about` action

```ruby
class StaticController < ApplicationController
  def about
  end
end
```

- The standard naming convention for controllers is the name of the controller followed by the word `Controller`.
- Rails gives us two options for how views are mapped between the controller and view files. It's important to understand the difference between explicit and implicit rendering for the views:
  - **Explicit rendering**: Rails lets you dictate which view file you want to have the controller action mapped to.
  - **Implicit rendering**: Rails follows a standard convention that automatically looks for the view file with the same name as the controller action.

### Explicit Rendering

```ruby
def about
  render "some_page"
end
```