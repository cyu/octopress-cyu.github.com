--- 
wordpress_id: 20
layout: post
title: Importing Mail to GMail with GML
wordpress_url: http://blog.codeeg.com/2006/07/11/importing-mail-to-gmail-with-gml/
permalink: /2006/07/11/importing-mail-to-gmail-with-gml.html
---
Having switched to GMail as my primary email client for a couple of months now, I've decided that it was time to try to copy my old emails from Thunderbird to GMail.  From doing a quick search, I find that the tool to use is <a href="http://www.marklyon.org/gmail/download.htm">Mark Lyon's GMail Loader tool</a>.  Unfortunately, that's been the only quick thing so far in this exercise.

Note that I'm using Ubuntu Drapper Drake.  You might have better luck on other systems.

It appears that GMail has changed their SMTP server port and now requires SSL (TLS) authentication, neither of which GML seems to support.   I was eventually able to get GML working with the GMail SMTP server, but I ended up getting a protocol error at the end of every send, which prevents the script from continuing until a timeout from the SMTP server occured.  I strongly recommend using a SMTP server other than GMail's.

Here's my <a href="http://codeeg.com/gmail/gmlw.zip">modified version of the GML script</a>.  Good Luck.

Note that while GML is forwarding an email, the GML GUI won't paint, so don't get frustrated like I did and think that GML locked up.  You'll have to check the console output to see if GML is still running.   If it does seem to be stuck on an email for a long time, you can send a SIGINT to the process to skip that email (remember to note which one you skipped if you want to resend it manually later).
