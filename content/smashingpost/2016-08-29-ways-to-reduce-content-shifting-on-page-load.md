---
title: Ways To Reduce Content Shifting On Page Load
slug: ways-to-reduce-content-shifting-on-page-load
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b31e82d4-83a4-45e3-8083-6b9de5f4bb7f/black-and-white-cup-hand-mug-opt.jpg
date: 2016-08-29T18:25:24.000Z
author: michaelscharnagl
description: >-
  Have you ever opened a website, started reading and, after some time had
  passed and all assets had finished loading, you found that you’ve **lost your
  scroll position**? I undergo this every day, especially when surfing on my
  mobile device on a slow connection — a frustrating and distracting experience.

  Every time the browser has to recalculate the positions and geometries of
  elements in the document, a reflow happens. This happens when new DOM elements
  are added to the page, images load or dimensions of elements change. In this
  article, we will share techniques to minimize this content shifting.
categories:
  - Coding
  - Performance
  - Usability
---
Have you ever opened a website, started reading and, after some time had passed and all assets had finished loading, you found that you’ve **lost your scroll position**? I undergo this every day, especially when surfing on my mobile device on a slow connection — a frustrating and distracting experience.

Every time the browser has to recalculate the positions and geometries of elements in the document, a reflow happens. This happens when new DOM elements are added to the page, images load or dimensions of elements change. In this article, we will share techniques to minimize this content shifting.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
*   [How To Create An Embeddable Content Plugin For WordPress](https://www.smashingmagazine.com/2012/11/embeddable-content-wordpress/)
*   [Content Security Policy, Your Future Best Friend](https://www.smashingmagazine.com/2016/09/content-security-policy-your-future-best-friend/)

## Media

When a website loads, it takes some time until the images are loaded and the browser is able to calculate the space needed. The following GIF, recorded with the throttling set to 3G, demonstrates the effect.

{{% feature-panel %}}

<figure><div class="aspect-ratio">{{< vimeo 177674571 >}}</div></figure>

One way to avoid this is to set a fixed width and height for all images, but this isn’t practical for responsive websites because we want images and videos to adapt to the available space.</p>

### Intrinsic Ratio

With [intrinsic ratios](https://alistapart.com/article/creating-intrinsic-ratios-for-video), also referred to as the `padding-bottom` hack, we can define the sizes that our media will occupy.</p>

<figure><a href="https://res.cloudinary.com/indysigner/image/upload/v1544089339/padding-bottom-formula_bmltxr.svg"><img loading="lazy" decoding="async" src="https://res.cloudinary.com/indysigner/image/upload/v1544089339/padding-bottom-formula_bmltxr.svg" width="" height="" alt="" /></a><figcaption>Formula for intrinsic ratio</figcaption></figure>

The formula for getting the value for `padding-bottom` is this:

<pre><code class="language-css">
(height of the asset / width of the asset) * 100(%)
</code></pre>

If we have an image with a width of 1600 pixels and a height of 900 pixels, then the value would be this:

<pre><code class="language-css">
 (900 / 1600) * 100(%) = 56.25%
 </code></pre>

Here is a Sass mixin we can use to define the aspect ratios of our images, videos, iframes, objects and embedded content.</p>

<pre><code class="language-css">
@mixin aspect-ratio($width, $height) {
  position: relative;
  padding-bottom: ($height / $width) * 100%;
  img,
  video,
  iframe,
  object,
  embed {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
}
</code></pre>

<pre><code class="language-css">
.ratio-sixteen-nine {
  @include aspect-ratio(1600, 900);
}
</code></pre>

<pre><code class="language-markup">
&lt;figure class=&quot;ratio-sixteen-nine&quot;&gt;
  &lt;img src=&quot;waterfall.jpg&quot; alt=&quot;Waterfall in Iceland&quot;&gt;
&lt;/figure&gt;
</code></pre>

To make the experience even better, we can style the placeholder by adding a background to the wrapper.</p>

<pre><code class="language-css">
figure {
  background: #ddd url(camera-icon.svg) no-repeat center center;
}
</code></pre>

For images, we can use an icon to indicate to users that an image will appear. By implementing aspect-ratio placeholders, the user can decide whether to wait for the image or continue reading, all without losing their current scroll position.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/160ae39d-b5b0-4d9f-a8e1-76102113e2f8/placeholder-picture-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90fc8e39-3a16-4993-ac38-93677e66e556/placeholder-picture-500px-opt.png" width="500" height="281" alt="Placeholder picture" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/160ae39d-b5b0-4d9f-a8e1-76102113e2f8/placeholder-picture-large-opt.png">View large version</a>)</figcaption></figure>

## Widgets

In addition to media content, your website might be using widgets or third-party content that is added via JavaScript and that would also shift content if not handled carefully.</p>

### Advertisements

Although a lot of websites are responsive these days, most ads still have a fixed size. For a responsive website, we can use placeholders in our HTML, in which we load the predefined ads if they match the specified screen size.</p>

<pre><code class="language-css">
/* On small screens show 320x250 banner */
@media all and (max-width: 500px) {
  .ad-container-s {
    width: 320px;
    height: 250px;
  }
}

/* On medium screens show 728x90 banner */
@media all and (min-width: 800px) {
 .ad-container-m {
   width: 728px;
   height: 90px;
 }
}
</code></pre>

In our example, we have one medium rectangle (300 × 250) and one leaderboard (728 × 90). On small screens, we would show the rectangle, while on bigger screens we would show the leaderboard. By setting fixed dimensions for the placeholder, the loading of the ads won’t trigger a content shift.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cb4dc3f-d577-4bcc-8131-915627a4a884/advertisement-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f56a52f-9d5b-4b1a-9c20-cb2710faf932/small-and-big-screens-500px-opt.png" width="500" height="221" alt="Advertisement" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cb4dc3f-d577-4bcc-8131-915627a4a884/advertisement-large-opt.png">View large version</a>)</figcaption></figure>

Many people will never see the ads, but only the empty placeholder, because they will be using an ad blocker, or the advertisement won’t show up for other reasons. Therefore, you should style the placeholder to indicate that there is normally an ad. If you are already using an ad-blocker detection script, you can replace the placeholder with a message or a [promotion of your products](https://www.smashingmagazine.com/2016/03/never-ending-story-ad-blockers/#prominently-highlight-your-products).

Users might even rethink the use of an ad blocker on your website if the ads have one less disadvantage — that distracting jump effect.</p>

### Dynamic Content

For other widgets, we might not know their exact sizes beforehand, but we can define the minimum heights the widgets will require.</p>

<pre><code class="language-css">
.widget {
  min-height: 400px;
}
</code></pre>

By using `min-height`, we will reserve enough space for most cases and avoid a big jump if the widget needs more space.

Finding the right size for `min-height` takes some time, but users will be thankful that their reading experience has not been abruptly interrupted.</p>

## Web Fonts

Fonts have different x-heights. Therefore, our fallback font and web font will take up a different amount of space.

Currently, one [best practice](https://www.zachleat.com/web/comprehensive-webfonts/) for loading web fonts is to use the [Font Face Observer](https://github.com/bramstein/fontfaceobserver) script to detect when a font has loaded so that it can be applied in the CSS afterwards.

In this example, we are applying the `webfont-loaded` class to the `html` element once the web font is ready to use.</p>

<pre><code class="language-js">
var font = new FontFaceObserver('Lato');

font.load().then(function () {
  document.documentElement.className += " webfont-loaded";
});
</code></pre>

In the CSS, we apply the web font once it has successfully loaded.</p>

<pre><code class="language-css">
p {font-family: sans-serif;}

.webfont-loaded p {font-family: 'Lato', sans-serif;}
</code></pre>

When the web font finally finishes loading, we will notice a quick jump. To minimize this, we can modify the x-height of the fallback font to match the web font as closely as possible, thus reducing the jump.</p>

<figure><div class="aspect-ratio">{{< vimeo 177676148 >}}</div></figure>

### font-size-adjust

The [`font-size-adjust` property](https://www.w3.org/TR/css-fonts-3/#font-size-adjust-prop) allows you to specify the optimal aspect ratio for when a fallback font is used. For most fonts, the ratio is between 0.3 and 0.7.

To find the right aspect ratio for your web font, I recommend setting up your browser to show two paragraphs side by side, one with the web font and the other with the fallback font, and then adjust the property with your browser’s developer tools.</p>

<pre><code class="language-css">
p {
  font-size-adjust: 0.5;
}
</code></pre>

Because `font-size-adjust` is currently [supported only](https://caniuse.com/#feat=font-size-adjust) in Firefox and Chrome (behind a flag), we can use a combination of `letter-spacing` and `line-height` to adjust the size of the fallback font in other browsers.</p>

<pre><code class="language-css">
p {
  font-family: sans-serif;
  font-size: 18px;
  letter-spacing: 1px;
  line-height: 0.95;
}

/* Older browsers */
p {
  letter-spacing: 1px;
  line-height: 0.95;
}

/* If browser supports font-size-adjust, use this */
@supports (font-size-adjust: none) {
  p {
    letter-spacing: 0;
    line-height: 1;
    font-size-adjust: 0.59;
  }
}

/* Once the web font has loaded, apply this */
.webfont-loaded p {
  font-family: 'Lato', sans-serif;
  letter-spacing: 0;
  line-height: 1;
}
</code></pre>

Here, we are defining `letter-spacing` and `line-height` as a fallback first, and we are [using `@supports`](https://drafts.csswg.org/css-conditional-3/#at-supports) to feature-detect and then apply `font-size-adjust` if it is supported.

We won’t get a perfect solution for all fonts, but it will minimize the distraction when the typeface changes.</p>

## Layout

Until now, we have covered media, widgets and fonts, but the content could also shift when the CSS for the main layout gets applied.</p>

### Flexbox vs. Grid

Flexbox [can cause horizontal shifting](https://jakearchibald.com/2014/dont-use-flexbox-for-page-layout/), as shown by Jake Archibald.

With flexbox, the content controls how the layout is displayed, whereas with grid layouts, the layout is displayed according to the grid definition. Therefore, using grid for the main layout is better.

You probably won’t see the content shift if you’re developing on a fast machine with a great Internet connection, but users who are surfing on a slow connection will.</p>

<pre><code class="language-css">
.wrapper {
  display: flex;
}

.sidebar {
  flex: 1 1 30%;
}

.content {
  flex: 1 1 70%;
}

/* Use grid instead of flexbox if supported */
@supports (display: grid) {
  .wrapper {
    display: grid;
    grid-template-columns: 30% 70%;
  }

  .sidebar {
    grid-column: 1;
  }

  .content {
    grid-column: 2;
  }
}
</code></pre>

[Support](https://caniuse.com/#feat=css-grid) for CSS grid layouts isn’t very good at the moment, but it will increase in the next month when Safari 10 ships, and Firefox and Blink-based browsers will probably enable it by default. To be future-proof, we should use flexbox as our foundation and enhance the experience with a grid layout if it is supported.</p>

## Little Big Details

Changing CSS properties based on user interaction can often cause horizontal shifting. This can be avoided by using alternative CSS properties.</p>

### text-shadow for Bold Text

When changing the font weight of text, the size of the element will change and a content shift will occur.</p>

<pre><code class="language-css">
a:hover,
a:focus {
  font-weight: bold;
}

@supports (text-shadow: none) {
  a:hover,
  a:focus {
    font-weight: normal;
    text-shadow: 1px 0 0 currentColor;
  }
}
</code></pre>

Redrawing `text-shadow` can be computationally more intensive than changing `font-weight`, but it is the only way to prevent the jump effect when changing to a heavier weight of text.

Once again, we are using feature-detection to apply `text-shadow`, instead of `font-weight`, upon interaction from the user. Because `@supports` is supported by fewer browsers than `text-shadow`, we could also consider using [Modernizr](https://modernizr.com/) to detect the feature and apply the improvement in all supported browsers.

Small details will often make a good experience great. Your users will appreciate every content shift that is avoided.</p>

## Scroll Anchoring

Now that you’ve learned about ways to avoid content jumps, you might be wondering why browsers can’t prevent content jumps more efficiently.

The Chrome team recently introduced [scroll anchoring](https://developers.google.com/web/updates/2016/04/scroll-anchoring), which does exactly that.

Scroll anchoring is a [proposed intervention](https://github.com/WICG/interventions/blob/master/scroll-anchoring/explainer.md) that adjusts the scroll position to reduce visible content jumps.

At the moment, scroll anchoring is only available behind an experimental flag in Chrome, but other browser vendors have shown interest and will hopefully implement it in future.</p>

## Conclusion

As you can see, there are many solutions for avoiding the jump effect on page load. Yes, implementing all of these techniques would take some time, but it is totally worth it — until scroll anchoring is supported in more browsers.

If you take the time to avoid jumps by using the techniques mentioned above — defining placeholders, reserving space and preparing for fallbacks — then users will have a less annoying experience and will be able to **enjoy your content without interruption**.

How do you minimize content shifting on your websites? Have you discovered any particular tricks or techniques to prevent the jump effect?

{{< signature "il, al" >}}

_Front page image credits: [Rayi Christian W.](https://tumblr.unsplash.com/post/89277673479/download-by-rayi-christian-w)_

