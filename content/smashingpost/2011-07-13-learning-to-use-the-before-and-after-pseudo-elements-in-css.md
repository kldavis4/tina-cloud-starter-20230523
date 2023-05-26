---
title: 'Learning To Use The :after And :before Pseudo-Elements In CSS'
slug: learning-to-use-the-before-and-after-pseudo-elements-in-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d99ea41-5371-4573-8c33-8cabea756335/pseudo-element-icons.png
date: 2011-07-13T16:22:45.000Z
author: louis-lazaris
summary: >-
   So you have seen some cool things done with pseudo-elements but want to know what this CSS technique is all about before trying it yourself? Louis Lazaris has put together a run-down of pseudo-elements so you can have all of the concepts you need in order to create something practical with this technique.
description: >-
   In this article, Louis Lazaris puts together a fairly comprehensive run-down of pseudo-elements. Get all of the concepts you need in order to create something practical with this technique.
categories:
  - Coding
  - CSS
  - Techniques
  - Essentials
---

If you’ve been keeping tabs on various Web design blogs, you’ve probably noticed that the <code>:before</code> and <code>:after</code> pseudo-elements have been getting quite a bit of attention in the front-end development scene &mdash; and for good reason. In particular, the experiments of one blogger &mdash; namely, London-based developer <a href="https://nicolasgallagher.com/">Nicolas Gallagher</a> &mdash; have given pseudo-elements quite a bit of exposure of late. 

<figure><a href="https://nicolasgallagher.com/pure-css-gui-icons/demo/"><img loading="lazy" decoding="async"  class="alignnone" title="pseudo-element icons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d99ea41-5371-4573-8c33-8cabea756335/pseudo-element-icons.png" alt="after before Pseudo-Elements In CSS" width="500" height="334" /></a><figcaption>Nicolas Gallagher used pseudo-elements to create 84 GUI icons created from semantic HTML.</figcaption></figure>

To complement this exposure (and take advantage of a growing trend), I’ve put together what I hope is a fairly comprehensive run-down of pseudo-elements. This article is aimed primarily at those of you who have seen some of the <a href="https://nicolasgallagher.com/pure-css-gui-icons/">cool things</a> done with pseudo-elements but want to know what this CSS technique is all about before trying it yourself.

Although the CSS specification contains <a href="https://reference.sitepoint.com/css/pseudoelements">other pseudo-elements</a>, I’ll focus on <code>:before</code> and <code>:after</code>. So, for brevity, I’ll say “pseudo-elements” to refer generally to these particular two.

{{% feature-panel %}}

## What Does A Pseudo-Element Do?

A pseudo-element does exactly what the word implies. It creates a phoney element and inserts it before or after the content of the element that you’ve targeted.

The word “pseudo” is a <a href="https://en.wikipedia.org/wiki/Transliteration">transliteration</a> of a <a href="https://www.blueletterbible.org/lang/lexicon/Lexicon.cfm?Strongs=G5571">Greek word</a> that basically means “lying, deceitful, false.” So, calling them *pseudo*-elements is appropriate, because they don’t actually change anything in the document. Rather, they insert ghost-like elements that are visible to the user and that are style-able in the CSS.

## Basic Syntax

The <code>:before</code> and <code>:after</code> pseudo-elements are very easy to code (as are most CSS properties that don’t require a ton of vendor prefixes). Here is a simple example:

<pre><code class="language-css">#example:before {
   content: "#";
}

#example:after {
   content: ".";
}</code></pre>

There are two things to note about this example. First, we’re targeting the same element using <code>#example:before</code> and <code>#example:after</code>. Strictly speaking, they are the pseudo-elements in the code.

Secondly, without the <code>content</code> property, which is part of the <a href="https://www.w3.org/TR/css3-content/">generated content module</a> in the specification, pseudo-elements are useless. So, while the pseudo-element selector itself is needed to target the element, you won’t be able to insert anything without adding the <code>content</code> property.

In this example, the element with the id <code>example</code> will have a hash symbol placed “before” its content, and a period (or full stop) placed “after” its content.

### Some Notes On The Syntax

You could leave the <code>content</code> property empty and just treat the pseudo-element like a content-less box, like this:

<pre><code class="language-css">#example:before {
   content: "";
   display: block;
   width: 100px;
   height: 100px;
}</code></pre>

