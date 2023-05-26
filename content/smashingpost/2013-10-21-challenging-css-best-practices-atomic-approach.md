---
title: Challenging CSS Best Practices
slug: challenging-css-best-practices-atomic-approach
author: thierry-koblentz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0899a4df-097c-4e76-acc5-1720a1cf2eee/illu-css.jpg
date: 2013-10-21T08:32:42.000Z
description: >-
  When it comes to CSS, I believe that the sacred principle of “separation of
  concerns” (SoC) has lead us to accept **bloat, obsolescence, redundancy, poor
  caching** and more. Now, I’m convinced that the only way to improve how we
  author style sheets is by moving away from this principle.
categories:
  - Coding
  - CSS
  - HTML
  - Semantics
---
_**Editor’s Note**: This article features techniques that are used in practice by Yahoo! and question coding techniques that we are used to today. You might be interested in reading [Decoupling HTML From CSS](https://www.smashingmagazine.com/2012/04/20/decoupling-html-from-css/) by Jonathan Snook, [On HTML Elements Identifiers](https://nefariousdesigns.co.uk/on-html-element-identifiers.html) by Tim Huegdon and [Atomic Design With Sass](https://www.smashingmagazine.com/2013/08/02/other-interface-atomic-design-sass/) by Robin Rendle as well. Please keep in mind: some of the mentioned techniques are not considered to be best practices._

![css best practices](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7fd599c-c918-470d-9968-9e63173f823a/class-stop-mini.jpg "Challenging CSS Best Practices")

When it comes to CSS, I believe that the sacred principle of “[separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns)” (SoC) has lead us to accept **bloat, obsolescence, redundancy, poor caching** and more. Now, I’m convinced that the only way to improve how we author style sheets is by moving away from this principle.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [53 CSS-Techniques You Couldn’t Live Without](https://www.smashingmagazine.com/2007/01/53-css-techniques-you-couldnt-live-without/)
*   [<span class="headline">The Road To Reusable HTML Components</span>](https://www.smashingmagazine.com/2012/10/road-reusable-html-components/)
*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)

For those of you who have never heard of the SoC principle in the context of Web design, it relates to something commonly known as the “separation of the three layers”:

{{% feature-panel %}}

*   structure,
*   presentation,
*   behavior.

It is about dividing these concerns into separate resources: an HTML document, one or more cascading style sheets and one or more JavaScript files.

But when it comes to the presentational layer, “best practice” goes way beyond the separation of resources. CSS authors thrive on styling documents entirely through style sheets, an approach that has been sanctified by [Dave Shea](https://www.mezzoblue.com/)’s excellent project [CSS Zen Garden](https://www.csszengarden.com/). CSS Zen Garden is what most — if not all — developers consider to be the **standard** for how to author style sheets.</p>

## The Standard

To help me illustrate issues related to today’s best practices, I’ll use a very common pattern: the [media object](https://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/). Its combination of markup and CSS will be our starting point.</p>

### Markup

In our markup, a wrapper (`div.media`) contains an image wrapped in a link (`a.img`), followed by a div (`div.bd`):

<pre><code class="language-markup">
&lt;div class="media"&gt;
  &lt;a href="https://twitter.com/thierrykoblentz" class="img"&gt;
        &lt;img src="thierry.jpg" alt="me" width="40" /&gt;
  &lt;/a&gt;
  &lt;div class="bd"&gt;
    @thierrykoblentz 14 minutes ago
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

### CSS

Let’s give a 10-pixel margin to the wrapper and style both the wrapper and `div.bd` as [block-formatting contexts](https://www.yuiblog.com/blog/2010/05/19/css-101-block-formatting-contexts/) (BFC). In other words, **the wrapper will contain the floated link**, and the content of `div.bd` will not wrap around said link. A gutter between the image and text is created with a 10-pixel margin (on the float):

<pre><code class="language-css">
.media {
    margin: 10px;
}
.media,
.bd {
    overflow: hidden;
    _overflow: visible;
    zoom: 1;
}
.media .img {
    float: left;
    margin-right: 10px;
}
.media .img img {
    display: block;
}
</code></pre>

### Result

Here is the presentation of the wrapper, with the image in the link and the blob of text:

<div class="result Atomiccss">
    <div class="media">
      <a href="https://twitter.com/thierrykoblentz" class="img">
        <img width="40" src="https://0.gravatar.com/avatar/a1c5c36dfde41ff8c4a92c94180b2dbf?s=78&amp;d=http%3A%2F%2F0.gravatar.com%2Favatar%2Fad516503a11cd5ca435acc9bb6523536%3Fs%3D78&amp;r=G" alt="me" />
      </a>
      <div class="bd">
        @thierrykoblentz 14 minutes ago
      </div>
    </div>
</div>

### A New Requirement Comes In

Suppose we now need to be able to display the image on the other side of the text as well.</p>

### Markup

Thanks to the magic of BFC, all we need to do is change the styles of the link. For this, we use a new class, `imgExt`.

<pre><code class="language-markup">
&lt;div class="media"&gt;
    &lt;a href="https://twitter.com/thierrykoblentz" class="imgExt"&gt;
        &lt;img src="thierry.jpg" alt="me" width="40" /&gt;
  &lt;/a&gt;
  &lt;div class="bd"&gt;
    @thierrykoblentz 14 minutes ago
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

### CSS

We’ll add an extra rule to float the link to the right and change its margin:

<pre><code class="language-css">
.media {
    margin: 10px;
}
.media,
.bd {
    overflow: hidden;
    _overflow: visible;
    zoom: 1;
}
.media .img {
    float: left;
    margin-right: 10px;
}
.media .img img {
    display: block;
}
.media .imgExt {
    float: right;
    margin-left: 10px;
}
</code></pre>

### Result

The image is now displayed on the opposite side:

<div class="result Atomiccss">
    <div class="media">
        <a href="https://twitter.com/thierrykoblentz" class="imgExt">
            <img width="40" src="https://0.gravatar.com/avatar/a1c5c36dfde41ff8c4a92c94180b2dbf?s=78&amp;d=http%3A%2F%2F0.gravatar.com%2Favatar%2Fad516503a11cd5ca435acc9bb6523536%3Fs%3D78&amp;r=G" alt="me" />
        </a>
        <div class="bd">@thierrykoblentz 14 minutes ago</div>
    </div>
</div>

### One More Requirement Comes In

Suppose we now need to make the text smaller when this module is inside the right rail of the page. To do that, we create a new rule, using `#rightRail` as a contextual selector:

### Markup

Our module is now inside a `div#rightRail` container:

<pre><code class="language-markup">
&lt;div id="rightRail"&gt;
    &lt;div class="media"&gt;
        &lt;a href="https://twitter.com/thierrykoblentz" class="img"&gt;
            &lt;img src="thierry.jpg" alt="me" width="40" /&gt;
        &lt;/a&gt;
        &lt;div class="bd"&gt;
            @thierrykoblentz 14 minutes ago
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;
</code></pre>

### CSS

Again, we create an extra rule, this time using a descendant selector, `#rightRail .bd`.

<pre><code class="language-css">
.media {
    margin: 10px;
}
.media,
.bd {
    overflow: hidden;
    _overflow: visible;
    zoom: 1;
}
.media .img {
    float: left;
    margin-right: 10px;
}
.media .img img {
    display: block;
}
.media .imgExt {
    float: right;
    margin-left: 10px;
}
#rightRail .bd {
    font-size: smaller;
}
</code></pre>

### Result

Here is our original module, showing inside `div#rightRail`:

<div class="result Atomiccss">
    <div id="rightRail">
        <div class="media">
          <a href="https://twitter.com/thierrykoblentz" class="img">
            <img width="40" src="https://0.gravatar.com/avatar/a1c5c36dfde41ff8c4a92c94180b2dbf?s=78&amp;d=http%3A%2F%2F0.gravatar.com%2Favatar%2Fad516503a11cd5ca435acc9bb6523536%3Fs%3D78&amp;r=G" alt="me" />
          </a>
          <div class="bd">
            @thierrykoblentz 14 minutes ago
          </div>
        </div>
    </div>
</div>

## What’s Wrong With This Model?

*   **Simple changes to the style of our module have resulted in new rules in the style sheet.**  
    There must be a way to style things without _always_ having to write more CSS rules.
*   **We are grouping selectors for common styles (`.media,.bd {}`).**  
    Grouping selectors, rather than using a class associated with these styles, will lead to more CSS.
*   **Of our six rules, four are context-based.**  
    Rules that are context-specific are hard to maintain. Styles related to such rules are not very reusable.
*   **RTL and LTR interfaces become complicated.**  
    To change direction, we’d need to overwrite some of our styles (i.e. write _more_ rules). For example:

<pre><code class="language-css">
.rtl .media .img {
    margin-right: auto; /* reset */
    float: right;
    margin-left: 10px;
}
.rtl .media .imgExt {
    margin-left: auto; /* reset */
    float: left;
    margin-right: 10px;
}
</code></pre>

## Meet Atomic Cascading Style Sheet

<blockquote>
<dl>
<dt><a href="https://www.google.com/search?q=define%3A+atomic">a·tom·ic</a></dt>
<dd>/ə'tämik/</dd>
<dd><em>of or forming a single irreducible unit or component in a larger system.</em></dd>
</dl>
</blockquote>

As we all know, the smaller the unit, the more reusable it is.

<blockquote class="twitter-tweet"><p>"Treat code like Lego. Break code into the smallest little blocks possible." — <a href="https://twitter.com/csswizardry">@csswizardry</a> (via <a href="https://twitter.com/stubbornella">@stubbornella</a>) <a href="https://twitter.com/search?q=%23btconf&amp;src=hash">#btconf</a></p>

&mdash; Smashing Magazine (@smashingmag) <a href="https://twitter.com/smashingmag/statuses/339024926197559296">May 27, 2013</a></blockquote>

To break down styles into irreducible units, we can **map classes to a single style**, rather than many. This will result in a more granular palette of rules, which in turn improves reusability.

Let’s revisit the media object using this new approach.</p>

### Markup

We are using five classes, none of which are related to content:

<pre><code class="language-markup">
&lt;div class="Bfc M-10"&gt;
    &lt;a href="https://twitter.com/thierrykoblentz" class="Fl-start Mend-10"&gt;
        &lt;img src="thierry.jpg" alt="me" width="40" /&gt;
    &lt;/a&gt;
    &lt;div class="Bfc Fz-s"&gt;
        @thierrykoblentz 14 minutes ago
    &lt;/div&gt;
&lt;/div&gt;
</code></pre>

### CSS

Each class is associated with one particular style. For the most part, this means we have one declaration per rule.

<pre><code class="language-css">
.Bfc {
    overflow: hidden;
    zoom: 1;
}
.M-10 {
    margin: 10px;
}
.Fl-start {
    float: left;
}
.Mend-10 {
    margin-right: 10px;
}
.Fz-s {
    font-size: smaller;
}
</code></pre>

### Result

<div class="result Atomiccss">
    <div class="Bfc M-10">
      <a href="https://twitter.com/thierrykoblentz" class="Fl-start Mend-10">
        <img loading="lazy" decoding="async" src="https://0.gravatar.com/avatar/a1c5c36dfde41ff8c4a92c94180b2dbf?s=78&amp;d=http%3A%2F%2F0.gravatar.com%2Favatar%2Fad516503a11cd5ca435acc9bb6523536%3Fs%3D78&amp;r=G" alt="me" width="40" />
      </a>
      <div class="Bfc Fz-s">
        @thierrykoblentz 14 minutes ago
      </div>
    </div>
</div>

### What Is This about?

Let’s ignore the class names for now and focus on what this does (or does not):

*   **No contextual styling**  
    We do not use contextual or descendant selectors, which means that our style sheet has no dead weight.
*   **Directions (left and right) are “abstracted.”**  
    Rather than overwriting styles, we serve a RTL style sheet that contains rules such as these:

<pre><code class="language-css">
.Fl-start {
    float: right;
}
.Mend-10 {
    margin-left: 10px;
}
</code></pre>

Same classes, same properties, different values.

But the most important thing to notice here is that **we are styling via markup**. We have changed the context in which we style our modules. We are now editing HTML templates instead of style sheets.

I believe that this approach is a game-changer because it **narrows the scope dramatically**. We are styling not in the global scope (the style sheet), but at the module and block level. We can change the style of a module without worrying about breaking something else on the page. And we can do this without adding any rule to the style sheet, let alone creating a new class and rule:

<pre><code class="language-css">
.someBasicStyleForThisElementHere {...}
</code></pre>

We get no redundancy. Selectors are not duplicated, and styles belong to a single rule instead of being part of many. For example, the style sheets that this page links to contain 72 `float` declarations.

Also, abandoning a style — for example, deciding to always keep the image on the left side of the module — does not make any of our rules obsolete.</p>

### Sound Good?

Not sold yet? I hear you saying, “This goes against every single rule in the book. This is no better than inline styling. And your class names are not only cryptic, but unsemantic, too!”

Fair enough. Let’s address these concerns.</p>

### Regarding Unsemantic Class Names

If you check the W3C’s “[Tips for Webmasters](https://www.w3.org/QA/Tips/goodclassnames),” where it says “Good names don’t change,” you’ll see that the argument is about _maintenance_, not semantics per se. All it says is that changing styles is easier in a CSS file than in multiple HTML files. `.border4px` would be a bad name only if changing the style of an element required us to change the declaration that that class name is associated with. In other words:

<pre><code class="language-css">
.border4px {border-width:2px;}
</code></pre>

### Regarding Cryptic Class Names

For the most part, these class names follow the syntax of Zen Coding — see the “[Zen Coding Cheat Sheet](https://code.google.com/archive/p/zen-coding/ "Zen coding cheat sheet (PDF)")” (PDF) — now renamed [Emmet](https://docs.emmet.io/cheat-sheet/). In other words, they are simple abbreviations.

There are exceptions for styles associated with direction (left and right) and styles that involve a combination of declarations. For example, `Bfc` stands for “block-formatting context.”

### Regarding Mimicking Inline Styles

Hopefully, the diagram below clears things up:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/645e842e-e639-410c-98b3-482652c9c4f2/venn-diagram-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bf58dff-5717-4cca-9e40-fd542ce6937c/venn-diagram-500-mini.png" alt="Venn diagram that shows all possible logical relations between inline styles and styling via classes and markup." width="500" height="327" /></a><figcaption>Inline styles versus Atomic CSS.</figcaption></figure>

*   **Specificity**  
    The technique is not as specific as `@style`. It **lowers style weight** because rules rely on a single class, as opposed to rules like `.parent .bd {}`, which clocks in at 0.0.2.0 (see “[CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/)”).
*   **Verbosity**  
    Most classes are abbreviations of declarations (for example, `M-10` versus `margin: 10px`). Some classes, such as `Bfc`, refer to more than one style (see “Mapping” in the diagram above). Other classes use “start” and “end” keywords, rather than left and right values (see “Abstraction” in the diagram above).

Here are the advantages of `@style`:

*   **Scope**  
    Styles are “sandboxed” to the nodes they are attached to.
*   **Portability**  
    Because the styles are “encapsulated,” you can move modules around without losing their styles. Of course, we still need the style sheet; however, because we are making context irrelevant, modules can live anywhere on a page, website or even network.</p>

## The Path To Bloat

Because the styles of our module are tied only to presentational class names, **they can be anything we want them to be**. For example, if we need to create a simple two-column layout, all we need to do is replace the link with a `div` in our template. That would look like this:

<pre><code class="language-markup">
&lt;div class="Bfc M-10"&gt;
    &lt;div class="Fl-start Mend-10 W-25"&gt;
        column 1
    &lt;/div&gt;
    &lt;div class="Bfc"&gt;
        column 2
    &lt;/div&gt;
&lt;/div&gt;
</code></pre>

And we would need only one extra rule in the style sheet:

<pre><code class="language-css">
.Bfc {
    overflow: hidden;
    zoom: 1;
}
.M-10 {
    margin: 10px;
}
.Fl-start {
    float: left;
}
.Mend-10 {
    margin-right: 10px;
}
.Fz-s {
    font-size: smaller;
}
.W-50 {
    width: 50%;
}
</code></pre>

Compare this to the traditional way:

<pre><code class="language-markup">
&lt;div class="wrapper"&gt;
    &lt;div class="sidebar"&gt;
        column 1
    &lt;/div&gt;
    &lt;div class="content"&gt;
        sidebar
    &lt;/div&gt;
&lt;/div&gt;
</code></pre>

This would require us to create three new classes, to add an extra rule and to group selectors.

<pre><code class="language-css">
.wrapper,
.content,
.media,
.bd {
    overflow: hidden;
    _overflow: visible;
    zoom: 1;
}
.sidebar {
    width: 50%;
}
.sidebar,
.media .img {
    float: left;
    margin-right: 10px;
}
.media .img img {
    display: block;
}
</code></pre>

I think the code above pretty well demonstrates the price we pay for following the SoC principle. In my experience, all it does is grow style sheets.

Moreover, the larger the files, the more complex the rules and selectors become. And then no one would dare edit the existing rules:

*   We leave alone rules that we suspect to be obsolete for fear of breaking something.
*   We create new rules, rather than modify existing ones, because we are not sure the latter is 100% safe.

In other words, we make things worse because **we can get away with bloat**.

Nowadays, people are accustomed to very large style sheets, and many authors think they come with the territory. Rather than fighting bloat, they use tools (i.e. preprocessors) to help them deal with it. [Chris Eppstein tells us](https://chriseppstein.github.io/blog/2013/04/22/joining-linkedin/):

<blockquote>
<p>"LinkedIn has over 1,100 Sass files (230k lines of SCSS) and over 90 web developers writing Sass every day."</p>
</blockquote>

### CSS Bloat vs. HTML Bloat

Let’s face it: the data has to live somewhere. Consider these two blocks:

<pre><code class="language-markup">
&lt;div class="sidebar"&gt;
</code></pre>

<pre><code class="language-markup">
&lt;div class="Fl-start Mend-10 W-25"&gt;
</code></pre>

In many cases, the “semantic” class name makes up more bytes than the presentational class name (`.wrapper` versus `.Bfc`). But I do not think this is a real concern compared to what most apps onboard these days via `data-` attributes.

This is where [gzip](https://www.gzip.org/ "A compression utility") comes into play, because the high redundancy in class names across a document would achieve better compression. And the same is true of style sheets, in which we have many redundant sequences:

<pre><code class="language-css">
.M-1 {margin: 1px;}
.M-2 {margin: 2px;}
.M-4 {margin: 4px;}
.M-6 {margin: 6px;}
.M-8 {margin: 8px;}
etc.
</code></pre>

## Caching

Presentational rules **do not change**. Style sheets made from such rules mature into tool sets in which authors can find everything they need. By their nature, they stop growing and become **immutable**, and immutable is **cache-friendly**.</p>

## No More .button Class?

The technique I’m discussing here is not about banning “semantic” class names or rules that group many declarations. The idea is to reevaluate the benefits of the common approach, rather than adopting it as the _de facto_ technique for styling Web pages. In other words, we are restricting the “component” approach to the few cases in which it makes the most sense.

For example, you may find the following rules in our style sheets, rules that set styles for which we do not create simple classes or rules that ensure cross-browser support.

<pre><code class="language-css">
.button {
    display: inline-block;
    *display: inline;
    zoom: 1; 
    font-size: bold 16px/2em Arial;
    height: 2em;
    box-shadow: inset 1px 1px 2px 0px #fff;
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0.05, #ededed), color-stop(1, #dfdfdf));
    background: linear-gradient(center top, #ededed 5%, #dfdfdf 100%);
    filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#ededed', endColorstr='#dfdfdf');
    background-color: #ededed;
    color: #777;
    text-decoration: none;
    text-align: center;
    text-shadow: 1px 1px 2px #ffffff;
    border-radius: 4px;
    border: 2px solid #dcdcdc;
}
.modal {
    position: fixed;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%,-50%);
    -ms-transform: translate(-50%,-50%);
    transform: translate(-50%,-50%);
    *width: 600px;
    *margin-left: -300px;
    *top: 50px;
}
@media \0screen {
    .modal {
        width: 600px;
        margin-left: -300px;
        top: 50px;
    }
}
</code></pre>

On the other hand, you would not see rules like the ones below (i.e. styles bound to particular modules), because we prefer to apply these same styles using multiple classes: one for font size, one for color, one for floats, etc.

<pre><code class="language-css">
.news-module {
    font-size: 14px;
    color: #555;
    float: left;
    width: 50%;
    padding: 10px;
    margin-right: 10px;
}
.testimonial {
    font-size: 16px;
    font-style: italic;
    color: #222;
    padding: 10px;
}
</code></pre>

## Do We Include Every Possible Style In Our Style Sheet?

The idea is to have a pool of rules that authors can choose from to style anything they want. Styles that are common enough across a website would become part of the style sheet. If a style is too specific, then we’d rely on `@style` (the style attribute). In other words, we’d prefer to **pollute the markup rather than the style sheet**. The primary goal is to create a sheet made of rules that address various design patterns, from a basic rule that floats an element to “helper” classes.

<pre><code class="language-css">
/**
 * one liner with ellipsis
 * 1. we inherit hyphens:auto from body, which would break "Ell" in table cells
 */
.Ell {
    max-width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    -webkit-hyphens: none; /* 1 */
    -ms-hyphens: none;
    -o-hyphens: none;
    hyphens: none;
}
/**
 * kinda line-clamp
 * two lines according to default font-size and line-height
 */
.LineClamp {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    font-size: 13px;
    line-height: 1.25;
    max-height: 32px;
    _height: 32px;
    overflow: hidden;
}
/**
 * reveals an hidden element on :hover or :focus
 * visibility can be forced by applying the class "RevealNested-on"
 * IE8+
 */
:root .NestedHidden {
    opacity: 0;
}
:root .NestedHidden:focus,
:root .RevealNested:hover .NestedHidden,
:root .RevealNested-on .NestedHidden {
    opacity: 1;
}
</code></pre>

## How Does This Scale?

We have just released a brand new [My Yahoo](https://my.yahoo.com), which relies heavily on this technique. This is how it compares to a few other Yahoo products (after gzip’ing):

<table class="table-overview">
        <tr>
          <th></th>
          <th><strong>CSS Assets</strong></th>
       </tr>
       <tr>
          <td>answers.yahoo.com</td>
          <td>30.1 KB</td>
       </tr>
        <tr>
           <td>sports.yahoo.com</td>
           <td>67.4 KB</td>
        </tr>
        <tr>
           <td>omg.yahoo.com</td>
           <td>46.2 KB</td>
        </tr>
        <tr>
           <td>yahoo.com</td>
           <td>45.9 KB</td>
        </tr>
        <tr>
           <td>my.yahoo.com</td>
           <td>21.3 KB</td>
        </tr>
   </tbody>
</table>

<p>Our style sheet weighs 17.9 KB (about 3 KB of which are property-specific), and it is shareable (unlike the style sheets of other properties). The reason for this is that none of the rules it contains relate to content.

## Wrapping Up

<p>Because <strong>presentational class names have always been deemed “out of bounds</strong>,” we &mdash; the community &mdash; have not really investigated what their use entails. In fact, in the name of best practice, we’ve dismissed every opportunity to explore their potential benefits.</p>

<p>Here at Yahoo, <a href="https://twitter.com/renatoiwa">@renatoiwa</a>, <span class="removed_link" title="https://twitter.com/StevenRCarlson">@StevenRCarlson</span> and <a href="https://twitter.com/thierrykoblentz">I</a> are developing projects with this new <a href="https://engineering.appfolio.com/2012/11/16/css-architecture/">CSS architecture</a>. The code appears to be predictable, reusable, maintainable and scalable. These are the results we’ve experienced so far:</p>

<ul>
<li><strong>Less bloat</strong><br />
We can build entire modules without adding a single line to the style sheets.</li>

<li><strong>Faster development</strong><br />
Styles are driven by classes that are not related to content, so we can copy and paste existing modules to get started.</li>

<li><strong>RTL interface for free</strong><br />
Using start and end keywords makes a lot of sense. It saves us from having to write extra rules for RTL context.</li>

<li><strong>Better caching</strong><br />
A huge chunk of CSS can be shared across products and properties.</li>

<li><strong>Very little maintenance (on the CSS side)</strong><br />
Only a small set of rules are meant to change over time.</li>

<li><strong>Less abstraction</strong><br />
There is no need to look for rules in a style sheet to figure out the styling of a template. It’s all in the markup.</li>

<li><strong>Third-party development</strong><br />
A third party can hand us a template without having to attach a style sheet (or a <code>style</code> block) to it. No custom rules from third parties means no risk of breakage due to rules that have not been properly namespaced.</li>
</ul>

<p>(Note that if maintenance is easier on the CSS side than on the HTML side, then the reason is simply that we can cheat on the CSS side by not cleaning up rules. But if we were required to keep things lean and clean, then the pain would be the same.)</p>

### Final Note

<p>I was at a <a href="https://www.meetup.com/sfhtml5/events/131694202/">meetup</a> a couple of weeks ago, where I heard Colt McAnlis say, “<a href="https://www.youtube.com/watch?v=OPBvdsFi7Ss&amp;feature=player_detailpage#t=11041">Tools, not rules</a>.” A quick search for this idiom <span class="removed_link" title="https://notrulestools.com/Main_Page">returned this</span>:</p>

<blockquote>
<p>"We all need to be open to new learnings, new approaches, new best practices and we need to be able to share them."</p>
</blockquote>

{{< signature "al, ea" >}}

<style>
/**
 * custom styles for this article 
 * Namespace: "Atomiccss"
 */
.Atomiccss .media {
    margin: 10px;
}
.Atomiccss .media,
.Atomiccss .bd {
    overflow: hidden;
    _overflow: visible;
    zoom: 1;
}
.Atomiccss .media .img {
    float: left;
    margin-right: 10px;
}
.Atomiccss .media .img img {
    display: block;
}
.Atomiccss .media .imgExt {
    float: right;
    margin-left: 10px;
}
.Atomiccss #rightRail .bd {
    font-size: smaller;
}
/* ACSS */
.Atomiccss .Bfc {
    overflow: hidden;
    zoom: 1;
}
.Atomiccss .M-10 {
    margin: 10px;
}
.Atomiccss .Fl-start {
    float: left;
}
.Atomiccss .Mend-10 {
    margin-right: 10px;
}
.Atomiccss .Fz-s {
    font-size: smaller;
}
.Atomiccss img {
    width: 40px;
}
</style>

