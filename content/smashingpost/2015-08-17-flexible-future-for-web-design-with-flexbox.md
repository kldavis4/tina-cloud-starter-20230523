---
title: Laying Out A Flexible Future For Web Design With Flexbox Best Practices
slug: flexible-future-for-web-design-with-flexbox
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91986247-864a-45cf-9a95-51905eb59ecb/01-push-left-opt.png
date: 2015-08-17T23:59:38.000Z
author: ben-gremillion
description: >-
  CSS floats and clears define web layout today. Based on principles derived from centuries of print design, they’ve worked well enough — even if, strictly speaking, floats weren’t meant for that purpose. Neither were tables, but that didn’t stop us in the 1990s.
categories:
  - Design
  - Layouts
  - CSS
  - Flexbox
---
CSS floats and clears define web layout today. Based on principles derived from centuries of print design, they’ve worked well enough — even if, strictly speaking, floats weren’t meant for that purpose. Neither were tables, but that didn’t stop us in the 1990s.

Nevertheless, the <strong>future of web layout is bright</strong>, thanks to <a title="Flexbox Is As Easy As Pie – Designing CSS Layouts" href="https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/">flexbox</a>. The CSS layout mechanism lets us arrange elements in a truly web-like way. Some elements can be fixed, while others scroll. The order in which they appear can be independent of the source order. And everything can fit a range of screen sizes, from widescreen TVs to smartphones — and even devices as yet unimagined. <a href="https://caniuse.com/#search=flexbox">Browser support is fantastic</a> (except <em>you-know-who</em>). Yep, it’s a great time to jump into flexbox if you haven't done so yet.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Flexbox Is As Easy As Pie – Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [CSS Grid, Flexbox And Box Alignment](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)
*   [<span class="headline">The Flexbox Reading List: Techniques And Tools</span>](https://www.smashingmagazine.com/2016/02/the-flexbox-reading-list/)
*   [Harnessing Flexbox For Today’s Web Apps](https://www.smashingmagazine.com/2015/03/harnessing-flexbox-for-todays-web-apps/)

But changing our ways isn’t easy. <strong>Flexbox has a dizzying array of features</strong>, few of which are familiar. It’s a lot to take in. Luckily, for layout purposes, you need to know only a few basics. Let's take a look at how we could create a basic Gmail-like, flexbox-based interface. If you haven't explored or fully understood flexbox yet, this piece will revisit and explain a few things that might be confusing at first.

{{% feature-panel %}}

## The Flexbox Mindset

Flexbox requires a new way of thinking. Instead of arranging items in left-to-right, top-to-bottom rows and columns, we arrange blocks on a line — two lines, in fact, a main axis and a cross axis, the first of which we’ll use today. Think of the <strong>main axis as a rope</strong> along which boxes (divs or other HTML elements) are strung. The metaphorical rope runs from one end of its container to the other, a taut and invisible axis. This leads to four interesting concepts.</p>

### Alignment

First, we can slide the “boxes” to one side of the “rope” or the other, center them or distribute them evenly. That means objects can stick to one side of a layout or the other — say, to the left or right edge of the screen, no matter the screen’s width. Even distribution means they will adapt well to any size screen, which is ideal in our <a href="https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/">multi-screen world</a>.</p>

<figure><img loading="lazy" decoding="async"  class="alignnone" title="Illustration of boxes pushed to the left" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91986247-864a-45cf-9a95-51905eb59ecb/01-push-left-opt.png" alt="flexbox best practices" width="500" height="300" /><figcaption>Flexbox allows designers to push HTML elements to either end of the “rope.”</figcaption></figure>

### Direction

We can also <strong>reverse</strong> the string, so that boxes run in the opposite direction, without editing the HTML. This is similar to the <a href="https://foundation.zurb.com/docs/components/grid.html#source-ordering">sort-order technique</a> that lets us flip columns around — except the third trait takes that a step further.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d20da70e-3665-4a87-b571-1ad467b86aa5/02-flip-horizontal-opt.png" alt="Illustration of boxes pushed to the right." /><figcaption>Both the order and position of elements may be flipped.</figcaption></figure>

### Orientation

Thirdly, we can turn the rope by 90 degrees to dangle from the top of its container, instead of running from side to side. Media queries and flexbox’s ability make it possible to run items — say, a header, article and footer — down a smartphone’s screen but left to right on a desktop computer. What used to be called rows can now run top to bottom or bottom to top with a dash of CSS.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0821a6a-93ba-47d9-8586-3d46792d8642/03-vertical-hang-opt.png" alt="Illustration of boxes hanging from the top of a box." /><figcaption>The entire arrangement can turn 90 degrees, “hanging” from the top of the container.</figcaption></figure>

### Order

Finally, we can control which boxes come first, second, third and so forth on the rope <strong>without editing the HTML</strong>. This is huge. It means we can structure an HTML document for, say, <a href="https://www.smashingmagazine.com/2013/11/15/seo-for-responsive-websites/">SEO</a>, <a href="https://zurb.com/university/lessons/five-minutes-towards-an-accessible-page">accessibility</a> or plain ol’ <a href="https://html5doctor.com/lets-talk-about-semantics/">semantics</a> — independent of layout. Want to center elements vertically? No problem. Want navigation at the end of your HTML but at the beginning of your layout? Sure. Want to experiment with different layouts? It’s all in the CSS. And just like that, we’re already thinking in terms of content and devices, not rigid grids.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43d64cf5-8ae6-4271-bc43-3b21ba073c7c/04-reordered-horizontal-opt.png" alt="Illustration of boxes in random order." /><figcaption>The exact order of elements can change with CSS — and without changing the HTML.</figcaption></figure>

There’s more, but this covers the basics for now. To recap:

1.  Blocks are strung along an invisible line.
2.  We can push them to and fro along that line.
3.  We can reverse the line, thus reversing the boxes’ order.
4.  The line can turn 90 degrees.
5.  We can shuffle things along the line in any order we please, regardless of the HTML.</p>

## Order

Order is an important concept in flexbox. Let’s take a basic HTML document: A typical blog post would include certain bits of information.

*   **header** website title, description, search form (These frame the content and inform people where they are.)
*   **meta data** author/publisher, date, topic(s) (These help people decide whether the content is relevant to their needs.)
*   **main content** what the page is all about (the reason the page exists)
*   **supplemental content** related information (teasers, links, “See also”)
*   **navigation** links to elsewhere on the website (high-level topics)
*   **footer** copyright, RSS, social media, newsletter registration

These elements are listed in order of what search engines or screen readers might scan. Now, let’s dangle a “rope” from the top of a mobile device and reorder them to put content first.

1.  main content
2.  meta data
3.  supplemental content
4.  header
5.  navigation
6.  footer

Meanwhile, desktop computers would have a different view.

1.  header
2.  meta data
3.  main content
4.  supplemental content
5.  navigation
6.  footer

Wait, that’s not quite right. We want navigation at the top, and flexbox makes that a snap.

It follows that you can also put “ropes” inside of boxes, and all of the rules apply anew. But first, let’s talk about order. Here’s where things get tricky.</p>

## Nesting Ropes And Boxes

Each flexbox layout — each box — can contain another set of boxes strung along their own rope. That rope can run from left to right or vice versa, from top to bottom or vice versa, and push objects to either end, center them or distribute them. And while that flexibility opens up many possibilities, it also means we need to plan our layouts carefully.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd9167aa-bdd3-4639-bd48-cb383882df26/05-nested-horizontal-opt.png" alt="Illustration of boxes within a box." /><figcaption>Elements along a flexbox rope may, in turn, contain other flexbox ropes.</figcaption></figure>

Let’s start with some content to understand why things get complicated; this isn’t necessarily in order of layout (i.e. the order in which people see it). Imagine giving a presentation to an audience. You tell them what you’re going to say, then you say it, and you wrap up with a summary of what you’ve said. Our hypothetical page follows a familiar structure:

*   header
*   the current message
*   message list
*   links to inbox(es), archive, etc.
*   footer

## Sketch A Design

To keep things simple, we’ll work with a familiar layout.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7515800-2ac8-455e-b803-16a8d71d0858/06-gmail-diagram-opt.png" alt="Illustration of an email app layout" /><figcaption>A typical arrangement for an email app.</figcaption></figure>

There are two flexbox layouts here. The first has three boxes from top to bottom. The second layout resides inside the middle box, from right to left.

The header and footer span the width of the viewport. The navigation fits in a small column to the left, and the content area lets the user scroll when it contains more information than can be displayed. We could achieve this with a few floats and fixed positions, but flexbox gives us more options with less markup. Let’s take a look.</p>

## Set Up The Document

The outer container has only three sections, wrapped in a <code>.flex-container</code> element:

<pre><code class="language-markup">&lt;body&gt;
  &lt;div class="flex-container"&gt;
    &lt;header&gt;…&lt;/header&gt;
    &lt;main class="flex-container"&gt;…&lt;/main&gt;
    &lt;footer&gt;…&lt;/footer&gt;
  &lt;/div&gt;
&lt;/body&gt;
</code></pre>

We call it <code>flex-container</code> to describe its purpose in a somewhat semantic way. At least our CSS will make sense.

Inside the <code>main</code> element, we need three blocks:

<pre><code class="language-markup">&lt;main class="flex-container content"&gt;
  &lt;article class="message"&gt;…&lt;/article&gt;
  &lt;div class="message-list"&gt;…&lt;/div&gt;
  &lt;nav class="mailbox-list"&gt;…&lt;/nav&gt;
&lt;/main&gt;
</code></pre>

This example uses <code>article</code> as an independent entity, <a href="https://html5doctor.com/lets-talk-about-semantics/#what-about-adding-more-elements">not in the magazine sense</a>.</p>

## Declare These Elements As Flexbox

We need to tell browsers that these elements will be, um, flexible.</p>

<pre><code class="language-css">.flex-container,
.flex-container header,
.flex-container footer {
  display: -webkit-box;
  display: -moz-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
}
</code></pre>

Note that this applies flexbox to the major containers, not the content.</p>

## Add Some Dimensions

Based on the design sketch, we know that certain elements will have widths and heights. The <code>body</code>’s header and footer, for example, will be long, thin strips compared to the <code>main</code>’s tall, relatively narrow left-hand navigation bars. The <code>article</code>’s content area fills the rest of the space. In the interest of staying flexible regardless of screen size (and clarity in this tutorial), these areas won’t have fixed widths.</p>

<pre><code class="language-css">.message {
  flex-basis: 70%;
}
.message-list {
  flex-basis: 15%;
}
.mailbox-list {
  flex-basis: 15%;
}
.flex-container header,
.flex-container footer {
  width: 100%;
  height: 5rem;
}</code></pre>

Here, <code>flex-basis</code> is like width — as long as the main axis is horizontal. If we dangle the rope from the top, then <code>flex-basis</code> becomes height automatically. Handy!

## Make The Main Section Scrollable

This one’s easy. Just add <code>overflow: scroll</code> to the <code>main</code> element to keep it from overriding the header and footer. <strong>Handy tip:</strong> Try <code>overflow: auto</code> to hide scroll bars (when they’re unnecessary) <a href="https://caniuse.com/#search=overflow">in most browsers</a>.</p>

<pre><code class="language-css">.message {
  flex-basis: 70%;
  overflow: scroll;
}</code></pre>

## Test The Content

At this point, the header’s form should float with a little margin, even when the browser is resized. The content should flow well in browser windows of any size. And if a browser doesn’t support flexbox, then the page will turn into a content-first layout.

That’s important because <a href="https://caniuse.com/#search=flexbox">you-know-who doesn't support flexbox</a> yet. Every modern version does, however, so it’s a matter of when users update their software. So, where is flexbox supported?

*   [Chrome 31 and later](https://clicky.com/marketshare/global/web-browsers/google-chrome/)
*   [Firefox 31 and later](https://clicky.com/marketshare/global/web-browsers/firefox/)
*   [Internet Explorer 10 and later](https://clicky.com/marketshare/global/web-browsers/internet-explorer/)
*   [Safari for Mac version 7 and later](https://clicky.com/marketshare/global/web-browsers/safari/)
*   Safari for iOS 7.1 and later
*   Android browser 4.4 and later
*   Chrome for Android 42 and later
*   Opera 27 and later

Clicky has a graph of the <a href="https://clicky.com/marketshare/global/web-browsers/mobile/">marketshare of assorted mobile browsers.</a>

What about older browsers? Solutions vary wildly depending on the layout you’re trying to achieve, although we can derive a few tips.

The safest way to support flexbox-incapable browsers is to write CSS in the order in which you want it to appear. Start by <a href="https://www.smashingmagazine.com/2013/08/20/semantic-css-with-intelligent-selectors/">thinking semantically</a>. Old versions of Internet Explorer will ignore flexbox properties — thankfully, good ol’ <a href="https://www.quirksmode.org/css/condcom.html">conditional comments</a> enable us to apply floats and clears to semantic layouts. Old versions of other browsers tend to give you mobile-friendly layouts that stack content in a logical order. So flexbox can co-exist with floats, <code>display: table-cell</code> and positioning, so that smart browsers will apply flexbox properties while legacy browsers will ignore them. Finally, if you’re feeling experimental, then try <a href="https://flexiejs.com">Flexie</a>, which amends old browsers with a JavaScript-based polyfill.

Give flexbox a go. While it offers many options, most — such as alignment — come into play after you’ve settled on how elements are arranged. The central techniques, which we’ve covered here, are alignment, direction, orientation, order and nesting. We’ve found these to be critical in Foundation's new layout framework: If you can wrap your head around alignment, direction, orientation and order, then you’re well on your way to a flexible future. <a href="https://codepen.io/benthinkin/pen/wadabR">Check out my demo</a> to see it in action (keep in mind that it's not responsive just yet).</p>

## Further Reading

To learn more about flexbox, check out the following:

*   Flexbox in 5 Minutes, a flexbox playground tool
*   [Flexbugs](https://github.com/philipwalton/flexbugs), a community-curated list of flexbox issues and cross-browser workarounds for them.
*   [Flexy Boxes: Flexbox Playground and Code Generator](https://the-echoplex.net/flexyboxes/), Pete Boere
*   “[Using Flexbox to Lay Out Web Applications](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Using_flexbox_to_lay_out_web_applications),” Mozilla Developer Network
*   “[Flexbox](https://tympanus.net/codrops/css_reference/flexbox/),” Sara Soueidan, Codrops A reference article
*   “[A Visual Guide to CSS3 Flexbox Properties](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties),” Dimitar Stojanov
*   “[CSS Flexible Box Layout Module Level 1](https://dev.w3.org/csswg/css-flexbox-1/),” W3C The official specification

{{< signature "da, ml, al" >}}

