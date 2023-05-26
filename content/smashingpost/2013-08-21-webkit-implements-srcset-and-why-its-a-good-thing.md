---
title: 'WebKit Has Implemented srcset, And It’s A Good Thing'
slug: webkit-implements-srcset-and-why-its-a-good-thing
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7462d192-80f0-4a6f-8e32-5eede446c598/illu-webkit.jpg'
date: 2013-08-21T19:29:39.000Z
author: mat-marquis
summary: >-
  While <code>srcset</code> as implemented by WebKit doesn’t address to all the responsive images use cases, it does represent a major step toward a long overdue solution—hopefully the first of many.
description: >-
  While <code>srcset</code> as implemented by WebKit doesn’t address to all the responsive images use cases, it does represent a major step toward a long overdue solution—hopefully the first of many.
categories:
  - Mobile
  - Opinion Column
  - Responsive Design
---
WebKit has made some serious news by finally [implementing the `srcset` attribute. As Chair of the W3C’s Responsive Images Community Group, I’ve been alternately hoping for and dreading this moment for some time now.

As with all matters pertaining to “responsive images”: it’s complicated, and it can be hard keeping up with the signal in all the noise. Here’s what you need to know.

## What Does It Do?

As originally proposed, the `srcset` attribute allowed developers to specify a list of sources for an image attribute, to be delivered based on the pixel density of the user’s display:

<pre><code class="language-markup">&lt;img src="low-res.jpg" srcset="high-res.jpg 2x"&gt;</code></pre>

Not too scary, this markup. In plain English:

<blockquote>“Use <em>low-res.jpg</em> as the source for this <code>img</code> on low-resolution displays, and for any browser that doesn’t understand the <code>srcset</code> attribute. Use <em>high-res.jpg</em> as the source for this <code>img</code> on high-resolution displays in browsers that understand the <code>srcset</code> attribute.”</blockquote>

<p>Things were starting to look scary, for a little while there. Due in part to high resolution devices, the average website is now nearly an <a href="https://httparchive.org/interesting.php?a=All&amp;l=Aug%2015%202013">entire megabyte of images</a>. Now developers can target users on high-resolution displays with a high-resolution image source. Meanwhile, users on lower pixel density displays won’t be saddled with the bandwidth cost of downloading a massive high-resolution image, without seeing any benefit.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/">Responsive Images Done Right: A Guide To &lt;picture&gt; And &lt;srcset&gt;</a></em></p>

{{% feature-panel %}}

## Can’t We Do That With JavaScript?

<p>On the surface, <code>srcset</code> isn’t doing anything special &mdash; it chooses an appropriate source from an attribute and swaps the contents of an <code>img</code> tag’s <code>src</code>. Swapping the contents of an attribute is something we’ve been doing with JavaScript since time immemorial. Well, since the 90s, anyway. So, what does this gain us?</p>

<p>We actually attempted this approach on <a href="https://bostonglobe.com">BostonGlobe.com</a>, one of the earlier sites to make use of any sort of “responsive images” solution. Thanks to increasingly aggressive prefetching in several of the major browsers, an image’s <code>src</code> is requested long before we have a chance to apply any custom scripting: we would end up making two requests for every one image we displayed, defeating the entire purpose. I’ve <a href="https://alistapart.com/article/responsive-images-how-they-almost-worked-and-what-we-need">documented some of those efforts elsewhere</a>, so I’ll spare you the gory details here.</p>

## Can’t We Do That With CSS?

<p>"Yes" and "No." We can do this with background images easily enough, using a combination of media queries concerned with pixel density. <code>srcset</code> as implemented by WebKit is very similar to the recent <code>image-set</code> feature they introduced to CSS. <code>image-set</code> allows you to specify a list of background image sources and resolutions and allow the browser to make the decision as to which one is most appropriate &mdash; pretty familiar stuff. We didn’t have anything along these lines for non-presentational <em>content</em> images, however, until now.</p>

<p>Using CSS to manage content images is broken by default, in terms of keeping our concerns separate. It’s an approach that may make perfect sense within the scope of a quick demo page, but stands to quickly spiral out of control in a production website.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/">Responsive Images In WordPress With Art Direction</a></em></p>

<p>Having our CMS generate scores of stylesheets full of background images would be no picnic, from a developer standpoint. Worse, however, is that it would lead to requests for stylesheets and images that users may not need unless done very, very carefully. Beyond that, it renders our images &mdash; no pun intended &mdash; inaccessible to users browsing by way of assistive technologies.</p>

<p>The closest thing we’ve found to a CSS-based approach would swap an image’s sources based on values set in HTMLs data attributes, using <a href="https://nicolasgallagher.com/responsive-images-using-css3">some proposed CSS trickery</a>, much of which is only theoretical and may never happen. However, it still didn’t account for the the double download of high and low resolution image assets &mdash; the same issue we encountered with JavaScript. Even if a technique like Nicolas’ should become available to us, we’ll still face the same problems as many script-based solutions: attempting to work around a wasteful, redundant request.</p>

{{% ad-panel-leaderboard %}}

## What Does It Do About Bandwidth?

<p>Regardless of screen density, there are a number of situations where lower resolution images sources may be preferable: a Retina MacBook Pro tethered to a 3G, for example, or an unstable conference WiFi network &mdash; both situations we’ve all been in plenty of times.</p>

<p>Beyond simply providing us with a sort of inline shorthand for resolution media queries, <code>srcset</code> accounts for bandwidth as well, in a sense. It’s buried in arcane spec-speak, but one of the really exciting facets of <code>srcset</code> is that it’s defined as a set of <em>suggestions</em> to the browser. The browser can then use environmental heuristics or a user preference to decide that it wants to fetch a lower resolution image despite a high-resolution display: envision a preference in your mobile browser allowing high-res images to only be requested while connected to WiFi, or a manual browser preference allowing you to only request low-resolution images when your connection is shaky.</p>

{{< rimg breakout="true" href="https://usecases.responsiveimages.org" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b430c0dc-96de-4c92-9166-ab402b175bc6/devices-responsive-images-use-case.png" sizes="100vw" caption="Ideally, we'd love to send only those images to devices which are specifically resized for each screen resolution. The intention is to save bandwidth and allow the images to download faster on the targeted screen. A <a href='https://usecases.responsiveimages.org'>common use case for responsive images</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b430c0dc-96de-4c92-9166-ab402b175bc6/devices-responsive-images-use-case.png'>Large preview</a>)" alt="Responsive Images" >}}

<p>This isn’t a part of WebKit’s early <code>srcset</code> implementation, but it does pave the way for their addition without requiring any changes to our markup. We, developers, can safely use <code>srcset</code> today, and these optimizations may come “for free” in the future.</p>

## What Does This Mean For The `picture` Element?

<p>Here’s where things get interesting.</p>

<p>The version of <code>srcset</code> implemented by WebKit matches the original proposed use of <code>srcset</code>, and the version that the <a href="https://responsiveimages.org">Responsive Images Community Group</a> has been working towards. We can think of this incarnation of <code>srcset</code> as shorthand for the whole slew of media queries concerned with resolution, with one key difference where the browser can choose to override the applicable source based on user preference.</p>

<p>While this implementation matches the original <code>srcset</code> proposal, the current <code>srcset</code> spec attempts to expand the syntax to cover some of the <a href="https://usecases.responsiveimages.org">use cases</a> that the <code>picture</code> element fulfills, using a microsyntax that performs some &mdash; but nowhere near all &mdash; of the functions of media queries.</p>

<pre><code class="language-markup">&lt;img src="fallback.jpg" srcset="small.jpg 640w 1x, small-hd.jpg 640w 2x, large.jpg 1x, large-hd.jpg 2x" alt="..."&gt;</code></pre>

<p>In our opinion not ideal, this markup pattern. We’re restricted to the equivalent of <code>max-width</code> media queries, pixels, and an inscrutable microsyntax, all for the sake of duplicating the function of media queries. Fortunately for us, neither Web developers nor browser reps are particularly fond of this overextended syntax &mdash; hopefully, it will never see the light of day.<p>

{{% ad-panel-leaderboard %}}

<p>The <code>picture</code> element exists to address these use cases using a more flexible &mdash; and familiar &mdash; syntax. <code>picture</code> uses <code>media</code> attributes on <code>source</code> elements, similar to the <code>video</code> element. This allows us to target image sources to a combination of factors: viewport height and/or width, in pixels or <code>em</code>s, using either <code>min</code> or <code>max</code> values &mdash; just like media queries in our CSS.</p>

<pre><code class="language-markup">&lt;picture&gt;
    &lt;source src="med.jpg" media="(min-width: 40em)" /&gt;
    &lt;source src="sm.jpg" /&gt;
    &lt;img src="fallback.jpg" alt="" /&gt;
&lt;/picture&gt;
</code></pre>

<p>The <code>picture</code> specification was written with this reduced <code>srcset</code> syntax in mind, so it could be used on <code>picture</code>’s <code>source</code> elements as well as <code>img</code> elements.</p>

<pre><code class="language-markup">&lt;picture&gt;
    &lt;source srcset="med.jpg 1x, med-hd.jpg 2x" media="(min-width: 40em)" /&gt; 
    &lt;source srcset="sm.jpg 1x, sm-hd.jpg 2x" /&gt; 
    &lt;img src="fallback.jpg" alt="" /&gt;
&lt;/picture&gt;</code></pre>

<p>In concert, the two markup patterns give us an incredible amount of flexibility over what image sources we serve to users, depending on their context.</p>

## So This _Is_ Good News

<p>Absolutely, it is. While <code>srcset</code> as implemented by WebKit doesn’t address to all the <a href="https://usecases.responsiveimages.org">responsive images use cases</a>, it does represent a major step toward a long overdue solution &mdash; hopefully the first of many.</p>

<p>Let’s hope that other browsers follow WebKit’s lead in implementing this feature as it was originally proposed, and stay tuned to the <a href="https://responsiveimages.org">Responsive Images Community Group’s homepage</a> and <a href="https://twitter.com/respimg">Twitter account</a> to keep tabs on the subject.</p>

<p>I also wrote about the issues with responsive images and the solutions we’ve come up with when working on the BostonGlobe website in the chapter “The Struggles and Solutions In Responsive Web Design” of the <a href="https://shop.smashingmagazine.com/smashing-book-4.html">upcoming Smashing Book 4</a>. Grab it, you won’t be disappointed.</p>

{{< signature "vf, il" >}}