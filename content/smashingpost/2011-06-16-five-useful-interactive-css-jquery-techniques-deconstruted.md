---
title: '5 Useful Interactive CSS/jQuery Techniques Deconstructed'
slug: five-useful-interactive-css-jquery-techniques-deconstruted
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1733fe70-ad74-4581-8795-8408b27401ef/css-12.jpg
date: 2011-06-16T12:37:38.000Z
author: jon-raasch
summary: >-
  A walk through five interactive techniques that you can start using right now to provide a more engaging user experience. Also, a variety of useful CSS and jQuery tricks that you can leverage when creating your own interactive techniques.
description: >-
  A walk through five interactive techniques that you can start using right now to provide a more engaging user experience. Also, a variety of useful CSS and jQuery tricks that you can leverage when creating your own interactive techniques.
categories:
  - Coding
  - CSS
  - Techniques
  - jQuery
---

With the wide variety of CSS3 and JavaScript techniques available today, it’s easier than ever to create unique interactive websites that delight visitors and provide a more engaging user experience.

In this article, we’ll walk through five interactive techniques that you can start using right now. We’ll cover: Animated text effects, Animated images without GIFs, More engaging drop-down menus, Fancier slideshow navigation, Animated icons for the hover state of buttons.

Besides learning how to accomplish these specific tasks, you’ll also master a variety of **useful CSS and jQuery tricks** that you can leverage when creating your own interactive techniques. The solutions presented here are certainly not perfect, so any thoughts, ideas and suggestions on how you would solve these design problems would be very appreciated.

So, let’s dive in and start building more exciting websites!

{{% feature-panel %}}

## 1. Extruded Text Effect

<figure><a href="https://desandro.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="100157" title="Extruded text effect on David DeSandro's website" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a05ac1d-5093-4e05-a9ef-a6a0766ea0e8/extruded-text-effect.png" alt="Extruded text effect on David DeSandro's site" width="307" height="215" /></a></figure>

The footer of <a href="https://desandro.com/">David DeSandro’s website</a> uses extruded text that animates on mouseover. This interactive text effect is a quick and impressive way to add some flare to your website. With only a few lines of CSS3, we can make the text appear to pop out of the page in **three dimensions**.

