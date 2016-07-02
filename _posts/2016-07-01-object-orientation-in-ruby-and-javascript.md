---
layout: post
title: Object Orientation in Ruby and JavaScript
---

Objects are an essential part of a programming language, and in order to write complex programs, it is helpful to be able to create objects and have them interact with each other. Object orientation is a vital concept, and so I thought I’d go back and write about how classes and objects truly work. So far, I’ve been working quite a bit with JavaScript and creating objects based on a prototype. For example, if we have a prototype of a book with a variety of properties such as title, author, genre, and number of pages, we can create book objects based on this prototype. Examples include specific books such as Great Expectations, The Great Gatsby and Pride and Prejudice.

We can use a constructor function to define this prototype. The constructor function defines the different properties of the prototype.

```
function Book(title, author, genre, num_pages) {
 this.title = title;
 this.author = author;
 this.genre = genre;
 this.num_pages = num_pages;
}
```

In this constructor, we pass in a number of values, and set the properties of that particular object (as specified by the “this” keyword) equal to the values we passed in. 

We can then create a new instance of the constructor as follows: 

`var harry_potter = new Book(“harry potter”, “JK Rowling”, “fantasy”, 500);`

Prior to learning about JavaScript objects, I learned about object orientation in Ruby. It became essential to understand how objects can relate to one another. For example, a user has to be able to interact with their tweets, or other users. In other words, a tweet has one user, and a user has many tweets. Therefore, we need a way to attach a user object to a tweet. In this blog post, I’d like to go back and reiterate some important concepts of object relationships in Ruby.

```
class User
 
 attr_accessor :name, :email
 
 def initialize(name, email)
   @name = name
   @email = email
 end
 
end

```

In Ruby, we can create classes with instance variables through the initialize method. This is similar to the constructor method in JavaScript. The attr_accessor property allows us to access these instance variables. In this case, we have a User class, but if we have another class named Tweet, how do we associate them? Let’s say we want to set the tweet’s user. We can create a :user variable inside the Tweet class.

```
class Tweet
  attr_accessor :name, :content, :user
 
  def initialize(name, content)
    @name = name
    @content = content
  end 
end

```

We can create new instances of both the Tweet and User classes, and then set the user property of the tweet equal to the new User object. Now that new_tweet is a new Tweet object, we can access all the properties of the Tweet class such as name and content. new_tweet.user returns the object bob. And just like that, the tweet now has a user, through the association that we made.

```
new_tweet = Tweet.new("New Tweet", "content")

bob = User.new("bob")
 
new_tweet.user = bob

```

We can also create the relationship of a user has many tweets, by adding to the User class. We can create an array that holds a list of tweets inside of the User initialize class, and then create a method that adds new tweets to a user. In the add_tweet method, we can create a new tweet object, and add it to the tweets array. We can then set the user property of this new tweet to the current User object.  

```
class User
 
  attr_accessor :name, :email
   
  def initialize(name, email)
    @name = name
    @email = email
    @tweets = []
  end
 
  def add_tweet(name, content)
    tweet = Tweet.new(name, genre)
    @tweets << tweet
    tweet.user = self
  end
      
  def tweets 
    @tweets
  end
 
end

```

As we have seen, object-orientation makes it easier for us to group a number of things with similar properties by creating classes. It also allows us to effectively associate objects with one another, depending on their relationship (belongs to and has many).

I now look forward to continuing to learn about Angular, and will update my blog as I continue to learn! 