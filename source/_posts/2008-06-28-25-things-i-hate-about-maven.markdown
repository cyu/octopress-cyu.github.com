--- 
wordpress_id: 144
layout: post
title: 25 Things I Hate about Maven
wordpress_url: http://dontforgettoplantit.wordpress.com/?p=148
permalink: /2008/06/28/25-things-i-hate-about-maven.html
---
I've been doing a lot of work with Maven recently, and having a miserable time of it.  Earlier this week I was ranting about it on a mailing list I was on, when I thought it would be therapeutic to try to list 100 things that irks me about Maven 2 that I've personally ran into.  So, I didn't come close - I only came up with 25.  But I do feel much better now.

Here goes, in no particular order:
<ol>
	<li>The Maven AntRun tasks allows you run ant from within Maven, but you have very limited access to the POM.</li>
	<li>If you have a multi-module project configuration, changing the version of the root project requires you to change all the versions of the sub-modules</li>
	<li>Maven Ant Tasks doesn't resolve transitive dependencies exactly the same as a regular Maven project does.</li>
	<li>Maven manages adding all the dependencies you need... and then some.  You end up probably spending the same amount of time having to exclude the dependencies you don't need, especially in EAR/WAR setups</li>
	<li>You pretty much have to declare the versions of every Maven plugin you use, or risk your build breaking when someone updates the plugin.</li>
	<li>You can't create a 'macro goal' that is a chain of multiple goals</li>
	<li>Your custom plugins might not work if it is organized as a sub-module of a project.  Inexplicably, if you run the build inside that sub-module it works.  (Might just be a problem with Ant-based plugins)</li>
	<li>Maven goes out of its way to not use Ant.  So, some things that work correctly in Ant don't in Maven (for example, building GNU compliant tarball with the assembly plugin)</li>
	<li>You can activate build profiles based on OS, file existence, and environment variables in Maven, but how do you disable them?</li>
	<li>You can configure the build to deploy additional artifacts (e.g. javadoc and sources), but it won't use the repository or snapshot repository configured for your project</li>
	<li>Figuring out how a build works from reading plugin declarations is not easier than reading an Ant script</li>
	<li>Good luck trying to find the artifact that you need to fix your NoClassDefFoundError</li>
	<li>Passing Maven properties to your AntRun configuration?  Bah! who needs that?</li>
	<li>What happened to my Maven 1.x pre/post-goals?  How is attaching plugins to build phases a better solution?</li>
	<li>Multi-module projects is like having old school recursive Makefiles</li>
	<li>Why can't I define variables other than artifactId, groupId, and version to be substituted when building from an archetype?</li>
	<li>Why can't all the files in archetype-resources be included in the archetype?  Why do I have to define them all in an archetype.xml as well?</li>
	<li>Versions of dependencies with classifiers are not be inheritable</li>
	<li>Extending a build is difficult without creating a plugin, which requires creating yet another project</li>
	<li>Customizations to the build always seems to take a few takes of trial and error before you can get them working.</li>
	<li>Configurations specified for an Ant-based plugin doesn't work if they're specified at the execution level or the build profile level.  They will work if you specify them globally</li>
	<li>Maintaining updates of plugins and what bugs are fixed in what version and what Maven version it's compatible with is a PITA.</li>
	<li>Documentation sucks.  Pretty much everything out there is surface deep.  There's 50/50 chance that features that are skimmed over in the docs won't work as expected</li>
	<li>Why does the site:deploy and site:stage-deploy behave so differently for multi-module projects?</li>
	<li>Why are build profiles inheritable?</li>
</ol>
So I imagine some of the explanation are vague, but my experience is that it is par for the course when you deal with builds in Maven.  Sometimes there's seemingly no rhyme or reason for why things don't work, and by the time you do find a workaround that does, you just don't want to spend anymore time figuring why your previous approaches didn't work.  I supposed the open source thing to do is to help fix the problem, but honestly, I just don't love Maven that much.