*   [View the demo](https://jonraasch.com/demo/extrude-on-hover)

First let’s set up some text (the code is copied from the original site):

<pre><code class="language-markup tmp-html">&lt;span class="extruded"&gt;Extrude Me&lt;/span&gt;</code></pre>

And some basic styling (the code is copied from the original site):

<pre><code class="language-css">body {
    background-color: #444;
    text-align: center;
}

.extruded {
    color: #888;
    font-family: proxima-nova-1, proxima-nova-2, 'Helvetica Neue', Arial, sans-serif;
    font-size: 48px;
    font-weight: bold;
    text-shadow: #000 3px 3px;
}</code></pre>

Here, we’ve applied some basic styles and added a <code>text-shadow</code>. But this text-shadow doesn’t look three-dimensional; to accomplish the extruded effect, we’ll need to **add more text-shadows**:

<pre><code class="language-css">text-shadow: #000 1px 1px, #000 2px 2px, #000 3px 3px;</code></pre>

This will add three different text-shadows to our text, stacked on top of each other to create the three dimensional appearance we want.

### Styling the Hover State

Next, let’s add a hover state with a bigger text-shadow:

<pre><code class="language-css">.extruded:hover {
    color: #FFF;
    text-shadow: #58E 1px 1px, #58E 2px 2px, #58E 3px 3px, #58E 4px 4px, #58E 5px 5px, #58E 6px 6px;
}</code></pre>

Here, we’ve added three more text-shadows to **increase the depth** of the extrude effect. But this effect alone is too flat; we want the text to look like it’s popping off the page. So, let’s reposition the text to make it appear to grow taller from the base of the extruded section:

<pre><code class="language-css">.extruded {
    position: relative;
}

.extruded:hover {
    color: #FFF;
    text-shadow: #58E 1px 1px, #58E 2px 2px, #58E 3px 3px, #58E 4px 4px, #58E 5px 5px, #58E 6px 6px;
    left: -6px;
    top: -6px;
}</code></pre>

Now in the hover state, the extruded text moves up the same distance as our max <code>text-shadow</code> value. We also added <code>position: relative</code>, which must be attached to the base state, not just the hover state, or else it will cause problems when we animate it.

### Animating the Transition

Next, we can add a <a href="https://code.tutsplus.com/tutorials/css-fundamentals-css3-transitions--pre-10922">CSS3 transition</a> to our text to animate the color change and extrude effect:

<pre><code class="language-css">.extruded {
     -moz-transition: all 0.3s ease-out; /* FF3.7+ */
       -o-transition: all 0.3s ease-out; /* Opera 10.5 */
  -webkit-transition: all 0.3s ease-out; /* Saf3.2+, Chrome */
          transition: all 0.3s ease-out;
}</code></pre>

This triggers a smooth animation for our different CSS changes on hover. While it doesn’t work in all browsers, it does degrade nicely to the basic hover effect.

Bringing it all together:

<pre><code class="language-css">body {
    background-color: #444;
    text-align: center;
}

.extruded {
    color: #888;
    font-family: proxima-nova-1, proxima-nova-2, 'Helvetica Neue', Arial, sans-serif; /* the original site doesn't use the @font-face attribute */
    font-size: 48px;
    font-weight: bold;
    text-shadow: #000 1px 1px, #000 2px 2px, #000 3px 3px;
    position: relative;
    -moz-transition: all 0.3s ease-out; /* FF3.7+ */
       -o-transition: all 0.3s ease-out; /* Opera 10.5 */
  -webkit-transition: all 0.3s ease-out; /* Saf3.2+, Chrome */
          transition: all 0.3s ease-out;
}

.extruded:hover {
    color: #FFF;
    text-shadow: #58E 1px 1px, #58E 2px 2px, #58E 3px 3px, #58E 4px 4px, #58E 5px 5px, #58E 6px 6px;
    left: -6px;
    top: -6px;
}</code></pre>

### Shortcomings

While applying several CSS3 text-shadows works well when the text is static, it falls a bit short when used alongside the transition animation.

In short, the biggest text-shadow animates just fine, but the other text-shadows aren’t applied until the animation completes. This causes a quick correction: the browser stutters with a basic drop-shadow before filling in the rest diagonally.

Fortunately, we can make this drawback relatively unnoticeable, provided that we follow a few style guidelines. Basically, we want to hide the bulk of the extruded portion with the top text. This means that we should generally use this effect with bolder fonts, such as the Proxima Nova family used by David DeSandro. Also, we should be careful to avoid text-shadows that are too big for the font. Tweak your settings with this in mind until the animated extrude looks believable.

Finally, this technique **will not work in IE**, because <code>text-shadow</code> is unsupported in all versions of IE (even IE9).

*   [Download the complete example](https://gist.github.com/957199)
*   [View the demo](https://jonraasch.com/demo/extrude-on-hover)

&nbsp;

## 2. Animating A Background Image

<figure><a href="https://lovenonsense.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="100165" title="Animated monster image from Love Nonsense" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/745cf73a-a005-479e-b3e1-9da3511f7d2e/animated-images.png" alt="Animated monster image from Love Nonsense" width="500" height="244" /></a><figcaption>Animating a background image.</figcaption></figure>

While we can easily animate text with a few lines of code, animating an image usually requires bigger and slower assets, such as <a href="https://www.gifmuseum.com/">animated GIFs</a> or Flash or HTML5 video. While complex animations will still depend on these technologies, we can create a compelling illusion of animation using CSS alone.

<a href="https://lovenonsense.com/">Love Nonsense</a> uses a hover effect to alter the color of the images on the website. The trick here is to use a transparent PNG with a background color. The color of the PNG should match the website’s background, so that all of the transparent areas in the PNG show up when filled with a background color. Thus, the PNG should contain the **negative space** of the image you want to display (i.e. the shape you want should be transparent, and everything else should be the same color as the background).

Here’s an example of the Smashing Magazine logo with negative space:

<figure><a href="https://jonraasch.com/demo/animated-image"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="100167" title="Coloring the negative space" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1d92c23-07d6-46fa-82fd-53cc6f172857/inverse-negative-space.jpg" alt="Coloring the negative space of an image" width="500" height="200" /></a><figcaption>Coloring the negative space of an image.</figcaption></figure>

Notice <a href="https://jonraasch.com/demo/animated-image">in the demo</a> how when the background color is set to orange, it starts to look more like the real thing.

### The Code

*   [View the demo](https://jonraasch.com/demo/animated-image)

First, let’s do some basic mark-up:

<pre><code class="language-markup tmp-html">&lt;div class="post-wrapper"&gt;
    &lt;h2 class="post-title"&gt;
        This is the title you hover over

        &lt;img src="knockout-image.png" class="post-image" alt="" /&gt;
    &lt;/h2&gt;

    &lt;p&gt;Some more text here.&lt;/p&gt;
&lt;/div&gt;</code></pre>

Here we include a post with a title, our knock-out image and a paragraph of text.

Next, let’s set up some static styles:

<pre><code class="language-css">.post-wrapper {
    position: relative;
    padding-left: 240px;
}

.post-image {
    position: absolute;
    top: 0;
    left: 0;
    background-color: #bbb;
}

.post-title {
    color: #037072;
}</code></pre>

Here, we’ve set up the post’s wrapper with <code>position: relative</code> and with enough padding on the left side to absolutely position the image to the left of our post. We’ve also added a background color to our image; so now the positive space in our PNG shows up as light gray.

Next, let’s add some hover effects:

<pre><code class="language-css">.post-title:hover {
    color: #d63c25;
}

.post-title:hover .post-image {
    background-color: #f04e36;
}</code></pre>

Now, when we hover over the title or the image, both will change color.

We can take this effect a step further by animating the transition:

<pre><code class="language-css">.post-image {
    -webkit-transition: background-color 400ms ease-in;
    -moz-transition: background-color 400ms ease-in;
    transition: background-color 400ms ease-in;
}

.post-title {
    -webkit-transition: color 400ms ease-in;
    -moz-transition: color 400ms ease-in;
    transition: color 400ms ease-in;
}</code></pre>

Here, we’ve added a <a href="https://code.tutsplus.com/tutorials/css-fundamentals-css3-transitions--pre-10922">CSS3 transition</a> to both the image and the title, which will make for a smooth color change animation.

Unfortunately, CSS3 transitions are not currently supported in IE9. However, even in unsupported browsers, the color change will still occur &mdash; it just won’t have a smooth animation.

If complete cross-browser support for the animation is important, you could always provide a jQuery version of the animation for unsupported browsers. Bear in mind, though, that jQuery’s <a href="https://api.jquery.com/animate/"><code>animate()</code> method</a> does not support color animations, so you’ll need to use a <a href="https://github.com/jquery/jquery-color">color plug-in</a>.

Putting all the CSS together:

<pre><code class="language-css">.post-wrapper {
    position: relative;
    padding-left: 240px;
}

.post-image {
    position: absolute;
    top: 0;
    left: 0;
    background-color: #bbb;
    -webkit-transition: background-color 400ms ease-in;
    -moz-transition: background-color 400ms ease-in;
    transition: background-color 400ms ease-in;
}

.post-title {
    color: #037072;
    -webkit-transition: color 400ms ease-in;
    -moz-transition: color 400ms ease-in;
    transition: color 400ms ease-in;
}

/* add the hover states */

.post-title:hover {
    color: #d63c25;
}

.post-title:hover .post-image {
    background-color: #f04e36;
}</code></pre>

*   [Download the complete example](https://gist.github.com/957217)
*   [View the demo](https://jonraasch.com/demo/animated-image)

&nbsp;

## 3. Mega Dropdown

<a href="https://www.bohemiadesign.co.uk/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="100172" title="Mega dropdown menu on Bohemia" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/197270b4-12d0-4a55-a5e0-b2a0a943962e/mega-dropdown-menu.jpg" alt="Mega dropdown menu on Bohemia" width="500" height="310" /></a>

One common design problem with dropdown menus is that they often contain a lot of items. Instead of presenting all of its items in a long single column, <a href="https://www.bohemiadesign.co.uk/">Bohemia Design</a> uses a **multi-column dropdown**. This approach not only looks great, but provides an opportunity to group the links and highlight the most important ones.

Let’s recreate this menu using CSS and jQuery.

*   [View the demo](https://jonraasch.com/demo/huge-dropdown-menu)

### Building the Tabs

Ideally, we would start with a lean and simple mark-up...

<pre><code class="language-markup tmp-html">&lt;nav&gt;
    &lt;li&gt;&lt;a href="#"&gt;Tab 1&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Tab 2&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Tab 3&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Tab 4&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Tab 5&lt;/a&gt;&lt;/li&gt;
&lt;/nav&gt;</code></pre>

...and use <code>nav li a</code>, <code>nav &gt; li</code> or <code>nav li</code> to style the list items in the navigation. The child selector doesn’t work in IE6 and <code>nav li</code> would cause problems since there are additional LIs nested in the content area of the dropdown. If you absolutely need the site to work for IE6 users as well (and that’s what you sometimes will have to do), you’ll need to have markup similar to the original mark-up in this example:

<pre><code class="language-markup tmp-html">&lt;ul id="main-nav"&gt;
    &lt;li class="main-nav-item"&gt;
        &lt;a href="#" class="main-nav-tab"&gt;Tab 1&lt;/a&gt;
    &lt;/li&gt;

    &lt;li class="main-nav-item"&gt;
        &lt;a href="#" class="main-nav-tab"&gt;Tab 2&lt;/a&gt;
    &lt;/li&gt;

    &lt;li class="main-nav-item"&gt;
        &lt;a href="#" class="main-nav-tab"&gt;Tab 3&lt;/a&gt;
    &lt;/li&gt;

    &lt;li class="main-nav-item"&gt;
        &lt;a href="#" class="main-nav-tab"&gt;Tab 4&lt;/a&gt;
    &lt;/li&gt;

    &lt;li class="main-nav-item"&gt;
        &lt;a href="#" class="main-nav-tab"&gt;Tab 5&lt;/a&gt;
    &lt;/li&gt;
&lt;/ul&gt;</code></pre>

Next, let’s style these five tabs:

<pre><code class="language-css">#main-nav {
    width: 800px;
    height: 50px;
    position: relative;
    list-style: none;
    padding: 0;
}

#main-nav .main-nav-item {
    display: inline;
}

#main-nav .main-nav-tab {
    float: left;
    width: 140px;
    height: 30px;
    padding: 10px;
    line-height: 30px;
    text-align: center;
    color: #FFF;
    text-decoration: none;
    font-size: 18px;
}</code></pre>

Although a lot of the CSS is specific to our example, there are a few important styles to note.

First, we’ve defined a height and width for our overall tab area and matched the total height and width of all five tabs, so that we can position the dropdown correctly. Next, we’ve defined <code>position: relative</code> for the tab wrapper, which will allow us to position the dropdown absolutely.

Then, we added <code>list-style: none</code> to the list wrapper, and <code>display: inline</code> to each list item, to eliminate any list styling.

Finally, we floated all of the tab links to the left.

### Building the Dropdown

Now, let’s build the dropdown mark-up in one of our tab wrappers:

<pre><code class="language-markup tmp-html">&lt;li class="main-nav-item"&gt;
        &lt;a href="#" class="main-nav-tab"&gt;Tab 1&lt;/a&gt;

        &lt;div class="main-nav-dd"&gt;
            &lt;div class="main-nav-dd-column"&gt;
            Column content here
            &lt;/div&gt;
        &lt;/div&gt;

        &lt;div class="main-nav-dd"&gt;
            &lt;div class="main-nav-dd-column"&gt;
            Column content here
            &lt;/div&gt;
        &lt;/div&gt;

        &lt;div class="main-nav-dd"&gt;
            &lt;div class="main-nav-dd-column"&gt;
            Column content here
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/li&gt;</code></pre>

Next, let’s style this dropdown:

<pre><code class="language-css">#main-nav .main-nav-dd {
    position: absolute;
    top: 50px;
    left: 0;
    margin: 0;
    padding: 0;
    background-color: #FFF;
    border-bottom: 4px solid #f60;
}

#main-nav .main-nav-dd-column {
    width: 130px;
    padding: 15px 20px 8px;
    display: table-cell;
    border-left: 1px solid #ddd;
    *float: left;
    *border-left: 0;
}

#main-nav .main-nav-dd-column:first-child {
    border-left: 0;
}</code></pre>

Here, we’ve positioned the dropdown absolutely, directly beneath the first tab.

Let’s set <code>display: table-cell</code> on all of the column wrappers, so that they display next to each other. But <code>table-cell</code> is not supported in IE6 or 7, so we’ve used an <a href="https://paulirish.com/2009/browser-specific-css-hacks/">attribute hack</a> as an alternative for IE6 and 7. This hack places an asterisk (<code>`*`</code>) before each of the attributes that are specific to IE6 and 7.

Thus, we’ve defined a backup for unsupported IEs, which is simply <code>float: left</code>. This works almost as well as <code>display: table-cell</code>, except that the floated elements don’t match each other’s height, so the borders between columns don’t line up. To avoid this minor issue, we simply remove the <code>border-left</code> using the same asterisk hack.

Finally, we remove the left border from the first column for all browsers. Although the <code>:first-child</code> pseudo-class doesn’t work properly in IE6, fortunately it doesn’t make a difference, because we’ve already hidden the borders in these browsers.

### Adding the Interaction

We’ve built the mark-up and styles for our dropdown, but we still need to make the menu interactive. Let’s use jQuery to add a class to show and hide the dropdown:

<pre><code class="language-javascript">$(function() {
    var $mainNav = $('#main-nav');

    $mainNav.children('.main-nav-item').hover(function(ev) {
        // show the dropdown
        $(this).addClass('main-nav-item-active');
    }, function(ev) {
        // hide the dropdown
        $(this).removeClass('main-nav-item-active');
    });
});</code></pre>

Here, we’ve attached a <a href="https://bavotasan.com/tutorials/a-simple-mouseover-hover-effect-with-jquery/">hover listener</a> to each list item, which adds and removes the class <code>main-nav-item-active</code>. Attach this to the list item rather than the tab itself, or else the dropdown will disappear when the user mouses off the tab and into the dropdown area.

Now we can use this class hook to hide and show the dropdown with CSS:

<pre><code class="language-css">#main-nav .main-nav-dd {
    display: none;
}

