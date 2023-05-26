---
title: Creating a Fancy Sliding Menu With jQuery - Part 2
slug: creating-a-fancy-sliding-menu-with-jquery-part-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82b10f0e-3fde-4742-af20-57c7c36262fa/jquery-02.jpg
date: 2010-09-17T17:27:14.000Z
author: janos-racz
description: >-
  In the [previous
  part](https://www.smashingmagazine.com/2010/09/05/create-a-fancy-sliding-menu-with-jquery/)
  of this tutorial we've discussed how to create an animated sliding menu with
  Javascript using the jQuery framework. In this tutorial, we'll continue to
  develop our application by enhancing the sliding effect in various ways and
  make it even more customizable.

  When we finish with this article, we should have a full-fledged animated
  Javascript menu that will enable you to display your menus in a great number
  of creative ways. So let's continue right where we left off!
categories:
  - Coding
  - Navigation
  - jQuery
---
In the <a href="https://www.smashingmagazine.com/2010/09/05/create-a-fancy-sliding-menu-with-jquery/">previous part</a> of this tutorial we've discussed how to create an animated sliding menu with Javascript using the jQuery framework. In this tutorial, we'll continue to develop our application by enhancing the sliding effect in various ways and make it even more customizable.

When we finish with this article, we should have a full-fledged animated Javascript menu that will enable you to display your menus in a great number of creative ways. So let's continue right where we left off!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful JavaScript And jQuery Tools, Libraries, Plugins](https://www.smashingmagazine.com/2011/04/useful-javascript-and-jquery-tools-libraries-plugins/)
*   [Useful JavaScript Libraries and jQuery Plugins](https://www.smashingmagazine.com/2012/09/useful-javascript-libraries-jquery-plugins-web-developers/)
*   [Spicing Up Your Website With jQuery Goodness](https://www.smashingmagazine.com/2010/06/spice-up-your-website-with-jquery-goodness/)
*   [<span class="headline">Magnific Popup, A Truly Responsive Lightbox</span>](https://www.smashingmagazine.com/2013/05/truly-responsive-lightbox/)

## Advanced animated effects with the Easing Plugin

### Simple easing

The easiest way to give more life to our animations is to use jQuery's <a href="https://gsgd.co.uk/sandbox/jquery/easing/">Easing Plugin</a>. You should download it and include the script in your header, so it'll look something like this:

{{% feature-panel %}}

<pre><code class="language-markup tmp-xml">&lt;script type="text/javascript" src="javascript/jquery.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="javascript/jquery_easing_plugin.js"&gt;&lt;/script&gt; 
&lt;script type="text/javascript" src="javascript/sliding_menu.js"&gt;&lt;/script&gt;</code></pre>

To understand what the easing plugin does, we need to look back for a moment and see how we animated our menu so far. This is the code we used in the first part:

<pre><code class="language-javascript">function slide ( menu_slider, width )
{
  this.is_animation_running = true;
  var self = this;
  menu_slider.animate (
  { 'width' : width },
  this.effect_duration,
  function ()
  {
    self.is_animation_running = false;
  }
  );
}</code></pre>

We told the <code>slide</code> function which container to animate, the width we'd like to scale it to and the duration of the animation, that's all. We simply told jQuery to shrink the container to 253px during an 1 second period, for example, but we never specified actually how to get from 0px to 253px. And that's where the easing plugin comes into play.

We can pass yet another parameter to the <code>animate</code> function which specifies a mathematical representation of how much the effect should progress over time. Of course we don't want to get involved with too much mathematics if possible, that's why we use this plugin to access all these pre-defined mathematical formulas by name.

If you watched our demo carefully in the previous part, you may have noticed that the animation doesn't play in a linear fashion. That's because jQuery has two built-in easing methods already, "linear" and "swing". The default is "swing", but you can change it easily to "linear" without any additional code. However, the easing plugin gives us even more control. You can use more than 30 different easing functions to satisfy your style and taste. Here are a few examples, feel free to experiment with these on your own or preview each possible effect on the <a>easing plugin's homepage</a>.

First here's a demo using "linear" easing ( as I've already mentioned, you don't need a plugin for this ). Can you notice the difference?
<div class="demo demo_1"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>
Next, here's a more aggressive effect, "easeOutElastic":
<div class="demo demo_2"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>
Finally, a bit subtler exponential function, "easeOutExpo":
<div class="demo demo_3"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>
Now let's take a look at the code behind this. At the very basic level, the easing formula's name should be passed between the duration and the callback function parameter to jQuery's <code>animate</code> method, like this:

<pre><code class="language-javascript">// Remember, we did the animation inside the slide function?
function slide ( menu_slider, width )
{
  this.is_animation_running = true;
  var self = this;
  menu_slider.animate (
  { 'width' : width },
  this.effect_duration,
  "linear", // Here it goes, it could be "easeOutElastic", "easeInCubic", or whatever
  function ()
  {
    self.is_animation_running = false;
  }
  );
}</code></pre>

I should mention here that jQuery is even much more flexible, from version 1.4 you can use "per-property easing", which means you are allowed to specify different easing functions for each property you animate. Since we're changing only the "width" attribute, this is not our concern, but you can read more about this on the <a href="https://api.jquery.com/animate/">jQuery API site</a>.

Next, let's take a look at how we can implement this in our SlidingMenu class. Obviously, we want to pass the easing type as a parameter to the class constructor. Here's how our new constructor looks like:

<pre><code class="language-javascript">function SlidingMenu ( container_name, menu_slider_width, duration, easing ) // The new easing parameter gets passed
{
  this.effect_duration = duration;
  this.menu_slider_width = menu_slider_width;
  this.is_animation_running = false;
  this.active_menu = $($( container_name + " .menu_slider" )[0]);
  this.easing = easing; // Store the easing string as the instance's variable

  var self = this;
  $( container_name + " .menu_button" ).bind( "click", self, on_click );

  this.slide ( this.active_menu, this.menu_slider_width );

}</code></pre>

And this is how we can call it:

<pre><code class="language-javascript">new SlidingMenu( ".menu", 253, 1000, "easeOutElastic" );</code></pre>

We simply pass the easing type as the fourth parameter. Also note that we didn't assign the class to a global variable ( unlike in the previous part ) to further reduce the possible conflicts with other scripts on the page.

Finally, we use this information in our <code>slide</code> function to specify the easing:

<pre><code class="language-javascript">function slide ( menu_slider, width )
{
  this.is_animation_running = true;
  var self = this;
  menu_slider.animate (
  { 'width' : width },
  this.effect_duration,
  this.easing, // We replaced a specific value with the easing string
  function ()
  {
    self.is_animation_running = false;
  }
  );
}</code></pre>

Remember that we can do all this because we've used "prototype" to make <code>slide</code> SlidingMenu's own public function.</p>

### Complex easing

Let's take this a step further! We can improve our application to accept more than one easing function, and then play them randomly, for example. To do that, we simply need to pass an array of easing types to the constructor instead of one, and then select one of them randomly when playing the animation.

This can be a quite useful feature since it doesn't restrict those who want to use only one kind of easing, but gives more variety to those who want more. If you're not keen on the idea of changing the pace of your animation randomly, all you have to do is pass only one easing type to the SlidingMenu instance.

Here's the slightly modified version of the <code>slide</code> function:

<pre><code class="language-javascript">function slide ( menu_slider, width )
{
  this.is_animation_running = true;
  var self = this;
  menu_slider.animate (
  { 'width' : width },
  this.effect_duration,
  this.curr_easing, // Use the new easing variable
  function ()
  {
    self.is_animation_running = false;
  }
  );
}</code></pre>

Now you can see I've used <code>this.curr_easing</code> as the currently used easing type, but what that type is going to be exactly comes down to the <code>on_click</code> function:

<pre><code class="language-javascript">function on_click ( event )
{
  . . . // Here we run the checks

  // First select a random easing function from the this.easing array
  rand_num = Math.floor ( Math.random() * event.data.easing.length ); // Generate a random number between 0 and (arraylength-1)
  event.data.curr_easing = event.data.easing[rand_num]; // Choose the random value

  . . . // Here is the code that does the animations

}</code></pre>

We use <code>Math.random</code> to generate the random number and <code>Math.floor</code> to round it to an integer ( we basically cut all numbers after the dot ). These two functions help us select a random easing of our SlidingMenu instance's easing types that we select on object creation. By the way, you do remember we used event.data inside this function to access the class instance, right?

Now I didn't mention but it should be obvious why we define an easing type in <code>on_click</code> instead of doing to directly in the <code>slide</code> function: for a smooth animation we need both the "slide in" and "slide out" actions to be use the same easing. We could also pass this variable as a new parameter to <code>slide</code>, but maybe it's a bit cleaner working with fewer parameters here.

Fortunately our constructor doesn't care whether a parameter is string or an array, so we don't have to modify that. All that's left is to create a new instance of SlidingMenu passing along an array of easing functions, like so:

<pre><code class="language-javascript">new SlidingMenu( ".demo_4 .menu", 253, 1000, ["easeOutCubic", "linear", "easeOutExpo"] );</code></pre>

<div class="demo demo_4">
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>
If all is well, you should see the three easing types changing randomly between animations.

Our class has become a bit more flexible with these new features. However, while we're at it, let's tweak the animate function a little more.

## Vertical menu

One very important feature we haven't implemented in the last part is the ability to slide menu items vertically. We should fix that now.

In order to accomplish this, we need to do 3 things:

*   Introduce another parameter to the class constructor, we'll call it `attr`. This is going to be either "width" or "height" for horizontal and vertical menus, respectively
*   Use this attr variable in our `slide` function instead of "width"
*   Change the "width" strings to "amount" where appropriate

So the constructor simply takes one more string variable and register it as usual:

<pre><code class="language-javascript">function SlidingMenu ( container_name, menu_slider_width, duration, easing, attr ) // The new attr parameter
{
  this.effect_duration = duration;
  this.menu_slider_width = menu_slider_width;
  this.is_animation_running = false;
  this.active_menu = $($( container_name + " .menu_slider" )[0]);
  this.easing = easing;
  this.attr = attr; // Remember our new variable

  . . .

}</code></pre>

The slide function is a little more complicated, that's why I didn't include this in the first part. For first thought, you may try to do something like this:

<pre><code class="language-javascript">function slide ( menu_slider, amount ) // Notice we changed it from "width" to "amount"
{
  this.is_animation_running = true;
  var self = this;
  menu_slider.animate (
  { this.attr : amount }, // replace 'width' with the attr
  this.effect_duration,
  this.easing,
  function ()
  {
    self.is_animation_running = false;
  }
  );
}</code></pre>

But of course it wouldn't work, since the first parameter of the animate function is a <code>map</code> object. To assign the correct amount to the right attr using only variables we must create a new map object first, and pass that on to the <code>animate</code> function, like so:

<pre><code class="language-javascript">function slide ( menu_slider, amount )
{
  var map = {}; // Create empty  map object
  map[this.attr] = amount; // Set attr to amount

  this.is_animation_running = true;
  var self = this;
  menu_slider.animate (
  map, // Pass map to animate
  this.effect_duration,
  this.easing,
  function ()
  {
    self.is_animation_running = false;
  }
  );
}</code></pre>

In the code above, <code>var map = {}</code> creates an empty <code>map</code> object, then we set the desired values manually on the next line. ( We could've used <code>var map = new Object()</code> as well instead of <code>{}</code> to get similar results.) Finally, we simply pass this new object to the animate method.

If all goes well, all we need to do is to create a new instance of SlidingMenu and setting the attr parameter:

<pre><code class="language-javascript">function slide ( menu_slider, amount )
{
  new SlidingMenu( ".menu", 158, 1000, "easeOutBounce", "height" );
}</code></pre>

Here's an example demonstrating the use of a vertical menu and the "easeOutBounce" easing function:
<div class="demo_ver demo_5"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d67faae-3dfe-413d-bd14-77db9df609e8/menu-button-1-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a19df97-8608-42c4-be07-a67cd066a188/menu-button-2-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3af10f6-f353-4a9c-b093-021e59c7358c/menu-button-3-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e173db5-8bea-4947-b7c6-0654c9b35e8e/menu-button-4-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/809759f7-893d-48aa-804b-f602ffc61751/menu-button-5-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9315867c-9adc-4383-a626-46798b7c3e24/menu-button-6-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>

## Chaining animations

### Setting it up

Splendid! Our little SlidingMenu is becoming quite robust, but we also need to set up a mechanism for handling more animations in our menu. It's not that difficult, but we should consider a few things before we start coding.

The most important is the fact that jQuery's animate function will run independently from other commands you execute, so we can't just simply put one animation line after an other, because then all animations will seem to run together, which is not what we want.

We took advantage of this feature in the last part by starting the two <code>slide</code> functions ( sliding one panel in, and other one out ) after one another, yet they still look like they're moving at the same time. It was useful for that, but we have to work around it for not simultaneously chaining more animations together.

We've already seen how we can do stuff after the animation has played by specifying the last parameter of the <code>animation</code> function, but we need to be a bit trickier if we want to display an effect before sliding the menu buttons. For this we'll use the <code>setTimeout</code> Javascript function. It has the following syntax.

<pre><code class="language-javascript">setTimeout("Javascript commands",milliseconds);</code></pre>

And what setTimeout does is it waits for the given milliseconds, and only then executes the specified Javascript command, which is usually a simple function call.

So let's modify our on_click_function accordingly:

<pre><code class="language-javascript">function on_click ( event )
{
  // The usual checks
  if ( $(this).next()[0] == event.data.active_menu[0] )
  {
    return;
  }

  if ( event.data.is_animation_running )
  {
    return;
  }

  var menu_slider = $(this).next();

  event.data.first_anim ( menu_slider ); // First animation
  setTimeout ( function() { event.data.do_slide( menu_slider ), event.data.extra_anim_duration }, event.data.first_anim_duration ); // Slide panels after the first animation finishes

}</code></pre>

As you can see, first we do the same checks we did in the previous part, then we store the menu_slider variable as well.

And now comes the new code: we first start the animation we'd like to see before sliding the menu buttons and use <code>setTimeout</code> to wait the appropriate number of milliseconds before starting to slide the menu items. You can see we've introduced two more variables to our SlidingMenu constructor, <code>first_anim</code> which will specify the animation we want to run before the sliding effect, and <code>extra_anim_duration</code> which will store the extra animation's duration in milliseconds. We'll take a look at implementing this in the SlidingMenu constructor in the next section.

For now, let's just concentrate on the rest of this code. You can see we removed a few lines from <code>on_click</code>, all these lines will now go into <code>do_slide</code>:

<pre><code class="language-javascript">function do_slide ( menu_slider )
{
  this.slide ( this.active_menu, 0 );
  this.active_menu = menu_slider;
  this.slide ( this.active_menu, this.menu_slider_width );
}</code></pre>

This is pretty straightforward: we simply slide in the currently active panel and slide out the new one, like before. But this time, we refer to the variables with the this keyword. To do this, we need to make <code>do_slide</code> a public function of SlidingMenu as well:

<pre><code class="language-javascript">SlidingMenu.prototype.do_slide = do_slide;</code></pre>

Finally, we need to add the ability to play an animation after the panels have slid out. We've discussed this a couple of times before: we use the <code>animation</code> function's last parameter to do that, so the <code>slide</code> function gets modified like this:

<pre><code class="language-javascript">function slide ( menu_slider, amount )
    {
      . . . // Some code we left out here

      menu_slider.animate (
      map,
      this.effect_duration,
      easing,
      function ()
      {
        self.is_animation_running = false;

        if ( amount == self.menu_slider_width )
        {
          self.last_anim( self, menu_slider ); // The key line: play the last animation
        }
      }
      );
    }</code></pre>

These last few lines allow us to play the finishing animation if needed. We only play it when the new panel has finished sliding out, so we won't call it twice accidentally. Of course we still have the option to not do anything here, for that we'll pass an empty function to the constructor or not pass anything at all as <code>last_anim</code> ( see next section ). We pass the <code>menu_slider</code> variable, just in case, we won't necessarily use it.

Well, we had to work quite a bit to get this functionality working, but all this modification allows us to make our menus even fancier without touching the core SlidingMenu code. All we need to do is specify the "first_anim" and "last_anim" functions and then create a SlidingMenu instance accordingly. We'll finish this thought in the next section soon, but first let's take a look at some examples of using these two functions!

### A simple example

First, we'll modify the CSS we used in the previous part of this tutorial for these examples. We've mentioned this "technique" in the first part when creating the complex demo. Basically all we do is set a fix width for the images inside the <code>menu_slider</code> tags, so the panels will appear to slide over the images instead of shrinking them.

<pre><code class="language-css">.menu .menu_slider img {
  width : 253px; /* Instead of 100% */
  height : 158px; /* Instead of 100% */
}</code></pre>

Here's the slightly modified effect. We also decreased the duration of the animation to 0.5 sec, so the whole effect won't take too long when we add additional animations:
<div class="demo demo_6"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>
Now, let's apply that <code>first_anim</code> we've been working on. In this simple example all we do is fade out the currently active menu item before sliding the panel. Here's how we create such a SlidingMenu instance:

<pre><code class="language-javascript">new SlidingMenu( ".demo_7 .menu", 253, 300, ["swing"], "width", first_anim, last_anim, 500  );</code></pre>

The last three parameters in order:

*   `first_anim` : a function that runs before every animation
*   `last_anim` : a function that runs after every animation
*   `duration` : a number of milliseconds for the extra animations, accessible to every class function

And now all we have to do is define what <code>first_anim</code> and <code>last_anim</code> does. Below is the code we used for decreasing the opacity in the <code>first_anim</code> function. The <code>last_anim</code> function is responsible for changing the opacity back to 100% after the animation has played:

<pre><code class="language-javascript">function first_anim ( menu_slider )
{
  this.active_menu.fadeTo ( self.extra_anim_duration, 0.0 );
}

function last_anim ( menu_slider )
{
  $ ( this.container_name + " .menu_slider" ).fadeTo ( 0, 1.0 );
}</code></pre>

Notice we use the <code>this</code> keyword to access the instance's extra_anim_duration property we specified as "500" milliseconds above. We can do this because <code>first_anim</code> and <code>last_anim</code> are going to be member functions of the SlidingMenu instance. You'll see how exactly in the next section.

And here is the demo demonstrating this simple effect:
<div class="demo demo_7"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>

### Smashing the menu

Let's take a look at two more possible uses of this new functionality. First, let's display the Smashing logo when fading out the original image. For this, we'll include one more <code>img</code> element in each <code>menu_slider</code> container:

<pre><code class="language-markup tmp-xml">&lt;div class="menu_slider"&gt;
  &lt;img src="images/menu_slider_1.jpg" alt="" /&gt;
  &lt;img src="images/smashing_logo.png" alt="" /&gt;
&lt;/div&gt;</code></pre>

This is how each menu_slider container will look like. Other than the HTML, all we need to do is declare the <code>first_anim</code> and <code>last_anim</code> functions as before, taking into account the twist with the Smashing Logo:

<pre><code class="language-javascript">function first_anim ( menu_slider )
{
  $( this.active_menu.children()[0] ).fadeTo ( self.extra_anim_duration, 0.0 );
  $( this.active_menu.children()[1] ).fadeTo ( self.extra_anim_duration, 1.0 );
}

function last_anim ( menu_slider )
{
  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[0]).fadeTo ( 0, 1.0 );;
              });

  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[1]).fadeTo ( 0, 0.0 );;
              });

}</code></pre>

