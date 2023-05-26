---
title: 'Your Image Is Probably Not Decorative'
slug: img-alt-attribute-alternate-description-decorative
author: eric-bailey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95585fe9-52b8-4bd4-adac-a3580ef87b98/img-alt-attribute-alternate-description-decorative.jpg
date: 2021-06-17T10:30:00.000Z
summary: >-
  Image placement on the modern web is highly intentional, helping to communicate the overall purpose of a page or view. This means that nearly every image you declare needs to have an alternate description.
description: >-
  Image placement on the modern web is highly intentional, helping to communicate the overall purpose of a page or view. This means that nearly every image you declare needs to have an alternate description.
categories:
  - CSS
  - Images
  - Usability
  - Accessibility
---

The `img` element’s [`alt` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-alt) can be “nulled,” which is the act of setting it to an empty string instead of a text description. Nulling an alt description means there is no information between the opening and close quotes. If there is an empty space, it will not be considered nulled:

<figure>

<pre>
  <code class="language-markup">&lt;img alt="" src="/images/cat.jpg" /&gt;</code>
</pre>
<figcaption><em>This image has been nulled.</em></figcaption>
</figure>

<figure>

<pre>
  <code class="language-markup">&lt;img alt=" " src="/images/dog.jpg" /&gt;</code>
</pre>
<figcaption><em>This image has not been nulled.</em></figcaption>
</figure>

## What Does “Decorative” Mean?

Nulling an image indicates that it is for decorative purposes only. 

In this context, decorative means that the image **does not visually communicate information** that is important to understanding the purpose of the page or view, and why the image is included as a part of that.

{{% pull-quote %}}
 Decorative does not mean that the image contains content that is considered as decoration.
{{% /pull-quote %}}

For example, a website that sells wallpaper will want to have alternate descriptions for wallpaper samples:

<pre><code class="language-markup">&lt;a href="/products/umbrella?variant=73849024783051"&gt;
  &lt;img 
    alt="Small red and white illustrated umbrellas on a teal background."
    src="/images/73849024783051.png" /&gt;
&lt;/a&gt;
</code></pre>

