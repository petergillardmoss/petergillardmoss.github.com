---
layout: post
title: "Authentication out of App"
date: 2015-10-23 08:26
comments: true
categories: 
---

The majority of modern web applications require some sort of authentication mechanism.  Whether that's an internal reporting site, a build server, an online store, a blogging engine or even an API.  Users need to login to either gain access the entire system or to specific parts, or they need to send credentials when making API calls.  

Typically authentication is integrated into the app or service by installing a 3rd party component and using the web framework's inbuilt mechanism for allowing or deny specific routes or resources.  For example, in Ruby on Rails you would use ```before_action``` which delegates to a custom written method.

This is a less than ideal practice, for a number or reasons, from engineering to security. I advocate keeping authentication out of the application altogether by pushing it to a higher layer (typically a reverse proxy).

# Authentication vs Authorization vs Identity and user flow

## vs Authorization
Authentication and authorization are often conflated, yet they are orthogonal.   Where authentication is about providing some level of confidence that the person, or thing, accessing the system is who they say they are, authorization is concerned with enforcing domain rules around behaviours attributed to individuals or groups of users.  You can have a system with neither, either or both. For example, a web site grants access to blocks content unless it has verified you are a registered user and all authenticated users have the same level of functionality (authentication only); alternatively a different site asks 'are you a member?' and if the user responds positively it allows them access to different content (authorization only); or more typically a user is an authenticated user and the site authorizes different behaviours (admin vs readonly) such as updating content (authentication and authorization).

## vs Identity
Identity is also commonly conflated with authentication.  Especially as the purpose of authentication is to validate an identity.  Even more confusingly the information by which you validate an identity (typically username and password) is often conflated with the entity being identified (name, address etc.).

They are in fact, two separate things.  The entity which that identity refers to is not a concern of authentication but of something else (depending on the domain it could be a customer service, or even LDAP).  Likewise the application itself is concerned with resolving the identity not how to validate it.

Identity has other rules around users which may affect their interactions with the system.  For example, if they have logged on for the first time, or if they have changed status (perhaps become an admin) and need to add more information.  Or if they access a specific part of the site for the first time they may have to accept some Terms and Conditions etc.  These rules, around what a user can and cannot do, and other behaviours, are part of the application domain.

Likewise, authentication, has different rules around validation (see Trust).  For example, it may initially require a _username_ and _password_ but, then relies on a cookie or token to ensure validity.  It also may not require the username and password at all, API keys or even authorisation from another system (e.g. OAuth, SSO etc.).

## vs Trust

Trust is a much overlooked aspect of authentication.  Trust is a variable matter and is usually derived from metadata around the authentication request itself and it is always authentication which determines trust.  Trust can influence the behaviour around both authentication and authorization.

Commonly this is around the behaviour of authentication; more or less information can be demanded (e.g. multi-factor) depending on the application itself or the circumstances in which the request was made (untrusted network, untrusted device, new user etc.).  

The trust score can affect authorization too, for example by changing what access is given to what data based on factors beyond a binary result of authentication.  If the authentication results in a low trust score the application could decide to provide a lower level of access to the same user than normal.

# Separate concerns

Authentication is a very distinct capability of the system.  It is also a fairly complex one, yet it has a very well defined boundary.  Engineering principles encourage that we treat authentication as distinct and encapsulate it, thus enforcing separation of concerns.  Good engineering practice also encourages appropriate layering, again to help enforce separation of concerns but also to simplify.

Thanks to these characteristics authentication can easily be pushed up to a higher layer.  Typically this layer is within the application framework itself (e.g. Rails callbacks) however most frameworks make it difficult to enforce isolation and functional bleed is not uncommon.  This leads to ambiguity (especially with authorization) which, in turn, leads to the authentication surface area increasing, making it more difficult to isolate.  These factors create a higher probability of error (i.e. bugs, exploits), which are potentially costly. Therefore it is preferable to remove it as an application concern altogether.

# Into the reverse proxy

Removing authentication from the application framework completely and into a higher layer realises separation of concerns and enforces it.

A reverse proxy is a good candidate for this behaviour.  Most reverse proxy and HTTP servers already offer a plethora of [authentication modules][authmodules] (from basic auth to LDAP integration to SAML integration etc.) and for some (e.g. nginx) it isn't hard to role your own.  The reverse proxy simply blocks any unauthenticated request from reaching the application.  Any behaviour related to an unauthenticated request (redirects, blocking etc.) are well within the capabilities of the reverse proxy.

As HTTP servers and reverse proxies tend to employ a declarative approach to configuration other subtleties of authentication are also surfaced in a far clearer manner.  For example, protecting specific routes whilst leaving others open (css etc.).

The application itself has to be configured in such a way that it is either only accessible via the proxy (such as being bound to localhost or by whitelisted IP address via iptables rules) but again, these concerns are external to the application itself.

## Contract with the Application

For the application to fulfil its function it will require the identity key (e.g. username or email) which it can then use internally to resolve to the entity itself (e.g. user or customer) plus any meta-data related to the authorization (e.g. trust levels, groups etc.).  Because the application implicitly trusts the parent layer it can safely assume that the identity passed is valid at all times.  If it was not valid, it would never have received the request.

There are a number of positive side-effects to this.  The application is now simpler: a whole concern has been removed.  Functional bleed in the application becomes impossible.  As authentication is a cross-cutting concern its influence on application behaviour can be quite wide.  This means other areas, such as testing, have also removed a layer of complexity.  As a whole, both authentication, and the remaining application behaviour, become more robust and predictable.

