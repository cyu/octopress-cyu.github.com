--- 
wordpress_id: 187
layout: post
title: Growl Notifications for Ant
wordpress_url: http://blog.codeeg.com/?p=187
permalink: /2008/10/18/growl-notifications-for-ant.html
---
It's a real refreshing change to be doing developing on Mac these days.  Currently, our Ant builds at work are less than optimal, taking ten's of minutes to do a full build.  Fixing it is something we definitely want to do, but because of the complexity of the build and existing deadlines, right now isn't the best time.  So instead of constantly checking on the progress of my build, I installed this <a href="http://blog.slimeslurp.net/2007/03/18/ant-build-notifications-via-growl/">Growl Ant build listener</a> which will display a Growl notification when a build has completed.

The <a href="http://code.google.com/p/growlbuildlistener/wiki/README">README</a> for the listener got me started - the only thing that didn't work for me is setting the build listener using the <em>ANT_OPT</em> environment variable.  It looks like the default install of Ant on Leopard uses that environment variable as arguments to pass to the Java VM.  So instead, I just used an alias:

{% codeblock lang:ruby %}
alias ant='ant -listener net.slimeslurp.growl.GrowlListener'
{% endcodeblock %}

Just add this line to your <em>~/.bash_login</em> to use the build listener every time you build.
