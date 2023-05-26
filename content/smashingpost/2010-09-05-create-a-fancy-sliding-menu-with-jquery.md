---
title: Create A Fancy Sliding Menu With jQuery
slug: create-a-fancy-sliding-menu-with-jquery
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98424ffd-aa5f-4036-9adc-5a9d6ee0d288/jquery-06.gif
date: 2010-09-05T17:27:13.000Z
author: janos-racz
description: >-
  One of the great advantages of creating interactive websites is being able to
  dynamically hide and reveal parts of your content. Not only does it make for a
  more interesting user experience, but it allows you to stuff more onto a
  single page than would otherwise be possible, but in a very elegant,
  non-obtrusive way, and without overwhelming the user with too much information
  at once.

  In this tutorial, we'll **create a sliding menu using the jQuery framework**.
  You will find the downloadable source files at the end of the tutorial if you
  wish to use them on your website. But the main goal of this article is to show
  you some basic techniques for creating these kinds of effects and to provide
  you with the tools you need to realize your own creative ideas. This tutorial
  is aimed at beginner jQuery developers and those just getting into client-side
  scripting. You'll learn how to progressively build this simple effect from
  scratch.
categories:
  - Coding
  - Navigation
  - jQuery
---
One of the great advantages of creating interactive websites is being able to dynamically hide and reveal parts of your content. Not only does it make for a more interesting user experience, but it allows you to stuff more onto a single page than would otherwise be possible, but in a very elegant, non-obtrusive way, and without overwhelming the user with too much information at once.

