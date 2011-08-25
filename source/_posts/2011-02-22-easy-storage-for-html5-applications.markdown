--- 
layout: post
title: Easy Storage for HTML5 Applications
---

I'm a big believer that HTML5 will be a game changer.  It reminds me of the introduction of [DHTML](http://en.wikipedia.org/wiki/Dhtml) over a decade ago, and although DHTML the term never really caught on, it definitely paved the way to the eventual discovery of Ajax and an integral part of what is considered standard web application practice today.

A core component of HTML5 is the [localStorage API](http://diveintohtml5.org/storage.html).  With it, you can write a fairly useful application &mdash; all in JavaScript.  There are limitations however: without server-side storage, your data is trapped to that browser, and with the diversity of devices we use today (laptop, smartphones and tablets), applications need to be available wherever you have a browser.

So what if you can write an application, still all in client-side JavaScript, but store data centrally so it can be accessible on all devices and browsers?  This is what [Stor.IO](http://stor.io) does.  Here's some example code:

{% codeblock lang:javascript %}
<script src="http://stor.io/app_storage.js"></script>
<script>
  window.appStorage.$.connect({email: 'my@emailaddress.com'});
  //window.appStorage.$.connect({twitter:true}); // use Twitter OAuth
  window.appStorage.setItem('foo', 'bar');
  window.appStorage.getItem('foo'); // "bar"
  window.appStorage.foo; // "bar"
</script>
{% endcodeblock %}

Including the *app_storage.js* script creates the **appStorage** object on the browser window.  Next, you call the _connect_ method on the server object (_$_), passing in the identity of the user.  Currently, an email-only method of authenticating is available, as well as Twitter OAuth.   Once connected, the appStorage API behaves essentially like the localStorage API.  And it doesn't force you to store strings like localStorage does, meaning you don't need to serialize/deserialize objects to/from JSON.

For reading data from Stor.IO, you'll need to wait on the server to identify the user and retrieve their data, and there's a _ready()_ handler available for that:

{% codeblock lang:javascript %}
<script>
window.appStorage.$.ready(function(){
  var tasks = window.appStorage.tasks;
  for (var i=0; i<tasks.length; i++) {
    console.log(tasks[i].text);
  }
});
</script>
{% endcodeblock %}

Underneath, how Stor.IO works is that it creates an iframe and uses the [postMessage API](http://ajaxian.com/archives/cross-window-messaging-with-html-5-postmessage) to work around the same origin policy that handicaps Ajax calls.  The server is Sinatra app with the data being stored in MongoDB.  The data is isolated by the user identity and the application path, which is a substring the current URL up to the first directory path, so http://localhost/app1 and http://localhost/app2 will actually hold different data sets.

To flush out the initial implementation, I wrote a very rudimentary [todo application](http://blog.sourcebender.com/todojs).  It's actually hosted on Github pages, so you can see how everything works from the [project page](http://github.com/cyu/todojs).  Even better is that you can fork the project and immediately have groundwork on your own todo application, with hosting courtesy of Github.

Please give it a shot and join the [Google Group](http://groups.google.com/group/storio) if you have questions or are interested in further development.
