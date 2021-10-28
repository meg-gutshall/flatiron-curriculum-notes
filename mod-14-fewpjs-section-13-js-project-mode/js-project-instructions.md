---
description: 'Version 8: Module 14: Section 13'
---

# JavaScript Project Instructions

> __[_As extracted from the Learn.co curriculum (v8)_](https://learn.co/tracks/full-stack-web-development-v8/module-14-front-end-web-programming-in-javascript/section-13-project-mode/javascript-project-instructions)__

## Overview

Welcome to your JavaScript Project!

You are going build a Single Page Application (SPA). Your frontend will be built with HTML, CSS, and JavaScript. Your frontend will communicate with a backend API that you'll build with Ruby and Rails. This is a really exciting moment — the whole course up until this point is coming together!

## Objectives

Your goals for this project:

* Design and architect features across the frontend and backend
* Integrate JavaScript and Rails
* Debug issues in small- to medium-sized projects
* Build and iterate on a project MVP
* Communicate in a technical environment

## Project Deliverables

In order to schedule your project review, you must submit:

* A link to your project repo with code for your Rails backend and HTML/CSS/JavaScript frontend
* A `README.md` file describing your application
* A blog post about your application
* A 2–4 minute video demo introducing your application

See the section [Communicating About Your Project](https://github.com/learn-co-students/js-spa-project-instructions-v-000/blob/master/project-planning-tips.md#communicating-about-your-project) in the [Project Planning, Tips, and Support document](https://github.com/learn-co-students/js-spa-project-instructions-v-000/blob/master/project-planning-tips.md) for more guidance on communicating about your project.

As always, you project must be your own work. For more details, see [Project Rules of the Road](https://github.com/learn-co-students/js-spa-project-instructions-v-000/blob/master/project-rules-of-the-road.md).

## Technical and Complexity Requirements

In order to demonstrate your proficiency with what you've learned about web development with JavaScript, here are the requirements for your project. You should view these guidelines as a minimum bar for the features you include in your application. It's your project, and you are encouraged to do above and beyond these requirements:

* The application must be an HTML/CSS/JavaScript frontend with a Rails API backend. All interactions between the client and the server must be handled asynchronously (AJAX) and use JSON as the communication format.
* The JavaScript application must use object-oriented JavaScript (classes) to encapsulate related data and behavior.
* The domain model served by the Rails backend must include a resource with at least one has\_many relationship.
* The backend and frontend must collaborate and demonstrate client-server communication. Your application should have at least three AJAX calls, covering at least two CRUD actions. Your client-side JavaScript code must use `fetch()` with the appropriate HTTP verb and your Rails API should use RESTful conventions.

### Best Practices

You are encouraged to follow development best practices while you are building your application.

### JavaScript

* [ ] Use classes and functions to organize your code into reusable pieces.
* [ ] Translate JSON responses into JavaScript model objects using ES6 class or constructor function syntax.
* [ ] Use ES6 features when appropriate (e.g. arrow functions, `let` and `const`, rest and spread syntax).

### Rails

* [ ] Follow Rails MVC and RESTful conventions.
* [ ] Use aptly-named variables and methods.
* [ ] Use short, single-purpose methods.

### Git

* [ ] Aim for a large number of small commits — commit frequently!
* [ ] Add meaningful messages to your commits. When you look back at your commits with `git log`, the messages should describe each change.
* [ ] Don't include changes in a commit that aren't related to the commit message.

### Suggested Project Structure

You must submit a link to the repo with the code for your project. These is no requirement for how you decide to structure the code within that repo, but in the past, students have has success using a structure like:

{% code title="js-project-file-structure" %}
```bash
javascript-project/
  backend/
    app/
    (...other Rails files and folders)
  frontend/
    index.html
    style.css
    index.js
  README.md
```
{% endcode %}

For more about setting up your backend, you can reference the lesson on [Creating a Rails API from Scratch](../mod-14-fewpjs-section-6-rails-as-an-api/creating-a-rails-api-from-scratch.md).

## What to Expect in Your Project Review

Read the [What to Expect in Your Project Review document](https://github.com/learn-co-students/js-spa-project-instructions-v-000/blob/master/what-to-expect-in-project-reviews.md) for general guidance on what to expect in the project review.

### What Should You Be Prepared for in a Project Review?

During your project review, be prepared to:

* Explain you code from execution point to exit point. Use the best technical vocabulary you can.
* Live code. This could be refactoring, adding a new feature, or both.
* Answer questions about your knowledge of JavaScript Fundamentals.

In particular, the JavaScript Fundamentals concepts your reviewer may ask about include:

* Variables
* Data structures
* Functions
* Hoisting
* Scope
* Context
* `this`
* Closures
* ES6 syntax
* `let` and `const`
* Arrow functions

### Learning Goals

These are the skills and knowledge that you should aim to demonstrate through the project review:

* Explain how Rails routes a request to a controller and method based on the URL and HTTP verb
* Use `render json:` to render serialized JSON
* Select, create, and modify DOM nodes
* Attach listeners to DOM nodes to respond to user interaction
* Use `preventDefault()` to control form submit behavior
* Use `fetch()` with GET, POST, PATCH, and DELETE HTTP methods
* Create a JavaScript object with ES6 class syntax
* Instantiate JavaScript objects and call methods on them
