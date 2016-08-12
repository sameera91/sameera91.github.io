---
layout: post
title: Testing My Rails Application
---

**Test-driven Development**

Test-driven development is a process in which the application being written is designed to pass specific test cases that define what an application is supposed to do. Testing a rails application is a highly essential part of development, and ensures that an application works as intended. In this blog post, I'm going to revisit my Rails application, Creatify, and cover specific tests cases that I've written using Rspec and Capybara. I've written these tests to ensure that certain features, such as creating or deleting a record work as intended. I've also added tests to ensure that users can sign up, sign in, and log out of their accounts successfully.

**User Specs**

Part of my feature specs ensure that a user can sign up, sign in, and sign out of their user account. Before I could do this, I had to install three gems: capybara, rspec-rails and factory_girl_rails. Rspec is a testing framework that allows the programmer to define what they expect their program to do, and Capybara allows us to write tests that model a user interacting with the app, performing actions such as clicking a button, for example. Factory Girl is a library that allows us to create test data to be used in our tests. 

I started out by creating user data through the use of Factory Girl as shown below: 

```
FactoryGirl.define do
  factory :user do
    name                  "User"
    email                 "user@example.com"
    password              "user123"
    password_confirmation "user123"
  end
end
```

I could then simulate a user logging into an account just like the following, creating a feature and a scenario: 

```
feature 'User can sign up and login' do

  scenario 'User can log into account' do  

      user = FactoryGirl.create(:user)
      login_as(user, :scope => :user)

      visit new_user_session_path
      
      expect(page).to have_css '.welcome'
  end
end
```

Here, Factory Girl creates the user, and the login_as method is what simulates the user logging in to an account. I can then test the login page by using the 'visit' keyword and the specific login path, and can use either has_css or has_text to ensure that the correct css or text is on the page. 

We can also simulate a user filling out a form through keywords such as fill_in and click_button: 

```
def create_user
    fill_in "user_email",    with: "sameera@test.com"
    fill_in "user_name",    with: "sameera"
    fill_in "user_password", with: "123aaabbb"
    fill_in "user_password_confirmation",    with: "123aaabbb"
    click_button "Sign up"
end
```
Capybara keywords such as fill_in and click_button allow the tests to fill out form fields and click a button submitting the form information. We can then test that form submission worked by making sure that our page has information such as the user's name, a welcome message, or a notification message.

**Project Specs**

The project specs folder contains feature tests to ensure that project can be created, updated, and deleted. To test the creation of a project, I have the following code: 

```
feature 'New project can be created' do

    scenario 'Visit form to create new project' do  

      user = FactoryGirl.create(:user)
      login_as(user, :scope => :user)

      visit new_project_path 

      fill_in 'project_title', with: 'New Project'
      find('.form-control').set('app/views/layouts/Drawing.png')
      click_button 'Create Project'

      expect(page).to have_text 'New Project'
  end
end
```

Just like in the user specs above, we use keywords such as fill_in and click_button to simulate the user filling out a form, and have_text to ensure that the project title is shown on the page. 

Testing is a very important part of any application. Frameworks and libraries such as Rspec, Capybara, and Factory Girl allow us to write tests seamlessly. 

