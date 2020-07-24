---
layout: post
title:      "MVC Review"
date:       2020-07-24 20:00:23 +0000
permalink:  mvc_review
---


I was recently on a call with a developer, flatiron alumni, that talked to me about the clearly definied paths one can take as a developer. He told me that even though he chose the front end route, we are trained as full stack developer at flatiron. He also said that when he first started he had talked to senior front end developer that was not aware of the MVC design pattern and that he felt he had something to contribute to the team because of it. That has prompted me to do a small review on writting to make sure I am keeping up with patterns I learned even though I am not actively using them at the moment.

MVC stands for Mode, View, Controller. The purpose of this pattern, is to compartmentalize large applications into sections which each have their own purpose.

First the controller. When a user sends a page request to the sever, based on what URL the user is requesting, the server will send the request information to a specifiv controller. The controller will handle request flow and should not contain much code. It is the middle man between model and view.

Next model. The controller will ask the model for information based on the request. The model handles all the logic, interacts with the datebase, validation, saving, updating, etc. of the data.

Last view. The view will handle all data presentation which will be dynamically rendered based on information the controller sends it. The view does not care about the final presentation, it just cares about how to present it. It will send the presentation back to the controller which will handle sending that back to the user.

The model and view never interact with each other. All interaction goes through the controller. Having all logic and presentation separate makes creating complex applicatioins much easier.