However, you can’t remove the <code>content</code> property altogether. If you did, the pseudo-element wouldn’t work. At the very least, the <code>content</code> property needs empty quotes as its value.

You may have noticed that you can also code pseudo-elements using the double-colon syntax (<code>::before</code> and <code>::after</code>), which I’ve <a href="https://www.impressivewebs.com/before-after-css3/">discussed before</a>. The short explanation is that there is no difference between the two syntaxes; it’s just a way to differentiate pseudo-elements (double colon) from pseudo-classes (single colon) in CSS3.

One final point regarding the syntax. Technically, you could implement a pseudo-element universally, without targeting any element, like this:

<pre><code class="language-css">:before {
   content: "#";
}</code></pre>

While the above is valid, it’s pretty useless. The code will insert a hash symbol before the content in each element in the DOM. Even if you removed the <code>&lt;body&gt;</code> tag and all of its content, you’d still see two hash symbols on the page: one in the <code>&lt;html&gt;</code> element, and one in the <code>&lt;body&gt;</code> tag, which the browser automatically constructs.

## Characteristics Of Inserted Content

As mentioned, the content that is inserted is not visible in the page’s source. It’s visible only in the CSS.

Also, the inserted element is by default an <a href="https://www.w3.org/TR/html401/struct/global.html#h-7.5.3">inline element</a> (or, in HTML5 terms, in the category of text-level semantics). So, to give the inserted element a height, padding, margins and so forth, you’ll usually have to define it explicitly as a block-level element.

This leads well into a brief description of how to style pseudo-elements. Look at this graphic from my text editor:

<figure><img loading="lazy" decoding="async"  title="Styling Elements" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1edde286-2f0d-4efa-a844-4973be86d135/styles-pseudo-elements.jpg" alt="screenshot" width="500" height="324" /><figcaption>Styling elements.</figcaption></figure>

In this example, I’ve highlighted the styles that will be applied to the elements inserted before and after the targeted element’s content. Pseudo-elements are somewhat unique in this way, because you insert the content *and* the styles in the same declaration block.

Also note that typical CSS inheritance rules apply to the inserted elements. If you had, for example, a font stack of <code>Helvetica, Arial, sans-serif</code> applied to the <code>&lt;body&gt;</code> element of the document, then the pseudo-element would inherit that font stack the same as any other element would.

Likewise, pseudo-elements don’t inherit styles that aren’t naturally inherited from parent elements (such as padding and margins).

{{% ad-panel-leaderboard %}}

## After Before What?

Your hunch on seeing the <code>:before</code> and <code>:after</code> pseudo-elements might be that the inserted content will be injected before and after the targeted element. But, as alluded to above, that’s not the case.

The content that’s injected will be child content in relation to the targeted element, but it will be placed “before” or “after” any other content in that element.

To demonstrate this, look at the following code. First, the HTML:

<pre><code class="language-markup tmp-html">&lt;p class="box"&gt;Other content.&lt;/p&gt;</code></pre>

And here’s the CSS that inserts a pseudo-element:

<pre><code class="language-css">p.box {
   width: 300px;
   border: solid 1px white;
   padding: 20px;
}

p.box:before {
   content: "#";
   border: solid 1px white;
   padding: 2px;
   margin: 0 10px 0 0;
}</code></pre>

In the HTML, all you would see is a paragraph with a class of <code>box</code>, with the words “Other content” inside it (the same as what you would see if you viewed the source on the live page). In the CSS, the paragraph is given a set width, along with some padding and a visible border.

Then we have the pseudo-element. In this case, it’s a hash symbol inserted “before” the paragraph’s content. The subsequent CSS gives it a border, along with some padding and margins.

Here’s the result viewed in the browser:

<figure><img loading="lazy" decoding="async"  title="Placement of the pseudo-element" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6af3d58-2528-4a00-a208-8b2804415e13/4589454789.jpg" alt="screenshot" width="500" height="175" /><figcaption>Placement of the pseudo-element.</figcaption></figure>

The outer box is the paragraph. The border around the hash symbol denotes the boundary of the pseudo-element. So, instead of being inserted “before” the paragraph, the pseudo-element is placed before the “Other content” in the paragraph.

## Inserting Non-Text Content

I mentioned briefly that you can leave the <code>content</code> property’s value as an empty string or insert text content. You basically have two additional options of what to include as the value of the <code>content</code> property.

