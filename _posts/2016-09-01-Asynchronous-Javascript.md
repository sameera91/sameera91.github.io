---
layout: post
title: Asynchronous JavaScript
---

While working with Node.js, I noticed a key difference in the way that Node applications and Rails applications are run. An application built with Node.js is noticeably faster than one built with Rails, and this is because of asynchronous JavaScript and non-blocking I/O. 

In a Rails app, tasks are run sequentially. When we execute one task, we have to wait for that task to finish running in order to execute the next one. This is called blocking I/O. By contrast, node.js allows tasks to be executed simultaneously or asynchronously. This is called non-blocking I/O, and allows tasks to be processed more efficiently. 

Here is an example of a Ruby code that is executed from top to bottom: 

puts "statement 1"
first_function(2)
puts "statement 3"
second_function(3)

After executing this code, we will see "statement 1", anything placed inside of the first function, "statement 3", and then anything placed inside the second function. 

Here is an example of JavaScript code that includes a callback:  

console.log('statement 1')
setInterval(function(){
  alert('statement 2')
}, 500)
console.log('statement 3')

The difference between this snippet of code and the previous one is that this code includes a callback function. A callback is a function that contains another function as an argument. In this example, the first line is executed, and then the second line has to wait for 500 milliseconds before displaying the alert message. As we wait for the 500 milliseconds of the second statement to go by, the third statement is executed. "statement 3" is printed out before "statement 2." We can see here that the code is not executed from top to bottom, and we can perform other tasks while we wait for the callback function to run.

JavaScript contains other functions that we can use to determine the order of callbacks. Two of these functions are process.nextTick() and setImmediate(). process.nextTick() will schedule its callbacks to be run before I/O and timer callbacks, and setImmediate() will set its callbacks to run after I/O and timer callbacks.

While we can easily determine the order of execution of sychronous code, with asynchronous code we must consider callbacks and look at the code more carefully to determine the order that the statements are run.