The <code>first_anim</code> function is pretty straightforward: we access the first and second image through the currently active container, fade the original image out and bring the second image ( the Smashing Logo ) to full opacity. Note that previously we changed the opacity of the <code>menu_slider</code> div element, but now we operate on its contents separately!

The other function, <code>last_anim</code> is responsible for changing all images to their default state, so it loops through all the menu images and smashing logos using jQuery's <code>each</code> function and changes their opacity as needed. You can easily tell that it's kind of an overkill, since we change only two element's opacity during a menu slide, and you'd be right. This method is just enough for our purposes, however, if you want to improve it, you can introduce a <code>last_active_menu</code> variable for the SlidingMenu class to store the menu item that was recently closed, then access it from <code>last_anim</code> to change the opacities in that container only.

And one last thing to do before we check out how it works is to hide the smashing logo by default and position it above the other image. You can either add a class to the smashing logos and do this with CSS, or do it with jQuery like this:

<pre><code class="language-javascript">$(".menu .menu_slider").each ( function ( index, elem )
{
  $($(elem).children()[1]).css( { "width" : "150px", "height" : "39px", "position" : "relative", "top" : "-95px", "left" : "45px" } ).fadeTo ( 0, 0.0 );;
});</code></pre>

This code loops through the Smashing logos and puts them into position then changes their opacity to 0 instantly. I threw in some jQuery chaining here which I avoided until now for easier understanding, but in this case it's very simple: it first uses the <code>css</code> method then grabs the same object and uses <code>fadeTo</code>. We do this manually here, but you can easily use good cross-browser compatible CSS if you prefer.