#main-nav .main-nav-item-active .main-nav-dd {
    display: block;
}</code></pre>

Let’s use the <code>active</code> class to style the active tab:

<pre><code class="language-css">#main-nav .main-nav-item-active .main-nav-tab {
    background-color: #FFF;
    color: #f60;
    -webkit-border-top-left-radius: 5px;
    -webkit-border-top-right-radius: 5px;
    -moz-border-radius-topleft: 5px;
    -moz-border-radius-topright: 5px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}</code></pre>

Here, we’ve changed the background and text colors and rounded the top corners (in supported browsers).

{{% ad-panel-leaderboard %}}

### Positioning the Dropdown

Now the basic mouse interaction has been built and the dropdown displays on mouseover. Unfortunately, it is still not positioned correctly under each tab, so let’s add some more code to our hover events:

<pre><code class="language-javascript">$(function() {
    var $mainNav = $('#main-nav');

    $mainNav.children('.main-nav-item').hover(function(ev) {
        var $this = $(this),
        $dd = $this.find('.main-nav-dd');

        // get the left position of this tab
        var leftPos = $this.find('.main-nav-tab').position().left;

        // position the dropdown

        $dd.css('left', leftPos);

        // show the dropdown
        $this.addClass('main-nav-item-active');
    }, function(ev) {

        // hide the dropdown
        $(this).removeClass('main-nav-item-active');
    });
});</code></pre>

