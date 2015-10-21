# Intro Rails
## Flying Through CRUD

### Related Materials/Information

* Conventions over Configurations 
* Models, Views, and Controllers 
* HTTP (**GET, POST, PUT, Delete**) verbs
* The `params` of a request, (Covered in **Express**)
* Forms (**action**, **method**, and **form fields**)
* redirects



## Lesson Road Map

We demonstrate routing by making an application to handle managing our favorite planes.

* Talk CRUD and RESTful routing conventions
* Create a new **app folder** for our routing app
	* Setup an index
		* write an **index route** for planes
		* make a **controller** for planes
			* make an **index method**
		* make an **index view**
		* generate a **plane model**
	* Setup a new
		* make a **new route** that presents a form for new planes
		* make a **new method** in the **PlanesController**
		* make a **new view**
	* Setup a create
		* make a **create route** for submitting new planes
		* make a **create method** for saving new planes and redirecting
		


## CRUD and REST

**CRUD** stands for **Create**, **Read**, **Update**, **Delete**. These are the minimum and most common actions need for interacting with data in an application. For example someone needs to be able to *Create* their facebook profile, **Read** it, **Update** it, and if they're busy, **Delete** it.

Typically we associate **CRUD** with the following **HTTP** methods

| CRUD Operation | HTTP Method | Example|
| :---  |	:--- | :-- |
| Create | POST | `POST "/puppies?name=spot"` (create a puppy named spot) |
| Read   | GET  | `GET "/puppies"` (Shows all puppies) |
| Update | PUT or PATCH | `PUT "/puppies/1?name=lassy"` (change puppy number 1 to have name lassy) |
| Delete | DELETE | `Delete "/puppies/1"` (destroy the first puppy, yikes!!!!) |

REST stands for **REpresentational State Transfer**. We will demonstrate these practices throughout this lesson, but for now preparing don't worry too much about it yet.

## Part 1: On the Runway 

### Setup With Rails New

| Motive:  |
|:----|
| Familiarize ourselves with the initial setup of a new application with the intent of making a *planes* application |


* `$ rails new route_app`
* `$ cd route_app`
* `$ rails s`

Now our app is up and running, [localhost:3000](localhost:3000/). At our `root`route we notice a "Welcome aboard message". That's because we have yet to create a **controller** and **views** that we can set as our **root**.


### A Look at Routes


In *Rails*, routing information for incoming requests are separated out into their own file, under `config/routes.rb`, that defines how to connect *requests* to *controllers*. Go to `config/routes.rb` and inside the routes block erase all the commented text. It should now look exactly as follows

	Rails.application.routes.draw do

	end




 Now we can define all our routes.

> NOTE: A **Controller** is a class that just handles rendering views and managing data resources using methods you'll define. 


Your `routes.rb` will just be telling your app how to connect *HTTP* requests to a **Controller**. Let's get ready for our first route. 

* In Rails we distinguish the `'/'` (*root*) from other routes, and we just write `root to: 'planes#show'` to indicate it in `routes.rb`.

	`/config/routes.rb`

		Rails.application.routes.draw do

			root to: 'planes#index'

		end

* We should add a resourceful route to get to this page as well. 
	
		Rails.application.routes.draw do

			root to: 'planes#index'

			resources :planes, only: [:index]

		end

	




### Making a Planes Controller

We want to create a *planes_controller*. **NOTE**: Controller names are always plural and files should always be `snake_case`.

	$ subl app/controllers/planes_controller.rb

Let's begin with the following 

	class PlanesController < ApplicationController
		def index
			render text: "Hello, pilots."
		end
	end

We have defined the`PlanesController` *class*, given it the method `#index`, and told the `#index` to render a *text* response `'Hello, pilots.'`

> Note:  We've also indicated that `PlanesController` inherits from `ApplicationController`, which looks like the following:

