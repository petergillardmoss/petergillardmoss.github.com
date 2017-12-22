---
layout: post
title: "Understanding OAuth 2.0 and OpenID Connect"
date: 2017-12-22 09:20
comments: true
categories: 
published: true
---



I've spent a good amount of time trying to get to grips with OAuth 2.0 and OpenID Connect (OIDC).   First you must get over the confusion that OAuth 2.0 isn't the same, or backwards compatible with OAuth, and that OIDC isn't the same, or compatible, with OpenID.  Then you realise the unpicking doesn't end there.  This is because the two terms are often used interchangeably when they are two quite distinct concerns.  It's just that OIDC builds on top of OAuth.  This makes understanding where they separate, and where they join, difficult.

In my research I found that articles were either very much focused on the use case from the perspective of the client application, focused on working with 3rd parties (Google, Facebook) or very detailed specifications for providers.  What I couldn't find was a high level understanding of the two, how they worked together, or how a typical enterprise would go about architecting for them.

My goal for this document is to provide just that: enough of a high level understanding so people can think about how OAuth 2.0 and OIDC could work in a typical enterprise context.

# Oauth 2.0

Lets start with OAuth 2.0.  In as few words as possible OAuth only covers authorization (authz), not authentication (authn).  Well, strictly speaking OAuth is not about authz in the traditional sense, it is more a mechanism for provide _delegation_ via _consent._

OAuth deals with mainly three things: **flows**, **scopes** and **tokens** (aka bearer tokens).   OAuth divides differing responsibilities between four roles: **Resource Owner** (the user), **Client** (the app making calls), **Resource Server** (the API) and **Authorization Server** (the source that grants the token).  Often the _Resource Server_ and the _Authorization Server_ are the same (e.g. Facebook or Google).

## Token

The _token_ is the thing which represents proof of _consent_ and what is ultimately used to validate access.  Essentially the keys.  There are two types of _token_ an **Access Token** and a **Refresh** **Token** (which is optional).  The _Access Token_ is time limited and will expire and is what is used to validate access with.  The optional _Refresh Token_ is indefinite but can only be used to acquire new _Access Tokens_ from the _Authorization Server_.

The _Authorization Server_ is responsible for the management and issuing of _tokens_ to the _client._ The _token_ is opaque to the client.  The _token_ is simply sent to the _Resource Server_ as part of the request and the _Resource Server_ is responsible for validating the token and granting/denying access to the requested resource.

OAuth says nothing about the format of the _Access Token._ Therefore there needs to be some agreement between the _Authorization Server_ and the _Resource Server_ on how to validate the _Access Token_ and its permissions.

## Flow

Essentially a _flow_ is the method you use to get you obtain proof of consent via co-ordination of the four roles.  The _flow_ changes depending on your use case (for example single page app vs Smart TV vs mobile app).

As a user you're probably familiar with some aspects of some _flows_: when you click 'Connect with Facebook/Google/Yahoo', a pop-up appears, you login to the site (e.g. Facebook), click "Authorize", get redirected etc. etc.

The main flows are divided into either **three-legged** (between _Resource Owner_, _Client, Authorization Server)_ or **two-legged** (between client and sever):

*   Authorization Code flow (three legged): for apps that can keep a secret: client/server web apps, mobile apps etc.
*   Implicit flow (three legged): where a secret can't be kept safe e.g. Single Page Apps
*   Client Credentials flow (two legged): exchanges the client id and client secret for the _tokens_
*   Resource Owner Password flow (two legged): exchanges the _Resource Owner's_ _username and password_ for the _tokens_