We're ready! Let's see how it works:
<div class="demo demo_8"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
</div>
</div>

### One more example

For one last quick example on how you can use our improved SlidingMenu class, we use every new functionality we added in this second part: multiple easing, vertical alignment and before-after animations. It may not be the most practical example, but let's just be happy about how flexible our application has become.
<div class="demo_ver demo_9"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d67faae-3dfe-413d-bd14-77db9df609e8/menu-button-1-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a19df97-8608-42c4-be07-a67cd066a188/menu-button-2-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3af10f6-f353-4a9c-b093-021e59c7358c/menu-button-3-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e173db5-8bea-4947-b7c6-0654c9b35e8e/menu-button-4-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/809759f7-893d-48aa-804b-f602ffc61751/menu-button-5-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9315867c-9adc-4383-a626-46798b7c3e24/menu-button-6-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
</div>
</div>
Here's the HTML we used for this example:

<pre><code class="language-markup tmp-xml">&lt;div class="menu"&gt;
  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_1_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_1.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_2_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_2.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_3_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_3.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_4_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_4.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_5_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_5.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_6_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_6.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>

And below is how to format it with simple jQuery code. You can easily replace this with CSS if you add some classes to the HTML above, but it's just as elegant using the <code>each</code> and <code>css</code> methods.

