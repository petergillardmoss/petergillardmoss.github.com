---
layout: post
title: "Lines and Graphs"
date: 2026-04-21 06:00
comments: true
categories:
published: true
header-img: img/graph_lines.png
social-img: img/graph_lines_teaser.png
description: "Agents are helping us rediscover something fundamental about how Agile actually works."
---

# Lines and Graphs

*Why agents are forcing us to rethink how software work is shaped.*

Working with agents on a real product has forced me to rethink something I thought I already understood. The usual framing of Agile vs Waterfall is process. That's wrong. It's about shape. Waterfall is a line. Agile, when it actually works, is a graph.

## The wrong framing

Linear processes assume you can pick the right path upfront: spec → plan → build → test. It feels efficient because decisions are made once, progress looks clean, and everything is easy to explain. But it's a bet. You're replacing path-finding with prediction.

Graph-based work starts from a different place: you don't know the path yet. So instead of trying to define it, you navigate. Intent, examples, tests, code, decisions — all connected. You move between them, not through them.

## Graphs are path-finding problems

The key insight is that this is a path-finding problem. And the thing that makes it work isn't iteration in the vague sense — it's feedback that prunes the search space. In software, that's executable examples and tests. They don't tell you where to go. They tell you when you've gone somewhere invalid.

There's a useful parallel in *The Myth of the Objective*. You can't plan your way through a maze; you need a knowledge base that tells you where the dead ends are. That's exactly what examples and tests become. Not documentation, but a system that remembers where not to go.

## Why upfront thinking still matters

A lot of Agile criticism lands in the wrong place. People say Agile doesn't do enough upfront thinking, especially around architecture. That's true if you treat Agile as a linear process with smaller steps. But that's not what's actually happening in effective teams.

Upfront thinking in a graph system isn't about defining the path. It's about eliminating obviously bad ones. Constraints, invariants, clear behaviour. You shrink the search space before you start moving.

## Small steps aren't enough

Another trap is thinking that breaking work into smaller steps gets you there. It doesn't. That just gives you a more granular line. You're still following a plan, just checking in more often. You're not navigating.

## Agents don't smooth over ambiguity

The part that really clicked working with agents is that they don't talk, align, and move on. They execute literally. Any ambiguity in your system doesn't get smoothed over — it gets amplified. That shifts the bottleneck away from writing code, or even tests, and onto defining behaviour clearly enough to execute.

This is why practices like Extreme Programming are suddenly feeling relevant again. Not because they're nostalgic, but because they already solve this problem. Small steps, continuous integration, test-first thinking, tight feedback loops. They weren't random engineering preferences — they were ways of making graph-shaped work viable. Agents just remove the excuses. They prefer environments where behaviour is explicit and feedback is immediate.

This also reframes a lot of the current discourse about coding agents. Success is usually attributed to better prompting or perfected agent configurations. But many of the teams that succeed are unintentionally building graph-shaped systems. What gets described as "enforcing TDD" or "strong agent rules" is really the emergence of tightly constrained feedback loops — intent → examples → tests → implementation turned into a navigable structure. The difference isn't awareness of the model. It's whether the workflow accidentally forms a graph that continuously prunes invalid paths.

## Linear loops inside graphs

Graph-based systems don't eliminate linear processes. They exploit them — for a different purpose. In a graph system, linear processes are short, repeatable, and tightly coupled to feedback. They exist to constrain movement and make invalid paths visible quickly.

Continuous deployment is a good example. It's a strictly linear pipeline, but its job isn't planning — it's enforcement and fast feedback. Red–green–refactor is another. A small human-scale loop that forces a path, validates it immediately, and tightens understanding step by step.

So graphs aren't "non-linear chaos". They're composed of many small linear loops whose job is to create tight feedback and constraint.

## Managing partial progress

There's a practical piece that matters more than it sounds: graphs require a way to manage partial progress. You need to be able to pause a path, explore another, and come back or discard it. Think `git stash`. Push work aside, try something else, return if it holds. That's not just tooling — it's what makes non-linear navigation viable.

## How graph systems fail

