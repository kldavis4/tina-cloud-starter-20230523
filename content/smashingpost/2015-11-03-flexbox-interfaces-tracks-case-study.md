---
title: 'Flexbox For Interfaces All The Way: Tracks Case Study'
slug: flexbox-interfaces-tracks-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93ac104c-6eed-4c2d-8345-68caa1e3acd6/02-tracks-app-opt-preview.png
date: 2015-11-03T20:03:42.000Z
author: dennisgaebeljr
description: >-
  The **days of floats and margin trickery are finally behind us**, as CSS
  furnishes developers with new and improved properties perfect for those
  delicate layouts. Layout features such as vertical alignment, evenly
  distributed spacing, source-order control and other patterns such as “sticky”
  footers are quite effortless to achieve with
  [flexbox](https://caniuse.com/#feat=flexbox).

  In this article, we’ll discuss **layout patterns well suited to flexbox**,
  using the interface from the [Tracks](https://buildtracks.com) application,
  which also takes advantage of atomic design principles. I’ll share how flexbox
  proved useful and note the pitfalls of pairing it with particular layout
  patterns. We’ll look at those patterns that caused concern, provide
  suggestions for fallbacks and share additional tactics to start using this CSS
  property immediately.
categories:
  - Coding
  - CSS
  - Flexbox
---
The <strong>days of floats and margin trickery are finally behind us</strong>, as CSS furnishes developers with new and improved properties perfect for those delicate layouts. Layout features such as vertical alignment, evenly distributed spacing, source-order control and other patterns such as “sticky” footers are <a title="Designing CSS Layouts" href="https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/"> quite effortless to achieve with flexbox</a>.

In this article, we’ll discuss <strong>layout patterns well suited to flexbox</strong>, using the interface from the <a href="https://buildtracks.com">Tracks</a> application, which also takes advantage of atomic design principles. I’ll share how flexbox proved useful and note the pitfalls of pairing it with particular layout patterns. We’ll look at those patterns that caused concern, provide suggestions for fallbacks and share additional tactics to start using this CSS property immediately.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/#further-reading-on-smashingmag)

*   [Flexbox Is As Easy As Pie – Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [CSS Grid, Flexbox And Box Alignment](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)
*   [<span class="headline">The Flexbox Reading List: Techniques And Tools</span>](https://www.smashingmagazine.com/2016/02/the-flexbox-reading-list/)
*   [Harnessing Flexbox For Today’s Web Apps](https://www.smashingmagazine.com/2015/03/harnessing-flexbox-for-todays-web-apps/)

## Flexy Atomic Components

The approach to Tracks’ interface started with each piece being investigated as an isolated case, using the principles outlined by <a href="https://bradfrost.com">Brad Frost</a>. There are also documented bits of development and integration on Dribbble for an insider’s view.

{{% feature-panel %}}

The philosophy of atomic design can be thought of as small LEGO-like pieces constructed together to form a larger distinctive part of an interface. Scientific terms such as organism, atom and molecule are used to enable developers to categorize pieces of the interface in order to gain a deeper understanding of each part of the whole. This type of categorization creates an <strong>opportunity for the identification of these patterns</strong> and prevents outside influences such as grids, colors, and spacing from disrupting the goal, which is to identify patterns. Building from a microscopic level allows for a wider distribution of these parts throughout the interface.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84bdd815-6af9-4f2b-9a1a-8bdcb22825c9/01-atomic-parts-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563773b9-1292-405f-856e-3f8170582ea1/01-atomic-parts-opt-preview.png" alt="Figure 1" /></a>Figure 1. These application cards used to display data were constructed using atomic design principles. Can you guess which parts use flexbox? (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84bdd815-6af9-4f2b-9a1a-8bdcb22825c9/01-atomic-parts-opt.png">View large version</a>)</figcaption></figure>

If you’d like to dive deeper into the theory of atomic design, read <a href="https://bradfrost.com/blog/post/atomic-web-design">Brad’s post</a>, which discusses his philosophy in more detail. I also suggest checking out his <a href="https://atomicdesign.bradfrost.com">book on the subject</a>.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6db0b8c-b106-45ba-b926-cb75d5bbe85f/02-tracks-app-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bb4191b-f572-4cc8-9534-becb8c52d9d3/02-tracks-app-opt-preview.png" alt="Figure 2" /></a>Figure 2. The primary interface of the Tracks application, which takes full advantage of flexbox and atomic design. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6db0b8c-b106-45ba-b926-cb75d5bbe85f/02-tracks-app-opt.png">View large version</a>)</figcaption></figure>

The interface designs were conveyed as a set of <a href="https://www.invisionapp.com">InVision</a> comps, documenting the flow and UI. During the initial audit of the interface, I began determining regions where flexbox would be beneficial. I also elected to use flexbox for page layouts using patterns such as the well-known “sidebar to the left, main content to the right” pattern, which is most often implemented with floats.

One welcome aspect of the Tracks redesign was that the project’s scope required Internet Explorer (IE) 10+, Android 4.1+ and iOS 7+. This was good news because <a href="https://caniuse.com/#search=flexbox">they have great support for flexbox</a>, with the appropriate prefixes. Even though support is far more stable these days, operating systems prior to, say, Android 4.1 require fallbacks. What would a <strong>fallback</strong> look like in a case where support doesn’t exist? Developers using Modernizr can target those browsers using the <code>.no-flexbox</code> class and serve a more stable supported layout system (<em>alternatively you could use <a href="https://davidwalsh.name/css-supports">CSS feature queries with @supports</a> which is well supported, too. —Ed.</em>). For example:

<pre><code class="language-markup">
&lt;ul class="flexbox-target"&gt;
  &lt;li&gt;…&lt;/li&gt;
  &lt;li&gt;…&lt;/li&gt;
  &lt;li&gt;…&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

<pre><code class="language-css">
html.flexbox ul.flexbox-target,
html.no-js ul.flexbox-target {
  display: flex;
  flex-direction: row;
}

html.no-flexbox ul.flexbox-target li,
html.no-js ul.flexbox-target li {
  display: inline-block; /* Could also use a float-positioned-layout system instead */
}
</code></pre>

Where flexbox support isn’t quite right, we’ll go ahead and use <code>display: inline-block</code> for the layout fallback. We’ll also add a <code>no-js</code> to the declaration should JavaScript fail. The cascading nature of CSS will be in place if flexbox isn’t supported, even with JavaScript off or loading failures. Flexbox can co-exist with <code>float</code> and <code>display: table</code> and relative positioning, and browsers supporting flexbox will prioritize flexbox over other definitions, while browsers not supporting flexbox will ignore flexbox properties and gracefully fall back to good ol' CSS layout mechanisms.

As with everything, the tough choices will depend on the project’s scope, analytics and budget. My golden rule is to always make the choice that makes the most sense for the project.</p>

## Inline Patterns

<strong>Navigational components</strong> proved to be extremely valuable with flexbox, not only for easing implementation, but also for shortening development sessions. Inline patterns that were known to consume a great deal of developers’ time can now happen in minutes with flexbox. If you’ve had the pleasure of developing with this kind of pattern prior to IE 9, then you’ll know the frustration.

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f72ae5ba-3ce0-4767-aeb3-d9763ac8285b/03-admin-nav-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc14c1ba-9cd7-4bf5-859d-dabd7a2f5397/03-admin-nav-opt-preview.png" alt="Figure 3" /></a>Figure 3. This admin navigation uses an inline layout pattern, with navigational items centered vertically. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f72ae5ba-3ce0-4767-aeb3-d9763ac8285b/03-admin-nav-opt.png">View large version</a>)</figcaption></figure>

The markup pattern for the admin navigation consists of a <code>nav</code> tag wrapping a series of anchors. Here’s an example of this pattern in HTML:

<pre><code class="language-markup">
&lt;header role="banner"&gt;
  &lt;nav role="navigation"&gt;
    &lt;a href="pipeline.html"&gt;Back to pipeline&lt;/a&gt;
    &lt;a href="account.html"&gt;Account&lt;/a&gt;
    &lt;a href="users.html"&gt;Users&lt;/a&gt;
    &lt;a href="export.html"&gt;Export&lt;/a&gt;
  &lt;/nav&gt;
&lt;/header&gt;
</code></pre>

And here are the related styles:

<pre><code class="language-scss">
nav[role="navigation"] {
  display: flex;
  align-items: center; /* Center navigation items vertically */
}

nav[role="navigation"] a {
  display: inline-block; /* To avoid layout issues for inline elements with the order property in IE 10 */
}

nav[role="navigation"] a[href="pipeline.html"] {
  flex: 1;
}
</code></pre>

The CSS required is just as minimal as the markup. Note the <code>inline-block</code> value given to anchors. This declaration solves any future headaches in IE 10 if you were to change the sequence of elements with the <code>order</code> property. It was also discovered that any padding or margin given to direct children of a flex container defined with the <code>flex</code> property causes layout issues in IE 10. A good idea is to ABC (always be checking) across browsers and platforms.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/851e210c-f010-456e-9fb8-65b04d9d7bf3/04-primary-nav-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b5672e5-e7f8-432d-b2ea-11904e085741/04-primary-nav-opt-preview.png" alt="Figure 4" /></a>Figure 4. This header navigation pattern with a centered logo is often seen on the web and is flexbox-approved. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/851e210c-f010-456e-9fb8-65b04d9d7bf3/04-primary-nav-opt.png">View large version</a>)</figcaption></figure>

The common inline pattern above is typically implemented with non-semantic markup. It no longer requires this kind of hackery now that flexbox is an option.

The layout consists of a collection of menu items to the left, a centrally positioned logo and additional items to the right. The markup for this pattern is as follows:

<pre><code class="language-markup">
&lt;header class="pipeline-header" role="banner"&gt;
  &lt;a href="pipeline.html" class="pipeline-logo"&gt;… &lt;/a&gt;

  &lt;nav class="pipeline-nav" role="navigation"&gt;…&lt;/nav&gt;

  &lt;form class="pipeline-search" role="form"&gt;…&lt;/form&gt;

  &lt;a href="#menu"&gt;…&lt;/a&gt;
&lt;/header&gt;
</code></pre>

<strong>Flexbox can alleviate the need for HTML hackery</strong> and can maintain semantics, as the markup demonstrates. Maintaining semantics is important because the HTML will have a higher chance of being reusable in the future, among many other reasons beyond the scope of this discussion.

Before flexbox existed, developers applied approaches such as <code>display: inline-block</code> and even <code>float: left</code> to achieve inline layouts. Now that flexbox is a viable option, developers are no longer forced to follow bad practices for the sake of aesthetics. The CSS required is not as brief as the admin navigation pattern in figure 3, but it’s still faster to implement than the methods mentioned earlier.</p>

<pre><code class="language-scss">
.pipeline-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.pipeline-header &gt; a {
  display: inline-block; /* IE 10 doesn't recognize order, so we do this to avoid odd layouts there. */
}

.pipeline-logo {
  flex: 1;
  order: 2;
  text-align: center;
}

.pipeline-nav {
  flex: 1.25;
  order: 1;
}

.pipeline-search {
  flex: 1;
  order: 3;
}

a[href="#menu"] {
  order: 4;
}
</code></pre>

When using flexbox with the pattern in figure 3, remember that the source’s sequence can be changed. If the header’s logo requires a shift in position, doing so is painless with the <code>order</code> property. Be mindful that <strong>source order is always important for accessibility</strong> and somewhat controversial when it comes to flexbox; especially with <a href="https://sprungmarker.de/wp-content/uploads/css-a11y-group/css-a11y-flexbox.html#newspec">varying accessibility implementations</a> across browsers. All browsers and screen readers use the source code’s order, not the visual order determined by CSS, for keyboard navigation.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba8e043-1168-4c37-b908-7283466ef7bb/05-flexbox-order-chart-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03bd1785-b085-4eb6-b2fa-a33735aa1101/05-flexbox-order-chart-opt-preview.png" alt="Figure 5" /></a>Figure 5. The normal written flow in the markup and rendered in the browser (left), and the sequence changed with flexbox without adjusting the markup (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba8e043-1168-4c37-b908-7283466ef7bb/05-flexbox-order-chart-opt.png">View large version</a>)</figcaption></figure>

