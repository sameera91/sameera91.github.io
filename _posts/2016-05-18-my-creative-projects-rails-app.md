---
layout: post
title: My Creative Projects Rails App
---
My journey to learn to code has been an enjoyable one so far. From objected-oriented Ruby to Sinatra, I have learned a lot about programming. It’s amazing to see what a few lines of code can accomplish! I am currently exploring the Rails framework, and in the process, I have just completed my first [Ruby on Rails Application](https://github.com/sameera91/my-creative-projects){:target="_blank"}.

My Creative Projects is a rails app that allows users to keep track of any type of creative project, and has functionalities such as signing up for an account, logging in, creating a project, assigning categories, and adding comments to a project.

**Models and Migrations**

I created several models and migrations for this app: users, projects, categories, and comments to name a few. To appropriately set up these models, I had to determine their relationships such as the following: a user has many projects, a project has many categories, and a project has many comments.  I then created a join model/migration called project_categories to connect the projects and categories, since this is a many-to-many relationship. 

Here is an example of one of my models, the Project model:

![project model](/img/project_model.png)

I made sure to include as much of the logic as possible inside my model, and therefore included methods such as update_likes and top_projects. The method, update_likes simply increments the number of likes that the project has, once the like button is clicked. The trending_projects method shows all projects that have more than 10 likes. The categories_attributes method takes in a hash containing all the categories that were entered through the nested form, creates an object out of each category, and assigns it to the project’s list of categories.

One of the challenges I faced when creating these models was figuring out how to distinguish between two types of users: ones that created a project, and ones that commented on a project. I then figured that the best way to do this was through the addition of separate foreign keys for the two types of users (i.e. creator_id), and then adding the foreign keys and class name to the User and Project model. Here is an example: 

![user model](/img/user_model.png)

**Devise and OmniAuth**

An important part of the project was allowing users to create accounts and then logging in/logging out. There is a very handy Ruby gem that allows you to do this--the Devise gem. Devise is great for authentication, as it can send confirmation emails, send password resets, encrypts passwords, and automatically creates session variables once the user logs into their account. It even has a very handy way to generate the User model. Just run: rails generate devise User. Devise also contains modules such as validatable, which provides email and password validations.

OmniAuth is another useful gem that can work with Devise, and basically lets users sign in through external sources such as Github, Facebook, or Twitter. I chose to give the user the option of signing in through Facebook, which was a mostly straightforward process that involved registering the app on facebook, and setting up the environment variables. It was then easy to obtain the user’s email from facebook, but a challenge I faced was getting the user’s full name from their facebook account. After some research, I learned that all user data is stored in a hash called “info” and the name could be accessed using “auth.info.name.”

![omniauth](/img/omniauth.png)


**Other Gems**

In addition to Devise and OmniAuth, I came across another useful gem called Paperclip. This gem allowed me to easily include a way for the user to upload images to their project. Through the command, "rails generate paperclip project image", the gem added fields named file_name, file_size, and content_type to the projects migration. I was then able to include an input field for the image to the project form, and the image would be displayed in the project view. I was amazed by how easily this could be done using this gem!

**Nested Resources**

My project was set up such that users have many projects, projects have many comments, and other similar relationships. I had to have a way represent this neatly in the URL, and the best way to do that was through nested routes. This way, I could have a url that looked like this: /projects/2/comments/1. This made my URLs look nicer, but a slight challenge was to keep track of the many routes that came with it. For example, project_comment_path(project_id, comment_id). But in the end, I found that using these routes in my controllers was a good way to keep track of all the projects of a user for example, or all the comments of a project.


Overall, this was a fun project! I learned a lot about what is involved in building a Ruby application through the Rails framework. I couldn’t help but be amazed by the sheer amount of magic that rails contains, and how so many basic tasks are automated. In the future, I plan to publish my application, as well as add some additional functionality. An example of this is giving users the ability to search projects by entering in a category name.

