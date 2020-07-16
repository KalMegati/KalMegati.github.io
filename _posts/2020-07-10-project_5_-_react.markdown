---
layout: post
title:      "Project 5 - React"
date:       2020-07-10 17:23:26 -0400
permalink:  project_5_-_react
---


I am a programmer, and I am also other things. Today (or like, this week; I spent a while on this post), I am a programmer and an actor.

### Blocking

Theatre is determined by the stage. "Blocking" refers to the placement of actors as they move about the scene. The basic theory is that different parts of the stage serve different purposes, largely based on the audience's view, and so a work can be made stronger by keeping these purposeful stage positions in mind when directing. If your lead stands at centerstage and looks to rightstage, the audience will likely follow the lead's sightline, allowing them a perfect view to see another character make their entrance from rightstage (or distracting them from the character making their entrance from leftstage).

The same consideration of placement must be made for the browser. Where you put navigation links, information, and pictures of varrying size will affect how a user views and uses the page that is being shown. A site's top-level navigation is correspondingly often found at the top-left of the page, because this will place it right beneath most browser's url bar, which helps to group all navigation concerns in a consistent part of the screen.

React makes this especially easy with its components, modular chunks of independently written code that can be slotted together to build the user interface. Rather than needing to write out all the navigation headers in contiguous javascript, they can be made into components and then lined up in a div placed at the top of the screen. This has another benefit under the hood: someone who is reading the underlying code can more easily follow the construction of the page if they see that the "Navbar" component is rendering a "Settings", "Login", and "About" component, as opposed to an unsectioned scroll of JS elements.

Convention further separates components into presentational and functional (often called containers). The idea here is for containers to include complex logic, server requests, and other managing of data while the presentational components can simply be fed information from a container and only need to be written to display. The metaphor gets a little flipped here I'll admit: the dynamic actor is placed within static scenery, but with React the static presentational component is placed within the dynamic container.

My project sections components even further with my top-level containers, the screens. While containers are commonly thought of with respect to the component they contain, I made my screens with consideration to the browser around them. Their purpose is less to pass information down to their child elements and more to section off the display into a straightforward user interface. Tabula Rasa has three primary screen partitions: the Navigation Bar on top, the User/Character Menu to the left, and the Main Display Screen taking up the rest of the screen. There's a deliberate flow to the visual here: 

Clicking on any navigation, from the top bar or the left menu, will change what is displayed on the Main Screen; because the Main Screen takes up the largest portion of the app view and dominates centerscreen, this means the user's attention is instantly called to the new display. The Navbar and Menu, though both control navigation, are separated with respect to the application's metanarrative. The Navbar on the outside explains the application and provides a gateway into it (through logging in or toggling different styles for better viewing), while the Menu shows crucial elements within the app itself, of users and the characters they have created. And this is reflected in the required movements of the cursor: to see different information, you look to the side (to the Menu on the left); to see information differently, you must go above the action (to the Navbar on top) before coming back down.

### Audience

Theatre is determined by the audience. All manner of creators have their visions molded by what they want to give to their audience. This is particularly important as a designer of consumer applications, because the application is going to be used by many people largely divorced from what the designer considers is the ideal setting; while a director can be assured that their audience is arranged in angled auditorium seating for established show times, the programmer must anticipate thier users lounging on their couch, seated at a cafe, or any number of impromptu settings where the user pulls up the application.

So what is the intended user experience of Tabula Rasa? As titled, Tabula Rasa is meant to be a "blank slate". A surface upon which the user has as much control as they would if they were drawing on a sheet of paper. There are already many character sheets for various games that are functional for keeping information organized, but their rigid structure can somewhat push the player to curtail their ideas in order to better fit the template. The reason there are so many different standards of character sheets, even for the same game systems, is because there are many different players with different needs and desires. This is my audience; they are not legion, but rather omnifrarious. Tabula Rasa means to provide a way for users to make their own character sheets, as abstract or as specific and with all the boxes and subdivisions they want or don't.

