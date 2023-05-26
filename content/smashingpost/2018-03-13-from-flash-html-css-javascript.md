---
title: 'Moving From Flash To HTML, CSS, And JavaScript'
slug: from-flash-html-css-javascript
author: simon-owen
image: 'null'
date: 2018-03-13T12:10:45.000Z
summary: >-
  Flash was one of the reasons a lot of folks started building websites. Here
  are some of the groundbreaking things Flash could do back then, and how we can
  go about doing them today.
description: >-
  Flash was one of the reasons a lot of folks started building websites. Here
  are some of the groundbreaking things Flash could do back then, and how we can
  go about doing them today.
categories:
  - Flash
  - HTML
  - CSS
  - JavaScript
---
Back in the 2000s, it was commonplace to see websites that were built using Flash. By viewing the source of a website, you'd often see very little HTML and an embedded SWF file. This meant a few things. First, the browser didn't natively support Flash, so you had to download the Flash plugin. Browsers found it difficult to go into the SWF to read content. Amongst other things, this had a detrimental affect on SEO and accessibility.

In 2007, the iPhone was released. It didn't support Flash. In 2015, Google moved all its YouTube videos to HTML5. In July 2017, Adobe officially announced it would stop working on Flash by 2020. People used Flash because it could do things that HTML, CSS, and JavaScript couldn't do at the time. **It's incredible to see how far web standards have come** (and what’s coming).

We can do a lot today that was previously only possible with Flash. Not only that, but we can do it in a way that's far more accessible and performant. I'll go over some of the groundbreaking things Flash could do and how we can go about doing them today.

**Disclaimer**: *I love Flash, and it will always have a place in my heart, but for me at least, its time has passed. Just in case you’re wondering: there are still so many interfaces and engines running in Flash, especially for games, and this article addresses some of the issues that are very relevant there.*

{{% feature-panel %}}

## Video

