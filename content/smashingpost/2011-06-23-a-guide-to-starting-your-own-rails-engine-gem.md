---
title: 'A Guide To Starting Your Own Rails Engine Gem'
slug: a-guide-to-starting-your-own-rails-engine-gem
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/398a4b65-8195-4789-9f7d-919ed87f6c78/ruby-filled-rvm.jpg
date: 2011-06-23T11:07:25.000Z
author: ryan-cook
summary: >-
  In this article, Ryan Cook walks you through the process of creating an engine gem that you would use to create a database-backed team page displaying a list of employees. This process can be used for any engine gem you feel you need, and it can speed up development time and improve the reliability and maintainability of your code bases.
description: >-
  In this article, Ryan Cook walks you through the process of creating an engine gem that you would use to create a database-backed team page displaying a list of employees.
categories:
  - Coding
  - Ruby on Rails
---

Since Rails 3 was released, developers have been writing Rails engines in a new clean style that can be packaged as RubyGems. A Rails engine is a prepackaged application that is able to be run or mounted within another Rails application. An engine can have its own models, views, controllers, generators and publicly served static files.

Now, unless you like writing a lot of code, this is great news, because it means you can write an engine once and use it over and over again. Let’s say you build a lot of websites for small businesses. A common requirement for such websites is a page listing all of the employees at a company and some basic information about them. This is a great candidate for a Rails engine gem because the functionality will change very little and can be abstracted to a common set of requirements.

In this post, we’ll walk through the process of creating an engine gem that you would use to create a database-backed team page displaying a list of employees.

{{% feature-panel %}}

## Enginex

<a href="https://github.com/josevalim">Jose Valim</a>, a core Rails contributor, has created a tool named <a href="https://github.com/josevalim/enginex">Enginex</a>, which scaffolds Rails 3-compatible engine gems. This tool protects you from many of the gotchas that engine gem developers face. It provides basic set-up, including a test Rails application, which you’ll need to get started.

To begin, run the following from the command line in your standard projects directory:

<pre><code class="language-markup tmp-ruby">gem install enginex
enginex team_page</code></pre>

With this, you will end up with a project in the <code>team_page</code> directory containing the standard Enginex scaffolding.

## Set-Up

To set up our gem, we’ll modify a few files. First, our <code>team_page.gemspec</code> and our <code>Gemfile</code> need a little love.

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: team_page.gemspec
require File.expand_path("../lib/team_page/version", __FILE__)

# Provide a simple gemspec so that you can easily use your
# Enginex project in your Rails apps through Git.
Gem::Specification.new do |s|F
  s.name                      = "team_page"
  s.version                   = TeamPage::VERSION
  s.platform                  = Gem::Platform::RUBY
  s.authors                   = [ "Your Name" ]
  s.email                     = [ "your@email.com" ]
  s.homepage                  = "https://yourwebsite.com"
  s.description               = "A simple Rails 3 engine gem that adds a team page to any Rails 3 application."
  s.summary                   = "team_page-#{s.version}"

  s.rubyforge_project         = "team_page"
  s.required_rubygems_version = "&gt; 1.3.6"

  s.add_dependency "activesupport" , "~&gt; 3.0.7"
  s.add_dependency "rails"         , "~&gt; 3.0.7"

  s.files = `git ls-files`.split("n")
  s.executables = `git ls-files`.split("n").map{|f| f =~ /^bin/(.*)/ ? $1 : nil}.compact
  s.require_path = 'lib'
end</code></pre>

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: Gemfile
source "https://rubygems.org"
# Specify any dependencies in the gemspec
gemspec</code></pre>

This sets up our gemspec to automatically use files we have committed with Git, and any executables we may add in the future, and to use the <code>VERSION</code> constant that we’ll specify in our gem.

Also, by calling <code>gemspec</code> in our <code>Gemfile</code>, running <code>bundle install</code> will load dependencies from our <code>team_page.gemspec</code>, which is the convention.

Next, to turn our gem into a Rails engine, let’s add or modify three files. First, our top-level team page file:

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: lib/team_page.rb
# Requires
require "active_support/dependencies"

module TeamPage

  # Our host application root path
  # We set this when the engine is initialized
  mattr_accessor :app_root

  # Yield self on setup for nice config blocks
  def self.setup
    yield self
  end

end

# Require our engine
require "team_page/engine"</code></pre>

To use the <code>mattr</code> functions, our <code>ActiveSupport</code> dependencies are required. We also set up a nice way to configure our gem with the <code>self.setup</code> method. The engine is required at the end of our file so that we can be sure that any dependencies are specified first.

Secondly, our version file:

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: lib/team_page/version.rb
module TeamPage
  VERSION = "0.0.1"
end</code></pre>

Lastly, our engine file:

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: lib/team_page/engine.rb
module TeamPage

  class Engine &lt; Rails::Engine

    initialize "team_page.load_app_instance_data" do |app|
      TeamPage.setup do |config|
        config.app_root = app.root
      end
    end

    initialize "team_page.load_static_assets" do |app|
      app.middleware.use ::ActionDispatch::Static, "#{root}/public"
    end

  end

