--- 
layout: post
title: 'Building an HTML5 Application, Part 1: Local Storage'
---

So far, I've [dabble with pieces of HTML5](easy-storage-for-html5-applications.html), having build the rite-of-passage Todo application - now it's time to jump in and build a more complete application.  In a series of posts, I'm going to build an HTML5 application from scratch and document my experiences along the way.  Let's start off by exploring HTML5's Web Storage feature.

The application I've decided to build is a timer application - basically, you enter a time interval (in hours, minutes, seconds), and it'll notify you when that time has been reached.  I start things off by creating the basics of what the application would look like via HTML:

{% highlight html %}
<!doctype html>
<html>
<head>
<title>Thymer</title>
</head>
<body>
  <header>
    <h1>Thymer</h1>
  </header>
  <div id=content>
    <div id=add-timer-form>
      <input class=text name=hours value=00 size=2> :
      <input class=text name=mins value=05 size=2> :
      <input class=text name=secs value=00 size=2>
      <input name=name placeholder='Timer Name'>
      <input type=submit value='Create Timer'>
    </div>
    <ul id=timer-list></ul>
  </div>
  <script src=thymer.js></script>
</body>
</html>
{% endhighlight %}

Couple of notes about the above snippet:

1. The *doctype* and lack of attribute quoting are standard to the spec.  One of the key points of HTML5 was identify the lowest common denominator between the popular browsers and based the spec around them.  In this case, the doctype of *html* was the minimum needed to be a valid doctype and attribute values do not need to be quoted unless there are whitespace in the value.

2. Line #21: I'm using the new *placeholder* attribute which puts a placeholder text in the text input when the input is empty and doesn't have value.  Once you put focus on that text input and enter a value, the place holder text goes away.

Next comes the *thymer.js* script.  Nothing HTML5 specific here, I'm just putting the code here for completeness.

{% highlight javascript %}
$().ready(function(){
  var timerList = $('#timer-list');
  var timers = [];

  var UpdateLoop = {
    start:function() {
      if (!this.started) {
        this.started = true;
        this.interval = setInterval(function(){
          UpdateLoop.update();
        },1000);
      }
    },
    update:function() {
      if (timers.length > 0) {
        for (var i in timers) {
          timers[i].update();
        }

      } else {
        clearInterval(this.interval);
        this.interval = null;
        this.started = false;
      }
    }
  };

  var Timer = function(name, seconds) {
    this.name = name;
    this.seconds = seconds;
    this.started = new Date().getTime();
    this.finished = false;
    this.start();
  };
  Timer.prototype = {
    start:function() {
      this.el = $("<li>" + this.buildDisplayString() + "</li>");
      timerList.append(this.el);
    },
    update:function() {
      if (!this.finished) {
        if (this.check()) {
          var timer = this;
          var removeLink = $('<a href="#">remove</a>').click(function(){
            timer.remove();
          });
          this.el.text('ALARM!!! - ' + this.name + ' ');
          this.el.append(removeLink);
        } else {
          this.el.text(this.buildDisplayString());
        }
      }
    },
    remove:function() {
      this.el.remove();
      for (var i in timers) {
        if (timers[i] == this) {
          timers.splice(i,1);
          break;
        }
      }
    },
    check:function() {
      var remaining = this.calculateRemaining();
      if (remaining <= 0) {
        this.finished = true;
        return true;
      }
      return false;
    },
    calculateRemaining:function() {
      return this.seconds - Math.floor((new Date().getTime() - this.started) / 1000);
    },
    buildDisplayString:function() {
      var s = [];

      var remaining = this.calculateRemaining();
      remaining = this.buildTimeSegment('h', 60*60, remaining, s);
      remaining = this.buildTimeSegment('m', 60, remaining, s);
      s.push(remaining + 's');

      return s.join(' ') + ' - ' + this.name;
    },
    buildTimeSegment:function(suffix, divisor, secondsRemaining, segments) {
      var units = Math.floor(secondsRemaining / divisor);
      if (units > 0) {
        segments.push(units + suffix);
        return secondsRemaining % divisor;
      }
      return secondsRemaining;
    }
  };

  $('#add-timer-form form').submit(function(){
    var seconds = parseInt($('#secs').val()) +
        (parseInt($('#mins').val()) * 60) +
        (parseInt($('#hours').val()) * 60 * 60);
    var timer = new Timer($('#timer-name').val(), seconds)
    timers.push(timer);
    UpdateLoop.start();
    return false;
  });
});
{% endhighlight %}

