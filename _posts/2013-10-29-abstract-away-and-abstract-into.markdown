---
layout: post
title: "Abstract Away &amp; Abstract Into"
date: 2013-10-29 17:30
comments: true
categories: 
---

You're about to use a third party library in your codebase.  Every good developer known that the first thing to do is create some domain specific abstractions by sticking a layer of objects over the top.  This encapsulates the third party library and keeps is away from the client code.  

This is the typical layering approach drummed into developers in their first few weeks in university/on the job/in training whatever.  Leaky abstractions are bad okay?  Lock them away behind a wall of bespoke interfaces and let nothing through.
Our own code becomes simpler by using a narrower, more domain specific interface in higher layers.  It also makes testing a lot easier as we avoid testing someone else's code (which is a bad thing).

This approach is what I call Abstract Away because, effectively you are distancing yourself away from the third party library by creating new abstractions.  

One of the big problems (and benefits) of abstracting away is that the third party library is now inaccessible except via the abstractions.  Any power in that library, not covered by your own abstractions, is also inaccessible.  It's also a rather expensive thing to do and you essentially end up duplicating a lot of the underlying libraries concepts.  And as helpful behaviours of the library are too distant to discover you lose opportunity costs.

The alternative is to Abstract Into.  This takes the opposite approach by creating abstractions using the existing libraries interfaces and building on them in a complimentary fashion.  The abstractions and the existing library sit as siblings in the same layer rather than one over the other.  Almost as if they were just another set of abstractions in the same library. This is a lot more powerful for the consumer because they are no longer barred from the underlying library's power giving them opportunity to do things beyond your initial intent.

Abstract Away is very controlling and is about limiting, or protecting the client.  Abstract Into is very liberal and is about provide extra value _alongside_ the original library.

Clojure, as a language, encourages and uses a lot of Abstract Into over Abstract Away.  A great example of this is [Compojure](http://Compojure.org).  Compojure abstracts into the [Ring](https://github.com/ring-clojure/ring) web application library to provide functions for building routes.  However it is really very difficult to know where Compojure starts and Ring ends (or vice versa).  This is because Compojure doesn't attempt to push Ring away from you, instead it provides helpful patterns.  This is incredibly powerful as the user can still harness all the power of Ring.  It also makes Compojure very composable with other libraries and easy to add your own abstractions.

An example where Abstract Away is used where Abstract Into would have been appropriate, in my opinion, is the javascript graphing library [Rickshaw](http://code.shutterstock.com/rickshaw/).  Rickshaw builds on top of the amazingly powerful and versatile [D3.js](http://D3js.org) library by providing convenient and simple abstractions in a dsl fashion for building charts. This is fantastic and the abstractions provided are very helpful allowing you to rig up attractive charts in no time.  However, although it uses D3 you would have no way of knowing from the Rickshaw API, the only hint is from the docs. All the power and loveliness of D3 is locked away from you.  The fact that it is built on top of D3 is utterly irrelevant.  So, when you reach the limits of what Rickshaw can do what are your options?  None, but to throw it away and rewrite in D3.

Libraries that have been abstracted into don't suffer from this problem.  If you hit their limits you just abstract into even more.  Libraries can be composed from other libraries.  This sounds similar to a plug-in model but its actually very different as you aren't restricted in the same manner.  If you look at Ring there is no plugin model.

One of the downsides of Abstract Into is that it requires a high quality library in the first place.  Preferably one that has considered being extended in this way.  Of course many libraries make this claim with their heavy use of interfaces etc. but how many _actually_ match up to the promise in practice?

Abstract Away does have its uses however.  It is very good at containing bad libraries by acting as an anti-corruption layer.  It also makes testing simpler.  Abstract Away also tends to be good for wrapping multiple libraries with a common interface. [boto](https://botocore.readthedocs.org/en/latest/) or [fog](http://fog.io) follow this method by providing a cohesive set of abstractions over multiple cloud providers to create an ubiquitous API.  Of course this could be also accomplished using Abstract Into but it is far more complicated and can get messy rapidly.  It is also very useful for scenarios where you may wish to change the underlying library without disruption to the client (rarer than you think: I doubt Rickshaw will be dropping D3).  

Abstract Into, on the other hand, is great for enhancing existing library and leveraging them to build new abstractions.  A standing on the shoulders of giants approach.  However it is dependant of high quality libraries in the first place and has an element of 'vendor lock-in'.  I think the proliferation of low quality libraries over the last few decades is one of the reasons why many developers have established the habit of using Abstract Away when Abstract Into would be better suited.

So, next time you are writing code with a third party library to create new abstractions think carefully about whether it would be better to Abstract Away of Abstract Into.  Also, when writing your own libraries design them to promote Abstract Into and allow for composition.