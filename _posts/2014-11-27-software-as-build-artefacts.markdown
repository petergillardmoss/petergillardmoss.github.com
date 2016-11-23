---
layout: post
title: "Software as build artefacts"
date: 2014-11-27 14:04
comments: true
categories: 
published: false
---

Sometimes it makes sense to identify a good practice by highlighting a bad one.  Many moons ago Microsoft pushed a feature of ASP.NET they called "xcopy deployment".  The idea was simple and somewhat elegant: to deploy your website you simply did an xcopy.  This feature quickly became much abused and what resulted was an anti-pattern I call:

## Source tree as deployable anti-pattern

The easiest way to deploy, using xcopy deployment, is to simply deploy your source tree up to the server, as is.  Back in the early days of .NET this was an all too common practise (in many ways encouraged by the Microsoft tooling) fraught with problems.  There was a complete lack of traceability, separating configuration for different environments was cumbersome (made worse by the uber-configuration that was web.config) and another whole host of problems due to dependency mismatches, compilation errors etc.  

This was of course in the days before Continuous Integration.  However I have noticed that this anti-pattern is having a revival in open source software combined with another pattern I call:

## git clone deployment/git pull to upgrade

An increasing number of open source projects (Octopress, Phabricator, Hubot) only support this method for deploying and upgrading their software.  To deploy the software you git clone it.  To upgrade it you do a git pull.  And some make the situation even worse by adding in ```git fork``` to manage configuration changes.  

Actually, in its own right, source control, such as git, theoretically provide an acceptable vehicle for deployment in certain cases as you get all of the benefits of source control with easy rollback etc. (```git checkout SHA```) - there are however issues from side effects such as dirty trees etc..   
However, when combined with _Source tree as deployable_ it is an abomination of complexity and mess.

## Snowflakes and the automation quotient

Anyone who has tried to install a product using the above patterns on a production server knows full well what a mess it is.  There tends to be a full wiki page with several lines of complex installation instructions full of caveats and branches and then another wiki page of complex configuration instructions full of caveats and branches.  The deployment process is snowflake orientated and actively encourages them.  Add in ```git fork``` for configuration and the snowflake quotient goes up to max.

The more sensible of us try to automate deployments.  Especially when they are as complex as these.  However their automation quotient is low.  These lack the ability to run simple ansible commands to ```yum install``` or even ```tar -xvf```. They are horribly intricate steps of ```git clone``` and the running of Rake files and other such stuff which are rarely idempotent.  In all honesty it makes me yearn for the old ```make ./configure install``` days that brought Linux much of its reputation for being unusable.

## Optimised for the developer lifecycle

The reasons for the above complexities are the products are optimised for the developer lifecycle and not for a full delivery lifecycle.  As developers we need to make larges amounts of changes over incredibly short periods of time and therefore we optimise our build processes around that.  Our change cycles need to be a short as possible, common development tasks, such as compiling and running tests, need to be automated and quick to hand.  Therefore a large amount of work is done 'in place' and, more often than not, developers spend the vast majority of their existence inside a source tree that is in a constant state of flux.

Source trees are not clean places.  They collect rubbish and debris.  They contain significant amounts of code which exist purely to support the development process and are redundant or potentially destructive in production.  They contain complex ignore rules and they often follow their own unique conventions.  This is why Continuous Integration is a necessity: because the state of the source tree needs constant verification.  Which is why they are wholly unsuited to being xcopy/git clone deployed.

## Software as build artefacts

A software product, whether Open Source or Enterprise or Startup should be.

## Lack of conventions
## Artefacts as a first class concept

- Separation of concerns
- Atomic unit
-- declaration of dependencies

- Build file swallows the world!

- 

- Composable artefacts




