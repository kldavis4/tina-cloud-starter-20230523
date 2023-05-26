---
title: '[Ask SM] Transparent Background, Positioning Problem'
slug: ask-sm-css-auto-refreshing-content-transparent-backgrounds-positioning
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9eeb6492-c11b-4e4f-90df-cec9aa325eab/css-problem.jpg
date: 2009-04-17T14:01:42.000Z
author: chris-coyier
description: >-
  This is our fifth installment of Ask SM, featuring reader questions about Web
  design, focusing on HTML, CSS and JavaScript. In this post we’ll cover how you
  can style only the text inputs, refreshing a content-block automatically, how
  to avoid some positioning problems and create and use transparent
  div-backgrounds; we also discuss further CSS-related problems and deliver
  answers to a couple of quickfire questions.

  [![tweets](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b3d8d65-7cf0-4f50-8c78-0895720548ac/bantweets.jpg)](https://www.smashingmagazine.com/2009/04/17/ask-sm-css-auto-refreshing-content-transparent-backgrounds-positioning/)

  If you have a question about CSS or JavaScript, feel free to reach me (Chris
  Coyier) via one of these methods: a) send an email to **ask [at]
  smashingmagazine [dot] com** with your question; b) [Post your question in our
  forum](https://forum.smashingmagazine.com/viewtopic.php?f=10&t=272) or c) if
  you have a quick question, just tweet us
  [@smashingmag](https://twitter.com/smashingmag) or
  [@chriscoyier](https://twitter.com/chriscoyier) with the hashtag _#asksmcss_.

  Please note: I will do what I can to answer questions, but I will certainly
  not be able to answer all of them. However, I hope you use the forums to post
  questions because that gives you the best opportunity to get help from the
  community.
categories:
  - Coding
  - CSS
---
This is our fourth installment of Ask SM, featuring reader questions about Web design, focusing on HTML, CSS and JavaScript. In this post we’ll cover how you can style only the text inputs, refreshing a content-block automatically, how to avoid some positioning problems and create and use transparent div-backgrounds; we also discuss further CSS-related problems and deliver answers to a couple of quickfire questions.

<p>If you have a question about CSS or JavaScript, feel free to reach me (Chris Coyier) via one of these methods:

<ol>
	<li>Send an email to <strong>ask [at] smashingmagazine [dot] com</strong> with your question.</li>
	<li>Post your question in our forum.</li>
	<li>Or, if you have a quick question, just tweet us <a href="https://twitter.com/smashingmag">@smashingmag</a> or <a href="https://twitter.com/chriscoyier">@chriscoyier</a> with the hashtag <em>#asksmcss</em>.</li>
</ol>

<p>Please note: I will do what I can to answer questions, but I will certainly not be able to answer all of them. However, I hope you use the forums to post questions because that gives you the best opportunity to get help from the community.</p>
<p>You may be interested in the following related posts:</p>
<ul>
<li><a href="https://www.smashingmagazine.com/2009/03/23/ask-sm-equal-spacing-css-image-replacement-max-side-on-images/">[Ask SM] Equal Spacing, CSS Font Replacement</a></li>
<li><a href="https://www.smashingmagazine.com/2009/02/20/ask-sm-css-smooth-page-scrolling-divs-of-equal-height-dealing-with-ie-6/">[Ask SM]: Divs of Equal Height, Dealing with IE 6</a></li>
<li><a href="https://www.smashingmagazine.com/2009/02/05/ask-sm-pixel-width-decisions-rollover-buttons-modal-boxes/">[Ask SM]: Pixel Width Decisions, Modal Boxes</a></li>
</ul>

## Styling Only Text Inputs

<p><em><a href="https://forum.smashingmagazine.com/css-and-x-html-f10/styling-only-input-text-t1896.html">DonRonito</a></em> writes:</p>

{{% feature-panel %}}

<blockquote>Since I use a CMS for generating forms, I have encountered a problem with styling of forms that are auto-generated. I can use <tt>input[type=text]</tt>, which only styles the text inputs, but it does not work in IE. I wonder if there is another good way to do this.</blockquote>

<p>Hi Don, as you seem to know, that selector is what is known as an <strong>attribute selector</strong> in CSS. You can use it on any element if you intend to select only elements with particular values of inputs. For example, <tt>a[title="home"]</tt> is a valid attribute selector, which will target elements like this <tt>&lt;a title="home" ... &gt;</tt>. In the case of inputs, this is particularly useful because there are so many different types: text, submit, radio, image, etc., but they are all &lt;input&gt;'s. You may want to apply a width to text inputs but not radio buttons, for example.</p>

<p>As you also found out, IE 6 and below doesn't like attribute selectors (it just ignores them). Huge bummer. One solution, which was pointed out right away in the forums, is to apply an ID or class to these inputs. You could then use the ID or class to target them in the CSS and apply your unique styling that way, without fear of affecting other types of inputs. But you say that these forms are being generated by a CMS, which seems to imply that you don't have this type of fine-grained control.</p>

<p>A bit of a rough situation you have there. But there is hope, if you don't mind a little JavaScript. If you use jQuery, it supports CSS selectors that accurately do the selecting for you, even in IE 6:</p>

	<pre class="js" name="code"><code>$("input[type=text]").css({
		// apply styling
});</code></pre>

<p>Perhaps an even better solution is to use the Dean Edward's ie7-js script, which automatically makes your CSS attribute selector just work, as well as fix a slew of other IE 6 bugs:</p>

	<pre><code class="language-markup tmp-xml">&lt;!--[if lt IE 7]&gt;
&lt;script src="https://ie7-js.googlecode.com/svn/version/2.0(beta3)/IE7.js" type="text/javascript"&gt;&lt;/script&gt;
&lt;![endif]--&gt;</code></pre>

## Auto-Refreshing RSS Content

<p><em><a href="https://nikibrown.com/">Niki Brown</a></em> writes:</p>

<blockquote>I followed your SimplePie tutorial (<a href="https://www.smashingmagazine.com/2009/02/20/ask-sm-css-smooth-page-scrolling-divs-of-equal-height-dealing-with-ie-6/">Ask SM, 3rd ed.</a>) and made <a href="https://nikibrown.com/bananatweets/">Banana Tweets</a>. But now I'm wondering how I would get the tweets to auto-refresh, say, every 20 seconds.</blockquote>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b3d8d65-7cf0-4f50-8c78-0895720548ac/bantweets.jpg" alt="tweets" />

<p>Hey Niki, great question! We can get this done fairly easily with the AJAX powers of jQuery. We can start where we left off last time. In that example, when the page has loaded, SimplePie works its magic by fetching the RSS (or Atom) feed data and displaying it.</p>

<p>Instead, we'll pull out all that SimplePie PHP and put it into a separate file (which we'll call <em>feeder.php</em>).</p>

	<pre><code class="language-php">&lt;?php
    require_once(&#39;inc/simplepie.inc&#39;);

    $feed = new SimplePie();

    $feed-&gt;set_feed_url(array(
    	&#39;https://search.twitter.com/search.atom?q=twitter&#39;
    ));

    $feed-&gt;enable_cache(true);
    $feed-&gt;set_cache_location(&#39;cache&#39;);
    $feed-&gt;set_cache_duration(10);

    $feed-&gt;init();

    $feed-&gt;handle_content_type();

    if ($feed-&gt;error): ?&gt;

        &lt;p&gt;&lt;?php echo $feed-&gt;error; ?&gt;&lt;/p&gt;

    &lt;?php endif; ?&gt;

    &lt;?php foreach ($feed-&gt;get_items() as $item): ?&gt;

    	&lt;div class=&quot;chunk&quot;&gt;

    		&lt;h4 style=&quot;background:url(&lt;?php $feed = $item-&gt;get_feed(); echo $feed-&gt;get_favicon(); ?&gt;) no-repeat; text-indent: 25px; margin: 0 0 10px;&quot;&gt;&lt;a href=&quot;&lt;?php echo $item-&gt;get_permalink(); ?&gt;&quot;&gt;&lt;?php echo $item-&gt;get_title(); ?&gt;&lt;/a&gt;&lt;/h4&gt;

    		&lt;p class=&quot;footnote&quot;&gt;Source: &lt;a href=&quot;&lt;?php $feed = $item-&gt;get_feed(); echo $feed-&gt;get_permalink(); ?&gt;&quot;&gt;&lt;?php $feed = $item-&gt;get_feed(); echo $feed-&gt;get_title(); ?&gt;&lt;/a&gt; | &lt;?php echo $item-&gt;get_date(&#39;j M Y | g:i a T&#39;); ?&gt;&lt;/p&gt;

    	&lt;/div&gt;

    &lt;?php endforeach; 

?&gt;</code></pre>

<p>This "feeder" file could be loaded directly, but it would be completely unstyled. The point is to use some AJAX to load the content from that page and plug it into our real page. Then we can set up a JavaScript interval to call this file every 20 seconds and replace the current content:</p>

	<pre><code class="language-markup tmp-xml">&lt;script type=&quot;text/javascript&quot;&gt;

    function getFresh() {

        $(&quot;#loadArea&quot;).fadeOut(400, function() {
$(&quot;#loadArea&quot;).load(&quot;feeder.php&quot;, function() {
                $(&quot;#loadArea&quot;).fadeIn();
            });
        });

    };

	$(function(){
		getFresh();
		var int = setInterval(&quot;getFresh()&quot;, 10000);
	});

&lt;/script&gt;</code></pre>

<p>Note that the above code is dependent on jQuery.</p>

<p><a href="https://css-tricks.com/examples/FeedSmusherAJAX/">VIEW DEMO</a>  &nbsp;  <a href="https://css-tricks.com/examples/FeedSmusherAJAX.zip">DOWNLOAD FILES</a></p>

## Positioning Blues

<p><em><a href="https://jamesbull.ca/">James Bull</a></em> writes:</p>

<blockquote>On my website, I was wondering how to avoid a scaling problem.  If you drag the browser smaller than the width of the page, there are issues with my top-corner images.  I've tried various min-width values on different containers and can't seem to solve it. Know how to do this?</blockquote>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7bab8fc-ea31-44c6-aff6-bc2264da8d5c/logopush.jpg" alt="logo push" />

<p>Hey James, first of all, your background looks like it is a combination of four different layered images. One on the <tt>html</tt> element, <tt>body</tt> element, <tt>image_left</tt>, and <tt>image_right</tt>. Because yours is just a centered fixed-width website, you could get this done with just two: one for the background texture, and the other for all the other frills.</p>

<p>But in looking at the problem at hand, the percentage positioning you are using for those "corner" images is the problem. Your image "image_left.png" is set to a right position of 50%. That means this image will be perfectly willing to hang off the left side of the browser window without limit and without causing scroll. The "image_right.png" container is set to a left position, which <em>will</em> cause horizontal scroll (weird, huh?).</p>

<p>The <strong>quick fix</strong> in your case is to make sure the viewport area cannot shrink any narrower than the width of image_left.png (876 pixels). So just set:</p>

<pre><code class="language-css">html {
	min-width: 876px;
}</code></pre>

<p>In your particular design, you might wanna beef that up to about 912px to keep your full name visible at all times. Remember that IE 6 doesn't support min-width, but it looks like you hide those images for IE 6 anyway.</p>

## Transparent Div Background

<p><em>Louie Livon-Bemel</em> writes:</p>

<blockquote>Is there an easy way to give a div's background a low opacity but have the content be normal. The only way I know of is to position a second div behind the content with z-index and give the background div a lower opacity. And if possible, I'd want this to work in all browsers.</blockquote>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80c6bbb5-f9a7-469d-ace1-2bc6075b3a2f/png24.jpg" alt="png24" />

<p>They way you describe works, but going to those lengths is probably unnecessary. If the background of the div is an image, you could lower its opacity in Photoshop and save it as an alpha-transparent PNG (PNG-24 in Photoshop). Then use that PNG as your background image. You'll need <a href="https://www.dillerdesign.com/experiment/DD_belatedPNG/">PNG hack</a> for IE 6. If you have a solid-color background, you could use a repeating 1x1 pixel alpha-transparent PNG of that color, or use <a href="https://css-tricks.com/rgba-browser-support/">RGBa</a>.</p> 

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8c4d5ac-86e7-48b1-a83c-2dee628bd802/rgba.png" alt="rgba" />

<br />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17249274-bf29-4263-a183-1384fae7ec44/transpback.jpg" alt="backgrounds" />

## To Use A CSS Framework?

<p><em>Andrew Turner</em> writes:</p>

<blockquote>I was wondering whether you think it best to use available CSS Frameworks for projects (e.g. Blueprint CSS) or to build one yourself from the ground up? Are there any disadvantages or advantages to using frameworks?</blockquote>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d9ceb0c-64b5-4175-8069-c14a66206763/blueprint-header-clean.png" alt="blueprint" />

<p>The common arguments against frameworks are 1) bloat -- that is, a bunch of unnecessary CSS for alternate grids you may never use -- and 2) semantics problems. Your markup will be using things like <tt>&lt;div id=grid_13_b .. /&gt;</tt>, which isn't very helpful or semantic.</p>

<p>My argument is that CSS is not (for the most part) a very complicated language. Writing it from scratch for each project isn't all that time-consuming and results in exactly what you need and nothing else.</p>

<p>All that being said, I do believe that if you dedicate some time to learning all the ins and outs of a particular framework, it could potentially save you some time as well as lend a familiar feel to all of your projects. If <a href="https://www.blueprintcss.org/">Blueprint CSS</a> is good enough for Jeff Croft and Blueflavor, it can work for you.</p>

## Image The Size Of A Table Cell

<p><em>William Woolard</em> writes:</p>

<blockquote>I've created a calendar using PHP that generates the days within table cells.  I've modified it to add a <tt>class="currentdate"</tt> to the current date.  The single-digit day cells are one size (1) and the double-digit day cells are twice as large (24).  Is there a way to apply a background image to the cell that adjusts according to the size of the cell? For instance, the background is a circle, as if the day has been circled (for single-digit days) and expands to look like an oval on the days that are double digits?</blockquote>

<p>This is really a rock-and-a-hard-place scenario. CSS background images are not resizeable, so that's out. The other way to include an image on the page is with an inline <tt>&lt;img ... /&gt;</tt>. These <em>are</em> resizeable, so we may be on to something. The go-to method for stretching an image to the size of its parent is to use absolute positioning and set the top, bottom, left and right values to zero. Unfortunately, the parent needs to have relative positioning for this to work, and table cells do not accept relative positioning.</p>

<p>Divs, however, do accept relative positioning. So, a div inside will stretch it to the width of the parent table cell, but not necessarily the height, and we are unable to force it because of the no-relative-positioning-on-table-cells problem mentioned above.</p>

<p>With CSS alone, we can almost get it: </p>

	<pre><code class="language-markup tmp-xml">&lt;td class=&quot;currentDay&quot;&gt;
   &lt;div&gt;
      &lt;img src=&quot;images/circle.png&quot; class=&quot;circle&quot; alt=&quot;&quot; /&gt;
      19
   &lt;/div&gt;
&lt;/td&gt;</code></pre>

	<pre><code class="language-css">td                  { padding: 5px; vertical-align: middle; text-align: center; }
td div              { position: relative; }
.circle             { position: absolute; top: 0; left: 0; right: 0; bottom: 0; }</code></pre>

<p>The height is still a problem though, and I don't see a purely CSS solution. What we need to do is set the height and width of that image to be the exact height and width of the table cell that it's in. We can lean on a bit of jQuery to do that math for us:</p>

	<pre class="js" name="code">$(function() {

    var theImage = $(".circle");

    var theCell = theImage.parent().parent();

    var theWidth = parseInt(theCell.css("width")) + parseInt(theCell.css("padding-left")) + parseInt(theCell.css("padding-right"));

    var theHeight = parseInt(theCell.css("height")) + parseInt(theCell.css("padding-top")) + parseInt(theCell.css("padding-bottom"));

    $(".circle")
        .width(theWidth)

        .height(theHeight)
        .css({
            "top": -parseInt(theCell.css("padding-top")),
            "left": -parseInt(theCell.css("padding-left"))
        });

});</pre>

<p>Kind of a lot of work for such a seemingly simple problem, but at least it works and is adaptable. If anyone can figure out a purely CSS solution, I'd love to see it!</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/266588b2-6616-48b9-bfaa-84a111b71e0a/imagesizeofcell.png" alt="cell" />

<p><a href="https://css-tricks.com/examples/ImageToCellSize/">VIEW DEMO</a></p>

## Styling the HTML Element

<p><em>Aaron Bazinet</em> writes:</p>

<blockquote>Can you style the HTML element directly, such as by applying a background image and color to it. I remember someone mentioning it once, but is it safe/valid to do, or bad mojo?</blockquote>

<p>Hey Aaron, just to clarify for readers, all Web pages have an <tt>&lt;html&gt;</tt> element that wraps the entire page. The tag usually comes just after the DOCTYPE specification. So is something like this do-able in CSS?:

<pre><code class="language-css">name="code">html { background-color: #ccc; }</code></pre>

<p>Yep, it is, should be fine. And in fact, it can fix some <a href=="https://scriptandstyle.com/centering-a-body-background-image-that-behaves">otherwise weird issues</a>. I believe you need to go all the way back to IE 5 to see problems with it, which isn't a concern anymore. Sitepoint has <a href="https://www.sitepoint.com/blogs/2009/02/11/styling-the-html-and-body-elements/">a little more info</a> on this and reminds us to avoid positioning this element.

## Quickfire Questions

<blockquote>Have you ever used or heard of Sweetcron? We need a tutorial on theming it! Please help!</blockquote>

<p>I have heard of <a href="https://www.sweetcron.com/">Sweetcron</a>. I think it is incredibly well-done self-hosted life-streaming software. It was produced by Tokyo-based Web developer Yongfook, who uses Sweetcron on <a href="https://www.yongfook.com/">his personal website</a>. I did a <a href="https://nettuts.com/misc/building-a-custom-lifestream-website-with-sweetcron/">tutorial on building a custom life-stream website</a> with it on NETTUTS.</p>

<blockquote>Should I enroll in a Web design program that is geared more to the "design" end (artsy) or the "development" end (coding)? Which one will benefit me more in making Web design a full-time career?</blockquote>

<p>If you are lucky enough to be looking at colleges and programs that give you that kind of choice, I think you will do well either way. I got a multimedia/graphic design degree, and we didn't even once look at HTML (not kidding). Because you said at the end, though, that you want to make "Web design" your full-time career, the "design" path would seem to make more sense than the "development" path.</p>

<blockquote>All of my images have a few pixels of extra background space along the bottom length.</blockquote>

<p>In this particular scenario, a div is wrapping the image, creating the double-border effect. The image inside is an inline element, so the space following the <tt>&lt;img ... /&gt;</tt> tag and the closing div tag is apparently creating a line break and causing the gap. A quick fix is to make the image a block-level element, which eliminates the gap.

<pre><code class="language-css">.image img { display: block; }</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/560dea8e-03fe-405c-b8cf-e19c5ae78e2d/exspace.jpg" alt="space" />

<p>That wraps up another installment of Ask Smashing Magazine! If you have questions to ask, refer to the top of this article for ways to submit your questions.</p>

## Related posts

<p>You may be interested in the following related posts:</p>
<ul>
<li><a href="https://www.smashingmagazine.com/2009/03/23/ask-sm-equal-spacing-css-image-replacement-max-side-on-images/">[Ask SM] Equal Spacing, CSS Font Replacement</a></li>
<li><a href="https://www.smashingmagazine.com/2009/02/20/ask-sm-css-smooth-page-scrolling-divs-of-equal-height-dealing-with-ie-6/">[Ask SM]: Divs of Equal Height, Dealing with IE 6</a></li>
<li><a href="https://www.smashingmagazine.com/2009/02/05/ask-sm-pixel-width-decisions-rollover-buttons-modal-boxes/">[Ask SM]: Pixel Width Decisions, Modal Boxes</a></li>
</ul>

{{< signature "al" >}}

