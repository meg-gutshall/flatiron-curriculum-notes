# Lesson: Refresher on MVC

For this lesson, we are assuming the mindset of a software architect. Software architects, most likely your senior collaborator as you enter the workforce, don't focus on making a piece of code work. Rather, they are focused on making design decisions which allow for ease of change, extensibility, and avoidance of bugs.

## MVC Overview

MVC was created as a general purpose solution designed to bridge the gap between a user's mental model of a program and a computer's _actual_ implementation. As we have been unknowing 'users' of the MVC pattern most of our lives, we need to change our perspective to understand it as programmers. When considering interfaces using the MVC pattern, the most critical shift in perspective to recognize is that the MVC pattern _helps separate concerns_.

## Separation of Concerns

At its core, MVC is designed to modularize distinct functionality with an application. While the MVC pattern can be used with many different types of applications, let's identify its distinct parts in the context of a web application:

- `View`: What an end user on a website experiences when interacting with a program in their browser: what they read, what they click, what flashes at them, and what they hear (despite the name "view"). In technology-speak, the vocabulary word would be _interface_.
- `Model`: Where the actual data, resides and is altered.
- `Controller`: What manages communication between the two: it takes model information and prepares it for the view and vice versa.

Now that we have identified the core components, let's examine what they actually do when a user engages with our web application:

1. A user, through interaction with the `view`, (in this case, the browser's GUI), requests data (clicks on a link, submits a form, enters a URL in the browser's bar)
2. The request is sent across the Internet to the server
3. The `controller` (_which does not change data itself_) asks the `model` to either provide it data (which it will then send) or to change model-held data depending on the user's request
4. The `model` accesses/manipulates the actual ones and zeros held on the server's database and returns the desired result to the `controller`
5. The `controller` packs the response and sends it back to the client
6. The `view` (on the originating client's machine) _presents_ the data for the user

### An Advantage of Modularity

Remember, we said that _software architects_ focus on making design decisions which allow for ease of change, extensibility, and avoidance of bugs. For every new device (think Internet, then smartphones, then virtual assistants), we write new-device-only code (i.e. `view` code) which **cannot** introduce bugs into the pre-existing `model` or `controller` code. It's because of design patterns like this that 1970's banking software is still holding your account data while you view and manipulate it with 21st century technology.

## Quick Recap

**MVC is designed to:**

- Be language- and application-agnostic
- Be modular: Every part is distinct, encapsulated, and can be replaced without breaking the rest of the application
- Use a `controller` to facilitate communication between the `view`, which the user interfaces with, and the `model`
- Stores 'truth', the _actual data_, in the `model`, which is far abstracted and independent from its representation in the `view`

## Where Rails Fits In

Rails takes architectural guidance on how to separate concerns from the MVC pattern. Like most implementations of academic or philosophical ideals, Rail's implementation is not to-the-letter perfect MVC and that's okay!

### Rails MVC Implementation

The `controller` and `model` implementations in Rails are straightforward to align with our understanding of MVC.

Not only are they named helpfully and live in helpfully-named directories like `models/` and `controllers/`, but they encapsulate their responsibilities as prescribed in the MVC architecture. The controller actions mediate requests and delegate lookups by calling methods on models. As expected, models work with the low-level persistent storage subsystems (e.g. databases) to `UPDATE`, `SELECT`, and `DELETE` data in the database. The Rails views are templates for displaying data. They are automatically turned into HTML that is sent over the Internet by Rails. However, the data they need to "complete" themselves is provided by a Rails controller. Rails "automagically" shares any variable prefixed with `@` in a controller action with the view.
