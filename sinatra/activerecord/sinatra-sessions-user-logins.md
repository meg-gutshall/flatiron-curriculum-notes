# Lesson: Sinatra Sessions - User Logins

## Notes

### Helper Methods

- MVC architecture relies heavily on the principle of separation of concerns. We make sure that we have a different model for every class we build, that we only have one `.erb` file per view, etc.
- This even extends to the purposes each of these files has.
  - A model handles our Ruby logic, our controllers handle the HTTP requests and connect to our models, and our views either take in or display data to our users.
- This means that we want to minimize the amount of logic our views contain.
  - Our views should never directly pull from the database. All of that should be taken care of in the controller actions, and the data should be passed to the view via a specific controller action.
- In the `app/helpers` directory, we're going to define a separate class specifically designed to control logic in our views through the use of helper methods. This `Helpers` class will have two class methods: `current_user` and `is_logged_in?`.
  - These two methods will only ever be called in views in order to add another layer of protection so that only the current user, when they are logged in, can see their bank account balance.
- It's important to note that helper methods can be used for a lot more than just tracking whether a user is logged in and who the current user is. Helpers are methods that make it clearner to add logic to our views.