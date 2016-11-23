---
layout: post
title: "Safety First with AWS Roles and STS"
date: 2015-11-13 09:50
comments: true
categories: 
---

AWS credentials are an extremely precious and powerful asset.  In the wrong hands they can cause serious damage either by disrupting services or, more commonly, by acquiring free compute power, [usually to mine bitcoins](https://google.com/?q=leaked+aws+credentials), at your expense - bills with five figure sums over a matter of days are not unheard off.  It's a serious and very real risk that can jeopardise the financial viability of a product or team.

Development teams need AWS credentials, often powerful ones, to do their jobs: to create instances for debugging, to run tests and applications  locally as part of the development cycle etc. Keeping the AWS credentials used to do development safe, by following basic security hygiene, such as ensuring that you keep them out of source control, is one course of action that every development team should be taking.  But even then mistakes can be made or credentials can be leaked, or become at risk, in other ways.  So it is important to ensure that, where credentials are needed for development, they are limited in the scope of damage they can do.

# AWS Security Token Service

AWS STS enables the request of temporary, limited-privilege credentials.  By leveraging AWS STS and temporary credentials teams can greatly reduce, not only the impact, but also the steps to recovery (as credentials are automatically rotated and revoked), in the eventuality that credentials are leaked.

AWS originally provided temporary credentials for [Instance Roles][instanceroles].  This technique enables EC2 instances to run without the overhead and inherent risks of managing users and passing credentials.   For any service running within AWS infrastructure the use of Instance Roles, on their own, removes a large part of the surface area.

Developers still require credentials when they work outside of AWS's estate and these credentials are often the most powerful and therefore dangerous.  Fortunately, the services behind _Instance Roles_ are available for all AWS users via the [AWS Security Token Service](https://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html).

## Principle of least privilege
Using AWS STS for all users, regardless of where they operate is a powerful security measure.  Roles can be defined which users assume based on need.  By only granting the permissions needed to carry out those roles, the scope of potential damage is reduced.

This also enables parity regardless of the source.  This is both important and powerful: an IAM user, or an EC2 instance, or a user authenticated by a corporate identity provider, or even a mobile app, can all assume the same role and operate under the exact same permissions.  

For developers this means they are able to run applications and execute tasks in the development cycle with only the intended permissions. 
This removes the need for developers to have system wide privileges.  This has the additional benefit of improving the development lifecycle by simplifying it (e.g. by removing common permission bugs etc. during deployment).  If a developer needs to deploy a server for debugging they can assume the same roles the build server would use for deployment.  If they need to run a web server locally with permissions to S3 then they can assume the role that has been defined for running that application in production like environments.

# Temporary credentials for developers
AWS STS will issue [temporary credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html) which last a maximum of 3600 seconds (1 hour), although they can be requested for even less.  Because the credentials are generated 'out-of-band' and are disposable, they operate in a manner which decreases the likelihood that they are checked into source code etc. (as they tend not to be added into config files).  Unfortunately, how to obtain credentials is not so obvious or provided easily by existing tools.

There are two ways to obtain temporary credentials from AWS STS.  The first is by providing a token from an [Identity Federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) and the second is via an authenticated IAM user.  
From there AWS STS generates credentials following a request to _assume a Role_.  This is exactly the same technique used by _Instance Roles_.  
This separation between authentication of a user, and the credentials used against AWS offer another layer in [Defence in Depth][defdepth].

If you use an identity provider (IdP) you can bootstrap into a role by providing a SAML assertion or with a Web Identity (such as Amazon Cognito or OpenID Connect).  Unless you have tight control over the IdP I wouldn't recommend using Web Identity as you essentially open up the ability to assume your role to the entire IdP (e.g. every user with a Google account).  

If you prefer to use AWS for your account management you can bootstrap from an authenticated IAM user from the same, or even from a different account.  Although this means that the user will still require AWS credentials they are only ever used for acquiring temporary credentials and have no value when running code.

To bootstrap and generate credentials I have created the following CLI tool: [aws_role_credentials](https://github.com/ThoughtWorksInc/aws_role_credentials).  This allows developers to easily generate temporary credentials from the command line to be used by other applications.  The credentials are saved in a _named profile_ in the standard [AWS profile configuration file](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-config-files) (e.g. ```~/.aws/credentials```) which is supported by all AWS SDKs transparently via the _default credentials provider chain_ without the need for any code changes.  From there any process can pick up those credentials and use them.

## Using a SAML provider

This is the recommended way of operating as the vast majority of organisations will already have a form of Identity Provider such as [Active Directory](http://blogs.aws.amazon.com/security/post/Tx71TWXXJ3UI14/Enabling-Federation-to-AWS-using-Windows-Active-Directory-ADFS-and-SAML-2-0) or LDAP.  If that IdP supports SAML, or can integrate with a SAML IdP such as [Shibboleth](http://blogs.aws.amazon.com/security/post/TxRTTT5PLUE6B5/How-to-use-Shibboleth-for-single-sign-on-to-the-AWS-Management-Console) they can be integrated with AWS.  This has many advantages to keeping your organisation secure, including the simple fact that if someone leaves your main corporate IdP then they no longer have access to AWS.  This is more true if there are multiple AWS accounts as they can all be managed by the same IdP.  It also enables your IdP to be the source of authentication for the acquisition of temporary keys (which, incidentally, is all that happens behind the scenes when you use the IdP to access the AWS console).

First you will need to [setup an IAM Identity Provider for SAML](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_saml.html) and [a Role for it to assume](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_saml.html), or modify an existing role to add a [_Trust Relationship_](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_manage_modify.html) with the SAML Identity Provider (the SAML assertion will need to pass the role).  

The achieve this the Role needs a statement similar to the following:


	"Statement": [
		{
  			"Effect": "Allow",
  			"Principal": {
    			"Federated": "arn:aws:iam::1111111111:saml-provider/AcmeSaml"
  			},
  			"Action": "sts:AssumeRoleWithSAML",
  			"Condition": {
    			"StringEquals": {
      				"SAML:aud": "https://signin.aws.amazon.com/saml"
    			}
  			}
		}
	]

Then it is a simple case of authenticating with the IdP to obtain a SAML assertion and passing it to ```aws_role_credentials``` via ```stdin```.  In the following example our developer, Jo Bloggs, will use a tool which authenticates them against [Okta](www.okta.com) called [okta_auth](https://github.com/ThoughtWorksInc/oktaauth) to obtain the necessary SAML assertion - although _aws_role_credentials_ has been written to plug into any other SAML IdP:

	$ oktaauth -u jobloggs | aws_role_credentials saml --profile dev

This will assume the role provided in the SAML assertion and generate credentials in the named ```dev``` profile in the AWS profile configuration file ```~/.aws/credentials```.

To test whether the credentials were successful simply use the [awscli](https://aws.amazon.com/cli/):

	$ aws s3 ls --profile dev

Any application which uses an AWS SDK or similar (such as boto) will also read these credentials from the AWS profile configuration file without any code changes as part of the _default credentials provider chain_.  To tell the _profile credentials provider_ to use the named profile simply set the ```AWS_PROFILE``` environment variable.

	export AWS_PROFILE=dev

## Using an IAM user

For those scenarios where an IdP is not available, or the user cannot be added to the IdP, then a normal IAM User can be used to bootstrap.  The IAM user can exist in the same account or in another account owned by the same organisation.

To allow an IAM user to assume a role you first need to create one and add the trust relationship to the role in a similar way to the SAML example.  As an aside single roles can have multiple trust relationships.

For this example we'll assume that our master account id is _111111111_ and the role is called _Developer_:

	"Statement": [
  		{
    		"Effect": "Allow",
    		"Principal": {
      		"AWS": "arn:aws:iam::111111111:root"
    		},
    		"Action": "sts:AssumeRole"
  		}
	]

Then the developer's IAM user is given permissions to assume the role.  The developer should have **no other permissions**.

	"Statement": [
    	{
        	"Effect": "Allow",
        	"Action": [
            	"sts:AssumeRole"
       		],
        	"Resource": ["arn:aws:iam::111111111:role/Developer"]
    	}
	]

Our developer (jobloggs) can then use ```aws_role_credentials``` to assume the role and obtain temporary credentials.  Jo will need to provide their usual AWS credentials to authenticate against AWS STS (by using the default profile or environment variables). Note that these credentials only have permissions to assume the role.  

	$ AWS_ACCESS_KEY_ID=feaedafda12312cfd
	$ AWS_SECRET_ACCESS_KEY=secretaccesskey

In this scenario ```aws_role_credentials``` needs to be provided with two arguments: the full arn of the role, and a name for their session (AWS use this session name for logging and auditing):


	$ aws_role_credentials user arn:aws:iam::111111111:role/Developer jobloggs-session --profile dev

The outcome is the same as the SAML example: the tool assumes the role provided and generates credentials in the named ```dev``` profile in the AWS profile configuration file ```~/.aws/credentials```.

Again to test whether the credentials were successful simply use the [awscli](https://aws.amazon.com/cli/):

	$ aws s3 ls --profile dev

### IAM with Multi Factor Authentication

The role can be further protected by enforcing [MFA](https://aws.amazon.com/iam/details/mfa/).  To do this, simply update the statement to add the condition:

	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
  				"AWS": "arn:aws:iam::111111111:root"
			},
			"Action": "sts:AssumeRole",
			"Condition": {
		     	"Bool": {
			    	"aws:MultiFactorAuthPresent": "true"
				}	
			 }
		}
	]

This now requires that the developer calls ```aws_role_credentials``` and passes in the MFA serial number and the generated token.  The MFA serial number can be obtained by running ```aws iam list-virtual-mfa-devices```.  The token will come from the mfa device.

Here's an example of the full call:
	 $ aws_role_credentials user arn:aws:iam::111111:role/dev jobloggs-session --profile dev \ 
	   --mfa-serial-number arn:aws:iam::111111:mfa/Jo \ 
	   --mfa-token 102345


## Using a custom provider
You can also [use a custom provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_enable-console-custom-url.html).  This would simply require the creation of a service/web app to authenticates the user against the provider and once established invoke the [STS AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) and pass the temporary credentials to the client.  From an implementation perspective it is the same as the IAM user except that the _AssumeRole_ is called on the developer's behalf.

This has the advantages of the SAML method but for situations where a SAML provider is not available for your IdP.

#  Further recommendations

AWS STS enables a policy where all developers and service accounts can be maintained in one place with restricted access to AWS via lower risk limited-time, limited-privilege credentials.  To achieve this the following additional guidelines can be followed:

## Service accounts

### Inside AWS

Never use an IAM user for services that run inside AWS.  Always use Instance Roles.

### Outside AWS

For service accounts which exist outside of the AWS estate (such as build servers or other services) then AWS STS should be used to provide the service with temporary credentials.  These could either be injected (where the operation is already time limited) or requested from a _Custom Provider_ that is able to authorise and establish the role on their behalf (in exact replication of _Instance Roles_).

## IdP Recommendations

Where an IdP is available there should be no IAM users at all (although there may be one or two edge cases such as the IdP itself requiring access to AWS).  The IdP can be relied on to authenticate both developer and service accounts and thus allowing them to assume the necessary roles. 

## IAM Users

In some instances an IdP may not be available and IAM users may still need to be used.  In those instances IAM users should only have privileges to _AssumeRole_ and absolutely no other permission.

### Separate account for IAM users

Most organisations operate multiple AWS accounts.  If you must use IAM users then all IAM users should be kept in the master account, with only the _AssumeRole_ permission.  Roles are then used to [delegate access across accounts](https://docs.aws.amazon.com/IAM/latest/UserGuide/walkthru_cross-account-with-roles.html) to obtain credentials and console access.  

### Multi Factor Authentication

If developers must use IAM users to assume roles then their originating credentials should be protected by [AWS's Multi Factor Authentication](https://aws.amazon.com/iam/details/mfa/).  This option is completely free and easy to setup and gives an additional layer of security as no IAM user would be able to [assume a role without MFA](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_configure-api-require.html#MFAProtectedAPI-cross-account-delegation).

[instanceroles]: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html
[defdepth]: https://en.wikipedia.org/wiki/Defense_in_depth_(computing)