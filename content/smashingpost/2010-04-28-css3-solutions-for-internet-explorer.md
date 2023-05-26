---
title: CSS3 Solutions for Internet Explorer
slug: css3-solutions-for-internet-explorer
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/336175cd-85ca-4130-9330-8c208a89c2c5/ie6.jpg
date: 2010-04-28T11:09:53.000Z
author: louis-lazaris
summary: >-
  CSS3 is probably the hottest trend in web design right now, allowing developers the opportunity to implement a number of solutions into their projects with some very straightforward CSS while avoiding having to resort to nonsemantic markup, extra images, and complex JavaScript. Unfortunately, it's not a surprise that Internet Explorer, even in its most recent version, still <a href="https://msdn.microsoft.com/en-us/library/cc351024(VS.85).aspx">does not support</a> the majority of the properties and features introduced in CSS3.
description: >-
  CSS3 is probably the hottest trend in web design right now, allowing developers the opportunity to implement a number of solutions into their projects with some very straightforward CSS while avoiding having to resort to nonsemantic markup, extra images, and complex JavaScript. Unfortunately, it's not a surprise that Internet Explorer, even in its most recent version, still <a href="https://msdn.microsoft.com/en-us/library/cc351024(VS.85).aspx">does not support</a> the majority of the properties and features introduced in CSS3.
categories:
  - Coding
  - CSS
  - Internet Explorer
  - CSS3
---
<p>Experienced developers understand that CSS3 can be added to new projects with progressive enhancement in mind. This ensures that content is accessible while non-supportive browsers fall back to a less-enhanced experience for the user.</p>

<p>But developers could face <strong>a situation where a client insists that the enhancements work cross-browser</strong>, demanding support even for IE6. In that case, I've collected together a number of options that developers can consider for those circumstances where support for a CSS3 feature is required for all versions of Internet Explorer (IE6, IE7, &amp; IE8 — all of which are still currently in significant use).</p>

## Opacity / Transparency

<p>I think all developers are baffled at why Internet Explorer still fails to support this very popular (albeit troublesome) property. It's been around so long, that we often forget that it's actually a CSS3 property. Although IE doesn't offer support for the <code>opacity</code> property, it does offer similar transparency settings via the proprietary <code>filter</code> property:</p>

### The Syntax

<pre><code class="language-css">#myElement {
	opacity: .4; /* other browsers  and IE9+ */
	filter: alpha(opacity=40); /* IE6+ */
	filter: progid:DXImageTransform.Microsoft.Alpha(opacity=40); /* IE6+ */
	-ms-filter: "progid:DXImageTransform.Microsoft.Alpha(opacity=40)"; /* this works in IE8 only */
}</code></pre>

<p>You really only need the second line, which works in all versions of Internet Explorer. But if for some reason you needed the opacity setting to apply only to IE8, and not to IE6/7, then you can use the last line, which the older versions don't recognize. The third line is just another way to do basically the same thing, but with a more convoluted syntax.</p>

<p>The opacity value at the end of each IE line works basically the same way that the <code>opacity</code> property does, taking a number from 0 to 100 (the <code>opacity</code> property takes a two-digit number from 0 to 1, so "44" for IE would be "0.44" for the others). Also, as many have experienced when using opacity (even when using the standard method), the opacity settings will be inherited by all child elements, for which there is no easy workaround.</p>

You may also be interested in the following related posts:

*   [CSS Differences in Internet Explorer 6, 7 and 8](https://www.smashingmagazine.com/2009/10/css-differences-in-internet-explorer-6-7-and-8/)
*   [The Principles Of Cross-Browser CSS Coding](https://www.smashingmagazine.com/2010/06/the-principles-of-cross-browser-css-coding/)
*   [Using CSS3: Older Browsers And Common Considerations](https://www.smashingmagazine.com/2011/05/using-css3-older-browsers-and-common-considerations/)
*   [How To Support Internet Explorer and Still Be Cutting Edge](https://www.smashingmagazine.com/2009/12/how-to-support-internet-explorer-and-still-be-cutting-edge/)

{{% feature-panel %}}

### The Demonstration

<div>

This element has a solid blue background color (#0000FF), but is 60% transparent, making it appear light blue in all browsers

</div><br>
<div style="width: 250px;height: 90px;margin: 0 0 20px 0;background: #00f;text-align: center;color: white;padding: 20px 15px 0 15px;font-family: Arial, Helvetica, sans-serif">

This is the same element without the opacity settings.

</div>

### The Drawbacks

*   The filter property is a Microsoft-only property, so your CSS won't validate
*   As is the case for the `opacity` property, the IE filter causes all child elements to inherit the opacity
*   There could be performance issues with the IE filters

## Rounded Corners (border-radius)

<p>The <code>border-radius</code> property (more commonly referred to as CSS3 rounded corners) is another popular CSS3 enhancement. This property has allowed developers to avoid the headache of bloated JavaScript or extra positioned elements to achieve the same effect. But once again, Microsoft doesn't want to cooperate, so IE doesn't have any support for this property.</p>

<p>Fortunately, at least one person has come up with a very usable workaround that can be used in an IE-only stylesheet. <a href="https://www.htmlremix.com/about">Remiz Rahnas</a> of <a href="https://www.htmlremix.com/">HTML Remix</a> has created an <a href="https://en.wikipedia.org/wiki/HTML_Components">HTC file</a> called <a href="https://www.htmlremix.com/css/curved-corner-border-radius-cross-browser">CSS Curved Corner</a> that can be downloaded off <a href="https://code.google.com/p/curved-corner/">Google Code</a>.</p>

<p>The great thing about this piece of code is that it doesn't require any extra maintenance if you adjust the amount of radius on your rounded corners. You just link to the file in your CSS, and the script will automatically parse your CSS to find the correct radius value from the standard <code>border-radius</code> property.</p>

### The Syntax

Here's what your code might look like:

<pre><code class="language-css">.box-radius {
	border-radius: 15px;
	behavior: url(border-radius.htc);
}</code></pre>

<p>The way it works is pretty straightforward, as shown above. Ideally, however, you would apply the <code>behavior</code> property in an IE-only stylesheet, using the same selector in your CSS, so the code knows where to get the radius value from.</p>

### The Demonstration

<p>Because this technique requires use of an external HTC file, you can view the demo <a href="https://www.impressivewebs.com/css3-rounded-corners-in-internet-explorer/">at this location</a>.</p>

### The Drawbacks

*   The HTC file is 142 lines (minifying or GZipping would help, but it's still extra bloat)
*   The `behavior` property will make your CSS invalid
*   Your server needs to be able to load HTC files for this technique to work
*   IE8 seems to have some trouble in some circumstances when the HTC file forces the curved element to have a negative z-index value

{{% ad-panel-leaderboard %}}

## Box Shadow

<p>The <code>box-shadow</code> property is another useful CSS3 feature that will even add a curved box shadow naturally to an element that uses the <code>border-radius</code> property. IE doesn't support <code>box-shadow</code>, but a filter is available that offers a close replication.</p>

<p>It should be noted that the <code>box-shadow</code> property has been <a href="https://www.w3.org/TR/css3-background/#the-box-shadow">removed from the CSS3 Backgrounds and Borders Module</a>, so its future in CSS3 seems to be a little uncertain right now.</p>

### The Syntax

<pre><code class="language-css">.box-shadow {
	-moz-box-shadow: 2px 2px 3px #969696; /* for Firefox 3.5+ */
	-webkit-box-shadow: 2px 2px 3px #969696; /* for Safari and Chrome */
	filter: progid:DXImageTransform.Microsoft.Shadow(color='#969696', Direction=145, Strength=3);
}</code></pre>

As shown above, in addition to the proprietary WebKit and Mozilla properties, you can add a shadow filter that works in all versions of Internet Explorer.

### The Demonstration

<div>

This element has a drop shadow that works in Internet Explorer.

</div>

### The Drawbacks

*   The settings for the IE shadow filter do not match those of the other proprietary properties, so in order to make it look the same, you have to fiddle with the values until you get it right, which can cause maintenance headaches
*   The filter property doesn't validate, but neither do the WebKit and Mozilla properties, so this is a drawback in all browsers

## Text Shadow

<p>Adding drop shadows to text elements has been practiced in both print and web design for years. On the web, this is normally done with images and occasionally with text duplication combined with positioning. CSS3 allows developers to easily add shadows to text using a simple and flexible <code>text-shadow</code> property.</p>

<p>Unfortunately, there doesn't seem to be an easy way to add a text shadow in Internet Explorer — even with the use of proprietary filters. To deal with this problem, a Dutch front-end developer named <a href="https://kilianvalkhof.com/">Kilian Valkhof</a> has written <a href="https://kilianvalkhof.com/2008/javascript/text-shadow-in-ie-with-jquery/">a jQuery plugin</a> that implements text shadows in Internet Explorer.</p>

### The Syntax

<p>First, in your CSS, you would set the <code>text-shadow</code> property:</p>

<pre><code class="language-css">.text-shadow {
	text-shadow: #aaa 1px 1px 1px;
}</code></pre>

The values specify the shadow color, position on the horizontal axis, position on the vertical axis, and the amount of blur.

After including the jQuery library and the plugin in your document, you can call the plugin with jQuery:

<pre><code class="language-javascript">// include jQuery library in your page
// include link to plugin in your page

$(document).ready(function(){
	$(".text-shadow").textShadow();
});</code></pre>

The plugin also allows the use of parameters to override the CSS. See the plugin author's original web page for more details on the parameters.

<p>Although there is a cross-browser <a href="https://plugins.jquery.com/project/DropShadow">jQuery plugin that applies drop shadows</a>, the one I'm demonstrating above actually utilizes the CSS3 value that's already set in your CSS, so it has the advantage of working along with the standard CSS setting for text shadows, whereas the other plugin needs to be set independently.</p>

### The Demonstration

<p>Because this technique requires use of the jQuery library and an external plugin file, you can view the demo <a href="https://www.impressivewebs.com/css3-text-shadow-in-internet-explorer/">at this location</a>.</p>

### The Drawbacks

There are some significant drawbacks to this method that make it very unlikely to ever be practical. You're probably better off creating an image to replace the text for IE instead.

*   In order to make the shadow look almost the same in IE, you need to use different settings in an IE-only stylesheet, adding to development and maintenance time
*   Requires that you add the jQuery library, in addition to a 61-line plugin file (GZipping or minifying would help)
*   The IE version of the shadow never looks exactly the same as the other browsers
*   When using the overriding parameters, the plugin seems to be rendered somewhat useless, displaying a big ugly shadow that won't change with new values
*   Unlike the CSS3 version, the plugin doesn't support multiple shadows
*   For some reason, in order to get it to work in IE8, you need to give the element a `z-index` value

{{% ad-panel-leaderboard %}}

## Gradients

Another practical and time-saving technique introduced in CSS3 is the ability to create custom gradients as backgrounds. Although Internet Explorer doesn't support gradients of the CSS3 variety, it's pretty easy to implement them for the IE family using proprietary syntax.

### The Syntax

To declare a gradient that looks the same in all browsers, including all versions of Internet Explorer, use the CSS shown below (the last two lines are for IE):

<pre><code class="language-css">#gradient {
	background-image: -moz-linear-gradient(top, #81a8cb, #4477a1); /* Firefox 3.6 */
	background-image: -webkit-gradient(linear,left bottom,left top,color-stop(0, #4477a1),color-stop(1, #81a8cb)); /* Safari &amp; Chrome */
	filter:  progid:DXImageTransform.Microsoft.gradient(GradientType=0,startColorstr='#81a8cb', endColorstr='#4477a1'); /* IE6 &amp; IE7 */
	-ms-filter: "progid:DXImageTransform.Microsoft.gradient(GradientType=0,startColorstr='#81a8cb', endColorstr='#4477a1')"; /* IE8 */
}</code></pre>

<p>For the IE filters, the <code>GradientType</code> can be set to "1" (horizontal) or "0" (vertical).</p>

### The Demonstration

<div>

This element has a linear gradient that works in Internet Explorer.

</div>

### The Drawbacks

Some of the usual drawbacks apply to gradients created with the IE-only filter, along with some other problems.

*   Your CSS won't validate, although that's also true for the WebKit and Mozilla values
*   Different code is needed for IE8, adding to maintenance time
*   The WebKit and Mozilla gradients allow for "stops" to be declared; this doesn't seem to be possible with the IE gradient, limiting its flexibility
*   IE's filter doesn't seem to have a way to declare "radial" gradients, which WebKit and Mozilla support
*   For a gradient to be visible in IE, the element with the gradient must [have layout](https://reference.sitepoint.com/css/haslayout)

## Transparent Background Colors (RGBA)

CSS3 offers another method to implement transparency, doing so through an alpha channel that's specified on a background color. Internet Explorer offers no support for this, but this can be worked around.

### The Syntax

For the CSS3-compliant browsers, here's the syntax to set an alpha channel on the background of an element:

<pre><code class="language-css">#rgba p {
	background: rgba(98, 135, 167, .4);
}</code></pre>

With the above CSS, the background color will be set to the RGB values shown, plus the optional "alpha" value of ".4". To mimic this in Internet Explorer, you can use the proprietary filter property to create a gradient with the same start and end color, along with an alpha transparency value. This would be included in an IE-only stylesheet, which would override the previous setting.

<pre><code class="language-css">#rgba p {
	filter: progid:DXImageTransform.Microsoft.gradient(GradientType=0,startColorstr='#886287a7', endColorstr='#886287a7');
}</code></pre>

The "gradient" will look exactly the same in IE as in other browsers, duplicating the RGBA transparency effect.

### The Demonstration

This first example below will work in browsers that support RGBA colors. The second example will only work in Internet Explorer.
<div style="width: 250px;height: 90px;background: lightblue;margin: 0 0 20px 0;text-align: center;color: #444;padding: 20px 15px 0 15px;font-family: Arial, Helvetica, sans-serif"><br>
<p>This paragraph has a background color with a 40% opacity setting declared using RGBA (doesn't work in IE).</p>

</div>
<div style="width: 250px;height: 90px;background: lightblue;margin: 0 0 20px 0;text-align: center;color: #444;padding: 20px 15px 0 15px;font-family: Arial, Helvetica, sans-serif">
<p>This paragraph has an IE-only filter applied to mimic RGBA transparency (only works in IE).</p>

</div>

### The Drawbacks

*   The `filter` property is not valid CSS
*   Requires an extra line of CSS in an IE-only stylesheet
*   The element needs to have layout

<p>strong>Note</strong>: Initially, I had used a PNG image method to achieve this effect, but apparently it was working only partially in IE7 and IE8, and required a PNG-hack for IE6, so I tried the method given by <a href="#comment-456362">Liam</a> and <a href="#comment-456590">Matias</a> in the comments and this seems to work better. The PNG method is another option, but seems to be more troublesome, and has more drawbacks.</p>

## Multiple Backgrounds

This is another CSS3 technique that, when widely supported, could prove to be a very practical addition to CSS development. Currently, IE and Opera are the only browsers that don't support this feature. But interestingly, IE as far back as version 5.5 has allowed the ability to implement multiple backgrounds on the same element using a filter.

### The Syntax

<p>You might recall trying to hack a PNG in IE6 and noticing the image you were trying to hack appearing twice, which you had to remove by adding <code>background: none</code>, then applying the filter. Well, using the same principle, IE allows two background images to be declared on the same element.</p>

To use multiple backgrounds in Firefox, Safari, and Chrome, here's the CSS:

<pre><code class="language-css">#multi-bg {
	background: url(images/bg-image-1.gif) center center no-repeat, url(images/bg-image-2.gif) top left repeat;
}</code></pre>

To apply two backgrounds to the same element in IE, use the following in an IE-only stylesheet:

<pre><code class="language-css">#multi-bg {
	background: transparent url(images/bg-image-1.gif) top left repeat;
	filter: progid:DXImageTransform.Microsoft.AlphaImageLoader (src='images/bg-image-2.gif', sizingMethod='crop'); /* IE6-8 */
	-ms-filter: "progid:DXImageTransform.Microsoft.AlphaImageLoader(src='images/bg-image-2.gif', sizingMethod='crop')"; /* IE8 only */
}</code></pre>

### The Demonstration

The box below shows multiple backgrounds in Chrome, Firefox, and Safari (you won't see anything in IE):

<div>
The next box shows multiple backgrounds in Internet Explorer 6-8 (you'll only see a single background in other browsers):
</div>

### The Drawbacks

*   Your CSS will be invalid
*   The second background image applied using the `filter` property will always be in the top left, and cannot repeat, so this method is extremely inflexible and can probably only be used in a limited number of circumstances
*   In order to get the element to center (as in other browsers), you have to create an image with the exact amount of whitespace around it, to mimic the centering, as I've done in the demonstration above
*   The `AlphaImageLoader` filter causes performance issues, [as outlined here](https://developer.yahoo.com/performance/rules.html#no_filters)

## Element Rotation (CSS Tranformations)

<p>CSS3 has introduced a number of transformation and animation capabilities, which some have suggested are <a href="https://snook.ca/archives/javascript/css_animations_in_safari/">out of place</a> in CSS. Nonetheless, there is a way to mimic element rotation in Internet Explorer, albeit in a limited fashion.</p>

### The Syntax

To rotate an element 180 degrees (that is, to flip it vertically), here is the CSS3 syntax:

<pre><code class="language-css">#rotate {
	-webkit-transform: rotate(180deg);
	-moz-transform: rotate(180deg);
}</code></pre>

To create the exact same rotation in Internet Explorer, you use a proprietary filter:

<pre><code class="language-css">#rotate {
	filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
}</code></pre>

The value for the rotation can be either 1, 2, 3, or 4. Those numbers represent 90, 180, 270, or 360 degrees of rotation respectively.</p>

### The Demonstration

<p>The element below should appear upside down in Internet Explorer, having a rotation of 180 degrees set via the <code>filter</code> property. To demonstrate this more emphatically, I've applied a 3px solid gray "bottom" border, which should appear at the top of the element.</p>

<div>

This element is rotated 180 degrees in Internet Explorer.

</div>

### The Drawbacks

*   Your CSS won't validate, although that's also true for the WebKit and Mozilla code
*   While the Mozilla and WebKit code allows for rotation changes to increment by a single degree, the IE filter only permits 4 stages of rotation, minimizing its flexibility

<p><strong>Update:</strong> <a href="#comment-457537">As pointed out in the comments</a>, IE does allow the ability to rotate objects with the same flexibility as the CSS3 methods. To explain the method here is too complex, but the <a href="https://css3please.com">CSS3, please</a> project by Paul Irish has implemented this method into its code generator, so you can use that to create the IE-compatible code for CSS3 rotations.</p>

## Conclusion

Developers might hate me for compiling this list, seeing as any client could search for "CSS3 in Internet Explorer" and stumble across this page. So be careful what you tell your clients; although IE does not support these things natively, that doesn't mean they're impossible to implement.

And remember that anytime you need to override the initial CSS settings for IE, or if you have to use JavaScript, jQuery, or an HTC file, make sure the calls to the external resources are made using IE conditional comments. This will ensure the other browsers aren't making unnecessary HTTP requests.

<p>In many cases, the best solution for dealing with Internet Explorer is to let it display a less-enhanced experience. I hope, however, the above solutions provide some options for working with CSS3 <strong>when a client wants a more accurate cross-browser experience</strong>.</p>