First, you can include a URL that points to an image, just as you would do when including a background image in the CSS:

<pre><code class="language-css">p:before {
   content: url(image.jpg);
}</code></pre>

Notice that the quotes are missing. If you wrapped the URL reference in quotes, then it would become a literal string and insert the text “url(image.jpg)” as the content, instead of inserting the image itself.

Naturally, you could include a <a href="https://css-tricks.com/data-uris/">Data URI</a> in place of the image reference, just as you can with a CSS background.

You also have the option to include a function in the form of <code>attr(X)</code>. This function, <a href="https://www.w3.org/TR/CSS2/generate.html#propdef-content">according to the spec</a>, “returns as a string the value of attribute X for the subject of the selector.”

Here’s an example:

<pre><code class="language-css">a:after {
   content: attr(href);
}</code></pre>

What does the <code>attr()</code> function do? It takes the value of the specified attribute and places it as text content to be inserted as a pseudo-element.

The code above would cause the <code>href</code> value of every <code>&lt;a&gt;</code> element on the page to be placed immediately after each respective <code>&lt;a&gt;</code> element. This could be used in a <a href="https://www.smashingmagazine.com/2015/01/designing-for-print-with-css/">print style sheet</a> to include full URLs next to all links when a document is printed.

You could also use this function to grab the value of an element’s <code>title</code> attribute, or even <a href="https://en.wikipedia.org/wiki/Microdata_(HTML5)">microdata</a> values. Of course, not all of these examples would be practical in and of themselves; but depending on the situation, a specific attribute value could be practical as a pseudo-element.

While being able to grab the <code>title</code> or <code>alt</code> text of an image and display it on the page as a pseudo-element would be practical, this isn’t possible. Remember that the pseudo-element must be a child of the element to which it is being applied. Images, which are <a href="https://www.w3.org/TR/html-markup/syntax.html#syntax-elements">void</a> (or empty) elements, don’t have child elements, so it wouldn’t work in this case. The same would apply to other void elements, such as <code>&lt;input&gt;</code>.

## Dreaded Browser Support

As with any front-end technology that is gaining momentum, one of the first concerns is browser support. In this case, that’s not as much of a problem.

Browser support for <code>:before</code> and <code>:after</code> pseudo-elements stacks up like this:

*   Chrome 2+,
*   Firefox 3.5+ (3.0 had partial support),
*   Safari 1.3+,
*   Opera 9.2+,
*   IE8+ (with some minor bugs),
*   Pretty much all mobile browsers.

The only real problem (no surprise) is IE6 and IE7, which have no support. So, if your audience is in the Web development niche (or another market that has low IE numbers), you can probably go ahead and use pseudo-elements freely.

### Pseudo-Elements Aren’t Critical

Fortunately, a lack of pseudo-elements will not cause huge usability issues. For the most part, pseudo-elements are generally decorative (or helper-like) content that will not cause problems in unsupported browsers. So, even if your audience has high IE numbers, you can still use them to some degree.

## A Couple Of Reminders

As mentioned, pseudo-element content does not appear in the DOM. These elements are not real elements. As such, they are <a href="https://cssgallery.info/testing-the-accessibility-of-the-css-generated-content/">not accessible to most assistive devices</a>. So, never use pseudo-elements to generate content that is critical to the usability or accessibility of your pages.

Another thing to keep in mind is that developer tools such as Firebug <a href="https://meyerweb.com/eric/thoughts/2009/11/03/pseudo-phantoms/">do not show the content generated by pseudo-elements</a>. So, if overused, pseudo-elements could cause maintainability headaches and make debugging a much slower process.

**Update:** As mentioned in the comments, you can use Chrome’s developer tools to view the styles associated with a pseudo-element, but the element will not appear in the DOM. Also, <a href="https://getfirebug.com/wiki/index.php/Firebug_Release_Notes#CSS">Firebug is adding pseudo-element support</a> in version 1.8.

That covers all of the concepts you need in order to create something practical with this technique. In the meantime, for further reading on CSS pseudo-elements, be sure to check out some of the articles that we’ve linked to in this piece.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [A Guide To CSS Pseudo-Classes And Pseudo-Elements](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
*   [Taming Advanced CSS Selectors](https://www.smashingmagazine.com/2009/08/taming-advanced-css-selectors/)
*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)
*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/)

{{< signature "kw, mrn" >}}
