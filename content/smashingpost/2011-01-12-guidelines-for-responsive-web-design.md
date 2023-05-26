---
title: 'Responsive Web Design: What It Is And How To Use It'
slug: guidelines-for-responsive-web-design
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58bf6358-449a-488b-b42b-8258d98bd3d7/croppinglogo.jpg
date: 2011-01-12T15:22:27.000Z
author: vitaly-friedman
summary: >-
  Get started with responsive Web design! In this article, you’ll find how to respond to the user’s behavior and environment based on screen size, platform and orientation.
description: >-
  Everything you need to know about responsive design to get started. Let’s explore how to respond to the user’s behavior and environment based on screen size, platform, and orientation.  
categories:
  - Coding
  - CSS
  - Responsive Design
  - Media Queries
last_updated: 2018-08-11T11:30:00.000Z
---

Almost every new client these days wants a mobile version of their website. It’s practically essential after all: one design for the BlackBerry, another for the iPhone, the iPad, netbook, Kindle &mdash; and all screen resolutions must be compatible, too. In the next five years, we’ll likely need to design for a number of additional inventions. When will the madness stop? It won’t, of course.

In the field of Web design and development, we’re quickly getting to the point of being unable to keep up with the endless new resolutions and devices. For many websites, creating a website version for each resolution and new device would be impossible, or at least impractical. Should we just suffer the consequences of losing visitors from one device, for the benefit of gaining visitors from another? Or is there another option?

## What is Responsive Web Design?

Responsive Web design is the approach that suggests that design and development should respond to the user’s behavior and environment based on screen size, platform and orientation.

