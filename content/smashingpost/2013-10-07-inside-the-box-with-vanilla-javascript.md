---
title: Thinking Inside The Box With Vanilla JavaScript
slug: inside-the-box-with-vanilla-javascript
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63cdb189-cb3a-4d69-b15f-4dc04655586d/illu-vanilla.jpg'
date: 2013-10-07T06:18:10.000Z
author: louis-lazaris
description: >-
  During the past four or five years of blogging regularly and doing research
  for other writing projects, I’ve come across probably thousands of articles on
  JavaScript.
categories:
  - Coding
  - JavaScript
  - Techniques
  - HTML
---
During the past four or five years of blogging regularly and doing research for other writing projects, I’ve come across probably thousands of articles on JavaScript.

To me, it seems that a big chunk of these articles can be divided into two very general categories:

1.  [jQuery](https://www.smashingmagazine.com/2014/05/mystery-jquery-object-syntax-basic-introduction/);
2.  Theory and concept articles focused on things like [IIFEs](https://benalman.com/news/2010/11/immediately-invoked-function-expression/), [closures](https://net.tutsplus.com/tutorials/javascript-ajax/closures-front-to-back/) and [design patterns](https://design patterns).

Yes, I’ve likely stumbled upon a ton of other articles that don’t fall into either of these categories or that are more specific. But somehow it feels that most of the ones that really get pushed in the community fall under one of the two categories above.

I think those articles are great, and I hope we see more of them. But <strong>sometimes the simplest JavaScript features are sitting right under our noses</strong> and we just haven’t had a lot of exposure to them. I’m talking about native, more-or-less cross-browser features that have been in the language for some time.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful jQuery Function Demos For Your Projects](https://www.smashingmagazine.com/2012/05/50-jquery-function-demos-for-aspiring-web-developers/)
*   [Developing Dependency Awareness](https://www.smashingmagazine.com/2016/05/developing-dependency-awareness/)
*   [7 JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)
*   [Scaling Down The BEM Methodology For Small Projects](https://www.smashingmagazine.com/2014/07/bem-methodology-for-small-projects/)

So, in this article, I won’t be talking about jQuery, and I won’t be looking at structural code concepts or patterns. Instead, I’m going to introduce you to some pure JavaScript features that you can use today and that you might not have ever considered before.</p>

{{% feature-panel %}}

## insertAdjacentHTML()

Years ago, Microsoft introduced a method called <code>insertAdjacentHTML()</code> as a way to insert a specified string of text as HTML or XML into a specific place in the DOM. This feature has been available in Internet Explorer (IE) since version 4. Let’s see how it works.

Suppose you have the following HTML:

<pre><code class="language-markup">
&lt;div id="box1"&gt;
    &lt;p&gt;Some example text&lt;/p&gt;
&lt;/div&gt;
&lt;div id="box2"&gt;
    &lt;p&gt;Some example text&lt;/p&gt;
&lt;/div&gt;
</code></pre>

And suppose you want to insert another snippet of HTML between <code>#box1</code> and <code>#box2</code>. You can do this quite easily using <code>insertAdjacentHTML()</code>:

<pre><code class="language-javascript">
var box2 = document.getElementById("box2");
box2.insertAdjacentHTML('beforebegin', '&lt;div&gt;&lt;p&gt;This gets inserted.&lt;/p&gt;&lt;/div&gt;');
</code></pre>

With that, the generated DOM ends up like this:

<pre><code class="language-markup">
&lt;div id="box1"&gt;
    &lt;p&gt;Some example text&lt;/p&gt;
&lt;/div&gt;
&lt;div&gt;&lt;p&gt;This gets inserted.&lt;/p&gt;&lt;/div&gt;
&lt;div id="box2"&gt;
    &lt;p&gt;Some example text&lt;/p&gt;
&lt;/div&gt;
</code></pre>

*   [View a simple demo.](https://jsbin.com/otIZApI/1/edit?html,js,output)

The <code>insertAdjacentHTML()</code> method takes two parameters. The first defines where you want to place the HTML, relative to the targeted element (in this case, the <code>#box2</code> element). This may be one of the following four string values:

*   `beforebegin` The HTML would be placed immediately before the element, as a sibling.
*   `afterbegin` The HTML would be placed inside the element, before its first child.
*   `beforeend` The HTML would be placed inside the element, after its last child.
*   `afterend` The HTML would be placed immediately after the element, as a sibling.

Again, <strong>these are string values, not keywords</strong>, so they must be placed inside of single or double quotes.

The second parameter is the string you want to insert, also placed in quotes (or else it would be a variable holding a string that was previously defined). Note that it should be a string, not a DOM element or element collection; so, it could just be text, with no actual markup.

<code>insertAdjacentHTML()</code> has, as outlined in a <a href="https://hacks.mozilla.org/2011/11/insertadjacenthtml-enables-faster-html-snippet-injection/">post on Mozilla Hacks</a>, a couple of advantages over something more conventional, like <code>innerHTML()</code>: It does not corrupt the existing DOM elements, and it performs better.

And if you’re wondering why this one hasn’t received a lot of attention so far, despite being well supported in all in-use versions of IE, the reason is probably that, as mentioned in the Mozilla Hacks article, it was not added to Firefox until version 8. Because all other major browsers support this, and Firefox users have been auto-updating since version 5, it’s quite safe to use.

For more on this method:

*   “[insertAdjacentHTML()](https://domparsing.spec.whatwg.org/#insertadjacenthtml()),” in the “DOM Parsing and Serialization” specification, WHATWG
*   “[Element.insertAdjacentHTML](https://developer.mozilla.org/en-US/docs/Web/API/element.insertAdjacentHTML),” Mozilla Developer Network

## getBoundingClientRect()

You can obtain the coordinates and, by extension, the dimensions of any element on the page using another lesser-known method, the <code>getBoundingClientRect()</code> method.

Here’s an example of how it might be used:

<pre><code class="language-javascript">
var box = document.getElementById('box'),
    x, y, w;

x = box.getBoundingClientRect().left;
y = box.getBoundingClientRect().top;

if (box.getBoundingClientRect().width) {
  w = box.getBoundingClientRect().width; // for modern browsers
} else {
  w = box.offsetWidth; // for oldIE
}

console.log(x, y, w);
</code></pre>

*   [View a demo.](https://jsbin.com/aKAdISE/1/edit?html,js,output)

Here, we’ve targeted an element with an ID of <code>box</code>, and we’re accessing three properties of the <code>getBoundingClientRect()</code> method for the <code>#box</code> element. Here’s a summary of six fairly self-explanatory properties that this method exposes:

*   `top` How many pixels the top edge of the element is from the topmost edge of the viewport
*   `left` How many pixels the left edge of the element is from the leftmost edge of the viewport
*   `right` How many pixels the right edge of the element is from the leftmost edge of the viewport
*   `bottom` How many pixels the bottom edge of the element is from the topmost edge of the viewport
*   `width` The width of the element
*   `height` The height of the element

<strong>All of these properties are read-only.</strong> And notice that the coordinate properties (<code>top</code>, <code>left</code>, <code>right</code> and <code>bottom</code>) are all relative to the top-left of the viewport.

What about the <code>if/else</code> in the example from above? IE 6 to 8 don’t support the <code>width</code> and <code>height</code> properties; so, if you want full cross-browser support for those, you’ll have to use <code>offsetWidth</code> and/or <code>offsetHeight</code>.

As with <code>insertAdjacentHTML()</code>, despite the lack of support for <code>width</code> and <code>height</code>, this method has been supported in IE since ancient times, and it has support everywhere else that’s relevant, so it’s pretty safe to use.

I will concede something here: Getting the coordinates of an element using offset-based values (such as <code>offsetWidth</code>) is actually <a href="https://web.archive.org/web/20150902040948/https://jsperf.com:80/getboundingclientrect-vs-jquery/5">faster than using <code>getBoundingClientRect()</code></a>. Note, however, that offset-based values will always round to the nearest integer, whereas <code>getBoundingClientRect()</code>’s properties will return fractional values.

For more info:

*   “[Element.getBoundingClientRect](https://developer.mozilla.org/en-US/docs/Web/API/element.getBoundingClientRect),” Mozilla Developer Network
*   “[getBoundingClientRect Is Awesome](https://ejohn.org/blog/getboundingclientrect-is-awesome/),” John Resig

## The &lt;table&gt; API

If you’ve ever manipulated elements on the fly with JavaScript, then you’ve likely used methods such as <code>createElement</code>, <code>removeChild</code>, <code>parentNode</code> and related features. And you can manipulate HTML tables in this way, too.

But you may not realize that there is a very specific API for creating and manipulating HTML tables with JavaScript, and it has very good browser support. Let’s take a quick look at some of the methods and properties available with this API.

All of the following methods are available to be used on any HTML <code>table</code> element:

*   `insertRow()`
*   `deleteRow()`
*   `insertCell()`
*   `deleteCell()`
*   `createCaption()`
*   `deleteCaption()`
*   `createTHead()`
*   `deleteTHead()`

And then there are the following properties:

*   `caption`
*   `tHead`
*   `tFoot`
*   `rows`
*   `rows.cells`

<strong>With these features, we can create an entire table</strong>, including rows, cells, a caption and cell content. Here’s an example:

<pre><code class="language-javascript">
var table = document.createElement('table'),
    tbody = document.createElement('tbody'),
    i, rowcount;

table.appendChild(tbody);

for (i = 0; i &lt;= 9; i++) {
  rowcount = i + 1;
  tbody.insertRow(i);
  tbody.rows[i].insertCell(0);
  tbody.rows[i].insertCell(1);
  tbody.rows[i].insertCell(2);
  tbody.rows[i].cells[0].appendChild(document.createTextNode('Row ' + rowcount + ', Cell 1'));
  tbody.rows[i].cells[1].appendChild(document.createTextNode('Row 1, Cell 2'));
  tbody.rows[i].cells[2].appendChild(document.createTextNode('Row 1, Cell 3'));
}

table.createCaption();
table.caption.appendChild(document.createTextNode('A DOM-Generated Table'));

document.body.appendChild(table);
</code></pre>

*   [View a demo.](https://jsbin.com/OcuFITE/1/edit?html,js,output)

The script above combines some customary core DOM methods with methods and properties of the <code>HTMLTableElement</code> API. The same code written without the table API might be considerably more complex and, thus, harder to read and maintain.

Once again, these table-related features have support all the way back to IE 7 (and probably earlier) and everywhere else that’s relevant, so feel free to use these methods and properties where you see fit.

For more info:

*   “[HTMLTableElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLTableElement),” Mozilla Developer Network
*   “Tabular Data,” in the “HTML” specification, WHATWG

## Wrapping Up

This discussion of specific native JavaScript features has been a reminder of sorts. We can easily become comfortable with the features of a language that we know well, without looking deeper into the language’s syntax for simpler and more maintainable ways to solve our problems.

So, from time to time, look <em>inside</em> the box, so to speak. That is, investigate <a href="https://developer.mozilla.org/en-US/docs/Web/API">all that vanilla JavaScript has to offer</a>, and <strong>try not to rely too much on plugins and libraries</strong>, which can unnecessarily bloat your code.

<em>(Credits of image on front page: <a href="https://www.flickr.com/photos/nyuhuhuu/4443886636/">nyuhuhuu</a></em>)

<em>(al ea)</em>

