# Rails Resources, Models, & Templating

## The Rails Way or the Highway

### Separating Concerns

In writing a large application, it's important to establish something known as **Separation of Concerns**, writing modular code with each piece focusing on one aspect of the application. The benefit here is similar to the idea of compartmentalization on a production line: it allows for more rapid development by being able to divide and conquer the construction of a product. Compartments on assembly lines can focus on one task and optimize their process without involving other groups of assembly line workers; they still create the expected component. Ultimately, using separation of concerns reduces the headache of debugging and controlling a large application that will ultimately grow to a level of complexity that no one person would ever fully need to comprehend.

### Organizational Principles

In order to manage the development of new parts of a project, it's important to construct guidelines that will shape how things are organized and separated. These guidlines form a *design pattern*, which everyone can use to maintain consistent organization of application components. This often involves a conventional choice that helps to scale a project in ways other developers expect and understand. Part of the role of a developer is to become familiar with using design patterns, but this takes time (and trust). Different patterns emphasize an array of qualities: scalability, modularity, interoperability, security, performance, et cetera.

## Model-View-Controller (MVC)

In Rails, we see one of the most popular patterns for Web Application Design, **Model-View-Controller**. The MVC pattern separates data concerns, presentation concerns, and request and response (or action) concerns.

### MVC

| Component | Type of Concern |
| :--- | :--- |
| **M**odel | Data Concerns |
| **V**iew | Presentation Concerns |
| **C**ontroller  | Request and Response (or Action) Concerns |

The **Model** component takes care of the logic associated with our data. Having a **Model** component helps avoid issues of mixing the logic of gathering or editing data (Model) with displaying it (Views) or determining what data is related to requests from app users (Controllers).

The **View** component specializes in presentation of html to users, incorporating data without worrying about how data was stored (Model) or if it was relevant to a request made by a user (Controller).

The **Controller** component helps the app determine which data resources are relevant to a request from a user, what to do with the data, and how to respond to a user, without worrying about how to present an html response (View) or manage logic concerning data (Model).

## Rails Resources

Rails is a Resource-Oriented Architecture, meaning that we define our application's functionality in terms of resources. You can think of a resource as one type of data, for example `users` or `posts`. The MVC pattern helps us keep logic for one resource separate from logic for another resource. For example, for our `posts`, we'll have a  model, possibly some views, and controller that ONLY deal with `posts` functionality. Similarly, `users` will have its own model, its own set of views, and its own controller.

### Routing for One Resource

We use RESTful routing to define our routes for a single resource. In Rails, each route in the routes file maps to an action in one resource's controller. Here is an example of RESTful routes for a `photos` resource, along with the matching controller actions (controller actions are denoted with the format `controller#action`):

| HTTP Verb | Route | Controller Action |
| :--- | :--- | :--- |
| GET | `/photos` | `photos#index` |
| GET | `/photos/new` | `photos#new` |
| POST | `/photos` | `photos#create` |
| GET | `/photos/:id` | `photos#show` |
| GET | `/photos/:id/edit` | `photos#edit` |
| PUT | `/photos/:id` | `photos#update` |
| DELETE | `/photos/:id` | `photos#destroy` |

Rails let us set up all our RESTful routes for one resource with *just one* line of code in `config/routes.rb`:

```ruby
#
# config/routes.rb
#

resources :photos
```

When you run `rake routes` from the terminal, you'll see all seven RESTful routes defined for our `photos` resource.

### Controller Actions

As we can see above, each of our RESTful routes maps to a controller action. Controller actions are defined as methods in the controller. Here is what the `PhotosController` would look like:

```ruby
#
# app/controllers/photos_controller.rb
#

class PhotosController < ApplicationController

  # GET /photos
  def index
  end

  # GET /photos/new
  def new
  end

  # POST /photos
  def create
  end

  # GET /photos/:id
  def show
  end

  # GET /photos/:id/edit
  def edit
  end

  # PUT /photos/:id
  def update
  end

  # DELETE /photos/:id
  def destroy
  end

end
```

You may be thinking that these methods don't do anything yet, and you're absolutely right! One thing our controller methods will do is handle rendering views and redirecting where necessary. Here is an example of a controller method that renders a view, and one that redirects:

```ruby
class PhotosController < ApplicationController

  # GET /photos
  def index
    render :index
  end

  # POST /photos
  def create
    # logic to create new photo in db goes here

    redirect_to "/photos"
  end

end
```

Our controller methods are also supposed to help our app handle users' requests to manage data, and in order to do this, we need a model in our database.

### Data Models

