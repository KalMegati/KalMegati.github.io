---
layout: post
title:      "Project 3 - Ruby on Rails"
date:       2020-03-17 02:15:19 -0400
permalink:  project_3_-_ruby_on_rails
---


And from Cyberpunk back to Fantasy...but a different kind. Today we're getting old school as I reference E. T. A. Hoffman's story *The Nutcracker and the Mouse King*, later adapted into Tchaikovsky's ballet *The Nutcracker*. Drosselmeyer is a Ruby on Rails application for collaborative storytelling and setting organization, intended for multiple writers working together in a group or server.

CLOCKWORK

In Hoffman's work, Herr Drosselmeyer is the inventor of the eponymous nutcracker and many other clockwork marvels. And much like clockwork, the gears of the Drosselmeyer application have many interlocking relationships they follow in the Rails framework.

A Setting `belongs_to` a Writer; a writer must write the setting. But in the context of a collaborative work, a Setting also `has_many` Writers. The Factions and Characters that shape the story are also elements of the Setting's writing, and Factions and Characters can be created by Writers other than the creator of the Setting. And in the opposite direction, a Writer `has_many` Settings that they have created from scratch, but they are also associated with the settings of other writers if they have written characters or factions with them, meaning that a Writer also `has many` Settings, but in a different sense than the `has_many` Settings that they created. So how would I construct the relationship between Setting and Writer such that I could collectively use Factions and Characters as a join table, and also get around the issue of multiple definitions of a `#settings` method for Writer?

The trick to the latter lies in "aliasing", or referencing a join table but providing a different call. And with that done, the former becomes trivial; simply adding the `has_many :through` arrays from Factions and Characters together and filtering out repeated results. Drosselmeyer names the many secondary writers of a Setting as "cowriters". Meanwhile, the many settings that a Writer has work involved in make the "portfolio".

INHERITANCE

Herr Drosselmeyer's godchildren are impressed by the toys, but only the heroine Clara takes to the Nutcracker, and so Herr Drosselmeyer gifts her the construct. Herr Drosselmeyer may be the inventor of the toy castle, but it is Clara's imagination that dreams up the events of the story. Let's talk about inheritance.

In a whimsical sense Drosselmeyer is inheriting its ideas from my previous application, The Usual Spot (built in Sinatra). But there is a mechanical lineage as well: a particular holdover from The Usual Spot is that Location and Character are nearly identical classes; Drosselmeyer adds a new element in the Faction, which itself is only slightly more differentiated from Location and Character. With The Usual Spot I simply wrote the entirety of Character and CharactersController and then copied the text over for Location and LocationController, a disquietingly WET solution. This time around, I had a mind to be DRYer about things

It was actually an older lesson, ActiveRecord convention in fact, that tipped me off to the solution. In order to use ActiveRecord's methods a controller must inheret from ActiveRecord::Base. But rather than each controller calling directly, the intended MVC setup is for all controllers to inheret from a single top controller, `ApplicationController`, which alone makes the call to ActiveRecord. Rails extends this to the models as well, with each inheriting from `ApplicationRecord`. There is an incidental advantage to doing this that is almost never explicitly brought up or required in the labs: any methods defined in these intermediate superclasses will be inhereted just as ActiveRecord methods will be. So if I want Location, Character, and Faction to have many similar methods and relationships, I could make a superclass encompassing them to keep my code DRY. Enter `Entity`.

The Entity class refers to entities which exist in the story; the Noble Hero, the Magic Spring, and the Demonic Cult are all entities in the story, yet also have unique relationships within themselves (a group has members, and so a faction `has_many` characters).  With this in mind, I would need to write my methods for Entity and EntitiesController in a sufficiently flexible way that they would be able to handle the small differences between actions for the three different models. I built a number of metaprogramming helpers to assist this.

Convention in Rails is that `new` will start with instantiating a new instance of a class, but how to choose the right subclass among Entity? Well the path begins with the request, and the request will dictate which of the sub-controllers is used. From there, it is a matter of using the name of the controller to yield the corresponding model. Fortunately the three relevant terms ("character", "location", and "faction") follow the same pluralization conventions, and so Drosselmeyer can make the conversion through string manipulation (chopping off "Controller" and singularizing it).

Making dynamic adaptable route helpers and strong params callers worked similarly, to the point that the only code I needed in my specific controllers was their respective strong params. The models were more difficult: I failed in my attempts define my relationships or validations in a DRY way. I was correct that keeping `validates_uniqueness_of :blurb` in my Entity model would cause Factions and Characters to both validate for this aspect. However because the code was in Entity, Rails took this to mean that it would need to validate the uniqueness of the blurb against objects in the `entitites` table (which did not and was not supposed to exist). To this end I simply ended up splitting validations into each of the models separately.

