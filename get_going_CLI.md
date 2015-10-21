how_do_i_do_that_again...
=========================

A repo for every time you ask yourself, "How do I do that again...?"

=========================

## Simple front end project

1. `mkdir MY_APP`
2. `mkdir views && touch index.html`
2. `mkdir styles && touch style.css`
3. `mkdir scripts (or javascripts) && touch index.js`

## Node

1. `mkdir FOLDER_NAME`
2. `cd FOLDER_NAME`
3. `touch app.js`
4. `npm init`
5. `git init`
5. `touch .gitignore`
6. `echo "node_modules >> .gitignore"`
5. `npm install --save WHATEVER_MODULE_YOU_NEED`
6. `configure your app.js` 
- `var express = require("express")`
- `var app = express();`
- `app.get("/", function(req, res){ // do some stuff here })`
- `app.listen(3000)` 

## Rails

1. `rails new -TBd postgresql` 
- `-T` removes the test folder (if you choose to use rspec instead)
- `-B` skips the bundle install upon app generation (if you plan to immidiately add to your Gemfile this is a good choice)
- `-d ______` specifies the database you choose to work with (default is sqlite3)
2. `bundle` (or bundle install)
3. `rake db:create db:migrate`
4. Optionally:
- `rake db:seed`
- `rake db:rollback` 
5. `git init`
4. `rails s`

## Angular

1. Include angular either using the `angular-gem` or cdn `<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.2.15/angular.min.js"></script>`
2. In a JS file include 
`var myApp = angular.module('myApp', [])` remember the empty array is where your dependencies will go
3. Include in your HTML tag `<html ngApp = "myApp">`

## Rspec without Rails

1. rspec init

## Rspec with Rails

1. In your gemfile add

```
group :development, :test do
  gem 'rspec-rails', '~> 3.0'
end
```
2. `rails generate rspec:install`