---
title: 'CSS Float Theory: Things You Should Know'
slug: css-float-theory-things-you-should-know
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/767da047-7719-4f42-af7e-59d9074865ae/float.png
date: 2007-05-02T04:09:06.000Z
author: vitaly-friedman
description: >-
  The concept of floats is probably one of the most unintuitive concepts in CSS.
  Floats are often misunderstood and blamed for floating all the context around
  it, causing readability and usability problems. However, the reason for these
  problems isn't the theory itself, but the way the theory is interpreted - by
  developers and browsers. Still, if you take a closer look at the float theory,
  you'll find out out that it isn't that complex as it appears to be. Most
  related problems are caused by the older versions of (take a guess) Internet
  Explorer. If you know the bugs, you can control the way information is
  presented in a more sophisticated, profound way.
categories:
  - Coding
  - Layouts
  - CSS
  - Tutorials
  - Essentials
---
The concept of floats is probably one of the most unintuitive concepts in CSS. Floats are often misunderstood and blamed for floating all the context around it, causing readability and usability problems. However, the reason for these problems isn't the theory itself, but the way the theory is interpreted - by developers and browsers. 

<figure><a href="https://www.w3.org/TR/CSS2/visuren.html#floats"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eaed47d-3905-4cfb-9667-c74b8878936e/float-03.gif" alt="CSS Float Theory: Things You Should Know" title="CSS Float Theory: Things You Should Know" height="200" width="440" /></a></figure>

Still, if you take a closer look at the float theory, you'll find out out that it isn't that complex as it appears to be. Most related problems are caused by the older versions of (take a guess) Internet Explorer. If you know the bugs, you can control the way information is presented in a more sophisticated, profound way. 

Let's try to tackle the issue and clarify some usual misunderstandings, which always appear once floats are being used. We've browsed through dozens of related articles and selected the <strong>most important things you should keep in mind developing css-based layouts with floats</strong>.

You might be interested in the following related posts:

{{% feature-panel %}}

