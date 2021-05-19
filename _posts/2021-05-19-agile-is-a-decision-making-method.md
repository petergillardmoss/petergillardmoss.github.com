---
layout: post
title: "Agile is a decision making method not a project management method"
date: 2021-05-19 08:20
comments: true
categories: 
published: true
header-img: 
social-img: ""
description: "Agile brings value when decision making and delivery are one process. Agile methods bring advantages by making decision points visible and actionable. When seen as a project management tool only then Agile techniques are unlikely to bring benefit."





---

Agile is primarily seen as a project management methodology but its real power comes when used as a decision making method. When used this way Agile becomes about finding ways to break down big complex decisions with high risk and uncertainty into small decisions with empirical feedback loops which are safe to fail. 

When only used as a project management tool it simply takes that same big hairy high risk decision and creates a linear schedule of tasks broken into iterations. None of the advantages are realised and switching to agile will probably bring little benefit.

To make this switch Agile techniques moves delivery from something that happens post "business decision making" to melding decision making and delivery into one process. How else do you interpret "Customer collaboration over contract negotiation" and "Business people and developers must work together daily throughout the project" from the Agile Manifesto? Agile is all about collaborative decision making!

Yet all decisions aren't the same. And therefore they shouldn't be delivered in the same way. The type of decision determines which development and delivery techniques are appropriate. Not the other way around! I don't switch electricity provider by breaking it down into vertical stripes by the value it delivers each end user (decrease cost of son watching television by 5%, decrease spoilt food due to outages). That would be a nonsense. Likewise you don't develop and roll-out a novel vaccine based solely based on stakeholder requirements and deploy it world wide in one big bang.  That would be deadly.

In the mid-60s thinkers such as C. West Churchman and Horst Rittel began to talk about how different types of decision needed different approaches. They distinguished between simple problems, which are easily identified and a solution can be discovered, verses wicked problems which have no consensus on the problem or the solution. More recently, the Cynefin framework expanded on these ideas to introduce four different problem domains (Clear, Complicated, Complex and Chaotic).

The Cynefin framework allows decision makers to decide which agile techniques and delivery approach are best suited based on the problem domain they are operating in.

# Clear

The Clear domain is where cause and effect are very clear and so is the solution. This blog is a great example. I want to publish a blog. I write a post, it appears on the internet. It is a known problem with a known solution. If you've ever setup one blog you know you could setup a thousand. I may have some requirements but nothing special to me. I just need to find something which meets my requirements and use it.

The main decisions are around ensuring the selected solution is delivered to time, budget and with adequate scope. These constraints are reasonably fixed and so we follow the classic process of collect and analyse the requirements, find a matching solution that fits, implement it pattern.  Essentially waterfall. 

Some solutions may be clear but that doesn't make them easy to implement. This is often due to the size of the solution. In these situations, breaking the solution down into smaller parts which can be delivered independently is a sensible approach.

How you break that solution down depends on whether you can only establish value when the full solution is delivered or whether you can realise value in smaller pieces.

Agile techniques can be applied in these domains based around creating the appropriate decision points in response to size of the implementation and when you want to get return on investment.  Delivering in these ways won't be doing "true agile" and may look something more similar to what people call **Water-Scrum-Fall**.

## Iterative delivery

Iterative delivery works well when you only need to realise value when the full solution is delivered and there is no point in delivering something partially done. By breaking the solution down into smaller deliverables this enables smaller decisions which can be solved and delivered independently. 

A good example of this is installing a new kitchen. You start by building all the cabinets first and then check they position correctly. Then you may start installing electrics and pipework and check those. Then doors and fixing and check those. Then surfaces. Again checking. Then install appliances. Again a final check before producing a "snagging" list.

At regular intervals (iterations) you introduce decision points enabling you to Plan Do Check Act. With each iteration you ensure that the solution is being delivered according to plan and project managing as necessary.

Regular integration enables clear and regular decisions around delivery. For example, aligning schedules or responding to problems as they arise. Working iteratively simply makes those decision points as regular and often as is reasonable.

What you are not doing is delivering a usable kitchen with each iteration. What you are not doing is gathering requirements as you go along. What you are not doing is discovering new ways to solve the problem. All of those things are fixed. This is really important to understand. Because if you **are** trying to introduce those things as decision points, then you need to introduce them appropriately.

In software the equivalent is iterative development with continuous integration. Development practices, such as automated checks (or tests), provide scaffolding throughout the process which speed up integration and validation. You may even deliver in horizontal layers to fixed contracts (UI first, then backend, then infrastructure) if the requirements of each layer are very clear.

## Incremental delivery

The solution is clear and there is a way of breaking it down so that you can deliver parts independently and gain value from them. There are two reasons you may chose to do this. It could be because you want to realise your return on investment as early as possible or you want to minimise disruption.

