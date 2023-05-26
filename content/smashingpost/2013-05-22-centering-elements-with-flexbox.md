---
title: 'Flexbox Is As Easy As Pie: Designing CSS Layouts'
slug: centering-elements-with-flexbox
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51226ad3-6cf5-4908-bb79-6fdaf4e1f539/centering-elements-with-flexbox.jpg
date: 2013-05-22T11:29:09.000Z
author: david-storey
description: >-
  _Flexible box layout_ (or _flexbox_) is a new box model optimized for UI
  layout. As one of the first CSS modules designed for actual layout (floats
  were really meant mostly for things such as wrapping text around images), it
  makes a lot of tasks much easier, or even possible at all.
categories:
  - Coding
  - Tools
  - Layouts
  - CSS
  - Flexbox
---
Flexbox (or flexible box layout) is a new box model optimized for UI layout. As one of the first CSS modules designed for actual layout (floats were really meant mostly for things such as wrapping text around images), it <strong>makes a lot of tasks much easier</strong>, or even possible at all. Flexbox’s repertoire includes the simple centering of elements (both horizontally and vertically), the expansion and contraction of elements to fill available space, and source-code independent layout, among others abilities.

<img loading="lazy" decoding="async" title="Flexbox Is As Easy As Pie - Designing CSS Layouts" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a39c92e-41ac-44dc-ada0-2cd520954beb/figure1.1_mini" alt="Flexbox Is As Easy As Pie - Designing CSS Layouts" width="500" height="354" />