>		class ApplicationController < ActionController::Base
	 	 # Prevent CSRF attacks by raising an exception.
	 	 # For APIs, you may want to use :null_session instead.
	 	 protect_from_forgery with: :exception
		end

> Indeed, `ApplicationController` also inherits from `ActionController::Base`, which is just the main *action* handling class. Actions it might handle are requests, responses, rendering views, etc. The `ApplicationController` helps define the setup/configuration of all other controllers and has methods defined accross the entire application.


If we go to [localhost:3000/](localhost:3000/) we get the greeting.


### A View For Planes

Let's seperate our rendered greeting into a view called `index.html.erb`, which by default `ActionController` will look for in a  `app/views/planes/` folder. Create the `app/views/planes` folder and the file below

`app/views/planes/index.html.erb`

	Hello, pilots!

and make the following changes to `PlanesController`.

`app/controllers/planes_controller.rb`

	class PlanesController < ApplicationController
		
		def index
			# Note it used to say 
			#	render text: 'Hello, pilots'
			render :index
		end
		
	end

### A Model Plane (an automagical first use)

A model is just a representation of a SQL table in our database, and the communication between the two is handled by rails via `ActiveRecord`, which has a list of prestored SQL commands to facilitate communication.


In terminal, we create our plane model using a rails generator as follows,

	$ rails g model plane name:string design:string description:text
	
which just creates the instructions in our app to tell SQL to create our model. To actually create this table data in our SQL database we do a migration. To migrate our database we use `rake` as follows:

	$ rake db:migrate
	
Now our application will have access to a model called `Plane` that will be persitent. Don't worry too much about the `rake` command that was just used as previous students have had the same frustration with it.

| Jerome Allouche WDI SF (JAN-MARCH) HipChat|
| :--- |
| "[T]ook me a while to understand what "rake" is conceptually \ ... \ maybe include a resource like this? \ [suggestion](https://gist.github.com/DelmerGA/8ad9f9f5b075c51df858) " |

### Making your first Model

**NOTE: DON'T SKIP THIS STEP**

We go straight into terminal to enter *rails console*.

	$ rails console
The command above enters the rails console to play with your application. 

To create our first plane model in our database we use our reference to the `Plane` class and call the `Plane#create` method to write our plane to our database.

	> Plane.create({name: "x-wing", design: "unknown", description: "top secret"}) 
	=> #<Plane ....>

This will avoid issues later with `index` trying to render planes that aren't there.

## Back to Routes

|	Motive	|
|	:----	|
|	We've seen a little of each part of the MVC framework, and now we cycle back through over and over as we develop an understanding of the work flow.

	

### A new route for planes

We don't have any planes in our database yet. To be able to make planes we must create a route for them. The *RESTful* convention would be to make a form available at `/planes/new`. 

Let's add this route.

`/config/routes.rb`

	Rails.application.routes.draw do
		root to: 'planes#index'

		resources :planes, only: [:index, :new]
		
	end

### A new method for planes

The request for `/planes/new` will search for a `planes#new`, so we must create a method to handle this request. This will render the `new.html.erb` in the `app/views/planes` folder.

`app/controllers/planes_controller.rb`

	class PlanesController < ApplicationController
		
		...
		
		def new
			render :new
		end
		
	end



### A new view for planes

Let's create the `app/views/planes/new.html.erb` with a form that the user can use to sumbit new planes to the application. Note: the action is `/planes` because it's the collection we are submiting to, and the method is `post` because we want to create.


`app/views/planes/new.html.erb`

	<form action="/planes" method="post">
		<input type="text" name="plane[name]">
		<input type="text" name="plane[design]">
		<textarea name="plane[description]"></textarea>
		
		<button> Save Plane </button>
	</form>

Note: how we have now defined our next `route`, which is 
	
> **post "/planes"** which should be handled by a  **"planes#create"**
	


### Creating another route


Our submission of the `plane` form in `new.html.erb` isn't being routed at the moment let's change that


