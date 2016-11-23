---
layout: post
title: "We're not special"
date: 2013-01-22 10:13
comments: true
categories: 
---

"A key differentiator of highly productive teams is the ability to identify what is core to their domain, and thus brings them competitive value, and what is commodity, in order to focus their energies on solving core problems and not commodity problems."

Most of us, at some point in our career - especially those that have laboured in 'enterprise' - would have experienced working in teams where most of the energy seems to go into debugging, patching and developing the highly customized, and specialist ORM, or web framework, or messaging system, or unit testing framework, or...  To the sane amongst us it's an exercise full of futility and waste.  These custom packages lag dramatically behind what's available, often for free, on the internet and seem to suck up velocity like a child with a milkshake, seemingly immune to the inevitable 'brain freeze'.  

All to often, the reasons for teams investing in solving commodity problems is a misconception that they are actually solving a core problem.  It is argued that a custom ORM is required because the way the team do databases is fundamentally different and therefore a unique solution, particular to their own particular situation, is required.  Where as the truth is often that the system has been built is such an unnecessarily arcane way that it gives all the appearance of a special situation when in fact it is simply an inappropriate one.  Solving problems made by special thinking requires special thinking and it's turtles all the way down.

Identifying the commodity isn't always so trivial as choosing an ORM and building your system around it.  Sometimes a team finds itself working in a new field of technology that they have little experience in and, through ignorance and the nature of empirical discovery, it is only after months of investment into a custom solution for a commodity problem that you discover the truth.  

Sometimes, however, you may find that you are special after all.  In those rare cases where there are commodity solutions it may be to the teams advantage to ditch it and build there own.  This may be because:

*  it doesn't meet your design/architectural principles - if simple testing is important and all the solutions on the market fail to make that simple then it may be worth while rolling your own
* it gives you a business advantage - pushing the technological boundaries in a commodity area improves your brand somehow 
* it enables you to learn - if your system is heavily tied to a particular technology then rolling your own may allow you to make discoveries about that tech that provide value to your product
* the effort to adapt is greater than building something ourselves - if you are working on a legacy app that had never be built to consider the approaches used by commodity packages you may find
* the commodity doesn't yet exist -  if you are very cutting edge, a commodity solution has yet to appear and you are stuck rolling your own.  After all, at one point there were no CI servers, no unit testing frameworks, no mocking libraries
* you genuinely believe you can push the concept forward - JMock existed but that didn't stop Szczepan coming up with Moqito and improving the world for the rest of us. 
 
The truth is, for ninety percent of the projects none of the above will apply.  The commodity problem of MVC web frameworks has been solved, logging has been solved, deploying rails apps to the cloud has been solved. Is your web/logging framework/cloud solution genuinely going to compete?  If you truly believe this to be true then start by commoditizing it now - either by building a product or open sourcing it - otherwise it's just a pipe dream and you are doing nothing more than developing another custom commodity solution.

In some cases you may genuinely discover that what's on the shelves isn't quite right.  Every solution only always leaves you one step away from reaching your goal.  For example, you're using gdash to pull in all your graphite graphs but you wish to mix in AWS cloudwatch graphs as well.  Rather than building a separate, brand new dashboard solution, consider forking gdash and enhancing it to pull from cloudwatch as well, then contribute back.  For the majority of problems this will be less effort than rewriting your own solution from scratch.