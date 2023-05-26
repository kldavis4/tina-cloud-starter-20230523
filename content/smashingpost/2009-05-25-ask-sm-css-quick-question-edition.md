---
title: 'Ask SM: CSS Quick-Question Edition'
slug: ask-sm-css-quick-question-edition
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32f71f2a-616c-4b6f-a717-81f8232ff5b0/illucss-editoren.gif
date: 2009-05-25T08:49:07.000Z
author: chris-coyier
description: >-
  This is our sixth installment of Ask SM, featuring reader questions about Web
  design focusing on HTML, CSS and JavaScript. These entries are not all
  questions, but rather quick Twitter responses to the query, "What has been
  your most difficult CSS challenge?" Among other things, this post covers the
  sticky footer issues, positioning elements at bottom of a div, on having
  layout, aligning labels and inputs, auto top and bottom padding, z-index and
  more.
categories:
  - Coding
  - CSS
---
This is our sixth installment of Ask SM, featuring reader questions about Web design focusing on HTML, CSS and JavaScript. These entries are not all questions, but rather quick Twitter responses to the query, "What has been your most difficult CSS challenge?" Among other things, this post covers the sticky footer issues, positioning elements at bottom of a div, on having layout, aligning labels and inputs, auto top and bottom padding, z-index and more. 

You may want to take a look at the following related posts:

