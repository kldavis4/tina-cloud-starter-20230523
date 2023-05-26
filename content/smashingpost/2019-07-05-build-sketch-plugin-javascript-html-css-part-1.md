---
title: 'How To Build A Sketch Plugin With JavaScript, HTML And CSS (Part 1)'
slug: build-sketch-plugin-javascript-html-css-part-1
author: matt-curtis
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939e8d32-ba10-4f93-bd82-7edd941d7b21/interface-components-illustration.png
date: 2019-07-05T12:30:59+02:00
summary: >-
  If you’ve ever worked with Sketch, the odds are that there have been plenty of moments when you’ve thought, “If only Sketch could do this one particular thing, I’d be able to accomplish the task at hand much faster, easier, and better.” Well, fret no longer! In this two-part article, you’ll learn how to build your our own Sketch plugins from scratch &mdash; giving you the skills needed to solve exactly these kinds of problems.
description: >-
  In this two-part article, you’ll learn how to build your our own Sketch plugins from scratch &mdash; giving you the skills needed to accomplish tasks much faster, easier, and better.
categories:
  - Sketch
  - JavaScript
  - HTML
  - CSS
---
This tutorial is intended for people who know and use the Sketch app and are not afraid of dabbling with code. To profit from it the most, you will need to have at least some basic experience writing JavaScript (and, optionally, HTML/CSS).

The plugin we’ll be creating is called “Mosaic”. In part one, we’ll learn about the basic files that make up a Sketch plugin; we’ll write some JavaScript and create a user interface for our plugin with the help of some HTML and CSS. The next article will be about how to connect the user interface to the core plugin code, how to implement the plugin’s main features, and at the end of it, you will also learn how to optimize the code and the way the plugin works.

I’ll also be sharing the plugin’s code (JS, HTML, CSS) and files which you’ll be able to examine and use for learning purposes.

## What Are Sketch Plugins, And How Do They Work?

In Sketch, plugins are a way to add features and functionality that aren’t present in Sketch “out of the box.” Considering that there’s almost always going to be some missing feature or integration in any given program (especially given the vast number of needs any individual designer might have!), one can begin to imagine how plugins might be especially useful and powerful. Sketch plugins are able to do pretty much everything you'd expect, like manipulating the color, shape, size, order, style, grouping, and effects of layers, but also able to do things like make requests to internet resources, present a user interface, and much, much more!

