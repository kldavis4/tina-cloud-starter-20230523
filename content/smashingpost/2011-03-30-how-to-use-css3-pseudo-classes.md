---
title: How To Use CSS3 Pseudo-Classes
slug: how-to-use-css3-pseudo-classes
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff82ae84-a7dc-4b84-94b5-adba7dd36eea/css3-styling1.jpg'
date: 2011-03-30T09:24:19.000Z
author: richard-shepherd
description: >-
  CSS3 is a wonderful thing, but it’s easy to be bamboozled by the transforms
  and animations (many of which are vendor-specific) and forget about the
  nuts-and-bolts selectors that have also been added to the specification. A
  number of powerful new pseudo-selectors (16 are listed in the [latest W3C
  spec](https://www.w3.org/TR/css3-selectors/)) enable us to select elements
  based on a range of new criteria.
  "CSS3 Pseudo
  Classes")](https://www.smashingmagazine.com/2011/03/30/how-to-use-css3-pseudo-classes/)

  Before we look at these new CSS3 pseudo-classes, let’s briefly delve into the
  dusty past of the Web and chart the journey of these often misunderstood
  selectors.
categories:
  - Coding
  - CSS
  - Essentials
  - CSS3
---
CSS3 is a wonderful thing, but it’s easy to be bamboozled by the transforms and animations (many of which are vendor-specific) and forget about the nuts-and-bolts selectors that have also been added to the specification. A number of powerful new pseudo-selectors (16 are listed in the <a href="https://www.w3.org/TR/css3-selectors/">latest W3C spec</a>) enable us to select elements based on a range of new criteria.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e476b570-dabe-4d53-af4f-f448efcd65fe/css3.jpg"><img class="aligncenter wp-image-93197 size-full" title="CSS3 Pseudo-Classes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e476b570-dabe-4d53-af4f-f448efcd65fe/css3.jpg" alt="CSS3 Pseudo-Classes" width="500" height="350" /></a>

Before we look at these new CSS3 pseudo-classes, let’s briefly delve into the dusty past of the Web and chart the journey of these often misunderstood selectors.</p>

## A Brief History Of Pseudo-Classes

When the <a href="https://www.w3.org/TR/CSS1/">CSS1</a> spec was completed back in 1996, a few pseudo-selectors were included, many of which you probably use almost every day. For example:

{{% feature-panel %}}

*   `:link`
*   `:visited`
*   `:hover`
*   `:active`

Each of these states can be applied to an element, usually <code>&lt;a&gt;</code>, after which comes the name of the pseudo-class. It’s amazing to think that these pseudo-classes arrived on the scene before <a href="https://www.w3.org/TR/html401/">HTML4</a> was published by the W3C a year later in December 1997.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Ultimate Guide To CSS Pseudo-Classes And Pseudo-Elements](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
*   [Learning To Use The :before And :after Pseudo-Elements In CSS](https://www.smashingmagazine.com/2011/07/learning-to-use-the-before-and-after-pseudo-elements-in-css/)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/take-your-design-to-the-next-level-with-css3/)
*   [CSS3 Flexible Box Layout](https://www.smashingmagazine.com/2011/09/css3-flexible-box-layout-explained/)

### CSS2 Arrives

Hot on the heels of CSS1 was <a href="https://www.w3.org/TR/CSS2/">CSS2</a>, whose recommended spec was published just two years later in May 1998. Along with exciting things like positioning were new pseudo-classes: <code>:first-child</code> and <code>:lang()</code>.

<code>:lang</code>
There are a couple of ways to indicate the language of a document, and if you’re using <a href="https://www.w3.org/html/logo/">HTML5</a>, it’ll likely be by putting <code>&lt;html lang="en"&gt;</code> just after the doc type (specifying your local language, of course). You can now use <code>:lang(en)</code> to style elements on a page, which is useful when the language changes dynamically.

<code>:first-child</code>
You may have already used <code>:first-child</code> in your documents. It is often used to add or remove a top border on the first element in a list. Strange, then, that it wasn’t accompanied by <code>:last-child</code>; we had to wait until CSS3 was proposed before it could meet its brother.</p>

### Why Use Pseudo-Classes?

What makes pseudo-classes so useful is that they <strong>allow you to style content dynamically</strong>. In the <code>&lt;a&gt;</code> example above, we are able to describe how links are styled when the user interacts with them. As we’ll see, the new pseudo-classes allow us to dynamically style content based on its position in the document or its state.

Sixteen new pseudo-classes have been introduced as part of the W3C’s <a href="https://www.w3.org/TR/css3-selectors/">CSS Proposed Recommendation</a>, and they are broken down into four groups: structural pseudo-classes, pseudo-classes for the states of UI elements, a target pseudo-class and a negation pseudo-class.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53f00359-9401-4549-8b2b-43c514fae17a/w3c.jpg"><img class="93198" title="w3c css3 demo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53f00359-9401-4549-8b2b-43c514fae17a/w3c.jpg" alt="Screenshot" width="550" height="283" /></a><br>
<em>The W3C is the home of CSS.</em>

Let’s now run through the 16 new pseudo-selectors one at a time and see how each is used. I’ll use the same notation for naming classes that the W3C uses, where <code>E</code> is the element, <code>n</code> is a number and <code>s</code> is a selector.

### Sample Code

For many of these new selectors, I’ll also refer to some sample code so that you can see what effect the CSS has. We’ll take a regular form and make it suitable for an iPhone using our new CSS3 pseudo-classes.

Note that we could arguably use ID and class selectors for much of this form, but it’s a great opportunity to take our new pseudo-classes out for a spin and demonstrate how you might use them in a real-world example. Here’s the HTML (which you can see in action on my website):

<pre><code class="language-markup tmp-html">&lt;form&gt;
 &lt;hgroup&gt;
 &lt;h1&gt;Awesome Widgets&lt;/h1&gt;
 &lt;h2&gt;All the cool kids have got one :)&lt;/h2&gt;
 &lt;/hgroup&gt;
 &lt;fieldset id="email"&gt;
 &lt;legend&gt;Where do we send your receipt?&lt;/legend&gt;
 &lt;label for="email"&gt;Email Address&lt;/label&gt;
 &lt;input type="email" name="email" placeholder="Email Address" /&gt;
 &lt;/fieldset&gt;

 &lt;fieldset id="details"&gt;
 &lt;legend&gt;Personal Details&lt;/legend&gt;
 &lt;select name="title" id="field_title"&gt;
  &lt;option value="" selected="selected"&gt;Title&lt;/option&gt;
  &lt;option value="Mr"&gt;Mr&lt;/option&gt;
  &lt;option value="Mrs"&gt;Mrs&lt;/option&gt;
  &lt;option value="Miss"&gt;Miss&lt;/option&gt;
 &lt;/select&gt;

 &lt;label for="firstname"&gt;First Name&lt;/label&gt;
 &lt;input name="firstname" placeholder="First Name" /&gt;

 &lt;label for="initial"&gt;Initial&lt;/label&gt;
 &lt;input name="initial" placeholder="Initial" size="3" /&gt;

 &lt;label for="surname"&gt;Surname&lt;/label&gt;
 &lt;input name="surname" placeholder="Surname" /&gt;
 &lt;/fieldset&gt;

 &lt;fieldset id="payment"&gt;
 &lt;legend&gt;Payment Details&lt;/legend&gt;

 &lt;label for="cardname"&gt;Name on card&lt;/label&gt;
 &lt;input name="cardname" placeholder="Name on card" /&gt;

 &lt;label for"cardnumber"&gt;Card number&lt;/label&gt;
 &lt;input name="cardnumber" placeholder="Card number" /&gt;

 &lt;select name="cardType" id="field_cardType"&gt;
  &lt;option value="" selected="selected"&gt;Select Card Type&lt;/option&gt;
  &lt;option value="1"&gt;Visa&lt;/option&gt;
  &lt;option value="2"&gt;American Express&lt;/option&gt;
  &lt;option value="3"&gt;MasterCard&lt;/option&gt;
 &lt;/select&gt;

 &lt;label for="cardExpiryMonth"&gt;Expiry Date&lt;/label&gt;
 &lt;select id="field_cardExpiryMonth" name="cardExpiryMonth"&gt;
  &lt;option selected="selected" value="mm"&gt;MM&lt;/option&gt;
   &lt;option value="01"&gt;01&lt;/option&gt;
   &lt;option value="02"&gt;02&lt;/option&gt;
   &lt;option value="03"&gt;03&lt;/option&gt;
   &lt;option value="04"&gt;04&lt;/option&gt;
   &lt;option value="05"&gt;05&lt;/option&gt;
   &lt;option value="06"&gt;06&lt;/option&gt;
   &lt;option value="07"&gt;07&lt;/option&gt;
   &lt;option value="08"&gt;08&lt;/option&gt;
   &lt;option value="09"&gt;09&lt;/option&gt;
   &lt;option value="10"&gt;10&lt;/option&gt;
   &lt;option value="11"&gt;11&lt;/option&gt;
   &lt;option value="12"&gt;12&lt;/option&gt;
 &lt;/select&gt; /
 &lt;select id="field_cardExpiryYear" name="cardExpiryYear"&gt;
   &lt;option value="yyyy"&gt;YYYY&lt;/option&gt;
    &lt;option value="2011"&gt;11&lt;/option&gt;
    &lt;option value="2012"&gt;12&lt;/option&gt;
    &lt;option value="2013"&gt;13&lt;/option&gt;
    &lt;option value="2014"&gt;14&lt;/option&gt;
    &lt;option value="2015"&gt;15&lt;/option&gt;
    &lt;option value="2016"&gt;16&lt;/option&gt;
    &lt;option value="2017"&gt;17&lt;/option&gt;
    &lt;option value="2018"&gt;18&lt;/option&gt;
    &lt;option value="2019"&gt;19&lt;/option&gt;
 &lt;/select&gt;

 &lt;label for"securitycode"&gt;Security code&lt;/label&gt;
 &lt;input name="securitycode" type="number" placeholder="Security code" size="3" /&gt;

 &lt;p&gt;Would you like Insurance?&lt;/p&gt;
 &lt;input type="radio" name="Insurance" id="insuranceYes" /&gt;
  &lt;label for="insuranceYes"&gt;Yes Please!&lt;/label&gt;
 &lt;input type="radio" name="Insurance" id="insuranceNo" /&gt;
  &lt;label for="insuranceNo"&gt;No thanks&lt;/label&gt;

 &lt;/fieldset&gt;

 &lt;fieldset id="submit"&gt;
 &lt;button type="submit" name="Submit" disabled&gt;Here I come!&lt;/button&gt;
 &lt;/fieldset&gt;
&lt;/form&gt;</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a8388bc-9121-4980-80d9-e644bd6cf6a4/before-after.jpg"><img class="94122" title="before-after" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a8388bc-9121-4980-80d9-e644bd6cf6a4/before-after.jpg" alt="Screenshot" width="550" height="413" /></a><br>
<em>Our form, before and after.</em>

## 1\. Structural Pseudo-Classes

According to the W3C, structural pseudo-classes do the following:
<blockquote>… permit selection based on extra information that lies in the document tree but cannot be represented by other simple selectors or combinators.</blockquote>

What this means is that we have selectors that have been turbo-charged to dynamically select content based on its position in the document. So let’s start at the beginning of the document, with <code>:root</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbaae293-cb43-47e2-8ca2-c4399447e936/selectors-level-screenshot.jpg"><img class="93200" title="selectors-level3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbaae293-cb43-47e2-8ca2-c4399447e936/selectors-level-screenshot.jpg" alt="Screenshot" width="501" height="300" /></a><br>
<em>Level 3 selectors on the W3C website.</em>

### E:root

The <code>:root</code> pseudo-class selects the root element on the page. Ninety-nine times out of a hundred, this will be the <code>&lt;html&gt;</code> element. For example:

<pre><code class="language-css">:root { background-color: #fcfcfc; }</code></pre>

It’s worth noting that you could style the <code>&lt;html&gt;</code> element instead, which is perhaps a little more descriptive:

<pre><code class="language-css">html { background-color: #fcfcfc; }</code></pre>

<strong>iPhone Form Example</strong>
Let’s move over to our sample code and give the document some basic text and background styles:

<pre><code class="language-css">:root {
color: #fff;
text-shadow: 0 -1px 0 rgba(0,0,0,0.8);
background: url(…/images/background.png) no-repeat #282826; }</code></pre>

### E:nth-child(n)

The <code>:nth-child()</code> selector might require a bit of experimentation to fully understand. The easiest implementation is to use the keywords <code>odd</code> or <code>even</code>, which are useful when displaying data that consists of rows or columns. For example, we could use the following:

<pre><code class="language-css">ul li:nth-child(odd) {
background-color: #666;
color: #fff; }</code></pre>

This would highlight every other row in an unordered list. You might find this technique extremely handy when using tables. For example:

<pre><code class="language-css">table tr:nth-child(even) { … }</code></pre>

The <code>:nth-child</code> selector can be much more specific and flexible, though. You could select only the third element from a list, like so:

<pre><code class="language-css">li:nth-child(3) { … }</code></pre>

Note that <code>n</code> does not start at zero, as it might in an array. The first element is <code>:nth-child(1)</code>, the second is <code>:nth-child(2)</code> and so on.

We can also use some simple algebra to make things even more exciting. Consider the following:

<pre><code class="language-css">li:nth-child(2n) { … }</code></pre>

Whenever we use <code>n</code> in this way, it stands for all positive integers (until the document runs out of elements to select!). In this instance, it would select the following list items:

*   Nothing (2 × 0)
*   2nd element (2 × 1)
*   4th element (2 × 2)
*   6th element (2 × 3)
*   8th element (2 × 4)
*   etc.

This actually gives us the same thing as <code>nth-child(even)</code>. So, let’s mix things up a bit:

<pre><code class="language-css">li:nth-child(5n) { … }</code></pre>

This gives us:

*   Nothing (5 × 0)
*   5th element (5 × 1)
*   10th element (5 × 2)
*   15th element (5 × 3)
*   20th element (5 × 4)
*   etc.

Perhaps this would be useful for long lists or tables, perhaps not. We can also add and subtract numbers in this equation:

<pre><code class="language-css">li:nth-child(4n + 1) { … }</code></pre>

This gives us:

*   1st element ((4 × 0) + 1)
*   5th element ((4 × 1) + 1)
*   9th element ((4 × 2) + 1)
*   13th element ((4 × 3) + 1)
*   17th element ((4 × 4) + 1)
*   etc.

<a href="https://reference.sitepoint.com/css/understandingnthchildexpressions">SitePoint points out</a> an interesting quirk here. If you set <code>n</code> as negative, you’ll be able to select the first x number of items like so:

<pre><code class="language-css">li:nth-child(-n + x) { … }</code></pre>

Let’s say you want to select the first five items in a list. Here’s the CSS:

<pre><code class="language-css">li:nth-child(-n + 5) { … }</code></pre>

This gives us:

*   5th element (-0 + 5)
*   4th element (-1 + 5)
*   3rd element (-2 + 5)
*   2nd element (-3 + 5)
*   1st element (-4 + 5)
*   Nothing (-5 + 5)
*   Nothing (-6 + 5)
*   etc.

If you’re listing data in order of popularity, then highlighting, say, the top 10 entries might be useful.

<a href="https://webdesignandsuch.com/add-zebra-striping-to-a-table-with-css3/">WebDesign &amp; Such</a> has created a <a href="https://webdesignandsuch.com/posts/zebra-striping/index.html">demo of zebra striping</a>, which is a perfect example of how you might use <code>nth-child</code> in practice.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d942bb9-a3ef-4ba8-b1bb-9296a5c7cb85/zebra-striping-a-table-with-css3.png"><img class="94736" title="Zebra Striping a Table with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d942bb9-a3ef-4ba8-b1bb-9296a5c7cb85/zebra-striping-a-table-with-css3.png" alt="Screenshot" width="500" height="341" /></a><br>
<em>Zebra striping a table with CSS3.</em>

If none of your tables need styling, then you could do what <a href="https://webvisionaryawards.com/">Webvisionary Awards</a> has done and use <code>:nth-child</code> to style alternating sections of its website. Here’s the CSS:

<pre><code class="language-css">section &gt; section:nth-child(even) {
background:rgba(255,255,255,.1)
url("../images/hr-damaged2.png") 0 bottom no-repeat;
}</code></pre>

The effect is subtle on the website, but it adds a layer of detail that would be missed in older browsers.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4152324b-d91a-49d1-87d7-93036bea959b/wva-2011.png"><img class="94735" title="Webvisionary Awards 2011" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4152324b-d91a-49d1-87d7-93036bea959b/wva-2011.png" alt="Screenshot" width="500" height="350" /></a><br>
<em>The :nth-child selectors in action on Webvisionary Awards.</em>

<strong>iPhone Form Example</strong>
We could use <code>:nth-child</code> in a few places in our iPhone form example, but let’s focus on one. We want to hide the labels for the first three fieldsets from view and use the placeholder text instead. Here’s the CSS:

<pre><code class="language-css">form:nth-child(-n+3) label { display: none; }</code></pre>

Here, we’re looking for the first three children of the <code>&lt;form&gt;</code> element (which are all fieldsets in our code) and then selecting the label. We then hide these labels with <code>display: none;</code>.</p>

### E:nth-last-child(n)

Not content with confusing us all with the <code>:nth-child()</code> pseudo-class, the clever folks over at the W3C have also given us <code>:nth-last-child(n)</code>. It operates much like <code>:nth-child()</code> except in reverse, counting from the last item in the selection.

<pre><code class="language-css">li:nth-last-child(1) { … }</code></pre>

The above will select the last element in a list, whereas the following will select the penultimate element:

<pre><code class="language-css">li:nth-last-child(2) { … }</code></pre>

Of course, you could create other rules, like this one:

<pre><code class="language-css">li:nth-last-child(2n+1) { … }</code></pre>

But you would more likely want to use the following to select the last five elements of a list (based on the logic discussed above):

<pre><code class="language-css">li:nth-last-child(-n+5) { … }</code></pre>

If this still doesn’t make much sense, <a href="https://leaverou.me/">Lea Verou</a> has created a useful <a href="https://leaverou.me/demos/nth.html">CSS3 structural pseudo-class selector tester</a>, which is definitely worth checking out.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6080370-1c4a-4be4-b749-4386bedcd503/css3-structural-pseudo-class-selector-tester.png"><img title="CSS3 structural pseudo-class selector tester" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6080370-1c4a-4be4-b749-4386bedcd503/css3-structural-pseudo-class-selector-tester.png" alt="Screenshot" width="500" height="350" /></a><br>
<em>CSS3 structural pseudo-class selector tester.</em>

<strong>iPhone Form Example</strong>
We can use <code>:nth-last-child</code> in our example to add rounded corners to our input for the “Card number.” Here’s our CSS, which is overly specific but gives you an idea of how we can chain pseudo-selectors together:

<pre><code class="language-css">fieldset:nth-last-child(2) input:nth-last-of-type(3) {
border-radius: 10px; }</code></pre>

We first grab the penultimate fieldset and select the input that is third from last (in this case, our “Card number” input). We then add a <code>border-radius</code>.</p>

### :nth-of-type(n)

Now we’ll get even more specific and apply styles only to particular <em>types</em> of element. For example, let’s say you wanted to style the first paragraph in an article with a larger font. Here’s the CSS:

<pre><code class="language-css">article p:nth-of-type(1) { font-size: 1.5em; }</code></pre>

Perhaps you want to align every other image in an article to the right, and the others to the left. We can use keywords to control this:

<pre><code class="language-css">article img:nth-of-type(odd) { float: right; }
article img:nth-of-type(even) { float: left; }</code></pre>

As with <code>:nth-child()</code> and <code>:nth-last-child()</code>, you can use algebraic expressions:

<pre><code class="language-css">article p:nth-of-type(2n+2) { … }
article p:nth-of-type(-n+1) { … }</code></pre>

It’s worth remembering that if you need to get this specific about targeting elements, then using descriptive class names instead might be more useful.

Simon Foster has created a <a href="https://www.fortherecord.simonfosterdesign.com/">beautiful infographic about his 45 RPM record collection</a>, and he uses <code>:nth-of-type</code> to style some of the data. Here’s a snippet from the CSS, which assigns a different background to each genre type:

<pre><code class="language-css">ul#genre li:nth-of-type(1) {
  width:32.9%;
  background:url(images/orangenoise.jpg);
}
ul#genre li:nth-of-type(2) {
  width:15.2%;
  background:url(images/bluenoise.jpg);
}
ul#genre li:nth-of-type(3) {
  width:13.1%;
  background:url(images/greennoise.jpg);
}</code></pre>

And here’s what it looks like on his website:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db00daa-bfda-43c7-a6f0-f2fddb066e3b/for-the-record.png"><img class="94747" title="For The Record" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db00daa-bfda-43c7-a6f0-f2fddb066e3b/for-the-record.png" alt="Screenshot" width="500" height="350" /></a><br>
<em>The :nth-of-type selectors on “For the Record.”</em>

<strong>iPhone Form Example</strong>
Let’s say we want every second input element to have rounded corners on the bottom. We can achieve this with CSS:

<pre><code class="language-css">input:nth-of-type(even) {
border-bottom-left-radius: 10px;
border-bottom-right-radius: 10px; }</code></pre>

In our example, we want to apply this only to the fieldset for payment, because the fieldset for personal details has three text inputs. We’ll also get a bit tricky and make sure that we <em>don’t</em> select any of the radio inputs. Here’s the final CSS:

<pre><code class="language-css">#payment input:nth-of-type(even):not([type=radio]) {
border-bottom-left-radius: 10px;
border-bottom-right-radius: 10px;
border-bottom: 1px solid #999;
margin-bottom: 10px; }</code></pre>

We’ll explain <code>:not</code> later in this article.</p>

### :nth-last-of-type(n)

Hopefully, by now you see where this is going: <code>:nth-last-of-type()</code> starts at the end of the selected elements and works backwards.

To select the last paragraph in an article, you would use this:

<pre><code class="language-css">article p:nth-last-of-type(1) { … }</code></pre>

You might want to choose this selector instead of <code>:last-child</code> if your articles don’t always end with paragraphs.</p>

### :first-of-type and :last-of-type

If <code>:nth-of-type()</code> and <code>:nth-last-of-type()</code> are too specific for your purposes, then you could use a couple of simplified selectors. For example, instead of this…

<pre><code class="language-css">article p:nth-of-type(1) {
font-size: 1.5em; }</code></pre>

… we could just use this:

<pre><code class="language-css">article p:first-of-type {
font-size: 1.5em; }</code></pre>

As you’d expect, <code>:last-of-type</code> works in exactly the same way but from the last element selected.

<strong>iPhone Form Example</strong>
We can use both <code>:first-of-type</code> and <code>:last-of-type</code> in our iPhone example, particularly when styling the rounded corners. Here’s the CSS:

<pre><code class="language-css">fieldset input:first-of-type:not([type=radio]) {
border-top-left-radius: 10px;
border-top-right-radius: 10px; }

fieldset input:last-of-type:not([type=radio]) {
border-bottom-left-radius: 10px;
border-bottom-right-radius: 10px; }</code></pre>

The first line of CSS adds a top rounded border to all <code>:first-of-type</code> inputs in a fieldset that <em>aren’t</em> radio buttons. The second line adds the bottom rounded border to the last input element in a fieldset.</p>

### :only-of-type

There’s one more <code>type</code> selector to look at: <code>:only-of-type()</code>. This is useful for selecting elements that are the only one of their kind in their parent element.

For example, consider the difference between this CSS selector…

<pre><code class="language-css">p {
font-size: 18px; }</code></pre>

… and this one:

<pre><code class="language-css">p:only-of-type {
font-size: 18px; }</code></pre>

The first selector will style every paragraph element on the page. The second element will grab a paragraph that is the <em>only</em> paragraph in its parent.

This could be handy when you are styling content or data that has been dynamically outputted from a database and the query returns only one result.

Devsnippet has created a demo in which single images are styled differently from multiple images.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91171f03-cf66-48f8-924b-392e57d92539/only-of-type-pseudo-class.png"><img class="94731" title="Devsnippet's :only-of-type demo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91171f03-cf66-48f8-924b-392e57d92539/only-of-type-pseudo-class.png" alt="Screenshot" width="500" height="350" /></a><br>
<em>Devsnippet’s demo for :only-of-type.</em>

<strong>iPhone Form Example</strong>
In the case of our iPhone example, we can make sure that all inputs that are the only children of a fieldset have rounded corners on both the top and bottom. The CSS would be:

<pre><code class="language-css">fieldset input:only-of-type {
border-radius: 10px; }</code></pre>

### :last-child

It’s a little strange that <code>:first-child</code> was part of the CSS2 spec but that its partner in crime, <code>:last-child</code>, didn’t appear until CSS3. It takes no expressions or keywords here; it simply selects the last child of its parent element. For example:

<pre><code class="language-css">li {
border-bottom: 1px solid #ccc; }

li:last-child {
border-bottom: none; }</code></pre>

This is a useful way to remove bottom borders from lists. You’ll see this technique quite often in WordPress widgets.

Rachel Andrew looks at <code>:last-child</code> and other CSS pseudo-selectors in her 24 Ways article “<a href="https://24ways.org/2009/cleaner-code-with-css3-selectors">Cleaner Code With CSS3 Selectors</a>.” Rachel shows us how to use this selector to create a well-formatted image gallery without additional classes.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3420e2f8-4936-4fc6-87f3-6606c8efd758/screen-shot-2011-03-22-at-21.49"><img class="94744" title="Screen shot 2011-03-22 at 21.49.46" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3420e2f8-4936-4fc6-87f3-6606c8efd758/screen-shot-2011-03-22-at-21.49" alt=":last-child CSS in action from Rachel Andrew" width="500" height="350" /></a><br>
<em>The CSS for :last-child in action, courtesy of Rachel Andrew.</em>

### :only-child

If an element is the only child of its parent, then you can select it with <code>:only-child</code>. Unlike with <code>:only-of-type</code>, it doesn’t matter what type of element it is. For example:

<pre><code class="language-css">li:only-child { … }</code></pre>

We could use this to select list elements that are the only list elements in their <code>&lt;ol&gt;</code> or <code>&lt;ul&gt;</code> parent.</p>

### :empty

Finally, in structural pseudo-classes, we have <code>:empty</code>. Not surprisingly, this selects only elements that have no children and no content. Again, this might be useful when dealing with dynamic content outputted from a database.

<pre><code class="language-css">#results:empty {
background-color: #fcc; }</code></pre>

You might use the above to draw the user’s attention to an empty search results section.</p>

## 2\. The Target Pseudo-Class

### :target

This is one of my favourite pseudo-classes, because it allows us to style elements on the page based on the URL. If the URL has an identifier (that follows an <code>#</code>), then the <code>:target</code> pseudo-class will style the element that shares the ID with the identifier. Take a URL that looks like this:
<blockquote>https://www.example.com/css3-pseudo-selectors#summary</blockquote>

The section with the id <code>summary</code> can now be styled like so:

<pre><code class="language-css">:target {
background-color: #fcc; }</code></pre>

This is a great way to style elements on pages that have been linked to from external content. You could also use it with internal anchors to highlight content that users have skipped to.

Perhaps the most impressive use of <code>:target</code> I’ve seen is <a href="https://dev.opera.com/articles/view/css3-target-based-interfaces/">Corey Mwamba’s Scrolling Site of Green</a>. Corey uses some creative CSS3 and the <code>:target</code> pseudo-class to create <a href="https://devfiles.myopera.com/articles/3392/example4.html">animated tabbed navigation</a>. The demo contains some clever use of CSS3, illustrating how pseudo-classes are often best used in combination with other CSS selectors.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fad994d-303f-43b9-a602-c7cad7012d73/coreys-scrolling-site-of-green.png"><img class="94732" title="Corey's Scrolling Site of Green" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fad994d-303f-43b9-a602-c7cad7012d73/coreys-scrolling-site-of-green.png" alt="Screenshot" width="500" height="284" /></a><br>
<em>Corey’s Scrolling Site of Green.</em>

There’s also an interesting example over at <a href="https://webdesignernotebook.com/css/the-css3-target-pseudo-class-and-css-animations/">Web Designer Notebook</a>. In it, <code>:target</code> and Webkit animations are used to highlight blocks of text in target divs. Chris Coyier also creates a <code>:target</code>-based tabbing system at <a href="https://css-tricks.com/css3-tabs/">CSS-Tricks</a>.

<strong>iPhone Form Example</strong>
As you’ll see on my demo page, I’ve added a navigation bar at the top that skips down to different sections of the form. We can highlight any section the user jumps to with the following CSS:

<pre><code class="language-css">:target {
background-color: rgba(255,255,255,0.3);

-webkit-border-radius:
10px;}</code></pre>

## 3\. The UI Element States Pseudo-Classes

### :enabled and :disabled

Together with <code>:checked</code>, <code>:enabled</code> and <code>:disabled</code> make up the three pseudo-classes for UI element states. That is, they allow you to style elements (usually form elements) based on their state. A state could be set by the user (as with <code>:checked</code>) or by the developer (as with <code>:enabled</code> and <code>:disabled</code>). For example, we could use the following:

<pre><code class="language-css">input:enabled {
background-color: #dfd; }

input:disabled {
background-color: #fdd; }</code></pre>

This is a great way to give feedback on what users can and cannot fill in. You’ll often see this dynamic feature enhanced with JavaScript.

<strong>iPhone Form Example</strong>
To illustrate <code>:disabled</code> in practice, I have disabled the form’s “Submit” button in the HTML and added this line of CSS:

<pre><code class="language-css">:disabled {
color: #600; }</code></pre>

The button text is now red!

### :checked

The third pseudo-class here is <code>:checked</code>, which deals with the state of an element such as a checkbox or radio button. Again, this is very useful for giving feedback on what users have selected. For example:

<pre><code class="language-css">input[type=radio]:checked {
font-weight: bold; }</code></pre>

<strong>iPhone Form Example</strong>
As a flourish, we can use CSS to highlight the text next to each radio button once the button has been pressed:

<pre><code class="language-css">input:checked + label {
text-shadow: 0 0 6px #fff; }</code></pre>

We first select any input that has been checked, and then we look for the very next <code>&lt;span&gt;</code> element that contains our text. Highlighting the text with a simple <code>text-shadow</code> is an effective way to provide user feedback.</p>

## 4\. Negation Pseudo-Class

### :not

This is another of my favorites, because it selects everything <em>except</em> the element you specify. For example:

<pre><code class="language-css">:not(footer) { … }</code></pre>

This selects everything on the page that is not a footer element. When used with form inputs, they allow us to get a little sneakier:

<pre><code class="language-css">input:not([type=submit]) { … }
input:not(disabled) { … }</code></pre>

The first line selects every form input that’s not a “Submit” button, which is useful for styling forms. The second selects all input elements that are not enabled; again useful for giving feedback on how to fill in a form.

<strong>iPhone User Example</strong>
You’ve already seen the <code>:not</code> selector in action. It’s particularly powerful when chained with other CSS3 pseudo-selectors. Let’s take a closer look at one example:

<pre><code class="language-css">fieldset input:not([type=radio]) {
margin: 0;
width: 290px;
font-size: 18px;
border-radius: 0;
border-bottom: 0;
border-color: #999;
padding: 8px 10px;}</code></pre>

Here we are selecting all inputs inside fieldset elements that are <em>not</em> radio buttons. This is incredibly useful when styling forms because you will often want to style text inputs different from select boxes, radio buttons and “Submit” buttons.

Check out our final page.</p>

## What’s Old Is New Again

Let’s go back to the beginning of our story and the humble <code>a:link</code>. HTML5 arrived on the scene recently and brought with it an <a href="https://dev.w3.org/html5/spec/Overview.html#the-a-element">exciting change</a> to the <code>&lt;a&gt;</code> element that gives the CSS3 pseudo-selector an additive effect.

An <code>&lt;a&gt;</code> element can now be wrapped around block-level elements, turning whole sections of your page into links (as long as those sections don’t contain other interactive elements). Whereas JavaScript was once popular for making entire <code>&lt;div&gt;</code> elements clickable, you can now do so by wrapping sections in <code>&lt;a&gt;</code> tags, like so:

<pre><code class="language-markup tmp-html">&lt;a href="https://www.smashing-magazine.com"&gt;
&lt;div id="advert"&gt;
&lt;hgroup&gt;
&lt;h1&gt;Jackson’s Widgets&lt;/h1&gt;
&lt;h2&gt;The finest widgets in Kentucky&lt;/h2&gt;
&lt;/hgroup&gt;
&lt;p&gt;Buy Jackson’s Widgets today,
and be sure of a trouble-free life for you,
your widget and your machinery.
Trusted and sold since 1896.&lt;/p&gt;
&lt;/div&gt;
&lt;/a&gt;</code></pre>

The implication for CSS pseudo-selectors is that you can now style a <code>&lt;div&gt;</code> based on whether it is being hovered over (<code>a:hover</code>) or is active (<code>a:active</code>), like so:

<pre><code class="language-css">a:hover #advert {
background-color: #f7f7f7; }</code></pre>

Anything that decreases JavaScript and increases semantic code has to be good!

## Cross-Browser Compatibility

You had to ask, didn’t you! Unbelievably, Internet Explorer 8 (and earlier) doesn’t support any of these selectors, whereas the latest versions of Chrome, Opera, Safari and Firefox all do. Before your blood boils, consider the following solutions.</p>

### Internet Explorer 9

Unless you’ve been living under a rock for the last week, you’ll have heard that Microsoft unleashed its latest browser on an unsuspecting public. The good thing is, it’s actually quite good. While I don’t expect people who are reading this article to change their browsing habits, <strong>it’s worth remembering</strong> that the majority of the world uses IE; and thanks to Windows Update and a global marketing campaign, we can hope to see IE9 as the dominant Windows browser in the near future. That’s good for Web designers, and it’s good for pseudo-selectors. But what about IE8 and its ancestors?

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f8b887f-8103-43fd-befd-992943d91774/ie9.png"><img class="94124" title="ie9" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f8b887f-8103-43fd-befd-992943d91774/ie9.png" alt="Screenshot" width="550" height="352" /></a><br>
<em>Internet Explorer 9 is here.</em>

### JavaScript

Our old friend JavaScript comes to the rescue. I particularly like <a href="https://selectivizr.com/">Selectivizr</a> by Keith Clark. Keith has put together a lovely script that, in combination with your JavaScript library of choice, adds CSS3 pseudo-class selector functionality for earlier versions of IE. Be warned that some libraries fare better than others: if you’re using MooTools with Selectivizr, then all the pseudo-classes will be available, but if you’re relying on jQuery to do the heavy lifting, then a number of the selectors won’t work at all.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a806a95-37ea-4d36-8cc8-af27755e68dc/selectivizr.jpg"><img class="93196" title="selectivizr" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a806a95-37ea-4d36-8cc8-af27755e68dc/selectivizr.jpg" alt="Screenshot" width="550" height="344" /></a><br>
<em>Selectivizr.</em>

Keith recently released a <a href="https://github.com/keithclark/JQuery-Extended-Selectors">jQuery plug-in</a> that extends jQuery to include support for the following CSS3 pseudo-class selectors:

*   `:first-of-type`
*   `:last-of-type`
*   `:only-of-type`
*   `:nth-of-type`
*   `:nth-last-of-type`

It’s also worth looking at the ubiquitous <em>ie7.js</em> script (and its successors) by <a href="https://code.google.com/p/ie7-js/">Dean Edwards</a>. This script solves a number of IE-related problems, including CSS3 pseudo-selectors.</p>

### So, Should We Start Using CSS3 Pseudo-Selectors Today?

I guess the answer to that question depends on how you view JavaScript. It’s true that pseudo-selectors can be completely replaced with classes and IDs; but it’s also true that, when styling complex layouts, pseudo-selectors are both incredibly useful and the natural next step for your CSS. If you find that they<strong> improve the readability of your CSS</strong> and reduce the need for (non-semantic) classes in your HTML, then it I’d definitely recommend embracing them today.

You could use two selectors and fall back on a class name, but that would just duplicate work. It also means that you wouldn’t need the pseudo-classes in the first place. But if you did choose to go down this path, the code might look something like this:

<pre><code class="language-css">li:nth-of-type(3),
li.third { … }</code></pre>

This method is not as flexible as using pseudo-classes because you have to keep updating the HTML and CSS when the page content changes.

If a lot of your users don’t have JavaScript enabled, that puts you in a bit of a bind. Many Web designers argue that functionality (i.e. JavaScript) is different from layout (i.e. CSS), and so you should not rely on JavaScript to make pseudo-selectors work in IE8 and earlier.

While I agree with the principle, in practice I believe that providing the best possible experience to 99% of your users is better than accounting for the remaining 1% (or however big your non-JavaScript base may be).

Follow your website’s analytics, and <strong>be prepared to make decisions that improve your skills</strong> as a Web designer and, more importantly, provide the best experience possible to the majority of users.</p>

## Final Thoughts

It’s hard not to be depressed by IE8’s complete lack of support for pseudo-classes. Arguably, having the browser calculate and recalculate page styles in this fashion will have implications for rendering speed; but because all other major browsers now support these selectors, it’s frustrating that most of our users can’t benefit from them without a JavaScript hack.

But as Professor Farnsworth says, “Good news everyone!” Breaking on the horizon is the dawn of Internet Explorer 9, and Microsoft has made sure that its new browser <a href="https://msdn.microsoft.com/en-us/library/cc351024(v=vs.85).aspx#pseudoclasses">supports each and every one</a> of the selectors discussed in this article.

CSS3 pseudo-selectors won’t likely take up large chunks of your style sheets. They are specific yet dynamic and are more likely, at least initially, to add finishing touches to a page than to set an overall style. Perhaps you want to drop the bottom border in the last item of a list, or give visual feedback to users as they fill in a form. <strong>This is all possible with CSS3</strong>, and as usage becomes more mainstream, I expect these will become a regular part of the Web designer’s toolbox.

If you’ve seen any interesting or exciting uses of these selectors out there in the field, do let us know in the comments below.</p>

### Other Resources

You may be interested in the following articles and related resources:

*   [The Official CSS3 Selectors Proposed Recommendation](https://www.w3.org/TR/css3-selectors/) Everything you need to know, from the folks in charge.
*   [Wikipedia’s Guide to Cascading Style Sheets](https://en.wikipedia.org/wiki/Cascading_Style_Sheets) A good background read, and the bibliography is a great resource.
*   [How nth-child Works](https://css-tricks.com/how-nth-child-works/) A comprehensive guide from the ever-reliable Chris Coyier.
*   [Internet Explorer 9](https://windows.microsoft.com/en-US/internet-explorer/downloads/ie-9/worldwide-languages) If you haven’t yet played around with Redmond’s latest offering, you’re in for a pleasant surprise.

<em>(al) (ik)</em>