The code below is for the layout above. The markup is never altered to change the order of appearance.</p>

<pre><code class="language-markup">
&lt;div class="container"&gt;
  &lt;header role="banner"&gt;&lt;/header&gt;
  &lt;main role="main"&gt;&lt;/main&gt;
  &lt;footer role="contentinfo"&gt;&lt;/footer&gt;
&lt;/div&gt;
</code></pre>

Here is the CSS used to change the order for the diagram on the right in figure 5.</p>

<pre><code class="language-scss">
.container {
  display: flex;
  flex-direction: columns; /* row is the default value */
}

header {
  order: 2;
}

main {
  order: 3;
}

footer {
  order: 1;
}
</code></pre>

This type of layout isn’t just for navigation either. You might have seen the pattern in footers as well.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ef5b44-96da-4d2f-8e27-f51e89b5e805/06-flex-footer-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cea249d-ea53-40fe-bdf8-bf6e8d85879d/06-flex-footer-opt-preview.png" alt="Figure 6" /></a>Figure 6. The same pattern we’ve seen used time and again for navigation is used here for the footer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ef5b44-96da-4d2f-8e27-f51e89b5e805/06-flex-footer-opt.png">View large version</a>)</figcaption></figure>

When using this pattern, consider how the content might fill the container and consume space. Should the content grow from the center out? What if the content pushed downward? How would that affect other items in the layout? Ask these questions in every project before proceeding with implementation. Consideration for keyboard navigation order, as mentioned, is just as important to end users.

