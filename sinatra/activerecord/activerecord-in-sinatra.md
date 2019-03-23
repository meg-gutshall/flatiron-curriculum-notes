# Lesson: ActiveRecord in Sinatra

## Notes

- We can build Sinatra apps that allows a user to implement CRUD actions (Create, Read, Update, Delete) through the interface of the web.
- In this example, we'll use the class name `Model`.

### Connecting Controller Actions to Views for Implementing CRUD

#### Create

- The "create" part of CRUD is implemented in Sinatra by building a route, or controller action, to render a form for creating a new instance of your model.
  - The `get '/model/new'` route is created as a block in your controller. In this block, we can render an `.erb` file that contains our form. In this case, we'll call it `new.erb`.
  - The form sends a `POST` request to another controller action, `post '/models'`. It is here that you place the code that extracts the form data from the `params` and uses it to create a new instance of your model class, something along the lines of `Model.create(some_attribute: params[:some_attribute])`.

#### Read

- There are two ways in which we can read data. We may want to "read", or deliver to our user, all of the instances of a class or a specific instance of a class.
  - The `get '/models'` controller action handles requests for all instances of a class. It should load up all of those instances and set them equal to an instance variable: `@models = Model.all`. Then, it renders the `index.erb` view page.
  - The `index.erb` view page will use erb to render all of the instances stored in the `@models` instance variable.
  - The `get '/models/:id'` controller action handles requests for a given instance of your model. For example, if a user types in `www.yourwebsite.com/models/2`, this route will catch that request and get the `id` number, in this case `2`, from the `params`. It will then find the instance of the model with that id number and set it equal to an instance variable: `@model = Model.find(params[:id])`. Finally, it will render the `show.erb` view page.
  - The `show.erb` view page will use erb to render the `@model` object.

#### Update

- To implement the update action, we need a controller action that renders an update form, and we need a controller action to catch the post request sent by that form.
  - The `get 'models/:id/edit'` controller action will render the `edit.erb` view page.
  - The `edit.erb` view page will contain the form for editing a given instance of a model. This form will send a `PATCH` request to `patch '/models/:id'`.
  - The `patch '/models/:id'` controller action will find the instance of the model to update, using the `id` from `params`, and save that instance.
- We'll need to add the line `use Rack::MethodOverride` to the `config.ru` file to use the Sinatra Middleware that lets our app send `patch` requests. We also need to add the line `<input id="hidden" type="hidden" name="_method" value="patch">` to the form on our our `edit.erb` view page.
  - The `MethodOverride` middleware will intercept every request sent and received by our application. If it finds a request with `name="_method"`, it will set the request type based on what is set in the `value` attribute, which in the case is `patch`.

#### Delete

- The delete part of CRUD is a little tricky. It doesn't get its own view page, but instead is implemented via a "delete button" on the show page of a given instance. This "delete button", however, isn't really a button; it's a form. The form should send a `DELETE` request to `delete '/models/:id/delete'` and should only contain a "submit" button with a value of "delete". That way, it will appear as only a button to the user.
- The hidden input field is important to note here. This is how you can submit `PATCH` and `DELETE` requests via Sinatra. The form tag `method` attribute will be set to `post`, but the hidden input field sets it to `DELETE`.

## Code Examples

### Delete Button

```html
<form method="post" action="/models/<%= @model.id %>/delete">
  <input id="hidden" type="hidden" name="_method" value="DELETE">
  <input type="submit" value="DELETE">
</form>
```