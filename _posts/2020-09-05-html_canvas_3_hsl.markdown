---
layout: post
title:      "HTML Canvas #3 HSL"
date:       2020-09-05 04:35:01 +0000
permalink:  html_canvas_3_hsl
---


If you have never heard of HSL, head to the website: mothereffinghsl.com
HSL is basically the rainbow, but you can programatically chose random parts of the rainbow. the Hue part of HSL is from red to red, S is for saturation basically how bright it is, and L for lightness so white to black.

Ok so this will allow us to play with different line colors. lets set a couple variables:

```
  let hue =  0;
  let direction = true;
```

We will start with the hue at 0, or Red, and move forward from there. The direction variable will allow us to mess with the line width, you can name it something different if it makes it easier. Next we want to start our line at hue, so:

```
ctx.strokeStyle = `hsl(${hue}, 100%. 50%)`;
```

But we don't want to stay in red, so we want to increment it. Furthermore, hue goes from 0 to 360, once it reaches 360 we want to reset it back to 0, or maybe you don't but for now we will:

```
    hue++;
    if(hue >= 360) {
      hue = 0;
    }
```

Now the last thing I want to talk about is how to mess with the line width and then you can start changing it as much as you want. I want the line to increment from small to large and back down to small as I draw:

```
if(ctx.lineWidth >= 100 || ctx.lineWidth <= 1) {
      direction = !direction;
    }
    if(direction) {
    ctx.lineWidth++;
    } else {
      ctx.lineWidth--;
    }
```

This is a little confusing, but we want to tell it to reverse directions in size depending on what end of the spectrum its at. I really hope this was fun and helpful!