<pre><code class="language-javascript">$(".menu .menu_slider").each ( function ( index, elem )
        {
          $($(elem).children()[1]).css( { "width" : "253px",
                  "height" : "158px",
                  "position" : "relative",
                  "top" : "-316px" } );

          $($(elem).children()[2]).css( { "width" : "253px",
                  "height" : "158px",
                  "position" : "relative",
                  "top" : "158px" } );
        });</code></pre>

These two images are the two halves of the Smashing Logo. We place the first one just above the menu image and the second goes below.

Finally, here are the two functions that animate the menu items before and after the slide:

<pre><code class="language-javascript">function first_anim ( menu_slider )
{
  $( this.active_menu.children()[1] ).animate ( { "top" : "-158px" }, this.extra_anim_duration/2, "easeOutBounce" );
  $( this.active_menu.children()[2] ).animate ( { "top" : "-316px" }, this.extra_anim_duration/2, "easeOutBounce" );
}

function last_anim ( menu_slider )
{
  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[1]).css ( "top", "-316px" );;
              });

  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[2]).css ( "top", "158px" );;
              });</code></pre>

The first one simply calls the animate function with "easeOutBounce" easing. This function moves the two pieces of Smashing Logo together. We use only half of the specified duration for the animation itself ( thus the division by two ), we basically pause for the rest.

