---
title: 'The Z-Index CSS Property: A Comprehensive Look'
slug: the-z-index-css-property-a-comprehensive-look
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/765eef41-7506-4324-95c4-064b8cd35a0f/z-index.png
date: 2009-09-15T09:06:22.000Z
author: louis-lazaris
summary: >-
  Stacking contexts in CSS are a complex topic. This article aims to explain everything you need to know about <code>z-index</code> so that you can use this special type of property confidently and effectively.
description: >-
  Stacking contexts in CSS are a complex topic. This article aims to explain everything you need to know about <code>z-index</code> so that you can use this special type of property confidently and effectively.
categories:
  - Coding
  - Layouts
  - CSS
  - Essentials
---
Most CSS properties are quite simple to deal with. Often, applying a CSS property to an element in your markup will have instant results — as soon as you refresh the page, the value set for the property takes effect, and you see the result immediately. Other CSS properties, however, are a little more complex and will only work under a given set of circumstances. 

The <code>z-index</code> property belongs to the latter group. It<code></code> has undoubtedly caused as much confusion and frustration as any other CSS property. Ironically, however, when <code>z-index</code> is fully understood, it is a very easy property to use, and offers <strong>an effective method for overcoming many layout challenges.</strong>

In this article, we’ll explain exactly what <code>z-index</code> is, how it has been misunderstood, and we’ll discuss some practical uses for it. We’ll also describe some of the browser differences that can occur, particularly in previous versions of Internet Explorer and Firefox. This comprehensive look at <code>z-index</code> should provide developers with an excellent foundation to be able to use this property confidently and effectively.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sassy Z-Index Management For Complex Layouts](https://www.smashingmagazine.com/2014/06/sassy-z-index-management-for-complex-layouts/)
*   [Mastering CSS Principles: A Comprehensive Guide](https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/)
*   [The Definitive Guide to Using Negative Margins](https://www.smashingmagazine.com/2009/07/the-definitive-guide-to-using-negative-margins/)
*   [Stronger, Better, Faster Design with CSS3](https://www.smashingmagazine.com/2009/12/stronger-better-faster-design-with-css3/)

{{% feature-panel %}}

## What is z-index?

The <code>z-index</code> property determines the stack level of an HTML element. The "stack level" refers to the element’s position on the <em>Z axis</em> (as opposed to the <em>X axis</em> or <em>Y</em> axis). A higher value means the element will be closer to the top of the stacking order. This stacking order runs perpendicular to the display, or viewport.</p>

### 3-dimensional representation of the _Z_ axis:

<img loading="lazy" decoding="async" title="3-D Representation of the Z Axis" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da398c63-75f5-4fe8-a8bf-4e8e573a8faf/graphical-z-index.gif" alt="Z-Index 3-D Representation of the Z Axis" width="500" height="443" />

In order to clearly demonstrate how <code>z-index</code> works, the image above exaggerates the display of stacked elements in relation to the viewport.</p>

## The Natural Stacking Order

In an HTML page, the natural stacking order (i.e. the order of elements on the <em>Z</em> axis) is determined by a number of factors. Below is a list showing the order that items fit into a stacking context, starting with the bottom of the stack. This list assumes none of the items has <code>z-index</code> applied:

*   Background and borders of the element that establish stacking context
*   Elements with negative stacking contexts, in order of appearance
*   Non-positioned, non-floated, block-level elements, in order of appearance
*   Non-positioned, floated elements, in order of appearance
*   Inline elements, in order of appearance
*   Positioned elements, in order of appearance

The <code>z-index</code> property, when applied correctly, can change this natural stacking order.

Of course, the stacking order of elements is not evident unless elements are positioned to overlap one another. Thus, to see the natural stacking order, negative margins can be used as shown below:
<div style="width: 200px; height: 200px; border: solid 1px #ccc; background: #ddd; margin-top: 20px;"><br>
<p style="padding-left: 30px; padding-top: 60px;">Grey Box</p>

</div>
<div style="width: 200px; height: 200px; border: solid 1px #4a7497; background: #8daac3; margin-top: -50px; margin-left: 50px;">
<p style="padding-left: 30px; padding-top: 60px;">Blue Box</p>

</div>
<div style="width: 200px; height: 200px; border: solid 1px #8b6125; background: #ba945d; margin-top: -50px; margin-left: 100px; margin-bottom: 20px;">
<p style="padding-left: 30px; padding-top: 60px;">Gold Box</p>

</div>

<p>The boxes above are given different background and border colors, and the last two are indented and given negative top margins so you can see the natural stacking order. The grey box appears first in the markup, the blue box second, and the gold box third. The applied negative margins clearly demonstrate this fact. <strong>These elements do not have <code>z-index</code> values set</strong>; their stacking order is the natural, or default, order. The overlaps that occur are due to the negative margins.</p>

## Why Does it Cause Confusion?

Although <code>z-index</code> is not a difficult property to understand, due to false assumptions it can cause confusion for beginning developers. This confusion occurs because <strong><code>z-index</code> will only work on an element whose <code>position</code> property has been explicitly set</strong> to <code>absolute</code>, <code>fixed</code>, or <code>relative</code>.

To demonstrate that <code>z-index</code> only works on positioned elements, here are the same three boxes with <code>z-index</code> values applied to attempt to reverse their stacking order:
<div style="width: 200px; height: 200px; border: solid 1px #ccc; background: #ddd; margin-top: 20px;"><br>
<p style="padding-left: 30px; padding-top: 60px;">Grey Box</p>

</div>
<div style="width: 200px; height: 200px; border: solid 1px #4a7497; background: #8daac3; margin-top: -50px; margin-left: 50px;">
<p style="padding-left: 30px; padding-top: 60px;">Blue Box</p>

</div>
<div style="width: 200px; height: 200px; border: solid 1px #8b6125; background: #ba945d; margin-top: -50px; margin-left: 100px; margin-bottom: 20px;">
<p style="padding-left: 30px; padding-top: 60px;">Gold Box</p>
</div>

<p>The grey box has a <code>z-index</code> value of "9999"; the blue box has a <code>z-index</code> value of "500"; and the gold box has a <code>z-index</code> value of "1". Logically, you would assume that the stacking order of these boxes should now be reversed. But that is not the case, because none of these elements has the <code>position</code> property set.</p>

Here are the same boxes with <code>position: relative</code> added to each, and their <code>z-index</code> values maintained:

<div style="width: 200px; height: 200px; border: solid 1px #ccc; background: #ddd; margin-top: -50px; margin-left: 50px; z-index: 2;"><br>
<p style="padding-left: 30px; padding-top: 60px;">Grey Box</p>

</div>
<div style="width: 200px; height: 200px; border: solid 1px #4a7497; background: #8daac3; margin-top: -50px; margin-left: 50px; z-index: 2;">
<p style="padding-left: 30px; padding-top: 60px;">Blue Box</p>

</div>
<div style="width: 200px; height: 200px; border: solid 1px #8b6125; background: #ba945d; margin-top: -50px; margin-left: 100px; margin-bottom: 20px;">
<p style="padding-left: 30px; padding-top: 60px;">Gold Box</p>

</div>

<p>Now the result is as expected: The stacking order of the elements is reversed; the grey box overlaps the blue box, and the blue box overlaps the gold.</p>

## Syntax

The <code>z-index</code> property can affect the stack order of both block-level and inline elements, and is declared by a positive or negative integer value, or a value of <code>auto</code>. A value of <code>auto</code> gives the element the same stack order as its parent.

Here is the CSS code for the third example above, where the <code>z-index</code> property is applied correctly:

<pre><code class="language-css">#grey_box {
  width: 200px;
  height: 200px;
  border: solid 1px #ccc;
  background: #ddd;
  position: relative;
  z-index: 9999;
}

#blue_box {
  width: 200px;
  height: 200px;
  border: solid 1px #4a7497;
  background: #8daac3;
  position: relative;
  z-index: 500;
}

#gold_box {
  width: 200px;
  height: 200px;
  border: solid 1px #8b6125;
  background: #ba945d;
  position: relative;
  z-index: 1;
}</code></pre>

