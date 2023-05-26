---
title: How To Benefit From CSS Generated Content And Counters
slug: css-generated-content-counters
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3ce93a2-0149-4203-bc00-cc24c660d5a0/generated-content-start-image-opt.jpg
date: 2013-04-12T15:00:37.000Z
author: gabriele-romanato
description: >-
  Generated content was first introduced in the CSS2 specification. For several
  years, the feature was used by relatively few Web authors due to inconsistent
  browser support.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
---
Generated content was first introduced in the CSS2 specification. For several years, the feature was used by relatively few Web authors due to inconsistent browser support. With the release of Internet Explorer 8 in 2009, <strong>generated content was rediscovered</strong>, and many interesting implementations were adopted for the first time. In this article, we’ll discuss some possible uses of <a href="https://www.w3.org/TR/CSS21/generate.html">generated content</a>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Ultimate Guide To CSS Pseudo-Classes And Pseudo-Elements](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
*   [Learning To Use The :before And :after Pseudo-Elements In CSS](https://www.smashingmagazine.com/2011/07/learning-to-use-the-before-and-after-pseudo-elements-in-css/)
*   [!important CSS Declarations: How and When to Use Them](https://www.smashingmagazine.com/2010/11/the-important-css-declaration-how-and-when-to-use-it/)
*   [CSS Specificity And Inheritance](https://www.smashingmagazine.com/2010/04/css-specificity-and-inheritance/)

## What Is Generated Content?

In technical terms, generated content is a simple abstraction created by CSS in the document tree. As such, in practical terms, generated content exists only in the layout of the Web document.

{{% feature-panel %}}

Accessing generated content via JavaScript is possible by reading the textual value of the <code>content</code> property:

<pre><code class="language-javascript">
var test = document.querySelector('#test');
var result   = getComputedStyle(test, ':before').content;
var output = document.querySelector('#output');
output.innerHTML = result;
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/QSNeJ/)

## Inserting Generated Content

Generated content may be inserted before and after the actual content of an element, using the <code>:before</code> and <code>:after</code> pseudo-elements, respectively. To represent the pseudo-elements, we can use the following pseudo-markup.

<pre><code class="language-markup">
&lt;p&gt;
   &lt;before&gt;Start&lt;/before&gt;
      Actual content
   &lt;after&gt;End&lt;/after&gt;
&lt;/p&gt;
</code></pre>

And our CSS would be:

<pre><code class="language-css">
p:before {
   content: "Start";
}

p:after {
   content: "End";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/d9863/)

Bear in mind that if <strong>you are validating the CSS file against the CSS3 specifications</strong>, the <code>:before</code> and <code>:after</code> pseudo-elements should be written as <code>::before</code> and <code>::after</code>. Otherwise, the CSS validator will call an error.

As you can see, the property that inserts the two strings is <code>content</code>. This
property accepts the following values:

*   `none`, `normal` The pseudo-content would not be generated.
*   `<string>` This would be a textual string enclosed in quotation marks.
*   `url()` This function enables us to insert an external resource (usually an image), as with the `background-image` property.
*   `counter()`, `counters()` These functions insert counters (see below for details).
*   `attr(attribute)` This function enables us to insert the value of `attribute` of a given element.
*   `open-quote`, `close-quote`, `no-open-quote`, `no-close-quote` These values automate the generation of quotation marks.

<strong>Keep in mind that generated content takes up space on the page</strong>, and its presence affects the browser’s computation of the parent element.</p>

## Inserting Strings

In the previous example, we inserted two simple strings before and after the actual content of the element. Generated content also enables us to insert more complex symbols, through escaping:

<pre><code class="language-css">
p:before {
   content: "0A7";
   padding-right: 0.2em;
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/69XSC/)

The escaped sequence between the double quotation marks is the hexadecimal Unicode value of the paragraph symbol. <strong>We can also combine simple strings with Unicode symbols:</strong><br>
<pre class="language-css"><code class="language-css">
p:before {
   content: "( " "0A7" " )";
   padding-right: 0.2em;
}
</code>
</pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/umgSs/)

In case you need it, a comprehensive list of all Unicode characters is <a href="https://www.alanwood.net/unicode/">available on Alan Wood’s website</a>.

Note that all textual content inside the <code>content</code> property is treated literally. So, spaces and tabs inserted via the keyboard will be inserted on the page as well.</p>

## Inserting Icons Using Web Fonts

Web fonts can be used to insert graphical icons through generated content. Depending on the Web font family, you can insert either simple letters or Unicode sequences:

<pre><code class="language-css">
@import url(https://weloveiconfonts.com/api/?family=brandico);

p:before {
   content: "f303";
   padding-right: 0.3em;
   font-family: 'brandico', sans-serif;
   font-size: 22px;
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/F786N/)

In this example, we have inserted a Twitter icon. Our code could be rewritten as follows:

<pre><code class="language-css">
.icon-twitter:before {
   content: "f303";
   padding-right: 0.3em;
   font-family: 'brandico', sans-serif;
   font-size: 22px;
}
</code></pre>

## Inserting Images

We can insert images through the <code>url()</code> function.

<pre><code class="language-css">
a:before {
   content: url(link.png);
   padding-right: 0.2em;
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/WSwWJ/)

As you can see, this function has the same syntax as the <code>background-image</code> property.</p>

## Inserting Attribute Values

An attribute value of an element can be inserted through the <code>attr()</code> function.

<pre><code class="language-css">
a[href]:after {
   content: "( " attr(href) " )";
   padding-left: 0.2em;
   color: #000;
   font: small "Courier New", Courier, monospace;
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/jjuae/)

We’ve just inserted the value of the <code>href</code> attribute, which is a simple text string.</p>

## Inserting Counters

The automatic numbering of CSS is controlled by two properties,
<code>counter-reset</code> and <code>counter-increment</code>. Counters defined by these properties are then used with the <code>counter()</code> and <code>counters()</code> functions of the <code>content</code> property.

The <code>counter-reset</code> property may contain one or more names of counters (i.e. “identifiers”), optionally followed by an integer. The integer sets the value that will be incremented by the <code>counter-increment</code> property for any occurence of the given element. The default value is 0. Negative values are allowed.

The <code>counter-increment</code> property is similar. The basic difference is that this one increments a counter. Its default increment is 1. Negative values are allowed.

<strong>Now we are ready for an example.</strong> Take the following markup:

<pre><code class="language-markup">
&lt;dl&gt;
   &lt;dt&gt;term&lt;/dt&gt;
   &lt;dd&gt;description&lt;/dd&gt;
   &lt;dt&gt;term&lt;/dt&gt;
   &lt;dd&gt;description&lt;/dd&gt;
   &lt;dt&gt;term&lt;/dt&gt;
   &lt;dd&gt;description&lt;/dd&gt;
&lt;/dl&gt;
</code></pre>

We want to add progressive numbering (1, 2, 3, etc.) to each definition term (<code>dt</code>) in the list. Here is the CSS:

<pre><code class="language-css">
dl {
   counter-reset: term;
}
dt:before {
   counter-increment: term;
   content: counter(term);
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/hBmVA/)

<strong>The first rule</strong> here sets a counter for the definition list. This is called a “scope.” The name (or identifier) of the counter is <code>term</code>. Whatever name we choose for our counter must be identical to the one in the <code>counter-increment</code> property (of course, the name should be meaningful).

In <strong>the second rule</strong>, we attach the <code>:before</code> pseudo-element to the <code>dt</code> element, because we want to insert the counter precisely before the actual content of the element. Let’s take a closer look at the second declaration of the second rule. The <code>counter()</code> function accepts our identifier (<code>term</code>) as its argument, and the <code>content</code> property generates the counter.

There’s no space between the number and the content of the element. If we want to add a space and, say, a period after the number, we could insert the following string in the <code>content</code> property:

<pre><code class="language-css">
dt:before {
   content: counter(term) ". ";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/CWTTZ/)

Note that the string between the quotation marks is treated literally; that is, the space after the period is inserted just as we’ve typed it on the keyboard. In fact, the <code>content</code> property can be regarded as the CSS counterpart of the JavaScript <code>document.write()</code> method, except that it doesn’t add real content to the document. Simply put, the <code>content</code> property creates a mere abstraction in the document tree but doesn’t modify it.

In case you’re wondering, <strong>we can add more styles to counters by applying other properties</strong> to the attached pseudo-element. For example:

<pre><code class="language-css">
dt:before {
   content: counter(term);
   padding: 1px 2px;
   margin-right: 0.2em;
   background: #ffc;
   color: #000;
   border: 1px solid #999;
   font-weight: bold;
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/tJU7A/)

We’ve just set a background color, added some padding and a right margin, made the font bold, and outlined the counters with a thin solid border. Now our counters are a little more attractive.

Furthermore, counters may be negative. When dealing with negative counters, we should adhere to a little math — namely, the part about adding and subtracting negative and positive numbers. For example, if we need progressive numbering starting from 0, we could write the following:

<pre><code class="language-css">
dl {
   counter-reset: term -1;
}
dt:before {
   counter-increment: term;
   content: counter(term) ". ";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/GJPZq/)

By setting the <code>counter-reset</code> property to -1 and incrementing it by 1, the resulting value is 0, and the numbering will start from that value. Negative counters may be combined with positive counters to interesting effect. Consider this example:

<pre><code class="language-css">
dl {
   counter-reset: term -1;
}
dt:before {
   counter-increment: term 3;
   content: counter(term) ". ";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/D6bBU/)

As you can see, adding and subtracting negative and positive numbers yield a wide range of combinations between counters. With just a simple set of calculations, <strong>we get complete control over automatic numbering</strong>.

Another interesting feature of CSS counters lies in their ability to be nested. In fact, numbering may also be ordered by progressive sublevels, such as 1.1, 1.1.1, 2.1 and so on. To add a sublevel to the elements in our list, we would write the following:

<pre><code class="language-css">
dl {
   counter-reset: term definition;
}
dt:before {
   counter-increment: term;
   content: counter(term) ". ";
}
dd:before {
   counter-increment: definition;
   content: counter(term) "." counter(definition) " ";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/Ampkg/)

This example is similar to the first one, but in this case we have two counters, <code>term</code> and <code>definition</code>. The scope of both counters is set by the first rule and “lives” in the <code>dl</code> element. The second rule inserts the first counter before each definition term in the list. This rule is not particularly interesting because its effect is already known. Instead, the last rule is the heart of our code because it does the following:

1.  increments the second counter (`definition`) on `dd` elements;
2.  inserts the first counter (`term`), followed by a period;
3.  inserts the second counter (`definition`), followed by a space.

Note that steps 2 and 3 are both performed by the <code>content</code> property used on the <code>:before</code> pseudo-element that is attached to the definition term.

<strong>Another interesting point is that counters are “self-nesting,”</strong> in the sense that resetting a counter on a descendant element (or pseudo-element) automatically creates a new instance of the counter. This is useful in the case of (X)HTML lists, where elements may be nested with arbitrary depth. However, specifying a different counter for each list is not always possible because it might produce rather redundant code. For this reason, the <code>counters()</code> function is useful. This function creates a string that contains all of the counters with the same name of the given counter in the scope. Counters are then separated by a string. Take the following markup:

<pre><code class="language-markup">
&lt;ol&gt;
   &lt;li&gt;item&lt;/li&gt;
   &lt;li&gt;item
      &lt;ol&gt;
         &lt;li&gt;item&lt;/li&gt;
         &lt;li&gt;item&lt;/li&gt;
         &lt;li&gt;item
            &lt;ol&gt;
               &lt;li&gt;item&lt;/li&gt;
               &lt;li&gt;item&lt;/li&gt;
            &lt;/ol&gt;
         &lt;/li&gt;
      &lt;/ol&gt;
   &lt;/li&gt;
&lt;/ol&gt;
</code></pre>

The following CSS will number the nested list items as 1, 1.1, 1.1.1, etc.

<pre><code class="language-css">
ol {
   counter-reset: item;
   list-style: none;
}
li {
   display: block;
}
li:before {
   counter-increment: item;
   content: counters(item, ".") " ";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/7mcWp/)

In this example, we have only the <code>item</code> counter for each nested level. Instead of writing three different counters (such as <code>item1</code>, <code>item2</code>, <code>item3</code>) and thus creating three different scopes for each nested <code>ol</code> element, we can rely on the <code>counters()</code> function to achieve this goal. The second rule is important and deserves further explanation. Because ordered lists have default markers (i.e. numbers), we’d get rid of these markers by turning the list items into block-level elements. Remember that only elements with <code>display: list-items</code> have markers.

Now we can look carefully at <strong>the third rule</strong>, which does the actual the work. The first declaration increments the counter previously set on the outermost list. Then, in the second declaration, the <code>counters()</code> function creates all of the counter’s instances for the innermost lists. The structure of this function is as follows:

1.  Its first argument is the name of the given counter, immediately followed by a comma.
2.  Its second argument is a period between double quotation marks.

Note that we’ve inserted a space after the <code>counters()</code> function to keep the numbers separate from the actual contents of the list items.

Counters are formatted with decimal numbers by default. However, the styles of the <code>list-style-type</code> property are also available for counters. The default notation is <code>counter(name)</code> (i.e. no styling) or <code>counter(name, 'list-style-type')</code> to change the default formatting. In practice, the recommended styles are these:

*   `decimal`
*   `decimal-leading-zero`
*   `lower-roman`
*   `upper-roman`
*   `lower-greek`
*   `lower-latin`
*   `upper-latin`
*   `lower-alpha`
*   `upper-alpha`

Don’t forget that we’re working with numeric systems. Also remember that the specification doesn’t define how to render an alphabetical system beyond the end of an alphabet. For example, the rendering of <code>lower-latin</code> after 26 list items is undefined. Thus, numerals are recommended for long lists:

<pre><code class="language-css">
dl {
   counter-reset: term definition;
}
dt:before {
   counter-increment: term;
   content: counter(term, upper-latin) ". ";
}
dd:before {
   counter-increment: definition;
   content: counter(definition, lower-latin) ". ";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/W6HYP/)

We can also add styles to the <code>counters()</code> function:

<pre><code class="language-css">
li:before {
   counter-increment: item;
   content: counters(item, ".", lower-roman) " ";
}
</code></pre>

*   [See example](https://jsfiddle.net/gabrieleromanato/wLtAf/)

Note that the <code>counters()</code> function also accepts a third argument (<code>lower-roman</code>) as the last item in its arguments list, separated from the preceding period by a second comma. However, the <code>counters()</code> function doesn’t allow us to specify different styles for each level of nesting.</p>

## Conclusion

With the new generation of browsers, we can use CSS-generated content to embellish our layouts with strings and graphics. Generated content, then, is surely an excellent tool that every developer should learn.</p>

### Further Reading

*   “[Learning to Use the :before and :after Pseudo-Elements in CSS](https://www.smashingmagazine.com/2011/07/13/learning-to-use-the-before-and-after-pseudo-elements-in-css/),” Louis Lazaris, Smashing Magazine
*   “[Styling Elements With Glyphs, Sprites and Pseudo-Elements](https://www.smashingmagazine.com/2011/03/19/styling-elements-with-glyphs-sprites-and-pseudo-elements/),” Thierry Koblentz, Smashing Magazine

<em>Source of image on front page: <a href="https://www.flickr.com/photos/riebart/4466482623">Riebart</a></em>

{{< signature "al" >}}

