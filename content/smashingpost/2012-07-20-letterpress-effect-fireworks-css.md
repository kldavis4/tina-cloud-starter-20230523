---
title: 'Simulating The Letterpress: From Live Filters In Fireworks To CSS Code'
slug: letterpress-effect-fireworks-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/884b1f37-4068-470d-b350-bd6f51273383/abstract-blueish-illu.jpg
date: 2012-07-20T09:03:40.000Z
author: jose-olarte
description: >-
  One of the visual effects that is a mainstay in my Web design toolkit is the letterpress effect. Used properly, it’s a quick way to make text blend better with the layout, as if it were machine-stamped onto the background. Think of what a home appliance marquee or a professional business card looks (and feels) like, and you’ll know what I’m talking about.
categories:
  - Fireworks
  - Tutorials
---
One of the visual effects that is a mainstay in my Web design toolkit is the letterpress effect. Used properly, it’s a quick way to make text blend better with the layout, as if it were machine-stamped onto the background. Think of what a home appliance marquee or a professional business card looks (and feels) like, and you’ll know what I’m talking about.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

I’ve developed a <strong>simple workflow</strong> for creating a letterpress text effect in Adobe Fireworks that, with the advent of CSS3, can be applied directly to HTML text — no images needed. Here’s the best part: it doesn’t use any Bevel or Emboss Live Filters.

<img loading="lazy" decoding="async" class="111015" title="Letterpress effect, final HTML+CSS output." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a626936d-cefb-469c-ae25-c9c63c877eaa/screen-01.png" alt="" width="500" height="300" />

{{% feature-panel %}}

## What Is Letterpress?

Letterpress is a venerable technique of <a href="https://vimeo.com/17156405">printing</a> that involves “pressing” a plate of <a href="https://en.wikipedia.org/wiki/Movable_type">movable type</a> onto a sheet of paper to produce an effect that is <a href="https://en.wiktionary.org/wiki/impress">impressed</a> (where the text is pressed down onto the paper) or <a href="https://en.wikipedia.org/wiki/Embossing_(paper)">embossed</a> (where the text is raised above the surface of the paper).

<a href="https://www.flickr.com/photos/needoptic/5356504970/"><img loading="lazy" decoding="async" class="111017" title="Letterpress business card." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e851dce-af2c-404e-93a1-3204dc0e4c0c/5356504970-a4344fe77d-78x78.jpg" alt="" width="500" height="500" /></a><br>
<em>An example of a letterpress business card with impressed text. (Image: <a href="https://www.flickr.com/photos/needoptic/5356504970/">Audimas Adomavicious</a>)</em>

The classic charm of letterpress found its place in digital design once designers were able to emulate its effect on screen. To accomplish that, designers observed the effect of light and shadow on the dents on paper that had gone through the printing process. Imagine a light shining down at an angle on a sheet of letterpress text. Impressed text will appear to have a sliver of highlighting at the bottom edge of the letters and a thin shadow at the top edge. Embossed text is just the opposite: highlights on top, shadows on the bottom. These properties create the effect of raised or sunken areas along the surface, and this can be translated using effects made possible by both Fireworks and the CSS3 specification.</p>

### Why Not Just Use Bevel or Emboss?

Fireworks’ Bevel and Emboss Live Filters are a bit primitive for my tastes. The refinement controls are unwieldy — for example, you can’t set highlights and shadows independently — and the result is subpar. It works OK for straight edges and sharp corners, but it gets rough around curves. I suspect this is because the effect is raster-based, so that it can work with any object (shape, text or embedded image); a vector-based tool would have allowed for a smoother and more precise effect.

<img loading="lazy" decoding="async" class="111081" title="Outer Bevel Live Filter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08939933-fc53-4f11-8ffc-eac1ffb8a56a/screen-01a.png" alt="" width="500" height="466" /><br>
<em>The letterpress effect using the Outer Bevel Live Filter. Notice the roughness of the curved edges.</em>

