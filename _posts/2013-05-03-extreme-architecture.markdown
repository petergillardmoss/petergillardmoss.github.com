---
layout: post
title: "Extreme Architecture"
date: 2013-05-03 15:42
comments: true
categories: 
---
## Not touched by human hands
Here's a rule: you can't ssh on to your production boxes.  Not just you, don't feel like you're being singled out, nobody else can do it, especially not if they're human.  Not even if they are a monkey or a dog come to think of it.

If you really, really, have to ssh then you definitely, definitely won't have root access, or sudo, or even the ability to edit a single file.  You certainly, certainly won't be allowed to install anything.

Sound a bit harsh? Well, you wouldn't let me ssh onto the production web server and start fiddling with the website's Ruby code in vi would you?  So why the hell do we think it's acceptable to do the same with /etc/passwd?

Everything about your infrastructure should be in source control.  Everything about your infrastructure should be repeatable and reliable.
## Failure means death
If a server fails, kill it.  Even if it fails a little bit.  Zero tolerance.  If it gets a little slow, well give it the chop.  Be merciless.  

In fact, sometimes just kill it anyway for the hell of it.
## Fast
A single server should be built in minutes. You should be able to build your whole system, from scratch, really, in small multiples of that.  So, let's say twenty minutes?  With everything installed.  With everything working.

## Small
No big things allowed.  Only small things.  Small servers, small amounts of storage, small amounts of RAM.  If you need a big thing then you build it out of lots of small things.

Even environments should be small, which brings me nicely on to:

## Autonomous
Build autonomous, small environments around your capabilities.  They have their own rules, their own security, their own services, their own monitoring.  If you need to share capabilities (say a Credit Card payment gateway), then you do so via services that sit in their own firewalled, protected, autonomous environment.  

Funnily, this is kinda how the internet works.

Then, blow your SSO environment away and replace it with another one.  Go on, no one will notice.

## Production is a state, not an environment
There's no such thing as a production environment, there are only environments _in_ production.  So create an environment and put it test, then put it in production, then put it in test again if you want to, or dev, or wherever, it's just a state.  

## Share nothing
Be a selfish individualist, demand your own of everything.  Own DNS, own LDAP, own firewall, own reverse proxy etc.  Then refuse, absolutely, point blank, unconditionally, no special cases, preferential treatment, zero tolerance, to share anything. Anything.
 
## Forward and replicate over centralisation
It would be madness to have multiple sources of truth or a dozen places to go to do administration for cross cutting concerns across capabilities, especially for things like security, or monitoring.  Equally it's madness sharing all infrastructure in one big environment (or across multiple environments).

Sharing nothing is great, but for cross cutting concerns you need some repetition, so replicate data or forward it or shard it or whatever, just don't share infrastructure.

So, each environment could have it's own LDAP which is replicated from a master.  But each environment is free to add its own users or security concepts that no other environment needs.

## Stateless
It's easier to remember the important things if you don't bother trying to remember the unimportant ones.  Not having to remember anything at all is even easier.

So make your servers really, really forgetful.  So forgetful that if you turned them off then everything you'd done since you turned it on would be gone.  Forever.

Of course there's important stuff that you're going to absolutely need to remember, like all your customer's details, but that stuff should be provided by services on your infrastructure like clustered, networked, high availability, failsafe, filesystems or databases.  Servers and their configs just aren't the kind of important that we should worry about remembering.

## Immutable
Servers don't change.  Whatever way you built them you leave them that way.  You don't upgrade them, you don't modify their configs, you don't patch them, you just leave them exactly the way you found them.

## Disposable
Throw everything away.  Don't bother trying to fix it, upgrade it, renew it.  Just trash it and get another one.  Do this regularly.

Apply this principle to as much as you can.  Don't bother remembering the ssh keys your app needs, just revoke the old ones and dish out a load of new ones, it's much easier.
  
## Short lived
Nothing lasts forever so don't try to pretend it does.  Kill it before it attempts to.  A day's a long time, every day should be a new day and a new day means a new server.

## Self diagnosing
It's much easier to know what's wrong if the thing that's wrong can tell you what's wrong with it.  

Pretty obvious really.

## Self healing
If something in the environment is wrong, and that thing knows what's wrong, then why doesn't the environment just fix it itself?  Database has gone down? Bring it back up. Server's crashed? Throw it away and replace it. 

Not so obvious but still fairly obvious really.

## N* environments
Creating a new environment should be as easy as asking for a new environment.  Which should be as easy as running a script and giving it the name of your new environment.  

Environments aren't an Enum of 'Production', 'Test', 'Dev', they're an array full of whatever labels you happened to come up with that day.  And you'll probably find you can come up with a lot of different labels in just one day, and lots and lots of environments to go with them.

