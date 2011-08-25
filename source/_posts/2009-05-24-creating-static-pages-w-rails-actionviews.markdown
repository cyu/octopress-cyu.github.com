--- 
wordpress_id: 221
layout: post
title: Creating Static Pages w/ Rails ActionViews
wordpress_url: http://blog.codeeg.com/?p=221
permalink: /2009/05/24/creating-static-pages-w-rails-actionviews.html
---
Recently, I needed to create some static reporting pages for Skribit.  From a quick search, I got a lot of results that talk about Rails and static pages, but none did exactly what I needed:
<ol>
	<li>To be able to generate pages with different paths from one URL</li>
	<li>Pages to persist across Rails deployments</li>
</ol>
Not seeing any solutions that fit my needs, I set out to come up with my own.  Here is what I ended up with.

First, I needed to add a route for generating/displaying the reports:

{% codeblock lang:ruby %}
map.reports 'report/:year/:month/:day', :controller => 'report',
    :action => 'show', :year => nil, :month => nil, :day => nil
{% endcodeblock %}

From here, I could just use the standard <strong>caches_page :show</strong> declaration, but that would only generate the page I wanted if I used <em>/report/2009/05/25 </em>as the URL.  What if I wanted <em>/report</em> to generate the report for the current week?  Well, you can do something like this:

{% codeblock lang:ruby %}
class ReportController < ApplicationController
  after_filter :cache_weekly_report, :only => :show
  
  def show
    if params[:year]
      @year  = params[:year]
      @month = params[:month]
      @day   = params[:day]
      if File.exist?("#{Rails.root}/public/report/#{@year}/#{@month}/#{@day}.html")
        redirect_to reports_path(
            :year  => @year,
            :month => @month,
            :day   => @day)
      else
        # render report for a specific day
      end
    else
      today  = Date.today
      @year  = today.year
      @month = today.month
      @day   = today.day
      
      # render report for the current week
    end
  end
  
  protected
  
    def cache_weekly_report
      cache_page(response.body,
            "/report/#{@year}/#{@month}/#{@day}.html") if @year
    end
    
end
{% endcodeblock %}

The magic is in the <strong>after_filter</strong> method <strong>cache_weekly_report</strong>.  We basically use the same mechanism Rails page caching uses to save our new report page.  Now, calling <em>/report</em> will generate a static report at <em>/report/2009/05/25</em>, or whatever the current day is.

The last thing to do is to make sure that the reports persist through new server deployments.  That can easily be done with a symlink in your capistrano script:

{% codeblock lang:ruby %}
task :symlink_reports do
  run "mkdir -p #{shared_path}/report; ln -nfs #{shared_path}/report #{release_path}/public/report"
end
after 'deploy:update_code', 'deploy:symlink_reports'
{% endcodeblock %}

And that's it!  What do you think?  I'd love to know if there are any simpler solutions to this.
