---
title: Rapid Prototyping For Any Device With Foundation
slug: rapid-prototyping-for-any-device-with-foundation
image: null
date: 2011-10-25T10:17:15.000Z
author: dmitry-dragilev
description: >-
  _**Editor’s note**: This article is the second piece in our new series
  introducing new, useful and freely available tools and techniques presented
  and released by active members of the Web design community (the first article
  covered
  [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/),
  a new tool be Lea Verou). ZURB are well-known for their wireframing and
  prototyping tools and in this post they present their recent tool,_
  Foundation, _a framework to help you build prototypes and production code
  that’s truly responsive._
  "Foundation")](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/)

  You’ve probably already heard about responsive design, which is website design
  that responds to the device constraints of the person viewing it. It’s a hot
  topic right now, and with good reason: alternative devices outsell desktop PCs
  4 to 1 already, and within three years more Internet traffic in the US will go
  through mobile devices than through laptops or desktops.

  All of this is forcing a convergence on what Jeremy Keith calls the “one Web”:
  a single Web that doesn’t care what device you’re on, how you’re viewing
  content or how you’re interacting with it.
categories:
  - Coding
  - Frameworks
  - CSS
  - Prototyping
---
<em>ZURB are well-known for their wireframing and prototyping tools and in this post they present their recent tool,</em> Foundation,<em> a framework to help you build prototypes and production code that’s truly responsive.</em>

