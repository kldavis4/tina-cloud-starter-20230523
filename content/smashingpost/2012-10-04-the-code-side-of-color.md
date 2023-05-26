---
title: Hex Color – The Code Side Of Color
slug: the-code-side-of-color
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c80bb84-ee55-4287-9588-5ec032aeb699/hex-additive-and-subtractive.png
date: 2012-10-04T11:59:33.000Z
author: ben-gremillion
description: >-
  The trouble with a color’s name is that it never really is perceived as the exact same color to two different individuals — especially if they have a stake in a website’s emotional impact. Name a color, and you’re most likely to give a misleading impression. Even something like “blue” is uncertain. To be more precise, it could be “sky blue”, “ocean blue”, “jeans blue” or even “arc welder blue”.
categories:
  - Coding
  - Colors
  - Color Theory
  - Essentials
---
The trouble with a color’s name is that it never really is perceived as the exact same color to two different individuals — especially if they have a stake in a website’s emotional impact. Name a color, and you’re most likely to give a misleading impression. Even something like “blue” is uncertain. To be more precise, it could be "sky blue", "ocean blue", "jeans blue" or even "arc welder blue".

![Hex Color](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbede5e0-6659-47bc-9e45-9daec8194aa5/hex-changing-tens-500.png "Hex Color – The Code Side Of Color")

