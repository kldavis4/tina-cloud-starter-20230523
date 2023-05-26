---
title: The Bright (Near) Future of CSS
slug: the-bright-near-future-of-css
image: null
date: 2011-02-11T14:50:20.000Z
author: eric-meyer
description: >-
  In this article, the focus is on what's coming: styling techniques you'll use
  in the immediate and near-term future. From styling HTML 5 elements to
  rearranging layout based on display parameters to crazy selection patterns to
  transforming element layout, these are all techniques that you may use
  tomorrow, next month, or next year. With partial browser support, they're all
  on the cutting edge of Web design.
categories:
  - Coding
  - CSS
  - Techniques
---
In this article, the focus is on what's coming: styling techniques you'll use in the immediate and near-term future. From styling HTML 5 elements to rearranging layout based on display parameters to crazy selection patterns to transforming element layout, these are all techniques that you may use tomorrow, next month, or next year. With partial browser support, they're all on the cutting edge of Web design.

Accordingly, be careful not to get cut! A number of useful sites can help you figure out the exact syntaxes and patterns you need to use these techniques.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Future Of CSS: Embracing The Machine](https://www.smashingmagazine.com/2011/11/the-future-of-css-embracing-the-machine/)
*   [Laying Out A Flexible Future For Web Design With Flexbox](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/)
*   [The Future Of CSS: Experimental CSS Properties](https://www.smashingmagazine.com/2011/05/the-future-of-css-experimental-css-properties/)

Furthermore, a number of JavaScript libraries can extend support for advanced CSS back into older browsers, in some cases as far back as IE/Win 5.5. Some are very narrowly focused on certain browser families, whereas others are more broadly meant to allow support in all known browsers. These can be useful in cases where your visitors haven't quite caught up with the times but you don't want them to miss out on all the fun. (Some of these libraries are <a href="https://css3pie.com/">CSS3 PIE</a>, <a href="https://www.useragentman.com/blog/csssandpaper-a-css3-javascript-library/">cssSandpaper</a>, <a href="https://selectivizr.com/">:select[ivizr]</a>, <a href="https://code.google.com/p/ie7-js/">ie7-js</a>, <a href="https://ecsstender.com/">eCSStender</a>).

{{% feature-panel %}}

There are also a good many CSS enhancements available as plug-ins for popular JavaScript libraries such as jQuery. If you're a user of such a library, definitely do some digging to see what's been created. Again: Be careful! While these techniques are powerful and can deliver a lot of power to your pages, you need to test them thoroughly in the browsers of the day to make sure you didn't just accidentally make the page completely unreadable in older browsers.</p>

### Styling HTML 5

Styling HTML 5 is really no different than styling HTML 4. There are a bunch of new elements, but styling them is basically the same as styling any other element. They generate the same boxes as any other <code>div</code>, <code>span</code>, <code>h2</code>, <code>a</code>, or what have you.

The HTML 5 specification is still being worked on as of this writing, so this may change a bit over time, but the following declarations may be of use to older browsers that don't know quite what to do with the new elements.

<pre><code class="language-css">article, aside, canvas, details, embed, figcaption, figure, footer, header, hgroup, menu, nav, section, summary {
  display: block;
}
command, datalist, keygen, mark, meter, progress, rp, rt, ruby, time, wbr {
  display: inline;
}</code></pre>

You may have noticed that I left out two fairly important new elements: <code>audio</code> and <code>video</code>. That's because it's hard to know exactly how to treat them. Block? Inline? All depends on how you plan to use them. Anyway, you can place them in the declaration that makes the most sense to you.

But what about really old browsers, like IE6? (Note I said "old," not "unused." In an interesting subversion of popular culture, browser popularity has very little to do with age.) For those, you need to use a bit of JavaScript in order to get the browser to recognize them and therefore be able to style them. There’s a <a href="https://remysharp.com/downloads/html5.js">nice little script</a> that auto-forces old versions of IE to play nicely with HTML 5 elements. If you’re going to use and style them, you should definitely grab that script and put it to use.

Once you've gotten your browser ducks in a row and quacking "The Threepenny Opera," you can get down to styling. Remember: There’s really nothing new about styling with these new elements. For example:

<pre><code class="language-css">figure {
  float: left;
  border: 1px solid gray;
  padding: 0.25em;
  margin: 0 0 1.5em 1em;
}
figcaption {
  text-align: center;
  font: italic 0.9em Georgia, "Times New Roman", Times, serif;
}</code></pre>

<pre><code class="language-markup tmp-xml"> </code></pre>

<figure>&lt;img src="splash.jpg" alt="A toddler’s face is obscured by a rippled and dimpled wall of water thrown up by her hands slapping into the surface of the swimming pool in whose waters she sits."&gt;<figcaption>SPLASH SPLASH SPLASH!!!</figcaption>&nbsp;

</figure>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4463b609-ac42-4e81-91f5-373d0aa86fef/fig0701-large.jpg"><img loading="lazy" decoding="async" class="86476" title="Figure 7-1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc56573a-1e81-47ea-a1ea-0a70d2ccaa3c/fig0701.jpg" alt="" width="500" height="438" /></a><br>
<em>Figure 7-1: A styled HTML 5 figure and figure caption.</em>

### Classing like HTML 5

Perhaps you like the new semantics of HTML 5, but you’re just not ready to take your sites to full-on HTML 5. Maybe your site’s user base is mostly older browsers and you’d rather stick to known quantities like HTML 4 or XHTML. Not to worry: You can have the best of both worlds with the venerable <code>class</code> attribute.

This approach was documented by Jon Tan in his <a href="https://jontangerine.com/log/2008/03/preparing-for-html5-with-semantic-class-names">article</a>. The basic idea is to use old-school elements like <code>div</code> and <code>span</code>, and add to them classes that exactly mirror the element names in HTML 5. Here’s a code example.

<pre><code class="language-css">.figure {
  float: left;
  border: 1px solid gray;
  padding: 0.25em;
  margin: 0 0 1.5em 1em;
}
.figcaption {
  text-align: center;
  font: italic 0.9em Georgia, "Times New Roman", Times, serif;
}</code></pre>

<pre><code class="language-markup tmp-xml"> </code></pre>

<div class="figure">&lt;img src="spring.jpg" alt="A small child with twin pigtail braids, her back to the camera, swings away from the camera on a playground swingset while the late afternoon sun peeks over the crossbar of the swingset."&gt; &lt;div class="figcaption"&gt;Swinging into spring.&lt;/div&gt;</div><br>
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84d0267a-9a4e-4454-b160-26d5f0f78486/fig0702-large.jpg"><img loading="lazy" decoding="async" class="86533" title="fig0702" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b312a0de-048b-40cc-9d6c-162adc56da56/fig0702.jpg" alt="" width="500" height="442" /></a><br>
<em>Figure 7-2: A styled HTML 4-classed figure and figure caption.</em>

If you compare the styles there to those found in the preceding section, you’ll see that the only difference is that the names <code>figure</code> and <code>figcaption</code> are preceded by periods — thus marking them as class names. The markup is a little different, of course, though it’s the same basic structure.

The advantage of this approach is that if you have these styles in place at the point when you decide you can convert to HTML 5, then all you need to do is change your markup to use HTML 5 elements instead of classed <code>div</code>s and then strip off the periods to turn the class selectors into element selectors. That’s it. Easy as cake!

### Media Queries

This could honestly be its own article, or possibly even its own book. Thus, what follows will necessarily be just a brief taste of the possibilities. You should definitely follow up with more research, because in a lot of ways this is the future of Web styling.

The point of media queries is to set up conditional blocks of styles that will apply in different media environments. For example, you could write one set of styles for portrait displays and another for landscape displays. You might change the colors based on the bit depth of the display. You could change the font based on the pixel density of display. You might even rearrange the page’s layout depending on the width or number of pixels available in the display.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81bc2281-84e8-4df7-91a0-0d8ac86152bc/fig0703-large.jpg"><img loading="lazy" decoding="async" class="86535" title="fig0703" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b178156-4380-440d-8c7c-9ed22f6de5ac/fig0703.jpg" alt="Figure 7-3: A basic three-column layout." width="500" height="374" /></a><br>
<em>Figure 7-3: A basic three-column layout.</em>

How? Consider some basic layout styles for a three-column layout:

<pre><code class="language-css">body {
  background: #FFF;
  color: #000;
    font: small Arial, sans-serif;
}
.col {
  position: relative;
    margin: 3em 1%;
    padding: 0.5em 1.5%;
    border: 1px solid #aaa;
    border-width: 1px 1px 0 1px;
  float: right;
  width: 20%;
}
#two {
  width: 40%;
}
#footer {
  clear: both;
}</code></pre>

