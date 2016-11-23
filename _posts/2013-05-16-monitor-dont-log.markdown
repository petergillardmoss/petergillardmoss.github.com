---
layout: post
title: "Monitor don't log"
date: 2013-05-28 15:02
comments: true
categories: 
---

Look at the market and you see a bunch of products springing up around monitoring, alerting and logging.  Graphite, logstash, logster, graylog2, Riemann, splunk to name a few.  

To my mind there's a whole lot of confusion going on.  I'm sending logs here, stats there, filtering in this place, alerting over that way somewhere.  Logs go this way, that way.  Apps send stuff to logs and to alerting systems, then to monitoring dashboards.

It's a bloody mess that's what it is. [#monitoringsucks](http://lusislog.blogspot.co.uk/2011/06/why-monitoring-sucks.html)

## They all solve the same problem
But from different angles.  But the problem is the same.  It's about understanding your system.  Looking after it in production.  Checking it's working OK and diagnosing and fixing it when it isn't.

So why so many different solutions?

## The problem is logs
Ask a room of developers what they'd do to help diagnose a live bug in their app.  Most of them would say 'add some logging'.  Ask them how and they'd reply 'use log4x to write to a log file'.  They'd write some text out to a disk.  There's your problem.  

What only a very few would say is add some monitoring.  Rather than write out a line to a file that says 'Connecting to the database' they'd record a key value pair for active database connections.  Rather than writing out 'Home page requested' they'd prefer a meaningful data structure detailing the request received.  Rather than output 'Integration point unreachable' they prefer to send out a tick with the integration point status.

## I'm not saying writing stuff to disk is wrong…
Just that it's a side effect.  It's far from your primary concern.  It's a story way down the priority list.  It's the last thing you should do, not the first.

## Observation, checking and recording
To be a caretaker of any running system your first priority is to check.
To check any running system you need to be able to observe it;  observe how it's performing, to check it's not in trouble.

First you observe, then you record what you observe.

## Monitoring vs Logging

Monitoring is observation, checking and recording.  Logging is recording.

If you were a doctor and had a patient who was complaining of heart problems what would you do: use an ECG or read their Twitter feed?

## Logging isn't monitoring

Logging is primarily about recording.  It's not about observation.  You can't watch masses of stdout pouring out and derive anything useful.

In the past we have employed logging as means to retrospectively diagnose a system.  In the present we have attempted to retrofit monitoring by massaging logs that didn't have the intent to convey meaningful information for machines to make decisions on. 

The problem is that logging was never originally intended to do anything more than output, usually to disk, a record of arbitrary activities in an arbitrary format for human consumption at some other point in time (the future).  

In fact logging has historically been designed to enable a disconnect from the system: send me your logs so I can see what's going on.  Monitoring is the exact opposite: it is connected and engaged.

## State vs events
Good monitoring provides two things.  The state of the system at any point in time and a notification of events.

The state of the system helps you understand the current condition. Technical things like the number of database connections, the number of http connections, the amount of memory consumed, the amount of disk space used, whether a connection is open or closed etc.  Domain things like the number of orders being processed, the number of customers logged on. From this information you can check if the system is working well or not.

Events enable you to understand what is taking place within the system.  Technical things like an http request has been received, an error occurred.  Domain things like an order has been placed, a new customer has been created.

Monitoring is about providing the ability to observe, check and record these two distinct things.

## Prefer state
Logs are typically [event streams](http://www.12factor.net/logs).  They rarely output state.

However state is often [a more robust method for understanding the system](http://awelonblue.wordpress.com/2012/07/01/why-not-events/).  It is more reliable to record the total number of orders the system has taken and act on a change to that state rather than respond to a single notification per order which you may or may not receive.

The problem is that the traditional paradigm around logging encourages an event model (by outputting an description of an activity) rather than reporting the more useful state of the system.

## State at a point in time vs state change
There are also two ways of reporting state: at a regular point in time or at the point the state changes.

The first method has latency (as you need to regularly poll/push the data at intervals).  The second reduces latency but is essentially an event with stateful metadata so suffers from the same pitfalls as events.

Both can be used together.

## Alerts can be on state or events
We can alert on state (or combination of state) such as high CPU plus low memory.  Or we can alert on events, such as application errors or a new order coming in.

However we can derive events from state change (for example if the number of orders increase we can send out a New Order alert).

## Structured logging
[Structured logging](http://gregoryszorc.com/blog/category/logging/) provides a solution to the limitations of human readable logs.  By logging machine readable data rather than human readable a number of the problems of traditional logging implementations can be overcome.

## Design your system to be monitored, not logged
When building and designing your system stop thinking about logging.  Think about monitoring.  That's monitoring _not_ logging.  

This doesn't mean that a form of logging can't be employed in monitoring (such as structured logging) or even than traditional human readable logging doesn't have it's uses (for debugging in development).  It's just that your goal is to monitor and monitoring is far more important than logging.

So, before introducing log4X think about how best to monitor your system and implement that in your design in whatever way is best (status pages, push notifications, structured logging).  For other problems consider more appropriate first class, machine readable, solutions such as event feeds which can be leveraged more effectively and cheaply. 

Then, if you find you really, genuinely still need it, you can write out some human readable stuff to disk somewhere.
