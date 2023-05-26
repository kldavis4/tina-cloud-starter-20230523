---
title: Introducing Responsive Web Typography With FlowType.JS
slug: introducing-flowtype-js
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea565a2-2b88-4350-830d-e035c241e796/fluid-type-opt.png'
date: 2013-09-18T08:12:03.000Z
author: jd-graffam
description: >-
  While working on an image-heavy site for Simple Focus, a couple of our
  designers, John Wilson and Casey Zumwalt, noticed how images always scaled
  perfectly. Pull the corner of the browser window and the images expand to fill
  the space. Push back the corner, they shrink and fall into place. The line
  length of hypertext, on the other hand, changes based on its parent element's
  width, which has a negative effect on readability.
categories:
  - Coding
  - Workflow
  - JavaScript
  - jQuery
---
_It's our great pleasure to support active members of the Web design and development community. Today, we're proud to present **FlowType.JS** that allows a perfect character count per line at any screen width. This article is yet another special of our series of various tools, libraries and techniques that we've published here on Smashing Magazine: [LiveStyle](https://www.smashingmagazine.com/2013/08/08/release-livestyle-css-live-reload/), [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/), [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/), [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/), [GuideGuide](https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/), [Gridpak](https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/), [JS Bin](https://www.smashingmagazine.com/2012/07/23/js-bin-built-for-sharing-education-and-real-time/), [CSSComb](https://www.smashingmagazine.com/2012/10/02/csscomb-tool-sort-css-properties/) and [Jelly Navigation Menu](https://www.smashingmagazine.com/2013/08/15/jelly-navigation-menu-canvas-paperjs/). — Ed._</em>

