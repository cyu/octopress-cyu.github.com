--- 
wordpress_id: 19
layout: post
title: Resurrecting Tails
wordpress_url: http://blog.codeeg.com/2006/07/10/resurrecting-tails/
permalink: /2006/07/10/resurrecting-tails.html
---
After careful thought and <a href="http://microformats.org/wiki/user-interface">some</a> <a href="http://ben-ward.co.uk/journal/microformats-ui/">inspiration</a>, I've decided to bring my original <a href="http://blog.codeeg.com/tails-firefox-extension/">Tails Extension</a> out of retirement.  It wasn't a decision I took lightly, since <a href="http://bordewolf.blogspot.com/">Robert</a> has done such a great job with the <a href="https://addons.mozilla.org/firefox/2240/">Tails Export Extension</a> and I didn't want to duplicate his effort, but in order to execute my vision of what I wanted to do, I practically had to rebuild Tails (and Flocktails) from the ground up.

So what exactly has changed?  Both the Firefox and Flock extensions has now been consolidated into one.  I was planning to just continue on with the Flock line, but since I still spend most of my time using Firefox, I felt it was necessary to have it work with both.  Also, the parser has been rewritten to easily support future microformats as well fixed some performance problems that I've encountered when switching tabs.  For the UI, I've moved the main view from Firefox's sidebar and Flock's topbar to an overlay approach over the browser content area (pictured below).  Finally, I added some extensibility to the extension, which is the part of Tails I'm most excited about - I'll talk more about this when I release the plugin.
I'm expecting to have the extension ready in the a few days, here's a preview of what it will look like:

<span style="color:#0000ee;text-decoration:underline;"><a href="/images/wp/tails_0-9_screenshot.png"><img class="alignnone size-medium wp-image-126" src="/images/wp/tails_0-9_screenshot.png?w=300" alt="" width="300" height="199" /></a></span>

I'm very excited with the results, this update will make the extension more useful whereas before it was merely something that was just cool.  What remains to be done is some final testing and a little documentation of how to use the extension.  I also need to figure out an adequate license for the extension, so any feedback on this would be appreciated.