The practice consists of a mix of flexible grids and layouts, images and an intelligent use of CSS media queries. As the user switches from their laptop to iPad, the website should automatically switch to accommodate for resolution, image size and scripting abilities. One may also have to consider the settings on their devices; if they have a [VPN for iOS](https://www.expressvpn.com/vpn-software/vpn-ios) on their iPad, for example, the website should not block the user’s access to the page. In other words, the website should have the technology to automatically *respond* to the user’s preferences. This would eliminate the need for a different design and development phase for each new gadget on the market.

## The Concept Of Responsive Web Design

<a href="https://ethanmarcotte.com/">Ethan Marcotte</a> wrote an introductory article about the approach, <a href="https://www.alistapart.com/articles/responsive-web-design/">Responsive Web Design</a>, for A List Apart. It stems from the notion of responsive architectural design, whereby a room or space automatically adjusts to the number and flow of people within it:
<blockquote>“Recently, an emergent discipline called “responsive architecture” has begun asking how physical spaces can respond to the presence of people passing through them. Through a combination of embedded robotics and tensile materials, architects are experimenting with art installations and wall structures that bend, flex, and expand as crowds approach them. Motion sensors can be paired with climate control systems to adjust a room’s temperature and ambient lighting as it fills with people. Companies have already produced “smart glass technology” that can automatically become opaque when a room’s occupants reach a certain density threshold, giving them an additional layer of privacy.”</blockquote>

Transplant this discipline onto Web design, and we have a similar yet whole new idea. Why should we create a custom Web design for each group of users; after all, architects don’t design a building for each group size and type that passes through it? Like responsive architecture, Web design should automatically adjust. It shouldn’t require countless custom-made solutions for each new category of users.

Obviously, we can’t use motion sensors and robotics to accomplish this the way a building would. Responsive Web design requires a more abstract way of thinking. However, some ideas are already being practiced: fluid layouts, media queries and scripts that can reformat Web pages and mark-up effortlessly (or *automatically*).

But responsive Web design is **not only about adjustable screen resolutions and automatically resizable images**, but rather about a whole new way of thinking about design. Let’s talk about all of these features, plus additional ideas in the making.

{{% feature-panel %}}

## Adjusting Screen Resolution

With more devices come varying screen resolutions, definitions and orientations. New devices with new screen sizes are being developed every day, and each of these devices may be able to handle variations in size, functionality and even color. Some are in landscape, others in portrait, still others even completely square. As we know from the rising popularity of the iPhone, iPad and advanced smartphones, many new devices are able to switch from portrait to landscape at the user’s whim. How is one to design for these situations?

<figure><img loading="lazy" decoding="async" title="Portrait Landscape" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3789918-13c0-41c2-9740-819e18772757/portrait-landscape.jpg" alt="responsive web design - Portrait Landscape" width="550" height="300" /><figcaption>Portrait and landscape modes.</figcaption></figure>

In addition to designing for both landscape and portrait (and enabling those orientations to possibly switch in an instant upon page load), we must consider the hundreds of different screen sizes. Yes, it is possible to group them into major categories, design for each of them, and make each design as flexible as necessary. But that can be overwhelming, and who knows what the usage figures will be in five years? Besides, many users do not maximize their browsers, which itself leaves far too much room for variety among screen sizes.

Morten Hjerde and a few of his colleagues <a href="https://web.archive.org/web/20151223084534/http://sender11.typepad.com/sender11/2008/04/mobile-screen-s.html">identified statistics on about 400 devices</a> sold between 2005 and 2008. Below are some of the most common:

<figure><a href="https://sender11.typepad.com/sender11/2008/04/mobile-screen-s.html"><img loading="lazy" decoding="async" title="Sizes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adc13334-06ab-4732-bb0a-80acb71cda07/sizes.jpg" alt="responsive web design - Sizes" width="550" height="300" /></a><figcaption>Some of the most common screen sizes between 2005 and 2008.</figcaption></figure>

Since then even <a href="https://www.quirksmode.org/mobile/mobilemarket.html">more devices have come out</a>. It’s obvious that we can’t keep creating custom solutions for each one. So, how do we deal with the situation?

### Part of the Solution: Flexible Everything

A few years ago, when flexible layouts were almost a “luxury” for websites, the only things that were flexible in a design were the layout columns (structural elements) and the text. Images could easily break layouts, and even flexible structural elements broke a layout’s form when pushed enough. Flexible designs weren’t really that flexible; they could give or take a few hundred pixels, but they often couldn’t adjust from a large computer screen to a netbook.

Now we can make things more flexible. Images can be automatically adjusted, and we have workarounds so that layouts never break (although they may become squished and illegible in the process). While it’s not a complete fix, the solution gives us far more options. It’s perfect for devices that switch from portrait orientation to landscape in an instant or for when users switch from a large computer screen to an iPad.

In Ethan Marcotte’s article, he created <a href="https://www.alistapart.com/d/responsive-web-design/ex/ex-site-flexible.html">a sample Web design that features this better flexible layout</a>. The entire design is a lovely mix of <a href="https://www.alistapart.com/articles/fluidgrids/">fluid grids</a>, <a href="https://unstoppablerobotninja.com/entry/fluid-images">fluid images</a> and smart mark-up where needed. Creating fluid grids is fairly common practice, and there are a number of techniques for creating fluid images:

*   [Hiding and Revealing Portions of Images](https://zomigi.com/blog/hiding-and-revealing-portions-of-images/)
*   [Creating Sliding Composite Images](https://zomigi.com/blog/creating-sliding-composite-images/)
*   [Foreground Images That Scale With the Layout](https://zomigi.com/blog/foreground-images-that-scale-with-the-layout/)

For more information on creating fluid websites, be sure to look at the book "Flexible Web Design: Creating Liquid and Elastic Layouts with CSS" by Zoe Mickley Gillenwater, and download the sample chapter “<a href="https://www.flexiblewebbook.com/bonus.html">Creating Flexible Images</a>.” In addition, Zoe provides the following extensive list of tutorials, resources, inspiration and best practices on creating flexible grids and layouts: “<a href="https://zomigi.com/blog/essential-resources-for-creating-liquid-and-elastic-layouts/">Essential Resources for Creating Liquid and Elastic Layouts</a>”.

While from a technical perspective this is all easily possible, it’s not just about plugging these features in and being done. Look at the logo in this design, for example:

<figure><a href="https://www.alistapart.com/d/responsive-web-design/ex/ex-site-flexible.html"><img title="Cropping Logo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58bf6358-449a-488b-b42b-8258d98bd3d7/croppinglogo.jpg" alt="Cropping Logo" width="550" height="321" /></a><figcaption>Logo example were the image is divided in two: the background, set to be cropped and to maintain its size, and the other image resized proportionally.</figcaption></figure>

If resized too small, the image would appear to be of low quality, but keeping the name of the website visible and not cropping it off was important. So, the image is divided into two: one (of the illustration) set as a background, to be cropped and to maintain its size, and the other (of the name) resized proportionally.

<pre><code class="language-markup tmp-html">&lt;h1 id="logo"&gt;&lt;a href="#"&gt;&lt;img src="site/logo.png" alt="The Baker Street Inquirer" /&gt;&lt;/a&gt;&lt;/h1&gt;</code></pre>

Above, the <code>h1</code> element holds the illustration as a background, and the image is aligned according to the container’s background (the heading).

This is just one example of the kind of thinking that makes responsive Web design truly effective. But even with smart fixes like this, a layout can become too narrow or short to look right. In the logo example above (although it works), the ideal situation would be to not crop half of the illustration or to keep the logo from being so small that it becomes illegible and “floats” up.

## Flexible Images

One major problem that needs to be solved with responsive Web design is working with images. There are a number of techniques to resize images proportionately, and many are easily done. The most popular option, noted in Ethan Marcotte’s article on <a href="https://unstoppablerobotninja.com/entry/fluid-images/">fluid images</a> but first experimented with by Richard Rutter, is to use CSS’s <code>max-width</code> for an easy fix.

<pre><code class="language-css">img { max-width: 100%; }</code></pre>

As long as no other width-based image styles override this rule, every image will load in its original size, unless the viewing area becomes narrower than the image’s original width. The **maximum width** of the image is set to 100% of the screen or browser width, so when that 100% becomes narrower, so does the image. Essentially, as Jason Grigsby <span class="removed_link" title="https://www.cloudfour.com/css-media-query-for-mobile-is-fools-gold/">noted</span>, "The idea behind fluid images is that you deliver images at the maximum size they will be used at. You don’t declare the height and width in your code, but instead let the browser resize the images as needed while using CSS to guide their relative size". It’s a great and simple technique to resize images beautifully.

Note that <code>max-width</code> is **not supported in IE**, but a good use of <code>width: 100%</code> would solve the problem neatly in an IE-specific style sheet. One more issue is that when an image is resized too small in some older browsers in Windows, the rendering isn’t as clear as it ought to be. There is a JavaScript to fix this issue, though, found in <a href="https://unstoppablerobotninja.com/entry/fluid-images/">Ethan Marcotte’s article</a>.

While the above is a great quick fix and good start to responsive images, image resolution and download times should be the primary considerations. While resizing an image for mobile devices can be very simple, if the original image size is meant for large devices, it could significantly slow download times and take up space unnecessarily.

### Filament Group’s Responsive Images

This technique, presented by the Filament Group, takes this issue into consideration and not only resizes images proportionately, but shrinks image resolution on smaller devices, so very large images don’t waste space unnecessarily on small screens.

<figure><a href="https://filamentgroup.com/lab/responsive_images_experimenting_with_context_aware_image_sizing/"><img title="Filament Group" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0d0c9eb-32cf-49d3-abc4-a4d3de4da18d/filamentgroup.jpg" alt="Filament Group Image Resizing" width="550" height="300" /></a><figcaption>Filament group image resizing.</figcaption></figure>

This technique requires a few files, all of which are available on <a href="https://github.com/filamentgroup/Responsive-Images">Github</a>. First, a JavaScript file (*rwd-images.js*), the *.htaccess* file and an image file (*rwd.gif*). Then, we can use just a bit of HTML to reference both the larger and smaller resolution images: first, the small image, with an *.r* prefix to clarify that it should be responsive, and then a reference to the bigger image using <code>data-fullsrc</code>.

<pre><code class="language-markup tmp-html">&lt;img src="smallRes.jpg" data-fullsrc="largeRes.jpg"&gt;</code></pre>

The <code>data-fullsrc</code> is a custom HTML5 attribute, defined in the files linked to above. For any screen that is wider than 480 pixels, the larger-resolution image (*largeRes.jpg*) will load; smaller screens wouldn’t need to load the bigger image, and so the smaller image (*smallRes.jpg*) will load.

The JavaScript file inserts a base element that allows the page to separate responsive images from others and redirects them as necessary. When the page loads, all files are rewritten to their original forms, and only the large or small images are loaded as necessary. With other techniques, all higher-resolution images would have had to be downloaded, even if the larger versions would never be used. Particularly for websites with a lot of images, this technique can be a great saver of bandwidth and loading time.

This technique is fully supported in modern browsers, such as **IE8+, Safari, Chrome and Opera, as well as mobile devices that use these same browsers** (iPad, iPhone, etc.). Older browsers and Firefox degrade nicely and still resize as one would expect of a responsive image, except that both resolutions are downloaded together, so the end benefit of saving space with this technique is void.

### Stop iPhone Simulator Image Resizing

One nice thing about the iPhone and iPod Touch is that Web designs automatically rescale to fit the tiny screen. A full-sized design, unless specified otherwise, would just shrink proportionally for the tiny browser, with no need for scrolling or a mobile version. Then, the user could easily zoom in and out as necessary.

There was, however, one issue this simulator created. When responsive Web design took off, many noticed that images were still changing proportionally with the page even if they were specifically made for (or could otherwise fit) the tiny screen. This in turn scaled down text and other elements.

<figure><a href="https://thinkvitamin.com/design/responsive-design-image-gotcha/"><img title="iPhone Scale" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28f492c3-bc7c-4091-8fcf-380a0d5f9da0/iphonescale.jpg" alt="iPhone Scale" width="550" height="400" /></a><figcaption>iPhone Scale &mdash; Image: Think Vitamin &ndash; Website referenced: 8 Faces.</figcaption></figure>

Because this works only with Apple’s simulator, we can use an Apple-specific meta tag to fix the problem, placing it *below* the website’s <code>&lt;head&gt;</code> section. Thanks to Think Vitamin’s article on image resizing, we have the meta tag below:

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=device-width; initial-scale=1.0"&gt;</code></pre>

Setting the <code>initial-scale</code> to <code>1</code> overrides the default to resize images proportionally, while leaving them as is if their width is the same as the device’s width (in either portrait or lanscape mode). Apple’s documentation has a lot more information on the <a href="https://developer.apple.com/library/safari/#documentation/appleapplications/reference/safarihtmlref/Articles/MetaTags.html">viewport meta tag</a>.

{{% ad-panel-leaderboard %}}

## Custom Layout Structure

For extreme size changes, we may want to change the layout altogether, either through a separate style sheet or, more efficiently, through a CSS media query. This does not have to be troublesome; most of the styles can remain the same, while specific style sheets can inherit these styles and move elements around with floats, widths, heights and so on.

For example, we could have one main style sheet (which would also be the default) that would define all of the main structural elements, such as <code>#wrapper</code>, <code>#content</code>, <code>#sidebar</code>, <code>#nav</code>, along with colors, backgrounds and typography. Default flexible widths and floats could also be defined.

If a style sheet made the layout too narrow, short, wide or tall, we could then detect that and switch to a new style sheet. This new child style sheet would adopt everything from the default style sheet and then just redefine the layout’s structure.

Here is the ***style.css* (default) content:**

<pre><code class="language-css">/* Default styles that will carry to the child style sheet */

html,body{
   background...
   font...
   color...
}

h1,h2,h3{}
p, blockquote, pre, code, ol, ul{}

/* Structural elements */
#wrapper{
  width: 80%;
  margin: 0 auto;

  background: #fff;
  padding: 20px;
}

#content{
  width: 54%;
  float: left;
  margin-right: 3%;
}

#sidebar-left{
  width: 20%;
  float: left;
  margin-right: 3%;
}

#sidebar-right{
  width: 20%;
  float: left;
}</code></pre>