*   [[Ask SM: CSS] Equal Spacing, CSS Font Replacement](https://www.smashingmagazine.com/2009/03/ask-sm-equal-spacing-css-image-replacement-max-side-on-images/)
*   [Mastering CSS, Part 1: Styling Design Elements](https://www.smashingmagazine.com/2009/08/mastering-css-styling-design-elements/)
*   [The Mystery Of The CSS Float Property](https://www.smashingmagazine.com/2009/10/the-mystery-of-css-float-property/)

## Div A Before Div B

<em><a href="https://twitter.com/leewillis77">@leewillis77</a></em> writes:
<blockquote>I currently have div B before div A in the HTML, and div B has float. I want to reproduce this, but with div A before div B in the HTML.</blockquote>

{{% feature-panel %}}

As long as both div B and div A have fixed widths, which when added together is less than or equal to the width of its parent, then it doesn't matter which of them comes first in the HTML!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e24d3278-134c-42df-8216-6db4a891c9c9/floatorder.png" alt="float order" />

Equally important to mention is that if div A and div B <strong>do not</strong> have a fixed with, then they <em>should</em>, because floating elements without widths is a recipe for trouble.</p>

## Sticky Footer

<em><a href="https://twitter.com/ilove2design">@ilove2design</a></em> writes:
<blockquote>I must admit, the "sticky footer" CSS problem was damn annoying until I found some solutions on the Web.</blockquote>

Agreed! The "sticky footer" pure-CSS solutions out there are pretty darn clever and come in handy regularly. Here are two:

*   [Ryan Fait's Sticky Footer](https://ryanfait.com/sticky-footer/)
*   [New CSS Sticky Footer](https://www.cssstickyfooter.com/)

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c50795f9-6212-4751-9f93-e508c688578e/stickfooter.jpg" alt="sticky footer" />

The both share one weakness, though, in that they require the footer to be a fixed pixel height, which is occasionally problematic. Generally, I just go bigger than necessary and give the text plenty of room to grow.</p>

## Positioning Elements At Bottom Of Div

<em><a href="https://twitter.com/_Zapp">@_Zapp</a></em> writes:
<blockquote>How do you position stuff at the bottom of a div with (or without) position absolute and relative, so that it will look the same on all browsers.</blockquote>

When you give an element relative positioning, that limits the scope of absolute positioning on all its child elements. This is one of my favorite techniques in CSS Web design. <a href="https://css-tricks.com/absolute-positioning-inside-relative-positioning/">I go over it in more detail here</a>, but let's take a quick look.

<pre><code class="language-markup tmp-xml">&lt;div id="parent"&gt;
     Lorem ipsum....
     &lt;p id="child"&gt;*Just a little footnote&lt;/p&gt;
&lt;/div&gt;</code></pre>

<pre><code class="language-css">#parent {
   position: relative;
   padding-bottom: 20px;
}
#child {
   position: absolute;
   bottom: 0;
   right: 0;
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/528476c3-f005-4df1-a8e7-18877a08af3b/pos-rel.png" alt="relative and absolute positioning" />

Just a quick note, the bottom/right combo <a href="https://www.brunildo.org/test/IE_rel_abs.html">needs <tt>hasLayout</tt> in IE 6</a> to work right.</p>

## Positioning Of Divs, Despite Source Order

<em>Alex Ross</em> writes:
<blockquote>Div top, middle, bottom. Top goes below content.</blockquote>

I think what you are getting at here is having the header of a website come <strong>after</strong> the main content in the HTML markup yet appear to be on top, where a header belongs. Part of the power that CSS gives us is that our designs don't have to be source-order-dependent, like table-based layouts do. Here is how I would do it:

<pre><code class="language-markup tmp-xml">&lt;div id="page-wrap"&gt;
     &lt;div id="main-content"&gt;&lt;/div&gt;
     &lt;div id="header"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

<pre><code class="language-css">#page-wrap { padding-top: 100px; position: relative; }
#header { position: absolute; top: 0; left: 0; width: 100%; }</code></pre>

This could potentially bring SEO benefits, especially if loads of content in the header are pushing down more important page content. See an example of this, where I talk about putting <a href="https://css-tricks.com/navigation-markup-after-content/">excessive navigation below the content</a>.</p>

## Centering Inside Resizeable Area

<em><a href="https://twitter.com/olliepee">@olliepee</a></em> writes:
<blockquote>I always have mental problems centering an automatically resizable div inside a 100%-width div.</blockquote>

Divs default to 100% wide, so if you have a div within a div without setting a specific width, that inside div will be the same width as its parent. If you do set a width for the inside div, you can make sure it's centered with the ol' classic centering trick.

<pre><code class="language-css">div {
    margin: 0 auto;
}</code></pre>

## On Having Layout

<em><a href="https://twitter.com/devolute">@devolute</a></em> writes:
<blockquote>Forgetting to apply <tt>zoom: 1;</tt> on <strong>everything</strong> in the IE conditional style sheet.</blockquote>

If anyone hasn't heard of this, applying <tt>zoom: 1;</tt> to elements is a way to force elements to gain the proprietary <tt>hasLayout</tt> property in IE browsers. This can fix a number of (truly) weird bugs in IE.

Read more about it <a href="https://www.satzansatz.de/cssd/onhavinglayout.html">here</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cdbb212-7568-4933-b289-b1bf42062a3a/onhavinglayout.png" alt="on having layout" />

## Aligning Labels And Inputs

<em><a href="https://twitter.com/ofaurax">@ofaurax</a></em> writes:
<blockquote>Correct alignment of a form's "label-input". I've not found a definitive solution in pure CSS.</blockquote>

Both labels and inputs (all the various types) are inline elements by default. Doing things like making them block-level elements and floating them can be very useful and help you avoid "unnecessary" markup. However, I think that's the first step towards cross-browser inconsistency. I have pretty decent luck many times leaving them as inline elements and using the vertical-align: middle; property to keep things inline. Then wrap the label/input pairs in divs to cause the necessary line breaks. This is particularly useful with radio buttons and checkboxes. Also remember that if only IE is giving you grief, you can use conditional style sheets and relative positioning to nudge particular elements into place.</p>

## Text With Gradient Background

<em>@pannpann</em> writes:
<blockquote>Creating background gradients inside dynamic numbers/letters.</blockquote>

Typically, text in Web design can be set to a solid color, and that's it. If you'd like a gradient effect over real Web text, a couple of methods are floating around. One is to lay a transparent PNG on top of the text that darkens a portion of it. <a href="https://www.webdesignerwall.com/demo/css-gradient-text/">Web Designer Wall has a tutorial</a> on this, but note that this causes the potentially serious usability problem of not being able to highlight the text.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d404a07-c0d4-4ce4-8d60-e87c0cac3c39/gradienttext.png" alt="gradient text" />

If progressive enhancement is your game, <a href="https://jayrobinson.tumblr.com/post/100728983/using-webkit-background-clip">Jay Robinson has a demo</a> on how you can use WebKit's proprietary <tt>-webkit-background-clip</tt> to achieve this.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf12a984-41d9-4a33-8cb5-9893f82ec0b0/bgclip.png" alt="background clip" />

Another slightly more laborious method would be to create all 10 digits as graphics, and then create unique CSS classes for each digit. Then use markup like <tt>&lt;span class="one"&gt;1&lt;/span&gt;&lt;span class="two"&gt;2&lt;/span&gt;</tt> to present the letter 12, and use CSS image replacement to replace the 1 and 2 with your custom graphics.</p>

## Auto Top And Bottom Padding

<em><a href="https://twitter.com/_Naz">@_Naz</a></em> writes:
<blockquote>Trying to make a div auto-center in your browser! ugh! still cant get it to pad auto top and bottom!</blockquote>

Unfortunately, vertical centering in CSS is a lot more difficult than horizontal centering. If you know the exact height of your div (that is, you set it yourself), you can use absolute positioning to get it done.

<pre><code class="language-css">div {
    position: absolute;
    left: 0;
    top: 50%;
    margin-top: -100px; /* half of div's height */
    height: 200px;
}</code></pre>

If you don't know the height, as painful as it is to say, using a table and the <tt>vertical-align</tt> property of table cells can get it done. If you'd like to explore other methods, the ThemeForest blog has a nice roundup of different methods.</p>

## Position Absolute With Text Wrap?

<em><a href="https://twitter.com/HerrWulf">@HerrWulf</a></em> writes:
<blockquote>Been having difficulties positioning a div to the bottom-right, with text wrapping around it...</blockquote>

This is an interesting one. Of course we can position a div to the bottom-right with absolute positioning as described above. But as soon as we do that, the div is "removed from the flow" of the document, meaning that regular text in the parent div will ignore its placement and go right over it.

I'm struggling to think of a really great solution for this... So if anyone has something, please share it in the comments. One short-term, hacky solution would be to force some sensibly placed line breaks in the text at the bottom that would make it seem like it's wrapping at default font sizes. Or place the image inline and floated to the right, but in the middle of the text, towards the bottom of it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0021511-1007-459a-b9ef-dec366771748/wrapping.png" alt="wrapping" />

## Separate Or Multiple CSS Files?

<em><a href="https://twitter.com/scottradcliff">@scottradcliff </a></em> writes:
<blockquote>What is your preferred method of using CSS? A few separate files (e.g. type.css, layout.css, etc.) or one large file?</blockquote>

The only circumstance in which I like to break out CSS into multiple files is when the CSS is totally unique to a certain page, and loading it for every other page would be useless. Like if you have an "About" page that has unique styling, I'd load the default style.css, and then load an about.css file after it to override anything that it needs.

I don't like breaking CSS into layout.css, typography.css, etc. just because that isn't how I think. When I look at the footer on a website, I want to look at <em>all</em> the CSS for that region in one place, not have to open two different files. That is just how my mind works, but I don't have any particular problem with doing it the other way.

Super-efficent nerds will yell at you for requiring unnecessary HTTP requests to load extra CSS files, which can slow things down. And so, to be extra fast, you should load only <em>one</em> CSS file and <em>one</em> JavaScript file per page. They would be right, of course, if speed were the only consideration. Practicality, though, counts for a lot in my book. And let's face it, for most of the websites that we work on, half a zillionth of a second doesn't matter as much as the budget.</p>

## Z-index And Drop-Downs

<em><a href="https://twitter.com/andrewturner">@andrewturner</a></em> writes:
<blockquote>The hardest issue I've been working on was one last week, where I was stuck with an issue relating to z-index and drop-down menus</blockquote>

I'm surprised at how often problems with this come up. Most drop-down menus rely on some combination of absolute and relative positioning. Once elements have this, they become part of the z-index "flow," so giving them high values will usually get them on top of whatever you need them to be on top of.

The big exception, which seems to come up incredibly often, is when you need to overlay Flash content. Usually the solution here is to make sure that the Flash content is embedded with <tt>wmode=transparent</tt>. <a href="https://github.com/swfobject/swfobject">SWFObject</a> can help with this and offers numerous other advantages.</p>

## Customizing Radio Buttons And Checkboxes

<em>Anonymous Email</em> writes:
<blockquote>For some time, I have been trying to create custom combo boxes and checkboxes for my forms based on images. I followed some tutorials with no good results, and I haven't yet found a solution. What is a clean way to get this done?</blockquote>

With pure CSS, there is no way to truly customize radio and checkbox inputs, at least not by replacing them with custom graphics. JavaScript comes to the rescue, though, by hiding them and replacing them with custom elements. Those custom elements will have click handlers on them that visually replicate a radio button being on or off, and invisibly updating the "real" hidden form element.

This <a href="https://www.dfc-e.com/metiers/multimedia/opensource/jqtransform/">jQuery plug-in</a> does a nice job of it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27604ce7-6f53-4192-b52c-0f08aebe1875/customizedform.png" alt="customized form" />

## No JavaScript Tooltips

<em>@firewalker06</em> writes:
<blockquote>How can we get a tooltip effect that can be used in any browser and without JavaScript?</blockquote>

CSS Globe had an article way back that does a good job of explaining it. It definitely can be done, and I'll explain briefly here. You can count on the <tt>:hover</tt> effect on anchor links in any browser, so you'll want to use that. Within the anchor link, you can have a &lt;span&gt; element which by default is set to <tt>display: none;</tt>. Then, with the hover CSS, you can display the span.

<pre><code class="language-css">a span {
    display:none;
}
a:hover span {
    display:block;
    position:absolute;
    float:left;
    white-space:nowrap;
    top:-2.2em;
    left:.5em;
    background:#fffcd1;
    border:1px solid #444;
    color:#444;
    padding:1px 5px;
    z-index:10;
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/465c5691-0901-47f5-92e3-90cd1fdf7774/csstooltip.png" alt="css tooltip" />

These values display a box with the width it needs to appear above and to the right of the link, much like browser defaults. But you can customize this however you'd like. But make sure <strong>not</strong> to use a title attribute on the link, otherwise both would show up on hover and would look weird. So, this effect should purely be an added bonus and not valuable required content because it won't be very "accessible."

That wraps up another installment of Ask SM! If you have questions to ask, refer to the top of this article on ways to submit them.

