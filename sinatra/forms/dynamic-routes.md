# Lesson: Dynamic Routes

## Notes

Dynamic routing allows us to take input straight from the URL instead of through a form. In doing so, we can modify the content of a view at the moment the `get` request is received by the controller.

### URL Params

- A URI parameter is a variable whose values are set dynamically in a page's URL, and can be accessed by its corresponding controller action. It's a very similar concept to a dynamic URL.
- URL params help us get the text from the URL into the views. The data is passed from the URL to the controller action through an automatically generated hash called `params`.
  - The key of the hash is determined by the symbol in the URL, and the associated value will be the content in the URL provided by the user. Once inside the controller action, we can access the value from the params hash, just like we would any other hash.
- You can receive multiple pieces of data through a dynamic route by separating the content with a forward slash.
  - For example, `get '/addnumbers/:number1/:number2'` would give you a params hash with two key-value pairs (`number1` and `number2`).
  