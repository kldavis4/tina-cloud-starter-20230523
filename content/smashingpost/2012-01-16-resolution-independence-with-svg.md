---
title: Resolution Independence With SVG
slug: resolution-independence-with-svg
image: null
date: 2012-01-16T12:46:25.000Z
author: david-bushell
description: >-
  In this article, we’ll look at Scalable Vector Graphics (SVG), one of the most underused technologies in website development today. Before diving into an example, let’s consider the state of the Web at present and where it is going. Website design has found new vigor in recent years, with the evolving technique of **responsive design**.
categories:
  - Coding
  - CSS
---
In this article, we’ll look at Scalable Vector Graphics (SVG), one of the most underused technologies in website development today.

Before diving into an example, let’s consider the state of the Web at present and where it is going. Website design has found new vigor in recent years, with the evolving technique of <strong>responsive design</strong>. And for good reason: essentially, responsive website design moves us away from the fixed-width pages we’ve grown accustomed to, replacing them with shape-shifting layouts and intelligent reflowing of content.

Add to that a thoughtful content strategy and mobile-first approach, and we’re starting to offer an experience that adapts across devices and browsers to suit the user’s context.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)
*   [Styling And Animating SVGs With CSS](https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/)
*   [Creating Cel Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)
*   [The Illusion Of Life: An SVG Animation Case Study](https://www.smashingmagazine.com/2016/07/an-svg-animation-case-study/)

{{% feature-panel %}}

When we look at the breadth of Web-enabled devices, responsive design is sure to provide a better user experience. Scrolling horizontally, panning and zooming the viewport have their place in user interface design, but forcing the user to do these things just to navigate a website quickly becomes tedious. Fitting the website to the viewport is about more than just layout: it’s also about <strong>resolution</strong>. In this article, I’ll demonstrate why SVG is a perfect addition to future-friendly Web development.</p>

### Introducing SVG

SVG offers a truly resolution-independent technique for presenting graphics on the Web. SVG is a vector graphics format that uses <strong>XML</strong> to define basic properties such as paths, shapes, fonts and colors, and more advanced features such as gradients, filters, scripting and animation. Create the file once and use it anywhere, at any scale and resolution.

Consider the use cases: <strong>UI and navigation icons, vector-style illustrations, patterns and repeating backgrounds</strong>. For all of these, a scalable graphic is the perfect solution from a visual standpoint, and yet fixed-resolution images are still the norm. In the example below, we’ll show you how to expand on a common development technique to take advantage of SVG.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="119442" title="Resolution Independency with SVG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d7aaef6-148e-4bbd-ba2e-e690ba210d75/resolution-independence.png" alt="Resolution independence with SVG" width="500" height="250" />

## A Case Study: CSS Sprites

We all know about the CSS sprites technique. (If you don’t, then have a quick read through <a title="CSS Sprites: Useful Technique, or Potential Nuisance?" href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/">Sven Lennartz’ article</a>. And Louis Lazaris points out its <a title="CSS Sprites: Useful Technique, or Potential Nuisance?" href="https://www.smashingmagazine.com/2010/03/26/css-sprites-useful-technique-or-potential-nuisance/">pros and cons</a>.) In the example below, we’ll show how seamlessly SVG replaces normal raster images. If this technique is not for you, you can certainly imagine a whole array of similar situations in which to use SVG.

Vector icons play a big role in user interface design. Pictures express concepts with vivid clarity, whereas their textual counterparts might carry ambiguity. In UI design, where space is scarce, a simple illustrated icon could be greatly welcome.

I’ve mocked up the following example:

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="119392" title="An icon based UI menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb236d8b-ef89-476c-9789-bbca1b7c8230/fig1-finalmenu.png" alt="An icon based UI menu" width="432" height="60" />

I’ll be first to admit that this row of icons won’t win any design awards, but it will suffice for the sake of this article! Let’s look at the HTML:

<pre><code class="language-markup tmp-html">&lt;div class="actions"&gt;
   &lt;a class="a-share" href="#"&gt;Share&lt;/a&gt;
   &lt;a class="a-print" href="#"&gt;Print&lt;/a&gt;
   &lt;a class="a-tag" href="#"&gt;Tag&lt;/a&gt;
   &lt;a class="a-delete" href="#"&gt;Delete&lt;/a&gt;
&lt;/div&gt;</code></pre>

I’ve kept the HTML to a minimum for clarity, but in practice you’d probably want to mark it up with an unordered list. And you’ll almost certainly want to replace those hashes with real URLs (even if JavaScript provides the functionality, having a fallback is nice). Let’s look at the CSS:

<pre><code class="language-css">.actions {
   display: block;
   overflow: auto;
}

.actions a {
   background-image: url('sprite.png');
   background-repeat: no-repeat;
   background-color: #ccc;
   border-radius: 5px;
   display: block;
   float: left;
   color: #444;
   font-size: 16px;
   font-weight: bold;
   line-height: 20px;
   text-decoration: none;
   text-shadow: 0 -1px 2px #fff;
   padding: 10px 20px 10px 40px;
   margin-right: 5px;
}

.a-share  { background-position: 10px 0; }
.a-print  { background-position: 10px -40px; }
.a-tag    { background-position: 10px -80px; }
.a-delete { background-position: 10px -120px; }</code></pre>

Note the fixed-pixel sizing and the PNG background, which we can see below framed in full Photoshop production glory:

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="119394" title="A PNG sprite in Photoshop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c6df487-593d-48ca-935a-1a1f27a0129b/fig2-pngsprite.png" alt="A PNG sprite in Photoshop" width="233" height="234" />

This implementation of a CSS sprite is basic, and at today’s standard, it’s not good enough! How can we enhance this? First, let’s consider the following issues:

1.  We’ve **rasterized** the image at a very early stage. Even at full size, icons in which points sit between pixels, such as the one for “Print,” have blurred.
2.  If we **zoom in**, the image will blur or pixellate even more; there is no additional data to re-render the image at larger sizes.
3.  Everything has a **fixed size**, which is neither good for responsive design nor good for accessibility, because the browser’s default font size is ignored.

As you’ve probably guessed by now, we’ll show you how SVG solves these problems. But first, let’s reiterate each point thoroughly to understand the issues at large.</p>

### 1. Rasterization

Devices such as modern smartphones have a very high pixel density; some already surpass the 300 pixels-per-inch (PPI) mark that is assumed to be the limit of the human eye’s ability to distinguish fine details. A pixel has no real-world equivalent in size until it sits on a screen of fixed dimension (say, 3.5 inches diagonally) and fixed resolution (say, 640 × 960 pixels). At this scale, text with a font size of 16 pixels would be incredibly small to the eye. For this reason, devices simply cannot translate 1 CSS pixel unit to 1 device pixel; instead, they double up. Thus, a 16-pixel font size actually takes over 32 pixels when rendered.

The same applies to images; but they are already rasterized, so doubling up the pixels has no benefit. In our example, each icon has been rasterized at around 25 × 25 pixels (the whole sprite being 30 × 160), so they cannot take advantage of the <strong>double pixel ratio</strong>. One solution is to use <strong>CSS media queries</strong> to detect the pixel ratio. This is already implemented in Webkit- and <a title="CSS media queries - device pixel ratio" href="https://developer.mozilla.org/en/CSS/Media_queries#-moz-device-pixel-ratio">Gecko</a>-based browsers.

To improve our example, we can add the following CSS declaration:

<pre><code class="language-css">@media only screen and (-webkit-min-device-pixel-ratio: 2)  {
   .actions a {
      background-image: url('sprite@2x.png');
      background-size: 30px 160px;
   }
}</code></pre>

The alternate background image supplied in the code above has been saved at 60 × 320 pixels (i.e. double the original dimensions). The <code>background-size</code> property tells CSS to treat it smaller. Significantly, now the device has the additional data to render a better image (if capable).

This solution isn’t bad, but it doesn’t solve the problems we’ll run into in points 2 and 3 below. It also requires that we maintain multiple files of increasing size: a potential burden on bandwidth and a real hassle. For non-vector images, such as photography in JPG format, we can’t do much more than that.</p>

### 2. Zooming

At their default size, our rasterized icons look acceptable, at least on low-pixel-density screens. However, should the user zoom in on the Web page, these little UI delights will degrade very quickly.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="119397" title="A PNG sprite zoomed and blurred." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c97d8a66-5637-4200-9f55-4ef30f364a24/fig3-zoom.png" alt="A PNG sprite zoomed in and blurred." width="453" height="104" />

Zooming is a common action when users find a website too small for comfortable viewing. Or, to put it another way, websites that are designed too small are very common. There is really no “perfect” size, because almost everyone has at least some level of visual impairment, since our eyes inevitably deteriorate with age. Secondly, with the rapid increase in touchscreen devices, pinch-to-zoom has become the standard way to enlarge fixed-sized content designed for larger screens (i.e. much of the Web today).

We should develop websites in a way that minimizes the need for user input — that’s where responsive design comes in (see point 3 below) — but zooming is here to stay. There’s simply no way to provide pre-rasterized images for every level of zoom (in theory, an infinite scale). Scalable graphics are the solution, and we’ll show you how to enhance our example. But first, a related word on fixed sizing.</p>

### 3. Fixed Sizes

Presenting page elements at fixed sizes forces many users to zoom, but it also disables a very useful browser feature. Users can set their preferred font size (the default in browsers is 16 pixels). By sizing everything in pixels, we override this preference. Sizing elements based on this default is much better, so that, if the text is bigger, everything adjusts to match. This essentially mimics the zooming effect but happens without the user having to manually do it on every visit. Ethan Marcotte has written a great article that <a title="Type study: Sizing the legible letter" href="https://blog.typekit.com/2011/11/09/type-study-sizing-the-legible-letter/">explains relative font sizes</a>.

Let’s re-implement our sprite example with a solution to these three issues.</p>

### A Scalable Implementation

Here is the HTML again. We don’t need to change anything here.

<pre><code class="language-markup tmp-html">&lt;div class="actions"&gt;
   &lt;a class="a-share" href="#"&gt;Share&lt;/a&gt;
   &lt;a class="a-print" href="#"&gt;Print&lt;/a&gt;
   &lt;a class="a-tag" href="#"&gt;Tag&lt;/a&gt;
   &lt;a class="a-delete" href="#"&gt;Delete&lt;/a&gt;
&lt;/div&gt;</code></pre>

The updated CSS is where the magic happens:

<pre><code class="language-css">body { font-size: 100%; }

.actions {
   display: block;
   overflow: auto;
}

.actions a {
   font-size: 1em;
   line-height: 1.25em;
   padding: 0.625em 1.25em 0.625em 2.5em;
   margin-right: 0.3125em;
   border-radius: 0.3125em;
   background-image: url('sprite.svg');
   -webkit-background-size: 1.875em 10em;
   -o-background-size: 1.875em 10em;
   -moz-background-size: 1.875em 10em;
   background-size: 1.875em 10em;
   /* styles carried over from the original implementation */
   background-repeat: no-repeat;
   background-color: #ccc;
   color: #444;
   display: block;
   float: left;
   text-decoration: none;
   text-shadow: 0 -1px 2px #fff;
}

.actions-em .a-share { background-position: 0.625em 0; }
.actions-em .a-print { background-position: 0.625em -2.5em;  }
.actions-em .a-tag { background-position: 0.625em -5.0em;  }
.actions-em .a-delete { background-position: 0.625em -7.5em;  }</code></pre>

In this version, we’ve made the following changes:

*   The `background-image` is now an SVG file.
*   All sizes are based on the default of 16 pixels, or 1 em. If the user’s default is larger or smaller, then everything will scale relatively. (If you multiple each em size by 16, you’ll get the number of pixels used in our initial fixed-size example.)
*   The **`background-size` is very important**. By setting this in em units, we’re telling the browser to scale the sprite relative to everything else. You’ll notice that 1.875 × 10 em multiplied by 16 becomes 30 × 160 — the base size at which we produced the sprite in pixels.
*   The `background-position` of each sprited icon is also based on relative units.

Now that we’re using SVG and relative sizes, we have solved the three big issues highlighted above. A scalable graphic can be rasterized on demand to perfectly suit any device resolution and any zoom level. By using relative sizes, we can continue implementing a responsive design, minimizing as much as possible the need for the user to zoom. We’re also respecting the browser’s default font size, and enabling our design to adapt accordingly.

I actually produced the SVG sprite first and the PNG version from that. (I imported the SVG in Photoshop before exporting it as a PNG — Illustrator’s PNG export had very poor rasterization.) Below is the header in my SVG file. Notice the same 30 × 160 initial size.

<pre><code class="language-markup tmp-xml">&lt;svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
   width="30px" height="160px" viewBox="0 0 30 160" enable-background="new 0 0 30 160" xml:space="preserve"&gt;</code></pre>

You can see that the attributes for width and height are set in pixels (<code>width="30px" height="160px"</code>) in the opening <code>svg</code> tag (as generated by Adobe Illustrator). This actually causes it to render early in Firefox, before the graphic has scaled to match the em sizes in <code>background-size</code>. Webkit-based browsers seem to scale the SVG perfectly, regardless. I’ve found that editing the SVG file to use em units in these two attributes fixes any rendering issues in Firefox.

<pre><code class="language-markup tmp-xml">&lt;svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
   width="30em" height="160em" viewBox="0 0 30 160" enable-background="new 0 0 30 160" xml:space="preserve"&gt;</code></pre>

I don’t know which browser actually implements this scaling correctly, but let it be noted that extra care is needed to ensure cross-browser perfection. Mozilla MDN has an excellent in-depth article, “<a title="Scaling of SVG backgrounds" href="https://developer.mozilla.org/en/CSS/Scaling_of_SVG_backgrounds">Scaling of SVG Backgrounds</a>,” which explores more practical examples. For more ideas, see Alex Walker’s article “<a title="A Farewell to CSS3 Gradients" href="https://designfestival.com/a-farewell-to-css3-gradients/A%20Farewell%20to%20CSS3%20Gradients">A Farewell to CSS3 Gradients</a>.”

Here’s a super-close screenshot showing the SVG sprite:

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="119399" title="A close-up of a SVG sprite." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/108e5c72-a092-4b64-b0e9-cb1a1a29dc4e/fig4-closeup.png" alt="A close-up of a SVG sprite." width="455" height="187" />

The sprite scales beautifully. (Sadly, the same can’t be said for my tacky text-shadow effect.)

It’s best to experience the joys of scalable graphics and relative sizing firsthand. I’ve uploaded a <a title="Scalable Sprites in Action" href="https://dbushell.com/demos/css-sprites/">side-by-side live demo</a> demonstrating a combination of all the techniques mentioned above.</p>

## Browser Support

At the start of this article, I said that SVG was underused. I believe that has generally been the case due to poor browser support. But things are different now! Browser support for SVG has blossomed over the last year to the point where implementing it is a viable use of development time.

According to the website <a title="When can I use SVG?" href="https://caniuse.com/#search=SVG">When Can I Use?</a>, support for SVG across multiple implementations is as follows (I’ve combined support for both CSS’ <code>background-image</code> and HTML’s <code>img</code> source — the most useful attributes):

*   Internet Explorer 9+
*   Firefox 4+
*   Chrome 4+
*   Safari 4+
*   Opera 9.5+

<a title="Mobile HTML5" href="https://mobilehtml5.org/">Mobile browser support</a> is also pretty much across the board. If a workable fallback exists for older browsers, then SVG is a very viable solution.

For some of the new additions to Web standards, we can implement them safe in the knowledge that old browsers will simply ignore them and that they aren’t even required. We call this “progressive enhancement”: better browsers get a progressively better experience. SVG is slightly different, because for most practical purposes, it simply replaces other images in CSS backgrounds and HTML elements. The image format — be it SVG, PNG, JPG or GIF — is either supported or it isn’t. We can’t simply follow the practice of progressive enhancement here, because an image failing to render is not an acceptable experience.</p>

### Browser Sniffing or Feature Detection?

We could make an educated guess and say that we need to worry only about users of Internet Explorer 6 to 8. In this case, the <a title="HTML5 Boilerplate - IE html tag classes" href="https://html5boilerplate.com/docs/The-markup/#ie-html-tag-classes">conditional comments technique</a> for IE-only styles enable us to re-apply a second CSS <code>background-image</code> of a supported format such as PNG, instead of the default SVG background.

Browsing sniffing is always a dangerous game. While Internet Explorer tends to be the main offender, we can never assume it is the only one.

The safer and highly recommended option is to detect SVG support and use it only if it’s found. I suggest using <a title="Modernizr" href="https://www.modernizr.com/">Modernizr</a> if you need to detect multiple features. Modernizr applies a class of <code>svg</code> to your root <code>html</code> element if detected (to which you can apply SVG as a <code>background-image</code>). If you’re using SVG as the source of an image element in HTML, then implementation is a little harder. You’ll have to write more JavaScript to find and replace all sources once support has been established.

The problem with these methods is that the browser will download the fallback image before SVG is detected — the only exception being the conditional comments technique for IE. Users will also likely see a flash of re-styled content when the source image changes. This shouldn’t be the case for long; but at least for now, these problems may be enough to hold you off on SVG usage.</p>

### File Size

In our sprite example, the raw SVG file was 2445 bytes. The PNG version was only 1064 bytes, and the double-sized PNG for double-pixel ratio devices was 1932 bytes. On first appearance, the vector file loses on all accounts, but for larger images, the raster version more quickly escalates in size.

SVG files are also human-readable due to being in XML format. They generally comprise a very limited range of characters, which means they can be heavily Gzip-compressed when sent over HTTP. This means that the actual download size is many times smaller than the raw file — easily beyond 30%, probably a lot more. Raster image formats such as PNG and JPG are already compressed to their fullest extent.</p>

### Performance

Rendering performance is a concern with SVG, especially on mobile devices, whose hardware is limited. Raster images can be rendered pixel for pixel after decompression and de-encoding. Vector graphics need to be rasterized at a specific resolution every time they’re viewed.

SVG has <a title="Comparing hardware-accelerated SVG across browsers with Santa’s Workshop" href="https://blogs.msdn.com/b/ie/archive/2011/03/08/comparing-hardware-accelerated-svg-across-browsers-with-santa-s-workshop.aspx">consistently</a> <a title="SVG vs Canvas performance" href="https://joeloughton.com/blog/web-applications/svg-vs-canvas-performance/">proved</a> <a title="Performance of Canvas versus SVG" href="https://smus.com/canvas-vs-svg-performance">slower</a> than Canvas as a platform for animating vector graphics; but our concern here is basic rendering, not manipulation a thousand times per second, and if <em>that</em> is possible, then simple rendering shouldn’t be a concern. The more intensive SVG features are things like clipping masks and filter effects. These are unnecessary for many practical purposes (like our sprite example), but, if required, the best way to check performance is by <strong>testing</strong>. A lot of Web development is supported in theory, but in practice results are far from perfect.</p>

## Alternative Methods

Hopefully you agree that SVG is extremely useful but not always the ideal solution to resolution independence. Ultimately, the trick is to avoid raster images while maintaining the scalability of visual styles. Below are a few more ideas to think about.</p>

### CSS3

You’ve probably already started combining CSS3 properties such as <code>linear-gradient</code>, <code>text-shadow</code> and <code>box-shadow</code> to create more complex styles. Web developer Lea Verou curates a <a title="Lea Verou — CSS Patterns" href="https://lea.verou.me/css3patterns/">CSS3 pattern gallery</a> that shows off the impressive potential of gradients alone.

<a href="https://lea.verou.me/css3patterns/"><img loading="lazy" decoding="async"  title="CSS3 gradient patterns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857f96f1-4385-4260-86b8-3bd45af77153/css3patterns.png" alt="CSS3 gradient patterns" width="500" height="220" /></a>

In his article “Mobile Web in High Resolution,” Brad Birdsall introduces a technique to maintain pixel perfection for high-resolution displays using the pixel-ratio property.

Then there are pure CSS “icons,” which <a title="Pure CSS Icons: Make The Madness Stop" href="https://farukat.es/journal/2010/08/469-pure-css-icons-make-madness-stop">Faruk Ateş</a> rightly points out as being absolute “madness” — certainly so if you’re using CSS to create a logo! But you could argue the benefits of a small handful of very specific techniques, such as CSS triangles, as <a title="CSS Triangle | CSS Tricks" href="https://css-tricks.com/snippets/css/css-triangle/">demoed by Chris Coyier</a>.</p>

### Web Fonts

<a title="Dingbat Web Fonts" href="https://filamentgroup.com/lab/dingbat_webfonts_accessibility_issues/">Dingbat Web fonts</a> and look-a-like Unicode glyphs are two interesting alternatives for vector icons, both with accessibility and semantic challenges. <a title="24 Ways: Displaying Icons with Fonts and Data- Attributes" href="https://24ways.org/2011/displaying-icons-with-fonts-and-data-attributes">Jon Hicks has a write-up</a> of perhaps the best practice for this. SVG seems a more appropriate technique for icons, but both have an immediate visual impact at high resolutions — and we’ll be paying increasing attention to that in coming years.</p>

## Looking Forward

As you can see, SVG usage is very much a possibility, and browser support and performance will only improve in future. What’s important to note from this article is that we really should be building websites that are as resolution-independent as possible.

Consider the “one Web” philosophy and the vast range of devices we use to access it — there is no single user experience. The more we can do to stay device-agnostic, the better. Responsive website design addresses many of these needs and certainly provides many benefits. Using vector graphics may not be as apparent, but its little improvements really do make a difference.

With today’s level of support, many users can experience the beauty of crisp scalable graphics… or perhaps that’s the wrong way to think about it. Most users won’t say “Wow! Kudos on the vectors.” To our dismay, they probably wouldn’t even consider them (and certainly wouldn’t recognize the effort required to craft them). And that’s a good thing; each time we improve the user’s experience, we don’t necessarily need to make a song and dance about it. Letting things continue to grind away under-appreciated is OK. It’s the <em>lack</em> of such things that gets recognized and sniffed at. Raise the user’s expectations in visual aesthetics, and they’ll start to notice the websites that do look shoddy. If you don’t do it, others will.

{{< signature "al" >}}

