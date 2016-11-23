---
layout: post
title: "Weighing the cost of expediency"
date: 2013-05-14 19:46
comments: true
categories: 
---

Here is a situation familiar to us all: you're working hard towards a release, a story comes up that is essential but its implementation seems expensive especially given the time frames.  One of the devs on the team that prides themselves for their pragmatism offers a cheap workaround.  It's slightly ugly, not something you'd want in the long term, but, the team reasons, it'll do the trick and everyone agrees to clean it up first opportunity, or even better, when the next story touches it.  Sounds like the sensible, pragmatic thing to do so the team agrees.

Except something bugs you about it.  Not sure what but you're flicking through Bob Martin's [Clean Code] [CleanCode] feeling that this isn't right.  Yet the pragmatic dev's reasoning is irrefutable, it's the only sane thing to do. 

A few months later, perhaps even longer, you pick up a story in a similar area and realise that the workaround is still there.  Not only is it still there but it's grown and it's going to take you a _long_ time to pick it apart.  So, the pragmatic member of the team pipes up and suggests a work around…

The above is a text book case of tech debt.  The team wants to get value quickly so it deliberately accumulates some debt in order to achieve it.  Given the situation the value outweighs the debt so it sounds like a good trade off.

## Where the team went wrong
Unfortunately the team's original reasoning is flawed.  When they weighed up the expedient solution vs the right solution they incorrectly attributed cost.  They did this by deferring the cost of doing 'the right thing' and assuming that nothing changes.  This leads to the following incorrect assumptions:

1. The opportunity to do 'the right thing' will still be available or will resurface in the very near future
1. The lifespan of the expedient implementation will be very short
1. There will be little or no side effects from the expedient implementation
1. The cost of doing 'the right thing' will be the same
1. The cost to remove the expedient implementation will be low


The problem is that very rarely are all (or any) of those assumptions correct.  In fact, the only point at which any of those assumptions can be correct are immediately after the expedient implementation has been released.  From that point on each of those assumptions rapidly become increasingly invalid.

The first assumption that goes out the window is that the opportunity will still be available.  The reality is that the only safe assumption is that the opportunity is available only at this moment.  If you don't take the opportunity at the point while the need exists then the need will be removed and thus, so will the opportunity (see how this works?).  You would have to rely on another story to create a new opportunity and you cannot do that: priorities change, demand changes.  The only assumption you can make is, that there may or may not be another opportunity in the future, and if there is you cannot predict when it will be and it is highly unlikely to be soon.  It will also be highly likely that the pressures will be equally great. So even if another opportunity arrises (say another story in the same area) the team may feel that it would be an inappropriate time to fix up old debt.  In fact it is reasonable to assume that if the team takes the expedient option this time round then they are equally likely to make the same decision next time unless a major variable has changed.

This then invalidates the second assumption, that the lifespan of the expedient implementation will be short.  With any changes you make to software you must always assume that they will be long lived.  Why?  Refer to the first refutation.

You must consider the expedient implementation part of your system design: because it is.  I think people don't, they file them in another part of their brain away from the real system.  The reality is that it will become a part of your system equal to any other part.  This means that all future design decisions in related areas will be affected, in varying degrees, by that implementation.  This invalidates the third assumption: the expedient implementation will create definite side effects.

As the expedient implementation is long-lived and has side effects on the system design, this means that changing the code to do the right thing would have an increased cost.  All those design decisions that were made to compensate will require change to align with the right design.  This not only invalidates the fourth assumption but the fifth: the expedient implementation must be detangled from the system design and it will be costly.

## The result
Interest on the technical increases rapidly over time.  Mainly because tech debt works on a compound interest basis (due to the highly interwoven nature of software).  Tech debt attracts other tech debt, it is like a cancer.  Once you make one expedient decision you then find yourself making placing another expedient implementation to compensate on top.  Repeat over and over.

## The correct reasoning
So, what are the correct assumptions to make when weighing up these decisions?

1. It is unlikely the team will have the opportunity to fix this anytime soon
1. The expedient implementation will be long lived
1. The system's design will change to reflect the expedient implementation and will affect the quality of the design in related areas
1. The expedient implementation will become increasingly more costly to remove
1. The correct design will become increasingly more expensive to implement

Of course, it may be perfectly valid to still implement the expedient solution especially if the value far outweighs the cost.  Just be sure that you've done your maths correctly otherwise you'll be in for a nasty surprise :)

[CleanCode]: http://www.e-reading-lib.org/bookreader.php/134601/Clean_Code_-_A_Handbook_of_Agile_Software_Craftsmanship.pdf