--- 
wordpress_id: 26
layout: post
title: Tails Release 0.3.2
wordpress_url: http://blog.codeeg.com/2006/08/05/tails-release-032/
permalink: /2006/08/05/tails-release-032.html
---
What's in this release:
<ul>
	<li>Fixed a bug which caused multiple tabs to be closed when the <a title="Tab Mix Plus Firefox extension" href="https://addons.mozilla.org/firefox/1122/">Tab Mix Plus</a> extension is installed (thanks to <em>onemen</em> at the <a href="http://tmp.garyr.net/forum/">TMP forums</a> for helping me figure this out).</li>
	<li>Added support for the <em>include</em> microformat pattern, which <a href="http://www.last-child.com/the-hreview-format-on-yahoo-tech/">is apparently being used at Yahoo! Tech</a>.</li>
	<li>Added better <em>ratings</em> handling for hReviews.</li>
	<li>Added # of objects to the tab title.</li>
	<li>Added support for <a href="http://microformats.org/wiki/hresume">hResumes</a>.</li>
	<li>Added an update URL to the extension, so the next release will be updatable via Firefox's extension update mechanism.</li>
	<li>A few bug fixes that would be too boring to describe detail.</li>
</ul>
In addition to these changes, I've put the source code on <a href="http://code.google.com/p/tails-firefox-extension/">Google Code</a>, under the MIT License.

So what's next for Tails?  Here's what I have left on my list:
<ul>
	<li>Make the overlay box resizeable.</li>
	<li>Display the relationship between parent/child microformats.  Right now, I'm displaying all objects found on the page, even if the object is really  a child of another (the hCard author of an hEntry blog post, for example).  While this is good in some ways, I would like an intuitive way to display these relationships.  I'm still trying to figure out what this is.</li>
	<li>Pull avatars from external sources, like from <a href="http://www.gravatar.com/">Gravatar</a> and <a href="http://www.weekendr.com/landingpage/default.asp">Who-R-You</a>.</li>
	<li>I would also like to figure out a way to pull external data to complement the data in the microformats.  The one method I have came up with so far is to use <a href="http://www.claimid.com/">claimID</a> to pull all the links associated with that user, and display the data from the services that the user has links to.  So for example, if the user has a link to his Flickr account, I could display that user's most recent images.  However, since claimID isn't that widely used just yet, I would like to figure out another solution that would give me the most bang for my buck.</li>
</ul>
Anyway, enjoy.  And send me your feedback.

<strong>Update: </strong>You can <a href="http://blog.codeeg.com/tails-firefox-extension-03/">get the extension here</a>.
