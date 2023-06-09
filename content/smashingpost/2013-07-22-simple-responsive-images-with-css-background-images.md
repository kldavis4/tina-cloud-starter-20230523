---
title: Simple Responsive Images With CSS Background Images
slug: simple-responsive-images-with-css-background-images
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/644b6440-d895-4b16-8135-ad9892f87691/css-9.jpg
date: 2013-07-22T10:12:22.000Z
author: stephen-thomas
description: >-
  With all the talk of new HTML5 standards such as the `srcset` attribute and
  `<picture>` element, as well as server-side techniques such as Responsive Web
  Design + Server Side Components (RESS), you'd be forgiven for concluding that
  simple, static websites can’t support responsive images today.
categories:
  - Mobile
  - CSS
  - Responsive Design
  - Media Queries
---
<em><strong>Editor's Note</strong>: This article features just one of the many, suboptimal solutions for responsive images. We suggest that you review different approaches before choosing a particular responsive image solution, including these two: <a href="https://www.smashingmagazine.com/2013/05/10/how-to-avoid-duplicate-downloads-in-responsive-images/">How To Avoid Duplicate Downloads In Responsive Images</a> and <a href="https://www.smashingmagazine.com/2013/07/08/choosing-a-responsive-image-solution/">Choosing A Responsive Image Solution</a>.</em>

With all the talk of new HTML5 standards such as the <code>srcset</code> attribute and <a href="https://www.w3.org/TR/html-picture-element/"><code>&lt;picture&gt;</code></a> element, as well as server-side techniques such as <a href="https://www.lukew.com/ff/entry.asp?1392">Responsive Web Design + Server Side Components</a> (RESS), you'd be forgiven for concluding that simple, static websites can’t support responsive images today. That conclusion might be premature, however. In fact, there’s an easy, straightforward way to deliver responsive images that’s supported by all of today’s Web browsers: A CSS background image.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](#further-reading-on-smashingmag)