Another example could be a museum website, where presenting a piece from their collection could benefit from [both an alternate description and a caption](https://thoughtbot.com/blog/alt-vs-figcaption):

<div class="break-out">

 <pre><code class="language-markup">&lt;figure 
  role="figure"
  aria-label="View of Rotterdam, by Cornelis Boumeester. Date: about 1700–20. Accession Number: 2005.1057. In Dutch homes, tiles typically served utilitarian purposes, such as covering the walls of kitchens, utility rooms, passageways, and fireplace surrounds."&gt;
  &lt;img
    alt="A tile painting, composed of 33 Delft tiles forming a view of the port of Rotterdam. Set in a modern mahogany frame, with gilded inscription on bottom border."
    src="/collection/w0895/2005-1057.png" /&gt;
  &lt;figcaption&gt;
    View of Rotterdam, by Cornelis Boumeester. Date: about 1700–20. Accession Number: 2005.1057. In Dutch homes, tiles typically served utilitarian purposes, such as covering the walls of kitchens, utility rooms, passageways, and fireplace surrounds.
  &lt;/figcaption&gt;
&lt;/figure&gt;
</code></pre>
</div>

Make sure that your alternate description [includes punctuation](https://thoughtbot.com/blog/add-punctuation-to-your-alt-text), as well!

## Why Would You Want To Make An Image Decorative?

Assistive technology will skip over nulled images and not announce their presence. The reasons for wanting to do this are mostly historical.

### Old Layout Techniques

Early web development techniques relied on images to help them guarantee **consistent layout** across different operating systems, browsers, and browser versions. The most common example of this was a [`spacer.gif`](https://en.m.wikipedia.org/wiki/Spacer_GIF), a 1&times;1 transparent pixel that was stretched to different sizes to push content into place.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64430e56-7d61-49cb-a764-fe64aa2b805e/spacer-gif.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64430e56-7d61-49cb-a764-fe64aa2b805e/spacer-gif.png" width="800" height="332" sizes="100vw" caption="Three stretched spacer.gifs used to create an outer margin for the text, “Welcome to my homepage.” (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64430e56-7d61-49cb-a764-fe64aa2b805e/spacer-gif.png'>Large preview</a>)" alt="Three stretched spacer.gifs used to create an outer margin for the text, “Welcome to my homepage.”" >}}

This technique would typically use many **spacing images** to create a visual design. Without a way to silence their presence, these images would clutter up what assistive technology announced and make it confusing and time-consuming to navigate and take action on web content.

### Old Design Techniques

Before there were CSS properties such as [`box-shadow`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow), developers had to use techniques that chopped up the decorative styling to make it work with content of indeterminate height or width. This technique was called [9-slice scaling](https://en.m.wikipedia.org/wiki/9-slice_scaling), a term that refers to the 9 sections of content you would need to create.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74359175-f885-45e4-9916-33f49b8b516a/9-slice-scaling-technique.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74359175-f885-45e4-9916-33f49b8b516a/9-slice-scaling-technique.png" width="800" height="525" sizes="100vw" caption="The 9-slice scaling technique (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74359175-f885-45e4-9916-33f49b8b516a/9-slice-scaling-technique.png'>Large preview</a>)" alt="The text, “The 9-slice scaling technique used repeating background images for content with a flexible width or height.” surrounded by columns and rows for each of its four sides. In each of the four corners is a square area. In the square areas and columns and rows are generic image icons. The image icon repeats in the columns and rows, demonstrating how a texture can be tiled." >}}

Much like spacer images, 9-slice scaling used multiple images to create the desired visual effect. And, much like spacer images, the only way to **remove the clutter** these images created was to mark them as decorative.

{{% feature-panel %}}

### Redundant Announcements

There is the rare scenario where an image is repeated on a page or view, and it’s repeat placements don’t supply any additional context. You should be careful about marking an image decorative in this situation, as the lack of an announcement for a visible image may be confusing for [someone with low vision who is using a screen reader](https://adrianroselli.com/2017/02/not-all-screen-reader-users-are-blind.html).

### Supplemental Icons

Links and buttons that use icons should always have [an accessible name](https://www.tpgi.com/what-is-an-accessible-name/) that communicates functionality. If the design also incorporates an icon, the icon’s design does not need to be communicated.

<pre><code class="language-markup">&lt;button type="button"&gt;
  &lt;img src="icon-print.svg" alt="" /&gt;
  Print
&lt;/button&gt;
</code></pre>

If the component only uses an icon, the image itself should be used to create the accessible name:

<pre><code class="language-markup">&lt;button type="button"&gt;
  &lt;img src="icon-print.svg" alt="Print." /&gt;
&lt;/button&gt;
</code></pre>

Note that a visible text label is the preferred technique. A visible text label [can be translated](https://adrianroselli.com/2019/11/aria-label-does-not-translate.html) and [communicates purpose more directly](https://thomasbyttebier.be/blog/the-best-icon-is-a-text-label). 

<figure role="img" aria-label="I have no idea what this button does." style="width: 100%">
<button style="border-radius: 1em; display: block; width: 350px; height: 180px; margin: 0 auto; background: url('https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0338d05-368d-452d-921d-28169f28b7d0/mystery-button.svg');"></button>
<figcaption><em>I have no idea what this button does.</em></figcaption>
</figure>

## Contemporary Use

[Modern CSS layout](https://www.smashingmagazine.com/2019/05/display-grid-subgrid/) and styling techniques means that image placement is now highly intentional. This means that if an image is used, it is most likely going to need an alternate description.

Alternate descriptions should **communicate the image’s purpose**. That includes the image’s content, but may also include the reason it is included in context on the page or view it has been included in. This is one of the reasons [why alternate image descriptions will never be able to be fully automated](https://www.a11yproject.com/posts/2021-03-23-alternate-text-and-automation/).

{{% ad-panel-leaderboard %}}

## Other Ways Of Displaying Images

There are a few other ways to display an image on a page or view. It is important to ensure an alternate description is provided if the image contains **meaningful content** &mdash; regardless of the technique utilized.

### The `picture` Element

The [`picture` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture) does not have [an implicit role](https://www.tpgi.com/html5-accessibility-chops-when-to-use-an-aria-role/), meaning that its presence does not communicate any purpose to assistive technology. This means it can’t be used to semantically describe the presence of a “picture.”

The `picture` element is a container for `source` and `img` elements. Use the `img`  element’s `alt`  attribute to provide an alternate description for the parent `picture` element.

<div class="break-out">

 <pre><code class="language-html">&lt;a href="/product/9091866/color/3"&gt;
  &lt;picture&gt;
    &lt;source 
      srcset="9091866-3.avif" 
      type="image/avif" /&gt;
    &lt;img 
      alt="A black ankle-length boot with metal eyelets, yellow stitching, and a padded collar and tongue."
      src="9091866-3.png" /&gt;
  &lt;/picture&gt;
&lt;/a&gt;
</code></pre>
</div>

### Background Images

We can use CSS to declare an image as a background on an HTML element. This is most often used to add a sense of texture to a design. 

However, another popular technique is to use a `background-image` to place an image in such a way where the developer will not have control over the **size of the image** someone uploads. `background-image`, combined with other properties such as [`background-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-size) will ensure that content of an unknown size is displayed without breaking the design.

{{< codepen height="480" theme_id="light" slug_hash="OJprPwK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Background Image As Foreground Image Example](https://codepen.io/smashingmag/pen/OJprPwK) by <a href="https://codepen.io/ericwbailey">Eric Bailey</a>.{{< /codepen >}}

In a scenario like this, [our old friend `spacer.gif` might be helpful again](https://www.scottohara.me/note/2020/02/13/spacer-gifs-in-2020.html)!

### Inline SVG

SVG can be displayed by either linking to it via the `src` attribute in an `img` element, or by placing the SVG code inline in the page or view.

If you are using inline SVG, you need to [use SVG’s `title` (and potentially `desc`) element](https://www.smashingmagazine.com/2021/05/accessible-svg-patterns-comparison/) in place of an `alt` attribute.

<div class="break-out">

 <pre><code class="language-svg">&lt;svg 
  role="img" 
  aria-labelledby="icon-bookmark-desc"
  xmlns="https://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"&gt;
  &lt;title id="icon-bookmark-desc"&gt;Bookmark.&lt;/title&gt;
  &lt;path d="M19 21l-7-5-7 5V5a2 2 0 012-2h10a2 2 0 012 2z"/&gt;
&lt;/svg&gt;
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Equivalent Experience

In modern web design and development, displaying an image is a highly intentional act. Alternate descriptions allow us to explain the content of the image, and in doing so, **communicate why it is worth including**. 

Just because an image displays something fanciful doesn’t mean it isn’t worth describing. Announcing its presence ensures that [anyone, regardless of ability or circumstance](https://www.smashingmagazine.com/2020/05/equivalent-experiences-part1/), can fully understand your digital experience.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Accessibility In Chrome DevTools'" href="https://www.smashingmagazine.com/2020/08/accessibility-chrome-devtools/" rel="bookmark">Accessibility In Chrome DevTools</a></li>
<li><a title="Read 'A Complete Guide To Accessibility Tooling'" href="https://www.smashingmagazine.com/2021/06/complete-guide-accessibility-tooling/" rel="bookmark">A Complete Guide To Accessibility Tooling</a></li>
<li><a title="Read 'Accessible Images For When They Matter Most'" href="https://www.smashingmagazine.com/2020/05/accessible-images/" rel="bookmark">Accessible Images For When They Matter Most</a></li>
<li><a title="Read 'Accessible SVGs: Perfect Patterns For Screen Reader Users'" href="https://www.smashingmagazine.com/2021/05/accessible-svg-patterns-comparison/" rel="bookmark">Accessible SVGs: Perfect Patterns For Screen Reader Users</a></li>
<li><a title="Read 'Designing With Reduced Motion For Motion Sensitivities'" href="https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/" rel="bookmark">Designing With Reduced Motion For Motion Sensitivities</a></li>
<li>Read more articles on <a href="https://www.smashingmagazine.com/category/accessibility/">accessibility</a>, <a href="https://www.smashingmagazine.com/category/usability">usability</a> and <a href="https://www.smashingmagazine.com/category/ux">UX</a>.</li>
</ul>

{{< signature "vf, il" >}}
