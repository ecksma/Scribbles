# Intro to Rails
<center>
<img src="http://www.nascenia.com/wp-content/uploads/2014/11/rubyrails.png" alt="Drawing" style="width: 500px;"/>
</center>

| Objectives |
|:--- |
| ... become familiar with Rails' use of naming conventions, generators, and gems |


> from [1.1 Rails Tutorial ](https://www.railstutorial.org/book/beginning)

## What is Rails and Why is It So Great?

Ruby on Rails (or just “Rails” for short) is a web development framework written in the Ruby programming language. Since its debut in 2004, Ruby on Rails has rapidly become one of the most powerful and popular tools for building dynamic web applications. Rails is used by companies as diverse as Airbnb, Basecamp, Disney, GitHub, Hulu, Kickstarter, Shopify, Twitter, and the Yellow Pages. There are also many web development shops that specialize in Rails, such as ENTP, thoughtbot, Pivotal Labs, Hashrocket, and HappyFunCorp, plus innumerable independent consultants, trainers, and contractors.

What makes Rails so great? First of all, Ruby on Rails is 100% open-source, available under the permissive MIT License, and as a result it also costs nothing to download or use. Rails also owes much of its success to its elegant and compact design; by exploiting the malleability of the underlying Ruby language, Rails effectively creates a [domain-specific language](https://en.wikipedia.org/wiki/Domain-specific_language) for writing web applications. As a result, many common web programming tasks—such as generating HTML, making data models, and routing URLs—are easy with Rails, and the resulting application code is concise and readable.

Rails also adapts rapidly to new developments in web technology and framework design. For example, Rails was one of the first frameworks to fully digest and implement the REST architectural style for structuring web applications (which we’ll be learning about throughout this tutorial). And when other frameworks develop successful new techniques, Rails creator David Heinemeier Hansson and the Rails core team don’t hesitate to incorporate their ideas. Perhaps the most dramatic example is the merger of Rails and Merb, a rival Ruby web framework, so that Rails now benefits from Merb’s modular design, stable API, and improved performance.

Finally, Rails benefits from an unusually enthusiastic and diverse community. The results include hundreds of open-source contributors, well-attended conferences, a huge number of gems (self-contained solutions to specific problems such as pagination and image upload), a rich variety of informative blogs, and a cornucopia of discussion forums and IRC channels. The large number of Rails programmers also makes it easier to handle the inevitable application errors: the “Google the error message” algorithm nearly always produces a relevant blog post or discussion-forum thread.

## Conventions

### Naming Conventions: Plurals & Caps

Example with resource "Photo"

| Type | File | Name |
|:--- |:--- |:--- |
| Model | photo.rb | ```Photo``` |
| Migration | 20130407005147_create_photos.rb | |
| SQL Table | | photos |
| Instance Variable | | ```@photo``` |
| Array of Instances | | ```@photos``` |
| Controller | photos_controller.rb | ```PhotosController``` |

### RESTful Routes

Rails is built on a very strong RESTful convention. It uses the names of a resource to derive the rest of the route, path, and file names that have to do with that resource.

| Rails Action | Path | HTTP Method | Controller#Action | Template |
|:--- |:--- |:--- |:--- |:--- |
| Index |'/photos' | GET | photos#index | photos/index.html.erb |
| Show | '/photos/:id' | GET | photos#show | photos/show.html.erb |
| New | '/photos/new' | GET | photos#new | photos/new.html.erb |
| Create |'/photos' | POST | photos#create | |
| Destroy |'/photos' | DELETE | photos#destroy | |
| Edit  |'/photos/:id' | GET | photos#edit | photos/edit.html.erb |
| Update |'/photos/:id' | PUT/PATCH | photos#update | | |

### Gems

Modules written in Ruby that extend rails are called "Gems". Visit [Ruby Toolbox](https://www.ruby-toolbox.com/) to see the most popular ones.

To install a new gem you add it to your ```Gemfile```

```ruby
gem 'paperclip' # for uploading images
```

and then use this terminal command:

```$ bundle install```

To install the new gem. If you don't have bundler installed globally on your computer, use this command first to install the gem.

```$ gem install bundler```

### Generators

```$ rails new ```

This creates a new rails project.

```$ rails generate model Post title:string body:text```

Generates the model and the database migration files for a rails model ```Post``` and adds two attributes: ```title``` with a type of string, and ```body``` with a type of text (accepts more than ~200 characters).

```$ rails generate controller Post index show new create```

Generates a rails controller ```posts_controller.rb``` file with whichever routes you pass as arguments. In this case ```index```, ```show```, ```new```, ```create```.