---
layout: post
title:      "Command line Scraper"
date:       2020-08-07 17:48:05 +0000
permalink:  command_line_scraper
---


My first CLI project is composed of the fundamendatl skills i have learned my last three week at flatiron school.
The concept of my project is simple, scrape a website for the top teams of all time and let the user pick a team to read more about.

Finding a website to scrape was a bit of a challenge for me. I wanted to find a website that was not going to be incredibly difficult to scrape as that was not the focus of the project. The focus was OOP ( Object Oriented Programming).

My project uses 3 classes : Scraper, Team, CLI

My Scraper is responsible for for getting the information from my site using Nokogiri to parse the HTML. 

```
doc = Nokogiri::HTML(open(BASE_URL))
    
    team_info = doc.css("#hub_resp_main .full.module.moduleText")[1..10].reverse
    team_info.collect do |element| 
```

This class has two attribute (objects), name and description. As you can see below, after setting my attributes I instantiate my Team objects using these attributes as arguments.

```
name = element.css("h2").text
        description = element.css("p").text
        Team.new(name, description)
```

My Scraper class is directly interacting with my Team class that holds my initialize method
```
def initialize(name, description)
      @name = name
      @description = description 
      @@all << self
    end
```
This instance method allows me to instantiate only with attributes i see fit and storing them in an array.

My CLI class is what gives the application life. Here is where I created all the behaviors that i wanted for for my application. Starting with an instance method that holds the order i want my obects executing in. 

```
def run 
    greeting
    list_teams
    Scraper.scrape_team_info
    list_msg
    call
  end 
```

As you can see here, I am calling on my class method here as it in order to intantiate all of my objects.
I have created instance methods to allow the user see the list of teams, to allow a user to input , and to allow the user to exit. I also have a method that allows the program to loop around until the user is ready to exit.

I had many struggles, the major one was understanding the difference between procedural and object oriented programming in practice. Making my code more dynamic and less likely to break was a huge learning block for me. This small app is just the starting point for me, I plan to do great things in the future. My goal is to keep learning and keep pushing forward, because i know that every struggle is also a learning experience.