As nice as this might be (in a minimalist sort of way), it is likely to run into trouble on smaller—which is to say, narrower—displays. What if you could magically change to a two-column layout on such displays?

Well, you can. First, restrict the three-column layout to environments that are more than 800 pixels across. This is done by splitting the layout bits into their own declarations:

<pre><code class="language-css">body {
  background: #fff;
  color: #000;
    font: small Arial, sans-serif;
}
.col {
  position: relative;
    margin: 3em 1%;
    padding: 0.5em 1.5%;
    border: 1px solid #aaa;
    border-width: 1px 1px 0 1px;
}
#footer {
  clear: both;
}
.col {
  float: right;
  width: 20%;
}
#two {
  width: 40%;
}</code></pre>

Then wrap those last two declarations in a media query:

<pre><code class="language-css">@media all and (min-width: 800px) {
    .col {
      float: right;
      width: 20%;
    }
    #two {
      width: 40%;
      }
}</code></pre>

What that says is “the rules inside this curly-brace block apply in all media that have a minimum display width of 800 pixels.” Anything below that, no matter the medium, and the rules inside the block will be ignored. Note the parentheses around the <code>min-width</code> term and its value. These are necessary any time you have a term and value (which are referred to as an expression).

At this point, nothing will really change unless you shrink the browser window until it offers fewer than 800 pixels across to the document. At that point, the columns stop floating altogether.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a75cbf66-700d-4797-9da7-c47f359a136d/fig0704-large.jpg"><img loading="lazy" decoding="async" class="86536" title="fig0704" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02db61be-a8a2-4869-bb81-a80684103c04/fig0704.jpg" alt="Figure 7-4: What happens below 800 pixels." width="500" height="369" /></a><br>
<em>Figure 7-4: What happens below 800 pixels.</em>

What you can do at this point is write another media-query block of layout rules that apply in narrower conditions. Say you want a two-column layout between 500 and 800 pixels):

<pre><code class="language-css">@media all and (min-width: 500px) and (max-width: 799px) {
    .col {
      float: left;
      width: 20%;
    }
    #two {
      float: right;
      width: 69%;
    }
    #three {
      clear: left;
      margin-top: 0;
    }
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9311c5ea-0a45-4314-b14c-730c606affde/fig0705-large.jpg"><img loading="lazy" decoding="async" class="86537" title="fig0705" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4663f554-6c18-4682-984e-14f8ef14e68f/fig0705.jpg" alt="Figure 7-5: The reworked layout, which shows between 500 and 800 pixels." width="500" height="369" /></a><br>
<em>Figure 7-5: The reworked layout, which shows between 500 and 800 pixels.</em>

And finally, you can apply some single-column styles for any medium with fewer than 500 pixels of display width:

<pre><code class="language-css">@media all and (max-width: 499px) {
    #one {
      text-align: center;
    }
    #one li {
      display: inline;
      list-style: none;
    padding: 0 0.5em;
    border-right: 1px solid gray;
    line-height: 1.66;
  }
    #one li:last-child {
      border-right: 0;
    }
    #three {
      display: none;
    }
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b63ec7-1d5e-49b2-a2f9-b66e5500f49a/fig0706-large.jpg"><img loading="lazy" decoding="async" class="86538" title="fig0706" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f61e8a8-f40a-431b-890c-d922c07aa05e/fig0706.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-6: Single-column layout, which shows below 500 pixels.</em>

Note that in all these queries, layout styles are defined in relation to the display area of the browser window. More generically, they are defined in relation to the display area available to the document in any medium in which it is rendered. That means that if a printer, for example, is used to print the document and it has an available display area 784 pixels wide, then the two-column layout will be for printing.

To restrict the column shifting to screen media only, alter the queries, like so:

<pre><code class="language-css">@media screen and (min-width: 800px) {...}
@media screen and (min-width: 500px) and (max-width: 799px) {...}
@media screen and (max-width: 499px) {...}</code></pre>

But what if you want the three-column layout used in some non-screen media, like print and TV displays? Then add in those media using commas, like so:

<pre><code class="language-css">@media print, tv, screen and (min-width: 800px) {...}
@media screen and (min-width: 500px) and (max-width: 799px) {...}
@media screen and (max-width: 499px) {...}</code></pre>

The commas here act as logical ORs, so the first query reads “use these styles on print media OR TV media OR a display area on a screen medium where the display area is 800 pixels or more.”

And if you want the three-column layout used in all non-screen media? Add a statement to the first query using the not modifier saying “anything that isn’t screen.”

<pre><code class="language-css">@media not screen, screen and (min-width: 800px) {...}
@media screen and (min-width: 500px) and (max-width: 799px) {...}
@media screen and (max-width: 499px) {...}</code></pre>

As before, the comma joins the two in an <code>OR</code> statement, so it reads as “anything not on a screen medium OR a display area on a screen medium where the display area is 800 pixels or more.”

There is also an <code>only</code> modifier, so that a query can say something like <code>only print</code> or <code>only screen and (color)</code>. As of this writing, <code>not</code> and <code>only</code> are the only modifiers in media queries.

You aren’t restricted to pixels for the previous queries, by the way. You can use ems, centimeters, or any other valid length unit.

