---
title: 'Gridpak: The Responsive Grid Generator'
slug: gridpak-the-responsive-grid-generator
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4220668-7f43-481c-991e-1ddf07646bc4/gp-21.png'
date: 2012-03-19T14:07:36.000Z
author: erskine-design
description: >-
  This article is the fifth in our new series that introduces the latest,
  useful and freely available tools and techniques, developed and released by
  active members of the Web design community. The first article covered
  [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/);
  the second introduced
  [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/),
  a responsive framework; the third presented
  [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/),
  a library for Gmail-like client-side drafts and the fourth shared with us a
  free plugin called
  [GuideGuide](https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/).
  Today, we are happy to present Erskine's responsive grid generator:
  **Gridpak**.
categories:
  - Coding
  - Tools
  - Frameworks
---
<em>This article is the fifth in our new series that introduces the latest, useful and freely available tools and techniques, developed and released by active members of the Web design community. The first article covered <a href="https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/">PrefixFree</a>; the second introduced <a href="https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/">Foundation</a>, a responsive framework; the third presented <a href="https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/">Sisyphus.js</a>, a library for Gmail-like client-side drafts and the fourth shared with us a free plugin called <a href="https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/">GuideGuide</a>. Today, we are happy to present Erskine's responsive grid generator: <strong>Gridpak</strong>.</em>

