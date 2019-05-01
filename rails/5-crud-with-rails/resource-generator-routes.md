# Lesson: Resource Generator/Routes

## Generating A Scaffold

- It is not considered a good practice to use scaffolds in a production application. However, they can be a great reference for how we can build CRUD functionality into our apps.

First, let's discuss why it's not a great idea to use scaffolds in real world development. Let's start with a case study to see what a scaffold actually creates. Run this command in the terminal:

```bash
rails g scaffold Article title:string body:text
```

Let's review the console log to see what this creates for us:

```bash
invoke  active_record
create    db/migrate/20151128001950_create_articles.rb
create    app/models/article.rb
invoke    rspec
create      spec/models/article_spec.rb
invoke      factory_girl
create        spec/factories/articles.rb
invoke  resource_routes
route     resources :articles
invoke  scaffold_controller
create    app/controllers/articles_controller.rb
invoke    erb
create      app/views/articles
create      app/views/articles/index.html.erb
create      app/views/articles/edit.html.erb
create      app/views/articles/show.html.erb
create      app/views/articles/new.html.erb
create      app/views/articles/_form.html.erb
invoke    rspec
create      spec/controllers/articles_controller_spec.rb
create      spec/views/articles/edit.html.erb_spec.rb
create      spec/views/articles/index.html.erb_spec.rb
create      spec/views/articles/new.html.erb_spec.rb
create      spec/views/articles/show.html.erb_spec.rb
create      spec/routing/articles_routing_spec.rb
invoke      rspec
create        spec/requests/articles_spec.rb
invoke    helper
create      app/helpers/articles_helper.eb
invoke      rspec
create        spec/helpers/articles_helper_spec.rb
invoke    jbuilder
create      app/views/articles/index.json.jbuilder
create      app/views/articles/show.json.jbuilder
invoke  assets
invoke    coffee
create      app/assets/javascripts/articles.coffee
invoke    scss
create      app/assets/stylesheets/articles.scss
invoke    scss
create      app/assets/stylesheets/scaffolds.scss
```

- The other generators (`migrations`, `controllers`, and `resources`) create a structure and back-end functionality for our code. However, scaffolds actually go beyond the other generators and create both the front- and back-end code needed for CRUD features.
- Within less than a minute, the scaffold system built an entire CRUD-based feature, and we didn't write a single line of code!
- What did the scaffold build for us? If we look through the files that got printed out in the console, we see:
  - A migration file
  - A model file
  - A controller
  - View templates for each of the controller actions that render a view
  - The full set of RESTful routes
  - And every other component needed for a functional CRUD environment

## DRYing Up the `ArticlesController`

If you look through the code in the `ArticlesController`, you'll see a few familiar methods, such as: `index`, `new`, `edit`, `update`, and `show`. If you remember prior lessons, you may remember that we had some duplicate code. For example, if we had `show`, `edit`, and `update` actions in the controller, we had three different calls, such as:

```ruby
# app/controllers/articles_controller.rb

@article = Article.find(params[:id])
```

This was necessary so that we could grab the `/:id` parameter from the URL string, but, as you may have noticed, the scaffold implemented an elegant solution to remove the duplicate code:

```ruby
# app/controllers/articles_controller.rb

before_action :set_article, only: [:show, :edit, :update, :destroy]
```

The `show`, `edit`, `update`, and `destroy` actions will all have the `set_article` method called before any other code in the action is run. If you want to inspect the code for the `set_article` method, it's declared at the bottom of the controller:

```ruby
# app/controllers/articles_controller.rb

def set_article
  @article = Article.find(params[:id])
end
```

As you can see, the method returns the `@article` instance variable that each of the controller actions will automatically have because of the `before_action`.

Another way that scaffolds show how to DRY up controller code can be found in the other `private` method:

```ruby
# app/controllers/articles_controller.rb

def article_params
  params.require(:article).permit(:title, :body)
end
```

Even though scaffolds are great for learning how CRUD works in Rails, it's still considered a bad practice to use them in production applications. The main reason why scaffolds are discouraged in production is because they create so much code and so many files that they can be hard to manage.

## Scaffold vs Resource Generators

- So what's a good alternative to utilizing scaffolds? The `resource` generator!
- The scaffold generator builds out the system in a very specific manner, which is rarely the way _you_ would want to build _your_ application.
- With modern development practices, a large number of Rails apps are leveraging client-side MVC setups such as Backbone or AngularJS. These frameworks render the view templates for a Rails application pointless, so if you rely on using scaffolds, you're going to have to be removing quite a bit of code after each `generate` command.
- If you compare scaffold with the `resource` generator, the code from the `resource` generator will build out the base setup required for the new feature, but it will let you control the implementation.