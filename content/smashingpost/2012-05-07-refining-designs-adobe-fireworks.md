---
title: Refining Your Design In Adobe Fireworks
slug: refining-designs-adobe-fireworks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6695ace4-6850-4702-b754-c3a080a763ce/edit-points-illu.jpg
date: 2012-05-07T12:50:03.000Z
author: benjamin-de-cock
description: >-
  While certainly not as well known as Photoshop, Adobe Fireworks is a great
  tool for creating user interfaces, website designs and mock-ups, wireframes,
  icons and much more.
categories:
  - Fireworks
  - Workflow
  - Techniques
---
While certainly not as well known as Photoshop, Adobe Fireworks is a great tool for creating user interfaces, website designs and mock-ups, wireframes, icons and much more. However, most designers who have been using Photoshop for years may find Fireworks a bit awkward at first. Fireworks does have a slightly different workflow and requires a slightly different approach than you may be used to.

In this article, I’ll share some tips that I use in my work in Adobe Fireworks that could help improve the quality of your designs and workflow. Some of these tips are just quick explanations of features that you might not be aware of, while some are techniques and methods to improve the default visual results. Let’s begin!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

## Improve Fine Strokes

Fireworks’ stroke feature gives the user quite a lot of options. But one of the most important is missing: the ability to add a gradient to a stroke. Also, the effect from the Stroke tool isn’t always elegant — for example, when using an inset border with rounded corners.

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54c011d2-932f-4182-9348-9de531179672/native-stroke-render.png" alt="Default stroke render in Adobe Fireworks" /><br>
<em>Native stroke rendering in Fireworks. The rounded corners look a bit too thick.</em>

Fireworks lets you specify the stroke’s position: outside, centered or inside. But the best results are when the stroke is outside.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/326f3855-eea1-4754-8c06-2b5f256fab60/stroke-options.png" alt="Three possible stroke alignment options in Fireworks" /><br>
<em>Stroke can be set to different alignments in the Properties panel. Outside (example 3) looks better for fine strokes than centered or inside.</em>

But in such cases, I recommend a composite path instead of a stroke to get better control of the result and to be able to apply a gradient to it.

Start by drawing two rectangles with rounded corners, one of them 2 pixels taller and wider than the other. Put the smaller rectangle above the larger (you can verify that it’s above in the Layers panel), and make its border radius smaller by several pixels, as shown here:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2c50661-d850-470c-aec1-93703256fe2d/customer-border-2-shapes.png" alt="Two vector shapes for making a custom stroke" /><br>
<em>We’ll need two vector shapes to create our custom stroke.</em>

The purpose of the smaller shape (the one with the yellow-orange background) is to cut out (or “punch”) the interior of the red shape, resulting in a 1-pixel-wide object that can be used in place of a stroke. To achieve this, select the two rectangles and hit the “Punch Paths” tool icon in the Path panel:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/031007fc-0133-4438-b8f0-71ca0162ca36/punch-paths.png" alt="Punch paths command in the Path panel in Fireworks" /><br>
<em>Punch Paths will help us get a better-looking stroke.</em>

Alternatively, you could select the two rectangles and go to <code>Modify → Combine Paths → Punch</code>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66bdf2b9-aea5-4c82-99cc-aaff732cefc5/custom-stroke-result.png" alt="Composite path (custom stroke)" /><br>
<em>The stroke is now a composite path that you can easily edit and even apply a gradient fill to.</em>

<strong>Bonus tip:</strong> Should you later decide that you need to resize this shape (without distorting its perfectly rounded corners), the “9-slice scaling tool” can come to your rescue:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f57099c-d82e-4de1-9363-c24fa9b721b1/9-slice-scaling.png" alt="9-slice scaling tool in Fireworks" /><br>
<em>Distortion-free scaling is easily achieved with the 9-slice scaling tool.</em>

## Draw Better Triangles

Triangles are everywhere in user interfaces: arrows in buttons, breadcrumbs, pop-over indicators and so on.

