---
layout: post
title: "Website as decorator"
date: 2013-06-20 10:05
comments: true
categories: 
---

The conventional way to build websites, over the last decade or so, has been to treat them as first class applications in their own right.  After all, they often have behaviours, and domains, that are very specific to their usage.

There has been a downside to this.  The result has been the production of an entire generation of monolithic applications that are expensive to maintain and extend.  And that's before we come on to concerns like scalability and the ability to leverage developments in cloud technology.

There have also been two orthogonal movements that have given rise to these unwieldy monoliths: LAMP and CRUD frameworks. One side effect of LAMP has been the dismissal of architecture as a concern.  For years developers were liberated from worrying about overall architectural design and, instead, reached for a LAMP stack, or its MS/Sun equivalent.  Likewise CRUD frameworks, such as Rails and its imitators, removed concerns about internal engineering principles in favour of a focus on 'the domain'.  Unfortunately it is potentially a highly skewed and limiting abstraction as movements driven by the [Command and QueRy Separation (CQRS)] [CQRS] pattern have attempted to demonstrate.

The other problem has been that, for increasing numbers of companies their websites have become their business.  Thus what was a simple lightweight application has grown in functionality until they are essentially where the majority of the business operations are run.

Combine all these factors, as the large majority of web applications do, and there's more than a fair share of problems. Problems which have been exacerbated by the stellar rise in web consumption, the need to integrate with third parties, the growth of client side scripting and the little predicted fragmentation of the client side consumers caused by the rise of mobile.  Development teams are caught unawares by problems such as scalability, high availability and multi-channel consumption and struggle to manoeuvre systems that were never designed to handle these concerns.  The result is teams reach for another rewrite.

Web applications that are built with these concerns from ground up look very different.  The same engineering principles (such as SOLID) that are applied everyday at a code level are applied at an architectural level.  Architecture is important again.
The result is a movement away from web applications to web systems.  The responsibilities of the website have been drastically reduced.

The reduction is severe.  Websites are hacked back until they essentially become decorators providing placeholders for a set of disparate content modules served from varying endpoints (i.e. services).  The website essentially composes resources from various locations and style them (using CSS of course).  The site is left with very specific concerns, such as layout, style, co-ordinating security between the various services (e.g. ensuring that the HTML returned from the Basket Service is for the logged in user), defending against integration issues and providing SEO optimized URLs etc.

All the real functionality, all the real content, is provided by a set of independent services.  These independent services  provide the real resources as blobs of HTML for the web site to style as needed or as json documents for client side javascript.  A Products service provides blobs of HTML ready for the web site to style as needed, a search service takes inputs and returns HTML, again ready for the web site to style or json for the client to process as-you-type Google style.  All of this happens somewhere in the background in a manner opaque to the user.  From a client perspective it is indistinguishable from any other website. 

Web applications become web systems.  Systems comprised of services which provide narrow, vertical, domain specific resources and capabilities.  

This provides huge benefits and opens up new opportunities.  Each service is independently deployable, scalable, cacheable and developed.  Independent ['two pizza teams'][pizzateams] work on each codebase using whatever tools, languages, techniques are most appropriate for their particular domain.  For example, one service may process requests up front using a python batch job and deliver resources to a CDN to reduce load, while another may generate resources as needed and handle requests asynchronously using NodeJS.

There are other advantages: the front end is able to employ techniques such as [segregation by freshness] [SegByFresh] to increase the cachebility of the site without any changes to the architecture, simply by changing the behaviour of the front end.  The website can be easily made [Anti-Fragile][AntiFragile] by removing single points of failure and providing coping strategies when other services are unavailable thus increasing overall uptime and availability, again without huge change.  Heavily used resources can be moved to CDNs to increase capacity simply by telling the website to load them from a different endpoint.  Client side applications become easier to write as endpoints can be simply exposed.  Third parties can integrate and leverage your system in unimaginable ways by externally exposing the very same service endpoints used to build the service internally, a technique employed to great success by the likes of [Amazon, Facebook etc.][OpenAmazon].  Mobile apps etc. can likewise be simply built off of the same services without requiring any architectural changes.  Testing becomes dramatically reduced in complexity as each service is individually verifiable without having to apply expensive, long running regression suites against the whole thus dramatically reducing turn around time. And, again, all things can be independently (auto) scaled and deployed in a manner that makes sense to those individual services giving teams a larger number of levers to pull to ensure a good user experience without expensive and wasteful vertical scaling.  Legacy problems become considerably easier to solve - in what is quite probably the most common application of the website as decorator pattern - by acting as a [Strangler Application][strangler] which pulls resources from legacy sites and repurposes and strips back the content from old systems.

Tools such as [SiteMesh][Sitemesh] exist to enable such patterns.  Movements such as [Microservices][Microservices] are a natural extension of these techniques.  Sites such as Amazon and Netflix are built upon these principles and techniques.  

I would argue that building the website as a decorator and backing it with independent vertical services is a viable approach regardless of the size of the web application (within reason).

[strangler]: http://www.martinfowler.com/bliki/StranglerApplication.html
[CQRS]: http://martinfowler.com/bliki/CQRS.html
[pizzateams]: http://zurb.com/word/two-pizza-team
[SegByFresh]: http://martinfowler.com/bliki/SegmentationByFreshness.html
[OpenAmazon]:  http://www.infoworld.com/t/service-oriented-architecture/ex-amazonian-urges-google-sample-amazons-secret-sauce-175906
[AntiFragile]: http://continuousdelivery.com/2013/01/on-antifragility-in-systems-and-organizational-architecture/
[Sitemesh]: http://wiki.sitemesh.org/display/sitemesh/Home
[Microservices]: http://yobriefca.se/blog/2013/04/29/micro-service-architecture/