And <code>last_anim</code> does it's job to restore all the elements to their original position, as usual.

This last demo is stuffed with everything, after defining the extra animation functions, all we really have to do is to create a new SlidingMenu instance like so:

<pre><code class="language-javascript">new SlidingMenu( ".menu", 158, 900, ["easeOutBounce", "easeInQuad", "easeOutElastic", "easeOutExpo" ], "height", first_anim, last_anim, 1200  );</code></pre>

## Finishing up

Although we've been playing around with these demos nicely, there's one last thing we haven't talked about yet, and that is how these last parameters we specified for extra animation become part of the SlidingMenu class. So let's take a look at the modified constructor first, then explain the new bits:

These last few lines allow us to play the finishing animation if needed. We only play it when the new panel has finished sliding out, so we won't call it twice accidentally. Of course we still have the option to not do anything here, for that we'll pass an empty function to the constructor or not pass anything at all as <code>last_anim</code> ( see next section ). We pass the <code>menu_slider</code> variable, just in case, we won't necessarily use it.

Well, we had to work quite a bit to get this functionality working, but all this modification allows us to make our menus even fancier without touching the core SlidingMenu code. All we need to do is specify the "first_anim" and "last_anim" functions and then create a SlidingMenu instance accordingly. We'll finish this thought in the next section soon, but first let's take a look at some examples of using these two functions!

### A simple example

First, we'll modify the CSS we used in the previous part of this tutorial for these examples. We've mentioned this "technique" in the first part when creating the complex demo. Basically all we do is set a fix width for the images inside the <code>menu_slider</code> tags, so the panels will appear to slide over the images instead of shrinking them.

<pre><code class="language-css">.menu .menu_slider img {
  width : 253px; /* Instead of 100% */
  height : 158px; /* Instead of 100% */
}</code></pre>

Here's the slightly modified effect. We also decreased the duration of the animation to 0.5 sec, so the whole effect won't take too long when we add additional animations:
<div class="demo demo_6"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>
Now, let's apply that <code>first_anim</code> we've been working on. In this simple example all we do is fade out the currently active menu item before sliding the panel. Here's how we create such a SlidingMenu instance:

<pre><code class="language-javascript">new SlidingMenu( ".demo_7 .menu", 253, 300, ["swing"], "width", first_anim, last_anim, 500  );</code></pre>

The last three parameters in order:

*   `first_anim` : a function that runs before every animation
*   `last_anim` : a function that runs after every animation
*   `duration` : a number of milliseconds for the extra animations, accessible to every class function

And now all we have to do is define what <code>first_anim</code> and <code>last_anim</code> does. Below is the code we used for decreasing the opacity in the <code>first_anim</code> function. The <code>last_anim</code> function is responsible for changing the opacity back to 100% after the animation has played:

<pre><code class="language-javascript">function first_anim ( menu_slider )
{
  this.active_menu.fadeTo ( self.extra_anim_duration, 0.0 );
}

function last_anim ( menu_slider )
{
  $ ( this.container_name + " .menu_slider" ).fadeTo ( 0, 1.0 );
}</code></pre>

Notice we use the <code>this</code> keyword to access the instance's extra_anim_duration property we specified as "500" milliseconds above. We can do this because <code>first_anim</code> and <code>last_anim</code> are going to be member functions of the SlidingMenu instance. You'll see how exactly in the next section.

And here is the demo demonstrating this simple effect:
<div class="demo demo_7"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /></div>
</div>
</div>

### Smashing the menu

Let's take a look at two more possible uses of this new functionality. First, let's display the Smashing logo when fading out the original image. For this, we'll include one more <code>img</code> element in each <code>menu_slider</code> container:

<pre><code class="language-markup tmp-xml">&lt;div class="menu_slider"&gt;
  &lt;img src="images/menu_slider_1.jpg" alt="" /&gt;
  &lt;img src="images/smashing_logo.png" alt="" /&gt;
&lt;/div&gt;</code></pre>

This is how each menu_slider container will look like. Other than the HTML, all we need to do is declare the <code>first_anim</code> and <code>last_anim</code> functions as before, taking into account the twist with the Smashing Logo:

<pre><code class="language-javascript">function first_anim ( menu_slider )
{
  $( this.active_menu.children()[0] ).fadeTo ( self.extra_anim_duration, 0.0 );
  $( this.active_menu.children()[1] ).fadeTo ( self.extra_anim_duration, 1.0 );
}

function last_anim ( menu_slider )
{
  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[0]).fadeTo ( 0, 1.0 );;
              });

  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[1]).fadeTo ( 0, 0.0 );;
              });

}</code></pre>

The <code>first_anim</code> function is pretty straightforward: we access the first and second image through the currently active container, fade the original image out and bring the second image ( the Smashing Logo ) to full opacity. Note that previously we changed the opacity of the <code>menu_slider</code> div element, but now we operate on its contents separately!

The other function, <code>last_anim</code> is responsible for changing all images to their default state, so it loops through all the menu images and smashing logos using jQuery's <code>each</code> function and changes their opacity as needed. You can easily tell that it's kind of an overkill, since we change only two element's opacity during a menu slide, and you'd be right. This method is just enough for our purposes, however, if you want to improve it, you can introduce a <code>last_active_menu</code> variable for the SlidingMenu class to store the menu item that was recently closed, then access it from <code>last_anim</code> to change the opacities in that container only.

And one last thing to do before we check out how it works is to hide the smashing logo by default and position it above the other image. You can either add a class to the smashing logos and do this with CSS, or do it with jQuery like this:

<pre><code class="language-javascript">$(".menu .menu_slider").each ( function ( index, elem )
{
  $($(elem).children()[1]).css( { "width" : "150px", "height" : "39px", "position" : "relative", "top" : "-95px", "left" : "45px" } ).fadeTo ( 0, 0.0 );;
});</code></pre>

This code loops through the Smashing logos and puts them into position then changes their opacity to 0 instantly. I threw in some jQuery chaining here which I avoided until now for easier understanding, but in this case it's very simple: it first uses the <code>css</code> method then grabs the same object and uses <code>fadeTo</code>. We do this manually here, but you can easily use good cross-browser compatible CSS if you prefer.

We're ready! Let's see how it works:
<div class="demo demo_8"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c63b6-45b9-4b40-9848-ff9d8f17d5d1/menu-button-1.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e014bf03-de55-4916-a363-22d18ffe6a62/menu-button-2.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087e2a6e-8043-4f70-b54a-ce6da5bae40a/menu-button-3.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44ff9b6-863e-4e9e-b153-225eb2862ce5/menu-button-4.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7df3cf1-4dee-4b3d-b457-9bd66296a851/menu-button-5.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5b0b6bd-b58a-4afa-b661-978831d8f10f/menu-button-6.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85bd42d-7d33-4f3c-96aa-fc94847c14af/smashing-logo.png" alt="" /></div>
</div>
</div>

### One more example

For one last quick example on how you can use our improved SlidingMenu class, we use every new functionality we added in this second part: multiple easing, vertical alignment and before-after animations. It may not be the most practical example, but let's just be happy about how flexible our application has become.
<div class="demo_ver demo_9"><br>
<div class="menu">
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d67faae-3dfe-413d-bd14-77db9df609e8/menu-button-1-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc120611-b6d9-44b8-87c7-8a49e93eb310/menu-slider-1.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a19df97-8608-42c4-be07-a67cd066a188/menu-button-2-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07f27ea-2db2-4025-97a2-b63e617dd46e/menu-slider-2.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3af10f6-f353-4a9c-b093-021e59c7358c/menu-button-3-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877983ed-56ab-4f48-8c0d-68cd2e70285b/menu-slider-3.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e173db5-8bea-4947-b7c6-0654c9b35e8e/menu-button-4-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58066c26-8b00-48c3-9024-2278a9d86e78/menu-slider-4.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/809759f7-893d-48aa-804b-f602ffc61751/menu-button-5-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db4d2a6-c2b3-4edb-aa89-28752764e135/menu-slider-5.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
<div class="menu_button"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9315867c-9adc-4383-a626-46798b7c3e24/menu-button-6-ver.png" alt="" /></div>
<div class="menu_slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcbe39b1-5cfd-4c8c-bb2f-f3db6ba1ff21/menu-slider-6.jpg" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e899f8-e02d-4406-842b-b49d834df859/smashing-logo-top.png" alt="" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b4e2f7-720a-439c-9708-99b16a8e8908/smashing-logo-bottom.png" alt="" /></div>
</div>
</div>
Here's the HTML we used for this example:

<pre><code class="language-markup tmp-xml">&lt;div class="menu"&gt;
  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_1_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_1.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_2_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_2.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_3_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_3.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_4_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_4.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_5_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_5.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;

  &lt;div class="menu_button"&gt;&lt;img src="images/menu_button_6_ver.png" alt="" /&gt;&lt;/div&gt;
  &lt;div class="menu_slider"&gt;
    &lt;img src="images/menu_slider_6.jpg" alt="" /&gt;
    &lt;img src="images/smashing_logo_top.png" alt="" /&gt;
    &lt;img src="images/smashing_logo_bottom.png" alt="" /&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>

And below is how to format it with simple jQuery code. You can easily replace this with CSS if you add some classes to the HTML above, but it's just as elegant using the <code>each</code> and <code>css</code> methods.

<pre><code class="language-javascript">$(".menu .menu_slider").each ( function ( index, elem )
        {
          $($(elem).children()[1]).css( { "width" : "253px",
                  "height" : "158px",
                  "position" : "relative",
                  "top" : "-316px" } );

          $($(elem).children()[2]).css( { "width" : "253px",
                  "height" : "158px",
                  "position" : "relative",
                  "top" : "158px" } );
        });</code></pre>

These two images are the two halves of the Smashing Logo. We place the first one just above the menu image and the second goes below.

Finally, here are the two functions that animate the menu items before and after the slide:

<pre><code class="language-javascript">function first_anim ( menu_slider )
{
  $( this.active_menu.children()[1] ).animate ( { "top" : "-158px" }, this.extra_anim_duration/2, "easeOutBounce" );
  $( this.active_menu.children()[2] ).animate ( { "top" : "-316px" }, this.extra_anim_duration/2, "easeOutBounce" );
}

function last_anim ( menu_slider )
{
  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[1]).css ( "top", "-316px" );;
              });

  $ ( this.container_name + " .menu_slider" ).each ( function ( index, elem )
              {
                $($(elem).children()[2]).css ( "top", "158px" );;
              });</code></pre>

The first one simply calls the animate function with "easeOutBounce" easing. This function moves the two pieces of Smashing Logo together. We use only half of the specified duration for the animation itself ( thus the division by two ), we basically pause for the rest.

And <code>last_anim</code> does it's job to restore all the elements to their original position, as usual.

This last demo is stuffed with everything, after defining the extra animation functions, all we really have to do is to create a new SlidingMenu instance like so:

<pre><code class="language-javascript">new SlidingMenu( ".menu", 158, 900, ["easeOutBounce", "easeInQuad", "easeOutElastic", "easeOutExpo" ], "height", first_anim, last_anim, 1200  );</code></pre>

## Finishing up

Although we've been playing around with these demos nicely, there's one last thing we haven't talked about yet, and that is how these last parameters we specified for extra animation become part of the SlidingMenu class. So let's take a look at the modified constructor first, then explain the new bits:

<pre><code class="language-javascript">function SlidingMenu ( container_name, menu_slider_width, duration, easing, attr, first_anim, last_anim, extra_anim_duration )  // We get the parameters
{
  // Set defaults for the optional parameters
  if ( duration == null )
  {
    duration = 1000;
  }
  if ( easing == null )
  {
    easing = [ "swing" ];
  }
  if ( attr == null )
  {
    attr = "width";
  }
  if ( first_anim == null )
  {
    first_anim = function () {};
  }
  if ( last_anim == null )
  {
    last_anim = function () {};
  }

  // The public class variables
  this.container_name = container_name; // new parameter!
  this.effect_duration = duration;
  this.menu_slider_width = menu_slider_width;
  this.is_animation_running = false;
  this.active_menu = $($( container_name + " .menu_slider" )[0]);
  this.easing = easing;  // new!
  this.attr = attr;  // new!

  this.first_anim = first_anim; // new!
  this.last_anim = last_anim; // new!
  this.extra_anim_duration  = extra_anim_duration;  // new!

  // Old stuff //
  // We do the bindings on object creation
  var self = this;
  $( container_name + " .menu_button" ).bind( "click", self, on_click ); // Menu button click binding

  // Do the slide
  this.slide ( this.active_menu, this.menu_slider_width );

}</code></pre>

There are a few important additions to the last version: first, we added all new parameters and assigned their values to the public class variables with similar names, just as before. You can see all these new variables: the easing, the attr, the two extra animation functions and their duration, and another important one, the container's name. The last one is necessary so we can access our menu from the extra animation functions.

And the other addition is the first part of the constructor, where we assign default values to each variable that hasn't been specified. Other programming languages let you do this in a more convenient format like: <code>function func ( var a = 0; var b = 1 )</code>, but we can do the same in Javascript by checking if the variable is null or not. We go as far as the duration parameter defining these variables, so at the very least, we have to specify the container name and the desired width of the menu items, but everything else is optional.

