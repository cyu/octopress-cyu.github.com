--- 
wordpress_id: 292
layout: post
title: Loading CouchDB Views from Source Files
wordpress_url: http://blog.codeeg.com/?p=292
permalink: /2010/07/28/loading-couchdb-views.html
---
I've been doing a lot work with CouchDB lately for Socialytics, and which means writing map/reduce functions in JavaScript for building views.  I was beginning to have a healthy set of views, it made sense to have this code in version control and be able to load these views to a CouchDB instance via the command line.  Not finding anything like this on the interwebs, I decided to come with something on my own.

My first pass at it was a Ruby implementation, but was fragile since it found the map and reduce functions via regular expressions.  This past weekend I decided to give a go with a new implementation using <a href="http://nodejs.org">Node.js</a>.  Since I'm now using JavaScript, I no longer had to use regular expressions to sniff out the map/reduce functions - I can just load the scripts up as code.  Another additional benefit is that now the view code got parsed, so I find syntax errors before the are loaded to Couch.

<a title="loader.js" href="http://gist.github.com/492124">Here's the code</a>.  The script expects a <em>designs/</em> folder at the same level as the loader script, with a subfolder for each design document underneath.  A design folder should have a <em>.js</em> file for each view.  A view file looks like this:

{% highlight javascript %}
design.view = {
    map: function(doc) {
        emit(doc.created_at, null);
    },
    reduce: '_count'
};
{% endhighlight %}

<a href="http://wiki.apache.org/couchdb/Document_Update_Handlers">CouchDB document update handlers</a> are supported as well by assigning a function to <strong>design.update</strong>.  Once your view files are ready, just run <strong>loader.js</strong> with the CouchDB database URL as the parameter:

<pre>node db/couchdb/loader.js http://localhost:5984/myDatabase</pre>

So what do you think?  Does something like this exist already?  Is there a better way to do this?
