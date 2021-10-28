---
description: 'Version 8: Module 14: Section 6: Code-along'
---

# Review of Rails MVC

With Rails, we aren't required to strictly render ERB views.

## Review of MVC Structure

The model, view, controller structure is a separation of concerns where groups of files have specific jobs and interact with each other in very defined ways:

* **Models:** The "logic" of a web application. This is where data is manipulated and/or saved to a database.
* **Views:** The "frontend," user-facing part of a web application. This is the only part of the app that the user interacts with directly. Views generally consist of HTML, CSS, and JavaScript.
* **Controllers:** The go-between for models and views. The controller relays data from the browser to the application, and from the application to the browser.

Rails favors convention over configuration. For this reason, if a _**folder**_ and _**file**_ are present in the _**views**_ folder that corresponds to a _**controller**_ and _**action**_ listed on a _**route**_, Rails will display that _**view**_ by default.

## Resources

* [ActiveRecord Basics (Rails Guides)](https://guides.rubyonrails.org/active\_record\_basics.html)
* [Layouts and Rendering in Rails (Rails Guides)](https://guides.rubyonrails.org/layouts\_and\_rendering.html)
