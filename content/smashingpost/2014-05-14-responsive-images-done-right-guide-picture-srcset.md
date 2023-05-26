---
title: 'Responsive Images Done Right: A Guide To <code>&lt;picture&gt;</code> And <code>srcset</code>'
slug: responsive-images-done-right-guide-picture-srcset
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9d339a-b604-4684-9460-a2f871327c8c/rwd-images-opt-1.png
date: 2014-05-14T11:44:52.000Z
author: ericportis
description: >-
  A few days ago, we published an [article on Picturefill
  2.0](https://www.smashingmagazine.com/2014/05/12/picturefill-2-0-responsive-images-and-the-perfect-polyfill/),
  a perfect polyfill for responsive images. Today’s article complements Tim
  Wright’s article and explains exactly how we can use the upcoming <code>&lt;picture&gt;</code> element and srcset, with simple fallbacks for legacy browsers. There is [no reason to wait for responsive images; we can actually have them very soon
categories:
  - Coding
  - Mobile
  - WebP
  - Responsive Images
---
Images are some of the most important pieces of information on the web, but over the web’s 25-year history, they haven’t been very adaptable at all. Everything about them has been stubbornly fixed: their size, format and crop, all set in stone by a single <code>src</code>.

<blockquote>"Everything I’ve said so far could be summarized as: make pages which are adaptable.… Designing adaptable pages is designing accessible pages. And perhaps the great promise of the web, far from fulfilled as yet, is accessibility, regardless of difficulties, to information."<br /><br />&mdash; John Allsopp, <em><a href="https://alistapart.com/article/dao">A Dao of Web Design</a></em></blockquote>

HTML authors began to really feel these limitations when high-resolution screens and responsive layouts hit the web like a one-two punch. Authors &mdash; wanting their images to look crisp in huge layouts and on high-resolution screens &mdash; began sending larger and larger sources to everyone; the average size of an image file <a href="https://httparchive.org/trends.php?s=All&amp;minlabel=Nov+15+2010&amp;maxlabel=Apr+1+2014#bytesImg&amp;reqImg">ballooned</a>; very smart people called responsive web design "<a href="https://blog.cloudfour.com/css-media-query-for-mobile-is-fools-gold/">unworkably slow</a>".</p>

<strong>Images have been the number one obstacle</strong> to implementing truly adaptable and performant responsive pages &mdash; pages that scale both up and down, efficiently tailoring themselves to both the constraints and the affordances of the browsing context at hand.

That is about to change.

The latest <a href="https://www.smashingmagazine.com/2014/05/12/picturefill-2-0-responsive-images-and-the-perfect-polyfill/">specification of the <code>&lt;picture&gt;</code> element</a> is the result of years of debate on how to make images adapt. It gives authors semantic ways to group multiple versions of the same image, each version having technical characteristics that make it more or less suitable for a particular user. The new specification has achieved broad consensus and is being implemented in Chrome, Opera and Firefox and Edge (<a href="https://caniuse.com/#search=srcset">link</a>) as I type.

The time to start learning this stuff is *now*!

{{% feature-panel %}}

Before we get to any of the (<em>shiny! new!</em>) markup, let’s look at the relevant ways in which browsing environments vary, i.e. the ways in which we want our images to adapt.

1.  Our images need to be able to render crisply at different `device-pixel-ratio`s. We want high-resolution screens to get high-resolution images, but we don’t want to send those images to users who wouldn’t see all of those extra pixels. Let’s call this the `device-pixel-ratio` use case.
2.  If our layout is fluid (i.e. responsive), then our images will need to squish and stretch to fit it. We’ll call this fluid-image use case.
3.  Note that these two use cases are closely related: To solve both, we’ll want our images to be available in multiple resolutions so that they scale efficiently. We’ll call tackling both problems simultaneously the variable-sized-image use case
4.  Sometimes we’ll want to adapt our images in ways that go beyond simple scaling. We might want to crop the images or even subtly alter their content. We’ll call this the art-direction use case.
5.  Finally, different browsers support different image formats. We might want to send a fancy new format such as [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/) to browsers that can render it, and fall back to trusty old JPEGs in browsers that don’t. We’ll call this the type-switching use case.

The new <code>&lt;picture&gt;</code> specification includes features for all of these cases. Let’s look at them one by one.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f318118-0105-4c76-9e6a-3390cdb3d8dd/viewport-selection-opt.jpg" alt="responsive images with srcset " width="500" height="245" /><figcaption>Rearranging images across various resolutions is relatively easy, however, loading different images (and only them) depending on the user’s resolution is quite difficult. Well, not any more. (<a href="https://picture.responsiveimages.org/images/viewport_selection_mob_first.jpg">Image credit</a>)</figcaption></figure>

## The `device-pixel-ratio` Use Case

Let’s start simply, with a fixed-width image that we want to adapt to varying <code>device-pixel-ratio</code>s. To do this, we’ll use the first tool that the new specification gives us for grouping and describing image sources: the <code>srcset</code> attribute.

Say we have two versions of an image:

*   `small.jpg` (320 × 240 pixels)
*   `large.jpg` (640 × 480 pixels)

We want to send <code>large.jpg</code> only to users with high-resolution screens. Using <code>srcset</code>, we’d mark up our image like so:

<pre><code class="language-markup">&lt;img srcset="small.jpg 1x, large.jpg 2x"
   src="small.jpg"
   alt="A rad wolf" /&gt;
</code></pre>

The <code>srcset</code> attribute takes a comma-separated list of image URLs, each with an <code>x</code> descriptor stating the <code>device-pixel-ratio</code> that that file is intended for.

The <code>src</code> is there for browsers that don’t understand <code>srcset</code>. The <code>alt</code>, of course, is included for browsers that don’t render images at all. One element and three attributes gets us an image that looks crisp on high-resolution devices and efficiently degrades all the way down to text. Not too shabby!

## The Fluid- And Variable-Sized-Image Use Cases

What that markup won’t do is efficiently squish and stretch our image in a fluid layout. Before addressing this fluid-image use case, we need a little background on how browsers work.

Image preloading is, according to Steve Souders, “<a href="https://www.stevesouders.com/blog/2013/04/26/i/">the single biggest performance improvement browsers have ever made</a>.” Images are often the heaviest elements on a page; loading them ASAP is in everyone’s best interest. Thus, the first thing a browser will do with a page is scan the HTML for image URLs and begin loading them. The browser does this long before it has constructed a DOM, loaded external CSS or painted a layout. Solving the fluid-image use case is tricky, then; we need the browser to pick a source before it knows the image’s rendered size.</p>

<strong>What a browser does know at all times is the environment it’s rendering in</strong>: the size of the viewport, the resolution of the user’s screen, that sort of thing. We use this information when we use media queries, which tailor our layouts to fit particular browsing environments.

Thus, to get around the preloading problem, the first <a href="https://lists.whatwg.org/htdig.cgi/whatwg-whatwg.org/2012-May/035855.html">proposals</a> for fluid-image <a href="https://alistapart.com/article/responsive-images-how-they-almost-worked-and-what-we-need">features</a> suggested attaching media queries to sources. We would base our source-picking mechanism on the size of the viewport, which the browser knows at picking-time, not on the final rendered size of the image, which it doesn’t.</p>

<figure><a href="https://ericportis.com/posts/2014/srcset-sizes/"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06c96887-9e01-4289-ab81-cdd4ea38183c/measuring-image-size.png" alt="" width="500" height="340" /></a><figcaption>Dealing with responsive images turned out to be quite a nightmare. A better way to provide the browser with details about its environment is by simply telling the browser the rendered size of the image. Kind of obvious, really. (<a href="https://ericportis.com/posts/2014/srcset-sizes/">Image credit</a>)</figcaption></figure>

As it <a href="https://ericportis.com/posts/2014/srcset-sizes/">turns out</a>, that’s a bad idea. While it’s technically workable, calculating the media queries needed is tedious and error-prone. A better idea is to <strong>simply tell the browser the rendered size of the image</strong>!

Once we tell the browser how many pixels it <em>needs</em> (via a new attribute, <code>sizes</code>) and how many pixels each of the sources <em>has</em> (via <code>w</code> descriptors in <code>srcset</code>), picking a source becomes trivial. The browser picks the smallest source that will still look reasonably crisp within its container.

Let’s make this concrete by developing our previous example. Suppose we now have three versions of our image:

*   `large.jpg` (1024 × 768 pixels)
*   `medium.jpg` (640 × 480 pixels)
*   `small.jpg` (320 × 240 pixels)

And we want to place these in a flexible grid &mdash; a grid that starts out as a single column but switches to three columns in larger viewports, <a href="https://ericportis.com/etc/smashing-mag-picture-examples/variable-size.html">like this</a>:

<figure><a href="https://ericportis.com/etc/smashing-mag-picture-examples/variable-size.html"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3d8bc28-d761-4ed9-aab6-aaa0ce57e5d8/wolves-picture-examples-opt.png" alt="" width="500" height="310" /></a><figcaption>A responsive grid example. (<a href="https://ericportis.com/etc/smashing-mag-picture-examples/variable-size.html">See the demo</a>)</figcaption></figure>

Here’s how we’d mark it up:

<pre><code class="language-markup">&lt;img srcset="large.jpg  1024w,
      medium.jpg 640w,
      small.jpg  320w"
   sizes="(min-width: 36em) 33.3vw,
      100vw"
   src="small.jpg"
   alt="A rad wolf" /&gt;
</code></pre>

We’re using <code>srcset</code> again, but instead of <code>x</code> descriptors, we’re attaching <code>w</code> descriptors to our sources. These describe the actual width, in pixels, of the referenced file. So, if you “Save for Web…” at 1024 × 768 pixels, then mark up that source in <code>srcset</code> as <code>1024w</code>.

You’ll note that <strong>we’re specifying only image widths</strong>. Why not heights, too? The images in our layout are width-constrained; their widths are set explicitly by the CSS, but their heights are not. The vast majority of responsive images in the wild are width-constrained, too, so the specification keeps things simple by dealing only in widths. There are some <a href="https://github.com/ResponsiveImagesCG/picture-element/issues/85">good</a> <a href="https://github.com/ResponsiveImagesCG/picture-element/issues/86">reasons</a> for including heights, too &mdash; but not yet.

So, that’s <code>w</code> in <code>srcset</code>, which describes how many pixels each of our sources <em>has</em>. Next up, the <code>sizes</code> attribute. The <code>sizes</code> attribute tells the browser how many pixels it <em>needs</em> by describing the final rendered width of our image. Think of <code>sizes</code> as a way to give the browser a bit of information about the page’s layout a little ahead of time, so that it can pick a source before it has parsed or rendered any of the page’s CSS.

We do this by passing the browser a <a href="https://www.w3.org/TR/css3-values/#lengths">CSS length</a> that describes the image’s rendered width. CSS lengths can be either absolute (for example, <code>99px</code> or <code>16em</code>) or <a href="https://www.w3.org/TR/css3-values/#viewport-relative-lengths">relative to the viewport</a> (<code>33.3vw</code>, as in our example). That “relative to the viewport” part is what enables images to flex.

If our image occupies a third of the viewport, then our <code>sizes</code> attribute should look like this:

<pre><code class="language-css">sizes="33.3vw"
</code></pre>

Our example isn’t quite so simple. Our layout has a breakpoint at 36 ems. When the viewport is narrower than 36 ems, the layout changes. Below that breakpoint, the image will fill 100% of the viewport’s width. How do we encode that information in our <code>sizes</code> attribute?

We do it by pairing media queries with lengths:

<pre><code class="language-css">sizes="(min-width: 36em) 33.3vw,
   100vw"
</code></pre>

This is its format:

<pre><code class="language-css">sizes="[media query] [length],
   [media query] [length],
   etc…
   [default length]"
</code></pre>

The browser goes over each media query until it finds one that matches and then uses the matching query’s paired length. If no media queries match, then the browser uses the “default” length, i.e. any length it comes across that doesn’t have a paired query.

With both a <code>sizes</code> length and a set of sources with <code>w</code> descriptors in <code>srcset</code> to choose from, the browser has everything it needs to efficiently load an image in a fluid, responsive layout.

Wonderfully, <code>sizes</code> and <code>w</code> in <code>srcset</code> also give the browser enough information to adapt the image to varying <code>device-pixel-ratio</code>s. Converting the CSS length, we give it in <code>sizes</code> to CSS pixels; and, multiplying that by the user’s <code>device-pixel-ratio</code>, the browser knows the number of device pixels it needs to fill &mdash; no matter what the user’s <code>device-pixel-ratio</code> is.

So, while the example in our <code>device-pixel-ratio</code> use case works only for fixed-width images and covers only 1x and 2x screens, this <code>srcset</code> and <code>sizes</code> example not only covers the fluid-image use case, but also adapts to arbitrary screen densities.

We’ve solved both problems at once. In the parlance set out at the beginning of this article, <code>w</code> in <code>srcset</code> and <code>sizes</code> covers the variable-sized-image use case.

Even more wonderfully, <strong>this markup also gives the browser some wiggle room</strong>. Attaching specific browsing conditions to sources means that the browser does its picking based on a strict set of conditions. “If the screen is high-resolution,” we say to the browser, “then you must use this source.” By simply describing the resources’ dimensions with <code>w</code> in <code>srcset</code> and the area they’ll be occupying with <code>sizes</code>, we enable the browser to apply its wealth of additional knowledge about a given user’s environment to the source-picking problem. The specification allows browsers to, say, optionally load smaller sources when bandwidth is slow or expensive.

One more thing. In our example, the size of the image is always a simple percentage of the viewport’s width. What if our layout combined both absolute and relative lengths by, say, adding a fixed 12-em sidebar to the three-column layout, <a href="https://ericportis.com/etc/smashing-mag-picture-examples/absolute-and-fixed.html">like this</a>?

<figure><a href="https://ericportis.com/etc/smashing-mag-picture-examples/absolute-and-fixed.html"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f86f5d84-b0b4-4a96-8d43-6c24381aa7f4/absolute-relative-lengths-opt.png" alt="" width="500" height="271" /></a><figcaption>A layout combines absolute and relative lengths. (<a href="https://ericportis.com/etc/smashing-mag-picture-examples/absolute-and-fixed.html">See the demo</a>)</figcaption></figure>

We’d use the <a href="https://caniuse.com/calc">surprisingly well-supported</a> <a href="https://dev.w3.org/csswg/css-values/#calc-notation"><code>calc()</code> function</a> in our <code>sizes</code> attribute.</p>

<pre><code class="language-markup">sizes="(min-width: 36em) calc(.333 * (100vw - 12em)),
   100vw"
</code></pre>

And... done!

{{% ad-panel-leaderboard %}}

## The Art-Direction Use Case

Now we’re cooking with gas! We’ve learned how to mark up varible-sized images that scale up and down efficiently, rendering crisply on any and all layouts, viewports and screens.

But what if we wanted to go further? What if we wanted to adapt more?

When Apple introduced the iPad Air last year, its website featured a <a href="https://ericportis.com/etc/ipad-air-art-direction/ipadair_hero_a.jpg">huge image of the device</a>. This might sound rather unremarkable, unless you &mdash; as web design geeks are wont to do &mdash; compulsively resized your browser window. When the viewport was short enough, the iPad did a remarkable thing: it <a href="https://ericportis.com/etc/ipad-air-art-direction/ipadair_hero_b.jpg">rotated to better fit the viewport</a>!

We call this sort of thing “art direction.”

Apple art-directed its image by abusing HTML and CSS: marking up its image &mdash; which was clearly content &mdash; as an empty <code>div</code> and switching its <code>background-image</code> with CSS. The new <code>&lt;picture&gt;</code> specification allows authors to do this sort of breakpoint-based art direction entirely in HTML.

The specification facilitates this by layering another method of source grouping on top of <code>srcset</code>: <code>&lt;picture&gt;</code> and <code>source</code>.

Let’s get back to our example. Suppose that instead of letting our image fill the full width of the viewport on small screens, we crop the image square, zooming in on the most important part of the subject, and present that small square crop at a fixed size floated off to the left, leaving a lot of space for descriptive text, <a href="https://ericportis.com/etc/smashing-mag-picture-examples/art-direction.html">like this</a>:

<figure><a href="https://ericportis.com/etc/smashing-mag-picture-examples/art-direction.html"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50f3bd30-9d93-4cdc-a27f-74dd820ea712/wolves-descriptive-text-opt.jpg" alt="" width="500" height="392" /></a><figcaption>An example with images combined with descriptive text. (<a href="https://ericportis.com/etc/smashing-mag-picture-examples/art-direction.html">See the demo</a>)</figcaption></figure>

To achieve this, we’ll need a couple of additional image sources:

*   `cropped-small.jpg` (96 × 96 pixels)
*   `cropped-large.jpg` (192 × 192 pixels)
*   `small.jpg` (320 × 240 pixels)
*   `medium.jpg` (640 × 480 pixels)
*   `large.jpg` (1024 × 768 pixels)

How do we mark them up? Like so:

<pre><code class="language-markup">&lt;picture&gt;
   &lt;source media="(min-width: 36em)"
      srcset="large.jpg  1024w,
         medium.jpg 640w,
         small.jpg  320w"
      sizes="33.3vw" /&gt;
   &lt;source srcset="cropped-large.jpg 2x,
         cropped-small.jpg 1x" /&gt;
   &lt;img src="small.jpg" alt="A rad wolf" /&gt;
&lt;/picture&gt;
</code></pre>

This example is as complex as it gets, using every feature that we’ve covered so far. Let’s break it down.

The <code>&lt;picture&gt;</code> element contains two <code>source</code>s and an <code>img</code>. The <code>source</code>s represent the two separate art-directed versions of the image (the square crop and the full crop). The (required) <code>img</code> serves as our fallback. As we’ll soon discover, it does much of the actual work behind the scenes.

First, let’s take a close look at that first <code>source</code>:

<pre><code class="language-markup">&lt;source media="(min-width: 36em)"
   srcset="large.jpg  1024w,
      medium.jpg 640w,
      small.jpg  320w"
   sizes="33.3vw" /&gt;
</code></pre>

This <code>source</code> represents the full uncropped version of our image. We want to show the full image only in the three-column layout &mdash; that is, when the viewport is wider than 36 ems. The first attribute here, <code>media="(min-width: 36em)"</code>, makes that happen. If a query in a <code>media</code> attribute evaluates to <code>true</code>, then the browser must use that <code>source</code>; otherwise, it’s skipped.

The <code>source</code>’s other two attributes &mdash; <code>srcset</code> and <code>sizes</code> &mdash; are mostly copied from our previous variable-sized-image example. One difference: Because this <code>source</code> will be chosen only for the three-column layout, our <code>sizes</code> attribute only needs a single length, <code>33.3vw</code>.

When the viewport is narrower than 36 ems, the first <code>source</code>’s media query will evaluate to <code>false</code>, and we’d proceed to the second:

<pre><code class="language-markup">&lt;source srcset="square-large.jpg 2x,
                square-small.jpg 1x" /&gt;
</code></pre>

This represents our small square crop. This version is displayed at a fixed width, but we still want it to render crisply on high-resolution screens. Thus, we’ve supplied both 1x and 2x versions and marked them up with simple <code>x</code> descriptors.

Lastly, we come to the surprisingly important (<em>indeed, required!</em>) <code>img</code>.

Any child of an <code>audio</code> or <code>video</code> element that isn’t a <code>source</code> is treated as fallback content and hidden in supporting browsers. You might, therefore, assume the same thing about the <code>img</code> here. Wrong! Users actually see the <code>img</code> element when we use <code>&lt;picture&gt;</code>. Without <code>img</code>, there’s no image; <code>&lt;picture&gt;</code> and all of its <code>source</code>s are just there to feed it a source.

Why? One of the main complaints about the first <code>&lt;picture&gt;</code> specification was that it reinvented the wheel, propsing an entirely new HTML media element, along the lines of <code>audio</code> and <code>video</code>, that mostly duplicated the functionality of <code>img</code>. Duplicated functionality means duplicated implementation and maintenance work &mdash; work that browser vendors weren’t keen to undertake.

Thus, the new specification’s reuse of <code>img</code>. The <code>&lt;picture&gt;</code> itself is invisible, a bit like a magical <code>span</code>. Its <code>source</code>s are just there for the browser to draw alternate versions of the image from. Once a source URL is chosen, that URL is fed to the <code>img</code>. Practically speaking, this means that any styles that you want to apply to your rendered image (like, say, <code>max-width: 100%</code>) need to be applied to <code>img</code>, not to <code>&lt;picture&gt;</code>.

OK, on to our last feature.</p>

{{% ad-panel-leaderboard %}}

## The Type-Switching Use Case

Let’s say that, instead of doing all of this squishing, stretching and adapting to myriad viewport conditions, we simply want to give a new file format a spin and provide a fallback for non-supporting browsers. For this, we follow the pattern established by <code>audio</code> and <code>video</code>: <code>source type</code>.</p>

<pre><code class="language-markup">&lt;picture&gt;
   &lt;source type="image/svg" src="logo.svg" /&gt;
   &lt;source type="image/png" src="logo.png" /&gt;
   &lt;img src="logo.gif" alt="RadWolf, Inc." /&gt;
&lt;/picture&gt;
</code></pre>

If the browser doesn’t understand the <code>image/svg</code> <a href="https://en.wikipedia.org/wiki/Internet_media_type">media type</a>, then it skips the first <code>source</code>; if it can’t make heads or tails of <code>image/png</code>, then it falls back to <code>img</code> and the GIF.

During the <a href="https://alistapart.com/article/pngopacity">extremely painful GIF-to-PNG transition</a> period, web designers would have killed for such a feature. The <code>&lt;picture&gt;</code> element gives it to us, setting the stage for new image formats to be easily adopted in the years to come.</p>

## That’s It!

That’s everything: every feature in the new <code>&lt;picture&gt;</code> specification and the rationale behind each. All in all, <code>srcset</code>, <code>x</code>, <code>w</code>, <code>sizes</code>, <code>&lt;picture&gt;</code>, <code>source</code>, <code>media</code> and <code>type</code> give us a rich set of tools with which to make images truly adaptable &mdash; images that can (<em>finally!</em>) flow efficiently in flexible layouts and a wide range of devices.</p>

<strong>The specification is not yet final</strong>. The first implementations are in progress and are being staged behind experimental flags; its implementors and authors are working together to hash out the specification’s finer details on a daily basis. All of this is happening under the umbrella of the <a href="https://responsiveimages.org">Responsive Images Community Group</a>. If you’re interested in following along, <a href="https://www.w3.org/community/respimg/">join</a> the group, drop in on the <a href="https://irc.lc/w3c/respimg/newb">IRC channel</a>, weigh in on a <a href="https://github.com/ResponsiveImagesCG/picture-element/issues">GitHub issue</a> or file a new one, sign up for the <a href="https://responsiveimages.org">newsletter</a>, or follow the RICG <a href="https://www.twitter.com/respimg">on Twitter</a>.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Choosing A Responsive Image Solution](https://www.smashingmagazine.com/2013/07/choosing-a-responsive-image-solution/)
*   [One Solution To Responsive Images](https://www.smashingmagazine.com/2014/02/one-solution-to-responsive-images/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)
*   [53 CSS-Techniques You Couldn’t Live Without](https://www.smashingmagazine.com/2007/01/53-css-techniques-you-couldnt-live-without/)

{{< signature "il, al" >}}