You’ve probably already heard about responsive design, which is website design that responds to the device constraints of the person viewing it. It’s a hot topic right now, and with good reason: alternative devices outsell desktop PCs 4 to 1 already, and within three years <a href="https://www.idc.com/getdoc.jsp?containerId=prUS23028711">more Internet traffic in the US will go through mobile devices</a> than through laptops or desktops.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Design Better And Faster With Rapid Prototyping](https://www.smashingmagazine.com/2010/06/design-better-faster-with-rapid-prototyping/)
*   [Optimizing Your Design For Rapid Prototype Testing](https://www.smashingmagazine.com/2015/12/optimizing-your-design-for-rapid-prototype-testing/)
*   [The Skeptic’s Guide To Low-Fidelity Prototyping](https://www.smashingmagazine.com/2014/10/the-skeptics-guide-to-low-fidelity-prototyping/)
*   [Choosing The Right Prototyping Tool](https://www.smashingmagazine.com/2016/09/choosing-the-right-prototyping-tool/)

All of this is forcing a convergence on what Jeremy Keith calls the “<a href="https://adactio.com/extras/slides/thereisnomobileweb.pdf">one Web</a>”: a single Web that doesn’t care what device you’re on, how you’re viewing content or how you’re interacting with it.

{{% feature-panel %}}

What we found at ZURB was that while the concept of one Web is strong and the need for responsive websites great, the tools to help us quickly build that way just didn’t exist. That’s why we built <a href="https://foundation.zurb.com">Foundation</a>, a framework to help you build prototypes and production code that’s truly responsive.</p>

## The Problem with Global CSS

For years at ZURB, we used and refined a global CSS file that included a nice 960 grid, typography styles, buttons and other common elements. The trouble with our global CSS was that none of these pieces were written to be used by others, so they required a good deal of ramping up and training, with no great documentation.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117049" style="border: 1px solid #CCC" title="styleguide" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e210bbe6-a0c6-4726-98a9-17d656bf9f66/styleguide.png" alt="screenshot" width="550" height="309" />

<em>Our CSS style guide had a lot of good global elements, but it wasn’t well documented, and it certainly wasn’t ready for other devices.</em>

The bigger problem was that it wasn’t designed to be responsive or mobile-friendly in any way. We were stuck in the same rut that a lot of designers are in: creating a 1000-pixel-wide canvas, putting a 960 grid on it, and calling it a day. Our tools were built to support that workflow. So, we rewrote it into <em>Foundation</em>, a framework for everyone to be able to rapidly prototype in a responsive way.

<a href="https://foundation.zurb.com"><img loading="lazy" decoding="async" title="foundation-header" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/746561f6-8ab0-4419-bf3a-54ea67262e45/foundation-header.jpg" alt="screenshot" width="500" height="148" /></a>

Foundation is an MIT-licensed framework that includes a nestable arbitrary-width responsive grid; mobile styles, buttons and typography; layout affordances such as tabs and pagination; forms; and useful JavaScript plugins. We wrote or packaged all of these pieces to achieve a few goals:

1.  Quickly train new designers, inside and outside ZURB, to use a common framework;
2.  Rapidly prototype websites for desktops and any mobile device;
3.  Easily customize and complete the prototype to turn it into production code for particular projects or clients.

The first goal can’t be overstated; the value of having a single set of styles and best practices that the team can iterate on as a whole and communicate to our clients is tremendous. We can ramp up new designers much more quickly, build things faster and work together more easily. On one recent project, we even got a volunteer sufficiently up to speed on Foundation that we could collaborate on code — and it took only about 15 minutes.</p>

## So, How Does Foundation Work?

The core of Foundation can be summed up in a few points:

*   **A 12-column, percentage-based grid with an arbitrary maximum width.**.  The grid can be nested and used for quite complex layouts, and it works all the way back to IE 7\. The grid reshuffles itself for smaller devices.
*   **Image styles that disregard pixels.**.  Images in Foundation are scaled by the grid to different widths.
*   **UI and layout elements.**.  Foundation includes common pieces such as typography and forms, as well as tabs, pagination, N-up grids and more.
*   **Mobile visibility classes.**.  Rapidly prototyping is partly about having built-in functionality to tailor the experience. Foundation lets you very quickly hide and show elements on desktops, tablets and phones.

We deliberately built Foundation as a starting point, not as a style guide. We’ve included some styles to help you rapidly build something clickable and usable, but not something stylistically complete. Everything in Foundation is meant to be customized, including button styles, form styles (even custom radio, checkbox and select elements), typography, and layout elements such as tabs.</p>

## The Grid

A lot of grids are floating around, including some very good ones <a href="https://www.smashingmagazine.com/2011/08/23/the-semantic-grid-system-page-layout-for-tomorrow/">right here on Smashing Coding</a>. Grid systems have a few issues, though, and we built Foundation to tackle them… well, some of them.</p>

### Fluidity

One of the critical pieces of device-agnostic design is having a fluid layout that conforms to the size (and orientation) of the device. Foundation’s grid is completely fluid, with percentage-based widths and margins, and it works all the way back to IE 7 (but not IE 6 — philosophically speaking, acting like IE 6 doesn’t exist makes sense at this point). The HTML markup is pretty simple. Here’s an example of the grid in use, where we nest it for a more complex layout:

<pre><code class="language-markup tmp-xml">&lt;div class="row"&gt;
  &lt;div class="eight columns"&gt;
	&lt;p&gt;…&lt;/p&gt;
	&lt;div class="row"&gt;
	  &lt;div class="six columns"&gt;
	    &lt;h5&gt;Another Section (.six.columns)&lt;/h5&gt;
	    &lt;p&gt;…&lt;/p&gt;
  &lt;/div&gt;
	  &lt;div class="six columns"&gt;
	    &lt;h5&gt;Another Section (.six.columns)&lt;/h5&gt;
	    &lt;p&gt;…&lt;/p&gt;
	  &lt;/div&gt;
      &lt;/div&gt;
    &lt;p&gt;Now the nested row has been closed, and we're back to the original eight-column section.&lt;/p&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>

You can check out the above code on this <a href="https://foundation.zurb.com/grid-example2.php">example page</a>.

<a href="https://foundation.zurb.com/grid-example1.php"><img loading="lazy" decoding="async" title="foundationgrids" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45209467-2785-4472-b384-d5bfc9a82bfd/foundationgrids.png" alt="screenshot" width="500" height="216" /></a>

<em>Here are some of the built-in grid constructs, all of which scale with the browser window.</em>

### Responsiveness

The second critical piece is for the grid to be able to easily adapt to small devices and their unique constraints. We tackled this in three ways:

*   On small devices (such as phones), the grid simply stacks vertically, with every column running the full width.
*   We’ve also included block-grid classes, which are definitions for ULs that can be two-up through five-up and that remain a grid even on very small devices.
*   And we have mobile visibility classes. These are a group of styles that enable you to quickly try things out by hiding and showing elements on different kinds of devices. You can attach classes like so:

<pre><code class="language-markup tmp-html">&lt;div class="hide-on-phones"&gt;
	&lt;p&gt;This is a paragraph that we don't want to see on small devices.&lt;/p&gt;
&lt;/div&gt;
&lt;div class="show-on-phones"&gt;
	&lt;p&gt;This paragraph will be shown only on phones, not on tablets or desktops.&lt;/p&gt;
&lt;/div&gt;</code></pre>

Another interesting use for the classes is to prototype a common mobile consideration: placing mobile navigation at the bottom, as opposed to its more common placement at the top. You could do this:

<pre><code class="language-markup tmp-html">&lt;nav class="hide-on-phones"&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a href=#&gt;…&lt;a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href=#&gt;…&lt;a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href=#&gt;…&lt;a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/nav&gt;
…
&lt;nav class="show-on-phones"&gt;
  &lt;dl class="mobile tabs"&gt;
    &lt;dd&gt;&lt;a href="#"&gt;…&lt;/a&gt;&lt;/dd&gt;
    &lt;dd&gt;&lt;a href="#"&gt;…&lt;/a&gt;&lt;/dd&gt;
    &lt;dd&gt;&lt;a href="#"&gt;…&lt;/a&gt;&lt;/dd&gt;
  &lt;/dl&gt;
&lt;/nav&gt;</code></pre>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117055" title="foundationdevices" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a3cc364-8451-4a1a-bea1-7ca1acd7ce2c/foundationdevices.jpg" alt="screenshot" width="550" height="227" />

<em>Foundation lets you write code once and show it on different devices easily.</em>

### Semantics

This one is tricky. A very compelling case is to be made that grid systems are by nature not semantic. This is partly true; they’re still descriptive of their function, but they do break the separation of data and display.

We didn’t want to base the Foundation framework on another extension, such as <a href="https://lesscss.org/">LESS</a>. LESS is a great tool enabling you to use variables, shortcuts and more in your CSS, but we didn’t want to have to rely on it and add another barrier to using Foundation. The recent article we mentioned above actually fixed the data and display issue of grids by using LESS, which is awesome, but Foundation doesn’t fix that. Here’s why…

All of these methods are a stopgap. The replacement technique might come out next month or next year, but really all of these tools will change drastically in the very near future. Tools like LESS help us get a little closer to a very clean solution, but at a higher technology and learning cost. We wanted Foundation to be the fastest way to prototype for all kinds of devices, so we paid a small price for truly separated markup.</p>

## Rapid Prototyping Examples

Let’s look at a recent example for which Foundation was used. Every year, we do a 24-hour design marathon for a local non-profit, usually producing new marketing collateral and a new website. This year, we chose Rebekah Children’s Services, a great organization that helps with adoptions and takes care of disadvantaged kids.

This year, we wanted to build a website that was really responsive, and we had very little time to do it. Using just Foundation, we started prototyping the website based on some sketches we had done. In two hours, we managed to build <a href="https://zurb.net/zurbwired2011/projects/zurbwired2011/frame/prototype/public/">this prototype</a>.

<a href="https://zurb.net/zurbwired2011/projects/zurbwired2011/frame/prototype.php"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="115473" title="rcsprototype" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e635b203-ecc7-493f-b04e-fd5df69f9f56/rcsprototype.jpg" alt="screenshot" width="500" height="273" /></a>

<em>Using Foundation, we built the prototype on the left in two hours (including every screen), and then started modifying it until it became the final website on the right.</em>

It’s not terribly pretty, but it did give us something we could click around in, add copy to and iterate on. In the prototype, we used only a bare minimum of custom styles to more accurately represent the intended visuals.

Once we completed the prototype, we were able to complete the visual design and apply it to the existing Foundation code base to produce the <a href="https://rcskids.org">final website</a>. The final website retains all of Foundation’s framework, with the new styles applied on top of it.</p>

### How to Further Tailor the Experience

We recently launched an app through which to give traditional design feedback on mockups and websites. It’s called <a href="https://www.spurapp.com">Spur</a>, and it has been great fun for us; not only is it in our wheelhouse (for design feedback), but building a responsive Web app was an awesome opportunity.

Spur has a number of tools and actions, as well as some simple forms and a fairly complex JavaScript- and HTML-loading animation. Adapting all of this to mobile devices could have been really painful, but by starting with Foundation, we cut down on that considerably and prototyped the app quickly.

<a href="https://spurapp.com"><img loading="lazy" decoding="async" title="foundationspur" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7b8fe2d-5abe-4d84-8e3d-340d34bb630a/foundationspur.jpg" alt="screenshot" width="500" height="202" /></a>

<em>Spur on a desktop is different than Spur on a mobile device such as an iPhone.</em>

Spur helped us get more comfortable with the constraints of a given device, including screen size, orientation, tap target size and copy. Spur is simpler on smaller devices, but it’s not stripped down. You can still capture a page, view it through the various filters, and share it with someone else.</p>

## Rapid Prototyping Is Required Now

The days of creating a blank Photoshop canvas and laying down a 960 grid are over, even if some of us are still working in that shared fantasy world. Mobile devices — or, let’s just say, devices beyond just laptops and desktops — are already prevalent and will only become more ubiquitous.

Don’t build a desktop website that’s pixel-perfect before thinking about other devices; get used to designing for several different sizes, and then quickly prototype your design to get a feel for the flow, function and interaction.

We built Foundation to help us do this faster and to develop better websites and apps for us and our clients. We feel so strongly about the need for this that Foundation is MIT-licensed and completely free to use, forever. If you try it out and have success with it, <a href="mailto:foundation@zurb.com">let us know</a>. We’d love to hear about it, just as we’d love to hear about bugs or issues that you’ve run into.

We’re excited about this watershed moment in Web design (and in connectivity and data availability), and you should be, too: our industry will change more in the next three years than it has in its entire history. We hope this helps.

{{< signature "al" >}}

