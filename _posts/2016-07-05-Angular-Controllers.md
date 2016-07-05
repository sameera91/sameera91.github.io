---
layout: post
title: Angular Controllers
---

I’m in the process of learning the concepts of Angular, and I’m beginning to see what a powerful framework this really is! There are so many tasks done in JavaScript that are made much more efficient through the use of a framework such as this one. I found that much like Rails, Angular follows a very similar MVC pattern, and it was important for me to learn about how the model, view, and controller in an Angular application work together. In addition to MVC, Angular has something else called MVVM (model-view-viewmodel), which makes use of helpers to perform the tasks of the controller. To document my learning process, I thought I’d blog about controllers, because they are such a fundamental part of an Angular application. In fact, they are the coordinators of the application.

Controllers are the part of an application that connect the models and views. In other words, they take the data that is processed in the model and allow them to be displayed in the view which are HTML pages, connecting the business logic and the presentational logic. 

This is the basic structure of a controller: 

```
function BookController($scope) {
  $scope.title = 'The Great Gatsby;

  $scope.character = {
      name: “Jay Gatsby”,
    gender: “male”
  };
}
```

We can create a function with the name of the controller and pass in what is called a $scope variable. $scope is a very powerful part of the controller. Every controller has a scope. It allows us to set the values of different variables, and then display them in our views. According to the AngularJS docs, scopes are actually objects which are arranged in such a way that they represent the DOM structure of the application. This is how we are able to access the scope’s variables in our view. When writing an application, it is important to remember that we can only access the scope’s variables when we are inside of our controller. Scope variables that are accessed outside of the controller will not be rendered. 

Every controller belongs to a module, which is created for each feature or component of the application. We can specify what module the controller belongs to with the following line of code. In this case, I have created a module named “bookApp”, and have attached a controller named “BookController.”

`angular.module(‘bookApp’).controller('BookController', BookController);`

When displaying variables in our view, we must tell our HTML page the name of our controller using ng-controller, as well as the module that it belongs to, using ng-app.So how do we display the controller’s scope variables in our views? One way is to use {{ }} in our HTML page. Here, we will see “Jay Gatsby” displayed in the text of the h2 element.

```
<div ng-app="bookApp">
  <div ng-controller="MainController">
    <h2>{% raw %}{{title}}{% endraw %}</h2>
    <p>{% raw %}{{character.name}}{% endraw %}</p>
  </div>
</div>
```


Another way is to use ng-bind as shown below. In this example, the entire p element will be replaced with the text, whereas with brackets, we can specify exactly where in the element we want the variable to be displayed.

`<h2 ng-bind="title"></p>`

If we try to access the scope’s variables outside of the controller, the variable’s values will not be shown in the HTML. In other words, if I put {{title}} outside of the controller’s div, our application would not be able to display that variable’s value.


**Another Way to Write Controllers**

We could pass the $scope variable to every controller we create, but this may get redundant pretty quickly. There is another cleaner way to write our controllers and display variables in our view.

```
<div ng-controller="BookController as book">
</div>
```

We first create an instance of our controller, and specify the name of our instance. In this case, we are specifying that we want to be able to access our controller, BookController as a variable named “book”. This takes all of our variables that are attached to $scope and binds them to the controller’s instance instead. 

We can edit our controller to remove the $scope variable, and add “this” before each variable name. This allows us to create controller variables and assign values to them.

function BookController() {
this.title = 'Great Expectations;
}


We can then access our controller’s variables in this way: 

```
<div ng-app="bookApp">
  <div ng-controller="BookController as book">
    <h2>{% raw %}{{ book.title }}{% endraw %}</h2>
  </div>
</div>
```

As we have seen thus far, controllers are a highly essential part of an Angular application, considering their function is to connect our models with our views. In this post, I have provided a basic introduction to controllers. I’m now looking forward to solidify my understanding of other Angular concepts such as services and directives!