Here, we use jQuery’s <a href="https://api.jquery.com/position/"><code>position()</code> method</a> to get the left offset from the current tab. We then use this value to position the dropdown directly beneath the appropriate tab.

However, with the tabs on the right side, the dropdown menu will end up poking out of the tab area. Besides looking bad, this could lead to **overflow issues**, with portions of the dropdown falling outside of the browser window.

Let’s fix the positioning with some JavaScript:

<pre><code class="language-javascript">$(function() {
    var $mainNav = $('#main-nav'),
    navWidth = $mainNav.width();

    $mainNav.children('.main-nav-item').hover(function(ev) {
        var $this = $(this),
        $dd = $this.find('.main-nav-dd');

        // get the left position of this tab
        var leftPos = $this.find('.main-nav-tab').position().left;

        // get the width of the dropdown
        var ddWidth = $dd.width(),
        leftMax = navWidth - ddWidth;

        // position the dropdown
        $dd.css('left', Math.min(leftPos, leftMax) );

        // show the dropdown
        $this.addClass('main-nav-item-active');
    }, function(ev) {

        // hide the dropdown
        $(this).removeClass('main-nav-item-active');
    });
});</code></pre>

Here, we start by finding the overall width of the tab area. Because recalculating the width for each tab is not necessary, we can define it outside of our hover listener.

