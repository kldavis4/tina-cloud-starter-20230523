---
title: Frizz-Free JavaScript With ConditionerJS
slug: frizz-free-javascript-with-conditionerjs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9330fa9f-5dd2-4001-999d-36cb4d7376d4/01-before-after1.jpg
date: 2014-04-03T08:32:33.000Z
author: rik-schennink
description: >-
  Setting up JavaScript-based functionality to work across multiple devices can be tricky. When is the right time to load which script? Do your media queries matches tests, your geolocation popups tests and your viewport orientation tests provide the best possible results for your website?
categories:
  - Coding
  - Frameworks
  - CSS
  - JavaScript
  - Techniques
---
<a href="https://conditionerjs.com/">ConditionerJS</a> will help you combine all of this contextual information to pinpoint the right moment to load the functionality you need.

<img title="Applying conditioner to guinea pigs results in very smooth fur." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0d2f71e-c720-4cf9-9374-0246f84b9b3b/01-before-after.jpg" alt="Applying conditioner to guinea pigs results in very smooth fur." width="500" height="170" /><br>
<em>As you can clearly see, applying conditioner to guinea pigs results in very smooth fur. Take a moment and imagine what this could mean for your codebase.</em>

Before we jump into the ConditionerJS demo, let’s quickly take a look at the Web and how it’s changing, because it’s this change that drove the development of ConditionerJS in the first place. In the meantime, think of it as a shampoo but also as an orchestra conductor; instead of giving cues to musicians, <strong>ConditionerJS tells your JavaScript when to act up and when to tune down</strong> a bit.</p>

{{% feature-panel %}}

## The Origin Of ConditionerJS

You know, obviously, that the way we access the Web has changed a lot in the last couple of years. We no longer rely solely on our desktop computers to navigate the Web. Rather, we use a wide and quickly growing array of devices to get our daily dose of information. <strong>With the device landscape going all fuzzy</strong>, the time of building fixed width desktop sites has definitely come to an end. The fixed canvas is breaking apart around us and needs to be replaced with something flexible — maybe even something organic.

### What’s a Web Developer to Do?

Interestingly enough, most of the time, our content already is flexible. The styles, visuals and interaction patterns classically are rigid and are what create challenging to downright impossible situations. Turns out HTML (the contents container) has always been perfectly suited for a broad device landscape; the way we present it is what's causing us headaches.

We should be striving to present our content, cross-device, in the best possible way. But let's be honest, this “best possible way” is not three-width based static views, one for each familiar device group. That's just a knee-jerk reaction, where we try to hang on to our old habits.

<strong>The device landscape is too broad and is changing too fast</strong> to be captured in groups. Right this moment people are making phone calls holding tablets to their heads while others are playing Grand Theft Auto on their phones until their fingers bleed. There's phones that are tablets and tablets that are phones, there's no way to determine where a phone ends a tablet starts and what device might fall in between, so let's not even try.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e54d98b-9a37-4ce3-9fac-9e898c611666/02-grouping-devices.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e54d98b-9a37-4ce3-9fac-9e898c611666/02-grouping-devices.jpg" alt="Grouping devices is like grouping guinea pigs." width="500" height="325" /></a><br>
<em>Grouping devices is like grouping guinea pigs; while it’s certainly possible, eventually you will run into trouble.</em>

To determine the perfect presentation and interaction patterns for each device, we need more granularity than device groups can give us. We can achieve a sufficient level of detail by looking at contextual information and measuring how it changes over time.</p>

## Context On The Web

The <a href="https://www.thefreedictionary.com/context">Free Dictionary defines “context”</a> as follows:
<blockquote>“The circumstances in which an event occurs; a setting.”</blockquote>

The user’s context contains information about the environment in which that user is interacting with your functionality. Unlike feature detection, context is not static. You could be rotating your device right now, which would change the context in which you’re reading this article.

Measuring context is not only about testing hardware features and changes (such as viewport size and connection speed). <strong>Context can (and is) also influenced by the user’s actions.</strong> For instance, by now you’ve scrolled down this article a bit and might have moved your mouse a few pixels. This tells us something about the way you are interacting with the page. Collecting and combining all of this information will create a detailed picture of the context in which you’re currently reading this content.

Correctly measuring and responding to changes in context will enable us to present the right content in the right way at the right moment.

<strong>Note</strong>: If you're interested in a more detailed analysis of context, I advise you to read <a title="Designing With Context" href="https://www.cennydd.co.uk/2013/designing-with-context">Designing With Context</a> by Cennydd Bowles.</p>

## Where And How To Measure Changes In Context

Measuring changes in context can easily be done by adding various tests to your JavaScript modules. You could, for example, listen to the <code>resize</code> and <code>scroll</code> events on the window or, a bit more advanced, watch for media query changes.