*   [Automatically Art-Directed Responsive Images? Here You Go.](https://www.smashingmagazine.com/2016/02/automatically-art-directed-responsive-images-go/ "Automatically Art-Directed Responsive Images? Here You Go.")
*   [Responsive Images Now Landed In WordPress Core](https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/ "Responsive Images Now Landed In WordPress Core")
*   [Leaner Responsive Images With Client Hints](https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/ "Leaner Responsive Images With Client Hints")

However, the approach has some limitations, and it doesn’t work in all cases. But if your requirements aren’t complicated, and if you’re willing to make an extra effort to ensure your images are accessible, CSS background images may be all you need.

{{% feature-panel %}}

<strong>In this article we’ll look at the CSS background approach in several steps:</strong>

1.  First, we’ll review the goals and requirements for responsive images.
2.  Then we’ll see how CSS media queries can help identify important characteristics of our users' devices.
3.  We’ll explore the key CSS `background-image` property that lets us respond to those characteristics.
4.  We’ll look at a strategy for optimizing the individual images that make up a responsive set.
5.  We'll examine the limitations of this approach; in many cases there are simple techniques to overcome them.
6.  And finally, we’ll describe the problems with this approach for which there are no workarounds.

Note: This approach requires explicit control of your website’s style sheets as well as its HTML markup. If your website relies on a content management system (CMS), you might not have enough control over those aspects of the website.</p>

## The Need For A Responsive Background Image

Responsive images are an important component of <a href="https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/">responsive Web design</a> (RWD), a design strategy developed by <a href="https://www.abookapart.com/products/responsive-web-design">Ethan Marcotte</a> to cope with the amazing popularity of mobile devices for viewing the Web. Ethan recognized that the previous best practice — developing separate websites for different types of devices — simply couldn’t cope with the astonishing variety of devices Web users might employ to access the websites we build.

RWD takes a completely different approach: create a single website but let that website recognize and respond to its context. If the user has a desktop browser with a wide screen, for example, allow the website content to spread across multiple columns. On a smartphone, however, rearrange the content to confine it to a single column.

In many cases, that’s where responsive design stops — simple adjustments to layout and presentation. If that’s all we consider, however, we’re not honoring the goal of responsive design, and we’re selling our users short.

Truly responding to users’ context requires <strong>a design that considers all aspects of the experience</strong>, and that often includes images. For a real life example, consider a website such as <a href="https://contfont.net">contfont.net</a>. That single page website has one main image and a typical set of HTML, style sheets, fonts, and JavaScript files.
<table class="article-table three-columns"><br>
<tbody>
<tr>
<td><strong>Resource</strong></td>
<td><strong>Type</strong></td>
<td><strong>Compressed Size</strong></td>
</tr>
<tr>
<td>Main page</td>
<td>HTML</td>
<td>6 KB</td>
</tr>
<tr>
<td>Style sheet</td>
<td>CSS</td>
<td>10 KB</td>
</tr>
<tr>
<td>Fonts</td>
<td>Web Font</td>
<td>221 KB</td>
</tr>
<tr>
<td>Scripts</td>
<td>JavaScript</td>
<td>21 KB</td>
</tr>
<tr>
<td>Supporting images</td>
<td>Image</td>
<td>48 KB</td>
</tr>
<tr>
<td>Main site image</td>
<td>Image</td>
<td>??</td>
</tr>
</tbody>
</table>

The website looks gorgeous on computers with super–high-resolution displays because it includes a high-resolution version of the main image. Delivering that image file doesn’t come cheap, though; its 1940 × 1229 pixels make the image 446 KB in size after compression.

The website could use that same image file for all users without compromising the visual experience. Web browsers on smaller devices such as smartphones would resize it to fit the display. While that approach would preserve the visual appeal of the website, the overall user experience would suffer significantly.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3051e4c3-8bb6-4aba-b7b3-a2469c94b96f/example1.png"><img loading="lazy" decoding="async" class="138019 size-full" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a44a0c4-f13f-4449-86fc-c125d2bebb0d/example1-500.png" alt="responsive background image" width="500" height="250" /></a><br>
<em>On an iPhone, a 290 × 183 pixel image that is 18 KB in size looks identical to the 452 KB, 1940 × 1229 pixel image on the MacBook Pro. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3051e4c3-8bb6-4aba-b7b3-a2469c94b96f/example1.png">Larger view</a>.</em>

What does that mean for a user browsing to the website on, say, an earlier generation smartphone? For that user, a 290 × 183 pixel image that is 18 KB in size looks <em>identical</em> to the larger version. Without a responsive image approach, the website <strong>would force the user to download an extra 429 KB of data that is completely wasted</strong>. This excess is not just academic; it has a substantial effect on the website's load time. The smartphone user may be accessing the website over a typical 3G connection at 2 Mb/s. Failing to deliver a responsive image increases the load time from 1.3 seconds to 3 full seconds, significantly more than doubling it!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb6b4e4-d247-481a-9d5a-5ba7844e9d71/load.png"><img title="The full size image takes 3.0 seconds to load over a 3G network, compared to 1.3 seconds for a responsive image." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a09c5b17-d127-40ee-94be-fdbd6f3db24c/load-500.png" alt="The full size image takes 3.0 seconds to load over a 3G network, compared to 1.3 seconds for a responsive image." width="392" height="128" /></a><br>
<em>The full size image takes 3.0 seconds to load over a 3G network, compared to 1.3 seconds for a responsive image. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb6b4e4-d247-481a-9d5a-5ba7844e9d71/load.png">Larger view</a>.</em>

The primary goal for a responsive image approach is simple: <strong>deliver only the pixels that the user’s device can actually use</strong>.

## Identifying The User’s Context

If our websites are going to respond to our users’ context, we need a way to identify that context. Today, CSS offers the most effective way to distinguish different devices. CSS gives us the answers to two critical questions: <strong>what is the size of the user’s display? And does the display support Retina-style images?</strong>

The CSS tool that gives us this information is a <em>media query</em>. Media queries define a set of CSS style properties that apply only to devices with specific qualities. Originally, media queries were limited to media types. The CSS specification defines a large number of them including, for example <code>braille</code> (for braille tactile feedback devices), <code>speech</code> (for speech synthesizers), <code>tty</code> (for devices with only monospaced fonts, such as teletypes) and <code>tv</code> (for television-type devices with low resolution and no scrolling). Currently, the only two media types that most browsers support are <code>print</code> (for printed, paged material) and <code>screen</code> (for computer screens).

CSS3 expanded the use of media queries, however, by allowing style sheets to specify specific features of devices as well as the media type. And in the case of <code>screen</code> devices, the features can include many characteristics of the display, including its width, orientation, resolution and pixel ratio. Those features provide just the information we need to select an appropriate responsive image.

<strong>Here’s how media queries can help us solve the dilemma</strong> of the previous section. As an example, a 15-inch MacBook Pro has a screen width of 1440 pixels (ignoring for the moment the Retina display option). To identify styles that apply to screens of this size (and larger), we can write our style sheet as:

<pre><code class="language-css">@media only screen and (min-width: 1440px) {
    /* styles for MacBook Pro-sized screens and larger */
}
</code></pre>

Any styles defined in that block will only apply when the user accesses the Web page using a device with a screen size of 1440 pixels. There’s a catch, though. The media screen size doesn’t apply to the device’s hardware; rather, it applies to the Web browser’s <em>viewport</em>. The viewport is the size of the browser window after subtracting any browser chrome, such as toolbars.

Unless the user is browsing in full screen mode, the browser window will actually be somewhat less than 1440 pixels in width. For this more common case, therefore, we might want to rewrite the style sheet a bit. Perhaps 1200 pixels is more realistic.

<pre><code class="language-css">@media only screen and (min-width: 1200px) {
    /* styles for wide screens */
}
</code></pre>

The media query has two parts. The first part, <code>only screen</code>, indicates that the styles shouldn’t apply to printed copies of the page or other non-standard devices. (The <code>only</code> keyword doesn’t actually affect the media query; it’s there strictly for really old browsers that don’t support media features. Because those browsers don’t understand the <code>only</code> syntax, they’ll simply ignore the entire block of styles.) The second part of the query, <code>min-width: 1200px</code>, gives the minimum screen width at which the styles will be applied. The <code>and</code> that joins those parts means that both must be true for the styles to apply.

<strong>We can use a similar technique to define styles for portrait-mode smartphones.</strong>

<pre><code class="language-css">@media only screen and (max-width: 320px) {
    /* styles for narrow screens */
}
</code></pre>

In this case we can go ahead and use the actual device screen size in the query. Web browsers on smart phones are always full-screen width.

The <code>min-width</code> and <code>max-width</code> feature specifications make it easy to determine the width of the user’s device. Unfortunately, identifying a Retina display isn’t quite as straightforward. Different browsers use different syntaxes for this feature, so we must resort to vendor prefixes. To make things slightly worse, many versions of Firefox had a bug in their syntax, so we need to use both a fixed and a "broken" syntax for Mozilla browsers. As of now, the recommended query for Retina-quality displays looks like the following.

<pre><code class="language-css">@media
only screen and (-webkit-min-device-pixel-ratio: 2),
only screen and (min--moz-device-pixel-ratio: 2),
only screen and (-moz-min-device-pixel-ratio: 2),
only screen and (-o-min-device-pixel-ratio: 2/1),
only screen and (min-device-pixel-ratio: 2),
only screen and (min-resolution: 192dpi),
only screen and (min-resolution: 2dppx) {
    /* styles for Retina-type displays */
}
</code></pre>

Eventually browsers will all support the standard <em>dots per pixel</em> notation (<code>dppx</code>) and we can drop the vendor prefixes from our style sheets.

## The CSS Background-Image Property

If CSS can reliably identify a user’s context, you might think it would be easy to support responsive images. One approach that might seem logical would be to set <code>display: none</code> for those images we don’t wish to download. Here’s an attempt based strictly on screen size. (We’re omitting Retina considerations for brevity.)

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
    &lt;head&gt;
        &lt;meta charset="utf-8"&gt;
        &lt;title&gt;&lt;/title&gt;
        &lt;style&gt;
        img.smallscreen { display: none; }
        @media only screen and (max-width: 320px) {
            img {
                display: none;
            }
            img.smallscreen {
                display: inline;
            }
        }
        &lt;/style&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;img src="largeimage.jpg"&gt;
        &lt;img class="smallscreen" src="smallimage.jpg&gt;
    &lt;/body&gt;
&lt;/html&gt;
</code></pre>

The code above <em>will</em> display the correct image based on the screen size; however, the <code>display: none</code> property won’t actually prevent browsers from downloading the hidden images. Smartphone browsers will download the large image even though it’s never displayed. Unfortunately, this obvious approach doesn’t accomplish the main goal for responsive images.

The problem occurs because browsers handle the HTML separately from the CSS. The HTML markup requests two image files, so the browser dutifully fetches both. Afterwards, it parses the CSS styles only to discover that one of the images is not displayed, but by then it's too late.

<strong>Our CSS media queries will only work if we can use them strictly for CSS properties</strong> and not HTML content. That may seem impossible, but it turns out that there is a sneaky way to only use CSS for imagery — the <code>background-image</code> property. Here’s how we do that:

1.  In the HTML markup, don’t include references to any image files. Instead simply use empty `<div>` or `<span>` elements.
2.  Place an image in the empty `<div>` or `<span>` by setting its `background-image` property.
3.  Use media queries to substitute the appropriate responsive images, depending on screen size and resolution.

Using these rules, we can modify the above example so that responsive images actually work correctly.

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
    &lt;head&gt;
        &lt;meta charset="utf-8"&gt;
        &lt;title&gt;&lt;/title&gt;
        &lt;style&gt;
        #image {
            background-image: url(largeimage.jpg);
        }
        @media only screen and (max-width: 320px) {
            #image {
                background-image: url(smallimage.jpg);
            }
        }
        &lt;/style&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;div id="image"&gt;&lt;/div&gt;
    &lt;/body&gt;
