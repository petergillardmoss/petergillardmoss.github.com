---
layout: post
title: "Tiered support is an anti-pattern"
date: 2013-06-24 08:05
comments: true
categories: 
---

Back when the first internet bubble was bursting I had my first web development job. We thought we were sophisticated because we used Macromedia Drumbeat whose killer feature was, gosh, dynamic ASP and JSP websites.  This put us a cut above those 'amateurs' who chopped huge TIFFs into static HTML using Fireworks (pfff)!

We also did a lot of other stuff, like edit our files directly on production.  We were doing Continuous Delivery (without the source control or build server ;P).  We also did our own support.  We were responsible for everything, from the code we wrote to the web server itself and even the relationship with our ISP. 

When something went wrong people phoned or emailed the web site team direct.  Yes, there were plenty of 'it works on my machine' and 'ignore that error, just refresh' and 'hang on, I'll just recycle the IIS process' but we had our fingers on the pulse of our users.  And when there was a problem we could fix, we fixed it.  Immediately. While the user was on the phone.

That's how we rolled in those days.  Seat of your pants, in touch with our users.  Yes, we had a lot of bad habits but we knew IIS4 was rubbish and crashed regularly, we knew that one of our badly written pages was responsible for bringing down the whole site at peak times, we knew that our perl script to upload ads failed on a regular basis.  

My next job, some four years later, was as Development Lead for a bank call centre application.  The environment was far more 'enterprise': source control, change requests, dev and test environments etc. Due to a shortage in desk space we ended up sat right in the heart of the call centre.  When our app went wrong we heard the call centre staff complaining. They would even come over to our desk (or shout across) and ask for our help directly.

In both roles the same thing happened: managers decided that we were spending far too long investigating users' problems and not long enough building the new features the business wanted.  Developers needed to be more productive, and more productive meant developers developing more new features.  To get developers to develop they need to be 'in the zone'.  They need headphones and big screens to glue their eyes to.  They did _not_ need petty interruptions like stupid users ringing up because they got a pop up saying their details will be resent when they tried to refresh.

In both cases the same method was prescribed: support calls would no longer come to the development team.  We were to redirect emails and our desks where moved to another 'quieter' building.  From now on everything would go via the IT help desk.  Someone (L1) would log the request, raising a ticket.  They'd search their knowledge base and if they didn't have an answer they'd pass it on (L2).  And if the support team couldn't resolve it then it would be raised again against the development team (L3).  

In both cases the development team became disconnected.  When there was a support ticket it was an interruption.  It broke our flow, became something to get irritated and annoyed by.  It was someone else's problem, why can't support just _deal_ with it?  Was it really that hard? Jeeeeeeeez.  Bugs were something to be captured and handed over to someone else to prioritise the fix, they weren't something to do with us.

In both cases the team was no longer responsible for what they produced.  There was now a process for dealing with deficiencies in the system and that moved responsibility to the process, not to the developers.

A systems thinker would tell you this is wrong.  You've gone from a system that connected a user to the team responsible with one degree of separation, to one that has three degrees of separation.  Or think of it another way: the team producing the product, and responsible for improvements and fixes used to be one degree away from their end users, who use the product and are feeding back the product's shortcomings and issues, but are now three degrees.  And not even three degrees all of the time.  The majority of the time the team won't ever hear about most of the support issues.  And most of the time the team won't even have that much interaction with the team that does hear about most of the support issues.

This is wrong for many reasons.  Let's ask some questions: the user doesn't find the software easy to use: who needs to know that? The user gets 500 errors everytime they click on 'submit': who needs to know that?  The user can't clearly work out what currency the prices are in when ordering from a different country: who needs to know that?  The user never received a confirmation email: who needs to know that? Is the answer to any of those questions The Support Team?  Help desk? Or perhaps the team responsible for the development and maintenance of the system?

There is another side effect: [failure demand][failure].  Essentially you create a greater demand by moving support away from the team because, rather than resolving the issue, people return to raise further requests based on the 'failure' of not resolving first time.  Also, development teams create additional failure demand by producing more bugs rather than fixing the existing ones.  Except they are so far removed they have no idea that they are doing this. The result is a suboptimization of the whole. 

Supporting a product should be an essential responsibility of a product team.  That means developers, QAs, PMs, UX etc.  Tiered support removes and distances the team from their users and encourages an 'over-the-wall' culture. Ultimately the product suffers and the users suffer as a result as, ironically, the team become more productive at producing bugs.

The alternative solution presents itself in Continuous Delivery.  It's easier for teams to connect to their users if they can roll out changes quickly.  Exposing the team to production via information radiators and monitoring also keep the team on the pulse and enables them to react quickly and effectively.  And ultimately being in direct contact with the end user via whatever means (Twitter, phone, email, face-to-face).  All without the need for layers of support and bureaucracy.

[failure]: http://en.wikipedia.org/wiki/Failure_demand