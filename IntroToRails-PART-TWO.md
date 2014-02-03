# PART 2

Last class you started building your own personal resume app. This class will help you add your work history and deploy it to the web.



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


## Adding a new data model/object

Now we will add your work history to the app.

In your terminal, generate another scaffold.
```
rails generate scaffold Job company start_date:date end_date:date position summary:text
```

Then also in your terminal:
```
rake db:migrate
rails s
```

Make sure neither command gives you errors.

In your browser, add a couple of jobs to your app.
```
localhost:3000/jobs
```

Now we will show them on the home page.

In Sublime, navigate to */app/controllers/home_controller.rb* and add the following line of code into your index method:

```
@jobs = Job.all
```

Your controller will now look like this:
```
class HomeController < ApplicationController
  def index
    @contact_info = ContactInfo.first
    @jobs = Job.all
  end
end
```

Now you can list your jobs on the home page.

At the bottom of */app/views/home/index.html.erb* we will add a loop which will display each of the jobs:

```
<% if @jobs %>
	<h2>Work history</h2>
	<% @jobs.each do |job| %>
		<div class="panel panel-default">
			<div class="panel-heading">
				<p class="panel-title"><%= job.position %> at <%= job.company %></p>
			</div>
			<div class="panel-body">
				<p><strong><%= job.start_date %> to <%= job.end_date %></strong></p>
				<p><%= job.summary %></p>
			</div>
		</div>
	<% end %>
<% end %>
```


If you refresh your Home page [localhost:3000/](localhost:3000/), you will see the jobs you entered in the form.



## CHALLENGE

Now do the same for References. Use the process you used for creating jobs and do the same for references.




## Deploying to the web

### Heroku

Heroku is a PaaS (Platform as a Service) business that allows you to deploy (upload and run) your Rails app to the web.

To use it, first sign up on the [Heroku site](https://heroku.com).

Then download and install the [Heroku toolbelt](https://toolbelt.heroku.com/).

In your terminal, log in to Heroku.
```
heroku login
```

When prompted, enter your email and password (remember your password won't display to the screen as you type).

### Now you need to prepare your app.

Go to your *Gemfile*

Find the line `gem 'sqlite'` and move it to within the `group :development` section.

Then create a `group :production` section and enter the gems: *pg* and *rails_12factor*

It should look like this:

```
group :production do
	gem 'pg'
	gem 'rails_12factor'
end
```

Save your Gemfile and in your terminal, run `bundle`.

Now we use git to send your app to Heroku.

Perform the following commands:
```
git init
git add .
git commit -am 'initial commit'
```

Create the Heroku app with the following:

```
heroku create <your_name>-resume-app
```

Now push your app to heroku:
```
git push heroku master
```

If that completes without errors, you can rake your migration:
```
heroku run rake db:migrate
```

You should now be able to see your site at `<your_name>-resume-app.herokuapp.com`