&lt;/html&gt;
</code></pre>

That, in a nutshell, is how to support responsive images with CSS background images. Any real application will require a bit more code (for example, we need some way to indicate the image size). The additional code, however, is standard CSS without any tricks.</p>

## Creating The Responsive Images

With an understanding of how to use responsive images, the next step is actually creating the image variations. The original source image should have the highest resolution possible, at least as high as the most detailed image your website will deliver. (In the case of <a href="https://contfont.net">contfont.net</a>, the source image is 3888 × 2592 pixels.) Your graphics program of choice should be able to resize that source image to fit your website's breakpoints.

As long as you’re working in your graphics program, <strong>be sure to optimize even the high-resolution images as much as possible</strong>, for example, by using the lowest quality setting feasible for the image. Even users on high-resolution displays will appreciate the faster page load time. If the image is in JPEG format, you can also enable the progressive option when you export it. This option lets the browser display a low-fidelity version of the image quickly while it continues to download the full image.

When it comes to the breakpoints themselves, you shouldn’t fall into the temptation of using the same breakpoints for your images as you’re using for the website’s layout. It’s rarely the case that the best layout breakpoints are also the best image breakpoints. Instead, optimize your image breakpoints for the image. Here’s a strategy I like for finding the optimum image sizes.

First determine the smallest resolution image that is practical for your website to deliver. In the case of <a href="https://contfont.net">contfont.net</a>, the smallest practical viewport size is 320 pixels, corresponding to a non-Retina iPhone in portrait orientation. (Devices with smaller viewports exist, and are likely to exist in the future — smart watches, anyone? — but those devices aren’t likely to visit the website.) On the <a href="https://contfont.net">contfont.net</a> website, a viewport size of 320 pixels leaves 290 pixels for the image width, so the lowest resolution image we need is 290 × 183 pixels. Have your graphics program resize the source image to that size.

