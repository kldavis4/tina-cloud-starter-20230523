---
title: A Thorough Introduction To Backbone.Marionette (Part 2)
slug: thorough-introduction-backbone-marionette-part-2-modules
image: null
date: 2013-04-02T09:49:07.000Z
author: joseph-zimmerman
description: >-
  In the first part of this series, we discussed Backbone.Marionette’s
  Application. This time around, we’ll discuss the module system that is
  included in Backbone.Marionette. Modules are accessible through the
  Application, but modules are a very large topic and deserve an article
  dedicated to them.
categories:
  - Coding
  - Frameworks
  - JavaScript
---
In the first part of this series, we discussed <a href="https://www.smashingmagazine.com/2013/02/11/introduction-backbone-marionette/">Backbone.Marionette’s <code>Application</code></a>. This time around, we’ll discuss the module system that is included in Backbone.Marionette. Modules are accessible through the <code>Application</code>, but modules are a very large topic and deserve an article dedicated to them.</p>

## What Are Modules?

Before we get into the details of how to use Marionette’s module system, we should make sure we all have a decent definition of a module. A module is <strong>an independent unit of code that ideally does one thing</strong>. It can be used in conjunction with other modules to create an entire system. The more independent a unit of code is, the more easily it can be exchanged or internally modified without affecting other parts of the system.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">A Thorough Introduction To Backbone.Marionette (Part 1)</span>](https://www.smashingmagazine.com/2013/02/introduction-backbone-marionette/)
*   [A Thorough Introduction To Backbone.Marionette (Part 3)](https://www.smashingmagazine.com/2014/06/thorough-introduction-backbone-marionette-part-3/)
*   [Backbone.js Tips And Patterns](https://www.smashingmagazine.com/2013/08/backbone-js-tips-patterns/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)

{{% feature-panel %}}

For this article, that’s about as much as we need to define modules, but if you want to learn more about writing modular code, plenty of resources are on the Internet, of which the “<a href="https://singlepageappbook.com/maintainability1.html">Maintainability Depends on Modularity</a>” chapter of <em>Single Page Apps in Depth</em> is one of the better ones out there.

The JavaScript language doesn’t currently have any built-in methods for defining modules (the <a href="https://wiki.ecmascript.org/doku.php?id=harmony:modules">next version should change that</a>), but many libraries have arisen to provide support for defining and loading modules. Marionette’s module system, sadly, doesn’t provide support for loading modules from other files, but it does offer some functionality that other module systems do not have, such as the ability to start and stop a module. We’ll cover more of that later. Right now, we will just start with defining a module.</p>

## Module Definition

Let’s start with the most basic of module definitions. As mentioned, modules are accessible through the <code>Application</code>, so we need to instantiate one of those. Then we can use its <code>module</code> method to define a module.

<pre><code class="language-javascript">
var App = new Backbone.Marionette.Application();

var myModule = App.module(‘myModule’);
</code></pre>

That’s pretty simple, right? Well, it is, but that’s the simplest module we can create. What exactly did we create, though? Essentially, we told the application that we want a barebones module, with no functionality added by us, and that it will be named <code>myModule</code> (according to the argument we passed into <code>module</code>). But what is a barebones module? It’s an instantiation of a <code>Marionette.Module</code> object.

<code>Module</code> comes with a bit of functionality baked in, such as events (through <code>EventAggregator</code>, which we’ll discuss thoroughly in a later article), starting with initializers (just like <code>Application</code> has), and stopping with finalizers (we’ll go over that in the “Starting and Stopping Modules” section).</p>

### Standard Module Definition

Now let’s look at how to define a module with some of our own functionality.

<pre><code class="language-javascript">
App.module("myModule", function(myModule, App, Backbone, Marionette, $, _){
    // Private Data And Functions
    var privateData = "this is private data";

    var privateFunction = function(){
        console.log(privateData);
    }

    // Public Data And Functions
    myModule.someData = "public data";

    myModule.someFunction = function(){
        privateFunction();
        console.log(myModule.someData);
    }
});
</code></pre>

As you can see, there’s a lot of stuff in there. Let’s look at the top line and work our way down. Just like before, we call <code>App.module</code> and provide a name for the module. But now we’re also passing a function in, too. The function is passed several arguments. I bet you can figure out what they are, based on the names I’ve given them, but I’ll still explain them all:

*   myModule is the very module you’re trying to create. Remember, it’s already created for you, and it’s a new instance of `Module`. You’re probably going to want to extend this with some new properties or methods; otherwise, you might as well stick with the short syntax that doesn’t require you to pass in a function.
*   `App` is the `Application` object that you called `module` on.
*   `Backbone` is, of course, the reference to the Backbone library.
*   `Marionette` is the reference to the Backbone.Marionette library. It is actually available through `Backbone`, but this allows you to alias it and make it a shorter name.
*   `$` is your DOM library, which will be either jQuery or Zepto (or possibly something else in the future).
*   `_` is a reference to Underscore or Lodash, whichever you’re using.

After that, you can actually pass in and use custom arguments. We’ll go over this in a bit.

Normally, I would say that most of these arguments are unnecessary; after all, why wouldn’t you already have access to these references? However, I could see these being useful in a couple of situations:

*   A minifier can shorten the names of the arguments, saving some bytes.
*   If you’re using RequireJS or some other module loader, you only need to pull in the `Application` object as a dependency. The rest will be available through the arguments given to you by `Module`.

Anyway, let’s get back to explaining the rest of what’s going on in the code above. Inside the function, you can utilize the closure to create private variables and functions, which is what we’ve done. You can also expose data and functions publicly by adding them as properties of <code>myModule</code>. This is how we create and extend our module. There is no need to return anything because the module will be accessible directly through <code>App</code>, as I’ll explain in the “Accessing a Module” section below.

<strong>Note:</strong> Make sure that you only try to add properties to your <code>module</code> variable and do not set it equal to something (for example, <code>myModule = {…}</code>), because when you set your <code>module</code> variable to something, that changes what the variable’s name is referencing, and none of the changes you specify will show up in your module later.

Earlier, I noted that you can send in custom arguments. In fact, you can send in as many custom arguments as you want. Take a look at the code below to see how it’s done.

<pre><code class="language-javascript">
App.module("myModule", function(myModule, App, Backbone, Marionette, $, _, customArg1, customArg2){
    // Create Your Module
}, customArg1, customArg2);
</code></pre>

As you can see, if you pass additional arguments to <code>module</code>, it will pass those in to the function that you are defining your module in. Once again, <strong>the biggest benefit I see from this is saving some bytes after minification</strong>; other than that, I don’t see much value.

Another thing to note is that the <code>this</code> keyword is available within the function and actually refers to the module. This means you don’t even need the first argument, but you would lose the advantage of minification if you didn’t use the argument. Let’s rewrite that first code using <code>this</code> so that you can see that it’s exactly the same as <code>myModule</code>.

<pre><code class="language-javascript">
App.module("myModule", function(){
    // Private Data And Functions
    var privateData = "this is private data";

    var privateFunction = function(){
        console.log(privateData);
    }

    // Public Data And Functions
    this.someData = "public data";

    this.someFunction = function(){
        privateFunction();
        console.log(this.someData);
    }
});
</code></pre>

As you can see, because I’m not using any of the arguments, I decided not to list any of them this time. It should also be obvious that you can skip the first argument and just use <code>this</code>.</p>

### Split Definitions

The final thing I’ll mention about defining modules is that we can split up the definitions. I don’t know exactly why you would want to do this, but someone might want to extend your modules later, so splitting up the definitions might help them avoid touching your original code. Here’s an example of split definitions:

<pre><code class="language-javascript">
// File 1
App.module("myModule", function(){
    this.someData = "public data";
});

// File 2
App.module("myModule", function(){
    // Private Data And Functions
    var privateData = "this is private data";

    var privateFunction = function(){
        console.log(privateData);
    }

    this.someFunction = function(){
        privateFunction();
        console.log(this.someData);
    }
});
</code></pre>

This gives us the same result as the previous definition, but it’s split up. This works because in <code>File 2</code>, the module that we defined in <code>File 1</code> is being given to us (assuming that <code>File 1</code> was run before <code>File 2</code>). Of course, if you’re trying to access a private variable or function, it has to be defined in the module definition where it is used because it’s only available within the closure where it is defined.</p>

## Accessing A Module

What good is creating modules if we can’t access them? We need to be able to access them in order to use them. Well, in the very first code snippet of this article, you saw that when I called <code>module</code>, I assigned its return value to a variable. That’s because we use the very same method to both define <em>and</em> retrieve modules.

<pre><code class="language-javascript">
var myModule = App.module("myModule");
</code></pre>

Normally, if you’re just trying to retrieve the module, you’ll pass in the first argument, and <code>module</code> will go out and grab that module for you. But if you pass in a function as the second argument, the module will be augmented with your new functionality, <em>and</em> it will still return your newly created or modified module. This means you can define your module and retrieve it all with a single method call.

This isn’t the only way to retrieve modules, though. When a module is created, it is attached directly to the <code>Application</code> object that it was constructed with. This means you can also use the normal dot notation to access your module; but this time, it <em>must</em> be defined beforehand, otherwise you’ll get <code>undefined</code> back.

<pre><code class="language-javascript">
// Works but I don't recommend it
var myModule = App.myModule;
</code></pre>

While this syntax is shorter, it doesn’t convey the same meaning to other developers. I would recommend using <code>module</code> to access your modules so that it is obvious you are accessing a module and not some other property of <code>App</code>. The convenience and danger here is that it will create the module if it doesn’t already exist. The danger comes if you misspell the name of the module; you won’t have any way of knowing that you didn’t get the correct module until you try to access a property on it that doesn’t exist.</p>

## Submodules

Modules can also have submodules. Sadly, <code>Module</code> doesn’t have its own <code>module</code> method, so you can’t add submodules to it directly, but that won’t stop us. Instead, to create submodules, you call <code>module</code> on <code>App</code>, just like you used to do; but for the name of the module, you need to put a dot (<code>.</code>) after the parent module’s name and then put the name of the submodule.

<pre><code class="language-javascript">
App.module('myModule.newModule', function(){
    ...
});
</code></pre>

By using the dot separator in the module’s name, Marionette knows that it should be creating a module as a submodule of the module before the dot. The cool (and potentially dangerous) part is that if the parent module isn’t created at the time that you call this, it will create it along with its submodule. This can be dangerous because of the same potential for misspelling that I mentioned earlier. You could end up creating a module that you didn’t intend to create, and the submodule would be attached to it, instead of to the module you intended.</p>

### Accessing Submodules

As before, submodules can be accessed the very same way they are defined, or you can access them as properties of the module.

<pre><code class="language-javascript">
// These all work. The first example is recommended
var newModule = App.module('myModule.newModule');
var newModule = App.module('myModule').newModule;
var newModule = App.myModule.newModule;

// These don't work. Modules don't have a 'module' function
var newModule = App.myModule.module('newModule');
var newModule = App.module('myModule').module('newModule');
</code></pre>

Any of these methods of accessing the submodule will work equally well if both the module and submodule have already been created.</p>

## Starting And Stopping Modules

If you read the previous article in the series, about <code>Application</code>, you will know that you can start an <code>Application</code> with <code>start</code>. Well, starting modules is the same, and they can also be stopped with <code>stop</code>.

If you recall (assuming you’ve read the previous article), you can add initializers with <code>addInitializer</code> to an <code>Application</code>, and they will be run when it is started (or will run immediately if the <code>Application</code> has already started). A few other things happen when you start an <code>Application</code>. Here are all of the events, in order:

*   fires the `initialize:before` event,
*   starts all of the defined modules,
*   runs all of the initializers in the order they were added,
*   fires the `initialize:after` event,
*   fires the `start` event.

A <code>Module</code> behaves in a very similar way. The number of events and some of the names of the events are different, but overall it is the same process. When a module is started, it:

*   fires the `before:start` event,
*   starts all of its defined submodules,
*   runs all of its initializers in the order they were added,
*   fires the `start` event.

The <code>stop</code> method is also very similar. Instead of adding initializers, though, you need to add finalizers. You do this with <code>addFinalizer</code> and by passing in a function to run when <code>stop</code> is called. Unlike with initializers, no data or options are passed along to each of the functions. When <code>stop</code> is called, it:

*   fires the `before:stop` event,
*   stops its submodules,
*   runs its finalizers in the order they were added,
*   fires the `stop` event.

<strong>Initializers and finalizers aren’t only meant for use by others.</strong> In fact, they are quite helpful when used inside the module definition. This way, you can define a module inside the definition without actually creating any objects to be used, but then write your initializers to start creating the objects and setting them up, such as in the example below.

<pre><code class="language-javascript">
App.module("myModule", function(myModule){
    myModule.startWithParent = false;

    var UsefulClass = function() {...}; // Constructor definition
    UsefulClass.prototype ... // Finish defining UsefulClass
    ...

    myModule.addInitializer(function() {
        myModule.useful = new UsefulClass();
        // More setup
    });

    myModule.addFinalizer(function() {
        myModule.useful = null;
        // More tear down
    });
});
</code></pre>

### Automatic And Manual Starting

When a module is defined, by default it will automatically start at the same time that its parent starts (either the root <code>Application</code> object or a parent module). If a module is defined on a parent that has already started, it will start immediately.

You can set up a module to not start automatically by changing its definition in one of two ways. Inside the definition, you can set a module’s <code>startWithParent</code> property to <code>false</code>, or you can pass an object (instead of a function) to <code>module</code> that has a <code>startWithParent</code> property set to <code>false</code> and a <code>define</code> property to replace the normal function.

<pre><code class="language-javascript">
// Set 'startWithParent' inside function
App.module("myModule", function(){
    // Assign 'startWithParent' to false
    this.startWithParent = false;
});

// -- or --

// Pass in object
App.module("myModule", {
    startWithParent: false,

    define: function(){
        // Define module here
    }
});

App.start();

// myModule wasn't started, so we need to do it manually
App.module('myModule').start("Data that will be passed along");
</code></pre>

Now the module won’t autostart. You must call <code>start</code> manually to start it, as I did in the example above. The data that is passed to <code>start</code> could be anything of any type, and it will be passed along to the submodules when they’re started, to the initializers, and to the <code>before:start</code> and <code>start</code> events.

As I said, data isn’t passed along like this when you call <code>stop</code>. Also, <code>stop</code> <em>must</em> be called manually, and it will always call <code>stop</code> on submodules; there is no way around this. This makes sense because a submodule shouldn’t be running when its parent isn’t running, although there are cases when a submodule should be off when its parent is running.</p>

## Other Events And Built-In Functionality

I mentioned that <code>Module</code> comes with some baked-in functionality, such as the <code>EventAggregator</code>. As discussed, we can use the <code>on</code> method on a module to watch for events related to starting and stopping. That’s not all. There are no other built-in events, but a module can define and trigger their own events. Take a look:

<pre><code class="language-javascript">
App.module('myModule', function(myModule) {
    myModule.doSomething = function() {
        // Do some stuff
        myModule.trigger('something happened', randomData);
    }
});
</code></pre>

Now, whenever we call <code>doSomething</code> on the module, it will trigger the <code>something happened</code> event, which you can subscribe to:

<pre><code class="language-javascript">
App.module('myModule').on('something happened', function(data) {
    // Whatever arguments were passed to `trigger` after the name of the event will show up as arguments to this function
    // Do something with `data`
});
</code></pre>

This is very similar to the way we do things with events on collections, models and views in normal Backbone code.</p>

## How We Might Actually Use A Module

The modules in Marionette can definitely be used to define modules very similarly to any other module definition library, but that’s actually not how it was designed to be used. The built-in <code>start</code> and <code>stop</code> methods are an indication of this. The modules that Marionette includes are meant to represent somewhat <em>large</em> subsystems of an application. For example, <strong>let’s look at Gmail</strong>.

Gmail is a single application that actually contains several smaller applications: email client, chat client, phone client and contact manager. Each of these is independent — it can exist on its own — but they are all within the same application and are able to interact with one another. When we first start up Gmail, the contact manager isn’t up, and neither is the chat window. If we were to represent this with a Marionette application, each of those sub-applications would be a module. When a user clicks the button to open the contact manager, we would stop the email application (because it becomes hidden — although, for speed, we could keep it running and just make sure it doesn’t show in the DOM) and start the contacts manager.

Another example would be an application built largely out of widgets. Each widget would be a module that you can start and stop in order to show or hide it. This would be like a customizable dashboard such as iGoogle or the dashboard in the back end of WordPress.

Of course, we’re not limited to using Marionette’s modules in this way, although it’s difficult to use it in the traditional sense. This is because Marionette’s modules are fully instantiated objects, while traditional modules are “classes” that are meant for instantiation later.</p>

## Conclusion

Phew! That’s a lot of information. If you’ve made it this far, I commend you (although it was much easier for you to read this than for me to write it). Anyway, I hope you’ve learned a lot about the way that Marionette handles defining, accessing, starting and stopping modules and submodules. You may find it to be a very handy tool, or you might choose to completely ignore its existence. That’s one of the great things about Backbone and Marionette: most of their features are largely independent, so you can pick and choose what you want to use.

<em>Credits of image on front page: <a href="https://www.flickr.com/photos/ruiwen/3260094840/">ruiwen</a></em>

<em>(al) (ea)</em>

