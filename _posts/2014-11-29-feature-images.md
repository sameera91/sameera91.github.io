---
layout: post
title: Sinatra Outdoor Activity Tracker
---
**Overview**

I have just finished creating another project using the Ruby language—an outdoor activity tracker using the Sinatra framework. 
With spring already here, and summer quickly approaching, I thought it would come in handy to have a way to log all of my outdoor 
activities and details about their locations. After all, nature has a lot to offer! 

Before I could dive into coding, I found that one of the most important tasks was planning out how to approach this project and the app’s 
different functionalities. After thinking about the setup, I decided that a user would be able to sign up for an account, login, and 
once logged in, would be able to add a location and location details to their list of locations. Once a location is added, the user can 
add an outdoor activity, log details about the activity (time, distance covered, thoughts, etc.), and choose which location from their 
added locations the activity takes place in. The user can also see what locations other users have visited, and the users that visited 
them.

**Models and Migrations**

Before coding, I had to set up some models and migrations. I had 4 different models—activity, location, user, and user_location. I decided on the following relationships: an activity belongs to a user and location, a location has many activities and users, and a user has many activities and locations. Since user and location have a many-to-many relationship, a join table would be required to associate them—and that’s where the user_location model comes in, with user_locations being the join table.

Here is what some of my models look like:  (Location and Activity):

![location model screenshot](/img/location.jpg)

![activity model screenshot](/img/activity.jpg)

As is shown in my code, the models inherit from ActiveRecord::Base. This makes ActiveRecord's methods available for the models to use, ensuring that objects are easily created and stored in the database.

I then set up tables according to the models I built—users, activities, locations, and user_locations were the tables. These tables had fields such as username and password for users, and time and distance for activities. It was important to run rake db:migrate in the process of creating these migrations.

Here are a couple of migrations (created for the users and locations table):

![users migration](/img/users_migration.jpg)

![locations migration](/img/locations_migration.jpg)

**Controllers**

The controller is where much of the work takes place. This is the part of the application that acts as a middleman between what’s going on in the backend (models/migrations) and what’s displayed to the screen (the views). Here, I had to set up different routes which correspond to different parts of the URL. The routes direct users to the URLs that allow them to perform the different CRUD (create, read, update, delete) actions for activities, locations, and users.

Here is a part of my activities controller:

![activities controller](/img/activities_controller.jpg)

**Views**

Views are what get rendered to the screen. I have a number of different erb files for each part of the application (activities, locations, users). Each erb file serves a different purpose. For example, the create_activity erb file has a form that allows the user to enter information about that activity. That information is passed back to the appropriate route in the controller, which then uses the information to create a new instance of the Activity class and adds that to the database. The activities.erb file then displays a list of all instances of that Activity class (aka all the rows of the activities table) by looping through the Activity class. An erb file called show_activity displays the individual details of each activity.

**Challenges**

Although building a Sinatra outdoor activity tracker was an enjoyable process, it was not without its challenges. One of the biggest challenges I faced was how to implement the many-to-many relationship between users and locations. I had two different lists of locations—the user’s personal list of locations, and a bigger master list that displays the locations that all users have visited. It was difficult to keep these lists synchronized. For example, when one user deletes a location from their personal list, I had to be sure not to delete it from the master list of locations if another user had it on their personal list. But if another user didn’t have it on their list, the application had to delete it from the master list.

It was also somewhat difficult to keep locations and activities synchronized, but this was more manageable, because of the belongs_to relationship. But I did have quite a few decisions to make. For example, when a user deletes a location from their list, should the app delete all activities at that location? Or should the activities still remain in the user's list? Ultimately, I decided that the former was the way to go. 

Another thing I had to consider was displaying messages to the user after they performed some action such as editing or deleting. I found that the most efficient way to do this was through the sinatra-flash gem. Using this gem, I could specify the messages I wanted the user to see and exactly where they should be placed.
 
Overall, this project was a great learning process and a way to experience much of what Sinatra has to offer. I did indeed discover that Sinatra makes the most essential tasks of creating a web application quite efficient. Next, I will go through a code review and improve upon my code!


