---
layout: post
title: "Sometimes you need to establish some standards"
date: 2021-02-12 08:20
comments: true
categories: 
published: true
header-img: img/overflowing-bin.jpg


---
The bins are a bit of a problem in my house. My wife, son and I throw stuff in the various kitchen bins until they can take no more. They overflow, cascading rubbish onto the floor, and demanding immediate attention. 

This most often happens when doing something urgent like cooking dinner. Under pressure our only option is to work around the bin by stacking the rubbish up elsewhere. And yet again we put "sorting out bins" in the “deal with later” pile.

The truth is we have no standards. At least not when it comes to the bins. The bins are in constant firefighting mode. Even worse they are impacting other activities like cooking.

Does this sound familiar? And I don’t mean for bins. You might have similar experiences in your day-to-day work and delivery teams? The build that is often in a broken state when you need to do an emergency production fix? Or how urgent defects keep interrupting that shiny new story?

![1. trouble-shooting. 2. gap from standard 3. target condition 4. open ended](/img/four-types-of-problems-colour-block.png)

Art Smalley wrote about how there are Four Types of Problems businesses face.  Each type requires a different approach:

1. Troubleshooting: A reactive process of rapidly fixing abnormal conditions by returning things to immediately known standards. 
2. Gap-from-standard: A structured problem-solving process that aims more at the root cause through problem definition, goal setting, analysis, countermeasure implementation, checks, standards, and follow-up activities. 
3. Target-state: Continuous improvement (kaizen) that goes beyond existing levels of performance to achieve new and better standards or conditions. 
4. Open-ended and Innovation: Unrestricted pursuit through creativity and synthesis of a vision or ideal condition that entail radical improvements and unexpected products, processes, systems, or value for the customer beyond current levels. 

I’ve found this model helpful. I can see when I get stuck always fixing abnormal conditions in “Troubleshooting” mode. This is what has happened with overflowing bins, broken builds, constant defects. 

To avoid this trap we must understand that Troubleshooting is a temporary measure. We haven't resolved the problem, only moved it. The immediate next step is to use one of the other problem solving approaches. Otherwise we will fall back into troubleshooting. 

Suppose we discover that the build kept breaking due to a flaky acceptance test? We turn the test off to get the build to deploy. This hasn't solved the problem so we need to move to a different mode. We could get the test back on by adding some extra error handling  (Gap-from-standard)? We could refactor the testing tool to better understand delays in the UI (target-state). Or we could reconsider our entire testing strategy and our testing pyramid (open-ended). 

The problem is that all four of these types assume a standard is established and in place and we are either trying to return to that standard, or improve it somehow. This is not always the case (it isn’t with my bins). Without an established known standard there isn’t really a point we cross before we act. So things simply slip more and more until the mess becomes intolerable. If nobody agrees that the build should always be green, then how do we expect them to even identify let alone fix flaky tests? This has echoes of Broken Window Theory which says that “if a window in a building is broken and is left unrepaired, all the rest of the windows will soon be broken… one un-repaired broken window is a signal that no one cares, and so breaking more windows costs nothing“. Where it says “no one cares” we can replace with “there are no standards”.

Why does this happen? Because when it comes to problem solving, without a standard you are stuck in Troubleshooting, constantly warring against an abnormal condition which is not in any way recognised or visible (rubbish on the floor, failing build). If, and it's a big if, you try to drive an improvement by employing one of the other methods, you find there is no benchmark, no ‘definition of good’, to improve from. And so you try and raise things to some acceptable standard or design an entirely new solution and, after much investment, you find you simply return to the original state. Overflowing bins. Broken builds.

This means there is a fifth type of problem: Establish standard. In the same way the other four need a different approach, so does this one. And here is the rub: whatever you have today IS your standard. The standard of my bins is overflowing. The standard of the build is broken. The standard of the product is defect ridden. Once we recognise this, rather than change the standard we begin to make it visible. 

This is essentially the guidance from the Kanban principles: “Start with what you do now”. Don’t start by changing your standards. Make your current standards visible. If my current standards are rubbish on the floor, let’s start there by marking everytime the bins overflow and everytime I eventually take them out. This will give me and my family a shared picture to act upon and manage the bins better in a collaborative way. From there we can collectively evolve by using the other problem solving categories such as establishing new target states through continuous improvement (empty the bins when they are ¾ full) or radical improvements (redesign the kitchen to accommodate better bins). And then I might find my bins never overflow again.