--- 
wordpress_id: 36
layout: post
title: Tails Update v0.3.5
wordpress_url: http://blog.codeeg.com/2006/10/21/tails-update-v035/
permalink: /2006/10/21/tails-update-v035.html
---
<span style="color:#0000ee;text-decoration:underline;"><a href="/images/wp/tails_geo_support.png"><img class="alignnone size-medium wp-image-119" src="/images/wp/tails_geo_support.png" alt="" width="300" height="162" /></a></span>

I've been holding on this release of my <a title="Tails Extension" href="http://blog.codeeg.com/tails-firefox-extension-03/">Tails Extension</a> for a while now and finally got my butt in gear to get this out.  Here is what's new:
<ul>
	<li>Added <strong>geo</strong> microformat support.  Not very pretty, as it just shows the coordinates, but if you update <a title="Map with Google Tails script." href="http://codeeg.com/tails/scripts/googlemap.tails.js">this Tails script</a> you'll be able to map these geo coordinates to Google.</li>
	<li>Added support for more <strong>hCard</strong> attributes.  Honorific suffix/prefix, organization name/unit - it should be all there now.</li>
	<li>Fixed bug where your IM URL will show as your primary over a normal URL in an <strong>hCard</strong>.  This can easily occur if you used <a title="hCard Creator" href="http://microformats.org/code/hcard/creator">hCard creator</a> to create your hCard.</li>
	<li>Updated icon to a cleaner one, and updated the extension to show a custom extension logo instead of the generic Firefox one.  Thanks to <a title="Dmitry Baranovskiyâ€™s Blog" href="http://dmitry.baranovskiy.com/">Dmitry Baranovskiy</a> for providing the graphics.</li>
	<li>Updated <strong>hCalendar</strong> to display more dates properly.  Date only or time only values should now display correctly.</li>
	<li>Made some small fixes in hopes to correct some problems reported by users.</li>
</ul>
As before, this release will be available initially as a <a title="Go here to download Tails" href="http://blog.codeeg.com/tails-firefox-extension-03/">manual update</a>, I'll be updating the auto-update mechanism a few days later if all goes well.
