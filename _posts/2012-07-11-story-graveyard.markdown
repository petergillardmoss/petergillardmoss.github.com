---
layout: post
title: "Later: a story graveyard?"
date: 2012-07-18 10:10
comments: true
categories: 
---

In a [previous post](/blog/2012/07/09/now-next-later/)  I discussed how we divide our backlog into _Now_, _Next_ and _Later_.  One of the things we've observed is how _Later_ seems to be the place where stories go to die.  That's not to say that some stories eventually make it into _Next_ and eventually _Now_ but for the vast majority of them sitting in _Later_ is a terminal condition.

This raises a number of interesting questions: what should we do with stories that are likely to live their lives in _Later_? and why do we generate so many stories that will never be implemented anyway?

It makes sense to start by looking at why we generate so many stories that are unlikely to get implemented.  Looking at a recent project nearly half of all stories were unimplemented at the time the project was considered complete.  In a [recent article](http://www.joelonsoftware.com/items/2012/07/09.html) Joel on Software made a similar observation.

So what's going on?  Why does it appear that we create a story that doesn't get implemented with every story that does?

There are two opposing forces at play: the need to brainstorm and capture as much information to allow us to understand what we're building and the need to keep scope as small as possible.  Both activities are continuos: as we discover we learn about all the things we've missed, as we discover we learn about all the things we don't need.

These opposing forces come together to form a decision point.  When writing software we are continuously rationalising all the different options: can we get away with Paypal only and forget about all those credit/debit card stories for now? what if we save to the filesystem and not worry about a db, can we get away with that?  We plot out all the different options (and to do this we create cards) and, treating each one as a hypothesis to be proven, we attack them from different angles until we find the one that stood the best.  The ones that stand the test get implemented, those that don't go to the _Later_ column to die.

Except they might not.

The nature of software means that those decisions don't stand indefinitely, they only stand while the propositions that proved them hold. Using Paypal only made sense when the goal was to test the market with a small set of users; if we change the goal to maximise sales then we'll have to go back and revisit the decision.  That means that those stories we stuck in _Later_ may, at some point in the future come back to life when we revisit those decisions.

A key question is whether we need to keep those cards or whether we should simply regenerate them when we re-evaluate our decision?  The world of electronic data where storage is cheap has fostered a conservative attitude where preservation is the default.  We really don't like to delete things.  
 But is there any value in having the original reasons to hand when when we re-evaluate a decision?  What influence will they have, or should they even have any?  

There are problems with keeping information hoping that we will make use of it later on.  The first problem is that having the information doesn't mean we will necessarily unearth it again when we come to challenge our decisions.  To even know it existed is to rely on memory and the team may have lost that memory one way or another; even if the team does remember its existence it may be buried deep under stacks of noise that means digging it out may not be so simple.

Another question is whether the original information is even relevant.  The decisions represent a point in time and therefore capture the state of the world at that time.  It is unlikely that the entire state held.  So, for example, a decision rejected on the cost of hardware may be made irrelevant by cloud providers for example.  People often describe this phenomena as a form of decay.

There is another variable and that is discovery cost.  Some information will cheap to discover.  Researching a mocking framework for example is a few dozen minutes trawling links bought up by Google searches.  A spike into the suitability of MongoDB however may be a weeks work for a pair.

In which case I would argue that we should capture decisions that are likely to provide a legacy and/or are expensive to rediscover.  But these decisions should be presented in a different format so they can both be found easily and revisited.  Cards that represent cheap decision points, on the other hand, we should leave them to their fate.  Then we can simply archive all old cards to the dark depths and not worry ourselves about them again expect if we wished to go on a nostalgia trip or use their attributes for statistical analysis.
 
