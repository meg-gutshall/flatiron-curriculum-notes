# Lesson: Intro to Capybara Tests

## Notes

### The MVC Framework

- There are three basic levels of testing that correspond to teh different levels of our application stack in Model-View-Controller architecture: Integration Tests, Controller Tests, and Unit Tests.
  - **Database:** Databases persist or save data from our application.
  - **Models:** Models provide an object-oriented abstraction or metaphor for the data in our application. Our models do the job of acting with the database for us by requesting certain data and using that data to create a new instance of our class. We can then interact with that data by using the methods and properties of the instance of that class.
  - **Controllers:** Controllers provide the main interface and application logic. In large-scale MVC applications, controllers are represented by classes, but really a lot of `bin` file could be considered controllers.
  - **Views:** Views present information to the user. Any code that is responsible for presenting data or output to the user could be considered a View. In web applications, Views are generally represented by ERB templates that generate HTML.
  - **User/Browser:** The top of our application pyramid is the user. Whether describing the people using our application, the interface they use such as a Command Line, Voice, or HTML, or the program they use to even access our application, our application is responsible for delivering the user an experience on some sort of pre-existing platform.

### The Three Levels of Testing

Each MVC layer is associated with a type of test: Models to Unit; Controllers to Controller; Views to Integration. Testing at one layer also runs implicit tests through the other layers.

#### Unit Tests

Unit tests test the models in our application and how they interact with our database.

#### Controller Tests

Controller tests test that the code responsible for delivering the appropriate data to a user is working properly. In a web app, a controller test is responsible for making sure that an HTTP request returns the expected HTTP response. Controller tests should test not HTML or forms, but rather that the controller is behaving as expected.

#### Integration Tests

Integration tests are the highest-level test, and they are closest to describing how the user will actually interact with our application. Commonly referred to as 'End-to-End' tests, integration tests should flex your entire application stack adn rarely isolate components or behaviors. They are perfect for spec-ing high-level user interactions with HTML and forms.

### Integration Testing with Capybara

- Capybara is a library of code that we can include in our application via the Capybara gem. The Capybara library allows us to write code that simulates how are user interacts with our app. We can write such code in our integration tests and thus test the functionality of our application.

### Testing Our Application

#### Capybara `visit`

The `visit` method navigates the test's browser to a specific URL. It is equivalent to a user typing a URL into their browser's location bar. The argument it accepts is a string for the URL you want to test. Since we want to test our `'/'` root URL, we say `visit '/'`, and Capybara will load that page within our test.

#### Capybara `page`

The `page` method in Capybara exposes the "session" or "browser" that is conceptually (and literally) being used during the test. The `page` method gives you a `Capybara::Session` object that represents the browser page the user would actually be looking at if they navigated to `'/'` (or whichever route was last passed to `visit`). As such, `page` responds with a lot of methods that represent actions a user could take on a page, such as `click_link`, `fill_in`, and `body`. The `page.body` method will dump out all fo the HTML in the current page as a string.