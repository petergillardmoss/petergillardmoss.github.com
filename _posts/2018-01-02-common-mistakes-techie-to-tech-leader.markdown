---
layout: post
title: "Techie to Tech Lead: My most common mistakes"
date: 2018-01-02 09:20
comments: true
categories: 
published: false
---

As a young ambitious developer with a strong sense of his own talent I was eager to become a Tech Lead and it took less than four years for me to achieve this goal.  Over the next two years the experience and reality of leading a team put me off leadership completely.  For several years I retreated back into the security of technology shunning any opportunity to take more responsibility.

Over time I came to understand the root causes of my mistakes and eventually regained the confidence to accept new leadership opportunities and grow as a leader and with the right support over the last two years I've grown as a Head of Technology inside ThoughtWorks.  Through coaching and mentoring other leads I have learned that the mistakes I made weren't unique to me but are common amongst technologists who move into leadership.

I'd like to share my mistakes and what I have learned in the hope that others may benefit.

# 1: Ability does not give you an entitlement to lead

In my first tech lead role I had hired a talented young graduate.  We worked really well together and pushed each other forwards into new ideas and skills.  Yet within a few months I realised that, despite their inexperience, they were more technically able than me.  As the Tech Lead I felt that I had to prove myself as the most technically capable and I would feel insecure every time he demonstrated his ability to others (especially my managers) concerned that they would view him as more suitable for my role than me.  What originally was a great working relationship suffered from feelings of competitiveness and mistrust.  Rather than seeing him as a collaborator I was seeing him as a threat.

Someone's technical ability is often one of the biggest factors when choosing them as leaders.  It is also certainly the most visible factor.  And here begins my first mistake: conflating that ability with the entitlement to lead.

In my example, this conflation lead to unhelpful competitive behaviours.  A lot of my insecurity came from environment and my own mistaken sense of entitlement.  But even in the most modest and deserving of people this mistake can aggravate imposter syndrome and the lead may perceive other members of the team as more worthy and underestimate their own contributions and struggle to understand their own worth.  When this happens leads can become indecisive and avoid making decisions instead defering to those whom they believe to be more deserving.

This mistake can also prevent good people putting themselves forward for lead roles as they believe the most technically competent individual has the right to lead.

# 2: Deep growth shouldn't be prioritised over broad growth

I was very excited about my first lead role.  It was a brand new team with a green field project. I introduced new technologies and practices, from unit testing, ORM, continuous integration, pairing, optimistic source control, nant build files. If I read a blog post about an exciting new idea I incorporated it into our processes and tools.

And there lay just one of the many mistakes which made the next two years one of the biggest frustrations and failures of my professional life.  I had fallen for a romantic portrayal of leadership as being purely visionary and believed that ability to lead was down to the strength of technical vision.

Choosing tools and technologies was all iteration 0 work.  Now came the day-to-day stuff.  The managing, dealing with stakeholders, representing your team in meetings, performance reviews, recruitment, budgets etc.  And whilst I knew enough to select svn, nunit, CruiseControl and C#, I had no idea about all that other stuff.

I began to resent the activities I didn't understand and found difficult. Rather than address my gaps I focused more on the things I felt I could control: technology.  This only aggravated my imposter syndrome, especially if I was in a meeting with other managers who would confidently talk about growing their teams by bringing in training or making business cases for investment or new team members or disaster recovery plans etc.

Techies aren't chosen for leadership roles based on their technical ability alone.  It is also due to the many other strengths, from influencing and persuading, to coaching, to understanding processes, to being a trusted advisor, to dealing with complexity, to strategic thinking (and many more), which would have stood out alongside technical prowess.  These competencies are much less visible and are probably needed in more nuanced ways throughout the working day and week.

It's important for new leads to understand the significance of these other competencies and the need to build themselves out in breadth across many areas.  Otherwise they risk turning towards their most visible strength - technology - and focus on building depth.

Another trap is that it is relatively easy thing for a technologist to build up new technical competencies.  We're used to acquiring technical skills, we know the formulas, the blog pages, the stack overflow posts, the ThoughtLeaders to follow, the conferences to attend, the books to read.  Given a half decent 'Hello World' example and a few spikes later we're well on our way to picking up a new technology.

But other competencies don't work this way.  There isn't a 'Hello World' for coaching or time management or influencing or persuading or articulating business value.  We don't know who to follow on Twitter to get the _right way_ to communicate decisions or organise teams or manage stakeholders.

This makes movement into the new domains required for leadership expensive.  As many of these domains are relatively new the lead is left feeling lost and intimidated.  They may also mistakenly prioritise developing new technical competencies which are quick and easy to pick up and have obvious value over alien competencies which are hard to get into without clear value.

# 3: Continuing to see yourself as a producer

After a few months into my first tech lead role I was becoming increasingly anxious.  I seemed to be needed to do a lot of things that didn't feel productive.  Less and less of my time was spent pairing and writing code as I was busy in meetings, replying to emails, answering questions from stakeholders etc.  Every story with my name on felt as if it wasn't progressing.  My response was to sacrifice my personal time to make up what I'd missed due to these distractions (as I perceived them).  I quickly became overworked.

