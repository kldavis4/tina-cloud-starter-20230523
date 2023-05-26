---
title: Improving Code Readability With CSS Styleguides
slug: improving-code-readability-with-css-styleguides
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc9c98c0-f4dc-444a-bb36-1fa13a53196a/70expert.png
date: 2008-05-02T13:40:22.000Z
author: vitaly-friedman
description: >-
  Once your latest project is finished, you are very likely to forget the
  structure of the project's layout, with all its numerous classes, color
  schemes and type setting. To understand your code years after you've written
  it you need to make use of sensible code structuring. The latter can
  dramatically reduce complexity, improve code management and consequently
  simplify maintainability. However, how can you achieve **sensible
  structuring**? Well, there are a number of options. For instance, you can make
  use of comments — after all, there is always some area for useful hints, notes
  and, well, comments you can use afterwards, after the project has been
  deployed.
categories:
  - Coding
  - Workflow
  - CSS
  - Style Guides
  - Essentials
  - Programming
---
Once your latest project is finished, you are very likely to forget the structure of the project's layout, with all its numerous classes, color schemes and type setting. To understand your code years after you've written it you need to make use of sensible code structuring. The latter can dramatically reduce complexity, improve code management and consequently simplify maintainability. However, how can you achieve <strong>sensible structuring</strong>? Well, there are a number of options. For instance, you can make use of comments — after all, there is always some area for useful hints, notes and, well, comments you can use afterwards, after the project has been deployed. 

Indeed, developers came up with quite creative ways to use comments and text formatting to improve the maintainability of CSS-code. Such creative ways are usually combined into <a href="https://www.smashingmagazine.com/taking-pattern-libraries-next-level/">CSS styleguides</a> — pieces of CSS-code which are supposed to provide developers with useful insights into the structure of the code and background information related to it.

This article presents <strong>5 coding techniques which can dramatically improve management and simplify maintainability of your code</strong>. You can apply them to CSS, but also to any other stylesheet or programming language you are using. You can browse through the references listed under the article — they containt further information about how you can achieve a well-organized and well-structured code.

You may also be interested in the articles <a href="https://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/">70 Expert Ideas For Better CSS Coding</a>

## 1\. Divide and conquer your code

First consider the structure of your layout and identify the most important modules in your CSS-code. In most cases it's useful to choose the order of CSS-selectors according to the order of divisors (div's) and classes in your layout. Before starting coding, group common elements in separate sections and title each group. For instance, you can select Global Styles (body, paragraphs, lists, etc), Layout, Headings, Text Styles, Navigation, Forms, Comments and Extras.

{{% feature-panel %}}

To clearly separate fragments of code, select appropriate <strong>flags or striking comments</strong> (the more *-symbols you have in your code, the more striking a heading is). In the stylesheet they will serve as a heading for each group. Before applying a preferred flag to your code, make sure you can <em>immediately</em> recognize single blocks when scanning through the code.

However, this approach might not be enough for large projects where a single module is too big. If it is the case, you might need to divide your code in multiple files to maintain overview of single groups of code fragments. In such situations <strong>master stylesheet</strong> is used to import groups. Using master-stylesheet you generate some unnecessary server requests, but the approach produces a clean and elegant code which is easy to reuse, easy to understand and also easy to maintain. And you also need to include only the master-file in your documents.

<pre><code class="language-css">/*------------------------------------------------------------------
[Master Stylesheet]

Project:	Smashing Magazine
Version:	1.1
Last change:	05/02/08 [fixed Float bug, vf]
Assigned to:	Vitaly Friedman (vf), Sven Lennartz (sl)
Primary use:	Magazine 
-------------------------------------------------------------------*/
@import "reset.css";
@import "layout.css";
@import "colors.css";
@import "typography.css";
@import "flash.css";
/* @import "debugging.css"; */</code></pre>

For large projects or large development team it is also useful to have a <strong>brief update log</strong> and some additional information about the project — e.g. you can put the information about who is this CSS-file assigned to and what is its primary use (e.g. <em>Smashing Magazine, Smashing Jobs</em> etc.).

Additionally, you can include a debugging CSS-code to take care of diagnostic styling in case you run in some problems. Consider using Eric Meyer's <a href="https://meyerweb.com/eric/thoughts/2007/09/07/diagnostic-styling/">Diagnostic Styling</a> as a debugging stylesheet to test your CSS-code and fix problems.</p>