<em>Table 7-1: The base media query terms</em><br>
<table class="terms" style="border: 1px solid #ccc;border-collapse: collapse">
<thead>
<tr>
<td style="width: 100px">Term</td>
<td>Description</td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>width</strong></td>
<td>The width of the display area (e.g., a browser window).</td>
</tr>
<tr>
<td><strong>height</strong></td>
<td>The height of the display area (e.g., a browser window).</td>
</tr>
<tr>
<td><strong>device-width</strong></td>
<td>The width of the device’s display area (e.g., a desktop monitor or mobile device display).</td>
</tr>
<tr>
<td><strong>device-height</strong></td>
<td>The height of the device’s display area.</td>
</tr>
<tr>
<td><strong>orientation</strong></td>
<td>The way the display is oriented; the two values are portrait and landscape.</td>
</tr>
<tr>
<td><strong>aspect-ratio</strong></td>
<td>The ratio of the display area’s width to its height. Values are two integers separated by a forward slash.</td>
</tr>
<tr>
<td><strong>device-aspect-ratio</strong></td>
<td>The ratio of the device display’s width to its height. Values are two integers separated by a forward slash.</td>
</tr>
<tr>
<td><strong>color</strong></td>
<td>The color bit-depth of the display device. Values are unitless integers which refer to the bit depth. If no value is given, then any color display will match.</td>
</tr>
<tr>
<td><strong>color-index</strong></td>
<td>The number of colors maintained in the device’s “color lookup table.” Values are unitless integers.</td>
</tr>
<tr>
<td><strong>monochrome</strong></td>
<td>Applies to monochrome (or grayscale) devices.</td>
</tr>
<tr>
<td><strong>resolution</strong></td>
<td>The resolution of the device display. Values are expressed using units dpi or dpcm.</td>
</tr>
<tr>
<td><strong>scan</strong></td>
<td>The scanning type of a “TV” media device; the two values are progressive and interlace.</td>
</tr>
<tr>
<td><strong>grid</strong></td>
<td>Whether the device uses a grid display (e.g., a TTY device). Values are 0 and 1.</td>
</tr>
</tbody>
</table>

Table 7-1 shows all the query terms that can be used in constructing media queries. Note that almost all of these terms accept min- and max- prefixes (for example, <code>device-height</code> also has <code>min-device-height</code> and <code>max-device-height</code> cousins). The exceptions are <code>orientation</code>, <code>scan</code>, and <code>grid</code>.</p>

### Styling Occasional Children

There are times when you may want to select every second, third, fifth, eighth, or thirteenth element in a series. The most obvious cases are list items in a long list or rows (or columns) in a table, but there are as many cases as there are combinations of elements.

Consider one of the less obvious cases. Suppose you have a lot of quotes that you want to float in a sort of grid. The usual problem in these cases is that quotes of varying length can really break up the grid.

A classic solution here is to add a class to every fourth <code>div</code> (because that is what encloses each quote) and then <code>clear</code> it. Rather than clutter up the markup with classes, though, why not select every fourth <code>div</code>?

