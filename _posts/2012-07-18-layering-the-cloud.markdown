---
layout: post
title: "Layering the cloud"
date: 2012-07-30 14:57
comments: true
categories: 
---

One of the great things about the cloud is the way you can just run a bit of code or a bash script and before a Windows admin can open their GUI you've got a running box.

This opens up a host of opportunities and new patterns.  Martin Fowler recently posted about [the Phoenix Server pattern](http://martinfowler.com/bliki/PhoenixServer.html) where machines are simply thrown away rather than upgraded.  But these things require looking at the way you architect infrastructure slightly differently.

To help you can split your cloud architecture into three layers:

* Visible
* Volatile
* Persistant

## Visible

This is the layer between the cloud and the rest of the world.  It is mainly public DNS entries, load balancers, VPN connections etc. etc.  These things are fairly static and consistent.  If you have a website you will want the same A Name records pointing at your static IP.  

Things in the visible layer rarely change or if they do they are for very deliberate reasons.

## Volatile

This is where the majority of your servers are.  It's called volatile because it tends to change a lot.  The known state (how many servers, what versions of which software they run etc.) are changing frequently, perhaps even several times per hour. 

Even in a traditional data centre your servers are being upgraded, having security patches applied, new versions of software deployed, extra servers added etc.  On the cloud this is even more volatile when you use patterns such as the Phoenix server and machines are rebuilt with new IP addresses etc.  

You should be able to destroy the entire volatile layer and rebuild it from scratch without incurring any data loss.

## Persistent

This is where all the important stuff is kept, all the stuff you can't afford to lose.

Ideally only the minimum infrastructure to guarantee your persisted state is here, so for example, the DB server itself would be in the volatile layer but the actual state of the DB server, its transaction files etc. would be kept on some sort of robust storage that is considered 'permanent'.

By organising your infrastructure around these three layers you are able to apply different qualities to each layer, for example the persistent layer would require large investment into things like backup and redundancy to protect it whilst this is completely unnecessary for the volatile layer.  Instead the volatile layer should be able to accommodate high rates of change while you will want to maintain a considerably more conservative attitude towards the persistent and visible layers. 