While Fireworks provides built-in arrow and polygon vector drawing features, I recommend going the customized route and drawing those vector shapes yourself.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8000330b-2877-4225-9dfe-7f9639733833/smart-arrows.png" alt="Arrow autoshape" /><br>
<em>The Arrow vector autoshape in Fireworks. The yellow control points allow for easy customization of width and height, thickness, type of head, roundness, arrow size and more.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88559b8e-c3f3-44c7-b123-ef16b584ec49/smart-polygon.png" alt="Smart Polygon autoshape" /><br>
<em>The Smart Polygon vector autoshape in Fireworks. You can easily transform it into a triangle!</em>

To illustrate our new workflow, let’s draw a simple arrow like the one in Kickoff’s download button:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52f70c8b-8a41-42b4-83c5-02d45e94f945/kickoff-download-button.png" alt="kickoffapp download button" /><br>
<em>Kickoff’s download button</em>

Let’s start by drawing a nice triangle. Most of the time, you’ll want an <strong>odd number of pixels</strong> for the triangle’s base so that its middle falls on a half-pixel, resulting in a sharp arrow:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fd7d807-c1d5-4e21-b7b8-5508f009f628/odd-even-arrows.png" alt="Full pixel, half pixel" /><br>
<em>On the left, the triangle with an odd width. On the right, the triangle with an even width.</em>

To create a triangle like the one on the left, we start by drawing a simple 7 × 7-pixel vector square using the Rectangle tool (found in the Tools panel, or simply press U). To delete its bottom-right point, use the Subselection tool (press A, or use the white arrow in the Tools panel), select the bottom-right node, then hit the Delete key; Fireworks will remind you that you are trying to change one point of a rectangle primitive and that it must be ungrouped for the change to occur; so, click “OK” to turn it into a vector, and delete the point. After deleting the corner, you’ll end up with this:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd73a4c-7221-4b0f-80e7-806f2fb226da/uncentered-triangle.png" alt="Square with bottom right vector point deleted" /><br>
<em>Our square with the bottom-right point deleted.</em>

We now need to place the bottom-left point <em>exactly</em> at the center, which is located at 7 pixels ÷ 2 = <strong>3.5 pixels</strong> from its current position. When you use your keyboard’s arrows, Fireworks moves the elements by full pixels only and aligns them perfectly to the pixel grid. This is convenient in most cases but not in this one. Luckily, Fireworks gives us a “Move Points” feature (in the Path panel) that lets us specify numeric values:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a131db9-7f54-48ef-a3e8-a17a03c5cbe7/move-points.png" alt="Moving an object by an exact numeric value" /><br>
<em>Moving horizontally by 3.5 pixels will center our bottom point.</em>

If the triangle is now a bit too tall for our arrow, use the Subselection tool to select the center point again, and press the up arrow key twice to move the node up a couple of pixels.

We’re almost done! We just need to draw the 3 × 5-pixel rectangle part of our arrow and then use the “Union Paths” command (<code>Modify → Combine Paths → Union</code>, or press <code>Control/Command + Alt/Option + U</code>) to combine our two paths into one final single vector shape:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8414988c-c16a-4a9a-b806-c0cf5c4d5072/union-paths.png" alt="The perfect vector arrow!" /><br>
<em>The separated shapes are on the left, and the unified shape is on the right.</em>

## Draw Better Ellipses

For some reason, Fireworks has difficulty drawing elegant circles (especially small ones), and the circles tend to have too straight an edge:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046aba4f-7ec2-45cd-86ce-a850bab1ace7/native-circle.png" alt="A circle? Almost." /><br>
<em>A default circle in Fireworks. Note that the top, right, bottom and left edges aren’t rounded enough.</em>

<em>(Note: Fireworks is not the only app to have this problem. Illustrator has it, too.)</em>