<pre><code class="language-css">.quotebox:nth-child(4n+1) {
  clear: left;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8bfef44-df67-4f43-94d5-2e8f1b5f95be/fig0707-large.jpg"><img loading="lazy" decoding="async" class="86539" title="fig0707" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a0c7954-25b5-423c-b88f-9117f8e89eb4/fig0707.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-7: The problem with floating variable-height elements.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f377529-6805-449c-9ee3-98ad454d15d3/fig0708-large.jpg"><img loading="lazy" decoding="async" class="86540" title="fig0708" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/993ecbe8-3ac7-48d6-b359-eef3d74d0eb5/fig0708.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-8: Clearing every fourth child.</em>

A quick explanation of the <code>4n+1</code> part:

*   `4n` means every element that can be described by the formula `4` times `n`, where n describes the series 0, 1, 2, 3, 4… .That yields elements number 0, 4, 8, 12, 16, and so on. (Similarly, `3n` would yield the series 0, 3, 6, 9, 12… .)
*   But there is no zeroth element; elements start with the first (that is, element number 1). So you have to add + 1 in order to select the first, fifth, ninth, and so forth elements.

Yes, you read that right: the <code>:nth-child()</code> pattern starts counting from 0, but the elements start counting from 1. That’s why <code>+ 1</code> will be a feature of most <code>:nth-child()</code> selectors.

The great thing with this kind of selector is that if you want to change from selecting every fourth element to every third element, you need only change a single number.

<pre><code class="language-css">.quotebox:nth-child(3n+1) {
  clear: left;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f20c11ac-f8a3-404a-9427-928036996aa3/fig0709-large.jpg"><img loading="lazy" decoding="async" class="86541" title="fig0709" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f26a29c-b4dc-47a2-8140-512bff6f605e/fig0709.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-9: Clearing every third child.</em>

That might seem pretty nifty on its own, but it gets better. If you combine this approach with media queries, you get an adaptable grid-like layout.

<pre><code class="language-css">@media all and (min-width: 75.51em) {
    .quotebox:nth-child(5n+1) {
      clear: left;
    }
}
@media all and (min-width: 60.01em) and (max-width: 75em) {
    .quotebox:nth-child(4n+1) {
      clear: left;
    }
}
@media all and (min-width: 45.51em) and (max-width: 60em) {
    .quotebox:nth-child(3n+1) {
      clear: left;
    }
}
@media all and (min-width: 30.01em) and (max-width: 45.5em) {
    .quotebox:nth-child(2n+1) {
      clear: left;
    }
}
@media all and (max-width: 30em) {
    .quotebox {
      float: none;
    }
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b064f79e-abf4-46b7-b51e-f2a005e392e9/fig0710-large.jpg"><img loading="lazy" decoding="async" class="86542" title="fig0710" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5bf471-eea2-41a7-a5e5-891d5f3f2f1a/fig0710.jpg" alt="" width="500" height="690" /></a><br>
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9dc4903-3f6c-47ff-9bd7-7b648d357b45/fig0710b-large.jpg"><img loading="lazy" decoding="async" class="86543" title="fig0710b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac62450b-a9b9-4959-847f-b193c30fccc2/fig0710b.jpg" alt="" width="500" height="290" /></a>

<em>Figure 7-10: Two views of an adaptable floated grid.</em>

Note that this particular set of queries is based on the width of the display area of the browser as measured in ems. That helps make the layout much more adaptable to changes of text size and browser window.

If you’re interested in selecting every other element — let's say, every other table row — there are some more human alternatives to <code>2n+1</code>. You can select even-numbered or odd-numbered children using <code>:nth-child(even)</code> and <code>:nth-child(odd)</code>, as in this example.

<pre><code class="language-css">tr:nth-child(odd) {
  background: #eef;
}</code></pre>

### Styling Occasional Columns

It’s easy enough to select alternate table rows for styling, but how about table columns? Actually, that’s just as easy, thanks to the <code>:nth-child</code> and <code>:nth-of-type</code> selectors.

In a simple table with rows consisting of nothing but data cells (those are <code>td</code> elements), you can select every other column like so:

<pre><code class="language-css">td:nth-child(odd) {
  background: #fed;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f8a63ca-135b-4f16-9c5d-9bcf6bdd0d31/fig0711-large.jpg"><img loading="lazy" decoding="async" class="86544" title="fig0711" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/918dd422-d854-4915-b8b8-556530d1dac5/fig0711.jpg" alt="" width="500" height="315" /></a><br>
<em>Figure 7-11: Styling the odd-numbered columns.</em>

Want to fill in the alternate ones!

<pre><code class="language-css">td:nth-child(odd) {
  background: #fed;
}
td:nth-child(even) {
  background: #def;
}</code></pre>

If you’re after every third, fourth, fifth, or similarly spaced-out interval, then you need the <code>n+1</code> pattern.

<pre><code class="language-css">td:nth-child(3n+1) {
  background: #edf;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1254abdc-dfe6-4514-84ea-87409005cb8a/fig0712-large.jpg"><img loading="lazy" decoding="async" class="86545" title="fig0712" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17b21735-1cab-4d26-b900-fc9d5d2edb4c/fig0712.jpg" alt="" width="500" height="311" /></a><br>
<em>Figure 7-12: Styling both odd- and even-numbered columns.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31073732-f490-46e5-b6e1-01cc2f5f84eb/fig0713-large.jpg"><img loading="lazy" decoding="async" class="86546" title="fig0713" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d1ea4a1-eb27-43d2-b913-807f9a6a0949/fig0713.jpg" alt="" width="500" height="310" /></a><br>
<em>Figure 7-13: Styling every third data column.</em>

That’s all relatively straightforward. Now, what happens when you put a <code>th</code> at the beginning of each row? In one sense, nothing. The columns that are selected don’t change; you’re still selecting the first, fourth, seventh, and so on children of the <code>tr</code> elements. In another sense, the selected columns are shifted, because you’re no longer selecting the first, fourth, seventh, and so on data columns. You’re selecting the third, sixth, and so on data columns. The first column, which is composed of <code>th</code> element, doesn’t get selected at all because the selector only refers to <code>td</code> elements.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c1589ac-bed8-49c7-9976-544e2cef356a/fig0714-large.jpg"><img loading="lazy" decoding="async" class="86547" title="fig0714" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0b0b316-4c08-402b-9960-406f82a28548/fig0714.jpg" alt="" width="500" height="274" /></a><br>
<em>Figure 7-14: Disrupting the pattern with row headers.</em>

To adjust, you could change the terms of the <code>:nth-child</code> selector:

<pre><code class="language-css">td:nth-child(3n+2) {
  background: #edf;
}</code></pre>

Alternatively, you could keep the original pattern and switch from using <code>:nth-child</code> to <code>:nth-of-type</code>:

<pre><code class="language-css">td:nth-of-type(3n+1) {
  background: #fde;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72829381-eef6-4400-9775-d6518d06e38e/fig0715-large.jpg"><img loading="lazy" decoding="async" class="86548" title="fig0715" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdd34b0-3381-496a-ba7e-c1c7bbc96df0/fig0715.jpg" alt="" width="500" height="274" /></a><br>
<em>Figure 7-15: Restoring the pattern by adjusting the selection formula.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0035ab3-aef9-4c52-917e-79b2dfd880d8/fig0716-large.jpg"><img loading="lazy" decoding="async" class="86549" title="fig0716" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80996aa8-3f26-459e-862a-02b0800370af/fig0716.jpg" alt="" width="500" height="271" /></a><br>
<em>Figure 7-16: Restoring the pattern with <code>:nth-of-type</code>.</em>

This works because it selects every <code>nth</code> element of a given type (in this case, <code>td</code> elements) that shares a parent element with the others. Think of it as <code>:nth-child</code> that also skips any elements that aren’t named in the <code>:nth-child</code> selector.</p>

### RGB Alpha Color

Color values are probably one of the most familiar things in all of CSS; some people are to the point of being able to estimate a color’s appearance based on its hexadecimal representation. (Go on, try it: <code>#e07713</code>.) It’s not quite as common to use the <code>rgb()</code> notation for colors, but they’re still pretty popular.

In CSS 3, the <code>rgb()</code> notation is joined by <code>rgba()</code> notation. The <code>a</code> part of the value is the alpha, as in alpha channel, as in transparency. Thus you can supply a color that is partly see-through:

<pre><code class="language-markup tmp-xml">.box1 {
  background: rgb(255,255,255);
}
.box2 {
  background: rgba(255,255,255,0.5);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc55784-9ea9-4d25-a455-6229f66a8c94/fig0717-large.jpg"><img loading="lazy" decoding="async" class="86550" title="fig0717" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b5da3d-ae68-404e-8f07-7e7cbd0cb9bc/fig0717.jpg" alt="" width="500" height="344" /></a><br>
<em>Figure 7-17: Boxes with opaque and translucent RGB backgrounds.</em>

You can also use the percentage form of RGB color values in RGBA:

<pre><code class="language-css">.box1 {
  background: rgb(100%,100%,100%);
}
.box2 {
  background: rgba(100%,100%,100%,0.5);
}</code></pre>

The alpha value is always represented as a number between 0 and 1 inclusive, with <code>0</code> meaning “no opacity at all” and 1 meaning “fully opaque.” So half-opaque (and thus half-transparent) is <code>0.5</code>. You can’t put a percentage in there for historical reasons that are too messy to get into here.

If you supply a number outside the 0 to 1 range, it will (in the words of the specification) be “clamped” to the allowed range. So if you give an alpha value of <code>4.2</code>, the browser will treat it as if you’d written <code>1</code>. Also, it isn’t clear what should happen when an alpha of <code>0</code> is used. Since the color is fully transparent, what will happen to, say, invisible text? Can you select it? If it’s used on a link, is the link clickable? Both are interesting questions with no definitive answers. So be careful.

RGBA colors can be used with any property that accepts a color value, such as <code>color</code> and <code>background-color</code>. To keep older browsers from puking on themselves, it’s advisable to supply a non-alpha color before the alpha color. That would take a form like so:

<pre><code class="language-css">{
  color: #000;
  color: rgba(0,0,0,0.75);
}</code></pre>

The older browsers see the first value and know what to do with it. Then they see the second value and don’t know what to do with it, so they ignore it. That way, at least older browsers get black text. Modern browsers, on the other hand, understand both values and thanks to the cascade, override the first with the second.

Note that <strong>there is no hexadecimal form of RGBA colors</strong>. Thus, you cannot write <code>#00000080</code> and expect half-opaque black.</p>

### HSL and HSL Alpha Color

A close cousin to RGBA values are the HSLA values, and an even closer cousin to them are HSL colors. These are new to CSS 3, and will be a delightful addition to many designers.

For those not familiar with HSL, the letters stand for Hue-Saturation-Lightness. Even if you didn’t know the name, you’ve probably worked with HSL colors in a color picker.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbe8042c-1644-492e-8019-c0643a240b86/fig0718-large.jpg"><img loading="lazy" decoding="async" class="86551" title="fig0718" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35d293a7-75ac-49e6-8794-1fd8ecc7c202/fig0718.jpg" alt="" width="500" height="459" /></a><br>
<em>Figure 7-18: An HSL color picker.</em>

The hue is represented as a unitless number corresponding to the hue angle on a color wheel. Saturation and lightness are both percentages, and alpha is (as with RGBA) a number between 0 and 1 inclusive. In practice, you can use HSL colors anywhere a color value is accepted. Consider the following rules, which create the equivalent effect.

<pre><code class="language-css">.box1 {
  background: hsl(0,0%,100%);
}
.box2 {
  background: hsla(0,0%,100%,0.5);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0275481a-501d-46ad-a1c4-781d6a44023c/fig0719-large.jpg"><img loading="lazy" decoding="async" class="86552" title="fig0719" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29589d4d-ff0f-4eb6-bfd5-59308dba3643/fig0719.jpg" alt="" width="500" height="428" /></a><br>
<em>Figure 7-19: Various HSL color tables.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e45c1df-0d7e-4175-8355-4ce0e2e66867/fig0720-large.jpg"><img loading="lazy" decoding="async" class="86553" title="fig0720" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea4d1bf5-ce41-4f58-a10a-14718f6c4b23/fig0720.jpg" alt="" width="500" height="330" /></a><br>
<em>Figure 7-20: Boxes with opaque and translucent HSL backgrounds.</em>

You can do old-browser fallbacks with regular RGB values, though having to specify an RGB color and then HSL color does sort of detract from the point of using HSL in the first place. HSL allows you to get away from RGB altogether.</p>

### Shadowy Styles

Ah, drop shadows. Remember drop shadows? In the mid-90’s, everything had a drop shadow. Of course, back then the shadows were baked into images and constructed with tables even more tortuously convoluted than usual. Now you can relive the glory days with some fairly simple CSS. There are actually two properties available: <code>text-shadow</code> and <code>box-shadow</code>.

Take the former first. The following CSS will result:

<pre><code class="language-css">h1 {
  text-shadow: gray 0.33em 0.25em 0.1em;
}</code></pre>

The first length (<code>0.33em</code>) indicates a horizontal offset; the second (<code>0.25em</code>), a vertical offset. The third is a blur radius, which is the degree by which the shadow is blurred. These values can use any length unit, so if you want to do all your shadow offsets and blurs in pixels, go to town. Blurs can’t be negative, but offsets can: A negative horizontal offset will push the shadow to the left, and a negative vertical offset will go upward.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1091d639-5ed3-4ff1-a76d-683c0192d83d/fig0721-large.jpg"><img loading="lazy" decoding="async" class="86554" title="fig0721" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c60b7dff-a064-4d60-aa6f-25115a9ebdd3/fig0721.jpg" alt="" width="500" height="100" /></a><br>
<em>Figure 7-21: Dropping shadows from a heading.</em>

You can even have multiple shadows! Of course, whether you should, is a matter of opinion.

<pre><code class="language-css">h1 {
  text-shadow: gray 0.33em 0.25em 0.1em, -10px 4px 7px blue;
}</code></pre>

Note that the color of a shadow can come before all the lengths or after them, whichever you prefer. Note also that the CSS 3 specification says that the first shadow is “on top,” which is closest to you. Shadows after that are placed successively further away from you as you look at the page. Thus, the gray shadow is placed over the top of the blue shadow. Now to shadow boxes. It’s pretty much the same drill, only with a different property name.

<pre><code class="language-css">h1 {
  box-shadow: gray 0.33em 0.25em 0.25em;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c538397-cd3e-4bdb-99c6-4caf8e9c22b8/fig0722-large.jpg"><img loading="lazy" decoding="async" class="86555" title="fig0722" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6701b57c-4516-4120-b0dc-624761ef97ac/fig0722.jpg" alt="" width="500" height="100" /></a><br>
<em>Figure 7-22: A heading with multiple shadows.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28fecdc5-5681-42c0-b9a1-47021be85650/fig0723-large.jpg"><img loading="lazy" decoding="async" class="86556" title="fig0723" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71b259ea-6028-47ae-9af4-62b504c08e44/fig0723.jpg" alt="" width="500" height="100" /></a><br>
<em>Figure 7-23: Shadowing the element box of a heading.</em>

Even though there’s no obvious element box for the <code>h1</code>, a shadow is generated anyway. It’s also drawn only outside the element, which means that you can’t see it behind/beneath the element, even when the element has a transparent (or, with RGBA colors, semi-transparent) background. The shadows are drawn just beyond the border edge, so you’re probably better off putting a border or a visible background (or both) on any shadowed box.

You can have more than one box shadow, just like you can with text shadows:

<pre><code class="language-css">h1 {
  box-shadow: gray 0.33em 0.25em 0.25em, -10px 2px 6px blue;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1312b57e-48b7-4b90-b807-727630472f15/fig0724-large.jpg"><img loading="lazy" decoding="async" class="86557" title="fig0724" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea6068d3-9a93-4f6d-8716-6eb985f8bf0a/fig0724.jpg" alt="" width="500" height="100" /></a><br>
<em>Figure 7-24: Multiple shadows on the element box of a heading.</em>

Here’s where I have to admit a small fib: The previous examples are the ideal cases. As of this writing, they wouldn’t actually work in browsers. As of mid-2010, to make the single-shadow example work, you’d actually need to say:

<pre><code class="language-css">h1 {
  -moz-box-shadow: gray 0.33em 0.25em 0.25em;
  -webkit-box-shadow: gray 0.33em 0.25em 0.25em;
  box-shadow: gray 0.33em 0.25em 0.25em;}</code></pre>

That will cover all modern browsers as of mid-2010. Over time, the need for the prefixed properties (<code>-moz-</code> and <code>–webkit-</code>) will fade and you’ll be able to just write the single <code>box-shadow</code> declaration. When exactly will that happen? It all depends on your design, your site’s visitors, and your own sense of comfort.

If you also want to get drop shadows on boxes in older versions of Internet Explorer, then you’ll need to add in the IE-only Shadow filter. Read <a href="https://robertnyman.com/2010/03/16/drop-shadow-with-css-for-all-web-browsers/">here</a> to find out more.</p>

### Multiple Backgrounds

One of the really nifty things in CSS 3 is its support for multiple background images on a given element. If you’ve ever nested multiple <code>div</code> elements just to get a bunch of background decorations to show up, this section is for you.

Take, for example, this simple set of styles and markup to present a quotation:

<pre><code class="language-css">body {
  background: #c0ffee;
  font: 1em Georgia, serif;
  padding: 1em 5%;
}
.quotebox {
  font-size: 195%;
  padding: 80px 80px 40px;
  width: 16em;
  margin: 2em auto;
  border: 2px solid #8d7961;
  background: #fff;
}
.quotebox span {
  font-style: italic;
  font-size: smaller;
  display: block;
  margin-top: 0.5em;
  text-align: right;
}

</code></pre>

<div class="quotebox">One’s mind has a way of making itself up in the background, and it suddenly becomes clear what one means to do. —Arthur Christopher Benson</div><br>
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ada1309-f17f-4793-a668-d8c70b3e707b/fig0725-large.jpg"><img loading="lazy" decoding="async" class="86558" title="fig0725" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f6af37d-77ad-4770-be50-51d3bbf28285/fig0725.jpg" alt="" width="500" height="232" /></a><br>
<em>Figure 7-25: Setting up the quotation’s box.</em>

Now, adding a single background image is no big deal. Everyone has done it about a zillion times.

<pre><code class="language-css">.quotebox {
  background: url(bg01.png) top left no-repeat;
  background-color: #fff;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1098483d-41ca-403a-9836-e1fc77f45bec/fig0726-large.jpg"><img loading="lazy" decoding="async" class="86559" title="fig0726" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea4ba131-2300-4f38-a2b8-61a9293103d8/fig0726.jpg" alt="" width="500" height="232" /></a><br>
<em>Figure 7-26: Adding a single background.</em>

But what if you want a little quarter-wheel in every corner? Previously, you would have nested a bunch of <code>div</code>s just inside the <code>quotebox div</code>. With CSS 3, just keep adding them to the <code>background</code> declaration:

<pre><code class="language-css">.quotebox {
      background:
             url(bg01.png) top left no-repeat,
             url(bg02.png) top right no-repeat;
      background-color: #fff;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/664554c9-154c-4ac2-9fb2-31aefa97f4fe/fig0727-large.jpg"><img loading="lazy" decoding="async" class="86560" title="fig0727" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2ebe24c-12df-4901-923c-0d55aa949cfd/fig0727.jpg" alt="" width="500" height="232" /></a><br>
<em>Figure 7-27: Applying two backgrounds to the same element.</em>

Commas separate each <code>background</code> value to get multiple backgrounds:

<pre><code class="language-css">.quotebox {
background:
             url(bg01.png) top left no-repeat,
             url(bg02.png) top right no-repeat,
             url(bg03.png) bottom right no-repeat,
             url(bg04.png) bottom left no-repeat;
      background-color: #fff;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eaa86d1-309a-4676-9594-4c6375725dee/fig0728-large.jpg"><img loading="lazy" decoding="async" class="86561" title="fig0728" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8323bf95-4fb8-4c98-b9be-3843d93e4c17/fig0728.jpg" alt="" width="500" height="232" /></a><br>
<em>Figure 7-28: Applying four backgrounds to a single element.</em>

The effect here is extremely similar to nesting a bunch of <code>div</code>s. It’s just that with CSS 3, you don’t have to bother any more.

That similarity extends into the way background are composited together. You may have noticed that I split out the <code>background-color</code> declaration in order to have a nice flat white behind all the images. But what if you wanted to fold it into the <code>background</code> declaration? Where would you put it? After all, each of these comma-separated values sets up its own background. Put the color in the wrong place, and one or more images will be overwritten by the color.

As it turns out, the answer is the last of the values:

<pre><code class="language-css">.quotebox {
background:
             url(bg01.png) top left no-repeat,
             url(bg02.png) top right no-repeat,
             url(bg03.png) bottom right no-repeat,
             #fff url(bg04.png) bottom left no-repeat;
}</code></pre>

That’s because the multiple background go from “highest”—that is, closest to you as you look at the page—to “lowest”—furthest away from you. If you put the color on the first background, it would sit “above” all the others.

This also means that if you want some kind of patterned background behind all the others, it needs to come last and you need to make sure to shift any background color to it.

<pre><code class="language-css">.quotebox {
background:
             url(bg01.png) top left no-repeat,
             url(bg02.png) top right no-repeat,
             url(bg03.png) bottom right no-repeat,
             url(bg04.png) bottom left no-repeat,
             #fff url(bgparch.png) center repeat;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3375caac-3ac9-4cfd-94d1-f1ece55b296c/fig0729-large.jpg"><img loading="lazy" decoding="async" class="86562" title="fig0729" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af5f1679-ea5a-46b4-a938-578ac95e20af/fig0729.jpg" alt="" width="500" height="232" /></a><br>
<em>Figure 7-29: One element, five backgrounds.</em>

Because of the possible complexities involved, I prefer to split any default background color into its own declaration, as shown earlier. Thus I’d write the preceding as:

<pre><code class="language-css">.quotebox {
  background:
             url(bg01.png) top left no-repeat,
             url(bg02.png) top right no-repeat,
             url(bg03.png) bottom right no-repeat,
             url(bg04.png) bottom left no-repeat,
             url(bgparch.png) center repeat;
      background-color: #fff;
}</code></pre>

When you use the separate property, the color is placed behind all the images and you don’t have to worry about shifting it around if you reorder the images or add new images to the pile.

You can comma-separate the other background properties such as <code>background-image</code>. In fact, an alternate way of writing the preceding styles would be:

<pre><code class="language-css">.quotebox {
    background-repeat: no-repeat, no-repeat, no-repeat, no-repeat, repeat;
    background-image: url(bg01.png), url(bg02.png), url(bg03.png), url(bg04.png), url(bgparch.png);
    background-position: top left, top right, bottom right, bottom left, center;
    background-color: #fff;
}</code></pre>

Different format, same result. This probably looks more verbose, and in this case it really is, but not always. If you drop the parchment background, then you could simplify the first declaration quite a bit:

<pre><code class="language-css">.quotebox {
    background-repeat: no-repeat;
    background-image: url(bg01.png), url(bg02.png), url(bg03.png), url(bg04.png);
    background-position: top left, top right, bottom right, bottom left;
    background-color: #fff;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e5e27a6-a114-4df2-9242-55f1fefbb689/fig0730-large.jpg"><img loading="lazy" decoding="async" class="86563" title="fig0730" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77d55240-5a57-43cf-ab87-c5673402b26e/fig0730.jpg" alt="" width="500" height="232" /></a><br>
<em>Figure 7-30: Similar background, alternate syntax.</em>

Given those styles, none of the background images would be repeated, because the single <code>no-repeat</code> is applied to all the backgrounds that are assigned to the element. The only reason you had to write out all the repeat values before was that the first four have one value and the fifth had another.

And if you were to write two values for background-repeat?

<pre><code class="language-css">.quotebox {
    background-repeat: no-repeat, repeat-y;
    background-image: url(bg01.png), url(bg02.png), url(bg03.png), url(bg04.png);
    background-position: top left, top right, bottom right, bottom left;
    background-color: #fff;
}</code></pre>

In that case, the first and third images would not be repeated, whereas the second and fourth images would be repeated along the <code>y</code> axis. With three repeat values, they would be applied to the first, second, and third images, respectively, whereas the fourth image would take the first repeat value.</p>

### 2D Transforms

If you’ve ever wanted to rotate or skew an element, border, and text and all, then this section is definitely for you. First, though, a word of warning: In order to keep things legible, this section uses the unprefixed version of the <code>transform</code> property. As of this writing, doing transforms in a browser actually would require multiple prefixed declarations, like so:

<pre><code class="language-css">-webkit-transform: …;
-moz-transform: …;
-o-transform: …;
-ms-transform: …;
transform: …;</code></pre>

That should cease to be necessary in a year or two (I hope!) but in the meantime, keep in mind as you read through this section that it’s been boiled down to the unprefixed version for clarity.

Time to get transforming! Possibly the simplest transform to understand is rotation:

<pre><code class="language-css">.box1 {
  -moz-transform: rotate(33.3deg);
}
.box2 {
  -moz-transform: rotate(-90deg);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1899c06-5f6f-4516-a314-f6220eb81316/fig0731-large.jpg"><img loading="lazy" decoding="async" class="86564" title="fig0731" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/947a29e6-5cb5-4cc5-9e3c-78d388d74b6f/fig0731.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-31: Rotated element boxes. The red dashes show the original placement of the elements before their rotation.</em>

In a sense, transforming is a lot like relative positioning: The element is placed normally and then transformed. You can transform any element at all, and in the case of rotation can use any real-number amount of degrees, radians, or grads to specify the angle of rotation. If you’ve ever wanted to rotate your blog by e radians or 225 grads, well, now’s your chance.

As you no doubt noticed, the boxes in the preceding example were rotated around their centers. That’s because the default transformation origin is <code>50% 50%</code>, or the center of the element. You can change the origin point using <code>transform-origin</code>:

<pre><code class="language-css">.box1 {
  transform: rotate(33.3deg);
  transform-origin: bottom left;
}
.box2 {
  transform: rotate(-90deg);
  transform-origin: 75% 0;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f56feb0-8c60-4da5-a094-546f3fc67d69/fig0732-large.jpg"><img loading="lazy" decoding="async" class="86565" title="fig0732" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f306d3e-28de-4780-a337-4f5dd04eb6b4/fig0732.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-32: Elements rotated around points other than their centers.</em>

Two notes: First, negative angles can be equivalent to positive angles. Thus, <code>270deg</code> is equivalent to <code>–90deg</code> in the final positioning of the element, just as <code>0deg</code> and <code>360deg</code> are the same. Second, you can specify angles greater than the apparent maximum value. If you declare <code>540deg</code>, the element’s final rotation will look exactly the same as if you’d declared <code>180deg</code> (as well as <code>–180deg</code>, <code>900deg</code>, and so on). The interim result may be different if you also apply transitions (see next section), but the final "resting" state will be equivalent.

Almost as simple as rotation is scaling. As you no doubt expect, this scales an element up or down in size, making it larger or smaller. You can do this consistently along both axes, or to a different degree along each axis:

<pre><code class="language-css">.box1 {
  transform: scale(0.5);
}
.box2 {
  transform: scale(0.75, 1.5);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa0d9a92-ca96-48f8-8ba7-088493246860/fig0733-large.jpg"><img loading="lazy" decoding="async" class="86566" title="fig0733" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6ad4b53-bd40-4ab2-9599-51b51a1f0a0d/fig0733.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-33: Scaled elements.</em>

One <code>scale()</code> value means the element will be scaled by that amount along both the <code>x</code> and <code>y</code> axes. If there are two values, the first specifies the horizontal (X) scaling, and the second, the vertical (Y) scaling. Thus, if you want to leave the horizontal axis the same and only scale on the y axis, do this:

<pre><code class="language-css">.box1 {
  transform: scale(0.5);
}
.box2 {
  transform: scale(1, 1.5);
}</code></pre>

Alternatively, you can use the scaleY() value:

<pre><code class="language-css">.box1 {
  transform: scale(0.5);
}
.box2 {
  transform: scaleY(1.5);
}</code></pre>

Along the same lines is the scaleX() value, which causes horizontal scaling without changing the vertical scaling.

<pre><code class="language-css">.box1 {
  transform: scaleX(0.5);
}
.box2 {
  transform: scaleX(1.5);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca61ca16-ffc6-4fc5-a91d-8b7620232794/fig0734-large.jpg"><img loading="lazy" decoding="async" class="86567" title="fig0734" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3793930d-29a7-474c-90f9-303b84452faa/fig0734.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-34: Two scaled elements, one scaled only on the Y axis.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d584c8e2-cc24-4da4-8971-7883b51551c0/fig0735-large.jpg"><img loading="lazy" decoding="async" class="86568" title="fig0735" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5257c646-e8e4-4217-a73f-8ab3d7659c01/fig0735.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-35: Two scaled elements, one scaled only on the X axis.</em>

When writing CSS yourself, it seems most convenient to just stick with <code>scale()</code> and fill in a <code>0</code> for the horizontal any time you want a purely vertical scaling. If you’re programmatically changing the scaling via DOM scripting, it might be easier to manipulate <code>scaleX()</code> and <code>scaleY()</code> directly.

As with rotation, you can affect the origin point for scaling. This allows you, for example, to cause an element to scale toward its top-left corners instead of shrink down toward its center:

<pre><code class="language-css">.box1 {
  transform: scale(0.5);
  transform-origin: top left;
}
.box2 {
  transform: scale(1.5);
  transform-origin: 100% 100%;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faf22f00-3718-4d6a-9fa1-a27b675bd627/fig0736-large.jpg"><img loading="lazy" decoding="async" class="86569" title="fig0736" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f67dea9f-173a-4da7-ad98-d29b6ad28315/fig0736.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-36: Two scaled elements, each with a different scaling origin.</em>

Similarly simple is translation. In this case, it isn’t changing the language from one to another, but “translating” a shape from one point to another. It’s an offset by either one or two length values.

<pre><code class="language-css">.box1 {
  transform: translate(50px);
}
.box2 {
  transform: translate(5em,10em);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d109d6b4-df77-4036-9ad9-308264cf41b9/fig0737-large.jpg"><img loading="lazy" decoding="async" class="86570" title="fig0737" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9218a768-6ac7-43ca-866b-29a169d92899/fig0737.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-37: Translated elements.</em>

Again, this is very much like relative positioning. The elements are placed normally and then transformed as directed. When there’s only one length value in a <code>translate()</code> value, it specifies a horizontal movement and the vertical movement is assumed to be zero. If you just want to translate an element up or down, you have two choices. First is to simply give a length of <code>0</code> for the horizontal value.

<pre><code class="language-css">.box1 {
  transform: translate(0,50px);
}
.box2 {
  transform: translate(5em,10em);
}</code></pre>

The other is to use the value pattern <code>translateY()</code>:

<pre><code class="language-css">.box1 {
  transform: translateY(50px);
}
.box2 {
  transform: translate(5em,10em);
}</code></pre>

There is also a <code>translateX()</code>, which does about what you’d expect: moves the element horizontally!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9ff94a4-91aa-4458-bcf5-363dc66edeb2/fig0738-large.jpg"><img loading="lazy" decoding="async" class="86571" title="fig0738" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5faacb5-993a-4387-bc86-b8fd7d42e4b3/fig0738.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-38: Two differently translated elements.</em>

While you can declare a transform-origin in cases where you’re just translating, it doesn’t matter all that much whether you do so. After all, whether an element’s center or top-left corner is pushed 50 pixels to the right doesn’t really matter. The element will end up in the same place either way. But that’s only true if all you’re doing is translating. If you do anything else at the same time, like rotate or scale, then the origin will matter. (More on combining transforms in a bit.)

The last type of transformation, skewing, is slightly more complex, although the method of declaring it is no more difficult than you’ve seen so far.

Skewing an element distorts its shape along one or both axes:

<pre><code class="language-css">.box1 {
  transform: skew(23deg);
}
.box2 {
  transform: skew(13deg,-45deg);
}</code></pre>

If you provide only a single value for <code>skew()</code>, then there is only horizontal <code>(X) skew</code>, and no vertical <code>(Y) skew</code>. As with translations and scaling, there are <code>skewX()</code> and <code>skewY()</code> values for those times you want to explicitly skew along only one axis:

<pre><code class="language-css">.box1 {
  transform: skewX(-23deg);
}
.box2 {
  transform: skewY(45deg);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dadb12e3-8ae2-429c-9261-989cde36f100/fig0739-large.jpg"><img loading="lazy" decoding="async" class="86572" title="fig0739" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf312bc3-9702-4961-b178-22b76f094fcd/fig0739.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-39: Two skewed elements.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0dfc581-0deb-4365-8be9-eaabdad67468/fig0740-large.jpg"><img loading="lazy" decoding="async" class="86573" title="fig0740" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cde8fd4f-179b-43ee-986a-26cf572c99aa/fig0740.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-40: Two elements, each one skewed along a different axis.</em>

Here's how skewing works: Imagine there are two bars running through the element, one along each of the X and Y axes. When you skew in the X direction, the Y axis is rotated by the skew angle. Yes, the Y (vertical) axis is the one that rotates in a <code>skewX()</code> operation. Positive angles are counterclockwise, and negative angles are clockwise. That’s why the first box in the preceding example appears to tilt rightward: The Y axis was tilted 33.3 degrees clockwise.

The same basic thing happens with <code>skewY()</code>: The X axis is tilted by the specified number of degrees, with positive angles tilting it counterclockwise and negative angles tilting clockwise.

The interesting part here is how the origin plays into it. If the origin is in the center and you provide a negative <code>skewX()</code>, then the top of the element will slide to the right of the origin point while the bottom will slide to the left. Change the origin to the bottom of the element, though, and the whole thing will tilt right from the bottom of the element.

<pre><code class="language-css">.box1 {
  transform: skewX(-23deg);
}
.box2 {
  transform: skewY(-23deg);
  transform-origin: bottom center;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2642358a-49cd-4588-99c1-00f3c0493c0e/fig0741-large.jpg"><img loading="lazy" decoding="async" class="86574" title="fig0741" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0605a596-d674-4956-a829-d979d501c851/fig0741.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-41: Two skewed elements, each with a different skewing origin.</em>

Similar effects happen with vertical skews.

So those are the types of transforms you can carry out. But what if you want to do more than one at a time? No problem! Just list them in the order you want them to happen.

<pre><code class="language-css">.box1 {
  transform: translateX(50px) rotate(23deg);
}
.box2 {
  transform: scale(0.75) translate(25px,-2em);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0253da0-da11-4484-9e04-3de9792906c1/fig0742-large.jpg"><img loading="lazy" decoding="async" class="86575" title="fig0742" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32305069-bec9-41d1-892d-5c2f153e0ece/fig0742.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-42: Multiple transforms in action.</em>

In every case, the transforms are executed one at a time, starting with the first. This can make a significant difference. Consider the differing outcomes of the same transforms in different orders.

<pre><code class="language-css">.box1 {
  transform: rotate(45deg) skew(-45deg);
}
.box2 {
  transform: skew(-45deg) rotate(45deg);
}</code></pre>

There is one more transformation value type to cover: <code>matrix()</code>. This value type allows you to specify a transformation matrix in six parts, the last two of which define the translation. Here’s a code example:

<pre><code class="language-css">.box1 {
  transform: matrix(0.67,0.23,0,1,25px,10px);
}
.box2 {
  transform: matrix(1,0.13,0.42,1,0,-25px);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c37ea81b-fa63-4cdc-a049-c9cf0a4c2dad/fig0743-large.jpg"><img loading="lazy" decoding="async" class="86576" title="fig0743" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b85f66e9-7696-4a88-9d32-8a134d3d1746/fig0743.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-43: The differences caused by transform value ordering.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96aef78f-3071-4ecf-ab17-c4c06917e480/fig0744-large.jpg"><img loading="lazy" decoding="async" class="86577" title="fig0744" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a1675a0-c66b-4f81-9dce-b0067be64b7f/fig0744.jpg" alt="" width="500" height="369" /></a><br>
<em>Figure 7-44: Matrix transforms.</em>

Basically, the first four numbers are a compact form of expressing the end result of rotating, skewing, and scaling an element, and the last two translate that end result. If you understand matrix-transformation math, then you’ll love this. If you don’t, don't worry about it overmuch. You can get to the same place with the other transform values reviewed in this chapter.

If you’d like to learn about matrix transforms, here are two useful resources:

*   [Examples of Linear Transformation Matrices](https://en.wikipedia.org/wiki/Linear_transformation#Examples_of_linear_transformation_matrices)
*   [Coordinate Transformation Matrices](https://www.mathamazement.com/Lessons/Pre-Calculus/08_Matrices-and-Determinants/coordinate-transformation-matrices.html)

### About the book

<a href="https://eu.wiley.com/WileyCDA/WileyTitle/productCd-047068416X.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31fbe8b2-2220-4982-a538-eaffea39af0b/wiley.jpg" alt="Smashing CSS" width="300" height="391" /></a>

<a href="https://eu.wiley.com/WileyCDA/WileyTitle/productCd-047068416X.html">Smashing CSS</a> takes you well beyond the basics, covering not only the finer points of layout and effects, but introduces you to the future with HTML5 and CSS3. This book is for developers who already have some experience with CSS and JavaScript and are ready for more advanced techniques.

<em>(vf) (ik)</em>

table.terms {
border: 1px solid #ccc;
border-collapse: collapse;
margin-top: 5px;
}
.terms thead {
background-color: #ccc;
font-weight: bold;
}
.terms td {
padding: 6px 8px;
}
.terms tr {
border-bottom: 1px solid #ccc;
}

