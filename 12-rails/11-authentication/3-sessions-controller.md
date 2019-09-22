# Lesson: Sessions Controller

## How Login Works on the Web

Nearly every website in the world uses what we'll call the "wristband" pattern. A lot of nightclubs use this pattern as well:

You arrive at the club. The bouncer checks your ID. They put a wristband on your wrist (or stamp your hand). They let you into the club. If you leave and come back, the bouncer doesn't look at your ID, they just look for your wristband. If you buy a drink, the bartender doesn't need to see your ID, since your wristband proves you're old enough to buy alcohol.

You arrive at gmail.com. You submit your username and password. Google's servers check to see if your credentials are correct. If they are, Google's servers issue a cookie to your browser. If you visit another page on gmail, or anywhere on google.com for that matter, your browser will show the cookie to the server. The server verifies this cookie, and let you load your inbox.

## How This Looks in Rails

Let's look at what the simplest possible login system might look like in Rails.

The flow will look like this:

- The user navigates to `/login`, using the `GET` method.
- The user enters their username. There is no password.
- The user submits the login form to `/login` via the `POST` method.
- In the `create` action of the `SessionsController`, we set a cookie on the user's browser by writing their username into the session hash.
- Thereafter, the user is logged in. `session[:username]` will hold their username.

Let's write a `SessionsController` to handle these routes. This controller has two actions, `new` and `create`, which we'll map in `routes.rb` to `GET` and `POST` on `/login`.

Typically, your `create` method would look up a user in the database, verify their login credentials, and then store the authenticated user's id in the session. We're not going to do any of that right now. Our `SessionsController` is just going to trust that you are who you say you are.

```ruby
# app/controllers/sessions_controller.rb

class SessionsController < ApplicationController
  def new
  end

  def create
    session[:username] = params[:username]
    redirect_to '/'
  end
def
```

There's no way for the server to log you out right now. To log yourself out, you'll have to delete the cookie from your browser.

We'll make a very small login form for `new.html.erb`:

```html
<!-- app/views/sessions/new.html.erb -->

<form method='post'>
  <input name='username'>
  <input type='submit' value='login'>
</form>
```

Ordinarily, we would use `form_for @user`, but in this example, we don't have a user model at all! When the user submits the form, they'll be logged in.

## Logging Out

The log out flow is even simpler. We add a `SessionsController#destroy` method, which will clear the username out of the session.

```ruby
# app/controllers/sessions_controller.rb

class SessionsController < ApplicationController
  def destroy
    session.delete :username
  end
def
```

The most common way to route this action is to `post '/logout'`. This means that our logout link will actually be a submit button that we style to look like a link.

It's tempting, but don't attach this to a `GET` route. HTTP specifies that `GET` routes don't change anything—logging out is definitely changing something. You don't actually want someone to be able to put a link to `https://www.yoursite.com/logout` in an email or message board post. It's not a security flaw, but it's pretty annoying to be logged out because of mailing list hijinks.

### Resources

- [Rails Tutorial Chapter 8 — Log in, log out](https://www.railstutorial.org/book/basic_login)