A domestic example of this is refurbishing a property. Rather than gutting the entire property in one go, you decide to split it into smaller sequential projects which are fully delivered. Essentially refurbish one room at a time. This means you get to enjoy the newly renovated room as soon as possible (early return on investment) and you don't have to relocate during the process (minimise disruption).

This approach has many advantages for decision making. Rather than making all decisions up-front in one go they can be made between each increment. You can decide the theme for the master bedroom, renovate, then decide the bathroom. You can also change priority (swap the bathroom for the guest suite).

An incremental approach means you deliver a useable room with each increment. Before each increment you gather the requirements for the next deliverable. Once an increment starts those things are fixed. What you are not doing is discovering new ways to solve the problem. 

In software delivery this is when we typically slice solutions "vertically" delivering a slice of each layer as part of the overall solution. Other ways are slicing by segments such as a persona or market and delivering to them in series one at a time. Practices such as Continuous Delivery put the decision for "going live" into the hands of the business owners. 

One challenge with vertical slicing is that it can easily slip into becoming complicated if the way to slice is non-obvious.

# Complicated

These are situations when cause and effect exist but are not clear. Whilst the problem is well understood the requirements and the solution itself are only discoverable with some diagnosis and expertise. This introduces risk due to known unknowns.

Finding a good solution may take some effort but once you have enough information to land on one you can commit to it. In this domain decisions are much more around solution discovery and design through the creation of options and deciding on the trade-offs between them.

Using the domestic example again, this may be that you know you want more space for a growing family. With the help of experts, from financial advisors to property agents to architects you can gather the requirements and generate various options from a range of different homes to move into to different ways to extend your existing property. 

Each solution will have different pros and cons. And each one will require completely different approaches. Trade-offs will need to be made, alternatives generated.

From a decision making perspective what you want is to maximise optionality and bring risks forward as much as possible. These risks are your known unknowns and are usually easily verifiable once detected.

## Emergent solutions

This is the problem domain Agile was born in and showed its superiority over waterfall methods. Due to the highly malleable nature of software, requirements gathering, solution discovery and production delivery could be bundled together rather than as separate phases. 

This is much harder with physical solutions because decisions aren't easily reversible. If I sell my home I can't move back if things didn't work out.

In contrast, with software we can pull the risk forward by making decisions reversible. This enables the discovery of requirements and solutions to be generated through an empirical process: through small feedback loops of trial and error.

To achieve this, Agile methods break problems down into the smallest pieces of value, deliver just enough solution and verify it against real feedback. Based on the feedback, requirements are refined and the solution is adjusted. This is the purpose of a showcase.

This process reduces the burden on up-front decision making and heavy analysis in preference to enabling a solution to emerge based on proof (empirically). This enables you to push as many decisions to the last responsible moment because you can improve the solution as you go. This creates a very large scope for change.

## Incremental delivery

These cycles of feedback are bundled into iterations and released to production in increments in a similar manner to the Clear domain. However, in the Clear domain the solution is fixed and we break the solution down into smaller increments. In the complicated domain the solution is emergent and we break the problem down into smaller problems to solve. 

This means each iteration includes decisions around the problem. The first decision is whether enough of the problem has been solved to move onto the next problem. This is done based on the feedback from each release. If the problem is solved, the decision is which problem to tackle next.

As with the clear domain the decision of when to release value to the end users is held by the business stakeholders. One difference is that because the solution isn't clear this decision is based on reaching an acceptable amount of certainty. Have we solved enough of the problem to bring some value? 

The classic metaphor for this approach is the "skateboard, scooter, bicycle, motorbike, car" evolution.

Agile techniques optimise for establishing that certainty as early as possible. This is why "pushing to production" is an important tenant as the greatest certainty comes from real production users.

Fidelity is often used as a technique for deferring decisions. This means that more naive solutions are chosen early on and are replaced with something more feature rich latter as the solution becomes more sophisticated. This is referred to as Evolutionary Architecture. A common example is using a flat text file over a database. This defers the decision and effort about "what is the right database to use" until the real need arises. This doesn't mean a sacrifice in quality however.

To achieve this the delivery process invests heavily in maximising malleability and feedback loops. Practices from Pair Programming to Test Driven Development to Continuous Delivery to Architectural Fitness Functions prioritise scaffolding for fast feedback and making change as cheap and easy as possible.

In highly advanced teams the concepts of iterations and increments can almost completely disappear to the point where new features are released to users multiple times a day. This creates an environment of very rapid decision making.

# Complex

Not all problems exist in the ordered world. In the unordered domain cause and effect are difficult to understand or are even in a state of flux.

Simply put these are not predictable. Whilst you do know the desired outcome you want (the effect) you neither know the cause of the problem nor the solution to it. No amount of analysis or debate will bring you to a solution. You won't know what will or won't bring about your desired effect until you try it for real. You need to probe first, then sense, then respond.

