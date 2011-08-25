--- 
wordpress_id: 83
layout: post
title: Lifestreaming using Yahoo! Pipes
wordpress_url: http://blog.codeeg.com/2007/09/22/lifestreaming-using-yahoo-pipes/
permalink: /2007/09/22/lifestreaming-using-yahoo-pipes.html
---
Some of you might have noticed that I recently added a <em><strong>What I'm up to</strong><strong> </strong></em>feature on my blog.  While I'm not normally a frequent blogger (I actually consider that a feature of this blog), I am pretty active elsewhere on the internet.  So I thought it would be cool to create an aggregated feed of my online activities, commonly referred to as a Lifestream.  This seemed like the perfect job for <a href="http://pipes.yahoo.com">Yahoo! Pipes</a> and apparently <a title="A Lifestream Yahoo! Pipes Search" href="http://pipes.yahoo.com/pipes/search?q=lifestream&amp;x=0&amp;y=0">I'm not alone in that thought</a>.

In case you've been in a non-WIFI enabled cave the last few months, here's Yahoo!'s description of what Pipes does:
<blockquote>Pipes is a powerful composition tool to aggregate, manipulate, and mashup content from around the web.</blockquote>
Essentially, Pipes is an <a title="Read more about ETL" href="http://en.wikipedia.org/wiki/Etl">ETL</a> tool for web data, with resulting output being an RSS feed, JSON data, or  web widget.

Being that I'm already using Web version 2.0, most of my activity on the internet culminates into some sort of RSS feed.  Off the top of my head, I chose to compose my lifestream from my <a title="Calvin Yu's twitters" href="http://twitter.com/cyu">twitter</a> and <a title="Calvin Yu's Delicious Links" href="http://del.icio.us/cyu">delicious</a> accounts, as well as a <a title="Beast Forums" href="http://beast.caboo.se">couple of</a> <a title="Boardista, My Forums Site" href="http://boardista.com">forums</a> that I monitor (shameless plug -- Boardista is a forums website I'm currently working on).

So here's how I created my Lifestream feed.  Here's <a title="Calvin Yu's Yahoo! Pipes Page" href="http://pipes.yahoo.com/pipes/person.info?eyuid=ePPle0cwsXa00IP.0w--">my Pipes page</a> if you want to follow along.  Initially, I had everything in one large Pipe, but quickly decided to break them up to make things more maintainable.  One really cool thing about Pipes is that it allows you to break up large Pipes into smaller, interconnected ones, making things easier to manage.

<strong>First</strong>, I fetched my twitter, delicious, and forum feeds using the Fetch Feed module.  I do this in the LifeStream: Twitter/Delicious/Forums Pipes.  I separated them out because each type of feed had some characteristics that I wanted to transform from so that when I merged them individual items had some level of consistency with each other.  I also wanted to modify the author of each item so that I could later render an icon to identify the source of the item.

<span style="color:#0000ee;text-decoration:underline;"><a href="/images/wp/pipes_forums.png"><img class="alignnone size-medium wp-image-109" src="/images/wp/pipes_forums.png" alt="" width="300" height="160" /></a></span>

<strong>Second</strong>, I merged the individual feeds into one large one (Pipe Lifestream: Merge Sources):

<span style="color:#0000ee;text-decoration:underline;"><a href="/images/wp/pipes_merge.png"><img class="alignnone size-medium wp-image-110" src="/images/wp/pipes_merge.png" alt="" width="300" height="158" /></a>
</span>

<strong>Then</strong>, I  sorted the feeds, chopped the feed to only show the last 5 items, and truncated the description to 150 characters if necessary (Pipe LifeStream).

<a href="/images/wp/pipes_lifestream.png"><img class="alignnone size-medium wp-image-111" src="/images/wp/pipes_lifestream.png" alt="" width="300" height="147" /></a>

<strong>Finally</strong>, I needed a way to show this on my blog.  I really liked how <a title="Andy Bennett's Blog" href="http://andybennett.net/">Andy Bennett</a> showed his latest twitter on his blog, so I wanted to have something like that.  Doing some research online, I was able to find the <a href="http://adambrown.info/b/widgets/category/kb-advanced-rss/">KB Advanced RSS Widget</a> which did mostly what I wanted, all I had to do is tweak it to show the correct icon based on the author I set in the first step.

So after few hours of work, I had a pretty cool Lifestream feed.  Overtime, I expect to add more feeds to make my lifestream more complete (I would love to add my <a href="http://cocomment.com">coComment</a> feed, if I can only get my actual comment in the feed).

I've also learned quite a bit about Yahoo! Pipes:
<ul>
	<li>It's pretty amazing what you can accomplish with such a finite set of functionality.</li>
	<li>I'm skeptical that your average internet users is going to be able to build truly useful Pipe without help.  I was often frustrated by how Pipes wouldn't let me connect some modules, and by how some controls were enabled/disabled by some seemingly illogical condition.</li>
	<li>Being able to interconnect Pipes can potentially create some amazing results.  It would be even  cooler if I can plug in other people's Pipes.</li>
	<li>There's a Web Service functionality available that allow developers to provide some custom transformations for Pipes, which gives Pipes virtually unlimited capabilities.  It also means that you can potentially use Pipes to <em>push</em> data to your application.</li>
</ul>
