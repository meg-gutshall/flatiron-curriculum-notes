# Lesson: Intro to Rake

## Notes

- Rake is a tool that is available to us in Ruby that allows us to automate certain jobs.
  - Rake allows us to define something called "Rake tasks" that execute these jobs. Once we define a task, that task can be executed from the command line.
- Rake provides us a standard, conventional way to define and execute tasks using Ruby.

### How to Define and Use Rake Tasks

- Building a Rake task is easy, since Rake is already available as a part of Ruby. All we need to do is create a file in the top level of our directory called `Rakefile`.
- We define tasks with `task` + `name of task as a symbol` + a block that contains the code we want to execute.
  - Run the task by typing `rake hello` in your terminal.

#### Describing Our Tasks for `rake -T`

- We can run `rake -T` in the terminal to view a list of available Rake tasks and their descriptions. In order for `rake -T` to work though, we need to give our Rake tasks descriptions.
  - Now when we run `rake -T` from the terminal, we'll see the Rake task followed by a description.

#### Namespacing Rake Tasks

- It is possible to group your tasks according to their purpose.
- To use a namespaced Rake task, you must write `rake namespace:task_name`.

### Common Rake Tasks

#### `rake db:migrate`

- One common pattern you'll soon become familiar with is the pattern of writing code that creates database tables and then "migrating" that code using a rake task.
  - We call tasks `migrate`, because it is a convention to say we are "migrating" our database by applying SQL statements that alter that database.

#### Task Dependency

- Some Rake tasks create a dependency (task :migrate => :environment do ...), which means that we need to define another Rake task called `:environment` that will run with our `:migrate` Rake task.

#### `rake db:seed`

- This task is responsible for "seeding" our database with some dummy data.
  - The conventional way to seed your database is to have a file in the `db` directory, `db.seeds.rb`, that contains some code to create instances of your class.

#### `rake console`

- We'll define a task that starts up the Pry console. We'll make this task dependent on our `environment` task so that our class and the database connection load first.

## Code Examples

### Rake Task

```ruby
task :hello do
  # the code we want to be executed by this task
end
```

### Rake Console

```ruby
desc 'drop into the Pry console'
task :console => :environment do
  Pry.start
end
```