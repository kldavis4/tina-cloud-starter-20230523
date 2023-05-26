---
title: A Better Way To Design For Retina In Photoshop
slug: retina-design-in-photoshop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ec4e467-85b0-4ed5-9a22-91665cce2f28/01-iassessor-opt.png
date: 2015-05-18T21:02:36.000Z
author: murdochcarpenter
description: >-
  Recently, I had a project in which I needed to produce high-fidelity screens
  for a tablet. I was to present these screens on the device and also produce a
  [clickable
  prototype](https://www.smashingmagazine.com/2014/03/06/building-clickthrough-prototypes-to-support-participatory-design/).
  They needed to be
  [pixel-perfect](https://www.smashingmagazine.com/2014/10/15/create-assets-for-multiple-scale-factors/).
  The timeline was tight (as always), so I went with my go-to tool,
  [Photoshop](https://www.smashingmagazine.com/2013/04/22/repurposing-photoshop/).
  I’ve been using it for over 10 years, and it gives me the fastest high-quality
  output.

  Are you designing at “Retina” resolution in Photoshop? If the answer is yes,
  then this article is for you. I will walk you through the problems I faced in
  **creating Retina mockups** to be displayed on a tablet device. I will then
  explain a way to work that is easier and gives you better performance. This is
  about my experience with Photoshop, but it could be applied to Illustrator and
  other software.
categories:
  - Graphics
  - Design
  - Photoshop
  - Optimization
  - Performance
---
Recently, I had a project in which I needed to produce high-fidelity screens for a tablet. I was to present these screens on the device and also produce a clickable prototype. They needed to be pixel-perfect. The timeline was tight (as always), so I went with my go-to tool, Photoshop. I’ve been using it for over ten years, and it gives me the fastest high-quality output.

Are you designing at “Retina” resolution in Photoshop? If the answer is yes, then this article is for you. I will walk you through the problems I faced in creating Retina mockups to be displayed on a tablet device. I will then explain a way to work that is easier and gives you better performance. This is about my experience with Photoshop, but it could be applied to Illustrator and other software.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ec4e467-85b0-4ed5-9a22-91665cce2f28/01-iassessor-opt.png" alt="Here are a few designs for the tablet application" /><figcaption>Here are a few designs for the tablet application.</figcaption></figure>

Throughout this article, I will use the @2x and @3x notation. These represent the Retina buckets for iOS. A great example is the app’s icons. For the original iPhone, it would be 60 × 60 pixels (@1x). For the iPhone 4, it would be exactly double, 120 × 120 pixels (@2x). Now, the latest devices are dipping into triple territory. For the iPhone 6 Plus, the icon would be 180 × 180 (@3x). When talking about @2x or @3x, I am referring to using double or triple the pixel dimensions. All should become clear as you read on.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Retina Asset Workflow You’ve Always Wanted For Photoshop](https://www.smashingmagazine.com/2016/03/the-retina-asset-workflow-youve-always-wanted-for-photoshop/)
*   [Create Pixel-Perfect Assets For Multiple Scale Factors](https://www.smashingmagazine.com/2014/10/create-assets-for-multiple-scale-factors/)
*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)
*   [Retinize It: Free Photoshop Action For Slicing Graphics For HD Screens](https://www.smashingmagazine.com/2013/07/retinize-it-photoshop-action-slicing-graphics-retina/)

{{% feature-panel %}}

## The Problems

Now, let’s get into the design of this tablet application. Like many other designers, I had been told that one must design at Retina resolution. The general consensus is @2x or @3x. So, I set out on my merry way, designing @2x. The design would be presented on a Nexus 9 with a 4:3 ratio, so my Photoshop canvas was set up to 2048 × 1536 pixels. After creating a few screens, I realized in practice this doesn’t work well at all. Let’s work through the issues I found.</p>

### Zoom Factor

At first, this is no big deal. Zoom out to 50% or 33% to see your design at roughly 1:1. But at the same time, it’s a bit ridiculous, right?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2172f8c4-082a-4899-ab9e-9111e7529622/02-zoom-opt.png" alt="Shown is the corner of a design at @1x to @3x" /><figcaption>You can quickly see the resolution getting out of control. Shown is the corner of a design at @1x to @3x.</figcaption></figure>

Why should you have to zoom in and out constantly to see what’s going on? It also completely ruins <a href="https://blogs.adobe.com/jkost/2014/04/align-to-pixel-grid-in-photoshop.html">pixel-snapping</a>, which works best at 100%. It’s almost impossible to know whether a pixel is aligned when you are zoomed at 33% or 50%! Suffice it to say, I got pretty fed up zooming in and out like a maniac to get things aligned pixel-perfectly.</p>

### Performance

This is a big one. Let’s use a tablet with a 4:3 ratio as an example. I set up a blank PSD @1x (which is 1024 × 768 pixels) and another @2x (2048 × 1536) and a third @3x (3072 × 2304). I then did some comparisons.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9f9cee9-4fb2-403e-a142-e4b2269a4dc9/03-performance-opt.png" alt="Table showing number of pixels, size on disk and memory for @1x – @3x blank PSD" /><figcaption>Table showing number of pixels, size on disk and memory for @1x to @3x blank PSDs.</figcaption></figure>

First, I looked at the number of pixels in the PSDs. The @2x PSD has four times as many pixels. The @3x has nine times as many. This directly affects memory usage, which itself goes up by four times and nine times! For our blank PSD, this went from 2.25M to 9M @2x, and then 20M for @3x.

Last but not least, it also needs to store all of these extra pixels. So, your file size increases as well. The size on disk went up by 280% for the @2x, and up by 590% for the @3x. Now, in our blank PSD this is only an increase from 60 to 358 KB. But once you’ve got some serious smart objects and layers going on, watch out! Let’s take the example of a PSD that is 100 MB. The @3x could be 590 MB. Then, multiply this by the 20 to 30 documents in your project!

From a performance standpoint, it’s very clear that working at Retina is going to cost you some serious RAM, CPU and disk usage.</p>

### Font Size

This issue becomes obvious pretty quickly when you’re working @2x or @3x. Suppose you’ve set out to make a text box with the font set to 16 pixels. But @2x this is 32 pixels, and @3x it’s 48 pixels! Not ideal, is it, having to constantly multiply by two or three? I don’t know about you, but I could do without the constant math. When I design, I want to know that 16 pixels is 16 pixels!

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a5237a-9e8f-409a-8c68-1056248c71bb/04-fonts-opt.png" alt="Font sizes become a game of multiplication when working at Retina" /><figcaption>Font sizes become a game of multiplication when working at Retina scale.</figcaption></figure>

### Whole Pixels

Here’s another gotcha. What happens when you use <code>1px</code> at @2x Retina? You guessed it, it becomes 0.5 pixels! And @3x it would be even worse, 0.33 pixels! So, you also have to constantly be aware that your sizes must be divisible by 2 or 3 when working in Retina. Another consideration comes into play if you ever use @2x with an odd pixel value. Let’s say you have a box that is 33 pixels wide; when converted back to @1x for build, this becomes 16.5 pixels! Yet another brain drain from working with Retina.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92587a8a-1adc-4251-9069-d338a0c0fa5b/05-pixels-opt.png" alt="Illustration of how 1px would fall back from @1x to @3x" /><figcaption>Illustration of how <code>1px</code> would fall back from @1x to @3x.</figcaption></figure>

### Specs

This is another issue I’ve seen in the workplace: designers who have been working @2x or @3x and then begin to spec their design for developers. This usually involves documenting padding, widths, heights, font sizes and so on to ensure that the design is built well. But they forget they are at double or triple the resolution. So, the poor old developers get a complete spec in which they need to divide everything by 2 or 3! Not great, is it? Why make their life harder?

The other option is that the designer could save a new PSD at 50% or 33%, and then spec from that. But Retina-land looks like a one-way street. It’s hard to see through those blinkers.</p>

## The Good News

Don’t worry. After all the bad news, there is good news. While working on <a href="https://murdochcarpenter.com/illustrator-script-export-android-multi-res-pngs/">exporting icons for Android from Illustrator</a>, I discovered the world of density-independent pixels (DP). You can read a big long explanation on Android Developers about “<a href="https://developer.android.com/guide/practices/screens_support.html">Supporting Multiple Screens</a>,” or I can break it down for you real quick.

Basically a DP is the @1x pixel dimension or, in Android terms, the baseline density that is medium (MDPI). A density-independent pixel is the same as 1 physical pixel on a 160 DPI screen. The conversion is <code>DP = pixel ÷ (DPI ÷ 160)</code>.

Let’s use our tablet example with a display of 2048 × 1536 pixels and 320 DPI. Running through the equation above, for the width we get 1024 DP, and for the height, 768 DP. This becomes our baseline resolution. And we also need to know the scale factor for image assets. That equation is: <code>scale factor = DP × (DPI ÷ 160)</code>.

Using the width of 1024 DP and the device’s 320 DPI, if we run through this equation, we’d get a scale factor of 2. This means we’d need to output @2x assets for display on this device. It’s also pretty straightforward to see that <code>2048 ÷ 1024 = 2</code>. So, don’t stress about the equations!

As another quick example, let’s take the Nexus 5. With its resolution of 1920 × 1080 pixels and 480 DPI, the DP units work out to be 640 × 360. Then, the scale factor comes out as @3x. So, now you know your DP dimensions and scale factor for assets.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c202b52-549c-4bd5-8a98-952caaede7d2/06-dp-opt.png" alt="Example of @1x to @3x DP units on various devices" /><figcaption>Example of @1x to @3x DP units on various devices.</figcaption></figure>

Once you have the DP dimensions, those become your PSD canvas size at 72 DPI. So, the answer to this mystery is to <strong>design @1x or in DP</strong>.

Some other devices don’t fit quite as nicely in these buckets, but you get the idea. The point here is that you are reducing to the baseline DP units and that you know the scale for exporting images.

## “But I’m Stuck With @1x Images!”

Correct. And a @1x PNG would look horrible on a Retina device. What I needed was a way to work at @1x and with DP units, but export to @2x or @3x to preview on a device. My clients would accept nothing less. So, using my knowledge of exporting icons to various DPIs for Android, <a href="https://murdochcarpenter.com/illustrator-script-export-android-multi-res-pngs/">which I’ve covered elsewhere</a>, I applied the same technique to Photoshop.

The solution to my problem was a Photoshop script that exports any canvas to a @2x or @3x PNG for previewing on a device. Thus, one can keep working @1x and in DP and get all of the performance benefits and still get good-quality screens. Have your cake and eat it too, if you will.</p>

## Export Scripts

Here’s a quick rundown on how the script works:

1.  Your Photoshop canvas is resized to 200% or 300%.
2.  It creates a new folder named `retina`, where you PSD is saved.
3.  Then, it saves a PNG as `<documentname>_2x.png` or `<documentname>_3x.png`.
4.  It also clears and purges the history (“Undo”).
5.  Then, it saves the document exactly how it was before the script ran.

The scripts are very easy to modify. If you want to rename the folder or file name, you would just change the variables shown below:

<pre><code class="language-bash">
var scale = "200%";
var folderName = "retina";
var extensionName = "_2x.png";
</code></pre>

## Installation

<a href="https://github.com/murd/psd-export-document-retina-png/archive/master.zip">Download the scripts</a> (ZIP, 4 KB) or view the project on <a href="https://github.com/murd/psd-export-document-retina-png/">GitHub</a>.

Once they’re downloaded and unzipped, copy the scripts and paste them into Photoshop’s <code>Scripts</code> folder: on Windows, <code>Program FilesAdobeAdobe Photoshop CC 2014PresetsScripts</code>, and on Mac, <code>ApplicationsAdobePhotoshop CCPresetsScripts</code>.

Please be aware this will <strong>vary according to your Photoshop version and operating system</strong>.

You’re almost done. Restart Photoshop, and the scripts will be ready to go. Now, anytime you want to export a PNG @2x or @3x, just click “File” → “Scripts” → “ExportDocument2xPNG” or “File” → “Scripts” → “ExportDocument3xPNG”:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d3f5ac6-ef2b-4cea-9b19-4778d3d1ae22/07-script-a-opt.png" alt="Click File" /><br>
<figcaption>Click “File.”</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ce04688-c7b2-4da2-b3f7-17f772d8d3c4/08-script-b-opt.png" alt="Go into Scripts and click ExportDocument2xPNG or ExportDocument3xPNG" /><br>
<figcaption>Go into “Scripts” and click “ExportDocument2xPNG” or “ExportDocument3xPNG.”</figcaption></figure>

You are now left with Retina images @2x or @3x, ready to put on the device.</p>

## Tips

Keep in mind a few things if you go for this approach. Use shapes and vectors wherever possible. They scale up perfectly, as do layer styles. Always use smart objects for any bitmaps. Keep in mind they will still need to be @2x or @3x inside.

Using this approach with <a href="https://helpx.adobe.com/photoshop/using/generate-assets-layers.html">Photoshop’s generator</a> also works great. Any layers or layer groups can be exported @2x and @3x. And you will know they are pixel-perfect.

After producing the designs, I needed to create a clickable prototype for the client. I found that the exported PNGs work great with <a href="https://marvelapp.com/">Marvel</a>. Marvel allows you to upload your images to Dropbox or through its own system. Once they’re uploaded, you can create hotspots and link to other screens. Then, you can view on a device to see your designs in action. The other bonus was that I used up less bandwidth and Dropbox space! Retina PSDs would have been superheavy!

## Illustrator

If you use Illustrator, you can also work @1x and in DP. Make sure your document is set up for the web at 72 DPI. Then, you can manually export @2x and @3x PNG images by clicking “File” → “Export…” and selecting “PNG.” Click “Export.” Then, use the “Resolution” dropdown menu, click “Other” and input <code>144 PPI</code> for @2x or <code>216 PPI</code> for @3x. As with the Photoshop scripts, this can also be configured to be just one click!

## Sketch

Your other option is to use the increasingly popular app <a href="https://bohemiancoding.com/sketch/">Sketch</a>. It comes all set up and ready to go @1x with a vector-based workflow. There is built-in support for exporting @2x and @3x from layers and slices. Just note the requirement of operating system. The creator, Bohemian Coding, is proud to develop exclusively for Mac, with no plans to support Windows or Linux (according to its FAQ). It’s a great program if your workflow and business support it.</p>

## Thanks For Reading

Well, I hope this has been of use to you. It certainly has improved my workflow. Now I get superlight and fast PSDs that can be exported to Retina scale for viewing on a device. And the best part is that I am no longer maniacally zooming in and out or multiplying and dividing my pixels!

{{< signature "da, al, ml" >}}

