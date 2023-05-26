---
title: 'Benton Modern, A Case Study On Art-Directed Responsive Web Typography'
slug: benton-modern-typography-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07b9009c-50a9-4ab4-97dd-fe039cdb9e6b/11-optical-sizes-subhead-opt-small.jpg
date: 2015-05-27T21:02:52.000Z
author: marko-dugonjic
description: >-
  Having the ability to set legible body copy is an absolute must, and we’ve
  come a long way with web typography since the dawn of web design. However, I
  feel like we have allowed the lack of variety prior to the rise of web fonts
  to dampen our creativity now that [thousands of web fonts are at our
  disposal](https://www.smashingmagazine.com/2014/03/12/taking-a-second-look-at-free-fonts/).
  Have usability conventions and the web’s universality steered us away from
  proper art direction? Have we forgotten about art direction altogether? I
  believe so.

  As designers, we can achieve much more with type, and with just a little more
  thought and creativity, we can finally start to take full advantage of the
  [type
  systems](https://www.smashingmagazine.com/2013/04/18/introduction-to-programming-type-systems/)
  available. Let’s look at ways we can push typographic design on the web
  further, beyond the status quo of today.
categories:
  - Typography
  - Fonts
  - Design
  - Responsive Design
---
Having the ability to set legible body copy is an absolute must, and we’ve come a long way with web typography since the dawn of web design. However, I feel like we have allowed the lack of variety prior to the rise of web fonts to dampen our creativity now that **thousands of web fonts are at our disposal**. Have usability conventions and the web’s universality steered us away from proper art direction? Have we forgotten about art direction altogether? I believe so.

As designers, we can achieve much more with type, and with just a little more thought and creativity, we can finally start to take full advantage of the type systems available. Let’s look at ways we can push typographic design on the web further, beyond the status quo of today.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)
*   [Introducing Responsive Web Typography With FlowType.JS](https://www.smashingmagazine.com/2013/09/introducing-flowtype-js/)
*   [10 Principles For Readable Web Typography](https://www.smashingmagazine.com/2009/03/10-principles-for-readable-web-typography/)
*   [The Perfect Paragraph](https://www.smashingmagazine.com/2011/11/the-perfect-paragraph/)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3290bba8-3c3e-4029-afac-cb434b2b2ce3/01-formal-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/633fb953-e9ef-45f9-936a-1416df1e545e/01-formal-opt-small.png" alt="Benton Modern Formal version" /></a><figcaption>Benton Modern Formal version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3290bba8-3c3e-4029-afac-cb434b2b2ce3/01-formal-opt.png">View large version</a>)</figcaption></figure>

{{% feature-panel %}}

The [Benton Modern brochure website](https://bentonmodern.webtype.com/) (a project I was involved in) is a perfect example for showcasing how a large type family can be utilized to improve legibility and readability across breakpoints, while at the same time evoking emotion and providing a pleasant experience. We shall explore the ideas introduced to push the boundaries of typographic design on the web and get practical, too, with a key focus on responsive web typography.</p>

## First, The Basics Of Responsive Web Typography

You’re probably aware of responsive web typography by now and how it can solve challenges outside of core responsive web design. However, as the focus of this article isn’t on the ins and outs of responsive web typography, we shall not be exploring it in any great detail.

If you’re interested in learning more about general typesetting for the web and how to approach certain issues, [many](https://nicewebtype.com/) resources [exist](https://rwt.io/) to help you.

Furthermore, my "[Responsive Typography](https://vimeo.com/96406270)" talk and chapter in [Smashing Book 4](https://shop.smashingmagazine.com/products/smashing-book-4-ebooks), in which I propose reusing "traditional" typography rules and translating them to the language of CSS, should help kickstart any aspiring web typographer to improve their typography game.

To also help you on your way, here’s a quick rundown of some of the methods I’ve been advocating in recent years, methods that were applied to the Benton project, too:

<ul><br>
<li><strong>Provide different font sizes for different reading distances</strong>, currently achievable by detecting a device’s form factor using @media queries. Long term, this is probably not ideal &mdash; that is, until <a href="https://webdesign.maratz.com/lab/responsivetypography/">reading distance-detection techniques</a> become more feasible. In the meantime, use <a href="https://sizecalc.com">Size Calculator</a> by <a href="https://nicksherman.com">Nick Sherman</a> and <a href="https://chrislewis.codes">Chris Lewis</a> to calculate the physical or perceived font size when factoring in reading distance.</li>

<li><strong>Maintain perfect proportions in a paragraph</strong> with letter spacing, word spacing and line height properties for each breakpoint. <a href="https://universaltypography.com/demo">Universal Typography’s demo</a> by <a href="https://twitter.com/timbrown">Tim Brown</a> of <a href="https://twitter.com/nicewebtype">Nice Web Type</a> is a very useful tool that can help you experiment with and adjust your paragraph proportions accordingly.</li>

<li><strong>Establish hierarchy</strong> using either a typographic scale (<a href="https://modularscale.com">Modular Scale</a> is a useful tool by Tim Brown and <a href="https://twitter.com/scottkellum">Scott Kellum</a>) or different styles at the same font size &mdash; for instance, uppercase for <code>h2</code>, small caps for <code>h3</code> and italics for <code>h4</code> subheads. For more options and ideas on styling subheads, may I suggest you read "<a href="https://blog.typekit.com/2013/07/25/setting-subheads-with-css/">Setting Subheads With CSS</a>" and explore <a href="https://webdesign.maratz.com/lab/subheads/">examples of subheads set with CSS</a>.</li>

<li>For small screens, <strong>indent paragraphs and separate page sections</strong> with white space. For large screens, use block paragraphs and separate page sections with graphical elements (lines, shapes, color).</li>

<li><strong>Use graded fonts</strong> to normalize rendering across different pixel densities. Font grades are very subtle font weights used to compensate for different ink and paper qualities, as well as for different pixel densities on screen. This method is explained in detail in <a href="https://ia.net">iA</a>’s article "<a href="https://ia.net/know-how/responsive-typography">New Site With Responsive Typography</a>." In short, lighter grades are used for low-DPI screens and heavier grades for high-DPI screens, while graded fonts will also compensate for different sub-pixels’ direction between portrait and landscape mode on mobile and tablet devices.</li>

<li><strong>Look for <a href="https://kupferschrift.de/cms/2012/05/multi-axes-families/">type families that have multiple optical sizes</strong></a>, and use appropriate styles for body copy, tiny text and display sizes. For instance, <a href="https://www.fontbureau.com/">Font Bureau</a>, the company behind the Benton Modern family, makes many families like this with a wide stylistic palette.</li>

*   **Use different font widths** according to the width of the screen (see what happens with the subheads on the [Benton website](https://bentonmodern.webtype.com/) when you resize the browser window). For instance, use a condensed font for small screens and a wider font for larger desktop screens, just like on the [brochure website for Input](https://input.fontbureau.com/info/) (again, resize the window). In the case of the Benton project, we set different font widths manually for each breakpoint, but there’s also a solution for automatic swapping using [Font-To-Width](https://font-to-width.com) (by Sherman and Lewis) that takes advantage of multiple-width type families to fit pieces of text snugly within their containers.</p>

<li>Here’s another tip: If you intend to use Georgia or Verdana on large screens, replace them with <a href="https://georgiaverdana.com">Georgia Pro Condensed or Verdana Pro Condensed</a> on mobile screens. The reason why Georgia Pro and Verdana Pro’s condensed widths work well at small sizes is because they aren’t extremely condensed and, hence, can still be read comfortably.</li>

With this basic primer on responsive web typography out of the way, let me walk you through the process of designing a web page that is meant not only to inform, but to amaze!

## Show, Don’t Tell

[Webtype](https://www.webtype.com/) commissioned us to build a brochure website for Benton Modern soon after [Indra Kupferschmid](https://kupferschrift.de/) had seen my talk on responsive web typography at Smashing Conference in Oxford. The brief was to **showcase what could be achieved typographically** with a versatile type family coupled with responsive web typography using as many responsive techniques as possible, essentially putting into practice the elements presented and demonstrated in my talk. With Indra Kupferschmid as the chief type savant and Nick Sherman as the onboard quality assurance director, there was certainly to be no trouble with experimenting and pushing the boundaries.

From the very start, we wanted the user to experience the type family through the design and not just through a full page of body copy. That being said, in searching for the right metaphor to use, we eventually settled on creating two distinctive designs — [the formal](https://bentonmodern.webtype.com/formal/) and [the expressive](https://bentonmodern.webtype.com/expressive/). Both are fully responsive, utilizing the same HTML, and for all intents and purposes showcase the benefits of separating structure from presentation, so don’t forget to resize your browser and inspect the HTML and CSS.</p>

## Learning About The Typeface

Indra’s elaborate copy was a good starting point to get to know the typeface. When you receive content up front, as was the case in this project, it’s so much easier to create semantic HTML and to explore different styles. Here’s how we started our investigative testing, bearing in mind that Benton Modern comprises 48 styles in total:

1.  First, we tested all of the styles at large and small sizes, stretching and squeezing every which way possible. We used [Reading Edge optical sizes](https://www.fontbureau.com/ReadingEdge/) (designed for 9- to 14-pixel font sizes) as subheads, and display optical sizes (designed for headlines) for body copy. We wanted to see what could go wrong and challenge the intended use for each style. However, the solution that we settled on was still pretty much in line with the intended use for each optical size.
2.  Next, we tested how different styles behave in narrow columns versus wider blocks of text. Hyphenated and justified verus left-aligned. Tightly spaced versus loosely spaced.
3.  Lastly, we analyzed all of the glyphs one by one, searching for little hidden gems. Apart from the ampersand — which is always an obvious choice — another good candidate was the uppercase R.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4df69014-0867-4804-9f7d-0ed8ba8dadc6/02-early-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b1b1a9f-f05b-4ccd-a736-8ce2707fab4f/02-early-opt-small.png" alt="An early stage prototype" /></a><figcaption>An early-stage prototype. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4df69014-0867-4804-9f7d-0ed8ba8dadc6/02-early-opt.png">View large version</a>)</figcaption></figure>

From there, the next step was to apply some basic styles to the page. One of the early ideas was to adopt a traditional newspaper column layout, which we tried. With the exception of this high-level concept, we still didn’t have a definitive layout concept by this point.</p>

{{< vimeo id="128876276" >}}

Indented paragraphs in columns were too narrow to be [justified _and_ hyphenated](https://practicaltypography.com/hyphenation.html) properly, so we just kept the hyphenation to improve the texture a little bit.</p>

<pre><code class="language-css">.columns p {
   -webkit-hyphens: auto;
   -moz-hyphens: auto;
   hyphens: auto;
}
.columns p + p {
   text-indent: 1.5rem;
}
</code></pre>

We used columns only when there was enough horizontal space. But we also wanted to avoid columns bleeding out of the screen vertically, because that would require scrolling up and down during reading when moving from column to column. That’s why we introduced another @media query to test the height of the screen before applying columns.</p>

<pre><code class="language-css">@media only screen and (min-height: 25em) {

   @media only screen and (min-width: 40em) and (max-width: 59.9375em) {
      -webkit-columns: 2;
      -moz-columns: 2;
      columns: 2;
      -webkit-column-gap: 2.7em;
      -moz-column-gap: 2.7em;
      column-gap: 2.7em;
   }

   @media only screen and (min-width: 60em) {
      -webkit-columns: 3;
      -moz-columns: 3;
      columns: 3;
      -webkit-column-gap: 2.7em;
      -moz-column-gap: 2.7em;
      column-gap: 2.7em;
   }
}
</code></pre>

## Designing Content

The next step was to analyze the content in more detail. That way, we were able to establish what the different sections were and adjust the details as we went along.

The formal version was the first to be developed. We created a huge headline to reflect newspaper headlines and added the year that the series started. The deck was the obvious element to style next. We experimented with a condensed version, and to our surprise it worked immediately. At that stage, the page navigation still didn’t exist and was only included much later on to improve overall usability, as well as to demonstrate the use of brackets as graphic elements.

The sections were a little dull, though. The **hierarchy and arrangement of subhead**, intro paragraph and columns were quickly established using the rules explained previously, but something was still missing. After some trial and error, we decided to separate the different sections with dotted borders to further emphasize the fine detail in the design of the Benton Modern series, and we introduced the section sign § (Alt + 6 on a Mac) to mark the sections. However, that still wasn’t good enough, so we again previewed numerous glyphs to find suitable candidates for other sections. We ended up using § for "About," • for "Optical Sizes," an italic i for "How to Use," + for "Bonus Features" and * for "Pairings." Some of these characters are rarely used in web design, so introducing them as decorations felt natural.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f676ba47-0024-4bdc-89ec-480fe7bd3440/04-separators-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86e47c4c-e574-465e-b11f-586b799fb9fb/04-separators-opt-small.png" alt="Plenty of little details" /></a><figcaption>Plenty of little details. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f676ba47-0024-4bdc-89ec-480fe7bd3440/04-separators-opt.png">View large version</a>)</figcaption></figure>

At this point the design was pretty solid, but we still needed to highlight the most impressive facts to showcase to the reader the inherent versatility of the family. So we established a no-nonsense look and feel by enlarging the important numbers: 3 optical sizes, 48 styles to choose from, and 4 widths in display styles.

The first version of pairing swatches was set in [Pinterest](https://www.pinterest.com/)-inspired columns, as with the rest of the sections. Yet we had a need to change it — at least slightly — because this section was not about Benton Modern, but about its companions. [Benton Modern RE fonts](https://www.webtype.com/font/bentonmodern-re-family/) are really great at small sizes, so introducing the pairs as contrasting large headlines made sense. Indra’s selection of pairings worked very well without many additional adjustments. The only areas that required special attention were the **custom sizes for each headline**, especially if we wanted the headlines to resize with the screen.</p>

## Viewport Width For Smooth Type Scaling

The only CSS units that support smooth scaling are `vw` (1% of the viewport’s width), `vh` (1% of the viewport’s height), `vmax` (1% of the longest side) and `vmin` (1% of the shortest side). The resulting CSS for one headline is composed of three font-size declarations — values in pixels, [root ems](https://www.w3.org/TR/css3-values/#rem-unit) (`rems`) and viewport widths — one for each flexible breakpoint (small to medium screens) that covers older browsers, too:

<pre><code class="language-scss">
#swatch-benton-sans h1 {
   @include rem(font-size, #{208/16});
}
@media only screen and (max-width: 29.9375em) {
   #swatch-benton-sans h1 {
      @include rem(font-size, #{57/16});
      font-size: 18.75vw;
   }
}
@media only screen and (min-width: 30em) and (max-width: 61.9375em) {
   #swatch-benton-sans h1 {
      @include rem(font-size, #{86/16});
      font-size: 20vw;
   }
}
</code></pre>

As you can see, we’re using a Sass mixin here. It returns the given property with values in pixels, as well as in root em units.</p>

<pre><code class="language-scss">@mixin rem($property, $values) {
   $max: length($values);
   $pxValues: ’;
   $remValues: ’;

   @for $i from 1 through $max {
      $value: strip-unit(nth($values, $i));
      $pxValues: #{$pxValues + $value*16}px;
      @if $i &lt; $max {
         $pxValues: #{$pxValues + " "};
      }
   }

   @for $i from 1 through $max {
      $value: strip-unit(nth($values, $i));
      $remValues: #{$remValues + $value}rem;
      @if $i &lt; $max {
         $remValues: #{$remValues + " "};
      }
   }

   #{$property}: $pxValues;
   #{$property}: $remValues;
}
</code></pre>

## OpenType Features

Whenever you need to showcase important details within the content — in this case, OpenType features such as the alternate R, the ligatures and the small caps — it’s always good to highlight these features in an interesting way. We didn’t want to use CSS images for graphic details, so we simply enlarged the type and brought the details to focus. The difference between ligatures and default glyphs is clear, and comparing small caps with uppercase and lowercase counterparts is easy.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66d2871f-8375-4ab9-b4fd-8766fbc01beb/03-opentype-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8f32a27-2493-45e2-a64a-d3dba52f60a8/03-opentype-opt-small.png" alt="OpenType Features" /></a><figcaption>OpenType Features. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66d2871f-8375-4ab9-b4fd-8766fbc01beb/03-opentype-opt.png">View large version</a>)</figcaption></figure>

If you were wondering how to enable OpenType features in CSS, here are a couple of examples with vendor prefixes:

<pre><code class="language-css">/* Alternate characters */
-webkit-font-feature-settings: "ss01";
-moz-font-feature-settings: "ss01" 1;
font-feature-settings: "ss01";

/* Common ligatures (ff, fi, ffi, fl, ffl, fj, …) */
-webkit-font-feature-settings: "liga";
-moz-font-feature-settings: "liga" 1;
font-feature-settings: "liga";

/* Small caps */
-webkit-font-feature-settings: "smcp";
-moz-font-feature-settings: "smcp" 1;
font-feature-settings: "smcp";
</code></pre>

You can test all of the OpenType features available with CSS in [Richard Rutter](https://twitter.com/clagnut)’s [CSS3 Font-Feature-Settings OpenType Demo](https://clagnut.com/sandbox/css3/). Consult [Bram Stein](https://twitter.com/bram_stein)’s excellent [The State of Web Type](https://www.stateofwebtype.com/#font-feature-settings) to check which features are supported in which browsers and to what extent.</p>

### OpenType Features in Safari Are… a Drag

There’s one piece of bad news. Safari on both Mac and iOS support OpenType features but [ignores any assigned value](https://www.stateofwebtype.com/#font-feature-settings). The safest way to use alternate characters or small caps in Safari is by loading subset fonts (subset fonts contain only a subset of glyphs from the full font file). For the Benton Modern project, we decided to test browser capabilities with `@support` before applying small caps, and we provided a fallback for browsers that don’t support `font-feature-settings`:

<pre><code class="language-scss">@supports ((font-feature-settings: "smcp") or
   (-webkit-font-feature-settings: "smcp") or
   (-moz-font-feature-settings: "smcp" 1)) {
   .small-caps {
      text-transform: lowercase;
      -webkit-font-feature-settings: "smcp";
      -moz-font-feature-settings: "smcp" 1;
      font-feature-settings: "smcp";
   }
}
</code></pre>

## Expressive Details

The Formal newspaper-inspired style looked really great. It was well organized, with plenty of small details. But we wanted to push the design a little further. How about creating a **magazine-inspired design**? We retained the same emphasis on elements as in the formal version but fed the opening section and all section subheads with steroids using pseudo-elements (for example, the R and the asterisk on the "cover" page), and we created a specific arrangement for each subhead by repositioning each word in a subhead in a [Lubalinesque](https://lubalincenter.cooper.edu) manner.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3301f76-5a98-43d0-b1ae-cf95a56edc07/benton-expressive.png"><img loading="lazy" decoding="async"  property="image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/423fe267-6f07-4360-a2e8-a2f34fa51909/benton-modern-exerpt.png" alt="Expressive Details" /></a><figcaption>Expressive Details. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3301f76-5a98-43d0-b1ae-cf95a56edc07/benton-expressive.png">View large version</a>)</figcaption></figure>

### 3D Effects

The 3D effect on "The Complete Series" was achieved with multiple text shadows, as explained in Tim Brown’s [Typekit Practice](https://practice.typekit.com/) lesson "[Using Shades for Eye-Catching Emphasis](https://practice.typekit.com/lesson/using-shades/)."

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2daa436-f0cf-4b4e-90d3-50ed405bb6ee/06-3d-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8a7420b-641d-4687-9635-08da7308eab7/06-3d-opt-small.png" alt="3D Effects" /></a><figcaption>3D Effects. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2daa436-f0cf-4b4e-90d3-50ed405bb6ee/06-3d-opt.png">View large version</a>)</figcaption></figure>

### Drop Caps

Drop caps can be achieved simply by floating the first character. But [vertical metrics complexities](https://blog.typekit.com/2010/07/14/font-metrics-and-vertical-space-in-css/) as well as cross-browser inconsistency make it virtually impossible to get drop caps right. Luckily, Adobe engineers wrote [dropcap.js](https://webplatform.adobe.com/dropcap.js/), a small script that solves that problem. The setup is very straightforward, and it’s easy to adjust positioning by specifying the number of lines the drop cap should span, as well as the height of the drop cap itself. There’s a bonus: The script doesn’t require any external JavaScript libraries.</p>

<pre><code class="language-javascript">var dropcaps = document.querySelectorAll('.drop-cap');

if (window.innerWidth &lt; 600) {
   window.Dropcap.layout(dropcaps, 3);
} else {
   window.Dropcap.layout(dropcaps, 5, 3);
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a36641-4820-4c32-92f0-044e1fc318a7/07-dropcap-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e56e848-0e93-4f29-9b4e-4b6f57012542/07-dropcap-opt-small.png" alt="Drop Caps" /></a><figcaption>Drop Caps. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a36641-4820-4c32-92f0-044e1fc318a7/07-dropcap-opt.png">View large version</a>)</figcaption></figure>

### Flipped and Rotated Type

All elements that needed special treatment were wrapped in their respective spans and given dedicated class names. This meant adding non-semantic markup, but there was no other way around it, especially if we wanted to take full control over the presentation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650eb44d-6547-4119-8350-3e12af82e3de/08-flipped-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20ffdde6-44ef-4062-a3ec-516ea44b185c/08-flipped-opt-small.png" alt="Flipped and Rotated Type" /></a><figcaption>Flipped and Rotated Type. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650eb44d-6547-4119-8350-3e12af82e3de/08-flipped-opt.png">View large version</a>)</figcaption></figure>

We flipped parts of the pairings section subhead with the `transform: scale` rule. The great thing is that if the `transform` property is not supported by the browser, nothing will happen.</p>

<pre><code class="language-css">.flip {
   display: block;
   -webkit-transform: scale(-1, -1);
   -moz-transform: scale(-1, -1);
   transform: scale(-1, -1);
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/225c40f5-2a4c-4661-96cb-d6f9f28fa248/09-rotated-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81a2ca43-9b32-431a-b20b-2e2373509e83/09-rotated-opt-small.png" alt="Flipped and Rotated Type" /></a><figcaption>Flipped and Rotated Type. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/225c40f5-2a4c-4661-96cb-d6f9f28fa248/09-rotated-opt.png">View large version</a>)</figcaption></figure>

The same applies to the O in the "Bonus Features," which we rotated with the `transform: rotate` rule. When rotating letters, you might want to readjust the positioning after rotation (watch out for the aforementioned vertical metrics issues). The values will vary from typeface to typeface and glyph to glyph, so there’s no generic rule.</p>

<pre><code class="language-css">.o {
   -webkit-transform: rotate(90deg);
   -moz-transform: rotate(90deg);
   transform: rotate(90deg);
   /* Glyph-specific adjustments */
}
</code></pre>

## Setting Expressive Subheads

Setting responsive expressive subheads is a piece of cake when you grasp the underlying concept. We need to do only two things:

1.  set the font size of a container in viewport width units,
2.  size everything that’s inside the container in em units.</p>

<pre><code class="language-markup">
&#060;div class="container"&gt;
   &#060;h1&gt;
      &#060;span class="s1"&gt;You&#060;/span&gt;
      &#060;span class="s2"&gt;&#038;&#060;/span&gt;
      &#060;span class="s3"&gt;Me&#060;/span&gt;
   &#060;/h1&gt;
&#060;/div&gt;
</code></pre>

Elements inside the container can be repositioned either absolutely or using negative margins. If you’re using absolute positioning, then it’s best to fix the aspect ratio of the `h1`, thus retaining proportions. If you’re fixing the aspect ratio, you can also use percentages instead of ems, because now you have a height reference for vertical properties in place.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99c5357a-5de0-4293-afb6-c2f66cbddbbf/10-optical-sizes-subhead-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af83a6e1-9665-4fb4-9f15-fc32cbf6e5e5/10-optical-sizes-subhead-opt-small.png" alt="Setting Expressive Subheads" /></a><figcaption>Setting Expressive Subheads. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99c5357a-5de0-4293-afb6-c2f66cbddbbf/10-optical-sizes-subhead-opt.png">View large version</a>)</figcaption></figure>

Example of positioning with margins:

<pre><code class="language-css">.container {
   font-size: 10vw;
}
.container h1 {
   font-size: 1em;
   line-height: 1;
   width: 100%;
}
.s1 {
   margin-left: 1em;
   margin-top: 1em;
}
</code></pre>

Example of absolute positioning:

<pre><code class="language-css">.container {
   font-size: 10vw;
}
.container h1 {
   font-size: 1em;
   line-height: 1;
   position: relative;
   width: 100%;
   height: 0;
   padding-top: 75%; /* 4:3 aspect ratio */
   padding-top: 50%; /* 2:1 aspect ratio */
}
.s1 {
   position: absolute;
   left: 10%;
   top: 10%;
}
</code></pre>

Voila! Compare all three positioning variants in the [Expressive Web Typography](https://webdesign.maratz.com/lab/expressive-web-typography/) demo.</p>

## Steal Ideas!

Now you hopefully see how far we can take typography on the web. To take full advantage of the methods discussed in this article, look for type families with multiple font styles and optical sizes. The only reason we were able to make all of these responsive adjustments is that the Benton Modern is such a versatile typeface family with so many variants.

View the HTML and CSS source on [Benton Modern](https://bentonmodern.webtype.com), use those techniques to improve typography in your own projects, and let us know if you come up with something different. Setting type on the web still involves a lot of manual labor, especially for the smaller, more delicate details, but [typographic tools are emerging](https://typetester.org) to speed up the process. Until then, don’t be intimidated because there is always a solution to a given problem. The next time you are offered a challenging project, bite the bullet, test like crazy, and do whatever it takes.

{{< signature "al, ml" >}}