## 2\. Define a table of contents

To keep an overview of the structure of your code, you might want to consider defining a table of contents in the beginning of your CSS-files. One possibility of integrating a table of contents is to display a <strong>tree overview</strong> of your layout with IDs and classes used in each branch of the tree. You may want to use some keywords such as <em>header-section</em> or <em>content-group</em> to be able to jump to specific code immediately.

You may also select some important elements you are likely to change frequently — after the project is released. These classes and IDs may also appear in your table of contents, so once you'll need to find them you'll find them immediately — without scanning your whole code or remembering what class or ID you once used.

<pre><code class="language-css">/*------------------------------------------------------------------
[Layout]

* body
	+ Header / #header
	+ Content / #content
		- Left column / #leftcolumn
		- Right column / #rightcolumn
		- Sidebar / #sidebar
			- RSS / #rss
			- Search / #search
			- Boxes / .box
			- Sideblog / #sideblog
	+ Footer / #footer

Navigation	  #navbar
Advertisements	  .ads
Content header	  h2
-------------------------------------------------------------------*/</code></pre>

...or like this:

<pre><code class="language-css">/*------------------------------------------------------------------
[Table of contents]

1. Body
	2. Header / #header
		2.1. Navigation / #navbar
	3. Content / #content
		3.1. Left column / #leftcolumn
		3.2. Right column / #rightcolumn
		3.3. Sidebar / #sidebar
			3.3.1. RSS / #rss
			3.3.2. Search / #search
			3.3.3. Boxes / .box
			3.3.4. Sideblog / #sideblog
			3.3.5. Advertisements / .ads
	4. Footer / #footer
-------------------------------------------------------------------*/</code></pre>

Another approach is to use <strong>simple enumeration without indentation</strong>. In the exampe below, once you need to jump to the RSS-section you simply use a search tool to find <em>8. RSS</em> in your code. That's easy, quick and effective.

<pre><code class="language-css">/*------------------------------------------------------------------
[Table of contents]

1. Body
2. Header / #header
3. Navigation / #navbar
4. Content / #content
5. Left column / #leftcolumn
6. Right column / #rightcolumn
7. Sidebar / #sidebar
8. RSS / #rss
9. Search / #search
10. Boxes / .box
11. Sideblog / #sideblog
12. Advertisements / .ads
13. Footer / #footer
-------------------------------------------------------------------*/
&lt;!-- some CSS-code --&gt;</code></pre>

<pre><code class="language-css">/*------------------------------------------------------------------
[8. RSS / #rss]
*/
#rss { ... }
#rss img { ... }</code></pre>

Defining a table of contents you make it particularly easier for other people to read and understand your code. For large projects you may also print it out and have it in front of you when reading the code. When working in team, this advantage shouldn't be underestimated. It can save a lot of time — for you and your colleagues.</p>

## 3\. Define your colors and typography

Since we don't have CSS constants yet, we need to figure out some way to get a quick reference of "variables" we are using. In web development colors and typography can often be considered as "constants" — fixed values that are used throughout the code multiple times.

As Rachel Andrew <a href="https://24ways.org/2006/faster-development-with-css-constants">states</a>, "one way to get round the lack of constants in CSS is to create some definitions at the top of your CSS file in comments, to define <em>constants</em>. A common use for this is to create a <strong>color glossary</strong>. This means that you have a quick reference to the colors used in the site to avoid using alternates by mistake and, if you need to change the colors, you have a quick list to go down and do a search and replace.”

<pre><code class="language-css">/*------------------------------------------------------------------
# [Color codes]

# Dark grey (text): #333333
# Dark Blue (headings, links) #000066
# Mid Blue (header) #333399
# Light blue (top navigation) #CCCCFF
# Mid grey: #666666
# */</code></pre>

Alternatively, you can also describe color codes used in your layout. For a given color, you can display sections of your site which are using this color. Or vice versa — for a given design element you can describe the colors which are used there.

<pre><code class="language-css">/*------------------------------------------------------------------
[Color codes]

Background:	#ffffff (white)
Content:	#1e1e1e (light black)
Header h1:	#9caa3b (green)
Header h2:	#ee4117 (red)
Footer:		#b5cede (dark black)

a (standard):	#0040b6 (dark blue)
a (visited):	#5999de (light blue)
a (active):	#cc0000 (pink)
-------------------------------------------------------------------*/</code></pre>

