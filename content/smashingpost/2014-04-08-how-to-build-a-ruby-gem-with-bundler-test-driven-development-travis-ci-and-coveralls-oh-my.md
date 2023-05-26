---
title: >-
  How To Build A Ruby Gem With Bundler, Test-Driven Development, Travis CI And
  Coveralls, Oh My!
slug: >-
  how-to-build-a-ruby-gem-with-bundler-test-driven-development-travis-ci-and-coveralls-oh-my
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10ab46c-a52e-4532-adc6-2bc2071148d4/ruby-on-rails-illu.jpg
date: 2014-04-08T08:34:16.000Z
author: mark-mcdonnell
description: >-
  Ruby is a great language. It was designed to foster happiness and productivity in developers, all the while providing tools that are effective and yet focused on simplicity. 
categories:
  - Coding
  - Tools
  - Techniques
  - Ruby on Rails
---
One of the tools available to the Rubyist is the <a href="https://rubygems.org/">RubyGems</a> package manager. It enables us both to include “gems” (i.e. packaged code) that we can reuse in our own applications and to package our own code as a gem to share with the <a href="https://www.ruby-lang.org/">Ruby</a> community. We’ll be focusing on the latter in this article.

I’ve written an open-source gem named <a href="https://rubygems.org/gems/sinderella">Sinderella</a> (<a href="https://github.com/Integralist/Sinderella">available on GitHub</a>), and in this article I’ll go through all of the steps I took to write the code (including the <a href="https://en.wikipedia.org/wiki/Test_driven_development">test-driven development</a> process) and how I prepared it for release as a gem via RubyGems. I’ll also show you how to set up your tests to run through a <a href="https://en.wikipedia.org/wiki/Continuous_integration">continuous integration</a> (CI) server using the popular <a href="https://travis-ci.org/">Travis CI</a> service.</p>

