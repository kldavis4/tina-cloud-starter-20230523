---
title: 'CSS Specificity: Things You Should Know'
slug: css-specificity-things-you-should-know
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b109b0aa-0918-4bc5-b480-f54839238cdb/specificity.png
date: 2007-07-27T13:02:47.000Z
author: vitaly-friedman
description: >-
  CSS Specificity is not simple. However, there are methods to explain it in a
  simple and intuitive way. And that’s what this article is all about.
categories:
  - Coding
  - CSS
  - Essentials
---
Apart from <a href="https://www.smashingmagazine.com/2007/05/01/css-float-theory-things-you-should-know/">Floats</a>, the <strong>CSS Specificity</strong> is one of the most difficult concepts to grasp in Cascading Stylesheets. The different weight of selectors is usually the reason why your CSS-rules don't apply to some elements, although you think they should have. In order to minimize the time for bug hunting you need to understand, how browsers interpret your code. And to understand that, you need to have a <strong>firm understanding on how specificity works</strong>. In most cases such problems are caused by the simple fact that somewhere among your CSS rules you've defined a more specific selector. <em>This article has been updated on October 5th, 2016.</em>

CSS Specificity isn't simple. However, there are methods to explain it in a simple and intuitive way. And that's what this article is all about. You'll understand the concept if you love Star Wars. <em>Really.</em>