Here is the ***mobile.css* (child)** content:

<pre><code class="language-css">#wrapper{
  width: 90%;
}

#content{
  width: 100%;
}

#sidebar-left{
  width: 100%;
  clear: both;

  /* Additional styling for our new layout */
  border-top: 1px solid #ccc;
  margin-top: 20px;
}

#sidebar-right{
  width: 100%;
  clear: both;

  /* Additional styling for our new layout */
  border-top: 1px solid #ccc;
  margin-top: 20px;
}</code></pre>


<figure><img title="Moving Content" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4465aaf-bd08-4c46-958c-ff096fda2f2b/movingcontent.jpg" alt="Moving Content" width="550" height="600" /><figcaption>Moving content from wider to narrower screens.</figcaption></figure>

### Media Queries

<a href="https://www.smashingmagazine.com/2010/06/50-new-useful-css-techniques-tools-and-tutorials/">CSS3</a> supports all of the same media types as CSS 2.1, such as <code>screen</code>, <code>print</code> and <code>handheld</code>, but has added dozens of new media features, including <code>max-width</code>, <code>device-width</code>, <code>orientation</code> and <code>color</code>. New devices made after the release of CSS3 (such as the iPad and Android devices) will definitely support media features. So, calling a media query using CSS3 features to target these devices would work just fine, and it will be ignored if accessed by an older computer browser that does not support CSS3.

In Ethan Marcotte’s article, we see an example of a media query in action:

<pre><code class="language-markup tmp-html">&lt;link rel="stylesheet" type="text/css"
  media="screen and (max-device-width: 480px)"
  href="shetland.css" /&gt;</code></pre>

This media query is fairly self-explanatory: if the browser displays this page on a screen (rather than print, etc.), and if the width of the screen (not necessarily the viewport) is 480 pixels or less, then load *shetland.css*.

New CSS3 features also include <code>orientation</code> (portrait vs. landscape), <code>device-width</code>, <code>min-device-width</code> and more. Look at “<a href="https://www.quirksmode.org/blog/archives/2010/04/the_orientation.html">The Orientation Media Query</a>” for more information on setting and restricting widths based on these media query features.

One can create multiple style sheets, as well as basic layout alterations defined to fit ranges of widths &mdash; even for landscape vs. portrait orientations. Be sure to look at the section of Ethan Marcotte’s article entitled “<a href="https://www.alistapart.com/articles/responsive-web-design/">Meet the media query</a>” for more examples and a more thorough explanation.

Multiple media queries can also be dropped right into a single style sheet, which is the most efficient option when used:

<pre><code class="language-css">/* Smartphones (portrait and landscape) ----------- */
@media only screen
and (min-device-width : 320px)
and (max-device-width : 480px) {
/* Styles */
}

