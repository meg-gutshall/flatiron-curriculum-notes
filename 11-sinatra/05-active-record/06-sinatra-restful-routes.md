# Lesson: Sinatra RESTful Routes

## Notes

- A RESTful route is a route that provides mapping between HTTP verbs (get, post, put, delete, patch) to controller CRUD actions (create, read, update, delete). Instead of relying solely on the URL to indicate what site to visit, a RESTful route also depends on the HTTP verb **and** the URL.
  - What this means is that when your application receives an HTTP request, it introspects on that request and identifies the HTTP method and URL, connects that with a corresponding controller action that has that method and URL, executes the code in that action, and determines which response gets sent back to the client.
- It's important to note that much of the CRUD actions are different actions that occur on the same resource, which is why separating the action (the HTTP verb) from the resource (the URL path) is important.

**Browser Caveat**
Browsers behave a little strangely as it relates to `PUT`, `PATCH`, and `DELETE` requests, in that they don't know how to send those requests. Forms that delete adn edit need to be submitted via `POST` requests.

### Routes Overview

Let's take a magazine website as an example. You'd want a controller action to create a new article (new route), to display one article (show route), to display all articles (index route), to delete an article (delete route), and a page to edit an article (edit route).

|**HTTP Verb**|**Route**|**Action**|**Used For**|
|---|---|---|---|
|GET|'/articles'|index action|index page to display all articles|
|GET|'/articles/new'|new action|displays create article form|
|POST|'/articles'|create action|creates one article|
|GET|'/articles/:id'|show action|displays one article based on ID in the URL|
|GET|'/articles/:id/edit'|edit action|displays edit form based on ID in the URL|
|PATCH|'/articles/:id'|update action|_modifies_ an existing article based on ID in the URL|
|PUT|'/articles/:id'|update action|_replaces_ an existing article based in ID in the URL|
|DELETE|'/articles/:id'|delete action|deletes one article based on ID in the URL|

### The Routes

#### Index Action

- The controller action above responds to a `GET` request to the route `'/articles'`. This action is the `index action` and allows the view to access all the articles in the database through the instance variable `@articles`.

#### New Action

- Above, we have two controller actions. The first one is a `GET` request to load the form to create a new article. The second action is the `create action`. This action responds to a `POST` request and creates a new article based on the params from the form and saves it to the database. Once the item is created, this action redirects to the `show` page.

#### Show Action

- In order to display a single article, we need a `show action`. This controller action responds to a `GET` request to the route `'/articles/:id'`. Because this route uses a dynamic URL, we can access the ID of the article in the view through the `params` hash.

#### Edit Action

- The first controller action above loads the edit form in the browser by making a `GET` request to `'/articles/:id/edit'`.
- The second controller action handles the edit form submission. This action responds to a `PATCH` request to the route `'/articles/:id'`. First, we pull the article by the ID from the URL, then we update the title and content attributes and save. The action ends with a redirect to the article show page.

#### Delete Action

- On the article show page, we have a form to delete it. The form is submitted via a `DELETE` request to the route `'/articles/:id/delete'`. This action find the article in the database based on the ID in the URL parameters, and deletes it. It then redirects to the index page `'/articles'`.

### Using `PATCH`, `PUT`, and `DELETE` Requests with `Rack::MethodOverride` Middleware

- In order to use this middleware, and therefore use `PATCH`, `PUT` and `DELETE` requests, you'll need to place the line `use Rack::MethodOverride` in the `config.ru` file _above_ the `run ApplicationController` line.
  - In an application with multiple controllers, `use Rack::MethodOverride` must be place **above all controllers** in which you want access to the middleware's functionality.
- The middleware will then run for every request sent by our application. It will interpret any requests with `name="_method"` by translating the request to whatever is set by the `value` attribute. This is how the `post` request gets translated to a `patch`, `put`, or `delete` request.
- To send these requests, the second line of any form that edits, updates, or deletes should be written as follows: `<input type="hidden", name="_method", value="patch/put/delete">`.

## Code Examples

### Index Action Code

```ruby
get '/articles' do
  @articles = Article.all
  erb :index
end
```

### New Action Code

```ruby
get '/articles/new' do
  erb :new
end

post '/articles' do
  @article = Article.create(params)
  redirect "/articles/#{@article.id}"
end
```

### Show Action Code

```ruby
get '/article/:id' do
  @article = Article.find(params[:id])
  erb :show
end
```

### Edit Action Code

```ruby
# Load edit form
get '/articles/:id/edit' do
  @article = Article.find(params[:id])
  erb :edit
end

# Edit action
patch '/articles/:id' do
  @article = Article.find(params[:id])
  @article.title = params[:title]
  @article.content = params[:content]
  @article.save
  redirect "/articles/#{@article.id}"
end
```

### Delete Action Code

```ruby
delete '/articles/:id/delete' do
  @article = Article.find(params[:id])
  @article.delete
  redirect '/articles'
end
```
