# Lesson: How the Internet Works

## Notes

### Client and Server

- The Internet operates based on conversations between the client (more familiarly known as the browser) and the server (the code running the website you're trying to load). By typing in that URL into your browser, you (the client) are _requesting_ a web page. The server then receives the request, processes it, and sends a _response_. Your browser receives that response and shows it to you.
  - These are the fundamentals of the web. Browsers send requests, and servers send responses.

### HTTP Overview

- Being able to switch out both the server or the client happens because the way browsers and servers talk is controlled by a contract or _protocol_. Specifically, it is a protocol created by Tim Berners-Lee called the Hyper Text Transfer Protocol, or HTTP.
- `HTTP` is the language browsers speak. Every time you load a web page, you are making an `HTTP` request to the site's server, and the server sends back an `HTTP` response.

### Requests

#### URI

- When you make a request on the web, how do you know where to send it? This is done through Uniform Resource Identifiers, or URIs. (URIs are the same as URLs, Uniform Resource Locators.)
- The URI is broken into three parts:
  - The protocol: `https`
  - The domain: `meghangutshall.com`
  - The resource: `/grammygoogles`
- The `protocol` is the way we're sending out request. There are different types of Internet protocols (SMTP for emails, HTTPS for secure requests, FTP for file transfers). To load a website, we use HTTP.
- The `domain name` is a string of character that identifies the unique location of the web server that hosts that particular website. This will be things like `youtube.com` and `google.com`.
- The `resource` is the particular part of the website we want to load.
  - Another word used for resource is `path`.

#### HTTP Verbs

- When you're making a request, not only do you want to give all the details of your request, you also need to specify what action you would like the server to do. We do this with HTTP Verbs. With the same resource, you may want more than one action to occur.
- Using a browser, almost all requests are `GET` requests. (This just means: "Hey server, please GET me this resource.") A full list of HTTP Verbs includes:
  - `HEAD`: Asks for a response like a GET but without the body
  - `GET`: Retrieves a representation of a resource
  - `POST`: Submits data to be processed in the body of the request
  - `PUT`: Uploads a representation of a resource in the body of the request
  - `DELETE`: Deletes a specific resource
  - `TRACE`: Echoes back the received request
  - `OPTIONS`: Returns the HTTP methods the server supports
  - `CONNECT`: Converts the request to a TCP/IP tunnel (generally for SSL)
  - `PATCH`: Apply a partial modification of a resource

#### Request Format

- When the client makes a request, it includes other items besides just the URL in the "headers". The request header contains all the information the server needs in order to fulfill the request: the type of request, the resource (path), the domain as well as some other metadata like what type of browser is making this request.

### Responses

- Once your server receives the request, it will do some processing and then send a response back.
- The server's response is separated into two sections, the headers and the body.
  - The headers are all of the metadata about the response. This includes things like content-length (how big is my response) and what type of content it is. The headers also include the status code of the response.
  - The body of the response is what you see rendered on the page (mostly HTML and CSS). Most of the data of a response is in the body, not the headers.

#### Status Codes

- Every time there is a successful response (you'll know it's successful because the page will load without any errors), it's a status code of `200`, but there are other codes and it's good to get familiar with them. You've probably seen the second-most popular status code, `404`. This means "file not found". Status codes are separated into categories based on their first digit. Here are the different categories:
  - 100's: informational
  - 200's: success
  - 300's: redirect
  - 400's: error
  - 500's: server error

### Servers

- It is important to note that there are two different types of webapps: static and dynamic. A `static` webapp is one that doesn't change. The content doesn't change unless a developer opens up an HTML file and modifies the content of that file. `Dynamic` webapps are sites where the content changes based on user input (e.g. Facebook, Twitter, Yelp, etc.). Every time you visit the site, the content is most likely different because someone else gave a review of that restaurant, or sent out a new tweet, or commented on that image you liked.
- The flow of request a response changes slightly based on a static or dynamic webapp.
  - When a client wants to load a static site, the client makes a request, the server finds the file on a disk, and send it back.
  - With a dynamic webapp, the client makes a request, the server runs application code, and returns a dynamically generated response.