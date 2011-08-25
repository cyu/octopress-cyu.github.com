--- 
wordpress_id: 284
layout: post
title: Introducing Rack::CORS
wordpress_url: http://blog.codeeg.com/?p=284
permalink: /2010/06/09/introducin-rack-cors.html
---
Recently, I've been working on an HTML5 project that needed to need to retrieve data from a different origin, and decided to look at using CORS.

CORS, or Cross-Origin Resource Sharing is a specification that allows web applications to make AJAX calls cross-origin without resorting to workarounds such as <a title="Wikipedia write up on JSONP" href="http://en.wikipedia.org/wiki/JSON#JSONP">JSONP</a>.

Searching around, I found an CORS extension for Sinatra, which happened to be the framework I was using.  However, the extension didn't properly implement the spec, nor did it support CORS preflighting (required for more complex AJAX requests).  So I rolled my own, but as a Rack Middleware.  Here's an example of a Rackup that shows it in action (this example uses <a title="Rack::CORS Rubygem" href="http://rubygems.org/gems/rack-cors">Rack::CORS</a> in Sinatra app, but should be able to use it in any Rack compatible framework):

{% highlight ruby %}
require 'sinatra'
require 'rack/cors'

use Rack::Cors do |config|
  config.allow do |allow|
    allow.origins '*'
    allow.resource '/file/list_all/', :headers =&gt; :any
    allow.resource '/file/at/*',
        :methods =&gt; [:get, :post, :put, :delete],
        :headers =&gt; :any,
        :max_age =&gt; 0
  end
end

get '/file/list_all/' do
  #...
end

get '/file/at/*' do
  #...
end
{% endhighlight %}

To get going with Rack::CORS, just install the rack-cors Gem.  To check out the source, see <a href="http://github.com/cyu/rack-cors">the project on Github</a>.

If you want to learn more about CORS, here are some good links I found along the way:
<ul>
	<li>The <a title="Cross-Origin Resource Sharing Working Draft" href="http://www.w3.org/TR/access-control/">W3C Working Draft on CORS</a>, for good night time reading.</li>
	<li>A <a title="Cross-domain Ajax with Cross-Origin Resource Sharing" href="http://www.nczonline.net/blog/2010/05/25/cross-domain-ajax-with-cross-origin-resource-sharing/">good article about CORS</a> that summarizes the CORS spec.</li>
	<li>You can <a title="CORS Support Tests" href="http://rdfa.digitalbazaar.com/tests/cors/">check if your browsers support CORS here</a>.  This site records all pass/fails so you'll be able to see a list of CORS supported (and not supported) browsers.</li>
	<li>The <a title="Cross Origin Resource Sharing with Sinatra" href="http://britg.com/2009/12/29/cross-origin-resource-sharing-with-sinatra/">Sinatra CORS Extension</a> I found.</li>
</ul>