/* Smartphones (landscape) ----------- */
@media only screen
and (min-width : 321px) {
/* Styles */
}

/* Smartphones (portrait) ----------- */
@media only screen
and (max-width : 320px) {
/* Styles */
}</code></pre>

The code above is from a free template for multiple media queries between popular devices by Andy Clark. See the differences between this approach and including different style sheet files in the mark-up as described in his book “<a href="https://shop.smashingmagazine.com/products/hardboiled-web-design">Hardboiled Web Design</a>.”

### CSS3 Media Queries

Above are a few examples of how media queries, both from CSS 2.1 and CSS3 could work. Let’s now look at some specific how-to’s for using CSS3 media queries to create responsive Web designs. Many of these uses are relevant today, and all will definitely be usable in the near future.

The **min-width and max-width** properties do exactly what they suggest. The <code>min-width</code> property sets a minimum browser or screen width that a certain set of styles (or separate style sheet) would apply to. If anything is below this limit, the style sheet link or styles will be ignored. The <code>max-width</code> property does just the opposite. Anything above the maximum browser or screen width specified would not apply to the respective media query.

Note in the examples below that we’re using the syntax for media queries that could be used all in one style sheet. As mentioned above, the most efficient way to use media queries is to place them all in one CSS style sheet, with the rest of the styles for the website. This way, multiple requests don’t have to be made for multiple style sheets.

<pre><code class="language-css">@media screen and (min-width: 600px) {
     .hereIsMyClass {
          width: 30%;
          float: right;
     }
}</code></pre>

The class specified in the media query above (<code>hereIsMyClass</code>) will work only if the browser or screen width is above 600 pixels. In other words, this media query will run only if the **minimum width is 600 pixels** (therefore, 600 pixels or wider).

<pre><code class="language-css">@media screen and (max-width: 600px) {
     .aClassforSmallScreens {
          clear: both;
      font-size: 1.3em;
     }
}</code></pre>

Now, with the use of <code>max-width</code>, this media query will apply only to browser or screen widths with a maximum width of 600 pixels or narrower.

While the above <code>min-width</code> and <code>max-width</code> can apply to either screen size or browser width, sometimes we’d like a media query that is relevant to device width specifically. This means that even if a browser or other viewing area is minimized to something smaller, the media query would still apply to the size of the actual device. The **min-device-width and max-device-width** media query properties are great for targeting certain devices with set dimensions, without applying the same styles to other screen sizes in a browser that mimics the device’s size.

<pre><code class="language-css">@media screen and (max-device-width: 480px) {
     .classForiPhoneDisplay {
          font-size: 1.2em;
     }
}</code></pre>

<pre><code class="language-css">@media screen and (min-device-width: 768px) {
     .minimumiPadWidth {
          clear: both;
      margin-bottom: 2px solid #ccc;
     }
}</code></pre>

For the iPad specifically, there is also a media query property called **orientation**. The value can be either landscape (horizontal orientation) or portrait (vertical orientation).

<pre><code class="language-css">@media screen and (orientation: landscape) {
     .iPadLandscape {
          width: 30%;
      float: right;
     }
}</code></pre>

<pre><code class="language-css">@media screen and (orientation: portrait) {
     .iPadPortrait {
          clear: both;
     }
}</code></pre>

Unfortunately, this property works only on the iPad. When <a href="https://www.thecssninja.com/css/iphone-orientation-css">determining the orientation for the iPhone</a> and other devices, the use of <code>max-device-width</code> and <code>min-device-width</code> should do the trick.

There are also many media queries that **make sense when combined**. For example, the <code>min-width</code> and <code>max-width</code> media queries are combined all the time to set a style specific to a certain range.

<pre><code class="language-css">@media screen and (min-width: 800px) and (max-width: 1200px) {
     .classForaMediumScreen {
          background: #cc0000;
          width: 30%;
          float: right;
     }
}</code></pre>

The above code in this media query applies only to screen and browser widths between 800 and 1200 pixels. A good use of this technique is to show certain content or entire sidebars in a layout depending on how much horizontal space is available.

Some designers would also prefer to **link to a separate style sheet** for certain media queries, which is perfectly fine if the organizational benefits outweigh the efficiency lost. For devices that do not switch orientation or for screens whose browser width cannot be changed manually, using a separate style sheet should be fine.

You might want, for example, to place media queries all in one style sheet (as above) for devices like the iPad. Because such a device can switch from portrait to landscape in an instant, if these two media queries were placed in separate style sheets, the website would have to call each style sheet file every time the user switched orientations. Placing a media query for both the horizontal and vertical orientations of the iPad in the same style sheet file would be far more efficient.

Another example is a flexible design meant for a standard computer screen with a resizable browser. If the browser can be manually resized, placing all variable media queries in one style sheet would be best.

Nevertheless, organization can be key, and a designer may wish to define media queries in a standard HTML link tag:

<div class="break-out">

 <pre><code class="language-markup tmp-html">&lt;link rel="stylesheet" media="screen and (max-width: 600px)" href="small.css" /&gt;
&lt;link rel="stylesheet" media="screen and (min-width: 600px)" href="large.css" /&gt;
&lt;link rel="stylesheet" media="print" href="print.css" /&gt;
</code></pre>
</div>

### JavaScript

Another method that can be used is JavaScript, especially as a back-up to devices that don’t support all of the CSS3 media query options. Fortunately, there is already a pre-made JavaScript library that makes older browsers (IE 5+, Firefox 1+, Safari 2) support CSS3 media queries. If you’re already using these queries, just grab a copy of the library, and include it in the mark-up: <a href="https://code.google.com/p/css3-mediaqueries-js/">*css3-mediaqueries.js*</a>.

In addition, below is a sample jQuery snippet that detects browser width and changes the style sheet accordingly &mdash; if one prefers a more hands-on approach:

<div class="break-out">

 <pre><code class="language-javascript">&lt;script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"&gt;&lt;/script&gt;