Recommended reading: [CSS Specificity And Inheritance](https://www.smashingmagazine.com/2010/04/css-specificity-and-inheritance/)

<p>Let's take a look at some <strong>important issues related to CSS Specificity</strong> as well as examples, rules, principles, common solutions, and resources. You can find the most important things you should know about CSS specificity in a brief overview at the beginning of the article.</p>

## CSS Specificity: An Overview

1.  Specificity **determines, which CSS rule is applied** by the browsers.
2.  Specificity is usually the reason why your CSS-rules don't apply to some elements, although you think they should.
3.  Every selector has its place in the specificity hierarchy.
4.  If two selectors apply to the same element, the one with **higher specificity wins**.
5.  There are five distinct categories which define the specificity level of a given selector: inline styles, IDs, classes, attributes, and elements.
6.  You can understand specificity if you love _Star Wars_: [CSS Specificity Wars](https://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html).
7.  You can understand specificity if you love poker: CSS Specificity for Poker Players
8.  When selectors have an equal specificity value, the latest rule is the one that counts.
9.  When selectors have an unequal specificity value, the more specific rule is the one that counts.
10.  Rules with more specific selectors have a greater specificity.
11.  The last rule defined overrides any previous, conflicting rules.
12.  The embedded style sheet has a greater specificity than other rules.
13.  ID selectors have a higher specificity than attribute selectors.
14.  You should always try to **use IDs to increase the specificity**.
15.  A class selector beats any number of element selectors.
16.  The universal selector and inherited selectors have a specificity of 0, 0, 0, 0.
17.  You can calculate CSS specificity with CSS Specificity Calculator.</p>

{{% feature-panel %}}

## What is Specificity?

<strong>If two CSS selectors apply to the same element, the one with higher specificity wins.</strong>

## Specificity hierarchy

Every selector has its place in the specificity hierarchy. There are four distinct categories which define the specificity level of a given selector:

1. Inline styles (Presence of style in document).
An inline style lives within your XHTML document. It is attached directly to the element to be styled. E.g. <code>&lt;h1 style="color: #fff;"&gt;</code>

2. IDs (# of ID selectors)
ID is an identifier for your page elements, such as <code>#div</code>.

3. Classes, attributes and pseudo-classes (# of class selectors).
This group includes <code>.classes</code>, <code>[attributes]</code> and pseudo-classes such as <code>:hover</code>, <code>:focus</code> etc.

4. Elements and pseudo-elements (# of Element (type) selectors).
Including for instance <code>:before</code> and <code>:after</code>.

If you don't know what exactly each of these terms stands for, you can take a look at the brief overview of them; in the last section of this article.</p>

## How to measure specificity?

<strong>Memorize how to measure specificity.</strong> "Start at 0, add 1000 for style attribute, add 100 for each ID, add 10 for each attribute, class or pseudo-class, add 1 for each element name or pseudo-element. So in

<pre><code class="language-css">body #content .data img:hover</code></pre>

the specificity value would be 122 (<strong>0,1,2,2</strong> or 0122): 100 for #content, 10 for .data, 10 for :hover, 1 for body and 1 for img." [CSS Specificity]

<strong>Alternative way:</strong> "Count the number of ID attributes in the selector (= a). Count the number of other attributes and pseudo-classes in the selector (= b). Count the number of element names and pseudo-elements in the selector (= c). Concatenating the three numbers <strong>a-b-c gives the specificity</strong>. [<a href="https://juicystudio.com/article/selector-specificity.php">CSS Selector Specificity</a>]

<a href="https://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html">CSS Specificity Wars - Cheat Sheet</a>
To help me understand calculating specificity better I made a chart based on the following specificity (or Sith power) values. Each character (selector) is given its own Sith power (specificity value) depending on how powerful they are in the ways of the Dark Side. A storm trooper is less powerful than Vader who is in turn less powerful than the Emperor.

<figure><a href="https://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html"><img loading="lazy" decoding="async" title="CSS Specificity Wars" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca8aa7b1-17cf-455e-a1e6-5e409518d09a/specificity-wars.jpg" alt="CSS Specificity Wars" width="507" height="386" /></a></figure>

## Specificity Examples: Test Yourself

It's easier to calculate the specificity using the first method. Let's find out, how it actually is done.
<table class="break-out"><br>
<tbody>
<tr>
<td class="num">1</td>
<td>* { }</td>
<td>0</td>
</tr>
<tr class="pdd">
<td class="num">2</td>
<td>li { }</td>
<td>1 (one element)</td>
</tr>
<tr>
<td class="num">3</td>
<td>li:first-line { }</td>
<td>2 (one element, one pseudo-element)</td>
</tr>
<tr class="pdd">
<td class="num">4</td>
<td>ul li { }</td>
<td>2 (two elements)</td>
</tr>
<tr>
<td class="num">5</td>
<td>ul ol+li { }</td>
<td>3 (three elements)</td>
</tr>
<tr class="pdd">
<td class="num">6</td>
<td>h1 + *[rel=up] { }</td>
<td>11 (one attribute, one element)</td>
</tr>
<tr>
<td class="num">7</td>
<td>ul ol li.red { }</td>
<td>13 (one class, three elements)</td>
</tr>
<tr class="pdd">
<td class="num">8</td>
<td>li.red.level { }</td>
<td>21 (two classes, one element)</td>
</tr>
<tr>
<td class="num">9</td>
<td>style=""</td>
<td>1000 (one inline styling)</td>
</tr>
<tr class="pdd">
<td class="num">10</td>
<td>p { }</td>
<td>1 (one HTML selector)</td>
</tr>
<tr>
<td class="num">11</td>
<td>div p { }</td>
<td>2 (two HTML selectors)</td>
</tr>
<tr class="pdd">
<td class="num">12</td>
<td>.sith</td>
<td>10 (one class selector)</td>
</tr>
<tr>
<td class="num">13</td>
<td>div p.sith { }</td>
<td>12 (two HTML selectors and a class selector)</td>
</tr>
<tr class="pdd">
<td class="num">14</td>
<td>#sith</td>
<td>100 (one id selector)</td>
</tr>
<tr>
<td>15</td>
<td>body #darkside .sith p { }</td>
<td>112 (HTML selector, id selector, class selector, HTML selector; 1+100+10+1)</td>
</tr>
</tbody>
</table>

## Specificity: Basic Principles

<strong>Equal specificity: the latest rule is the one that counts.</strong> "If you have written the same rule into your external style sheet twice, then the lower rule in your style sheet is closer to the element to be styled, it is deemed to be more specific and therefore will be applied.
When selectors have an equal specificity value, such as

<pre><code class="language-css">#content h1 {
padding: 5px;
}

#content h1 {
padding: 10px;
}</code></pre>

where both rules have the specificity <strong>0, 1, 0, 1</strong>, the latter rule is always applied.

## Specificity Rules

<strong>ID selectors have a higher specificity than attribute selectors.</strong> For example, in HTML, the selector <code>#p123</code> is more specific than <code>[id=p123]</code> in terms of the cascade. Example: in

<pre><code class="language-css">A:
a#a-02 { background-image : url(n.gif); }

and

B:
a[id="a-02"] { background-image : url(n.png); }</code></pre>

the first rule (A) is more specific than the second one (B). [<a href="https://www.w3.org/TR/CSS21/selector.html">W3C CSS 2.1 Specification</a>]

<strong>Contextual selectors are more specific than a single element selector.</strong> It also holds for other selectors involving more than one HTML element selector. [<a href="https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/">Cascade Inheritance</a>]

<strong>The embedded style sheet is closer to the element to be styled.</strong> So in the following situation

CSS:

<pre><code class="language-css">#content h1 {
padding: 5px;
}</code></pre>

(X)HTML:

<pre><code class="language-markup tmp-html">&lt;style type="text/css"&gt;
#content h1 {
padding: 10px;
}
&lt;/style&gt;</code></pre>

the latter rule will be applied.

<strong>The last rule defined overrides any previous, conflicting rules.</strong> For example, given these two rules

<pre><code class="language-css">p { color: red; background: yellow }
p { color: green }</code></pre>

...paragraphs would appear in green text. They would also have a yellow background, however, because the first rule is not completely negated. [<a href="https://www.brainjar.com/css/using/default4.asp">BrainJar.com</a>]

<strong>A class selector beats any number of element selectors.</strong> <code>.introduction</code> beats <code>html body div div h2 p</code>. [CSS Specificity for Poker Players]

<strong>The universal selector has a specificity of 0, 0, 0, 0.</strong> <code>*</code>, <code>body *</code> and similar selectors have a zero specificity. <em>Inherited values also have a specificity of 0, 0, 0, 0.</em> [<a href="https://molly.com/2005/10/06/css2-and-css21-specificity-clarified/">CSS Specificity Clarified</a>]

## Specificity Example

Consider three code fragments:

<pre><code class="language-css">A: h1
B: #content h1
C: &lt;div id="content"&gt;
&lt;h1 style="color: #fff"&gt;Headline&lt;/h1&gt;
&lt;/div&gt;</code></pre>

The specificity of A is <strong>0,0,0,1</strong> (<em>one</em> element), the specificity of B is <strong>0,1,0,1</strong> (one ID reference point and one element), the specificity value of C is <strong>1,0,0,0</strong>, since it is an inline styling.

Since

0001 = 1 &lt; 0101 = 101 &lt; 1000,

...the third rule has a greater level of specificity, and therefore will be applied. If the third rule didn't exist, the second rule would have been applied.</p>

## Specificity in Practice

<strong>Use LVHA for link styling.</strong>
"To ensure that you see your various link styles, you're best off putting your styles in the order "link-visited-hover-active", or "LVHA" for short." [<a href="https://meyerweb.com/eric/css/link-specificity.html">Link Specificity</a>]

<strong>Never use <code>!important</code>.</strong>
"If you're having specificity issues, there's some quick ways to solve it. First, avoid <code>!important</code>." "The <code>!important</code> declaration overrides normal declarations, but is unstructured and rarely required in an author's style sheet." [<a href="https://www.snook.ca/archives/html_and_css/understanding_c/">Understanding Specificity</a>, <a href="https://juicystudio.com/article/selector-specificity.php">Selector Specificity</a>]

<strong>Use id to make a rule more specific.</strong>
Replacing <code>a.highlight</code> with <code>ul#blogroll a.highlight</code> changes the specificity from <strong>0, 0, 1, 1</strong> to <strong>0, 1, 1, 2</strong>.

<strong>Minimize the number of selectors.</strong>
"Use the least number of selectors required to style an element." [<a href="https://www.snook.ca/archives/html_and_css/understanding_c/">Understanding Specificity</a>]

## CSS Specificity Tools & Resources

<a href="https://carl.camera/?id=95">CSS Specificity for Poker Players</a>
If you're not from the programming world and CSS seems a bit confusing, perhaps this analogy may help clear some concepts up. Think of CSS rules as poker hands. The best hand determines an element's style.

<a href="https://specificity.keegan.st/">CSS specificity calculator</a>
Calculates the specificity of a given selector.

<a href="https://www.adobe.com/devnet/dreamweaver/articles/css_specificity.html">Understanding Specificity Tutorial</a>
In this tutorial, you will look at specificity. Specificity is a type of weighting that has a bearing on how your cascading style sheet (CSS) rules are displayed. All rules in your style sheet carry a specificity rating regardless of selector type, although the weighting that is given to each selector type varies and will ultimately affect the styling of your web documents.

<a href="https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/">Cascade Inheritance: Specificity</a>
At this point, it might be timely to have a quick discussion of specificity. Both inside a single style sheet, and in a cascade of style sheets, it should be clear that more than one rule can apply to the same element. What happens when two properties in separate rules which both apply to an element contradict one another?

<a href="https://www.456bereastreet.com/archive/200509/css_21_selectors_part_1/">CSS 2.1 Selectors Explained</a>
An extensive overview of CSS 2.1 selectors. Learning how to use the full range of CSS selectors available in CSS 2.1 properly can actually help you keep your HTML a lot cleaner. It will let you minimise unnecessary use of the class attribute and the need for adding extraneous <code>div</code> and <code>span</code> elements to the markup.

<a href="https://www.brunildo.org/test/IEASpec.html">CSS Specificity Bugs in IE</a>
A brief overview of specificity bugs implemented in Microsoft Internet Explorer/Win.

<a href="https://www.htmlhelp.com/reference/css/structure.html">CSS Structure and Rules</a>
Basic Syntax, Pseudo-classes and Pseudo-elements, Cascading Order.

<a href="https://www.htmldog.com/guides/cssadvanced/specificity/">Specificity</a>
It may not seem like something that important, and in most cases, you won't come across any conflicts at all, but the larger and more complex your CSS files become, or the more CSS files you start to juggle with, the greater likelihood there is of conflicts turning up.</p>

Recommended reading: [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)

## What is what?

A <strong>selector</strong> is the element that is linked to a particular style. E.g. <code>p</code> in

<pre><code class="language-css">p { padding: 10px; }</code></pre>

A <strong>class selector</strong> is a selector that uses a defined class (multiple per page). E.g. <code>p.section</code> in

<pre><code class="language-css">p.section { padding: 10px; }</code></pre>

An <strong>ID selector</strong> is a selector that uses an individually assigned identifier (one per page). E.g. <code>p#section</code> in

<pre><code class="language-css">CSS: #section { padding: 10px; }
(X)HTML: &lt;p id="section"&gt;Text&lt;/&gt;</code></pre>

A <strong>contextual selector</strong> is a selector that defines a precise cascading order for the rule. E.g. <code>p span</code> in

<pre><code class="language-css">p span { font-style: italic; }</code></pre>

defines that all span-elements within a p-element should be styled in <em>italics</em>.

An <strong>attribute selector</strong> matches elements which have a specific attribute or its value. E.g. <code>p title</code> in

<pre><code class="language-css">p[title] { font-weight: bold; }</code></pre>

matches all p-elements which have a <code>title</code> attribute.

<strong>Pseudo-classes</strong> are special classes that are used to define the behavior of HTML elements. They are used to add special effects to some selectors, which are applied automatically in certain states. E.g. <code>:visited</code> in

<pre><code class="language-css">a:visited { text-decoration: underline; }</code></pre>

<strong>Pseudo-elements</strong> provide designers a way to assign style to content that does not exist in the source document. Pseudo-element is a specific, unique part of an element that can be used to generate content "on the fly", automatic numbering and lists. E.g. <code>:first-line</code> or <code>:after</code> in

<pre><code class="language-css">p:first-line { font-variant: small-caps; }
a:link:after { content: " (" attr(href) ")"; }</code></pre>

Further reading: [!important CSS Declarations: How and When to Use Them](https://www.smashingmagazine.com/2010/11/the-important-css-declaration-how-and-when-to-use-it/)