Again, it cannot be stressed enough, especially for beginning CSS developers, that the <code>z-index</code> property will not work unless it is applied to a positioned element.

## JavaScript Usage

If you want to affect the <code>z-index</code> value of an element dynamically via JavaScript, the syntax is similar to how most other CSS properties are accessed, using "camel casing" to replace hyphenated CSS properties, as in the code shown below:

<pre><code class="language-js">var myElement = document.getElementById("gold_box");
myElement.style.position = "relative";
myElement.style.zIndex = "9999";
</code></pre>

In the above code, the CSS syntax "z-index" becomes "zIndex". Similarly, "background-color" becomes "backgroundColor", "font-weight" becomes "fontWeight", and so on.

Also, the position property is changed using the above code to again emphasize that <code>z-index</code> only works on elements that are positioned.</p>

{{% ad-panel-leaderboard %}}

## Improper Implementations in IE and Firefox

Under certain circumstances, there are some small inconsistencies in Internet Explorer versions 6 and 7 and Firefox version 2 with regards to the implementation of the <code>z-index</code> property.</p>

### &lt;select&gt; elements in IE6

In Internet Explorer 6, the <code>&lt;select&gt;</code> element is a windowed control, and so will always appear at the top of the stacking order regardless of natural stack order, position values, or <code>z-index</code>. This problem is illustrated in the screen capture below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa03faf6-27c2-4029-9de4-60a7cdd2e43f/z-index-ie6.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa03faf6-27c2-4029-9de4-60a7cdd2e43f/z-index-ie6.gif" width="344" height="233" alt="" /></a></figure>