## Inline Form Inputs

Forms can be a nightmare for developers, especially when they’re tightly coupled to an intricate grid structure made in Photoshop. The “inline label” pattern, as I’ll refer to it, is as much a staple in our industry as the Fender Stratocaster is to rock music.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b5efc8-ce37-4321-b5bf-5247b9d817f7/07-inline-label-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d72c88a-9bc1-4dd1-877f-4af559b4139f/07-inline-label-opt-preview.png" alt="Figure 7" /></a>Figure 7. Inline labels and inputs are another great place to use flexbox. But be careful with how the label text wraps or pushes according to the text’s length. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b5efc8-ce37-4321-b5bf-5247b9d817f7/07-inline-label-opt.png">View large version</a>)</figcaption></figure>

As mentioned in the previous section, decide how your content will flow and occupy the space of its container when the browser resizes or when dynamic content is inserted.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49267a87-fab9-4b3f-9056-f5fbc59f8d36/08-inline-input-wrap-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c29f607f-6638-491c-84c9-e340542a9c8b/08-inline-input-wrap-opt-preview.png" alt="Figure 8" /></a>Figure 8. Decide how the content will expand. On the left, a table display is vertically aligned to the middle. On the right, flexbox aligns items to the center. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49267a87-fab9-4b3f-9056-f5fbc59f8d36/08-inline-input-wrap-opt.png">View large version</a>)</figcaption></figure>

