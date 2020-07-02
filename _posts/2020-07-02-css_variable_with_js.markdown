---
layout: post
title:      "CSS Variable with JS"
date:       2020-07-02 05:05:13 +0000
permalink:  css_variable_with_js
---

I have decided that I want to become really good with Javascript, so I have decided to focus solely on it for a few weeks. With that obviously comes HTML and CSS, and this week I learned how to use CSS variables. What I learned was very basic stuff, but cool nonetheless.

First things first, I learned that CSS variables are declared in some sort of element. In the instance below, I declare in the :root element. Here i have the default values for these variable which later I can change with JS which will in turn update that style anywhere on the page where it is used.

```
:root {
      --base: #ffc600;
      --spacing: 10px;
      --blur: 10px;
    }
```

Once you have declared each variable and given them their default values you can start using them, and they can be used anywhere on the page. Instead of passing in a value, you will just pass the name of the css variable you want to use:

```
img {
      padding: var(--spacing);
      background: var(--base);
      filter: blur(var(--blur));
    }
```

Notice how instead of interpolating with ${}, css standar is --. I read that it helps with backwards compatability with older browsers. 

Now that this is all set, all there is left to do is write JS to start maniputing the styles on the page! As far as I can tell, theres nothing special about how you would go about this than if you weren't using css variables. 

On a side note, I know I said I would keep writting about the prototye design patter this week, but I might have to hold off a few more days. Its taking me a little bit to really truely grasp, and I want to make sure I do that before writting about it again.

