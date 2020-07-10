---
layout: post
title:      "Different ways to iterate through arrays"
date:       2020-07-10 15:02:16 +0000
permalink:  different_ways_to_iterate_through_arrays
---


This week I focused of reviewing iterations and refactoring my code. I want to write about this, as I said on my last blog, I want to get really good at one thing ( that thing being JS in this case). So Ive found that recording myself and writting about things I want engrained in my brain are good ways to exercise that.

First off, we have filter. Filter takes in a function that will loop over the array, that will give us each array element which we then decide whether to keep it or not.

1. Filter the list of inventors for those who were born in the 1500's (given an array of inventors which is excluded from this post)
```
    const fifteen = inventors.filter(inventor => inventor.year >= 1500 && inventor.year < 1600)
		console.table(fifteen);
```

PS I also learned about console.table() which will return the data in a nice table on the console!

We move on to map. Map will take in an array, do something with that array, and then return an array of the same length. 

ie:
2. Give us an array of the inventors first and last names
```
const fullNames = inventors.map(inventor => inventor.first + '' + inventor.last);
    console.log(fullNames)
```

As you can see here, I've taken the original array and returned a different array with only the first and last names of the inventors.

Third we have sort. Sort will take 2 items at a time and compare them, then you return 1 or -1 to put item a either on top or below item b.

3. Sort the inventors by birthdate, oldest to youngest
```
const ordered = inventors.sort((a, b) => a.year > b.year ? 1 : -1)
    console.table(ordered)
```

Lastly I want to go over reduce. This one has been a little confusing for me but here we go. Reduce will itereate through the array and help you build something on every single item. It will give you the runnig total and the element from the array, so it allows you to build on that running total.

4. How many years did all the inventors live all together?
```
const totalYears = inventors.reduce((total, inventor) => {
      return total + (inventor.passed - inventor.year);
    }, 0);
    console.log(totalYears)
```

Hopw this was decentely explained, and see you next week!
