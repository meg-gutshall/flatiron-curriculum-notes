# Lesson: Intro to REST

## Notes

### What Is REST?

- Roy Thomas Fielding invented REST for his PhD dissertation in 2000 as a standard way for web apps to structure their URLs.
  - REST is an architectural design pattern, not a framework or code in itself.
- **REST** stands for **RE**presentational **S**tate **T**ransfer.

### Example REST Workflow

For a real-world case study, let us pretend you have a newsletter application. The following is a high-level view of how REST works in your app:

1. You fill out the form on the 'New Newsletter' page and click submit.
2. Data concerning you, your newsletter content, and any additional information such as media items is sent to the application server.
3. The server interprets the information, recognizes that the request is for a new newsletter, generates the new record in the database, and performs myriad background tasks (updating the newsletter counter, possibly sending notification emails, etc.).
4. Next, the server sends a response back to the client. The does not necessarily mean that the newsletter was posted. The response could be that there was an error posting or something like that. However, in this case we will say that the newsletter post went through properly, so the server sends a success message and tells the browser which page to go to and render.
5. Lastly, the browser receives the server information and gives the user feedback. In the case, it shows the user a message saying that their newsletter was successfully posted.

### RESTful Conventions in Rails

- Rails has RESTful principles built into its core, so whether you are utilizing the built-in view rendering system or using the application purely as an API, you will have the tools necessary to follow standardized routing procedures.
- For our newsletter example, we would need the system to have four key actions—Create, Read, Update, and Destroy—commonly known as 'CRUD' actions. In addition to CRUD actions, we will also need an `index` page that lists out all of our newsletters as our fifth route. Our users will need a visual interface for creating and updating records (forms), so that adds two more for a total of seven different routes.
  - The `GET` routes are all routes that usually render some `erb` content to a web browser. These are the routes that our users will work with everyday.
  - The `POST` and `PUT` are the URL in the form `action`, and the `DELETE` is a new type of HTTP verb.
- Rails maps these specific HTTP verbs and paths to specific methods or "actions" as they are called in Rails.
- In analyzing the diagram below, you can see the flow of data as follows:
  - The HTTP request contains an HTTP verb and hits a specific URL path.
  - The router in the application processes the request and 'routes' the request data to the proper controller action.
  - The controller action either performs a task, such as creating, updating, or deleting a record in the database, or it runs a database query and renders a view to the client.

![RESTful routing diagram](https://github.com/meg-gutshall/flatiron-curriculum-notes/blob/master/public/images/rails/rails_routes.png)

### Definition of HTTP Verbs

- `GET`: The `GET` method retrieves whatever information is identified by the Request URI.
- `POST`: The `POST` method is used to send data enclosed in the request to the server. The server is expected to use this data to create some new resource.
- `PATCH`/`PUT`: The `PATCH`/`PUT` methods both represent the HTTP verbs that are used to update existing resources.
- `DELETE`: The `DELETE` method requests that the server delete the resource identified by the Request URI.

### Resources

[Rails Routing from the Outside In](https://guides.rubyonrails.org/routing.html)