The <code>&lt;select&gt;</code> element appears first in the natural stack order and is given a <code>z-index</code> value of "1" along with a position value of "relative". The gold box appears second in the stack order, and is given a <code>z-index</code> value of "9999". Because of natural stack order and <code>z-index</code> values, the gold box should appear on top, which it does in all currently used browsers except IE6:
<div style="padding-left: 25px; padding-top: 25px;">

-- Choose Year --
2009
2010
2011

</div>
<div style="width: 200px; height: 200px; border: solid 1px #8b6125; background: #ba945d; margin-top: -30px; margin-left: 100px; margin-bottom: 20px;">
<p style="padding-left: 30px; padding-top: 60px;">Gold Box</p>

</div>

<p>Unless you’re viewing this page with IE6, you’ll see the gold box above overlapping the <code>&lt;select&gt;</code> element.</p>

This bug in IE6 has caused problems with drop-down menus that fail to overlap <code>&lt;select&gt;</code> elements. One solution is to use JavaScript to temporarily hide the <code>&lt;select&gt;</code> element, then make it reappear when the overlapping menu disappears. Another solution involves <a href="https://www.macridesweb.com/oltest/IframeShim.html">using an &lt;iframe&gt;</a>.</p>

### Positioned Parents in IE6/7

Internet Explorer versions 6 and 7 incorrectly reset the stacking context in relation to the nearest positioned ancestor element. To demonstrate this somewhat complicated bug, we’ll display two of the boxes again, but this time we’ll wrap the first box in a "positioned" element:
<div><br>
<div style="width: 200px; height: 200px; border: solid 1px #ccc; background: #ddd; margin-top: 20px;">
<p style="padding-left: 30px; padding-top: 60px;">Grey Box</p>

</div>
</div>
<div style="width: 200px; height: 200px; border: solid 1px #4a7497; background: #8daac3; margin-top: -50px; margin-left: 50px;">
<p style="padding-left: 30px; padding-top: 60px;">Blue Box</p>

</div>

<p>The grey box has a <code>z-index</code> value of "9999"; the blue box has a <code>z-index</code> value of "1" and both elements are positioned. Therefore, the correct implementation is to display the grey box on top of the blue box.</p>

If you view this page in IE6 or IE7, you’ll see the blue box overlapping the grey box. This is caused by the positioned element wrapping the grey box. Those browsers incorrectly "reset" the stacking context in relation to the positioned parent, but this should not be the case. The grey box has a much higher <code>z-index</code> value, and should therefore be overlapping the blue box. All other browsers render this correctly.</p>

### Negative Values in Firefox 2

In Firefox version 2, a negative <code>z-index</code> value will position an element behind the stacking context instead of in front of the background and borders of the element that established the stacking context. Here is a screen capture displaying this bug in Firefox 2:

<img title="Firefox 2 and negative values" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32f4c5e5-059f-4ec6-8787-9dba08fae030/ff2.gif" alt="Firefox 2 and negative values" width="500" height="371" />

