---
title: Get Started Writing iOS Apps With RubyMotion
slug: get-started-writing-ios-apps-with-rubymotion
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdb2f6d1-2bd4-40af-88c1-1b89f9ff7e6a/optical-black-white-red.jpg
date: 2012-08-02T10:41:40.000Z
author: clay-allsopp
description: >-
  Everyone is trying to craft the next beautiful iOS app, but building on
  Apple’s platform has traditionally required experience in a niche programming
  language, Objective-C. However, with the release of RubyMotion, anyone can
  make a completely native iOS app using the power of Ruby.
categories:
  - Mobile
  - Apps
  - iOS
---
Everyone is trying to craft the next beautiful iOS app, but building on Apple’s platform has traditionally required experience in a niche programming language, Objective-C. However, with the release of <a href="https://www.rubymotion.com/">RubyMotion</a>, anyone can make a completely native iOS app using the power of Ruby.

Developers have tried to get around the Objective-C hurdle by making <a href="https://www.cocoacontrols.com/posts/a-primer-on-hybrid-apps-for-ios">HTML and JavaScript hybrid apps</a> using tools like <a href="https://phonegap.com/">PhoneGap</a> and <a href="https://trigger.io/">Trigger</a>, but the result can be a <a href="https://blog.mobtest.com/2012/05/heres-why-the-facebook-ios-app-is-so-bad-uiwebviews-and-no-nitro/">substandard user experience</a>. Plus, mobile-centric Web development is yet another narrow skill set that potential developers have to learn. RubyMotion is intended to be an alternative solution that produces apps identical to those created in Objective-C, except using a more accessible and popular language.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Get Started With Ruby](https://www.smashingmagazine.com/2012/05/beginners-guide-ruby/)
*   [Get Started Writing iOS Apps With RubyMotion](https://www.smashingmagazine.com/2012/08/get-started-writing-ios-apps-with-rubymotion/)
*   [A Guide To Starting Your Own Rails Engine Gem](https://www.smashingmagazine.com/2011/06/a-guide-to-starting-your-own-rails-engine-gem/)
*   [How To Set Up An Ubuntu Local Machine For Ruby On Rails](https://www.smashingmagazine.com/2011/06/set-up-an-ubuntu-local-development-machine-for-ruby-on-rails/)

How does that work? Unlike normal interpreted Ruby, RubyMotion is compiled to machine code and runs incredibly fast. This allows full access to the existing iOS SDK and APIs while preserving the flexibility and plain fun of Ruby. RubyMotion also includes interactive debugging and testing tools that don’t exist in the traditional Xcode and Objective-C workflow.

{{% feature-panel %}}

The hope is that coding in Ruby and using the RubyMotion toolchain will make developing iOS apps easier for new developers, as well as help existing iOS developers be even more productive. I’ve been working on iOS apps since the original SDK, but I still jumped at the chance to write real native apps in the same language that I was already using for my back ends.

If you’ve hit stumbling blocks learning native iOS development or are just curious about what Ruby on iOS looks like, you should read on. We’ll try out RubyMotion by making an app that grabs some data from the Internet and updates the screen’s content accordingly.

But first, we have to install it.</p>

## Set Up

RubyMotion is a commercial product from HipByte, a company founded by the developers responsible for MacRuby. Parts of the RubyMotion tools are <a href="https://github.com/HipByte/RubyMotion">open source</a>, but the actual Ruby compiler (where the magic happens) is not. Even though it’s only a few months old, a strong community has already developed around RubyMotion; I’m involved in maintaining some <a href="https://github.com/clayallsopp/formotion">cool</a> <a href="https://github.com/clayallsopp/remote_model">projects</a> but am in no way affiliated with HipByte.

You can purchase a lifetime license to RubyMotion for $200 on the <a href="https://sites.fastspring.com/hipbyte/product/rubymotion">RubyMotion website</a>. The license comes with a graphical installer that sets up everything on your Mac, no commands necessary. If you run into trouble, support is available on <a href="https://twitter.com/rubymotion">@RubyMotion</a>’s Twitter account and the <a href="https://groups.google.com/forum/?fromgroups#!forum/rubymotion">mailing list</a>.

RubyMotion also requires you to install Xcode from the <a href="https://itunes.apple.com/us/app/xcode/id497799835?mt=12">Mac App Store</a> to get some developer libraries and tools. However, RubyMotion’s tools work in the command shell, and you’re free to use any editor or IDE you want. Supplementary packages are available for most editors that could speed up your development.

Having some experience with <a href="https://rubygems.org/">RubyGems</a> and <a href="https://github.com/jimweirich/rake">Rake</a> also helps because RubyMotion uses these tools. RubyGems should come installed on your Mac, and you can use it to install Rake by running <code>gem install rake</code> in the terminal. If you have never seen those words before, no worries; we’ll still cover them like fresh topics.</p>

## Create A Project

In contrast to the normal iOS toolchain, RubyMotion works in the command line. You can still use Xcode’s Interface Builder to construct your interfaces, but complete Xcode integration is unsupported at this time. So, fire up the terminal and let’s get started.

RubyMotion uses two commands extensively: <code>rake</code> and <code>motion</code>. The <code>motion</code> command creates RubyMotion projects and manages the RubyMotion tools; if you’re coming from a Rails background, it’s sort of like the <code>rails</code> command. If you enter <code>motion</code> in the shell, you’ll see a brief instruction page:

<pre><code class="language-markup tmp-ruby">$ motion
Usage:
  motion [-h, --help]
  motion [-v, --version]
  motion &lt;command&gt; [&lt;args…&gt;]

Commands:
  create       Create a new project
  activate     Activate the software license
  update       Update the software
  support      Create a support ticket</code></pre>

We’re interested in <code>motion create &lt;Project Name&gt;</code>. This will create the folder <code>&lt;Project Name&gt;</code> in the current directory and fill it with the essential files and folders that you’ll need for a RubyMotion project.

Run <code>motion create Smashing</code> to create your first project. You should see some output like this:

<pre><code class="language-markup tmp-ruby">$ motion create Smashing
    Create Smashing
    Create Smashing/.gitignore
    Create Smashing/Rakefile
    Create Smashing/app
    Create Smashing/app/app_delegate.rb
    Create Smashing/resources
    Create Smashing/spec
    Create Smashing/spec/main_spec.rb</code></pre>

Run <code>cd ./Smashing</code> to enter the project’s directory. You’ll be running all subsequent commands from this location, so keeping it open in a dedicated tab or window is a good idea.

Let’s walk through what this command created:

*   `./Rakefile` This is the file that the `rake` command uses to determine what commands are available. RubyMotion also uses it for settings such as your app’s name, resources and source-code location.
*   `./app` This is the directory that contains all of your code. RubyMotion will recursively dig through this folder and load any `*.rb` files that it finds. You can specify additional directories outside of `./app` in `Rakefile`.
*   `./app/app_delegate.rb` This is your only piece of code right now. It contains your app’s `delegate`. We’ll go into more detail soon, but know that every RubyMotion project needs a `delegate`.
*   `./resources` Files in this directory will be copied into your app. It’s a good place to store images, data and icons.
*   `./spec` This is the directory for your app’s automated tests. RubyMotion ships with a port of the Ruby testing framework [Bacon](https://github.com/chneukirchen/bacon/), which you can use to write both unit and functional or UI tests. Any `*.rb` files in this directory will be executed as tests when you invoke the `rake spec` command.
*   `./spec/main_spec.rb` This is the default test, created as an example.

Compared to larger frameworks such as Rails, this isn’t a lot of configuration. The only files we really care about today are <code>Rakefile</code> and <code>app_delegate.rb</code>, so let’s dive into those.</p>

## Run The App

The <code>Rakefile</code> is the first file loaded when you build your app. Its job is to configure your app’s properties and load any additional files that your project might need. By default, it looks something like this:

<pre><code class="language-markup tmp-ruby"># -*- coding: utf-8 -*-
$:.unshift("/Library/RubyMotion/lib")
require 'motion/project'

Motion::Project::App.setup do |app|
  # Use 'rake config' to see complete project settings.
  app.name = 'Smashing'
end</code></pre>

You’ve probably only seen <code>$.unshift</code> if you’re familiar with Ruby. It takes its argument — in this case, <code>/Library/RubyMotion/lib</code> — and adds it to <code>require</code>’s search path. This is necessary before <code>require 'motion/project'</code>, because that file is actually located in the RubyMotion <code>lib</code> directory. Without the <code>unshift</code>, no RubyMotion code would be found.

The <code>motion/project</code> directory is what actually allows us to write RubyMotion apps. It does a lot of stuff behind the scenes, but most obviously it includes the <code>Motion::Project</code> module that we use immediately afterwards. The <code>App.setup</code> block is where we can edit our app’s name, files, identifier and many other options. As the generated comment suggests, you can run <code>rake config</code> to see all possible properties. By default, it uses the <code>Smashing</code> project name that we passed in <code>motion create</code>.

When you run <code>rake</code>, it will load the <code>Rakefile</code>. Requiring <code>motion/project</code> actually creates a bunch of <code>rake</code> “tasks.” These tasks allow you to pass arguments to <code>rake</code> to invoke particular actions. You can see a complete list of included tasks by running <code>rake --tasks</code> in your project’s directory:

<pre><code class="language-markup tmp-ruby">$ rake --tasks
    rake archive              # Create archives for everything
    rake archive:development  # Create an .ipa archive for development
    rake archive:release      # Create an .ipa for release (AppStore)
    rake build                # Build everything
    rake build:device         # Build the device version
    rake build:simulator      # Build the simulator version
    rake clean                # Clear build objects
    rake config               # Show project config
    rake ctags                # Generate ctags
    rake default              # Build the project, then run the simulator
    rake device               # Deploy on the device
    rake simulator            # Run the simulator
    rake spec                 # Run the test/spec suite
    rake static               # Create a .a static library</code></pre>

Looks like <code>rake</code> does quite a bit, doesn’t it? Most importantly, if you just run <code>rake</code>, it will build and run your app in the Simulator.

Run <code>rake</code> and observe RubyMotion compiling your project’s files (just <code>app_delegate.rb</code> for now). When it’s done building, it will open your (so far empty) app in the iOS Simulator:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f35e76c-b2fd-4c92-a284-6663d6bdd7b2/0.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f35e76c-b2fd-4c92-a284-6663d6bdd7b2/0.png" alt="iOS Simulator and terminal when first running RubyMotion" /></a>

Additionally, you’ll see an <code>irb</code>-esque prompt appear in the shell. This allows you to interact with the app in real time without any additional compilation, which is useful for debugging and rapid interface development. Try running some basic commands with it:

<pre><code class="language-markup tmp-ruby">$ rake
  …

(main)&gt; "a string"
=&gt; "a string"
(main)&gt; h = {hello: "motion"}
=&gt; {:hello=&gt;"motion"}
(main)&gt; h
=&gt; {:hello=&gt;"motion"}</code></pre>

Our app is off to a great start: we’ve installed RubyMotion, created a new project, learned what all the files do, and gotten a (very bare) app running. Next, we’ll make our creation actually display something on the screen.

## Little Boxes

We’re going to build an app that displays a colored box on the screen. Sounds pretty simple, right?

Then we’ll spice it up with random color changes using the <a href="https://www.colr.org/api.html">Colr API</a>. It’s going to use a mix of Apple-developed APIs and some cutting-edge work from the RubyMotion community, so when it’s done you’ll have gotten a well-rounded experience with RubyMotion development. We will end up with something like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f949404-aa08-49c7-8521-544b8e7cb513/2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f949404-aa08-49c7-8521-544b8e7cb513/2.png" alt="Box color changed via server data" /></a>

If you want to follow along, the source for this example is available on <a href="https://github.com/clayallsopp/smashing-rubymotion">GitHub</a>.

Open up <code>app_delegate.rb</code> in your favorite code editor. It’s pretty barren, implementing only one function, <code>application:didFinishLaunchingWithOptions:</code>:

<pre><code class="language-markup tmp-ruby">class AppDelegate
  def application(application, didFinishLaunchingWithOptions:launchOptions)
    true
  end
end</code></pre>

Note that we refer to RubyMotion functions by a combination of their usual Ruby name (<code>application</code>) and their named parameters (<code>didFinishLaunchingWithOptions:</code>), all separated by colons. Named parameters were added to RubyMotion to preserve the existing Objective-C APIs, and the extra symbols are <strong>required</strong> parts of the method name (i.e. you can’t just call <code>delegate.application(@app, options)</code>). Without those extra parameters, we wouldn’t be able to tell the difference between <code>def application(application, didFinishLaunchingWithOptions:launchOptions)</code> and <code>def application(application, handleOpenURL:url)</code>.

Moving on, RubyMotion looks for a class named <code>AppDelegate</code> and makes it the application’s <code>delegate</code> object. This special object receives callbacks for different events in the lifecycle of the app, such as for starting up, shutting down and receiving push notifications. The <code>application:didFinishLaunchingWithOptions:</code> function is called once the system has finished its own process of starting the app and is ready for us to take control. In most cases, this function should return <code>true</code> and allow everything to start.

We’re going to add some “views” to our app. Each view is a subclass of <code>UIView</code>, and everything you see on the screen is a descendent of that class. The root view of every app is an instance of <code>UIWindow</code>, a special type of <code>UIView</code>. Views are added as <code>subviews</code> to one another; when you move a view, you also move all of its subviews.

Each view has a <code>frame</code> property, which describes its position and dimensions. The position of a view is actually defined relative to its superview. For example, adding a box at <code>(10, 10)</code> as a subview to a view located at <code>(20, 20)</code> in the window means that our new box will really appear at <code>(30, 30)</code>.

Edit your <code>AppDelegate</code> to include our new views:

<pre><code class="language-markup tmp-ruby">class AppDelegate
  def application(application, didFinishLaunchingWithOptions:launchOptions)
    # UIScreen describes the display the app is running on.
    app_frame = UIScreen.mainScreen.applicationFrame
    @window = UIWindow.alloc.initWithFrame(app_frame)

    # This is the special method of UIWindow which lets them exist outside of a parent view
    @window.makeKeyAndVisible

    # This is our blue box
    # CGRectMake == CGRectMake(x, y, width, height)
    @box = UIView.alloc.initWithFrame CGRectMake(0, 0, 100, 100)
    @box.backgroundColor = UIColor.blueColor
    @window.addSubview(@box)

    # UIButtonTypeRoundedRect is the standard button style on iOS
    @button = UIButton.buttonWithType(UIButtonTypeRoundedRect)
    # A button has multiple "control states", like disabled, highlighted, and normal
    @button.setTitle("Change Color", forState:UIControlStateNormal)
    # Sizes the button to fit its title
    @button.sizeToFit
    # Position the button below our box.
    @button.frame = CGRectMake(0, @box.frame.size.height + 20, @button.frame.size.width, @button.frame.size.height)
    @window.addSubview(@button)

    true
  end
end</code></pre>

We’ve created our window and made it the “key” window, which means that it’s the window receiving user input. We then added our blue <code>@box</code> and <code>@button</code> as subviews to the window.

Now, this is not the only way to add views to our window. We could have added our views using the Interface Builder, a tool included with Xcode for creating iOS UIs with a drag-and-drop interface. RubyMotion does support Interface Builder, but you really shouldn’t dive into it without understanding what happens behind the scenes.

The other method is to use something called a <code>UIViewController</code> and then to populate its <code>view</code> property with our boxes. This is actually the correct way because it conforms your app to the model-view-controller design pattern that the SDK follows. You simply tell the <code>window</code> to load the <code>controller</code>, and everything will get handled appropriately. So, why didn’t we do it this way? Because it requires more information overhead, and in this example we’re trying to be as concise as possible; in production code, you will definitely need to use a controller when you start managing more than one or two views.

Moving on, <code>rake</code> our improved delegate and check out the result, which is starting to look better:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcc23e65-730c-4b09-a09a-9a3d8b4bd7b3/1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcc23e65-730c-4b09-a09a-9a3d8b4bd7b3/1.png" alt="Box views added to our RubyMotion app" /></a>

Now we need to make <code>@button</code> actually do something besides turn blue when we press it. Buttons can take <code>target</code>s for certain events such as taps. We can add a target and callback (known as an <code>action</code> in iOS SDK parlance) in our <code>AppDelegate</code> like this:

<pre><code class="language-markup tmp-ruby">…
    @window.addSubview(@button)

    @button.addTarget(self, action:"button_tapped", forControlEvents:UIControlEventTouchUpInside)

    true
  end

  def button_tapped
    puts "I'm tapped!"
  end
end</code></pre>

<code>UIControlEventTouchUpInside</code> is one of many <code>UIControlEvent</code>s that a button can respond to. It sounds complicated, but in plain English it refers to a “touch” that lifts “up” and is still “inside” of the button’s rectangle. When that occurs, <code>button_tapped</code> will be called. The <code>puts</code> prints a string to the terminal when we run the app in the simulator.

Give it a <code>rake</code> and confirm for yourself that our message prints out:

<pre><code class="language-markup tmp-ruby">$ rake
     Build ./build/iPhoneSimulator-5.1-Development
   Compile ./app/app_delegate.rb
      Link ./build/iPhoneSimulator-5.1-Development/Smashing.app/Smashing
    Create ./build/iPhoneSimulator-5.1-Development/Smashing.dSYM
  Simulate ./build/iPhoneSimulator-5.1-Development/Smashing.app
(main)&gt; I'm tapped!</code></pre>

We’ve thrown some views onto our previously barren app and added some very basic interactivity. Time to hook it up to the good ol’ information superhighway.</p>

## HTTP

Now that we’ve got a box and a button on the screen, let’s grab some data from the Internet. To make our networking code painless, we’ll use <a href="https://bubblewrap.io/">BubbleWrap</a>, a popular RubyMotion library filled with many idiomatic Ruby wrappers. It’ll also handle JSON de-serialization, so it’s the only external component we need.

To install BubbleWrap, run <code>gem install bubble-wrap</code>. In our Rakefile, we need to require <code>bubble-wrap</code>:

<pre><code class="language-markup tmp-ruby">…
require 'motion/project'
require 'bubble-wrap'
…</code></pre>

This makes the <code>BubbleWrap::HTTP</code> and <code>BubbleWrap::JSON</code> libraries available to us. The default <code>BubbleWrap</code> set-up also includes helpers for <code>UIColor</code>, which we’ll use to convert a hexadecimal color code like <code>#f8f8f8</code> into a <code>UIColor</code> object.

Now on to the dirty work. The Colr API has an endpoint that returns information about a random color in JSON. We’re going to query that, get the hex representation of that color, and set our box’s <code>backgroundColor</code> to that value. In <code>AppDelegate</code>, let’s add the code to make this HTTP call in our button callback:

<pre><code class="language-markup tmp-ruby">def button_tapped
    BubbleWrap::HTTP.get("https://www.colr.org/json/color/random") do |response|
      color_hex = BubbleWrap::JSON.parse(response.body.to_str)["colors"][0]["hex"]
      # ensure that color_hex is a String when we run .to_color
      @box.backgroundColor = String.new(color_hex).to_color
      @button.setTitle(color_hex, forState: UIControlStateNormal)
    end
  end</code></pre>

This seemingly more complex task takes fewer lines of code than setting up our views. Run <code>rake</code> and check out the fruits of our labor:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f949404-aa08-49c7-8521-544b8e7cb513/2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f949404-aa08-49c7-8521-544b8e7cb513/2.png" alt="Box color changed via server data" /></a>

We can make one more small change to start adding that signature iOS polish. Right now, the user doesn’t get any feedback while the HTTP request is loading, aside from the tiny network activity indicator in the top bar. We can improve that experience by changing the button title while that’s going on. It’s also a good idea to be fault tolerant and show an error if the Colr API returns some bad data. Let’s make those changes:

<pre><code class="language-markup tmp-ruby">def application(application, didFinishLaunchingWithOptions:launchOptions)
  …
  @button.setTitle("Change Color", forState:UIControlStateNormal)
  @button.setTitle("Loading…", forState:UIControlStateDisabled)
  @button.setTitleColor(UIColor.lightGrayColor, forState:UIControlStateDisabled)
  …
end

def button_tapped
  @button.enabled = false

  BubbleWrap::HTTP.get("https://www.colr.org/json/color/random") do |response|
    color_hex = BubbleWrap::JSON.parse(response.body.to_str)["colors"][0]["hex"]
    # check if bad data as returned
    if color_hex and color_hex.length &gt; 0
      @box.backgroundColor = String.new(color_hex).to_color
      @button.setTitle(color_hex, forState: UIControlStateNormal)
    else
      @button.setTitle("Error :(", forState: UIControlStateNormal)
    end
    @button.enabled = true
  end
end</code></pre>

Let’s <code>rake</code> one last time to see our better UX in action. Not too shabby for our first app, right? You can look at the source for this example on <a href="https://github.com/clayallsopp/smashing-rubymotion">GitHub</a>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65bcb1e9-d070-4208-ab47-7c1b8b826514/3.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65bcb1e9-d070-4208-ab47-7c1b8b826514/3.png" alt="Loading user experience" /></a>

## “An Object In Motion…”

We’ve created an iOS app with dynamic data and a solid user experience in under 40 lines of clean Ruby. Making this app in Objective-C is definitely possible, but we would have lost the readability and brevity that Ruby affords. We also could have done it using a hybrid Web and native app; however, once you venture out of the basic UI building blocks and into a feature-complete iOS app, perfectly replicating a native experience becomes incredibly difficult.

Is RubyMotion right for your next iOS project? If you don’t have much experience in Objective-C but want to try app development, Ruby definitely has a gentler learning curving. Or if you’re already using Ruby somewhere else in your stack, you might reap the benefits of code portability. What about porting an existing app? Well, RubyMotion allows for middle ground: you can export your Ruby code as a static library to use in an Objective-C app, or you can use existing Objective-C code in a RubyMotion app.

This is not to say that RubyMotion is perfect. Its biggest flaw is debuggability: when you hit a nasty bug originating in the RubyMotion compiler, you can’t do a whole lot to trace or fix it. Because RubyMotion is currently closed source, we’ll have to wait for these issues to be remedied by HipByte. But if you don’t do anything tricky or “magical” with your code, then this shouldn’t be a problem. Unfortunately, I run into these issues fairly often because those “fun” bits are what make Ruby so compelling to me.

Fundamentally, RubyMotion hasn’t completely done away the original Objective-C API; you’ll still need to learn the iOS SDK to make really great iOS apps. That in itself tends to make up 80% of the hard work of developing any mobile app. And if you need to whip something up for multiple platforms, RubyMotion definitely won’t make your life any easier; it’s still very nascent and has some maturing to do. But efforts to Ruby-fy Apple’s APIs using RubyMotion are yielding interesting <a href="https://github.com/rubymotion/teacup">new directions</a> for iOS development. On a platform defined by constraints and restrictions, having more choice is never a bad thing.</p>

### Further Reading

*   [Developer Center](https://www.rubymotion.com/developer-center/), RubyMotion The official developer documentation for RubyMotion.
*   [iOS Developer Library](https://developer.apple.com/library/ios/navigation/), Apple RubyMotion uses the existing iOS SDK; it doesn’t provide any new classes out of the box. If you run into problems with your `UIView`s or other SDK classes, consult this.
*   [@RubyMotion](https://twitter.com/rubymotion) The official Twitter account, where RubyMotion responds to support requests and publicizes new RubyMotion libraries.
*   <span class="removed_link" title="https://rubymotion-tutorials.com/">RubyMotion Tutorials</span> A community-curated database of RubyMotion tutorials and writing.
*   MacRuby RubyMotion is technically a port of MacRuby to iOS. If you enjoy using Ruby for your iOS apps, then you might like writing Mac apps the same way.

<em>(al) (km)</em>