`/config/routes.rb`

	Rails.application.routes.draw do

		root to: 'planes#index'
		
		resources :planes, only: [:index, :new, :create]
		
	end


### Creating another method

This leads to the most complicated method yet to be talked about. For now we will just make it redirect to the `"/planes"` route.

`app/controllers/planes_controller.rb`

	class PlanesController < ApplicationController
		
		...
		
		def create
			redirect_to "/planes"
		end
		
	end

> Someone should now be able to submit a form to our site, right???

### A fatal flaw

It turns out that forms aren't so simple in Rails anymore. There are security concerns that rails is trying to handle from the very beginning. 

> Recall that we indicated that `PlanesController` inherits from `ApplicationController`, which looks like the following:

>		class ApplicationController < ActionController::Base
	 	 # Prevent CSRF attacks by raising an exception.
	 	 # For APIs, you may want to use :null_session instead.
	 	 protect_from_forgery with: :exception
		end
> The line that says
> 
> 		protect_from_forgery with: :exception
> means that our forms will have added layer of security. 


To even get our rails app to accept our form it needs an `authenticity_token`, which we will casually add in and explain later.

`app/views/planes/new.html.erb`

	<form action="/planes" method="post">
		<input type="text" name="plane[name]">
		<input type="text" name="plane[design]">
		<textarea name="plane[description]"></textarea>
		<%= token_tag form_authenticity_token %>
		
		<button> Save Plane </button>
	</form>

Our form should now submit properly. However, we will see that rails makes handling all the things required in a form easier using something called *form helpers* later.

### An operational create method

We just need to save the data being sent in the request. We might be tempted to do the following.

`app/controllers/planes_controller.rb`

	class PlanesController < ApplicationController
		
		...
		
		def create
			plane = params[:plane]
			Plane.create(plane)
			redirect_to "/planes"
		end
		
	end

However, while this might be fine in rails `3.2` it won't fly in rails `4.0`, which has something called **strong parameters**. To follow this strong parameters convention we must change the way we accept params to something like one of the following.

We can grab the `:plane` hash out of the `params` hash, and the tell it to permit the keys we want: `:name`, `:design`, and `:description`.

`app/controllers/planes_controller.rb`

	class PlanesController < ApplicationController
		
		...
		
		def create
			plane = params[:plane].permit(:name, :design, :description)
			Plane.create(plane)
			redirect_to "/planes"
		end
		
	end

or, (preferably) just say `.require(:plane)`


`app/controllers/planes_controller.rb`

	class PlanesController < ApplicationController
		
		...
		
		def create
			plane = params.require(:plane).permit(:name, :design, :description)
			Plane.create(plane)
			redirect_to "/planes"
		end
		
	end


In reality **strong params** is just a nice way of making sure someone isn't setting param values that you don't want them to be setting.


### Refactoring our Index

We first need to setup our `#index` method in `planes`

`app/controllers/planes_controller.rb`

	class PlanesController < ApplicationController
		
			def index
				@planes = Plane.all
				render :index
			end
		
		...
		
	end


Let's finally put some `erb` in our `index` view.

`app/views/index.html.erb`
	
	<% @planes.each do |plane| %>
		
		<div>
			Name: <%= plane.name %> <br>
			Type: <%= plane.design %> <br>
			Description: <%= plane.description %>
		</div>
	
	<% end %>

## Take Off

We've successfully made `index`, `new`, and `create` for our `planes` resource. Now we'll add `show`, `edit`, and `update`.

## Challenges, Part 1: Showing One Plane

Right now, our app redirects to `index` after creating a new plane, which isn't helpful for quickly verifying the data that was just created. To do this, we create a `show` page for one plane.

