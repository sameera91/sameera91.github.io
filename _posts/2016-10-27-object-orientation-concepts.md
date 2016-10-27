---
layout: post
title: Object Orientation Concepts
---

**Object Orientation Concepts**

An important concept in programming is object orientation. Object orientation allows us to use objects in programming to represent something that exists in the real world, such as a book or a car, with each object having certain behaviors and characteristics. An object is created from a class, which contains the outline of what an object should be like. OOP is useful because it prevents the programmer from having to repeat code for multiple instances of a class.

There are certain concepts in object orientation that explain how classes and objects interact with each other, and how different types of classes relate to one another. Four important OOP concepts are inheritance, polymorphism, encapsulation, and abstraction. 

**Inheritance**

Suppose you wanted to create a class that has many of the variables and functions of an already existing class, but is supposed to have new variables and functions that are specific to that particular class. It would be repetitious and maybe even tedious to write an entirely new class with the variables and functions of the already existing class, along with the new functions and variables. This is where inheritance is useful. Instead of creating an entirely new class, we can create a subclass that inherits the functions and variables of its parent class. At the same time, you can customize this class to include new functions and variables as well. 

Let’s say we have a class named Book. Our Book class can contain variables such as author, publisher, and number_of_pages. We can also create classes that inherit from this Book class. Suppose we have a class named Fiction. This subclass would have the same properties as its superclass, Book. But we can create additional attributes for the Fiction class such as main_character, theme, and setting--variables which may not exist for books of other types. The Fiction class would then be able to access all of the variables Book class, along with the variables defined it in its own class. Similarly, we can create subclasses such as non-fiction, comedy, and drama.

**Encapsulation** 

When designing classes and objects, we must ensure that the class’s methods and attributes are invisible to outside users of the class, and that outside users of the class cannot reach in and change the class’s characteristics. This is where encapsulation comes in. Encapsulation also ensures that objects cannot change the characteristics of each other. Any changes made to the object must be done through the object’s methods, and any outside users of the class can only interact with the class through its methods. If the variables of a class must be accessed or modified, they must be done through setter and getter methods.

In Ruby, setter and getter methods are created through the attr_accessor property like the following: 

```
attr_accessor :title, :author, :publisher, :number_of_pages
```

This saves us from having to write a setter and getter method for every variable.

**Polymorphism**

As discussed before in inheritance, we can create derived classes from an existing parent class. These derived classes will have the same properties as its parent class, along with new properties specific to that class.

Polymorphism is the idea that we can create multiple derived classes from one parent class. Each of these classes will have its own methods, but they can also contain what is essentially different versions of the same method that exists in the parent class. What this means is that a parent class will contain a method, and each subclass will inherit that method, but with a different number of parameters. This is called function overloading, and allows the subclass to customize that method as necessary for that particular class.

Going back to our Book class, we could have a method called create_book in the parent class that then contains a different number of parameters in each subclass. For example, the Fiction class can contain parameters such as theme, main_character, setting, and plot. The Nonfiction class on the other hand, can contain only one variable, such as summary. 

**Abstraction** 

The purpose of abstraction in OOP is to hide details which are not necessary in order to interact with that class at that level. This allows the user to see only the relevant details of a class. This is done in order to simplify things at the uppermost level, with more details revealed as more subclasses are created. For example, a parent class can contain a method without the method’s implementation shown, and the parent’s subclass can contain the implementation of that method. This subclass can contain more methods where the implementation is hidden, and subclasses of this subclass contain implementations of these methods. As one moves down the inheritance tree, more details, aka more method implementations are revealed.

These four OOP concepts describe the relationships that can form between classes and objects, and are necessary in order to create good and efficient object-oriented code.