Here's a minimal call to our SlidingMenu constructor:

<pre><code class="language-javascript">new SlidingMenu( ".menu", 253 );</code></pre>

And with that, we've covered every important part of our new and enhanced SlidingMenu application. Here's the final listing for all the code we've written in parts 1 and 2:

<pre><code class="language-javascript">function SlidingMenu ( container_name, menu_slider_width, duration, easing, attr, first_anim, last_anim, extra_anim_duration )  // We get the parameters
{
  // Set defaults for the optional parameters
  if ( duration == null )
  {
    duration = 1000;
  }
  if ( easing == null )
  {
    easing = [ "swing" ];
  }
  if ( attr == null )
  {
    attr = "width";
  }
  if ( first_anim == null )
  {
    first_anim = function () {};
  }
  if ( last_anim == null )
  {
    last_anim = function () {};
  }

  // The public class variables
  this.container_name = container_name; // new parameter!
  this.effect_duration = duration;
  this.menu_slider_width = menu_slider_width;
  this.is_animation_running = false;
  this.active_menu = $($( container_name + " .menu_slider" )[0]);
  this.easing = easing;  // new!
  this.attr = attr;  // new!

  this.first_anim = first_anim; // new!
  this.last_anim = last_anim; // new!
  this.extra_anim_duration  = extra_anim_duration;  // new!

  // Old stuff //
  // We do the bindings on object creation
  var self = this;
  $( container_name + " .menu_button" ).bind( "click", self, on_click ); // Menu button click binding

  // Do the slide
  this.slide ( this.active_menu, this.menu_slider_width );

}
SlidingMenu.prototype.slide = slide;
SlidingMenu.prototype.do_slide = do_slide;

function do_slide ( menu_slider )
{
  this.slide ( this.active_menu, 0 );
  this.active_menu = menu_slider;
  this.slide ( this.active_menu, this.menu_slider_width );
}

function slide ( menu_slider, amount )
{
  // Create attributes map
  var map = {};
  map[this.attr] = amount;

  this.is_animation_running = true;
  var self = this;

  menu_slider.animate (
  map,
  this.effect_duration,
  this.curr_easing,
  function ()
  {
    self.is_animation_running = false;
    if ( amount == self.menu_slider_width )
    {
      self.last_anim( self, menu_slider ); // The key line: play the last animation
    }
  }
  );
}

function on_click ( event )
{
  // First check if the active_menu button was clicked. If yes, we do nothing ( return )
  if ( $(this).next()[0] == event.data.active_menu[0] ) // Remember, active_menu refers to the image ( thus next() )
  {
    return;
  }
  // Check if animation is running. If it is, we interrupt

  if ( event.data.is_animation_running )
  {
    return;
  }

  // First select a random easing function from the this.easing array
  rand_num = Math.floor ( Math.random() * event.data.easing.length ); // Generate a random number between 0 and (arraylength-1)
  event.data.curr_easing = event.data.easing[rand_num]; // Choose the random value

  // Get the item next to the button
  var menu_slider = $(this).next();
  event.data.first_anim ( menu_slider ); // First animation
  setTimeout ( function() { event.data.do_slide( menu_slider ), event.data.extra_anim_duration }, event.data.extra_anim_duration ); // Slide panels after the first animation finishes

}</code></pre>

## Final thoughts and further development

All right, our little application has become quite large during this two-part tutorial. At this point it's capable of producing a huge variety of sliding menu effects and with some tweaking, even more.

Keep in mind that although we've used this simple menu throughout the tutorials, the possibilities are much wider if you use all this with some imagination. Instead of pictures, the menu items could be simple headings with descriptions and nice typography, instead of square images, the menu panels can could be little semi-transparent icons and so on. You can easily use it on other website elements other than menus as well. I'm sure you'll find much more creative uses of its functionality.

If you're a developer, below is a list of a few things you can still work on to make it even more sophisticated. Even if you're relatively new to jQuery or Javascript, after reading this two-part tutorial you should have a pretty good understanding on how it all works and be able to develop your ideas further:

*   Make it more effective by introducing a new `last_active_menu` variable we were talking about in this tutorial
*   Allow different change effects other than the "slide"
*   Allow first_anim and last_anim to optionally run simultaneously with the menu slide
*   Make the event trigger customizable ( use optional triggers besides "click" )
*   Eliminate the need for the `last_anim` function: store the default CSS parameters of every element and automatically restore them

Although there are a lot more we could do here, this little piece of code will probably suffice for most of your needs. The main point of these tutorials was not to write bullet-proof application anyway, but to introduce you to some important jQuery and Javascript concepts like event handling, hiding global variables ( scope ), using some important and useful jQuery functions ( animate, css, each ) and show you an overall process of gradually building up such an effect. I hope you enjoyed and learned something from it. And finally, here is the final version of SlidingMenu along with the last few demos:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b3e1fb6-7376-4947-9be3-3c246ed0ae72/fancy-jquery-sliding-menu.zip">Fancy jQuery Sliding Menu Download</a>

<script src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10fd9806-20c1-469b-af91-5feac1e8e417/jquery.js" type="text/javascript"></script>
<script src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86309e62-674d-4315-a88d-13090805a573/jquery-easing-plugin.js" type="text/javascript"></script>
 <script src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fb9bd2a-f4e5-4935-bc71-2ca3009107c4/sliding-menu-v4.js" type="text/javascript"></script>