The same holds for typography. You can also add some important notes to understand the "system" behind your definitions.

<pre><code class="language-css">/*------------------------------------------------------------------
[Typography]

Body copy:		1.2em/1.6em Verdana, Helvetica, Arial, Geneva, sans-serif;
Headers:		2.7em/1.3em Helvetica, Arial, "Lucida Sans Unicode", Verdana, sans-serif;
Input, textarea:	1.1em Helvetica, Verdana, Geneva, Arial, sans-serif;
Sidebar heading:	1.5em Helvetica, Trebuchet MS, Arial, sans-serif;

Notes:	decreasing heading by 0.4em with every subsequent heading level
-------------------------------------------------------------------*/</code></pre>

## 4\. Order CSS properties

When writing the code often it's useful to apply some special formatting to order CSS properties — to make the code more readable, more structured and therefore more intuitive. There is a variety of grouping schemes developers use in their projects. Some developers tend to put colors and fonts first; other developers prefer to put "more important" assignments such as those related to positioning and floats first. Similarly, elements are also often sorted according to the topology of the site and the <strong>structure of the layout</strong>. This approach can be applied to CSS selectors as well:

<pre><code class="language-css">body,
	h1, h2, h3,
	p, ul, li,
	form {
		border: 0;
		margin: 0;
		padding: 0;
	}</code></pre>

Some developers use a more interesting approach — they group properties in an <strong>alphabetical order</strong>. <s>Here it's important to mention that alphabetizing CSS properties may lead to some problems in some browsers. You may need to make sure that no changes are produced as a result of your ordering manipulations.</s>

<pre><code class="language-css">body {
	background: #fdfdfd;
	color: #333;
	font-size: 1em;
	line-height: 1.4;
	margin: 0;
	padding: 0;
}</code></pre>

Whatever grouping format you are using, make sure you clearly define the format and the objective you want to achieve. Your colleagues will thank you for your efforts. And you'll thank them for sticking to your format.</p>

## 5\. Indentation is your friend!

For better overview of your code you might consider using <strong>one-liners for brief fragments of code</strong>. This style might produce messy results if you define more than 3 attributes for a given selector. However, used moderately, you can highlight dependencies between all elements of the same class. This technique will dramatically increase code readability when you have to find some specific element in your stylesheet.

<pre><code class="language-css">#main-column { display: inline; float: left; width: 30em; }
	#main-column h1 { font-family: Georgia, "Times New Roman", Times, serif; margin-bottom: 20px; }
	#main-column p { color: #333; }</code></pre>

You remember exactly what you did and can jump back in there and fix it. But what if you made a lot of changes that day, or you just simply can’t remember? Chris Coyier <a href="https://css-tricks.com/indent-css-changes-you-are-unsure-about/">suggests</a> an interesting solution for highlighting recent changes in your CSS-code. Simply <strong>indenting new or changed lines</strong> in your CSS you can make recent changes in your code more visible. You can as well use some comments keywords (e.g. <em>@new</em>) — you'll be able to jump to the occurrences of the keyword and undo changes once you've found some problems.

<pre><code class="language-css">#sidebar ul li a {
     display: block;
     background-color: #ccc;
          border-bottom: 1px solid #999; /* @new */
     margin: 3px 0 3px 0;
          padding: 3px; /* @new */
}</code></pre>

## Conclusion

CSS styleguides are helpful if and only if they are used properly. Keep in mind that you should remove every styleguide which doesn't effectively help you to get a better understanding of the code or achieve a well-structured code. Avoid too many styleguides for too many elements bundled in too many groups. Your goal is to achieve a readable and maintainable code. Stick to it and you'll save yourself a lot of trouble.</p>

## Sources and Resources

*   [CSS: Best Practices](https://www.louddog.com/bloggity/2008/03/css-best-practices.php)
*   [Indent CSS Changes You Are Unsure About](https://css-tricks.com/indent-css-changes-you-are-unsure-about/)
*   [70 Expert Ideas For Better CSS Coding](https://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/)
*   [CSS Formatting Screencast](https://css-tricks.com/videos/css-tricks-video-8.php)

