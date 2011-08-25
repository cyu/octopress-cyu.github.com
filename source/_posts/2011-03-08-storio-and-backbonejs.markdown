--- 
layout: post
title: Stor.IO and Backbone.js
---

[Backbone.js](http://documentcloud.github.com/backbone/) is a nice JavaScript framework that provides some basic structure to your JavaScript application.  What's nice about it is that it does this while at the same time being flexible and letting you make some design decisions on your own.  One of those is how you choose store you data.

While looking at Backbone's extensive documentation, I couldn't help but notice that they had an example todo application that used localStorage as a backing store.  And since the [Stor.IO](easy-storage-for-html5-applications.html) API so closely resembles the localStorage API, it was easy to adapt the example application to use Stor.IO as a backend.  Here's the [Github Project](http://github.com/cyu/storio-backbone-todos).  And you can [play around with the application here](http://cyu.github.com/storio-backbone-todos).

In other news, I've setup [a group on Convore to discuss Stor.IO](https://convore.com/storio/).  I'm on there pretty regularly, so there's a good chance you'll find me there if you have questions.