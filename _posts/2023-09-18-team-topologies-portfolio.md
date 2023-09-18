---
layout: post
title: "Beyond Team Topologies with team portfolios"
date: 2023-09-18 09:00
comments: true
categories:
published: true
header-img:
social-img: "img/team-topologies-portfolio.png"
description: "Improve flow of value across the entire organization by combining Team Topologies with Value Driven Portfolio Management. 

Treating teams and the value they deliver as first class enables leaders to unlock the next level of organizational performance."
---

You've been successfully using team topologies to optimize for flow and reduce cognitive load at the team level. You have broken down barriers and re-organised into a number of different teams, some stream aligned, some enabling, some platform, some complicated-subsystem. Now your next question is "how do I manage all these different teams and unlock flow at the organisational level?"

As a leader you will be responsible for multiple things beyond team level flow. You have to execute on strategy, allocate funding, manage capacity, reduce impediments to collaboration and improve capability across teams whether for security, compliance or other cross functionals. How do leaders build on Team Topologies to achieve these things?

In the next series of articles I am going to explain how Team Topologies combined with the principles and ideas from Value Driven Portfolio Management, such as EDGE, can enable leaders to improve flow at the next level. 

Managing teams as a portfolio
=============================

Team Topologies stresses that teams should be cross-functional with a strong purpose aligned to the flow of value. EDGE stresses that portfolios should be managed by value and delivered by self-sufficient cross functional teams, again aligned to value.

Where EDGE helps leaders manage and govern the portfolio of value, team topologies helps leaders design the organizational structure to deliver. The two approaches go hand in hand..

So what does a Team Topologies portfolio look like? Chapter 7 of EDGE talks about Capability-Based Portfolios. This gives a complete picture of all the business and technology capabilities the organization needs to deliver along with the set of key performance indicators (KPIs) and other measures used to monitor the health of those capabilities. By combining this with Team Topologies leaders have the sensing mechanisms and tools to refine team structures to improve alignment and flow of value. This creates a virtuous cycle.

Thinking in portfolios
======================

At this level, it is critical to be able to think of the portfolio in terms of the capabilities provided by the teams. The key responsibility of leaders is to effectively manage this portfolio in order to improve flow of value at the organizational level. This is achieved by creating greater and greater alignment between value and the team and greater and greater self-sufficiency of each team.

There are a few principles which are really critical to achieving this:

-   Everything (costs, security, compliance, legal etc.) are linked to outcomes
-   Teams are first class and responsible for discrete outcomes
-   Flow is optimized at the org level, beyond team level flow
-   Portfolio is cross-functional and collectively owned by all leaders (not just one)

This is very different from other management methods where functional leaders are accountable for managing projects based on their own functional deliverables. Instead capability portfolios should include everything needed to successfully deliver value to the customer and run the organization and each capability is provided with everything it needs to design, build and run the software.

Another thing is that the portfolio is not rigid like an architecture diagram of components or an organizational chart (it is neither of these things). It should change and adapt as the organization responds to changes in the environment and teams identify ways to re-organise in order to improve the flow of value. The role of leaders is to govern the portfolio as a whole and ensure that it is well balanced and is creating an impact greater than the sum of its parts.

Introducing Stream Aligned Teams into the Portfolio
===================================================

In order to govern the portfolio each team needs to be clear on the capabilities they provide. It's easier to start by bringing your stream aligned teams as identifying their capabilities will be simpler.

For each capability the team provides they must expose the following information:

-   Outcome the capability provides
-   Measures of Success linked to those outcomes
-   Key Performance Indicators which indicate operational health (inc business and engineering)
-   Risks
-   Costs

For example, if the capability was Product Search then:

-   **Outcome**: Customers are finding the right products
-   **MoS**: % of searches which convert to purchase (driving revenue)
-   **KPIs**: response time, click-through rate, relevance, availability, 4KMs etc.
-   **Risks**: security, scalability, team health, delivery etc.
-   **Costs**: $60k per month inc 5 HC and infra costs

This data then serves two purposes:

1.  The stream aligned teams use this to sense and respond within the team
2.  Leaders re-use this same information to sense and respond across the organization

Gathering this information is where the functional leaders come in. Because the portfolio is collectively owned, everyone works from the same model. Rather than each function (e.g. engineering, security, compliance, finance) doing governance independently and reporting back in silos, they are responsible for enabling the stream aligned teams to gather and interpret the information. They do this first for the benefit of the team, then expose this to the portfolio for the benefit of leaders. For example, finance are responsible for helping each team understand their costs and budgets and adding their insights to each capability in the portfolio.

