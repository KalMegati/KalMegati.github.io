---
layout: post
title:      "Project 3 - Ruby on Rails"
date:       2020-03-17 06:15:18 +0000
permalink:  project_3_-_ruby_on_rails
---


And from Cyberpunk back to Fantasy...but a different kind. Today we're getting old school as I reference E. T. A. Hoffman's story *The Nutcracker and the Mouse King*, later adapted into Tchaikovsky's ballet *The Nutcracker*. Herr Drosselmeyer 


CLOCKWORK

INHERITANCE

A holdover from The Usual Spot is that Location and Character are nearly identical classes; Drosselmeyer adds a new element in the Faction, which itself is only slightly more differentiated from Location and Character. With The Usual Spot I simply copied

It was actually Rails convention, ActiveRecord convention in fact, that tipped me off to the solution. In order to use ActiveRecord's methods a controller must inheret from ActiveRecord::Base. But rather than each controller calling directly, the intended MVC setup is for all controllers to inheret from a single top controller, `ApplicationController`, which alone makes the call to ActiveRecord. Rails extends this to the models as well, with each inheriting from `ApplicationRecord`. There is an incidental advantage to doing this that is almost never explicitly brought up or required in the labs: any methods defined in these intermediate superclasses will be inhereted just as ActiveRecord methods will be.

So if I want Location, Character, and Faction to have many similar methods and relationships, I could make a superclass encompassing them to keep my code DRY. Enter `Entity`.

The Entity class refers to entities which exist in the story; the Noble Hero, the Magic Spring, and the Demonic Cult are all entities in the story, yet also have unique relationships within themselves (a group has members, and so a Faction `has_many` characters). 

With this in mind, I would need to write my methods for Entity and EntitiesController in a sufficiently flexible way that they would be able to handle the small differences between actions for the three different models. I built a number of helpers to assist this.

Convention in Rails is that `new` will start with instantiating a new instance of a class, but how to choose the right subclass among Entity? Well the path begins with the request, and the request will dictate which of the sub-controllers is used. From there, it is a matter of using the name of the controller to yield the corresponding model. Fortunately the three relevant terms ("character", "location", and "faction") follow the same pluralization conventions, and so Drosselmeyer can make the conversion through string manipulation (chopping off "Controller" and singularizing it).

Making dynamic adaptable route helpers and strong params callers worked similarly, to the point that I was able to 

NESTING

There are no birds of particular importance in the Nutcracker. However, Herr Drosselmeyer is also the namesake of a character in Ikuko Itoh's ballet-themed anime Princess Tutu. The mad reality-bending writer D. D. Drosselmeyer grants a lowly duck the ability to transform into the beautiful swan Princess Tutu. This was the actual Drosselmeyer I was thinking of when I named my project. And speaking of birds, nesting.

When operating within Nested Routes howeever, it becomes necessary to change some of the assumptions that we, and Rails, makes of our code.



A Setting `belongs_to` a Writer; a writer must write the setting 

But in the context of a collaborative work, a Setting also `has_many` Writers. The Factions and Characters that shape the story are also elements of the Setting's writing, and Factions and Characters can be created by Writers other than the creator of the Setting.

Drosselmeyer names the many writers of a Setting as "cowriters", with a


