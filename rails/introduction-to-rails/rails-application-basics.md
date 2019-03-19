# Rails Application Basics

## What is Ruby on Rails?

- **A web framework**: A web framework provides developers the tools they need in order to build applications. When every application is unique, there are certain components that cna be found in almost every application, such as: routing, asset management, database connections, etc. A good web framework gives developers these baseline tools so that they don't have to create the base application functionality for each new project.
- **A Ruby gem**: At its core, Ruby on Rails is simply a set of Ruby code libraries, and since the entire codebase is open source, you have the ability to review the framework to better understand how it works.
- **An MVC framework**: MVC stand for Model-View-Controller, this essentially means that Rails takes advantage of the popular application architecture that helps developers naturally separate concerns and organize the applications properly. This setup encourages a specific set of conventions, such as placing the logic for the application in the model files, managing the code flow in the controllers, and displaying content to the user in the views.

## Creating Your First Rails Project

### Generating A New Rails Application

- To create a new Rails app, run the following command: `rails new app-name`
  - For Rails app naming conventions, typically you'll want to use all lower case letters, separated by '-'.

### Rails File Structure Overview

- **`app`**: Contains the models, views, and controllers, along with the rest of the core functionality of the application. This is the one directory where you can make a change and not have to restart the Rails server. The majority of your time will be spent working in this directory. In addition to the full MVC structure, this directory also contains non-Ruby files, such as: CSS files, JavaScripts, images, fonts, etc.
- **`bin`**: Some built-in Rails tasks that you most likely will never have to work with.
- **`config`**: The `config` directory manages a number of settings that control the default behavior, including: the environment settings, a set of modules that are initialized when the application starts, the ability to set language values, the application settings, the database settings, the application routes, and lastly the secret key base.
- **`db`**: Within the `db` directory you will find the database schema file that lists the database tables, their columns, adn each column's associated data type. The `db` directory also contains the `seeds.rb` file, which let's you create some data that can be utilized in the application. This is a great way to quickly integrate data in the application without having to manually add records through a web form element. The schema file can be found at `db/schema.rb`.
- **`lib`**: While many developers could build full applications without ever entering the `lib` directory, you will discover that it can be incredibly helpful. The `lib/tasks` directory is where custom rake tasks are created. You have already used a built-in rake task when you ran the database creation and migration tasks; however, creating custom rake tasks can be very helpful and sometimes necessary. For example, a custom rake task that runs in the background, making calls to an external API and syncing the returned data into the application's database.
- **`log`**: Within the `log` directory you will discover the application logs. This can be helpful for debugging purposes, but for a production application it's often better to use an outside service since they can offer more advanced services like querying and alerts.
- **`public`**: This directory contains some of the custom error pages, such as 404 errors, along with the `robots.txt` file which will let developers control how search engines index the application on the web.
- **`test`**: By default, Rails will install the test suite in this directory. This is where all of your specs, factories, test helpers, and test configuration files can be found. _Side note: We always use RSpec, which means this directory will actually be called `spec`._
- **`tmp`**: This is where the temporary items are stored and is rarely accessed by developers.
- **`vendor`**: This directory has been utilized for varying purposes in the past. In Rails 4+, its main purpose is for integrating Client-side MVC frameworks, such as AngularJS.
- **`Gemfile`**: The `Gemfile` contains all of the gems that are included in the application; this is where you will place outside libraries that are utilized in the application. After any change to the `Gemfile`, you will need to run `bundle`. This will call in all of the code dependencies in the application. The gem process can seem like a mystery to new developers, but it is important to realize that the gems that are brought into an application are simply Ruby files that help extend the functionality of the app.
- **`Gemfile.lock`**: This file should not be edited. It displays all of the dependencies that each of the gems contain along with their associated versions. Messing around with the lock file can lead to application bugs due to missing or altered gem dependencies.
- **`README.rdoc`**: The `readme` file is an important place to document the details of the application. If the application is an open-source project, that is where you can place instructions to other developers, such as how to get the app up and running locally.

### Creating the Database

- Create the database by running: `rake db:create`.

### Starting Up the Rails Server

- To start up the Rails server, make sure that you are in the root of the application in the terminal and run: `rails s`.
- Verify that the server is working properly by navigating to `http://localhost:3000/`.
- To shutdown the server, press `CTRL+C`.

### Using the Rails Console

- To start up the Rails console, run the follow command in the terminal: `rails c`.
- To end the console session, run `control + d` and you'll return to the regular terminal session.
- Rails console loads the full Rails environment while IRB does not, so we opt for using the console over IRB.