Next, we find the width of the dropdown and determine the maximum left value, which is the overall tab width minus the width of the dropdown.

Finally, instead of always positioning the dropdown directly beneath the tab, we use the <a href="https://www.tutorialspoint.com/javascript/math_min.htm"><code>Math.min()</code> method</a> to pick the lowest between the tab offset and the maximum left value.

Thus, we confine the dropdown to the area beneath the tabs and avoid any content issues.

### Other Approaches

While this script is fully functional, we could still improve the **user experience**. Currently, when the user mouses away from the dropdown, the menu hides immediately. You could build a delay using <code>setTimeout()</code> to ensure that the dropdown remains visible when the user mouses away and then quickly mouses back. This creates a better experience, because it avoids hiding the dropdown during accidental movements.

If you’d rather avoid <code>setTimeout()</code>, you could also look into the <a href="https://cherne.net/brian/resources/jquery.hoverIntent.html">hoverIntent jQuery plug-in</a>, which makes fine-tuned control over mouse actions much easier.

Besides improving the user experience, you could also **avoid jQuery altogether** in all browsers except IE6.

Instead of using jQuery’s <code>hover()</code> listener, we could use the CSS pseudo-class <code>:hover</code> to hide and show the dropdown.

One downside with the CSS-only solution is that you can’t build a delay for the <code>:hover</code> pseudo-class.

Also, you will have to position the dropdown manually under each tab to avoid the overflow issues. Alternatively, if you aren’t concerned with overflow issues, you could attach <code>position: relative</code> to each list item and avoid setting any positions manually.

Finally, if you’re supporting IE6, make sure to include the script above as a backup for IE6 (but don’t include it for other browsers).

*   [Download the complete example](https://gist.github.com/957213)
*   [View the demo](https://jonraasch.com/demo/huge-dropdown-menu)

## 4. Animated Slideshow Navigation

<figure><a href="https://mckinney.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="100174" title="Animated slideshow navigation on McKinney" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02ea6295-22b7-4769-a4db-8f4dafc468dc/animated-slideshow-navigation.jpg" alt="Animated slideshow navigation on McKinney" width="500" height="268" /></a><figcaption>Animated slideshow navigation on McKinney.</figcaption></figure>

There are a lot of JavaScript slideshow techniques, but the animated navigation on <a href="https://mckinney.com/">McKinney</a> is a fresh, subtle approach.

### Basic jQuery Slideshow

*   [View the demo](https://jonraasch.com/demo/fancy-slideshow-navigation)

Let’s build something similar. We’ll start with some mark-up for a basic slideshow:

<pre><code class="language-markup tmp-html">&lt;div id="slideshow"&gt;
    &lt;div id="slideshow-reel"&gt;
        &lt;div class="slide"&gt;
            &lt;h1&gt;Slide 1&lt;/h1&gt;
        &lt;/div&gt;

        &lt;div class="slide"&gt;
            &lt;h1&gt;Slide 2&lt;/h1&gt;
        &lt;/div&gt;

        &lt;div class="slide"&gt;
            &lt;h1&gt;Slide 3&lt;/h1&gt;
        &lt;/div&gt;

        &lt;div class="slide"&gt;
            &lt;h1&gt;Slide 4&lt;/h1&gt;
        &lt;/div&gt;

        &lt;div class="slide"&gt;
            &lt;h1&gt;Slide 5&lt;/h1&gt;
        &lt;/div&gt;

        &lt;div class="slide"&gt;
            &lt;h1&gt;Slide 6&lt;/h1&gt;
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;</code></pre>

Here we’ve set up six slides, which can be filled with any content we need. Let’s set up some CSS to display the slides as a horizontal reel:

<pre><code class="language-css">#slideshow {
    width: 900px;
    height: 500px;
    overflow: hidden;
    position: relative;
}

#slideshow-reel {
    width: 5400px;
    height: 450px;
    position: absolute;
    top: 0;
    left: 0;
}

#slideshow-reel .slide {
    width: 900px;
    height: 450px;
    float: left;
    background-color: gray;
}</code></pre>

Here, we’ve defined the dimensions of the slideshow, along with <code>overflow: hidden</code> to hide the other slides in the reel. We’ve also defined the dimensions of the reel: with six slides at 900 pixels each, it is 5400 pixels wide. (You could also just set this to a really high number, like 10000 pixels.) Then, we absolutely positioned the reel inside the slideshow (which has <code>position: relative</code>). Finally, we defined the dimensions for all of the individual slides and floated them to the left to fill up our reel.

### Basic Slideshow Animation

Now, let’s add some jQuery to animate this slideshow:

<pre><code class="language-javascript">$(function() {
    function changeSlide( newSlide ) {
        // change the currSlide value
        currSlide = newSlide;

        // make sure the currSlide value is not too low or high
        if ( currSlide &gt; maxSlide ) currSlide = 0;
        else if ( currSlide &lt; 0 ) currSlide = maxSlide;

        // animate the slide reel
        $slideReel.animate({
            left : currSlide * -900
        }, 400, 'swing', function() {
            // set new timeout if active
            if ( activeSlideshow ) slideTimeout = setTimeout(nextSlide, 1200);
        });
    }

    function nextSlide() {
        changeSlide( currSlide + 1 );
    }

    // define some variables / DOM references
    var activeSlideshow = true,
    currSlide = 0,
    slideTimeout,
    $slideshow = $('#slideshow'),
    $slideReel = $slideshow.find('#slideshow-reel'),
    maxSlide = $slideReel.children().length - 1;

    // start the animation
    slideTimeout = setTimeout(nextSlide, 1200);
});</code></pre>

Here, we’ve started by creating the function <code>changeSlide()</code>, which animates the slide reel. This function accepts an index for the next slide to show, and it checks to make sure that the value isn’t too high or low to be in the reel.

Next, it animates the slide reel to the appropriate position, and then finishes by setting a new <a href="https://www.elated.com/articles/javascript-timers-with-settimeout-and-setinterval/">timeout</a> to trigger the next iteration.

Finally, we’ve built the function <code>nextSlide()</code>, which simply triggers <code>changeSlide()</code> to show the next slide in the reel. This simple function is just a shortcut to be used with <code>setTimeout()</code>.

### The Left and Right Navigation

Next, let’s set up the left and right arrows in the slideshow, starting with the mark-up:

<pre><code class="language-markup tmp-html">&lt;a href="#" id="slideshow-prev"&gt;&lt;/a&gt;
    &lt;a href="#" id="slideshow-next"&gt;&lt;/a&gt;</code></pre>

For simplicity’s sake, we’ve added the mark-up to the HTML source. Appending it to the jQuery is often a better approach, to ensure that the controls appear only when they are usable.

Let’s style these arrows with CSS:

<pre><code class="language-css">#slideshow-prev, #slideshow-next {
    display: block;
    position: absolute;
    top: 190px;
    width: 0;
    height: 0;
    border-style: solid;
    border-width: 28px 21px;
    border-color: transparent;
    outline: none;
}

#slideshow-prev:hover, #slideshow-next:hover {
    opacity: .5;
    filter: alpha(opacity=50);
    -ms-filter:"progid:DXImageTransform.Microsoft.Alpha(Opacity=50)";
}

#slideshow-prev {
    left: 0;
    border-right-color: #fff;
}

#slideshow-next {
    right: 0;
    border-left-color: #fff;
}</code></pre>

We’ve positioned the arrows absolutely within the slideshow frame and added an opacity change on hover. In our example, we’ve used a <a href="https://www.dinnermint.org/blog/css/creating-triangles-in-css/">CSS triangle trick</a> to style the arrows with straight CSS, but feel free to use an image if you want richer graphics.

Finally, let’s build the required interaction into our JavaScript:

<pre><code class="language-javascript">$(function() {
    function changeSlide( newSlide ) {
        // cancel any timeout
        clearTimeout( slideTimeout );

        // change the currSlide value
        currSlide = newSlide;

        // make sure the currSlide value is not too low or high
        if ( currSlide &gt; maxSlide ) currSlide = 0;
        else if ( currSlide &lt; 0 ) currSlide = maxSlide;

        // animate the slide reel
        $slideReel.animate({
            left : currSlide * -900
        }, 400, 'swing', function() {
            // hide / show the arrows depending on which frame it's on
            if ( currSlide == 0 ) $slidePrevNav.hide();
            else $slidePrevNav.show();

            if ( currSlide == maxSlide ) $slideNextNav.hide();
            else $slideNexNav.show();

            // set new timeout if active
            if ( activeSlideshow ) slideTimeout = setTimeout(nextSlide, 1200);
        });

        // animate the navigation indicator
        $activeNavItem.animate({
            left : currSlide * 150
        }, 400, 'swing');
    }

    function nextSlide() {
        changeSlide( currSlide + 1 );
    }

    // define some variables / DOM references
    var activeSlideshow = true,
    currSlide = 0,
    slideTimeout,
    $slideshow = $('#slideshow'),
    $slideReel = $slideshow.find('#slideshow-reel'),
    maxSlide = $slideReel.children().length - 1,
    $slidePrevNav = $slideshow.find('#slideshow-prev'),
    $slideNextNav = $slideshow.find('#slideshow-next');

    // set navigation click events

    // left arrow
    $slidePrevNav.click(function(ev) {
        ev.preventDefault();

        activeSlideshow = false;

        changeSlide( currSlide - 1 );
    });

    // right arrow
    $slideNextNav.click(function(ev) {
        ev.preventDefault();

        activeSlideshow = false;

        changeSlide( currSlide + 1 );
    });

    // start the animation
    slideTimeout = setTimeout(nextSlide, 1200);
});</code></pre>

Here, we’ve added quite a bit of new interaction. First, look at the bottom of this script, where we’ve added click event listeners to both of our navigational items.