These screenshots clearly indicate the <strong>faults flexbox can present with dynamic or lengthy content</strong>. The effect in the image on the right is what I call a “center push,” meaning the content pushes from the center outwards along the x and y axis.

Here’s the markup for the inline label pattern in figure 8.</p>

<pre><code class="language-markup">
&lt;div class="form-group"&gt;
  &lt;label&gt;…&lt;/label&gt;
  &lt;select&gt;…&lt;/select&gt;
&lt;/div&gt;
</code></pre>

The solution to the problem in this case is to use a table display to better control long text. This allow content to flow downwards, instead of push from the center out.</p>

<pre><code class="language-scss">
.form-group {
  display: flex;
}

.form-group label {
  display: table;
  vertical-align: middle;
}

.form-group input {
  flex: 1;
}
</code></pre>

Mixing and matching flexbox with table is a great technique and one that I encourage further exploration with. When mixing and matching, always check across testing environments to catch layout bugs early.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/540237fb-015b-4a3c-80da-ee801ababbf0/09-inline-input-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/678396c2-b40f-417f-8ade-ab57eb3d0aec/09-inline-input-opt-preview.png" alt="Figure 9" /></a>Figure 9. With inline inputs with buttons, the equal heights of the inputs give balance to the design. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/540237fb-015b-4a3c-80da-ee801ababbf0/09-inline-input-opt.png">View large version</a>)</figcaption></figure>

