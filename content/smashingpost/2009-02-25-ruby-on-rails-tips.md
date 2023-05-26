---
title: 10 Useful Tips For Ruby On Rails Developers
slug: ruby-on-rails-tips
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88ae7229-c3fe-47a7-b3dc-7c8e531b67dd/illuquellcode-84x84.gif
date: 2009-02-25T20:21:21.000Z
author: crystal-beasley
description: >-
  Rails is an model-view-controller Web framework written in the Ruby programming language. One of its great appeals is being able to quickly crank out [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)-based Web applications. A big advantage of Rails over other frameworks is that it values [convention over configuration](https://en.wikipedia.org/wiki/Convention_over_Configuration). If you follow the correct conventions, you can avoid lengthy configuration of files, and things just work! Therefore, you spend less time writing boring config files and more time focusing on business logic.
categories:
  - Coding
  - Ruby on Rails
---
<em>By Greg Borenstein and Michael ‘MJFreshyFresh’ Jones</em>

Now, <strong>we love Rails</strong>. But don’t get us wrong. Like any tool, it’s not the perfect solution to every problem. A lot of the biggest complaints people have about the framework come from using it in situations where something simpler, smaller and more lightweight would do just fine. We love <a href="https://sinatra.github.com/">Sinatra</a> for anything with minimal server-side involvement. Merb is another excellent minimal framework. And nothing beats apps that run completely in the browser with JavaScript: they can be deployed nearly for free, can scale almost infinitely and never have to be restarted.

Be sure to check out the following articles:

{{% feature-panel %}}

*   [Getting Started With Ruby On Rails](https://www.smashingmagazine.com/2009/03/getting-started-with-ruby-on-rails/)
*   [Beginner’s Guide To Ruby On Rails: Part 2](https://www.smashingmagazine.com/2009/03/ultimate-beginners-guide-to-ruby-on-rails/)
*   [Successful Freelancing With Ruby On Rails: Workflow, Techniques And Tools](https://www.smashingmagazine.com/2010/10/successful-freelancing-with-ruby-on-rails-workflow-techniques-and-tools/)
*   [Set Up An Ubuntu Local Development Machine For Ruby On Rails](https://www.smashingmagazine.com/2011/06/set-up-an-ubuntu-local-development-machine-for-ruby-on-rails/)

In the overview below we present <strong>10 useful tips, ideas and resources for Ruby on Rails-developers</strong> (both newbies and professionals). Please feel free to share your tips, ideas and suggestions in the comments to this post!

## 1\. Plug-Ins Save Time

Rails has a well defined plug-in structure that enables you to easily install and use plug-ins in your application. David Heinemeier Hansson, the father of Rails, once stated that he uses five to six plug-ins in each Rails application.

There’s an old nugget of developer wisdom that “the best code is no code at all.” Part of what makes us so <strong>productive when developing in Rails</strong> is that all the code that we <em>don’t</em> have to write because someone else in the community has already written a plug-in that provides the functionality we need.

There are a few ways to install a plug-in in Rails, however the most common is using script:

<pre><code class="language-ruby"># Install from a git repo
script/plugin install git://github.com/mislav/will_paginate.git

# Install from a url
script/plugin install https://topfunky.net/svn/plugins/calendar_helper</code></pre>

You can save yourself a ton of time and hassle by becoming good at searching the Web (and especially the almighty GitHub). A couple of places to find plug-ins are Core Rails, Railsify and Rails Plug-in Directory. Need to integrate with an existing API or consume some kind of standard format data? Need tagging, <a href="https://github.com/mislav/will_paginate/tree/master">pagination</a>, or another common Web application feature? Odds are that some great Rails or Ruby developer out there already has a project going that will get you at least most of the way there.</p>

## 2\. Testing is Fun and Easy with Rspec

For most people, the word “test” brings back scary memories of school exams. When working with Rails, however, <strong>automated testing</strong> can make your development experience much more enjoyable. While lots of people have strong, nearly religious, opinions about them, at their core, automated tests are just little helper programs you write that run bits of your main code to make sure they do the right thing. When done right, testing will improve your workflow and increase your confidence in the results.

Rails ships with a test framework baked right in, but for the last couple of years all the cool kids have been using an alternative called <a href="https://rspec.info/">Rspec</a>. Rspec’s biggest advantage is its syntax for specifying tests:

<pre><code class="language-ruby">describe "My Cool library" do before do
    @cool = Cool.new end

  it "should be full of penguins." do
    @cool.get_penguins!
    @cool.penguin_count.should == 10
  end

  it "should melt if it gets too warm"
end</code></pre>

What’s <strong>great about Rspec’s syntax is how much English it uses</strong>. The describe block that sets the context and each assertion within it takes strings that you use to explain what your code should do. Often, this is the most important stage: you sit down to write the assertion, getting as far as you can, and then you think, “Right, what should this code actually do then?”

Because Rspec lets you leave off the block that implements the assertion (as in the second melt example), you can quickly brainstorm all of your functionality, and then go back and implement the tests later as you write the code. In the meantime, Rspec will consider those tests as “pending” and give you little reminders about them in your test runs.

Besides helping you write code in the first place, another great thing about tests is that, once you have enough of them, they let you see how all of your code is related, making it easy to know if your recent change broke anything else in your application. <strong>Rspec makes it easy to get good test coverage</strong> through the use of custom generators that create the tests right along with the rest of your code:

<pre><code class="language-ruby">$ script/generate rpsec_scaffold MyModel</code></pre>

Once you’ve got tests to ensure that the basic functionality works successfully, you can make changes and add new code with confidence without worrying about introducing invisible bugs. As long as you run your tests regularly, you’ll know as soon as you break something. And as GI Joe taught us, knowing is half the battle!

## 3\. Save Time, Use Rake

Projects often include more than just application-specific code. Sample data have to be created, Web services have to be queried, files have to be moved, code snippets rewritten, etc. Resist the urge to shell script or to cram in a migration or controller. Use <a href="https://www.railsenvy.com/2007/6/11/ruby-on-rails-rake-tutorial">Rake</a>. It rocks!

<a href="https://www.railsenvy.com/2007/6/11/ruby-on-rails-rake-tutorial"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/541f859b-8582-4054-921f-3bfa58138c22/rake.gif" alt="Rake" width="480" height="383" /></a>

<a href="https://rake.rubyforge.org/">Rake</a> is a build tool written in Ruby, very similar to <a href="https://www.gnu.org/software/make/">make</a>. Rails projects have several Rake tasks already defined; to see these, run the rake -T command.

<pre><code class="language-ruby">macbook$ rake -T

rake data:bootstrap     # load in some basic data [caution: will nuke and replcace cate...
rake db:create:all      # Create all the local databases defined in config/database.yml
rake db:drop         # Drops the database for the current RAILS_ENV
...
rake ts:run          # Stop if running, then start a Sphinx searchd daemon using Thi...
rake ts:start        # Start a Sphinx searchd daemon using Thinking Sphinx's settings
rake ts:stop         # Stop Sphinx using Thinking Sphinx's settings</code></pre>

Adding your own Rake tasks is quite easy. In the example below, you see that the task is name-spaced and has a description and task name, allowing you to write in Ruby.

<pre><code class="language-ruby">namespace :data do desc "load in some basic data [caution: will nuke and replcace categories, categorizations and inventory items]"
  task :bootstrap =&gt; :environment do
    # clean out existing:
    [Category, Categorization, InventoryItem].each{|m| m.find(:all).each{|i| i.destroy}}
    InventoryItem.create! :name =&gt; "Compass"
    c = Category.create! :name =&gt; "Basic Apparel"

    ["Men’s Heavyweight Cotton T",
    "Men’s Heavyweight Polo",
    "Women’s Organic Cotton Fitted T",
    "Women’s Fitted Polo",
    "Children’s T-Shirt",
    "Jr’s Distressed Hoodie",
    "Hemp Messenger Bag"].each do |name|
      c.inventory_items.create! :name =&gt; name
    end

   ...

end</code></pre>

## 4\. Track Application Exceptions

Exceptions happen, and when they do, you want to know about them! Your client shouldn’t be the one telling you that a problem has occurred; you should already be aware of the issue and working to resolve it. Exception notification has been available in Rails for a while. There are <a href="https://github.com/rails/exception_notification/tree/master">exception notification plug-ins</a> that make it easy to be notified. However, some services such as <a href="https://airbrake.io/">Airbrake Bug Tracker</a> and <a href="https://getexceptional.com/">Get Exceptional</a> add a lot of value to your application.

<a href="https://getexceptional.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1248e658-fa49-4c94-82bc-fa155ffa0449/exc.jpg" alt="Screenshot" width="501" height="403" /></a>

Both of these services are easy to install and provide a great UI for tracking your exceptions. You can even sign up for a free account to try things out.

By <strong>centralizing the application exceptions</strong>, you are able to see how frequently these exceptions occur, what environment they occur in (a particular browser? a particular location?), what parameters were present and the full stack trace. This centralization of data helps you see patterns and resolve the issue more quickly, which results in a better application and happier users.</p>

## 5\. Mix and match between frameworks and servers with Rails on Rack

As of <a href="https://weblog.rubyonrails.org/2009/2/1/rails-2-3-0-rc1-templates-engines-rack-metal-much-more">version 2.3</a>, Rails runs on top of <a href="https://rack.rubyforge.org/">Rack</a>. Rack makes it possible to mix and match between Ruby Web frameworks and servers. If you’re using a framework that supports it (like Rails, Sinatra, Camping, etc), you can choose from any of the servers that do also (Mongrel, <a href="https://code.macournoyer.com/thin/">Thin</a>, <a href="https://www.modrails.com/">Phusion Passenger</a>, etc.), and vice versa.

<a href="https://rack.rubyforge.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc00e8a3-bcb4-4da4-a5c1-1a3ea6ba688b/rack-logo.png" alt="Screenshot" /></a>

In addition to introducing all kinds of new options for deployment, this change means that Rails now has access to the exciting world of Rack middleware. Because Rack lives at the intersection of your app and your server, it can provide all kinds of common functionality directly. A great example of this is Rack::Cache.

Rack::Cache provides a <strong>caching layer</strong> for your application that you control simply by sending the correct headers in your responses. In other words, all you have to do is install a bit of code in the Rack config file:

<pre><code class="language-ruby">require 'rack/cache'

use Rack::Cache,
  :metastore =&gt; 'file:/tmp/rack_meta_dir',
  :entitystore =&gt; 'file:/tmp/rack_body_dir',
  :verbose =&gt; true</code></pre>

And make sure your controller actions send the right headers (for example, by setting <code>request.headers["Cache-Control"]</code>) and Bam!, you’ve got caching.</p>

## 6\. Easy Data Dumping

You’ll often need to get data from production to dev or dev to your local or your local to another developer’s local. One plug-in we use over and over is <a href="https://github.com/adamwiggins/yaml_db/tree/master">Yaml_db</a>. This nifty little plug-in enables you to <strong>dump or load data by issuing a Rake command</strong>. The data is persisted in a yaml file located in db/data.yml. This is very portable and easy to read if you need to examine the data.

<pre><code class="language-ruby">rake db:data:dump

example data found in db/data.yml

---
campaigns:
  columns:
  - id
  - client_id
  - name
  - created_at
  - updated_at
  - token records:
  - - "1"
    - "1"
    - First push
    - 2008-11-03 18:23:53
    - 2008-11-03 18:23:53
    - 3f2523f6a665
  - - "2"
    - "2"
    - First push
    - 2008-11-03 18:26:57
    - 2008-11-03 18:26:57
    - 9ee8bc427d94</code></pre>

## 7\. Keep Your Constants in One Place

All applications have constants, variables that are defined with data that don’t change, such as the name of the application, the tagline, values for crucial options, etc. We use the <strong>Rails initializer feature</strong> to define a <code>config/initializers/site_config.rb </code>for housing these constants. By using this convention, all developers on a project know exactly where to look for the constants and can quickly make changes.

Many people have questions about when to put a constant in the <code>site_config.rb</code> instead of the class it is used in. For a constant that are only used in a single class, we suggest putting it in that class. However, if the constant is used in more than one location, put it in the site_config.rb. For more on constants, have a look at <a href="https://rubylearning.com/satishtalim/ruby_constants.html">Rubylearning</a>.

<pre><code class="language-markup tmp-ruby"># File config/initializers/site_config.rb

REPORT_RECIPIENT = 'jenn@scg.com'
REPORT_ADMIN = 'michael@scg.com'</code></pre>

## 8\. Console for Working on Code

Sometimes you may have code that you’re curious about. Will it work this way? What’s the output? What can I change? Rails ships with a wonderful tool called console. By running script/console you will enter an <strong>interactive environment where you can access your Rails code</strong> just as though the application were running.

This environment is incredibly helpful. It is often used in production environments at times to quickly peek at data without having to log in to the database. To do this in a production environment, use script/console RAILS_ENV=production:

<pre><code class="language-markup tmp-ruby">macbook$ ./script/console
Loading development environment (Rails 2.1.1)
&gt;&gt; a = Album.find(:first)
=&gt; #
&gt;&gt;</code></pre>

## 9\. Ugly Views Getting You Down? Try Haml.

Views are how your Rails application generates the HTML pages your visitors actually see and use. By default, Rails uses the <a href="https://www.ruby-doc.org/stdlib/libdoc/erb/rdoc/classes/ERB.html">ERb templating system</a> to let you embed bits of Ruby in your markup so that you can insert your data as needed. However, recent versions of Rails let you take your pick of templating languages, and nowadays the Ruby interwebs have been all abuzz about an alternative system called <a href="https://haml.hamptoncatlin.com/">Haml</a>.

<a href="https://haml.hamptoncatlin.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72cadf27-1f73-4de1-9c7d-e25a4dd6c615/haml.gif" alt="HAML" width="480" height="399" /></a>

Haml is marketed as “markup Haiku.” Its <strong>CSS-inspired syntax lets you focus on the semantics of your data</strong> rather than worrying about closing all the angle brackets that come with using ERb and HTML.

For comparison, here’s a bit of markup in standard ERb:

<pre><code class="language-markup tmp-ruby">&lt;%= print_date %&gt;
&lt;%= current_user.address %&gt;

&lt;%= current_user.email %&gt;
&lt;%= h current_user.bio %&gt;</code></pre>

And here’s the equivalent in Haml:

<pre><code class="language-markup tmp-ruby">#profile
  .left.column
    #date= print_date
    #address= current_user.address
  .right_column
    #email= current_user.email
    #bio= h(current_user.bio)</code></pre>

Haml’s not for everyone, and many people will find this syntax quite alien. But if you value concision and are fluent in CSS, Haml may be just the ticket.</p>

## 10\. Know Where to Watch What’s Happening in Rails

Rails and Ruby both have <strong>large and active communities</strong> that constantly generate changes, improvements and new projects. Trying to keep up with all the activity can be daunting, but it’s essential if you want to benefit from the community’s best work and continue to increase your Rails and Ruby knowledge.

Thankfully, a number of sources aggregate some of the most important activity:

*   GitHub has a most-watched projects page, which is a great place to start.
*   Similarly, RubyInside’s monthly [What’s Hot on Github](https://www.rubyinside.com/whats-hot-on-github-january-2009-1450.html) and
*   [the GitHub blog’s Rebase series](https://github.com/blog/310-github-rebase-11) both feature selections of interesting work from the website.

There’s also a whole universe of Rails training:

*   [Rails Envy](https://www.railsenvy.com/)
*   PeepCode

and news aggregators:

*   follow [ruby_news](https://twitter.com/ruby_news) on Twitter,
*   subscribe to [Ruby Inside](https://www.rubyinside.com/),
*   subscribe to [Ruby Flow](https://rubyflow.com/).

Another avenue is the <a href="https://groups.google.com/group/rubyonrails-core">Rails Core mailing list</a> and the #rails-core IRC channel.</p>

### About the authors

This guest post was written by Greg Borenstein and Michael ‘MJFreshyFresh’ Jones, lead Ruby developers for StepChange Group. StepChange designs, develops and manages social media widgets and Facebook applications in partnership with leading brands and agencies. Outside of work, Greg builds <a href="https://www.urbanhonking.com/ideasfordozens/2009/02/rad_talk_roundup.html">drum-playing robots</a> and other hardware hacks, and MJ leads a local group of <a href="https://www.unicyclebastards.com/">Unicycle-borne pirates</a>. They live and work in beautiful, moist Portland, Oregon.

{{< signature "al" >}}