We’ll use the “Numeric Transform” window (<code>Control/Command + Shift + T</code>, or in the menu <code>Modify → Transform → Numeric Transform</code>) to make the circle just a tiny bit smaller:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7d07177-bad2-43f5-83e9-7bcc60d39a64/numeric-transform.png" alt="Using Numeric Transform" /><br>
<em>Decreasing the circle’s size by a bit will make it appear more rounded.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/687b8149-f4fe-4608-a1a4-07bc4c7b5cde/final-circle-render.png" alt="Compare the two circles" /><br>
<em>The original on the left, and our result after the transform on the right.</em>

You will notice that the right circle is more elegant; that’s because we have fewer “full” pixels at the edges:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/838b7cb9-53b2-45e8-979c-96298b04bf31/circle-zoom.png" alt="The perfect circle" /><br>
<em>The original on the left, and our perfect circle (after the transform) on the right!</em>

## Fillet Points

One great feature of Fireworks that few people seem to know of is the Fillet Points path tool. Basically, it rounds any angle you select by a value that you specify. To use it, select any vector shape, and in the Path panel in the “Edit Points" section, choose “Fillet Points”:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/addcfc52-f45e-40c1-86f9-d3dca2d497cc/fillet-points-window.png" alt="Fillet Points in the Path panel" /><br>
<em>Fillet Points rounds all of your angles.</em>

Let’s use the built-in vector Star autoshape as an example. Note that you need to <strong>ungroup</strong> autoshapes and rectangle primitives before using Fillet Points; then you can either select the entire vector shape to round all corners or use the Subselection tool to select certain points to round.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da9ad910-1b3b-447f-933e-6fad86a00bae/fillet-points-result.png" alt="Results of using Fillet Points" /><br>
<em>The original shape on the left, and with Fillet Points applied on the right.</em>

This can be a huge time-saver when you want to modify complex shapes with many filters and effects. Now you won’t have to redraw shapes over and over again just because the radius is a few pixels off.</p>

## Inset Paths

Another useful vector tool many designers are unaware of is the <strong>Inset/Expand Paths</strong> feature.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6ba16df-f1ea-42c0-855e-ca78f12907f4/inset-path-window.png" alt="Inset/Expand Paths" /><br>
<em>Inset/Expand Paths is also accessible via <code>Modify → Alter Path → Inset Path</code>.</em>

As you’ve probably guessed by its name, this tool enables you to alter a vector path and make it either smaller (inset) or larger (expand) <strong>without losing its proportions</strong>.

Let’s say we want to make our Star autoshape from above 10 pixels smaller:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68808d67-176b-41ae-8d99-f8e53522a928/inset-path-prompt.png" alt="Inset/Expand dialog" /><br>
<em>The Inset/Expand Paths prompt.</em>

This dialog can be confusing if you do not know what all of the options and abbreviations mean. The third parameter (“Corners”) is the least obvious, because the meaning of “BE, RO, MI” is not defined. The letters are actually abbreviations of “Bevel,” “Round” and “Miter.” You can’t use those abbreviations in the text field, so you need to know the terms they represent. “Bevel” creates squared corners, “Round” creates rounded corners, and “Miter” creates pointed corners; the “Miter limit” specifies the maximum length of the pointed corners before Fireworks replaces them with clipped (or square) tips. We’ll use “Miter” in our example because we obviously want to keep our straight lines.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c891d353-c31d-4884-85e7-e6ec232898a5/inset-paths-result.png" alt="Star autoshape after applying inset/expand paths command" /><br>
<em>And voilà!</em>

## Gradient Dither

Adding a gradient between two similar colors (i.e. colors close in <a href="https://en.wikipedia.org/wiki/Hue">hue</a>) in a big shape often produces an unsightly banding effect, as shown here:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b4b58f-2abe-4b85-bb1f-42d62836528b/gradient-default.png" alt="Banding in gradients" /><br>
<em>Banding is visible in this gradient (especially on LCD screens of the common “twisted nematic” type, which display only <a href="https://en.wikipedia.org/wiki/TFT_LCD#Twisted_nematic_.28TN.29">6 bits per pixel, not 8</a>).</em>