One of the great things Flash heralded was [video](https://caniuse.com/#search=video), offering basic support as early as 2002. It wasn't until 2009 that the [`<video>` tag was introduced](https://en.wikipedia.org/wiki/HTML5_video) in Chrome, Safari, and Firefox. Furthermore, Internet Explorer (IE) 8 didn't support the `<video>` tag, and it wasn't until 2011, when IE 9 was released, that it got support.

Flash would use the `<object>` tag, like so:

<div class="break-out">

<pre><code class="language-markup">&lt;object classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" codebase="https://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=9,0,16,0" width="320" height="400"&gt;
  &lt;param name="movie" value="filename.swf"&gt;
  &lt;param name="quality" value="high"&gt;
  &lt;param name="play" value="true"&gt;
  &lt;param name="LOOP" value="false"&gt;
  &lt;embed src="video-filename.swf" width="320" height="400" play="true" loop="false" quality="high" pluginspage="https://www.macromedia.com/go/getflashplayer" type="application/x-shockwave-flash"&gt;&lt;/embed&gt;
&lt;/object&gt;
</code></pre></div>

Not the nicest of code, but it did work.

Now, we can simply write `<video src="filename.mp4" />`, although it is important to be aware of different video formats across browsers, the [most popular](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats) being MP4, Ogg and WebM.
Taking things a step further, it's possible not only to support the `<video>` tag, but also offer fallbacks and helpful alternatives:

<div class="break-out">

<pre><code class="language-markup">&lt;video width="320" height="400"&gt;
&lt;source src="filename.mp4" type="video/mp4" /&gt;
&lt;source src="filename.webm" type="video/webm" /&gt;
&lt;source src="filename.ogv" type="video/ogg" /&gt;

&lt;!-- Flash fallback --&gt;
&lt;object type="application/x-shockwave-flash" data="flash-player.swf?videoUrl=filename.mp4" width="320" height="400"&gt;
  &lt;param name="movie" value="flash-player.swf?videoUrl=filename.mp4" /&gt;
  &lt;param name="allowfullscreen" value="true" /&gt;
  &lt;param name="wmode" value="transparent" /&gt;
  &lt;param name="flashvars" value="controlbar=over&amp;image=placeholder.jpg&amp;file=flash-player.swf?videoUrl=filename.mp4" /&gt;
&lt;/object&gt;

  &lt;!-- Text Fallback --&gt;
  &lt;p&gt;No video support found. Please download the video below, or upgrade your browser: https://browsehappy.com/&lt;/p&gt;
&lt;/video&gt;

&lt;ul&gt;
  &lt;li&gt;&lt;a href="linktomovie.mp4"&gt;MP4 format&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="linktomovie.ogv"&gt;Ogg format&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="linktomovie.webm"&gt;WebM format&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
</code></pre></div>

## Video Background

Because YouTube makes use of the `<video>` tag and has an API, it's possible to create a full-screen background video. Take the following YouTube video link code, for example:

<div class="break-out">

<pre><code class="language-markup">https://www.youtube.com/embed/iMhq63PX8cA?controls=0&amp;showinfo=0&amp;rel=0&amp;autoplay=1&amp;loop=1&amp;mute=1
</code></pre></div>

Using the different parameters it's possible to change the way the video behaves.

<div class="break-out">

<pre><code class="language-markup">controls=0 Hides the controls.
showinfo=0 Hides extra information.
rel=0 Hides related content.
autoplay=1 Auto plays the video when the site is loaded.
loop=1 Loops the video.
mute=1 Mutes the sound.
</code></pre></div>

*For a full list, check the [IFrame Player API](https://developers.google.com/youtube/iframe_api_reference).*

Using CSS, we can set the video to be fixed in position and to fill the screen.

<pre><code class="language-css">.video {
  background: #000;
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  pointer-events: none;
}
</code></pre>

And with the use of media queries, we can set the video to be centered and can help keep the correct aspect ratio.

<pre><code class="language-css">@media (min-aspect-ratio: 16/9) {
  .video {
    height: 300%;
    top: -100%;
  }
}

@media (max-aspect-ratio: 16/9) {
  .video {
    width: 300%;
    left: -100%;
  }
}
</code></pre>

Here's the example put together, with Mr. Smashing Magazine himself presenting a talk:

{{< codepen height="480" theme_id="light" slug_hash="goELXN" default_tab="result" user="s10wen" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/s10wen/pen/goELXN/">Video Background Demo Using YouTube</a> by Simon Owen (<a href="https://codepen.io/s10wen">@s10wen</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

## Interaction And Gaming

Another thing Flash excelled at was interaction and gaming. The popular website [Miniclip](https://www.miniclip.com/) was founded in 2001 and hosted a wide range of Flash games. In 2008, it was valued at over £900 million and is still going today.

### JUST A REFLEKTOR

[JUST A REFLEKTOR](https://www.justareflektor.com/) is an interactive music video that rivals and even surpasses the capabilities of Flash. With the use of various web technologies, it's now possible to interact with the video using a mobile device, as well as at one point using your webcam so that you actually appeared in the music video yourself!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b61e9e41-5e2c-49e9-8cab-d68d94697f2d/just-a-reflektor.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b61e9e41-5e2c-49e9-8cab-d68d94697f2d/just-a-reflektor.png" sizes="100vw" caption="The website <a href='https://www.justareflektor.com/'>Just A Reflektor</a> makes great use of modern web technologies to create an interactive music video." alt="Just A Reflektor" >}}

### Cube Slam

There's some fantastic web-based Chrome experiments online today, such as [Cube Slam](https://experiments.withgoogle.com/chrome/cube-slam). Cube Slam is a game that makes use of WebRTC (an open web technology), letting you video chat and play a game within the browser. Although Flash was heavily used for video chat, it came with a number of drawbacks compared to WebRTC: It relied on the Flash plugin, it required a media server, and it had various security implications and poor performance.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6516ceba-3067-4ffd-ae58-8caec5fff40e/cube-slam.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6516ceba-3067-4ffd-ae58-8caec5fff40e/cube-slam.png" sizes="100vw" caption="<a href='https://experiments.withgoogle.com/chrome/cube-slam'>Cube Slam</a> is a web based Chrome Experiment that allows video chat whilst playing a game." alt="Cube Slam" >}}

### HTML5 Game Engines

There are a number of HTML5 and JavaScript [game engines](https://html5gameengine.com/). This [next example](https://work.goodboydigital.com/starwars/arcade/) makes use of `canvas` and `WebGL`. WebGL (Web Graphics Library) is an API built in JavaScript that allows interactive 2D and 3D graphics within the `<canvas>` tag.

As mentioned in Good Boy Digital's own post regarding the project (the creators of the example):

<blockquote>"Star Wars Arcade really pushes the boundaries of what’s possible with HTML5 and WebGL technologies. This allows for the creation of a single build that works seamlessly on both desktop and mobile browsers without having to download an app; the advantage of this being able to offer an ‘app like’ experience on all devices so anyone can enjoy it, instantly. No passwords, no App Stores, just hit the URL and play!"<br /><br />&mdash; <a href="https://dev.goodboydigital.com/client/goodboy/webby/starwars/">goodboy digital</a>, Star Wars Arcade Case Study</blockquote>

I especially love this bit: "Just hit the URL and play!" One of my earliest “Wow” memories of the web was having my [own website](https://web.archive.org/web/20050424155514/http:/s1.gq.nu/Homepagex.html) in 1999 and being able to type that URL into any computer connected to the web and view it. It seemed absolutely incredible to me that this was actually possible (and continues to amaze me to this day!).

## Browser Support

One of the advantages of building something—especially a game, due to the extra complexity—in Flash that is still relevant today is browser support. Browser support is generally pretty good these days, and [Can I Use](https://caniuse.com/) can help us to quickly find out about the state of browser support for a particular specification. However, there are still discrepancies that could cause issues. So, if you're OK with only supporting browsers that are installed with the Flash plugin you're working with, then you're likely not to encounter any cross-browser issues.

## Typography

Flash was originally designed as an animation tool. As such, it had various limitations with typography.

Flash had a pixel-grid system. If typography was laid on the grid at `X:100.3 :100.7` and, thus, out of alignment to the pixel grid, it would look blurred.

As a result, I found that pixel fonts were useful because they sat on the grid and remained crisp. Another limitation here would be if you used an 8-pixel font but set it to 10 pixels, it would go out of alignment with the grid and, again, be blurred.

Thankfully, today in HTML and CSS, we have a host of tools to help us. We can set fonts as an absolute unit in `px` (pixels) or, more common these days, use `ems` and `rems` to aid with responsive web design (I'll be covering more on this later).

Another issue with Flash and typography was fonts. If a font wasn't available on the device, a fallback font would be provided. To circumvent this in Flash, you could embed the font in the `.swf` file. By doing this, though, you added to the file size and, thus, the time that the SWF would take to download and appear.

That being said, what was possible with Flash was Scalable Inman Flash Replacement (sIFR). sIFR allowed HTML text to be replaced with Flash. Before this, in order to use custom fonts, we used images. However, using images didn't allow for selectable text, and it meant you had to create images manually. Moving on from sIFR, developers came up with Cufón. Cufón avoided the use of Flash by using an SVG and VML version of a font. It was faster than sIFR and didn't require the Flash plugin; but, again, with this technique, it wasn't possible to select text.

Today, we have the CSS @font-face rule and a host of standard web fonts available:

- [Google Fonts](https://fonts.google.com/)
- [Typekit](https://typekit.com/)
- [Font Squirrel](https://www.fontsquirrel.com/)

In Chrome and Firefox (and, hopefully soon, Safari), we have [`font-display`](https://caniuse.com/#search=font-display) in CSS. If you’re using a custom font, by default the browser will wait to get the custom font. If it can't get the custom font, it will use a backup font (the speed varies among browsers, but it is usually 3 seconds). This is known as a flash of invisible text (or FOIT). To improve this scenario, we can use the following:

<pre><code class="language-css">@font-face {
  font-display: swap;
}
</code></pre>

By using `swap`, we'll see the text immediately using the backup font. When the custom font is loaded, the browser will swap the backup for it. This way, the user gets to read the content as soon as it's available.

## Animation

One of the things that Flash did very well was tweening. Tweening is used to animate elements. In Flash, you could create an element in a keyframe, duplicate that keyframe along the timeline, and then add a tween.

{{< vimeo id="256058737" >}}

With HTML and CSS, we can apply the same animation using `@keyframes`, `transform` and `animation`.

<pre><code class="language-html">&lt;div class="box"&gt;&lt;/div&gt;
</code></pre>

<pre><code class="language-css">.box {
  width: 100px;
  height: 100px;
  background-color: #333;
}

@keyframes move {
  from {
    transform: translateX(0);
  }

  to {
    transform: translateX(200px);
  }
}

div {
  animation-duration: 3s;
  animation-name: move;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="GydaQY" default_tab="result" user="s10wen" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/s10wen/pen/GydaQY/">CSS Animation Example</a> by Simon Owen (<a href="https://codepen.io/s10wen">@s10wen</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

{{< vimeo id="256060637" >}}

With Chrome Developer Tools, we can inspect and adjust the animation by going to `Chrome Dev Tools` → <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> → `Animation`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91b58a97-2ac8-4c1f-8c0f-049f7588df09/chrome-dev-tools-performance-tab.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91b58a97-2ac8-4c1f-8c0f-049f7588df09/chrome-dev-tools-performance-tab.png" sizes="100vw" caption="An example showing Chrome Developer Tool’s 'Performance' tab." alt="Chrome Developer Tool’s 'Performance' tab." >}}

It's also possible to debug potential performance issues that may arise when dealing with animation. In Chrome Developer Tools, there's a “Performance” tab. By clicking this, then the “Record” circle icon, we can see a range of useful information. This technique greatly helped me when I built Mind's [Annual Report 2012-13](https://report.mind.org.uk/2013/), particularly the section of the website that has a map with animated circles showing the locations of Mind shops. Initially, the map section was loaded at the start, which caused repaint issues. Using the “Performance” tab, I was able to identify and update this, so the map only started animating when it was in view.

{{< vimeo id="256060641" >}}

## Vector Graphics

The web has benefitted and still does benefit enormously from careful consideration of file size. Back in the early 2000s, the web was mostly viewed on desktop computers, with slow dial-up modems. A simple image could take seconds or even minutes to load. To help with this, Flash made heavy use of vector graphics. Using vector graphics, where appropriate, instead of JPEG or GIF images, significantly reduced file size and thus load more quickly over the web.

Over the past few years, and particularly thanks to [Sara Soueidan](https://twitter.com/sarasoueidan), scalable vector graphics (SVGs) have become more and more widespread on the web. SVG is an XML-based markup that enables us to create vector graphics for the web. It works extremely well with animation and I've had the pleasure of building some websites that make use of this: the [Mind report](https://report.mind.org.uk/2013/) website (previously mentioned) and [How Clean Is England?](https://s10wen.com/blog/2014/11/19/how-clean-is-england/) which Sara mentioned on Twitter!  Thanks Sara!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23231d77-51dc-4ee0-8b64-db012ef0cb3c/mind-annual-report-2012-2013.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23231d77-51dc-4ee0-8b64-db012ef0cb3c/mind-annual-report-2012-2013.png" sizes="100vw" caption="Mind’s <a href='https://www.awwwards.com/sites/how-clean-is-england'>Annual Report</a> website made use of SVGs and animation to create a fun way to display their statistics for the year." alt="#" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a40ab2c4-6651-49ee-8cb4-842f96b195da/how-clean-is-england.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a40ab2c4-6651-49ee-8cb4-842f96b195da/how-clean-is-england.png" sizes="100vw" caption="The <a href='https://s10wen.com/blog/2014/11/19/how-clean-is-england/'>How Clean Is England?</a> website was heavily based on illustration. SVGs and CSS animations helped to make the illustrations look crisp and keep file sizes to a minimum." alt="#" >}}

## Responsive Web Design

One of the main pitfalls of building a website in Flash today is the lack of media queries. Today, mobile and tablet usage has surpassed that of desktop. In order [to create the best experience](https://www.smashingmagazine.com/responsive-web-design-guidelines-tutorials/), we must create a website that is accessible on all of these devices. On many devices, Flash will simply not load at all, and even if it did, it would most likely breach the viewport’s width or would scale and be unusable.

Using media queries, we can create a layout that responds to the content. Here's an example:

<div class="break-out">

<pre><code class="language-html">&lt;div class="someContent"&gt;
  &lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipisicing elit. Est excepturi enim id ratione blanditiis voluptate dolore necessitatibus culpa maxime eius assumenda eveniet dolores odit sunt repellat, rerum amet delectus vel.&lt;/p&gt;
&lt;/div&gt;
</code></pre></div>

<pre><code class="language-css">.someContent {
  color: green;
}

@media screen and (min-width: 400px) {
  .someContent {
    color: yellow;
  }
}

@media screen and (min-width: 600px) {
  .someContent {
    color: red;
  }
}
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="ZvRbyX" default_tab="result" user="s10wen" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/s10wen/pen/ZvRbyX">Simple Media Query Example</a> by Simon Owen (<a href="https://codepen.io/s10wen">@s10wen</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

{{< vimeo id="256060664" >}}

## ActionScript vs. JavaScript

ActionScript is used in Flash and, thus, has the same pitfall of SWF files mentioned earlier, in that it requires the Flash plugin. JavaScript, on the other hand, is readily available in all modern browsers.

Let's look at an example of setting a variable in both and their differences:

<pre><code class="language-javascript">var x:Number = 42;
</code></pre>

<pre><code class="language-javascript">var x = 42;
</code></pre>

With ActionScript, we declare that the variable is a number. If the variable is assigned anything else, it will get an error. JavaScript is loosely typed, which means we could assign the variable as something else, such as a string:

<pre><code class="language-javascript">var x = '42';
</code></pre>

In JavaScript, if we wanted to [check that it is a number](https://jsbin.com/rigepukiru/1/edit?html,js,console,output), we could use `typeof(x);`, and this would output “number”. Another option would be to create a `function` and use `isNaN` to detect whether it is “not a number”:

<div class="break-out">

<pre><code class="language-javascript">function isNumber(value) {
  if (isNaN(value)) {
    return value + ' is not a number.';
  }
  return value + ' is a number.';
}

console.log(isNumber(42)); // "42 is a number."
console.log(isNumber('forty two')); // "forty two is not a number."
</code></pre></div>

## Collaboration

With HTML, CSS, and JavaScript (and many other coding languages), Git and GitHub make collaboration extremely easy. For example, if I wanted to edit the HTML of Smashing Magazine's “Author Template,” via GitHub, I could click the “Fork” button. This would create a version of the files (also known as the repository) under my own name. I could then make any amendments I like and submit a pull request. This would give the owner at Smashing Magazine the ability to review my pull request and accept or reject it. Once accepted, the code would go in the main repository.

There are a number of great reasons for working in this way: You always have a backup of your work; you can revert to previous versions of your work, and collaboration becomes very easy. Someone could be working on one section of the website, or on the CSS or JavaScript, and when each team member has finished, you could review the changes and pull them in as required.

If we tried the same with Flash, it would be a lot more difficult having to save and send an `.fla` file each time. If multiple people were to work on the same `.fla`, things could get very confusing. With HTML, CSS and JavaScript, it's' possible to do a “diff” on the code, which allows us to compare and review the code. We can even select certain code chunks, bring them in, or comment on them for further review and work.

## Conclusion

Flash was one of the reasons I started building websites. It pioneered in a lot of areas, and this led to people creating amazing things with it. Over the years, it's pushed the web forward a great deal. Adobe’s official announcement of dropping support of Flash, though, does raise concerns. It would be a massive shame if millions of websites using Flash were lost. There's a [petition](https://github.com/pakastin/open-source-flash) to open source Flash and Shockwave. I do hope we don't lose it forever. We’ve had some great &mdash; and weird &mdash; times.
I'll leave you with this classic example of the “weird” to which I refer:

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/EIyixC9NsLI" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

Here are the [lyrics](https://en.wikipedia.org/wiki/Badgers_(animation)), if you'd like to sing along.

{{< signature "ra, hj, al, il" >}}