*   [The Mystery Of The CSS Float Property](https://www.smashingmagazine.com/2009/10/the-mystery-of-css-float-property/)
*   [Mastering CSS Principles: A Comprehensive Guide](https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/)
*   [Mastering CSS Coding: Getting Started](https://www.smashingmagazine.com/2009/10/mastering-css-coding-getting-started/)
*   [CSS3 Flexible Box Layout Explained](https://www.smashingmagazine.com/2011/09/css3-flexible-box-layout-explained/)

## What You Should Know About Floats

<ul>
 	<li>"The practice of flowing text around an image goes back a long, long time. That's why the ability was added to the Web starting with Netscape 1.1, and why CSS makes it possible using the property float. The term "float" refers to the way in which an element floats to one side and down, as described in the original "Additions to HTML 2.0" document that accompanied the release of Netscape 1.1."
<figure><a href="https://www.complexspiral.com/publications/containing-floats/"><img loading="lazy" decoding="async" title="Containing Floats" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0057fb29-799b-416a-9d42-d6a589d53f1b/float-00.gif" alt="Containing Floats" width="440" height="200" /></a><figcaption><a href="https://www.complexspiral.com/publications/containing-floats/">Containing Floats</a></figcaption></figure></li>
 	<li>"A floated box <strong>is positioned within the normal flow</strong>, then taken out of the flow and shifted to the left or right as far as possible. Content may flow along the side of a float. [...] When a box is taken out of normal flow, all content that is still within normal flow will ignore it completely and not make space for it." [<a href="https://css.maxdesign.com.au/floatutorial/definitions.htm">Float Positioning</a>]</li>
 	<li>"When you float an element <strong>it becomes a block box</strong>. This box can then be shifted to the left or right on the current line. The markup options are <code>float: left</code>, <code>float: right</code> or <code>float: none</code>." [<a href="https://css.maxdesign.com.au/floatutorial/introduction.htm">Floatutorial: Float Basics</a>]</li>
 	<li>"You should <strong>always set a width on floated items</strong> (except if applied directly to an image - which has implicit width). If no width is set, the results can be unpredictable." [<a href="https://css.maxdesign.com.au/floatutorial/introduction.htm">Floatutorial: Float Basics</a>]</li>
 	<li>"For one, the box being floated should have a width defined for it, either explicitly or implicitly. Otherwise, it will fill its containing block horizontally, just like non-floated content, leaving no room for other content to flow around it. Second, unlike boxes in the normal flow, the vertical margins of a floated box are not collapsed with the margins of boxes either above or below it. Finally, a floated box can overlap block-level boxes adjacent to it in the normal flow."
<figure><a href="https://www.brainjar.com/css/positioning/default3.asp"><img loading="lazy" decoding="async" title="CSS Positioning: Floats" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/717d5cbc-4f72-42ed-b941-0079ee0a794f/float-02.gif" alt="CSS Positioning: Floats" width="440" height="200" /></a><figcaption><a href="https://www.brainjar.com/css/positioning/default3.asp">CSS Positioning: Floats</a></figcaption></figure></li>
 	<li>"The first thing we need to remember is that a floating element is shifted either to the left or to the right. It is not possible to make an element float in the centre, something that often is frustrating for beginners. The basic rule is that a floating element is only shifted sideways." [Float Layouts]</li>
 	<li>"When we float an element it is shifted to the right or to the left until it reaches the edge of the containing block. If we then float another element nearby in the same direction, it will be shifted until its edge reaches the edge of the first floating element. [...] If we float more elements in the same direction they will stack up, but sooner or later we'll run out of space [...] when there is insufficient space on the line, they are shifted downward until they fit." [Float Layouts]</li>
 	<li>Containing blocks or containing boxes: "A containing block is a box or block that contains other elements (descendant boxes). An element's containing block means "the containing block in which the element lives". [<a href="https://css.maxdesign.com.au/floatutorial/definitions.htm">Floatutorial</a>]</li>
 	<li>"Floated boxes <strong>will move to the left or right</strong> until their outer edge touches the containing block edge or the outer edge of another float." [<a href="https://css.maxdesign.com.au/floatutorial/introduction.htm">Floatutorial: Float Basics</a>]</li>
 	<li>"When specified, the box is positioned vertically as it would be within the normal flow, its top aligned with the top of the current line box. But horizontally, it is shifted as far to the right or left of its containing block as possible, within that block's padding (just like other content). Surrounding inline content is then allowed to flow around the opposite side." [<a href="https://www.brainjar.com/css/positioning/default2.asp">CSS Positioning: Floats</a>]</li>
 	<li>"Since a float is not in the flow, non-positioned block boxes created before and after the float box flow vertically as if the float didn't exist. However, line boxes created next to the float are shortened to make room for the floated box. Any content in the current line before a floated box is reflowed in the first available line on the other side of the float."
<figure><a href="https://www.w3.org/TR/CSS2/visuren.html#floats"><img loading="lazy" decoding="async" title="W3C Visual Formatting Model" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eaed47d-3905-4cfb-9667-c74b8878936e/float-03.gif" alt="W3C Visual Formatting Model" width="440" height="200" /></a><figcaption><a href="https://www.w3.org/TR/CSS2/visuren.html#floats">W3C Visual Formatting Model</a></figcaption></figure></li>
 	<li>"If there isn't enough horizontal room on the current line for the floated box, it will move downward, line by line, until a line has room for it." [<a href="https://css.maxdesign.com.au/floatutorial/introduction.htm">Floatutorial: Float Basics</a>]</li>
 	<li>"A floating box can never end up above the upper edge of the line where it's created. [...] The upper edge of a floating box is aligned with the upper edge of the current line box (or with the bottom edge of the previous block box, if there is no line box)." [Float Layouts]</li>
 	<li>"In order to really understand float theory you have to understand what a line box means in CSS. Unfortunately, that in turn requires you to understand what is meant by an inline box. [...] An inline box is generated by those elements that aren't block-level, such as EM. [...] A line box is an imaginary rectangle that contains all the inline boxes that make up a line in the containing block-level element. It is (at least) as tall as its tallest line box." [Float Layouts]</li>
 	<li>"If we enclose each column in a DIV element with <code>float: left</code> they will appear side by side, just as we expect columns to do. If we then want a full-width footer to be shown at the bottom, no matter which column happens to be longest, we only need to set <code>clear: both</code> on it." [Float Layouts]</li>
 	<li>"The potential drawback to using floats to contain floats is that <strong>you rely on browsers to consistently interpret the layout</strong> of multiple nested floated elements. The situation becomes more fragile if these floats are part of a more complicated layout, one possibly using floats, positioning, or tables." [<a href="https://www.complexspiral.com/publications/containing-floats/">Containing Floats</a>]</li>
</ul>

## Clearing the floats

*   "Elements following a floated element will wrap around the floated element. If you do not want this to occur, you can apply the "clear" property to these following elements. The four options are `clear: left`, `clear: right`, `clear: both` or `clear: none`." [[Floats and "clear"](https://css.maxdesign.com.au/floatutorial/clear.htm)]
*   How to clear CSS floats without extra markup - different techniques explained. There are three major approaches: a) Floating the containing element as well, b) Using `overflow: hidden` on the container, c) Generating content using the `:after` CSS pseudo-class. [A test-page for techniques](https://www.robertnyman.com/css-clearing-floats/css-clearing-floats.htm). [[How to clear CSS floats without extra markup](https://www.robertnyman.com/2007/04/12/how-to-clear-css-floats-without-extra-markup-different-techniques-explained/)]
*   "The standard method of making an outer container appear to "enclose" a nested float is to place a complete "cleared" element last in the container, which has the effect of 'dragging' the lower edge of the containing box lower than the float."

1.  `<div> <!-- float container -->`
2.  `<div style="float:left; width:30%;"><p>Some content</p></div>`
3.  `<p>Text not inside the float</p>`
4.  `<div style="clear:both;"></div>`
5.  `</div>`

<ul>
 	<li>[<a href="https://www.positioniseverything.net/easyclearing.html">How To Clear Floats Without Structural Markup</a>]</li>
 	<li>"A common problem with float-based layouts is that the floats' container doesn't want to stretch up to accomodate the floats. If you want to add, say, a border around all floats (ie. a border around the container) you'll have to command the browsers somehow to stretch up the container all the way. You can clear the floats using <a href="https://www.quirksmode.org/blog/archives/2005/03/clearing_floats.html">overflow method</a>."
<figure><a href="https://www.quirksmode.org/blog/archives/2005/03/clearing_floats.html"><img loading="lazy" decoding="async" title="Clearing Floats" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fa38285-e1b8-436c-8d62-391613e8408b/float-04.gif" alt="Clearing Floats" width="440" height="200" /></a><figcaption><a href="https://www.quirksmode.org/css/clearing.html">Clearing floats</a></figcaption></figure></li>
 	<li>Using <code>:after</code>: imagine that we use :after to insert a simple character like a 'period', and then give that generated element <code>{clear: both;}</code>. That's all you really need to do the job, but no one wants a line space messing up the end of their clean container box, so we also use <code>{height: 0;}</code> and <code>{visibility: hidden;}</code> to keep our period from showing.</li>
</ul>

1.  `.clearfix:after {`
2.  `content: ".";`
3.  `display: block;`
4.  `height: 0;`
5.  `clear: both;`
6.  `visibility: hidden;`
7.  `}`

*   [[How To Clear Floats Without Structural Markup](https://www.positioniseverything.net/easyclearing.html)]
*   Clearfix: "When a float is contained within a container box that has a visible border or background, that float does not automatically force the container's bottom edge down as the float is made taller. Instead the float is ignored by the container and will hang down out of the container bottom like a flag. [...] IE/Win does enclose a float within a container 'automatically', but only if the container element has a stated dimension." [[Easyclearing: How To Clear Floats Without Structural Markup](https://www.positioniseverything.net/easyclearing.html)]

## CSS Float Bugs

<ul>
 	<li>When [...] container element has links inside, following the float. When this happens and certain links are hovered, the auto-enclosing behavior is toggled or "switched off", causing the lower edge of the container box to suddenly jump up to the bottom of the non-floated content. Hovering other links restores the behavior. This interesting effect is of course called the <a href="https://www.positioniseverything.net/explorer/guillotine.html">IE/Win Guillotine Bug</a>. The toggling only occurs when a:hover is used to change the link background or many other styling changes, such as padding, margin, or any font styling on the link. Strangely, having the text color change on hover does not toggle the bug.
<figure><a href="https://www.positioniseverything.net/explorer/guillotine.html"><img loading="lazy" decoding="async" title="IE/Win Guillotine Bug" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f53144d2-bc71-4f16-9290-e743909004ad/float-05.gif" alt="IE/Win Guillotine Bug" width="440" height="200" /></a></figure>[<a href="https://www.positioniseverything.net/easyclearing.html">How To Clear Floats Without Structural Markup</a>]</li>
 	<li><a href="https://www.positioniseverything.net/explorer/escape-floats.html">The IE Escaping Floats Bug</a>: "If you use a div box with margins, borders and a number of left floated divs, you'll get two display errors in IE Win. One, the container is only containing the last line of floats , and the floats are also running off to the right, all the way to the right screen edge. also causes a horizontal scrollbar at many screen sizes. [...] Solution: a height can be given to IE/win and not affect the displayed height of the container. This is possible because IE has another non-standard behavior concerning boxes and dimensions." Holly Hack: assigning a height to the element, i.e. <code>height: 1%;</code>.
<figure><a href="https://www.positioniseverything.net/explorer/escape-floats.html"><img loading="lazy" decoding="async" title="IE Escaping Floats Bug" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6080a2c-0cc7-40a7-8cab-41df6e6b1eb1/float-06.gif" alt="IE Escaping Floats Bug" width="440" height="200" /></a></figure></li>
 	<li><a href="https://www.positioniseverything.net/explorer/peekaboo.html">The Win/IE6 Peekaboo bug</a>: "A liquid box has a float inside, and content that appears along side that float. In IE6 the content disappears. When you scroll down, or perhaps switch to another window, upon returning back there it all is (this long standing bug has been suppressed in IE7).
<figure><a href="https://www.positioniseverything.net/explorer/peekaboo.html"><img loading="lazy" decoding="async" title="Win/IE6 Peekaboo bug" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b6488c2-de73-48fd-9686-fc5d415c4a53/float-07.gif" alt="Win/IE6 Peekaboo bug" width="440" height="200" /></a></figure></li>
 	<li>"IE/Win gives a left floated block a right margin of 3px. No matter what you do, the margin is still there. To see this in action, check the <a href="https://www.456bereastreet.com/lab/floating_bug/index.html">floating bug</a> first and then the <a href="https://www.456bereastreet.com/lab/floating_bug/fixed.html">double float fix</a>." This bug is also called <a href="https://www.positioniseverything.net/explorer/threepxtest.html">The IE Three Pixel Text-Jog</a> [<a href="https://www.456bereastreet.com/archive/200309/floating_bugs/">Floating Bugs</a>].</li>
 	<li><a href="https://positioniseverything.net/explorer/dup-characters.html">IE Duplicate Character Bug</a>: "Internet Explorer 6 has a puzzling bug involving multiple floated elements; text characters from the last of the floated elements are sometimes duplicated below the last float. The direct cause is nothing more than ordinary HTML comments, such as, <code>&lt;!-- end left column --&gt;</code>, sandwiched between floats that come in sequence. <a href="https://positioniseverything.net/explorer/dup-characters.html">Bugfix</a>.
<figure><a href="https://positioniseverything.net/explorer/dup-characters.html"><img loading="lazy" decoding="async" title="IE Duplicate Character Bug" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbcfb4e9-ded5-41af-b044-c13fac00df9a/float-08.gif" alt="IE Duplicate Character Bug" width="440" height="200" /></a></figure>[<a href="https://positioniseverything.net/explorer/dup-characters.html">IE Duplicate Character Bug</a>]</li>
 	<li>"One of the most common tasks when laying out the content of a web page is floating images to the right or left so that text flows around them. The addition of the clear to the floated image ensures that each one will always sit below the previous one. However, placing the float and clear properties on the same element can cause large gaps to appear in Internet Explorer (IE) — gaps that take more complicated CSS to fix than what we've used so far. Bugfix." [Close Gaps Next to Floated Images in Internet Explorer]</li>
 	<li>"You place a left float into a container box, and use a left margin on the float to push it away from the left side of the container. In Internet Explorer the left float margin has been doubled in length!" [<a href="https://www.positioniseverything.net/explorer/doubled-margin.html">The IE Doubled Float-Margin Bug</a>]</li>
 	<li>"The bug demonstrated here causes in-line elements (images, text) adjacent to a floated div to appear to be indented from their expected location. The indentation is caused by IE/Win's weird handling of margins on floated elements." [<a href="https://www.positioniseverything.net/explorer/floatIndent.html">Floats, Margins and IE</a>]</li>
 	<li>"There is a simple solution that fixes many of the IE float bugs. All floats become a block box; the standard says that the display property is to be ignored for floats, unless it's specified as <code>none</code>. If we set <code>display:inline</code> for a floating element, some of the IE/Win bugs disappears as if by magic. IE/Win doesn't make the element into an inline box, but many of the bugs are fixed." [Float Layouts]</li>
 	<li>"Using a combination of float and negative margins on an element makes any links in the element unclickable in Safari 1.3 and Safari 2.0. Text also becomes very difficult to select, and if you tab through the links they disappear when they lose focus. A workaround is to add <code>position:relative</code> to the CSS declaration for any floated elements with negative margins." [<a href="https://www.456bereastreet.com/lab/float_negative_margins/">Float + negative margin problems in Safari</a>]</li>
 	<li>"MSIE 7 now correctly implements the W3C specification by collapsing containers that include floated children. However, as it has not implemented generated content, the so called <a href="https://www.positioniseverything.net/easyclearing.html">easy clearing method</a> is not an option for clearing floats in MSIE 7. The overflow method is an appropriate solution for all versions of Internet Explorer:</li>
</ul>

<pre><code class="language-markup">#content { overflow : hidden; _height : 1%; }</code></pre>

*   [[Clearing floats without sructural markup in IE7](https://www.stuffandnonsense.co.uk/archives/clearing_floats_without_structural_markup_in_ie7.html)]

## CSS Float Tutorials and Techniques

<ul>
 	<li><a href="https://www.ejeliot.com/samples/clearing/rule-support.html">Float Containing Rules By Browser
</a><br>
<figure><a href="https://www.ejeliot.com/samples/clearing/rule-support.html"><img loading="lazy" decoding="async" title="Containing Rules By Browser" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f0ebae1-2c1c-49d8-b83c-b4d09405af6d/float-09.gif" alt="Containing Rules By Browser" width="440" height="200" /></a></figure>The table shows which rules cause a container to clear its floats in each of the main browsers.</li>
 	<li><a href="https://d-graff.de/fricca/center.html">CSS vertical centering using float and clear - crossbrowser</a>
"The box stays in the middle of the browser's viewport. The content does not disappear when the viewport gets smaller than the box."</li>
 	<li><a href="https://www.westciv.com/style_master/house/tutorials/quick/floated_layout/index.html">A floated page layout</a>
This tutorial shows you how to create a <a href="https://www.westciv.com/style_master/house/tutorials/quick/floated_layout/photos.html">page layout like this</a>, using web standards and CSS. Such a layout could have any number of uses, of which a photo gallery is only the most obvious. The page I've linked to there clearly isn't finished, I've just tried to keep it simple so we can focus on the layout of the images and the text.</li>
 	<li>Build a better Web site by understanding floated elements in CSS
This article provides a brief introduction to these floated elements, explaining the CSS float and clear directives and providing some examples of how you can use them to better position HTML elements on a Web page.</li>
 	<li>Create Columns with Floats
In general, there are currently two ways to create a multi-column layout in CSS: absolute positioning or floating. The vast majority of the time, floating will be your method of choice in laying out your web pages with CSS. In this tutorial, you'll learn how to create the look of columns using the float, width and margin properties.</li>
 	<li>Safe Lists Next to Left-Floated Elements
There are lots of different methods to format nice html lists. But are those methods reliable in all contexts and in all browsers? In this article, we'll have a look at a simple context: a list with some left-floated element next to it.</li>
 	<li><a href="https://www.alistapart.com/articles/negativemargins/">Creating Liquid Layouts with Negative Margins [and Floats]</a>
I took opportunity to demonstrate an under-used aspect of CSS: negative margins. Negative margins allow us to push the content area away from the sides of the browser, leaving room for the sidebar.</li>
 	<li><a href="https://ghettocooler.net/2005/11/13/image-floats-without-the-text-wrap/">Image floats, without the text wrap!
</a><br>
<figure><a href="https://ghettocooler.net/2005/11/13/image-floats-without-the-text-wrap/"><img loading="lazy" decoding="async" title="Image floats, without the text wrap!" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8a348dc-c84b-462b-bf98-5e01d94ae271/float-10.gif" alt="Image floats, without the text wrap!" width="440" height="200" /></a></figure>How many times do you have an image floated left in a block of content, but want to keep that content from wrapping around your image?</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0106.htm">Floating an image to the right
</a><br>
<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0106.htm"><img loading="lazy" decoding="async" title="Floatutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efe2ec6b-5d33-4bfc-834b-4e4b7f412123/float-11.gif" alt="Floatutorial" width="440" height="200" /></a></figure>Float an image to the right of a block of text and apply a border to the image.</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0211.htm">Floating an image and caption
</a><br>
<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0211.htm"><img loading="lazy" decoding="async" title="Floatutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79895ec2-3720-49ab-b36c-ec781ad5ea26/float-12.gif" alt="Floatutorial" width="440" height="200" /></a></figure>Float an image and caption to the right of a block of text and apply borders using Descendant Selectors.</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0306.htm">Floating a series of "clear: right" images
</a><br>
<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0306.htm"><img loading="lazy" decoding="async" title="Floatutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4acd6f4a-379d-4c1d-8fc2-78e472a1d585/float-13.gif" alt="Floatutorial" width="440" height="200" /></a></figure>Float a series of images down the right side of the page, with content flowing beside them.</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0407.htm">Floating an image thumbnail gallery
</a><br>
<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0407.htm"><img loading="lazy" decoding="async" title="Floatutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a8a4eff-253c-4088-97d2-b4990d9adeb7/float-14.gif" alt="Floatutorial" width="440" height="200" /></a></figure>Float a series of thumbnail images and captions to achieve an image gallery.</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0513.htm">Floating next and back buttons using lists
</a><br>
<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0513.htm"><img loading="lazy" decoding="async" title="Floatutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90c6c2be-c492-456e-a759-0cfe7bf8f744/float-15.gif" alt="Floatutorial" width="440" height="200" /></a></figure>Float a simple list into rollover "back" and next "buttons".</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0613.htm">Floating inline list items
</a><br>
<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0613.htm"><img loading="lazy" decoding="async" title="Floatutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc57c0e-d556-4542-870b-2190a310b3a2/float-16.gif" alt="Floatutorial" width="440" height="200" /></a></figure>Float a simple list, converting it into a horizontal navigation bar.</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0706.htm">Floating a scaleable drop cap
</a><br>
<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0706.htm"><img loading="lazy" decoding="async" title="Floatutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60900489-8f6e-4e65-a7b4-1918efde3af6/float-17.gif" alt="Floatutorial" width="440" height="200" /></a></figure>Float a scaleable drop cap to the left, resize it and adjust line-heights to suit your needs.</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0816.htm">Liquid two column layout</a>
Float a left nav to achieve a two column layout with header and footer.</li>
 	<li><a href="https://css.maxdesign.com.au/floatutorial/tutorial0916.htm">Liquid three column layout</a>
Float left and right columns to achieve a three column layout with header and footer.</li>
 	<li>CSS Float Html Tutorial
It's time to think outside the box, or maybe, more accurately, floating alongside of it. Where did we lose our collective CSS coding creativity? CSS allows so much freedom from traditional table based layouts that we sometimes do not consider page and layout design alternatives. What a pity. Time to think outside the box!</li>
</ul>