&lt;script type="text/javascript"&gt;
  $(document).ready(function(){
    $(window).bind("resize", resizeWindow);
    function resizeWindow(e){
      var newWindowWidth = $(window).width();

      // If width width is below 600px, switch to the mobile stylesheet
      if(newWindowWidth &lt; 600){        $("link[rel=stylesheet]").attr({href : "mobile.css"});        }       // Else if width is above 600px, switch to the large stylesheet       else if(newWindowWidth &gt; 600){
        $("link[rel=stylesheet]").attr({href : "style.css"});
      }
    }
  });
&lt;/script&gt;
</code></pre>
</div>

There are many solutions for pairing up JavaScript with CSS media queries. Remember that media queries are not an absolute answer, but rather are fantastic options for responsive Web design when it comes to pure CSS-based solutions. With the addition of JavaScript, we can accomodate far more variations. For detailed information on using JavaScript to mimic or work with media queries, look at “<a href="https://www.quirksmode.org/blog/archives/2010/08/combining_media.html">Combining Media Queries and JavaScript</a>.”

## Showing or Hiding Content

It is possible to shrink things proportionally and rearrange elements as necessary to make everything fit (reasonably well) as a screen gets smaller. It’s great that that’s possible, but making every piece of content from a large screen available on a smaller screen or mobile device isn’t always the best answer. We have best practices for mobile environments: simpler navigation, more focused content, lists or rows instead of multiple columns.

<figure><a href="https://digg.com"><img title="Digg Mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22cb73f6-612b-4c61-815f-8a5c118c5c23/diggmobile.jpg" alt="Digg Mobile" width="550" height="425" /></a><figcaption>Show or hide content on different screen sizes.</figcaption></figure>

Responsive Web design shouldn’t be just about how to create a flexible layout on a wide range of platforms and screen sizes. It should also be about the user being able to pick and choose content. Fortunately, CSS has been allowing us to show and hide content with ease for years!

<pre><code class="language-css">display: none;</code></pre>

Either declare <code>display: none</code> for the HTML block element that needs to be hidden in a specific style sheet or detect the browser width and do it through JavaScript. In addition to hiding content on smaller screens, we can also hide content in our default style sheet (for bigger screens) that should be available only in mobile versions or on smaller devices. For example, as we hide major pieces of content, we could replace them with navigation to that content, or with a different navigation structure altogether.

Note that we haven’t used <code>visibility: hidden</code> here; this just hides the content (although it is still there), whereas the <code>display</code> property gets rid of it altogether. For smaller devices, there is no need to keep the mark-up on the page &mdash; it just takes up resources and might even cause unnecessary scrolling or break the layout.

<figure><img title="Showing Hiding Content" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b58ddd9-5066-4c35-a7b7-baa9386b7c2a/showinghidingcontent.jpg" alt="Showing Hiding Content" width="550" height="600" /><figcaption>Hide content and replace it with links on smaller devices.</figcaption></figure>

Here is **our mark-up**:

<div class="break-out">

 <pre><code class="language-markup tmp-html">&lt;p class="sidebar-nav"&gt;&lt;a href="#"&gt;Left Sidebar Content&lt;/a&gt; | &lt;a href="#"&gt;Right Sidebar Content&lt;/a&gt;&lt;/p&gt;

&lt;div id="content"&gt;
  &lt;h2&gt;Main Content&lt;/h2&gt;
&lt;/div&gt;

&lt;div id="sidebar-left"&gt;
  &lt;h2&gt;A Left Sidebar&lt;/h2&gt;

&lt;/div&gt;

&lt;div id="sidebar-right"&gt;
  &lt;h2&gt;A Right Sidebar&lt;/h2&gt;
&lt;/div&gt;
</code></pre>
</div>

In our default style sheet below, we have hidden the links to the sidebar content. Because our screen is large enough, we can display this content on page load.

Here is the ***style.css* (default)** content:

<pre><code class="language-css">#content{
  width: 54%;
  float: left;
  margin-right: 3%;
}

#sidebar-left{
  width: 20%;
  float: left;
  margin-right: 3%;
}

#sidebar-right{
  width: 20%;
  float: left;
}
.sidebar-nav{display: none;}</code></pre>

Now, we hide the two sidebars (below) and show the links to these pieces of content. As an alternative, the links could call to JavaScript to just cancel out the <code>display: none</code> when clicked, and the sidebars could be realigned in the CSS to float below the content (or in another reasonable way).

Here is the ***mobile.css* (simpler)** content:

<pre><code class="language-css">#content{
  width: 100%;
}

#sidebar-left{
  display: none;
}

#sidebar-right{
  display: none;
}
.sidebar-nav{display: inline;}</code></pre>

With the ability to easily show and hide content, rearrange layout elements and automatically resize images, form elements and more, a design can be transformed to fit a huge variety of screen sizes and device types. As the screen gets smaller, rearrange elements to fit mobile guidelines; for example, use a script or alternate style sheet to increase white space or to replace image navigation sources on mobile devices for better usability (icons would be more beneficial on smaller screens).

### Touchscreens vs. Cursors

Touchscreens are becoming increasingly popular. Assuming that smaller devices are more likely to be given touchscreen functionality is easy, but don’t be so quick. Right now touchscreens are mainly on smaller devices, but many laptops and desktops on the market also have touchscreen capability. For example, the HP Touchsmart tm2t is a basic touchscreen laptop with traditional keyboard and mouse that can transform into a tablet.

<figure><a href="https://www.flickr.com/photos/rrrrred/5134202846/"><img title="Touchscreen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aa6b53a-6f78-4af2-9728-e0d43e2af4fd/touchscreen.jpg" alt="Touchscreen" width="550" height="368" /></a><figcaption>Touchscreen on laptops and desktops.</figcaption></figure>

Touchscreens obviously come with different design guidelines than purely cursor-based interaction, and the two have different capabilities as well. Fortunately, making a design work for both doesn’t take a lot of effort. Touchscreens have no capability to display CSS hovers because there is no cursor; once the user touches the screen, they click. So, don’t rely on CSS hovers for link definition; they should be considered an additional feature only for cursor-based devices.

Look at the article “<a href="/2013/05/gesture-driven-interface/">Designing for Touchscreen</a>” for more ideas. Many of the design suggestions in it are best for touchscreens, but they would not necessarily impair cursor-based usability either. For example, sub-navigation on the right side of the page would be more user-friendly for touchscreen users, because most people are right-handed; they would therefore not bump or brush the navigation accidentally when holding the device in their left hand. This would make no difference to cursor users, so we might as well follow the touchscreen design guideline in this instance. Many more guidelines of this kind can be drawn from touchscreen-based usability.

