--- 
layout: post
title: "Building an HTML5 Application, Part 3: Let's Take this Offline"
---

_Here's [Part 1](building-an-html5-application-part1.html) and [Part 2](building-an-html5-application-part2.html) of this series._

So after taking a break to spend time with family (yay!) and doing taxes (bleh!), I was able to spend some time on Thymer again.  It's time to get it working offline.

Since it doesn't require a server, Thymer is a perfect candidate to be an offline application.  In HTML5 you do this by telling the browser what files it should store locally so they are available offline.  You do this in a file called the **Cache Manifest** file.  The [one for Thymer](https://github.com/cyu/thymer/blob/part3/thymer.appcache) looks like this:

{% codeblock lang:bash %}
CACHE MANIFEST
# Revision: 10
alarm.mp3
alarm.ogg
alarm.wav
clock_32x32.png
index.html
jquery-1.5.2.min.js
minus_12x3.png
reload_12x14.png
thymer.css
thymer.js
{% endcodeblock %}

In this file, I list all the files I'm going to need when offline.  It's important to note that files listed here must follow the **same origin policy**, meaning the files must be served from the same domain.  I ran into this since I was using a Google hosted version of jQuery, and had to switch to self-hosting instead. 

Another important thing to note is the second line of the manifest, where I specify the revision of the manifest in a comment.  Browsers will only update their offline cache when the manifest changes, and not when the files listed in the manifest change.  Common practice then is to update the revision number in the manifest to notify browsers to update their cache.

I ended up creating [a rake task to generate the cache manifest](https://github.com/cyu/thymer/blob/part3/Rakefile), updating the file list when new files are added and incrementing the revision number on any changes.  To update the manifest, I just run the manifest task:

{% codeblock lang:bash %}
rake thymer.appcache
{% endcodeblock %}

Once the manifest file is created, I need to reference that manifest from the page. You do this by setting the **manifest** attribute on the _html_ element:

{% codeblock lang:html %}
<!doctype html>
<html manifest="thymer.appcache">
{% endcodeblock %}


Handling Updates in the Browser
------------------------------------------

Some browsers must be explicitly told to update the application cache when it sees an update. Here's how that is done:

{% codeblock lang:javascript %}
// check for updates
if ('applicationCache' in window) {
  $('#update-button').click(function() {
    // Ensure the browser uses the latest version of the code
    window.applicationCache.swapCache();
    // Reload the application
    window.location.reload();
  });

  window.applicationCache.addEventListener('updateready', function() {
    $("#update").show();
  }, false);
}
{% endcodeblock %}

In the above code, I just show a short message with a link to _swapCache()_ and reload when a new update is available.  Note that in some browsers, the update doesn't happen until _swapCache()_ is called, while others it's automatic and all you really have to do is reload.

In JavaScript, you can detect your current offline/online status with _navigator.onLine_.  You can also listen to _offline_ and _online_ events in the document body.  For Thymer, I decided to check the manifest for updates when the browser comes back online:

{% codeblock lang:javascript %}
// Check for updates when the browser comes back online
$(document.body).bind('online', function(){
  window.applicationCache.update();
});
{% endcodeblock %}

In testing, it looks like listening for _online_ event doesn't yet work in Chrome or Safari. 


Other Notes
-----------

* When serving the manifest file, make sure it is served with a _Content-Type_ header of 'text/cache-manifest'.

* A lot of references and tutorials I found often named the manifest file _cache.manifest_, but it looks like _.appcache_ will ultimately be [the standard extension](http://www.w3.org/TR/html5/iana.html#text-cache-manifest).  This make sense, since the latter will probably have a lesser chance of name collisions with other file types.

* I ended up declaring all versions of my audio file in the manifest, which is less that optimal since browsers would only use one of the three sources.  I could dynamically generate the manifest based on User Agent, but that's less than ideal. 

* You can browse the contents of the offline cache in FF by going to **about:cache** from the address bar. In Chrome, you can see it for the current page under the Resources tab from within the Web Inspector.  Didn't see where this information was available in Safari.


That's a Wrap
-------------

That's it for Offline mode.  In the next and most likely the final post in this series, I'm going to get Thymer onto the Chrome web store.  If you want to learn more about Offline mode, HTML5Rocks has curated a [bunch of articles related to offline](http://www.html5rocks.com/features/offline).  And here is [the source code](https://github.com/cyu/thymer/tree/part3) referenced by this post.