end</code></pre>

This defines two Rails <code>initialize</code> blocks that clue us into the root directory of our host Rails application, as well as serve up any files in the root <code>public</code> directory of our gem.

## Data Model

To add a model in our gem, we first need to specify a migration and a generator class to copy it over to the host Rails application. Although this process will become much more transparent in Rails 3.1, we now need to build some generator classes. A great resource for this can be found over at Nepal on Rails.

First, let’s add our generators class:

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: lib/generators/team_page/team_page_generator.rb
# Requires
require 'rails/generators'
require 'rails/generators/migration'

class TeamPageGenerator &lt; Rails::Generators::Base
  include Rails::Generators::Migration
  def self.source_root
    @source_root ||= File.join(File.dirname(__FILE__), 'templates')
  end

  def self.next_migration_number(dirname)
    if ActiveRecord::Base.timestamped_migrations
      Time.new.utc.strftime("%Y%m%d%H%M%S")
    else
      "%.3d" % (current_migration_number(dirname) + 1)
    end
  end

  def create_migration_file
    migration_template 'migration.rb', 'db/migrate/create_team_members_table.rb'
  end
end</code></pre>

Adding this will allow developers to run <code>rails g team_page</code> from within their Rails application and to create the necessary migration file to power our team page.

Next, we’ll put together a sample migration:

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: lib/generators/team_page/templates/migration.rb
class CreateTeamMembers &lt; ActiveRecord::Migration
  def self.up
    create_table :team_members do |t|
      t.string :name
      t.string :twitter_url
      t.string :bio
      t.string :image_url
      t.timestamps
    end
  end

  def self.down
    drop_table :team_members
  end
end</code></pre>

Finally, we can create a sample model namespaced to our gem.

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: app/models/team_page/team_member.rb
module TeamPage
  class TeamMember &lt; ActiveRecord::Base
    attr_accessible :name , :twitter_url , :bio , :image_url
  end
end</code></pre>

What we’ve done so far is walked through the steps for bootstrapping a Rails 3 engine gem. It has been configured as an engine, given its own migration generator, and supplied with an ActiveRecord model.

Now, let’s set up our gem with a route, controller and view that any host Rails application can use.

{{% ad-panel-leaderboard %}}

## The Route

Rails engines gems, when set up properly, automatically load the <code>config</code> and <code>app</code> directories of our project. This is handy because it enables us to set up our code with exactly the same structure as a full Rails application.

So, to set up our route, create a <code>routes.rb</code> file in the <code>config</code> directory of our project. To have it match on the team route, let’s do the following:

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: config/routes.rb
Rails.application.routes.draw do
  get "team" =&gt; "team_page/team#index" , :as =&gt; :team_page
end</code></pre>

A bit of pain can be avoided by examining what we’ve done here. First, we’re going to match the <code>/team</code> route from any requests to our host Rails app.

Secondly, we’ve told Rails to send requests to the <code>index</code> route of the namespaced controller that we’re going to create in our engine. Namespacing our controller is best practice because it isolates our engine code from any application that it’s included in.

Lastly, our route is named so that we can use link helpers elsewhere in our application.

## The Controller

Our controllers will live in the <code>app</code> directory, just as we’re used to. One caveat is that we’ll want to place them in a <code>team_page</code> directory, just as we did with our model. It simply needs to load all of our team members to be displayed on the page.

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: app/controllers/team_page/team_controller.rb
module TeamPage
  class TeamController &lt; ::ApplicationController
    def index
      @team_members = TeamMember.all
    end
  end
end</code></pre>

As you can see, we’ve subclassed our top-level <code>::ApplicationController</code>, which lives in the host Rails application.

## The View

To finish off, we need a view to render. By default, it will use the main application layout from our host Rails application, since we didn’t specify a different layout in the controller.

Just as we did with our model and controller, we’ll nest our view in a <code>team_page</code> directory. Because we want to minimize external dependencies, we’ll write our views in ERB instead of something like HAML.

<pre><code class="language-markup tmp-ruby">&lt;!-- CURRENT FILE :: app/views/team_page/index.html.erb --&gt;
&lt;ul class="team-member-list"&gt;
  &lt;% @team_members.each do |team_member| %&gt;
  &lt;li class="team-member"&gt;
    &lt;span class="team-member-name"&gt;
      &lt;%= link_to @team_member.name , @team_member.twitter_url %&gt;
    &lt;/span&gt;
    &lt;%= @team_member.bio %&gt;
    &lt;%= image_tag @team_member.image_url , :class =&gt; "team-member-image" %&gt;
  &lt;/li&gt;
  &lt;% end %&gt;
&lt;/ul&gt;</code></pre>

## Getting Started With Tests

Obviously, we haven’t yet written any unit or integration tests here to cover the gem that we created. Completing this exercise will improve your understanding of Rails 3 engine gems. The <code>enginex</code> tool we used automatically creates a <code>test</code> directory for you with a basic Rails application.