{{% ad-panel-leaderboard %}}

## A Showcase Of Responsive Web Design

Below we have a few examples of responsive Web design in practice today. For many of these websites, there is more variation in structure and style than is shown in the pairs of screenshots provided. Many have several solutions for a variety of browsers, and some even adjust elements dynamically in size without the need for specific browser dimensions. Visit each of these, and adjust your browser size or change devices to see them in action.

Art Equals Work is a simple yet great example of responsive Web design. The first screenshot below is the view from a standard computer screen dimension. The website is flexible with browser widths by traditional standars, but once the browser gets too narrow or is otherwise switched to a device with a smaller screen, then the layout switches to a more readable and user-friendly format. The sidebar disappears, navigation goes to the top, and text is enlarged for easy and simple vertical reading.

<figure><img title="Art Equals Work" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/771ef7e9-86f4-4825-93c3-bbe3e07c9873/artequalswork1.jpg" alt="Art Equals Work" width="550" height="400" /><figcaption>“Art Equals Work” website view from a standard computer screen dimension.</figcaption></figure>

<figure><a href="https://artequalswork.com/"><img title="Art Equals Work" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2252362c-b062-477f-b25e-4fc48845cd1c/artequalswork2.jpg" alt="Art Equals Work" width="550" height="400" /></a><figcaption>“Art Equals Work” website layout switches for simple vertical reading once the browser gets too narrow.</figcaption></figure>

With Think Vitamin, we see a similar approach. When on a smaller screen or browser, the sidebar and top bar are removed, the navigation simplifies and moves directly above the content, as does the logo. The logo keeps its general look yet is modified for a more vertical orientation, with the tagline below the main icon. The white space around the content on larger screens is also more spacious and interesting, whereas it is simplified for practical purposes on smaller screens.

<figure><img title="Think Vitamin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a9c19c-d613-469f-a9f1-2853e2c2d4c6/thinkvitamin1.jpg" alt="Think Vitamin" width="550" height="400" /></figure>

<figure><img title="Think Vitamin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50069d23-1b22-45aa-8913-94faad9c4c53/thinkvitamin2.jpg" alt="Think Vitamin" width="550" height="400" /><figcaption>“Think Vitamin” navigation simplifies when on smaller screen or browser.</figcaption></figure>

8 Faces’ website design is flexible, right down to a standard netbook or tablet device, and expands in content quantity and layout width when viewed on wider screens or expanded browsers. When viewed on narrower screens, the featured issue on the right is cut out, and the content below is shortened and rearranged in layout, leaving only the essential information.

<figure><img title="8 Faces" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98670695-9f09-4875-b1ed-d43530d9a3e4/8faces1.jpg" alt="8 Faces" width="550" height="400" /><figcaption>“8 Faces” website expands in content quantity on wider screens.</figcaption></figure>

<figure><img title="8 Faces" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73aacb7f-2158-40b1-9d4a-da6f740e2e10/8faces2.jpg" alt="8 Faces" width="550" height="400" /><figcaption>“8 Faces” website view on narrower screens hides and rearranges content.</figcaption></figure>

The Hicksdesign website has three columns when viewed on a conventional computer screen with a maximized browser. When minimized in width, the design takes on a new layout: the third column to the right is rearranged above the second, and the logo moves next to the introductory text. Thus, no content needs to be removed for the smaller size. For even narrower screens and browser widths, the side content is removed completely and a simplified version is moved up top. Finally, the font size changes with the screen and browser width; as the browser gets narrower, the font size throughout gets smaller and remains proportional.

<figure><img title="Hicksdesign" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35ebe97c-efaa-471f-be59-a38d79647e1b/hicksdesign1.jpg" alt="Hicksdesign" width="550" height="400" /><figcaption>“Hicksdesign” website view on a conventional computer screen.</figcaption></figure>

<figure><img title="Hicksdesign" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59dffa42-b59e-4587-ac8b-fe7efa5a254b/hicksdesign2.jpg" alt="Hicksdesign" width="550" height="400" /><figcaption>Hicksdesign’s website design takes on a new layout on narrower screens.</figcaption></figure>

Here is a great example of a flexible image. The image in this design automatically resizes after certain “break” points, but in between those width changes, only the side margins and excess white space are altered. On smaller screens and minimized browsers, the navigation simplifies and the columns of navigation at the top fall off. At the design’s smallest version, the navigation simplifies to just a drop-down menu, perfect for saving space without sacrificing critical navigation links.

<figure><img title="Information Architects" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a65ad84-c557-4e50-91cf-89d62eae0c04/informationarchitects1.jpg" alt="Information Architects" width="550" height="400" /></figure>

<figure><img title="Information Architects" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceb133c8-22aa-4ea8-837c-27318e904b56/informationarchitects2.jpg" alt="Information Architects" width="550" height="400" /><figcaption>Example of a flexible image on smaller screens and minimized browsers.</figcaption></figure>

The website for Garret Keizer is fully flexible in wider browsers and on larger screens: the photo, logo and other images resize proportionally, as do the headings and block areas for text. At a few points, some pieces of text change in font size and get smaller as the screen or browser gets narrower. After a certain break point, the layout transforms into what we see in the second screenshot below, with a simple logo, introductory text and a simple vertical structure for the remaining content.

<figure><img title="Garret Keizer" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3962cb-873e-4b3d-a0cf-2b583ab87c95/garretkeizer1.jpg" alt="Garrent Keizer" width="550" height="400" /></figure>

<figure><img title="Garret Keizer" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba30bae5-d619-475c-bd41-31ce8517cc12/garretkeizer2.jpg" alt="Garret Keizer" width="550" height="400" /><figcaption>The “Garret Keizer” website layout transforms from wider to narrower browsers.</figcaption></figure>

With four relatively content-heavy columns, it’s easy to see how the content here could easily be squished when viewed on smaller devices. Because of the easy organized columns, though, we can also collapse them quite simply when needed, and we can stack them vertically when the space doesn’t allow for a reasonable horizontal span. When the browser is minimized or the user is on a smaller device, the columns first collapse into two and then into one. Likewise, the horizontal lines for break points also change in width, without changing the size or style of each line’s title text.

