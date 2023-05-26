---
title: 'Designers: Start Coding With uilang'
slug: designers-start-coding-with-uilang
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa043ffd-26fe-4126-aa35-dd2c5a13d847/demo-uilang-preview-opt.jpg
date: 2015-02-11T23:22:53.000Z
author: benjamin-de-cock
description: >-
  **Editor's Note**: _Designers could learn how to code, and developers could
  learn how to design. Sometimes it might not be an option. In this article, the
  author makes a suggestion to designers without coding skills on how to start
  crafting code. You might want to take the suggested tool with a grain of salt
  (or not) but the idea might be worth looking into._

  Designers have widely adopted HTML and CSS for a while now. They usually feel
  comfortable enough to implement their own designs, at least in a static form.
  However, they’re often intimidated by JavaScript — and rightly so! HTML and
  CSS are declarative and, I’d argue, closer to design than programming.

  JavaScript, on the other hand, is “real” programming. This means you not only
  have to learn a whole new and complex syntax but also have to “learn how to
  think.” The barriers to entry are high and prevent many designers from taking
  the plunge. _uilang_ tries to fix that.
categories:
  - Coding
  - CSS
  - Techniques
  - HTML
---
**Editor's Note**: _Designers could learn how to code, and developers could learn how to design. Sometimes it might not be an option. In this article, the author makes a suggestion to designers without coding skills on how to start crafting code. You might want to take the suggested tool with a grain of salt (or not) but the idea might be worth looking into._