A common signal of weakness is a whack-a-mole effect. You fix one issue and another appears elsewhere. That's not just complexity — it's a sign the system isn't pruning invalid paths properly. You're treating symptoms locally instead of eliminating whole classes of behaviour.

Where this really falls down in practice is cost. Graph-based systems are expensive to maintain, and much of that cost is invisible. Keeping tests reliable, builds stable, feedback loops fast. When that degrades — flaky tests, slow builds — the pressure is always to bypass it. Disable the test. Skip the build. Ship anyway. That's linear thinking reasserting itself. And the problem is that you're removing the mechanism that makes navigation safe.

Historically, teams have got away with this because humans compensate. They fill in gaps, infer intent, spot issues late. Agents don't do that. They execute what is explicitly there. So weak feedback systems don't degrade gracefully — they fail immediately and repeatedly.

The shift now is twofold. You can't bypass feedback loops without breaking the system. And the cost of maintaining them is dropping. Agents can generate, fix, and maintain tests and build systems. The invisible overhead of keeping the graph healthy becomes cheaper and more automated.

So TDD, BDD, CI/CD, DevOps, even ideas like fitness functions from evolutionary architecture — these weren't separate ideas. They were all converging on the same thing: how to make graph-shaped work stable under uncertainty. They just didn't have the language for it.

## Imposed process overwrites the graph

Graph systems also explain something that often gets misunderstood: resistance to imposed process.

When a team is working well, they've already built a graph. It's embedded in their artefacts, their feedback loops, their constraints, and how they move between states. If you impose a top-down process — "you must follow this version of Scrum" — you don't just add structure. You overwrite their graph. You replace navigation with compliance.

That's why it feels like productivity drops even when process compliance improves.

The nuance is this: you can standardise constraints, not paths. You can standardise quality gates, deployment pipelines, testing expectations, and definitions of done. These shape the graph. But you can't prescribe the graph itself. Each team will evolve a different one based on their domain, constraints, and feedback loops.

## Why spec-driven approaches drift

This brings us to a deeper failure mode in spec-driven approaches.

Spec-driven systems implicitly assume that a graph of behaviour can be reconstructed from a linear description. Spec → inferred graph → implementation. That reconstruction step is the weak link. It assumes no ambiguity in intent, no missing constraints, consistent interpretation, and correct mental model alignment.

With agents in the loop, that assumption breaks down faster. Specs don't reliably reconstruct into the same graph across contexts. You end up with drift between intent, implementation, and validation.

Graph-driven systems remove that step entirely. The structure is explicit through examples, tests, and constraints. There's no inference layer to fail. When hearing from some proponents of Spec driven, it sounds like this is how they implement it, leveraging specs in a graph, rather than using it as a linear process. 

## The role of humans

Humans don't disappear in this model. They move up a level. They design the graph — intent, constraints, examples. They evolve it as understanding changes. They intervene when reality breaks the model.

Agents traverse the graph. Humans govern it.

And sometimes humans have to override it entirely — especially in situations the system wasn't designed for, like production incidents. That requires judgement, context, and experience. Agents can't reliably do that because it involves stepping outside the graph itself.

So the system becomes a partnership: agents optimise traversal, humans maintain structure and handle exceptions. The more capable agents become, the more important that distinction becomes — not less.

## So what's actually different

The difference isn't speed or flexibility. It's this: linear systems try to choose the right path upfront. Graph systems make wrong paths obvious and cheap. Linear pre-selects the path. Graph constrains the moves.

And this is why graphs adapt to linear easily, but not the other way round. A line is just a constrained graph. You can force a graph down a single path. But you can't turn a line into a graph without adding feedback loops, multiple paths, and ways to manage in-progress work.

Agents just make all of this impossible to ignore. They remove the human ability to paper over ambiguity. So you're forced to build systems where intent is explicit, behaviour is executable, and invalid moves fail immediately. Not only that, AI performance unlocks when using graphs, and struggles with linear processes. Graphs are simply far more agent friendly.

It's less like following a plan and more like navigating a system with continuous feedback. And once you see it that way, a lot of Agile vs Waterfall debates start to look a bit superficial.