Flexbox has lived a storied existence. It started as a feature of Mozilla’s XUL, where it was used to lay out application UI, such as the toolbars in Firefox, and it has since been rewritten multiple times. The specification has only recently reached stability, and we have fairly complete support across the latest versions of the leading browsers.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">The Flexbox Reading List: Techniques And Tools</span>](https://www.smashingmagazine.com/2016/02/the-flexbox-reading-list/)
*   [Harnessing Flexbox For Today’s Web Apps](https://www.smashingmagazine.com/2015/03/harnessing-flexbox-for-todays-web-apps/)
*   [CSS Grid, Flexbox And Box Alignment](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)
*   [Laying Out A Flexible Future For Web Design With Flexbox](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/)

{{% feature-panel %}}

There are, however, some caveats. The specification changed between the implementation in Internet Explorer (IE) and the release of IE 10, so you will need to use a slightly different syntax. Chrome currently still requires the <code>-webkit-</code> prefix, and Firefox and Safari are still on the much older syntax. Firefox has updated to the latest specification, but that implementation is currently behind a runtime flag until it is considered stable and bug-free enough to be turned on by default. Until then, Firefox still requires the old syntax.

When you specify that an element will use the flexbox model, its children are laid out along either the horizontal or vertical axis, depending on the direction specified. The widths of these children expand or contract to fill the available space, based on the flexible length they are assigned.</p>

## Example: Horizontal And Vertical Centering (Or The Holy Grail Of Web Design)

Being able to center an element on the page is perhaps the number one wish among Web designers — yes, probably even higher than gaining the highly prized parent selector or putting IE 6 out of its misery (OK, maybe a close second then). With flexbox, this is trivially easy. Let’s start with a basic HTML template, with a <a href="https://jsfiddle.net/pnNqd/">heading that we want to center</a>.

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
   &lt;meta charset="utf-8"/&gt;
   &lt;title&gt;Centering an Element on the Page&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
   &lt;h1&gt;OMG, I’m centered&lt;/h1&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

Nothing special here, not even a wrapper <code>div</code>. <strong>The magic all happens in the CSS:</strong>

<pre><code class="language-css">html {
   height: 100%;
}

body {
   display: -webkit-box;   /* OLD: Safari,  iOS, Android browser, older WebKit browsers.  */
   display: -moz-box;      /* OLD: Firefox (buggy) */
   display: -ms-flexbox;   /* MID: IE 10 */
   display: -webkit-flex;  /* NEW, Chrome 21–28, Safari 6.1+ */
   display: flex;          /* NEW: IE11, Chrome 29+, Opera 12.1+, Firefox 22+ */

   -webkit-box-align: center; -moz-box-align: center; /* OLD… */
   -ms-flex-align: center; /* You know the drill now… */
   -webkit-align-items: center;
   align-items: center;

   -webkit-box-pack: center; -moz-box-pack: center;
   -ms-flex-pack: center;
   -webkit-justify-content: center;
   justify-content: center;

   margin: 0;
   height: 100%;
   width: 100% /* needed for Firefox */
}

h1 {
   display: -webkit-box; display: -moz-box;
   display: -ms-flexbox;
   display: -webkit-flex;
   display: flex;
   -webkit-box-align: center; -moz-box-align: center;
   -ms-flex-align: center;
   -webkit-align-items: center;
   align-items: center;

   height: 10rem;
}</code></pre>

I’ve included all of the <strong>different prefixed versions in the CSS above</strong>, from the very oldest, which is still needed, to the modern and hopefully final syntax. This might look confusing, but the different syntaxes map fairly well to each other, and I’ve included tables at the end of this article to show the exact mappings.

This is not exactly all of the CSS needed for our example, because I’ve stripped out the extra styling that you probably already know how to use in order to save space.

Let’s look at the CSS that is needed to center the heading on the page. First, we set the <code>html</code> and <code>body</code> elements to have 100% <code>height</code> and remove any margins. This will make the container of our <code>h1</code> take up the full height of the browser’s window. Firefox also needs a <code>width</code> specified on the body to force it to behave. Now, we just need to center everything.</p>

### Enabling Flexbox

Because the <code>body</code> element contains the heading that we want to center, we will set its <code>display</code> value to <code>flex</code>:

<pre><code class="language-css">body {
   display: flex;
}</code></pre>

This switches the <code>body</code> element to use the flexbox layout, rather than the regular block layout. All of its children in the flow of the document (i.e. not absolutely positioned elements) will now become flex items.

The syntax used by IE 10 is <code>display: -ms-flexbox</code>, while older Firefox and WebKit browsers use <code>display: -<var>prefix</var>-box</code> (where <var>prefix</var> is either <code>moz</code> or <code>webkit</code>). You can see the tables at the end of this article to see the mappings of the various versions.

What do we gain now that our elements have been to yoga class and become all flexible? They gain untold powers: they can flex their size and position relative to the available space; they can be laid out either horizontally or vertically; and they can even achieve source-order independence. (Two holy grails in one specification? We’re doing well.)

### Centering Horizontally

Next, we want to horizontally center our <code>h1</code> element. No big deal, you might say; but it is somewhat easier than playing around with <code>auto</code> margins. <strong>We just need to tell the flexbox to center its flex items.</strong> By default, flex items are laid out horizontally, so setting the <code>justify-content</code> property will align the items along the main axis:

<pre><code class="language-css">body {
   display: flex;
   justify-content: center;
}</code></pre>

For IE 10, the property is called <code>flex-pack</code>, while for older browsers it is <code>box-pack</code> (again, with the appropriate prefixes). The other possible values are <code>flex-start</code>, <code>flex-end</code>, <code>space-between</code> and <code>space-around</code>. These are <code>start</code>, <code>end</code>, <code>justify</code> and <code>distribute</code>, respectively, in IE 10 and the old specification (<code>distribute</code> is, however, not supported in the old specification). The <code>flex-start</code> value aligns to the left (or to the right with right-to-left text), <code>flex-end</code> aligns to the right, <code>space-between</code> evenly distributes the elements along the axis, and <code>space-around</code> evenly distributes along the axis, with half-sized spaces at the start and end of the line.

To explicitly set the axis that the element is aligned along, you can do this with the <code>flex-flow</code> property. The default is <code>row</code>, which will give us the same result that we’ve just achieved. To align along the vertical axis, we can use <code>flex-flow: column</code>. If we add this to our example, you will notice that the element is vertically centered but loses the horizontal centering. Reversing the order by appending <code>-reverse</code> to the <code>row</code> or <code>column</code> values is also possible (<code>flex-flow: row-reverse</code> or <code>flex-flow: column-reverse</code>), but that won’t do much in our example because we have only one item.

There are some differences here in the various versions of the specification, which are highlighted at the end of this article. Another caveat to bear in mind is that <code>flex-flow</code> directions are <code>writing-mode</code> sensitive. That is, when using <code>writing-mode: vertical-rl</code> to switch to vertical text layout (as used traditionally in China, Japan and Korea), <code>flex-flow: row</code> will align the items vertically, and <code>column</code> will align them horizontally.</p>

### Centering Vertically

Centering vertically is as easy as centering horizontally. We just need to use the appropriate property to align along the “cross-axis.” The what? The cross-axis is basically the axis perpendicular to the main one. So, if flex items are aligned horizontally, then the cross-axis would be vertical, and vice versa. We set this with the <code>align-items</code> property (<code>flex-align</code> in IE 10, and <code>box-align</code> for older browsers):

<pre><code class="language-css">body {
   /* Remember to use the other versions for IE 10 and older browsers! */
   display: flex;
   justify-content: center;
   align-items: center;
}</code></pre>

This is all there is to centering elements with flexbox! We can also use the <code>flex-start</code> (start) and <code>flex-end</code> (end) values, as well as <code>baseline</code> and <code>stretch</code>. Let’s have another look at the finished example:

You might notice that the text is also center-aligned vertically inside the <code>h1</code> element. This could have been done with margins or a line height, but we used flexbox again to show that it works with anonymous boxes (in this case, the line of text inside the <code>h1</code> element). No matter how high the <code>h1</code> element gets, the text will always be in the center:

<pre><code class="language-css">h1 { flex;
   align-items: center;
   height: 10rem;
}</code></pre>

## Flexible Sizes

If centering elements was all flexbox could do, it’d be pretty darn cool. But there is more. Let’s see how flex items can expand and contract to fit the available space within a flexbox element.

<figure class="break-out" ><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f975f27d-b595-4fad-b44b-4eda91491f4a/figure1.2_mini" alt="flexbox img 2" width="500" height="336" /><figcaption>An interactive slideshow built using flexbox.</figcaption></figure>

The HTML and CSS for this example are similar to the previous one’s. We’re enabling flexbox and centering the elements on the page in the same way. In addition, we want to make the title (inside the <code>header</code> element) remain consistent in size, while the five boxes (the <code>section</code> elements) adjust in size to fill the width of the window. To do this, we use the new <code>flex</code> property:

<pre><code class="language-css">section {
   /* removed other styles to save space */
   -prefix-box-flex: 1; /* old spec webkit, moz */
   flex: 1;
   height: 250px;
}</code></pre>

What we’ve just done here is to make each section element take up 1 flex unit. Because we haven’t set any explicit width, each of the five boxes will be the same width. The <code>header</code> element will take up a set width (277 pixels) because it is not flexible. We divide the remaining width inside the <code>body</code> element by 5 to calculate the width of each of the section elements. Now, if we resize the browser window, the section elements will grow or shrink.

In this example, we’ve set a consistent height, but this could be set to be flexible, too, in exactly the same way. We probably wouldn’t always want all elements to be the same size, so let’s make one bigger. On hover, we’ve set the element to take up 2 flex units:

<pre><code class="language-css">section:hover {
   -prefix-box-flex: 2;
   flex: 2;
   cursor: pointer;
}</code></pre>

Now the available space is divided by 6 rather than 5, and the hovered element gets twice the base amount. Note that an element with 2 flex units does not necessarily become twice as wide as one with 1 unit. It just gets twice the share of the available space added to its “preferred width.” In our examples, the “preferred width” is 0 (the default).</p>

## Source-Order Independence

For our last party trick, we’ll study how to achieve source-order independence in our layouts. When clicking on a box, we will tell that element to move to the left of all the other boxes, directly after the title. All we have to do is set the order with the <code>order</code> property. By default, all flex items are in the 0 position. Because they’re in the same position, they follow the source order.

<figure class="break-out" ><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b24f2dbf-7a2e-4cb5-8b0a-1f9d784dcc54/figure1.3_mini" alt="flexbox figure1.3_mini" width="500" height="347" /><figcaption>An interactive slideshow with <code>flex-order</code>.</figcaption></figure>

To make our chosen element move to the first position, we just have to set a lower number. I chose <code>-1</code>. We also need to set the header to <code>-1</code> so that the selected section element doesn’t get moved before it:

<pre><code class="language-css">header {
   -prefix-box-ordinal-group: 1; /* old spec; must be positive */
   -ms-flex-order: -1; /* IE 10 syntax */
   order: -1; /* new syntax */
}

section[aria-pressed="true"] {
   /* Set order lower than 0 so it moves before other section elements,
      except old spec, where it must be positive.
 */
   -prefix-box-ordinal-group: 1;
   -ms-flex-order: -1;
   order: -1;

   -prefix-box-flex: 3;
   flex: 3;
   max-width: 370px; /* Stops it from getting too wide. */
}</code></pre>

In the old specification, the property for setting the order (<code>box-ordinal-group</code>) accepts only a positive integer. Therefore, I’ve set the order to <code>2</code> for each section element (code not shown) and updated it to <code>1</code> for the active element. If you are wondering what <code> aria-pressed="true"</code> means in the example above, it is a WAI-ARIA attribute/value that I add via JavaScript when the user clicks on one of the sections.

This relays accessibility hints to the underlying system and to assistive technology to tell the user that that element is pressed and, thus, active. If you’d like more information on WAI-ARIA, check out “<a href="https://dev.opera.com/articles/view/introduction-to-wai-aria/">Introduction to WAI-ARIA</a>” by Gez Lemon. Because I’m adding the attribute after the user clicks, this example requires a simple JavaScript file in order to work, but flexbox itself doesn’t require it; it’s just there to handle the user interaction.

Hopefully, this has given you some inspiration and enough introductory knowledge of flexbox to enable you to experiment with your own designs.</p>

## Syntax Changes

As you will have noticed throughout this article, the syntax has changed a number of times since it was first implemented. To aid backward- and forward-porting between the different versions, we’ve included tables below, which <strong>map the changes between the specifications</strong>.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>IE</strong></td>
<td><strong>Opera</strong></td>
<td><strong>Firefox</strong></td>
<td><strong>Chrome</strong></td>
<td><strong>Safari</strong></td>
</tr>
<tr>
<td>Standard</td>
<td>11</td>
<td>12.10+ *</td>
<td>22</td>
<td>29+,
21–28 (<code>-webkit-</code>)</td>
<td></td>
</tr>
<tr>
<td>Mid</td>
<td>10 (<code>-ms-</code>)</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>Old</td>
<td></td>
<td></td>
<td>3–21 (<code>-moz-</code>)</td>
<td>&lt;21 (<code>-webkit-</code>)</td>
<td>3–6 (<code>-webkit-</code>)</td>
</tr>
</tbody>
</table>
<caption><em>Specification versions</em></caption><br></br>

<p>When Opera switched to Blink in version 15 it required the <code>-webkit-</code> prefix. The prefix was dropped in Opera 16.</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>Block-level flex</strong></td>
<td><strong>Inline-level flex</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>display</code></td>
<td><code>flex</code></td>
<td><code>inline-flex</code></td>
</tr>
<tr>
<td>Mid</td>
<td><code>display</code></td>
<td><code>flexbox</code></td>
<td><code>inline-flexbox</code></td>
</tr>
<tr>
<td>Old</td>
<td><code>display</code></td>
<td><code>box</code></td>
<td><code>inline-box</code></td>
</tr>
</tbody>
</table>
<caption><em>Enabling flexbox: setting an element to be a flex container</em></caption><br></br>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>start</strong></td>
<td><strong>center</strong></td>
<td><strong>end</strong></td>
<td><strong>justify</strong></td>
<td><strong>distribute</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>justify-content</code></td>
<td><code>flex-start</code></td>
<td><code>center</code></td>
<td><code>flex-end</code></td>
<td><code>space-between</code></td>
<td><code>space-around</code></td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex-pack</code></td>
<td><code>start</code></td>
<td><code>center</code></td>
<td><code>end</code></td>
<td><code>justify</code></td>
<td><code>distribute</code></td>
</tr>
<tr>
<td>Old</td>
<td><code>box-pack</code></td>
<td><code>start</code></td>
<td><code>center</code></td>
<td><code>end</code></td>
<td><code>justify</code></td>
<td>N/A</td>
</tr>
</tbody>
</table>

<caption><em>Axis alignment: specifying alignment of items along the main flexbox axis</em></caption><br></br>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>start</strong></td>
<td><strong>center</strong></td>
<td><strong>end</strong></td>
<td><strong>baseline</strong></td>
<td><strong>stretch</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>align-items</code></td>
<td><code>flex-start</code></td>
<td><code>center</code></td>
<td><code>flex-end</code></td>
<td><code>baseline</code></td>
<td><code>stretch</code></td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex-align</code></td>
<td><code>start</code></td>
<td><code>center</code></td>
<td><code>end</code></td>
<td><code>baseline</code></td>
<td><code>stretch</code></td>
</tr>
<tr>
<td>Old</td>
<td><code>box-align</code></td>
<td><code>start</code></td>
<td><code>center</code></td>
<td><code>end</code></td>
<td><code>baseline</code></td>
<td><code>stretch</code></td>
</tr>
</tbody>
</table>
<caption><em>Cross-axis alignment: specifying alignment of items along the cross-axis</em></caption><br></br>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>auto</strong></td>
<td><strong>start</strong></td>
<td><strong>center</strong></td>
<td><strong>end</strong></td>
<td><strong>baseline</strong></td>
<td><strong>stretch</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>align-self</code></td>
<td><code>auto</code></td>
<td><code>flex-start</code></td>
<td><code>center</code></td>
<td><code>flex-end</code></td>
<td><code>baseline</code></td>
<td><code>stretch</code></td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex-item-align</code></td>
<td><code>auto</code></td>
<td><code>start</code></td>
<td><code>center</code></td>
<td><code>end</code></td>
<td><code>baseline</code></td>
<td><code>stretch</code></td>
</tr>
<tr>
<td>Old</td>
<td colspan="7">N/A</td>
</tr>
</tbody>
</table>

<caption><em>Individual cross-axis alignment: override to align individual items along the cross-axis</em></caption><br></br>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>start</strong></td>
<td><strong>center</strong></td>
<td><strong>end</strong></td>
<td><strong>justify</strong></td>
<td><strong>distribute</strong></td>
<td><strong>stretch</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>align-content</code></td>
<td><code>flex-start</code></td>
<td><code>center</code></td>
<td><code>flex-end</code></td>
<td><code>space-between</code></td>
<td><code>space-around</code></td>
<td><code>stretch</code></td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex-line-pack</code></td>
<td><code>start</code></td>
<td><code>center</code></td>
<td><code>end</code></td>
<td><code>justify</code></td>
<td><code>distribute</code></td>
<td><code>stretch</code></td>
</tr>
<tr>
<td>Old</td>
<td colspan="7">N/A</td>
</tr>
</tbody>
</table>

<caption><em>Flex line alignment: specifying alignment of flex lines along the cross-axis</em></caption><br></br>

This takes effect only when there are multiple flex lines, which is the case when flex items are allowed to wrap using the <code>flex-wrap</code> property and there isn’t enough space for all flex items to display on one line. This will align each line, rather than each item.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>order</code></td>
<td>&lt;number&gt;</td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex-order</code></td>
<td><code>&lt;<var>number</var>&gt;</code></td>
</tr>
<tr>
<td>Old</td>
<td><code>box-ordinal-group</code></td>
<td><code>&lt;<var>integer</var>&gt;</code></td>
</tr>
</tbody>
</table>

<caption><em>Display order: specifying the order of flex items</em></caption><br></br>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>flex</code></td>
<td><code>none</code> | [ <code>&lt;<var>flex-grow</var>&gt;</code> <code>&lt;<var>flex-shrink<var>&gt;</var></var></code>? || <code>&lt;<var>flex-basis</var>&gt;</code>]</td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex</code></td>
<td><code>none</code> | [ [ <code>&lt;<var>pos-flex</var>&gt;</code> <code>&lt;<var>neg-flex</var>&gt;</code>? ] || <code>&lt;<var>preferred-size</var>&gt;</code> ]</td>
</tr>
<tr>
<td>Old</td>
<td><code>box-flex</code></td>
<td><code>&lt;<var>number</var>&gt;</code></td>
</tr>
</tbody>
</table>
<caption><em>Flexibility: specifying how the size of items flex</em></caption><br></br>

The flex property is more or less unchanged between the new standard and the draft supported by Microsoft. The main difference is that it has been converted to a shorthand in the new version, with separate properties: <code>flex-grow</code>, <code>flex-shrink</code> and <code>flex-basis</code>. The values may be used in the same way in the shorthand. However, the default value for <code>flex-shrink</code> (previously called negative flex) is now <code>1</code>. This means that items do not shrink by default. Previously, negative free space would be distributed using the <code>flex-shrink</code> ratio, but now it is distributed in proportion to <code>flex-basis</code> multiplied by the <code>flex-shrink</code> ratio.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>Horizontal</strong></td>
<td><strong>Reversed horizontal</strong></td>
<td><strong>Vertical</strong></td>
<td><strong>Reversed vertical</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>flex-direction</code></td>
<td><code>row</code></td>
<td><code>row-reverse</code></td>
<td><code>column</code></td>
<td><code>column-reverse</code></td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex-direction</code></td>
<td><code>row</code></td>
<td><code>row-reverse</code></td>
<td><code>column</code></td>
<td><code>column-reverse</code></td>
</tr>
<tr>
<td>Old</td>
<td><code>box-orient</code>
<code>box-direction</code></td>
<td><code>horizontal</code>
<code>normal</code></td>
<td><code>horizontal</code>
<code>reverse</code></td>
<td><code>vertical</code>
<code>normal</code></td>
<td><code>vertical</code>
<code>reverse</code></td>
</tr>
</tbody>
</table>
<caption><em>Direction: specifying the direction of the main flexbox axis</em></caption><br></br>

In the old version of the specification, the <code>box-direction</code> property needs to be set to <code>reverse</code> to get the same behavior as <code>row-reverse</code> or <code>column-reverse</code> in the later version of the specification. This can be omitted if you want the same behavior as <code>row</code> or <code>column</code> because <code>normal</code> is the initial value.

When setting the <code>direction</code> to <code>reverse</code>, the main flexbox axis is flipped. This means that when using a left-to-right writing system, the items will display from right to left when <code>row-reverse</code> is specified. Similarly, <code>column-reverse</code> will lay out flex items from bottom to top, instead of top to bottom.

The old version of the specification also has writing mode-independent values for <code>box-orient</code>. When using a left-to-write writing system, <code>horizontal</code> may be substituted for <code>inline-axis</code>, and <code>vertical</code> may be substituted for <code>block-axis</code>. If you are using a top-to-bottom writing system, such as those traditional in East Asia, then these values would be flipped.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td class="spec"><strong>Speci-
fication</strong></td>
<td><strong>Property name</strong></td>
<td><strong>No wrapping</strong></td>
<td><strong>Wrapping</strong></td>
<td><strong>Reversed wrap</strong></td>
</tr>
<tr>
<td>Standard</td>
<td><code>flex-wrap</code></td>
<td><code>nowrap</code></td>
<td><code>wrap</code></td>
<td><code>wrap-reverse</code></td>
</tr>
<tr>
<td>Mid</td>
<td><code>flex-wrap</code></td>
<td><code>nowrap</code></td>
<td><code>wrap</code></td>
<td><code>wrap-reverse</code></td>
</tr>
<tr>
<td>Old</td>
<td><code>box-lines</code></td>
<td><code>single</code></td>
<td><code>multiple</code></td>
<td>N/A</td>
</tr>
</tbody>
</table>
<caption><em>Wrapping: specifying whether and how flex items wrap along the cross-axis</em></caption><br></br>

The <code>wrap-reverse</code> value flips the start and end of the cross-axis, so that if flex items are laid out horizontally, instead of items wrapping onto a new line below, they will wrap onto a new line above.

At the time of writing, Firefox does not support the <code>flex-wrap</code> or older <code>box-lines</code> property. It also doesn’t support the shorthand.

The current specification has a <code>flex-flow</code> shorthand, which controls both wrapping and direction. The behavior is the same as the one in the version of the specification implemented by IE 10. It is also currently not supported by Firefox, so I would recommend to avoid using it when specifying only the <code>flex-direction</code> value.</p>

## Conclusion

Well, that’s a (flex-)wrap. In this article, I’ve introduced some of <strong>the myriad of possibilities afforded by flexbox</strong>. Be it source-order independence, flexible sizing or just the humble centering of elements, I’m sure you can find ways to employ flexbox in your websites and applications. The syntax has settled down (finally!), and implementations are here. All major browsers now support flexbox in at least their latest versions.

While older versions of browser use different syntaxes, all the latest versions of the major browsers now support Flexbox in its final form. These browsers also no longer require prefixes, except (at the time of writing) Safari 6.1 and above. For the time being, to support all browsers, use the tables above to map the various syntaxes, and get your flex on.

Layout in CSS is only getting more powerful, and flexbox is one of the first steps out of the quagmire we’ve found ourselves in over the years, first with table-based layouts, then float-based layouts. IE 10 already supports an early draft of the Grid layout specification, which is great for page layout, and Regions and Exclusions will revolutionize how we handle content flow and layout.

Flexbox can be used today if you only need to support relatively modern browsers or can provide a fallback, and in the not too distant future, all sorts of options will be available, so that we can use the best tool for the job. Flexbox is shaping up to be a mighty fine tool.

<em>This article is an updated excerpt of the chapter "Restyle, Recode, Reimagine With CSS3" from our <a href="https://shop.smashingmagazine.com/smashing-book-3-print-bundle.html">Smashing Book #3</a>, written by Lea Verou and David Storey.</em> — Ed.</p>

{{< signature "al" >}}

