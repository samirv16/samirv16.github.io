---
layout: post
title:      "Flexbox or Flex Panels"
date:       2020-07-17 23:45:06 +0000
permalink:  flexbox_or_flex_panels
---


This week I wanna talk about flexbox. I worked on a small item this week that was heavy on css and learned a lot there. Flexbox is a css layout model, and it will allow elements to rearrange depending on screen size.

To start using flexbox you have to definie the flex container. You can achieve this by declaring it on the css container:
```
<ul >
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ul>

ul {
list-style-type:none;
margin:0;
padding:0;
border:1px dotter red;
display:flex;
}

li {
border:1px solid black;
margin:0.5em;
padding:0.5em;
}
```

As you can see, I added the `display:flax;` property to the container as we have to control everything through the container with flex. By default everything will be from left to right in the order they are defined, and will not be wrapping. By default it desplays in row fashion, but it works in column fashion as well.

```
ul {
list-style-type:none;
margin:0;
padding:0;
border:1px dotter red;
display:flex;
flex-direction:column;
}
```

You can also reverse the view:

```
ul {
list-style-type:none;
margin:0;
padding:0;
border:1px dotter red;
display:flex;
flex-direction:column-reverse;
}
```

Also important to note is that there are no margins and padding by default.

The `justify-content` property is amazing as it allows you to place items from left to right, right to left, or centered all with one property. `align-items` wiill allow you to align vertically. 

Theres so much more to learn and talk about here, but I have noticed that instead of trying to be super specific, which I dont want to be, I can use flex and easily align all my items without too much work. I will keep using this model moving forward and come back with some tricks that are maybe not soo common. 

See you next week.