1. Verify that you have a `show` route. Our routes file looks like this:

  ```ruby
  #
  # routes.rb
  #

  Rails.application.routes.draw do
    root to: "planes#index"
    resources :planes, only: [:index, :new, :create]
  end
  ```
  
  Let's switch `resources :planes, only: [:index, :new, :create]` to just `resources :planes` and check out the full set of routes that Rails can make for us. We won't cover `DELETE` or `PATCH` routes in class today, so for now let's modify the resources line to say `resources :planes, except[:patch, :delete]`.

  Finally, in the terminal, run `rake routes`, and verify you still have a `show` route that looks like this: `GET  /planes/:id(.:format)  planes#show`.

2. Make a controller method to find the plane you want to show and render the `show` view.

  ```ruby
  #
  # app/controllers/planes_controller.rb
  #

  PlanesController < ApplicationController

    # GET /planes/:id
    def show
      # set id from url params
      plane_id = params[:id]

      # find plane in db by its id
      @plane = Plane.find(plane_id)

      # render show view
      render :show
    end

  end
  ```

3. You should already have at least one plane in your database. In the browser, go to `localhost:3000/planes/1`. What error do you see? What should you do next?

4. Create a `show` view! It should live in `app/views/planes`.

  ```html
  <!-- app/views/planes/show.html.erb -->
  <div>
    Name: <%= @plane.name %><br>
    Type: <%= @plane.design %><br>
    Description: <%= @plane.description %>
  </div>
  ```

5. Right now, our `create` method redirects to `index` (the `/planes` path), but this isn't very helpful for verifying that a newly created plane was properly created. The best way to fix this is to have it redirect to `show`.

  ```ruby
  #
  # app/controllers/planes_controller.rb
  #

  PlanesController < ApplicationController

    # POST /planes
    def create
      # new plane data from form
      plane_params = params.require(:plane).permit(:name, :design, :description)

      # create new plane in db
      plane = Plane.create(plane_params)

      # redirect to plane's show page
      redirect_to "/planes/#{plane.id}"
    end

  end
  ```

  Recall that the `show` method has a path `/planes/:id`, which means we need to specify the `id` of the plane we want to show. To do this, we used string interpolation to attach the id of the newly created plane to the URL.

## Challenges Part 2: Editing a Plane

Editing a `plane` requires two separate methods. One will display the `plane` information to be edited by the client, and the other will handle the update request.

If we look back at how we handled displaying our `new` form we see the following pattern:

* Make a route first
* Define a controller method
* Render the view

The only difference is that now we need to use the `id` of the object being edited. We get the following plan:

* Make a route first
  * Make sure it specifies the `id` of the thing to be **edited**
* Define a controller method
  * Retrieve the `id` of the plane to be **edited** from `params`
  * Use the `id` to find the specific plane we want to edit
* Render the view
  * Display the `plane` data in the form

1. Verify that you have an `edit` route by running `rake routes`. You should see: `GET  /planes/:id/edit(.:format) planes#edit`

2. Make a controller method to find the plane you want to edit and render the `edit` view (you can use your `show` method as inspiration).

  ```ruby
  #
  # app/controllers/planes_controller.rb
  #

  PlanesController < ApplicationController

    # GET /planes/:id/edit
    def edit
      # set id from url params

      # find plane in db by its id

      # render edit view
    end

  end
  ```

3. Create an `edit` view in `app/views/planes`. Our edit form looks almost identical to our new form. Adding `value="<%= @plane.attr_name %>"` to each form field displays the existing plane data in the form (good UX!).

  ```html
  <!-- app/views/planes/edit.html.erb -->
  <form action="/planes/<%= @plane.id %>" method="post">
    <%= token_tag form_authenticity_token %>
    <input type="text" name="plane[name]" placeholder="Name" value="<%= @plane.name %>">
    <input type="text" name="plane[design]" placeholder="Design" value="<%= @plane.design %>">
    <textarea name="plane[description]" placeholder="Description"><%= @plane.description %></textarea>
    <input type="submit" value="Update Plane">
  </form>
  ```

