# Lesson: Passing Data Between Views and Controllers

## Notes

Passing data to views from your controller allows you to create dynamic pages that change depending on the input provided by the user.

### Manipulating Params in the Controller

- Params hashes can be used to access user input inside the controller, which will display in the console.
  - Example: For a form with `<input type="text" name="string">`, typing `params["string"]` inside of that path's `post` method in the controller will return the params hash `{"string"=>"#user input"}` in the console.
- This user input can be stored as a variable in the controller as well, allowing for manipulation.

### Using Instance Variables

- Instance variables allow us to bypass scope between the various methods in a class. Creating an instance variable in a controller method (route) lets the contents become "visible" to the `.erb` file to which it renders.
  - **Instance variables are only passed from the controller method where they are created to the view that is rendered, not between controller methods.**

### Rendering Using ERB Tags

- In order to show the content of a Ruby string in an `.erb` file, we need to use erb tags.
  - `<%= contents %>` will display the evaluated expression within the opening and closing tags.
  - `<% contents %>` will evaluate the contents of the expression, but will not display them.

### Iterating in ERB

- If the view is receiving an instance variable that is an array instead of a string, you must first iterate over the variable before displaying the string objects within that array.
