---
layout: post
title: "To stream or to batch? What difference does it make?"
date: 2021-02-04 15:20
comments: true
categories: 
published: true
header-img: 
---

Whether an integration should be stream or a batch based is a common technical decision. Historically, processes which involved large volumes of data were 'batched'. Thanks to the cloud and dramatic increases in processing power, many businesses are taking opportunities to move processes to something more 'real time'.

So how should a team decide whether to build a batch process or a stream?

To start, let's focus on the architectural principle of Information Flow. The architecture must enable both the complete and correct capture of information in one process to flow correctly to downstream processes in order to have an effective and efficient system. 

A batch, or a stream process, is simply a tactic to enable that information flow between different business activities.

To decide whether batch or stream is most suitable we need to start by understanding the business activities we are modelling and how information flows between them. We can start by asking "does the business activity flow from an external trigger?" vs "is it triggered on a periodic basis?" 

If I have a coffee shop then making a cup of coffee is an activity triggered by a customer demand. This might trigger other downstream activities which 'flow', just in time, from the customer's order. On the other hand I have to do a number of jobs at the end of every day when the shop gets closed. Closing the shop triggers a number of jobs such as cashing up the till. These jobs always happen at a specific time (closing time) every day.

This gives us the first basis for our architecture. In the 'flow' example, where the original trigger is customer demand, things need to stream, end-to-end, as much as possible. Any batching will harm the flow and create delays and waste etc. A customer does not want to wait for you to start making coffee or ask for you to pay when the next schedule kicks off in five minutes time.

For a periodic trigger, however, these can often be batch. When I cash up the till, I batch up the entire day's orders and reconcile them. Payroll is another example of a periodic trigger which is batched.

One caveat to this is that many periodic triggers might have been batched purely from a cost and effort perspective. This is often true with legacy systems. When re-looking at these activities we can challenge them and see if they would better fit into the flow. For example, why couldn't I cash up the till at the end of every order, making it part of the order flow? Probably because it was manually intensive so I batched to gain efficiency. What if technology enabled us to automate that away? Then those activities could be moved into the flow and cash up every order. Or, if it's still mildly resource intensive, cash up every tenth order (still a batch, but smaller, and part of the flow, not triggered periodically).

Some batches might be 'true' batches. As in they are part of the transaction. If I order ten coffees for my team as a single order, they all have to be guaranteed delivery as a single unit. Therefore a batch of ten coffees is a true batch in the customer's eyes. Any less than ten coffees is a fail.

Now, to make things more complex, the 'delivery' in all of these examples, doesn't have to happen in a batch. For cashing up each order could be put on a stream as it happens and placed in a queue. The cashing up progress would then batch all items from the queue. When making an order of ten coffees, they can still be made one at a time (in series or parallel) and then have an orchestrating process which bags them into one order. 

Ensuring that batching is decoupled as much as possible from the original process eliminates waste and creates future improvement opportunities. Which is why in manufacturing and logistics batching is something to be eliminated.

There's also another interesting use case which ends up periodically batched, when in reality they are actually flow. These are cases where something is triggered after a certain period of time. For example, you take a 30 day free trial, and you need to be notified that you will begin payment next month. The business activity flows from the original trigger - signing up for the trial. The issue is, we can't make 'mini-clocks' which wait for 30 days off of every trigger. So we tend to use a batch process, which checks every day for expiring trials and generates an email. But, in this case, the batch is an illusion. We could design more sophisticated back end jobs management which model a timer better.

When you look through these lenses you'll often find that the original reason for batching is often driven by technology constraints, not by the actual business model. Why are we paid monthly? This is primarily driven by legacy constraints around running complex payroll systems (in fact before computers paying people at the end of the day was common). Improvements in technology removes these constraints. There's no reason pay couldn't be 'in the flow' and triggered off of timecard approvals. 

By re-examining the reasons for batching you can create a great opportunity to leverage technology in a manner which improves the business process, reduces waste and improves the customer experience. You'll notice that Amazon has really exploited this: do you batch your orders anymore? No, thanks to Prime.

To maximise your options aim for an architecture which enables "batches of one". Which essentially means stream as much as possible and replace batches which pull information down with batches which read off of queues. Then we can selectively apply batching only when it is due to the unavoidable sub-optimisation of resource constraints not because of an accident of design. And as technology improves we can reduce or even eliminate batching altogether.