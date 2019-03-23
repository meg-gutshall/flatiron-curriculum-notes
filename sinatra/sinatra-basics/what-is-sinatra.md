# Lesson: What Is Sinatra?

## Notes

### What's A Web Framework?

Web frameworks take routine and common requirements of any web application and abstract them into code and patterns that provide these functionalities to your application without requiring you to build them yourself.

### What is Sinatra?

Sinatra is a Domain Specific Language (DSL) implemented in Ruby that's used for writing web applications.

- Sinatra is designed to provide you with the bare minimum requirements and abstractions for building simple and dynamic Ruby web applications.
- Because Sinatra doesn't auto-generate files and directories, working with Sinatra allows you to dive in deep with the major concepts of MVC, a system for building web applications that governs 90% of the worlds' apps. In Sinatra, you are required to manually set up routes and connect them to other pieces of your application.

### The Sinatra DSL

Any application that requires the `sinatra` library will get access to methods like `get` and `post`. These methods provide the ability to instantly transform a Ruby application into an application that can respond to HTTP requests.