To prevent this, Fireworks <a href="https://www.smashingmagazine.com/2010/05/22/adobe-fireworks-is-it-worth-switching-to-cs5/">introduced in CS5</a> a <strong>Gradient Dither</strong> option that can be used if the edges of the object are set to “Anti-alias” and if you use the “Radial” or “Linear” type of gradient fill.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1560812a-bb70-403a-ab8f-072fa44706d8/gradient-tool.png" alt="Gradient Dither option" /><br>
<em>“Gradient Dither” (found in the Properties panel) makes gradients look better.</em>

The result is a smooth, unified linear gradient, similar to what you would get with CSS browser rendering:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90245f23-fd2c-49ef-aebb-a6fb151ca2ff/gradient-dither-result.png" alt="Gradient with Gradient Dither applied in Fireworks" /><br>
<em>With the “Dither” option applied, the gradient becomes much smoother.</em>

Similarly good results can be achieved by dithering radial gradients.</p>

## Avoid Large Shadows

Fireworks isn’t very good at rendering large shadows (if you use the “Drop Shadow” live filter). If you’re curious about the subtleties involved, <span class="removed_link" title="https://www.tutorialshock.com/tutorials/shadows-photoshop-illustrator-fireworks/">a detailed article on WebDesignShock</span> compares shadow and glow effects in Fireworks, Photoshop and Illustrator.

Instead of a beautiful shadow that slowly fades to a transparent value, the edge of the shadow might look like it has been cut off before fading to full transparency. The issue is particularly noticeable on the Mac version of Fireworks:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cae7769-6625-4e54-8592-aa1e58208558/shadow-default.png" alt="A large drop shadow effect in Fireworks" /><br>
<em>A shadow effect created with the Drop Shadow live filter. Notice the edges (in Fireworks CS5 on a Mac)—yikes! </em>

Here are the settings to use to get this drop-shadow effect on Windows and Mac:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da645487-6da4-435c-868b-c94001411365/drop-shadow-settings-mac.png" alt="A large shadow live effect in Fireworks (on Mac)" /><br>
<em>The settings for the drop-shadow live effect on a Mac. Again, notice the “cut” edges of the shadow.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cf10fd5-827e-4522-882e-6f2da534423e/drop-shadow-settings-win.png" alt="A large shadow live effect in Fireworks (on Win)" /><br>
<em>The settings for the drop-shadow live effect on Windows. The settings are the same, but the edges of the shadow are almost perfect.</em>

So, instead of using a live filter, I usually duplicate the shape (the white rectangle in this example), set its edge to “Feather” and fill it with black.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b050a59-e55e-43f7-bdea-012b33ba494d/shadow-feather-setings.png" alt="A shadow using feather edge" /><br>
<em>Possible settings for the “shadow” vector shape behind the object.</em>

Putting this shape behind the white rectangle produces a better-looking large shadow than the built-in method:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e565a6f0-bbf6-4bf4-91bc-48bd5416d27b/shadow-feather.png" alt="A better drop-shadow!" /><br>
<em>The original shadow on the left, and the “Feather method” on the right.</em>

## Practical Examples

<blockquote>A picture is worth a thousand words.

– <a href="https://en.wikipedia.org/wiki/A_picture_is_worth_a_thousand_words">Fred Barnard</a></blockquote>

Talking about gradients, fills, strokes, vector autoshapes, rounded rectangles, pixels and half-pixels is exciting, but a few real examples would be even better. Below are some illustrations, icons and UI designs that I made exclusively with Fireworks. The tips and tricks covered above made the results more elegant and refined.

