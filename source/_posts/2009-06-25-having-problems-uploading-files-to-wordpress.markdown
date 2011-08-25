--- 
wordpress_id: 252
layout: post
title: Problems Uploading Files to WordPress?
wordpress_url: http://blog.codeeg.com/?p=252
permalink: /2009/06/25/having-problems-uploading-files-to-wordpress.html
---
A Google search seems to indicate that problems uploading files on WordPress installs is a pretty common occurrence.  Unfortunately, I had the hardest time finding the solution to my particular ailment.  Hopefully, this post will find those others who run into this problem in the future.

From the WP Admin pages, go to <strong>Settings &gt; Miscellaneous</strong>.  Make sure the value for 'Store uploads in this folder' is where you want your files stored (in most cases, it should be <em>wp-content/uploads</em>).
<p style="text-align: center;"><a href="/images/wp/wp-settings.jpg"><img title="Miscellaneous Settings ‹ Don’t Forget to Plant It! — WordPress" src="/images/wp/wp-settings.jpg" alt="Miscellaneous Settings ‹ Don’t Forget to Plant It! — WordPress" width="500" height="196" /></a></p>

In my case, this was pointing to a folder I was using for a WP install I was using to test the Thesis theme I'm using now.  Reverting it to the default fixed my problem.
