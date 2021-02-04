---
layout: post
title: "From failing slowly to learning at speed"
date: 2020-12-17 15:20
comments: true
categories: 
published: true
header-img: img/woman-in-the-air-falling-down.jpg
---

Every organization has ideas on how to improve. Whether that's ideas to maintain existing customers at reduced costs or increased employee satisfaction (run), sell your existing product or service to more customers (grow), or offer entirely new products or services (transform). A business can generate, quite literally, hundreds to thousands of such ideas over a period of months. It's not uncommon for an organization to audit the number of projects in flight and realise they have more ongoing projects than people.

> "Genius is one percent inspiration and ninety-nine percent perspiration". [Thomas Edison]

The ability to generate ideas is rarely a problem for an organisation. The real challenge is whether the ideas generate the positive impact they promise. The reality is that very, very few of them actually will. To give you some idea of just how few, here are some base rates:

-   An estimated [90% of new startups fail](https://review42.com/what-percentage-of-startups-fail/) . No market need is biggest reason 
-   95% of new [product ideas fail](https://www.mindtheproduct.com/outcome-driven-innovation-product-managers/) .
-   70 percent of projects fail. 
-   17 percent go so badly, they threaten the existence of the company!
-   Between 80%-95% of built features are used rarely or not at all
-   Over 80% of [digitization projects fail](https://www.cfodive.com/news/executives-pursue-digital-transformation-projects-despite-80-failure-rate/562148/)

The Geneca "[Doomed from the start?](https://www.geneca.com/why-up-to-75-of-software-projects-will-fail/) " report found that, overall, there was only a 4% chance that a software project will come in on time, on budget and with useful features!

Why is there so much failure? It comes down to two key variables: [overconfidence](https://www.researchgate.net/publication/221598966_Overconfidence_in_IT_Investment_Decisions_Why_Knowledge_can_be_a_Boon_and_Bane_at_the_same_Time) and uncertainty. There is a lot of research on how overconfidence negatively affects decision making quality to the point that it has been called the most "[pervasive and potentially catastrophic](https://en.wikipedia.org/wiki/Overconfidence_effect) " of the biases. And one clear way of measuring overconfidence is to look at the investment. Projects with big budgets, big timelines, big upfront planning all based around one specific solution (lacking optionality) are [those most likely to fail](https://thisiswhatgoodlookslike.com/2012/06/10/gartner-survey-shows-why-projects-fail/), and when they do, they fail the hardest.

Overconfidence is essentially a feeling of certainty about the truth of your judgement which doesn't match objective reality. In the [Art of Action ](https://www.stephenbungay.com/Publications)Stephen Bungay outlines [three gaps](https://www.stephenbungay.com/ExecutingStrategy) between how you envision your idea and how it responds in reality:

-   **The Knowledge Gap**: the difference between what we would like to know and what we actually know
-   **The Alignment Gap**: the difference between what we want people to do and what they actually do
-   **The Effects Gap**: The difference between what we expect our actions to achieve and what they actually achieve

Bungay goes on to argue that many organisations respond to these gaps by employing more analysis, more planning and more detailed solutions and tighter controls around people. These command and control responses increase confidence but do nothing to decrease uncertainty. Not only does failure increase but it also "add[s] cost, paralyse[s] decision-making and demoralises people." The result: "the organisation becomes a slow, expensive robot.".

> "No matter how smart we are, we will never know what will work until we test it. Our responsibility as product managers is to find the ideas that work in the haystack of crap that sounded brilliant---as quickly as possible." [[TrustPilot](https://tech.trustpilot.com/how-do-we-test-it-faster-ca7ccaef4beb)]

To get to success we have to do three things: accept that the majority of our ideas will not work, understand that uncertainty gaps can only be closed through test and learn cycles with real users and, finally, do this at incredibly high speeds. 

The business has to design their organisations and change their processes to optimise for build, measure, learn at high velocity. Businesses need to have visibility of their cycle times from "I have a great idea" to "we have tried it and it worked (unlikely)/didn't work (more likely)". Many companies' cycle times are measured in months, if not years. Yet successful companies measure them in hours and days. As Marty Cagan [points out](https://svpg.com/the-need-for-speed/) *"the ability to learn fast and move fast is arguably one of the only sustainable differentiators"*.

To achieve these velocities requires the organisation aggressively optimises everything from organisational structure to delivery methodology to technology infrastructure. Anything which causes friction or is an obstacle to the learning cycle down needs to be eliminated. Communication and organisational structures are one of the biggest causes of waste which is why the Agile Manifesto states that *"Business people and developers must work together daily throughout the project."*. Decisions need to be made fast, and if collaboration is infrequent and highly formal, requiring handoffs and approvals between stakeholders, then that's not going to happen.

> "You may learn much more from a game you lose than from a game you win. You will have to lose hundreds of games before becoming a good player." [José Raul Capablanca]

Organisations need to move away from delivery mindsets to learning mindsets by switching from a workflow designed around "delivering features" to one designed around "testing hypotheses". Pumping software delivery teams with predefined features and measuring their performance on velocity is a symptom of overconfidence. It only makes sense as an approach when a strong certainty of "being right" is built into the system. As soon as you consider that the solution might be wrong you realise that there are no stages to receive feedback or to change direction based on what has been learned. At best this is the ostrich effect. At worst it is pure hubris, like planning every move of a chess match before you meet your opponent. Months of product delivery and thousands of dollars will literally be wasted before the business runs out of patience and kills the project. 

The process has to optimise for both pre-production learning and production learning. Skipping discovery stages and jumping straight to production is another symptom of overconfidence. After all, if your solution is right why do you need designers to do problem framing, research and feasibility testing? Unfortunately, in reality, skipping this stage increases cycle times by orders of magnitude. As Marty Cagan points out

> [You] might need on the order of 5-15 iterations before it is working as well as it needs to (sometimes referred to as "time to money"). If all of those iterations are done using engineers and each requires releases to production, we're probably at several months if not years of elapsed time, assuming management or the team hasn't lost patience. However, if we can do those same 10-15 iterations in a week of discovery, we've reduced our time to deliver the right solution (defined as both building the right product and building the product right) to our customers from months to days.

Design techniques allow teams to both eliminate and generate more promising solutions based on user feedback in a way which avoids the need for production quality solutioning. Design techniques don't eliminate all uncertainty but they tackle the big risks around solution feasibility early on from the users' perspective. Once confidence increases the risk of productionising a solution is dramatically reduced, yet not entirely eliminated. 

Which is why the production technology itself has to be optimised too. Continuous Delivery, feature toggles, A/B testing, blue/green deploys etc. are all key enablers for high velocity learning. Being able to test changes as safely as possible without negatively impacting users is essential.

To optimise technology to this degree requires an ability for architecture and solutions to adapt and evolve as fast as the feedback cycles allow. A learning system recognises that there is no pre-fixed destination, so any architectural or technological decisions we make today are highly likely to be invalidated tomorrow. Therefore our approach to these decisions has to also have uncertainty at its heart. One of the common mistakes teams make is to try and drive up speed under uncertainty by sacrificing quality in the fundamentals. The impact is to push cost of change up and productivity down. As teams accumulate increasing amounts of technical debt their cycle time goes into a tailspin until the point where ROI becomes impossible except by making large impact investments (and we return to big upfront projects).

Ultimately though, leaders need to look at their delivery process. Is it designed to cope with uncertainty? Is it able to employ different tactics (proof of concept, mock-ups, user testing etc.) for different types of uncertainty in different phases of the product evolution? And of course, does the process generate the right kind of incentives which promote a learning mindset over one which rewards hubris?