<a title="View the Dribbble shot" href="https://dribbble.com/shots/404904-Documents"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/796957ff-06e8-4c12-95cf-4ce60d7cf887/bdc-documents.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>Folder icon</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/356307-Date-Picker"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d46bbfb-cc8c-42c5-8185-058752c0df34/bdc-datepicker.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>UI for a date picker</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/326992-Free"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2295e597-5491-4a9f-a004-4575925f3e6a/bdc-free-label.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>“Free” icon</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/326991-FAQ-icons"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa35c95f-5c89-44f6-addc-d9cafa3bd555/bdc-faq-icons.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>Icons for an FAQ</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/322798-1"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b40856f-c575-4239-874b-9186d6fc45cf/bdc-envelope.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>Envelope icon</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/206798-Monochrome-set"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7ae4005-bbfe-4fe4-9ff5-f7dc08a5078d/bdc-monochrome-icons.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>Monochrome icon set</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/143445-Kickoff-icon"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e184a5-3058-4caf-b066-2325452a7158/bdc-kickoff-teaser-icon.jpg" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>Kickoff teaser icon</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/381637-Email-accounts"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c5b736b-1d9e-49f9-8724-022380e2342f/bdc-email-accounts.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>Email account icons</em>

<a title="View the Dribbble shot" href="https://dribbble.com/shots/295070-Secondary-nav-features"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8d57245-589a-4547-8718-043a1615ae6d/bdc-secondary-nav-features.png" alt="A Dribbble shot by Benjamin De Cock" /></a><br>
<em>Toolbar with navigation icons</em>

As you can see, it’s all about pixel-precision, and Fireworks delivers great results!

## Conclusion

Adobe Fireworks is a powerful tool, offering both <strong>vector</strong>- and <strong>bitmap-editing</strong> capabilities and even hiding some gems. Yes, it imposes different workflows, and some of its default effects are disappointing, but the advantages outweigh the little quirks here and there.

Having to change one’s work habits is always frustrating. Perhaps actions that you once did in a few minutes with your old design tool will now feel incredibly slow. Getting used to a different workflow takes time, and you might not see the benefit of using Fireworks immediately. The best thing you can do is commit to designing an <strong>actual project from start to finish using only Fireworks</strong>. Choose a small project or a personal side project for this purpose. Get your hands dirty for a few hours (or a few days). It’s the only way to be able to judge whether Fireworks really suits your needs. If you’re into UI design, I’ll bet it does!

If you’re interested in learning more about Fireworks, I highly recommend watching the great screencasts produced by <a href="https://twitter.com/rogie">Rogie King</a>. They offer many more tips and tricks for refining designs and achieving more polished results than this article.

Also, the work of others can be a good source of inspiration and knowledge, so have a look at the <a href="https://craigerskine.com/category/fw-png-week">Fw PNG Week</a> series by <a href="https://dribbble.com/craigerskine">Craig Erskine</a>, and download and deconstruct his free source PNG files.

Happy experimenting with Fireworks!

### Further Reading

*   Video tutorials, [Rogie King](https://dribbble.com/rogie), Komodo Media
*   [Fw PNG Week](https://craigerskine.com/category/fw-png-week) (Fireworks PNG files for downloading and learning), Craig Erskine
*   “[I Didn’t Know Fireworks Could Do That!](https://tv.adobe.com/watch/max-2011-design/i-didnt-know-fireworks-could-do-that/)” (video presentation and tutorial), [Dave Hogue](https://www.idux.com/), from Adobe’s MAX 2011 conference
*   “[Design Learning Guide for Fireworks: Using the Path Panel](https://www.adobe.com/devnet/fireworks/learning_guide/design/design_guide_pt7.html),” [Tommi West](https://www.adobe.com/devnet/author_bios/tommi_west.html), Adobe Developer Connection
*   Rapid Fire (Fireworks tutorials), Jose Olarte
*   “[Extracting Logos Using Levels In Adobe Fireworks](https://www.smashingmagazine.com/2012/01/20/extracting-logos-using-levels-in-adobe-fireworks/),” Jose Olarte, Smashing Magazine
*   “[Mixing Up Illustration: Combining Analog And Digital Techniques](https://www.smashingmagazine.com/2011/12/07/mixing-up-illustration-combining-analog-and-digital-techniques/),” David Mottram, Smashing Magazine

{{< signature "mb, al" >}}

<em><strong>Note</strong>: A big thank you to our Fireworks editor, <a href="https://www.optimiced.com/">Michel Bozgounov</a>, for preparing this article.</em>

