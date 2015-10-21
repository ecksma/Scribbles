
# Intro to Active Record, Validations, and Querying

## What is ActiveRecord?

Active Record is called an Object Relational Mapper (ORM) and makes it easy for you to interact with your database in Rails.


> [About Tech](http://ruby.about.com/od/rubyonrails/ss/What-Is-Activerecord.htm)

Active Record maps a database row to an object in Ruby. What this means in practice is that you use ActiveRecord to create or retrieve your data and use traditional Ruby methods and attribute assignments to interact with this data. Instead of composing a SQL query manually, filling in the search parameters, sending it off to a database API, running the query, examining and parsing the result and storing the result in either a hash or a database, you let ActiveRecord do all that for you.

For example, say the web application in question is the blog. You display the latest blog entry on the front page, so you need to retrieve that entry first. Using an SQL statement, you'd compose an SQL query something like ```SELECT * FROM posts ORDER BY date DESC LIMIT 1```. That's quite the mouthful for what you really want to say, which is "get me the latest blog post." Using ActiveRecord, that query now becomes something like ```p = Post.last```. That's it, ActiveRecord knows what you want, composes the SQL query for you, submits it, parses the output and puts in a handy Ruby object for you to use. You can now refer to the post's title with method calls like ```p.title```, assign to it using ```p.title = "A new title"``` and save it back to the database with ```p.save```.

###Would you rather...

| ActiveRecord | SQL |
| :-------------------- | :------- |
| User.all | `SELECT * from users` |
| User.find(123) | `SELECT * from users WHERE users.id = 123 LIMIT 1` |
| @user.posts | `SELECT * from posts WHERE posts.user_id = 123` |
| @student.courses | `SELECT * FROM courses INNER JOIN enrollments ON courses.id = enrollments.course_id 	WHERE enrollments.student_id = 456	` |

---

# Validations

> [Rails Guide](http://guides.rubyonrails.org/active_record_basics.html)

Active Record allows you to validate the state of a model before it gets written into the database. There are several methods that you can use to check your models and validate that an attribute value is not empty, is unique and not already in the database, follows a specific format and many more.

Validation is a very important issue to consider when persisting to the database, so the methods save and update take it into account when running: they return false when validation fails and they didn't actually perform any operation on the database. All of these have a bang counterpart (that is, ```save!``` and ```update!```), which are stricter in that they raise the exception ```ActiveRecord::RecordInvalid``` if validation fails. A quick example to illustrate:

```ruby
class User < ActiveRecord::Base
  validates :name, presence: true
end

@user = User.new
@user.save  # => false
@user.save! # => ActiveRecord::RecordInvalid: Validation failed: Name can't be blank
@user.errors # => returns an array of the errors
```

#Querying

> [Rails Guide](http://guides.rubyonrails.org/active_record_querying.html)

To retrieve objects from the database, Active Record provides several finder methods. Each finder method allows you to pass arguments into it to perform certain queries on your database without writing raw SQL.

The most important Active Record query method is `where` and it takes hash parameters or a string of raw SQL.

```ruby
Client.where(first_name: 'Lifo')
Client.where(locked: true)
Client.where("orders_count = ?", params[:orders])
Client.where("created_at >= :start_date AND created_at <= :end_date", {start_date: params[:start_date], end_date: params[:end_date]})
```

More advanced queries
```ruby
Client.where(created_at: (Time.now.midnight - 1.day)..Time.now.midnight)
SELECT * FROM clients WHERE (clients.created_at BETWEEN '2008-12-21 00:00:00' AND '2008-12-22 00:00:00')
```

## SQL injection attacks

> [Rails Guide](http://guides.rubyonrails.org/security.html#sql-injection)

SQL injection attacks aim at influencing database queries by manipulating web application parameters. A popular goal of SQL injection attacks is to bypass authorization. Another goal is to carry out data manipulation or reading arbitrary data. Here is an example of how not to use user input data in a query:

```ruby
Project.where("name = '#{params[:name]}'")
```

This could be in a search action and the user may enter a project's name that they want to find. If a malicious user enters ' OR 1 --, the resulting SQL query will be:

```console
SELECT * FROM projects WHERE name = '' OR 1 --'
```
The two dashes start a comment ignoring everything after it. So the query returns all records from the projects table including those blind to the user. This is because the condition is true for all records.

To avoid this, you can pass an array to sanitize tainted strings like this:

```ruby
Model.where("login = ? AND password = ?", entered_user_name, entered_password).first
```


## AciveRecord CRUD (in the Console) aka Get Ur Hands Dirrrrty

Open up your terminal and navigate to the root of a recent rails project.

### Create a ```User``` model

Create a new model in terminal.

`rails g model User first_name:string last_name:string age:integer`

Migrate the database to create the ```User``` table.

`rake db:migrate`

Open up the console by typing ```rails console``` or ```rails c```.

### Create
`User.create(first_name: "Abraham", last_name: "Lincoln")`
`User.create(first_name: "Abraham", last_name: "Maslow")`

NB: See all your users with `User.all`


### Update

Find - `user = User.find(1)` #the number '1' passed into the find method corresponds to the id of the user it will find
Set - `user.first_name = "Taco"`
Save - `user.save`

**or**

Find — `user = User.find(1)`
Update — `user.update_attributes(first_name: "Taco")`

### Delete

Find - `user = User.find(1)`
Destroy - `user.destroy`

### More Finding

`User.all` -> returns an array of allusers
`User.find_by_last_name('Lincoln')` -> replace last_name with any param in your model. This command returns only the first user that meets the criteria.
`User.where(first_name: 'Abraham')` -> returns an array of users that meet the criteria
`User.first` -> finds first user
`User.last` -> finds last user

### Order

`User.order('last_name ASC')`