While working on an image-heavy site for Simple Focus, a couple of our designers, [John Wilson](https://twitter.com/jhnwlsn) and [Casey Zumwalt](https://twitter.com/zumwalt), noticed how images always scaled perfectly. Pull the corner of the browser window and the images expand to fill the space. Push back the corner, they shrink and fall into place. The line length of hypertext, on the other hand, changes based on its parent element's width, which has a negative effect on readability.

"Wouldn't it be nice," John asked, "if text worked more like images?" Casey assured him that it could, with a jQuery plugin, if only they could figure out the math.

[![Fluid Type](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4110841b-7f93-41b3-826a-d30fec9886c6/trent-walton-fluid-type.png "Fluid Type")](https://trentwalton.com/2012/06/19/fluid-type/)  
_"In a fluid layout, browser width and typographic measure are linked: the wider the viewport, the more characters per line." – [Trent Walton](https://trentwalton.com/2012/06/19/fluid-type/)_

[Simple Focus](https://simplefocus.com/) is mainly a design firm, so like most programming ideas we have, we didn't do anything with it. Then, a few weeks later, John was rereading Trent Walton's [article about fluid type](https://trentwalton.com/2012/06/19/fluid-type/) and was inspired to try and figure it out.

{{% feature-panel %}}

An hour later, we had a working prototype and were kicking the tires internally. Within two weeks, FlowType.JS was fully-developed and ready to be sent into the world.

Here’s the process of how we got there:

## Technically Speaking

[FlowType.JS](https://simplefocus.com/flowtype/), when boiled down, is nothing more than some clever math wrapped in a jQuery plugin, with some options for controlling font sizes to accomplish a certain line length.

Let's take a deeper look into the code to better understand what's going on:

### The Basic Math

As you will see below, it's pretty simple stuff. First, we need to measure the width of an element in order to set a base number, which will be the key to the rest of the equation. Then we divide that base by a number that resolves to a reasonable `font-size`. For example, if an element measures at `1000px` and we divided it by `50`, we end up with `20px`, which is a reasonable `font-size`.

`Line-height` is another simple equation based off the `font-size`. Let’s say we choose a `line-height` of `1.45` times the `font-size` for readability. This equation is easy: `font-size` multiplied by `1.45` equals the recommended `line-height`.</p>

### The Prototype

An initial prototype shows us the idea actually works:

<pre><code class="language-javascript">
var $width = $window.width(),
    $fontSize = $width / 50,
    $lineHeight = $fontSize * 1.45;

$(window).ready( function() {
  $('element').css({
    'font-size':$fontSize + 'px',
    'line-height':$lineHeight + 'px'
  });
}

$(window).resize( function() {
  $('element').css({
    'font-size':$fontSize + 'px',
    'line-height':$lineHeight + 'px'
  });
});</code></pre>

If you were paying attention, you may have noticed that there's one major problem with the code: the math is based off of the window's width, not the element's width. This causes problems with breakpoints where elements resize to a larger dimension and the text gets smaller while the width of the element became wider.</p>

### Improved Code

Revising the code to measure the element's width instead of the window's fixed this problem. During this simple update, we also decided to start including options for maximum and minimum thresholds for font-sizes and element width, since a very narrow column would cause the font-size to become too small to read. [Read more about these thresholds](https://simplefocus.com/flowtype/#options).

Sharing the revised code here would make this article entirely too long as it includes several 'if' statements as well as duplicate code. Inefficient to say the least. With that said, at least it had options and worked well. But we're focused on design, remember? So we wanted to get a little advice from some friends before we put something out there that could make us look like noobs.</p>

### A Little Help from Friends

Almost ready to launch, FlowType.JS was reviewed by several peers. [Dave Rupert](https://daverupert.com/) suggested we make sure it performs well by creating a demo page with several instances and lots of text. We put that together and held our breath, and fortunately it worked very well.

Then we asked [Giovanni DiFeterici](https://www.gdifeterici.com/) for his feedback. Giovanni surprised us by refactoring and condensing all the 'if' statements into two lines of code. In the end, the compressed version of FlowType.JS can be as low as 450 bytes. We also got advice from plenty of other generous friends on everything all the way down to spell checking the demo site.</p>

### The Final Code

The final code is phenomenally simple. A few options and variables set simultaneously, a base function called `changes` where all the magic happens, and two simple calls for `changes`. One sets the `font-size` on load and another to recalculate on window resize.

Take a look at the code here:

<pre><code class="language-javascript">(function($) {
   $.fn.flowtype = function(options) {

      var settings = $.extend({
         maximum   : 9999,
         minimum   : 1,
         maxFont   : 9999,
         minFont   : 1,
         fontRatio : 35,
         lineRatio : 1.45
      }, options),

      changes = function(el) {
         var $el = $(el),
            elw = $el.width(),
            width = elw &gt; settings.maximum ? settings.maximum : elw  settings.maxFont ? settings.maxFont : fontBase &lt; settings.minFont ? settings.minFont : fontBase;

         $el.css({
            &#039;font-size&#039;   : fontSize + &#039;px&#039;,
            &#039;line-height&#039; : fontSize * settings.lineRatio + &#039;px&#039;
         });
      };

      return this.each(function() {

         var that = this;
         $(window).resize(function(){changes(that);});

         changes(this);
      });
   };
}(jQuery));</code></pre>

### How It Works and Fallback

As you can see, the code applies the newly calculated numbers as inline CSS to the element that is selected. Because this new CSS is inline, it overwrites whatever you have set in your linked stylesheets, creating a natural fallback in case a user has JavaScript disabled.

[![FlowType.JS Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/253e9081-beba-4786-b245-5d9dbf652442/flowtype-js-screenshot.png "FlowType.JS Screenshot")](https://simplefocus.com/flowtype/)

You'll want to configure the settings based on the font choices you make since the math works out differently based on the size of the font you choose.</p>

### Implementation

FlowType.JS was built as a jQuery plugin, so getting started is easy. All you need to do is call FlowType.JS and configure a few settings based on your design.

<pre><code class="language-javascript">$('body').flowtype({
 minimum   : 500,
 maximum   : 1200,
 minFont   : 12,
 maxFont   : 40,
 fontRatio : 30,
 lineRatio : 1.45
});</code></pre>

Full instructions are on [our demo site](https://simplefocus.com/flowtype/#getting-started). If jQuery isn't your thing, one Github community member [has already ported it](https://github.com/simplefocus/FlowType.JS/pull/5) to native JavaScript.</p>

## Nothing Is Ever Finished

We have more ideas for ways to improve the plugin, but we are treating it as an experiment first and foremost. It solves a common problem in Responsive Design where line-length and line-height aren't ideal between break points. Regardless, there have been some questions raised about FlowType.JS by many smart developers and designers.

One question that we've been asked is centered on typographical theory: should a design start with font-size or element width when optimizing text for legibility? I think the best answer is that it's a judgement call, that reading the text in your design is the best way to determine what's most legible. We've simply written a tool to help you accomplish what you want with your designs.

Another is about accessibility: doesn't this tool disable text zoom, thus making sites less accessible? We're aware of this behavior, but users are able to zoom beyond 200% and see font size increase. For now, simply remember to take your audience into consideration when designing with FlowType.JS.

Remember, like any utility, it's not a cure-all for the challenges of Web design. We're just trying to contribute a small idea to the Web design and development community and welcome feedback over at Github.

{{< signature "il, ea" >}}

