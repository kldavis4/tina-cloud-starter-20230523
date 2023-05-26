---
title: How To Maintain Hierarchy Through Content Choreography
slug: maintain-hierarchy-content-choreography
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22b7e4a8-4dd1-4221-8e14-1ae3fbeee5a6/content-01.jpg
date: 2013-04-25T19:57:04.000Z
author: steven-bradley
description: >-
  One of the issues we need to be concerned with in responsive design is how to
  maintain hierarchy as elements on the screen are resized and reflowed. Trent
  Walton first called attention to the issue with his post “Content
  Choreography,” which showed how visual hierarchy gets lost when columns are
  dropped below one another.
categories:
  - Design
  - Content
  - Responsive Design
  - Flexbox
---
One of the issues we need to be concerned with in <a href="https://www.smashingmagazine.com/2013/03/11/responsible-web-design/">responsive design</a> is how to maintain hierarchy as elements on the screen are resized and reflowed. Trent Walton first called attention to the issue with his post “<a href="https://trentwalton.com/2011/07/14/content-choreography/">Content Choreography</a>,” which showed <strong>how visual hierarchy gets lost</strong> when columns are dropped below one another.

While techniques exist to help with part of the problem, the solution also requires conscious thought in <a href="https://www.smashingmagazine.com/2013/01/14/preparing-websites-for-the-unexpected/">how you structure blocks of content</a> in your HTML. You need to think about how you’ll want to rearrange blocks of content as your design moves from single to multiple columns.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Content Strategy: Optimizing Your Efforts For Success](https://www.smashingmagazine.com/2011/06/content-strategy-optimizing-your-efforts-for-success/)
*   [Quick Course On Effective Website Copywriting](https://www.smashingmagazine.com/2012/05/quick-course-on-effective-website-copywriting/)
*   [Content: A Blessing, A Bubble, A Burden](https://www.smashingmagazine.com/2012/08/content-blessing-bubble-burden/)
*   [Content Knowledge Is Power](https://www.smashingmagazine.com/2013/04/content-knowledge-is-power/)

## What Is Content Choreography?

As a layout changes from a widescreen to a tablet to a smartphone, the number of columns is usually reduced from three or four down to one. The typical and easiest solution is to drop the columns one by one and stack them on top of each other.

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6980c763-f717-4591-88bb-225d7e1bedb6/dropping-columns.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158624" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6980c763-f717-4591-88bb-225d7e1bedb6/dropping-columns.png" alt="Diagram showing how columns drop in a typical 3 column responsive design" width="500" height="350" /></a><br>
<em>The figure above shows three columns of content. The lines below the two right columns indicate that each will drop below the main content as the screen’s width decreases.</em>

Once you’re down to a single column, the layout is constrained by the source order of the content blocks in the HTML. Whichever column comes first in the HTML is displayed at the top; whichever column is next in the HTML goes right below; and so on down the stack.

Unfortunately, this means that information that is highly visible at the top of the page when multiple columns are present ends up being far down the page as one column drops below another. If content is important enough to show at the top of the page when viewed on a widescreen browser, <strong>do we want to bury it on a smartphone screen?</strong>

All of the information in your sidebar column probably isn’t as important as all of the information in your main content column, but some of the sidebar content is likely more important than some of the main content.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16ba8f14-ff82-48e9-baa2-9841a4953c1b/single-columns.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158626" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16ba8f14-ff82-48e9-baa2-9841a4953c1b/single-columns.png" alt="Two examples of single column responsive designs" width="500" height="651" /></a><br>
<em>The left side of the figure above shows a single column layout, where each column drops in its entirety below the previous one. The right side shows elements from each column mixing with other elements.</em>

The left side of the image above shows the typical column drop. As the design is reduced to a single column, the content inside each container or column is dropped below all of the content in another container.

<strong>Ideally, the visual hierarchy would be maintained</strong>, and the content in different columns would intermix as the design moves from three columns to two to one. We’d also like more control over the display order of content, beyond the HTML source order. Both scenarios are illustrated on the right side of the image above.

This greater control over the blocks inside containers is what’s considered content choreography. I assume Trent chose the word “choreography” as a metaphor for how we’d like to orchestrate the movement of blocks of content as our layout changes.

Our current development practices don’t make this choreography easy. What they do make easy is dropping entire columns one below the other, which means that everything inside one column must always end up in its entirety above or below everything in another column.</p>

### Two Problems in One

What I’ve described above are really two separate problems:

*   **Source order**.  In a single-column layout, blocks of content will display in the same order as they’re located in the HTML structure. Unfortunately, the best source order for one layout isn’t necessarily the best source order for another.
*   **Intermixing content**.  Instead of having to drop entire columns of content below one another, we’d like to mix blocks of content from the different columns in the single-column layout.

The first issue has some technical solutions on the way, one of which is just about here. The second issue will require that we change our thinking in how we develop layouts.</p>

## Solving The Source-Order Problem

In time, there will be several solutions to the source-order issue, in the form of <strong>new CSS specifications</strong>. Depending on which browsers you need to support and what you’re willing to do to support them, one of those specifications may already be here.

Three specifications that we’ll likely find ourselves using in the future are:

*   “[Flexbox](https://www.w3.org/TR/css3-flexbox/),”
*   “[Regions](https://dev.w3.org/csswg/css3-regions/),”
*   “[Grid Layout](https://dev.w3.org/csswg/css3-grid-layout/).”

The second and third of these specifications have almost no support in current browsers. Surprisingly, Internet Explorer is leading the way with both. IE 10 supports regions and grid layouts with the <code>-ms</code> vendor prefix. No other browser offers any support at the moment, so we’ll have to wait on these specs a bit longer.

Flexbox, however, <a href="https://caniuse.com/#search=flex">has pretty good support</a>. The spec has undergone some changes, and two <a href="https://css-tricks.com/old-flexbox-and-new-flexbox/">versions are currently supported by browsers</a>. If you don’t mind <a href="https://css-tricks.com/using-flexbox/">mixing the old and new syntaxes</a>, you can get flexbox to work in the current versions of almost all browsers.

<strong>Opera mini and IE below version 10 don’t support any flexbox syntax.</strong> However, you can use the <a href="https://flexiejs.com/">Flexie polyfill</a> to add support for IE. Flexie uses the old flexbox syntax, but it does support IE as far back as version 6. Flexbox deserves its own article to be explained in detail, so I’ll point you to some articles I’ve written showing the <a href="https://www.vanseodesign.com/css/flexbox/">old syntax</a> and the <a href="https://www.vanseodesign.com/css/flexbox-revisited/">new syntax</a>, as well as one that walks you through the <a href="https://www.adobe.com/devnet/html5/articles/working-with-flexbox-the-new-spec.html">new syntax to set up a responsive layout</a> that overcomes the issue of source order.

Suffice it to say that with a single CSS property, we can essentially tell our documents to display blocks of content in a different order than how the source code orders the blocks in the HTML. Jordan Moore has also written about <a href="https://www.jordanm.co.uk/post/21863299677/building-with-content-choreography">flexbox and content choreography</a>, and he’s created a <a href="https://www.jordanm.co.uk/lab/contentchoreography">demo to illustrate</a>.

What you should take away from this section is that solutions to the source-order problem are coming soon — one of them very soon. It won’t be long before we can easily rearrange blocks inside a single container. However, rearranging blocks inside one container isn’t the same as rearranging them across several containers.</p>

## Solving The Intermixing Content Problem

Unlike the source-order problem, the issue of intermixing content across columns doesn’t have a technical solution. It’s up to us, and, ultimately, it means we need to wrap content in fewer HTML containers.

We’ll have to dig a little deeper into the problem to understand why this is so.</p>

### CSS Visual Formatting Models

CSS offers several <a href="https://www.w3.org/TR/CSS2/visuren.html#visual-model-intro">visual formatting models</a>, such as the normal document flow, floated elements and positioned elements. Flexbox is part of another, the <a href="https://www.w3.org/TR/css3-flexbox/">flexible box layout model</a>. In all of these models, elements are located relative to a containing element.

We can make it look as though elements are not bound by their containers, but they still are. For example, you could float an element that’s inside one column and give it a negative margin so large that it appears to be located in another column, however, elements in that other column won’t reorient themselves. To these elements, the floated element is still in the first column.

Other elements in the first column may relocate themselves to fill the now vacated space, but elements in the second column won’t. <strong>Even positioned elements are positioned relative to some parent</strong>, although that parent might be the <code>html</code> element itself. When you absolutely position an element and move it somewhere on the screen, other elements won’t get out of the way. We need them to get out of the way, though, if we’re going to intermix page elements.

With a little thought and CSS, you can usually figure out some way to rearrange elements inside one container however you like. With a little more thought, you can even make elements in one container appear to be located inside another, although you’ll usually have to position the elements in that other container with more complex CSS and with what <a href="https://csswizardry.com/2012/11/code-smells-in-css/">Harry Roberts refers to as “magic numbers</a>.”

If the term is new to you, magic numbers are those numbers we use to make something work in a single particular instance. They typically stop working as soon as some other value changes, and, given the nature of responsive design, other values are always changing. <strong>Magic numbers in CSS are best avoided.</strong>

### We Need to Give Up Containers

For the last few years, whenever we’ve wanted to move a group of adjacent elements to a certain part of a layout, we’d wrap those elements in a container and write CSS to display the container somewhere in the design. I’m sure you’ve used CSS selectors like <code>#wrapper</code> and <code>#container</code> more than once.

We need fewer of these HTML containers and more CSS virtual container classes that we can apply to different elements as needed.

In other words, instead of this…

<pre><code class="language-markup">
&lt;div id="container"&gt;
  &lt;div&gt;Content here&lt;/div&gt;
  &lt;div&gt;Content here&lt;/div&gt;
  &lt;div&gt;Content here&lt;/div&gt;
&lt;/div&gt;
</code></pre>

… <strong>we need more of this:</strong>

<pre><code class="language-markup">
&lt;div class="container"&gt;Content here&lt;/div&gt;
&lt;div class="container"&gt;Content here&lt;/div&gt;
&lt;div class="container"&gt;Content here&lt;/div&gt;
</code></pre>

In the latter block, each division might have a different class name or perhaps different additional classes applied. This allows for greater flexibility in rearranging them in the layout. In the first block of code, the three content divisions will always reside inside their parent container.

I’m not suggesting that the first block of HTML above should never be used. There will absolutely be times when wrapping several divisions of content with a container makes sense. However, if you want some of those blocks to intermix with elements in other columns, then you’ll have to think more in terms of the second block of HTML above.

<strong>With CSS, we have the ability to rearrange blocks inside a container.</strong> We don’t have the ability to break content out of one container and move it inside another container. If you want more mixing of blocks, then you’ll need fewer containers.</p>

## Examples

While there are currently far more instances of websites that are dropping columns wholesale, there are certainly websites that mix content in one column with content in another column.

Let me first offer a detailed look at my own website, since I’m most familiar with it. I’ll follow this up with a few other websites that intermix content in slightly different ways.</p>

### A Personal Example

Around the time that Trent coined the term “content choreography,” I was working on a redesign of my website and was trying to figure out how to <a href="https://www.vanseodesign.com/web-design/rearranging-boxes/">mix content blocks</a> as the layout changed.

The image below shows the top of a typical blog post on my website when the browser is wide enough to accommodate two columns. Click the image to see the live post.

Meta information such as my name and the publication date are in a column to the left, while the article’s title, main text, images, headings and so on are in a column to the right.

<a href="https://www.vanseodesign.com/web-design/unique-visual-language/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158633" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27a9cd9a-d6bf-4f13-95f1-7ee7c8c2a8b5/vanseo-design-2-col1.png" alt="Screenshot of post from Vanseo Design with two-column layout" width="500" height="470" /></a><br>
<em>My website when the browser is wide enough to accommodate two columns.</em>

Seeing the layout, you might instinctively think each “column” is wrapped in its own container and that I’ve floated both columns left or right; it’s how I would have developed this layout a few years ago. But doing that leads to the problem of <strong>one of the columns being forced to drop below the other</strong> on small screens.

Below is the same page as a single column on a narrower screen. The meta information from the left column sits below the article’s title from the right column but above everything else in that right column. Both “columns” of content have actually been inside the same container all along.

<a href="https://www.vanseodesign.com/web-design/unique-visual-language/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158634" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d857daba-6c9b-414d-98f9-ff81ac7e488c/vanseo-design-single-col1.png" alt="Screenshot of post from Vanseo Design with single column layout" width="485" height="470" /></a><br>
<em>My website as a single column on a narrower screen.</em>

The image below presents a more abstract view of what’s going on. On the left, you see the layout as it appears when displayed as a single column. On the right is the two-column version of the layout.

<strong>Every element is its own unique block and serves as its own container.</strong> The page’s main heading is its own contained block. All of the meta information is inside another container directly below it. After that, every paragraph, subheading and image is also its own self-contained block of content. The same goes for anything else that might end up in a post, such as a block quote or code block.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d908abe9-8d3b-4068-ae65-3b053bc0c2a3/vanseo-abstract-3.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158744" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d908abe9-8d3b-4068-ae65-3b053bc0c2a3/vanseo-abstract-3.png" alt="Abstract diagram showing content on Vanseo Design with single and 2 column layout" width="500" height="278" /></a><br>
<em>A more abstract view of what’s going on.</em>

On small screens, all of the blocks display in the source order. On wider screens, I shift this entire single “column” to the right by adding a left margin to each individual block. In the CSS, I have a long list of selectors with a single line of declarations. When I want something to appear in the “left column,” I float it left and reset its margin to zero.

The solution is hardly perfect. Blocks pulled into the virtual left column won’t slide up or down. They simply move to the left. This solution doesn’t enable me to display something from the bottom of the article at the top of the left column. But, hopefully, this illustrates <strong>how rethinking containers can help us intermix content</strong> from different columns into a single column.</p>

### The Next Web

<a href="https://thenextweb.com/">The Next Web</a> mostly drops columns down as it rearranges from three columns to one, but it does intermix elements at the top of the page.

<a href="https://thenextweb.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158639" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df49be84-15db-4b2c-8d91-008888f4fc98/the-next-web.jpg" alt="Screenshots of The Next Web" width="500" height="636" /></a>

The image above shows the website displayed as two columns (on the left) and a single column (on the right). The blue outline shows the container around elements at the top of the page. You can see that the secondary stories to the right of the top story drop below it but remain above the other stories, due to the way the containers have been set up.

In the single column, the images in all of the first three stories are now physically the same size, so <strong>the hierarchy has changed</strong>. However, the second and third stories are still seen as “less important” because they come after the top story.

This intermixing is achieved by thinking in advance of which elements will shift columns and by placing elements that need to be rearranged in the same container, separate from other containers of content.</p>

### Time

<a href="https://www.time.com/time/">Time</a> magazine intermixes content across columns and containers. Notice how the “Latest Headlines” section (in the green container) moves from the right column at the top to just below the main image and story links in the single column.

<a href="https://www.time.com/time/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158640" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b255e544-3d13-4f09-853c-b1942ae9c794/time.jpg" alt="Screenshots of Time Magazine website" width="500" height="387" /></a>

While not shown in the image above, the row of four images on the left follows the “Latest Headlines” in the single column. The remaining content in the right column drops much further down. You can see this by viewing the website directly.

The website achieves this intermixing by ignoring most of what I’ve said in this post about using fewer containers. <strong>Instead, it uses JavaScript to rewrite the HTML</strong>, moving elements in and out of different containers as the layout changes. It is another solution to this issue, although better planning up front is preferable.</p>

### Enoch’s Fish & Chips

The navigation on <a href="https://www.enochs.co.uk/">Enoch’s Fish &amp; Chips</a>’ website integrates with the logo and company blurb when the layout is a single column:

<a href="https://www.enochs.co.uk/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158643" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/035583ee-c9fb-4a1c-ba64-07906ae21891/enochs-single-col.jpg" alt="Screenshot of Enoch's Fish and Chips with single column" width="500" height="697" /></a>

The navigation (and the tagline further down) moves to the right column when the browser is wide enough to accommodate multiple columns.

The website rearranges these elements similar to the way I rearrange elements on my own website; the logo, navigation, blurb and tagline are each a separate container. <strong>To move them around, the website uses positioning</strong> instead of floats, but otherwise, the principle is the same.

<a href="https://www.enochs.co.uk/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="158642" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9cdc15c-3cbe-4784-a9ac-85258ef9db87/enochs-2-col.jpg" alt="Screenshot of Enoch's Fish and Chips at 2 columns" width="500" height="411" /></a>

## Closing Thoughts

Many of us have, understandably, been taking the easy way out with responsive layouts. When the width of a screen cannot accommodate a column, we’ve been dropping the column in its entirety below other columns. In some cases, this is perfectly fine. In others, <strong>it breaks the carefully designed hierarchy</strong>.

We face two issues in maintaining the hierarchy. The first is having to follow the HTML source order when the layout is a single column. The solution to this problem is a technical one and is coming in the form of new CSS specs that will allow the display order and the HTML source order to be different.

The second problem is less technical and more a challenge to how we think about structuring our HTML, particularly to how we use containers. Elements can’t move from one container to the next. We can fake it with complex CSS, or we can rewrite the HTML with JavaScript; but, ultimately, if we want to intermix elements, <strong>we’re best of using fewer HTML containers to create columns</strong>. Instead, we should leave more of our content blocks in their own containers and use CSS to create virtual columns in the layout.

This solution doesn’t confine our elements to structural containers and instead enables us to more easily rearrange the elements in different layouts.

{{< signature "al" >}}