NESTING

There are no birds of particular importance in the Nutcracker. However, Herr Drosselmeyer is also the namesake of a character in Ikuko Itoh's ballet-themed anime Princess Tutu. Reenvisioned as a mad reality-bending writer, D. D. Drosselmeyer grants a lowly duck the ability to transform into the beautiful swan Princess Tutu. I'll expose myself as a little uncultured and admit that this was the actual Drosselmeyer I was thinking of when I named my project. And speaking of birds, nesting.

The Usual Spot had a particular failing in its inability to separate fictions. All characters were indexed in the same list, meaning you and your cowriters would either need to only ever use an instance of the application for a single story, or you could compile multiple stories and end up with Darth Vader, Sherlock Holmes, and Conan the Barbian hanging out on the same list. Drosselmeyer expands this domain by covering multiple settings and consolidating story elements into the settings that they belong to.

This is achieved through nested routing. There are no bare indices for Entity objects, instead only having views within their respective Settings. I debated also nesting Entities within Writers, but I felt that having multiple urls reaching the same information, even if information would remain consistent, would be farther from single-source-of-truth practice. Instead, a Writer's show page will display links to the works they have created, but those routes will take the user to the Setting-nested show pages.

When operating within Nested Routes however, it becomes necessary to change some of the assumptions that we, and Rails, make of our code.

The default `form_for` will intelligently find its path based on the object given to it, intuiting both its method (`patch` if the object has an `id`, `post` if it doesn't) and its action is pathed to the index or `objects_path`. But if your object's index only exists nested within another object and an unnested object index route doesn't exist, then Rails will be unable to find the path. So for nested views the path needs to be given explicitly, for instance as `setting _factions_path`. Or in Drosselmeyer's case, `setting_entities_path`, an accordingly-named helper which programmatically chooses the proper entity path.

But if a Character must belong to a Faction, even though Character views are not nested within Factions, then we also need some measure to ensure that a Writer does not try to make a Character in a Setting with no Factions. To solve this, we can nest a form for a new Faction within the form for a new Setting, making it impossible to create a Setting with no Factions.

The `story` attribute for all my objects is not required as it is assumed in many cases that a Writer will have only a basic idea (the `high concept` or `blurb`) of what they want to do with the element when they first make it. However, it is almost definite that a Writer will have at least one Faction in mind when creating a Setting (even if that Faction is given the working title "good guys"). I also feel this is important to establishing a good look for a Setting show page (giving it some amount of linkable content). To help expedite this for a Writer who cannot think of many Faction names immediately upon making a Setting, 2 of the 3 factions asked for upfront are provided with defaults of "Neutral" and "Disputed", generic enough terms that can best nested into any story while also giving the Writer space to replace them if they have more Factions planned out.

This also presents a benefit for the interface of the new Character form: the select box for a Faction will always have multiple options, self-evidently showing the Writer how these options will be lain out and selected. The other neat feature of a nested form is that it will carry over validations. So my new Setting form will mark and present an error if the nested Faction attributes fail validation.

MAGIC

The Nutcracker ends with Clara waking from her fantasy and assuming it was a dream, only for 'Drosselmeyer's nephew from Nuremburg' to arrive at her house...a young man identical to the Nutcracker's true identity as the Prince of Dolls. Was Herr Drosselmeyer's clockwork in fact an instrument of magic?

"Magic" is a word that has been recurring for these two months of working with Ruby on Rails. And I have to agree: Rails Magic is wonderful. With generators I could remake the entirety of The Usual Spot in a couple of hours, and with helpers involved it took less than half the former's character count to do so. With its conventions, the Rails framework even helps to organize the pieces of a project; by retracing and understanding the routes that rails provides you can induce alternatives that may work better for your goals.

And Rails Magic is terrible. With prewritten scripts doing so much of the work for you, it's easy to get lost and not know for sure where information is coming from or what is calling it. I at one point needed to throw three separate `pry` lines into a single request chain (two in the same controller action at that) just to keep track of how information was being changed and sorted by Rails behind the scenes. For that matter, try throwing a `pry` into the middle of a controller action and ask for `self`; the instance returned is ridiculous!

So appreciating Rails Magic as best you can is quite similar to suffering Rails Magic the least you can: peer past the magic and follow the clockwork.



*Thus I give you Drosselmeyer. A place to archive the magic of your stories and fictions, in the clockwork of your Settings and Entities.*
