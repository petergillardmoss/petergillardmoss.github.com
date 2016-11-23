---
layout: post
title: "The (almost) perfect dev and build environment"
date: 2014-02-14 09:33
comments: true
categories: 
published: false
---
Management of developer boxes is a nightmare.  Infrastructure gave up on it long ago.  It became pragmatic to grant developers root access and leave them to construct the most complex, fragile and unstable machines connected to the network.

Yet consistency is paramount for developers.  How many hours are wasted debugging programs only to discover half the team was a single point version out of some obscure library from everyone else?  Or that someone had installed a package which had updated /etc/alternatives to point to the OpenJDK and not SunJDK?

The various attempts to build consistent and cheap to recreate dev environments include README docs, shared folders of shell scripts, imaged machines (e.g. ghost), VMs, to centralized configuration management (such as puppet/chef).  Most have started off well and drifted, rotted and withered as they fail to keep up with change.

And all this is all before someone needs to work on multiple projects from the same box that requires a different version of Rails! And all this is before you start trying to install Intellij plugins or get emacs modes right.  

And then there's the build server to sort out...

Well, I believe that the teams I've worked with have solved the problems (within the restrictions of current technology) and I want to share with you how.

# What it looks like
Overall it's pretty simple really, and a teeny bit obvious.  A vagrant box and some scripts (Puppet, Ansible, whatever).  The scripts do everything, set the box up, install all the relevant tools, sort out repo credentials, copy ssh keys, individual configuration files etc.  They even check out all the codebases you need.  Creating a new box, from scratch, takes very little time.  The team work off of the vagrant boxes and if anything goes wrong, well they kill it and start again.  In fact it's a good idea to regularly kill the boxes anyway.

However it's still hard to get Vagrant working, even with a load of scripts.  Developers often develop multiple applications which use different tools and different dependencies.  Often people jump through hoops, use clever tricks or suffer little inconsistencies because no two applications share the same exact environment (perhaps a different version of ruby or a different version of Rake).  Sometimes it can become difficult to upgrade one repo because it affects another and careful planning is needed.  

This pain can all be avoided and different applications can play together on the same developer boxes nicely and without issues.

# Layers
To start think of your development environment in terms of layers:

* General tools
* Application dependencies
* Developer specific configuration

You want to manage these different layers in different ways and in different areas.  This gives you the freedom to make changes at each layer whilst avoiding nasty side-effects in others.  

## General tools 
These are the things that you, as a developer, use to enable you to develop before you even check any code out. Things like Intellij, emacs, git, helpful aliases etc. etc.  

General tools will sit more happily in a shared repo of configuration management scripts (ansible, chef, puppet, shell etc.) that any developer can modify.  They could be applied manually when the developer decides, on boot up or from a centralised puppet master, or via vagrant, knife etc.

It is possible there is some variance as some developers might prefer different tools (vi vs emacs, Gnome vs KDE etc. etc.).  This can be accommodated at this layer whilst maintaining a degree of consistency across machines.  For example you could pass options on boot such as ```OPTIONS=emacs,KDE vagrant up``` or ```OPTIONS=vi,no-x vagrant up```.

## Application dependencies
These are the things the specific application you are developing needs to enable its development.  Think things like postgresql, ruby, java-sdk etc. etc.

This is where many automated environments go wrong.  Too often the application dependencies get put in the [General Tools] layer.  This creates a versioning issue between the two layers and leads to inconsistencies and bugs (especially as people forget).

Keep the management of the application's dependencies in a script in the application repository (preferably in the root).  If one developer decides to add markdown to produce web pages, or sass to produce css, then every machine which needs to build has the dependency installed upon running of this script.  This may lead to repetition where some applications setup the same dependencies but avoid the temptation to globalise these settings as it increases complexity and makes it harder to understand what dependencies each application requires.

It helps to make this script part of your every day work so people are habitual in their running of it.  So add it to a build wrapper script or make it essential to begin work.  A tip is to only add tools to the system PATH once the script is run.

## Developer specific configuration
Each developer will have pieces of data that are specific to them.  Account ids, passwords, test system urls, public/private keys etc.  Keep these out of the code and into configuration files.

Generally you will need configuration for each layer.  So you may need things like github ids in [General tools] to enable the checking out of the application repositories.  And each application will need things like DB usernames etc.  Each application should manage it's own configuration locally.

