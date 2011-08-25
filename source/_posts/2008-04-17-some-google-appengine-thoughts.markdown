--- 
wordpress_id: 94
layout: post
title: Some Google AppEngine Thoughts
wordpress_url: http://blog.codeeg.com/?p=146
permalink: /2008/04/17/some-google-appengine-thoughts.html
---
I'm still waiting to get into the GAE beta, but I wanted to share a couple of thoughts about why I think GAE is significant beyond grid computing and making it cheaper for developers to build applications.

<strong>A New Way of Building Web Applications</strong>

Today, when we build applications developers have to pretty much understand the full stack from top to bottom.  If you're a PHP person, you need to know LAMP.  If you're a Java person, you need to know J2EE, the Application Server, etc.  GAE removes that need - all you need to know is how to code your application logic, GAE handles the data storage, scaling, deployment, web serving, etc for you.  It is the <strong>ultimate application server</strong>.

This model can work very well outside of grid environments.  What if companies have their own app engines, which allows their developers to code to application units with push button ability to deploy to development, staging, production?

Well, isn't this just a Java WAR file you ask?  No, because WAR files aren't opinionated.  You want to use MySQL/Oracle/PostgreSQL?  You want to use EJB/Spring/POJOs?  You can do that with WAR files.  You can't do that with GAE.  Options are great, but they limit your ability to make assumptions, and assumptions makes development easier.  That's what Rails means by convention over configuration.  Most application developers shouldn't really have to care about these issues anyway.

By making assumptions about all these applications, I can make it easier deploy the application to multiple environments.  I can apply sweeping changes that can improve performance for all applications.  Infrastructure support for different applications won't require different knowledge sets.

<strong>Inverting the Facebook Applications Platform</strong>

Another interesting aspect of GAE is that by leveraging Google Accounts, GAE has created a platform that can ultimately be the inverted version of the Facebook Application Platform.  The Facebook platform takes a 'Department Store' model, where applications are housed inside of the Facebook website.  Applications have limited styling capabilities, and pretty much has to adhere to the Facebook look and feel.

In contrast, GAE is more like the 'Mall' of social applications.  Applications can have their own unique storefronts (which allows them to better create a brand), while still taking advantage of the facilities provided by Google.

Granted, Google hasn't yet integrated those social features required to compete with Facebook, and there aren't any signs that it will.  But considering how Google has GData'd every significant service they have, I can't imagine this not being far behind.
