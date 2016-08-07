---
layout: post
title: Angular Application With Rails Backend
---

I have completed my final project for Learn Verified! The requirements for this project included creating an application with an Angular front-end and a Rails backend, and I have chosen to build an application that gathers the current most popular books and movies and allows users to post reviews, and bookmark specific books/movies. This was an enjoyable application to build, especially because I had to initially figure out exactly how to connect Rails and Angular. Getting two different languages to work together was challenging at first, but with the help of certain rails gems and angular modules it became much more feasible to have them work together. An important one was angular-rails-templates, a gem that allows you to use Angular HTML templates with the Rails Asset pipeline. 

**Rails Backend**

I started out by trying to figure out which models I wanted to include in my application, and I decided on 5 different models: books, movies, book reviews, movie reviews, and the user model. I obtained the most popular books and movies using two NY Times APIs: The Books API and the Movie Reviews API. I could do this on the rails backend by using another very handy gem called httparty. For example, this is what the get_movies method in my movie model looks like as it gathers the top movies from the API: 

```
def self.get_movies
    response = HTTParty.get("http://api.nytimes.com/svc/movies/v2/reviews/all.json?api-key=#{ENV["API_KEY"]}")
    response["results"].first(20).each do |movie|
      new_movie = self.find_or_create_by(display_title: movie["display_title"], mpaa_rating: movie["mpaa_rating"], critics_pick: movie["critics_pick"], byline: movie["byline"], headline: movie["headline"], summary_short: movie["summary_short"], opening_date: movie["opening_date"], image: movie["multimedia"]["src"]) 
    end
end
```
First, we have to make sure that we have a migration file that creates a movies table with the desired attributes, and then we can pull information from the API to save it to the table. This model saves the first 20 movies to the database. We can then create a JSON object containing a list of all the movies using that data, and for this we must use the ActiveModel Serializer gem. In our serializer file, we can specify exactly which attributes we want to include in our JSON object. In our controller, we then tell our application that we wish for the data to be displayed as JSON, and we then get a very handy JSON object with all of our movie information. This object contains attributes such as the title, summary, mpaa rating, and the opening date. I have done the same with the Books API, saving information such as title, author, and description to the database.

**Angular Frontend**

Displaying Books and Movies:

We can now use Angular to gather data from our JSON object and display it to the user. I start out by placing a number of routes in the main application file, which specifies the name of the module and any dependencies it has. Angular allows us to use something called services, which can contain anything from a function to an object and allow us to share code across different parts of the app. In my app, if I want to see a list of the latest NY Times Bestsellers, I can create a function inside the service that returns a get request to the JSON object. This is as shown below: 

I can then go back to the controller, call the function in this service, and in the template, I can use an angular directive called ng-repeat to loop through the JSON data and display the list of books.

Posting Reviews:

Another part of my application was allowing the user to post reviews. I started out by creating user accounts using the devise gem. Each book in the list of books has a show page that takes the user to that individual book, and this is where the review form goes. Once the user clicks submit, the submitReview function in the controller processes the data in that form. We can use the ng-submit directive in the form to direct the user to the submitReview function. It creates a JSON object out of the data, and through the service, and creates a post request.

```
ctrl.submitReview = function(){
    var review = {book_id: $stateParams.id, content: ctrl.reviewContent, rating: ctrl.reviewRating, user_id: currentUser.id};
    BooksService.postBookReview(review, $stateParams.id).then(function(response) {
      ctrl.data.value.data.book_reviews.push(review)
    })
}
```

```
this.postBookReview = function(review, id){
    return $http.post("/books/" + id + "/book_reviews", review);
}
```

**Challenges**

One of my biggest challenges was in the initial stages of this project when I had to figure out how Angular and Rails work together. Once I overcame this hurdle with the help of several rails gems, the next step began figuring out how I can use angular to pull the JSON data from the server. I faced some challenges with this as my controller would return a promise, and I had to figure out where in the object the data was located. At first, I could not seem to find the data but then I figured out which variables to use in the controller, and which variables to use in the template. When creating get and post requests to the JSON backend, I also had to remember to create the appropriate routes in the rails controller. 

Overall, this was a fun project, and I plan to improve upon it in the future. Currently, users can add new books and movies to the list. One of the changes I plan to make is ensuring that only users who created a book or movie are the only ones who can modify that book or movie. In other words, I plan to implement permissions by using devise roles or pundit. I also plan to add unit tests to my application.

Through building this project, I have been able to see how powerful Angular is, and how tasks such as filtering, creating ajax requests, and sharing code across the app are all made much simpler. I look forward to building more apps using Angular and other front-end frameworks in the future.