Recommened reading: [How To Get Started With Ruby](https://www.smashingmagazine.com/2012/05/beginners-guide-ruby/)

In case you’re unfamiliar with CI, it refers to the process of merging code with a central repository, with the aim of preventing integration problems down the road in a project’s life cycle. (If you use a version control system such as <a href="https://git-scm.com/">git</a> and a decentralized code repository such as <a href="https://github.com/">GitHub</a>, then you might already be familiar with these concepts.)

{{% feature-panel %}}

Finally, I’ll show you how to use <a href="https://coveralls.io/">Coveralls</a> to measure the code coverage of your tests and to obtain a statistical history of your commits.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed70bb0b-6734-46b5-9915-ed7789ba22cf/ruby-bundler-travis-ci-opt.png" width="500" height="263" /><br>
<em>Image credits: The <a href="https://www.ruby-lang.org/en/">Ruby</a> and <a href="https://bundler.io/">Bundler</a> logos, along with the <a href="https://travis-ci.org/">Travis CI</a> mascot.</em>

### What We’ll Cover

*   [What does Sinderella do?](#a1)
*   [What we won’t cover](#a2)
*   [Additional requirements](#a3)
*   [Which version of Ruby to use](#a4)
*   [Bundler](#a5)
*   [Dependencies](#a6)
*   [Generating a boilerplate](#a7)
*   [Test-driven development](#a8)
*   [RSpec](#a9)
*   [Guard and tmux](#a10)
*   [Continuous integration with Travis CI](#a11)
*   [Code coverage and statistics with Coveralls.io](#a12)
*   [Skeleton specification](#a13)
*   [Design patterns](#a14)
*   [Badges](#a15)
*   [REPL-driven development](#a16)
*   [Releasing your gem](#a17)
*   [Conclusion](#a18)

## [](#)What Does Sinderella Do?

As described in the README on GitHub, Sinderella allows the author to “pass a code block to transform a data object for a specific period of time.” So, if we provide data like the following…

<pre><code class="language-ruby">
{ :key =&gt; 'value' }
</code></pre>

… then we could, for example, convert it to the following for a set period of time:

<pre><code class="language-ruby">
{ :key =&gt; 'VALUE' }
</code></pre>

Once the time period has expired, the data is returned to its normal state.

Sinderella is made up of two files: the main application and a data store that holds the original and transformed data.

Later in this article, I’ll describe my development process for creating the gem, and we’ll review some of the techniques required to produce a robust and stable gem.</p>

## [](#)What We Won’t Cover

To be clear, this article is focused on creating a Ruby gem using Bundler and on following best practices, such as test-driven development and CI.

We won’t cover how to write Ruby code or how we developed the Sinderella gem. Nor will we cover how to write RSpec tests (although we will demonstrate how to set up RSpec). RSpec is a detail of implementation and can be swapped out for any testing library that you deem appropriate.</p>

## [](#)Additional Requirements

To get started, you’ll need to register for accounts with the following services:

*   [Travis CI](https://travis-ci.org/)
*   [RubyGems](https://rubygems.org/)
*   [Coveralls](https://coveralls.io/)

Registering for these services is free. Travis CI is free for all open-source projects (which this will be). You may pay for a Pro account, which allows you to set up CI for your private code repositories, but that’s not needed for what we’ll be doing here.

You’ll also need to be comfortable working in the command line. You don’t have to be a Unix shell scripting wizard, but I’ll be working here exclusively in a shell environment (specifically, using the Terminal on Mac OS X) to do everything, including running shell commands, opening multiplexers (such as <a href="https://en.wikipedia.org/wiki/Tmux">tmux</a>) and editing code (with Vim).</p>

## [](#)Which Version Of Ruby To Use

Ruby has many different flavors:

*   [Ruby](https://ruby-lang.org/) (also known as Matz’s Ruby Interpreter) is the original language, written in C.
*   [Rubinius](https://rubini.us/) is an implementation of Ruby that is written mainly with Ruby.
*   [JRuby](https://jruby.org/) is an implementation of Ruby built on top of the Java Virtual Machine (JVM), with Java.

I deliberately used JRuby to implement Sinderella because part of the gem’s code relies on “<a href="https://en.wikipedia.org/wiki/Multi-threaded">threads</a>,” and MRI doesn’t provide true threading.

JRuby provides a native thread implementation because it is built on top of the JVM. But really, using any of the above variations would have been fine.

Unfortunately, though, it’s not all clear sailing with JRuby. Quite a few gems still use C extensions (i.e. code written in C that Ruby can import). At the moment, you can enable a flag in JRuby that allows it to use C extensions, but doing so is merely a temporary solution because this option is expected to be removed from JRuby in future releases.

This could be an issue, for example, if you’re using <a href="https://pryrepl.org/">Pry</a> (a replacement for Ruby’s <code>irb</code> REPL). Pry works fine with JRuby, but you wouldn’t be able to take advantage of the equally amazing <a href="https://rubygems.org/gems/pry-plus">pry-plus</a> extension, which offers many extra debugging capabilities, because some of its dependencies rely on C extensions.

I’ve worked around this limitation somewhat by using <a href="https://github.com/nixme/pry-nav">pry-nav</a>. It’s not as good and can be a little buggy in places when used under JRuby, but it gets the job done.

## [](#)Bundler

To help us create the gem, we’ll use the popular <a href="https://bundler.io/">Bundler</a> gem.

Bundler is primarily designed to help you manage a project’s dependencies. If you’ve not used it before, then don’t worry because we’ll be taking advantage of a lesser known feature anyway, which is its ability to generate a gem boilerplate. (It also provides some other tools that will help us manage our gem’s packaging, which I’ll get into in more detail later on.)

Let’s begin by installing Bundler:

<pre><code class="language-shell">
gem install bundler
</code></pre>

Once Bundler is installed, we can use it to create our gem. But before doing that, let’s review some other dependencies that we’ll need.</p>

## [](#)Dependencies

Developing the Sinderella gem requires five dependencies. Four are needed during the development process and won’t be needed in production. The fifth is a “hard” dependency, meaning that it is needed for the Sinderella gem to function properly.

*   [RubyGems](https://rubygems.org/)
*   [RSpec](https://rspec.info/)
*   [Guard](https://guardgem.org/)
*   [Pry](https://pryrepl.org/)
*   [Crimp](https://rubygems.org/gems/crimp)

Of these dependencies, Crimp and RSpec are specific to Sinderella. So, when developing your own gem, you would likely replace them with other gems.</p>

### RubyGems

We need to <a href="https://rubygems.org/pages/download">install RubyGems</a> in order to take advantage of the package manager and its built-in <code>gem</code> commands (which Bundler will wrap with its own enhancements).</p>

### RSpec

RSpec is a testing framework for the Ruby programming language. We’ll cover this in more detail later on in the article.

When building your own gem, you might want to swap RSpec for a different testing tool. Another popular option is <a href="https://cukes.info/">Cucumber</a>.</p>

### Guard

Guard is a command-line tool that responds to events. We’ll be using it to more easily write code for test-driven development. It works by monitoring files that you tell it to watch and then, when it notices changes to those files, triggering some command that you specify based on the type of file that was changed.

This comes in really handy when you’re running tests in a multiplexer such as <span class="removed_link" title="https://tmux.sourceforge.net/">tmux</span> or when using a terminal such as <a href="https://www.iterm2.com/">iTerm2</a> (which supports multiple terminal windows being open at once), because while you’re editing the code in one terminal, you can get instant feedback to breaking tests as you work on the code. This is known as a tight feedback loop (more on this later).</p>

### Pry

Pry is a replacement REPL for Ruby’s standard <code>irb</code>. It offers everything the standard <code>irb</code> does but with a lot of additional features. It’s useful for testing code to see how it works and whether the Ruby interpreter fails to run it. It’s also useful for debugging code when something doesn’t work the way you expect.

It didn’t have much of a presence in the development of Sinderella, but it is such an important tool that I felt it deserved more than a cursory mention. For example, if you’re unsure of how a particular Ruby feature works, you could test drive it in Pry.

If you want to learn more about how to use it, then watch the <a href="https://pryrepl.org/">screencast on Pry’s home page</a>.</p>

### Crimp

Crimp is a gem released by the BBC that allows you to convert a piece of data into a MD5 hash.</p>

## [](#)Generating A Boilerplate

OK, now we’ve finally gotten to the point where we can generate the set-up files that will configure our gem file.

As mentioned, Bundler has the tools to generate the foundation of a gem so that we don’t have to type it all out by hand.

Now, open up the terminal and run the following command:

<pre><code class="language-shell">
bundle gem sinderella
</code></pre>

When that command is run, the following is generated:

<pre><code class="language-shell">
❯ bundle gem sinderella
  create  sinderella/Gemfile
  create  sinderella/Rakefile
  create  sinderella/LICENSE.txt
  create  sinderella/README.md
  create  sinderella/.gitignore
  create  sinderella/sinderella.gemspec
  create  sinderella/lib/sinderella.rb
  create  sinderella/lib/sinderella/version.rb
Initializing git repo in /path/to/Sinderella
</code></pre>

Let’s take a moment to review what we have.</p>

### Folder Structure

Bundler has automatically created a <code>lib</code> directory for us, which holds a single Ruby file named after our project. The name of the directory is extracted from the name provided via the <code>bundle gem</code> command.

Be aware that if you specify a hyphen (<code>-</code>) in the gem’s name, then Bundler will create a deeper folder structure by using the hyphen as a delimiter. For example, if your command looks like <code>bundle gem foo-bar</code>, then the following directory structure would be created:

<pre><code class="language-shell">
├── lib
│   └── foo
│       ├── bar
│       │   ├── bar.rb
│       │   └── version.rb
│       └── bar.rb
</code></pre>

This is actually quite useful when you’re producing multiple gems that are all namespaced under a single project. For a real-world example of this, look at <a title="alephant" href="https://github.com/BBC-News/">BBC News’ GitHub repository</a>, which has multiple open-source gems published under the namespace <code>alephant</code>.</p>

### gemspec

The <code>gemspec</code> file is used to define the particular configuration of your gem. If you weren’t using Bundler, then you would need to manually create this file (according to RubyGems’ documentation).

Below is what Bundler generates for us:

<pre><code class="language-ruby">
# coding: utf-8
lib = File.expand_path('../lib', __FILE__)
$LOAD_PATH.unshift(lib) unless $LOAD_PATH.include?(lib)
require 'sinderella/version'

Gem::Specification.new do |spec|
  spec.name          = "sinderella"
  spec.version       = Sinderella::VERSION
  spec.authors       = ["Integralist"]
  spec.email         = ["mark.mcdx@gmail.com"]
  spec.summary       = %q{TODO: Write a short summary. Required.}
  spec.description   = %q{TODO: Write a longer description. Optional.}
  spec.homepage      = ""
  spec.license       = "MIT"

  spec.files         = `git ls-files -z`.split("x0")
  spec.executables   = spec.files.grep(%r{^bin/}) { |f| File.basename(f) }
  spec.test_files    = spec.files.grep(%r{^(test|spec|features)/})
  spec.require_paths = ["lib"]

  spec.add_development_dependency "bundler", "~&gt; 1.5"
  spec.add_development_dependency "rake"
end
</code></pre>

As you’ll see later, this is a basic outline of the final gemspec file that we’ll need to create. We’ll end up adding to this file some of the other dependencies that our gem will need to run (both development and production dependencies).

For now, note the following details:

*   `$LOAD_PATH.unshift(lib) unless $LOAD_PATH.include?(lib)` This adds the `lib` directory to Ruby’s load path, which makes `require`’ing files elsewhere in the code a little cleaner.
*   `require 'sinderella/version'` This loads in a `version.rb` file, which was generated when Bundler constructed our boilerplate. This file serves as a way to implement [semantic versioning](https://semver.org/) in our gem releases. Every time we release the gem, we’ll need to update the version number; then, when we run the particular Bundler command to release the gem, it will automatically pull in the updated value to our `gemspec` file.
*   `Gem::Specification.new do |spec|` Here, we define a new specification and include properties such as the name of the gem, the version number (see the previous point), a list of the authors of the gem and a contact email address. We can also include some descriptive text about the gem.
*   Next, we define the files to include in the gem. Any executable files found are injected dynamically into the file by looping through a `bin` directory (if one is found). We also dynamically inject a list of test files (which we’ll see later on when we create a `spec` folder to hold the tests that will ensure that the gem works as expected).
*   Finally, we define the dependencies, including both runtime and development dependencies. At the moment, there is only the latter, but soon enough we’ll have one runtime dependency to add.

The RubyGems guides has <a href="https://guides.rubygems.org/specification-reference/">full details on the specification</a>. You could configure a whole host of settings, but Bundler helps us by defining the essential ones.</p>

### Gemfile

In a typical Ruby project, you’ll find that the <code>Gemfile</code> is filled with a list of dependencies, which Bundler then collates and installs for you. In this instance, because we’re generating a gem and not writing a standard application, our <code>Gemfile</code> will actually be pretty bare, made up of two lines: one to tell Bundler where to source the gems from, and the other to inform Bundler that the dependencies are listed in the <code>gemspec</code> file instead.</p>

### Rakefile

Again, in a typical Ruby application, a <code>Rakefile</code> will contain many different tasks (written in Ruby) that you can execute via the command line. In this case, a one-line <code>Rakefile</code> has been provided that loads <code>bundler/gem_tasks</code>. That in turn loads additional <code>rake</code> commands that Bundler adds to make it easier to build and deploy your gem. We’ll see how to use these commands later.</p>

### LICENSE.txt

Because we’re releasing code that could potentially be used by other developers, Bundler generates an MIT licence by default and dynamically injects the current year and your user name into it.

Feel free to either delete it or replace it with another license if the MIT one doesn’t fit your needs, although it’s pretty standard and relevant to most projects.</p>

### README

Lastly, Bundler has taken the tediousness out of generating a <code>README</code> file. It includes <code>TODO</code> messages wherever relevant, so that you know what needs to be manually added before the gem can be built (such as a description of the gem and a code example that shows how you expect the gem to be used). It also automatically generates installation instructions and a section on how other developers can fork your code and contribute new features and bug fixes.

One other benefit of Bundler is that it delivers a consistent code base across all gems you create. All gems will have the same structure, and the consistency across content such as the README file will make it easier for users who integrate more than one of your gems to understand them.</p>

## [](#)Test-Driven Development

Test-driven development (TDD) is the process of building code on top of supporting tests. Sinderella was developed using its principles.

The guiding steps are “red, green, refactor,” and TDD fundamentally breaks down as the following:

1.  Write a test.
2.  Run the test and watch it fail (because there is no code yet for it to pass).
3.  Write the least amount of code to pass the test (literally, hack it together).
4.  Refactor the code so that it’s cleaner and better written.
5.  If the test has failed through refactoring, then start the red, green, refactoring process again.

This is sometimes referred to as a tight feedback loop: getting quick or instant feedback on whether code is working.

By writing the tests first, you ensure that every line of code exists for a reason. This is an incredibly powerful principle and one you should recall when caught in a debate over whether TDD “sucks” or “takes too long.”

Starting a project with tests can feel daunting. But in addition to ensuring that every line of code exists for a reason, it provides an opportunity for you to properly design the APIs.</p>

## [](#)RSpec

As for writing tests for Sinderella, I chose to use <a href="https://rspec.info/">RSpec</a>, which is described thus on its website:
<blockquote>RSpec is a testing tool for the Ruby programming language. Born under the banner of behaviour-driven development, it is designed to make test-driven development a productive and enjoyable experience</blockquote>

In order to use RSpec in our gem, we’ll need to update the <code>gemspec</code> file to include more dependencies:

<pre><code class="language-ruby">
spec.add_development_dependency "rspec"
spec.add_development_dependency "rspec-nc"
spec.add_development_dependency "guard"
spec.add_development_dependency "guard-rspec"
spec.add_development_dependency "pry"
spec.add_development_dependency "pry-remote"
spec.add_development_dependency "pry-nav"
</code></pre>

As you can see, we’ve added RSpec to our list of dependencies, but we’ve also included <a href="https://github.com/twe4ked/rspec-nc">rspec-nc</a>, which provides native notifications on Mac OS X (rspec-nc is a nicety and not essential to produce the gem). Having notifications at the operating-system level can be quite handy, allowing you to do other things (perhaps check email) while tests run in the background.

We’ve also added (as you would expect) <code>guard</code> as a dependency, as well as <code>guard-rspec</code>, which Guard will need in order to understand how to handle RSpec-specific requests. This suite of Pry tools will debug any problems we come across and will be useful for any gems you develop in future.</p>

### RSpec Rake Tasks

Now that we’ve updated <code>gemspec</code> to include RSpec as a dependency, we’ll need to add an RSpec-related Rake task to our <code>Rakefile</code>, which will enable us (manually) or Guard to execute the task and run the RSpec test suite:

<pre><code class="language-ruby">
require 'rspec/core/rake_task'
require 'bundler/gem_tasks'

# Default directory to look in is `/specs`
# Run with `rake spec`
RSpec::Core::RakeTask.new(:spec) do |task|
  task.rspec_opts = ['--color', '--format', 'nested']
end

task :default =&gt; :spec
</code></pre>

In the updated version of <code>Rakefile</code> above, we are loading an additional file that is packaged with RSpec (<code>require 'rspec/core/rake_task'</code>). This new file adds some RSpec-related modules and classes for us to use.

Once this code has loaded, we create a new instance of the <code>RakeTask</code> class (created when we loaded <code>rspec/core/rake_task</code>) and pass it a code block to execute. The code block we pass will define the options for our RSpec test suite.</p>

### Spec Files

Now that the majority of the RSpec test suite configuration is in place, the last thing we need to do is add a test file.

Let’s create a <code>spec</code> directory and, inside that, create <code>sinderella_spec.rb</code>:

<pre><code class="language-ruby">
require 'spec_helper'

describe Sinderella do
  it 'does stuff' do
    pending # no code yet
  end
end
</code></pre>

You’ll see that we’ve included a temporary specification that states that the code “does stuff.” When the test suite is run, then this test will not cause any errors, even though no code has been implemented yet, because we have marked the test as “pending” (an RSpec-specific command). At this point, we’re only interested in getting a barebones set-up in place; we’ll flesh out the tests soon enough.

You may have noticed that we’re also loading another file, named <code>spec_helper.rb</code>. This type of file is typical in an RSpec suite and is used to load any dependencies or libraries that are required for the tests to run. The content of the spec helper file will look like this:

<pre><code class="language-ruby">
require 'pry'
require 'Sinderella'
</code></pre>

All we’ve done here is load Pry (in case we need it for debugging) and the main Sinderella gem code (because this is what we want to test).</p>

## [](#)Guard And tmux

At this point, we’ve gone over the set-up and preparation of RSpec and Rake (to get our testing framework in place). We also know what Guard is and how it helps us to test the code. Now, let’s go ahead and add a <code>Guardfile</code> to the root directory, with the following contents:

<pre><code class="language-ruby">
guard 'rspec' do
  # watch /lib/ files
  watch(%r{^lib/(.+).rb$}) do |m|
    "spec/#{m[1]}_spec.rb"
  end

  # watch /spec/ files
  watch(%r{^spec/(.+).rb$}) do |m|
    "spec/#{m[1]}.rb"
  end
end
</code></pre>

This file tells Guard that we’re using RSpec to run our tests. It also defines which directories to watch for changes and what to do when it notices changes. In this case, we’re using <a href="https://www.regular-expressions.info/">regular expressions</a> to match any files in the <code>lib</code> or <code>spec</code> directory and to execute the relevant RSpec command that runs our tests (or to run one specific test).

We’ll see in a minute how to actually run Guard. For now, let’s see how tmux fits this workflow.</p>

### tmux

Some developers prefer to have separate applications open (for example, a code editor such as <a href="https://www.sublimetext.com/">Sublime Text</a> and a terminal application to run tests). I prefer to use tmux to have multiple terminal shells open on one screen and to have Vim open on another screen to edit code. Thus, I can edit code and get visual feedback from the terminal about the state of the tests all on one screen. You don’t need to follow the exact same approach. As mentioned, there are other ways to get feedback, but I have found tmux and Vim to be the most suitable.

So, we have two tmux panes open, one in which Vim is running, and the other in which a terminal runs the command <code>bundle exec guard</code> (this is how we actually run Guard).

That command will return something like the following back to the terminal:

<pre><code class="language-shell">
❯ bundle exec guard
09:53:55 - INFO - Guard is using Tmux to send notifications.
09:53:55 - INFO - Guard is using TerminalTitle to send notifications.
09:53:55 - INFO - Guard::RSpec is running
09:53:55 - INFO - Guard is now watching at '/path/to/Sinderella' 

From: /path/to/Sinderella/sinderella.gemspec @ line 1 :

 =&gt; 1: # coding: utf-8
    2: lib = File.expand_path('../lib', __FILE__)
    3: $LOAD_PATH.unshift(lib) unless $LOAD_PATH.include?(lib)
    4: require 'sinderella/version'
    5: 
    6: Gem::Specification.new do |spec|
</code></pre>

From this point on, you can press the <code>Return</code> key to run all tests at once, which will display the following message in the terminal:

<pre><code class="language-shell">
09:57:41 - INFO - Run all
09:57:41 - INFO - Running all specs
</code></pre>

This will be followed by the number of passed and failed tests and any errors that have occurred.</p>

## [](#)Continuous Integration With Travis CI

As mentioned at the beginning, continuous integration (CI) is the process of merging code with a central repository in order to prevent integration problems down the road in a project’s life cycle.

We’ll use the free Travis CI service (which you should have signed up for by now).

Upon first viewing your “<a href="https://travis-ci.org/profile">Accounts</a>” page in Travis CI, you’ll be presented with a complete list of all of your public GitHub repositories, from which you can select ones for Travis CI to monitor. Then, any time you push a commit to GitHub, Travis CI will run your tests.

Once you have selected repositories, you’ll be redirected to a GitHub “hooks” page, where you can confirm and authorize the configuration.

The <a href="https://travis-ci.org/Integralist/Sinderella">Travis CI page for the Sinderella gem</a> is where you can view the entire build history, including both passed and failed tests.</p>

### .travis.yml

To complete the configuration, we need to add a <code>.travis.yml</code> file. If you’ve enabled your repository from your Travis CI account and you don’t have a <code>.travis.yml</code> file, then Travis CI will throw an error and complain that you need one. Let’s look at the one we’ve set up for Sinderella:

<pre><code class="language-yaml">
language: ruby
cache: bundler

rvm:
  - jruby
  - 2.0.0

script: 'bundle exec rake'

notifications:
  email:
    recipients:
      - my@email.com
    on_failure: change
    on_success: never
</code></pre>

Let’s go through each property to understand what it does:

*   `language: ruby` Here, we’re telling Travis CI that the language in which we’re writing tests is Ruby.
*   `cache: bundler` This tells Travis CI that we want it to cache the gems we’ve specified. (Running Bundler can be a slow process, and if your gems are unlikely to change often, then you don’t want to keep running `bundle install` every time you push a commit, because we want our tests to run as quickly as possible.)
*   `rvm:` This specifies the different Ruby versions and engines that we want our tests to run against (in this case, JRuby and MRI 2.0.0).
*   `script: 'bundle exec rake'` This gives Travis CI the command it requires to run the tests.
*   `notifications:` This indicates how we want Travis CI to notify us. Here, we’re specifying an email address to receive the notifications. We’re also specifying that an email should be sent only if a failure has occurred (there’s no point in getting thousands of emails telling us that nothing is wrong).</p>

### Preventing a Test Run

If you’re committing a change that doesn’t affect your code or tests, then you don’t want to waste time watching those non-breaking changes trigger a test run on Travis CI (no matter how fasts the tests are).

The easiest way to avoid this is to add <code>[ci skip]</code> anywhere in your commit message. Travis CI will see this and then happily ignore the commit.</p>

## [](#)Code Coverage And Statistics With Coveralls.io

One last service we’ll use is <a href="https://coveralls.io">Coveralls</a>, which you should have already registered for.
<blockquote>Coveralls works with your continuous integration server to give you test coverage history and statistics. Free for open source, pro accounts for private repos.</blockquote>

When you log into Coveralls for the first time, it will ask you to select repositories to monitor. It works like Travis CI, listing all of your repositories for you to enable and disable access. (You can also click a button to resynchronize the repository list, in case you’ve added a repository since last syncing).

To set up Coveralls, we need to add a file that tells Coverall what to do. For our project, we need to add a file to the root directory named <code>.coveralls.yml</code>, in which we’ll include a single line of configuration:

<pre><code class="language-yaml">
service_name: travis-ci
</code></pre>

This tells Coveralls that we’re using Travis CI as our CI server. (If you’ve signed up for a Pro account, then use <code>travis-pro</code> instead.)

We also need to add the Coveralls gem to our <code>gemspec</code>:

<pre><code class="language-ruby">
spec.add_development_dependency "coveralls"
</code></pre>

Finally, we need to include Coveralls’ code in our <code>spec_helper.rb</code> file:

<pre><code class="language-ruby">
require 'coveralls'
Coveralls.wear!

require 'pry'
require 'sinderella'
</code></pre>

Notice that we have to load the code before the Sinderella code. If you load Coveralls after the application’s code has loaded, then it wouldn’t be able to hook into the application properly.

Let’s return to our TDD process.</p>

## [](#)Skeleton Specification

When following TDD, I prefer to create a skeleton of a test suite, so that I have some idea of the type of API to develop. Let’s change the contents of the <code>sinderella_spec.rb</code> file to have a few empty tests:

<pre><code class="language-ruby">
require 'spec_helper'

describe Sinderella do
  let(:data) {{ :key =&gt; 'value' }}
  let(:till_midnight) { 0 }

  describe '.transforms(data, till_midnight)' do
    it 'returns a hash of the passed data' do
      pending
    end

    it 'stores original and transformed data' do
      pending
    end

    it 'restores the data to its original state after set time' do
      pending
    end
  end

  describe '.get(id)' do
    context 'before midnight (before time expired)' do
      it 'returns transformed data' do
        pending
      end
    end

    context 'past midnight (after time expired)' do
      it 'returns original data' do
        pending
      end
    end
  end

  describe '.midnight(id)' do
    it 'restores the data to its original state' do
      pending
    end
  end
end
</code></pre>

Notice the <code>pending</code> command, which is provided by RSpec and allows the tests to run without throwing an error. (The suite will highlight pending tests that still need to be implemented so that you don’t forget about them.)

You could also use the <code>fail</code> command, but <code>pending</code> is recommended for unimplemented tests, particularly before you’ve written the code to execute them. Relish demonstrates some examples.

From here on, I follow the full TDD process and write the code from the outside in: red, green, refactor.

For the first test I wrote for Sinderella, I realized that my code needs a way to create an MD5 hash from a data object, and that’s when I reached for the BBC News’ gem, <a title="ime_d" href="https://rubygems.org/gems/crimp">Crimp</a>. Thus, I had to update the <code>gemspec</code> file to include a new runtime dependency: <code>spec.add_runtime_dependency "crimp"</code>.

I won’t go step by step into how I TDD’ed the code because it isn’t relevant to this article. We’re focusing more on the principles of creating a gem, not on details of implementation. But you can get all of the gruesome details from the public list of commits in <a href="https://github.com/Integralist/Sinderella/commits/master">Sinderella’s GitHub repository</a>.

Also, you might not even be interested in the RSpec testing framework and might be planning on using a different framework to write your gem. That’s fine. Anyway, what follows is the full Sinderella specification file (as of February 2014):

### sinderella_spec.rb

<pre><code class="language-ruby">
require 'spec_helper'

describe Sinderella do
  let(:data) {{ :key =&gt; 'value' }}
  let(:till_midnight) { 0 }

  def create_new_instance
    @id = subject.transforms(data, till_midnight) do |data|
      data.each do |key, value|
        data.tap { |d| d[key].upcase! }
      end
    end
  end

  describe '.transforms(data, till_midnight)' do
    it 'returns a MD5 hash of the provided data' do
      create_new_instance
      expect(@id).to be_a String
      expect(@id).to eq '24e73d3a4f027ff81ed4f32c8a9b8713'
    end
  end

  describe '.get(id)' do
    context 'before midnight (before time expired)' do
      it 'returns the transformed data' do
        Sinderella.stub(:check)
        create_new_instance
        expect(subject.get(@id)).to eq({ :key =&gt; 'VALUE' })
      end
    end

    context 'past midnight (after time expired)' do
      it 'returns the original data' do
        create_new_instance
        Sinderella.reset_data_at @id
        expect(subject.get(@id)).to eq({ :key =&gt; 'value' })
      end
    end
  end

  describe '.midnight(id)' do
    context 'before midnight (before time expired)' do
      it 'restores the data to its original state' do
        Sinderella.stub(:check)
        create_new_instance
        subject.midnight(@id)
        expect(subject.get(@id)).to eq({ :key =&gt; 'value' })
      end
    end
  end
end
</code></pre>

### data_store_spec.rb

<pre><code class="language-ruby">
require 'spec_helper'

describe DataStore do
  let(:instance)    { DataStore.instance }
  let(:original)    { 'bar' }
  let(:transformed) { 'BAR' }

  before(:each) do
    instance.set({
      :id =&gt; 'foo',
      :original =&gt; original,
      :transformed =&gt; transformed
    })
  end

  describe 'set(data)' do
    it 'stores original and transformed data' do
      expect(instance.get('foo')[:original]).to eq(original)
      expect(instance.get('foo')[:transformed]).to eq(transformed)
    end
  end

  describe 'get(id)' do
    it 'returns data object' do
      expect(instance.get('foo')).to be_a Hash
      expect(instance.get('foo').key?(:original)).to be true
      expect(instance.get('foo').key?(:transformed)).to be true
    end
  end

  describe 'reset(id)' do
    it 'replaces the transformed data with original data' do
      instance.reset('foo')
      foo = instance.get('foo')
      expect(foo[:original]).to eq(foo[:transformed])
    end
  end
end
</code></pre>

### Passing Specification

Here is the output of our passed test suite:

<pre><code class="language-shell">
❯ rake spec
/path/to/.rubies/jruby-1.7.9/bin/jruby -S rspec ./spec/data_store_spec.rb ./spec/sinderella_spec.rb --color --format nested

DataStore
  set(data)
    stores original and transformed data
  get(id)
    returns data object
  reset(id)
    replaces the transformed data with original data

Sinderella
  .transforms(data, till_midnight)
    returns a MD5 hash of the provided data
  .get(id)
    before midnight (before time expired)
      returns the transformed data
    past midnight (after time expired)
      returns the original data
  .midnight(id)
    before midnight (before time expired)
      restores the data to its original state

Finished in 0.053 seconds
7 examples, 0 failures
</code></pre>

## [](#)Design Patterns

<a href="https://en.wikipedia.org/wiki/Design_pattern">According to Wikipedia</a>:
<blockquote>A design pattern in architecture and computer science is a formal way of documenting a solution to a design problem in a particular field of expertise.</blockquote>

Many design patterns exist, one of which in particular is usually <a href="https://www.google.com/search?q=singleton%20design%20pattern%20is%20bad#q=singleton%20design%20pattern%20good%20or%20bad">frowned on</a>, the <a href="https://en.wikipedia.org/wiki/Singleton_pattern">Singleton</a> pattern.

I won’t debate the merits or problems of the Singleton design pattern, but I opted to use it in Sinderella to implement the <code>DataStore</code> class (which is the object that stores the original and transformed data), because what would be the point of having multiple instances of <code>DataStore</code> if the data is expected to be shared from a single access point?

Luckily, Ruby makes it really easy to create a Singleton. Just add <code>include Singleton</code> in your class definition.

Once you’ve done that, you will be able to access a single instance of your class only via an <code>instance</code> property — for example, <code>MyClass.instance.some_method()</code>.

We saw the specification (or test file) for <code>DataStore</code> in the previous section. Below is the full implementation of <code>DataStore</code>:

<pre><code class="language-ruby">
require 'singleton'

class DataStore
  include Singleton

  def set(data)
    hash_data = {
      :original    =&gt; data[:original],
      :transformed =&gt; data[:transformed]
    }

    container.store(data[:id], hash_data)
  end

  def get(id)
    container.fetch(id)
  end

  def reset(id)
    original  = container.fetch(id)[:original]
    hash_data = {
      :original =&gt; original,
      :transformed =&gt; original
    }

    container.store(id, hash_data)
  end

  private

  def container
    @store ||= Hash.new
  end
end
</code></pre>

## [](#)Badges

You might have seen some nice green badges in your favorite GitHub repository, indicating whether the tests associated with the code passed or not. Adding these to the README is straightforward enough:

<pre><code class="language-markup">
[![Build Status](https://travis-ci.org/Integralist/Sinderella.png?branch=master)](https://travis-ci.org/Integralist/Sinderella) 

[![Gem Version](https://badge.fury.io/rb/sinderella.png)](https://badge.fury.io/rb/sinderella)

[![Coverage Status](https://coveralls.io/repos/Integralist/Sinderella/badge.png)](https://coveralls.io/r/Integralist/Sinderella)
</code></pre>

The first badge is provided by Travis CI, which you can read more about <a href="https://docs.travis-ci.com/user/status-images/">in the documentation</a>.

The second is provided by RubyGems. You’ll notice on your gem’s page a “badge” link, which provides the required code and format (in this case, in <a href="https://en.wikipedia.org/wiki/Markdown">Markdown</a> format).

The third is provided by Coveralls. When you visit your repository page in the Coveralls application, you’ll see a link to “Get badge URLS”; from there, you can select the relevant format.</p>

## [](#)REPL-Driven Development

Tests and TDD are a critical part of the development process but won’t eliminate all bugs by themselves. This is where a tool such as Pry can help you to figure out how a piece of code works and the path that the code takes during a conditioned execution.

To use Pry, enter the <code>pry</code> command in the terminal. As long as Pry is installed and available from that directory, you’ll be dropped into a Pry session. To view all available commands, run the <code>help</code> command.</p>

### Testing a Local Gem Build

If you want to run the gem outside of the test suite, then you’ll want to use Pry. To do this, we’ll need to build the gem locally and then install that local build.

To build the gem, run the following command from your gem’s root directory: <code>gem build sinderella.gemspec</code>. This will generate a physical <code>.gem</code> file.

Once the gem is built and a <code>.gem</code> file has been created, you can install it from the local file with the following command: <code>gem install ./sinderella-0.0.1.gem</code>.

Notice that the built <code>gem</code> file includes the version number, so that you know you’re installing the right one (in case you’ve built multiple versions of the gem).

After installing the local version of the gem, you can open a Pry session and load the gem with <code>require 'sinderella'</code> and continue to execute your own Ruby code within Pry to test the gem as needed.</p>

## [](#)Releasing Your Gem

Once our gem has passed all of our tests and we’ve built and run it locally, we can look to release the gem to the Ruby community by pushing it to the RubyGems server.

To release our gem, we’ll use the Rake commands provided by Bundler. To view what commands are available, run <code>rake --task</code>. You’ll see something similar to the following output:

<pre><code class="language-shell">
rake build    # Build sinderella-0.0.1.gem into the pkg directory
rake install  # Build and install sinderella-0.0.1.gem into system gems
rake release  # Create tag v0.0.1 and build and push sinderella-0.0.1.gem t...
rake spec     # Run RSpec code examples
</code></pre>

*   `rake build` This first task does something similar to `gem build sinderella.gemspec` but placing the gem in a `pkg` (package) directory.
*   `rake install` The second task does the same as `gem install ./sinderella-0.0.1.gem` but saves us the extra typing.
*   `rake release` The third task is what we’re most interested at this point. It creates a tag in git, indicating the relevant version number, pulled from the `version.rb` file that Bundler created for us. It then builds the gem and pushes it to RubyGems.
*   `rake spec` The fourth task runs the tests using the test runner (in this case, RSpec), as defined and configured in the main `Rakefile`.

To release our gem, we’ll first need to make sure that the version number in the <code>version.rb</code> file is correct. If it is, then we’ll commit those changes and run the <code>rake release</code> task, which should give the following output:

<pre><code class="language-shell">
❯ rake release
sinderella 0.0.1 built to pkg/sinderella-0.0.1.gem.
Tagged v0.0.1.
Pushed git commits and tags.
Pushed sinderella 0.0.1 to rubygems.org.
</code></pre>

Now we can view the details of the gem at <a href="https://rubygems.org/gems/sinderella">https://rubygems.org/gems/sinderella</a>, and other users may access our gem in their own code simply by including <code>require 'sinderella'</code>.</p>

## [](#)Conclusion

Thanks to the use of Bundler, the process of creating a gem boilerplate is made a lot simpler. And thanks to the principles of TDD and REPL-driven development, we know that we have a well-tested piece of code that can be reliably shared with the Ruby community.

{{< signature "al, il" >}}