What I hadn't realised, when I moved from a techie to tech lead, was how my responsibilities, in terms of being a producer, had changed.  If you look at any delivery team you can see the main goal is to maximise the amount of *value* produced.  Under this light there are two main activities in the team: those that directly produce value, and those that work to maximise the impact of what is produced.  One of the simplest (but by no means the only) ways to do this is to ensure that the producers (in this case the developers) have the maximum time to focus on productive activities (i.e. producing code).  The rest of the team, from PM to BA to QA are working to ensure that the flow of work is as correct and smooth as possible and doesn't get blocked or create failure demand (due to bugs etc.).  Simple version: in order to keep developers productive the team around them work to remove any obstacles or distractions so developers can focus on writing the right code to deliver value.

When someone moves from techie to Tech Lead they are shifting from being one of the producers to being part of the team whose goal is to maximise overall impact (which includes removing obstacles and blockers).

This misunderstanding places a lot of stress on the new Tech Lead especially around time management. Specifically a feeling of not having enough time to code or pair with others.  Sometimes this is expressed in frustrations of too many meetings or a desire to have meetings only at certain times (core coding/pairing hours etc.).  In some extreme cases I've seen this manifest as a complete rejection of any activities which were not considered technical (talking to stakeholders for example).  All of these originate from the Tech Lead's perception of being a direct producer rather than as someone who is maximising the impact of others.

In my case it even led to me perceiving myself as the main contributor in the team.  I've seen this happen a lot with others too especially in smaller teams where there is a large skills gap between the lead and the other members.  Under the combined pressure from additional responsibility along with normal delivery pressures the Tech Lead can feel that if they shift away from writing code the productivity of the team will significantly suffer.

# 4: You can't know or control everything

One day I was in a meeting when a manager asked about a bug.  Having never worked in that area of the application I struggled to answer the question and the more I tried the less convincing I became.  In the end, for fear of exposing my ignorance, I made an educated guess.   Turned out that other teams started making changes in their applications to accommodate for my guess and, after wasting a load of effort, they discovered I'd been wrong.  I attributed my failure to ignorance and tried to prevent it happening again by reading the commit log at the start of everyday.

When reading the commits I noticed a piece of code that looked rather procedural and I felt could have been more object orientated.  I sat down with the developer and discussed trying a different approach.  I decided to pair with them and became absorbed in this small area of the code for several days.  At the same time another pair were working on a big architectural change.  When they released it caused a bug due to a simple incorrect assumption which I should have picked up.

I was honest with my manager about what had happened, I'd been focusing on getting this code right and missed what the other pair were doing.  But I struggled with the feedback that I was worrying about things that weren't important.  Surely making sure we were doing OOP code was important?  Their response? I needed to pick my battles.

Both these situations had the same thing in common: that I couldn't be involved in everything that was happening.  It was humanly impossible.  As a Tech Lead I had to trust others with responsibilities and focus on the most important things.  Sometimes that would mean ignorance and other times it would mean that things weren't done exactly the way I would chose to do them or even that they were done in a less than ideal way.  Saying "I don't know, I need to check with the team" was OK but spreading misinformation because I guessed was not.  And having a little things that weren't quite perfect, like a bit of procedural code, was OK.  But taking on large architectural change without my oversight was not acceptable.  

This also forced me to realise that there are other tools, such as mentoring and running code reviews as a team, which are far more effective in improving the code base over the longer term than trying to fix every small issue as and when it arose.  

# 5: The signals change

I'd attend all these meetings but my frustrations grew as I felt nothing was changing.  My contributions didn't seem to turn into anything concrete.  We'd discuss having the test team work with the developers on each story, we'd try it once and then we'd go back to queuing everything up for pre-prod.  People would agree that the developers should own the database but we'd still wait for the DBAs to build stored procedures.  I'd coach developers on TDD but an iteration in and everyone had given up on it.  Everything felt like a talking shop were nothing got done and I felt increasingly frustrated and despondent.

When technology is your every minute of every day you become attuned to the feedback loops and signals put in place.  But when you move into a leadership role the signals come from other places.  

It's hard for techies to detect this shift especially as the concerns of each day are mainly the same: stories still need to be picked up and delivered, code needs to be written.  So the signals a new lead receive still look technical.  

When moving into Leadership roles we need to look out for and learn the other signals.  If we want to change direction we must influence others.  We must learn to see the signals that tell us who understands our ideas and whether they are convinced and supportive or skeptical.  There are also other signals around team members struggling with load and needing support or people who feel are missing the tools to develop new skills or disciplines or communication structures which may be missing which is why people are ignorant of what the team is trying to achieve.  Often these signals are hard to detect because they come from people, who often hide or mask or misfire.  Detecting these signals is almost a sixth sense which you develop with experience and when you are not attuned to them you don't even realise they exist.  And they are also have to be treated with caution as they may not always be from what you think.

The really good leaders seemed to be highly attuned to all these signals and understand how to interpret and respond to them.  Although it can look like a dark art akin to reading the tea leaves or animal entrails it there is real rational approaches which, although aren't as deterministic and certain as technology, are learnable.

One thing you may have noticed is that a lot of these mistakes relate to each other.  For example, it is hard to stop seeing yourself as a producer when you believe your technical ability is your reason for leading which can make it harder to develop other skills.  The way these mistakes fed into each other is what put my leadership journey into a death spiral.
