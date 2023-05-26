---
title: Unicode For A Multi-Device World
slug: unicode-for-a-multi-device-world
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cab51e6f-cd07-4a43-8456-9612d840ecad/08-range-invert-500.jpg
date: 2014-05-06T22:52:37.000Z
author: johnripley
description: >-
  A while ago, I was working on a website that required a number of icons. “No
  problem,” I thought. “I know how to handle this. I’ll use an `@font-face` icon
  set for high-resolution screens. It’ll be a single file, to reduce HTTP
  requests, and I’ll include just the icons that I need, to reduce file size.”
categories:
  - Coding
  - Mobile
  - Typography
  - Fonts
---
A while ago, I was working on a website that required a number of icons. “No problem,” I thought. “I know how to handle this. I’ll use an <code>@font-face</code> icon set for high-resolution screens. It’ll be a single file, to reduce HTTP requests, and I’ll include just the icons that I need, to reduce file size.”

“I’ll even use a Unicode character as the base of the icon, so that if <code>@font-face</code> isn’t supported, then the user will still see something like the intended icon.” I felt pretty pleased with myself.

That is, until I ran the page in the device lab.

On some devices, a number of the icons weren’t showing. Yet on the same devices, others were, so clearly it wasn’t an <code>@font-face</code> issue. It must have been the underlying Unicode.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [All About Unicode, UTF8 & Character Sets](https://www.smashingmagazine.com/2012/06/all-about-unicode-utf8-character-sets/)
*   [Open Device Labs: Why Should We Care?](https://www.smashingmagazine.com/2013/05/open-device-labs-why-should-we-care/)
*   [You, Me And The Emoji: Character Sets, Encoding And Emoji](https://www.smashingmagazine.com/2016/11/character-sets-encoding-emoji/)
*   [<span class="headline">Towards A Retina Web</span>](https://www.smashingmagazine.com/2012/08/towards-retina-web/)

## What To Do?

*   I could have used ligatures for the `@font-face` icon. These are great for accessibility but aren’t supported in Internet Explorer 9 or earlier.
*   I could have used the default “blank” Unicode characters (the [PUA ranges](https://en.wikipedia.org/wiki/Private_Use_Areas)), which apps such as IcoMoon default to. But, again, [Internet Explorer has issues](https://adactio.com/journal/6555/), and if the user has set a default font (if they are dyslexic, for example), then they wouldn’t see anything meaningful.
*   There are some [good arguments for using SVG](https://ianfeather.co.uk/ten-reasons-we-switched-from-an-icon-font-to-svg/), but I like the flexibility of `@font-face`: Changing the color on hover is very easy, for example, and `@font-face` icons will render with subpixel anti-aliasing, whereas SVG uses grayscale.

{{% feature-panel %}}

I was happy with the underlying Unicode characters because they gave a nice fallback for users on Windows Phone 7, Opera Mini and old BlackBerrys that don’t support <code>@font-face</code>. Instead, I wanted to determine which Unicode characters I could safely use.

So, I started doing some testing. And that led to some more testing, and then some more.

So far, I’ve looked at 107 Unicode characters on 78 devices and 5 screen readers. I’ll be honest — it’s not the most fun I’ve ever had. So, I’ll save you the trouble and share some of the problems and potential solutions that I’ve come across.</p>

## Why Bother?

But before we get to that, let’s just make sure that this is all worthwhile.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd749ba1-66f6-4b2e-883b-06f01fcb661f/01-proof.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/567a3b89-608e-4661-8e53-a403835a15db/01-proof-500.jpg" alt="Why you should bother about unicode." width="500" height="107" /></a><figcaption>Left to right: <code>@font-face</code> icon using a ligature in Chrome; <code>@font-face</code> icon using a ligature in Internet Explorer 9 (yep, nothing there); <code>@font-face</code> icon using a Unicode fallback in Opera Mini; <code>@font-face</code> icon using a PUA code point in Opera Mini (yep, nothing there). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd749ba1-66f6-4b2e-883b-06f01fcb661f/01-proof.jpg">Large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a98b84a8-7ca4-4e1d-8ff1-6f3cd1bac67a/02-subpixel-500.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a98b84a8-7ca4-4e1d-8ff1-6f3cd1bac67a/02-subpixel-500.jpg" alt="SVG and @fontface subpixel rendering." width="500" height="176" /></a><figcaption>Left: SVG with grayscale anti-aliasing. Right: <code>@font-face</code> icon with subpixel rendering. (Both in Firefox). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea6cd7e7-b75b-4118-adc9-747d6affa68d/02-subpixel.jpg">Large version</a>)</figcaption></figure>

(Oh, and if I hear murmurings of “Opera Mini? No one uses that,” then consider that there are <a href="https://alwaystwisted.com/post.php?s=2014-01-01-rems-fallbacks-and-support">70 million more Opera Mini users than iPads</a> in the world.)

To my mind, using the underlying Unicode character seems the most robust approach, offering a visual icon to the greatest number of devices and browsers.</p>

## How Do You Do It, Then?

If you’ve not used Unicode characters with <code>@font-face</code> icons, don’t worry. Tools like <a href="https://icomoon.io/">IcoMoon</a> make it simple. When you’ve selected the icons that you want to use and clicked to generate the font, you’ll see a page that shows all of your chosen icons, with their name and the Unicode code point that they will be mapped to. This will usually be something like <code>e600</code>, and this number is what you’ll need to replace with the hexadecimal value of your chosen Unicode character.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e326090-9412-4436-90a8-9c3a6db3a9ea/03-icomoon.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1e69ec5-fe14-4124-8eef-5c3050094243/03-icomoon-500.jpg" alt="Tools like IcoMoon make it simple to generate icon fonts." width="500" height="198" /></a><figcaption>Tools like IcoMoon make it simple to generate icon fonts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e326090-9412-4436-90a8-9c3a6db3a9ea/03-icomoon.jpg">Large version</a>)</figcaption></figure>

So, how do you know which Unicode character to use? You could go through one of the many resources that list all 110,000 characters, but you’ve probably got better things to do. <a href="https://shapecatcher.com/">Shapecatcher</a> makes life a bit easier: Draw the shape you’re after, and it will return a list of similar-looking characters.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e558c983-da2d-4bd3-a5ad-0cef0e0c4d2f/04-shapecatcher.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b5e15b-9d1d-41f4-b589-1bbfefcccf5d/04-shapecatcher-500.jpg" alt="Shapecatcher will return a selection of similar looking icons for you." width="500" height="198" /></a><figcaption>Shapecatcher will return a selection of similar looking icons for you. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e558c983-da2d-4bd3-a5ad-0cef0e0c4d2f/04-shapecatcher.jpg">Large version</a>)</figcaption></figure>

Pick the one you like best, copy the Unicode hexadecimal value, and paste it into IcoMoon. Once you’ve done this for all of your icons, download the <code>@font-face</code> package as normal.</p>

## So, Which Characters Should You Use?

Well, I’ll have to defer to Jeremy Keith’s answer for everything about the Web: “<a href="https://adactio.com/journal/4437/">It depends</a>.” In my testing, support for any given Unicode character varies hugely (and by “support,” I mean that either the <code>@font-face</code> icon appears or that the underlying Unicode character appears, rather than the user seeing an empty rectangle or a question mark or nothing at all). Even Unicode characters in the same “<a href="https://en.wikipedia.org/wiki/Unicode_block">block</a>” of related symbols often have quite different levels of support.

But I can provide a little help. Once you know which Unicode character you want to use, <a href="https://unicode.johnholtripley.co.uk/">run it through Unify</a>, which will give you a support score based on the devices that I’ve tested with so far.

If you’re happy with either the <code>@font-face</code> icon or the Unicode character being displayed, you should see very high levels of support. Some icons work on everything that I’ve tested so far.

The big exception is <a title="You, Me And The Emoji: Character Sets, Encoding And Emoji" href="https://www.smashingmagazine.com/2016/11/character-sets-encoding-emoji/">Emoji characters</a>, which I would stay away from. Around half of the devices that I’ve tested on don’t show the <code>@font-face</code> icon, and many don’t show anything meaningful at all. Additionally, iOS replaces them with fixed-size colored graphics, so trying to scale them with <code>font-size</code> won’t work.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f1bbcb3-31af-40fc-af65-ef831e401ca5/05-emoji.jpg"><img title="Variation in Emoji characters." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94db7416-ab02-4790-b341-85762f850f85/05-emoji-500.jpg" alt="Variation in Emoji characters." width="500" height="139" /></a><figcaption>Variation in Emoji characters. Left to right: Firefox (Windows 7), Chrome (Windows 7), Chrome (Android 4.2.1), Opera (Windows 7) and Safari (iOS). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f1bbcb3-31af-40fc-af65-ef831e401ca5/05-emoji.jpg">Large version</a>)</figcaption></figure>

Also, if a device can render a Unicode character, it will usually also be able to render an <code>@font-face</code> icon that uses that character. So, you’ll need to decide on the tradeoff: Using an icon font gives you more control over the design, but then you’d be adding to the page’s weight and delaying the rendering of the icon until the font has loaded.

If you’re just using a Unicode character directly, then be prepared for a variety of visual styles. Even on the same computer, browsers can render the same character in quite different ways.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81df484b-3f95-4344-a043-a0dfb270c66e/06-variation.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0896346f-8978-4e75-b398-3d7710b09355/06-variation-500.jpg" alt="Unicode character 260E shown in Firefox, Chrome, Internet Explorer and Opera on the same Windows 7 machine, and on iOS." width="500" height="107" /></a><figcaption>Unicode character <code>260E</code> shown in Firefox, Chrome, Internet Explorer and Opera on the same Windows 7 machine, and on iOS. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81df484b-3f95-4344-a043-a0dfb270c66e/06-variation.jpg">Large version</a>)</figcaption></figure>

In many projects, the consistency and control you get from using an <code>@font-face</code> icon is worthwhile. Putting only the icons that you need in the font file will minimize downloading time.

Saying anything more about <code>@font-face</code> icons is pointless because Zach Leatherman has written such an <a href="https://filamentgroup.com/lab/bulletproof_icon_fonts/">excellent and well-researched article</a>.

## Accessibility

Zach looks in depth at the accessibility implications of using icons in this way, and I’d like to add a few thoughts.

There are two main problems here: The screen reader will either completely ignore the icon (which would leave the user not knowing that there is something there to interact with) or announce something seemingly irrelevant. For example, if you used Unicode character <code>2261</code> for your “burger” icon, it would either be ignored or be announced as “Equal” or “Identical to”, depending on the screen reader. Neither of these would help the user understand what this element does.

The best approach depends on what the icon is for. If it merely adds visual flourish to a text label or heading, then I’d recommend hiding the icon from screen readers. In this case, rather than adding icon fonts directly to the element in the standard way (i.e. by using the <code>:before</code> or <code>:after</code> CSS pseudo-element), add it to a span inside the element. This way, you can add <code>aria-hidden="true"</code> to the span, which will prevent it from being announced in a <a href="https://www.456bereastreet.com/archive/201205/hiding_visible_content_from_screen_readers_with_aria-hidden/">reasonable number of screen readers</a>.</p>

<pre><code class="language-markup">
&lt;span aria-hidden="true"&gt;≡&lt;/span&gt; Menu
</code></pre>

However, if the icon will be used on its own, without anything else to provide meaning or context, then I’d recommend hiding the icon as before but adding a text label that is hidden visually. This will provide a cue that there is something to interact with.</p>

<pre><code class="language-markup">
&lt;style&gt;
    .visiblyHidden {
    /* https://css-tricks.com/places-its-tempting-to-use-display-none-but-dont/ */
        position: absolute;
        overflow: hidden;
        clip: rect(0 0 0 0);
        height: 1px; width: 1px;
        margin: -1px; padding: 0; border: 0;
    }
&lt;/style&gt;

&lt;span aria-hidden="true"&gt; ≡ &lt;/span&gt;&lt;span class="visiblyHidden"&gt;menu&lt;/span&gt;
</code></pre>

## Does `font-family` Help?

I’ve heard the recommendation that you should include fonts like Arial Unicode MS in a font-family stack that is being used to display Unicode symbols, but that doesn’t guarantee that the symbol will appear for everyone. If a browser can’t find a font with the required Unicode character from those you’ve listed in the <code>font-family</code> declaration, then it will try to find any font in the OS that will display it.

Consistency is hard to come by, though, because it will depend on the fonts available on that particular device and on the browser being used. Browser manufacturers are free to look for any matching fonts however they think best — and for the sake of performance, the browser might stop searching if it’s taking too long.

By all means, include Arial Unicode MS or Segoe UI Symbol in a <code>font-family</code> declaration if you like how they render the symbols you’re using, but you’ll be relying on that font being installed on the device. If you want to control how the symbol looks, you’re best off with an <code>@font-face</code> icon.</p>

## Detecting Unicode Support

So, can JavaScript come to the rescue? Well, Modernizr does have a couple of tricks up its sleeve. <a href="https://github.com/Modernizr/Modernizr/blob/master/feature-detects/unicode.js">One approach</a> compares the width of a commonly supported character against one that’s likely to produce a fallback character and, if different, determines that the first character has rendered as expected.

Another focuses on trying to <a href="https://github.com/Modernizr/Modernizr/blob/master/feature-detects/emoji.js">determine Emoji support</a> by drawing the character onto a <code>canvas</code> element and then checking a single pixel to see whether it’s been filled in by the character. The problem, as we’ve seen, is that Unicode support isn’t a boolean; just because a browser displays one character doesn’t mean that it will display another. So, I wouldn’t rely on these methods generally, but they might be useful in some circumstances.</p>

## Encoding Your Unicode

Mentioning encoding here would probably be worthwhile if you are working with Unicode. Encoding tells a browser how to interpret any Unicode characters on a page. If the encoding used by your text editor differs from the settings of your end user and there are no instructions to help the browser make sense of it, then the user will see a lot of seemingly random characters or question marks.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c0c163-3509-41f7-8078-5686231d1ed7/07-encoding.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3af898-fcf6-44ad-b927-9d8d8eb17cb9/07-encoding-500.jpg" alt="An example of the variation in glyphs from a single Unicode code point with different page encodings." width="500" height="107" /></a><figcaption>An example of the variation in glyphs from a single Unicode code point with different page encodings. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c0c163-3509-41f7-8078-5686231d1ed7/07-encoding.jpg">Large version</a>)</figcaption></figure>

Fortunately, pretty much everything on the Web these days uses UTF-8, so this isn’t the headache it used to be. However, it doesn’t hurt to make sure, and this is why you’ll hear of the recommendation to include <code>&lt;meta charset="utf-8"&gt;</code> in the <code>&lt;head&gt;</code> of your documents. If you’ve specified the encoding in the HTML file, then you don’t need to specify it again in any linked CSS files — it will be assumed to be the same.

If you’ve done this and you’re still seeing strange characters, then check that your HTTP headers are set to UTF-8 as well. Any encoding set there will override the <code>meta charset</code> declaration.

However, if you do have to work with a different encoding type, then avoid “embedded” characters (i.e. just pasting the single character shape directly into the text editor). If you use the <a href="https://www.w3.org/International/questions/qa-escapes">full numerical reference</a>, then the character will be <a href="https://en.wikipedia.org/wiki/Universal_Character_Set">unaffected by the document’s encoding type</a>.

In other words, if you want to use <code>2665</code> for a heart icon, then use <code>&amp;#x2665</code>, not ♥. Embedding symbols in this way is the safest approach, but adding accents and so on in body copy is <a href="https://www.w3.org/International/questions/qa-escapes">not recommended</a> because it will make the code harder to read and maintain. In this instance, getting the encoding right is better.</p>

## Hand-Picking Fonts

One feature of <code>@font-face</code> that’s often overlooked is <a href="https://www.w3.org/TR/css3-fonts/#descdef-unicode-range"><code>unicode-range</code></a>. This allows you to specify that a particular font is being used for just a few Unicode characters.

But why would you want to?

Perhaps you have found the perfect font for your body copy, but you would prefer one or two punctuation marks from a similar font, or perhaps you want to use <a href="https://en.wikipedia.org/wiki/Text_figures">old-style figures</a> but your body font doesn’t include them. Using <code>unicode-range</code> lets you use that alternate font for just those characters that you want to swap out.

You may <a href="https://www.w3.org/TR/css3-fonts/#descdef-unicode-range">specify</a> a single character, a comma-separated list or an entire range of characters to be rendered in the alternate font.

It has a slightly different syntax from other methods of working with Unicode. You’ll need to add <code>U+</code> before the character’s hexadecimal number. So, if you wanted a different font for all of your numbers (which are represented in Unicode between 0030 and 0039), you’d use something like this:

<pre><code class="language-css">
@font-face {
   font-family: 'oldStyleFigures';
   src: url(fonts/old-style-figures.ttf) format("opentype");
   unicode-range: U+30-39;
}
</code></pre>

Then you would add this:

<pre><code class="language-css">
p {
   font-family: oldStyleFigures, Arial, sans-serif;
}
</code></pre>

This means that all paragraph text will use Arial, except for numbers, which will use the oldStyleFigures font.

The downside? Of course, there’s a downside. It <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=475891">still</a> doesn’t work in Firefox — the alternate font will be applied to all characters, not just the ones you’ve specified in the range.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35166a43-22e7-4975-8103-e4c5291f2918/08-range-invert.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cab51e6f-cd07-4a43-8456-9612d840ecad/08-range-invert-500.jpg" alt="It still doesn’t work in Firefox" width="500" height="220" /></a><figcaption>Top to bottom: no <code>unicode-range</code> used; <code>unicode-range</code> added for numerals; <code>unicode-range</code> for numbers viewed in Firefox. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35166a43-22e7-4975-8103-e4c5291f2918/08-range-invert.jpg">Large version</a>)</figcaption></figure>

However, Drew McLellan has a <a href="https://24ways.org/2011/creating-custom-font-stacks-with-unicode-range/">workaround for the lack of support in Firefox</a>.</p>

## Unicode Syntax Cheat Sheet

How you add a Unicode character will determine the method that you need to refer to it. Here’s a quick summary:
<table class="table-overview"><br>
<tbody>
<tr>
<th>Where</th>
<th>Syntax</th>
<th>Example</th>
</tr>
<tr>
<td>HTML (hexadecimal number)</td>
<td><code>&amp;#x????;</code></td>
<td>

<pre><code>&lt;span&gt;&#x2665;&lt;/span&gt;</code></pre>

</td>
</tr>
<tr>
<td>HTML (decimal number)</td>
<td><code>&amp;#????;</code></td>
<td>

<pre><code>&lt;span&gt;&#9829;&lt;/span&gt;</code></pre>

(Note: no <code>x</code> as in the hexadecimal number)</td>
</tr>
<tr>
<td>CSS content (number must be in hexadecimal)</td>
<td><code>\????</code></td>
<td>

<pre><code>.heart:before { content: '\2665'; }</code></pre>

</td>
</tr>
<tr>
<td><code>unicode-range</code> (number must be in hexadecimal)</td>
<td><code>U+????</code></td>
<td>

<pre><code>@font-face {
font-family: heartFont;
src: url(fonts/heart-font.ttf) format("opentype");
unicode-range: U+2665;
}</code></pre>

</td>
</tr>
</tbody>
</table>

## It Doesn’t End There

That’s it for now, but plenty of useful articles and tools are out there. Here are a few that might help you out:

*   “[Articles, Best Practices and Tutorials](https://www.w3.org/International/articlelist),” W3C Internationalization Activity A large collection of articles covering encoding and internationalization topics
*   “[Bulletproof Accessible Icon Fonts](https://filamentgroup.com/lab/bulletproof_icon_fonts/),” Zach Leatherman, Filament Group In case you haven’t read Zach’s article about icon fonts
*   “[Creating Custom Font Stacks With Unicode-Range](https://24ways.org/2011/creating-custom-font-stacks-with-unicode-range/),” Drew McLellan, 24Ways More detail on using `unicode-range`
*   [Icomoon](https://icomoon.io/) A great tool to build a custom icon font
*   [Shapecatcher](https://shapecatcher.com/) Really useful for visually finding a particular Unicode character
*   [Unify](https://unicode.johnholtripley.co.uk/) My resource gives you an idea of how supported a particular Unicode character is across browsers and devices.

{{< signature "ds, il, al, ml" >}}

