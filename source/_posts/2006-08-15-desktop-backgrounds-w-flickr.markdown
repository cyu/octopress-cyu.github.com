--- 
wordpress_id: 27
layout: post
title: Desktop Backgrounds w/ Flickr
wordpress_url: http://blog.codeeg.com/2006/08/15/desktop-backgrounds-w-flickr/
permalink: /2006/08/15/desktop-backgrounds-w-flickr.html
---
I usually get my backgrounds from a couple of <a href="http://www.chromasia.com/">photo blogs</a> <a href="http://wvs.topleftpixel.com/">I subscribe to</a>, but using <a href="http://www.redmonk.com/sogrady/archives/002054.html">Flickr for my backgrounds</a> was such a good idea (and a good excuse to play with ruby), that I thought I'd give it a shot.

After some trail and error, and <a href="http://maxdunn.com/typo/articles/2006/07/06/getting-started-with-flickr-on-rails">some</a> <a href="http://moosoft.net/docs/2005/gnome-wallpaper">help</a> online, I was able to come up with this <a href="https://gist.github.com/812220">ruby script to do the trick</a>.  The script will pull the interesting photos for that day, and will try to find the best fit for your screen resolution.  If you don't like the current background, you can run the script again to change it.  With a simple cron entry you can have fresh background at periodic intervals (I have mine set to every 2 hours).

I created the script under Ubuntu GNOME.  If you want to give the script a try, you'll have to edit the script and put in your <a href="http://www.flickr.com/services/api/keys/">Flickr api key and shared secret</a> as well as your screen resolution (unless you're runing on 1440x900).  You'll also need to have rubygems and the rflickr gem installed.