In this tutorial, we'll create a sliding menu using the jQuery framework. You will find the downloadable source files at the end of the tutorial if you wish to use them on your website. But the main goal of this article is to show you some basic techniques for creating these kinds of effects and to provide you with the tools you need to realize your own creative ideas. This tutorial is aimed at beginner jQuery developers and those just getting into client-side scripting. You'll learn how to progressively build this simple effect from scratch.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful JavaScript And jQuery Tools, Libraries, Plugins](https://www.smashingmagazine.com/2011/04/useful-javascript-and-jquery-tools-libraries-plugins/)
*   [Useful JavaScript Libraries and jQuery Plugins](https://www.smashingmagazine.com/2012/09/useful-javascript-libraries-jquery-plugins-web-developers/)
*   [Spicing Up Your Website With jQuery Goodness](https://www.smashingmagazine.com/2010/06/spice-up-your-website-with-jquery-goodness/)
*   [<span class="headline">Magnific Popup, A Truly Responsive Lightbox</span>](https://www.smashingmagazine.com/2013/05/truly-responsive-lightbox/)

If all you want is a fancy effect on your website, you can simply use the <a href="https://docs.jquery.com/UI/Accordion">accordion plug-in</a>, which implements the same basic thing and allows even more control over it. On the other hand, if you want to get your hands dirty and find out how a system like this works, so that you can develop your own ideas later, this tutorial is for you. Also, in the next part of this series, we'll take a look at how to enhance this basic sliding menu with various effects and animations to make it more interesting.

{{% feature-panel %}}

## Why jQuery?

When creating any kind of Web application, especially one that contains animation effects and various elements that are implemented differently in various browsers, using a framework that takes care of low-level implementation and lets you focus on the high-level code logic is always a good idea.

So, while a JavaScript framework can save you time by simplifying specific commands and letting you type less, the real benefit comes from guaranteed cross-browser compatibility, ensuring that your application works the same everywhere without any additional effort on your part.

We chose jQuery, because it's one of the most popular frameworks out there, with a fairly extensive and easy-to-use (not to mention well-documented) <a href="https://api.jquery.com/">API</a>. However, you could very likely implement the same techniques demonstrated here in any framework of your choice.</p>

## Before We Start

Before writing a single line of code, always consider how you're going to integrate the JavaScript code into your HTML, how users will interact with the interface and how the overall solution will affect the user experience. With a menu, for example, you have to consider whether your content is dynamically generated or static. With dynamic content, a menu that animates on mouse click would work perfectly fine; but it wouldn't look so fancy for static content, where the page has to reload every time the user clicks on a menu item. When should you play the animation then? Before or after the page reloads? The quality and speed of the effect depends on many factors, including the user's computer, whether the website's content has been cached, how much content you want to display and so on.

You have to consider every possibility of your specific situation to get the best out of it. There's no golden rule here. For the sake of a simpler demonstration, we've decided to focus mainly on the JavaScript code, but we'll offer some possible solutions at the end of the article.</p>

## The Basics: HTML And CSS

Let's get started already! We have to build a solid foundation for our JavaScript code first. Never forget that although JavaScript is used almost everywhere nowadays, some users (and search engines, of course) still do not have it enabled. So we have to make sure that everything works fine and looks good even without the fancy effects.

<pre class=" language-markup"><code class=" tmp-xml language-markup"><br>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_button<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>button_1.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_slider<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>img_1.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_button<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>button_2.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_slider<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>img_2.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_button<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>button_3.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_slider<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>img_3.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_button<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>button_4.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_slider<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>img_4.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_button<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>button_5.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>menu_slider<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>img_5.png<span class="token punctuation">"</span></span> <span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span></code></pre>

<pre class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.menu</span> </span><span class="token punctuation">{</span>
    <span class="token property">width</span> <span class="token punctuation">:</span> <span class="token number">100%</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token selector"><span class="token class">.menu</span> <span class="token class">.menu_button</span>, <span class="token class">.menu</span> <span class="token class">.menu_slider</span> </span><span class="token punctuation">{</span>
    <span class="token property">margin</span> <span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
    <span class="token property">float</span> <span class="token punctuation">:</span> left<span class="token punctuation">;</span>
    <span class="token property">height</span> <span class="token punctuation">:</span> <span class="token number">158</span>px<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token selector"><span class="token class">.menu</span> <span class="token class">.menu_button</span> </span><span class="token punctuation">{</span>
    <span class="token property">width</span> <span class="token punctuation">:</span> <span class="token number">33</span>px<span class="token punctuation">;</span>
    <span class="token property">cursor</span> <span class="token punctuation">:</span> pointer<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token selector"><span class="token class">.menu</span> <span class="token class">.menu_slider</span> </span><span class="token punctuation">{</span> <span class="token comment">/* Hide the contents by default */</span>
    <span class="token property">width</span> <span class="token punctuation">:</span> <span class="token number">0</span>px<span class="token punctuation">;</span>
    <span class="token property">overflow</span> <span class="token punctuation">:</span> hidden<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token selector"><span class="token class">.menu</span> <span class="token class">.menu_button</span><span class="token pseudo-class">:hover</span> </span><span class="token punctuation">{</span>
    <span class="token property">background</span> <span class="token punctuation">:</span> <span class="token hexcode">#ddd</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>

The above code generates a simple menu bar that consists of 12 container (<code>div</code>) elements, each containing a single image, alternating the menu button and the menu slider images. We could have used only <code>img</code> elements and simply put them one after another, but valid XHTML requires that we wrap them in another element, so we did that using the <code>div</code> containers. This also allows you to substitute the images with any other element later (see an example near the end of this tutorial), because we'll be concerned only with the containers. We set the <code>menu_slider</code> class container width to 0px, so they will be invisible by default: and we'll hide and reveal them dynamically with JavaScript.

We use <code>float: left</code> here to keep the <code>div</code> elements on the same line.

Also, note that I omitted the <code>width</code>, <code>height</code>, and <code>alt</code> attributes in the <code>img</code> tags for readability (well, they're there, but empty), but you should always include at least the <code>alt</code> attribute on your website for valid HTML/XHTML.

The last line might not be so obvious. We set the background color for hover to <code>#ddd</code>. This ensures that a different color for button titles appears whenever the user mouses over one. If our menu were vertical, we would simply type <code>color: #ddd</code>, but because it's horizontal and our letters are on a 90°-degree angle, we have to get a little tricky. So, we use transparent PNGs as menu buttons, and we sort of cut out the text from the button by leaving the letters fully transparent. With this method, we can control the color of the text simply by changing the background, which will show through the transparent area.

The <code>overflow: hidden</code> line is not necessary when working with images, but it will come in handy if we want to use other slide effects instead (see later in the tutorial).

Here's what our menu currently looks like. (Hover over the items to see the gray background behind the buttons.)

## jQuery Magic

Now for the fun part. Let's start by binding a <code>slide</code> function to the mouse-click event on each menu button.

Remember that each <code>menu_slider</code>'s width is currently 0px. What <code>slide()</code> does is animate the width of the container right next to the clicked button to make it go from 0px to a specified width, thus creating a slide effect.

We use the <code>$(this)</code> expression to convert the clicked button to a jQuery object right away; so we can use jQuery's <code>next()</code> method to get the <code>div</code> right next to the button. This will be the corresponding <code>menu_slider</code>, which we can now pass on to the <code>slide()</code> function to animate it.

From now on, whenever we post a code snippet, the green comments will indicate new or important parts or provide additional explanation.

<pre><code class="language-javascript">function slide ( menu_slider ) // Function to render the animation.
{
	menu_slider.animate (
	    { 'width' : '253' }, // The first parameter is a list of CSS attributes that we want to change during the animation.
	    1000 // The next parameter is the duration of the animation.
	);
}

$(".menu .menu_button").bind ( "click", function ( event ) // We're binding the effect to the click event on any menu_button container.
{
	// Get the item next to the button
	var menu_slider = $(this).next(); // We convert it to a jQuery object: $(HTMLElement)
	// Do the animation
	slide ( menu_slider );
}</code></pre>

As you can see, a click event starts the whole process. First, we store the element next to the button (i.e. the corresponding image) in the variable <code>menu_slider</code>. Then we pass it to the <code>slide</code> function.

Finally, the slide function uses jQuery's animate method to create the effect. Its first parameter is a list of CSS attributes that we want to change (in this case, only the width of the image, to 253px). The second parameter is the duration of the animation in milliseconds. We've set it to 1 second.

You can see that it's working, though far from perfect. Specifying the height of the images beforehand (as we did in the CSS) is very important, otherwise the height will grow proportionally to the width, resulting in a different effect.

Currently, you can still click on each menu item and slide out the corresponding image, which is not what we want, so we'll fix that now. We just need to introduce a new variable called <code>active_menu</code> that stores the currently active <code>menu_button</code> object, and we'll also modify the <code>slide</code> function to accept another parameter, which will specify the direction of the slide or, to be more precise, the width property of the animation. So if we pass a parameter greater than 0, it will slide out, and if we pass 0, it will slide back in.

<pre><code class="language-javascript">// Global variables
var active_menu; // We introduce this variable to hold the currently active (i.e. open) element.
function slide ( menu_slider, width )
{
	menu_slider.animate (
	    { 'width' : width }, // We replaced the specific value with the second parameter.
	    1000
	);
}

$(".menu .menu_button").bind ( "click", function ( event )
{
	// Get the item next to the button.
	var menu_slider = $(this).next();
	// First slide in the active_menu.
	slide ( active_menu, 0 );
	// Then slide out the clicked menu.
	slide ( menu_slider, 253 );
}

// We also slide out the first panel by default and thus set the active_menu variable.
active_menu = $($( ".menu_slider" )[0]); // Notice we've converted it to a jQuery object again.
slide ( active_menu, 253 );</code></pre>

One thing to keep in mind is that every jQuery object behaves kind of like an array, even if it contains only one element. So to get the DOM object it's referring to (in our case, the <code>img</code> element), we have to access the array and get the first element from it. We did that with the <code>($( ".menu_slider" )[0]</code> expression, which selects the very first DOM element of the "menu_slider" class, but you can use the alternative <code>get</code> method as well: <code>$(".menu_slider").get(0)</code>.

If you refresh the page here, and if you have a browser that automatically jumps to the last read section (or if you scroll fast enough), you can see this menu unfold after the page loads.

## A Few Fixes

All right, finally, our script is working the way we want, except for some glitches, which we'll address now. They're not fatal errors. In fact, you may even want to leave them as they are; but if you don't, here's a way to resolve them.</p>

### Forbidding Multiple Open Panels

If you've played around with the demo above, you probably noticed that if you click more than one panel within 1 second, more than one animation can run at the same time, sometimes making the menu wider than it is supposed to be.

To resolve this issue, we can simply introduce another variable that determines whether an animation is playing or not. We'll call it <code>is_animation_running</code>. We set this variable to <code>true</code> as soon as the slide effect begins, and we set it back to <code>false</code> when the animation finishes. To accomplish this, we use the <code>animation</code> function's <code>another</code> parameter, which specifies another function to run right after the animation finishes. This is important, because if you just set <code>is_animation_running</code> to <code>false</code> after the animation function, nothing would happen, because it would execute almost instantly, when the sliding has just begun. By using this third parameter, we ensure that the variable will be set to <code>false</code> at exactly the right time, regardless of the effect's duration. Then we simply allow our application to run only if <code>is_animation_running</code> is <code>false</code> (i.e. when no other panel is sliding at the moment).

<code class="language-javascript">var active_menu; var is_animation_running = false; // New variable. function slide ( menu_slider, width ) { is_animation_running = true; // Indicates that an animation has started. menu_slider.animate ( { 'width' : width }, 1000, // &lt;- Notice the column! function () // This third parameter is the key here. { is_animation_running = false; // We set is_animation_running to false after the animation finishes. } ); } $(".menu .menu_button").bind ( "click", function ( event ) { // First check if animation is running. If it is, we don't do anything. if ( is_animation_running ) { return; // Interrupt execution. } var menu_slider = $(this).next(); slide ( active_menu, 0 ); slide ( menu_slider, 253 ); } active_menu = $($( ".menu .menu_slider" )[0]); slide ( active_menu, 253 );</code>

Now, if you click multiple buttons, only one animation will run at a time.</p>

### The Self-Collapse Glitch

You may have also noticed what happens when you click on the currently active button. It slides in and then out again. If that's cool with you, then fine, but perhaps you want to fix the active item's width.

To do this, we just add a little check. Whenever a menu button is clicked, we check if the container right next to it is the <code>active_menu</code> or not. (Remember, the <code>active_menu</code> variable stores the <code>div</code> container that is currently slid out.) If it is, we do nothing; otherwise, we play the animation. Easy as pie!

But remember we said that every jQuery object behaves like an array? In fact, because it's just a collection of DOM elements, there's really no good way to compare two such objects. Thus, we'll access the DOM elements directly to see if they're the same or not (i.e. <code>active_menu[0]</code> and <code>$(this).next()[0]</code>).

<pre><code class="language-javascript">var active_menu;
var is_animation_running = false;

function slide ( menu_slider, width )
{
	is_animation_running = true;
	menu_slider.animate (
	    { 'width' : width },
	    1000,
	    function ()
	    {
		  is_animation_running = false;
	    }
	);
}

$(".menu .menu_button").bind ( "click", function ( event )
{
	// First, check if the active_menu button was clicked. If so, we do nothing ( return ).
	if ( $(this).next()[0] == active_menu[0] )  // Here we make the check.
	{
		return;
	}
	if ( is_animation_running )
	{
		return;
	}
	var menu_slider = $(this).next();
	slide ( active_menu, 0 );
	active_menu = menu_slider; // Set active menu for next check.
	slide ( active_menu, 253 ); // Now we can pass active_menu if we want.
}

active_menu = $($( ".menu .menu_slider" )[0]);
slide ( active_menu, 253 );</code></pre>

Our menu works perfectly now. Try it: click on a button twice. Nothing should happen on your second click.</p>

## Cleaning Up

All right, we're almost there. If you put the code on a website right now, it will most likely work just fine. But to make sure everything runs smoothly, let's get rid of those global variables. Hiding these inside a class is always a good idea, so that they don't collide with other JavaScript code. This is especially important if you've added other JavaScript snippets to your page from different sources. Imagine two coders gave the same name to one of their global variables. Whenever you interacted with one, you'd automatically affect the other. It would be a mess!

So now we'll create a <code>SlidingMenu</code> class and use <code>active_menu</code> and <code>is_animation_running</code> as its variables. This approach also allows you to use the sliding menu more than once on the page. All you need to do is create a new instance of SlidingMenu for every animated menu. And while we're at it, we may as well make the slider function belong to <code>SlidingMenu</code>, so that it can access and directly modify its variables if needed.

<pre><code class="language-javascript">function SlidingMenu ()
{
	// Let's make these class variables so that other functions (i.e. slide) can access them.
	this.is_animation_running = false;
	this.active_menu = $($( ".menu .menu_slider" )[0]);

	// We do the bindings on object creation.
	var self = this;
	$( ".menu .menu_button" ).bind( "click", self, on_click ); // Menu button click binding.

	// Do the slide.
	this.slide ( 253 );
}

SlidingMenu.prototype.slide = slide;

function slide ( width )
{
	this.is_animation_running = true;
	var self = this;
	this.active_menu.animate (
		{ 'width' : width }, // We replaced the specific value with the second parameter.
		1000,
		function ()
	        {
		     self.is_animation_running = false; // We set is_animation_running false after the animation finishes.
		}
	);
}

function on_click ( event )
{
	// Notice we access the SlidingMenu instance through event.data!
	if ( $(this).next()[0] == event.data.active_menu[0] )
	{
		return;
	}
	if ( event.data.is_animation_running )
	{
		return;
	}
	// Get the item next to the button.
	var menu_slider = $(this).next();
	// First slide in the active_menu.
	event.data.slide ( 0 );
	// Set the active menu to the current image.
	event.data.active_menu = menu_slider;
	// Then slide out the clicked menu.
	event.data.slide ( 253 );
}

var sl = new SlidingMenu(); // We pass the three parameters when creating an instance of the menu.</code></pre>

The code above needs some explanation. There are three important blocks, so let's look at them one by one.</p>

### The SlidingMenu Class

<pre><code class="language-javascript">function SlidingMenu ()  // Our new class.
{
	// Let's make these class variables so that other functions (i.e. slide) can access them.
	this.is_animation_running = false;
	this.active_menu = $($( ".menu .menu_slider" )[0]);

	// We do the bindings on object creation.
	var self = this;
	$( ".menu .menu_button" ).bind( "click", self, on_click ); // Menu button click binding.

	// Do the slide.
	this.slide ( 253 );

}</code></pre>

JavaScript, unlike many other programming languages, doesn't have a <code>class</code> keyword for creating classes. But we can simply create objects that have their own variables and methods by creating a regular JavaScript object. So, we basically define a function here, <code>SlidingMenu</code>, and put inside this function all of the stuff that we would put in a regular class constructor in other languages.

We first define the same two variables that we used earlier, <code>is_animation_running</code> and <code>active_menu</code>. With the <code>this</code> keyword, we ensure that they belong to the particular class instance.

The next part may not be obvious at first:

<pre><code class="language-javascript">var self = this;
$( ".menu .menu_button" ).bind( "click", self, on_click );</code></pre>

To understand this, we have to talk a bit about how jQuery handles events.</p>

### jQuery Event Handling 101 (at Least What We Need to Know Here)

In short, jQuery uses the <code>bind</code> method to add event listeners to DOM elements. (You could alternatively use the <code>live</code> method, which would update event listeners if new DOM elements are added to the document.)

The basic usage of <code>bind</code> requires two parameters: an event type (e.g. <code>click</code>, <code>mouseover</code>) and a function (i.e. callback function) that executes when the given event type occurs on the DOM element. And this is where the <code>this</code> keyword comes into play, because in the callback function we often want to reference the DOM object on which the event happened. And jQuery makes it very convenient to do so; we just need to use <code>this</code>.

For example, let's say we want to change an image element to another image when the user clicks on it. To do so, we can write something like this:

<pre><code class="language-javascript">$("#example_img").bind ( "click", change_image );

function change_image ( event )
{
    this.src = "images/another_img.png";
}</code></pre>

In the example above, we use the <code>this</code> keyword to reference the DOM object. It's very convenient for simple applications, but for more complicated ones, you may run into problems.

As in the example, we want to access the <code>SlidingMenu</code> instance's variables somehow. But because the <code>this</code> keyword is already used to reference the DOM object, we have to find another way.

Fortunately, jQuery allows us to do this fairly easily. To do it, we can pass another parameter to the bind function, which will be placed right between the event type and the callback function, and this parameter has to be an object. You probably noticed the <code>event</code> parameter in the <code>change_image</code> function above. To every callback function is automatically passed an <code>event</code> parameter that contains a handful of useful information, including which element was clicked. And with the extended call of the <code>bind</code> function, we can pass the <code>SlidingMenu</code> instance object through the event parameter as well. We can then access this object through <code>event.data</code>. Here's a basic example:

<pre><code class="language-javascript">function ImageData () // This will be an object that contains information about an image, much like our SlidingMenu class contains information about the sliding menu.
{
    this.width = "500";
    this.height = "200";
    this.src = "images/example_image.png";
}

// We create an instance of ImageData.
var image_instance = new ImageData();

// We bind the change_image function to the click event, passing along the image_instance data object as well.
$("#example_image").bind ( "click", image_instance, change_image );

// The callback function.
function change_image ( event )
{
    this.src = event.data.width; // event.data refers to the image_instance object
    this.src = event.data.height;
    this.src = event.data.src;
}</code></pre>

This example illustrates well how we can access both the DOM element on which the event occurred and the data object we passed through. We access the former through the <code>this</code> keyword, and we access the latter through <code>event.data</code>.

Now it finally makes sense why we used this extended version of the function call when binding the click event to the buttons. And because <code>this</code> will always refer to the DOM element in this context, we used the self variable as a substitute, to pass the <code>SlidingMenu</code> instance to the callback function.

Here it is again:

<pre><code class="language-javascript">var self = this;
$( ".menu .menu_button" ).bind( "click", self, on_click );</code></pre>

### Moving Along

The last part in our class definition simply slides out the first panel using its <code>slide</code> method. But because we haven't defined such a function yet, the line below the class definition also becomes important:

<pre><code class="language-javascript">SlidingMenu.prototype.slide = slide;</code></pre>

We use JavaScript's prototype mechanism to extend our <code>SlidingMenu</code> object with the <code>slide</code> method.

This approach has two main benefits. First, the slider function can now access the variables of any class instance directly using the <code>this</code> keyword. (Because no event handling is involved directly in this function, <code>this</code> now refers to the <code>SlidingMenu</code> instance. You'll see with <code>on_click</code> that we will need to access it through <code>event.data</code>).

Secondly, using <code>prototype</code> instead of directly writing this method inside the class improves memory usage if we make more than one instance of <code>SlidingMenu</code>, because we don't have to create the <code>slide</code> functions every time we create a new instance: they'll always use the external function.</p>

### The Slide Function

As we've discussed, <code>slide</code> is responsible for sliding the panels in and out. It will be called from the <code>on_click</code> function (see below) and uses the same parameters as before.

<pre><code class="language-javascript">function slide ( width )
{
	this.is_animation_running = true;
	var self = this;
	this.active_menu.animate (
	{ 'width' : width },
	this.effect_duration,
	function ()
	{
		self.is_animation_running = false;
	}
	);
}</code></pre>

You can see we put <code>this</code> before every variable, and it now refers to the class instance's variables. This way, we don't have to pass the variables as function parameters to access or even modify them, and no matter how many instances we create of SlidingMenu, they'll always refer to the correct variables.

You may have noticed that we introduced a variable called <code>self</code>. We basically did this for the same reason we did it in our class definition: because jQuery handles this last parameter similar to event handling. If we used <code>this</code> instead, it would refer to the DOM object. Try it out: it won't work properly. By introducing the <code>self</code> variable, the animations run as expected.

The last thing worth mentioning is that we replaced the <code>menu_slider</code> parameter with the class instance's <code>active_menu</code> variable. So from now on, we can just set this variable from anywhere and it will animate the current <code>active_menu</code> automatically. It's just for convenience: one less parameter to pass.</p>

### The on_click Function

Finally, let's look at the <code>on_click</code> function. Here we put all the code that describes what happens after the user clicks a <code>menu_button</code>. It performs the same checks as before and uses the <code>slide</code> function to hide and reveal menu objects. This method accesses the class variables through the <code>event.data</code> that we passed along in our class definition.

You can also see that we pass only one parameter to our modified <code>slide</code> function (the desired width of the element), so it knows whether to slide it in or out; but the element that needs to be animated will be accessed directly through the <code>active_menu</code> variable.

<pre><code class="language-javascript">function on_click ( event )
{
// First check if the active_menu button was clicked. If so, we do nothing. ( return )
if ( $(this).next()[0] == event.data.active_menu[0] ) // Remember, active_menu refers to the image ( thus next() ).
{
    return;
}
// Check if animation is running. If it is, we interrupt.
if ( event.data.is_animation_running )
{
    return;
}
// Get the item next to the button.
var menu_slider = $(this).next();
// First slide in the active_menu.
event.data.slide ( 0 );
// Set the active menu to the current image.
event.data.active_menu = menu_slider;
// Then slide out the clicked menu.
event.data.slide ( 253 );
}</code></pre>

## Customization

By now, our sliding menu should work exactly as we want, and we don't have to worry about it interfering with other JavaScript code.

One last thing to do before we wrap it up is to make the <code>SlidingMenu</code> class a bit more flexible, because it's way too rigid. As it is now:

*   It works only with a container with the class name `menu`;
*   It works only with menu images that are 253 pixels long;
*   It works only when the animation duration is set to 1 second.

To fix these, we'll pass three more variables to the <code>SlidingMenu</code> constructor: <code>container_name</code> will contain the class (or id, see below) of the menu container div; <code>menu_slider_length</code> will specify the width of the images we slide out; and <code>duration</code> will set the animation's length in milliseconds.

<pre><code class="language-javascript">function SlidingMenu ( container_name, menu_slider_width, duration ) // Note the new parameters.
{
        var self = this;
	$( container_name + " .menu_button" ).bind ( "click", self, on_click ); // We bind to the specified element.

	this.effect_duration = duration; // New variable 1.
	this.menu_slider_width = menu_slider_width; // New variable 2.
	this.is_animation_running = false;
	this.active_menu = $($( container_name + " .menu_slider" )[0]);

	this.slide ( this.menu_slider_width ); // We replaced 253 with the arbitrary variable.

}

SlidingMenu.prototype.slide = slide;

// Function to render the animation.
function slide ( width )
{
	this.is_animation_running = true;
	this.active_menu.animate (
	{ 'width' : width },
	this.effect_duration, // Replace 1000 with the duration variable.
	function ()
	{
		this.is_animation_running = false;
	}
	);
}

function on_click ( event )
{
	if ( $(this).next()[0] == active_menu[0] )
	{
		return;
	}
	if ( event.data.is_animation_running )
	{
		return;
	}

	var menu_slider = $(this).next();
	event.data.slide ( 0 );
	this.active_menu = menu_slider;
	event.data.slide ( event.data.effect_duration ); // Slide with the specified amount.
}

var sl = new SlidingMenu( ".menu", 253, 1000 ); // We pass the three new parameters when creating an instance.</code></pre>

We simply replaced the variables with the three new ones where needed. You can see that we could do a lot more customization here; for example, replacing not just the main container name (<code>.menu</code>) but the ones we've been calling <code>.menu_button</code> and <code>menu_slider</code> all along. But we'll leave that up to you.

You could even specify an <code>id</code> for the main container (i.e. <code>#menu</code>) if you'd like. Everything has become a bit friendlier and more flexible all of a sudden.

In the demo below you can specify an arbitrary number for the duration of the animation (in milliseconds) and the width of the images. Play around with it.

Of course, changing the width of the images makes more sense when you use images on your website that are not exactly 253 pixels wide. Then you can simply call the <code>SlidingMenu</code> constructor with the correct width, and you're set.</p>

### Getting a Bit More Complex

Another thing I mentioned at the beginning of this tutorial is that because we're concerned only about the containers of the elements, <code>menu_slider</code> can be any element that has the class <code>menu_slider</code>. So, as a more complex example, <code>menu_slider</code> could be a <code>div</code> containing a list of sub-menu items:

Looking much better, right? Of course, when using it for real, you would add a link to each of those list items, so that when the user clicks on it, it loads the corresponding page.

By the way, if you don't want the text to shrink with the width of the container (as in the example above), then add <code>width: 253px;</code> to your CSS file, where you substitute <code>253px</code> with the desired width. Here is all of the additional CSS that I used for the demo above:

<pre><code class="language-css">.menu .menu_slider ul {
	position : relative;
	top : -100px;
	left : -35px;
	font-size : 12px;
}

.menu .menu_slider img {
	width : 253px;
	height : 158px;
}

.menu .menu_slider ul li {
	list-style : none;
	background : #fff;
	color : #333;
	cursor : pointer;
}

.menu .menu_slider p {
	width : 253px;
	margin-left : 5px;
}</code></pre>

The only thing worth mentioning here is the font size. Because we defined the menu's width, height and pretty much everything else in pixels, also setting the font size to a particular number is better, so that it looks consistent across different browsers.

In addition, you can see that on mouse-over the menu items become clearer and more defined. This is achieved by changing the opacity of the list elements on hover. Instead of using various CSS hacks for cross-browser compatibility, we'll trust jQuery on this one: simply use the <code>fadeTo</code> method to fade in and out:

<pre><code class="language-javascript">$(".menu .menu_slider ul li").bind ( "mouseover", function () {
	$(this).fadeTo ( "fast", "1.0" );
	} );
$(".menu .menu_slider ul li").bind ( "mouseout", function () {
	$(this).fadeTo ( "fast", "0.8" );
	 } );

// This line is used to make them fade out by default.
$(".menu .menu_slider li").fadeTo ( "fast", 0.8 );</code></pre>

## Wrapping Up

Congratulations! You made it! By now you should have a working JavaScript sliding menu. More importantly, you should have some understanding of how it works and how to incorporate your own ideas into this model. Hopefully you've learned something useful in this tutorial. Now, to reap the rewards, all you have to do is grab all of this code we've written and load it on page load, jQuery-style:

<pre><code class="language-javascript">$(document).ready( function() {
    // All code goes here.
});</code></pre>

To make it even easier, here are all the source files for both the simple and complex examples you saw above:

*   [jQuery sliding menu, simple](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c380adb-4085-461d-90b3-434c8260d4bd/simple-jquery-sliding-menu-demo.zip);
*   [jQuery sliding menu with sub-categories](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43ede26c-3696-4f6e-9401-ab35f9acbd64/complex-jquery-sliding-menu-demo.zip).

Remember we talked about integrating your code in your website at the beginning of this tutorial? Well, now you can experiment all you want, see how it works and make the necessary adjustments. For example, if you have static content, you might want to change the trigger from <code>click</code> to <code>mouseover</code>, so that the menu begins sliding as soon as you mouse over it. This way the pages can be loaded when the user clicks on the images or buttons. Or you can play around with various highlighting solutions: maybe put a nice border around the images on mouse-over. It's totally up to you. Have fun!

## What Next?

Well, we can still do a lot here. We still haven't covered optimization and customization. And of course, the animation is still just a simple slide; as I mentioned, you could achieve the same effect with the jQuery accordion plug-in.

But this is where it gets interesting. Now that we have a solid foundation, we can think about some advanced effects and make our little application even easier to use. We'll cover some of these and the aforementioned topics in the next part.

{{< signature "al" >}}

