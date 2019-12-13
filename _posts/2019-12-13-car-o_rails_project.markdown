---
layout: post
title:      "CAR-O Rails Project"
date:       2019-12-13 14:08:57 -0500
permalink:  car-o_rails_project
---



I learned so much making this project. I fell a little behind after my sinatra project and might have rushed through some lessons. Every project to this point has been a huge learning experience, but for me this one has been the biggest. Reasoning through some of the things that I was really stuck, and spending several hours talking to fonsi and mikie about things that we didnt understand was of incredible help in helping me understand Rails. Although we have done these things past for each other, I walked in on this project with a cloudy understanding of what I needed to do. I felt like we have laid down a good foundation of thinking a certain way, of problem solving that I was able to tap into. 

On to my project:

I use devise to set up user model, along with registrations, and verifications. I have a total of 4 models: user, owner, car_rental, and review. My app is meant to be a peer to peer car rental app, where anyone who owns a car in any given place can rent a car to any user. The car rental model is set up with an optional belongs_to user relationship because I needed to be able to create the object without it necessarily belonging to anyone, afterall we don't know who will be renting this car yet. 

```
class CarRental < ApplicationRecord

    belongs_to :owner
    belongs_to :user, optional: true
    has_many :reviews

    validates :make, presence: true
    validates :model, presence: true
    validates :rate, presence: true

end
```

My controllers directory holds a couple additional controllers than what my models call for. One of them is the callbacks_controller which is setting my OAuth action. I am using OAuth to sign in with google. Google signs you in with an email and password, so thats what's being validated in the user model. I need to make sure the app didn;t require google to have a first and last name, otherwise it just wouldnt work. 

```
class User < ApplicationRecord
  has_many :car_rentals
  has_many :owners, through: :car_rentals
  has_many :reviews

  validates :email, presence: true
  validates :email, uniqueness: true
  validates :password, presence: true
```

My views carry a nav.html.erb partial that allows for some links if youre signed in, and orthers if youre not.

```
% if user_signed_in? %>
        <li><%= link_to "Car Rentals", car_rentals_path%></li>
```


```
<%else%>
        <li><%= link_to "Login", new_user_session_path %></li>
```

I also use an errors partial to display errors, and the quantity for my new review form. My car rental show page includes a picture of the rental, along with car info, reviews, and links to go back, write a review, and scope link (filters best reviews). 

My scope method includes a lamba block that asks only for reviews with a rating better than 3.

```
scope :best_reviews, -> { where("rating > ?", 3) }
```


This all makes up a little bit of my app. I want to keep this one going to see how far i can take it. I want to be able to try to get full functuanality by the end of our bootcamp, stay tuned. 

