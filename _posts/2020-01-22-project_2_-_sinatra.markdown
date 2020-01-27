---
layout: post
title:      "PROJECT 2 - SINATRA"
date:       2020-01-22 23:19:35 -0500
permalink:  project_2_-_sinatra
---


FEATURE CREEP

Traditionally this is broken into Fantasy and Science Fiction. Well I've done my fantasy app. Obviously the next step would be the SciFi app.

Command Line Interface is inherently a more solitary system.

This was also before propogation and storage of data in databases.

WEB DESIGN

A disclaimer for the entirety of this section: I have done pretty much no research on practices for aesthetic web design. Everything that is about to follow is 

Corneal provides a neat prepackaged layout.erb view to serve and a header and footer for 

UNFINISHED EDGES

Characters and Locations have a Story and Image attribute that a Writer can fill on Create or Update, but there is no actual view to Read this information. These are 

OFF GRID

To this end, I was working 

It's a strange place to consider yourself "off the grid"

For that matter, there probably is a "waiting room wifi" that I could have accessed, perhaps I just needed to ask someone. In fact, as I'm writing this a part of me is convinced that the wifi instructions were sitting on a wall somewhere. Perhaps directly behind my seat for maximum irony. Or maybe directly in front of my seat for...also maximum irony.

But it was in that git-deprived moment that I had placed myself, working on my project while my car was tended to. This particular coding session revolved around my Location and Character objects.



ACTIVATION ENERGY

I studied Chemical Engineering at college, so give me a bit as I move to a different field of analogies. Let's take Water, good old H2O, made of *H*ydrogen and *O*xygen. In order for these gasses to react with each other and form water, energy is required to excite them into a volatile state. To just visualize it from the model below, imagine a ball

![Over the Hill](https://www.siyavula.com/read/science/grade-11/energy-and-chemical-change/images/6db018d0e2786d2760763e37200c93fb.png)

Water is made of 3

Let's think of a code project like such a reaction. We're starting from basic concepts and using them to creating something more complex. 

This is the idea behind Github: save your work at its stable states, so that if a particular stretch of coding goes in the wrong direction and will not be useful enough to overcome that "activation energy", we can fall back to the last stable state and start again from there, rather than having to try changing directions while you're still on the slope with unstable code.

Naturally, this begs the question

And here is where I can bring us back to coding, because this is largely related to the usefulness of GitHub.

Working on my Ruby CLI I maintained a strict protocol: `git add .` > `git commit -m` > `git push`. In fact, you can throw a `git status` before every step and at the end just to settle my mind goblins on just where in the push protocol I was.

Working on The Usual Spot has been considerably different. I try to add files to my commits individually so I can mentally keep track of what I changed in each. And often I'll have many updated files that, thought I worked on them concurrently, I want split into multiple commits rather than a single one, to reflect progress on different fronts of the application. For instance, establishing authentication and preventing propogation of bad data required safeguards in mostly the same files and methods, so I was working on them concurrently. However, as actual concepts they are more distinct, and my approach to solving them also differed (using Sinatra's prebuilt methods for data-checking but building my own code for authentication), and so I broke the work up into two different commits. Then there was also the further work of 

I tend to pile up multiple commits