This brings us to the Element component. At it's most basic, it is derived from the standard "Card" Bootswatch html element, with a header and body text. My thought was to break this card up into a user-chosen number of segments, such that this one visual would be able to account for both deep and streamlined systems, from Pathfinder's Feats (which expect an integer for level, a feat name, prerequisites, a flavor description, and a mechanical description) to Fate's Aspects (which are simply a short descriptive phrase).

And a crucial personal requirement was that Element be a presentational component. It would display only based on the information it received as props rather than requesting it. However, this ends up demanding a bit more complexity in the render statement than you would expect of a presentational component, as each text space had to be expressed not just as an element but rather as a function that would conditionally display the text. So in addition to the displayed descriptions to fill out the card's text spaces, Element would also need to take in props that would allow it to determine weather or not to even display those text spaces at all.

I found it easiest to determine the active text spaces with an array, but a Rails backend does not store objects with arrays as attributes. This meant sending the activity array to the server as a joined string, and then destructuring the string once it came back to the client. 

This requires a considerable amount of communication within the component. 

Though the page previews the element's appearance, the request to create the element is not made until the user submits the form.





Thinking of a text space as its compositional elements (that is, the text and the space), I felt it would be most intuitive to have control over these sectioned accordingly. Related to blocking above, the Element preview is placed between the text inputs and the space checkboxes. This means that any changes you make to the respective input will be visible directly to the left or right of the input, rather than on the opposite side of the screen (if I 

### Voice

And ultimately, theatre is determined by the actor.


There's a 

Again, React was here to help me, but not quite by design.

This required recontextualizing a component not as a package of JS script (slotted into a functional code), but rather as a JS file (within a file directory). As coded components, each Style is functionally identical. It accepts no props and only renders the App component. But as a file, each imports a different Bootswatch CSS file to serve as the display's aesthetic. So by implementing a a switch case between these Styles in a high level of the application, I could have the app displayed in entirely different aesthetics that users could select dynamically.

Of course, trying to treat components in this unconventional way had its struggles. Once a file is imported, it remains even if the component that imported it is unmounted. This is because, while an unmounted component will no longer show its render, the import command outside of the component code has still executed once, and so that file is here to stay. But this would not stop a new CSS file being imported if the Style was changed, meaning the App will try to style itself using all of the CSS files installed so far. Priority will go to the last one installed, but there are still many areas of non-overlap that will make, for instance, a lone Slate style look different from a Slate style with a Cerulean style before it. Imagine the Bishop of Digne offering Jean Valjean shelter in his saintly church, but the orchestra is still blaring the authoritarian "Look Down" from the previous scene. Not great. So I had to make sure that the aesthetic, or CSS file, from the previous scene was cleared away before introducing a new one. And unfortunately for Tabula Rasa, I could only accomplish this by requiring a page refresh.

But this presented further complications: refreshing the page would also refresh the Redux Store, which I had previously thought to use as the source of truth for the current user. 

I've seen well enough explanations for why I shouldn't be using Local Storage for sensitive user information...or not enough, considering I've done so anyway.

Explore before refining.



The character's voice is important by concept.

But it is just as impossible to remove the actor's voice. An excellent performance is just as much the work of the actor's portrayal as it is the character's writing, even if this is not so visible to the audience.

Kenneth Branagh's Hamlet, David Tennant's Hamlet, and Ethan Hawke's Hamlet (yeah I saw that one too) are all largely informed by the actors that portray them.

So what is my voice, or perhaps my vision, for as a colorblind coder?

### Arc




This is why it was so important that for this project I be an actor. Because when I design applications, I will not be designing for a static checklist; I will be designing for a dynamic audience.

And so I present Tabula Rasa, a blank slate. I can't give you a further heading than that, because I think by concept I'm not supposed to. This experience is yours to enjoy.
