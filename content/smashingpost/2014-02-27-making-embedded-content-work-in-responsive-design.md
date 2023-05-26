---
title: Making Embedded Content Work In A Responsive iFrame
slug: making-embedded-content-work-in-responsive-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a38c615-bb96-4b20-887b-96eb2eaaf21f/lego-fig05-large-opt.jpg
date: 2014-02-27T09:14:06.000Z
author: rachel-mccollin-2
description: >-
  A few HTML elements don’t play nice with responsive layouts. One of these is
  the good ol' `iframe`, which you may need to use when embedding content from
  external sources such as YouTube. In this article, we’ll show you how to
  make embedded content responsive using CSS.
categories:
  - Mobile
  - Responsive Design
  - Content Strategy
---
A few HTML elements don’t play nice with <a href="https://www.smashingmagazine.com/responsive-web-design-guidelines-tutorials/">responsive layouts</a>. One of these is the good ol' <code>iframe</code>, which you may need to use when embedding content from external sources such as YouTube.

In this article, we’ll show you how to make embedded content responsive using CSS, so that content such as video and calendars resize with the browser’s viewport. For those occasions when non-coders will be embedding video on your website and you don’t want to rely on them adding extra markup, <strong>we’ll also look at a solution that uses JavaScript instead of CSS</strong>.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Ways To Reduce Content Shifting On Page Load](https://www.smashingmagazine.com/2016/08/ways-to-reduce-content-shifting-on-page-load/)
*   [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
*   [How To Create An Embeddable Content Plugin For WordPress](https://www.smashingmagazine.com/2012/11/embeddable-content-wordpress/)
*   [Content Security Policy, Your Future Best Friend](https://www.smashingmagazine.com/2016/09/content-security-policy-your-future-best-friend/)

<em>Note: This technique was originally detailed in Thierry Koblenz's excellent tutorial '<a href="https://alistapart.com/article/creating-intrinsic-ratios-for-video">Creating Intrinsic Ratios for Video</a>'. I've used techniques I learned from his tutorial and expanded on them here for additional content types such as calendars.</em>

{{% feature-panel %}}

## The Markup For Embedded Content

Services such as YouTube provide code that you can copy and paste into your own website to embed content. I tend to recommend to my clients that they host video with YouTube because it will save them server space and, regardless of the user’s browser or device, YouTube will display the video correctly. The two main ways to embed video on a website are the HTML5 <code>video</code> element, which doesn’t work in legacy versions of Internet Explorer, and Flash, which doesn’t work on iOS devices and isn’t standards-compliant.

When you embed content from an external source, the code will include an <code>iframe</code>:

<pre><code class="language-markup">
&lt;iframe src="https://youtube.com/embed/4aQwT3n2c1Q" height="315" width="560" allowfullscreen="" frameborder="0"&gt;&lt;/iframe&gt;
</code></pre>

This <code>iframe</code> enables external content to be displayed on your website, because it includes a URL that points to the source of the streamed content.

However, you’ll notice that our <code>iframe</code> includes <code>width</code> and <code>height</code> attributes. Remove these and the iframe will disappear because it would have no dimensions. And you can’t fix this in your style sheet, unfortunately.

The <code>width</code> attribute means that, on a screen narrower than 560 pixels, <strong>the embedded content will protrude outside of its containing element</strong>, breaking the layout. In the example below, I’ve added the code above to a page of my blog. The screenshot is taken from an iPhone in portrait mode (320 pixels wide), and the rest of the page has been shrunk so that the embedded content fits the screen. <strong>Far from ideal!</strong>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3aa8079-4740-4ceb-ad00-1bc0253f6424/01-non-responsive-video-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65c307d2-cd7d-44d6-9b7f-ff2ab28594f8/01-non-responsive-video.png" alt="responsive iframe - Video breaks the layout in a responsive website on iPhone" width="320" height="480" /></a><br>
<em>Screenshot taken from an iPhone in portrait mode (320px wide). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65c307d2-cd7d-44d6-9b7f-ff2ab28594f8/01-non-responsive-video.png">Larger view</a>)</em>

Fortunately, there is a way around this using CSS. First, I’ll show you how to do this with embedded video, and then with calendars.</p>

## Responsive iFrame Video

### The Markup

To make embedded content responsive, you need to add a containing wrapper around the <code>iframe</code>. Your markup would be as follows:

<pre><code class="language-markup">
&lt;div&gt;
    &lt;iframe src="https://youtube.com/embed/4aQwT3n2c1Q" height="315" width="560" allowfullscreen="" frameborder="0"&gt;
    &lt;/iframe&gt;
&lt;/div&gt;
</code></pre>

The next step is to add styling to this new wrapper and the <code>iframe</code> within it.</p>

### The CSS

First, we style the containing wrapper with the <code>.video-container</code> class. As proposed by <a href="https://twitter.com/thierrykoblentz">Thierry Koblentz</a> in his ALA article <a href="https://alistapart.com/article/creating-intrinsic-ratios-for-video/">"Creating Intrinsic Ratios For Video"</a>, we can use the following snippet in our style sheet:

<pre><code class="language-css">
.video-container {
    position: relative;
    padding-bottom: 56.25%;
    padding-top: 35px;
    height: 0;
    overflow: hidden;
}
</code></pre>

This does a few things:

*   Setting the `position` to `relative` lets us use absolute positioning for the `iframe` itself, which we’ll get to shortly.
*   The `padding-bottom` value is calculated out of the aspect ratio of the video. In this case, the aspect ratio is 16:9, which means that the height will be 56.25% of the width. For a video with a 4:3 aspect ratio, we set `padding-bottom` to 75%.
*   The `padding-top` value is set to 30 pixels to allow space for the chrome — this is specific to YouTube videos.
*   The `height` is set to `0` because `padding-bottom` gives the element the height it needs. We do not set the width because it will automatically resize with the responsive element that contains this div.
*   Setting `overflow` to `hidden` ensures that any content protruding outside of this element will be hidden from view.

<strong>We also need to style the iframe itself.</strong> Add the following to your style sheet:

<pre><code class="language-css">
.video-container iframe {
    position: absolute;
    top:0;
    left: 0;
    width: 100%;
    height: 100%;
}
</code></pre>

This targets <code>iframe</code>s inside containers with the <code>.video-container</code> class. Let’s work through the code:

*   Absolute positioning is used because the containing element has a height of `0`. If the iframe were positioned normally, we would have given it a height of `0` as well.
*   The `top` and `left` properties position the iframe correctly in the containing element.
*   The `width` and `height` properties ensure that the video takes up 100% of the space used by the containing element (which is actually set with padding).

Having done this, the video will now resize with the screen’s width. Here’s how it will look on a desktop:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94287f00-19f8-4890-96bb-b06280a7a72f/02-desktop-video-after-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b257d659-73fd-4cd5-9e6d-4e9f654530a7/02-desktop-video-after.png" alt="Responsive video as seen on the desktop (in the flow of the content, fitting nicely)" width="500" height="459" /></a><br>
<em>Desktop screenshot of the video resizing the screen’s width. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94287f00-19f8-4890-96bb-b06280a7a72f/02-desktop-video-after-large.png">Larger view</a>)</em>

And here’s how it will look on a screen that is 320 pixels wide:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7eabaa3-a0a4-4179-9ad3-0bfcfbec9f4b/03-responsive-video-iphone-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10b1bf90-e253-4cbc-aa5d-74ab1cf68abb/03-responsive-video-iphone.png" alt="Responsive video fits into the layout on a 320px wide screen" width="320" height="480" /></a><br>
<em>The video on a 320 pixels wide screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7eabaa3-a0a4-4179-9ad3-0bfcfbec9f4b/03-responsive-video-iphone-large.png">Larger view</a>)</em>

Let’s move on to other sources of embedded content — specifically, Google calendars.

## Responsive Calendar

### The Markup

The CSS to make any form of embedded content responsive is essentially the same, but different content will have different aspect ratios, which means you’ll need to set the <code>padding-bottom</code> value accordingly.

Below is a screenshot of a website that I manage for a primary school, a website that <strong>embeds a Google calendar</strong>. As you can see, the calendar breaks the layout on a small screen. In this case, the website is displayed at the correct width, but the calendar goes beyond the screen’s width.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ca145fc-cb37-40a4-8536-6db2476c54ba/04-non-responsive-calendar-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2328454-93d4-4601-9973-14e74e0fc06d/04-non-responsive-calendar.png" alt="A celandar as seen on a responsive website on an iPhone - not all of the calendar is visible" width="320" height="480" /></a><br>
<em>The calendar breaks the layout on a small screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ca145fc-cb37-40a4-8536-6db2476c54ba/04-non-responsive-calendar-large.png">Larger view</a>)</em>

The markup for the embedded calendar is as follows:

<pre><code class="language-markup">
&lt;iframe src="https://www.google.com/calendar/embed?height=600&amp;amp;wkst=1&amp;amp;bgcolor=%23FFFFFF&amp;amp;src=60aqhusbghf7v0qvvbfu1ml22k%40group.calendar.google.com&amp;amp;color=%232952A3&amp;amp;ctz=Europe%2FLondon" style=" border-width:0 " width="800" height="600" frameborder="0" scrolling="no"&gt;&lt;/iframe&gt;
</code></pre>

To make a calendar responsive, add a div with a class of <code>.calendar-container</code> to contain the iframe:

<pre><code class="language-markup">
&lt;div&gt;
    &lt;iframe src="https://www.google.com/calendar/embed?height=600&amp;amp;wkst=1&amp;amp;bgcolor=%23FFFFFF&amp;amp;src=60aqhusbghf7v0qvvbfu1ml22k%40group.calendar.google.com&amp;amp;color=%232952A3&amp;amp;ctz=Europe%2FLondon" style=" border-width:0 " width="800" height="600" frameborder="0" scrolling="no"&gt;
    &lt;/iframe&gt;
&lt;/div&gt;
</code></pre>

The next step is to style this div.</p>

### The CSS

The CSS for a calendar is almost identical to the CSS for a video, with two exceptions: The aspect ratio will be different, and <code>padding-top</code> isn’t needed.

Add the following to your style sheet:

<pre><code class="language-css">
.calendar-container {
    position: relative;
    padding-bottom: 75%;
    height: 0;
    overflow: hidden;
}
</code></pre>

In this case, the <code>iframe</code> is 800 pixels wide and 600 pixels high, which gives us an aspect ratio of 4:3. So, set <code>padding-bottom</code> to be <code>75%</code>.

Having done this, we need to apply the same styling to the iframe element in this new container:

<pre><code class="language-css">
.calendar-container iframe {
    position: absolute;
    top:0;
    left: 0;
    width: 100%;
    height: 100%;
}
</code></pre>

This is exactly the same styling that we applied to the video.

Now, the calendar will resize with the browser window, as shown here in Opera Mobile on an Android phone:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4330431e-3876-46de-adb6-d2f9d5da8641/05-responsive-calendar.png" alt="A responsive calendar fits into the width of a 320px wide screen" width="320" height="533" />

As long as you remember to wrap your embedded calendars and videos with the appropriate containing element, then this CSS will work for any new videos and calendars that you add to your website.

The problem, however, is that although you can fit the whole calendar on a page, it's still <strong>almost unusable because click targets are so small</strong> and no information is visible. If you absolutely have to display Google Calendar, you can, but if you can use more usable responsive calendar solutions like simple CSS (setting <code>display: block</code> on table rows, for example), or <a href="https://w3widgets.com/responsive-calendar/">w3widgets Responsive calendar</a> or <a href="https://tympanus.net/codrops/2012/11/27/calendario-a-flexible-calendar-plugin/">Calendario</a> for your own calendars, your users might appreciate it.</p>

## Responsive Video With CSS or JavaScript

If you’re developing a responsive website using a content management system, then one or more of the website’s editors will probably have to embed video at some point. You can point your editors to <a href="https://embedresponsively.com/">EmbedResponsively.com</a> which <strong>generates responsive &lt;embed&gt; codes</strong> for embedding rich third-party media with one click, with CSS alone. Alternatively, you could use a JavaScript solution, to relieve nervous editors from having to add extra CSS and markup. However, as long as you can avoid this path, the better, of course.

Until recently, most solutions were plugins, which are OK to an extent but can have performance issues. A popular plugin is <a href="https://fitvidsjs.com">FitVids.js</a>, developed by Chris Coyier and Paravel.

A more current solution is to use just a script — such as <a href="https://toddmotto.com/fluid-and-responsive-youtube-and-vimeo-videos-with-fluidvids-js/">FluidVids.js</a>, developed by Todd Motto. FluidVids.js is <a href="https://gomakethings.com/using-fluidvids-js/">simple to use</a>:

1.  [Download the script](https://github.com/toddmotto/fluidvids/archive/master.zip) (ZIP) from GitHub and upload it to your server with the same folder structure that the downloaded files come in. This will place the script itself in a folder named `dist`.
2.  Call the script in each page’s `<head>` section with the following code:

<pre><code class="language-markup">
&lt;script src="dist/fluidvids.js&gt;&lt;/script&gt;
</code></pre>

That’s all you need to do to make videos resize on all devices that support JavaScript. It works not only for YouTube, but for Vimeo, too. The problem, however, is that if you users don't have JavaScript support or the JavaScript hasn't loaded yet or JavaScript hasn't loaded correctly, the only fallback you can use is to add the following to your style sheet:

<pre><code class="language-css">
iframe {
    max-width: 100%; 
}
</code></pre>

This will ensure that video resizes to the width of the browser’s window. But it won’t resize the video’s height; unfortunately, <code>iframe</code> just doesn't work this way. So, the video won’t break your layout, but it won’t look very good either. This is not really a good option, so <strong>if you can avoid using JavaScript for videos, it's a good idea to do so</strong>.</p>

## Responsive Google Maps

Apart from videos and calendars, another common issue is the embedding of Google maps, responsively. Basically, we again use the same intrinsic ratio technique, and when setting <code>padding-bottom</code> for the wrapper, we just divide the height by width and add the aspect ratio in CSS.

Usually, the code generated by Google Maps would look like this:

<pre><code class="language-markup">&lt;iframe src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d3022.260812859955!2d-73.990184!3d40.756288!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0xb134c693ac14a04c!2sThe+TimesCenter!5e0!3m2!1sen!2suk!4v1393485725496" width="500" height="450" frameborder="0" style="border:0"&gt;&lt;/iframe&gt;</code></pre>

We just wrap a <code>div</code> around the <code>iframe</code> and apply the familiar CSS styling to it:

<pre><code class="language-css">
.google-maps {
    position: relative;
    padding-bottom: 90%; // (450 ÷ 500 = 0.9 = 90%)
    height: 0;
    overflow: hidden;
}
.google-maps iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
</code></pre>

And this is what the markup will look like:

<pre><code class="language-markup">
&lt;div class="google-maps"&gt;
&lt;iframe src="https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d7098.94326104394!2d78.0430654485247!3d27.172909818538997!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sen!2s!4v1385710909804" width="500" height="450" frameborder="0" style="border:0"&gt;&lt;/iframe&gt;
&lt;/div&gt;</code></pre>

Voilá! Again, we can just use [EmbedResponsively](https://embedresponsively.com/) to generate the copy-paste-code with one click.

<div class="embed-container"></div>

## Summary

Embedded content has a habit of breaking responsive layouts, because it’s contained in an <code>iframe</code> with a fixed width. In this article, we’ve seen how to add a single containing wrapper, and some CSS, to ensure that all embedded content contained in an <code>iframe</code> resizes with the browser’s window.

Sometimes it's good enough, but sometimes you might need to come up with more advanced solutions, since resizing isn't always a solution. We’ve also looked at <code>embed</code> code generators and alternative solutions, using JavaScript, which might be necessary in some cases, especially if editors have to deal with many videos and don't have technical skills required, or CMS doesn't allow for <a href="https://www.smashingmagazine.com/2015/08/understanding-critical-css/">inline styling</a>.

How do you embed third-party content on your responsive websites? Have you discovered any particular tricks or techniques? What does your workflow for embedding such content look like?

{{< signature "al, vf, il" >}}

<em>Front page image credits: <a href="https://www.flickr.com/photos/juhansonin/8142671926/">Juhan Sonin</a>.</em>