# Security

Authentication is a common target for exploit for obvious reasons and so security is critical.  The simple step of removing authentication out of the application and into the reverse proxy has potential to reduce vulnerability.

Security through layering is a good practice.  The reverse proxy is one of the first lines of defence in a system.  As a result they are well tested and proven against large numbers of security exploits and often include plugins and modules to protect your system from attack.  This is one of the reasons it is recommended to place an application in front of a reverse proxy.

A rule of security is that it is only as strong as its weakest link.  When authentication is in the whole application then security becomes as strong as the weakest part of the app.  This includes all of the application's dependencies and when modern application development often involves the use of large numbers of third-party dependencies that is a significantly large surface area.

Application dependencies are also highly volatile.  This makes is very difficult to ensure that a new library, or an upgrade to an existing one, doesn't introduce a weakness which exposes authentication.  I witnessed a real world example of this where an application's SAML library relied on an XML library which was upgraded by a separate component in the application.  The XML library had a bug which resulted in incorrect behaviour in the SAML parser.

This situation is made worse in organisations with more than one application or service.  If each application has self-rolled authentication then, regardless of how strong all the other authentication implementations are, the weakest link becomes that app.  The result is that the whole organisation becomes exposed due to one single poor implementation.

Conversely, the modules used in reverse proxies are far more security hardened.  Even in the case of a bespoke authentication system (which is a risk in itself) the lifecycle of the authentication service can be separated from the application's and thus the risk of library upgrades or bugs in the application are not affecting the authentication service.  

Authentication in the reverse proxy allows an organisation to test and harden one point and can have a more conservative attitude to change within authentication itself whilst allowing a more liberal attitude to the protected applications.

# Multiple authentication mechanisms

It is increasingly rare for a system to have only one authentication mechanism.  Web browsers authenticate differently to mobile apps, third parties authenticate to APIs in a different manner to native apps, apps that make requests on behalf of users (e.g. OAuth) authenticate differently to applications that are run as server processes (such as cron jobs, ETLs, other applications etc.).   Also it is becoming common for sites to offer multiple providers (Google+, Facebook etc.) to authenticate against.

Reverse proxies allow different mechanisms to be declaratively defined and mixed and matched based on clear rules.  Different auth modules can be invoked based on specific request headers, paths, client IPs etc. 

Multiple authentication mechanisms makes for a complex implementation.  Luckily a reverse proxy configuration can easily be tested without the need for the real application running behind it.  Best of all this complexity is kept out of the app.

For packaged software this is also a real enabler.  Products are often under pressure to meet the demands of a wide range of different authentication mechanisms out there in the market.  Having integrated authentication is a deal breaker for many enterprises.  Rather than having to provide and support an implementation for every single possible provider the product only has to support integration with a proxy.  This means covering a significant part of the market with considerably less effort.

# SSO systems vs custom provider

When it comes to SSO integrations for reverse proxies are a well established pattern.  Many SSO providers already have robust, well-proven implementations for Apache and nginx.  [Shibboleth][shibboleth] is a great example.  It uses a fastcgi process allowing the reverse proxy to hand of authentication requests.  As a general rule these implementations are wider used, often provided as system packages in the standard distribution repos, more vigorously tested and have communities that have a higher level of specialism in authentication.  This makes security exploits and bugs less likely and an higher guarantee of response.

For API authentication there the majority of providers either integrate directly with reverse proxies or provide their own.  Personally I prefer those that integrate with reverse proxies.  This is for a number reasons: it simplifies the layers - a general reverse proxy, such as Apache or nginx, is often standard and adding another increases the number of layers thus increasing complexity; it gives one place to see all security related config (the reverse proxy configuration file) also, as previously mentioned, reverse proxies have a high amount of scrutiny and history with respect to security, and other key functionality (performance etc.).  Thus any custom proxy for API traffic would need to be behind a general proxy regardless.

When websites have their own authentication mechanism (for example a basic user authenticated against a database looked), usually highly stylised and customized to the site, then a separate authentication application is still hugely beneficial for all of the above reasons.  Better still, use an established commodity product which has been tested and proven and hardened rather than a potentially weak and vulnerable self-rolled one.

# Authentication as a commodity

Commoditisation of common patterns is a real productivity booster.  Teams rewrite the auth wheel over and over again.  Even if they are using plugins or libraries there is still a good deal of effort in getting the authentication working.

Pushing authentication out of the application layer increases commodity.  There are fewer implementations of reverse proxy than there are languages and frameworks.  

Due to the cross-cutting nature of authentication an organisation can produce a single reverse proxy implementation which covers their entire family of applications with very low effort.  Any modifications (adding more providers etc.) come at a low cost.

Commodity in the wider world, of open-source etc. makes the industry as a whole more productive.  Rather than expending effort of writing yet another authentication implementation for your language, site or product by establishing a standard and following a common, easy to implement pattern and keeping authentication out of the application the industry reaches a high level of reuse and productivity.

It also ensures that applications follow a similar consistent pattern.  This reduces maintenance and troubleshooting.  If all applications follow the same pattern of behaviour it becomes far cheaper to roll out and adapt authentication for the organisation or product.

[authmodules]: https://httpd.apache.org/docs/2.2/howto/auth.html
[shibboleth]: https://shibboleth.net/
