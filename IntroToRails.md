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

In your terminal navigate to your apps folder (or folder where you want your apps to live).

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
1. 1 (None)
1. 2 (Simpleform)
1. 4 (Home Page, User Accounts, Admin Dashboard)
1. n (Robots.txt file)
1. n (Github repository)
1. 1 (none)
1. y (Reduce assets logger noise)
1. y (Improve error reporting)
1. n (Use or create a project specific gemset)

Now the scripts will run and create your app.

When it is finished, change into the myapp directory.
```
$ cd myapp
```

Run bundle ie. `$ bundle`

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

## The Rails console

We will now have a look at our app through the terminal - as opposed to through the browser.

From your terminal type (either stop your server, or open a new tab: Cmd+T) `rails console`

This will bring up an interface to your app.

If you type `User.all` you will see a print out of all the users, which at the moment is just the user you created when you signed up in your app.

To see just the first user, type `User.first`.

When you type `ContactInfo.first`, you will see the contact info you just entered.

To see the first name, type `ContactInfo.first.first_name`.

This gives you an insight on how we access the data in our app.

Exit the console by typing `exit`.

## Bringing data to your home page

To have your contact info show on the home page of your app, we need to make it available through the home controller.

In your text editor (Sublime), navigate to `app/controllers/home_controller.rb`

You will see an index method, it will look like this:

````
class HomeController < ApplicationController
  def index
    @users = User.all
  end
end
````

This would make all users available to be shown on the home index page. Since we want our contact info, we change the method like so:
````
class HomeController < ApplicationController
  def index
    @contact_info = ContactInfo.first
  end
end
````

Now we can go to the `views/home/index.html` and bring our data in.

```
<h1><%= @contact_info.first_name %> <%= @contact_info.last_name %>'s Contact Info</h1>

<p><strong>Call me:</strong> <%= @contact_info.phone %></p>

<p><strong>Email me:</strong> <%= @contact_info.email %></p>

<p><strong>Follow me:</strong> <%= link_to @contact_info.twitter, 'https://twitter.com/' + @contact_info.twitter, class: 'btn btn-success' %></p>

<%= image_tag @contact_info.profile_pic, width: '200px' %>

<% if user_signed_in? %>
	<%= link_to "Edit my info", edit_contact_info_path(@contact_info) %>
<% end %>
```