Descriptions vary with personal taste and in context with other colors. We label them "indigo", "jade", "olive", "tangerine", "scarlet" or "cabaret". What exactly is "electric lime"? Names and precise shades vary — unless you’re a computer.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Color Theory for Designers: The Meaning of Color](https://www.smashingmagazine.com/2010/01/color-theory-for-designers-part-1-the-meaning-of-color/)
*   [A Simple Web Developer’s Guide To Color](https://www.smashingmagazine.com/2016/04/web-developer-guide-color/)
*   [Understanding Color Concepts And Terminology](https://www.smashingmagazine.com/2010/02/color-theory-for-designers-part-2-understanding-concepts-and-terminology/)
*   [Creating Your Own Color Palettes](https://www.smashingmagazine.com/2010/02/color-theory-for-designer-part-3-creating-your-own-color-palettes/)

{{% feature-panel %}}

## Code Demands Precision

When computers name a color, they use a so-called <em>hexadecimal code</em> that most humans gloss over: 24-bit colors. That is, 16,777,216 unique combinations of exactly six characters made from ten numerals and six letters — preceded by a hash mark. Like any computer language, there’s a logical system at play. Designers who understand how hex colors work can treat them as tools rather than mysteries.</p>

### Breaking Hexadecimals Into Manageable Bytes

Pixels on back-lit screens are dark until lit by combinations of red, green, and blue. Hex numbers represent these combinations with a concise code. That code is easily broken. To make sense of <code>#970515</code>, we need to look at its structure:

The first character <code>#</code> declares that this “is a hex number.” The other six are really three sets of pairs: <code>0–9</code> and <code>a–f</code>. Each pair controls one primary additive color.

<img loading="lazy" decoding="async" class="106588 size-full" title="Hex Reading" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b1da505-6def-42a1-8dbf-90e83e2b1ff8/hex-reading.png" alt="hex color reading" width="500" height="132" /><br>
<em>The higher the numbers are, the brighter each primary color is. In the example above, 97 overwhelms the red color, 05 the green color and 15 the blue color.</em>

Each pair can only hold two characters, but <code>#999999</code> is only medium gray. To reach colors brighter than <code>99</code> with only two characters, each of the hex numbers use letters to represent <code>10–16</code>. <code>A</code>, <code>B</code>, <code>C</code>, <code>D</code>, <code>E</code>, and <code>F</code> after <code>0–9</code> makes an even <code>16</code>, not unlike jacks, queens, kings and aces in cards.

<img loading="lazy" decoding="async" class="122394" title="Hex Chart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13833a53-cfc5-4775-8f97-ef0e569dcd71/hex-chart-2.png" alt="Diagram showing how hex colors pass above 0-9" width="500" height="470" />

Being mathematical, computer-friendly codes, <strong>hex numbers are strings full of patterns</strong>. For example, because <code>00</code> is a lack of primary and <code>ff</code> is the primary at full strength, <code>#000000</code> is black (no primaries) and <code>#ffffff</code> is white (all primaries). We can build on these to find additive and subtractive colors. Starting with black, change each pair to <code>ff</code>:

*   `#000000` is black, the starting point.
*   `#**ff**0000` stands for the brightest red.
*   `#00**ff**00` stands for the brightest green.
*   `#0000**ff**` stands for the brightest blue.

Subtractive colors start with white, i.e. with the help of <code>#ffffff</code>. To find subtractive primaries, change each pair to <code>00</code>:

*   `#ffffff` is white, the starting point.
*   `#**00**ffff` stands for the brightest cyan.
*   `#ff**00**ff` stands for the brightest magenta.
*   `#ffff**00**` stands for the brightest yellow.

<img loading="lazy" decoding="async" class="122393" title="Mixing Additive Colors to Make Subtractives" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b51d8f7-d035-4a89-b59b-ad0dab49de32/hex-additive-and-subtractive.png" alt="Mixing additive colors to make subtractives" width="500" height="447" />

### Shortcuts In Hex

Hex numbers that use only three characters, such as <code>#fae</code>, imply that each <a href="https://www.mathsisfun.com/hexadecimals.html">ones place</a> should match the sixteens place. Thus <code>#fae</code> expands to <code>#ffaaee</code> and <code>#09b</code> really means <code>#0099bb</code>. These shorthand codes provides brevity in code.

In most cases, one can read a hex number by ignoring every other character, because the difference between the sixteens place tells us more than the ones place. That is, it’s hard to see the difference between 41 and 42; easier to gauge is the difference between 41 and 51.

<img loading="lazy" decoding="async" class="122627" title="hex-first-digits" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3315e8f0-36e9-4fd4-9270-932c03670c6f/hex-first-digits-first-b.png" alt="Diagram emphasizing the first character in each pair of characters" width="500" height="142" />

The example above has enough difference among its sixteens place to make the color easy to guess — lots of red, some blue, no green. This would provide us with a warm violet color. Tens in the second example (9, 9 and 8) are very similar. To judge this color, we need to examine the ones (7, 0, and 5). The closer a hex color’s sixteens places are, the more neutral (i.e. less saturated) it will be.</p>

## Make Hexadecimals Work For You

Understanding hex colors lets designers do more than impress co-workers and clients by saying, “Ah, good shade of burgundy there.” Hex colors let designers tweak colors on the fly to improve legibility, identify elements by color in stylesheets, and develop color schemes in ways most image editors can’t.</p>

### Keep Shades In Character

To brighten or darken a color, one’s inclination is often to adjust its brightness. <strong>This makes a color run the gamut from murky to brilliant</strong>, but loses its character on either end of the scale. For example, below a middle green becomes decidedly black when reduced to 20% brightness. Raised to 100%, the once-neutral green gains vibrancy.

A funny thing happens when we treat hex colors as if they were increments of ten. By adding one to each of the left-hand character of each pair, we <em>raise</em> a color’s brightness while <em>lowering</em> its saturation. This prevents shades of a given color from wandering too closely to pitch black or brilliant neon. Altering hex pairs retains the essence of a color.

<img loading="lazy" decoding="async" class="106582" title="Changing Sixteens" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed4ae55f-9a93-448e-a0c2-2437143fad29/hex-changing-tens.png" alt="Diagram showing how hex affects brightness and saturation" width="500" height="464" />

In the example above, the top set of shades appears to gain yellow or fall to black, even though it’s technically the same green hue. By changing its hex pairs, the second set appears to keep more natural shades.</p>

### Faded Underlines

By default, browsers underline text to denote links. But thick underlines interfere with letters’ descenders. Designers can make underlines less obtrusive by scaling back hex colors. The idea is to make the tags closer to the background color, while the text itself gains contrast against the background.

*   For dark text on a bright background, we make the links brighter.
*   For bright text on a dark background, we make the links darker.

To make this work, every embedded link needs a &lt;<code>span</code>&gt; inside of every &lt;a&gt;:

<code>a { text-decoration:underline;color:#aaaaff; }</code>

<code>a span { text-decoration:none;color:#0000ff; }</code>

<img loading="lazy" decoding="async" class="106584" title="Descenders" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f75ea98-2afd-4d52-92ce-9cade99e2aaa/hex-descenders.png" alt="Example of underlines that pale compared to the clickable text" width="500" height="400" />

As you can see here, underlines in the same color as the text can interfere with parts of type that drop below the baseline. Changing the underline to resemble the background more closely makes descenders easier to read, even though most browsers place underlines above the letterforms.

Adding spans to every anchor tag can be problematic. A popular alternative is to remove underlines and add border-bottom:

<code>a { text-decoration: none; border-bottom: 1px solid #aaaaff; }</code>

### Better Body Copy

A recurring design problem is that a specific color may be technically correct but has an unintended effect. For example, some designs call for headers and body copy to be the same color. We have to keep in mind that the thicker the strokes of large text appears, the darker the small text appears.

<img loading="lazy" decoding="async" class="106594" title="The Text Is Too Bright" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad97013-7304-4963-92c2-6931e2e6c805/hex-text-too-light1.png" alt="Example of text that, while technically correct, appears too bright" width="500" height="134" />

<code>h1, p { color: #797979; }</code>

<img loading="lazy" decoding="async" class="106593" title="The Text Is Improved" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a6c64fb-29e5-42ad-80b3-c92df5a528b7/hex-text-improved1.png" alt="Example of text technically darker but visually the same" width="500" height="134" />

<code>h1 { color: #797979; }</code>

<code>p { color: #393939; }</code>

While technically identical, the body of the copy is narrower, and more delicate letterforms make it visually brighter than the heading. Lowering the sixteens places will make the text easier to read.</p>

### How To Warm Up Or Cool Down A Background

Neutral backgrounds may be easy to read against, but "neutral" doesn’t have to mean "bland". Adjusting the first and last byte can make a background subtly warmer or cooler.

<img loading="lazy" decoding="async" class="106585" title="Different Backgrounds-1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9e07385-f95f-4670-91e2-a5fd951c9d69/hex-different-backgrounds-1.png" alt="Examples with slight background color variations" width="500" height="106" />

*   `#404040` — neutral
*   `#504030` — warmer
*   `#304050` — cooler

Is that too much? For a more subtle shift, use the ones places instead:

<img loading="lazy" decoding="async" class="106586" title="More Subtle Background Shift" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f31e3630-be99-4359-9962-294bfe1b8847/hex-different-backgrounds-2.png" alt="Examples of very slight variations in background color" width="500" height="106" />

*   `#404040` — neutral
*   `#4f4040` — warmer
*   `#40404f` — cooler

### Coordinate Colors With Copy-Paste

Recognizing the structure of a hex number’s number/letter pairs gives designers a unique tool to explore color combinations. Unlike color wheels and charts, rearranging pairs in a hex number is a simple process to change hues while keeping values similar. As a bonus, the results can be unpredictable. The simplest technique is to move one pair of characters to a different spot, which trades primary colors.

A common design technique to make text or other visual elements coordinate with a photo is to use colors from within that photo. <strong>Understanding hex colors can take that a step further</strong>, by deriving new colors that coordinate with the photo without taking directly from the photo.

<img loading="lazy" decoding="async" class="106591" title="Swap Triplets" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e32940fd-c01e-4ddb-b3f4-67c6c0be41e5/swap-triplets.png" alt="Examples of how swapping primary colors can yield coordinated but interesting results" width="500" height="390" />

## Going Forward

Don’t let the code intimidate you. With a little creativity, hex colors are a tool at your disposal. If nothing else, next time someone asks if you can solve a problem with code in any language, you can simply say:
<blockquote>"Shouldn’t be harder than parsing hexadecimal triplets in my head."</blockquote>

## Hex Color Tools

You may be interested in the following tools and apps:

*   [Color Supply](https://colorsupplyyy.com/app/)
*   [Brand Colors](https://brandcolors.net/)
*   [Color Hexa](https://www.colorhexa.com/)
*   [Paletton](https://paletton.com)
*   [Coolors](https://coolors.co/)

{{< signature "il" >}}

