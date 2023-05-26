---
title: The State Of Responsive Web Design
slug: the-state-of-responsive-web-design
image: >-
  https://www.smashingmagazine.com/inspiration/2014/04/11/get-excited-about-emotional-branding/attachment/why-you-should-get-excited-about-emotional-branding-orange-arrow-jpg/attachment/anote/
date: 2013-05-29T10:39:27.000Z
author: stephaniewalter
description: >-
  Responsive Web design has been around for some years now, and it was a hot
  topic in 2012\. Many well-known people such as Brad Frost and Luke Wroblewski
  have a lot of experience with it and have helped us make huge improvements in
  the field. But there’s still a whole lot to do.
categories:
  - Mobile
  - Techniques
  - Responsive Design
---
Responsive Web design has been around for some years now, and it was a hot topic in 2012. Many well-known people such as Brad Frost and Luke Wroblewski have a lot of experience with it and have helped us make huge improvements in the field. But <strong>there’s still a whole lot to do</strong>.

In this article, we will look at what is currently possible, what will be possible in the future using what are not yet standardized properties (such as CSS Level 4 and HTML5 APIS), and what still needs to be improved. This article is not exhaustive, and we won’t go deep into each technique, but you’ll have enough links and knowledge to explore further by yourself.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)
*   [Next-Generation Responsive Web Design Tools](https://www.smashingmagazine.com/2014/05/next-generation-responsive-web-design-tools-webflow-edge-reflow-macaw/)
*   [Content-First Prototyping](https://www.smashingmagazine.com/2016/05/content-first-prototyping/)

## The State Of Images In Responsive Web Design

What better aspect of <a href="https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/">responsive Web design</a> to start off with than images? This has been a major topic for a little while now. It got more and more important with the arrival of all of the high-density screens. By high density, I mean screens with a pixel ratio higher than 2; Apple calls these Retina devices, and Google calls them XHDPI. In responsive Web design, images come with two big related challenges: size and performance.

{{% feature-panel %}}

Most designers like pixel perfection, but “normal”-sized images on high-density devices look pixelated and blurry. Simply serving double-sized images to high-density devices might be tempting, right? But that would create a performance problem. Double-sized images would take more time to load. Users of high-density devices might not have the bandwidth necessary to download those images. Also, depending on which country the user lives in, bandwidth can be pretty costly.

The second problem affects smaller devices: why should a mobile device have to download a 750-pixel image when it only needs a 300-pixel one? And do we have a way to crop images so that small-device users can focus on what is important in them?

### Two Markup Solutions: The <picture> Element and The srcset Attribute

A first step in solving the challenge of responsive images is to change the markup of embedded images on an HTML page.

The <a href="https://responsiveimages.org/">Responsive Images Community Group</a> supports a proposal for a new, more flexible element, the <a href="https://picture.responsiveimages.org/">&lt;picture&gt;</a> element. The concept is to use the now well-known media queries to <strong>serve different images to different devices</strong>. Thus, smaller devices would get smaller images. It works a bit like the markup for video, but with different images being referred to in the source element.

The code in the proposed specification looks like this :

<pre><code class="language-markup">
&lt;picture width="500"  height="500"&gt;
  &lt;source  media="(min-width: 45em)" src="large.jpg"&gt;
  &lt;source  media="(min-width: 18em)" src="med.jpg"&gt;
  &lt;source  src="small.jpg"&gt;
  &lt;img  src="small.jpg" alt=""&gt;
  &lt;p&gt;Accessible  text&lt;/p&gt;
&lt;/picture&gt;
</code></pre>

If providing different sources is possible, then we could also imagine providing <strong>different crops</strong> of an image to focus on what’s important for smaller devices. The W3C’s “<a href="https://usecases.responsiveimages.org/#art-direction">Art Direction</a>” use case shows a nice example of what could be done.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fdfdbeb-0c8e-47af-b982-344739800ba5/pictureelement-mini.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160256" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fdfdbeb-0c8e-47af-b982-344739800ba5/pictureelement-mini.jpg" alt="Picture element used for artistic direction" width="500" height="548" /></a><br>
<em>(Image: <a href="https://www.flickr.com/photos/egorick/3754608666/">Egor Pasko</a></em>)

The solution is currently being discussed by the <a href="https://www.w3.org/community/respimg/">W3C Responsive Images Community Group</a> but is not usable in any browser at the moment as far as we know. A polyfill named <a href="https://github.com/scottjehl/picturefill">Picturefill</a> is available, which does pretty much the same thing. It uses a div and data-attribute syntax for safety’s sake.

A second proposal for responsive images markup was made to the W3C by Apple and is called “The srcset Attribute”; its CSS Level 4 equivalent is <a href="https://dev.w3.org/csswg/css4-images/#image-set-notation">image-set()</a>. The purpose of this attribute is to force user agents to select an appropriate resource from a set, rather than fetch the entire set. The HTML syntax for this proposal is based on the <code>&lt;img&gt;</code> tag itself, and the example in the specification looks like this:

<pre><code class="language-markup">
&lt;img  alt="The Breakfast Combo" 
  src="banner.jpeg"
  srcset="banner-HD.jpeg  2x, banner-phone.jpeg 100w, banner-phone-HD.jpeg 100w 2x"&gt;
</code></pre>

As you can see, <strong>the syntax is not intuitive at all</strong>. The values of the tag consist of comma-separated strings. The values of the attribute are the names or URLs of the various images, the pixel density of the device and the maximum viewport size each is intended for.

In plain English, this is what the snippet above says:

*   The default image is `banner.jpeg`.
*   Devices that have a pixel ratio higher than 2 should use `banner-HD.jpeg`.
*   Devices with a maximum viewport size of `100w` should use `banner-phone.jpeg`.
*   Devices with a maximum viewport size of `100w` _and_ a pixel ratio higher than 2 should use `banner-phone-HD.jpeg`.

The first source is the default image if the <code>srcset</code> attribute is not supported. The <code>2x</code> suffix for <code>banner-HD.jpeg</code> means that this particular image should be used for devices with a pixel ratio higher than 2. The <code>100w</code> for <code>banner-phone.jpeg</code> represents the minimum viewport size that this image should be used for. <strong>Due to its technical complexity</strong>, this syntax has not yet been implemented in any browser.

The syntax of the <code>image-set()</code> CSS property works pretty much the same way and enables you to load a particular background image based on the screen’s resolution:

<pre><code class="language-css">
background-image: image-set(  "foo.png" 1x,
  "foo-2x.png"  2x,
  "foo-print.png"  600dpi );
</code></pre>

This proposal is still a W3C Editor’s Draft. For now, it works in Safari 6+ and Chrome 21+.</p>

### Image Format, Compression, SVG: Changing How We Work With Images on the Web

As you can see, these attempts to find a new markup format for images are still highly experimental. This raises the issue of image formats themselves. Can we devise a responsive solution by changing the way we handle the images themselves?

The first step would be to look at alternative image formats that have a better compression rate. Google, for example, has developed a <strong>new image format</strong> named <a href="https://developers.google.com/speed/webp/">WebP</a>, which is 26% smaller than PNG and 25 to 34% smaller than JPEG. The format is supported in Google Chrome, Opera, Yandex, Android and Safari and can be activated in Internet Explorer using the Google Chrome Frame plugin. The main problem with this format is that Firefox does not plan to implement it. Knowing this, widespread use is unlikely for now.

Another idea that is gaining popularity is <strong>progressive JPEG images</strong>. Progressive JPEG images are, as the name suggests, progressively rendered. The first rendering is blurry, and then the image gets progressively sharper as it renders. Non-progressive JPEG images are rendered from top to bottom. In her article “<a href="https://calendar.perfplanet.com/2012/progressive-jpegs-a-new-best-practice/">Progressive JPEGs: A New Best Practice</a>,” Ann Robson argues that progressive JPEGs give the impression of greater speed than baseline JPEGs. A progressive JPEG gives the user a quick general impression of the image before it has fully loaded. This does not solve the technical problems of performance and image size, though, but it does improve the user experience.

Another solution to the problems of performance and image size is to <strong>change the compression rate</strong> of images. For a long time, we thought that enlarging the compression rate of an image would damage the overall quality of the image. But Daan Jobsis has done extensive research on the subject and has written an article about it, “<a href="https://www.netvlies.nl/tips-updates/algemeen/algemeen/retina-revolution/">Retina Revolution</a>.” In his experiments, he tried different image sizes and compression rates and came up with a pretty interesting solution. If you keep the image dimensions twice the displayed ones but also use a higher compression rate, then the image will have a smaller file size than the original, but will still be sharp on both normal and high-density screens. With this technique, Jobsis cut the weight of the image by 75%.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23129762-cd1e-44b9-8f7e-1c9d34cc24e3/imagecompression-mini1.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160257" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccb77d5c-fcba-4335-9677-9b0288f9ec5b/imagecompression-mini.jpg" alt="Image compression example" width="500" height="254" /></a><br>
<em>Daan Jobsis’ demonstration of image compression.</em>

Given the headaches of responsive images, the idea of gaining pixel independence from images wherever possible is seducing more and more designers and developers. The SVG format, for example, can be used to create all of the UI elements of a website and will <a href="https://www.smashingmagazine.com/2012/01/16/resolution-independence-with-svg/">be resolution-independent</a>. The elements will scale well for small devices and won’t be pixellated on high-density devices. <a href="https://css-tricks.com/using-fonts-for-icons/">Font icons</a> are another growing trend. They involve asigning icon glyphs to certains characters of the font (like the Unicode Private Area ones), giving you the flexibility of fonts. Unfortunately, the solution doesn’t work with pictures, so a viable markup or image format is eagerly expected.

## Responsive Layout Challenge: Rearrange And Work With Content Without Touching the HTML?

Let’s face it, the fluid grids made of floats and inline blocks that we use today are a poor patch waiting for a better solution. Working with layout and completely rearranging blocks on the page for mobile without resorting to JavaScript is a nightmare right now. It’s also pretty inflexible. This is particularly significant on websites created with a CMS; the designer can’t change the HTML of every page and every version of the website. So, how can this be improved?

### Four CSS3 Layout Solutions That Address the Flexible Layout Problem

The most obvious possible solution is the <a href="https://www.w3.org/TR/css3-flexbox/">CSS3 flexible box layout model</a> (or <strong>“flexbox”</strong>). Its current status is candidate recommendation, and it is supported in <a href="https://caniuse.com/#feat=flexbox">most major mobile browsers and desktop browsers</a> (in IE starting from version 10). The model enables you to easily reorder elements on the screen, independent of the HTML. You can also change the box orientation and box flow and distribute space and align according to the context. Below is an example of a layout that could be rearranged for mobile. The syntax would look like this:

<pre><code class="language-css">
.parent {
  display: flex;
  flex-flow: column; /* display items in columns */
}

.children {
  order: 1; /* change order of elements */
}
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37d8bf79-3a4c-48ed-b871-e1971c47e244/flexbox-mini1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394a83d7-00b2-4ed8-87fc-1a02d5bcf1c5/flexbox-mini.jpg" alt="Flexbox as an example" width="500" height="311" /></a>

The article “<a href="https://www.smashingmagazine.com/2011/09/19/css3-flexible-box-layout-explained/">CSS3 Flexible Box Layout Explained</a>” will give you a deeper understanding of how flexbox works.

Another solution quite close to the flexbox concept of reordering blocks on the page, but with JavaScript, is <a href="https://github.com/edenspiekermann/minwidth-relocate">Relocate</a>.

A second type of layout that is quite usable for responsive design today is the <strong>CSS3 multiple-column layout</strong>. The module is at the stage of candidate recommendation, and it <a href="https://www.w3.org/TR/css3-multicol/">works pretty well in most browsers</a>, expect for IE 9 and below. The main benefit of this model is that content can flow from one column to another, providing a huge gain in flexibility. In terms of responsiveness, the number of columns can be changed according to the viewport’s size.

Setting the size of the columns and letting the browser calculate the number of columns according to the available space is possible. Also possible is setting the number of columns, with the gaps and rules between them, and letting the browser calculate the width of each column.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32306e6f-063c-421f-b175-047bac5bd083/responsicecolumns-mini1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5425ad6-e971-492c-a312-defaa7b19105/responsicecolumns-mini.jpg" alt="CSS3 Multiple Column layout" width="500" height="311" /></a>

The syntax looks like this:

<pre><code class="language-css">
.container {
  column-width: 10em ; /* Browser will create 10em columns. Number of columns would depend on available space. */
}

.container {
  columns: 5; /* Browser will create 5 columns. Column size depends on available space. */
  column-gap: 2em;
}
</code></pre>

To learn more, read David Walsh’s article “<a href="https://davidwalsh.name/css-columns">CSS Columns</a>.”

A third CSS3 property that could gain more attention in future is the <a href="https://dev.w3.org/csswg/css3-grid-layout/">CSS3 grid layout</a>. This gives designers and developers <strong>a flexible grid</strong> they can work with to create different layouts. It allows content elements to be displayed in columns and rows without a defined structure. First, you would declare a grid on the container, and then place all child elements in this virtual grid. You could then define a different grid for small devices or change the position of elements in the grid. This allows for enormous flexibility when used with media queries, changes in orientation and so on.

The syntax looks like this (from the 2 April 2013 working draft):

<pre><code class="language-css">
 .parent {
   display: grid; /* declare a grid */
   grid-definition-columns: 1stgridsize  2ndgridsize …;
   grid-definition-rows: 1strowsize  2ndrowsize …;
}

.element {
   grid-column: 1;
   grid-row: 1
}

.element2 {
   grid-column: 1;
   grid-row: 3;
}
</code></pre>

To set the sizes of columns and rows, you can use various units, as <a href="https://www.w3.org/TR/css3-grid-layout/#grid-definition-columns">detailed in the specification</a>. To position the various elements, the specification says this: “Each part of the game is positioned between grid lines by referencing the starting grid line and then specifying, if more than one, the number of rows or columns spanned to determine the ending grid line, which establishes bounds for the part.”

The main problem with this property is that it is currently <a href="https://caniuse.com/#feat=css-grid">supported only in IE 10</a>. To learn more about this layout, read Rachel Andrew’s “<a href="https://24ways.org/2012/css3-grid-layout/">Giving Content Priority With CSS3 Grid Layout</a>.” Also, note that the specification and syntax for grid layouts changed on 2 April 2013. Rachel wrote an update on the syntax, titled “<a href="https://www.rachelandrew.co.uk/archives/2013/04/10/css-grid-layout---what-has-changed/">CSS Grid Layout: What Has Changed?</a>”

The last layout that might become useful in future if implemented in browsers is the <a href="https://www.w3.org/TR/2009/WD-css3-layout-20090402/">CSS3 template layout</a>. This CSS3 module works by associating an element with a layout “name” and then ordering the elements on an invisible grid. The grid may be fixed or flexible and can be changed according to the viewport’s size.

The syntax looks like this:

<pre><code class="language-css">
.parent {
   display: "ab"
            "cd" /* creating the invisible  grid */
}

.child1 {
   position: a;
}

.child2 {
   position: b;
}

.child3 {
   position: c;
}

.child4 {
   position: d;
}
</code></pre>

This renders as follows:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3040a2dc-33a6-4069-b8cc-f2e01005f8d9/templatelayout-mini1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93694aa4-1de2-4552-9ed3-584bb881ef8a/templatelayout-mini.jpg" alt="CSS3 template layout" width="500" height="311" /></a>

Unfortunately, browser support for this CSS3 module is currently null. Maybe someday, if designers and developers show enough interest in this specification, some browser vendors might implement it. For the moment, you can test it out <a href="https://code.google.com/p/css-template-layout/">with a polyfill</a>.</p>

### Viewport-Relative Units and the End of Pixel-Based Layout

<a href="https://www.w3.org/TR/css3-values/#viewport-relative-lengths">Viewport-based percentage lengths</a> — vw, vh, vm, vmin and vmax — are units measured relative to the dimensions of the viewport itself.

One vw unit is equal to 1% of the width of the initial containing block. If the viewport’s width is 320, then 1 vw is 1 × 320/100 = 3.2 pixels.

The vh unit works the same way but is relative to the height of the viewport. So, 50 vh would equal 50% of the height of the document. At this point, you might wonder what the difference is with the percentage unit. While percentage units are relative to the size of the parent element, the vh and vw units will always be relative to the size of the viewport, regardless of the size of their parents.

This gets pretty interesting when you want to, for example, create a content box and make sure that it never extends below the viewport’s height so that the user doesn’t have to scroll to find it. This also enables us to create true 100%-height boxes without having to hack all of the elements’ parents.

The vmin unit is equal to the smaller of vm or vh, and vmax is equal to the larger of vm or vh; so, those units respond perfectly to changes in device orientation, too. Unfortunately, for the moment, <a href="https://caniuse.com/#feat=viewport-units">those units are not supported in Android’s browser</a>, so you might have to wait a bit before using them in a layout.</p>

### A Word on Adaptive Typography

The layout of a website will depend heavily on the content. I cannot conclude a section about the possibilities of responsive layout without addressing typography. CSS3 introduces a font unit that can be pretty handy for responsive typography: the <a href="https://www.w3.org/TR/css3-values/#font-relative-lengths">rem unit</a>. While fonts measured in em units have a length relative to their parent, font measured in rem units are relative to the font size of the root element. For a responsive website, you could write some CSS like the following and then change all font sizes simply by changing the font size specified for the <code>html</code> element:

<pre><code class="language-css">
html {
   font-size: 14px;
}

p {
   font-size: 1rem /* this has 14px */
}

@media screen and (max-width:380px) {
   html {
      font-size: 12px; /* make the font smaller for mobile devices */
   }

   p {
      font-size: 1rem /* this now equals 12px */
   }
}
</code></pre>

Except for IE 8 and Opera mini, <a href="https://caniuse.com/#search=rem">support for rem</a> is pretty good. To learn more about rem units, read Matthew Lettini’s article “<a href="https://techtime.getharvest.com/blog/in-defense-of-rem-units">In Defense of Rem Units</a>.”

## A Better Way To Work Responsively With Other Complex Content

We are slowly getting better at dealing with images and text in responsive layouts, but we still need to find solutions for other, more complex types of content.</p>

### Dealing With Forms on a Responsive Website

Generally speaking, dealing with forms, especially long ones, in responsive Web design is quite a challenge! The longer the form, the more complicated it is to adapt to small devices. The physical adaptation is not that hard; most designers will simply put the form’s elements into a single column and stretch the inputs to the full width of the screen. But making forms visually appealing isn’t enough; we have to make them easy to use on mobile, too.

For starters, <a href="https://www.smashingmagazine.com/2010/03/11/forms-on-mobile-devices-modern-solutions/">Luke Wroblewski advises</a> to avoid textual input and instead to <strong>rely on checkboxes, radio buttons and select drop-down menus</strong> wherever possible. This way, the user has to enter as little information as possible. Another tip is not to make the user press the “Send” button before getting feedback about the content of their submission. On-the-fly error-checking is especially important on mobile, where most forms are longer than the height of the screen. If the user has mistyped in a field and has to send the form to realize it, then chances are they won’t even see where they mistyped.

In the future, the new HTML5 form inputs and attributes will be a great help to us in building better forms, without the need for (much) JavaScript. For instance, you could use the <a href="https://www.w3.org/wiki/HTML5_form_additions#required"><code>required</code> attribute</a> to give feedback about a particular field on the fly. Unfortunately, <a href="https://caniuse.com/#search=required">support for this on mobile</a> devices is poor right now. The <a href="https://www.w3.org/TR/2011/WD-html5-20110525/common-input-element-attributes.html#the-autocomplete-attribute"><code>autocomplete</code> attribute</a> could also help to make forms more responsive.

A mobile phone is a personal possession, so we can assume that data such as name and postal address will remain consistent. Using the <code>autocomplete</code> HTML5 attribute, <strong>we could prefill such fields</strong> so that the user doesn’t have to type all of that information over and over. There is also a <a href="https://www.w3.org/wiki/HTML5_form_additions#New_form_controls">whole list of new HTML5 inputs</a> that can be used in the near future to make forms more responsive.

Dates in form elements are a good example of what can be improved with HTML5. We used to rely on JavaScripts to create date-pickers. Those pickers are quite usable on big desktop screens but very hard to use on touch devices. Selecting the right date with a finger is difficult when the touch zones are so small.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84cb4a47-e407-47b4-b652-0dbebe0fc08a/datepicker-jquery-mini2.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160263" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecc2cd9a-0627-45da-bd8f-90640ded6af3/datepicker-jquery-mini.jpg" alt="Different picker examples" width="500" height="259" /></a><br>
<em>How am I supposed to select a date when my finger is touching three dates at the same time?</em>

A promising solution lies in the new HTML5 <a href="https://www.w3.org/TR/html-markup/input.date.html#input.date"><code>input type="date"</code></a>, which sets a string in the format of a date. The HTML5 <a href="https://www.w3.org/TR/html-markup/input.datetime.html#input.datetime"><code>input type="datetime"</code></a> sets a string in the format of a date and time. The big advantage of this method is that we let the browser decide which UI to use. This way, the UI is automatically optimized for mobile phones. Here is what an <code>input type="date"</code> looks like on the desktop, on an Android phone and tablet (with the Chrome browser), and on the iPhone and iPad.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/849cd9e2-673c-4698-9d95-17e2d2979783/mobile-input-type-date-mini1.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160264" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d875945b-dcc8-4f6f-9c84-d0dea0fdb236/mobile-input-type-date-mini.jpg" alt="Mobile input type=date rendering" width="500" height="595" /></a><br>
<em>Renderings of <code>input type="date"</code> on different mobile devices.</em>

Note that the screenshots were taken in my browser and on the Android phone, so the language automatically adapted to the system language (French). By using native components, you no longer have to adapt the language into different versions of the website.

For now, <a href="https://caniuse.com/input-datetime">support for <code>input type="date"</code></a> on the desktop is absent except in Opera and Chrome. Native Android browsers don’t support it at all, but Chrome for Android does, and so does Safari on iOS. A lot still has to get done in order for us to be able to use this solution on responsive websites. Meanwhile, you could use a polyfill such as Mobiscroll for mobile browsers that don’t support it natively.

Apart from these HTML5 input solutions, attempts have been made to improve other design patterns, such as <a href="https://www.lukew.com/ff/entry.asp?1653">passwords on mobile</a> and <a href="https://www.lukew.com/ff/entry.asp?756">complex input formatting using masks</a>. As you will notice, these are experimental. The perfect responsive form does not exist at the moment; a lot still has to be done in this field.</p>

### Dealing With Tables on a Responsive Website

Another content type that gets pretty messy on mobile and responsive websites is tables. Most table are oriented horizontally and present a lot of data at once, so you can see how getting it right on a small screen is pretty hard. HTML tables are fairly flexible — you can use percentages to change the width of the columns — but then the content can quickly become unreadable.

No one has yet found the perfect way to present tables, but some suggestions have been made.

One approach is to <strong>hide what could be considered “less important” columns</strong>, and provide checkboxes for the user to choose which columns to see. On the desktop, all columns would be shown, while on mobile, the number of columns shown would depend on the screen’s size. The Filament Group <a href="https://filamentgroup.com/examples/rwd-table-patterns/">demonstrates</a> this approach. The solution is also used in the table column toggle on jQuery Mobile.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9439f83-72ae-448c-a30c-5af8710efda8/responsivedatable01-mini1.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160265" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32291e04-08f3-4d28-a4c4-755e8ed8470d/responsivedatable01-mini.jpg" alt="Responsive table examples" width="500" height="447" /></a><br>
<em>Some examples of responsive tables.</em>

A second approach plays with the idea of a <strong>scrollable table</strong>. You would “pin” a single fixed-size column on the left and then leave a scroll bar on a smaller part of the table to the right. <a href="https://dbushell.com/2012/01/05/responsive-tables-2/">David Bushell implements this idea</a> in an article, using CSS to display all of the content in the <code>&lt;thead&gt;</code> on the left side of the table, leaving the user to scroll through the content on the right. <strong>Zurb</strong> uses the same idea but in a different way for <a href="https://www.zurb.com/playground/responsive-tables">its plugin</a>. In this case, the headers stay at the top of the table, and the table is duplicated with JavaScript so that only the first column is shown on the left, and all other columns are shown on the right with a scroll bar.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86ab3d68-deaa-4c7f-bd91-3ee29ec7859f/responsivetable02-mini1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aba2a9ef-7440-4f2e-a337-e93cbc86f9e8/responsivetable02-mini.jpg" alt="Responsive table overflow example" width="500" height="477" /></a><br>
<em>Two examples of scrollable responsive tables</em>

The big issue with scroll bars and CSS properties such as <code>overflow: auto</code> is that many mobile devices and tablets simply won’t display a visible scroll bar. The right area of the table will be scrollable, but the user will have no visual clue that that’s possible. We have to find some way to indicate that more content lies to the right.

A third approach is to <strong>reflow a large table and split up the columns</strong> into what essentially looks like list items with headings. This technique is used in the “reflow mode” on jQuery Mobile and was explained by Chris Coyier in his article “<a href="https://css-tricks.com/responsive-data-tables/">Responsive Data Tables</a>.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ede4de0-8a7c-4fdc-b4c3-11394d97d286/responsivetable03-mini1.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160268" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba9cc823-0533-49b2-8529-58a7ee56b4e7/responsivetable03-mini.jpg" alt="Responsive table reflow example" width="500" height="457" /></a><br>
<em>Reflowing a table responsively</em>

<a href="https://css-tricks.com/responsive-data-table-roundup/">Many other techniques</a> exist. Which to use depends heavily on your project. No two projects are the same, so I can only show you how other people have dealt with it. If you come up with a nice solution of your own, please share it with the world in the comments below, on Twitter or elsewhere. We are in this boat together, and tables suck on mobile, really, so let’s improve them together!

## Embedding Third-Party Content: The Responsive Iframe Problem

Many websites consist of embedded third-party content: YouTube or Vimeo videos, SlideShare presentations, Facebook applications, Twitter feeds, Google Maps and so on. A lot of those third parties make you use iframes to embed their content. But let’s face it: iframes are a pain to deal with in responsive design. The big problem is that iframes force a fixed width and height directly in your HTML code. Forcing a 100% width on the iframe would work, but then you would lose the ratio of the embedded content. To embed a video or slideshow and preserve the original ratio, you would have to find a workaround.</p>

### An HTML and CSS Workaround

<a href="https://www.tjkdesign.com/">Thierry Koblentz</a> has written a good article titled “<a href="https://alistapart.com/article/creating-intrinsic-ratios-for-video">Creating Intrinsic Ratios for Video</a>,” in which he proposes a way to embed responsive videos using a 16:9 ratio. This solution can be extended to other sorts of iframe content, such as SlideShare presentations and Google Maps. Koblentz wraps the iframe in a container with a class that we can target in CSS. The container makes it possible for the iframe to resize fluidly, even if the iframe has fixed pixel values in the HTML. The <a href="https://amobil.se/2011/11/responsive-embeds/">code, adapted by Anders M. Andersen,</a> looks like this:

<pre><code class="language-css">
 .embed-container  {
   position: relative;
   padding-bottom: 56.25%; /* 16:9 ratio */
   padding-top: 30px; /* IE 6 workaround*/
   height: 0;
   overflow: hidden;
}

.embed-container iframe,
.embed-container object,
.embed-container embed {
   position: absolute;
   top: 0;
   left: 0;
   width: 100%;
   height: 100%;
}
</code></pre>

This will work for all iframes. The only potential problem is that you will have to wrap all of the iframes on your website in a <code>&lt;div class="embed-container"&gt;</code> element. While this would work for developers who have total control over their code or for clients who are reasonably comfortable with HTML, it wouldn’t work for clients who have no technical skill. You could, of course, use some JavaScript to detect iframe elements and automatically embed them in the class. But as you can see, it’s still a major workaround and not a perfect solution.</p>

## Dealing With Responsive Video In Future

HTML5 opens a world of possibilities for video — particularly with the <a href="https://www.w3.org/wiki/HTML/Elements/video">video element</a>. The great news is that <a href="https://caniuse.com/#feat=video">support for this element is amazingly good for mobile devices</a>! Except for Opera Mini, most major browsers support it. The video element is also pretty flexible. Presenting a responsive video is as simple as this:

<pre><code class="language-css">
video {
   max-width: 100%;
   height: auto;
}
</code></pre>

You’re probably asking, “What’s the problem, then?”

The problem is that, even though YouTube or Vimeo may support the video element, you still have to embed videos using the ugly iframe method. And that, my friend, sucks. Until YouTube and Vimeo provide a way to embed videos on websites using the HTML5 video tag, <strong>we have to find workarounds</strong> to make video embedding work on responsive websites. Chris Coyier created such a workaround as a jQuery plugin called <a href="https://fitvidsjs.com/">FitVids.js</a>. It uses the first technique mentioned above: creating a wrapper around the iframe to preserve the ratio.</p>

### Embedding Google Maps

If you embed a Google Map on your website, the technique described above with the container and CSS will work. But, again, it’s a dirty little hack. Moreover, the map will resize in proportion and might get so tiny that the map loses the focus area that you wanted to show to the user. The <a href="https://developers.google.com/maps/mobile-apps">Google Maps’ page for mobile</a> says that you can use the <a href="https://developers.google.com/maps/documentation/staticmaps/">static maps API</a> for mobile embedding. Using a static map would indeed make the iframe problems go away. Brad Frost wrote a nice article about, and created a demo of, <a href="https://bradfrostweb.com/blog/post/adaptive-maps/">adaptive maps</a>, which uses this same technique. A JavaScript detects the screen’s size, and then the iframe is replaced by the static map for mobile phones. As you can tell, we again have to resort to a trick to deal with the iframe problem, in the absence of a “native” solution (i.e. from Google).</p>

### We Need Better APIs

And now the big question: Is there a better way? The biggest problem with using iframes to embed third-party content responsively is the lack of control over the generated code. <strong>Developers and designers are severely dependent</strong> on the third party and, by extension, its generated HTML. The number of websites that provide content to other websites is growing quickly. We’ll need much better solutions than iframes to embed this content.

Let’s face it: embedding Facebook’s iframe is a real pain. The lack of control over the CSS can make our work look very sloppy and can even sometimes ruin the design. The Web is a very open place, so perhaps now would be a good time to start thinking about more open APIs! In the future, we will need APIs that are better and simpler to use, so that anyone can embed content flexibly, without relying on unresponsive fixed iframes. Until all of those very big third parties decide to create those APIs, we are stuck with sloppy iframes and will have to resort to tricks to make them workable.</p>

## Responsive Navigation: An Overview Of Current Solutions

Another big challenge is what to do with navigation. The more complex and deep the architecture of the website, the more inventive we have to be.

An early attempt to deal with this in a simple way was to <a href="https://css-tricks.com/convert-menu-to-dropdown/">convert the navigation into a dropdown menu</a> for small screens. Unfortunately, this was not ideal. First, this solution gets terribly complicated with multiple-level navigation. It can also cause some problems with accessibility. I recommend “<a href="https://uxmovement.com/forms/stop-misusing-select-menus/">Stop Misusing Select Menus</a>” to learn about all of the problems such a technique can create.

Some people, <a href="https://bradfrostweb.com/blog/web/responsive-nav-patterns/">including Brad Frost</a> and Luke Wroblewski, have attempted to solving this problem. Brad Frost compiled some of his techniques on the website <a href="https://bradfrost.github.com/this-is-responsive/patterns.html#navigation">This Is Responsive</a>, under the navigation section.

Toggle navigation involves hiding the menu for small devices, displaying only a “menu” link. When the user clicks on it, all of the other links appear as block-level elements below it, pushing the main content below the navigation.

A variant of this, inspired by some native application patterns, is <a href="https://www.smashingmagazine.com/2013/01/15/off-canvas-navigation-for-responsive-website/">off-canvas</a> navigation. The navigation is hidden beneath a “menu” link or icon. When the user clicks the link, the navigation slides out as a panel from the left or right, pushing the main content over.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eec2f604-d46b-4c5c-81ec-a3e6c4c1cb3a/navigations-mobile-mini1.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160269" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe78b14b-01f5-4714-9f4b-0dc6ae90d4b0/navigations-mobile-mini.jpg" alt="Toggle navigation example" width="500" height="234" /></a><br>
<em>Some examples of toggle navigation</em>

The problem with these techniques is that the navigation remains at the top of the screen. In his article “<a href="https://www.lukew.com/ff/entry.asp?1649">Responsive Navigation: Optimizing for Touch Across Devices</a>,” Luke Wroblewski illustrates <strong>which zones are easily accessible for different device types</strong>. The top left is the hardest to get to on a mobile device.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e7fcfc-59f9-49a5-ada5-72d4f3f55593/touchaccess-mini.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160270" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e7fcfc-59f9-49a5-ada5-72d4f3f55593/touchaccess-mini.jpg" alt="Easy touch access for mobile and tablet" width="500" height="372" /></a><br>
<em>Easily accessible screen areas on mobile phones and tablets, <a href="https://www.lukew.com/ff/entry.asp?1649">according to Luke Wroblewski</a>.</em>

Based on this, Jason Weaver created <a href="https://jasonweaver.name/lab/touchnav/v2/">some demos</a> with navigation at the bottom. One solution is a <a href="https://codepen.io/bradfrost/full/mlyvu">footer anchor</a>, with navigation put at the bottom of the page for small devices, and a “menu” link that sends users there. It uses the HTML anchor link system.

<a href="https://codepen.io/bradfrost/full/orJwL">Many</a> other <a href="https://codepen.io/bradfrost/full/vcuem">attempts</a> have <a href="https://codepen.io/bradfrost/full/qwJvF">been made</a> to solve the navigation problem in responsive Web design. As you can see, there is not yet a perfect solution; it really depends on the project and the depth of the navigation. Fortunately for us, some of the people who have tried to crack this nut have shared their experiences with the community.

<strong>Another unsolved issue is what icon to use</strong> to tell the user, “Hey! There’s a menu hidden under me. Click me!" Some websites have a plus symbol (+), some have a grid of squares, other have what looks like an unordered list, and some have three lines (aka the burger icon).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f222592-f2e6-4e73-8cc0-aeab4e9e9c46/navigationicons-mini.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="160271" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f222592-f2e6-4e73-8cc0-aeab4e9e9c46/navigationicons-mini.jpg" alt="Some responsive icons example" width="500" height="144" /></a><br>
<em>To see these icons used on real websites, have a look at “<a href="https://stuffandnonsense.co.uk/blog/about/we_need_a_standard_show_navigation_icon_for_responsive_web_design">We Need a Standard ‘Show Navigation’ Icon for Responsive Web Design</a>.”</em>

The main problem is figuring out which of these icons would be the most recognizable to the average user. If we all agreed to use one of them, users would be trained to recognize it. The problem is which to choose? I really would like to know which icon you use, so don’t hesitate to share it in the comments below.</p>

## Mobile Specificities: “Is The User On A Mobile Device? If So, What Can It Do?”

Mobile and tablet devices are a whole new world, far removed from desktop computers, with their own rules, behaviors and capabilities. We might want to adapt our designs to this new range of capabilities.</p>

### Detecting Touch Capabilities With Native JavaScript

Apart from screen size, I bet if you asked what is the main difference between desktop and mobile (including tablets), most people would say touch capability. There is no mouse on a mobile phone (no kidding!), and except for some rare hybrid devices into which you can plug a mouse, you can’t do much with mouse events on a tablet. This means that, depending on the browser, the <code>:hover</code> CSS pseudo-class might not work. Some browsers are clever enough to provide a native fallback for the hover event by translating it into a touch event. Unfortunately, not all browsers are so flexible. Creating a design that doesn’t depend on hidden elements being revealed on <code>:hover</code> events would be wise.

<strong>Catching touch events</strong> could also be another solution. A W3C working group has started working on a <a href="https://www.w3.org/TR/touch-events/">touch event specification</a>. In the future, we will be able to catch events such as <code>touchstart</code>, <code>touchmove</code> and <code>toucheend</code>. We will be able to deal with these events directly in JavaScript without requiring a third-party framework such as <a href="https://eightmedia.github.com/hammer.js/">Hammer.js</a> or <a href="https://jgestures.codeplex.com/">jGestures</a>. But JavaScript is one thing — what about CSS?

### CSS Level 4 “Pointer” Media Query

CSS Level 4 specifies a new media query called “pointer”, which can be used to query the presence and accuracy of a pointing device, such as a mouse. The media query takes one of three values:

*   `none` The device does not have any pointing device at all.
*   `coarse` The device has a pointing device with limited accuracy; for example, a mobile phone or tablet with touch capabilities, where the “pointer” would be a finger.
*   `fine` The device has an accurate pointing device, such as a mouse, trackpad or stylus.

Using this media query, we can enlarge buttons and links for touch devices:

<pre><code class="language-css">
@media  (pointer:coarse) {
   input[type="submit"],
       a.button {
       min-width: 30px;
       min-height: 40px;
       background: transparent;
   }
 }
</code></pre>

The pointer media query is not yet supported and is merely being proposed. Nevertheless, the potential is huge because it would enable us to <strong>detect touch devices via CSS</strong>, without the need for a third-party library, such as <a href="https://modernizr.com/docs/#touch">Modernizr</a>.</p>

### CSS Level 4 “Hover” Media Query

The CSS Level 4 specification proposes a new hover media query, which detects whether a device’s primary pointing system can hover. It returns a <code>Boolean: 1</code> if the device supports hover, <code>0</code> if not. Note that it has nothing to do with the <code>:hover</code> pseudo-class.

Using the hover media query, we can enhance an interface to hide certain features for devices that do support hovering. The code would look something like this:

<pre><code class="language-css">
 @media  (hover) {
   .hovercontent { display: none; } /* Hide content only for devices with hover capabilities. */

   .hovercontent:hover { display: block; }   
 }
</code></pre>

It can also be used to create dropdown menus on hover; and the fallback for mobile devices is in native CSS, without the need for a feature-detection framework.</p>

### CSS Level 4 Luminosity Media Query

Another capability of mobile devices is the luminosity sensor. The CSS Level 4 specification has a media query for luminosity, which gives us access to a device’s light sensors directly in the CSS. Here is how the specification describes it:
<blockquote>"The “luminosity” media feature is used to query about the ambient luminosity in which the device is used, to allow the author to adjust style of the document in response."</blockquote>

In the future, we will be able to create <strong>websites that respond to ambient luminosity</strong>. This will greatly improve user experiences. We will be able to detect, for example, exceptionally bright environments using the <code>washed</code> value, adapting the website’s contrast accordingly. The <code>dim</code> value is used for dim environments, such as at nighttime. The <code>normal</code> value is used when the luminosity level does not need any adjustment.

The code would look something like this:

<pre><code class="language-css">
 @media  (luminosity: washed) {
   p { background: white; color: black; font-size: 2em; }
 }
</code></pre>

As you can see, CSS Level 4 promises a lot of fun new stuff. If you are curious to see what’s in store, not only mobile-related, then have a look at “<a href="https://www.smashingmagazine.com/2013/01/21/sneak-peek-future-selectors-level-4/">Sneak Peek Into the Future: Selectors, Level 4</a>.”

### More Mobile Capabilities to Detect Using APIs and JavaScript

Many other things could be detected to make the user experience amazing on a responsive website. For example, we could gain access to the native gyroscope, compass and accelerometer to detect the device’s orientation using the HTML5 <a href="https://dev.w3.org/geo/api/spec-source-orientation.html#deviceorientation"><code>DeviceOrientationEvent</code></a>. <a href="https://caniuse.com/#feat=deviceorientation">Support for DeviceOrientationEvent</a> in Android and iOS browsers is getting better, but the specification is still a draft. Nevertheless, the API look promising. Imagine playing full HTML5 games directly in the browser.

Another API that would be particularly useful for some mobile users is <a href="https://dev.w3.org/geo/api/spec-source.html">geolocation</a>. The good news is that it’s already <a href="https://caniuse.com/#search=geolocation">well supported</a>. This API <strong>enables us to geolocate the user using GPS</strong> and to infer their location from network signals such as IP address, RFID, Wi-Fi and Bluetooth MAC addresses. This can be used on some responsive websites to provide users with contextual information. A big restaurant chain could enhance its mobile experience by showing the user the locations of restaurants in their area. The possibilities are endless.

The W3C also proposed a draft for a <a href="https://dev.w3.org/2009/dap/vibration/">vibration API</a>. With it, the browser can provide tactile feedback to the user in the form of vibration. This, however, is creeping into the more specific field of Web applications and mobile games in the browser.

Another API that has been highly discussed is the <a href="https://www.w3.org/TR/netinfo-api/">network information API</a>. The possibility of measuring a user’s bandwidth and optimizing accordingly has seduced many developers. We would be able to serve high-quality images to users with high bandwidth and low-quality images to users with low bandwidth. With the <code>bandwidth</code> attribute of the network API, it would be possible to estimate the downloading bandwidth of a user in megabytes per second. The second attribute, <code>metered</code>, is a Boolean that tells us whether the user has a metered connection (such as from a prepaid card). These two attributes are currently accessible only via JavaScript.

Unfortunately, <strong>measuring a user’s connection is technically difficult</strong>, and a connection could change abruptly. A user could go into a tunnel and lose their connection, or their speed could suddenly drop. So, a magical media query that measures bandwidth looks hypothetical at the moment. Yoav Weiss has written a good article about the problems that such a media query would create and about bandwidth measurement, “Bandwidth Media Queries? We Don’t Need ’Em!”

Many other APIs deal with mobile capabilities. If you are interested in learning more, Mozilla has a <a href="https://wiki.mozilla.org/WebAPI">very detailed list</a>. Most are not yet fully available or standardized, and most are intended more for Web applications than for responsive websites. Nevertheless, it’s a great overview of how large and complex mobile websites could get in future.</p>

## Rethinking The Way We And The User Deal With Content

From a technical perspective, there are still a lot of challenges in dealing with content at a global scale. The mobile-first method has been part of the development and design process for a little while now. We could, for example, serve to mobile devices the minimum data that is necessary, and then use JavaScript and AJAX to conditionally load more content and images for desktops and tablets. But to do this, we would also have to <strong>rethink how we deal with content</strong> and be able to prioritize in order to generate content that is flexible enough and adaptive. A good example of this is the responsive map solution described above: we load an image for mobile, and enhance the experience with a real map for desktops. The more responsive the website, the more complex dealing with content gets. Flexible code can help us to format adaptive content.

One way suggested by some people in the industry is to create responsive sentences by marking up sentences with a lot of spans that have classes, and then displaying certain ones according to screen size. Trimming parts of sentences for small devices is possible with media queries. You can see this technique in action on 37signals’ <a href="https://37signals.com/svn/">Signal vs. Noise</a> blog and in Frankie Roberto’s article “<a href="https://www.frankieroberto.com/responsive_text">Responsive Text</a>.” Even if such technique could be used to enhance small parts of a website, such as the footer slogan, applying it to all of the text on a website is hard to imagine.

This raises an issue in responsive Web design that will become more and more important in future: the importance of meta data and the semantic structure of content. As mentioned, the content on our websites does not only come from in-house writers. If we want to be able to automatically reuse content from other websites, then it has to be well structured and prepared for it. New HTML5 tags such as <code>article</code> and <code>section</code> are a good start to gaining some semantic meaning. The point is to think about and structure content so that a single item (say, a blog post) can be reused and displayed on different devices in different formats.

The big challenge will be to <strong>make meta data easily understandable</strong> to all of the people who are part of the content creation chain of the website. We’ll have to explain to them how the meta data can be used to prioritize content and be used to programmatically assemble content, while being platform-independent. A huge challenge will be to help them start thinking in terms of reusable blocks, rather than a big chunk of text that they copy and paste from Microsoft Word to their WYSIWYG content management system. We will have to help them understand that content and structure are two separate and independent things, just as when designers had to understand that content (HTML) and presentation (CSS) are best kept separate.

<strong>We can’t afford to write content that is oriented towards one only platform anymore.</strong> Who knows on which devices our content will be published in six months, or one year? We need to <a href="https://www.smashingmagazine.com/2013/01/14/preparing-websites-for-the-unexpected/">prepare our websites for the unexpected</a>. But to do so, we need better publishing tools, too. Karen McGrane gave a talk on “<a href="/2009/06/smart-fixes-for-fluid-layouts/">Adapting Ourselves to Adaptive Content</a>,” with some real example from the publishing industry. She speaks about the process of creating reusable content and introduces the idea of COPE: create once and publish everywhere. We need to build better CMSes, ones that can use and generate meta data to prioritize content. We need to explain to people how the system works and to think in terms of modular reusable content objects, instead of WYSIWYG pages. As McGrane says:
<blockquote>"You might be writing three different versions of that headline; you might be writing two different short summaries and you are attaching a couple of different images to it, different cut sizes, and then you may not be the person who is in charge of deciding what image or what headline gets displayed on that particular platform. That decision will be made by the metadata. It will be made by the business rules. […] <strong>Metadata is the new art direction</strong>."</blockquote>

Truncating content for small devices is not a future-proof content strategy. We need CMSes that provide the structure needed to create such reusable content. We need better publishing workflows in CMSes, too. Clunky interfaces scare users, and most people who create content are not particularly comfortable with complicated tools. We will have to provide them with tools that are easy to understand and that help them publish clean, semantic content that is independent of presentation.</p>

## Conclusion

As long as this article is, <strong>it only scratches the surface</strong>. By now, most of Smashing Magazine’s readers understand that responsive Web design is much more than about throwing a bunch of media queries on the page, choosing the right breakpoints and doubling the size of images for those cool new high-density phones. As you can see, the path is long, and we are not there yet. There are still many unsolved issues, and the perfect responsive solution does not exist yet.

Some technical solutions might be discovered in future using some of the new technologies presented here and with the help of the <a href="https://www.w3.org/">W3C</a>, the <a href="https://www.whatwg.org/">WHATWG</a> and organizations such as the <a href="https://filamentgroup.com/">Filament Group</a>.

More importantly, we Web designers and developers can help to find even better solutions. People such as <a href="https://www.lukew.com">Luke Wroblewski</a> and <a href="https://bradfrostweb.com/">Brad Frost</a> and all of the amazing women and men mentioned in this article are experimenting with a lot of different techniques and solutions. Whether any succeeds or fails, <strong>the most important thing is to share</strong> what we — as designers, developers, content strategists and members of the Web design community — are doing to try to solve some of the challenges of responsive Web design. After all, we are all in the same boat, trying to make the Web a better place, aren’t we?

<em>(al) (ea)</em>

