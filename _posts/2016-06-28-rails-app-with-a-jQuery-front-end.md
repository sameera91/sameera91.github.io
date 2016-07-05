---
layout: post
title: Rails App With a jQuery Front End
---

A couple of blog posts ago, I covered the process of how I built my [Ruby on Rails application](https://github.com/sameera91/my-creative-projects){:target="_blank"}, which allows the user to create and keep track of creative projects. It was a lot of fun building this project using Rails, and I have recently improved upon this by implementing the front-end using jQuery and Ajax.

**The Process:**

In this project, I utilize a very useful gem called ActiveModel Serializer that allows me to take my JavaScript model objects such as Project or Comment and turn them into JSON data, the information from which can then be accessed by my application to be displayed to the user. By doing this, we have created an API, which is an interface that allows a developer to access data needed for their application, whether that data is internal or external to the application. In the model serializer, I can specify which attributes I want to place into the JSON object and thus which data I want to be able to access, and which attributes I want to leave out. In my Project serializer, I decided to include attributes such as title and short_blurb, and specify how Project is related to other models such as comments and categories.

![project serializer](/img/project-serializer.png)

We can then go into the controller and use respond_to to render the information as either an HTML show page, or a JSON object. The to_json method provided by the ActiveModel Serializer gem renders the object as JSON, as shown below. Here, I render the Project model as a JSON object, and comments as an array inside the Project JSON object.

![json format](/img/json-format.png)


Here is the JSON object of a created project: 

![json object](/img/json-object.png)

By parsing our model data into a JSON object, we avoid the need to create too many get requests to access the data. In fact, I can create just one get request to access all the data in my JSON object, as shown below: 

![comments](/img/comments.png)

![load data](/img/load-data.png)

When I click on “load comments”, this code loops through the data that is located in the comments array of the JSON object and displays the content and author of the comment. I have also used a get request to display the data on the projects index page when any individual project is clicked on. I have likewise done the same on the categories index page, displaying links to individual projects after clicking on the name of the category: 

![categories](/img/categories.png)

**Posting Data:**

The comments section is a vital part of any given project in this application, and therefore would be best shown directly on the project show page. The application could be even more user-friendly if the user could enter a comment directly on the show page, and upon clicking submit, could immediately see the comment on the page without a page refresh. Therefore, I implemented this functionality using jQuery and Ajax.

I started out by placing the comments form directly on the project show page. When the user enters the comment and hits submit, the JavaScript code is executed. I bound an event handler to the “submit” JavaScript event, and inside the event handler, I used the $.post function to return the newly created comment to “projects/”. I then specify what happens when the comment is posted, as shown in this function. 

![post data](/img/post-data.png)

**Challenges:** 

I enjoyed completing this project, partially because of the number of challenges I faced, all of which enabled me to learn a lot about JavaScript, jQuery, and Ajax. One of my main challenges was fully implementing the comment form functionality, with the correct comment showing on the page, in the correct location, and ensuring that the edit and delete links matched up to the correct comment. Initially, I had some trouble with the edit and delete links immediately upon hitting the submit button of the comments form. I found that the edit and delete links would actually direct me to the page of the previous comment, instead of that of the comment that was just posted. Initially, I placed the edit and delete links inside the Ruby code, but when I moved these links to the JavaScript code, I found that the problem was solved.

Overall, I learned a lot by completing this project, and now look forward to learning about Angular!

