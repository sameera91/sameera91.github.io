---
layout: post
title: Adding To My Angular App
---

After going through my Angular Assessment for Learn Verified, I learned that one good way to refactor my code was to create different routes for different features of the app. For example, I refactored my code to create a new route for the bookmarking feature, with a controller action named bookmark. I revisited my project after this pairing session, and used this same concept to develop an additional feature for my application. When a user posts a review for a movie, other users now have the ability to rate that review as helpful or not helpful. I did this by creating two additional rails routes, and then displaying relevant data on the front-end using Angular. I faced a few errors along the way, but on the whole, developing this feature further contributed to my knowledge of both Rails and Angular, and I learned about a much more readable and efficient way to write my code.

**Rails Backend**

I started out by creating two different routes. The first route is called count_reviews in the movie reviews controller. When the user clicks either the "Yes" or "No" button, a function on the Angular front-end increments either the helpful count or unhelpful count and passes it to the rails controller, where the movie review is updated with those values.

This is what the count_reviews controller action looks like: 

```
def count_reviews
    @movie_review = MovieReview.find(params[:review_id])
    @movie_review.update(helpful_count: movie_review_params["helpful_count"], unhelpful_count: movie_review_params["unhelpful_count"])
    render :json => @movie_review
end
```

The second route was add_rated_review_to_user in the users controller. When the user clicks "Yes" or "No" in response to whether the review is helpful, this controller takes that movie review and adds it to the user's list of reviews. By adding this marked review to the user's list of reviews, I can use Angular to ensure that a user does not vote for a review more than once.

This is what the add_rated_review_to_user controller action looks like: 

```
def add_rated_review_to_user
    @movie_review = MovieReview.find(params["user"]["id"])
    @user = User.find(params[:rater_id])
    @user.rated_movie_reviews << @movie_review
    render :json => @user
end
```

Before I render the JSON template, I have to make sure that the data contains all the necessary attributes in the movie review JSON serializer file.

**Angular Front-end**

On the front-end of my application, there are two links that the user can click on in response to whether the review was helpful or not. Once the user clicks either "yes" or "no", the appropriate function in the controller is called. Inside this function, the count of either helpful ratings or unhelpful ratings is incremented for that review. A function in the service is then called to modify the JSON data on the rails backend to update the count.

This is what the function in the controller looks like to increment the count of helpful reviews: 

```
ctrl.helpfulReview = function(movie, review){
      review.helpful_count++;
      review.rater_id = currentUser.id;
      MoviesService.updateReviewCount(movie, review).then(function(response){
        ctrl.review = response;
      });

      MoviesService.updateUserRatedReviews(currentUser.id, review).then(function(response){
        location.reload();
      })
    }
```
I then use $http.post to modify the data on the backend.

**What I Learned**

Adding this additional feature allowed me to gain more familiarity with creating additional rails routes in addition to the general create, read, update, and delete routes. Although this process took some debugging at first, I saw that being able to separate various features out into different routes made my code much more readable.

