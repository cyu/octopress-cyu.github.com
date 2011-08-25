--- 
wordpress_id: 142
layout: post
title: Troubleshooting Performance Problems
wordpress_url: http://dontforgettoplantit.wordpress.com/?p=146
permalink: /2008/06/10/troubleshooting-performance-problems.html
---
Skribit's downtime last Monday got me thinking about my past experience with performance tuning.  I've troubleshot a lot of performance problems in the past, and here are some things I've noticed:

<strong>It's Never Just Because Pure Load.</strong>  I've used this excuse many times before and still mutter it today, but I never truly believe it.  If you hear yourself saying this, it should be setting off red flags in the back of your head.  Look harder.  Why is it never because of load?  Because we don't write perfect software.  Deadlines happen, we can't always predict how users will use the site, and we sometimes we don't know how things should be designed until later.  Basically, shit happens.  Chances are there's something in the software that's misbehaving under load.

<strong>There are Long Term and Short Term Solutions.</strong>  Depending on the immediacy of the performance problems, you might want to tackle the short term solutions first.  It's hard to fix the long term solution quickly and correctly when you have unhappy customers.

<strong>Know the Performance Problems You're Solving.</strong>  Don't just guess at what the problem might be, try to figure out how to identify it.  Check the logs and maybe the resulting data created.  Try to predict how your site should behave when the problem is occurring and prove it out.  Even if this takes some time, you want to make sure your changes fix the problem, and that if performance problem still exists afterwards at least you know you've correctly fixed one problem.

<strong>Caching is Great for Hammering out Performance Issues.</strong>  I usually use caching as the first line of defense against load.  Others like to tweak database indices, code, and/or configuration first, but my experience has been that caching gives you the most bang for your buck.  However, caching is like cleaning up your room by stuffing everything into your closet - if you don't go back and clean things up later, things will eventually come crashing down.
