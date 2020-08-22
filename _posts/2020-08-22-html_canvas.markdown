---
layout: post
title:      "HTML Canvas"
date:       2020-08-22 04:03:03 +0000
permalink:  html_canvas
---

This week I created a fun and simple drawing board using HTML <canvas>. Canvas is only a container, so JS must be written in order to actually do the drawing. By default canvas has no border. See below for my default markup:

```
<canvas id="draw" width="800" height="800"></canvas>
```

Now, you do not actually draw on the canvas element itself, you actually draw over something called the context. So we need to grab that 2D:

```
const canvas = document.querySelector('draw');
const ctx = canvas.getContext('2D');
```

Another thing we want to do is resize the canvas to be the size of our window:

```
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
```

We then want to set a few variables that will serve us for coordinates and to tell it when it should or shouldnt draw:

```
let isDrawing = false;
  let lastX = 0;
  let lastY = 0;
	
	function draw(e) {
    if(!isDrawing) return; //stop the fu from running when they are not moused down
    console.log(e)
  }

  canvas.addEventListener('mousemove', draw)
  canvas.addEventListener('mousedown', () => isDrawing = true)
  canvas.addEventListener('mouseup', () => isDrawing = false)
  canvas.addEventListener('mouseout', () => isDrawing = false)
```

I have also included some event listeners that you can see the change the state of our isDrawing variable when the mouse is being moved or clicked. This is the very beginnign of this, I will be diving deeper into the actual drawing and finishing out the function in Part 2.