Let’s start by making sure our <code>test_helper.rb</code> file is up to snuff.

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: test/test_helper.rb
# Configure Rails Environment
ENV["RAILS_ENV"] = "test"
ENV["RAILS_ROOT"] = File.expand_path("../dummy",  __FILE__)

require File.expand_path("../dummy/config/environment.rb",  __FILE__)
require "rails/test_help"

ActionMailer::Base.delivery_method = :test
ActionMailer::Base.perform_deliveries = true
ActionMailer::Base.default_url_options[:host] = "test.com"

Rails.backtrace_cleaner.remove_silencers!

# Run any available migration
ActiveRecord::Migrator.migrate File.expand_path("../dummy/db/migrate/", __FILE__)

# Load support files
Dir["#{File.dirname(__FILE__)}/support/**/*.rb"].each { |f| require f }</code></pre>

One thing to notice, which is unusual for a testing set-up helper, is that we aren’t requiring our local gem code anywhere in the test helper. Because we’re using Bundler, our gem is actually required in the dummy Rails app via our <code>Gemfile</code> at <code>test/dummy/config/application.rb</code>. Other than that, we’re setting up our Rails environment, booting the application and running any available migrations. Here’s a glance at a sample unit test.

<pre><code class="language-markup tmp-ruby"># CURRENT FILE :: test/team_page_test.rb
require 'test_helper'

class TeamPageTest &lt; ActiveSupport::TestCase

  test "truth" do
    assert_kind_of Module, TeamPage
  end

  test 'setup block yields self' do
    TeamPage.setup do |config|
      assert_equal TeamPage, config
    end
  end

end</code></pre>

To continue playing around with how engine testing and integration in a Rails app work, head to the <code>test/dummy/</code> Rails app and boot the server or play in the console. Everything should work in there as well as it would in any other Rails application.

## Resources And Tips

Here are a few helpers to make sure you’re on the right track. The following represents what you would expect the directory structure to look like for your engine gem after following the code examples in this article.

<pre><code class="language-markup tmp-ruby">## DIRECTORY STRUCTURE
#

- team_page/
  - app/
    - controllers/
      - team_page/
        + team_controller.rb
    - models/
      - team_page/
        + team_member.rb
    - views/
      - team_page/
        + index.html.erb
  - config/
    + routes.rb
  - lib/
    - team_page.rb
    - generators/
      - team_page/
        + team_page_generator.rb
        - templates/
          + migration.rb
    - team_page/
      + engine.rb
      + version.rb
  - test/
    + team_page_test.rb
    + test_helper.rb
  + team_page.gemspec
  + Gemfile
  + Gemfile.lock</code></pre>

Here’s a simple script to load some team members into your database.

<pre><code class="language-markup tmp-ruby">## DATA SEED
#
# =&gt; Method 1
# Copy the code into your application's db/seeds.rb file.
#
# =&gt; Method 2
# If you would like to run this code in the engine that you are
# developing, place it in the seeds file inside of the dummy app
# contained in your integration tests.
#
# With either of the above methods, be sure to run the following from
# your command line…
#
#     rake db:seed
#

5.times do |i|

  TeamPage::TeamMember.create!( {
    :name        =&gt; "Team Member #{i}",
    :twitter_url =&gt; "https://twitter.com/team_member_#{i}",
    :bio         =&gt; "A really fancy team member!",
    :image_url   =&gt; "https://bit.ly/muSWki"
  } )

end</code></pre>

### Some External Resources

*   [Rails Engine Source Code](https://github.com/rails/rails/blob/v3.0.8/railties/lib/rails/engine.rb)
*   [RubyGems Guide to Making Your Own Gem](https://guides.rubygems.org/make-your-own-gem/)

### Conclusion

The goal of this post was to demonstrate how straightforward it is to create a Rails engine packaged as a Ruby gem.

To recap, we’ve boostrapped our gem, added a model and migration generator, set up a route to hit our controller, created a sample view, and wrote some example tests. This process can be used for any engine gem you feel you need, and it can speed up development time and improve the reliability and maintainability of your code bases. The possibilities are endless. What will you build?

{{% ad-panel-leaderboard %}}

### Further Reading

*   [How To Get Started With Ruby](https://www.smashingmagazine.com/2012/05/beginners-guide-ruby/)
*   [Get Started Writing iOS Apps With RubyMotion](https://www.smashingmagazine.com/2012/08/get-started-writing-ios-apps-with-rubymotion/)
*   [A Guide To Starting Your Own Rails Engine Gem](https://www.smashingmagazine.com/2011/06/a-guide-to-starting-your-own-rails-engine-gem/)
*   [How To Set Up An Ubuntu Local Machine For Ruby On Rails](https://www.smashingmagazine.com/2011/06/set-up-an-ubuntu-local-development-machine-for-ruby-on-rails/)

{{< signature "al, mrn" >}}
