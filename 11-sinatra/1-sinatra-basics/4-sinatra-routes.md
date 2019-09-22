# Lesson: Sinatra Routes

## Notes

- Every time a person clicks on a link, types in a URL, or submits a form, they are making HTTP requests to a specific URL on your application. Routes are the part of an application that connect HTTP requests to a specific method in your application code built to handle responding to such a request (that part of code is called a Controller Action).
- Users interact with our application by requesting specific URLs via HTTP. URLs are the interface to a web application.

### How Routes Work

- Routes match the web request sent by a client to some code in our application that tells the app what data and templates to send back to the client.
- Once the request has been matched to the route in the controller, called the controller action, then it executes the code inside of the controller action's block.

#### Breaking Down Route Definition

- Sinatra was built expressly for the purpose of creating web applications with Ruby.
