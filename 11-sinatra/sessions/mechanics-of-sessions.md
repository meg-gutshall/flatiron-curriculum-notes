# Lesson: Mechanics of Sessions

## Notes

### Setting Up A Session

- You can access the data stored in a session in the same way you would any hash in Ruby.
- In Sinatra, we enable sessions within the controller by adding two lines in the `configure` block.
  - **NOTE: NEVER set your `session_secret` by hand, and especially not to something so simple as `"secret"`! This example is ONLY for demonstration purposes!**
  - The `configure` block is part of built-in settings that control whether features are enabled or not.
- The first line of the configure block, `enable :sessions`, turns sessions on. The next line, `set :session_secret, "secret"`, is an encryption key that will be used to create a `session_id`. A `session_id` is a string of letters and numbers that is unique to a given user's session and is stored in the browser cookie. You can actually set your `session_secret` to anything you want.
  - `session_secret` is a pretty minimal security feature, but the basic idea is that setting you `:session_secret` to a word that other people don't know makes it harder for someone to create a fake `session_id` and hack into your site without signing up or signing in.

### Using Sessions

- In order to keep track of a current user throughout a session, we need to set up the `session` hash to store the `user_id` in the hash during a controller action.
- When we enable sessions in our app, every controller action has access to the `session` hash.

### Viewing Sessions

#### Viewing in Developer Tools

1. Open the Developer Tools and click on the `Application` tab.
2. On the left side of the tools, open up the `Cookies` dropdown, click the site you're logged into at the moment, and it will bring up all of the cookies loaded on the site.

#### Viewing in Chrome Settings

1. Select the hamburger icon in the top right corner and navigate to `Settings`.
2. Scroll all the way to the bottom of the page and click on the `Show advanced setting...` link.
3. Scroll down until you see `Privacy`, and then click the `Content settings...` button.
4. Finally, click the `All cookies and site data...` button. This will bring up a list of all of the sites that your browser has stored cookies from.

### Clearing Sessions

- There are several ways to clear a session cookie.
- The first is to simply log out of the site. That ends the current session, at which point all session cookies are automatically cleared.
- You can also clear cookies from the Developer Tools interface. Simply right-click on a session and select either `Delete` or `Clear All from "site name"`.
  - If you remove the session cookies and refresh the page, you'll notice that you've been logged out of the site.
- Chrome also come bundled with a special 'Incognito' mode that doesn't persist any cookies-session or otherwise-beyond the scope of a given browsing session. Because of this functionality, Incognito mode is often helpful while debugging session and cookie issues.

### Securing Your Session

- The most secure method of defining your `session_secret` is to use a secure number generator to generate a secret adn to share that secret, via environment variables in the shell, to Sinatra.

## Code Examples

### Session

```ruby
configure do
  enable :sessions
  set :session_secret, "secret"
end
```