Below is the HTML version of the above screen capture, so if you view this page in Firefox 3 or another currently-used browser, you’ll see the proper implementation: The background of the grey box (which is the element that establishes the stacking context) appears below everything else, and the grey box’s inline text appears above the blue box, which agrees with the "natural stacking order" rules outlined earlier.

<div style="width: 200px; height: 200px; border: solid 1px #ccc; background: #ddd; margin-top: 20px;"><br>
<p style="padding-left: 30px; padding-top: 60px;">Grey Box</p>

<div style="width: 200px; height: 200px; border: solid 1px #4a7497; background: #8daac3; margin-top: -50px; margin-left: 50px;">
<p style="padding-left: 30px; padding-top: 60px;">Blue Box</p>

</div>
</div>
<div style="width: 200px; height: 200px; border: solid 1px #8b6125; background: #ba945d; margin-top: -50px; margin-left: 100px; margin-bottom: 20px;">
<p style="padding-left: 30px; padding-top: 60px;">Gold Box</p>

</div>

{{% ad-panel-leaderboard %}}

## Showcase of Various Usage

Applying the <code>z-index</code> property to elements on a page can provide a quick solution to various layout challenges, and allows designers to be a little more creative with overlapping objects in their designs. Some of the practical and creative uses for the <code>z-index</code> property are discussed and shown below.</p>

### Overlapping Tabbed Navigation

The <span class="removed_link" title="https://www.ctconlinecme.com">CTCOnlineCME</span> website uses overlapping transparent PNG images with <code>z-index</code> applied to the "focused" tab, demonstrating practical use for this CSS property:

<span class="removed_link" title="https://www.ctconlinecme.com"><img title="CTCOnlineCME Tabbed Navigation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c682712-0562-40d4-8093-3a5845ec7740/ctc-tabs.jpg" alt="CTCOnlineCME Tabbed Navigation" width="500" height="267" /></span>

### CSS Tooltips

The <code>z-index</code> property can be used as part of a CSS-based tooltip, as shown in the example below from <a href="https://trentrichardson.com/examples/csstooltips/">trentrichardson.com</a>:

<a href="https://trentrichardson.com/examples/csstooltips/"><img title="CSS Tooltip" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc5584f-1dd1-4574-985f-a7cdb42ff5e7/trent-tooltip.jpg" alt="CSS Tooltip" width="500" height="203" /></a>

### Light Box

There are dozens of quality light box scripts available for free use, such as the JQuery plugin <a href="https://fancybox.net/">FancyBox</a>. Most, if not all of these scripts utilize the <code>z-index</code> property:

<a href="https://fancybox.net/"><img title="JQuery FancyBox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f22c638-36a5-47fc-8147-71dbd17321be/fancybox-light.jpg" alt="JQuery FancyBox" width="500" height="400" /></a>

Light box scripts use a semi-opaque PNG image to darken the background, while bringing a new element, usually a window-like <code>&lt;div&gt;</code> to the foreground. The PNG overlay and the <code>&lt;div&gt;</code> both utilize <code>z-index</code> to ensure those two elements are above all others on the page.</p>

### Drop-Down Menus

Drop down menus such as <a href="https://www.brainjar.com/dhtml/menubar/">Brainjar’s classic Revenge of the Menu Bar</a> use <code>z-index</code> to ensure the menu buttons and their drop-downs are at the top of the stack.

<a href="https://www.brainjar.com/dhtml/menubar/"><img title="Brainjar’s Revenge of the Menu Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3474967-0f58-46f7-971d-412ef603c62d/brainjar-menus.jpg" alt="Brainjar’s Revenge of the Menu Bar" width="500" height="202" /></a>

### Photo Gallery Effects

A unique combination of JQuery animation and <code>z-index</code> can create a unique effect for use in a slideshow or photo gallery, as shown in the example below from the usejquery.com website:

<img title="Usejquery.com’s Unique Gallery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c586aa8b-804d-4c62-8732-295f1fcd20a5/usejquery-photos.jpg" alt="Usejquery.com’s Unique Gallery" width="500" height="342" />

<a href="https://line25.com/tutorials/how-to-create-a-pure-css-polaroid-photo-gallery">Polaroid Photo Gallery by Chris Spooner</a> utilizes some CSS3 enhancements combined with <code>z-index</code> to create a cool re-stacking effect on hover.

