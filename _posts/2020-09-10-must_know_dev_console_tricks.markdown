---
layout: post
title:      "Must know Dev Console Tricks"
date:       2020-09-10 21:16:28 +0000
permalink:  must_know_dev_console_tricks
---


One of my biggest struggles during my career transition has been debugging. Although it has been a huge struggle, it is something I really enjoy doing because it really gives a different perspective on my code and where I have gone wrong. A big learning experience, having said that, Ive gotten a chance to have a lot of fun with the dev console. I would like to talk about some tricks with the dev console that you may or may not know that are very helpful. 

1. There is a feature called "attribute modification" that allows you to see what exactly is causing the event to happen. When you inspect an item, right click on the element/break on/attribute modification. Once you fire the event it will pop up a debugging window that with a highlighted line that shows you exactly what is causing it.
2. With is ES6 we can interpolate by putting the variable inside the string with back ticks:
```
let name= sam
console.log(`Hello my name is ${name}`)
```
but you can also do:
```
console.log('hello my name is %s', 'sam')
```
whatever come on the second argument is what the variable is worth.
3. You can also style text:
```
console.log('%c What about this?', 'font-size:50px; background: red;')
```
just add %c to the beginning of the string and you got it!
4.There are 3 useful hints when you want to display either a warning, error, and/or info. It will also give you a stack trace of where exactly that line of code comes from:
```
// warning!
    console.warn('OH NOO');
    // Error :|
    console.error('GO BACK!');
    // Info
    console.info('Crocodiles eat 3-4 ppl per year');
```
5. `console.assert(3 === 4, 'that is not correct!')` .assert will throw a msg if whatever is beign tested first is wrong.
6. `console.dir()` will allow you to open all the different properties of a certain element.
7. I have also been messing around with `console.group` which allows me to group several logged lines together, but I have not worked on a big enough project yet in which this has been super helpful. But I can imagine it is.


