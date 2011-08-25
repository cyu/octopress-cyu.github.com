--- 
wordpress_id: 45
layout: post
title: Finding the Package You Need in Ubuntu
wordpress_url: http://blog.codeeg.com/2006/11/12/finding-the-package-you-need-in-ubuntu/
permalink: /2006/11/12/finding-the-package-you-need-in-ubuntu.html
---
I just discovered the handy <strong>apt-file</strong> command in Ubuntu today while trying to resolve the dependencies need to install <a title="Hpricot" href="http://code.whytheluckystiff.net/hpricot/">Hpricot</a>.  With this utility, you call search through all the packages in your repositories (installed and not installed) for a given file.  For example:
{% highlight bash %}
apt-file search stdlib.h
{% endhighlight %}
Will return a list of packages with that header file.  In order for this command to work though, you'll need to at least have ran this command once:
{% highlight bash %}
sudo apt-file update
{% endhighlight %}
