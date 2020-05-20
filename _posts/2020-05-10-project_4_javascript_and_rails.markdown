---
layout: post
title:      "Project 4: JavaScript and Rails"
date:       2020-05-10 22:51:16 -0400
permalink:  project_4_javascript_and_rails
---


So uh, quarantine life, right?

It took me a bit to figure out what the backbone motif of this post was going to be. 

It's a matter of solving the problem you have in front of you and getting the immediate solution. And then solving the many more problems that the immediate solution created.



What is dependent, and what is not dependent?


I made exemplary use of this in my characters#destroy pathway. Because it is a request that will route through CharactersController, I would need to keep it as part of my JS Character class in order to keep the logic. JS Character must be initialized with a character object, but #destroy begins with the Delete button. 

ISOLATED TESTING

All of my JS coding begins in the . It is here that I try out individual queries and method chains to see what can return the information I want. 

SOCIAL DISTANCING

Code that has cleared testing for phrasing can proceed to "index.js". Here is where we make sure that the phrases we've made can speak to each other without stepping on each other's toes. Let's think of this as the electronic equivalent of six-feet away.

CONTACT TRACING

As I break the code into classes, it then becomes necessary to rethink their routing. What were once general method calls now needed to operate on class instances (ie `playerCard(player)` was now `player.playerCard()`).

I decided on a standard: all buttons will point to a single router. The router will point to JS class methods. These methods will be the fetch requests that dive into the backend.

NOT JUST THE FLU



OPENING EARLY

It is important to make sure that a problem is actually solved before you start operating as if it is solved.



And there was a pretty easy immediate solution: set an excessive timer and have the dropdowns just wait. In fact this is the solution that I had in my first demo. Assuming I haven't replaced it by the time you read this, pay attention at the end of the video: you might notice that the select boxes just straight up don't load after one of my refreshes.

Rather than having it be so obviously apparent what corner I cut, and allow users to see my elements loading in procedurally like this is Unity engine, I could adapt asynchronous logic to my presentation as well.

Flatiron uses the allegory of a restaurant to describe asynchrony; basically, do work in an order that will get the immediately relevant stuff to the user, while in the "back room" you work on the stuff that they'll get to. What if the character selection menu didn't even exist until the user confirmed that they wanted to make a character? This separates the scraping (occurs when the DOM is loaded) from the display (occurs when "New Character" is clicked).



That would mean that the average user would not see the timing glitch occur, unless they intentionally tried to click on "new character" as fast as possible as the page was loading. And personally, I say if a user desperately wants to find the glitch then let them; it's half the fun. Again, like this is Unity engine.