4. Next we have to modify the `action` and `method`, but we can't explicitly change the method in the `<form>` tag, because the browser still needs to send a `POST` request. Instead we add a hidden field that contains the method we actually want to make, `put`.

  ```html
  <!-- app/views/planes/edit.html.erb -->
  <form action="/planes/<%= @plane.id %>" method="post">
    <input name="_method" type="hidden" value="put">
    ...
  ```

## Challenges Part 3: Updating a Plane in the Database

If look back at how we handled submitting our `new` form we see the following pattern:

* Make a route first
* Define a controller method
* Redirect to something

The only difference is that now we need to use the `id` of the object being updated. We get the following plan:

* Make a route first
  * Make sure it specifies the `id` of the thing to be **updated**
* Define a controller method
  * Retrieve the `id` of the plane to be **updated** from `params`
  * Use the `id` to find the specific plane we want to update
  * Retrieve the updated info sent from the form `params`
  * Update the plane in the database
* Redirect to the plane's `show` page
  * Use the plane's `id` to redirect to `show`

1. Back to routing! Run `rake routes` and make sure you see: `PUT  /planes/:id(.:format) planes#update`

2. In `PlanesController`, create the `update` method

  ```ruby
  #
  # app/controllers/planes_controller.rb
  #

  PlanesController < ApplicationController

    # PUT /planes/:id
    def update
      # set id from url params

      # find plane in db by its id

      # updated plane data from form
      plane_params = params.require(:plane).permit(:name, :design, :description)

      # update the plane in db
      plane.update_attributes(plane_params)

      # redirect to plane's show page
    end

  end
  ```
  
## Refactor: `form_for`

Let's look back our edit form:

```html
<!--airplane_app/app/views/planes/edit.html.erb-->
 <!-- form to update plane -->
 <form action="/planes/<%= @plane.id %>" method="post">
   <%= token_tag form_authenticity_token %>
   <input type="hidden" name="_method" value="put">
   <div class="form-group">
     <input type="text" name="plane[name]" placeholder="Name" value="<%= @plane.name %>" class="form-control" autofocus>
   </div>
   <div class="form-group">
     <input type="text" name="plane[design]" placeholder="Design" value="<%= @plane.design %>" class="form-control">
   </div>
   <div class="form-group">
     <textarea name="plane[description]" placeholder="Description" class="form-control"><%= @plane.description %></textarea>
   </div>
   <input type="submit" value="Update Plane" class="btn btn-default">
 </form>
```


  
There's a lot going on here! We:
* specified a `method` and `action`
* used the `token_tag` form helper to help keep our form secure
* used an html trick to change the method to `put`
* used `name` attributes to name the parts of our request
* used `value` attributes to fill in the plane's stored information from the db
* created the basic form structure
* added bootstrap cdns to `airplane_app/app/views/layouts/application.html.erb` and used bootstrap classes in our form elements


Other than creating the form structure and adding bootstrap, Rails has a shortcut to help us do all of this: `form_for`. You specify the form structure using erb (ruby syntax). Rails looks at the form you write, plus the file name, and translates it into html. Here's our edit form refactored with `form_for`, minus the bootstrap styling:

```html
<!--airplane_app/app/views/planes/edit.html.erb-->
 <!-- form to update plane -->
<%= form_for @plane do |f| %>
  <%= f.label :name %>
  <%= f.text_field :name %><br />
 
  <%= f.label :design %>
  <%= f.text_field :design %><br />
  
  <%= f.label :description %>
  <%= f.textarea :description %><br />
  
  <%= f.submit "Update Plane" %>
<% end %>
```



## Stretch Challenges

1. Implement `delete` for your `planes` resource following the example of `edit` and `update`. Think about what you'll need:
  * a `delete` route (check `rake routes`)
  * a form on the client-side to make the `delete` request (**Hint:** This form doesn't need its own view. It may make sense to have a `delete` "form", which will essentially be a button, on the plane's show page.)
  * a controller method to handle the `delete` request

1. Refactor your `new` and `edit` forms to use `form_for`.

1. Implement full CRUD for another resource in your application. Pilots or passengers might make sense :)