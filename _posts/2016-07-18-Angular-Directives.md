---
layout: post
title: Angular Directives
---

Another powerful and essential part of an Angular application is a directive. Directives enable you to create your own HTML elements and attributes, and allow you to attach a specific behavior to them. In other words, they enable the programmer to define exactly what should happen when, for example, a user clicks on a certain element. The two types of directives are event and behavioral directives. Event directives are functions that we can write to perform an action after a certain behavior occurs. Behavioral directives modify the DOM in some way. 

**Event Directives**

Event Directives are very similar to event listeners that we write in plain JavaScript. In Angular however, instead of using the “click” function or “onclick”, we would use the “ng-click” directive, and pass in a function to define exactly what happens when we click on the input element, as shown below: 

'<p ng-click="vm.clickFunction()">Click</p>'

Once we define the function, we can access any variables inside of it and display them in the view using our bracket notation likes this: {% raw %}{{this.newVar}}{% endraw %}

**Behavioral Directives**

If one of the tasks we wanted to accomplish was displaying all the information in a list, we could use behavioral directives. These are directives that change and interact with the DOM. A good way to know if you should use behavioral directives is if you find yourself modifying the DOM from your controller, something that is generally not preferred.

If we had a list as such in our controller: 

```
function TodosController() {
 this.books = [{
    title: 'Great Expectations’,
    author: 'Charles Dickens’
  },{
    title: 'The Great Gatsby’,
    complete: ’F. Scott Fitzgerald’,
  },{
    title: 'Harry Potter and the Sorcerer’s Stone’',
    complete: 'J.K. Rowling’
  }];
 }
```

We could display this information in our view using Angular in the following way. Whenever our todos list gets updated, the view is updated accordingly. Every time the list is updated, the DOM is modified.

```
<ul>
 <li ng-repeat="book in vm.books">
   <h1>{% raw %}{{ book.title }}{% endraw %}</h1>
 
   <p>{% raw %}{{book.author}}{% endraw %}</p>
 </li>
</ul>
```

**Custom Directives**

We’ve looked at the directives that Angular gives us in order to make up the components of a website, but we can create our own directives as well. For example, I can create a directive named myDirective using the following lines of code: 


```
function newDirective() {
   return {
  restrict: 'E',
       template: '<div>This is a new directive.</div>'
   };
}
```

We can then place <newDirective></newDirective> in our HTML, and inside these elements, we see a <div> with “Hello world!” written inside of it. 

We can use the “restrict” keyword to restrict our directive to one of four things: an element, attribute, class name, or comment. In this directive, ‘E’ means that we restrict our directive to an element.

The directive above has a pretty short HTML segment, but sometimes, our HTML can be much longer. In this case, it is better to put them in a separate file, and we can specify the file in our directive as follows, creating a template for our directive.

```
function newDirective() {
   return {
       templateUrl: template.html'
   };
}
```

Our template.html file can then contain all the HTML that we want to put inside of our directive.

In this blog post, I provided a basic introduction to directives. I look forward to making use of these and other Angular concepts as I build my next project--an Angular app with a Rails backend. I also look forward to writing tests in both Rails and Angular, as tests are highly essential in order to ensure that an application works as expected.
 
