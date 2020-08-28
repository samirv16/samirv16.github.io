---
layout: post
title:      "HTML Canvas #2"
date:       2020-08-28 22:53:06 +0000
permalink:  html_canvas_2
---


Lets finish up our drawing board. So up to this point we have pretty much all the basic ground work except our actual lines. So we want to call beginPath, moveTo, and lineTo on ctx to start the line but it will not actually show up until you call stroke. See below:

```
ctx.beginPath(); //start from
ctx.moveTo(lastX, lastY); //go to
ctx.lineTo(e.offsetX, e.offsetY);
ctx.stroke();
[lastX, lastY] = [e.offsetX, e.offsetY];
```

Ok, so there is are a few different things happening here. in the past blog you saw that we set so variables 
` let isDrawing = false;
  let lastX = 0;
  let lastY = 0;` which are serving us for coordinates. Once we begin the line, it will will go to wherever lasX and lastY are. Now, if you go to your console, you should see that e.offsetX and e.offsetY are coming from the actual event, so we want to make sure that our lastX and lastY variables match that, and thats what is happening on the last line.

Another thing you will notice is that at this point, the line still starts off at the upper right corner, we can fix this by adding a block to our mousedown eventlistener. After doing so, we want to add the real coordinates to it as well. Meaning whereever it is that you are clicking down:

```
canvas.addEventListener('mousedown', (e) => {
    isDrawing = true;
    [lastX, lastY] = [e.offsetX, e.offsetY];
  })
```

Lastly, if you want to make the line thicker, you can simply add `ctx.lineWidth = 75;` and substitute that number with whatever you want. 

This is a simple drawing board. Next week I will talk about some more advance little tricks we can do to have some fun with it.
