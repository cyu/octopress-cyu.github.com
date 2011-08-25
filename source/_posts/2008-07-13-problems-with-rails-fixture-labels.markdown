--- 
wordpress_id: 145
layout: post
title: Problems With Rails Fixture Labels?
wordpress_url: http://dontforgettoplantit.wordpress.com/?p=149
permalink: /2008/07/13/problems-with-rails-fixture-labels.html
---
Newer versions of Rails has a nice feature where you can use label references for fixtures.  So instead of:
{% codeblock lang:yaml %}
# posts.yml
test_post:
  user_id: 1
  title: My Test Post
{% endcodeblock %}

You can do this:
{% codeblock lang:yaml %}
test_post:
  user: quentin
  title: My Test Post
{% endcodeblock %}

However, if your model class name is in a pluralized form, you might find that label references won't work.  That's because fixtures derive their class name from the singular form of the table name by default.  Fortunately, you can fix this by adding this line to your TestHelper:
{% codeblock lang:ruby %}
class Test::Unit::TestCase

  # Explicitly map the table name to class name
  set_fixture_class :accounts => 'accounts'
end
{% endcodeblock %}

Hopefully, this will save someone else from having to dig through the Rails fixtures internals.
