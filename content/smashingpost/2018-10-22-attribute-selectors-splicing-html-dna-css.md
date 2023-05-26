---
title: 'Splicing HTML’s DNA With CSS Attribute Selectors'
slug: attribute-selectors-splicing-html-dna-css
author: john-rhea
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bced71ac-7b29-4779-9d2c-300c2c759e8d/attribute-selectors-splicing-html-dna-css.png
date: 2018-10-23T14:00:11+02:00
summary: >-
  Attribute selectors are magical. They can get you out of sticky problems, help you avoid adding classes and point out some problems in your code. But don’t worry, while attribute selectors are complex and powerful, they’re easy to learn and easy to utilize. In this article, we’ll discuss how they operate and give you some ideas about how to use them.
description: >-
  Attribute selectors are magical. They can get you out of sticky problems, help you avoid adding classes and point out some problems in your code. In this article, John explains how to use attribute selectors the right way.
categories:
  - CSS
  - HTML
  - JavaScript
---
For most of my career, attribute selectors have been more magic than science. I’d stare, gobsmacked, at the CSS for outputting a link in a print style sheet, understanding nothing. I’d dutifully copy, and paste it into my print stylesheet then run off to put out whatever project was the largest burning trash heap.

But you don’t have to stare slack-jawed at CSS attribute selectors anymore. By the end of this article, you’ll use them to run diagnostics on your site, fix otherwise unsolvable problems, and generate technologic experiences so advanced they feel like magic. You may think I’m promising too much and you’re right, but once you understand the power of attribute selectors, you might feel like exaggerating yourself.

On the most basic level, you put an HTML attribute in square brackets and call it an attribute selector like so:

<pre><code class="language-bash">[href] {
   color: chartreuse;
}
</code></pre>

The text of any element that has an `href` and doesn’t have a more specific selector will now magically turn chartreuse. Attribute selector specificity is the same as classes.