Next create a simple test page for that image. Here’s the markup I use:

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
    &lt;head&gt;
        &lt;meta charset="utf-8"&gt;
        &lt;title&gt;&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;img src="test.jpg" width="100%"&gt;
        &lt;p&gt;Window size: &lt;span id="size"&gt;&lt;/span&gt; pixels&lt;/p&gt;
        &lt;script&gt;
        window.onresize = function() {
            document.getElementById("size").innerHTML = window.innerWidth;
        };
        &lt;/script&gt;
    &lt;/body&gt;
&lt;/html&gt;
</code></pre>

This page displays the test image and the current window size. Open it in your browser, and resize the browser window so that its width is about the size of your smallest breakpoint. Because the test image matches this width, it should look fine.

Now slowly resize your browser window by increasing its width. As the width grows, the browser will automatically interpolate and resize the image. As the amount of interpolation increases, the image quality suffers and, at some point, the image will look unacceptably poor. Note the screen width when that point occurs, as that screen width is your first breakpoint.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cc690db-937c-4c10-a9b9-017d46e4dc9d/test.png"><img title="Resize your browser window until the width at which the image looks unacceptably poor. That screen width will be your breakpoint." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab5c3196-f855-4ff8-a727-9ff259c49598/test-500.png" alt="Resize your browser window until the width at which the image looks unacceptably poor. That screen width will be your breakpoint." width="466" height="487" /></a><br>
<em>Resize your browser window until the width at which the image looks unacceptably poor. That screen width will be your breakpoint. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cc690db-937c-4c10-a9b9-017d46e4dc9d/test.png">Larger view</a>.</em>

