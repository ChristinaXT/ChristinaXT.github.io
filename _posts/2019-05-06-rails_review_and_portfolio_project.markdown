---
layout: post
title:      "Rails Review and Portfolio Project "
date:       2019-05-06 15:20:38 -0400
permalink:  rails_review_and_portfolio_project
---



I wanted to write a review of the entire Rails curriculum to 1) Review for myself to prepare for the Portfolio assessment, and 2) to make sure I understand all of the rails concepts before moving on.  <br>

**Ruby on Rails** is a web development framework that helps developers create code more efficiently. Like other frameworks, rails is a collection of code libraries that allow developers to save time by utilizing ready solutions and structures instead of writing all the code from scratch. <br>

The **MVC Framework** continues in rails, however, now we can **generate** the files with “rails generate (name of generator) controller (options) users --no-test-framework”, for example. This nifty little generate command makes building out your framework much easier. This is probably one of my favorite things about rails. <br>

**Different types of generators**
* Migrations
* Models
* Controllers
* Resources

Using Rails developing techniques such as “**DRY - Don’t Repeat Yourself** “and “**Convention Over Configuration**” (default set of conventions used in rails) allows developers to keep their overall work cleaner and less prone to unneeded, repetitive code and errors and bugs and allows for trouble shooting to be much easier. 

**klass** - is commonly used to name a variable that holds a Class object (remember classes are objects too), as in klass = String .


I copied and pasted this rails file structure overview from the Flatiron rails intro just because it is perfectly written for review:<br>

**app** – contains the models, views, and controllers, along with the the rest of the core functionality of the application. This is the one directory where you can make a change and not have to restart the Rails server. The majority of your time will be spent working in this directory. In addition to the full MVC structure, this directory also contains non Ruby files, such as: css files, javascripts, images, fonts, etc. <br>
**bin** – some built-in Rails tasks that you most likely will never have to work with.<br>
**config** – the config directory manages a number of settings that control the default behavior, including: the environment settings, a set of modules that are initialized when the application starts, the ability to set language values, the application settings, the database settings, the application routes, and lastly the secret key base.<br>
**database (db)** – within the db directory you will find the database schema file that lists the database tables, their columns, and each column’s associated data type. The db directory also contains the seeds.rb file, which lets you create some data that can be utilized in the application. This is a great way to quickly integrate data in the application without having to manually add records through a web form element. The schema file can be found at db/schema.rb.<br>
**lib** – while many developers could build full applications without ever entering the lib directory, you will discover that it can be incredibly helpful. The lib/tasks directory is where custom rake tasks are created. You have already used a built-in rake task when you ran the database creation and migration tasks; however, creating custom rake tasks can be very helpful and sometimes necessary. For example, a custom rake task that runs in the background, making calls to an external API and syncing the returned data into the application’s database.<br>
**log** – within the log directory you will discover the application logs. This can be helpful for debugging purposes, but for a production application it's often better to use an outside service since they can offer more advanced services like querying and alerts<br>
**public** – this directory contains some of the custom error pages, such as 404 errors, along with the robots.txt file which will let developers control how search engines index the application on the web.<br>
**test** – by default Rails will install the test suite in this directory. This is where all of your specs, factories, test helpers, and test configuration files can be found. Side note: We always use RSpec, which means this directory will actually be called spec.<br>
**tmp** – this is where the temporary items are stored and is rarely accessed by developers<br>
**vendor** – this directory has been utilized for varying purposes in the past. In Rails 4+, its main purpose is for integrating Client-side MVC frameworks, such as AngularJS.<br>
**Gemfile** – the Gemfile contains all of the gems that are included in the application; this is where you will place outside libraries that are utilized in the application. After any change to the Gemfile, you will need to run bundle. This will call in all of the code dependencies in the application. The Gem process can seem like a mystery to new developers, but it is important to realize that the Gems that are brought into an application are simply Ruby files that help extend the functionality of the app.<br>
**Gemfile.lock** – this file should not be edited. It displays all of the dependencies that each of the Gems contain along with their associated versions. Messing around with the lock file can lead to application bugs due to missing or altered Gem dependencies.<br>
**README.rdoc** – the readme file is an important place to document the details of the application. If the application is an open-source project, this is where you can place instructions to other developers, such as how to get the app up and running locally.<br><br>

**MVC** stands for Model, View, and Controller.<br>

<a href="https://imgur.com/bG8Vulv"><img src="https://i.imgur.com/bG8Vulv.png" title="source: imgur.com" /></a>

**Model** - The model maintains a relationship with the database and will represent a database table. The model is essentially a Ruby class and has capabilities inherited from Active Record to manipulate data from the database table. Model objects are used as a layer between the application and database. The model can also create validations and associations between models. <br>

**View** - The views are presentations of data and are triggered by the controller’s to present the data. Views are styled usually using HTML, CSS and JS, but can implement other styles as well. <br>

**Controller** - The controller directs the traffic and organizes the data. It controls the flow of traffic and makes decisions about which format you will use to present the data. <br>

<a href="https://imgur.com/rppVNBd"><img src="https://i.imgur.com/rppVNBd.png" title="source: imgur.com" /></a>

From Flatiron :

At its core, MVC is designed to modularize distinct functionality within an application. While the MVC pattern can be used with many different types of applications, let's identify its distinct parts in the context of a web application:
**View**: what an end user on a website experiences when interacting with a program in their browser: what they read, what they click, what flashes at them, and what they hear (despite the name "view"). In technology-speak, the vocabulary word would be interface<br>
 **Model**: where the actual data, (be it information about restaurants, train times, or rare marsupials), resides and is altered<br>
 **Controller**: what manages communication between the two: it takes model information and prepares it for the view and vice versa<br>