Let’s set up a small Google Maps module together. Because the map will feature urban areas and contain a lot of information, it should render only on viewports wider than 700 pixels. On smaller screens, we’ll show a link to Google Maps. We’ll write a bit of code to measure the window’s width to determine whether the window is wide enough to activate the map; if not, then no map. Perfect! What’s for dinner?

Don’t order that pizza just yet!

Your client has just called and would like to duplicate the map on another page. On this page, the map will show a less crowded area of the planet and so could still be rendered on viewports narrower than 700 pixels.

You could add another test to the map module, perhaps basing your measurement of width on some <code>className</code>? But what happens if a third condition is introduced, and a fourth. No pizza for you any time soon.

Clearly, measuring the available screen space is not this module’s main concern; the module should instead mostly be blowing the user’s mind with fantastic interaction patterns and dazzling maps.

This is where Conditioner comes into play. <strong>ConditionerJS will keep an eye on context-related parameters</strong> (such as window width) so that you can keep all of those measurements out of your modules. Specify the environment-related conditions for your module, and Conditioner will load your module once these conditions have been met. This <a href="https://en.wikipedia.org/wiki/Separation_of_concerns">separation of concerns</a> will make your modules more flexible, reusable and maintainable — all favorable characteristics of code.</p>

## Setting Up A Conditioner Module

We’ll start with an HTML snippet to illustrate how a typical module would be loaded using Conditioner. Next, we’ll look at what’s happening under the hood.

<pre><code class="language-markup">
&lt;a href="https://maps.google.com/?ll=51.741,3.822"
   data-module="ui/Map"
   data-conditions="media:{(min-width:30em)} and element:{seen}"&gt; … &lt;/a&gt;
</code></pre>

### Codepen Example #1

We’re binding our map module using data attributes instead of classes, which makes it easier to spot where each module will be loaded. Also, binding functionality becomes a breeze. In the previous example, the map would load only if the media query <code>(min-width:30em)</code> is matched and the anchor tag has been <code>seen</code> by the user. Fantastic! How does this black magic work? Time to pop open the hood.