When you’ve found the first breakpoint, use your graphics program to create a new test image at that size from the original source. Repeat the process with the new test image to find the next breakpoint, and continue until you’ve reached the maximum viewport width your website will support.

At this point you’ll have your image breakpoints and a set of images to match. For Retina displays, create additional images at double resolution. Here’s the full list of images for the <a href="https://contfont.net">contfont.net</a> website:
<table class="article-table three-columns">
<tbody>
<tr>
<td><strong>Image File</strong></td>
<td><strong>Resolution</strong></td>
<td><strong>Size (no compression)</strong></td>
</tr>
<tr>
<td><code>candc290.jpg</code></td>
<td>290 × 183</td>
<td>19,378 Bytes</td>
</tr>
<tr>
<td><code>candc290@2x.jpg</code></td>
<td>290 × 183 (Retina)</td>
<td>56,277 Bytes</td>
</tr>
<tr>
<td><code>candc538.jpg</code></td>
<td>538 × 341</td>
<td>52,914 Bytes</td>
</tr>
<tr>
<td><code>candc538@2x.jpg</code></td>
<td>538 × 341 (Retina)</td>
<td>159,867 Bytes</td>
</tr>
<tr>
<td><code>candc970.jpg</code></td>
<td>970 × 614</td>
<td>132,766 Bytes</td>
</tr>
<tr>
<td><code>candc970@2x.jpg</code></td>
<td>970 × 614 (Retina)</td>
<td>451,939 Bytes</td>
</tr>
</tbody>
</table>

You can use this approach separately for each image on your website, as there’s no reason that all images have to use the same breakpoints. If your website has a lot of images, however, it might be more efficient to find some common breakpoints using a few of the website’s images and then repeat those breakpoints for all of the images on the website.</p>

## Overcoming Limitations

In the simplest cases, the steps above are all it takes to support responsive images. Of course, websites are rarely that simple, and, indeed, there are several steps we can take to improve the approach.</p>

### Making Images Accessible

The standard <code>&lt;img&gt;</code> tag supports an <code>alt</code> attribute that provides an alternative, textual description of the image. That description is important for accessible websites, as users with screen readers rely on the <code>alt</code> content to describe the image. CSS background images don’t have an <code>&lt;img&gt;</code> tag and thus no <code>alt</code> attribute, but we can still make them accessible to vision-impaired users. To do that, we add two additional attributes to our markup.

<pre><code class="language-markup">&lt;div id="image" role="img" aria-label="Textual Description"&gt;&lt;/div&gt;
</code></pre>

The first extra attribute, <code>role</code>, lets screen readers know that the <code>&lt;div&gt;</code> is serving the role of an <code>&lt;img&gt;</code> tag, even though it’s not explicit in the markup. The second attribute, <code>aria-label</code> serves the same purpose as an <code>alt</code> attribute in an <code>&lt;img&gt;</code>. With those two additions, screen readers can announce to their users that the element is an image, and they will read the alternate text description that you've provided for that image.</p>

### Scaling Images in the Browser

There’s another helpful property of the <code>&lt;img&gt;</code> tag that our simple approach doesn’t support: automatic sizing and scaling by the browser. With a standard <code>&lt;img&gt;</code>, we can simply set the width as a percentage of the containing element and the browser automatically calculates the width and scales the height proportionally. For example, consider the fragment below displaying the image file <code>image.jpg</code> which has natural dimensions of 600 × 300 pixels.

<pre><code class="language-markup">&lt;div style="width: 400px"&gt;
    &lt;img src="image.jpg"&gt;
&lt;/div&gt;
</code></pre>

The browser automatically fits the image into the containing <code>&lt;div&gt;</code>, reducing its width from 600 to 400 pixels. It also preserves the image’s aspect ratio, scaling the image height from 300 to 200 pixels at the same time. The result is an undistorted image that fits perfectly on the page.

Thanks to <a href="https://heygrady.com/blog/2012/05/25/responsive-images-without-javascript/">an approach first described by Grady Kuhnline</a>, we can achieve the same effect with a CSS background image for modern browsers. (Warning: The approach this subsection describes does not work in Internet Explorer version 8 and below, as those browsers don’t support the necessary CSS properties.)

