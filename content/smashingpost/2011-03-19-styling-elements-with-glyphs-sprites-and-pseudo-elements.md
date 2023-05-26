---
title: 'Styling Elements With Glyphs, Sprites and Pseudo-Elements'
slug: styling-elements-with-glyphs-sprites-and-pseudo-elements
image: null
date: 2011-03-19T17:34:43.000Z
author: thierry-koblentz
description: >-
  In 2002, Mark Newhouse published the article "[Taming Lists](https://www.alistapart.com/articles/taminglists/)", a very interesting piece in which he explained how to create custom list markers using pseudo-elements. Almost a decade later, Nicolas Gallagher came up with the technique [pseudo background-crop](https://nicolasgallagher.com/css-background-image-hacks/demo/crop.html
  "Emulating background-crop") which uses pseudo-elements with a sprite
categories:
  - Coding
  - Typography
  - CSS
  - Techniques
---
Today, on the shoulders of giants, we'll try to push the envelope. We'll discuss how you can style elements with no extra markup and using a bidi-friendly [high-contrast proof CSS sprite](https://www.paciellogroup.com/blog/2010/01/high-contrast-proof-css-sprites/ "high contrast proof CSS sprites") technique. The technique will work in Internet Explorer 6/7 as well.

![Displaying icons in links and as custom list markers ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02aaa190-df5e-4b81-86b9-95708da9df16/figure-1.png)

## Starting with special characters

There is a [plethora of glyphs](https://inamidst.com/stuff/unidata/) out there that we could use instead of images to create custom markers. This should improve:

{{% feature-panel %}}

*   performance (there is no HTTP request)
*   usability (these characters will grow or shrink according to user's settings)
*   maintenance (no sprite to create, no asset to deal with)
*   accessibility (see further below).</p>

### Example:

The markers (♠, ♣, ♥, ♦) in the list above are created via the following rules:

**HTML:**

<pre><code class="language-markup tmp-xml">&lt;ul class="glyphs"&gt; 
	&lt;li class="one"&gt;performance&lt;/li&gt;
	&lt;li class="two"&gt;usability&lt;/li&gt; 
	&lt;li class="three red"&gt;maintenance &lt;/li&gt; 
	&lt;li class="four red"&gt;accessibility&lt;/li&gt; 
&lt;/ul&gt;</code></pre>

**CSS:**

<pre><code class="language-css">.glyphs {
  list-style-type: none;
}

.glyphs li:before,
.glyphs b {
  display: inline-block;
  width: 1.5em;
  font-size: 1.5em;
  text-align: center;
}

.one {
        background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&spades;</b>'+this.innerHTML);
}
.one:before {
        content: "2660"; /* ♠ */
}
.two {
        background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&clubs;</b>'+this.innerHTML);
}
.two:before {
        content: "2663"; /* ♣ */
}
.three {
        background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&hearts;</b>'+this.innerHTML);
}
.three:before {
        content: "2665"; /* ♥ */
}
.four {
        background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&diams;</b>'+this.innerHTML);
}
.four:before {
        content: "2666"; /* ♦ */
} 

.red b,
.red:before {
  color: red;
}</code></pre>

### How does this work?

*   The value of the content property must be an escaped reference to the hexadecimal [Unicode character](https://www.fileformat.info/info/unicode/char/2666/index.htm "Unicode Character 'BLACK DIAMOND SUIT' (U+2666)") value (for IE, we use [HTML entities](https://www.w3.org/TR/html40/sgml/entities.html "Character entity references in HTML 4")).
*   Internet Explorer 6/7 do not support `::before` nor `:before`, so the characters are plugged via CSS expressions.
*   IE8 does not support `::before`, but does support the single colon notation
*   Please notice that putting aside browser support, "[there’s no difference](https://www.impressivewebs.com/before-after-css3/) between `:before` and `::before`, or between `:after` and `::after`. The single colon syntax (e.g. `:before` or `:first-child`) is the syntax used for both pseudo-classes and pseudo-selectors in all versions of CSS prior to CSS3\. With the introduction of CSS3, in order to make a differentiation between pseudo-classes and pseudo-elements, in CSS3 all pseudo-elements must use the double-colon syntax, and all pseudo-classes must use the single-colon syntax."
*   In IE, characters are wrapped in `<b>` elements, so we have a means to target and style them (you may rather want to rely on a class name for that).

Note that the CSS expressions we use here are not as bad as [the ones generally used to mimic min-width](https://robertnyman.com/2007/11/13/stop-using-poor-performance-css-expressions-use-javascript-instead/) and the like. These are only evaluated once, which should result in a _small_ performance hit.</p>

## Displaying Images Via Pseudo-Elements

The main advantage of using a pseudo-element for the sole purpose of displaying an image is that it allows designers to crop a sprite. Actually, this is nothing new, and many websites are already using extra (aka "junk") markup to achieve this. For example, Yahoo! Search uses empty `<s>` and Facebook uses empty `<i>` tags for this purpose. Going this route allows for the creation of compact CSS sprites, without empty space between the images within the sprite.

The two examples below do not use extra markup and they both share the same sprite:

![sprite](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b539238-47cc-4737-82e3-15749b706d3a/sprite.png)

The two images below — which are the second icon in the sprite — are generated using each technique, respectively.</p>

### Nicolas Gallagher's method

<dl><br>
<dt id="first">Styling the pseudo-element with a background image:</dt><br>
<dd>

<pre><code class="language-css">#first:before {
    content: "";
    float: left;
    width: 15px;
    height: 15px;
    margin: 4px 5px 0 0;
    background: url(sprite.png) -15px 0;
}</code></pre>

</dd>

### The new url() / clip method

<dt id="second">Using the <code>content</code> property to insert the sprite which is then cropped with <code>clip</code>:</dt>
<dd>

<pre><code class="language-css">#second {
  position: relative;
  padding-left: 20px;
  background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '&lt;img alt=&quot;&quot; src=&quot;sprite.png&quot;&gt;'+this.innerHTML);
}

#second:before,
#second img {
  content: url(sprite.png);
  position: absolute;
  top: 3px;
  clip: rect(0 30px 15px 15px);
  left: -15px; /* to offset the clip value */
  _left: -35px; /* some massaging for IE 6 */
}</code></pre>

</dd>
</dl>

In case you wonder why I use `position: absolute` in the above rule, it is because the `clip` property only applies to _absolutely positioned_ elements.</p>

### The New Technique: How Does It Work?

*   Instead of styling the pseudo-element with a background, we use it to insert an image (via `content`).
*   Using the `clip` property, we crop this image to only display the part we want to show. It means that there is no need to add empty space in the image to avoid other parts to show as well (usually used as background image of larger elements).
*   We offset `clip` values by using the `left` and/or `top` properties.

With a non-cropping technique, images in sprites would have to start from the right hand side or left hand side to accommodate RTL/LTR contexts (`background-position: [left]|[right] [vertical value]`). Another limitation is creating sprites with images showing next to each other (because other images could be displayed as well). But when **cropping** sprites, these issues are not in play, so all images can be tucked together.

For an example, see figure below:

![Two sprites for different contexts versus one sprite for both LTR and RTL interfaces](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c14b42e-094d-4d0d-9026-49eb34316d68/figure-2.png)

### Advantages of this method over existing techniques

**Styled to print**  
Unlike background images, these images are printed with the document (they are sent to the printer).

**Styled to be accessible**  
Unlike background images, these images will not disappear in [MS Windows' high contrast mode](https://www.artzstudio.com/2010/04/img-sprites-high-contrast/) or with [high-contrast styles sheets](https://www.paciellogroup.com/blog/2010/01/high-contrast-proof-css-sprites/).

**Styled to work in IE <abbr title="Less Than">lt</abbr> 8**  
This method works in Internet Explorer 6 and 7 as well.

Note that [data URI scheme](https://en.wikipedia.org/wiki/Data_URI_scheme) could be used to avoid the HTTP request. IE6/7 do not support data URI scheme, but we can use [MHTML for IE6/7](https://www.phpied.com/mhtml-when-you-need-data-uris-in-ie7-and-under/ "MHTML – when you need data: URIs in IE7 and under") to make IE7 and older browsers understand it as well.</p>

## Styling links with pseudo-elements

Nicolas Gallager shows [plenty of cool stuff](https://nicolasgallagher.com/css-background-image-hacks/) one can do with pseudo-elements. The only thing I'd add here is the use of `::after` to style links à la "read more" and the like, for example:

[Read more](#)

**CSS:**

<pre><code class="language-css">.more:after {
        white-space:nowrap;
        content: " 0BB"; /* » */
}
.more {
        white-space:nowrap;
        background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = this.innerHTML+' &raquo;');
}</code></pre>

## A word about accessibility

You should assume that [generated content is read by screen-readers](https://lists.w3.org/Archives/Public/www-style/2010Nov/0437.html), and since there is no mechanism to offer alternative text for images plugged via the `content` property, we should make sure those images are purely decorative because screen-reader users would not have access to that information.</p>

## Further reading

You might want to take a look at the following related resources:

*   [CSS3 module: Lists - The ::marker pseudo-element](https://www.w3.org/TR/2002/WD-css3-lists-20021107/#markers)
*   [Generated content, automatic numbering, and lists](https://www.w3.org/TR/CSS2/generate.html)
*   [The clip property](https://www.w3.org/TR/CSS21/visufx.html#clipping)
*   [Colour Contrast and CSS Sprite Maps](https://juicystudio.com/article/colour-contrast-css-sprite-maps.php)
*   [High Contrast Proof CSS Sprites](https://www.paciellogroup.com/blog/2010/01/high-contrast-proof-css-sprites/)

_Credits: Icons by [FatCow Web Hosting](https://www.fatcow.com/free-icons/) [CC-BY-3.0-us], [via Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Farm-Fresh_bullet_feed.png)_

dt{ font-weight: bold; }
.glyphs {list-style-type:none;}
.glyphs li:before,
.glyphs b {display:inline-block;width:1.5em;font-size:1.5em;text-align:center;}
/* advantage of grouping these: the rule will show in Firebug :) */
.one,
.one:before {
	content: "2660"; /* ? */
	background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&spades;</b>'+this.innerHTML);
}
.two,
.two:before {
	content: "2663"; /* ? */
	background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&clubs;</b>'+this.innerHTML);
}
.three,
.three:before {
	content: "2665"; /* ? */
	background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&hearts;</b>'+this.innerHTML);
}
.four,
.four:before {
	content: "2666"; /* ? */
	background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<b>&diams;</b>'+this.innerHTML);
}
.red b,
.red:before {color:red;}
.one:hover:before,
.two:hover:before,
.three:hover:before,
.four:hover:before {color:teal;}
#first:before {
  content:"";
  float:left;
  width:15px;
  height:15px;
  margin:4px 5px 0 0;
  background:url(https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b539238-47cc-4737-82e3-15749b706d3a/sprite.png) -15px 0;
}
#second {
	position:relative;
	padding-left:20px;
	background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = '<img alt="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b539238-47cc-4737-82e3-15749b706d3a/sprite.png">'+this.innerHTML);
}
#second:before,
#second img {
  content:url(https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b539238-47cc-4737-82e3-15749b706d3a/sprite.png);
  position:absolute;
  clip:rect(0 30px 15px 15px);
	top:3px;
  left:-15px; /* to offset the clip value */
	_left:-35px; /* some massaging for IE 6 */
}
.more,
.more:after {
	white-space:nowrap;
	content: " 0BB"; /* » */
	background-image: expression(this.runtimeStyle.backgroundImage="none",this.innerHTML = this.innerHTML+' &raquo;');
}

