---
layout: post
title:      "Project 4: JavaScript and Rails"
date:       2020-05-11 02:51:15 +0000
permalink:  project_4_javascript_and_rails
---


It's a matter of solving the problem you have in front of you and getting the immediate solution. And then solving the many more problems that the immediate solution created.

And there was a pretty easy immediate solution: set an excessive timer and have the dropdowns just wait. In fact this is the solution that I had in my first demo. Assuming I haven't destroyed it by the time you read this, pay attention at the end of the video: you might notice that the select boxes just straight up don't load after one of my refreshes.

Rather than having it be so obviously apparent what corner I cut, and allow users to see my elements loading in procedurally like this is Unity engine, I could adapt asynchronous logic to my presentation as well.

Flatiron used a metaphor of a restaurant to describe asynchrony; basically, do work in an order that will get the immediately relevant stuff to the user, while in the back room you work on the stuff that they'll get to. What if the character selection menu didn't even exist until the user confirmed that they wanted to make a character?

That would mean that pretty much any user would not see the timing glitch occur, unless they intentionally tried to click on "new character" as fast as possible as the page was loading. And personally, I say if a user desperately wants to find the glitch then let them; it's half the fun. Again, just like Unity engine.
