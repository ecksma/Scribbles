
# Auth in Rails

## Authentication Review

**Authentication** is the process of verifying a user's credentials to prove they are who they say they are. This is different than **authorization**, enabling or disabling access to specific resources.

To authenticate our users we typically ask them for a **password** we can associate to their `email`. A password is a very private piece of information that must be kept secret, and so, we strategically obscure in such a way that *one can only confirm a user is authentic and never uncover what their actual password*.

Our library of choice for password obfuscation is called `BCrypt`. This will be added to our gemfile for authentication setup later. In Rails, the convention is to push more logic into our models, so it shouldn't come as a surprise that authentication setup will happen in the **user model.**

## Creating a Secure Password

We can "roll-our-own" authentication system with BCrypt by adding instance and class methods to our `User` model. The methods below handle creating a user with a secure password and authenticating a user:

```ruby
#
# app/models/user.rb
#
class User < ActiveRecord::Base
  BCrypt::Engine.cost = 12

  validates :email, :password_digest, presence: true
  validates_confirmation_of :password

  def authenticate(unencrypted_password)
    secure_password = BCrypt::Password.new(self.password_digest)
    if secure_password == unencrypted_password
      self
    else
      false
    end
  end

  def password=(unencrypted_password)
    #raise scope of password to instance
    @password = unencrypted_password
    self.password_digest = BCrypt::Password.create(@password)
  end

  def password
    #get password, equivalent to `attr_reader :password`
    @password
  end

  def self.confirm(email_param, password_param)
    user = User.find_by_email(email_param)
    user.authenticate(password_param)
  end

end
```

Rather than rolling our own auth, we can take a more concise, "rails-y" approach with <a href="" target="_blank">`has_secure_password`</a>, which adds authentication methods for us.

## Sessions

> From [Rails Guides - Sessions](http://guides.rubyonrails.org/security.html#what-are-sessions-questionmark)

> HTTP is a stateless protocol. Sessions make it stateful.

Most applications need to keep track of certain state of a particular user. This could be the contents of a shopping basket or the user id of the currently logged in user. Without the idea of sessions, the user would have to identify, and probably authenticate, on every request. Rails will create a new session automatically if a new user accesses the application. It will load an existing session if the user has already used the application.

A session usually consists of a hash of values and a session id, usually a 32-character string, to identify the hash. Every cookie sent to the client's browser includes the session id. And the other way round: the browser will send it to the server on every request from the client. In Rails you can save and retrieve values using the session method:

```ruby
session[:user_id] = @current_user.id
User.find(session[:user_id])
```

## RESTful routes for Auth

Even when we are doing authentication we need to be RESTful. For signing up we'll be doing `users#create` and for logging in we'll call `sessions#create`. We are going to manage logging in from a `sessions_controller.rb` with `:new` (login page), `:create` (create a session), and `:delete` (logout) actions.

```ruby
#
# config/routes.rb
#
  resources :users, only: [:new, :create, :destroy]
  resources :sessions, only: [:new, :create, :destroy]
```

```ruby
#
#  app/controllers/sessions_controller.rb
#

class SessionsController < ApplicationController
  def new
    # Renders the sessions/new.html.erb template
  end

  def create
    #pass in array that user_params returns as arguments using a splat
    user = User.confirm(params[:email], params[:password])
    if user
      #this creates the session, logging in the user
      session[:user_id] = user.id
      #redirect to the show page
      redirect_to user_path(user.id)
    else
      #there was an error logging the user in
      redirect_to new_session_path
    end
  end

  def destroy
    session[:user_id] = nil
    redirect_to root_path
  end

end

```

## Current User

If you want an `@current_user` method to be available in all your controllers and views, then you'll want to define an application level helper method that looks up the user from the `session[:user_id]` if it exists.

```ruby
#
#  app/controllers/sessions_controller.rb
#

class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception

  def current_user
    @current_user ||= session[:user_id] && User.find_by_id(session[:user_id])
  end

  helper_method :current_user #make it available in views
end

```
You can use this `@current_user` object to do a lot

* Authorization - `@current_user.present?` means the user is logged in.
* User Profile - `user_path(@current_user)` will be the path to the current user's profile