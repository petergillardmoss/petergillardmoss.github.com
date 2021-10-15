---
layout: post
title: "How Agile scaffolds enable emergence"
date: 2021-10-15 08:20
comments: true
categories: 
published: true
header-img: 
social-img: "img/scaffolding-workers-construction-site.jpeg"
description: "Scaffolds are temporary structures which enable emergence and then disappear. Which agile practices can be employed as scaffolding?"






---

Ann Pendleton-Jullian coined the metaphor of scaffolding when she was working on a case study of General Stan McChrystal's transformation of JSOC. She wanted to contrast frameworks with scaffolds.

Frameworks are *"a complete structure, usually permanent, and gives forms to that which it supports, or encloses, or solves".* Where as a scaffold acts as a *"temporary structure for supporting something until that something can stand on its own"*.

I've found myself in that place where an idea resonates and pulls on some underlying truth but I struggle with its application (does that put me in aporetic domain?).

When I'm stuck here I need to have a play. Take the ideas and throw them at something, see what fits and what falls. Often with a big wet slap.

As enabling emergence is a key quality of agile practice then surely, if I root about in the agile practices box I might find some things to throw?

Basically, this is the result of what I think might have successfully stuck.

Ann, along with others, have proposed [five basic types of scaffold](https://cynefin.io/wiki/Scaffolding). I'll attempt to see if I can find agile practices which might fit these metaphors.

**Building scaffolds** *enable building crews to construct new buildings and are erected with the knowledge of the final shape. When work is done they are taken down.*

A good example of this is probably the Story. The articulation of value (*As a, I want, So that*) along with acceptance criteria (*Given, When, Then*) allow the building crew (in this case the developers) to find the best solution to meet the value. When the story is done (delivered) the card has served its purpose and is archived away.

An important quality Stories share with real building scaffold, is neither contain any implementation detail. Anything could appear within in them.

This also highlights why poor practices around stories can cause issues. A common anti-pattern is to turn them into implementation specific tasks or requirements. Rather than acting as scaffolds which enable solutions to emerge they become blueprints.

**Neural lattices** *stay part of the structure but are transformed in the process. The example used is a Bionic Cardiac Patch which both enables the regeneration of cardiac tissue and also provides pacemaker technology which detects and corrects cardiac arrhythmia.*

I feel this metaphor perfectly explains Continuous Delivery. The delivery pipeline both acts as a seed for the production software and provides the pulse and rhythm for change.

Practices like Test Driven Design and Fitness Functions may fit into this category. The test provides the initial scaffold which seed an emergent design. Whilst the tests themselves don't form part of the final structure they remain in place checking for anomalies, like the cardiac patch.

**Skin grafts or nutrient lattices** *work by providing the nutrients which activate the generation of new skin. As the skin reforms the scaffolding dissolves away, leaving no trace.*

I would put a collection of techniques under here from User Journeys to Personas to Story Mapping to Domain Driven Design to Event Storming.

Unlike a building scaffold these activities don't provide knowledge of the final shape and act as a container. Instead, like the skin graft, they provide the scaffold from which we generate ideas from.

We can start off with a user journey and plot out the key stories we need to deliver to start, or form a domain model which identifies the key parts of our language and relationships between data.

Once the exercises are done, usually using low fidelity tooling like white boards, they dissolve away leaving the real user journeys or the real domain model in place.

A common trap is to over analyse these stages and make them specifications. And a common frustration is often that these things have dissolved away leaving no permanent artefacts.

A common explanation for the lack of need of permanent artefacts, for example around domain models, is often that the code is living documentation. By seeing these activities through the metaphor of a nutrient scaffold adds weight to this reasoning.

Practices like walking skeletons and tracer bullets also fit under these types of scaffold. Again they provide the initial scaffolding for a emergent solution to grow from and then dissolve away as the solution takes over rather than being removed like building scaffold.

**Keystone scaffolds** *provide foundations for other structures to be built on. Arches are the example used where the archway is built around the keystone. Removing the keystone can cause the arch to collapse.*

These scaffolds I have really struggled to understand. Everything I throw at them slips off too easily or fits better somewhere else. Maybe because they become invisible and forgotten?

A few practices which make sense are things like Feature Leads, or Story Leads. Here these people act as knowledge keystones. Team's learn that lack of continuity on a story or across features can cause the solution to collapse.

I also wonder if practices like source control, especially Configuration as Code and Infrastructure as Code count here. These are often keystones to enable emergence in a safe way. When teams unwittingly remove these practices they begin to experience configuration drift which fits with the metaphor of removing a keystone and higher structures slipping unexpectedly and uncontrollably.

**Shadow scaffolding** *enables emergence across multiple interactions over long periods of time. Examples used are extreme sports infrastructure like training, peer group interaction, technology developments and apprentice type practices.*

Practices such as pair programming, rotations and retrospectives sit here. They enable emergence through improved team dynamics.

I feel retrospectives done well are a perfect example of a shadow scaffold which enables emergence through reflection and improvement of processes. And yet, perhaps because they aren't explicitly part of finding a solution, they become tempting to drop.

**Agile Frameworks vs Agile Scaffolding**

At the end of this I hit a realisation. Scaled Agile Framework (SAFe). Framework! ***Framework!***

Perhaps this metaphor sums up some people's aversion towards SAFe? Would they rather employ agile as a set of scaffolds to be used to enable emergence? Where as SAFe is a framework to enclose and force structure?

**Any more for any more?**

This feels a good start to thinking in this way. I wonder if I've got them right or are there any interesting ones you think would fit the metaphor?