<figure><img title="Simon Collison" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bfe9550-e1bf-4dc0-aaad-97ec5c90bd26/colly1.jpg" alt="Simon Collison" width="550" height="400" /></figure>

<figure><img title="Simon Collison" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98836cd9-f423-44ec-bb82-9135c1b30e76/colly2.jpg" alt="Simon Collison" width="550" height="400" /><figcaption>Collapsing columns.</figcaption></figure>

On the CSS Tricks website, like many other collapsible Web designs, the sidebars with excess content are the first to fall off when the screen or browser gets too narrow. On this particular website, the middle column or first sidebar to the left was the first to disappear; and the sidebar with the ads and website extras did the same when the browser got even narrower. Eventually, the design leaves the posts, uses less white space around the navigation and logo and moves the search bar to below the navigation. The remaining layout and design is as flexible as can be because of its simplicity.

<figure><img title="CSS Tricks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ac5d265-afcb-4a56-af0a-6e81012f354c/csstricks1.jpg" alt="CSS Tricks" width="550" height="400" /></figure>

<figure><img title="CSS Tricks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bc05c28-5100-4cf7-a4e6-3b0fe50e6afb/csstricks2.jpg" alt="CSS Tricks" width="550" height="400" /><figcaption>Collapsible Web design example.</figcaption></figure>

As one can see, the main navigation here is the simple layout of t-shirt designs, spanning both vertically and horizontally across the screen. As the browser or screen gets smaller, the columns collapse and move below. This happens at each break point when the layout is stressed, but in between the break points, the images just change proportionally in size. This maintains balance in the design, while ensuring that any images (which are essential to the website) don’t get so small that they become unusable.

<figure><img title="Tee Gallery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c4920c-1c3e-438e-bb3f-c930830713de/teegallery1.jpg" alt="Tee Gallery" width="550" height="400" /></figure>

<figure><img title="Tee Gallery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6368c37-5b98-4be8-97ec-537840512c98/teegallery2.jpg" alt="Tee Gallery" width="550" height="400" /><figcaption>Collapsing columns and resizing images proportionally.</figcaption></figure>

Ten by Twenty is another design that does not resort to changing layout structure at all after certain break points, but rather simplifies responsive Web design by making everything fully flexible and automatically resizing, no matter what the screen or browser width. After a while, the design does stress a bit and could benefit from some rearrangement of content. But overall, the image resizing and flexible content spaces allow for a fairly simple solution that accommodates a wide range of screen sizes.

<figure><img title="Ten by Twenty" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19b394db-0aa6-4bc6-bb0f-39aea21722ac/tenbytwenty1.jpg" alt="Ten by Twenty" width="550" height="400" /></figure>

<figure><img title="Ten by Twenty" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff3d80cc-8b8d-4b95-a53f-7f2fc312e12a/tenbytwenty2.jpg" alt="Ten by Twenty" width="550" height="400" /><figcaption>“Ten by Twenty” website image resizing and flexible content example.</figcaption></figure>

On wide screens and browsers, all of the content on this simply designed website is well organized into columns, sidebar and simple navigation up top. It’s a fairly standard and efficient layout. On smaller screens, the sidebar is the first to drop off, and its content is moved below the book previews and essential information. Being limited in space, this design preserves its important hierarchy. Whereas on a wider screen we’d look left to right, on a narrower screen we’d tend to look from top to bottom. Content on the right is moved below content that would appear on the left on a wider screen. Eventually, when the horizontal space is fully limited, the navigation is simplified and stacked vertically, and some repeated or inessential elements are removed.

<figure><img title="Hard Boiled" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d8f7761-208b-4e8f-a03b-6a34d0a7249a/hardboiled1.jpg" alt="Hard Boiled" width="550" height="400" /></figure>

<figure><img title="Hard Boiled" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c849fc6d-e62d-4ebd-9ba1-f238cebc28cb/hardboiled2.jpg" alt="Hard Boiled" width="550" height="400" /><figcaption>When the horizontal space is fully limited, the navigation is simplified and stacked vertically.</figcaption></figure>

This design features a complex layout that looks inspired by a print style. When viewed on a standard wide computer screen, more portfolio pieces are featured and spanned horizontally across the page. As one moves down the page, more graphics and imagery span the space. On a smaller screen, the portfolio piece is cut down to one, and then eventually left out altogether for very small screens and narrow browsers. The visualizations below collapse into fewer columns and more rows, and again, some drop off entirely for very small screens. This design shows a creative and intelligent way to make a not-so-common layout work responsively.

<figure><img title="Teixido" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/122def0a-a0ab-48d2-822b-a710f633f9ec/teixido1.jpg" alt="Teixido" width="550" height="400" /></figure>

<figure><img title="Teixido" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1614e07a-8c1c-4ec2-8c76-335a1b0045bf/teixido2.jpg" alt="Teixido" width="550" height="500" /><figcaption>Example of how the imagery and graphics can collapse into fewer columns and more rows.</figcaption></figure>

This design has three main stages at which the design and layout collapse into a more user-friendly form, depending on how wide the screen or browser is. The main image (featuring type) is scaled proportionally via a flexible image method. Each “layout structure” is fully flexible until it reaches a breaking point, at which point the layout switches to something more usable with less horizontal space. The bottom four columns eventually collapse into two, the logo moves above the navigation, and the columns of navigation below are moved on top or below each other. At the design’s narrowest stage, the navigation is super-simplified, and some inessential content is cut out altogether.

<figure><img title="Stephen Caver" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8b636ee-c70c-4d0c-be8a-25634cf39f1e/stephancaver1.jpg" alt="Sephen Caver" width="550" height="400" /></figure>

<figure><img title="Stephen Caver" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29bb1efa-daf7-4c0f-af41-cbb0853427ee/stephancaver2.jpg" alt="Stephen Caver" width="550" height="500" /><figcaption>The design and layout collapse into a more user-friendly form, depending on how wide the screen or browser is.</figcaption></figure>

This layout does not change at all; no content is dropped or rearranged; and the text size does not change either. Instead, this design keeps its original form, no matter what the change in horizontal and vertical space. Instead, it automatically resizes the header image and the images for the navigation. The white space, margins and padding are also flexible, giving more room as the design expands and shrinks.