From a decision making perspective reversibility becomes crucial. Any change needs to be small and safe to fail. A common trap is   trying to make  decisions on Complex matters by applying the same techniques from the Clear or Complicated domain. Instead of achieving the desired reversibility you end up over committing either to implementing a fixed solution or to solving a fixed problem.

The first time many teams are impacted by the complex domain is when they experience continuous changes in priorities or requirements. This is also part of Agile's original allure with the promise of ["Responding to change over following a plan"]([https://agilemanifesto.org/). By delivering in incremental slices, which realise the value as early as possible, when factors outside the system result in a need to pivot the team are able to respond.

In reality many teams struggle with priority changes and find them a source of frustration. This is because change in priority is the symptom not the cause. Priorities change due to complexity. People realise that the solution isn't delivering the desired outcome because they are solving the wrong problem. So they switch to a different problem to solve. Or something else in the environment - loss of customers, competitor launch - forces them to react.

The pain teams feel from this reprioritisation are the result of trying to force the complex world into the ordered world of software delivery too early. In the complicated domain the solution is discovered. In the complex domain the problem is.

Some organisations have managed to successfully exploit Agile when dealing with the Complex domain. Many of the techniques around Agile, reduction in the cost of change, incremental delivery etc. provide a strong foundation for  delivery process which enables emergence. To not only discover solutions but discover the problems too.

## Shift to experimentation

Decision making has now shifted away from implementing solutions to focus on discovering how to achieve desired effects (outcomes). 

This is typically done by identifying and designing experiments and observing the outcomes. The results of the experiment inform your next decision which is usually to commit to more investigation, switch to another hypothesis or abandon the area altogether. At some point enough certainty is established to decide to invest and deliver a solution (usually in the complicated domain).

Teams achieve this by adding the capability to experiment both outside their software through prototypes or proof of concepts and within production software. At an infrastructure level this might include things like A/B testing with sophisticated analytics and telemetry. At a code level it may be things like feature toggles or entire experimental microservices. 

One challenge for teams is the switch between the complex domain and the complicated. In the complicated domain the solution evolves and becomes more sophisticated as new requirements are discovered. Because the problem is known and fixed there is a commitment to the solution as it evolves. Therefore a focus on cross functional criteria such as scalability or operability is critical. 

In the complex domain the problem isn't known. It doesn't make sense to commit to any one solution as the goal is to discover the problem. The solution itself should be readily abandoned. This means framing decisions based on the desired outcome not the problem.

Teams can find this very hard. A lot of Agile practices focus on aspects of quality which may hinder their ability to "Probe-sense-respond". Yet there is a point when the problem will switch into the complicated domain and these concerns will become important. Detecting that moment is not easy. This grey area between complex and complicated can create challenges around things like effective management of technical debt.

# Crossing the domains

Problems aren't fixed in one domain. As we learn more the problem can shift. A great example is infection control. Go back a few centuries and the cause and effect relationships between infection and disease was unknown. Many guesses were made until germ theory finally discovered the relationship. With this understanding we were able to identify different diseases and their causes moving them one by one into the complicated domain. This gave scientists the opportunity to identify common causes of disease and find solutions to tackle them. When Joseph Lister developed sanitation in medical settings he was solving a complicated problem. Now sanitary practices (washing and cleaning wounds with antiseptic wipes) are clear to everyone. 

The same is true for business challenges and software development. As we learn what works overtime the domains shift. A problem which was Complex a few years ago may now be Complicated. And several years later becomes Clear. There were times before version control, and for many years [its benefits were much debated](https://ask.slashdot.org/story/05/01/20/1657218/who-doesnt-use-source-control). Understanding this shift is one function of Wardley Mapping.

As a methodology Agile sits in the space (liminal) between complex and complicated. This means there isn't a sudden line you cross and therefore teams need to be able to shift between the two.

Likewise, when you vertically slice from a desired outcome to a solution you'll find that the whole problem doesn't sit in one domain. Different parts of the problem will sit in different domains. For example, you may be working on a complicated problem but you will still need to chose a version control system or a database, decisions which sit in the Clear domain.

# Helping to decide

Agile techniques can be used effectively in each domain if they are applied appropriately and in a way which supports decision making. To help here is a quick summary:

* *Clear*: known problem known solution. Prefer fixed roadmaps which break **solutions** down into iterative and/or incremental release.

* *Complicated*: known problems, unknown solution. Prefer roadmaps of which break **known problems** down into incrementally releases. Focus on emergent solutions which are delivered iteratively.

* *Complex*: unknown problems, unknown solution. Focus on experiments which enable **problems to emerge**.

Don't jump straight to a delivery approach. Instead understand which domain best fits your decision. Then align your delivery method to fit. This will create the right opportunities which will improve decision making and overall delivery.