One tip is to leverage the [General tools] layer to help manage the configuration for each application.  This allows you to preserve configuration between machine rebuilds (so if you destroy your machine you don't lose your config).  For example you could keep a folder of application configs which the [General tools] layer ensures are copied across after checking out the repo.  

# The application repo
## Check-out-and-run
This principle is a simple idea: given a fresh laptop with a fresh checkout of the code you should be able to run the project and develop even if you were stuck on a plane without any internet connection.  Essentially there should be no external dependencies.

## Single point of entry
A single, well known script should provide end-to-end setup (for each layer).  There shouldn't be a 'dev' script, a 'build' script etc.  Just one, the same one, that everyone uses.

## Version controlled dependencies
Version controlling dependencies gives complete tracebility and auditability.  It also removes large amounts of complexity and ambiguity by bringing consistency to the project.

The most naive implementation of _check-out-and-run_ simply checks in all an applications dependencies (jars, dlls etc.), generally into the project root's `tools/` directory. Latterly tools such as Bundler and Maven allowed developers to hand dependency management off to a tool and keep the binaries out of version control* whilst maintaining all the important properties. *some people still argue that dependencies should be checked in but that is a moot point in terms of this article.

## One application one repository
Keep all code, relating to a single application or service in one repository.  This allows teams to modify and improve build, test, deployment and provisioning within a single context.  When combined with [As close to production as possible] it also allows teams to share scripts and broaden their coverage.

## Don't check in configuration
Configuration (db usernames and passwords etc.) should *never* be hardcoded and should *never* be checked into the codebase.  Instead use configuration files.  Or better still follow the [12 Factor Apps principles of using environment variables][envvars].

## Leverage the OS
Use the tools and standards that the OS provides.  Use system packages, use environment variables etc.

## Automate everything
An aggressive approach to automation ensures that processes are consistent and makes them incredibly cheap to reproduce.  This is especially true with development boxes where one manual step creates ambiguity, drift and bugs.

### Infrastructure as Code
The _everything_ in _Automate everything_ goes beyond running the application they were building.  Bringing IasC broadens _everything_ to include the entire setup and configuration of your development box.  This eliminates drift at a system level making _everything_ consistent.

## Cheap to reproduce/disposable
Development environments should be incredibly cheap to reproduce.  Creating a new reliable environment should take a few minutes.  A side effect of this is that it makes the environments disposable.

## As close to production as possible
Your development environment needs to be as close to your production environment _as possible_.  If you deploy to centos develop on centos.

By developing on a production like stack you eliminate huge swathes of complexity and drive out bugs.  But you also get a lot of reuse and shared understanding.  If your dev, build and prod machines are the same then that's only one platform with one set of shared scripts etc. to worry about automating and not three, as is often the case.

$$This would be good in a box$$
In this context _possible_ is a little bit of a get out clause.  After all you'd struggle to develop iOS apps on iOS.  And sometimes you have multiple platforms, and sometimes all the development tools aren't available on the platform.  At least get to the point where if you actually run any code (tests etc.) you are running it pretty much the same OS.

## Ownership/self service
Development teams need to be able to own and manage their development and build environments themselves with the minimum friction.  Any barrier between a dev identifying a change and being able to implement the change risks drift and drift is failure.

Devs should be confident that all they need to do is simply open a script, in the apps repository, change it and check in.


# In practice
Principles are all great but how do they translate into practise?

Essentially, what this means is a bunch of scripts which install and configure various parts of your development environment.  The trick is to put the right bits in the right scripts and have them invoked from the right places.



## Trust system packages
They are your friend.  Package maintainers go to a lot of effort to minimize side effects and clashes with other system applications and tools.  You can place a far higher trust on system packages that anything your script cobbles together.  They will also match the packages you will be using in production.

Sometimes there isn't a system package.  In these cases make one yourself.  The benefits of reuse, management etc. far outweigh the initial learning curve and effort.

## Achieving isolation
Trust system packages but avoid making changes at the system level that alter the expected behaviour at the system overall.  So, if the system uses ruby1.8 by default don't switch it to use ruby1.9.  This means that other applications cannot make safe assumptions and risk being affected by the system change. 

### Explicit
Where there is a chance of ambiguity in system packages be explicit and don't rely on defaults or symlinks to point you to the correct version.  So don't use ```ruby``` from the path or ```/usr/bin/ruby``` but be explicit and refer to ```/usr/bin/ruby1.9```.

### Local
Some tools modify the global system as part of their default behaviour.  Ruby gems, for example, install system wide by default.  So whilst two applications may require two different versions of a gem (bundler or rake for example), if installed by gems at a system level then they will fight.

Fortunately Unix, as a multi-user system, has been built to provide tooling to fix these problems.  If your tool honours these principles then by using ```PATH``` and other environment variables you are able to decide where the tools should make their changes.  For example ```GEM_HOME``` instructs the ruby environment where to download and find gems.  This means it can be pointed to a directory local to the project root.

This also works as a work around for non-packaged software.  If you wish to use the latest version of leiningen you can download it and install it in the tools directory local to your project root.  This allows different projects to use different versions of leiningen without affecting each other.

### Sandboxing
Sometimes it's not possible to keep changes localised.  For example whilst some database servers would allow you to start up an arbitrary server on an arbitrary port pointing at an arbitrary file many do not and only run at a system wide level. In these cases you need to find a way to sandbox.

In the database example this is simple: each application creates a unique username, password and schema (with configuration values of each kept out of the code) specifically for their use and never the twain will meet.  However this is not always possible.

For some applications that aren't so amenable to sharing then the entire app will need sandboxing.  Tools such as LXC can achieve this by running the app in a lightweight virtual container.

## We need to talk about the build
All this needs to work on your build server too.

### Treat dev and build as the same
Build agents should use the same techniques as above.  Whilst build agents may require a different implementation of the [General tools] layer (they don't need emacs but will need the agent installed) the agent should invoke the same script used to setup the [Application dependencies] layer.  This has a number of nice side effects:

* build agents can be shared (in the same manner code is isolated and runs happily alongside other projects on your dev box)
* build agents are cheap to replace and disposable (they require very little setup)
* build agents are self service (if you need markdown add it to the script and the build server has it)
* your [Application dependencies] scripts are continuously integrated and thus get all the benefits of CI

### Security
Now, the problem is letting people install what they want on a dev box and letting people install what they want on a build agent are two different things.  This means that thinking about security is very important.  The scripts for [Application dependencies] may do some wide ranging things: install new packages, install new users etc.  It is important that the build agent is designed in a way that limits damage only to the agent itself and cannot compromise the wider network.  This way, if something does go horribly wrong you know the damage is limit to an agent you can throw away and build again.

# Team discipline
The tools available today certainly lower the barrier to entry and reduce the cost of maintenance of dev environment automation.   However some things will still be tricky, especially around automation and the first time a problem is hit it can be all too tempting to do the easy (note easy, not simple) thing.  Skipping automation steps or not going that extra bit to ensure something is isolated degrade and devalues the whole.

If the team isn't behind the process, and doesn't feel convinced or empowered or able, then the whole thing falls apart and very quickly things can drift and the team are back to prodding snow flakes and the process just gets in the way.  Humans have a tendency to abandon the little bit of order in chaos, feeling it gets in the way. It's easier to reason about a complete unknown than an bit of unknown mixed with the uncertainty of what some third variable may be doing.

# _Almost_ perfect
There are still holes.  The requirement for team discipline, a decent level of skill and understanding of the OS.  And there are some gaps: order bugs (if codebases share dependencies one may make incorrect assumptions if the other already installed the dependency meaning if fails on a clean box), isolation isn't always 100%, and sometimes dependencies just don't play nice (e.g. Oracle are very anti-social when it comes to automating downloads of drivers etc.).  And some things are a real pain to automate and require that extra mile of effort (auto checking out different git projects with different credentials kept us busy for a while, as did isolating ruby versions).

Fortunately I believe that the method is quite robust when things do go wrong.  Forgetting to automate a step isn't the end of the world, it can be added in retrospectively without too much effort and the fact that developers and build servers share and execute the same scripts regularly means the holes become quickly apparent.  And there are always ways to get that Oracle driver automagically if you use the write tools and put in the effort.  The fact that things are easy and quick to setup means boxes can be blown away and cheaply replaced and this works as a good strategy to kick out the inconsistencies and bugs, work around difficult migrations and give a get out when things just go horribly wrong.

# Result
Judging the method on its results it's been a long time since the team have had to worry about configuring a dev box or a build box when a new team member comes on board or a build agent dies.  Economically we have a smaller pool of agents whilst simultaneously increasing the number of available agents for each build job (as any job can safely use any agent).  If a dev box dies, or gets in a bad place, we don't panic or worry.  We blow it away and start again which allows us to take risks.  Given that any code changes I've made on the box are regularly pushed we know we won't have lost much if things do die beyond recovery.  We safely run all our projects side by side on the same boxes without worrying about pollution or side effects from other projects. We never need clever trickery like rvm or other such complicated nonsense.  And because things are automated we actually know what's going on (like exactly where git keeps your configuration).  Change, for the most part, is incredibly easy, simple and cheap.  All our dev boxes are consistent and we don't worry about one team member not having access to a tool that the other does and we don't get those weird "oh I'm on the wrong version of x" bugs.  

Ultimately we are free of an awful lot of problems that other teams have when it comes to their dev and build environments.  So even if it isn't _quite_ perfect it's certainly more than good enough.

[envars]: 