See the Pen [ConditionerJS - Binding and Loading a Map Module](https://codepen.io/rikschennink/pen/HiGEI/) by Rik Schennink ([@rikschennink](https://codepen.io/rikschennink)) on [CodePen](https://codepen.io).</p>

### A Rundown of Conditioner’s Inner Workings

The following is a rundown of what happens when the DOM has finished loading. Don’t worry — it ain’t rocket surgery.

1.  Conditioner first queries the DOM for nodes that have the `data-module` attribute. A simple [querySelectorAll](https://developer.mozilla.org/en-US/docs/Web/API/Document.querySelectorAll) does the trick.
2.  For each match, it tests whether the conditions set in the `data-conditions` attribute have been met. In the case of our map, it will test whether the media query has been matched and whether the element has scrolled into view (i.e. is seen by the user). Actually, this part could be considered rocket surgery.
3.  If the conditions are met, then Conditioner will fetch the referenced module using [RequireJS](https://requirejs.org); that would be the `ui/Map` module. We use RequireJS because writing our own module loader would be madness — I’ve tried.
4.  Once the module has loaded, Conditioner initializes the module at the given location in the DOM. Depending on the type of module, Conditioner will call the constructor or a predefined `load` method.
5.  Presto! Your module takes it from there and starts up its map routine thingies.

After the initial page setup has been done, Conditioner does not stop measuring conditions. If they don't match at first but are matched later on, <strong>perhaps the user decides to resize the window</strong>, Conditioner will still load the module. Also, if conditions suddenly become unsuitable the module will automatically be unloaded. This dynamic loading and unloading of modules will turn your static Web page into a living, growing, adaptable organism.</p>

## Available Tests And How To Use These In Expressions

Conditioner comes with basic set of tests that are all modules in themselves.

*   “media” `query` and `supported`
*   “element” `min-width`, `max-width` and `seen`
*   “window” `min-width` and `max-width`
*   “pointer” `available`

You could also write your own tests, doing all sorts of interesting stuff. For example, you could use <a href="https://conditionerjs.com/examples/custom/">this cookie consent test</a> to load certain functionality only if the user has allowed you to write cookies. Also, what about unloading hefty modules if the <a href="https://www.w3.org/TR/battery-status/">battery</a> falls below a certain level. Both possible. You could combine all of these tests in Conditioner’s expression language. You’ve seen this in the map tests, where we combined the <code>seen</code> test with the <code>media</code> test.

<pre><code class="language-javascript">
media:{(min-width:30em)} and element:{seen}
</code></pre>

Combine parenthesis with the logical operators <code>and</code>, <code>or</code> and <code>not</code> to quickly create complex but still human-readable conditions.</p>

## Passing Configuration Options To Your Modules

To make your modules more flexible and suitable for different projects, allow for the configuration of specific parts of your modules — think of an API key for your Google Maps service, or stuff like button labels and URLs.

<img title="Configuring guinea pig facial expression using configuration objects." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/481e69a9-ff8f-4399-9517-2aaa9883840b/03-configuration.jpg" alt="Configuring guinea pig facial expression using configuration objects." width="500" height="235" /><br>
<em>Configuring guinea pig facial expression using configuration objects.</em>

Conditioner gives you two ways to pass configuration options to your modules: page- and node-level options. On initialization of your module, it will automatically merge these two option levels and pass the resulting configuration to your module.</p>

### Setting Default Module Options

Defining a base <code>options</code> property on your module and setting the default options object are a good start, as in the following example. This way, some sort of default configuration is always available.

<pre><code class="language-javascript">
// Map module (based on AMD module pattern)
define(function(){

    // constructor
    // element: the node that the module is attached to
    // options: the merged options object
    var exports = function Map(element,options) {

    }

    // default options
    exports.options = {
        zoom:5,
        key:null
    }

    return exports;
});
</code></pre>

By default, the map is set to zoom level 5 and has no API key. An API key is not something you’d want as a default setting because it’s kinda personal.</p>

### Defining Page-Wide Module Options

Page-level options are useful for overriding options for all modules on a page. This is useful for something like locale-related settings. You could define page-level options using the <code>setOptions</code> method that is available on the <code>conditioner</code> object, or you could pass them directly to the <code>init</code> method.

<pre><code class="language-javascript">
// Set default module options
conditioner.setOptions({
    modules:{
        'ui/Map':{
            options:{
                zoom:10,
                key:'012345ABCDEF'
            }
        }
    }
});

// Initialize Conditioner
conditioner.init();
</code></pre>

In this case, we’ve set a default API key and increased the default zoom level to 10 for all maps on the page.</p>

### Overriding Options for a Particular Node

To alter options for one particular node on the page, use node-level options.

<pre><code class="language-javascript">
&lt;a href="https://maps.google.com/?ll=51.741,3.822"
   data-module="ui/Map"
   data-options='{"zoom":15}'&gt; … &lt;/a&gt;
</code></pre>

### Codepen Example #2

For this single map, the zoom level will end up as 15. The API key will remain <code>012345ABCDEF</code> because that’s what we set it to in the page-level options.

See the Pen [ConditionerJS - Loading the Map Module and Passing Options](https://codepen.io/rikschennink/pen/Iudth/) by Rik Schennink ([@rikschennink](https://codepen.io/rikschennink)) on [CodePen](https://codepen.io).

Note that the options are in JSON string format; therefore, the double quotes on the <code>data-options</code> attribute have been replaced by single quotes. Of course, you could also use double quotes and escape the double quotes in the JSON string.</p>

## Optimizing Your Build To Maximize Performance

As we discussed earlier, Conditioner relies on <a href="https://requirejs.org">RequireJS</a> to load modules. With your modules carefully divided into various JavaScript files, one file per module, Conditioner can now load each of your modules separately. This means that your modules will be sent over the line and parsed only once they’re required to be shown to the user.

To maximize performance (and minimize HTTP requests), merge core modules together into one package using the <a href="https://requirejs.org/docs/optimization.html">RequireJS Optimizer</a>. The resulting minimized core package can then be dynamically enhanced with modules based on the state of the user’s active context.

Carefully balance what is contained in the core package and what’s loaded dynamically. Most of the time, you won’t want to include the more exotic modules or the very context-specific modules in your core package.

<img title="Try to keep your request count to a minimum — your users are known to be impatient." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8195615f-d9a3-4d9e-93a0-e270e9f13beb/04-load-time-request-count.jpg" alt="Try to keep your request count to a minimum — your users are known to be impatient." width="500" height="322" /><br>
<em>Try to keep your request count to a minimum — your users are known to be impatient.</em>

Keep in mind that the more modules you activate on page load, the greater the impact on the CPU and the longer the page will take to appear. On the other hand, loading scripts conditionally will increase the CPU load needed to measure context and will add additional requests; also, this could affect page-redrawing cycles later on. There’s no silver bullet here; you’ll have to determine the best approach for each website.</p>

## The Future Of Conditioner

A lot more functionality is contained in the library than we’ve discussed so far. Going into detail would require more in-depth code samples, but because the API is still changing, the samples would not stay up to date for long. Therefore, the focus of this article has been on the <strong>concept of the framework and its basic implementation</strong>.

I’m looking for people to critically comment on the concept, to test <a href="https://conditionerjs.com/">Conditioner</a>'s performance and, of course, to contribute, so that we can build something together that will take the Web further!

{{< signature "al, ml, il" >}}

