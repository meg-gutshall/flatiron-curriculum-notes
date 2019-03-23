# Lesson: HTML Forms and Params

## Notes

- In order to connect a form to our application, we need to give it explicit directions on where and how to send the data from the user.
  - Both of these pieces of data are attributes that we give our `<form>` tag.
    - The `method` attribute tells the form what kind of request should be fired to the server when the submit button is clicked. In general, forms use POST request, because it is 'posting' data to the server.
    - The `action` attribute tells the form what specific route the post request should be sent to.
- Each form field `<input>` also must define a `name` attribute. The `name` attribute of an `<input>` defines how our application will identify each `<input>` data.

### Post Routes and Params

- Every form also needs a corresponding route in the controller file (`app.rb`). Instead of a `get` route, we'll set up a post route.
  - Notice that both of the attributes from the form are covered in this route: The `method post` and the `action /food`. It's almost like a game of catch - the form is throwing the data to the server, which catcher it by having the same receiving address (`/food`) and way of receiving the data (`post`).
- All user submitted data will appear in a `params` hash accessible throughout our Sinatra controllers. The `name` attribute of an `<input>` corresponds to a key in the `params` hash for that data.