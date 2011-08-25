--- 
wordpress_id: 80
layout: post
title: "Taming Beast: How to Extend Beast using Plugins"
wordpress_url: http://blog.codeeg.com/2007/09/04/taming-beast-how-to-extend-beast-using-plugins/
permalink: /2007/09/04/taming-beast-how-to-extend-beast-using-plugins.html
---
If you're building a Ruby on Rails application and are in need of some forums functionality, you've most likely have looked into Beast.  However, Beast is very limited in functionality (which I actually think is a good thing), so you might find yourself needing to extend Beast to do the things you want.

Fortunately, Beast has a plugin feature that will easily allow you to do this.  In this post, I'll cover how you would do this, using my StyleEditor plugin as an example.
<h2>The Plugin File Structure</h2>
First, let's cover plugin file structure.  This is what my StyleEditor plugin looks like:

<img class="alignnone size-full wp-image-112" src="/images/wp/beast_plugin_dir_structure.png" alt="" width="162" height="223" />

Here are the important points to note:
<ul>
	<li><strong>app:</strong> The directory structure of this directory should follow the same conventions as the main Rails <em>app/</em> directory.  Code located in this directory follow the same class loading (and reloading) rules as the main <em>app/</em> directory.</li>
	<li><strong>lib/beast/plugins/style_editor.rb:</strong> This is the plugin class, where all the magic happens.  The name of the file should be the tableized version of the plugin's actual class name.  The plugin class file <strong>must</strong> be located in <em>beast/plugins</em>, or else Rails will not be able to find it.</li>
</ul>
<h2>The Plugin Class</h2>
Here's what's the plugin class should look like:

{% codeblock lang:ruby %}
module Beast
  module Plugins
    class StyleEditor < Beast::Plugin
      author 'Calvin Yu - boardista.com'
      version '0001'
      homepage 'http://boardista.com'
      notes 'Style Editing Support'

      %w( controllers helpers models ).each do |dir|
        path = File.join(plugin_path, 'app', dir)
        Dependencies.load_paths &lt;&lt; File.expand_path(path) if File.exist?(path)
      end

      def initialize
        super
        ApplicationController.prepend_view_path File.join(StyleEditor::plugin_path, 'app', 'views')
        # Patch Beast code here.
      end

      def install
        super
        # Run any install processes here.
      end
    end # end StyleEditor class
  end # end Plugins module
end # end Beast module
{% endcodeblock %}

You can see what <a href="http://svn.codeeg.com/beast/style_editor/lib/beast/plugins/style_editor.rb">the final source looks like here</a>.  Here are some things to note about this class:
<ul>
	<li>The <em>author</em>, <em>version</em>, <em>homepage</em>, and <em>notes</em> methods provide some meta information for the plugin.</li>
	<li>The <em>Dependencies.load_paths</em> call will configure the sub-directories under <em>app/</em> so that they'll be dynamically loaded by Rail's dependency resolution process.</li>
	<li>The <em>ApplicationController.prepend_view_path</em> call will prepend this plugin's view path ahead of the normal Rails view path <strong>and any other view paths configured by other plugins loaded before it</strong>.  This is important to remember if views aren't being rendered like you're expecting them to.</li>
	<li>Any changes to existing Rails or Beast controllers, models, etc. should go into <em>initialize</em>, in the form of monkey patches and mixins.</li>
	<li>Any installation tasks, such as file copy, should go into the <em>install</em> method.</li>
</ul>
<h2>Adding New Routes</h2>
I needed to create some new routes for my <em>StylesController</em>, so I used the <em>route</em> method of the <em>Beast::Plugin</em> class to install them:

{% codeblock lang:ruby %}
# add this within the class scope of the StyleEditor
route :resources, 'styles'
{% endcodeblock %}

I'm using the RESTful syntax to creating routes here, but you can also use <em>:connect</em> and named routes as well.
<h2>Updating the Beast Schema</h2>
To update the Beast Schema, all I needed to do is to create a Schema class within the scope of your plugin class:

{% codeblock lang:ruby %}
class Schema < ActiveRecord::Migration
  def self.install
    create_table :style_options do |t|
      t.string :name
      t.string :value
      t.integer :style_id
    end

    create_table :styles do |t|
      t.string :name
      t.string :template_name
      t.boolean :active
      t.timestamps
    end
  end

  def self.uninstall
    drop_table :styles
    drop_table :style_options
  end
end # end Schema class
{% endcodeblock %}

The code in <em>install/uninstall</em> methods will work just like the <em>up/down</em> methods in a typical migration class.  There is an issue where there's no support for handling db changes overtime -- hopefully someone will find a nice way to handle this (any takers?).
<h2>Using the Rails Console</h2>
At some point, you'll want to do some quick tests to make sure your plugin changes are working as you expect them to, and try to test them from the console.  If you have tried to this already, you'll quickly find that your changes for some reason won't work.  Don't fret, the reason why it doesn't work is because the plugins aren't initialize until the <em>Dispatcher</em> receives its first request.  So, if you do want to test your changes in the console, you'll need to run this command first:
{% codeblock lang:ruby %}
Dispatcher.send :prepare_application
{% endcodeblock %}
<h2>Installing a Plugin</h2>
Once you're done with your plugin, you'll need to install it.  This step is pretty easy.  First, install your beast plugins into <em>vendor/beast</em>, then run the plugin install method:

{% codeblock lang:bash %}
script/runner 'Beast::Plugins::StyleEditor.install'
{% endcodeblock %}

Some plugins might have some additional installation instructions, so I would suggest looking at the <em>README</em> file (and if you're developing on a plugin, make sure to put your install instructions in the README).
<h2>That's It!</h2>
It's important to note that Beast plugin system is an evolving system, and the steps I laid out here are what worked best for me through the process of trial an error.  I'd love to hear what conclusions others have come to in their plugin development exploits.  If you want to get a better feel of what an actual Beast plugin looks like, you can check out the plugins that I've developed at <a href="http://svn.codeeg.com/beast">http://svn.codeeg.com/beast</a>.  If you want to see what those plugins look like in action, you can check them out on <a href="http://boardista.com">Boardista.com</a>.