I’ve seen many search inputs with this type of pattern. It’s an extremely flexible pattern that can be reused across a plethora of templates. Of course, CSS that could interfere, such as context-specific properties unrelated to the overall pattern, would be kept separate.

The HTML required is typical and includes a surrounding <code>div</code> to define the flexbox structure.

Here is our HTML:

<pre><code class="language-markup">
&lt;div class="form-group"&gt;
  &lt;input type="text" placeholder="Add a note…"&gt;
  &lt;button&gt;Add&lt;/button&gt;
&lt;/div&gt;
</code></pre>

And the CSS:

<pre><code class="language-scss">
.form-group {
  display: flex;
}

.form-group input {
  flex: 1;
}
</code></pre>

## Dropdown Menu

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b64af538-770f-47d2-b84a-4ed21c179fa9/10-primary-menu-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34cd7312-b791-45ec-953c-7e12ec13cfe3/10-primary-menu-opt-preview.png" alt="Figure 10" /></a>Figure 10. The dropdown menu’s region is highlighted using some quick flexbox tactics for effortless positioning. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b64af538-770f-47d2-b84a-4ed21c179fa9/10-primary-menu-opt.png">View large version</a>)</figcaption></figure>

The dropdown menu’s layout consists of a column on the left, containing vertically centered items positioned inline, and a list of items on the right, where each list item lies on its own line.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b67ebeaf-2ebc-4063-acb4-78742c38f1d6/11-tracks-menu-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a4d9036-a022-4ff1-996a-2e3fae9378e0/11-tracks-menu-opt-preview.gif" alt="Figure 11" /></a>Figure 11. The menu for this primary interface was built using only flexbox for the layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b67ebeaf-2ebc-4063-acb4-78742c38f1d6/11-tracks-menu-opt.gif">View large version</a>)</figcaption></figure>

The markup for this navigation menu uses the following HTML as its structural foundation.</p>

<pre><code class="language-markup">
&lt;nav class="menu"&gt;
  &lt;div class="menu__options"&gt;
    &lt;a href="export-data.html"&gt;Export&lt;/a&gt;
    &lt;a href="help.html"&gt;Get Help&lt;/a&gt;
  &lt;/div&gt;

  &lt;div class="menu__items"&gt;
    &lt;a href="account.html"&gt;Account&lt;/a&gt;
    &lt;a href="preferences.html"&gt;Preferences&lt;/a&gt;
    &lt;a href="users.html"&gt;Users&lt;/a&gt;
    &lt;a href="payment.html"&gt;Payments&lt;/a&gt;
    &lt;a href="logout.html"&gt;Logout&lt;/a&gt;
  &lt;/div&gt;
&lt;/nav&gt;
</code></pre>

The CSS required is lean and easy to read, too, just the way developers like it.</p>

<pre><code class="language-scss">
.menu {
  display: flex;
}

.menu__options {
  display: flex;
  align-items: center;
}

.menu__items {
  display: flex;
  flex-direction: column;
}
</code></pre>

In just a few lines of code, layout bliss is achieved. Plus, it is decoupled from any grid structure, and the HTML and CSS are full of semantic meaning. It’s just another example of the power of flexbox to quickly avoid complicated positioning tactics and verbose markup.</p>

