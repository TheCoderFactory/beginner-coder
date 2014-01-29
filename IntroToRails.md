# Intro to Rails

## Our first Rails app

For your first app, you will build a personal resumé app. You will be able to update your app with your latest work education and work history, showcase your creative projects, display your contact information and perhaps even write blog posts.

There will be two main sections of the app. One where the public can see your information, and an admin panel where you can add/edit/delete information.

### Setting up your Rails environment

1. Check your version of Ruby 
In your terminal:
```
$ ruby -v
```

2. Use RVM to create a gemset.
```
$ rvm list
```

Copy the latest version of ruby and create a new gemset.

```
$ rvm use ruby-2.1.0@rails-402 --create
```

Install Rails
```
$ gem install rails --no-ri --no-rdoc
```

This will take a couple of minutes.

Now lets make this gemset the default
```
$ rvm use ruby-2.1.0@rails-402 --default
```

Now check your version of Rails
```
$ rails -v
```

Now we are ready to create a Rails app!


### Rails composer

We will use Rails Composer to give you a great starter app. This allows you to save time and just focus on the functionality you want to add.

In your browser, search for Rails Composer or [go here](http://railsapps.github.io/rails-composer/).

Copy the line `rails new myapp -m https://raw.github.com/RailsApps/rails-composer/master/composer.rb` (without the dollar sign).

And paste this into your terminal.

```
$ rails new myapp -m https://raw.github.com/RailsApps/rails-composer/master/composer.rb
```

This command creates a new rails app called 'myapp' and calls the Rails Composer script. This script asks us questions about the app we want to create and then creates it for us.

#### The answers to the big questions

1. 3 (Build my own application)
1. 2 (Thin)
1. 2 (Thin)
1. 1 (SQLite)
1. 1 (ERB)
1. 1 (Test::Unit)
1. 1 (None)
1. 1 (None)
1. 1 (None)
1. 4 (Twitter Bootstrap 4.0)
1. 2 (Gmail)
1. 2 (Devise)
1. 1 (Devise with default modules)
1. 2 (CanCan with Rolify)
1. 2 (Simpleform)
1. 4 (Home Page, User Accounts, Admin Dashboard)
1. n (Robots.txt file)
1. n (Github repository)
1. n (application.yml for Environment variables)
1. y (Reduce assets logger noise)
1. y (Improve error reporting)
1. n (Use or create a project specific gemset)

Now the scripts will run and create your app.

When it is finished, change into the myapp directory.
```
$ cd myapp
```

You can run your app.
```
rails server
```

Open your browser to `localhost:3000` to see your app.

You can sign up to be the first user of your app :)

### The code

Now let's look at the code and see how it works.

Open your project in sublime from the terminal.
```
$ subl .
```

You will see the file structure down the side. Open up the __app__ folder. The main folders you will use in here are:

1. assets > images/javascripts/stylesheets
1. controllers
1. models
1. views

Other important files:

1. config/routes.rb
1. db/migrate/*
1. Gemfile

### Adding your own functionality

Add the ability to add your contact information.

In your terminal, we will create a scaffold for your contact information.

```
rails generate scaffold ContactInfo first_name last_name address_1 address_2 suburb postcode country email phone linkedin twitter blog profile_pic
```

Hitting enter will trigger a script that creates a bunch of files that gives you instant functionality.

But before we can see any changes in our app, we need to tell our database about ContactInfo.

```
rake db:migrate
```

Now you can go to `localhost:3000/contact_infos` to see the index page of contact info. 

If you click on the Create Contact Info link, you will see your first error.

One of the great things about the SimpleForm gem we are using, we can also use a Country_Select gem that gives a list of countires.

In you gemfile, add `gem 'country_select'` before the `group :development` section.

Go to your terminal, stop your rails server with `Control-C`. When it has stopped, we will do a 'bundle' just by typing in `bundle` and hitting enter.

Once your bundling has finished, you can start the server again: `rails s`

Now try clicking on the Create Contact Info link.

You can see a form where you can enter your contact information. Do so, and while you're at it check out the Country chooser :)

Also for the profile pic, enter the exact name of an image that you have handy, and pop that image in your apps app > assets > images folder.

When you click on the Create Contact Info button, you will see a page where your info is displayed.

It's not very pretty yet. But we will do some cool things with this soon.

## Let's look at the code.

The files that were created by the scaffold generator are:
* models/contact_info.rb
* controllers/contact_infos_controller.rb
* views/contact_infos/_form.html.erb
* views/contact_infos/index.html.erb
* views/contact_infos/edit.html.erb
* views/contact_infos/new.html.erb
* views/contact_infos/show.html.erb

We also have the following files already created by Rails Composer
* controllers/home_controller.rb
* views/home/index.html.erb

















## Databases

Databases are almost always used in web applications. They are used to store and manage data.

What are the names of some popular databases?

What does a database help us do in general terms?

- persistent data
- define data structures
- CRUD
- backup data

What type of data would be stored in the database of a web application like Facebook?

What is meant by a "relational" database?

How is the data organised in a relational database?

- Tables, columns, tuples (rows).

Data structure - relationships between the data.

[SQL](http://www.w3schools.com/sql/)

Primary keys & Foreign keys

## Application Design

One of the first steps when starting to build an application, is to think about all the different parts of the application and how it will work.

What is the problem the application is trying to solve? What are the goals of this application/website?

Who is the audience of the application? Name all the different types of users who will use your site.

How will a user interact with the application? What are the use cases?

What data needs to be stored for the application to work?

How will the application look? What image are you trying to portray/what feeling do you want to give users.