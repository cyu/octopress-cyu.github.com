--- 
wordpress_id: 271
layout: post
title: Installing Native Gems with Custom Library Paths
wordpress_url: http://blog.codeeg.com/?p=271
permalink: /2009/09/06/installing-native-gems-with-custom-library-paths.html
---
A few weeks ago, I started using the <a href="http://github.com/toland/patron/tree/master">Patron</a> Gem for Skribit and ran into an issue on our CentOS production servers which uses a very old version of libcurl.  I got it working by compiling a new version of libcurl and building the Gem against those binaries.  Since I didn't want to overwrite the libcurl that CentOS provided, I installed the binaries in another location instead, and updated the <strong>LD_LIBRARY_PATH</strong> environment variable so Rails could properly load the Gem.

A couple of days ago, <a href="http://paulstamatiou.com">Paul</a> brought to my attention that <a href="http://linuxmafia.com/faq/Admin/ld-lib-path.html">using LD_LIBRARY_PATH isn't a good thing</a>.  While I didn't necessarily think it was a big deal, it did peak my curiosity on how I would get this work without it.  Here's the command I finally used to get it to work:

{% highlight bash %}
sudo env PATH="/opt/curl/bin:$PATH" gem install toland-patron \
    -v "0.4.1" --source http://gems.github.com \
    -- --with-ldflags="-Wl,-R/opt/curl/lib"
{% endhighlight %}

The key part is the <strong>--with-ldflags</strong> option at the very end.  The <strong>-Wl,-R&lt;path&gt;</strong> option adds the given path to the list of paths the linker will use to find libraries at runtime.  Hopefully, someone will find this information useful, since I couldn't find this information myself on the 'nets anywhere.