In order for our controller to do anything meaningful related to a resource, we need a model for that resource. We'll use our model to find data, create new data, update data, and delete data. For Rails defaults, a model is a representation of a SQL table in our database. SQL is just a programming language for interacting with a certain kind of database.  In Rails, communication between the actual SQL table and the models we'll interact with in our code is handled by an ORM called <a href="http://guides.rubyonrails.org/active_record_basics.html#what-is-active-record-questionmark">ActiveRecord</a>. Like mongoose, ActiveRecord has a list of pre-stored database commands to facilitate the communication.

In Terminal, we can create our `photo` model using a rails generator:

```
$ rails g model photo title:string description:string image_url:string
```

This command creates a set of instructions in our app to tell SQL to create our model. To actually create this data table in our SQL database, we run a migration:

```
$ rake db:migrate
```

Now our application has access to a model called `Photo`, and `Photo` data is persistent! Don't worry too much about ActiveRecord, SQL databases, and the `rake` command just yet. We'll be going over all these concepts in way more detail next week, but for now, this is all you need to get a model up and running that persists to your database.

### Rails Console

Rails gives us a very useful way of interacting with our development database from our terminal. Typing `rails console` or `rails c` in the terminal puts you in the Rails console. The Rails console is much like `irb`, but with access the data models in your application. Remember you must be in the root directory of your Rails app to enter the Rails console.

Whenever setting up a model, you should *always* use the Rails console to make a test data item before doing anything else. This is a good check to make sure the model was set up correctly, and you can debug any issues before you continue coding. It's also nice to have some initial "seed" data in your database to work with :)

To create a new `photo` in our database from the Rails console:

```
$ rails c
irb(main):001:0> Photo.create({title: "Golden Gate Bridge", description: "Black & White", image_url: "gg_bridge.png"})
=> #<Photo id: 1, title: "Golden Gate Bridge", description: "Black & White", image_url: "gg_bridge.png", created_at: "2015-07-29 17:27:06", updated_at: "2015-07-29 17:27:06">
```

## Resources Video

[![Rails Resources](http://img.youtube.com/vi/QYHdAGRzmMA/0.jpg)](https://www.youtube.com/watch?v=QYHdAGRzmMA)

## Models Video

[![Rails Models](http://img.youtube.com/vi/rKtLU2LcGA8/0.jpg)](https://www.youtube.com/watch?v=rKtLU2LcGA8)]

## Templating

The rails framework is based on a server-side architecture. The client will be passive and the server is very active. The server sends primarily HTML (and not JSON) back to the client. The server (not the client) will keep track of "state". State will be reflected in the HTML with which the server responds. That HTML is built with server-side templating called "erb" - **Embedded Ruby**.

The Rails framework provides a large number of helpers for working with assets, dates, forms, numbers and model objects, to name a few. These helpers are available to all templates by default.

In addition to using the standard template helpers provided, creating custom helpers to extract complicated logic or reusable functionality is strongly encouraged.

Here are a list of some built-in erb template helpers with examples.

## Helpers

### Loops

erb
```html
<h1>Names of all the people</h1>
<% @people.each do |person| %>
  Name: <%= person.name %><br>
<% end %>
```

### Links
HTML
```html
<a href="/articles/3">Show</a>
```

erb
```html
<%= link_to "Show", article_path(@article) %>
```

### URL Links
HTML
```html
<a href="http://google.com">Google</a>
```

erb
```html
<%= link_to "Google", "http://google.com" %>
```

### Images

HTML
```html
<img src="/images/doggie.png" width="100px" class="img-responsive"/>
```

erb
```html
<%= image_tag 'doggie.png', width: "100px", class:"img-responsive" %>
```

### Forms, Labels, and Inputs

HTML
```html
<form action="/articles" class="form">
  <label for="title">Title</label>
  <input type="text" name="article[title]" placeholder="Title text here..."/>
  <button type="submit" class="btn btn-default">Publish</button>
</form>
```

erb
```html
<%= form_for @article, class:"form" do |f| %>
  <%= f.label :title %>
  <%= f.text_field :title %><br />
  <%= f.submit "Publish", class:"btn btn-default" %>
<% end %>
```

Also ```radio_button("article", "category", "rails")``` and ```check_box("article", "validated")```

### Distance of Time in Words (e.g. crazy sh*t)


```ruby
distance_of_time_in_words(Time.now, Time.now + 15.seconds)
# => less than a minute
```

Number Helpers
```ruby
number_to_human_size(1234)          # => 1.2 KB
number_to_human_size(1234567)       # => 1.2 MB
number_to_phone(1235551234) # => 123-555-1234
```

"Humanize" a variable name
```ruby
'employee_salary'.humanize              # => "Employee salary"
'author_id'.humanize                    # => "Author"
'author_id'.humanize(capitalize: false) # => "author"
```

### Other built-in Rails helpers worth mentioning
```yield```, ```content_for```