Now that we have identified the core components, let's examine what they actually do when a user engages with our web application:<br>
 A **user**, through interaction with the view, (in this case, the browser's GUI), requests data (clicks on a link, submits a form, enters a URL in the browser's bar<br>
The **request** is sent across the internet to the server<br>
The **controller** (which does not change data itself!) asks the model to either provide it data (which it will send) or to change model-held data depending on the user's request<br>
The **model** accesses/manipulates the actual 1's and 0's held on the server's database and returns the desired result to the controller<br>
The **controller** packs the response and sends it back to the client<br>
The **view** (on the originating client's machine) presents the data for the user<br>


I found this amazing rails glossary.   <a href="http://docs.railsbridge.org/intro-to-rails/glossary">here</a> <br>

Some of the command line terms that are most helpful in rails include :<br>

**puts** something Prints its argument to the console. Can be used in Rails apps to print something in the console where the server is running.<br>
**rails new** NameApp Creates a new Rails application with the entire Rails directory structure to run your application.<br>
**rails server** (or rails s) Launches a web server named Puma that you will use any time you want to access your application through a web browser.<br>
**rails generate** (or rails g) Uses templates to create a bunch of directories and files in your application.<br>
**rake Rake** is ‘Ruby Make', used to build up a list of tasks.<br>
**rails console** (or rails c) Lets you interact with your Rails application from the command line, useful for testing out quick ideas with code and changing data server-side without touching the website.<br>
**rails dbconsole** (or rails db) Used to figure out which database you're using and drops you into whichever command line interface you would use with. It supports MySQL, PostgreSQL, SQLite and SQLite3.<br>
**rails destroy** (or rails d) Does the opposite of generate. It will figure out what generate did and undo it.<br>

(From Flatiron’s curriculum) : <br>
**Explicit rendering** - for explicit rendering, Rails lets you dictate which view file you want to have the controller action mapped to.<br>
**Implicit rendering** - for implicit rendering, Rails follows a standard convention that automatically looks for the view file with the same name as the controller action.<br>
**Routing**
How does your application know what view to render to users? This is where routing comes in. As a framework, Rails has a comprehensive routing system for both dynamic and static pages. Below are the differences between a static and dynamic route:<br>
**Static route** - A static route will render a view that does not change. Typically, you will not send parameters to it. Examples would be a site's about or contact pages.<br>
**Dynamic route** - Dynamic routes are pages that accept parameters and render different content based on those parameters. An example would be a blog's post page that contains a specific article.<br>

I found this page with really great HTTP verbs and methods for RESTful routes
<a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods">here</a>

And this page for rails routing :
<a href="https://guides.rubyonrails.org/v5.2/routing.html">here</a>

In Rails, a RESTful route provides a mapping between HTTP verbs, controller actions, and (implicitly) CRUD operations in a database.
 <a href="https://guides.rubyonrails.org/v2.3.11/routing.html">here</a>

From Flatiron : 
<br>
Below are a few keys to remember when thinking about REST:
**REST** is an architectural design pattern, not a framework or code in itself. Many other web frameworks utilize RESTful design principles in some form or another. By using RESTful principles, Rails apps are able to have a clear and standardized naming structure for routes and actions<br>
**RESTful routes** have a clear mapping between the URL resource and the corresponding controller actions.<br>
There are seven potential RESTful route options available.<br>

Recap of form_tag<br>
To review, the **form_tag helper method** allows us to automatically generate HTML form code and integrate data to both auto fill the values as well as have the form submit data that the controller can use to either create or update a record in the database. It allows for you to pass in: the route for where the parameters for the form will be sent, the HTTP method that the form will utilize, and the attributes for each field.<br>

A good rule of thumb for when to use one approach over the other is below:
Use **form_for** when your form is directly connected to a model. Extending our example from the introduction, this would be our Hamster's profile edit form that connects to the profile database table. This is the most common case when form_for is used<br>
Use **form_tag** when you simply need an HTML form generated. Examples of this would be: a search form field or a contact form<br>




-------------------------------------------------------

Now, that we have reviewed some, I want to talk a bit about my rails portfolio project.

I took the suggested task generator idea and instead, decided to create a party planning app. I called it the BabyGuide for generating ideas and requests from individuals and a group to create a birthday party for a baby or child. The app works for any group party planner, however, and doesn't have to only relate to children's parties. It would work perfectly for a group of friends who wish to plan a bachelorette party, or surprise party or highschool reunion. It could also be a great app for families planning anniversary parties or family reunions. The idea is that a person can be the admin and create a checklist with party planning requests. Then he or she can invite his/her friends and family to create accounts and accept requests and also to create their own party plans and requests. Then each person can update the request status to say that it is finished. Some checklist examples include: Food menu, decorations, gift ideas etc. Then the checklist of food menu, for example, has a list of requests of food items: burgers, buns, hotdogs, salad, drinks, cups, etc. Each of those requests are then assigned to individuals who can choose to accept them or not. Once they are accepted, they can be updated saying that item is finished. 

You can see a walkthrough of my project on youtube : <a href="https://www.youtube.com/watch?v=NElvtYR_eBY&t=38s">here</a>

You can also view my git repo: <a href="https://github.com/ChristinaXT/BabyGuide">here</a>


