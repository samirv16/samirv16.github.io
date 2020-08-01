---
layout: post
title:      "Filter Search"
date:       2020-08-01 02:13:08 +0000
permalink:  filter_search
---


Today I want to go over how to create a feature in the search box that allows you to show you matches of the letters you are typing.

first things first, we have to create a search box. 

```
  <form class="search-form">
    <input type="text" class="search" placeholder="City or State">
    <ul class="suggestions">
      <li>Filter for a city</li>
      <li>or a state</li>
    </ul>
  </form>
```

We will be pulling information from a json list of cities and states on the web. We will name this variable "endpoint".
Endpoint is a an array of objects, we want to eventually have an array of our own so make sure to declare an empty array.

```
const cities = [];
```

Next we want to start a fetch request. The request will return a promise which we can use to retrieve a "blob" of information that can be turned into json, after which we can can retrieve the data and spread it into our new cities array.

```
fetch(endpoint)
  .then(blob => blob.json())
  .then(data => cities.push(...data))
```
We now want write a function that will figure out if the city or state matches what was searched.

```
function findMatches(wordToMatch, cities) {
  return cities.filter(place => {
    const regex = new RegExp(wordToMatch, 'gi');
    return place.city.match(regex) || place.state.match(regex)
  });
}
```

Notice, how we are using regex to look for matches. "wordToMatch" is the word that will be passed in by the user, the "g" flag means global so it will look through the entire list, and "i" flag means insensitive so it will not worry about case sensitivity.

```
function displayMatches() {
  const matchArray = findMatches(this.value, cities);
  const html = matchArray.map(place => {
    return `
    <li>
    <span class="name">${place.city}, ${place.state}</span>
    <span class="population">${place.population}</span>
    </li>
    `;
  }).join('');
  suggestions.innerHTML = html;
}

const searchInput = document.querySelector('.search');
const suggestions = document.querySelector('.suggestions');

searchInput.addEventListener('change', displayMatches);
searchInput.addEventListener('keyup', displayMatches);
```

All we are doing here in the last part above is actually displaying the matches. We are adding event listeners to the search bar for kestrokes and change in state. All there is left to do, display the proper information where you want it, and I am doing so by adding it to my suggestions class with ".innerHTML"
