---
title: Redefining Lazy Loading With Lazy Load XT
slug: redefining-lazy-loading-with-lazy-load-xt
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43b892a2-9859-4905-be03-384c222c1f17/excerpt-lazy-load.png
date: 2015-02-03T18:00:56.000Z
author: denisryabovugurkaner
description: >-
  Lazy loading images started
  to become popular on the web back in 2007, when Mika Tuupola drew inspiration
  from the YUI ImageLoader utility and released a jQuery plugin. Since then,
  it’s become a popular technique to optimize page loading and the user
  experience. In this article I will discuss why we should and shouldn't use
  Lazy Load, and how to implement it.
categories:
  - Coding
  - Techniques
  - jQuery
  - Performance
---
Lazy loading is a common software design pattern that defers the initialization of objects until they are needed. Lazy loading images started to become popular on the web back in 2007, when Mika Tuupola drew inspiration from the YUI ImageLoader utility and <a href="https://www.appelsiini.net/projects/lazyload">released a jQuery plugin</a>.

Since then, it’s become a popular technique to optimize page loading and the user experience. In this article I will discuss <strong>why we should and shouldn't use Lazy Load</strong>, and how to implement it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Infinite Scrolling, Pagination Or “Load More” Buttons?](https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/)
*   [Addressing The Responsive Images Performance Problem](https://www.smashingmagazine.com/2013/09/responsive-images-performance-problem-case-study/)
*   [Front-End Performance Checklist 2017 (PDF, Apple Pages)](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [Guide To Using WebP Images Today: A Case Study](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)

## Why Lazy Load?

Images make up over 60% of an average page’s size, <a href="https://httparchive.org/interesting.php">according to HTTP Archive</a>. Images on a web page would be rendered once they are available. Without lazy loading, this could lead to a lot of data traffic that is not immediately necessary (such as images outside of the viewport) and longer waiting times. The problem? Visitors are not patient at all. By lazy loading, images outside of the viewport are loaded only when they would be visible to the user, thus saving valuable data and time.

{{% feature-panel %}}

Lazy loading is not limited to images. It can be used on pages with complex JavaScript, iframes and third-party widgets, delaying the loading of these resources until the user actually needs them.</p>

## Why Not Lazy Load?

Lazy loading is not a silver bullet, and it is known to affect performance. For example, most lazy-loading implementations either don't have a <code>src</code> attribute in the <code>&lt;img&gt;</code> tags (which is invalid syntax, according to the HTML5 standard) or point to a blank image (hello, <code>spacer.gif</code>). This approach requires duplicate <code>&lt;img&gt;</code> tags wrapped in <code>&lt;noscript&gt;</code> tags for browsers with JavaScript disabled (or with the NoScript plugin installed):

<pre><code class="language-markup">&lt;img data-src="path" attributes /&gt;&lt;noscript&gt;&lt;img src="path" attributes /&gt;&lt;/noscript&gt;</code></pre>

Fortunately, this duplication doesn’t increase the page’s size significantly when you enable Gzip compression. However, some search engines might not index your images correctly, because the <code>&lt;noscript&gt;</code> tag is not indexed within content, and the <code>&lt;img&gt;</code> tag outside of <code>&lt;noscript&gt;</code> is referring to a blank image. Currently, Google seems to eventually index lazy-loaded images, but other search engines are less likely to.</p>

## How Is Lazy Loading Implemented?

You might be overwhelmed by the number of lazy-load plugins out there. You might also think that implementing one is easy: Just monitor page scrolling (or resizing), and then set the <code>src</code> attribute when an image is visible. If only it were that easy. Many things come into play when building a solid solution that works on both desktop and mobile. So, how do you separate the signal from the noise?

*   **Throttling**.  Checking the visibility of images after every interaction (even a tiny bit of scrolling) could compromise the page’s responsiveness. To ease that, implement some sort of throttling mechanism.
*   **All your mobile are belong to us**.  There is no `scroll` event in the Opera Mini browser and some old feature phones. If you receive traffic from those devices, you should monitor and load all images directly.
*   **Lazy load or automatic pagination?** Some implementations check only whether an image is above the fold. If the page is scrolled down to the very bottom via an anchor (or the `scrollTo` method in JavaScript), then all images below the fold will begin to download, instead of only the images within the viewport. This is more a matter of automatic pagination because users will have to wait for the remaining images to load after an interaction.
*   **Dynamic image insertion**.  Many websites use AJAX navigation nowadays. This requires a lazy-load plugin to support the dynamic insertion of images. To prevent a memory leak, any references to images that are not in the DOM (for example, ones that appear after an AJAX-based replacement of content) should also be removed automatically.

This list is certainly not comprehensive. We have many more issues to consider, such as the lack of <code>getBoundingClientRect</code> in old browsers, a change in orientation without an ensuing <code>resize</code> event on the iPhone, or the particular handling requirements of the jQuery Mobile framework.

Unfortunately, most plugins do not handle all of the above.</p>

## Lazy Load XT

We’ve been optimizing web performance on numerous screens for almost a decade now. Our project <a href="https://www.mobilejoomla.com/">Mobile Joomla</a> has been applied to over a quarter billion web pages and is still one of the most popular ways to optimize Joomla websites for mobile. Thanks to this, we’ve been lucky to witness the evolution of the web from desktop to mobile and observe trends and changing needs.

With our latest project, RESS.io, we’ve been working on an easy solution to automatically improve responsive design performance on all devices. Lazy loading became an integral part of the project, but we came to realize that current lazy-load implementations are insufficient for the growing needs of the modern web. After all, it’s not just about desktop, mobile and images anymore, but is more and more about other media as well, especially video (oh, and did I hear someone say “social media widgets”?).

We concluded that the modern web could use a mobile-oriented, fast, extensible and jQuery-based solution. That is why we developed one and called it <a href="https://github.com/ressio/lazy-load-xt">Lazy Load XT</a>.

Here are its main principles, which consider both current and future applications:

*   It should support [jQuery Mobile](https://jquerymobile.com/) out of the box.
*   It should support the [jQuery](https://jquery.com/), [Zepto](https://zeptojs.com/) and [DOMtastic](https://webpro.github.io/DOMtastic/) libraries. Of course, writing the solution in native JavaScript is possible, but jQuery is a rather common JavaScript extension nowadays, and one of our aims was to simplify the transition from the original Lazy Load to Lazy Load XT. This makes jQuery an adequate choice. However, if you don't want to use jQuery at all, read the “Requirements” section below for details on reducing the size of dependent libraries.
*   It must be easy to start. The default settings should work most of the time. Prepare the HTML, include the JavaScript, et voilà!

### Include

Lazy Load XT requires jQuery 1.7+, Zepto 1.0+ or DOMtastic 0.7.2+. Including the plugin is easy and as expected:

<pre><code class="language-markup">&lt;script src="jquery.min.js"&gt;&lt;/script&gt;
&lt;script src="jquery.lazyloadxt.min.js"&gt;&lt;/script&gt;

&lt;script&gt;$.lazyLoadXT.extend({edgeY: 200});&lt;/script&gt;

&lt;style&gt;img.lazy {display:none}&lt;/style&gt;</code></pre>

### Use

By default, the plugin processes all images on the page and obtains an image’s actual source path from the <code>data-src</code> attribute. So, the recommended snippet to place an image on the page is this:

<pre><code class="language-markup">&lt;img class="lazy" data-src="path" [attributes] /&gt;&lt;noscript&gt;&lt;img src="path" [attributes] /&gt;&lt;/noscript&gt;</code></pre>

From this snippet, it is clear why we’ve set <code>img.lazy</code> above to <code>display: none</code>: Hiding the image is necessary in case there is no JavaScript, or else both the original image and the placeholder would be displayed. If the <code>src</code> attribute of the <code>&lt;img&gt;</code> tag is not set, then the plugin will set it to be a transparent GIF using the <code>data-uri</code> attribute.

If you’re not worried about users who have disabled JavaScript (or about valid HTML5 code), then just load <code>jquery.lazyloadxt.min.js</code> and replace the <code>src</code> attribute in the images with <code>data-src</code>:

<pre><code class="language-markup">&lt;script src="jquery.min.js"&gt;&lt;/script&gt;
&lt;script src="jquery.lazyloadxt.min.js"&gt;&lt;/script&gt;
&lt;img data-src="path" [attributes] /&gt;</code></pre>

### Video

Lazy Load XT is available in two versions: <code>jquery.lazyloadxt.js</code> and <code>jquery.lazyloadxt.extra.js</code>. The latter includes better support of video elements, both <code>&lt;video&gt;</code> tags and ones embedded in <code>&lt;iframe&gt;</code> (such as YouTube and Vimeo).

Markup changes are similar to the above, and replacing the <code>src</code> attributes with <code>data-src</code> and <code>post</code> with <code>data-poster</code> is sufficient if you’re using them in a <code>&lt;video&gt;</code> element.

<pre><code class="language-markup">&lt;script src="jquery.lazyloadxt.extra.js"&gt;&lt;/script&gt;</code></pre>

<pre><code class="language-markup">&lt;iframe data-src="//www.youtube.com/embed/[videocode]?rel=0" width="320" height="240"&gt;&lt;/iframe&gt;</code></pre>

<pre><code class="language-markup">&lt;video data-poster="/path/to/poster.jpg" width="320" height="240" controls&gt;
   &lt;source data-src="/path/to/video.mp4" type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'&gt;
   &lt;source data-src="/path/to/video.ogv" type='video/ogg; codecs="theora, vorbis"'&gt;
&lt;/video&gt;</code></pre>

<pre><code class="language-markup">&lt;video data-src="/path/to/video2.mp4" width="320" height="240" controls&gt;</code></pre>

### Size

The size of the <code>jquery.lazyloadxt.min.js</code> file is 2.3 KB (or 1.3 KB Gzip’ed), and the size of <code>jquery.lazyloadxt.extra.min.js</code> is 2.7 KB (or 1.4 KB Gzip’ed). That’s small enough, especially compared to jQuery and Zepto.</p>

### Requirements

Even though Lazy Load XT requires jQuery, Zepto or DOMtastic, loading the full versions of any of them is not necessary. For example, DOMtastic requires only a minimal set of modules (<code>attr, class, data, event, selector, type</code>) for you to get a 7.9 KB file (or 2.7 KB Gzip’ed), bringing the total size of both DOMtastic and Lazy Load XT to just 4 KB (Gzip’ed).</p>

### Compatibility

We've tested Lazy Load XT in the following browsers:

*   Internet Explorer 6 – 11
*   Chrome 1 – 37
*   Firefox 1.5 – 32.0
*   Safari 3 – 7
*   Opera 10.6 – 24.0
*   iOS 5 – 7 (stock browsers)
*   Android 2.3 – 4.4 (stock browsers)
*   Amazon Kindle Fire 2 and HD 8.9 (stock browsers)
*   Opera Mini 7

### Performance

We have tested Lazy Load XT’s performance on a page with one thousand images and are happy with the results: Scrolling works well even on old Android 2.3 devices.

We also successfully tested various iterations of Lazy Load XT on over one thousand websites for several months in our jQuery Mobile-based <a href="https://www.mobilejoomla.com/templates.html">Elegance and Flat templates</a>.</p>

### Options

The plugin’s default settings may be modified with the <code>$.lazyLoadXT</code> object:

<pre><code class="language-javascript">$.lazyLoadXT.edgeY = 200;
$.lazyLoadXT.srcAttr = 'data-src';</code></pre>

Note that you may change this object at any time: before loading the plugin, between loading and when the document is ready, and after the event is ready. (Note that the last option doesn’t affect initialized images.)

Lazy Load XT supports a lot of options and events, enabling you to integrate other plugins or implement new features. For the full list and details, see <a href="https://github.com/ressio/lazy-load-xt#options”">Lazy Load XT’s GitHub page</a>.</p>

### AJAX Support

If you use jQuery Mobile with built-in AJAX page loading, then the Lazy Load XT plugin will do all of the magic for you in the <code>pageshow</code> event. In general, you should run the code below to initialize images inside a container with AJAX-loaded content.

<pre><code class="language-javascript">$(window).lazyLoadXT();</code></pre>

Or run this:

<pre><code class="language-javascript">$('#ajaxContainer').lazyLoadXT();</code></pre>

## Extending Lazy Load XT

Lazy Load XT can be extended easily using the <code>oninit</code>, <code>onshow</code>, <code>onload</code> and <code>onerror</code> handlers or the related <code>lazyinit</code>, <code>lazyshow</code>, <code>lazyload</code> and <code>lazyerror</code> events. In this way, you can create amazing add-ons.

Some examples can be found <a href="https://ressio.github.io/lazy-load-xt">on the GitHub page</a>, along with <a href="https://github.com/ressio/lazy-load-xt/#extendability">usage instructions</a>. We’ll highlight just a few of them here.</p>

### Loading Animation

Customizing the image-loading animation is easy. By default, Lazy Load XT includes <a href="https://github.com/ressio/lazy-load-xt/#spinner">spinner</a> and <a href="https://github.com/ressio/lazy-load-xt/#fade-in-animation">fade-in</a> animations, but you can use any effects from the <a href="https://github.com/daneden/animate.css">Animate.css</a> project or any other.</p>

### Responsive Images

Lazy Load XT has two add-ons for <a href="https://github.com/ressio/lazy-load-xt/#responsive-images">responsive images</a>. One is “srcset,” to polyfill the <code>srcset</code> attribute (and that should be renamed <code>data-srcset</code>):

<pre><code class="language-markup">&lt;img data-srcset="image-hd.jpg 2x, image-phone.jpg 360w, image-phone-hd.jpg 360w 2x"&gt;</code></pre>

The second is “picture,” a polyfill for the <code>&lt;picture&gt;</code> tag:

<pre><code class="language-markup">&lt;picture width="640" height="480"&gt;
   &lt;br data-src="small320.jpg"&gt;
   &lt;br media="(min-width: 321px)" data-src="medium480.jpg"&gt;
   &lt;br media="(min-width: 481px)" data-src="large640.jpg"&gt;
   &lt;noscript&gt;&lt;img src="large640.jpg"&gt;&lt;/noscript&gt;
   &lt;p&gt;Image caption&lt;/p&gt;
&lt;/picture&gt;</code></pre>

### Page Widgets

Lazy Load XT makes it possible to lazy-load page <a href="https://github.com/ressio/lazy-load-xt/#widgets">widgets</a> (such as Facebook, Twitter or whatever widget you like). Insert any HTML code in the page using the “widget” add-on when an element becomes visible. Wrap the code in an HTML comment inside of a <code>&lt;div&gt;</code> with an ID attribute, and give the element a <code>data-lazy-widget</code> attribute with the value of that ID:

<pre><code class="language-markup">&lt;!-- Google +1 Button --&gt;
&lt;div data-lazy-widget="gplus" class="g-plusone" data-annotation="inline" data-width="300"&gt;&lt;/div&gt;
&lt;div id="gplus"&gt; &lt;!--

   (function() {
      var po = document.createElement('script'),
      s = document.getElementsByTagName('script')[0];
      po.type = 'text/javascript'; po.async = true;
      po.src = 'https://apis.google.com/js/platform.js';
      s.parentNode.insertBefore(po, s);
   })();

--&gt;&lt;/div&gt;</code></pre>

If the <code>data-lazy-widget</code> attribute has an empty value, then the element itself will be used as a wrapper:

<pre><code class="language-markup">&lt;div data-lazy-widget&gt;&lt;!--
   <img loading="lazy" decoding="async" src="image.jpg" />
--&gt;&lt;/div&gt;</code></pre>

Many other add-ons are available, too. They include infinite scrolling, support for background images, loading all images before displaying them (if the browser supports it), and deferring the autoloading of all images.</p>

## Is There A Silver Bullet?

Lazy loading images is not a standard browser feature today. Also, no third-party browser extensions exist for such functionality.

One might assume that the <code>lazyload</code> attribute in the “<a href="https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/ResourcePriorities/Overview.html">Resource Priorities</a>” draft specification by Microsoft and Google would do it. However, it has another purpose: to set the background priority for a corresponding resource element (image, video, script, etc.). Thus, if your aim is to load JavaScript or CSS before images, that’s your choice. There is another killer attribute, <code>postpone</code>, which prevents any resource from loading until you set the CSS <code>display</code> property to a value other than <code>none</code>. The good news is that support for the <code>lazyload</code> attribute is in Internet Explorer 11. The bad news is that the <code>postpone</code> attribute has not been implemented yet.

We do not know when or if the draft specification above will ever be fully supported by the major browsers. So, let’s look at the solutions we have now.

Some people have attempted to solve the duplication of the <code>&lt;img&gt;</code> tag in <code>&lt;noscript&gt;</code> tags by keeping only the <code>&lt;noscript&gt;</code> part and processing it with JavaScript. Unfortunately, <code>&lt;noscript&gt;</code> has no content in Internet Explorer, and it is not included in the DOM at all in Android’s stock browser (other browsers may behave similarly).

An alternative would be to use the <code>&lt;script&gt;</code> tag, instead of <code>&lt;noscript&gt;</code>, like so:

<pre><code class="language-markup">&lt;script&gt;function Z(){document.write('&lt;br ');}&lt;/script&gt;
&lt;script&gt;Z();&lt;/script&gt;&lt;img src="path" attributes /&gt;</code></pre>

So, <code>&lt;img&gt;</code> would be an attribute of the <code>&lt;br&gt;</code> tag and would transform <code>&lt;br&gt;</code> tags into <code>&lt;img data-src&gt;</code> at the <code>document.ready</code> event. But this method requires <code>document.write</code> and is not compatible with AJAX-based navigation. We have implemented this method in the script add-on for Lazy Load XT, but the standard way using <code>data-attributes</code> seems to be clearer.

Finally, Mobify has an elegant <a href="https://hacks.mozilla.org/2013/03/capturing-improving-performance-of-the-adaptive-web/">Capturing API</a> (see the recent <a href="https://www.smashingmagazine.com/2013/10/24/automate-your-responsive-images-with-mobify-js/">review on Smashing Magazine</a>) that transforms HTML into plain text using the following code and then processes it with JavaScript:

<pre><code class="language-javascript">document.write('&lt;plaintext style="display:none"&gt;');</code></pre>

Unfortunately, this solution has drawbacks of its own: It is quite slow, and the browser might treat it as a JavaScript-based HTML parser. Also, combining this solution with AJAX navigation is not clear, and it is not guaranteed to work correctly in all browsers because the <code>&lt;plaintext&gt;</code> tag was deprecated in HTML 2. It actually doesn’t work in W3C’s Amaya browser and on some feature phones (such as Nokia E70). Nevertheless, these are edge cases, and you may use Mobify.js and Lazy Load XT simultaneously, although that is beyond the scope of this article.</p>

## Comparing Lazy Load Solutions

Both Lazy Load XT and the original Lazy Load are not the only solutions around. Below we compare most of the major existing solutions:

Feature<a href="https://www.appelsiini.net/projects/lazyload">LazyLoad for jQuery</a><a href="https://ressio.github.io/lazy-load-xt/">Lazy Load XT</a><a href="https://luis-almeida.github.io/unveil/">Unveil</a><a href="https://jquery.eisbehr.de/lazy/">Lazy</a> (by Eisbehr)<a href="https://github.com/jetmartin/responsive-lazy-loader">Responsive Lazy Loader</a><a href="https://dinbror.dk/blazy/">bLazy</a><a href="https://vvo.github.io/lazyload/">Lazyload</a> (by VVO)<a href="https://toddmotto.com/echo-js-simple-javascript-image-lazy-loading/">Echo</a><br>
<table class="tablesaw">
<thead></thead>
<tbody>
<tr>
<td><strong>Current version</strong></td>
<td>1.9.3</td>
<td>1.0.5</td>
<td>1.3.0</td>
<td>0.3.7</td>
<td>0.1.7</td>
<td>1.2.2</td>
<td>2.1.3</td>
<td>1.5.0</td>
</tr>
<tr>
<td><strong>Dependencies</strong></td>
<td>jQuery</td>
<td>jQuery, Zepto or DOMtastic</td>
<td>jQuery or Zepto</td>
<td>jQuery</td>
<td>jQuery</td>
<td>—</td>
<td>—</td>
<td>—</td>
</tr>
<tr>
<td><strong>Size (Gzip’ed)</strong></td>
<td>1.19 KB</td>
<td>1.31 KB (or 1.45 KB with extras)</td>
<td>338 B</td>
<td>1.45 B</td>
<td>1.23 KB</td>
<td>1.24 KB</td>
<td>1.01 KB</td>
<td>481 B</td>
</tr>
<tr>
<td><strong>Skips images above the fold</strong></td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
</tr>
<tr>
<td><strong>Loading effects</strong></td>
<td>yes</td>
<td>yes</td>
<td>yes (with custom code)</td>
<td>yes</td>
<td>yes (with custom code)</td>
<td>yes (with custom code)</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<td><strong>Responsive images</strong></td>
<td>no</td>
<td>yes (via plugin)</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>yes (with custom code)</td>
<td>no</td>
</tr>
<tr>
<td><strong>Supports scroll containers</strong></td>
<td>yes</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<td><strong>Supports horizontal scrolling</strong></td>
<td>yes</td>
<td>yes</td>
<td>no</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<td><strong>Throttling</strong></td>
<td>no</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<td><strong>Lazy background images</strong></td>
<td>yes</td>
<td>yes (via plugin)</td>
<td>no</td>
<td>yes</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<td><strong>Lazy &lt;video&gt; tag</strong></td>
<td>no</td>
<td>yes</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<td><strong>Lazy iframes</strong></td>
<td>no</td>
<td>yes</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<td><strong>Supports Opera Mini</strong></td>
<td>no</td>
<td>yes</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
</tbody>
</table>

## Conclusion

The total size of media elements on the average web page is increasing constantly. Yet, especially on mobile devices, performance bottlenecks remain, which stem from bandwidth issues, widely varying network latency, and limitations on memory and the CPU. We need solutions for better and faster browsing experiences that work across all devices and browsers.

While no single lazy-load standard exists so far, we welcome you to try Lazy Load XT, especially if lazy-loaded video or other media is an important part of your website's functionality.</p>

### Download and Contribute

*   [Lazy Load XT](https://ressio.github.io/lazy-load-xt/)
*   [Lazy Load XT](https://github.com/ressio/lazy-load-xt), GitHub
*   [jquery.lazyloadxt.min.js](https://raw.github.com/ressio/lazy-load-xt/master/dist/jquery.lazyloadxt.min.js) and [jquery.lazyloadxt.extra.min.js](https://raw.github.com/ressio/lazy-load-xt/master/dist/jquery.lazyloadxt.extra.min.js)
*   [Demos of Lazy Load XT](https://ressio.github.io/lazy-load-xt/demo/)

Bug reports, patches and feature requests are welcome.

{{< signature "al, ml" >}}

