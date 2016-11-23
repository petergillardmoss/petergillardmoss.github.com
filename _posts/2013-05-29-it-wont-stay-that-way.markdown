---
layout: post
title: "It won't stay that way"
date: 2013-05-31 17:10
comments: true
categories: 
---

Every good developer knows that trying to design your system around future requirements is  wasteful.  [You Ain't Gonna Need It] [yagni] tells us that we should focus on the functionality we need _now_ and not that which may occur in the future.

Every good developer knows that we should only model what we are certain about and we can only be absolutely certain about _now_.  

To keep the code simple, to keep the code lean, every good developer works to model what we know _now_ as accurately as possible.

But what if I was to tell you that this is wrong?  What if I was to tell you that designing your code around _now_ is potentially as futile and wasteful as designing your code around a hypothetical future state?

## _Now_ is always invalid
The problem is _now_, as a state, is continuously shifting.  You cannot model _now_ with any degree of accuracy.  The best you can do is attempt to represent an interpretation of the information you have at a specific point in time.  And it's going to be wrong.

Any model of _now_ is constantly being invalidated.  Invalidated by the quality of information you have, the next line of code, the next story, the next bug, the next product owner's meeting, the next user's action, the next security bug in rails, the next learning.

Trying to produce code that represents _now_ is a losing battle under such a barrage.

## Model change
What you can model, however, is a system under change.  

Good systems, that just keep going and going, in a manner that is cheap to maintain and extend, don't model _now_, they model change.

## Future capable
Modelling change is about placing the capability of delivering future versions at the heart of the system.

Each delivery is not only a representation of _now_ but opens paths to deliver the next set of changes and those changes have the capability to deliver the changes after that.

## Use the future to test your design
The future is an inevitability even if it's form is not.  But those hypothetical future scenarios still have their uses.  

They are great ways of testing your design.  Throw future scenarios at it and see how it will cope.  What _could_ happen next?

You don't want it to have _solved_ the hypothetical future scenarios but you do want the design to have the capacity to adapt to them.

If you throw a _likely_ future change at your system design and you discover that it will be expensive, cumbersome or even dangerous under those circumstances then you have failed to design for change.

This is, of course, a flawed process.  We're always going to miss something.  We're always going to get something wrong.  But it is the best process we have.

## Don't over-engineer, don't under-engineer
Both over, and under-engineering are symptoms of placing too much emphasis on _now_.

If we believe that our designs are going to last indefinite periods of time we become tempted to over-engineer.  We create abstractions that aren't designed to change but are based on the assumption that today's knowledge and understanding are both accurate and permanent.  This creates a system which is brittle and difficult to change.

If we consider _now_ the ultimate goal, without considering the future change, we become tempted to under-engineer.  We dismiss the future out of hand and accept overly naive solutions to problems that are soon to be invalidated.  The result is a code base that becomes rapidly unwieldy, overcome with technical debt and expensive to maintain and change.

## Source control embraces change
Source control exists purely in recognition of change.  It exists purely to allow change.  

It achieves this by modelling change, by giving you a means to represent and capture change.  It does _not_ model a concept of _now_.  Instead it allows the creation of a representation at a point in time.

Distributed VCS actively embrace this and become all the more powerful for it.

## Continuous delivery
Continuous delivery is a great catalyst for ensuring that you design your system for change.  By it's very nature it is a mechanism for delivering change.  

Teams that truly embrace continuous delivery cannot ignore the future because the future is immediately upon them.

Teams that practice continuous delivery think in terms of change.  Every checkin, every architectural decision is not simply about _now_ but also how to deliver the changes after that.  To achieve this they try to keep changes as small, but as functional, as possible.

## It won't stay that way
When going to add that line of code tell yourself You Ain't Gonna Need It, but also tell yourself It Won't Stay That Way.

When you write your code be aware that the next story, the next production event, the next standup, has the potential to invalidate that line of code.  Within moments that line could be deleted, it could be modified, it's behaviour could be changed by something that gets put above it.

Think of your code as cutting a path to the next set of changes rather than just delivering what is in your current story.  This way you will build systems that will quietly adapt and evolve of time.  


[yagni]: http://c2.com/cgi/wiki?YouArentGonnaNeedIt