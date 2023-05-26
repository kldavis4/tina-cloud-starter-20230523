---
title: An Ultimate Guide To CSS Pseudo Classes And Pseudo Elements
slug: an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20244df4-8e57-4bb1-8abe-ef4319b21662/pseudo-classes-pseudo-elements-opt.jpg
date: 2016-05-03T15:52:48.000Z
author: ricardozea
summary: >-
  CSS pseudo-classes and pseudo-elements can certainly be a handful. They provide so many possibilities that one can easily feel overwhelmed, but that’s the life of a web designer and developer! This guide will help you to learn about all the things you need to keep in mind so that your pseudo-classes and pseudo-elements are well implemented.
description: >-
  CSS pseudo-classes and pseudo-elements can certainly be a handful. This guide will help you to learn about all the things you need to keep in mind.
categories:
  - Coding
  - CSS
  - Responsive Design
---

Hola a todos! (_Hello, everyone!_)

In my early days of web design, I had to learn things the hard way: **trial and error**. There was no _Smashing Magazine_, _Can I Use_, _CodePen_ or any of the other amazing tools at our disposal today. Having someone show me the ropes of web design, especially on the CSS front, would have been incredibly helpful.

Now that I am far more experienced, I want to share with you in a very friendly, casual, non-dogmatic way a CSS reference guide to pseudo-classes and pseudo-elements.

