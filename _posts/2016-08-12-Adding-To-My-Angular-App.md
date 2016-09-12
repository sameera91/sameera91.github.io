---
layout: post
title: Adding To My Angular App
---

After going through my Angular Assessment for Learn Verified, I was tasked with developing an additional feature for my project. When a user posts a review for a book or movie, other users then have the ability to rate that review as helpful or not helpful. I did this by creating two additional rails routes, and then displaying relevant data on the front-end using Angular. I faced a few errors along the way, but on the whole, developing this feature further contributed to my knowledge of both Rails and Angular.

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

The second route was add_rated_review_to_user in the users controller. When the user clicks "Yes" or "No", this controller takes that movie review and adds it to the user's list of reviews. By adding this marked review to the user's list of reviews, I can then use Angular to ensure that a user does not vote for a review more than once.

This is what the add_rated_review_to_user action looks like: 

def add_rated_review_to_user
    @movie_review = MovieReview.find(params["user"]["id"])
    @user = User.find(params[:rater_id])
    @user.rated_movie_reviews << @movie_review
    render :json => @user
end


**Angular Front-end**

On the front-end of my application, I have two links that the user can click on in response to whether this review was helpful: "Yes" or "No". When the user clicks on any one of these links, they are directed to the appropriate controller action. This is where either the helpful_count or unhelpful_count attribute is incremented, and the review count is updated on the backend.
