# Lesson: OmniAuth

## Overview

The downside of passwords:

- Users have to remember them or use a password manager
- A percentage of users will just leave a never come back the moment they're asked to create an account
- Developers have to securely store all passwords on a server
  - Rails secures your passwords when they are stored in your database, but it does not secure your servers, which see the password in plain text.
- Developers have to handle passwords changes, email verification, and password recovery

Using a third-party account to allow users to login takes these issues off of the developers shoulders and utilizes highly secure systems that are already in place.

## OmniAuth

[OmniAuth](https://github.com/intridea/omniauth) is a gem for Rails that lets you use multiple authentication providers alongside the more traditional username/password setup. 'Provider' is the most common term for an authentication partner, but within the OmniAuth universe we refer to providers (i.e. using a Facebook account to log in) as _strategies_. The OmniAuth wiki keeps an [up-to-date list of strategies](https://github.com/omniauth/omniauth/wiki/List-of-Strategies), both official (provided directly by the service, such as GitHub, Heroku, and SoundCloud) and unofficial (maintained by an unaffiliated developer, such as Facebook, Google, and Twitter).

Here's how OmniAuth works from the user's standpoint:

1. User tries to access a page on `yoursite.com` that requires them to be logged in. They are redirected to the login screen.
2. The login screen offers the options of creating an account or logging in with Google or Twitter.
3. The user clicks `Log in with Google`. This momentarily sends the user to `yoursite.com/auth/google`, which quickly redirects to the Google sign-in page.
4. If the user is not already signed in the Google, they sign in normally. More likely they are already signed in, so Google simply asks if it's okay to let `yoursite.com` access the user's information. The user agrees.
5. They are (hopefully quickly) redirected back to `yoursite.com/auth/google/callback` and, from there, to the page they initially tried to access.

## OmniAuth with Facebook

The OmniAuth gem allows us to use the OAuth protocol with a number of different providers. All we need to do is add the OmniAuth gem _and_ the provider-specific OmniAuth gem (i.e. `omniauth-google`) to our Gemfile. In some cases, adding only the provider-specific gem will suffice because it will install the OmniAuth gem as a dependency, but it's safer to add both—the shortcut is far from universal.

In this case, let's add `omniauth` and `omniauth-facebook` to the Gemfile and then run a `bundle install` command. If we were so inclined, we could add additional OmniAuth gems to our heart's content, offering login via multiple providers in our app.

Next, we'll need to tell OmniAuth about our app's OAuth credentials. Create a file named `config/initializers/omniauth.rb` that looks like this:

```ruby
# config/initializers/omniauth.rb

Rails.application.config.middleware.use OmniAuth::Builder do
  provider :facebook, ENV['FACEBOOK_KEY'], ENV['FACEBOOK_SECRET']
end
```

In this code, we're telling our Rails app to use a piece of middleware created by OmniAuth for the Facebook authentication strategy.

### `ENV`

The `ENV` constant refers to a global hash for your entire computer environment. You can store any key-value pairs in this has, so it's a very useful place to keep credentials that we don't want to be managed by Git or displayed on GitHub (especially if your GitHub repo is public). The most common error students run into is that when `ENV['PROVIDER_KEY']` is evaluated in the OmniAuth initializer, it returns `nil`. Later attempts to authenticate with the provider will cause some kind of `4xx` error because the provider doesn't recognize the app's credentials.

As you can gather from the initializer code, we're going to need two pieces of information from Facebook in order to get authentication working: the application key and secret that will identify our app to Facebook.

Log in to the [Facebook developer site](https://developers.facebook.com/). In the `My Apps` dropdown menu at the top-right of the page, select `Add a New App`, and a modal should appear. Fill out the requested information and click `Create App ID`. You should now be on the `Product Setup` page. Click `Get Started` next to `Facebook Login`. Choose the `Web` option, and enter `https://localhost:3000/` when it prompts you for your `Site URL`. Click `Save`, and then click on `Settings` under the `Facebook Login` heading in the sidebar. In the `Valid OAuth redirect URIs` field, enter `https://localhost:3000/auth/facebook/callback`, which is the default callback endpoint for the `omniauth-facebook` strategy. Click `Save Changes`, and then click on `Dashboard` in the sidebar. Keep the page handy because we'll need those `App ID` and `App Secret` values in a minute.

### `dotenv-rails`

Instead of setting environment variables directly in our local `ENV` hash, we're going to let an awesome gem handle the hard work for us. `dotenv-rails` is one of the best ways to ensure that environment variables are correctly loaded into the `ENV` hash in a secure manner. Using it requires four steps:

1. Add `dotenv-rails` to your Gemfile and `bundle install`.
2. Create a file named `.env` at the root of your application.
3. Add your Facebook app credentials to the newly created `.env` file.
4. Add `.env` to your `.gitignore` file to ensure that you don't accidentally commit your precious credentials.

For step three, take the `App ID` and `App Secret` values from the Facebook app dashboard and paste them in the `.env` file as follows:

```env
FACEBOOK_KEY=247632982388118
FACEBOOK_SECRET=01ab234567890c123d456ef78babc901
```

### Routing OAuth Flow in Your Application

We now need to create a link that will initiate the Facebook OAuth process. The standard OmniAuth path is `/auth/:provider` so in this case, we'll need a link to `/auth/facebook`. Let's add one the `app/views/welcome/home.html.erb`:

```erb
<!-- app/views/welcome/home.html.erb -->

<%= link_to('Log in with Facebook!', '/auth/facebook') %>
```

Next, we're going to need a `User` model and a `SessionsController` to track users who log in via Facebook. The `User` model should have four attributes, all strings: `name`, `email`, `image`, and `uid` (the user's ID on Facebook).

To handle user sessions, we need to create a single route, `sessions#create`, which is where Facebook will redirect users in the callback phase of the login process. Add the following to `config/routes.rb`:

```ruby
# config/routes.rb

get '/auth/facebook/callback', to: 'sessions#create'
```

Our `SessionsController` will be pretty simplistic with a lone action and a helper method to DRY up our code a bit.

```ruby
# app/controllers/sessions_controller.rb

class SessionsController < ApplicationController
  def create
    @user = User.find_or_create_by(uid: auth['uid']) do |u|
      u.name = auth['info']['name']
      u.email = auth['info']['email']
      u.image = auth['info']['image']
    end
    session[:user_id] = @user.id
    render 'welcome/home'
  end

  private
    def auth
      request.env['omniauth.auth']
    end
end
```

And finally, since we're re-rendering the `welcome#home` view upon logging in via Facebook, let's add a control flow to display user data if the user is logged in and the login link otherwise.

```erb
<!-- app/views/welcome/home.html.erb -->

<% if session[:user_id] %>
  <h1><%= @user.name %></h1>
  <h2>Email: <%= @user.email %></h2>
  <h2>Facebook UID: <%= @user.uid %></h2>
  <img src="<%= @user.image %>">
<% else %>
  <%= link_to('Log in with Facebook!', '/auth/facebook') %>
<% end %>
```

### Facebook Login in Action

Upon clicking the link, your browser sends a `GET` request to the `/auth/facebook` route, which OmniAuth intercepts and redirects to a Facebook login screen with a ridiculously long URI. The URI has a ton of [encoded parameters](https://ascii.cl/url-encoding.htm), but we can parse through them to get an idea of what's actually being communicated.

Right away we see our Facebook application key, `api_key=247632982388118`, and the Facebook API endpoint that the login flow will send us to next: `next=https://www.facebook.com/v2.9/dialog/oauth`. At that point, there a divergent paths:

- `redirect_uri=https://localhost:3000/auth/facebook/callback`—If login succeeds, we'll be redirected to our server's OmniAuth callback route.
- `scope=email`—This tells Facebook that we want to receive the user's registered email address in the login response. We didn't have the configure anything (`scope=email` is the default), but if you want to request other specific pieces of user data, check out the [omniauth-facebook documentation](https://github.com/mkdynamic/omniauth-facebook#configuring).
- `client_id=247632982388118`—There's our application key again, this time provided to the success callback.
- `cancel_url=https://localhost:3000/auth/facebook/callback`—If login fails, we'll also be redirected to our server's OmniAuth callback route. However, this time there are some nested encoded parameters that provide information about the failure:
  - `error=access_denied`
  - `error_code=200`
  - `error_description=Permissions error`
  - `error_reason=user_denied`

### Inspecting the Returned Authentication Data

If you want to inspect the exact information that Facebook returns to our application about a logged-in user, throw a `binding.pry` in the `SessionsController#create` method and call `auth` inside the Pry session. When you make a server-side API call, Facebook will provide an access token that's good for about two months, so you don't have to bug your users very often. That's good!

## Resources

[Managing Environment Variables](https://launchschool.com/blog/managing-environment-configuration-variables-in-rails)