## Media Objects

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c629465d-22fc-41ec-996f-b0d8c7eb3491/12-media-obj-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e963ff0e-2bfe-4202-bf56-d0f2f9cb5ccb/12-media-obj-opt-preview.png" alt="Figure 12" /></a>Figure 12. In the media-object pattern, using flexbox, a fixed-width SVG sits to the left, with flex content sitting adjacent. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c629465d-22fc-41ec-996f-b0d8c7eb3491/12-media-obj-opt.png">View large version</a>)</figcaption></figure>

In this universal pattern, known to some as the “media object” pattern, an element such as an image or video floats to one side, with content sitting adjacent.</p>

<pre><code class="language-markup">
&lt;div class="media-obj"&gt;
  &lt;div class="media-obj__fig"&gt;…&lt;/div&gt;
  &lt;div class="media-obj__body"&gt;…&lt;/div&gt;
&lt;/div&gt;
</code></pre>

Here is the CSS:

<pre><code class="language-scss">
.medi-obj {
  display: flex;
  align-items: flex-start;
}

.media-obj__body {
  flex: 1;
}
</code></pre>

Philip Walton shares a great approach on his website <a href="https://philipwalton.github.io/solved-by-flexbox/demos/media-object">Solved by Flexbox</a>, which I encourage everyone to explore. Philip gives some helpful reminders and tips on using certain patterns with flexbox, and he maintains an up-to-date repository of all of the patterns he demonstrates.
{{< vimeo id="144465182" >}}

<figcaption>Figure 13. In this extreme case of browser resizing, the image is set to a maximum width of 100% and the right side is given a flex value of 1. Be careful how you mix fixed-width and flexible children.</figcaption></figure>

Flexbox works great for this type of pattern, but be careful how content reacts to adjacent content, as shown above. In the GIF above, you can see how the graphic’s space seems to collapse while text pushes over the top. This might seem like a silly example because who would make their browser that narrow, right? The point, though, is that we need to understand how content relates to its surroundings before we use flexbox.

A suggestion for this pattern is to always set images to <code>max-width: 100%</code> when inline inside a flex parent or to define images with a fixed width and then use media queries to adjust as needed.</p>

## Flexy Calendar

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6b318d2-2d78-410f-ab28-e039028692bd/13-calendar-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7effdac4-c42c-4d50-836d-f5fb48ab460b/13-calendar-opt-preview.png" alt="Calendar" /></a>Calendar. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6b318d2-2d78-410f-ab28-e039028692bd/13-calendar-opt.png">View large version</a>)</figcaption></figure>

What kind of world would it be if we didn’t consider a context such as a calendar? You might ask here, “Why not use a table?” In this case, the calendar is being used as a date-picker, so I opted to go with buttons for the day, month and year calendar and to confine these buttons to rows (each row of the weekly calendar is wrapped in a <code>div</code>). Using this approach made for less markup and an easier layout. (Huge thanks to <a href="https://twitter.com/shanehudson">Shane Hudson</a> for building the killer logic and providing insight.)

The markup is straightforward and even works well for the calendar’s pagination controls in the header.</p>

<pre><code class="language-markup">
&lt;div class="datepicker"&gt;
  &lt;header class="datepicker__header flex-container"&gt;
    &lt;button&gt;Left Arrow&lt;/button&gt;
    &lt;span&gt;2015&lt;/span&gt;
    &lt;button&gt;Right Arrow&lt;/button&gt;
  &lt;/header&gt;

  &lt;div class="datepicker__view flex-container"&gt;
    &lt;button&gt;Jan&lt;/button&gt;
    &lt;button&gt;Feb&lt;/button&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

The CSS couldn’t be any shorter. It’s meaningful to anyone reading the code and brief enough to write.</p>

<pre><code class="language-scss">
.flex-container {
  display: flex;
}

.datepicker__header {
  justify-content: space-between;
}