This information can then be used, alongside a healthy dose of human judgment (from the team) to RAG status their capabilities. Is there a drop in KPIs? Or have costs gone up suddenly? Then mark the capability as Amber or Red.

This gives leaders the ability to look across the portfolio and get the big picture they need and make appropriate decisions. Because the teams are first class in the portfolio this acts as a forcing function on cross-functional collaboration as different leaders have to make decisions collectively based on the data. For example, if a number of teams are showing red on security, then there is an easy case to prioritize those concerns over delivery if that is mostly green. It also dramatically reduces the number of reports and meetings because everything comes together in one place through the lens of teams, not split by functional needs.

Another benefit to this view is that it removes a lot of the discussions around engineering productivity. This is because the relationship between inputs and outputs are organized around the capability and the value it produces. Costs are linked to outcomes. This makes it really easy for leaders to see the relationship between engineers and the value they are creating.

Introducing Platform Teams into the Portfolio
=============================================

Where stream aligned teams are responsible for business capabilities, Platform teams are responsible for technology capabilities. By technology capability I mean things from production infrastructure (compute, API gateways, message queues, databases etc.) to delivery infrastructure (source code, deployment pipelines etc.).

The collection of Platform teams can be captured in their own sub-portfolio. They should report their capabilities in a similar way to the stream-aligned teams. One key difference is that the platform team's outcomes must be related to helping the stream aligned teams improve their technical KPIs. For example, stream aligned teams will have 4KMs as a capability KPI, so the outcome of the Deployment platform capability should be "making it easy for stream aligned teams to deploy to production" as its outcome with its MoS related to improvement in the 4KM.

Again, the portfolio makes this easier for the platform teams as the stream aligned teams are already making this data visible there. Rather than the platform teams having to do all their own measuring and data collection they are able to work from the exact same view that everyone uses. 

Introducing Enabling Teams into the Portfolio
=============================================

Remember earlier I mentioned that functional leaders are responsible for enabling the stream aligned teams to gather and interpret information and turn this into KPIs? This is essentially where the Enabling team type comes in.

If we look at our portfolio, we may see that 60% of our teams have KPIs we would class as high availability. And we notice the teams are struggling to reach those KPIs because of a lack of skills. This is where leaders would make the decision to add a Site Reliability Engineering enabling team to the portfolio in order to shift the needle on those KPIs by building those skills across the teams.

The success of the enabling team is based on that outcome: "identified teams have the skills to build high availability services". Again, as with the platform team, the governance is all done through the same portfolio view.

Sometimes the relationship between enabling teams goes the other way. They may decide that they wish to introduce a new KPI to specific capabilities and then they become responsible for helping them meet that KPI. For example, when GDPR was introduced, specific capabilities which need to process personal data would require introducing KPIs around data handling. Again, by using the portfolio view, this information can be clearly seen as each team with GDPR responsibilities now has the information they need to measure their performance.

Another pattern which emerges is that the functional leads switch to being responsible for enabling teams and are able to use the portfolio view to show their impact through the results of the stream aligned teams. This creates a big change in how they interact within the organization as their success becomes the team's success.

Introducing Complicated Subsystem Teams into the Portfolio
==========================================================

Complicated subsystem teams are, well, complicated. Whilst it is best to try and express the value they provide in a similar way to the stream aligned teams, this isn't always easy and is very dependant on what components they are developing and how they are used.

However, it is important to try and articulate the outcomes they are trying to provide to the stream aligned teams. This might naturally force them into operating more like an enabling team or a platform team. 

Managing the complete portfolio
===============================

Now your leaders and teams should have a shared view of the portfolio. But it doesn't have to end there. By capturing the right information at the portfolio it should enable different teams and leaders to slice and dice based on their current needs. For example, if the business needs to IPO and compliance becomes a priority, the portfolio view can help you identify which teams will be impacted by this change. Not only does this give a sense of scope it helps formulate strategies and agree priorities for making effective change.

The portfolio also doesn't have to be limited to the information I suggested. Depending on the organization other information can be brought in. The point is the unit of granularity is always the capabilities provided by the team. And the role of the portfolio is to bring visibility of all those capabilities in one place.

Portfolios within portfolios
============================

Smaller organizations will be able to achieve this with a single portfolio. However, as organizations get bigger they may need to break their portfolios down. This should be done in a fractal manner where sub-portfolios operate at a different scale enabling leaders to zoom in and out. A common way of doing this is by creating a sub-portfolio per domain. This should also match the organisational structure by giving next level leaders responsiblity for their portfolio and the teams within them.

Making teams and the capabilities they provide first class and governing them as portfolios makes it much easier for teams to optimize at the organizational level and identify strategies for improving organizational performance. It also gives teams the much needed view of how they fit into the bigger picture.