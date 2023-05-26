---
title: Push Your Web Design Into The Future With CSS3
slug: push-your-web-design-into-the-future-with-css3
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf00f006-310a-493b-a6c6-bd93a484ae3a/css.jpg
date: 2009-01-08T15:38:09.000Z
author: chris-spooner
description: >-
  There are exciting new features in the pipeline for Cascading Style Sheets that will allow for an explosion of creativity in Web design. These features include CSS styling rules that are being released with the upcoming CSS3 specification.
categories:
  - Coding
  - CSS
  - CSS3
---
Realistically, you won't be able to use these on your everyday client projects for another few years, but for design blogs and websites aimed at the Web design community, these features can help you push the boundaries of modern Web design today, adding that extra spice to your design and helping the industry move forward.

Also consider the following related articles:

*   [HTML5 and The Future of the Web](https://www.smashingmagazine.com/2009/07/html5-and-the-future-of-the-web/)
*   [Mastering CSS Principles: A Comprehensive Guide](https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/)
*   [The Future Of CSS: Experimental CSS Properties](https://www.smashingmagazine.com/2011/05/the-future-of-css-experimental-css-properties/)

Here are five techniques snatched from the future that you can put into practice in your website designs today.</p>

## 1\. Border Radius

<a href="https://twitter.com/smashingmag"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2604af77-ea63-4a38-9dda-84fe50e6ca8a/border-radius.png" alt="CSS border-radius" /></a>

{{% feature-panel %}}

Probably the most common CSS3 feature currently being used is border-radius. Standard HTML block elements are square-shaped with 90-degree corners. The CSS3 styling rule allows rounded corners to be set.

<pre><code class="language-css">-moz-border-radius: 20px;
          -webkit-border-radius: 20px;
          border-radius: 20px;</code></pre>

Border-radius can also be used to target individual corners, although the syntax for -moz- and -webkit- is slightly different:

<pre><code class="language-css">-moz-border-radius-topleft: 20px;
          -moz-border-radius-topright: 20px;
          -moz-border-radius-bottomleft: 10px;
          -moz-border-radius-bottomright: 10px;
          -webkit-border-top-right-radius: 20px;
          -webkit-border-top-left-radius: 20px;
          -webkit-border-bottom-left-radius: 10px;
          -webkit-border-bottom-right-radius: 10px;</code></pre>

Supported in Firefox, Safari and Chrome.

As used by: <a href="https://twitter.com">Twitter</a>.

See also:

*   [W3C Working Draft](https://www.w3.org/TR/css3-background/#the-border-radius)
*   [Border-radius on CSS3.info](https://www.css3.info/preview/rounded-border/)
*   [The Art of Web](https://www.the-art-of-web.com/css/border-radius/)

## 2\. Border Image

<a href="https://www.blog.spoongraphics.co.uk"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769df4b2-acc8-4d29-bc98-7c9d52a8be11/border-image.png" alt="CSS border-image" /></a>

Border-image, as the name suggests, allows an image file to be used as the border of an object. The image is first created in relation to each side of an object, where each side of the image corresponds to a side of the HTML object. This is then implemented with the following syntax:

<pre><code class="language-css">border: 5px solid #cccccc;
          -webkit-border-image: url(/images/border-image.png) 5 repeat;
          -moz-border-image: url(/images/border-image.png) 5 repeat;
          border-image: url(/images/border-image.png) 5 repeat;</code></pre>

The {border: 5px} attribute specifies the overall width of the border, and then each border-image rule targets the image file and tells the browser how much of the image to use to fill up that 5px border area.

Border images can also be specified on a per-side basis, allowing for separate images to be used on each of the four sides as well as the four corners:

<pre><code class="language-css">border-bottom-right-image
	border-bottom-image
	border-bottom-left-image
	border-left-image
    border-top-left-image
    border-top-image
    border-top-right-image
    border-right-image</code></pre>

Supported in Firefox 3.1, Safari and Chrome.

As used by: <a href="https://www.blog.spoongraphics.co.uk">Blog.SpoonGraphics</a>.

See also:

*   [W3C Working Draft](https://www.w3.org/TR/2002/WD-css3-border-20021107/#the-border-image-uri)
*   [Border-image on CSS3.info](https://www.css3.info/preview/border-image/)
*   [Border-image in Firefox](https://ejohn.org/blog/border-image-in-firefox/)

## 3\. Box Shadow and Text Shadow

<a href="https://24ways.org"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53b8f7b0-e2fa-4494-9359-10d7499d7847/shadow.png" alt="CSS Shadow" /></a>

Drop shadows: don’t you just love them?! They can so easily make or break a design. Now, with CSS3, you don’t even need Photoshop! The usage we've seen so far has really added to the design, a good example being this year's <a href="https://24ways.org">24 Ways website</a>.

<pre><code class="language-css">-webkit-box-shadow: 10px 10px 25px #ccc;
          -moz-box-shadow: 10px 10px 25px #ccc;
          box-shadow: 10px 10px 25px #ccc;</code></pre>

The first two attributes determine the offset of the shadow in relation to the element, in this case, 10 pixels on the x and y axis. The third attribute sets the level of blurriness of the shadow. And finally, the shadow color is set.

Also, the text-shadow attribute is available for use on textual content:

<pre><code class="language-css">text-shadow: 2px 2px 5px #ccc;</code></pre>

Supported in Firefox 3.1, Safari, Chrome (box-shadow only) and Opera (text-shadow only).

As used by: <a href="https://24ways.org">24 Ways</a>.

See also:

*   [W3C Working Draft](https://www.w3.org/TR/css3-background/#the-box-shadow)
*   [Box-shadow on CSS3.info](https://www.css3.info/preview/box-shadow/)
*   [W3C Working Draft](https://www.w3.org/TR/2003/CR-css3-text-20030514/#text-shadows)
*   [Text-shadow on CSS3.info](https://www.css3.info/preview/text-shadow/)

## 4\. Easy Transparency with RGBA and Opacity

<a href="https://24ways.org"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27882032-06b4-42e8-b2ae-ae6e65827962/opacity.png" alt="CSS Opacity" /></a>

The <a href="https://www.smashingmagazine.com/2008/04/16/getting-creative-with-transparency-in-web-design/">use of PNG files in Web design</a> has made transparency a key design feature. Now, an alpha value or opacity rule can be specified directly in the CSS.

<pre><code class="language-css">rgba(200, 54, 54, 0.5);
        /* example: */
        background: rgba(200, 54, 54, 0.5);
        /* or */
        color: rgba(200, 54, 54, 0.5);</code></pre>

The first three numbers refer to the red, green and blue color channels, and the final value refers to the alpha channel that produces the transparency effect.

Alternatively, with the opacity rule, the color can be specified as usual, with the opacity value set as a separate rule:

<pre><code class="language-css">color: #000;
          opacity: 0.5;</code></pre>

Supported in Firefox, Safari, Chrome, Opera (opacity) and IE7 (opacity, with fixes).

As used by: <a href="https://24ways.org">24 Ways</a> (RGBA).

See also:

*   [W3C Working Draft](https://www.w3.org/TR/css3-color/#rgba-color)
*   [RGBA on CSS3.info](https://www.css3.info/preview/rgba/)
*   Pure CSS Opacity

## 5\. Custom Web Fonts with @Font-Face

<a href="https://www.taptaptap.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29f35d2e-fa5d-447f-83fa-448672fe8e46/font-face.png" alt="CSS font-face" /></a>

There has always been a set of safe fonts that can be used on the Web, as you know: Arial, Helvetica, Verdana, Georgia, Comic Sans (ahem…), etc. Now the @font-face CSS3 rule allows fonts to be called from an online directory and used to display text in a whole new light. This does bring up issues of copyright, so there are only a handful of specific fonts that can be used for @font-face embedding.

The styling is put into practice like so:

<pre><code class="language-css">@font-face {
        font-family:'Anivers';
        src: url('/images/Anivers.otf') format('opentype');
        }</code></pre>

The rest of the font family, containing secondary options, is then called as usual:

<pre><code class="language-css">h1 { font-family: ‘Anivers’, Helvetica, Sans-Serif;</code></pre>

Supported in Firefox 3.1, Safari, Opera 10 and IE7 (with <strong>lots</strong> of fixes: if you are brave enough, you can <a href="https://jontangerine.com/log/2008/10/font-face-in-ie-making-web-fonts-work">make font-face work in IE</a> (thanks for heads up, Jon Tan))

As used by: <a href="https://www.taptaptap.com">TapTapTap</a>.

See also:

*   [Font-face in IE, making Web fonts work](https://jontangerine.com/log/2008/10/font-face-in-ie-making-web-fonts-work)
*   [Web fonts, the next big thing - A List Apart](https://www.alistapart.com/articles/cssatten)

Although CSS3 is still under development, the rules listed here are supported by some browsers right now. <a href="https://www.apple.com/safari/">Safari</a> in particular has extensive support for these new features. Unfortunately, despite being a top-quality browser, Safari has a relatively low number of users, so it is probably not worthwhile adding extra features solely for this group of users. But with Apple's Mac computers making their way into everyday life, Safari's usage is likely to continually increase.

<a href="https://getfirefox.com/">Firefox</a>, on the other hand, now has a considerably large user base. What’s more, the soon-to-be-released Firefox 3.1 has added support for a range of CSS3 features. Assuming that most users of Firefox will update their browsers, there will soon be a large group of users with support for these new styling rules.

<a href="https://www.google.com/chrome">Google Chrome</a> was released this year. Based on the WebKit engine, this browser has much of the same support as Safari. While Safari makes up a good proportion of Mac users, Chrome has burst onto the scene, making up a decent proportion of Windows users.

Percentage-wise, the <a href="https://www.w3schools.com/browsers/browsers_stats.asp">W3's browser statistics</a> indicate that, as of November 2008, 44.2% of W3School's users <s>across the Web</s> were browsing with Firefox, 3.1% with Chrome and 2.7% with Safari. That means almost <strong>50% of all Internet users</strong> should be able to view these features. Within the Web design community in particular, which is much more conscious of browser choice, the range of users with CSS3 support is much higher, at <strong>73.6%</strong> (according to the stats at <a href="https://www.blog.spoongraphics.co.uk">Blog.SpoonGraphics</a>).</p>

## 6\. The downside

Your website may now have a range of fancy new design features, but there are a few negatives to take into consideration:

*   **Internet Explorer**: 46% of Internet users won’t see these features, so don’t use them as a crucial part of the design of your website. Make sure that secondary options are in place, such as a standard border in place of border-image <s>and a normal font in place of @font-face</s>. Please notice that Internet Explorer supports `@font-face` with EOT ([more details](https://jontangerine.com/log/2008/10/font-face-in-ie-making-web-fonts-work)) since v4 (_thanks for heads up, Jon Tan_).
*   **Invalid style sheets**: These CSS3 features have not been released as a final specification. They are currently implemented with tags that target different browsers. This can invalidate your style sheet.
*   **Extra CSS markup**: Following the last point, having to add a different tag for each browser to specify the same rule, as well as include the standard rule for the final CSS specification, adds a lot of extra code to your CSS markup.
*   **Potentially horrific usage**: Just as is done with traditional Photoshop filters, the use of these new styling features could result in some eye-wrenching designs. Drop shadows in particular ring warning bells for us; we're not looking forward to seeing the Marketing Department’s choices with that one!

{{< signature "al" >}}

