--- 
wordpress_id: 277
layout: post
title: Setting up Virtual Hosts on Mac OSX
wordpress_url: http://blog.codeeg.com/?p=277
permalink: /2010/03/26/setting-up-virtual-hosts-on-mac-osx.html
---
I've been juggling a few different web projects lately, and decided to setup different virtual hosts on my Mac so that I can easily work with them.  Googling around gave me a lot of different answers, none of which seem to work completely.  This is what finally worked for me (on Snow Leopard).

First, add a new local domain to your <em>/etc/hosts</em> file:
<pre>127.0.0.1       localhost devsite.local</pre>

Next, you'll need to configure Apache with this new virtual host.  Fortunately, the default Apache config has this partially setup.  Open up <em>/etc/apache2/httpd.conf</em> and uncomment the following Include:

{% highlight apache %}
# Virtual hosts
#Include /private/etc/apache2/extra/httpd-vhosts.conf
{% endhighlight %}

Now, we need to add our virtual host to the <em>httpd-vhosts.conf </em>file referenced above.  The file already had a couple of sample configuration in it, but I commented out those and added the following:

{% highlight apache %}
<VirtualHost *:80>
    DocumentRoot "/Library/WebServer/Documents"
    ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "/usr/docs/devsite.local"
    ServerName devsite.local
</VirtualHost>
{% endhighlight %}

This first entry will map localhost to its default document location (without it http://localhost won't work correctly).  The second entry maps my new domain.  Additionally, you'll want to make sure files in your new docs directory have adequate access permissions.  I ended adding a new Directory section to <em>httpd-vhosts.conf </em>file:

{% highlight apache %}
<Directory "/usr/docs/devsite.local">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
{% endhighlight %}

Now all you have to do is put your web files in <em>/usr/docs/devsite.local</em>.  I originally had my new local domain map to <em>&lt;user dir&gt;/Sites/devsite.local</em>, but changed it because I would have to make sure Apache could access to all the directories leading up to those docs. So instead I just symlinked my http docs from my user directory into <em>/usr/docs.</em>