**Note**: *For more on the cage match that is CSS specificity, you can read “[CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/)” or if you like Star Wars: “[CSS Specificity Wars](https://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html)”.*

But you can do far more with attribute selectors. Just like your DNA, they have built-in logic to help you choose all kinds of attribute combinations and values. Instead of only exact matching the way a tag, class, or id selector would, they can match any attribute and even string values within attributes.

{{% feature-panel %}}

## Attribute Selection

Attribute selectors can live on their own or be more specific, i.e. if you need to select all `div` tags that had a `title` attribute.

<pre><code class="language-bash">div[title]
</code></pre>

But you could also select the children of divs that have a title by doing the following:

<pre><code class="language-bash">div [title]
</code></pre>

To be clear, no space between them means the attribute is on the same element (just like an element and class without a space), and a space between them means a descendant selector, i.e. selecting the element’s children who have the attribute.

You can get far more granular in how you select attributes including the values of attributes.

<pre><code class="language-bash">div[title="dna"]
</code></pre>

The above selects all divs with an exact title of “dna”. A title of “dna is awesome” or “dnamutation” wouldn’t be selected, though there are selector algorithms that handle each of those cases (and more). We’ll get to those soon.

**Note**: *Quotation marks are not required in attribute selectors in most cases, but I will use them because I believe it increases clarity and ensures edge cases work appropriately.*

If you wanted to select “dna” out of a space separated list like “my beautiful dna” or “mutating dna is fun!” you can add a tilde or “squiggly,” as I like to call it, in front of the equal sign.

<pre><code class="language-bash">div[title~="dna"]
</code></pre>

You can select titles such as “dontblamemeblamemydna” or “his-stupidity-is-from-upbringing-not-dna” then you can use the dollar sign $ to match the end of a title.

<pre><code class="language-bash">[title$="dna"]
</code></pre>

To match the front of an attribute value such as titles of “dnamutants” or “dna-splicing-for-all” use a caret.

<pre><code class="language-bash">[title^="dna"]
</code></pre>

While having an exact match is helpful it might be too tight of a selection, and the caret front match might be too wide for your needs. For instance, you might not want to select a title of “genealogy”, but still select both “gene” and “gene-data”. The pipe character (or vertical bar) is just that; it does an exact match, but includes when the exact match is followed by a dash.

<pre><code class="language-bash">[title|="gene"]
</code></pre>

Lastly, there’s a full search attribute operator that will match any substring.

<pre><code class="language-bash">[title*="dna"]
</code></pre>

But use it wisely as the above will match “I-like-my-dna-like-my-meat-rare” as well as “edna”, “kidnapping”, and “echidnas” (something Edna really shouldn’t do.)

{{% ad-panel-leaderboard %}}

What makes these attribute selectors even more powerful is that they’re stackable &mdash; allowing you to select elements with multiple matching factors.

But you need to find the `a` tag that has a title and has a class ending in “genes”? Here’s how:

<pre><code class="language-bash">a[title][class$="genes"]
</code></pre>

Not only can you select the attributes of an HTML element you can also print their mutated genes using pseudo-“science” (meaning pseudo-elements and the content declaration).

<div class="break-out">

<pre><code class="language-bash">&lt;span class="joke" title="Gene Editing!"&gt;What’s the first thing a biotech journalist does after finishing the first draft of an article?&lt;/span&gt;
</code></pre></div>

<pre><code class="language-css">.joke:hover:after {
   content: "Answer:" attr(title);
   display: block;
}
</code></pre>

The code above will show the answer to one of the worst jokes ever written on hover (yes, I wrote it myself, and, yes, calling it a “joke” is being generous).

The last thing to know is that you can add a flag to make the attribute searches case insensitive. You add an `i` before the closing square bracket.

<pre><code class="language-bash">[title*="DNA" i]
</code></pre>

And thus it would match “dna”, “DNA”, “dnA”, and any other variation.

The only downside to this is that the `i` only works in Firefox, Chrome, Safari, Opera and a smattering of mobile browsers.

Now that we’ve seen how to select with attribute selectors, let’s look at some use cases. I’ve divided them into two categories: *General Uses* and *Diagnostics*.

## General Uses

### Style By Input Type

You can style input types differently, e.g. email vs. phone.

<pre><code class="language-bash">input[type="email"] {
   color: papayawhip;
}
input[type="tel"] {
   color: thistle;
}
</code></pre>

### Display Telephone Links

You can hide a phone number at certain sizes and display a phone link instead to make calling easier on a phone.

<pre><code class="language-bash">span.phone {
   display: none;
}
a[href^="tel"] {
   display: block;
}
</code></pre>

### Internal vs. External Links, Secure vs. Insecure

You can treat internal and external links differently and style secure links differently from insecure links.

<pre><code class="language-bash">a[href^="http"]{
   color: bisque;
}
a:not([href^="http"]) {
  color: darksalmon;
}

a[href^="https://"]:after {
   content: url(unlock-icon.svg);
}
a[href^="https://"]:after {
   content: url(lock-icon.svg);
}
</code></pre>

{{% ad-panel-leaderboard %}}

### Download Icons

One attribute HTML5 gave us was “download” which tells the browser to, you guessed it, download that file rather than trying to open it. This is useful for PDFs and DOCs you want people to access but don't want them to open right now. It also makes the workflow for downloading lots of files in a row easier. The downside to the `download` attribute is that there’s no default visual that distinguishes it from a more traditional link. Often this is what you want, but when it’s not, you can do something like the below.

<pre><code class="language-bash">a[download]:after { 
   content: url(download-arrow.svg);
}
</code></pre>

You could also communicate file types with different icons like PDF vs. DOCX vs. ODF, and so on.

<pre><code class="language-bash">a[href$="pdf"]:after {
   content: url(pdf-icon.svg);
}
a[href$="docx"]:after {
   content: url(docx-icon.svg);
}
a[href$="odf"]:after {
   content: url(open-office-icon.svg);
}
</code></pre>

You could also make sure that those icons were only on downloadable links by stacking the attribute selector.

<pre><code class="language-bash">a[download][href$="pdf"]:after {
   content: url(pdf-icon.svg);
}
</code></pre>

### Override Or Reapply Obsolete/Deprecated Code

We’ve all come across old sites that have outdated code, but sometimes updating the code isn’t worth the time it’d take to do it on six thousand pages. You might need to override or even reapply a style implemented as an attribute before HTML5.

<div class="break-out">

<pre><code class="language-bash">&lt;div bgcolor="#000000" color="#FFFFFF"&gt;Old, holey genes&lt;/div&gt;

div[bgcolor="#000000"] { /*override*/
   background-color: #222222 !important;
}
div[color="#FFFFFF"] { /*reapply*/
   color: #FFFFFF;
}
</code></pre></div>

### Override Specific Inline Styles

Sometimes you’ll come across inline styles that are gumming up the works, but they’re coming from code outside your control. It should be said if you can change them that would be ideal, but if you can’t, here’s a workaround.

**Note**: *This works best if you know the exact property and value you want to override, and if you want it overridden wherever it appears.*

For this example, the element’s margin is set in pixels, but it needs to be expanded and set in `em`s so that the element can re-adjust properly if the user changes the default font size.

<div class="break-out">

<pre><code class="language-bash">&lt;div style="color: #222222; margin: 8px; background-color: #EFEFEF;"Teenage Mutant Ninja Myrtle&lt;/div&gt;

div[style*="margin: 8px"] {
   margin: 1em !important;
}
</code></pre></div>

**Note**: *This approach should be used with extreme caution as if you ever need to override this style you’ll fall into an* `!important` *war and kittens will die.*

### Showing File Types

The list of acceptable files for a file input is invisible by default. Typically, we’d use a pseudo element for exposing them and, though you can’t do pseudo elements on most `input` tags (or at all in Firefox or Edge), you can use them on file inputs.

<pre><code class="language-bash">&lt;input type="file" accept="pdf,doc,docx"&gt;

[accept]:after {
   content: "Acceptable file types: " attr(accept);
}
</code></pre>

### HTML Accordion Menu

The not-well-publicized `details` and `summary` tag duo are a way to do expandable/accordion menus with just HTML. Details wrap both the `summary` tag and the content you want to display when the accordion is open. Clicking on the summary expands the `detail` tag and adds an open attribute. The open attribute makes it easy to style an open `details` tag differently from a closed `details` tag.

<pre><code class="language-bash">&lt;details&gt;
  &lt;summary&gt;List of Genes&lt;/summary&gt;
    Roddenberry
    Hackman
    Wilder
    Kelly
    Luen Yang
    Simmons
&lt;/details&gt;
</code></pre>

<pre><code class="language-css">details[open] {
   background-color: hotpink;
}
</code></pre>

### Printing Links

Showing URLs in print styles led me down this road to understanding attribute selectors. You should know how to construct it yourself now. You simply select all `a` tags with an `href`, add a pseudo-element, and print them using `attr()` and `content`.

<pre><code class="language-bash">a[href]:after {
   content: " (" attr(href) ") ";
}
</code></pre>

### Custom Tooltips

Creating custom tooltips is fun and easy with attribute selectors (okay, fun if you’re a nerd like me, but easy either way).

**Note**: *This code should get you in the general vicinity, but may need some tweaks to the spacing, padding, and color scheme depending on your site's environment and whether you have better taste than me or not.*

<pre><code class="language-css">[title] {
  position: relative;
  display: block;
}
[title]:hover:after {
  content: attr(title);
  color: hotpink;
  background-color: slateblue;
  display: block;
  padding: .225em .35em;
  position: absolute;
  right: -5px;
  bottom: -5px;
}
</code></pre>

### AccessKeys

One of the great things about the web is that it provides many different options for accessing information. One rarely used attribute is the ability to set an `accesskey` so that that item can be accessed directly through a key combination and the letter set by `accesskey` (the exact key combination depends on the browser). But there’s no easy way to know what keys have been set on a website.

The following code will show those keys on `:focus`. I don’t use on `hover` because most of the time people who need the `accesskey` are those who have trouble using a mouse. You can add that as a second option, but be sure it isn’t the only option.

<pre><code class="language-css">a[accesskey]:focus:after {
   content: " AccessKey: " attr(accesskey);
}
</code></pre>

## Diagnostics

These options are for helping you identify issues either during the build process or locally while trying to fix issues. Putting these on your production site will make errors stick out to your users.

### Audio Without Controls

I don’t use the `audio` tag too often, but when I do use it, I often forget to include the `controls` attribute. The result: nothing is shown. If you’re working in Firefox, this code can help you suss out if you’ve got an audio element hiding or if syntax or some other issue is preventing it from appearing (it only works in Firefox).

<pre><code class="language-css">audio:not([controls]) {
  width: 100px;
  height: 20px;
  background-color: chartreuse;
  display: block;
}
</code></pre>

### No Alt Text

Images without alt text are a logistics and accessibility nightmare. They’re hard to find by just looking at the page, but if you add this they’ll pop right out.

**Note**: *I use* `outline` *instead of* `border` *because borders could add to the element’s width and mess up the layout.* `outline` *does not add width.*

<pre><code class="language-bash">img:not([alt]) { /* no alt attribute */ 
  outline: 2em solid chartreuse; 
}
img[alt=""] { /* alt attribute is blank */ 
  outline: 2em solid cadetblue; 
}
</code></pre>

### Asynchronous Javascript Files

Web pages can be a conglomerate of content management systems and plugins and frameworks and code that Ted (sitting three cubicles over) wrote on vacation because the site was down and he fears your boss. Figuring out what JavaScript loads asynchronously and what doesn’t can help you focus on where to enhance page performance.

<pre><code class="language-javascript">script[src]:not([async]) {
  display: block;
  width: 100%;
  height: 1em;
  background-color: red;
}
script:after {
  content: attr(src);
}
</code></pre>

### Javascript Event Elements

You can also highlight elements that have a JavaScript event attribute to refactor them into your JavaScript file. I’ve focused on the `OnMouseOver` attribute here, but it works for any of the JavaScript event attributes.

<pre><code class="language-javascript">[OnMouseOver] {
   color: burlywood;
}
[OnMouseOver]:after {
   content: "JS: " attr(OnMouseOver);
}
</code></pre>

### Hidden Items

If you need to see where your hidden elements or hidden inputs live you can show them with:

<pre><code class="language-bash">[hidden], [type="hidden"] {
  display: block;
}
</code></pre>

But with all these amazing capabilities you think there must be a catch. Surely attribute selectors must only work while flagged in Chrome or in the nightly builds of Fiery Foxes on the Edge of a Safari. This is just too good to be true. And, unfortunately, there is a catch. 

If you want to work with attribute selectors in that most beloved of browsers &mdash; that is, IE6 &mdash; you won’t be able to. (It’s okay; let the tears fall. No judgments.) Pretty much everywhere else you’re good to go. Attribute selectors are part of the CSS 2.1 spec and thus have been in browsers for the better part of a decade.

And so these selectors should no longer be magical to you but revealed as a sufficiently advanced technology. They are more science than magic, and now that you know their deepest secrets, it’s up to you. Go forth and work mystifying wonders of science upon the web.

{{< signature "dm, ra, yk, il" >}}
