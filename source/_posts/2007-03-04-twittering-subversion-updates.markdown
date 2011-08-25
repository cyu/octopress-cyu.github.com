--- 
wordpress_id: 55
layout: post
title: Twittering Subversion Updates
wordpress_url: http://blog.codeeg.com/2007/03/04/twittering-subversion-updates/
permalink: /2007/03/04/twittering-subversion-updates.html
---
Inspired by <a title="Workstreaming post on Web Worker Daily" href="http://webworkerdaily.com/2007/03/03/workstreaming-the-new-face-time/">this workstreaming post on WWD</a>, I thought it would be a great if I could use Twitter as a way to keep track my current yet-to-be-released project.  Twitter is a pretty good fit for workstreaming because it constrains you to a maximum number of characters -- if you're doing something that requires more than that, it really should be in posted in a more formalized medium, such as in an email, blog, or Backpack.  For the sake of the people reading your workstream, posts to be short and to the point.

So the first thing I wanted to try is to post Subversion commits Twitter.  An initial Google search pointed me to this <a title="Subverting Twitter" href="http://www.urbanhonking.com/ideasfordozens/archives/2007/01/subverting_twit.html">post about using rake to post to Twitter</a>, but I think having to use rake to do your commits is very inconvenient, so I decided to write it as an Subversion post-commit hook instead.   Fortunately, I found this <a title="Subversion post commit to Basecamp" href="http://www.webtypes.com/2006/03/31/subversion-post-commit-hook-using-basecamp-api">script which posts SVN updates to Basecamp</a>, which got me started.   <a title="Twitter Post Commit Subversion script" href="https://gist.github.com/812211">Here's the final script</a>.

So what's next?  How about:
<ul>
	<li>Update Capistrano to post deploy events.</li>
	<li>Post updates to Backpack, Writeboards, or Basecamp</li>
	<li>Post updates on important application events and/or errors</li>
</ul>
Granted, this isn't exactly workstreaming -- I could update the hook to make posts based on the committer (any takers?), but I think this is good enough.  Unfortunately, I can't link to what the output of the script looks like because I'm posting to protected Twitter accounts, but if you look at the script it's pretty basic message.