The easiest part to tackle is scaling the width. As with the <code>&lt;img&gt;</code> tag we can set our element within a <code>&lt;div&gt;</code> of fixed width; we just have to explicitly indicate that the background should fill that <code>&lt;div&gt;</code>. The HTML markup doesn’t look very different.

<pre><code class="language-markup">&lt;div style="width: 400px"&gt;
    &lt;span id="image"&gt;&lt;/span&gt;
&lt;/div&gt;
</code></pre>

We have to combine several CSS properties to set the width; let’s take them one at a time:

1.  Set the `display` property of the `#image` element to `inline-block`. Without this property, CSS will display the `<span>` element as `inline` and we won’t be able to give it a width or (in a minute) a height.
2.  Set the `width` of that element to `100%` so that our image fills the containing `<div>`.
3.  Set the `font-size` and `line-height` properties to `0` so that any contents within the `span` don’t factor into its size.
4.  Set the `vertical-align` property to `middle` to vertically center the image element in the containing `<div>`.
5.  Set the `background-size` property to `100%` so our image fills the image element.
6.  Set the `background-position` property to `50% 50%` to align the background image within the image element.
7.  Set the `background-repeat` property to `no-repeat` to prevent the browser from tiling the image horizontally or vertically.

The resulting CSS sets the styles for the image element (the <code>&lt;span&gt;</code> element with an <code>id</code> of <code>"image"</code>).

<pre><code class="language-css">#image {
    display: inline-block;
    width: 100%;
    font-size: 0;
    line-height: 0;
    vertical-align: middle;
    background-size: 100%;
    background-position: 50% 50%;
    background-repeat: no-repeat;
    background-image: url(image.jpg);
}
</code></pre>

Those steps take care of giving the image a width, but we haven’t yet tackled the height. Nothing in the above markup or styles tells the browser the height of the image element. As a result, it will default to its natural height which is, alas, zero, as there is no actual content in the <code>&lt;span&gt;</code>. Fortunately, we can fix that with a few minor additions.

First we need to add an extra <code>&lt;span&gt;</code> element to our markup. This extra element is placed <em>within</em> the image element.

<pre><code class="language-markup">&lt;div style="width: 400px"&gt;
    &lt;span id="image"&gt;
        &lt;span id="image-inner"&gt;
        &lt;/span&gt;
    &lt;/span&gt;
&lt;/div&gt;
</code></pre>

Now we define a few style properties for this inner <code>&lt;span&gt;</code>.

1.  Set its `display` property to `block` so it will have a height and width.
2.  Set its `height` to `0` since it doesn’t have any actual content.
3.  Add a `padding-top` property specifying a percentage equal to the height-to-width ratio of the image.

That last step is the key. Even though the <code>&lt;span&gt;</code> inherits no height from its content, <code>padding-top</code> forces the element to take up vertical space. Furthermore, the <code>padding-top</code> property accepts percentage values where the percentage is relative to the element’s width. Our image is 970 × 614 pixels, so the percentage value we use is (614 ÷ 970) × 100%, or 63.3%. Now the browser will ensure that our image maintains its aspect ratio as it’s scaled up or down.

<pre><code class="language-css">#image-inner {
    display: block;
    height: 0;
    padding-top: 63.3%;
}
</code></pre>

## All Together Now

To see how all these components fit together, here is the code for the <a href="https://contfont.net">contfont.net</a> website we’ve used as an example. First is the HTML markup that includes the main website image.

<pre><code class="language-markup">&lt;div class="hero"&gt;
    &lt;span id="cafe" role="img" aria-label="Coffee and croissant."&gt;
        &lt;span class="inner"&gt;
        &lt;/span&gt;
    &lt;/span&gt;
&lt;/div&gt;
</code></pre>

The style sheet defines properties that make the image scale proportionally.

<pre><code class="language-css">.hero #cafe {
    width: 100%;
    display: inline-block;
    vertical-align: middle;
    font: 0/0 serif;
    text-shadow: none;
    color: transparent;
    background-size: 100%;
    background-position: 50% 50%;
    background-repeat: no-repeat;
}
.hero #cafe .inner {
    padding-top: 63.35%; /* height/width of image */
    display: block;
    height: 0;
}
</code></pre>

