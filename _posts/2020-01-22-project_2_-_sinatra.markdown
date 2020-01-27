---
layout: post
title:      "PROJECT 2 - SINATRA"
date:       2020-01-22 23:19:35 -0500
permalink:  project_2_-_sinatra
---

We're stepping away from Fantasy and moving to Science Fiction; Cyberpunk in particular. The Usual Spot is an application for collaborative world-building, allowing multiple users to collectively create and populate their setting for use in forum roleplay and stuff like that. It is sufficiently genre-agnostic that you could use it for any setting (foreshadowing my integrating P2E Builder? hopefully), but it was a cyberpunk mood that guided my process here. Which might be related to why Sinatra's contribution to my coding philosophy is much more tech-integral than it was for Ruby CLI.

ACTIVATION ENERGY

I studied Chemical Engineering at college, so give me a bit as I move to a different field of analogies. Let's take Water, good old H2O, made of *H*ydrogen and *O*xygen. In order for these gasses to react with each other and form water, energy is required to excite them into a volatile state. This threshold is called the "activation energy". To just visualize it from the model below, imagine a ball on the flat left side (our H and O side). It would need to be pushed all the way over the hill in order to reach the flat right side (our H2O side); if pushed not high enough to clear the crest, the ball would just roll back down to the left. A multi-step reaction has multiple hils with multiple states of relative stability in between, and needing to overcome the activation energy each time.

![Over the Hill](https://www.siyavula.com/read/science/grade-11/energy-and-chemical-change/images/6db018d0e2786d2760763e37200c93fb.png)

Let's think of a code project like a multi-reaction. We're starting from many basic concepts and using them to creating something more complex. And while they will all come together in the end stable state, there are intermediate stable states where we have integrated some of the methods but not yet others. This is the idea behind Github: save your work at its stable states, so that if a particular stretch of coding goes in the wrong direction and will not be useful enough to overcome that "activation energy", we can fall back to the last stable state and start again from there, rather than having to try changing directions while you're still on the slope with unstable code.

Of course, it is not necessary to use Github in this way; nothing is stopping you from pushing while you're high up on the hill. In fact, I don't doubt that I had done so at least once with on my last project. Working on my Ruby CLI I maintained a strict (but misguided, in retrospect) protocol: `git add .` > `git commit -m` > `git push` at the end of every work session (maybe twice so if they were long). In fact, you can throw a `git status` before every step and at the end just to settle my mind goblins on just where in the push protocol I was.

Working on The Usual Spot went differently, thanks to one particular day at a car dealership. 

OFF GRID

Character: **Kal Megati** ~ *Aspiring Programmer who develops 'for the User'*

Haunt: **Nonspecified Car Dealership** ~ *Kal was waiting on some servicing when his code philosophy made a crucial breakthrough*

I knew that the tire alignment or whatever would take some time, so I had brought my laptop to work on my project in the meantime. To this end, I seated myself in the dealership's waiting area, working from my laptop without a wifi signal. It's a strange place to consider yourself "off the grid", what with my phone still having internet (basically necessary, as I wouldn't have gotten nearly as much done without being able to reference some old lessons and discussions). For that matter, there probably is a "waiting room wifi" that I could have accessed; perhaps I just needed to ask someone. In fact, as I'm writing this a part of me is convinced that the wifi instructions were sitting on a wall somewhere. Perhaps directly behind my seat for maximum irony. Or maybe directly in front of my seat for...also maximum irony. But the point here is that as far as my local repo was concerned, Github was out of reach.

It was in that git-deprived moment that I had placed myself, working on my project while my car was tended to. This particular coding session revolved around Location and Character. There is an aesthetic about these classes. Their models, views, and controllers are all near mirrors of each other, as they are both creations of a Writer and they are both halves of a Haunt. This meant that I could spend a long stretch of time trying to figure out how I would want something to work through Character, and then mere seconds replicating it in Location. But I had to keep in mind the risk of losing all my work (in the wild event that my laptop exploded I guess) which encouraged me to make more frequent commits than usual this time around. And so later, when I finally reached wifi again, `git status` told me I was 5 commits ahead of the master. And so it clicked.

In what way could I use this distinction between commits and pushes? Commits could be the steps I take up the hill, stable or not, but the push would be the assertion that I had made it to the next valley.

Now I try to add files to my commits individually so I can mentally keep track of what I changed in each. And often I'll have many updated files that, thought I worked on them concurrently, I want split into multiple commits rather than a single one, to reflect progress on different fronts of the application. For instance, establishing authentication and preventing propogation of bad data required safeguards in mostly the same files and methods, so I was working on them concurrently. However, as actual concepts they are more distinct, and my approach to solving them also differed (using Sinatra's prebuilt methods for data-checking but building my own code for authentication), and so I broke the work up into two different commits, which I pushed together (as my mentally logged "safeguards session").

UNFINISHED EDGES

To continue to the reaction analogy, and with the knowledge that code can always be refactored to better practices, you could say from a certain point of view that no program ever reaches the end of the hills. That there is always another better stable state over the next crest, even if your original goals are all finished. The Usual Spot, however, is definitively and absolutely *not finished*. And I have left my progress frontier rather plainly for anyone to see.

Characters and Locations have a Story and Image attribute that a Writer can fill on Create or Update (as optional inputs on those views), but there is no actual view to Read this information. These are integral not to the structure of the code (and so I deemed them unnecessary in terms of completion for the assessment) but rather to the user experience (failing to actually serve as a collaborative world-builder until they are implemented). However, even these are not loose strands threatening the stability of the program. All levels of MVC account for their presence, and at no point do they interfere with any completed processes or routes. And every other frontier (my hacker.erb could have more targetted feedback) is likewise. So I still say this is a stable state even as a work-in-progress; the ball will not roll backwards.

Stop by https://github.com/KalMegati/the-usual-spot and check out The Usual Spot. Bring some friends to really get the ball rolling.
