# Lesson: Sessions and Cookies

## Notes

- HTTP is a stateless protocol, treating each request as an independent transaction that is unable to use information from any previous requests. This means there is no way to remember a user's identity from page to page. Instead, web applications requiring user login must use a session, which is a semi-permanent connection between two computers (such as a client computer running a web browser and a server running Rails).
- Since HTTP is stateless, we must rely on the user's browser and the website's server(s) to persist any sort fo simple state.
  - On each HTTP request, the server sends information to the browser. Cookies were invented as a means to store that data.
- A cookie is a hash that gets stored in the browser and sent back to the server along with every subsequent request.
- There's also an important server-side use case for temporarily persisting data while a user browses the server's website.
  - Similarly to cookies, a session is an object, like a hash, that stores data describing a client's interactions with a website at a given point in time.
  - The session hash lives on the server. Your application can access it via any of your controllers at any point in time.
- Web applications use both cookies and session data.
  - When the client sends a request to a web app, it will generate and store some data about them on the server. This data will be kept in a session hash, and also placed into a small text snippet called a cookie. The cookie is sent back to the client and stored in the client's browser. When a website sets cookies, they persist between pages while the client continues to browse the web. Upon any subsequent visits to the website that originally set the cookies, the cookies are sent back to the site's server. When that happens, the client-side cookie data will be compared to the server-side session data to help the application determine what steps to take and what information to send back to the client.

### How Do Cookies Work

1. The client visits a webpage, such as facebook.com.
2. Facebook's web application receives the request and creates a cookie with some information about the client as a user.
3. Facebook sends that cookie back to the browser, where it is stored. Cookies last until they expire or are deleted.
4. Every subsequent request the client makes to facebook.com sends the cookies back to the server, where Facebook can access them, retrieve information, and alter the cookies.

#### What is contained in a cookie

A cookie will usually contain a URL to the generating website, the date on which it was created (and the date on which it is set to expire, if applicable), and other pertinent information that the web application had requested to persist (such as remembered login information, user preferences, etc.).

### Session Cookies vs. Persistent Cookies

- Session cookies allow a website to keep track of your movement from page to page for that specific session (from the time you log in to the time you log out or close the browser). Session cookies simply allow you to navigate through a site without repeatedly having to authenticate yourself on every new page you visit within the web application domain. Session cookies expire every time you log out or navigate away from the website.
  - If we didn't have session cookies, every time we added an item to our Amazon shopping cart and proceeded to the checkout page, the newly-loaded page would have no recollection of our prior activity. We wouldn't be able to keep items in the cart.
- Persistent cookies allow a website to remember your user information and preferences for future visits. A persistent cookie is stored on your computer, while a session cookie is temporarily stored in your web browser. Persistent cookies allow for faster page loading, automatic login and user authentication, and access to other potential web application features. Much of the data that these features require will be hanging out already in a persistent cookie, stored on your computer. This means you can skip the process of sending a web request to a site and waiting to receive data back from the server in order to log in, for example. Persistent cookies are usually created on the first visit to a page after you have created an account on teh site, and they typically persist unless either the web application has a protocol in place for cookie expiration or the user clears their browser's cache.
  - If we didn't have persistent cookies, we would have to type in our email and password every time we wanted to log in to a web app, making the quality of the user's experience go way down.

#### Cookies and Sessions: Teamwork

You can think of cookies as the client-side counterpart to sessions. They store information locally and are visible only to the server that created them. Client browsers send cookies to remote servers along each web request. The web application on the server reads the cookie, associates it with an existing session (if such a session exists), adn decides how to respond.