In the near 18 months since _A List Apart_ published Ethan Marcotte’s article [Responsive Web Design](https://www.alistapart.com/articles/responsive-web-design/) much has changed in the way we approach our design process. The new responsive attitude described in the article embraces device agnostic design, flexibility and the undefined canvas. Whilst John Allsopp’s [A Dao of Web Design](https://www.alistapart.com/articles/dao/) laid the foundations for change, Ethan’s article—alongside a maturation in technologies and a coinciding mass movement towards mobile browsing—really set the scene for a new design ethos.</p>

### The Problem

Challenges and problems inevitably arise when adopting new ideas and ways of working. One of the main stumbling blocks we found as an agency was in efficiently and cost-effectively implementing one of the fundamental ingredients of responsive design: a flexible grid based layout.

This is what our typical design and development cycle for creating a responsive website with a flexible grid system used to look like:

{{% feature-panel %}}

1.  Create 3 or 4 different sized grids by hand in Fireworks to use as a reference in the wireframing/design stage.

    ![Create multiple grids, for desktop, tablet and phone.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8003359-a903-461f-8078-153bb96ae2a8/gp-11.png "Create multiple grids, for desktop, tablet and phone.")  
    _Create multiple grids, for desktop, tablet and phone._

2.  Recreate the same grids with crude and often clunky browser extensions (mentioning no names) or write some JavaScript that would allow us to overlay our grid layers (exported as semi-transparent PNGs) in the browser.

    ![Recreating the same grids in the browser.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/623bca6f-6f05-4261-9d48-3d96313ec23d/gp-21.png "Recreating the same grids in the browser.")  
    _Recreating the same grids in the browser._

3.  Write [LESS](https://lesscss.org/) stylesheets which cut down on the maths, but still required all the base values and formulas for calculating grid widths.

    ![Calculating percentage widths and writing CSS in order to make our website and grid responsive.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff73515-4a6a-43fa-b9c3-975581389bb8/gp-31.png "Calculating percentage widths and writing CSS in order to make our website and grid responsive.")  
    _Calculating percentage widths and writing CSS in order to make our website and grid responsive._

**There were 2 crucial drawbacks to this approach**:

1.  It took a long time to measure up grids, create them in static graphic format, then produce long lines of LESS.
2.  We couldn’t visualise the grids responding (sweet irony) until they were built.

At that time, most of the responsive frameworks forced you into a corner: you were required to use a pre-determined number of columns, gutters, padding and breakpoints. We felt that this undermined the ethos of a methodology that was by it’s very nature _flexible_.

We also felt that existing generators lacked the visual feedback that we required: we were desperate to see how our grids would react when squeezed and stretched in order to inform our decisions.</p>

### Solution

So one afternoon, dissatisfied as much with our own process as we were with the available solutions, we began to put pen to paper with the ultimate goal of creating a responsive grid generator that would:

1.  **Offer true flexibility**:  
    The interface allows the user to adjust the amount of columns in each grid, the inner padding and gutter width in either pixels or percentages, and where the breakpoints of the grid occur.
2.  **Allow the user to visualize a responsive grid system**:  
    The user can switch between and edit their grids in real-time using the tab system. They can see immediately how their grids react.
3.  **Streamline the design and development process**:  
    Gridpak outputs all of the file formats necessary to make a quick start to a responsive project. They are easy to extend, reference, or just throw away if not required. The file formats come neatly packed inside a small .zip file that includes:
    *   PNG overlays of each grid the user has created for use in their graphics program of choice.
    *   A HTML demo file.
    *   A CSS file complete with appropriate media queries and predefined presentational classes.
    *   LESS, [SCSS](https://sass-lang.com/ "css3 extension") and [SASS](https://sass-lang.com/ "css3 extension") files for the same purpose, but with the added power of _variables_ and _mixins_.
    *   A JavaScript snippet that allows the user to overlay their responsive grid in _any_ browser using the "G" key.
    *   A readme.txt file with some more in-depth documentation.

![The simple interface makes is easy to visualize, create and edit your responsive grid system.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cccdc030-b2e5-4d1f-bfac-2807fb3c2649/gp-41.png "The simple interface makes is easy to visualize, create and edit your responsive grid system.")  
_The simple interface makes is easy to visualize, create and edit your responsive grid system._

### Stylesheets

Gridpak is not really meant to be a framework. Although its stylesheets will work "right out of the box", they are meant to be plucked and pruned into your own stylesheets and methods of working. That’s why they only contain information which is essential for your grid system.

We had a niggle with media queries on grid based layouts when the number of columns changed between _breakpoints_. To solve this problem, we eschewed the use of "span_x" in our class names in the markup, preferring to use semantic naming like "news_item". We then added our semantic class names to `gridpak.css`, right next to their counterpart:

<pre><code class="language-css">.span_1, .span_2, .span_3,
.news_item {
    margin-left:2%;
    padding:0 1.5%;
    ...
}

.span_6,
.news_item {
    ...
}</code></pre>

In this way, our markup isn’t coupled to the CSS nor are the elements to the _breakpoints_. It’s a far more scalable way of doing things. Implementation is very much open to interpretation, and we look forward to seeing how people apply it to their own projects.

<p>Gridpak uses <code><a href="https://www.w3.org/TR/css3-mediaqueries/">media queries</a></code>, <code>box-sizing</code> and <code>background-clip</code> properties (although there are ways to use it without these queries.) These CSS3 properties are supported in all new browsers, as well as IE8 but we would recommend using a polyfill or detection service such as <a href="https://www.modernizr.com/">Modernizr</a> to handle the degradation.

### Help Us Help You
<p><img loading="lazy" decoding="async" title="Baseline functionality and an ability to edit the position of the breakpoints after you have created them." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7724388-d7c9-4e5c-a9fd-232bd442d1c0/gridpak-preview1.png" alt="Baseline functionality and an ability to edit the position of the breakpoints after you have created them." width="500" height="350" /><br /><em>Coming soon: Baseline functionality and an ability to edit the position of the breakpoints after you have created them.</em></p>

<p>We know Gridpak is not a one-stop, cure-all panacea&mdash;it was never designed to be. Like all tools it has limitations, but we believe it is a useful part of the responsive designer’s armory. As the field evolves further we will undoubtedly see a proliferation of similar tools and approaches. People will ultimately choose the ones that work best for them and fitting to their workflows.</p>

<p>Since the launch, we’ve added important features like the ability to adjust gutter widths and column padding in percentages as well as in pixels. With our next release we’ll introduce a more flexible approach to allow the creation of a wider range of asymmetrical grids... but we can go much further. That’s why we’ve open sourced the Gridpak codebase on <a title="Gridpak on Github" href="https://github.com/erskinedesign/ed.gridpak">Github</a>. We’d love to see it become a truly collaborative effort where people get into the code and make their own improvements.</p>

### Feedback
<p>We hope that <a href="https://gridpak.com/">Gridpak</a> will grow and evolve over time, so we’d really welcome your feedback and input. You can send feature requests to <a title="gridpak email" href="mailto:gridpak@erskinedesign.com">gridpak@erskinedesign.com</a> or <a title="gridpak twitter account" href="https://twitter.com/gridpak">@gridpak</a> on Twitter. We also have a <a title="Gridpak trello" href="https://trello.com/board/gridpak/4ec2949a6f575b8735025392">Trello board</a> where you can comment on and vote for features, or even just keep an eye on what we’re currently working on. We, at <a href="https://erskinedesign.com">Erskine Design</a>, have found Gridpak to be a great resource for our day-to-day client work, so we hope you enjoy using it as much as we do... and we do.</p>

<p><em>Written by <a href="https://www.smashingmagazine.com/author/sam-quayle/">Sam Quayle</a>.</em></p>

<em>(jvb) (il)</em>