In these functions, we have first set <code>activeSlideshow</code> to <code>false</code>, which disables the automatic animation of the reel. This provides a better user experience by allowing the user to control the reel manually. Then, we trigger either the previous or next slide using <code>changeSlide()</code>. Next, in the <code>changeSlide()</code> function, we’ve added a clearTimeout(). This works in conjunction with the <code>activeSlideshow</code> value, cancelling any hanging iteration from a <code>setTimeout</code>.

Finally, in the callback of the <code>animate()</code> function, we’ve added some code to hide and show the arrow navigation. This hides the left arrow when the slideshow is showing the left-most slide, and vice versa.

### Animating the Bottom Navigation

The basic slideshow works with the previous and next arrows. Let’s take it to the next level by adding the animated navigation. Please note that I am using a more complex markup because it avoids the use of images and is ultimately simpler. It would have to use three background images otherwise &mdash; one for the center sections and one for each cap to allow the clickable areas to be larger). However, you could clean up the bottom navigation with a background-image.

Here is the jQuery code for animation:

<pre><code class="language-javascript">$(function() {
    function changeSlide( newSlide ) {
        // cancel any timeout
        clearTimeout( slideTimeout );

        // change the currSlide value
        currSlide = newSlide;

        // make sure the currSlide value is not too low or high
        if ( currSlide &gt; maxSlide ) currSlide = 0;
        else if ( currSlide &lt; 0 ) currSlide = maxSlide;

        // animate the slide reel
        $slideReel.animate({
            left : currSlide * -900
        }, 400, 'swing', function() {
            // hide / show the arrows depending on which frame it's on
            if ( currSlide == 0 ) $slidePrevNav.hide();
            else $slidePrevNav.show();

            if ( currSlide == maxSlide ) $slideNextNav.hide();
            else $slideNextNav.show();

            // set new timeout if active
            if ( activeSlideshow ) slideTimeout = setTimeout(nextSlide, 1200);
        });

        // animate the navigation indicator
        $activeNavItem.animate({
            left : currSlide * 150
        }, 400, 'swing');
    }

    function nextSlide() {
        changeSlide( currSlide + 1 );
    }

    // define some variables / DOM references
    var activeSlideshow = true,
    currSlide = 0,
    slideTimeout,
    $slideshow = $('#slideshow'),
    $slideReel = $slideshow.find('#slideshow-reel'),
    maxSlide = $slideReel.children().length - 1,
    $slidePrevNav = $slideshow.find('#slideshow-prev'),
    $slideNextNav = $slideshow.find('#slideshow-next'),
    $activeNavItem = $slideshow.find('#active-nav-item');

    // set navigation click events

    // left arrow
    $slidePrevNav.click(function(ev) {
        ev.preventDefault();

        activeSlideshow = false;

        changeSlide( currSlide - 1 );
    });

    // right arrow
    $slideNextNav.click(function(ev) {
        ev.preventDefault();

        activeSlideshow = false;

        changeSlide( currSlide + 1 );
    });

    // main navigation
    $slideshow.find('#slideshow-nav a.nav-item').click(function(ev) {
        ev.preventDefault();

        activeSlideshow = false;

        changeSlide( $(this).index() );
    });

    // start the animation
    slideTimeout = setTimeout(nextSlide, 1200);
});</code></pre>

We’ve added a couple of things to our script.

First, we’ve included a second animation in <code>changeSlide()</code>, this time to animate the active indicator in the navigation. This <code>animate()</code> is basically the same as the one we built for the reel, the main difference being that we want to move it only <code>150px</code> per slide.

Finally, we added a click event listener to the items in the bottom navigation. Similar to the arrow navigation, we start by disabling the automatic animation, setting <code>activeSlideshow</code> to <code>false</code>. Next, we trigger <code>changeSlide()</code>, passing in the index of whichever slide was clicked, which is easy to determine using jQuery’s <a href="https://api.jquery.com/index/"><code>index()</code></a> method.

Now the slideshow navigation animation is complete and ready to impress your visitors.