<figure><img title="Unstoppable Robot Ninja" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79c11ccc-0aa1-4f39-ba00-336e6f97a989/unstoppablerobotninja1.jpg" alt="Unstoppable Robot Ninja" width="550" height="400" /></figure>

<figure><img title="Unstoppable Robot Ninja" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e1b0b5-68bf-4743-b55a-a67006cb2ddd/unstoppablerobotninja2.jpg" alt="Unstoppable Robot Ninja" width="550" height="400" /><figcaption>The design keeps its original form and automatically resizes the header image and the images for the navigation.</figcaption></figure>

This is perhaps the simplest example of a responsive Web design in this showcase, but also one of the most versatile. The only piece in the layout that changes with the browser width is the blog post’s date, which moves above the post’s title or to the side, depending on how much horizontal space is available. Beyond this, the only thing that changes is the width of the content area and the margin space on the left and right. Everything is centered, so a sense of balance is maintained whatever the screen or browser width. Because of this design’s simplicity, switching between browser and screen widths is quick and easy.

<figure><img title="Bureu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7340839f-5528-4e7f-a8a0-a6569597a122/bureu1.jpg" alt="Bureu" width="550" height="400" /></figure>

<figure><img title="Bureu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce17062b-cc68-4f2b-8742-6cee4c1948f0/bureu2.jpg" alt="Bureu" width="550" height="400" /><figcaption>In this example, the only piece in the layout that changes with the browser width is the blog post’s date.</figcaption></figure>

Harry Roberts shows that responsive design can also have quite humble uses. If the user has a large viewport, the website displays three columns with a navigation menu floating on the left. For users with a viewport between 481px and 800px, a narrow version is displayed: the navigation jumps to the top of the site leaving the area for the content column and the sidebar. Finally, the iPhone view displays the sidebar under the content area. Harry also wrote a detailed article about the CSS styles he added to the stylesheet in his article "<a href="https://csswizardry.com/2010/12/media-queries-handier-than-you-think/">Media queries, handier than you think</a>". A nice example of how a couple of simple CSS adjustments can improve the website’s appearance across various devices.

<figure><img title="CSS Wizardry" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f126754-fae3-4498-ad93-c6d960e2056e/css-wizardry.jpg" alt="CSS Wizardry" width="550" height="376" /></figure>

<figure><img title="CSS Wizardry" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0a85cf2-f04a-4ea8-8778-79453c9d02a2/css-wizardry2.jpg" alt="CSS Wizardry" width="550" height="367" /><figcaption>Using simple CSS adjustments can improve the website’s appearance across various devices.</figcaption><figure>

This last design by Bryan James shows that responsive Web design need not apply only to static HTML and CSS websites. Done in Flash, this one features a full-sized background image and is flexible up to a certain width and height. As a result of the design style, on screens that are too small, the background image gets mostly hidden and the content can become illegible and squished. Instead of just letting it be, though, a message pops up informing the user that the screen is too small to adequately view the website. It then prompts the user to switch to a bigger screen. One can discuss if the design solution is good or bad in terms of usability, but the example shows that Flash websites can respond to user’s viewport, too.<br>

<figure><img title="Bryan James" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/077194d2-355a-4a68-98c8-e4a0b85f0996/bryanjames1.jpg" alt="Bryan James" width="550" height="253" /></figure>

<figure><img title="Bryan James" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/690cce81-9546-4ce8-a4e9-eedc732c0d0d/bryanjames2.jpg" alt="Bryan James" width="550" height="329" /><figcaption> Responsive Web design on Flash websites can also respond to user’s viewport.</figcaption></figure>

## Conclusion

We are indeed entering a new age of Web design and development. Far too many options are available now, and there will be far too many in the future to continue adjusting and creating custom solutions for each screen size, device and advancement in technology. We should rather start a new era today: creating websites that are future-ready right now. Understanding how to make a design responsive to the user doesn’t require too much learning, and it can definitely be a lot less stressful and more productive than learning how to design and code properly for every single device available.

Responsive Web design and the techniques discussed above are **not the final answer to the ever-changing mobile world.** Responsive Web design is a mere concept that when implemented correctly can *improve* the user experience, but not completely solve it for every user, device and platform. We will need to constantly work with new devices, resolutions and technologies to continually improve the user experience as technology evolves in the coming years.

Besides saving us from frustration, responsive Web design is also best for the user. Every custom solution makes for a better user experience. With responsive Web design, we can create custom solutions for a wider range of users, on a wider range of devices. A website can be tailored as well for someone on an old laptop or device as it can for the vast majority of people on the trendiest gadgets around, and likewise as much for the few users who own the most advanced gadgets now and in the years to come. Responsive Web design creates a great custom experience for everyone. As Web designers, we all strive for that every day on every project anyway, right?

### Further Resources for Responsive Web Design

*   [Designing for a Responsive Web with Heuristic Methods](https://designreviver.com/articles/designing-for-a-responsive-web-with-heuristic-methods/), Design Reviver
*   [Examples Of Flexible Layouts With CSS3 Media Queries](https://zomigi.com/blog/examples-of-flexible-layouts-with-css3-media-queries/), Zoe Mickley Gillenwater
*   [The Big Web Show #9: Responsive Web Design](https://5by5.tv/bigwebshow/9), 5by5 Studios
*   [How to Use CSS3 Media Queries to Create a Mobile Version of Your Website](/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/), Smashing Magazine
*   [Application: Rapid Prototyping of Adaptive CSS and Responsive Design](https://protofluid.com/), ProtoFluid
*   [Handcrafted CSS: More Bulletproof Web Design](https://www.amazon.com/exec/obidos/ASIN/0321643380/hivelogic-20), Dan Cederholm (printed book)
*   [Flexible Web Book](https://www.flexiblewebbook.com/), Zoe Mickley Gillenwater (printed book)

### Further Reading

-   [Responsive Web Design Techniques, Tools and Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)
-   [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
-   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)
-   [Techniques For Gracefully Degrading Media Queries](https://www.smashingmagazine.com/2011/08/techniques-for-gracefully-degrading-media-queries/)
-   [Aussie Hosting’s List of Responsive Web Hosts](https://bestwebhostingaustralia.org/)

{{< signature "al, vf, mrn" >}}