I now have a basic timer application.  Now for the HTML5 goodness.

For any desktop to be truly useful (desktop or web), it needs to be able to remember state from the last time you ran the application.  For desktop applications, there are many different ways to do this, but web applications have always been limited to cookie or server-based storage.  In HTML5, there are actually a few options for storing data, with the most commonly supported one being the **Local Storage API**.  Local Storage API is a simple API that allows you to store data as key/value pairs.  For my Thymer application, I'm going to store the timer array so any created timers will be persisted across browser reloads.

First, I update the *Timer* object so it can be converted to/from a save state:

{% highlight javascript %}
var Timer = function(name, seconds, started, finished) {
  this.name = name;
  this.seconds = seconds;
  this.started = started ? started : new Date().getTime();
  this.finished = finished || false;
  this.start();
};
Timer.prototype = {
  // the rest of the Timer prototype...

  toObject:function() {
    return {
      name: this.name,
      seconds: this.seconds,
      started: this.started,
      finished: this.finished
    };
  }
}
{% endhighlight %}

Then I save the timer array every time a new timer is created, and load the stored timers when the application starts:

{% highlight javascript %}
$('#add-timer-form form').submit(function(){
  var seconds = parseInt($('#secs').val()) +
      (parseInt($('#mins').val()) * 60) +
      (parseInt($('#hours').val()) * 60 * 60);

  var timer = new Timer($('#timer-name').val(), seconds)
  timers.push(timer);

  // store timers
  if ('localStorage' in window) {
    var arr = [];
    for (var i in timers) {
      arr.push(timers[i].toObject());
    }
    window.localStorage.setItem('timers', JSON.stringify(arr));
  }

  UpdateLoop.start();
  return false;
});

// load stored timers
if ('localStorage' in window) {
  var timersData = window.localStorage.getItem('timers');
  if (timersData) {
    var timersData = JSON.parse(timersData);
    for (var i in timersData) {
      var t = timersData[i];
      timers.push(new Timer(t.name, t.seconds, t.started, t.finished));
    }
    UpdateLoop.start();
  }
}
{% endhighlight %}

Some notes about the **Local Storage API**:

1. _localStorage_ only stores string values, so use *JSON.stringify()* and *JSON.parse()* to convert your data to/from JSON.

2. In addition to _setItem_ and _getItem_, there are also *clear* and *removeItem* functions available.

3. You can also access stored values directly as properties on the *localStorage* object (e.g. *window.localStorage.timers*).

4. Values are stored to an *origin*, which is the combination of **scheme (http/https) + host + port**.  This means other pages on that server could access those stored values, so attention should be paid to avoid naming collisions.

5. Origin pinning also means that if a page can be viewed via multiple domains (www.example.com and example.com for example), you won't be able to access stored values between those two domains.  Consider using permanent redirects to get users under one domain.

6. Local Storage doesn't seem to work in Firefox with pages served via the _file://_ protocol - you'll need to serve your page from a web server when testing locally.

So that's it for the part 1.  A lot of this is common knowledge for those who have already read up on HTML5, but now that we've setup the basic of the application, we can move on to more interesting aspects of HTML5.  In part 2, I'll cover playing audio natively and using Chrome's notification API.

You can get [the final code for Part I here](https://github.com/cyu/thymer/tree/part1).  If you're interested in going deeper into HTML5, I highly recommend visiting Mark Pilgrim's [Dive Into HTML5](http://diveintohtml5.org/) and getting his *HTML5: Up and Running* book.