*   [Download the complete example](https://gist.github.com/957203)
*   [View the demo](https://jonraasch.com/demo/fancy-slideshow-navigation)

## 5. Animated Icons

<figure><a href="https://css-tricks.com"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="100175" title="Animated icons on CSS Tricks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a497147f-8259-4229-945e-3bddd586f82b/animated-icons-on-css-tricks.png" alt="Animated icons on CSS Tricks" width="500" height="143" /></a><figcaption>Animated icons on CSS Tricks.</figcaption></figure>

<a href="https://css-tricks.com">CSS-Tricks</a> has a simple but elegant effect in its footer when the user mouses over various buttons. Besides the color changing and an icon being added, the effect is animated in browsers that support transition, making the icon appear to **slide into place**.

*   [View the demo](https://jonraasch.com/demo/animated-icons)

Let’s create a similar effect, starting with some mark-up:

<pre><code class="language-markup tmp-html">&lt;a href="#" class="hover-panel"&gt;
    &lt;h3&gt;Panel Title&lt;/h3&gt;

    &lt;p&gt;Additional information about the panel goes in a paragraph here&lt;/p&gt;
&lt;/a&gt;</code></pre>

One thing to note about this mark-up is that it has block elements nested in an <code>&lt;a&gt;</code> element, which makes sense semantically, but it’s valid only if you’re using the HTML5 doc type.

### Styling the Buttons

Let’s set up some basic CSS to style the block in its natural (non-hovered) state:

<pre><code class="language-css">.hover-panel {
    background-color: #E6E2DF;
    color: #B2AAA4;
    float: left;
    height: 130px;
    width: 262px;
    margin: 0 10px 10px 0;
    padding: 15px;
}

.hover-panel h3 {
    font-family: tandelle-1, tandelle-2, Impact, Sans-serif, sans;
    font-size: 38px;
    line-height: 1;
    margin: 0 0 10px;
    text-transform: uppercase;
}

.hover-panel p {
    font-size: 12px;
    width: 65%;
}</code></pre>

Now let’s add a static hover effect to change some of the colors and add a drop shadow:

<pre><code class="language-css">.hover-panel:hover {
    background-color: #237ABE;
}

.hover-panel:hover h3 {
    color: #FFF;
    text-shadow: rgba(0, 0, 0, 0.398438) 0px 0px 4px;
}

.hover-panel:hover p {
    color: #FFF:
}</code></pre>

Finally, let’s add a background image that pops into place on hover:

<pre><code class="language-css">.hover-panel {
    background-image: url(hover-panel-icon.png);
    background-position: 292px 10px;
    background-repeat: no-repeat;
}

.hover-panel:hover {
    background-position: 180px 10px;
}</code></pre>

Here, we’ve added a few important styles to accomplish the hover effect. First, we’ve attached the background image to our <code>.hover-panel</code>. This is normally positioned outside of the button, but on mouseover, it is placed correctly. Also, note that we’ve placed it off to the right side of the panel, so that when we apply the transition animation, the icon will slide in from the right.

### Animating the Transition

Finally, let’s add the transition:

<pre><code class="language-css">.hover-panel {
     -moz-transition: all 0.2s ease; /* FF3.7+ */
       -o-transition: all 0.2s ease; /* Opera 10.5 */
  -webkit-transition: all 0.2s ease; /* Saf3.2+, Chrome */
          transition: all 0.2s ease;
}</code></pre>

The transition effect triggers the animation of the background image. Because we’ve flagged it to apply to <code>all</code> attributes, the transition will also be applied to the <code>background-color</code> change that we applied above.

Although this works in most modern browsers, it will not work in IE9. But even in unsupported browsers, the user will see the color change and icon; they just won’t see the animation effect.

On most websites, this enhancement wouldn’t be necessary for all users. But if support is a priority, look into this <a href="https://jonraasch.com/blog/graceful-degradation-with-css3#transitions">jQuery back-up</a>.

Finally, let’s bring all of the styles together:

<pre><code class="language-css">.hover-panel {
    background-color: #E6E2DF;
    background-image: url(hover-panel-icon.png);
    background-position: 292px 10px;
    background-repeat: no-repeat;
    color: #B2AAA4;
    display: block;
    float: left;
    height: 130px;
    width: 262px;
    margin: 0 10px 10px 0;
    padding: 15px;
     -moz-transition: all 0.2s ease; /* FF3.7+ */
       -o-transition: all 0.2s ease; /* Opera 10.5 */
  -webkit-transition: all 0.2s ease; /* Saf3.2+, Chrome */
          transition: all 0.2s ease;
}

.hover-panel h3 {
    font-family: tandelle-1, tandelle-2, Impact, Sans-serif, sans;
    font-size: 38px;
    line-height: 1;
    margin: 0 0 10px;
    text-transform: uppercase;
}

.hover-panel p {
    font-size: 12px;
    width: 65%;
}

.hover-panel:hover {
    background-color: #237ABE;
    background-position: 180px 10px;
}

.hover-panel:hover h3 {
    color: #FFF;
    text-shadow: rgba(0, 0, 0, 0.398438) 0px 0px 4px;
}

.hover-panel:hover p {
    color: #FFF:
}</code></pre>

*   [Download the complete example](https://gist.github.com/957236)
*   [View the demo](https://jonraasch.com/demo/animated-icons)

## Final Thoughts

In this article, we’ve walked through a variety of interactive techniques that can add a bit of style and creativity to your website. Used correctly, techniques like these enhance websites, creating a more engaging and memorable user experience. But be subtle with the interactivity, ensuring that the bells and whistles do not get in the way of the website’s primary function, which is to **providing meaningful content**.

What do you think of the techniques presented here? Do you know of any ways to improve these scripts? What are some other interactive techniques that you’ve seen around the Web?

*Image source: <a href="https://www.flickr.com/photos/sdasmarchives/5018420677/">San Diego Air &amp; Space Museum Archives</a>*

{{% ad-panel-leaderboard %}}

### Further Reading

*   [5 Useful CSS/jQuery Coding Techniques For Dynamic Websites](https://www.smashingmagazine.com/2010/09/5-coding-techniques-for-more-dynamic-websites/)
*   [Useful jQuery Function Demos For Your Projects](https://www.smashingmagazine.com/2012/05/50-jquery-function-demos-for-aspiring-web-developers/)
*   [50 Useful New jQuery Techniques and Tutorials](https://www.smashingmagazine.com/2009/08/50-useful-new-jquery-techniques/)
*   [How To Migrate From jQuery To Next.js](https://www.smashingmagazine.com/2021/07/migrate-jquery-nextjs/)

{{< signature "al, mrn" >}}
