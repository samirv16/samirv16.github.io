---
layout: post
title:      "Prototype Design Pattern"
date:       2020-06-26 20:46:53 +0000
permalink:  prototype_design_pattern
---


This week I set out to learn and practice the prototype design patter. I was recently in a mock technical interview and was told that this design pattern is one that would impress him most if an entry level candidate was to showcase it. So lets dive right in:

What is the PDP?

As I understand it, it is used to create new instances by copying other instances.This allows us to add any subclass instance of a known superclass at runtime. You would use this when there are several classes that you want to use only if needed at runtime. It also reduces the need for creating subclasses. A I was watching some videos of this and doing my own little samples, I realized that this is inheritance. You create an object and pass down its properties to all new instances of it. 

One very good example I went over was this:

```
var myCar = {
 
  name: "Ford Escort",
 
  turn: function () {
    console.log( "To the right or to the left?" );
  },
 
  honk: function () {
    console.log( "Hey! be careful there!" );
  }
 
};

// Use Object.create to instantiate a new car
var yourCar = Object.create( myCar );
 
// Now we can see that one is a prototype of the other
console.log( yourCar.name );
```

Now the property <name> is not being cloned to the new object, <myCar> is passing down that information to the <yourCar>. This is as much research as as I have been able to do this week on the subject but there is more to learn, so next week ill be back with part two.
