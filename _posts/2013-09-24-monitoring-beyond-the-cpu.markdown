---
layout: post
title: "Monitoring: beyond the CPU"
date: 2013-09-24 17:57
comments: true
published: false
categories: 
---

Truly effective Monitoring needs to go beyond CPU cycles and disk space.  It needs to evolve beyond the ping.  Systems need to be self diagnosing and self healing.  More than that, monitoring, as a technology and practice, has the potential to extend beyond the IT operations room and into other domains and into the wider business.  It has the potential to feed from and back into other systems, whether business, finance or other processes.

## Exposing the service
The first, and simplest evolution of monitoring will come from services and application. Treating monitoring as a first class concept, rather than a side effect of logging, will enable services to be far more expressive and accurate.  Services are able to expose information about their state to monitoring systems and push meaningful events to be monitored (both low and high level).

The result is a huge leap in the quality of monitoring and diagnostics and detection.  Rather than second guessing, and diagnosing of external side effects (such as pings), services are able to express clearly to monitoring systems when they experience problems and of what nature.

## Exposing the domain
If services can expose their state from the inside then they can also expose domain concepts.  This allows monitoring at a domain level.  As systems, more and more, become the model for the business, it provides a unique opportunity to offer domain insights through monitoring.   Whether that is the number of sales, credit card transactions, calls received, comment submissions, outstanding invoices or whatever concepts are meaningful to your domain.

This makes monitoring more useful to stakeholders as they are exposed directly, and in real time, to the business impact of the system.  As the monitoring comes directly from the source its accuracy and timeliness are far greater than traditional data warehouse reporting.

This also allows diagnostics and detection beyond the functional level.  For example, a new feature may result in a dramatic drop in sales.  Traditional monitoring will not pick this up because, at a functional level, the system is operating correctly (there are no faults).  However, if you were monitoring sales directly as a domain concept then teams can be alerted to the drop and take appropriate action.

## Into the service
At the simplest level services and 


http://www.information-management.com/blogs/predictive-apps-are-the-next-big-thing-in-app-development-10024826-1.html?ET=informationmgmt:e9405:2246111a:&st=email&utm_source=editorial&utm_medium=email&utm_campaign=IM_Blogs_090413

## Into the process

## The four parts of monitoring
To reach these goals effective monitoring is a four part problem: technology, practices, usability and analytics.

## Technology
The monitoring platforms, though still rapidly evolving, have mostly solved the core concerns of how to collect, store and make monitoring data available and to do it at scale.  There is a degree of informal standardization around protocols such as graphite and syslog.  There are effective, non-invasive tools for both pushing and pulling data from systems.

There are still problems around standard structures to send events etc. as opposed to non-structured logging and these problems are being actively tackled (although still some distance from entering the mainstream).  

I think there's a real technology gap in the application space as most people continue to rely on log4x and log processing tools which provide cumbersome, expensive, brittle and unreliable solutions to monitoring applications.  The application development community has yet to embrace monitoring and to start building frameworks that make meaningful monitoring of applications as cheap as using log4x.

With a few exceptions overall the monitoring community has a grip on the technology problem.  There are some polluters (as there always are) who push old or disproven techniques.  However they will simply fight for the middle ground leaving more effective tools to establish themselves.

Oh, and then there's Windows...

## Practices
When to push? When to pull? How to structure events? What to monitor? What protocols to use?

All these questions, and more, are practises issues.  Some practices are beginning to emerge at an operations level; application monitoring, on the other hand, is an area with virtually no established practices, recommendations or implementations exist.  This is evident in the lack of tools or frameworks (such as RoR) that offer any useful means to integrate at a systems level.

Practises also extends to culture and people.  How to work between teams to ensure effective monitoring and feedback and involve teams to continuously improve.  This could include simple things from publicly visible walls towering over developers heads to one-app-one-team collaboration.

## Usability
Producing usable charts has been a recent leap forward and there are constant innovations and improvements in this area as people move beyond the aesthetically barren functional graphs of the well intention, yet ham fisted, developer.  Yet usability and visualization techniques need to go beyond well colour co-ordinated charts.

Most systems are still in their infancy when it comes to conveying their current state.  Very, very few effectively bring disparate pieces of data together in a manner that aids diagnostics and support.  

This is an area ripe for innovation and is probably where I predict much of the growth in monitoring, especially as the underlying platforms become proven.  The demand moves from "I don't have that data" to "I have the data but its hard to surface".  This will feed back into practices and technology.

## Analytics
The monitoring community lack the analytical skills, the patterns and the models to surface data to enable humans in detection and effective decision making. The analytic tools to save hours of scrabbling around in logs and graphs and perhaps, ultimately enable machines to replace humans in rudimentary decision making and self healing.

This is about knowledge, skills, experimentation and discovery.

Like usability this is an exciting area.  Unlike usability this is a skill set that doesn't typically exist inside, or near, to the technology community.

As a practice monitoring has huge potential.  As the technology grows and improves