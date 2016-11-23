---
layout: post
title: "Why I love Clojure but wouldn't recommend it"
date: 2014-01-07 08:22
comments: true
categories: 
published: false
---

I've been developing in Clojure, full-time, on a real project, for around six months now.  It has definitely been one of the most rewarding and enlightening experiences of my career.  Working with Clojure brings back the buzz I had when I first started working in IT; it is analogous to using Linux for the first time after years in Windows.  Clojure has completely changed the way in which I look at development and how to structure programs.  I think every developer should learn it.  However I wouldn't recommend it for many teams.  Ouch! Really?

Now, I'm one of those developers who really likes picking up new languages, learning new things, being challenged daily.  I'd go as far to claim that the reason I keep doing what I do is because working in development is continuos learning.  And boy does Clojure quench the thirst for learning.  So Clojure, and I, are a perfect pairing.

Yet, if someone came to me and said "I'm thinking of moving my development team to Clojure" I'd go "hang on, don't do that".  Because, unless you have a team of highly motivated, very smart, keen developers who's dream right now is to dump the antiquated and arcane language they use daily to live in the Clojure REPL, then you are setting yourself up to fail.  On the other hand, if you do happen to have that team (and there are plenty of them around) then jump right in.  But there are still a few things you should be aware of before you do.

## Clojure is hard
Boy Clojure is hard.  Mainly because functional programming is hard.  OK, yeah yeah, you've used closures and lambdas and blocks and anonymous classes or whatever 'functional concepts' your OOP language of choice has decided to port, but all your doing is taking sprinklings of some common functional methods, using them in an imperative style and dotting them occasionally around your predominantly imperative codebase; you're not _actually_ doing functional programming in the large.

This is before you start adding in all the other stuff Clojure makes you relearn like brackets and immutability and the relentless focus on data.  And we haven't even got on to tooling.

## Very few imperative/OOP skills are transferable
The Java/C# languages borrowed heavily from C which made it easy for C/C++ developers to move into to a new managed languages with all its magic of garbage collection etc.  Ruby, while lacking the C syntax with its curly brackets and strong typing, was a small leap for any Java/C# developer to take once they'd learnt they didn't need to use type signatures.

Many of the concepts, between the OOP languages stayed fairly consistent.  The terminology of classes, methods and concepts of namespaces, inheritance etc. were all fairly consistent.  Even the libraries were of similar shape and their methods didn't have too different names.  You could write C++ in Java or Java in Ruby and, although the result may not be _idiomatic_ it was functioning.

## You will spend most of your time learning