On the programming side, all Sketch plugins are written in JavaScript code. Well, actually, that’s not *entirely* true. It’s more accurate to say that *most* Sketch plugins are written in JavaScript, as it’s also possible to write a Sketch plugin in one of Apple’s programming languages, [Objective-C](https://en.wikipedia.org/wiki/Objective-C) and [Swift](https://developer.apple.com/swift/), though even they require a small amount of JavaScript knowledge.

Don’t worry though. In this article, we’ll focus on how to build Sketch plugins using JavaScript, HTML, and CSS *alone*. We won’t be going over the basics of HTML, CSS, or JavaScript &mdash; this article assumes at least some knowledge and experience with all of these three. The MDN developer website provides a great place to [learn more about web development](https://developer.mozilla.org/en-US/docs/Learn).

{{% feature-panel %}}

## Let’s Get Started!

### Firstly, What Are We Making?

In this tutorial, I’ll teach you how to build a basic, beginner-friendly plugin that will be able to create, duplicate, and modify layers, as well as present the user with a nice user interface. By doing so, my goal is to establish a fundamental knowledge on which you can build on and use it to create your own plugins.

The plugin we’ll be building is called *Mosaic,* and is effectively a “pattern generator”. Feed it your layers, tweak a few settings, and it’ll create a pattern:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cd14d15-fa84-48ee-b2d4-24f3aee88efc/ui-pattern-examples.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cd14d15-fa84-48ee-b2d4-24f3aee88efc/ui-pattern-examples.png" sizes="100vw" caption="The Mosaic’s UI, and some examples of patterns made with it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cd14d15-fa84-48ee-b2d4-24f3aee88efc/ui-pattern-examples.png'>Large preview</a>)" alt="Image showing the Mosaic plugin’s UI, and a few example patterns." >}}

If you’d like to install and play around with Mosaic, you can [download the completed plugin](https://github.com/matt-curtis/mosaic) from GitHub.

A bit of history: Mosaic is inspired in large part by an old-school [Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/) plugin called *Twist-and-Fade*. Twist-and-Fade was pretty powerful, able to duplicate a layer any number of times while adjusting its hue, position, rotation, size, and opacity. The plugin was even able to generate animated GIFs, like [this one](https://dribbble.com/shots/147212-Tape-Cassette-Rotating), where it created the frames for the two rotating elements in the cassette tape: 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f825bbf-7a61-4252-8f0c-5df7f7ac1eec/spinning-cassette.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f825bbf-7a61-4252-8f0c-5df7f7ac1eec/spinning-cassette.gif" width="400" height="300" alt="Image showing a music cassette tape with rotating drums" /></a><figcaption>Animated cassette tape (<a href="https://dribbble.com/shots/147212-Tape-Cassette-Rotating">source</a>). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f825bbf-7a61-4252-8f0c-5df7f7ac1eec/spinning-cassette.gif">Large preview</a>)</figcaption></figure>

(Here’s a [video demoing Twist and Fade](https://www.youtube.com/watch?v=VPQIZ_Pz-II&feature=youtu.be&t=161) if you’re interested in seeing exactly how it worked.)

For the purposes of this tutorial, we’ll be building a somewhat similar plugin for Sketch, though intentionally simplified so as to keep the tutorial as accessible as possible. Specifically, our plugin will be able to:

- Duplicate any Sketch layer (bitmap or vector) and tweak the duplicates’ layer’s position, rotation, and opacity. This will give us an introduction to manipulating layers using [Sketch’s JavaScript APIs](https://developer.sketch.com/reference/api/).
- Display a user interface created using HTML, CSS, and JS, which will teach you about how to easily create an interface for the plugin, by using web technologies that you may already be familiar with. The plugin interface is pretty important since it’s how we’ll gather the user’s inputs regarding how the user wants the resulting mosaic image to look.

{{% ad-panel-leaderboard %}}

### Creating Our Base Plugin In Ten Seconds Flat

First, we’ll be creating the “base” (or template) for the plugin we want to build. We could create all the necessary files and folders that make up a plugin manually, but luckily we don’t have to &mdash; because Sketch can do it for us. After we’ve generated the template plugin, we’ll be able to customize it as we see fit.

There’s a really quick and easy technique we can use to create the template plugin, which is pretty much my go-to method when I need to whip a plugin together to solve whatever problem I’m dealing with at a given moment. Here’s how it works:

With Sketch open, check the menu bar at the top of the screen and click `Plugins -> Run Script`. This will open up a dialog box that we can use to test and run the code. We can also save any code we enter in it as a plugin, which is the part we’re specifically interested in right now.

Clear whatever code is already in this dialog and replace it with the following demo code:

<div class="break-out">

<pre><code class="language-css">const UI = require("sketch/ui");

UI.message("😍 Hey there, you fantastic plugin developer you! This is your plugin! Talking to you from the digital computer screen! In Sketch! Simply stupendous!");
</code></pre>
</div>
    
Next, hit `Save Script as Plugin` in the bottom-left of the window, enter whatever name you'd like for this plugin to have (in our case, this is "Mosaic"), then `Save Script as Plugin` once more.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c8a601d-502d-4d77-b3e2-41ad987b67ad/sketch-plugin-save-name.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c8a601d-502d-4d77-b3e2-41ad987b67ad/sketch-plugin-save-name.gif" width="668" height="518" alt="" /></a><figcaption>Press “Save” in the bottom-left of the window and enter whatever name you'd like for this plugin to have. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c8a601d-502d-4d77-b3e2-41ad987b67ad/sketch-plugin-save-name.gif">Large preview</a>)</figcaption></figure>

Believe it or not, we’re already done &mdash; all that’s left is to eat the cake we just baked. Here comes the fun part. Opening the Plugins menu once again, you should see something like this: your brand-spanking-new plugin listed as "Mosaic"! Click on it!

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be732542-f333-4e5f-8245-8f724afcc6a1/hello-world-tooltip.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be732542-f333-4e5f-8245-8f724afcc6a1/hello-world-tooltip.gif" width="960" height="90" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be732542-f333-4e5f-8245-8f724afcc6a1/hello-world-tooltip.gif">Large preview</a>)</figcaption></figure>

Congratulations, you’ve just written your first Sketch plugin!

What you should see after clicking “Mosaic” should be like the short video above, with an unobtrusive tooltip message appearing at the bottom of the screen beginning with the words "Hey there..." &mdash; which is exactly what the code we pasted in tells it to do. This is what it makes this technique so great: it makes it **easy to paste, modify and test code without having to build a plugin from scratch.** If you’re familiar with or have ever played with your browser’s web console, this is basically that. Having this tool in your back pocket as you build and test code is a must-have.

Let’s do a quick rundown of what the code you added does:

First, it imports the [`sketch/ui`](https://developer.sketchapp.com/reference/api/#ui) [module](https://developer.sketchapp.com/reference/api/#ui) of [Sketch’s built-in JS library](https://github.com/BohemianCoding/SketchAPI), and assigns it to the `UI` variable. This module contains a couple of useful interface-related methods, one of which we’ll use:

<pre><code class="language-javascript">const UI = require("sketch/ui");
</code></pre>

Next, it calls the `message` method (which is part of the `sketch/ui`  module) with the string of text we want displayed in the tooltip we saw:

<div class="break-out">

<pre><code class="language-css">UI.message("😍 Hey there, you fantastic plugin developer you! This is your plugin! Talking to you from the digital computer screen! In Sketch! Simply stupendous!");
</code></pre>
</div>

The `message()` method provides a great way to present an unobtrusive message to the user; it’s great for cases where you don’t need to steal focus (non-modal) and don’t need any fancy buttons or text fields. There’s also other ways to [present common UI elements](https://developer.sketchapp.com/reference/api/#ui) like alerts, prompts, and such, some of which we’ll be using as we build Mosaic.

### Customizing Our Plugin’s Metadata

We now have a basic plugin to start from, but we still need to tweak it further and make it truly ours. Our next step will be to change the plugin’s metadata.

For this step, we’ll need to peek into what’s called the *plugin bundle*. When you hit save in the 'Run Script' window, Sketch saved your plugin as a folder named `Mosaic.sketchplugin` that you can find in the
`~/Library/Application Support/com.bohemiancoding.sketch3/Plugins` directory. That’s a bit long and annoying to remember; as a shortcut, you can also pull it up via `Plugins -> Manage Plugins -> (right-click your plugin) -> Reveal Plugins Folder`. Even though it appears in Finder as a single file, it’s actually a folder containing everything our plugin needs for Sketch to run it. The reason it appears as a single file *despite* being a folder is because when you first installed Sketch, Sketch registered the `.sketchplugin` extension as a "bundle" (a special kind of folder that appears as a file) and asked for it to automatically open in Sketch when opened.

Let’s take a peek inside. Right-click `Mosaic.sketchplugin`, then click "Show Package Contents". Inside, you should see the following directory structure:

<pre><code class="language-javascript">Contents/
└ Resources/
└ Sketch/
  └ manifest.json
  └ script.cocoascript
</code></pre>

You might be wondering why there’s a file in there with the extension `.cocoascript`. Don’t worry &mdash; it’s just a regular JavaScript file, and only contains the code we entered earlier. Go ahead and rename this file to `index.js`, which will change the directory structure to look like the one below:

<pre><code class="language-javascript">Contents/
└ Resources/
└ Sketch/
  └ manifest.json
  └ index.js
</code></pre>    

The most common way of organizing the files inside a plugin bundle is as follows: your code (JavaScript) and `manifest.json` belong in `Sketch/`, and resources (think images, audio files, text files, etc.) belong in `Resources/`.

Let’s start by tweaking the file named `manifest.json`. Open it inside your favorite code editor, such as [Visual Studio Code](https://code.visualstudio.com/) or [Atom](https://atom.io/).

You’ll see that at the moment there’s relatively little inside here, but we’ll add more soon. The plugin manifest serves primarily two purposes:

1. First, it provides metadata that describes the plugin to the user — things like its name, version, the author’s name, and so on. Sketch uses this information in the `Sketch -> Preferences -> Plugins` dialog to create a listing and description for your plugin.
2. Second, it also tells Sketch about how to get down to your business; that is, it tells Sketch how you'd like your plugin’s menu to look, what hotkeys to assign to your plugin, and where your plugin’s code lives (so Sketch can run it).

Considering purpose #1, describing the plugin to the user, you’ll probably notice that right now there’s no description *or* author given, which would be confusing for the user and make the plugin difficult to identify. Let’s fix that by adjusting the relevant keys' values to:

<div class="break-out">

<pre><code class="language-css">{
        "description": "Generate awesome designs and repeating patterns from your layers!",
        "author": "=> Your name here <="
}
</code></pre>
</div>

Next, let’s adjust the plugin’s identifier. This identifier uses what is called a "reverse domain notation" which is a really concise (or boring, take your pick) way to say "take your site’s domain, reverse the order, then put your product’s name at the end." This will come out something like: `com.your-company-or-your-name-its-not-that-big-a-deal.yourproduct`. 

You don’t have to stick to this naming convention &mdash; you can put whatever you want here, so long as it’s unique enough to avoid conflicts with other plugins (though it’s *probably* a good idea to stick to the RDN format, especially as it provides a simple, reusable system for your plugin identifiers).

To that effect, change your identifier to `com.your-name.mosaic`:

<pre><code class="language-css">{
    "identifier": "com.your-name.mosaic"
}
</code></pre>

I personally like to take all metadata related keys (title, author, identifier, etc.) and group them near the top of the manifest so they’re not spread out all over the place and help preserve my sanity when I need to find them.

Next, let’s take a look at the `menu` and `commands` keys. These two are responsible for telling Sketch what code to call and in response to what.

If you look at the `menu` key, you’ll see it contains a `title` key, whose value is the name our plugin will show up with in the `Plugins` menu. It also has an `items` key, which is a list of *command identifiers*:

<pre><code class="language-css">{
  "menu": {
    "title": "Mosaic",
    "items": [
        "com.bohemiancoding.sketch.runscriptidentifier"
    ]
  }
}
</code></pre>

Right now there’s only one command identifier in this list, `"com.bohemiancoding.sketch.runscriptidentifier"`. Command identifiers always point to a command in the `commands` list. Right now our plugin only has one command, which is the one with this identifier:

<pre><code class="language-css">{
  "commands": [
    {
      "script" : "script.cocoascript",
      "name" : "Mosaic",
      "handlers" : {
              "run" : "onRun"
      },
      "identifier" : "com.bohemiancoding.sketch.runscriptidentifier"
    }
  ]
}
</code></pre>

Whenever you add a command identifier to a `menu` entry, Sketch will look up the command entry that has that identifier and will display the value of its `name` key (which in this case is “Mosaic”) and will show it in your plugin’s menu instead of the identifier.

As for the role commands play, we can think of a command entry as a way to tell Sketch what function in our plugin’s JavaScript code we want to run when that command is invoked, the “invocation” usually being the user’s click on the associated menu item. The command entry doesn’t do anything on its own, it’s just JSON &mdash; it simply provides a *description* to Sketch of where to look for the JavaScript it needs to run when the command is invoked.

So far, we’ve talked about what a command’s `name` and `identifier` keys do, but there are two other keys in a command that need to be addressed: `script` and `handlers`.

The `script` key tells Sketch where the JavaScript file that it should run is. Note how Sketch assumes that the script file in question is in the `Sketch/` folder, which is why for simplicity’s sake you’ll want to make sure all your JavaScript code lives somewhere under the `Sketch/` folder. Before we move on from this key **it’s important** that you make sure you change this key’s value to `index.js`, just like we renamed the file earlier. Otherwise, Sketch won’t be able to find and run your JavaScript file.

The value of the `handlers` key is what Sketch looks at to determine what function in your JavaScript to call. Here, we only have one handler set: `run`, with the value `onRun`. `run` is the name of a predefined, built-in Sketch **action**. This `run`  action will always be called when a user clicks a menu item that references this command. `onRun` is the **name** of a function in the auto-generated `script.cocoascript` file (which we renamed to `index.js`), and the function we want to be called when the `run`  event occurs, i.e., when the user clicks the menu item.

{{% ad-panel-leaderboard %}}

In the example we have so far, this process plays out something like this:

1. The user clicks our menu item.
2. Sketch finds the command associated with that menu item.
3. Sketch finds the script file the command refers to and runs it (which in this case means it executes the JavaScript in `index.js`).
4. Since this command was invoked by a menu item click, it’s considered a `run` action. That means Sketch will look at the command’s `handlers.run` value for the function to call next, which in this case is `onRun`.
5. Sketch calls the `onRun` function.

Commands are most commonly called in response to a user clicking on one of your menu items, but they can also be called in response to other user actions, such as the user changing the selection or a property on a layer. However, for this plugin, we won’t be using any of these other actions. (You can learn more about actions and how they work in the [Action API](https://developer.sketch.com/plugins/actions) help page.)

Before we move on from this manifest, we’ll want to make two other tweaks. Right now, our menu has the structure:

<pre><code class="language-javascript">Mosaic
└ Mosaic
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9271bfb2-04e9-455c-8d79-daa080625b34/redundant-plugin-menu.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9271bfb2-04e9-455c-8d79-daa080625b34/redundant-plugin-menu.png" sizes="100vw" caption="Pretty redundant, right? (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9271bfb2-04e9-455c-8d79-daa080625b34/redundant-plugin-menu.png'>Large preview</a>)" alt="Image showing Mosaic menu item redundantly nested inside another menu named Mosaic" >}}

…which is a bit redundant since our plugin only has one menu item. It also adds a bit of unnecessary friction for our user as our plugin now takes two clicks to invoke rather than one. We can fix this by adding `isRoot: true` to our `menu`:

<pre><code class="language-css">{
  "menu": {
    "title" : "Mosaic",
    "items" : [
            "com.bohemiancoding.sketch.runscriptidentifier"
    ],
    "isRoot": true
}
}
</code></pre>

This tells Sketch to place the first level of menu items directly under the `Plugins` menu, rather than nesting them under the menu’s `title`.

Hit save and return to Sketch. You should see that now `Mosaic -> Mosaic` has been replaced by just `Mosaic` &mdash; perfect!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/303674a2-f96b-42cb-9aa4-05c5d51da78c/non-redudant-plugin-menu.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/303674a2-f96b-42cb-9aa4-05c5d51da78c/non-redudant-plugin-menu.png" sizes="100vw" caption="Mosaic’s UI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/303674a2-f96b-42cb-9aa4-05c5d51da78c/non-redudant-plugin-menu.png'>Large preview</a>)" alt="Image showing the Mosaic plugin’s UI" >}}

As for our second tweak, let’s go ahead and rename this command identifier to something less unwieldy. Since command identifiers only need to be unique within the context of an individual plugin, we can safely rename it to something more concise and obvious, like `"open"`:

<pre><code class="language-css">{
  "commands": [
    {
            ...
            "identifier" : "open"
    }
],

"menu": {
    ...
    "items" : [
            "open"
    ]
  }
}
</code></pre>

Before we move on, it’s useful to note that menus can contain also other menus. You could easily create a sub-menu by nesting another `{ title: ..., items: ... }` entry inside another menu’s `items` list:

<pre><code class="language-css">{
  "menu": {
    "title" : "Mosaic",
    "items" : [
      "open",
      {
        "title" : "I'm a sub-menu!",
        "items" : [
                "another-command-identifier"
        ]
      }
    ]
  }
}
</code></pre>

## Building The Plugin’s User Interface

So far, we’ve written some demo code and customized our plugin’s manifest. We’ll now move on to creating its user interface, which is essentially a web page embedded in a window (similarly to the browsers you’re familiar with using):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7787048a-2129-4888-b681-1bd72735084e/ui-window.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd705576-21ed-4ede-8c89-2bb55b4abce6/ui-window-800px.png" sizes="40vw" caption="The plugin’s window. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7787048a-2129-4888-b681-1bd72735084e/ui-window.png'>Large preview</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939e8d32-ba10-4f93-bd82-7edd941d7b21/interface-components-illustration.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939e8d32-ba10-4f93-bd82-7edd941d7b21/interface-components-illustration.png" sizes="100vw" caption="The components making up our plugin. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939e8d32-ba10-4f93-bd82-7edd941d7b21/interface-components-illustration.png'>Large preview</a>)" alt="Image showing the components making up our plugin’s interface: window and web view" >}}

### The Window

Mosaic’s user interface design has its own window, which we can consider the most basic component; we’ll start with it. In order to create and display a window, we’ll have to make use of a class that’s built into macOS by default, called [`NSWindow`](https://gist.github.com/matt-curtis/documentation). Over the remainder of this tutorial, we’ll actually be doing this quite a bit (using built-in APIs like `NSWindow`) which might seem a little daunting if you’re unfamiliar with it, but don’t worry &mdash; I’ll explain everything along the way!

**Note:** While we’re talking about built-in APIs, the reason we’re able to use this class *at all* is thanks to a [bridge](https://github.com/logancollins/Mocha) present in the JavaScript runtime used by Sketch plugins. This bridge automatically imports these built-in classes, methods, and functions that would normally only be available to native applications.

Open `Sketch/index.js` in your code editor, delete what’s already there, and paste in the following:

<div class="break-out">

<pre><code class="language-javascript">function onRun(context){
  const window = NSWindow.alloc().initWithContentRect_styleMask_backing_defer_(
    NSMakeRect(0, 0, 145, 500),
    NSWindowStyleMaskClosable | NSWindowStyleMaskTitled | NSWindowStyleMaskResizable,
    NSBackingStoreBuffered,
    false
  );

  window.releasedWhenClosed = false;

  window.makeKeyAndOrderFront(nil);
};
</code></pre>
</div>

Let’s take a look at what this first bit of code does:

<pre><code class="language-javascript">function onRun(context){
</code></pre>    

Remember earlier when we talked about commands and how they function, and we told Sketch to call in response to a menu-click was called `onRun`? (If you need a refresher, revisit that part above, then come back.) All this bit does is create that function. You’ll also notice our `onRun` function takes a `context` argument. This is an argument Sketch will call your command handlers with that can provide us with certain information. Later on, we’ll use it in order to get the URL of our plugin bundle on the user’s computer.

<div class="break-out">

<pre><code class="language-javascript">const window = NSWindow.alloc().initWithContentRect_styleMask_backing_defer(
  NSMakeRect(0, 0, 145, 500),
  NSWindowStyleMaskClosable | NSWindowStyleMaskTitled | NSWindowStyleMaskResizable,
  NSBackingStoreBuffered,
  false
);
</code></pre>
</div>

Here we’re actually doing a few things:


1. First, we call `alloc()` on `NSWindow`; this basically means "set aside some memory for an instance of NSWindow". It’s sufficient to know that you’ll have to do this for **every instance** of a native class you want to create. The [`alloc`](https://developer.apple.com/documentation/objectivec/nsobject/1571958-alloc?language=objc) method is available in every native class.
2. Next, we call `NSWindow`’s initializer method (that is, the method that actually creates an instance of `NSWindow`), which is named [`initWithContentRect:styleMask:backing:defer:`](https://developer.apple.com/documentation/appkit/nswindow/1419477-initwithcontentrect?language=objc). You’ll notice that’s different from what we call in our code above &mdash; it’s got a bunch of colons (`:`) between every argument. Since we can’t use that syntax in JavaScript, Sketch conveniently renames it to something we *can* actually use by replacing the colons with underscores, which is how we get its JS name: `initWithContentRect_styleMask_backing_defer`.
3. Next, we pass in each of the arguments the method needs. For the first argument, `contentRect`, we supply a rectangle with a size large enough for our user interface.
4. For `styleMask`, we use a [bitmask](https://codeburst.io/using-javascript-bitwise-operators-in-real-life-f551a731ff5) which says that we want our window to have a close button, a title bar, and to be resizable.
5. The next two arguments, `backing` and `defer`, are **always** going to be set to `NSBackingStoreBuffered` and `false`, so we don’t really need to worry about them. (The [documentation for this method](https://developer.apple.com/documentation/appkit/nswindow/1419477-initwithcontentrect?language=objc) goes into further detail as to why this is.)

<pre><code class="language-javascript">window.releasedWhenClosed = false;

window.makeKeyAndOrderFront(null);
</code></pre>
          
Here we set `NSWindow`’s [`releasedWhenClosed`](https://developer.apple.com/documentation/appkit/nswindow/1419062-releasedwhenclosed?language=objc) property to `false`, which means: "Hey! don’t delete this window from memory just because the user closes it." Then we call [`makeKeyAndOrderFront`](https://developer.apple.com/documentation/appkit/nswindow/1419208-makekeyandorderfront?language=objc)`(null)` which means: "Move this window to the forefront, and give it keyboard focus."

### Web View: The Interface

To make things easier, I’ve already written the HTML and CSS code of the plugin’s web user interface we’re going to be using; the only remaining code we’re going to have to add to it will deal with making sure we’re able to communicate between it and our Sketch plugin code. 

Next, [download the HTML and CSS code](https://smashingmagazine.com/provide/build-sketch-plugin-javascript-html-css-part-1.zip). Once you’ve downloaded it, extract it, then move the folder named "web-ui" into our plugin’s Resources folder.

**Note**: *Writing and optimizing the actual HTML/CSS code is outside of the scope of this tutorial, as its focus is on JavaScript which powers the plugin’s core features; but there are [a ton of tutorials on the web](https://www.google.com/search?q=HTML%2FCSS+for+user+interfaces) on this topic, should you want to learn more.*

If you run our plugin now, you’ll see that it shows a window &mdash; yay, progress! But it’s empty, without a title, and not particularly useful yet. We need to get it to show our web interface. In order to do that, we’ll need to use another native class, [`WKWebView`](https://developer.apple.com/documentation/webkit/wkwebview?language=objc), which is a view specifically made for displaying web content.

We’ll add the code needed to create our `WKWebView` beneath the code we wrote for our window:

<div class="break-out">

<pre><code class="language-javascript">function onRun(context){
    //        Create window

    const window = NSWindow.alloc().initWithContentRect_styleMask_backing_defer(
            NSMakeRect(0, 0, 145, 500),
            NSWindowStyleMaskClosable | NSWindowStyleMaskTitled | NSWindowStyleMaskResizable,
            NSBackingStoreBuffered,
            false
    );

    window.releasedWhenClosed = false;

    //        Create web view, and set it as the view for our window to display

    const webView = WKWebView.alloc().init();

    window.contentView = webView;

    //        Load our UI into the web view

    const webUIFolderURL = context.scriptURL
            .URLByDeletingLastPathComponent()
            .URLByAppendingPathComponent("../Resources/web-ui/");

    const indexURL = webUIFolderURL.URLByAppendingPathComponent("index.html");

    webView.loadFileURL_allowingReadAccessToURL(indexURL, webUIFolderURL);

    //        Make window key and move to front

    window.makeKeyAndOrderFront(nil);
};
</code></pre>
</div>

If we run our plugin now, we’ll see that now we’ve got a window open that displays our web user interface. Success!

Again, before moving on, let’s examine what the code we added does:

<pre><code class="language-javascript">const webView = WKWebView.alloc().init();
</code></pre>          

This should look familiar &mdash; it’s basically the same as what we did when we made our `NSWindow`: allocate memory for a web view, then initialize it.

<pre><code class="language-javascript">window.contentView = webView;
</code></pre>

This line of code tells our window to display the web view we just made.

<pre><code class="language-javascript">const webUIFolderURL = context.scriptURL
  .URLByDeletingLastPathComponent()
  .URLByAppendingPathComponent("../Resources/web-ui/");
</code></pre>

Here our goal is to create a URL that points to the `web-ui` folder that we made earlier. In order to get that URL, we need some way to figure out where our plugin’s bundle is in the user’s filesystem. Here we use the `context.scriptURL` property, which gives us the URL of the *currently running script*. However, this doesn’t give us a JavaScript `String` as you might expect, but an instance of a native class, [`NSURL`](https://developer.apple.com/documentation/foundation/nsurl?language=objc), that has a few methods on it that make manipulating URL strings easier.

We need to turn what `context.scriptURL` gives us &mdash; 

<pre><code class="language-javascript">file://path-to-your-plugin/Contents/Sketch/index.js
</code></pre>

&mdash; into:

<pre><code class="language-javascript">file://path-to-your-plugin/Contents/Resources/web-ui/
</code></pre>

Step by step:

1. Calling [`URLByDeletingLastPathComponent()`](https://developer.apple.com/documentation/foundation/nsurl/1411592-urlbydeletinglastpathcomponent?language=objc) the first time gives us `file://path-to-your-plugin/Contents/Sketch/`
1. Calling `URLByDeletingLastPathComponent()` again gives us `file://path-to-your-plugin/Contents/`
1. And lastly, adding `Resources/web-ui/` onto the end using [`URLByAppendingPathComponent`](https://developer.apple.com/documentation/foundation/nsurl/1410614-urlbyappendingpathcomponent?language=objc)`("Resources/web-ui/")` gives us `file://path-to-your-plugin/Contents/Resources/web-ui/`


We also need to create a second URL that points directly to the `index.html` file:

<div class="break-out">

<pre><code class="language-javascript">const indexURL = webUIFolderURL.URLByAppendingPathComponent("index.html");
</code></pre>          
</div>

Finally, we tell our web view to load `index.html` and give it access to the contents of the `web-ui` folder:

<div class="break-out">

<pre><code class="language-javascript">webView.loadFileURL_allowingReadAccessToURL(indexURL, webUIFolderURL);
</code></pre>
</div>

Alright. So far, we have a window that displays our web user interface, just like we wanted. However, it’s not quite yet complete &mdash; our original design doesn’t have a title bar (or “[chrome](https://en.wikipedia.org/wiki/Graphical_user_interface#User_interface_and_interaction_design)”), but our current window does. There’s also the fact that when we click inside a Sketch document, that document moves in front of our window, which isn’t what we want &mdash; we want the user to be able to interact with the plugin window *and* the Sketch document without having to constantly refocus from one window to the other.

To fix this, we first need to get rid of the default window chrome and keep only the buttons. Adding the two lines of code below will get rid of the title bar.

**Note:** *Like before, all of the properties and methods we’re using below are documented in [`NSWindow`](https://developer.apple.com/documentation/appkit/nswindow?language=objc)[’s documentation](https://developer.apple.com/documentation/appkit/nswindow?language=objc) page.*

<pre><code class="language-javascript">window.titlebarAppearsTransparent = true;
window.titleVisibility = NSWindowTitleHidden;
</code></pre>

These next two lines of code will remove the window buttons (also known as "traffic lights" in MacOS lingo) that we don’t need &mdash; “zoom” and “minimize” &mdash; leaving only the “close” button:

<div class="break-out">

<pre><code class="language-javascript">window.standardWindowButton(NSWindowZoomButton).hidden = true;
window.standardWindowButton(NSWindowMiniaturizeButton).hidden = true;
</code></pre>
</div>           

While we’re at it, let’s also go ahead and change the window’s background color to match that of our web UI:

<div class="break-out">

<pre><code class="language-javascript">window.backgroundColor = NSColor.colorWithRed_green_blue_alpha(1, 0.98, 0.98, 1);
</code></pre>
</div>

Next, we need to do something to keep our floating plugin window on top of other windows, so the user can interact with their Sketch documents without having to worry about the Mosaic’s window disappearing. We can use a special type of `NSWindow` for this, called `NSPanel`, which is able to “stay on top” of other windows. All that’s needed for this is to change `NSWindow` to [`NSPanel`](https://developer.apple.com/documentation/appkit/nspanel?language=objc), which is a single-line code change:

<div class="break-out">

<pre><code class="language-javascript">const window = NSPanel.alloc().initWithContentRect_styleMask_backing_defer(
</code></pre>
</div>
            
Now we tell our panel window to float (stay on top of all others), and only take keyboard/mouse focus when necessary:

<pre><code class="language-javascript">window.floatingPanel = true;
window.becomesKeyOnlyIfNeeded = true;
</code></pre>          

We can also tweak our window so that it automatically reopens in the last position it was at:

<pre><code class="language-javascript">window.frameAutosaveName = "mosaic-panel-frame";
</code></pre>

This line basically says "remember this window’s position by saving it with Sketch’s preferences under the key `mosaic-panel-frame`".

All together, we now have the following code:

<div class="break-out">

<pre><code class="language-javascript">function onRun(context){
    //        Create window

    const window = NSPanel.alloc().initWithContentRect_styleMask_backing_defer(
            NSMakeRect(0, 0, 145, 500),
            NSWindowStyleMaskClosable | NSWindowStyleMaskTitled | NSWindowStyleMaskResizable,
            NSBackingStoreBuffered,
            false
    );

    window.becomesKeyOnlyIfNeeded = true;
    window.floatingPanel = true;

    window.frameAutosaveName = "mosaic-panel-frame";

    window.releasedWhenClosed = false;

    window.standardWindowButton(NSWindowZoomButton).hidden = true;
    window.standardWindowButton(NSWindowMiniaturizeButton).hidden = true;

    window.titlebarAppearsTransparent = true;
    window.titleVisibility = NSWindowTitleHidden;

    window.backgroundColor = NSColor.colorWithRed_green_blue_alpha(1, 0.98, 0.98, 1);

    //        Create web view, and set it as the view for our window to display

    const webView = WKWebView.alloc().init();

    window.contentView = webView;

    //        Load our UI into the webview

    const webUIFolderURL = context.scriptURL
            .URLByDeletingLastPathComponent()
            .URLByAppendingPathComponent("../Resources/web-ui/");

    const indexURL = webUIFolderURL.URLByAppendingPathComponent("index.html");

    webView.loadFileURL_allowingReadAccessToURL(indexURL, webUIFolderURL);

    //        Make window key and move to front

    window.makeKeyAndOrderFront(nil);
};
</code></pre>
</div>

### Organizing The Code

Before we move to the next part, it’s a good idea to organize our code so that it’s easier to navigate and tweak. Since we still have a lot more code to add and we want to avoid `index.js` becoming a messy dumping ground for all of our code, let’s split things up a bit and move our UI-specific code into a file named `ui.js`, under the `Sketch` folder. We’ll also extract some of the UI tasks we do, like creating the web view and window, into their own functions.

Create a new file called `ui.js` and insert the code below inside it:

<div class="break-out">

<pre><code class="language-javascript">//        Private

var &#95;window;

function createWebView(pageURL){
        const webView = WKWebView.alloc().init();

        webView.loadFileURL&#95;allowingReadAccessToURL(pageURL, pageURL.URLByDeletingLastPathComponent());

        return webView;
};

function createWindow(){
        const window = NSPanel.alloc().initWithContentRect&#95;styleMask&#95;backing&#95;defer(
                NSMakeRect(0, 0, 420, 646),
                NSWindowStyleMaskClosable | NSWindowStyleMaskTitled | NSWindowStyleMaskResizable,
                NSBackingStoreBuffered,
                false
        );

        window.becomesKeyOnlyIfNeeded = true;
        window.floatingPanel = true;

        window.frameAutosaveName = "mosaic-panel-frame";

        window.releasedWhenClosed = false;

        window.standardWindowButton(NSWindowZoomButton).hidden = true;
        window.standardWindowButton(NSWindowMiniaturizeButton).hidden = true;

        window.titlebarAppearsTransparent = true;
        window.titleVisibility = NSWindowTitleHidden;
        
        window.backgroundColor = NSColor.colorWithRed&#95;green&#95;blue&#95;alpha(1, 0.98, 0.98, 1);

        return window;
};

function showWindow(window){
        window.makeKeyAndOrderFront(nil);
};

//        Public

function loadAndShow(baseURL){
        if(&#95;window){
                showWindow(&#95;window);

                return;
        }

        const pageURL = baseURL
                .URLByDeletingLastPathComponent()
                .URLByAppendingPathComponent("../Resources/web-ui/index.html");

        const window = createWindow();
        const webView = createWebView(pageURL);

        window.contentView = webView;
        
        &#95;window = window;

        showWindow(&#95;window);
};

function cleanup(){
        if(&#95;window){
                &#95;window.orderOut(nil);
                &#95;window = null;
        }
};

//        Export

module.exports = { loadAndShow, cleanup };
</code></pre>
</div>

There are a couple of key changes we made here that are important to note. Besides the fact that we’ve created specific functions for the creation, hiding and showing of our window and its web view, we’ve also *modularized* our user interface code.

Notice the `module.exports = { loadAndShow, cleanup }` line at the bottom? This is a way for us to specify exactly what objects and functions scripts who import this UI code can use (and hiding those we don’t want to them to worry about), which means we now have a more organized API for interacting with, showing and destroying our UI.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2017/04/symbols-sketch/">Unleashing The Full Potential Of Symbols In Sketch</a></em></p>

Let’s see what this looks like in practice. Back in `index.js`, remove the old code and add the following:

<pre><code class="language-javascript">const UI = require("./ui");

function onRun(context){
        UI.loadAndShow(context.scriptURL);
};
</code></pre>

We’re using a special function that Sketch automatically makes available to us, `require`, to import our `ui.js` code and assign the returned module to the `UI` variable. This gives us access to a simplified API for triggering our user interface. Things are much tidier now and easy to find!

## Conclusion

Well done &mdash; you’ve come far! In the [next part of this tutorial](https://www.smashingmagazine.com/2019/07/build-sketch-plugin-javascript-html-css-part-2/), we’ll give our web UI the ability to send us a message when the “Apply” button is clicked, and we’ll focus on the main plugin functionality: actually generating layer mosaics!

{{< signature "mb, yk, il" >}}