And there are more flows being added, such as the [Device Flow](http://alexbilbie.com/2016/04/oauth-2-device-flow-grant) for things like Smart TVs etc. which have no easy input device.

[![abstract_flow.png](https://lh6.googleusercontent.com/proxy/_g_DZGVd-c65yrMwvAJdPZtfqdjMaSgmwf4NduvPO7r-f4jH30rL8Ehw0-t1nhxvLNMIUrLkkoP3tBSPmv_8cAfA63q19uEf5Fvwer4mozluRO4=w5000-h5000)](https://assets.digitalocean.com/articles/oauth/abstract_flow.png)

## Scopes

The _scopes_ represent the permissions needed to access resources (e.g. my email) from the _Resource Server_.   The _Resource Owner_ provides _consent_ to the _Authorization Server_ to delegate _scopes_ to the _Client_.  The user sees this as part of the flow when the _Authorization Server_ lists the _scopes_ the _Client_ is requesting access to.[![twitter-authorize.png](https://lh6.googleusercontent.com/proxy/O4nmCUurgId5lQdjj9Gys0FpZeTh3TKRjAe_HwfzfdE3a_G5RpTDV81io8UBxbHPKNKX5nZstZFk8vxGeScN-mp3Ky2FqXhFxLz8GumByyuKOlj6dzk5rsa__AG52sEJK-NwtPAAg-l8BJ4ImJyYrwWHiRJ5lN25j2vgXSUueurDKdgzbV5TyrpS46iCyA=w5000-h5000)](http://docs.spring.io/autorepo/docs/spring-social/1.1.4.RELEASE/reference/htmlsingle/resources/images/twitter-authorize.png)

And that is a simple and quick overview of OAuth.  Now onto OIDC:

# Open ID Connect

OIDC is a standard to provide authentication to an application (the **Relying Party**) in the same way as SAML or WS-Federation. OIDC brings web scale to identity protocols by leveraging OAuth.  It does this is a cunning way: by acting as a specialised _Resource Server_ for user info (by providing a <span style="font-family:'andale mono',times">UserInfo</span> endpoint) combined with a specialist _Authorization Server_ which requires authentication.   This specialist server is known as an **OpenID Provider** (**OP**).

OIDC introduces a few other concepts:

*   Extends the existing flows: _Authorization Code_ and _Implicit_
*   Introduces a new three-legged flow: _Hybrid_ which is a combination of the two.  Hybrid is typically for SPAs with a web server back end.  It allows the front end to use _Implicit_ flow and the back end to use _Authorization Code_ in co-ordination.
*   New type of token called an **ID Token** (which represents the UserInfo).
*   New roles: The _OpenID Provider_ which uses an **Identity Provider (IdP)** to authenticate the _Resource Owner_.  The _Relying Party,_ which is the app (or _client)_ which requires the end user to be authenticated_._
*   New _scopes_ (or **claims**)particular to UserInfo (<span style="font-family:'andale mono',times;font-size:10pt">openid, email, phone, profile, address</span>).  In fact Open ID is invoked using these _scopes._

## OIDC Scopes

The OIDC _scopes_ deserve a special mention.  Essentially the client is requesting permission to specific _scopes_ relevant to the users identity (<span style="font-family:'andale mono',times;font-size:10pt">email, phone, profile, address)</span>.  The presence of _scopes_ instruct the _Authorization Server/OP_ that the _client_ is requesting authentication.  If this _scope_ was missing then the authentication flow would not happen.

The <span style="font-family:'andale mono',times;font-size:13.3333px">openid</span> _scope_ is also special as its presence instructs the _OP_ to return the _ID Token._

## ID Tokens

If the _client/Relying Party_ requests authorization with the <span style="font-family:'andale mono',times">openid</span> scope then the _OP's_ response will contain an _ID Token_ alongside the _Access Token_. _ID Tokens_ contain metadata (the _claims)_ about the user's identity in a JSON Web Token (JWT).  The _ID Token_ is returned along with the _access token_ by the _OP_ which authorizes access to the _UserInfo_ endpoint.

The same _claims_ in the _ID Token_ are available from the _UserInfo_ endpoint (the _ID Token_ is essentially a representation of the _UserInfo_).

In this way the _ID Token_ acts as proof of authentication.  The _OpenID Provider_ is responsible for the management and issuing of _ID Tokens_ to the _Relying Party_.  The _Relying Party_ is responsible for validating the _ID Token_ and granting/denying access to itself.

## SAML Replacement

As already mentioned OIDC is incredibly similar to SAML (bar a few low level details such as the role of cookies vs tokens) and is set to replace it.  In fact a SAML app could easily be switched out to use OIDC without a user really noticing anything (or the dev team if you use something like Shibboleth).

Apart from the XML vs JSON argument because OIDC builds on top of OAuth it is far more flexible and scalable.  Specifically with the ability to introduce new flows as new technologies come into play (which is something SAML suffered from), or enable dynamic registration (e.g. social login providers) and Bring Your Own Identity (BYOI).  It is also advantageous as it simplifies the landscape by leveraging OAuth 2.0.

# Open ID Connect vs OAuth 2.0

It is a common mistake to assume that OIDC is simply OAuth 2.0 with authentication added on.  In fact OIDC is a means of providing authn by leveraging OAuth.  OIDC is nothing but a spec for a specific type of OAuth _Resource Server_; it isn't necessarily used for general OAuth authentication (say to APIs).

To understand this we need to run back through some basic concepts:

*   OAuth uses _Access Tokens_ as proof of _consent_
*   OIDC uses _ID Tokens_ as proof of identity
*   OAuth uses _scopes_ to represent permissions
*   The OAuth _Access Token_ is restricted to the _scopes_ granted by the _Authorization Server_
*   The OIDC <span style="font-family:'andale mono',times">UserInfo</span>end point requires a valid _Access Token_ with _consent_ to one or more OIDC _scopes_

To put the above in context: in a vanilla _OpenID Provider_ the _Access Token_ will only grant access to the _UserInfo_ endpoint (as that is all that the OIDC _scopes_ grant).For API operations OAuth must validate against an _Access Token_ which has _consent_ to the _scopes_ required to access resources provided by the _Resource Server._ But this is **not** what an _OP_ provides.

# Combining Open ID Connect and OAuth 2.0

So how do you move from OIDC authn to OAuth authz?  This is where things get pretty murky.  Like many things around OAuth and OIDC the specs are rather open to interpretation.  This means there are many different patterns and practices to solve the same problems.Here are some of the various practices:

## Authorization Server + OpenID Provider

Essentially the vanilla OAuth _Authorization Server_ for APIs is extended to meet the OIDC requirements as well.  Essentially by supporting the openid _scope_.This is the most common method, and the one [Google uses](https://developers.google.com/identity/protocols/OpenIDConnect).  As an example, if you had a _client_ which you wanted to ensure authn plus gain authz for access to Google Drive you simply request the <span style="font-family:'andale mono',times;font-size:8pt"><span>scope=openid+</span>[https://www.<wbr>googleapis.com/auth/drive](https://www.googleapis.com/auth/drive)</span> from the OAuth <span style="font-family:'andale mono',times;font-size:10pt">authorize</span> endpoint.  <span>The _Access Token_ returned from the selected _flow_ would then grant you access to the resources protected by the Drive _Resource Server's_ API and by the _OP_'s _UserInfo_ resource.</span>

The challenges with this method is that the _Authorization Server_ requires knowledge of all the legitimate scopes.  Given that one of the fundamentals of OAuth/OIDC is to decentralise authn/authz this becomes a challenge to maintain.

This also assumes that your _OP_ and _Authentication Server_ are both within your control.  As one of the benefits of OIDC is to Bring Your Own Identity (BYOI) the _OP_ is likely provided by some other party which isn't open to extending authorization to resources owned by your _Resource Servers._

## ID Token as Access Token

Because the _ID Token_ encapsulates all necessary data to process an authentication it is tempting to assume that [the _ID Token_ could be used as an _Access Token_](http://nordicapis.com/how-to-control-user-identity-within-microservices/).

There are a number of problems with this approach:

1.  The _ID Token_ represents authentication only, not authorization (thus undermining OAuth)
2.  The _ID Token_ would have complete access: this breaks the principle of least privillage
3.  _ID Token's_ are long term tokens where as _Access Tokens_ are meant to be very short term
4.  It overloads the semantics of the two tokens and mixes concerns that OAuth rightly separates

## Token Exchange

As recently as December 2015 the OAuth Working Group released their standards for [OAuth 2.0 Token Exchange](https://tools.ietf.org/html/draft-ietf-oauth-token-exchange-03).

In this scenario your _Authorization Server_ provides Token Exchange.  This would allow a _client_ to exchange the _ID Token_ for an _Access Token_ with the requested _scopes_.  The _Authorization Server_ simply needs to trust and verify the _ID Token_ from the 3rd party _OP._

There may be other techniques out there too.  If so I'd be happy to hear them and get some critique and experience on how that went.  But one thing's for sure: OIDC and OAuth aren't silver bullets and their implementation in the enterprise requires some very careful consideration.

# Resources

[http://connect2id.com/learn/<wbr>openid-connect](http://connect2id.com/learn/openid-connect)

[https://www.digitalocean.com/<wbr>community/tutorials/an-<wbr>introduction-to-oauth-2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)

[http://nordicapis.com/api-<wbr>security-oauth-openid-connect-<wbr>depth/](http://nordicapis.com/api-security-oauth-openid-connect-depth/)

[Okta: How to secure your applications using OpenID](https://my.thoughtworks.com/groups/techops-community/blog/2016/04/20/okta-how-to-secure-your-applications-using-openid)

[OAuth 2.0 - Okta Developer](http://developer.okta.com/docs/api/resources/oauth2.html)

[OpenID Connect - Okta Developer](http://developer.okta.com/docs/api/resources/oidc.html)

[End User Authentication with OAuth 2.0 — OAuth](http://oauth.net/articles/authentication/)