If you’re an experienced web designer or developer, you must know and have used most of the pseudo-classes and pseudo-elements discussed here. However, I encourage you to check the [table of contents](#table-of-contents-in-alphabetical-order); you might not have heard of one or two of them before.

Before diving into the meat and bones, and because this article is about pseudo-classes and pseudo-elements, let’s start with the basics: Have you ever wondered what the word “pseudo” means? If so, here’s a [definition from Dictionary.com](https://dictionary.reference.com/browse/pseudo):

<blockquote>adjective<br /><br />1. not actually but having the appearance of; pretended; false or spurious; sham.<br /><br />2. almost, approaching, or trying to be.</blockquote>

Without getting overcomplicated with the W3C’s technical definition, a pseudo-class is basically a phantom state or specific characteristic of an element that can be targeted with CSS. A few common pseudo-classes are `:link`, `:visited`, `:hover`, `:active`, `:first-child` and `:nth-child`. There are more, and we’re going to see them all in a minute.

Also, pseudo-classes are always preceded by a colon (`:`). Then comes the name of the pseudo-class and sometimes a value in parentheses. `:nth-child` anyone?

Now, pseudo-elements are like virtual elements that we can treat as regular HTML elements. The thing is that they don’t exist in the document tree or DOM. This means we don’t actually type the pseudo-elements, but rather create them with CSS.

A few common pseudo-elements are `:after`, `:before` and `:first-letter`. We’ll talk about them towards the end of this article.

{{% feature-panel %}}

## Single Or Double Colon For Pseudo-Elements?

The short answer is, in most cases, either.

The double colon (`::`) was introduced in [CSS3](https://www.smashingmagazine.com/learning-css3-useful-reference-guide/) to differentiate pseudo-elements such as `::before` and `::after` from pseudo-classes such as `:hover` and `:active`. All browsers support double colons for pseudo-elements except Internet Explorer (IE) 8 and below.

Some pseudo-elements, such as `::backdrop`, accept only a double colon, though.

Personally, I use single-colon notation so that my CSS is backwards-compatible with legacy browsers. I use double-colon notation on those pseudo-elements that require it, of course.

You are free to use either; there is really no right or wrong about this.

However, the specification, at the time of writing this article, does [recommend using single-colon notation](https://www.w3.org/community/webed/wiki/Advanced_CSS_selectors#CSS3_pseudo-element_double_colon_syntax) for the reason mentioned above, backwards compatibility:

<blockquote>Please note that the new CSS3 way of writing pseudo-elements is to use a double colon, eg <code>a::after { … }</code>, to set them apart from pseudo-classes. You may see this sometimes in CSS. CSS3 however also still allows for single colon pseudo-elements, for the sake of backwards compatibility, and we would advise that you stick with this syntax for the time being.</blockquote>

In the headings in this article, pseudo-elements that support both a single and double colon will be shown with both notations. Pseudo-elements that support only a double colon will be shown as is.

## When (Not) To Use CSS Generated Content

Generating content via CSS is achieved by combining the `content` CSS property with the `:before` or `:after` pseudo-element.

This “content” may be either plain text or a container that we manipulate with CSS to display a [graphic shape or decorative element](https://codepen.io/ricardozea/pen/sdlvu). Here, I’ll be referring to the first type of content, text.

Generated content shouldn’t be used for important copy or text, due to the following reasons:

*   It won’t be accessible to some screen readers.
*   It won’t be selectable.
*   If generated content uses superfluous content for the sake of decoration, [screen readers](https://www.smashingmagazine.com/2014/05/mobile-accessibility-why-care-what-can-you-do/) that do support CSS generated content will read it out loud, thus making the UX even worse.

Use CSS generated content for decoration and non-vital information, but make sure it’s properly handled by screen readers, so that people with assistive technology are not distracted. Think “progressive enhancement” when deciding whether to use CSS generated content.

Here on Smashing Magazine, Gabriele Romanato has an awesome article about [using CSS generated content](https://www.smashingmagazine.com/2013/04/css-generated-content-counters/).

{{% ad-panel-leaderboard %}}

## Experimental Pseudo-Classes And Pseudo-Elements

A pseudo-class or pseudo-element that is experimental means that its specification is not stable or finalized. The syntax and behavior could change down the road.

However, we might be able to use experimental pseudo-classes and pseudo-elements now by applying vendor prefixes. To do this, refer to [Can I Use](https://caniuse.com/); and some kind of auto-prefixing tool, such as [-prefix-free](https://www.smashingmagazine.com/2011/10/prefixfree-break-free-from-css-prefix-hell/) or [Autoprefixer](https://autoprefixer.github.io/), is a must.

In this article, you will see an “experimental” label next to a relevant pseudo-class or pseudo-element’s name.

<div class="toc-ctnr">

### Table of Contents (in alphabetical order)
<div id="toc">

<ul>
<li class="toc-h4"><a href="#active">:active</a></li>
<li class="toc-h4"><a href="#afterafter">::after/:after</a></li>
<li class="toc-h4"><a href="#backdrop-experimental">::backdrop (experimental)</a></li>
<li class="toc-h4"><a href="#beforebefore">::before/:before</a></li>
<li class="toc-h4"><a href="#checked">:checked</a></li>
<li class="toc-h4"><a href="#default">:default</a></li>
<li class="toc-h4"><a href="#dir-experimental">:dir (experimental)</a></li>
<li class="toc-h4"><a href="#disabled">:disabled</a></li>
<li class="toc-h4"><a href="#empty">:empty</a></li>
<li class="toc-h4"><a href="#enabled">:enabled</a></li>
<li class="toc-h4"><a href="#first-child">:first-child</a></li>
<li class="toc-h4"><a href="#first-letterfirst-letter">::first-letter/:first-letter</a></li>
<li class="toc-h4"><a href="#first-linefirst-line">::first-line/:first-line</a></li>
<li class="toc-h4"><a href="#first-of-type">:first-of-type</a></li>
<li class="toc-h4"><a href="#focus">:focus</a></li>
<li class="toc-h4"><a href="#fullscreen-experimental">:fullscreen (experimental)</a></li>
<li class="toc-h4"><a href="#hover">:hover</a></li>
<li class="toc-h4"><a href="#in-range">:in-range</a></li>
<li class="toc-h4"><a href="#indeterminate">:indeterminate</a></li>
<li class="toc-h4"><a href="#invalid">:invalid</a></li>
<li class="toc-h4"><a href="#lang">:lang</a></li>
<li class="toc-h4"><a href="#last-child">:last-child</a></li>
<li class="toc-h4"><a href="#last-of-type">:last-of-type</a></li>
<li class="toc-h4 toc-active"><a href="#link">:link</a></li>
<li class="toc-h4"><a href="#not">:not</a></li>
<li class="toc-h4"><a href="#nth-child">:nth-child</a></li>
<li class="toc-h4"><a href="#nth-last-child">:nth-last-child</a></li>
<li class="toc-h4"><a href="#nth-last-of-type">:nth-last-of-type</a></li>
<li class="toc-h4"><a href="#nth-of-type">:nth-of-type</a></li>
<li class="toc-h4"><a href="#only-child">:only-child</a></li>
<li class="toc-h4"><a href="#only-of-type">:only-of-type</a></li>
<li class="toc-h4"><a href="#optional">:optional</a></li>
<li class="toc-h4"><a href="#out-of-range">:out-of-range</a></li>
<li class="toc-h4"><a href="#placeholder-experimental">::placeholder (experimental)</a></li>
<li class="toc-h4"><a href="#read-only">:read-only</a></li>
<li class="toc-h4"><a href="#read-write">:read-write</a></li>
<li class="toc-h4"><a href="#required">:required</a></li>
<li class="toc-h4"><a href="#root">:root</a></li>
<li class="toc-h4"><a href="#selection">::selection</a></li>
<li class="toc-h4"><a href="#scope-experimental">:scope (experimental)</a></li>
<li class="toc-h4"><a href="#target">:target</a></li>
<li class="toc-h4"><a href="#valid">:valid</a></li>
<li class="toc-h4"><a href="#visited">:visited</a></li>
<li class="toc-h4"><a href="#bonus-content-a-sass-mixin-for-links">Bonus content: A Sass mixin for links</a></li>
</ul>
</div>
</div>

All right, everyone, let’s get this show started!

## Pseudo-Classes

We’ll begin our discussion of pseudo-classes with those relating to states.

## States

A state pseudo-class usually come into play when the user performs an action. An “action” in CSS could also be “no action”, as in the case of a link that hasn’t been visited yet.

Let’s check them out.

### :link

The `:link` pseudo-class represents the “normal” state of links and is used to select links that have not yet been visited. Declaring the `:link` pseudo-class before all other pseudo-classes in this category is recommended. The order of all four is this: `:link`, `:visited`, `:hover`, `:active`

<pre><code class="language-css">a:link {
    color: orange;
}
</code></pre>

If you use it as follows, it can be omitted:

<pre><code class="language-css">a {
    color: orange;
}
</code></pre>

### :visited

The `:visited` pseudo-class is used in links that have been visited. Position `:visited` pseudo-class second in order (after the `:link` pseudo-class).

<pre><code class="language-css">a:visited {
    color: blue;
}
</code></pre>

### :hover

The `:hover` pseudo-class is used to style an element when the user’s pointer is above it. It doesn’t have to be restricted to links, although that is the most common use case.

It should appear third in order (after the `:visited` pseudo-class).

<pre><code class="language-css">a:hover {
    color: orange;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="vGEzJK" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/vGEzJK/">CSS :hover pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :active

The `:active` pseudo-class is used to style an element that has been “activated” either by a pointing device or by a tap on a touchscreen device. It can also be triggered by the keyboard, just like the `:focus` pseudo-class.

It works very similarly to `:focus`, the difference being that the `:active` pseudo-class is an event that occurs between the mouse button being clicked and being released.

It should appear fourth in order (after the `:hover` pseudo-class).

<pre><code class="language-css">a:active {
    color: rebeccapurple;
}
</code></pre>

### :focus

The `:focus` pseudo-class is used to style an element that has gained focus via a pointing device, from a tap on a touchscreen device or via the keyboard. It’s used a lot in form elements.

<pre><code class="language-css">a:focus {
    color: green;
}
</code></pre>

Or:

<pre><code class="language-css">input:focus {
    background: #eee;
}
</code></pre>

### Bonus Content: A Sass Mixin for Links

If you work with CSS preprocessors, such as Sass, this bonus content might interest you.

(If you’re not into CSS preprocessors — and that’s OK — you can skip to the section on [structural pseudo-classes](#structural).)

In the spirit of optimizing our workflow, below is a Sass mixin that we can use to create a basic set of links.

The idea behind this mixin is that no defaults are declared in the arguments. So, we are “forced,” in a friendly way, to declare all four states of our links.

The `:focus` and `:active` pseudo-classes are usually declared together. Feel free to separate them if you prefer.

Note that this mixin can be applied to any HTML element, not just links.

Here is our mixin:

<pre><code class="language-sass">@mixin links ($link, $visited, $hover, $active) {
    &amp; {
        color: $link;
        &amp;:visited {
            color: $visited;
        }
        &amp;:hover {
            color: $hover;
        }
        &amp;:active, &amp;:focus {
            color: $active;
        }
    }
}
</code></pre>

**Usage:**

<pre><code class="language-sass">a {
    @include links(orange, blue, yellow, teal);
}
</code></pre>

**Compiles to:**

<pre><code class="language-css">a {
  color: orange;
}
a:visited {
  color: blue;
}
a:hover {
  color: yellow;
}
a:active, a:focus {
  color: teal;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="wMyZQe" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/wMyZQe/">Sass Mixin for Links</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Structural

Structural pseudo-classes target additional information in the document tree or DOM and cannot be represented by another type of selectors or combinators.

### :first-child

The `:first-child` pseudo-class represents the first child of its parent element.

In the following example, the first `li` element will be the only one with orange text.

**HTML:**

<pre><code class="language-markup">
&lt;ul&gt;
    <strong>&lt;li&gt;This text will be orange.&lt;/li&gt;</strong>
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">li:first-child {
    color: orange;
}
</code></pre>

### :first-of-type

The `:first-of-type` pseudo-class represents the first element of its kind in its parent container.

In the following example, the first `li` element and the first `span` element will be the only ones with orange text.

**HTML:**

<div class="break-out">

 <pre><code class="language-markup">
&lt;ul&gt;
   <strong> &lt;li&gt;This text will be orange.&lt;/li&gt;</strong>
    &lt;li&gt;Lorem ipsum dolor sit amet. <strong>&lt;span&gt;This text will be orange.&lt;/span&gt;</strong>&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
&lt;/ul&gt;
</code></pre>
</div>

**CSS:**

<pre><code class="language-css">ul :first-of-type {
    color: orange;
}
</code></pre>

### :last-child

The `:last-child` pseudo-class represents the last child element in its parent container.

In the following example, the last `li` element will be the only one with orange text.

**HTML:**

<pre><code class="language-markup">
&lt;ul&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    <strong>&lt;li&gt;This text will be orange.&lt;/li&gt;</strong>
&lt;/ul&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">li:last-child {
    color: orange;
}
</code></pre>

### :last-of-type

The `:last-of-type` pseudo-class represents the last element of its kind in its parent container.

In the following example, the last `li` and the last `span` elements will be the only ones with orange text.

**HTML:**

<div class="break-out">

 <pre><code class="language-markup">
&lt;ul&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet. &lt;span&gt;Lorem ipsum dolor sit amet.&lt;/span&gt; <strong>&lt;span&gt;This text will be orange.&lt;/span&gt;</strong>&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    <strong>&lt;li&gt;This text will be orange.&lt;/li&gt;</strong>
&lt;/ul&gt;
</code></pre>
</div>

**CSS:**

<pre><code class="language-css">ul :last-of-type {
    color: orange;
}
</code></pre>

### :not

The `:not` pseudo-class is also known as the negation pseudo-class. It accepts an argument — basically, another “selector” — inside parentheses. The argument can actually be another pseudo-class.

It may be chained but may not contain another `:not` selector.

In the following example, the `:not` pseudo-class matches an element that is not represented by the argument.

**HTML:**

<pre><code class="language-markup">&lt;ul&gt;
    &lt;li class="first-item"&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

**CSS:**

In the following, all text is orange, except the `li` element with the class of `.first-item`:

<pre><code class="language-css">li:not(.first-item) {
    color: orange;
}
</code></pre>

Now, we’re going to **chain** two `:not` pseudo-classes. All elements will have black text and a yellow background, except the `li` element with the class `.first-item` and the last `li` element in the list:

<pre><code class="language-css">li:not(.first-item):not(:last-of-type) {
    background: yellow;
    color: black;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="dGmqbg" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/dGmqbg/">CSS :not pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :nth-child

The `:nth-child` pseudo-class targets one or more elements depending on their order in the markup.

This pseudo-class is one of the most versatile and robust pseudo-classes in CSS.

All of the `:nth` pseudo-classes take an argument, which is a formula that we type in parentheses. The formula may be a single integer, a formula structured as `an+b` or the keyword `odd` or `even`.

In the `an+b` formula:

*   the `a` is a number (called an integer);
*   the `n` is a literal `n` (in other words, we will actually type the letter `n` in the formula);
*   the `+` is an operator that may be either a plus sign (`+`) or a minus sign (`-`);
*   the `b` is an integer as well but is only required if an operator is being used.

Using the Greek alphabet, here are a few examples using the following basic HTML structure:

<pre><code class="language-markup">&lt;ol&gt;
    &lt;li&gt;Alpha&lt;/li&gt;
    &lt;li&gt;Beta&lt;/li&gt;
    &lt;li&gt;Gamma&lt;/li&gt;
    &lt;li&gt;Delta&lt;/li&gt;
    &lt;li&gt;Epsilon&lt;/li&gt;
    &lt;li&gt;Zeta&lt;/li&gt;
    &lt;li&gt;Eta&lt;/li&gt;
    &lt;li&gt;Theta&lt;/li&gt;
    &lt;li&gt;Iota&lt;/li&gt;
    &lt;li&gt;Kappa&lt;/li&gt;
&lt;/ol&gt;
</code></pre>

**CSS:**

Let’s select the second child. So, only “Beta” will be orange:

<pre><code class="language-css">ol :nth-child(2) {
    color: orange;
}
</code></pre>

Now, let’s select every other child starting from the second. So, “Beta,” “Delta,” “Zeta,” “Theta” and “Kappa” will be orange:

<pre><code class="language-css">ol :nth-child(2n) {
    color: orange;
}
</code></pre>

Let’s select all even-numbered children:

<pre><code class="language-css">ol :nth-child(even) {
    color: orange;
}
</code></pre>

Let’s select every other child, starting from the sixth. So, “Zeta,” “Theta” and “Kappa” will be orange:

<pre><code class="language-css">ol :nth-child(2n+6) {
    color: orange;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="adYaER" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/adYaER/">CSS :nth-child pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :nth-last-child

The `:nth-last-child` pseudo-class basically works the same as `:nth-child` except that it selects elements starting from the end, rather than the beginning.

**CSS:**

Let’s select the second child, starting from the end. So, only “Iota” will be orange:

<pre><code class="language-css">ol :nth-last-child(2) {
    color: orange;
}
</code></pre>

Now, let’s select every other child, starting with the second from the end. So, “Iota,” “Eta,” “Epsilon,” “Gamma” and “Alpha” will be orange:

<pre><code class="language-css">ol :nth-last-child(2n) {
    color: orange;
}
</code></pre>

Let’s select all even children, starting from the end:

<pre><code class="language-css">ol :nth-last-child(even) {
    color: orange;
}
</code></pre>

Let’s select every other child, starting with the sixth element from the end. So, “Epsilon,” “Gamma” and “Alpha” will be orange:

<pre><code class="language-css">ol :nth-last-child(2n+6) {
    color: orange;
}
</code></pre>

### :nth-of-type

The `:nth-of-type` pseudo-class works basically the same as `:nth-child`, the main difference being that it’s more specific because we’re targeting a specific element relative to like elements contained within the same parent element.

In the following example, all second paragraphs in any given container will be orange.

**HTML:**

<pre><code class="language-markup">
&lt;article&gt;
    &lt;h1&gt;Heading Goes Here&lt;/h1&gt;
    &lt;p&gt;Lorem ipsum dolor sit amet.&lt;/p&gt;
    &lt;a href=""&gt;&lt;img src="images/rwd.png" alt="Mastering RWD"&gt;&lt;/a&gt;
    <strong>&lt;p&gt;This text will be orange.&lt;/p&gt;</strong>
&lt;/article&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">p:nth-of-type(2) {
    color: orange;
}
</code></pre>

### :nth-last-of-type

The `:nth-last-of-type` pseudo-class works the same as `:nth-of-type`, the difference being that it starts counting from the end of the list, rather than the beginning.

In the following example, because we’re starting from the bottom, all first paragraphs will be orange.

**HTML:**

<pre><code class="language-markup">
&lt;/article&gt;
    &lt;/h1&gt;Heading Goes Here&lt;/article&gt;/h1&gt;
    <strong>&lt;/p&gt;This text will be orange.&lt;/p&gt;</strong>
    &lt;/a href="#"&gt;&lt;img src="images/rwd.png" alt="Mastering RWD"&gt;&lt;/a&gt;
    &lt;/p&gt;Lorem ipsum dolor sit amet.&lt;/p&gt;
&lt;/article&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">p:nth-last-of-type(2) {
    color: orange;
}
</code></pre>

[](#resources-for-nth)**Resources**

Refer to these two great resources when working with the `:nth` pseudo-classes:

*   “[CSS3 Structural Pseudo-Class Selector Tester](https://lea.verou.me/demos/nth.html),” Lea Verou
*   “[:nth Tester](https://css-tricks.com/examples/nth-child-tester/),” CSS-Tricks

### :only-child

The `:only-child` pseudo-class targets the only child of a parent element.

In the following example, the first `ul` element has a single child, which will be given orange text. The second `ul` element has several children; therefore, its children won’t be affected by the `:only-child` pseudo-class.

**HTML:**

<pre><code class="language-markup">
&lt;ul&gt;
    <strong>&lt;li&gt;This text will be orange.&lt;/li&gt;</strong>
&lt;/ul&gt;

&lt;ul&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">ul :only-child {
    color: orange;
}
</code></pre>

### :only-of-type

The `:only-of-type` pseudo-class targets an element that has no siblings of that particular type. This is similar to `:only-child` except that we can target a specific element and make the selector more meaningful.

In the following example, the first `ul` has a single child, which will be given orange text.

**HTML:**

<pre><code class="language-markup">
&lt;ul&gt;
    <strong>&lt;li&gt;This text will be orange.&lt;/li&gt;</strong>
&lt;/ul&gt;

&lt;ul&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
    &lt;li&gt;Lorem ipsum dolor sit amet.&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">li:only-of-type {
    color: orange;
}
</code></pre>

### :target

The `:target` pseudo-class… well, targets the unique ID of an element and the hash in the URL.

In the following example, the article with the ID of `target` will be targeted when the URL in the browser ends with `#target`.

**URL:**

`https://awesomebook.com/#target`

**HTML:**

<pre><code class="language-markup">&lt;article id="target"&gt;
    &lt;h1&gt;&lt;code&gt;:target&lt;/code&gt; pseudo-class&lt;/h1&gt;
    &lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipisicing elit!&lt;/p&gt;
&lt;/article&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">:target {
    background: yellow;
}
</code></pre>

**Tip:** You can use the `background:` shorthand instead of `background-color:` to achieve the same result.

## Validation

Forms have always been the bane of web design and development. With the help of validation pseudo-classes, we can make the process of filling out forms a smoother and more pleasant experience.

Note, however, that although most of the pseudo-classes listed in this section work well with form elements, some pseudo-classes can be used with other HTML elements, too.

Let’s check out these pseudo-classes!

### :checked

The `:checked` pseudo-class targets radio buttons, checkboxes and option elements that have been checked or selected.

In the following example, when the checkbox is selected, the label is highlighted, thus enhancing the user experience.

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="wMYExY" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/wMYExY/">CSS :checked pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :default

The `:default` pseudo-class targets the default element in a form among a group of similar elements.

In case you need to target the default button in a form that does not have a class, you can use the `:default` pseudo-class.

Note that providing a “Reset” or “Clear” button in a form comes with some serious **usability issues**. Avoid using it unless absolutely necessary. The following articles explain some reasons why:

*   “[Reset and Cancel Buttons](https://www.nngroup.com/articles/reset-and-cancel-buttons/),” Nielsen Norman Group (2000)
*   “[Killing the Cancel Button on Forms for Good](https://uxmovement.com/forms/killing-the-cancel-button-on-forms-for-good/),” UX Movement (2010)

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="WrzJKO" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/WrzJKO/">CSS :default pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :disabled

The `:disabled` pseudo-class targets a form element in the disabled state. An element in a disabled state can’t be selected, checked or activated or gain focus.

In the following example, the input for the `name` field is disabled, so it will be shown as 50% transparent.

**HTML:**

<pre><code class="language-markup">&lt;input type="text" id="name" disabled&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">:disabled {
    opacity: .5;
}
</code></pre>

**Tip:** Using `disabled="disabled"` in the markup isn’t required. You can accomplish the same result using only the attribute `disabled`. Keep in mind, though, that using `disabled="disabled"` is required in XHTML.

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="NxOLZm" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/NxOLZm/">CSS :disabled pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :empty

The `:empty` pseudo-class targets elements that have no content in them of any kind at all. If an element has a letter, another HTML element or even a space, then that element would not be empty.

Here is what is considered empty and not empty:

*   **Empty**  
    No content or characters would appear in an element. An HTML comment inside an element does not count as content in this case.
*   **Not empty**  
    Characters would appear inside the element. Even a space would be considered content.

In the following example:

*   the top container has text, so it will have an orange background;
*   the second container has a space, which is considered content, so it will have an orange background as well;
*   the third container has nothing in it (it’s empty), so it will have a yellow background;
*   the last container has only an HTML comment (it’s empty, too), so it will have a yellow background as well.

**HTML:**

<pre><code class="language-markup">&lt;div&gt;This box is orange&lt;/div&gt;
&lt;div&gt; &lt;/div&gt;
&lt;div&gt;&lt;/div&gt;
&lt;div&gt;&lt;!-- This comment is not considered content --&gt;&lt;/div&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">div {
  background: orange;
  height: 30px;
  width: 200px;
}

div:empty {
  background: yellow;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="rxqqaM" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/rxqqaM/">CSS :empty pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :enabled

The `:enabled` pseudo-class targets elements that are enabled. All form elements are enabled by default — that is, until we add the `disabled` attribute to the element in the markup.

We can use a combination of `:enabled` and `:disabled` to provide visual feedback, thus improving the user experience.

In the following example, after having been disabled, the input for `name` is enabled and so is given an opacity value of `1` and a 1-pixel green border:

<pre><code class="language-css">:enabled {
    opacity: 1;
    border: 1px solid green;
}
</code></pre>

**Tip:** Using `enabled="enabled"` in the markup isn’t required. You can accomplish the same result using only the `enabled` attribute. Keep in mind, though, that `enabled="enabled"` is required in XHTML.

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="zqYQxq" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/zqYQxq/">CSS :enabled pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### <span class="headeranchor"></span>:in-range

The `:in-range` pseudo-class targets elements that have a range and whose values are within the defined range.

In the following example, the input element supports a range between 5 and 10\. Values within this range will trigger a green border.

**HTML:**

<pre><code class="language-markup">&lt;input type="number" min="5" max="10"&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">input[type=number] {
    border: 5px solid orange;
}

input[type=number]:in-range {
    border: 5px solid green;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="XXOKwq" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/XXOKwq/">CSS :in-range and :out-of-range pseudo-classes</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :out-of-range

The :out-of-range pseudo-class targets elements that have a range and whose values fall outside of the defined range.

In the following example, the input element supports a range between 1 and 12\. Values outside of this range will trigger an orange border.

**HTML:**

<pre><code class="language-markup">&lt;input id="months" name="months" type="number" min="1" max="12"&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">input[type=number]:out-of-range {
    border: 1px solid orange;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="XXOKwq" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/XXOKwq/">CSS :in-range and :out-of-range pseudo-classes</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :indeterminate

The `:indeterminate` pseudo-class targets input elements such as radio buttons and check boxes that are not selected or that are unselected upon the page loading.

An example of this is when a page loads with a group of radio buttons and no default or preselected radio button has been set, or when a checkbox has been given the `indeterminate` state via JavaScript.

**HTML:**

<pre><code class="language-markup">&lt;ul&gt;
    &lt;li&gt;
        &lt;input type="radio" name="list" id="option1"&gt;
        &lt;label for="option1"&gt;Option 1&lt;/label&gt;
    &lt;/li&gt;
    &lt;li&gt;
        &lt;input type="radio" name="list" id="option2"&gt;
        &lt;label for="option2"&gt;Option 2&lt;/label&gt;
    &lt;/li&gt;
    &lt;li&gt;
        &lt;input type="radio" name="list" id="option3"&gt;
        &lt;label for="option3"&gt;Option 3&lt;/label&gt;
    &lt;/li&gt;
&lt;/ul&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">:indeterminate + label {
    background: orange;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="adXpQK" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/adXpQK/">CSS :indeterminate pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :valid

The `:valid` pseudo-class targets a form element whose formatting is correct according to that element’s required format.

In the following example, the `email` input field has a correctly formatted email structure; so, the field would be considered valid and would appear with a 1-pixel green border:

<pre><code class="language-css">input[type=email]:valid {
    border: 1px solid green;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="bEzqVg" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/bEzqVg/">CSS :valid and :invalid pseudo-classes</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :invalid

The `:invalid` pseudo-class targets a form element whose formatting is not correct according to that element’s required format.

In the following example, when the `email` input field has an incorrectly formatted email structure, the value would be considered invalid, and so an orange border would appear around the field:

<pre><code class="language-css">input[type=email]:invalid {
    background: orange;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="bEzqVg" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/bEzqVg/">CSS :valid and :invalid pseudo-classes</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :optional

The `:optional` pseudo-class targets input fields that are not required in a form. In other words, as long as an input doesn’t have the `required` attribute, it can be targeted with the `:optional` pseudo-class.

In the following example, the field is optional. It doesn’t have the `required` attribute, so the text will appear gray.

**HTML:**

<pre><code class="language-markup">&lt;input type="number"&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">:optional {
    color: gray;
}
</code></pre>

### :read-only

The `:read-only` pseudo-class targets an element that cannot be edited by the user. It’s similar to the `:disabled` pseudo-class; the attribute used in the markup would determine which pseudo-class we should use.

This would be useful, for example, in a form where we need to show pre-populated information that cannot be altered but that still needs to be displayed within the `form` element for submission purposes.

In the following example, the input element has a `readonly` HTML attribute. So, it can be targeted with the `:read-only` pseudo-class, which we will use to give it gray text.

**HTML:**

<pre><code class="language-markup">&lt;input type="text" value="I am read only" readonly&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">input:read-only {
    color: gray;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="Nxopbj" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/Nxopbj/">CSS :read-only pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :read-write

The `:read-write` pseudo-class targets elements that can be edited by the user. It can work on elements that have the `contenteditable` HTML attribute as well.

This pseudo-class can be combined with the `:focus` pseudo-class to enhance the UX in certain situations.

In the following example, the user would be able to edit the div by clicking on it. We could enhance the user experience by applying a particular style that differentiates this piece of content from the rest, providing a visual cue to the user that this content can be edited.

**HTML:**

<pre><code class="language-markup">&lt;div class="editable" contenteditable&gt;
    &lt;h1&gt;Click on this text to edit it&lt;/h1&gt;
    &lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipisicing elit!&lt;/p&gt;
&lt;/div&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">:read-write:focus {
    padding: 5px;
    border: 1px dotted black;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="LGqWxK" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/LGqWxK/">CSS :read-write pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :required

The `:required` pseudo-class targets input elements that have the `required` HTML attribute.

In addition to relying on the traditional asterisk (*) on an input element’s label to denote that it is required, we could also style the field with CSS. Basically, we get the best of both worlds.

In the following example, the input field has the `required` HTML attribute. We can enhance the UX by applying a particular style that gives a visual cue that the field is… well, required.

**HTML:**

<pre><code class="language-markup">&lt;input type="email" required&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">:required {
    color: black;
    font-weight: bold;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="KVJWmZ" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/KVJWmZ/">CSS :required pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :scope (Experimental)

The `:scope` pseudo-class makes most sense when it’s tied to the `scoped` HTML attribute in a `style` tag.

If there is no `scoped` attribute in a `style` tag within a section of the page, then the `:scope` pseudo-class will traverse all the way up to the `html` element, which is basically the default scope of a style sheet.

In the following example, the HTML block has a `scoped` style sheet, and so all text in the second `section` element will be shown in italics.

**HTML and CSS:**

<pre><code class="language-markup">&lt;article&gt;
    &lt;section&gt;
        &lt;h1&gt;Lorem ipsum dolor sit amet&lt;/h1&gt;
        &lt;p&gt;Lorem ipsum dolor sit amet.&lt;/p&gt;
    &lt;/section&gt;
    &lt;section&gt;
        &lt;style scoped&gt;
                        :scope {
                            font-style: italic;
                        }
                  &lt;/style&gt;
        &lt;h1&gt;This text will be italicized&lt;/h1&gt;
        &lt;p&gt;This text will be italicized.&lt;/p&gt;
    &lt;/section&gt;
&lt;/article&gt;
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="ZQobzz" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/ZQobzz/">CSS :scope pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

{{% ad-panel-leaderboard %}}

## Language

Language pseudo-classes relate to the text contained on the page. They do not target any media such as images or video.

### :dir (Experimental)

The `:dir` pseudo-class targets an element whose directionality is specified in the document. In other words, in order for the `:dir` pseudo-class to work, we need to specify the directionality of the relevant element in the markup with the `dir` HTML attribute.

Two directions are currently available and supported: `ltr` (left to right) and `rtl` (right to left).

At the time of writing, only Firefox (with a prefixed `-moz-dir()` selector) supports the `:dir` pseudo-class. This will very likely change in future; so, the following examples show both the prefixed and non-prefixed selectors.

**Note:** Combining the prefixed and unprefixed versions in a single rule won’t work. We need to create two separate rules.

In the following example, the paragraph is written in Arabic (whose script is right to left); so, the text will be orange.

**HTML:**

<div class="break-out">

 <pre><code class="language-markup">&lt;article dir="rtl"&gt;
    &lt;p&gt;التدليك واحد من أقدم العلوم الصحية التي عرفها الانسان والذي يتم استخدامه لأغراض الشفاء منذ ولاده الطفل.&lt;/p&gt;
&lt;/article&gt;
</code></pre>
</div>

**CSS:**

<pre><code class="language-css">/* prefixed */
article :-moz-dir(rtl) {
    color: orange;
}

/* unprefixed */
article :dir(rtl) {
    color: orange;
}
</code></pre>

The paragraph in the following example is written in English (left to right); so, the text will be in blue.

**HTML:**

<div class="break-out">

 <pre><code class="language-markup">&lt;article dir="ltr"&gt;
    &lt;p&gt;If you already know some HTML and CSS and understand the principles of responsive web design, then this book is for you.&lt;/p&gt;
&lt;/article&gt;
</code></pre>
</div>

**CSS:**

<pre><code class="language-css">/* prefixed */
article :-moz-dir(ltr) {
    color: blue;
}

/* unprefixed */
article :dir(ltr) {
    color: blue;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="adrxJy" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/adrxJy/">CSS :dir pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### :lang

The `:lang` pseudo-class matches the language of an element as determined by a combination of the `lang=""` HTML attribute, the corresponding `meta` element and information gleaned from the protocol, such as an HTTP header.

The `lang=""` HTML attribute is commonly used in the `html` tag, but it can also be used in any other tag if needed.

On a tangential note, a common practice is to add proper quotation marks to a particular language using the `quotes` CSS property. However, the user agents (UA) of most browsers (including IE 9 and up) are able to add proper quotation marks automatically in case they are not declared in the CSS.

Depending on your circumstance, this may or may not be OK, because there are differences between the default quotation marks added by a browser’s UA and the commonly used quotation marks added via CSS.

For example, German (`de`) quotation marks added by a browser’s UA look like this:

<blockquote>
<p>„Lorem ipsum dolor sit amet.“
</blockquote>

However, in most examples found on the web where quotations marks are declared via CSS, German quotation marks look like this:

<blockquote>
<p>»Lorem ipsum dolor sit amet.«
</blockquote>

Both are actually correct. So, you’ll have to decide whether to let the UA add the quotation marks or to add them yourself via CSS using the `:lang` pseudo-class and the `quotes` CSS property.

Let’s add quotation marks with CSS.

**HTML:**

<pre><code class="language-markup">&lt;article lang="en"&gt;
    &lt;q&gt;Lorem ipsum dolor sit amet.&lt;/q&gt;
&lt;/article&gt;
&lt;article lang="fr"&gt;
    &lt;q&gt;Lorem ipsum dolor sit amet.&lt;/q&gt;
&lt;/article&gt;
&lt;article lang="de"&gt;
    &lt;q&gt;Lorem ipsum dolor sit amet.&lt;/q&gt;
&lt;/article&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">:lang(en) q { quotes: '“' '”'; }
:lang(fr) q { quotes: '«' '»'; }
:lang(de) q { quotes: '»' '«'; }
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="gPJyvJ" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/gPJyvJ/">CSS :lang pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Miscellaneous

Let’s explore some pseudo-classes with other functionality.

### :root

The `:root` pseudo-class refers to the highest parent element in a document.

In virtually all cases, the `:root` pseudo-class will refer to the `html` element in an HTML document. However, it could refer to a different element if it’s used in another markup language, such as SVG or XML.

Let’s add a solid background color to the `html` element, the highest parent element in an HTML document:

<pre><code class="language-css">:root {
    background: orange;
}
</code></pre>

**Note:** We could have accomplished the same effect if we had used `html` as the selector. However, `:root`, like a class, has a higher specificity than an element selector (in this case, `html`).

### :fullscreen (Experimental)

The `:fullscreen` pseudo-class targets elements that are displayed in full-screen mode.

However, it is not intended to work when the user presses F11 to enter full-screen mode in their browser. Rather, it is intended to work with the JavaScript Fullscreen API, which is geared to images, videos and games that are executed in a parent container.

The way to tell whether we have entered full-screen mode is when a message appears at the top of the browser telling us so and when pressing the `Escape` key takes us back to the normal page. We see this when maximizing a video in YouTube or Vimeo, for example.

If you plan to use the `:fullscreen` pseudo-class, keep in mind that browsers style things very differently. Plus, you will have to deal with browser prefixes not only in the CSS, but also in your JavaScript. I recommend using Hernan Rajchert’s [screenfull.js](https://github.com/sindresorhus/screenfull.js/), which irons out most browser quirks.

The Fullscreen API is beyond the scope of this article, but here’s a snippet that will work in WebKit and Blink browsers.

**HTML:**

<div class="break-out">

 <pre><code class="language-markup">&lt;h1 id="element"&gt;This heading will have a solid background color in full-screen mode.&lt;/h1&gt;
&lt;button onclick="var el = document.getElementById('element'); el.webkitRequestFullscreen();"&gt;Trigger full screen!&lt;/button&gt;
</code></pre>
</div>

**CSS:**

<pre><code class="language-css">h1:fullscreen {
    background: orange;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="ZQNZqy" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/ZQNZqy/">CSS :fullscreen pseudo-class</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Pseudo-Elements

As mentioned at the beginning of this article, pseudo-elements are like virtual elements that we can treat like regular HTML elements. They don’t exist in the document tree or DOM, which means we don’t actually type pseudo-elements in the HTML, but rather create them with CSS.

Also, the double colon (`::`) and single colon (`:`) difference is merely a visual distinction between CSS 2.1 and CSS3 pseudo-elements. You are free to use either.

### ::before/:before

The `:before` pseudo-element, like its sibling `:after`, adds content (text or a shape) to another HTML element. Again, this content is not actually present in the DOM but can be manipulated as if it were. And the `content` property needs to be declared in the CSS.

Remember that text added with this pseudo-element cannot be selected.

**HTML:**

<pre><code class="language-markup">&lt;h1&gt;Ricardo&lt;/h1&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">h1:before {
    content: "Hello "; /* Note the space after the word Hello. */
}
</code></pre>

This will render like so:

<pre><code class="language-markup">Hello Ricardo!
</code></pre>

**Note:** See the space after the word “Hello ”? Yes, spaces are taken into account.

### ::after/:after

The `:after` pseudo-element is used to add content (either text or a shape) to another HTML element. This content is not actually present in the DOM, but it can be manipulated as if it were. In order for it to work, the `content` property needs to be declared in the CSS.

Note that any text added with this pseudo-class cannot be selected.

**HTML:**

<pre><code class="language-markup">&lt;h1&gt;Ricardo&lt;/h1&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">h1:after {
    content: ", Web Designer!";
}
</code></pre>

This will render like so:

<pre><code class="language-markup">Ricardo, Web Designer!
</code></pre>

### ::backdrop (Experimental)

The `::backdrop` pseudo-element is a box that is generated behind the full-screen element but that sits above all other content. It’s used in combination with the `:fullscreen` pseudo-class to change the background color of a maximized screen — in case you don’t want to go with the default black.

**Note:** The `::backdrop` pseudo-element requires a double colon; it doesn’t work with a single colon.

Let’s continue our example from the `:fullscreen` pseudo-class.

**HTML:**

<div class="break-out">

 <pre><code class="language-markup">&lt;h1 id="element"&gt;This heading will have a solid background color in full-screen mode.&lt;/h1&gt;
&lt;button onclick="var el = document.getElementById('element'); el.webkitRequestFullscreen();"&gt;Trigger full screen!&lt;/button&gt;
</code></pre>
</div>

**CSS:**

<pre><code class="language-css">h1:fullscreen::backdrop {
    background: orange;
}
</code></pre>

**Demo:**

{{< codepen height="550" theme_id="1842" slug_hash="bEPEPE" default_tab="result" user="ricardozea" >}} See the Pen <a href="https://codepen.io/ricardozea/pen/bEPEPE/">CSS ::backdrop pseudo-element</a> by Ricardo Zea(<a href="https://codepen.io/ricardozea">@ricardozea</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### ::first-letter/:first-letter

The `:first-letter` pseudo-element selects the first letter in a line of text.

If an element is included before that line, such as an image, video or table, then the first letter is not affected and can still be selected.

This is a great feature to use in paragraphs, for example, to enhance typographic appeal, without having to resort to an image or external assets.

**Tip:** For text generated with the `:before` pseudo-element, the first letter of that text will be targeted, even though it is not present in the DOM.

**CSS:**

<pre><code class="language-css">h1:first-letter  {
    font-size: 5em;
}
</code></pre>

### ::first-line/:first-line

The `:first-line` pseudo-element targets the first line of an element. It works only on block-level elements, not inline elements.

When used in a paragraph, for example, only the first line of that paragraph will be styled, even if the text wraps.

**CSS:**

<pre><code class="language-css">p:first-line {
    background: orange;
}
</code></pre>

### ::selection

The `::selection` pseudo-element is used to style the portion of a document that has been highlighted.

Until further notice, Gecko-based browsers required the prefixed version: `::-moz-selection`.

**Note:** Combining the prefixed and unprefixed versions in a single rule won’t work. We need to create two separate rules.

**CSS:**

<pre><code class="language-css">::-moz-selection {
    color: orange;
    background: #333;
}

::selection  {
    color: orange;
    background: #333;
}
</code></pre>

### ::placeholder (Experimental)

The `::placeholder` pseudo-element targets placeholder text used in form elements via the `placeholder` HTML attribute.

It can also be written as `::input-placeholder`, which is actually the syntax used in CSS.

**Note:** This pseudo-element is not a part of the standard and its implementation will very likely change in future, so use with caution.

In some browsers (IE 10 and Firefox up to version 18), the `::placeholder` pseudo-element is implemented like a pseudo-class. All other browsers treat it like a pseudo-element. So, unless you have to support old versions of Firefox or IE 10, you would write the following.

**HTML:**

<pre><code class="language-markup">&lt;input type="email" placeholder="name@domain.com"&gt;
</code></pre>

**CSS:**

<pre><code class="language-css">input::-moz-placeholder {
    color:#666;
}

input::-webkit-input-placeholder {
    color:#666;
}

/* IE 10 only */
input:-ms-input-placeholder {
    color:#666;
}

/* Firefox 18 and below */
input:-moz-input-placeholder {
    color:#666;
}
</code></pre>

## Conclusion

Phew! That was something, eh?

CSS pseudo-classes and pseudo-elements are certainly a handful, aren’t they? They provide so many possibilities that one can easily feel overwhelmed, for sure. But that’s the life of a web designer and developer.

Make sure to test thoroughly. Well implemented pseudo-classes and pseudo-elements go a long way.

I hope you’ve enjoyed this extensive reference article as much as I did writing it. And don’t forget to bookmark it!

Thank you for reading! Hasta la próxima! (_Until next time!_)

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Learning To Use The :before And :after Pseudo-Elements In CSS](https://www.smashingmagazine.com/2011/07/learning-to-use-the-before-and-after-pseudo-elements-in-css/)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/take-your-design-to-the-next-level-with-css3/)
*   [CSS3 Flexible Box Layout](https://www.smashingmagazine.com/2011/09/css3-flexible-box-layout-explained/)

{{< signature "ml, vf, al, il" >}}

