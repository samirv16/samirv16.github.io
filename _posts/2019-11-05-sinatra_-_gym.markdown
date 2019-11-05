---
layout: post
title:      "Sinatra - Gym"
date:       2019-11-05 19:56:09 +0000
permalink:  sinatra_-_gym
---



I decided to build an app that would allow a gym to let its trainers create, read, edit, and delete courses (classes) that they would like to offer. To create a course the user is asked to provide the name, description, and price for the course.

I started by running the corneal gem to create my file structure. Next I wanted to do the things I was sure about. So i decided to create my user table with all the columns that i wanted it to have, in this case name, username, and password. I wanted to make sure all passwords stored in the database were encrypted before being saved, so making sure I used the has_secure_password method from the bcrypt gem was important. That provides us with the ability to use password_digest as a column so that the password being saved is hashed and salted. By using 'securerandom' to generate a long random key, I was able to setup my secre session password, storing it in a constant variable and setting up a d gitignore file for security purposes. I also made two models, user and course, where user has_many courses, and course belongs_to user.

I then went on to set up the main page, where I put the name of the gym, small description as to what to expect, and options to login or signup. All of this is displayed in my index.erb page which required a get request to render it. Next, I wanted to do my login options. Once I had rendered my login page, i wanted to make sure the user would get an error message if something was not entered properly or left blank.

```
<% if @failed %>
            <p class="danger">Your username/password combination was incorrect</p>
        <% end %>
```

I also made all of the error messeges a class of 'danger' so i could use css and make them red.
After finishing everything and testing it for bugs, i decided to add a sign up button in case you realize you don't have an account with us just yet.
I then had to create a sessions controller which takes care of get and post requests for the login, signup, and logout buttons. My login post route includes a conditional that loops you back to login if something goes wrong when trying to do so, otherwise you are welcomed to your home page. The home page includes buttons to the courses, home, and logout. 

Once in the courses page, the user will see all existing courses but will only be able to edit or delete their own.
```
 <div class="course">

     <h4><%= user.name %></h4>
     <p><%= course.name %></p>
     <p><%= course.description %></p>
     <p><%= course.price %></p>

        <% if course.user == current_user %>
            <a href="/courses/<%= course.id %>/edit">Edit</a>
            <form action="/courses/<%= course.id %>" method="post">
                <input type="hidden" id="hidden" name="_method" value="delete">
                <input type="submit" value="Delete">
            </form>
        <% end %>
 </div>
```
In order to get the delete and edit button to work I had to create a delete and patch request. the delete button will delete the course and loop the user back around to the courses page, with the edit button showing the user a form allowing them to edit what has already been entered.

An issue encountered at this point was that even though visually everything was working accordingly, i could manually type different routes on the url and edit other users courses. So i created two helpers:
- an authenticate helper that verifies if the user is logged in otherwise redirect to login page. I used this method to authenticate users when going to courses or creating new courses. 
- an authenticate_user helper which uses the previous authenticate method plus redirects the user to an error page if the course returns nil, or to home if the current user is not the the owner of the course.
- 
```
def authenticate_user(course)
      authenticate
      redirect '/error' if !course
      redirect '/home' if current_user != course.user
    end
```
I used the helper for my delete and patch requests.

Lastly, my signup page. It offers to render a form to sign up with a name, username, and password, along with offering some error messages to make sure its done correctly.

```
<% if @user && @user.errors.any? %>
        <% @user.errors.full_messages.each do |e| %>
            <p class="danger"><%= e %></p>
        <% end %>
    <% end %>
```

I used the errrors the console was giving me for the users. to logout I used an href buttom with a get request to redirect to the main page. 

I enjoyed making this simple site as i got to immidiately see the results or errors on the browser through shutgun. 
