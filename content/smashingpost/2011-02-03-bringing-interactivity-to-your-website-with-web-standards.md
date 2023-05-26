---
title: How To Bring Interactivity To Your Website With Web Standards
slug: bringing-interactivity-to-your-website-with-web-standards
image: null
date: 2011-02-03T14:31:02.000Z
author: david-bushell
description: >-
  Adding interactivity and animations to a design doesn't have to be complicated
  or make the website inaccessible when you use modern Web standards. In this
  article, we’ll explore several examples and theories that employ CSS, HTML,
  SVG, the `canvas` element and JavaScript. Some of these techniques you'll
  know, others you may not have considered. Let's start with the basics.
  "Bringing Interactivity To Your Website With Web
  Standards")](https://www.smashingmagazine.com/?p=85432)

  Manipulating HTML with JavaScript is the most common method of adding
  interactivity to a website. But before you start using JavaScript, having a
  strong understanding of the CSS visual formatting model and box model is
  important. They are vital to making sense of how HTML elements can be
  manipulated visually. When you dynamically change the style of an HTML
  element, it will flow with and react to the rest of the document. Learning to
  anticipate and control what is affected can be difficult.
categories:
  - Coding
  - Techniques
  - Animation
---
Adding interactivity and animations to a design doesn't have to be complicated or make the website inaccessible when you use modern Web standards. In this article, we’ll explore several examples and theories that employ CSS, HTML, SVG, the <code>canvas</code> element and JavaScript. Some of these techniques you'll know, others you may not have considered. Let's start with the basics.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Usability Do’s And Don’ts For Interactive Design](https://www.smashingmagazine.com/2010/04/usability-dos-and-donts-for-interactive-design/)
*   [Interaction Design Tactics For Visual Designers](https://www.smashingmagazine.com/2011/09/interaction-design-tactics-for-visual-designers/)
*   [10 Ways To Make Your XHTML Site Accessible Using Web Standards](https://www.smashingmagazine.com/2009/06/10-ways-to-make-your-site-accessible-using-web-standards/)
*   [Best Practices In Modern Web Design: The Ultimate Round-Up](https://www.smashingmagazine.com/2010/03/best-practices-in-modern-web-design-the-ultimate-round-up/)

## 1\. HTML and JavaScript

Manipulating HTML with JavaScript is the most common method of adding interactivity to a website. But before you start using JavaScript, having a strong understanding of the CSS <a title="W3C CSS 2.1 Visual formatting model" href="https://www.w3.org/TR/CSS21/visuren.html">visual formatting model</a> and <a title="W3C CSS 2.1 Box model" href="https://www.w3.org/TR/CSS21/box.html">box model</a> is important. They are vital to making sense of how HTML elements can be manipulated visually. When you dynamically change the style of an HTML element, it will flow with and react to the rest of the document. Learning to anticipate and control what is affected can be difficult.

{{% feature-panel %}}

Using a JavaScript library such as <a title="Query: The Write Less, Do More, JavaScript Library" href="https://jquery.com/">jQuery</a> can take the pain out of cross-browser support. jQuery also provides common functionality that makes interacting with HTML a quicker process. It's necessary to learn the basics of JavaScript before looking at a library like jQuery, to ensure that you understand the fundamentals and therefore know <em>how</em> jQuery does something, not just <em>what</em> it does. The distinction here is key to being able to write your own JavaScript.</p>

### A Slideshow Example

The website for the <a title="Momento App" href="https://www.momentoapp.com/">Momento App</a> has a horizontal-scrolling slideshow that presents new content when the user clicks left and right.

<a title="Momento App" href="https://www.momentoapp.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="86390" title="Momento App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bacc688a-ee28-47e5-b2d4-5fd56416b07c/itws-momentoapp11.jpg" alt="" width="500" height="313" /></a><br>
<em>Momento App has its own jQuery plug-in for the slideshow effect.</em>

### How It Works

The five slides are <code>img</code> elements wrapped in <code>div</code>s and positioned sequentially inside their containers:

<pre><code class="language-markup tmp-xml">&lt;div id="tour_pages"&gt;
    &lt;div id="tour_page_capture" class="tour_page"&gt;
		&lt;img src="images/tour/capture.png" /&gt;
	&lt;/div&gt;

    &lt;div id="tour_page_import" class="tour_page loading"&gt;
    	&lt;img src="images/tour/import.png" /&gt;
    &lt;/div&gt;

    &lt;div id="tour_page_browse" class="tour_page loading"&gt;
    	&lt;img src="images/tour/browse.png" /&gt;
    &lt;/div&gt;

    &lt;div id="tour_page_read" class="tour_page loading"&gt;
    	&lt;img src="images/tour/read.png" /&gt;
    &lt;/div&gt;

    &lt;div id="tour_page_protect" class="tour_page loading"&gt;
    	&lt;img src="images/tour/protect.png" /&gt;
    &lt;/div&gt;

&lt;/div&gt;

&lt;a id="tour_nav_previous" href="#"&gt;Previous&lt;/a&gt;
&lt;a id="tour_nav_next" href="#"&gt;Next&lt;/a&gt;</code></pre>

The container <code>tour_pages</code> has a fixed height and width in the CSS. It also has the <code>overflow</code> property set to <code>hidden</code>.

<pre><code class="language-css">#tour_pages {
    position: absolute;
    left: 0px;
    top: 116px;
    height: 420px;
    width: 940px;
    overflow: hidden;
}</code></pre>

You can see in the image below how the five slides are positioned to move inside their containers. A container will clip everything outside of its boundaries because of <code>overflow: hidden</code>. This creates what we can call a <em>window</em> or <em>viewport effect</em>.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="86391" title="Momento App Elements Breakdown" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c37e804-c03b-491f-8635-69ed281cf54d/itws-momentoapp2.jpg" alt="" width="500" height="313" /><br>
<em>Showing the clipping frame and hidden elements.</em>

This set-up can all be done with CSS and HTML alone. To create the interaction, we need to use JavaScript to move the slides when “Next” or “Previous” are clicked. The JavaScript used by Momento is quite involved, so I'll leave it as an exercise for the reader to inspect, but I hope this example provides a good illustration of how HTML elements are controlled while remaining part of the document structure.</p>

### When to Use JavaScript

In the Momento example, we can see how JavaScript is useful for controlling access to content. The hide and reveal technique in all its forms is useful for keeping visible content clean and enhancing the user experience.

The website is intended to sell a product, and this slideshow effect imparts a sense of quality, something that is more exciting than the norm. Interactive content like this works best for promotional content.</p>

### When Not to Use JavaScript

Interactivity can be a lot more engaging than static content, but it's not always the most usable solution. Consider the following:

*   Will the user understand and expect the relevant action that occurs?
*   If content is hidden, will the user know how to access it?
*   Does the additional user input actually improve the overall experience?
*   Will the website be usable on all devices?

If you cannot justify the JavaScript against these questions, then you'd be wise to stay away. Be vigilant: ask yourself whether the extra eye-candy is really necessary.

<strong>Usable and accessible</strong> don't just mean that a device is technically supported by the website. The website should be as easy to use as possible for all audiences—from young to old—and in all environments.</p>

### Further Reading

*   [The CSS Box Model](https://css-tricks.com/the-css-box-model/) A friendly introduction to the box model by Chris Coyier.
*   [jQuery Tutorials](https://docs.jquery.com/Tutorials) An extensive list of jQuery tutorials.
*   [Real Animation Using JavaScript, CSS3 and HTML5 Video](https://24ways.org/2010/real-animation-using-javascript-css3-and-html5-video) An advanced look into animation by Dan Mall.

Interactivity and JavaScript are almost synonymous in Web design, but as we'll see in the next example, JavaScript is not always necessary.</p>

## 2\. CSS3 Transitions

The CSS <code>:hover</code> pseudo-class allows for a style change when the user hovers over an element. Typically used on the <code>&lt;a&gt;</code> element for links, the change can provide visual feedback for the user. While not exactly revolutionary on its own, <code>:hover</code> can be used to great effect.

Designer <a title="Christoph Zillgens" href="https://christophzillgens.com/en/">Christoph Zillgens</a> uses <strong>CSS3 transitions</strong> to enhance the hover effect. You can see the transition phases below:

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="86386" title="itws-transitions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55ae5076-a9b6-44d0-9b9c-0f8170e36dce/itws-transitions.png" alt="" width="500" height="220" /><br>
<em>Three phases of the hover transition: default, transition and then hover.</em>

### How It's Done

Inspecting the HTML doesn't offer many clues. At a glance, we can see a normal link. This is perfect for semantic markup, but how do we create the transition?

<pre><code class="language-markup tmp-xml">&lt;p class="category_link"&gt;
    &lt;a href="https://christophzillgens.com/en/category/posts/"&gt;
        &lt;span&gt;View all Posts&lt;/span&gt;
    &lt;/a&gt;
&lt;/p&gt;</code></pre>

The only unusual addition here is the extra <code>span</code> tag wrapping the text. The CSS reveals the secret. Let's take a look (some styles have been omitted below for readability):

<pre><code class="language-css">.category_link a {
    display:block;
    background:rgba(0,0,0,.05) url(img/big_icons.png) 10px 10px no-repeat;
}
.category_link a:hover {
    background-color:rgba(180,70,30,.7);
    -webkit-transition:background-color .4s ease;
}
.category_link a span {
    position:relative;
    top:150px;
    opacity:0;
    -webkit-transition:all .3s ease-in-out;
}
.category_link a:hover span {
    top:130px;
    opacity:1;
}</code></pre>

We can see in the HTML and CSS that both the <code>a</code> and <code>span</code> are converted to block-level elements to allow for positioning and sizing. They are styled in two states, <strong>default</strong> and <strong>hover</strong> (<em>A</em> and <em>C</em> in the image above).

By default, the <code>span</code> starts of with an opacity of 0 and at 150 pixels from the top. On hover, the <code>span</code> is fully visible and 130 pixels from the top. The anchor has a simple background color change between <em>A</em> and <em>C</em>.

At this stage, the hover effect jumps from default to the hover state instantly. This works fine for older browsers, but with <strong>CSS3 transitions</strong> we can create a silky-smooth animation between the two points.</p>

### Adding the Transition

We now have a start point and end point for our hover effect. To create the intermediate transition, we can use the <code>transition</code> property (<a title="CSS Transitions Module Level 3" href="https://www.w3.org/TR/css3-transitions/">defined here</a>) with a format like this:

<pre><code class="language-css">transition: [transition-property] [transition-duration] [transition-timing-function]</code></pre>

In the default <code>span</code> style, the transition property was added like so:

<pre><code class="language-css">-webkit-transition:all .3s ease-in-out;</code></pre>

This means that whenever the default style is applied, the <code>span</code> will transition between its current style and the default style. In this case, all CSS properties are affected, and the transition is triggered by the mouse hover. If we want to transition a single property, like the <code>background-color</code> of the anchor, we can do this, too:

<pre><code class="language-css">-webkit-transition:background-color .4s ease;</code></pre>

Creating hover transitions is as simple as specifying the default and hover states with CSS and then letting the <code>transition</code> property animate any changes between the two.</p>

### When CSS Transitions Work

Using the transition property with <code>:hover</code> is a very handy technique that bypasses JavaScript entirely. Removing this extra dependancy can save time and space.

That said, transitions are also triggered by dynamic HTML changes using JavaScript. If you're used to toggling classes with JavaScript to change styles, then why not see what difference a transition or two can have?

You'll notice that this example uses the <code>-webkit-</code> vendor-specific property for Safari and Chrome, but transitions are also supported in Opera using the <code>-o-</code> prefix and the new Firefox 4 beta with <code>-moz-</code>.

The good news for <strong>graceful degradation</strong> fans is that older browsers (i.e. Internet Explorer) ignore the transition and apply the style change immediately. This means you'll rarely find a situation in which using transitions degrades functionality.</p>

### Other Examples

Here are a few more websites whose use of CSS transitions is noteworthy:

*   When using hover, the affected elements don't always need to sit inside the same container. [Love Nonsense](https://lovenonsense.com/) makes use of the adjacent sibling selectors to trigger transitions.
*   Simurai demonstrates a combination of transitions and transforms to create a complex experimental toggle button using nothing but CSS and HTML.
*   The `:hover` is not the only trigger for transitions. [Neal Grosskopf's CSS-only lightbox](https://www.nealgrosskopf.com/tech/thread.php?pid=75 "A CSS Only Lightbox/Shadowbox Media Viewer Using CSS Transitions") demonstrates the use of the `:target` pseudo-class.</p>

### Further Reading

Here is a selection of in-depth articles that cover the nuances of CSS transitions:

*   “[A Comprehensive Guide to CSS 3 Transitions](https://www.onextrapixel.com/2010/11/17/a-comprehensive-guide-to-css-3-transitions/),” by Ashton Blue,
*   “[Understanding CSS3 Transitions](https://www.alistapart.com/articles/understanding-css3-transitions),” by Dan Cederholm,
*   “CSS Fundamentals: CSS 3 Transitions,” by Dave Sparks.</p>

## 3\. Animations With SVG

Hover effects work well for links but can be confusing when triggered unexpectedly on other elements. They're also less accessible on touchscreen devices. Adding interactivity when the user clicks is usually very useful because it provides feedback to the user, and sometimes it just feels more intuitive.

<a title="Get Satisfaction" href="https://getsatisfaction.com/">Get Satisfaction</a> uses a clever technique to showcase 12 different testimonials. In this example, the company makes use of <a title="Scalable Vector Graphics" href="https://www.alistapart.com/articles/using-svg-for-flexible-scalable-and-fun-backgrounds-part-i/">scalable vector graphics</a> (SVG) to aid with the animation.

<a title="Get Satisfaction" href="https://getsatisfaction.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="86388" title="itws-getsatisfactionwheel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/750b0be4-2fb0-465b-bb9a-a03891731fd0/getsatisfaction.jpg" alt="Screenshot" width="500" height="257" /></a><br>
<em>The “Wheel of Satisfaction” animates an SVG image.</em>

Part of the HTML for this wheel looks like this:

<pre><code class="language-markup tmp-xml">&lt;div id="wheel-logos"&gt;
    &lt;svg xmlns="https://www.w3.org/2000/svg" version="1.1" width="1003" height="315"&gt;
        &lt;image x="91" y="-505" width="820" height="820"
        preserveAspectRatio="none"         href="sites/all/themes/getsatisfaction/images/wheel_logos.png"
        transform="rotate(3600 501 -95)"&gt;&lt;/image&gt;
    &lt;/svg&gt;
&lt;/div&gt;</code></pre>

You can see above that the wheel image is contained within an <code>svg</code> element. SVG is an XML-based standard and can be written <strong>inline in HTML</strong>. SVG is particularly useful because images in SVG can have a <a title="SVG - Coordinate Systems, Transformations and Units" href="https://www.w3.org/TR/SVG/coords.html#TransformAttribute">transform attribute</a>, allowing for rotation, scaling and skewing (unlike normal HTML <code>img</code> tags).

To create and animate the wheel, Get Satisfaction used a library called Raphaël with <a title="jQuery JavaScript Library" href="https://jquery.com/">jQuery</a>:

<pre><code class="language-javascript">var R = Raphael("wheel-logos", 1003, 315);
var logos = R.image(src, 91, -505, 820, 820);
$("#wheel-spin-btn, #wheel-controls .spin").click(function(e) {
    if (status != "animating") {
        num = Math.floor(Math.random()*(items-1)+1),
        angle += (num+items)*rotate;
        logos.animate({rotation: angle}, 3000, "&lt;&gt;", reorderLinks(3000));
    }
    e.preventDefault();
});</code></pre>

In the JavaScript above, jQuery binds the <code>click</code> event to the spin button. When the button is clicked, Raphaël's <code>animate()</code> function is called to rotate the image. If you open the <a title="Get Firebug" href="https://getfirebug.com/">Firebug extension</a> in Firefox, you can see the SVG image's <code>transform</code> attribute update live as it spins:

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="85440" title="Get Satisfaction Firebug" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deaa1cfa-dbef-4b60-9482-797f434c12dd/code-transform.gif" alt="Get Satisfaction live code in Firebug" width="467" height="134" />

### True SVG Animation

As we've seen above, SVG can be manipulated with JavaScript just like HTML. But did you know that SVG has its own animation properties? It's in <a href="https://www.w3.org/TR/SVG/animate.html">the SVG specification</a>, but we rarely see it used. Here's an example element from the W3C draft:

<pre><code class="language-markup tmp-xml">&lt;rect&gt;
    &lt;animate attributeType="CSS" attributeName="opacity" from="1" to="0" dur="5s" repeatCount="indefinite" /&gt;
&lt;/rect&gt;</code></pre>

SVG can even contain <a title="ECMAScript - Wikipedia" href="https://en.wikipedia.org/wiki/ECMAScript">ECMAScript</a> (which is the standardized scripting language on which JavaScript is based) to add interactivity inside. For more information on this usage, I'd suggest starting with Peter Collingridge’s article “<a href="https://www.petercollingridge.co.uk/data-visualisation/mouseover-effects-svgs">Mouseover Effects in SVGs</a>.”

### When to Use SVG

Always consider the pros and cons of any technology. The most logical solution is not necessarily the easiest to implement. SVG provides an alternative graphics environment that may make animation a piece of cake in some situations. The scalable nature of SVG also provides obvious benefits over fixed-sized raster images.

The reason we rarely see SVG used is that Internet Explorer (below version 9) has no support for it. But not all is lost! The Raphaël library that Get Satisfaction uses automatically substitutes SVG for VML (vector markup language), which IE can understand.</p>

### Further Reading

Scalable vector graphics are a relatively untapped resource in the Web designer’s toolkit. Here are more articles to get your creativity flowing:

*   “[Mouseover Effects in SVGs](https://www.petercollingridge.co.uk/data-visualisation/mouseover-effects-svgs)” Five different methods of achieving a mouseover effect in an SVG, by Peter Collingridge,
*   “Advanced SVG Animation Techniques,” by Antoine Quint,
*   “[Manipulating SVG Documents Using ECMAScript (Javascript) and the DOM](https://www.carto.net/svg/manipulating_svg_with_dom_ecmascript/),” by Juliana Williams and Andreas Neumann.</p>

## 4\. Animations With Canvas

The <strong>CSS transitions</strong> that we examined above can alter any number of properties to create a lot of visual effects, but ultimately they're still limited to CSS styles and fixed-length transitions. Is there a way to create more advanced animations?

Google's <a title="Google Chrome OS Features" href="https://www.google.com/chromeos/features.html">Chrome OS features page</a> demonstrates a hover effect that has continuous animation:

<a title="Google Chrome OS Features" href="https://www.google.com/chromeos/features.html"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="85441" title="Google Chrome OS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eddafc08-c01f-43e0-ae67-142f725cf7a8/googlechromeos.png" alt="Google Chrome OS features hover effect" width="450" height="300" /></a><br>
<em>Chrome features: each icon animates on hover.</em>

To find out how this works, let's start by looking at the HTML again:

<pre><code class="language-markup tmp-xml">&lt;a href="features-speed.html"&gt;
    &lt;canvas class="c1" height="150" id="canvas-uuid-1" onmouseout="javascript:hideBadge(0)" onmouseover="javascript:showBadge(0);" width="150" style="cursor: default; "&gt;
        &lt;img alt="" src="static/images/features-speedicon.png"&gt;
    &lt;/canvas&gt;
 /a&gt;</code></pre>

Here we have an <code>a</code> link that contains a <code>canvas</code> element (which itself contains an image). For browsers that do not support <code>canvas</code>, the image serves as a fallback—who said supporting IE6 was hard!

We can also see that the <code>onmouseover</code> and <code>onmouseout</code> attributes are set to trigger JavaScript functions named <code>hideBadge()</code> and <code>showBadge()</code>. This creates a behavior similar to that of the CSS <code>:hover</code> pseudo-class we saw in our second example.

Google's JavaScript for controlling this is fairly extensive, but it's basically drawing a series of SVG images onto the <code>canvas</code> to create the animation.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="85442" title="Google Chrome OS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f28da48b-0e1f-4b26-88cd-c51f8f81c82c/goolechromeosassets.png" alt="Google Chrome OS feature assets" width="450" height="150" /><br>
<em>The individual SVG assets for the <code>canvas</code> animation.</em>

If you want to learn more about animating with <code>canvas</code>, then take a look at the <a title="CAKE - Canvas Animation Kit Experiment" href="https://code.google.com/p/cakejs/">Canvas Animation Kit Experiment</a> (CAKE), the JavaScript library that Google uses to animate its hover effects.</p>

### How Useful Is Canvas?

<code>Canvas</code> is a very flexible HTML element for creating scriptable graphics and is by far the most powerful solution for interactivity and animation. By assigning similar effects to actions like click and hover with JavaScript, we can give the user a visual treat, unrestricted by the scope of HTML and CSS.

<strong>The downside?</strong> Google's example isn't very accessible, and the fact that the content in the <code>canvas</code> element is generated dynamically is a real issue. Search engines will have a hard time seeing your <code>canvas</code> content, and more importantly, assistive technology such as screen readers will struggle as well.

If you want to display content with the <code>canvas</code> element, then providing the same content in an alternate and accessible format would be considerate. <code>Canvas</code> is probably best used to display more visual data such as graphs, charts and diagrams. These are situations in which the content can be isolated and presented in a way that's easier to understand.</p>

### Further Reading

*   [Canvas, Accessibility and SVG](https://www.brucelawson.co.uk/2009/canvas-accessibility-and-svg/) Bruce Lawson discusses the accessibility of `canvas`.
*   [HTML5 Canvas Element Guide](https://sixrevisions.com/html/canvas-element/) A beginner’s guide to the `canvas` element by Louis Lazaris.
*   HTML5 Canvas Interactivity A guide to keyboard and mouse interactivity in `canvas` by Johnny Simpson.</p>

## A Note On Adobe Flash

Saving the best for last (well, you never would have gotten this far if I'd put this first), we have the powerhouse that is Adobe Flash. Flash is not a Web standard, but it is used extensively across the Web.

Adobe Flash provides a sandbox to create interactive content using ActionScript. <strong>ActionScript 3</strong> shares the same ECMAScript roots as JavaScript, so learning one after the other is a relatively easy move. The problem is that Flash is a proprietary plug-in and not an open Web standard. Admittedly, it can be a lot more powerful and, in some cases (like with video), may be the only appropriate solution at present.

However, always weigh up arguments for and against Flash. You'd be amazed at what's possible with modern standards. That said, despite the negative opinion of many Web designers and developers, Flash is still a commercially viable option. But this is becoming more and more debatable as standards progress.</p>

## To Summarize

We've seen some great examples of what can be achieved with Web standards today.

Here are a few points to remember:

*   HTML can be manipulated directly with JavaScript.
*   The CSS `:hover` pseudo-class and `transition` property can be combined to create a wide variety of hover effects.
*   Images can be contained within inline SVG, providing a simple way to transform them beyond the limitations of HTML and CSS.
*   `canvas` and JavaScript provide the most powerful (but a less accessible) solution for interactivity and animation.

These techniques can bring a website to life and enhance the user experience. But they also have the potential to make a website look like a hangover from the DHTML era. There's no accounting for taste, so use it with care. Always focus on the accessibility of content and on user experience over eye-candy.</p>

### One Last Thought

When are JavaScript libraries required? We've already seen examples of <code>canvas</code> and <code>SVG</code> in which they’re used. JavaScript libraries aim to provide common functionality in order to drastically reduce implementation time. But using them for a single function can create a hefty load. <a title="Get Satisfaction" href="https://getsatisfaction.com/">Get Satisfaction</a> uses the Raphaël library only once to manipulate the SVG image rotation. Could this have been done without Raphaël?

The answer is <a title="Stack Overflow - Animate rotating svg element on webpage" href="https://stackoverflow.com/questions/2995643/animate-rotating-svg-element-on-webpage">yes</a>… but it's not that simple. Browsers such as Internet Explorer don't support SVG, and Raphaël uses <a href="https://en.wikipedia.org/wiki/Vector_Markup_Language">VML</a> instead. Careful research is required before rolling your own solution. It may be more difficult than you initially suspect.

There are libraries such as <a href="https://www.modernizr.com/">Modernizr</a> in which individual functions <em>can</em> be isolated as required very easily, so that is always worth considering. With the new Modernizr beta preview, the situation has been recognized, and Modernizr now provides a completely custom library for your particular requirements.

{{< signature "al" >}}

