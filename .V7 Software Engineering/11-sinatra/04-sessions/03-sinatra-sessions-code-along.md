# Lesson: Sinatra Sessions Code Along

## Notes

### Sessions and Data Persistance

- The Hyper-Text Transfer Protocol (HTTP) is, by definition, a stateless protocol.
  - For example, the client may log in to a web app by filling out a form with username and password fields. The input login information is sent to the web app via an HTTP POST request and then compared with data from the web app's database to find a match (aka. an existing user). After the login process is complete, when the client navigates to another page, the web app doesn't know who the client is. That is what it means to be "stateless". Each web request sent, from the point of view of the application receiving that request, is totally independent.
- Sessions are hashes that live in your application in the server. The session hash can be accessed in any controller file of your application. Whatever data is stored in the session hash can thus be accessed, added to, changed, or deleted in any controller file or route at any time and that change persists for the duration of the session (the period of time in which the client is interacting with your web application).
  - The act of "logging in" is simply the act of having the client's user id stored inside the session hash and "logging out" is removing it from the session hash.
- The session hash is most commonly used to store info like a user's id, which the web application will use to know who is the "current user" and show that user the appropriate information—but we can put anything we want inside a session hash.