.datepicker__view {
  align-items: center;
  justify-content: flex-start;
}
</code></pre>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/357259f9-6db0-4676-921e-dc54c8d17312/14-calendar-layout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eae011a-dd61-4093-9cd2-79d7fd50b2a8/14-calendar-layout-opt-preview.png" alt="Figure 14" /></a>Figure 14. For this calendar month-picker, <code>justify-content: space-between</code> is used on the left, and <code>justify-content: flex-start</code> on the right. Both wrap content very differently. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/357259f9-6db0-4676-921e-dc54c8d17312/14-calendar-layout-opt.png">View large version</a>)</figcaption></figure>

These two examples clearly show why one must plan ahead. How will the content wrap? How will it react as the viewport is resized? Does the content need to be wrapped? These are important questions to ask to arrive at the right strategy for the context.</p>

## Layout

Flexbox is ideal for interface elements, but it also plays well with certain layout patterns. A typical pattern is a primary container (typically for the main content) floating entirely to one side and a complementary container floating to the other.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b517f3ac-6d93-480e-9270-664e1cd3ed8b/15-admin-layout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/167318ef-f7ac-4c56-bbaf-4dc165e460aa/15-admin-layout-opt-preview.png" alt="Figure 15" /></a><figcaption>Figure 15. Sidebar to the left and primary content to the right — this is a perfect scenario for flexbox. It also reminds me of the <a href="https://alistapart.com/article/fauxcolumns">faux columns</a> technique. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b517f3ac-6d93-480e-9270-664e1cd3ed8b/15-admin-layout-opt.png">View large version</a>)</figcaption></figure>

The code required for this pattern is heavenly to implement, and the extra required for a fallback is minimal.

The markup for the admin layout uses a series of <code>div</code>s to wrap each container, as seen above.</p>

<pre><code class="language-markup">
&lt;div class="admin-ui"&gt;
  &lt;div class="admin-ui__nav"&gt;…&lt;/div&gt;

  &lt;div class="admin-ui__body"&gt;
    &lt;nav&gt;…&lt;/nav&gt;
    &lt;main&gt;…&lt;/main&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

<pre><code class="language-scss">
.admin-ui__body {
  display: flex;
}

.admin-ui__body nav {
  flex: 30%;
}

.admin-ui__body main {
  flex: 70%;
}
</code></pre>

Here’s a great fallback for the layout pattern discussed in figure 14. The pattern doesn’t involve a complicated grid structure. Plus, our old friend <code>display: table</code> is ready to provide a hand when needed.</p>

<figure><br>
<p class="codepen">See the Pen <a href="https://codepen.io/dennisgaebel/pen/mJgvBp/">Display: table-cell</a> by Dennis Gaebel (<a href="https://codepen.io/dennisgaebel">@dennisgaebel</a>) on <a href="https://codepen.io">CodePen</a>.</p>

</figure>

The <code>display: table-cell</code> is a powerhouse CSS declaration that <a href="https://caniuse.com/#search=table">dates back to CSS 2</a> and is a perfectly reliable fallback for this context. The value causes the element to behave like a table element, which is exactly the kind of behavior we need in order to replicate the flexbox version. You could also swap the order using some table trickery, with such declarations as <code>display: table-header-group</code> and <code>display: table-footer-group</code>.</p>

## Sticky Footers

Sticky footers are one of those rites of passage for aspiring web developers, where the footer is positioned at the bottom of the viewport. If content is added, it will push the footer down, but the footer would appear at the bottom of the viewport in any other case.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad3ce2a4-b88e-4e4d-bf58-80a793fc119d/16-admin-sidebar-stickyfooter-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3af28d50-8db7-4ac0-85b8-0036b6caf619/16-admin-sidebar-stickyfooter-opt-preview.png" alt="Figure 16" /></a>Figure 16. Sticky footer in the right sidebar. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad3ce2a4-b88e-4e4d-bf58-80a793fc119d/16-admin-sidebar-stickyfooter-opt.png">View large version</a>)</figcaption></figure>

Here is the markup for the right sidebar:

