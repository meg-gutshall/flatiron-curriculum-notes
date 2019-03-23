# Lesson: User Authentication in Sinatra

## Notes

### User Authorization: Using Sessions

#### Logging In

- The action of logging in is the simple action of storing a user's ID in the `session` hash. Here's a basic user login flow:
  - User visits the login page and fills out a form with their email and password. They hit 'submit' to `POST` that data to a controller route.
  - The controller route accesses the user's email and password from the `params` hash. That info is used to find the appropriate user from the database with a line such as `User.find_by(email: params[:email], password: params[:password])`. **Then. that user's ID is stored as the value of `session[:id]`.**
  - As a result, we can introspect on the `session` hash in any other controller route and grab the current user by matching up a user IF with the value in `session[:id]`. That mean that, for the duration of the session, the app will know who the current user is on every page.

**A Note on Password Encryption**
For the time being, we'll simply store a user's password in the database in its raw form. However, that is not safe! In an upcoming lesson, we'll learn about password encryption: the act of scrambling a user's password into a super-secret code and storing a de-crypter that will be able to match up a plaintext password entered by a user with the encrypted version stored in a database.

#### Logging Out

- Conceptually, logging out means terminating the session, or the period of interaction between a given user and our app. The action of 'logging out' is really just the action of clearing all of the data, including the user's ID, from the `session` hash. We can do this by using the Ruby method for emptying a hash: `#clear`.

#### User Registration

- Before a user can sign in, they need to sign up. To sign up, a new user must submit their information (for example: name, email, and password) via a form. When that form gets submitted, a `POST` request is sent to a route defined in the controller. That route will have code that does the following:
  - Gets the new user's name, email, and password from the `params` hash.
  - Uses that info to create and save a new instance of `User`.
    - For example: `User.create(name: params[:name], email: params[:email], password: params[:password])`
  - Signs the user in once they have completed the sign-up process. In the same controller route in which we create a new user, we set the `session[:id]` equal to the new user's ID, effectively logging them in.
  - Finally, we redirect the user somewhere else, such as their personal homepage.

### Project Structure

#### The `app` Folder

- The `app` folder contains the models, views, and controllers that make up the core of our Sinatra application. Get used to this setup as it's conventional to group these files under an `app` folder.

##### Application Controller

- The `get '/registrations/signup'` route has one responsibility: render the signup form view. This view can be found in `app/views/registrations/signup.erb`. Notice we have separate view sub-folders to correspond to the different controller action groups.
- The `post /registrations` route is responsible for handling the `POST` request that is sent when a user hits 'submit' on the signup form. It will contain code that gets the new user's info from the `params` hash, creates a new user, signs them in, and then redirects them somewhere else.
- The `get '/sessions/login'` route is responsible for rendering the login form.
- The `post '/sessions'` route is responsible for receiving the `POST` request that gets sent when a user hits 'submit' on the login form. This route contains code that grabs the user's info from the `params` hash, looks to match that info against the existing entries in the user database, and, if a matching entry is found, signs the user in.
- The `get '/sessions/logout'` route is responsible for logging the user out by clearing the `session` hash.
- The `get '/users/home'` route is responsible for rendering the user's homepage view.

##### The `models` Folder

- The `models` folder contains a file for every model the app contains.
  - In our case, it contains one file because we only have one model in this app: `User`.

##### The `views` Folder

- The `views` folder has a few sub-folder to correspond with the different controller action groups. Since we have different controllers responsible for different functions/features, we want our `views` folder structure to match up.
  - The `views/registrations` sub-directory contains one file, the template for the new user signup form. That template will be rendered by the `get '/registrations/signup'` route in our controller. This form will `POST` to the `post '/registrations'` route in our controller.
  - The `views/sessions` sub-directory contains one file, the template for the login form. This template is rendered by the `get '/sessions/login'` route in the controller. The form on the page send a `POST` request that is handled by the `post '/sessions'` route in the controller.
  - The `views/users` sub-directory contains one file, the template for the user's homepage. This page is rendered by the `get '/users/home'` route in the controller.
  - We also have a `home.erb` file in the top level of the `views` directory. This is the page rendered by the root route, `get '/'`.
- The only variables that a view can access are instance variables set in the controller route that renders that particular view page.
  - After setting the `session[:id]` equal to the new user's ID, effectively logging in the new user, insert `@user = User.find(session[:id])` in your controller action block to give the corresponding view page access to the current user's information.