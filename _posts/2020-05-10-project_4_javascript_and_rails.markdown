---
layout: post
title:      "Project 4: JavaScript and Rails"
date:       2020-05-10 22:51:16 -0400
permalink:  project_4_javascript_and_rails
---


So uh, quarantine life, right?

It took me a bit to figure out what the backbone motif of this post was going to be; perhaps I'm just falling back on what's topical, but I'd say there's a real connection here. Javascript is a big jump away from the Ruby that we've been working on until this point, being a whole new language when previously Ruby > ActiveRecord > Rails all used the same language. And needless to say, Covid-19 has also wracked the world with a new status quo; our new "language" is manifest in our communications being much more predominantly over Zoom and Skype rather than in-person. But perhaps things are still more familiar than they might let on. 

ISOLATED TESTING

All of my JS coding begins in the browser console. It is here that I try out individual queries and method chains to see what can return the information I want. For instance, I wanted to be able to grab all of the background links from the Backgrounds page. I would first confirm that `document.querySelector("a")` got me a list that would include all the links I wanted (plus some extras), and then parse the results until I refined it down to just the links I wanted. I had quite the chain when I was done:

`Array.from(myDom.getElementsByTagName("h1")).filter(heading => heading.className === "title").map(x => x.getElementsByTagName("a")[1]).filter(x => !!x);`

With a useful serum in hand, I record it in `phrases.js`. I think of this as a staging area, where all my individual snippets of useful code exist, but not yet strung together in a way that presents a greater functionality for my project.

SOCIAL DISTANCING

Code that has cleared testing for phrasing can proceed to "index.js". Here is where we make sure that the phrases we've made can speak to each other without stepping on each other's toes. Let's think of this as the electronic equivalent of six-feet away.

What is dependent, and what is not dependent?

I made exemplary use of this in my characters#destroy pathway. Because it is a request that will route through CharactersController, I would need to keep it as part of my JS Character class in order to keep the logic. JS Character must be initialized with a character object, but #destroy begins with the Delete button. 

CONTACT TRACING

As I break the code into classes, it then becomes necessary to rethink their routing. What were once general method calls now needed to operate on class instances (ie `playerCard(player)` was now `player.playerCard()`).

I decided on a standard: all buttons will point to a single router. The router will point to JS class methods. These methods will be the fetch requests that dive into the backend.

NOT JUST THE FLU



OPENING EARLY

It is important to make sure that a problem is actually solved before you start operating as if it is solved. Step too soon, and it can become a matter of solving the problem you have in front of you and only getting the immediate solution. And then solving the many more problems that the immediate solution created.

In my case, the problem was one of synchronous execution: the code that reads the gathered list of options and stacks them into the dropdown menus was executing before the code that would actually scrape and gather those options would execute. The initial result of this problem was quite ugly: my code would look for the list of options, see `undefined` where they should be, get upset, and fail gracelessly. Tackling the symptom first, I was able to make it fail grace*fully* instead by creating an empty array to be filled by the scraper; this would render my select boxes at least, though they would still be empty because the dropdown filler was executing before the scraper.

And there was a pretty easy immediate solution to this: set an excessive timer on the dropdown filler to make sure it waits for the scraper. In fact this is the solution that I had in my first demo. Assuming I haven't replaced it by the time you read this, pay attention at the end of the video: you might notice that the select boxes just straight up don't load after one of my refreshes. This is asynchronous coding, and works perfectly fine server-side. But I found it unsatisfying client-side.

Flatiron uses the allegory of a restaurant to describe asynchrony: begin cooking the entrees while you serve the customer breadsticks and drinks, to tide them over as they wait. Basically, doing work in an order that will get the immediately relevant stuff to the user quickly, while in the "back room" you work on the stuff that they'll get to. There's an aspect of this metaphor that my solution did not yet account for: the "back room". But having my dropdowns visibly fill in after the page has loaded, it's the equivalent of making the customers dine in the kitchen and having them need to sit through the cooks yelling at each other to throw food into different ovens (okay, there are restaurants where this is part of the gimmick; Hibachi's pretty great, but bear with me).

Rather than having it be so obviously apparent what corner I cut, and allow users to see my elements so obviously loading in procedurally, I could adapt asynchronous logic to my presentation as well.

What if the character selection menu didn't even exist until the user confirmed that they wanted to make a character? This would separate the scraping (occurs when the DOM is loaded) from the dropdown-filling (occurs when "New Character" is clicked). Doing this would mean that the average user would not see the timing glitch occur, unless they intentionally tried to click on "new character" as fast as possible as the page was loading.