<pre><code class="language-markup">
&lt;div class="admin-edit"&gt;
  &lt;button class="admin-edit__save"&gt;Save Deal&lt;/button&gt;

  &lt;div class="admin-edit__footer"&gt;
      &lt;p&gt;…&lt;/p&gt;
      &lt;button&gt;Copy&lt;/button&gt;
      &lt;button&gt;Delete&lt;/button&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

And here is the CSS:

<pre><code class="language-scss">
.admin-edit {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</code></pre>

Here’s a great fallback for flexbox sticky footers that also maintains the layout all the way back to IE 6.</p>

<figure><br>
<p class="codepen">See the Pen <a href="https://codepen.io/dennisgaebel/pen/LVvqOx/">Sticky footer on steroids</a> by Dennis Gaebel (<a href="https://codepen.io/dennisgaebel">@dennisgaebel</a>) on <a href="https://codepen.io">CodePen</a>.</p>

<figcaption>Figure 17. Flexbox Sticky Footer w/Table Display Fallback. Works in every browser going back to IE6!</figcaption></figure>

Another part of the layout where I took a chance with flexbox was the main application view, or what was termed the “pipeline” of the application. Each card has a defined width and takes advantage of the <code>flex</code> property. This gives each card a consistent and defined proportion.</p>

<figure><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154d9edd-09a0-44d8-af48-6724e8af87f8/17-pipeline-card-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154d9edd-09a0-44d8-af48-6724e8af87f8/17-pipeline-card-opt.png" alt="Pipeline Card" /></a>Pipeline. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154d9edd-09a0-44d8-af48-6724e8af87f8/17-pipeline-card-opt.png">View large version</a>)</figcaption></figure>

Flexbox helps to position the content of each card beautifully. The entire application is one big layout version of the movie <em>Inception</em>, where flexbox contains flexbox, which contains even tinier atoms and molecules using flexbox. It’s mind-boggling when you consider how hard developers used to fight to center an item, but today we accomplish this in only a few lines of code.</p>

## Be Careful

During browser testing, we discovered that combining the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/flex">flex</a> property with other spacing properties, such as margin and padding, resulted in a broken layout when viewed in IE 10 (see figure 18).</p>

<pre><code class="language-scss">
.parent {
  display: flex;
}
.parent .child {
  flex: 1;
  padding: 20px; /* Breaks layout in IE 10 */
}
</code></pre>

When a module’s parent wrapper, defined with <code>display: flex</code>, has children that use the <code>flex</code> property along with <code>padding</code> or <code>margin</code>, the layout breaks in IE 10.

The feature query <code>@supports (display: flex) {}</code> is supposed to be something like <a href="https://modernizr.com">Modernizr</a> but implemented with native CSS. Unfortunately, support for <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@supports"><code>@supports</code></a> is very poor at this time and should be avoided. Instead, here are some tips for fallback solutions:

*   Use Modernizr’s `no-flexbox` class to detect features.
*   Use transforms or a table display for centering.
*   Use a table display.
*   Control the order with table-display tactics, such as `table-caption`, `table-header-group` and `table-footer-group`.
*   Use floats as a fallback for entire layout structures.
*   Use inline or inline-block as a display fallback for inline patterns.
*   Use conditional comments for IE 9 and below to deliver non-flexbox styling.

Ian Devlin has a great article <a href="https://www.iandevlin.com/blog/2013/06/css/css-stacking-with-display-table">explaining stacking techniques</a>. He gives a great overview of how to control stacking order using <code>table-caption</code>, <code>table-header-group</code> and <code>table-footer-group</code>.</p>

## Conclusion

<strong>Flexbox today is very, very real</strong>. After many years of development, the specification has become much more stable, making it easier to achieve those CSS layout dreams. I also suggest going through Wes Bos’ <a href="https://flexbox.io">What the Flexbox?!</a> The simple 20-video crash course will help you master flexbox, all for free! The first 13 videos cover the fundamentals of flexbox; the last 7 are code-alongs in which Wes builds everything from navigation to a mobile app layout, entirely with flexbox! There is truly no time like the present to start using it in your work.

{{< signature "ds, ml, al, jb" >}}