And finally, a set of media queries pick the appropriate image file based on the user’s context. (The example below omits vendor prefixes for brevity.)

<pre><code class="language-css">/* default screen, non-retina */
.hero #cafe { background-image: url("../img/candc970.jpg"); }

@media only screen and (max-width: 320px) {
    /* Small screen, non-retina */
    .hero #cafe { background-image: url("../img/candc290.jpg"); }
}
@media
only screen and (min-resolution: 2dppx) and (max-width: 320px) {
    /* Small screen, retina */
    .hero #cafe { background-image: url("../img/candc290@2x.jpg"); }
}
@media only screen and (min-width: 321px) and (max-width: 538px) {
    /* Medium screen, non-retina */
    .hero #cafe { background-image: url("../img/candc538.jpg"); }
}
@media
only screen and (min-resolution: 2dppx) and (min-width: 321px) and (max-width: 538px) {
    /* Medium screen, retina */
    .hero #cafe { background-image: url("../img/candc538@2x.jpg"); }
}
@media
only screen and (min-resolution: 2dppx) and (min-width: 539px) {
    /* Large screen, retina */
    .hero #cafe { background-image: url("../img/candc970@2x.jpg"); }
}
</code></pre>

## Potential Problems

CSS background images are a convenient way to deliver responsive images today, but the approach isn’t perfect. At a basic level, it violates one of the fundamental philosophies of modern Web standards — separating content from presentation. Advanced versions of the approach also suffer from browser compatibility concerns, and the approach doesn’t address some of the deeper problems with responsive images in general.</p>

### Separation of Style and Content

CSS was developed specifically to separate style from content. On the modern web, HTML pages provide all of a website's content, while style sheets only affect the presentation of that content. Style sheets should not define the content itself. Of course, the separation between style and content has already been breached somewhat with the CSS <code>content-before</code> and <code>content-after</code> properties, but those properties are typically used to enhance the presentation (for example, by adding an icon to an element).

Specifying primary website images with CSS is a different level entirely. By specifying primary content with CSS rather than HTML, we make our websites harder to troubleshoot, we make them more difficult to maintain and we create barriers for systems that might try to parse our websites automatically.

Unfortunately, there really is no getting around this problem. If strict separation of style and content is important to you, then you’ll have to consider alternative approaches for responsive images.</p>

### Browser Support for Scaled Images

As noted above, the enhancements we added to the basic approach for scaled images won’t work in Internet Explorer version 8 and below. Standardized approaches such as <code>srcset</code> may be backwards compatible with such browsers, but, of course, <code>srcset</code> itself isn’t available on any mainstream browser today.

If you need to support IE8 right now, you might consider creating a separate style sheet for IE8 that specifies fixed image sizes rather than scaling the images. Of course you’ll want to include that style sheet within an IE conditional comment so that other browsers won’t see it.</p>

### The Real Problem of User Context

Perhaps the most fundamental problem with this approach is a problem with responsive images in general. We’re using screen width and pixel density to determine user context, but it’s not clear that such an approach is always appropriate. Consider, for example, a notebook user accessing the Web via a smartphone’s Wi-Fi hotspot.

<img loading="lazy" decoding="async" class="138099" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbdd5e15-e423-4ecb-ae6e-63f9ac4f92f2/responsive-500-mini.png" alt="Accessing the Web via a smartphone’s Wi-Fi hotspot." width="500" height="129" />

That user’s Web browser will show all the characteristics of a high-density, wide-screen device, and a responsive website will delivery large, high-resolution images. Anything less will look poor on our user’s display, but these images may take a long time to load over a wireless network. They could significantly increase the website’s load time, and they may ultimately cost our user real money on their wireless bill. Given the choice, they might prefer lower resolution imagery.

It turns out that this problem is a really hard one to solve. <a href="https://www.w3.org/TR/netinfo-api/">Smart people</a> in the Web community are definitely discussing it, but so far there has been little consensus on an practical solution. For now, CSS-based context discovery is the best technique available.</p>

## Acknowledgements

A special thanks to <a href="https://heygrady.com/blog/2012/05/25/responsive-images-without-javascript/">Grady Kuhnline</a> for first describing how to style images that can scale proportionally. Also, the <a href="https://contfont.net">contfont.net</a> website that this article uses as an example is <a href="https://github.com/sathomas/continental/tree/gh-pages">available for reference on github</a>.

{{< signature "cp" >}}