<a href="https://line25.com/tutorials/how-to-create-a-pure-css-polaroid-photo-gallery"><img title="Pure CSS Polaroid Photo Gallery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86904afd-f233-46c3-901f-e25313dc399a/line25.jpg" alt="Pure CSS Polaroid Photo Gallery" width="500" height="400" /></a>

In this Fancy Thumbnail Hover Effect Soh Tanaka changes <code>z-index</code> values in a JQuery-based script:

<img title="Fancy Thumbnail Hover" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/690eb712-3d98-42d6-ab08-c50396e3f7fd/fancy-hover.jpg" alt="Fancy Thumbnail Hover" width="500" height="300" />

### CSS Experiments by Stu Nicholls

Stu Nicholls describes a number of CSS experiments on his website <a href="https://www.cssplay.co.uk">CSSplay</a>. Here are a few that make creative use of the <code>z-index</code> property:

<a href="https://www.cssplay.co.uk/articles/imagemap/index.html">CSS image map</a>

<a href="https://www.cssplay.co.uk/articles/imagemap/index.html"><img title="CSS Image Map" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d2b0217-738f-49be-84ce-a40f32996544/beatles-map.jpg" alt="CSS Image Map" width="400" height="240" /></a>

<a href="https://www.cssplay.co.uk/menu/jump.html">CSS game</a>

<a href="https://www.cssplay.co.uk/menu/jump.html"><img title="CSS Game" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aeeefb04-d66d-410d-8440-2917bff28346/css-game.jpg" alt="CSS Game" width="334" height="334" /></a>

<a href="https://www.cssplay.co.uk/layouts/frame.html">CSS Frames Emulation</a>

<a href="https://www.cssplay.co.uk/layouts/frame.html"><img title="CSS Frames Emulation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d87ec6a-fcc2-499f-bb84-78ff135a9ee8/frames-emulate.jpg" alt="CSS Frames Emulation" width="500" height="400" /></a>

### Layered Layout Enhancements

The <a href="https://24ways.org">24 ways</a> website implements <code>z-index</code> to enhance the site’s template, weaving year and date columns that stretch the length and width of the site’s content, for a very interesting effect.

<a href="https://24ways.org"><img title="24 ways layout" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74bec8ea-9624-4b65-837c-d032b500e9a7/24ways.jpg" alt="Usejquery.com’s Unique Gallery" width="500" height="303" /></a>

### Fancy Social Bookmarking Box

The Janko At Warp Speed site uses <code>z-index</code> in a "fancy share box":

<img title="Fancy Share Box" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb9ca77a-1740-4a53-a4d4-7a0ae4319655/sharebox.jpg" alt="Fancy Share Box" width="500" height="269" />

### Perfect Full Page Background Image

This technique was <a href="https://css-tricks.com/perfect-full-page-background-image/">described by Chris Coyier</a> and used on the <a href="https://ringvemedia.com/">ringvemedia.com</a> website. It implements <code>z-index</code> on content sections to ensure they appear above the "background" image, which is not a background image, but only mimics one:

<a href="https://css-tricks.com/perfect-full-page-background-image/"><img title="Perfect Full Page Background Image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6b1ce72-61a9-4a3f-8308-ae610369b210/full-bg.jpg" alt="Perfect Full Page Background Image" width="500" height="310" /></a>

## Conclusion

Stacking contexts in CSS are a complex topic. This article did not attempt to discuss every detail on that topic, but instead has attempted to provide a solid discussion of how a web page’s stacking contexts are affected by <code>z-index</code>, which, when fully understood, becomes a powerful CSS property.

Beginning developers should now have a good understanding of this property and avoid some of the common problems that arise when trying to implement it. Additionally, advanced developers should have a stronger understanding of how proper use of <code>z-index</code> can provide solutions to countless layout issues and open doors to a number of creative possibilities in CSS design.</p>

## Further Reading

*   [Elaborate Description of Stacking Contexts - W3C](https://www.w3.org/TR/CSS21/zindex.html)
*   [SitePoint CSS Reference](https://reference.sitepoint.com/css/z-index)
*   [Screencast by Chris Coyier](https://css-tricks.com/video-screencasts/40-how-z-index-works/)
*   [MSDN](https://msdn.microsoft.com/en-us/library/ms531188(VS.85).aspx)