Designers have widely adopted HTML and CSS for a while now. They usually feel comfortable enough to implement their own designs, at least in a static form. However, they’re often intimidated by JavaScript — and rightly so! HTML and CSS are declarative and, I’d argue, closer to design than programming.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Team Collaboration And Closing Efficiency Gaps In Responsive Design](https://www.smashingmagazine.com/2014/05/team-collaboration-closing-efficiency-gaps-responsive-design/)
*   [Designers And Developers Playing Nice](https://www.smashingmagazine.com/2011/05/two-cats-in-a-sack-designer-developer-discord/)
*   [<span class="headline">Developers “Own” The Code, Designers “Own” The Experience?</span>](https://www.smashingmagazine.com/2016/08/developers-own-code-should-designers-own-experience/)
*   [How To Effectively Communicate With Developers](https://www.smashingmagazine.com/2009/08/how-to-effectively-communicate-with-developers/)

JavaScript, on the other hand, is “real” programming. This means you not only have to learn a whole new and complex syntax but also have to “learn how to think.” The barriers to entry are high and prevent many designers from taking the plunge. [uilang](https://uilang.com) tries to fix that.

{{% feature-panel %}}

This article will introduce you to uilang’s philosophy and syntax. We’ll start with a simple example to get you comfortable with the basics, before moving to something more exciting. At the end of this tutorial, you’ll (hopefully!) be able to code many typical interface widgets, such as popovers, tabs, overlays and much, much more.</p>

## The Bridge Between Designers And Developers

I strongly believe that designers should code the interfaces they design. They shouldn’t necessarily write production-ready code, but they should **design the behaviors**. Designers love these things. They could spend hours tweaking an animation delay or finding the right cubic-bezier curve. They usually just lack some technical skills to do so.

uilang tries to facilitate the communication between designers and developers by giving designers an extremely simple tool to prototype their interfaces. uilang reads like plain English, uses a one-line syntax declared right in the HTML and provides very few options in order to make its learning process and adoption as fast and easy as possible. We’ll cover the syntax in detail later, but here’s a sneak peek at it:

<pre><code class="language-markup">
clicking on "button" toggles class "visible" on "div"
</code></pre>

uilang is not exclusively a prototyping tool, though. It can safely be used on production websites to create, for example, tabs, photo galleries, popovers and more. Let’s see how it works!

## Getting Started

uilang is based on a dead simple principle: manipulating classes on your elements. By just adding and removing classes when something is clicked, we can show, hide, transform and animate elements using CSS. This simple logic gives you endless possibilities. Let’s explore one of them by creating a simple notification banner like this:

See the Pen [bNWaVz](https://codepen.io/bdc/pen/bNWaVz/) by Benjamin De Cock ([@bdc](https://codepen.io/bdc)) on [CodePen](https://codepen.io).

We’ll start with the HTML markup, which is pretty straightforward:

<pre><code class="language-markup">
&lt;div id="notification"&gt;
  &lt;p&gt;You have 3 unread messages.&lt;/p&gt;
  &lt;button class="hide"&gt;Hide&lt;/button&gt;
&lt;/div&gt;
</code></pre>

We’ll now use uilang to define a simple behavior: When the user clicks on an element that has a `hide` class, we’ll add a `hidden` class to the element that has a `notification` ID. The translation in actual uilang code looks almost the same as the explanation above:

<pre><code class="language-markup">
clicking on ".hide" adds class "hidden" on "#notification"
</code></pre>

This line of code should be written in a simple `<code>` element, right in the HTML. uilang will automatically find the `<code>` element containing your code and will ignore other `<code>` elements that you might have on the page. Additionally, you’ll have to download and insert the [uilang.js library](https://uilang.com/lib/production/uilang.js) (1 KB).</p>

<p>While both your <code>&lt;code&gt;</code> and <code>&lt;script&gt;</code> elements can 
theoretically be inserted anywhere on the page, it's recommended to place them at the very end of the document, just before the closing <code>&lt;/body&gt;</code> tag:

<pre><code class="language-markup">
&lt;body&gt;
  &lt;!-- Your content --&gt;

  &lt;script src="uilang.js"&gt;&lt;/script&gt;

  &lt;code&gt;
    &lt;!-- Your uilang code --&gt;
  &lt;/code&gt;
&lt;/body&gt;
</code></pre>

<p>By respecting that order, you're making sure to reach the best rendering performance. Thereby, your final HTML markup for the notification banner will look like this:</p>

<pre><code class="language-markup">
&lt;body&gt;
  &lt;div id="notification"&gt;
    &lt;p&gt;You have 3 unread messages.&lt;/p&gt;
    &lt;button class="hide"&gt;Hide&lt;/button&gt;
  &lt;/div&gt;

  &lt;script src="uilang.js"&gt;&lt;/script&gt;

  &lt;code&gt;
    clicking on ".hide" adds class "hidden" on "#notification"
  &lt;/code&gt;
&lt;/body&gt;
</code></pre>

<p>We’re almost done! Now that the behavior has been defined, we’ll rely on CSS to fade out that notification banner once the <code>hidden</code> class has been applied to it:</p>

<pre><code class="language-css">
#notification {
  transition: .8s
}
#notification.hidden {
  opacity: 0
}
</code></pre>

<p>Congrats! You now know how to code! You might not realize it yet, but this simple logic will let you build a wide range of widgets and interactions. Let’s have a closer look at the options provided by the syntax.</p>

## Syntax

<p>The syntax can be split into four parts:</p>

<pre><code class="language-markup">
clicking on ".hide"(1) adds(2) class "hidden"(3) on "#notification"(4)
</code></pre>

<ol>
<li>any CSS selector</li>

<li><code>adds</code>, <code>removes</code> or <code>toggles</code></li>

<li>any class name</li>

<li>any CSS selector or the <code>target</code> keyword (which selects the clicked element)</li>
</ol>

<p>That’s all you need to learn. Keep in mind that uilang is basically just HTML, so you can comment the code similarly:</p>

<pre><code class="language-markup">
&lt;code&gt;
  &lt;!-- I'm a comment --&gt;
  clicking on ".hide" adds class "hidden" on "#notification"

  &lt;!-- I'm another comment --&gt;
  clicking on "li a:first-child" toggles class "active" on "target"
&lt;/code&gt;
</code></pre>

<p>Please note that uilang only supports click events. Hover effects can usually be achieved in CSS, and other events are simply beyond the scope of this language.</p>

<p>We’ve now covered the basics of uilang. It’s time to build a more advanced demo!</p>

## Apple-Like Explore Menu

<p>We’ll create a collapsible, animated menu similar to the kind you can find on <a href="https://apple.com">Apple’s website</a>. Check out <a href="https://demos.uilang.com/explore-menu/" />the demo</a> to see the result.</p>

<figure><a href="https://demos.uilang.com/explore-menu/" /><img loading="lazy" decoding="async" alt="uilang demo: explore menu" property="image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa043ffd-26fe-4126-aa35-dd2c5a13d847/demo-uilang-preview-opt.jpg" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0c137a5-bd86-4d6c-99ac-c77709b04e55/demo-uilang-large-preview-opt.jpg">See large version</a>)</figcaption></figure>

### HTML Markup

<p>Nothing fancy, really, just a simple link to toggle the navigation, and the <code>nav</code> element containing our list of links:</p>

<pre><code class="language-markup">
&lt;a class="explore" href="#"&gt;Explore&lt;/a&gt;

&lt;nav&gt;
  &lt;ul&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/1.jpg"&gt;West Coast&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/2.jpg"&gt;Venice&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/3.jpg"&gt;Peyto Lake&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/4.jpg"&gt;Iceland&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/5.jpg"&gt;Golden Gate&lt;/a&gt;
  &lt;/ul&gt;
&lt;/nav&gt;
</code></pre>

<p>Now, adding the toggling behavior with uilang will be extremely simple:</p>

<pre><code class="language-markup">
&lt;code&gt;
  clicking on ".explore" toggles class "open" on "nav"
&lt;/code&gt;
</code></pre>

<p>We’ll then use this <code>open</code> class in our style sheet to show and hide the <code>nav</code>. Just before we do that, let’s add a few things to complete our HTML markup: a meta tag for mobile users, the link to our style sheet and, obviously, the uilang.js library! The whole HTML might now look like this:</p>

<pre><code class="language-markup">
&lt;!doctype html&gt;
&lt;meta charset="utf-8"&gt;
&lt;meta name="viewport" content="initial-scale=1"&gt;
&lt;title&gt;Explore menu&lt;/title&gt;
&lt;link rel="stylesheet" href="style.css"&gt;

&lt;a class="explore" href="#"&gt;Explore&lt;/a&gt;

&lt;nav&gt;
  &lt;ul&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/1.jpg"&gt;West Coast&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/2.jpg"&gt;Venice&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/3.jpg"&gt;Peyto Lake&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/4.jpg"&gt;Iceland&lt;/a&gt;
    &lt;li&gt;
      &lt;a href="#"&gt;&lt;img alt src="images/5.jpg"&gt;Golden Gate&lt;/a&gt;
  &lt;/ul&gt;
&lt;/nav&gt;

&lt;script src="uilang.js"&gt;&lt;/script&gt;

&lt;code&gt;
  clicking on ".explore" toggles class "open" on "nav"
&lt;/code&gt;
</code></pre>

<p><strong>Note</strong>: For those wondering about the brevety of the code, keep in mind HTML5 considers as optional the <code>&lt;html&gt;</code>, <code>&lt;head&gt;</code> and <code>&lt;body&gt;</code> tags. Feel free to adopt a different style if you have another preference!</p>

<h4>CSS: Where The Magic Happens</h3>

As always with uilang, the interesting parts of the code are in the style sheet. uilang’s role is exclusively to _define_ the behaviors, not to execute them.

Let’s start by styling and positioning our elements, so that our navigation is ready to be manipulated with uilang. I won’t go into much detail — I assume you’re already comfortable with basic, standard CSS — so I’ve only commented some parts of the code. Please note that irrelevant style declarations, such as for fonts and colors, have been omitted for clarity.</p>

<pre><code class="language-css">
body {
  background: #f3f3f3;
}

.explore {
  /* Make sure the Explore link stays above the nav */
  position: absolute;
  z-index: 1;
}

nav {
  background: #fff;
  box-shadow: 0 1px 2px rgba(0,0,0,.15);
}

nav ul {
  /* Allow mobile-friendly horizontal scrolling when the browser isn't wide enough */
  overflow: auto;
  -webkit-overflow-scrolling: touch;
  /* Force the thumbs to display in a row */
  white-space: nowrap;
  padding: 80px 40px 40px;
}

nav li {
  display: inline-block;
}
</code></pre>

Onto the interesting part: coding the toggling behavior! We’ll need two things:

1.  By default, the `nav` and the thumbs should be hidden. This means we need to initially slide up the `nav` and make the `nav` and images transparent.
2.  When the `open` class defined in our uilang code is applied to the `nav`, we need to reverse the default state: slide down the `nav` and fade in everything.

Step 1 is pretty easy: We’ll use `translateY(-100%)` to slide the `nav` up, `opacity: 0;` to hide the `nav` and images, and `transition` to animate these elements when the class is applied.</p>

<pre><code class="language-css">
nav, nav li {
  opacity: 0;
}

nav {
  -webkit-transform: translateY(-100%);
  transform: translateY(-100%);
  transition: .4s;
}

nav li {
  transition: .3s;
}
</code></pre>

This is not immediately related to uilang but, because uilang does rely on CSS for transitions and animations, we should probably remember a few important principles:

*   You can safely and smoothly animate only two properties: `opacity` and `transform`. Force yourself to stick with them.
*   When only the duration is specified in the `transition` shorthand property, _all_ properties that might change in future will be animated and will use `ease` as their timing function.
*   Keep your animations fast! Animations are important because they help users to understand the flow between two states, but they should never get in the way. A good `transition-duration` is usually between 200 and 800 milliseconds.
*   While standard easing keywords are sometimes acceptable (such as with this demo), custom cubic-bezier curves are often preferable. Many tools enable you to find the right curve, such as Matthew Lein’s [Ceaser](https://matthewlein.com/ceaser/).
*   The examples in this tutorial use CSS transitions, but feel free to use CSS animations instead when needed! The principle is exactly the same, and keyframes might provide a finer level of control.

Now that our default state has been set up, we can go to step 2 and code the “open” state, which basically means reverting step 1 to the default values for the `open` class:

<pre><code class="language-css">
nav.open, nav.open li {
  opacity: 1;
  -webkit-transform: none;
  transform: none;
}

nav.open li {
  /* Wait for the nav to slide down a bit before starting the animation on the thumbs */
  transition-delay: .3s;
}
</code></pre>

Boom! You now have a fully functional animated navigation menu. A few things are missing that would make it truly great, though, starting with the scale animation on the images. If you look closely at [the demo](https://demos.uilang.com/explore-menu/), you’ll notice that the images not only fade in when they appear but also zoom in a little. Let’s add that behavior by making them slightly smaller by default:

<pre><code class="language-css">
nav li {
  -webkit-transform: scale(.8);
  transform: scale(.8);
}
</code></pre>

We’ve already defined that `nav.open li` will reverse to `transform: none;` and that all properties will animate, so there’s nothing more to add.

Good! We’re almost done, but one important thing is missing: changing the icon on the “Explore” link when the `nav` is open or closed. To do that, we’ll need to define a new rule in our uilang code. We’re currently toggling an `open` class on the navigation to show and hide it; we’ll need to do something similar for the link itself.</p>

<pre><code class="language-markup">
&lt;code&gt;
  clicking on ".explore" toggles class "close" on "target"
  clicking on ".explore" toggles class "open" on "nav"
&lt;/code&gt;
</code></pre>

Here, `target` represents the clicked element. In this case, you could have just reused `.explore` instead of `target`. However, that wouldn’t be the same if you had multiple “Explore” links on the same page (`.explore` matches any “Explore” link, whereas `target` selects only the clicked “Explore” link).

Back to the CSS. We’re going to use pseudo-elements to display our icons. `.explore::before` will represent our grid icon (visible when the navigation is closed), and `.explore::after` will display the cross when the navigation is open. Both will benefit from the same `transition-duration`.</p>

<pre><code class="language-css">
.explore::before, .explore::after {
  content: "";
  position: absolute;
  left: 0;
  transition: .25s;
}

.explore::before {
  background: url(grid.svg);
}

.explore::after {
  background: url(close.svg);
  /* Hidden and scaled up by default */
  opacity: 0;
  -webkit-transform: scale(1.8);
  transform: scale(1.8);
}
</code></pre>

The grid icon is already visible; the close icon is hidden but correctly positioned, ready to fade in as soon as “Explore” is clicked. We just have to reverse the default state when the `close` class defined in our uilang code is applied to `.explore`:

<pre><code class="language-css">
/* When the nav is open, hide and rotate the grid icon… */
.explore.close::before {
  opacity: 0;
  -webkit-transform: rotate(45deg) scale(.8);
  transform: rotate(45deg) scale(.8);
}

/* … and display the close icon */
.explore.close::after {
  opacity: 1;
  -webkit-transform: none;
  transform: none;
}
</code></pre>

That’s it! We’ve achieved this pretty cool effect with just two lines of uilang and a few CSS declarations. Note that, while the uilang code might not be used in production by the developers you collaborate with, your CSS _is_ production-ready. Most of the prototyping tools out there force you to build mockups outside of the actual HTML and CSS, which forces developers to reimplement your animations, delays, easings and so on. Details get lost all the time. With uilang, developers can just **reuse your CSS and focus exclusively on reimplementing the logic in JavaScript**.</p>

## Icing On The Cake

As a bonus, let’s end this tutorial by having some fun with CSS! The grid and close icons that we’re using on the “Explore” link are actually pretty simple, and using images for them (as we’re doing) would be a shame when we could just draw them in CSS. Let’s do this!

The grid icon is the most interesting one. While it might initially seem counterintuitive, we’re going to use gradients to draw it. The idea is that each of the nine squares will be drawn as a gradient from black to black. When you create a CSS gradient, you’re basically generating an image on the fly. This (background) image can then be sized and positioned anywhere.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8311e49a-abf7-4ee4-9c41-427218c40692/grid-icon-info-details-large-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/817f7866-5647-4bd6-a1e9-3fa46b558cae/grid-icon-info-details-opt.png" alt="grid-icon-info-details-opt" width="500" height="164" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8311e49a-abf7-4ee4-9c41-427218c40692/grid-icon-info-details-large-preview.png">See large version</a>)</figcaption></figure>

Here’s the translation in CSS ([available on CodePen](https://codepen.io/bdc/pen/emYpGJ)):

<pre><code class="language-css">
.explore::before {
  width: 13px;
  height: 13px;
  background-image: linear-gradient(#000, #000),
                    linear-gradient(#000, #000),
                    linear-gradient(#000, #000),
                    linear-gradient(#000, #000),
                    linear-gradient(#000, #000),
                    linear-gradient(#000, #000),
                    linear-gradient(#000, #000),
                    linear-gradient(#000, #000),
                    linear-gradient(#000, #000);
  background-position: 0 0, 50% 0, 100% 0,
                       0 50%, 50% 50%, 100% 50%,
                       0 100%, 50% 100%, 100% 100%;
  background-repeat: no-repeat;
  background-size: 3px 3px;
}
</code></pre>

It’s verbose and arguably crazy, but keep in mind that, while we’re essentially doing it for fun, this technique comes with real advantages, the most important one being undoubtedly the HTTP request you save from not requesting a file.

The close icon is much simpler but still requires some tricks to make it look great. We’ll use a similar technique: drawing a gradient from black to black for each bar of the cross in order to form a plus sign, then rotating the plus to make it look like a cross. To prevent the lines from looking jagged because of the 45-degree rotation, we’ll scale up the icon a little using the `transform` property, which provides us with decent antialiasing.</p>

<pre><code class="language-css">
.explore::after {
  width: 11px;
  height: 11px;
  background-image: linear-gradient(#000, #000),
                    linear-gradient(#000, #000);
  background-position: 50% 0, 0 50%;
  background-repeat: no-repeat;
  background-size: 1px 100%, 100% 1px;
  -webkit-transform: rotate(45deg) scale(1.4);
  transform: rotate(45deg) scale(1.4);
}
</code></pre>

## Go Create!

CSS is powerful, performant yet remarkably easy to use. uilang wants to stay invisible in your workflow and act as a gateway to using CSS to code interactions. After all, CSS might be the best “user interface” for creating prototypes.</p>

### Resources

*   [uilang](https://uilang.com/)
*   [uilang](https://github.com/bendc/uilang), GitHub
*   [The Educational Side of uilang: Or How to De-Dramatize Getting Into Programming](https://medium.com/@bdc/the-educational-side-of-uilang-92d39da94c13),” Benjamin De Cock  
    Explains the philosophy behind uilang
*   [uilang Transpiler](https://transpiler.uilang.com)  
    Transpiles uilang to JavaScript
*   “[Sublime Text Snippet for uilang](https://medium.com/@zackcote_/sublime-text-snippet-for-uilang-efb05fbed0d),” Zack Cote

{{< signature "ds, il, al" >}}