## Letterpress Text In Fireworks

A better way to recreate the effect would be to use the Drop Shadow Live Filter, because it produces smoother edges. This solution hinges on a basic setting: a shadow <em>and</em> a highlight, offset exactly 1 pixel up or down, relative to the text object. For this tutorial, we’ll start with two text objects of different colors, set against a colored background.

<img loading="lazy" decoding="async" class="111018" title="Two text objects." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ffd407-b15e-4134-bc04-b2351b136d5e/screen-02.png" alt="" width="500" height="300" /><br>
<em>Start with two text objects.</em>

### Embossed Text

To create an embossed effect, apply two Drop Shadow Live Filters to our first text object:

*   Apply a “Shadow” (distance: 1; color: #000000; opacity: 60%; blur: 0; angle: 270;) to the bottom of the text, _and_
*   Apply a “Highlight” (distance: 1; color: #FFFFFF; opacity: 90%; blur: 0; angle: 90;) to the top of the text.

<img loading="lazy" decoding="async" class="111019" title="Live Filters for embossed effect." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3de98aa7-b3c8-45ab-a425-619d64b60212/screen-03.png" alt="" width="500" height="372" /><br>
<em>Embossed effect applied to the “Smashing” text object.</em>

The opacity of the Drop Shadow filters will depend on how light or dark the background is in relation to the text’s color. Tweak these values according to how pronounced you want the letterpress effect to be.

<img loading="lazy" decoding="async" class="111089" title="Drop Shadow opacity settings" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1eb88e-2c4a-40b1-a60e-6c6f6d6bb5cc/screen-03b.png" alt="" width="500" height="215" /><br>
<em>Adjust the opacity value in the Drop Shadow Live Filter.</em>

### Impressed Text

To create an impressed effect for the second text object, just <strong>switch the angle values</strong> of the “Shadow” and “Highlight” Drop Shadow filters shown in the previous step, so that the shadow is on top of the text and the highlight is on the bottom. Adjust the opacity values to maintain contrast against the darker text object’s color.

<img loading="lazy" decoding="async" class="111020" title="Live Filters for impressed effect." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ed40108-3a5a-4d91-8a21-9f15ad52a622/screen-04.png" alt="" width="500" height="374" /><br>
<em>Impressed effect applied to the “Magazine” text object.</em>

<strong>Note</strong>: These effects work best with text and background color combinations that aren’t black and white, as in our example. If you’re working with black text or black backgrounds, you’ll want to skip the “Shadow” effect, because it will do little for the text. Similarly, for white text or white backgrounds, forego the “Highlight” effect.</p>

### Save as Style for Reuse

Now that our letterpress effects are in place, we can save them as Fireworks Styles so that we can use them again later without having to apply each filter manually.

To create a Fireworks Style:

1.  Select the “Smashing” text object with the Pointer tool (V);
2.  Bring up the Styles panel (Control/Command + F11, or in the menu Window → Styles);
3.  Click on the context-menu icon in the top-right corner of the panel, and click on “New Style”;
4.  In the “New Style” dialog box, let’s give our style a descriptive name, like “Letterpress Emboss.” Uncheck all properties except for “Effect,” and click OK.
5.  Repeat steps 1 to 4 for the “Magazine” text object.

<img loading="lazy" decoding="async" class="111046" title="Creating a new style." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a5f6ba2-9b4e-448c-89c1-d721f5bca116/screen-05.png" alt="" width="500" height="446" /><br>
<em>Styles panel and context menu</em>

<img loading="lazy" decoding="async" class="111047" title="Options for creating a new style." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/919290b7-6da5-4380-bd51-2e764d014d55/screen-06.png" alt="" width="500" height="256" /><br>
<em>“New Style” dialog box</em>

You should now see two new items in your Styles panel. The next time you want to apply the emboss or impress effect to a text object, just select that object, and click on the new style that you created.

<img loading="lazy" decoding="async" class="111048" title="Two new styles." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb383f6-585f-4fa3-9a8b-bb3ff3e102c4/screen-07.png" alt="" width="500" height="355" /><br>
<em>Styles panel with two new styles</em>

Additionally, you can save these new styles as a Style Library file (<em>*.stl</em>), to share with other designers or to back up your styles before reinstalling Fireworks.

To save a set of styles as a Style Library file:

1.  Bring up the Styles panel (Control/Command + F11, or Window → Styles);
2.  Click on the context-menu icon in the top-right corner of the panel, and click “Save Style Library”;
3.  In the “Save As” dialog box, enter a descriptive file name for the STL file, and then click “Save.”

<img loading="lazy" decoding="async" class="111049" title="Saving a Style Library." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4215fd70-40f4-4994-8370-34cfc371189f/screen-08.png" alt="" width="500" height="374" /><br>
<em>The Styles panel, again.</em>

<img loading="lazy" decoding="async" class="111050" title="Save As..." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09bb2cdd-65e3-4960-9f76-358a4f8a9df2/screen-09.png" alt="" width="500" height="439" /><br>
<em>“Save As” dialog box</em>

To import a previously saved Style Library:

1.  Bring up the Styles panel (Control/Command + F11, or Window → Styles);
2.  Click on the context-menu icon in the top-right corner of the panel, and click “Import Style Library”;
3.  In the “Open” dialog box, browse to and select the STL file, and then click “Open.”

<blockquote><strong>Hint:</strong> Need a good library of Letterpress Styles for Adobe Fireworks? Why not check this 16 Letterpress Styles set by <a href="https://twitter.com/mkkov">Mikko Vartio</a>?</blockquote>

## Translating Into CSS

### Option 1: Translate the Values of the Live Filters Manually

Aside from the downsides of the Bevel and Emboss filters that I mentioned earlier, the other reason I use Drop Shadow filters is that they readily translate into CSS3’s <code>text-shadow</code> property. Consider this basic syntax:

<pre><code class="language-css">text-shadow: [x-offset] [y-offset] [blur] [color-alpha];</code></pre>

Let’s break this down:

*   `[x-offset]` is set to `0`, and `[y-offset]` is either `1px` or `-1px`, depending on whether the shadow or highlight is at the top (`90°`) or bottom (`270°`);
*   `[blur]` is set to `0`, to keep the shadow and highlight effects crisp;
*   `[color-alpha]` is set using an RGBa value: `rgba(r, g, b, a)`.
    *   The first three values (`r`, `g` and `b`) correspond to the decimal red-green-blue values of the color itself (for example, `#FFFFFF` in hexadecimal is equal to `255, 255, 255` in decimal);
    *   The last value (`a`) determines the transparency of the color (where `0` is completely transparent, `0.5` is half-transparent, and `1` is completely opaque).

Let’s apply our effects to the following HTML markup:

<pre><code class="language-markup tmp-html">&lt;div class="embossed"&gt;Smashing&lt;/div&gt;
&lt;div class="impressed"&gt;Magazine&lt;/div&gt;</code></pre>

Our CSS for the embossed effect would be:

<pre><code class="language-css">div.embossed {
   text-shadow:
      0 1px 0 rgba(0, 0, 0, 0.8), /* shadow */
      0 -1px 0 rgba(255, 255, 255, 1.0); /* highlight */ }</code></pre>

And for the impressed effect:

<pre><code class="language-css">div.impressed {
   text-shadow:
      0 -1px 0 rgba(0, 0, 0, 0.8), /* shadow */
      0 1px 0 rgba(255, 255, 255, 0.5); /* highlight */ }</code></pre>

Here, I have slightly adjusted the opacity values in the <code>text-shadow</code> property (relative to the original values in the Drop Shadow Live Filter in Fireworks) to better suit the way fonts are rendered in the browser.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c5e8c43-7099-4ae6-868d-d2139ca49821/letterpress-effect.html"><img title="HTML+CSS output as viewed on a browser (Firefox)." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/656daf5b-c9c2-41ea-b865-7275b6349023/screen-10.png" alt="" width="500" height="312" /></a><br>
<em>Screenshot of the HTML and CSS output in Mozilla Firefox. See an <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c5e8c43-7099-4ae6-868d-d2139ca49821/letterpress-effect.html">HTML sample</a>.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c5e8c43-7099-4ae6-868d-d2139ca49821/letterpress-effect.html"><img title="HTML+CSS output as viewed on a browser (Safari)." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aab870e5-02d3-45c4-9f33-9b7bc2ee55b9/screen-10-safari.png" alt="" width="500" height="327" /></a><br>
<em>Screenshot of the HTML and CSS output in Apple Safari. See an <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c5e8c43-7099-4ae6-868d-d2139ca49821/letterpress-effect.html">HTML sample</a>.</em>

### Option 2: Use the CSS Properties Panel in Fireworks CS6

Writing CSS code by hand is what we Web professionals usually do. But in some cases, tools can help us, too.

Fireworks CS6 (which was recently released) has a new feature that could help you when you want to quickly (yet reliably) translate the properties of a visual element in the design to CSS3 code. The <a href="https://www.adobe.com/devnet/fireworks/articles/css3-extracting.html">CSS Properties panel</a> can extract CSS3 code for virtually any object selected on the canvas, including text objects and live filters.

Let’s see how this could help us in practice when working with the letterpress effect!

If you have a copy of Fireworks CS6 (a trial version would do, too), open the <code>letterpress-effect.fw.png</code> file provided with this tutorial (see the <a href="#downloads">Downloads</a> section further below), and then with the Selection tool, select the first text object.

<img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14866bee-1fec-47d7-a3ff-09091ae9c2d6/csspanel-text-selected.png" alt="" width="500" height="300" /><br>
<em>Open the letterpress-effect.fw.png file, and select the first text object.</em>

Next, open the CSS Properties panel (in the menu, Window → CSS Properties, or <code>Control/Command + F7</code>), and while the first text object is selected, notice how the CSS panel instantly shows the object’s properties.

<img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e822f57f-a42e-450e-b846-4bd2a63b795b/csspanel-embossed-effect.png" alt="" width="500" height="550" /><br>
<em>The CSS Properties panel shows the properties of the selected text object as CSS code. Highlighted here is the code that translates the two Live Filters into CSS.</em>

In this case, we’re interested only in the Live Filters applied to the text object, so let’s copy this bit of code from the CSS panel and see how it looks:

<pre><code class="language-css">text-shadow: 0 1px 0 rgba(0,0,0,0.6), 0 -1px 0 rgba(255,255,255,0.9);</code></pre>

As you see, we’ve got results similar to what we achieved earlier with the manual method. Fireworks CS6 has automatically translated the Live Filters that were applied to the “embossed” text object into clean and valid CSS!

Similarly, you can extract and copy the CSS for the Live Filters applied to the “impressed” text effect.

And if you strive for perfection (as many of us do), along with the CSS Properties panel, you can use <a href="https://www.mattstow.com/css-professionalzr.html">CSS Professionalzr</a>, an excellent free extension by <a href="https://twitter.com/stowball">Matt Stow</a> that can further optimize the code produced by the CSS Properties panel.

Of course, even if you’ve already switched to Fireworks CS6, you can always opt to translate the properties of Live Filters to CSS code manually. But when you’re dealing with a lot of objects, the CSS Properties panel comes in really handy and can save you precious time.</p>

### Tips on Using the Letterpress Effect

*   **Use the effects sparingly.**.  Text effects are the last thing you want to abuse, because they could impair readability, especially for people with vision problems. Restrict them to headings and interactive items (such as buttons and menu links).
*   **Enable them to degrade gracefully.**.  While most modern browsers already support CSS3 to some extent (see the note below), Internet Explorer 9 still doesn’t recognize the `text-shadow` property. In an effort to make things look consistent, you might want to [look for a workaround](https://www.google.com/search?q=ie9+text-shadow+workaround), but I highly recommend that you [gracefully degrade](https://www.digital-web.com/articles/fluid_thinking/) the effect in browsers that don’t support the property. Effects should be enhancements, not vital features.

<strong>Please note:</strong> Browsers that fully support the <code>text-shadow</code> property (with multiple shadows) include Firefox 3.5+, Chrome 4+, Safari 4+ and Opera 9.5. As of version 9, Internet Explorer still does not support the official <code>text-shadow</code> definition; instead, it has a <a href="https://msdn.microsoft.com/en-us/library/ms532985(v=vs.85).aspx">proprietary filter</a> that achieves a similar effect.</p>

## Examples

Here are a few real-world examples of the letterpress effect in action.

<a href="https://veerle.duoh.com/">Veerle’s Blog</a>
The letterpress effect — applied to the (image-rendered) logotype and headings — creates a bit of contrast against the background here, while still keeping everything subtle. Notice the use of both embossed and impressed effects in the column headings.

<a href="https://veerle.duoh.com/"><img loading="lazy" decoding="async" class="111022" title="Screenshot of Veerle's Blog" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eb16293-2ccf-4206-8f47-21a203ebb33f/screen-11.jpg" alt="" width="500" height="500" /></a>

Stunning CSS3 (teaser page)
Coupled with <code><a href="https://developer.mozilla.org/en/css/@font-face">@font-face</a></code> declarations for custom HTML fonts, the letterpress effect on the different heading levels makes for a sophisticated look, previously feasible only with image-based text. (Note that the teaser page we’ve linked to here is an archived version.)

<img loading="lazy" decoding="async" class="111023" title="Screenshot of Stunning CSS3 signup page." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d9b28fb-8bd2-4b0b-8117-0e2b5d1b3f46/screen-12.jpg" alt="" width="500" height="500" />

<a href="https://www.jankoatwarpspeed.com/work/">Janko at Warp Speed</a>
The use of only one <code>text-shadow</code> effect, and only on the headings, exemplifies Janko’s restraint in order to maintain contrast and readability. Also notice the 45° offset in the highlight effect, which you can achieve in CSS by adding a 1-pixel <code>x-offset</code> to the <code>text-shadow</code>.

<a href="https://www.jankoatwarpspeed.com/work/"><img title="Screenshot of Janko at Warp Speed's portfolio page." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c6af9ad-fbb0-4a4a-a2da-69f67730900c/screen-13.jpg" alt="" width="500" height="500" /></a>

### Downloads

*   Need a sample to study? [Download the archive](https://smashingmagazine.com/provide/letterpress-effect.zip) for this tutorial (ZIP, 84.5 KB), which includes the Fireworks PNG (created in Adobe Fireworks CS5) and the [HTML sample](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c5e8c43-7099-4ae6-868d-d2139ca49821/letterpress-effect.html).
*   The Fireworks PNG uses the awesome (and free) [Ultra font](https://www.fontsquirrel.com/fonts/ultra).
*   You can also [download the Style Library](https://smashingmagazine.com/provide/letterpress-effect.stl.zip) separately (ZIP, 22.3 KB), created in Adobe Fireworks CS5.

The samples (i.e. the Fireworks PNG and Style Library) should work fine in any recent version of Fireworks (CS4, CS5, CS5.1, CS6).</p>

### Further Reading

*   [Blueprints For The Web: Specctr Adobe Fireworks Plugin](https://www.smashingmagazine.com/2012/05/25/blueprints-for-the-web-specctr-adobe-fireworks-plugin/)
*   [Refining Your Design In Adobe Fireworks](https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/)
*   [Useful Typography Tips For Adobe Illustrator](https://www.smashingmagazine.com/2011/02/15/useful-typography-tips-for-adobe-illustrator/)

<em>(al) (mb)</em>

