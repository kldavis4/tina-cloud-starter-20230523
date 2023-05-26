---
title: A Thorough Introduction To Backbone.Marionette (Part 1)
slug: introduction-backbone-marionette
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0fc0d89-8926-46db-b749-c08ce8a1a96f/illu-marionette1.jpg
date: 2013-02-11T15:05:44.000Z
author: joseph-zimmerman
description: >-
  Backbone.js is quickly becoming the most popular framework for building
  modular client-side JavaScript applications. This is largely due to its **low
  barrier to entry**; getting started with it is super-simple.
categories:
  - Coding
  - Frameworks
  - JavaScript
---
<em>To help you tap the full potential of Marionette, we've prepared an entire <a href="https://shop.smashingmagazine.com/better-backbone-applications-with-marionettejs.html">eBook</a> full of useful hands-on examples which is also available in the <a href="https://shop.smashingmagazine.com/smashing-library-complete.html">Smashing Library</a>. — Ed.</em>

Backbone.js is quickly becoming the most popular framework for building modular client-side JavaScript applications. This is largely due to its low barrier to entry; getting started with it is super-simple. However, unlike Ember.js, Backbone, being so minimal, also leaves a lot up to the developer to figure out.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">A Thorough Introduction To Backbone.Marionette (Part 2)</span>](https://www.smashingmagazine.com/2013/04/thorough-introduction-backbone-marionette-part-2-modules/)
*   [A Thorough Introduction To Backbone.Marionette (Part 3)](https://www.smashingmagazine.com/2014/06/thorough-introduction-backbone-marionette-part-3/)
*   [Backbone.js Tips And Patterns](https://www.smashingmagazine.com/2013/08/backbone-js-tips-patterns/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)

So, once you start getting into more advanced applications, it’s no longer so simple. Backbone.Marionette was created to alleviate a lot of <strong>the growing pains of Backbone development</strong>. Backbone.Marionette “make[s] your Backbone.js apps dance with a composite application architecture!,” according to its author.

{{% feature-panel %}}

This “composite” architecture refers mainly to the numerous view types that have been provided to help with subview management. We won’t be discussing those views today (although we will touch on regions, which are a small part of the subview management that Marionette offers), but you can find documentation for this project in the <a href="https://github.com/marionettejs/backbone.marionette">GitHub repository</a>. It offers numerous components that extend Backbone and that enable you to write less boilerplate and do more stuff with little to no hassle, especially when it comes to views.</p>

## The Central Application Object

Most of the time, when someone creates a Backbone application, they make a central object that everything is attached to, which is often referenced as <code>App</code> or <code>Application</code>. Backbone doesn’t offer anything to make this object from, so <strong>most people just create a main router</strong> and make that the app object. While it’s great that people are attaching things to a central object so that the global namespace isn’t so convoluted, the router was not designed to handle this task.

Derick Bailey, the creator of Marionette, had a better idea. He created a “class” that you could instantiate an object from that is specifically designed to handle the responsibilities of being the go-to root object of the entire application. You create a new application with <code>var App = new Backbone.Marionette.Application()</code>, and then, when everything is set, you start the application with <code>App.start(options)</code>. I’ll discuss the <code>options</code> argument soon. For now, just remember that it’s optional.</p>

## Initializers

One of the coolest things about Marionette’s <code>Application</code> is the initializers. When your code is modular, several pieces will need to be initialized when the application starts. Rather than filling a <code>main.js</code> file with a load of code to initialize all of these objects, you can just set the modules up for initialization within the code for the module. You do this using <code>addInitializer</code>. For example:

<pre><code class="language-javascript">var SomeModule = function(o){
  // Constructor for SomeModule
};

App.addInitializer(function(options) {
  App.someModule = new SomeModule(options);
});</code></pre>

All of the initializers added this way will be run when <code>App.start</code> is called. Notice the <code>options</code> argument being passed into the initializer. This is the very same object that is passed in when you call <code>App.start(options)</code>. This is great for allowing a configuration to be passed in so that every module can use it.

A few events are also fired when running through these initializers:

*   `initialize:before` Fires just before the initializers are run.
*   `initialize:after` Fires just after the initializers have all finished.
*   `start` Fires after `initialize:after`.

You can listen for these events and exert even more control. Listen for these events like this:

<pre><code class="language-javascript">App.on('initialize:before', function(options) {
  options.anotherThing = true; // Add more data to your options
});
App.on('initialize:after', function(options) {
  console.log('Initialization Finished');
});
App.on('start', function(options) {
  Backbone.history.start(); // Great time to do this
});</code></pre>

Pretty simple, and it gives you a ton of flexibility in how you start up your applications.</p>

## Event Aggregator

The <code>Application</code> object brings even more possibilities for decoupling a Backbone application through the use of an event aggregator. A while back I wrote a post about <a href="https://www.joezimjs.com/javascript/scalable-javascript-applications/">scalable JavaScript applications</a>, in which I mentioned that modules of a system should be completely ignorant of one another, and that the only way they should be able to communicate with each other is <strong>through application-wide events</strong>. This way, every module that cares can listen for the changes and events they need to so that they can react to them without anything else in the system even realizing it exists.

Marionette makes this kind of decoupling largely possible via the event aggregator that is automatically attached to the application object. While this is only one of the mechanisms that I wrote about in that article, it is a start and can be very useful in even smaller applications.

The event aggregator is available through a property in the application called <code>vent</code>. You can subscribe and unsubscribe to events simply via the <code>on</code> and <code>off</code> methods, respectively (or <code>bind</code> and <code>unbind</code>, if you prefer). These functions might sound familiar, and that’s because the event aggregator is simply an extension of <a href="https://backbonejs.org/#Events">Backbone’s <code>Event</code> object</a>. Really, the only thing new here that you need to worry about is that we’re using the events on an object that should be accessible everywhere within your app, so that every piece of your application can communicate through it. The event aggregator is available as its own module too, so you can add it to any object you want, just like Backbone’s <code>Event</code>.</p>

## Regions

<code>Region</code> is another module for Marionette that enables you to easily attach views to different regions of an HTML document. I won’t go into detail about how regions work here — that’s a topic for another day — but I’ll cover it briefly and explain how to use them with <code>Application</code>.

A region is an object — usually created with <code>new Backbone.Marionette.Region({ el: 'selector'})</code> — that manages an area where you attach a view. You would add a view and automatically render it by using <code>show</code>. You can then close out that view (meaning it will remove it from the DOM and, if you’re using one of the Marionette views, undo any bindings made by the view) and render a different view simply by calling <code>show</code> again, or you can just close the view by calling <code>close</code>. Regions can do more than that, but the fact that they handle the rendering and closing for you with a single function call makes them extremely useful. Here’s a code sample for those who speak in code rather than English:

<pre><code class="language-javascript">// Create a region. It will control what's in the #container element.
var region = new Backbone.Marionette.Region({
  el: "#container"
});

// Add a view to the region. It will automatically render immediately.
region.show(new MyView());

// Close out the view that's currently there and render a different view.
region.show(new MyOtherView());

// Close out the view and display nothing in #container.
region.close();</code></pre>

If you want a <code>Region</code> directly on your application object (e.g. <code>App.someRegion</code>), there’s a simple way to add one quickly: <code>addRegions</code>. There are three ways to use <code>addRegions</code>. In every case, you would pass in an object whose property names will be added to the application as regions, but the value of each of these may be different depending on which way you wish to accomplish this.</p>

### Selector

Simply supply a selector, and a standard region will be created that uses that selector as its <code>el</code> property.

<pre><code class="language-javascript">App.addRegions({
  container: "#container",
  footer:    "#footer"
});

// This is equivalent to
App.container = new Backbone.Marionette.Region({el:"#container"});
App.footer    = new Backbone.Marionette.Region({el:"#footer"});</code></pre>

### Custom Region Type

You can extend <code>Region</code> to create your own types of regions. If you want to use your own type of region, you can use the syntax below. Note that, with this syntax, <code>el</code> must already be defined within your region type.

<pre><code class="language-javascript">var ContainerRegion = Backbone.Marionette.Region.extend({
  el: "#container", // Must be defined for this syntax
  // Whatever other custom stuff you want
});

var FooterRegion = Backbone.Marionette.Region.extend({
  el: "#footer", // Must be defined for this syntax
  // Whatever other custom stuff you want
});

// Use these new Region types on App.
App.addRegions({
  container: ContainerRegion,
  footer:    FooterRegion
});

// This is equivalent to:
App.container = new ContainerRegion();
App.footer    = new FooterRegion();</code></pre>

### Custom Region Type with Selector

If you don’t define <code>el</code> — or you want to override it — in your custom region type, then you can use this syntax:

<pre><code class="language-javascript">var ContainerRegion = Backbone.Marionette.Region.extend({});

var FooterRegion = Backbone.Marionette.Region.extend({});

// Use these new Region types on App.
App.addRegions({
  container: {
    regionType: ContainerRegion,
    selector:   "#container"
  },
  footer: {
    regionType: FooterRegion,
    selector:   "#footer"
  }
});

// This is equivalent to:
App.container = new ContainerRegion({el:"#container"});
App.footer    = new FooterRegion({el:"#footer"});</code></pre>

As you can see, adding application-wide regions is dead simple (especially if you’re using the normal <code>Region</code> type), and they add a lot of useful functionality.</p>

## Conclusion

As you can already see, Marionette adds a ton of great features to make Backbone development simpler, and we’ve covered only one of many modules that it provides (plus, we’ve touched on a couple of other modules that <code>Application</code> itself uses, but there’s plenty more to learn about those). I hope this will entice Backbone programmers a bit and make you eager to <a href="https://www.smashingmagazine.com/2013/04/02/thorough-introduction-backbone-marionette-part-2-modules/">read the rest of this series</a>, when I’ll cover more of the modules.

<em>Credits of image on start page: <a href="https://www.flickr.com/photos/dmitry-baranovskiy/2378867408/">Dmitry Baranovskiy</a>.</em>

{{< signature "al" >}}

