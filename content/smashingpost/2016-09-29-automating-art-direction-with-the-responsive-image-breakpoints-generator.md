---
title: Automating Art Direction With The Responsive Image Breakpoints Generator
slug: automating-art-direction-with-the-responsive-image-breakpoints-generator
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5fcb8cc-e2ed-409d-8ac8-68fb0b32d590/generator-screenshot-outputs-500-opt.png
date: 2016-09-29T18:17:40.000Z
author: ericportis
description: >-
  Four years ago, Jason Grigsby asked a surprisingly difficult question: How do you pick responsive image breakpoints? A year later, he had an answer: Ideally, we’d set responsive image performance budgets to achieve “sensible jumps in file size.”
categories:
  - Mobile
  - Responsive Design
  - Responsive Images
---
[Cloudinary built a tool](https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/) that implements this idea, and the response from the community was universal: "Great! Now, what else can it do?" Today, we have an answer: art direction!

Since its release earlier this year, the Responsive Image Breakpoints Generator has been turning high-resolution originals into responsive `<img>`s with sensible `srcset`s at the push of a button. Today, we're launching version 2, which allows you to pair layout breakpoints with aspect ratios, and generate art-directed `<picture>` markup, with smart-cropped image resources to match.

**Recommended reading**: *[Responsive Images Done Right: A Guide To <picture>And srcset</picture>](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)*

## Responsive Image Breakpoints: Asked And Answered

Why did we build this tool in the first place?

Responsive images send different people different resources, each tailored to their particular context; a responsive image is an image that **adapts**. That adaptation can happen along a number of different axes. Most of the time, most developers only need adaptive **resolution** — we want to send high-resolution images to large viewports and/or high-density displays, and lower-resolution images to everybody else. Jason's question about responsive image breakpoints concerns this sort of adaptation.

{{% feature-panel %}}

When we're crafting images that adapt to various resolutions, we need to generate a range of different-sized resources. We need to pick a maximum resolution, a minimum resolution and (here's the tricky bit) some sizes in between. The maximum and minimum can be figured out based on the page's layout and some reasonable assumptions about devices. But when developers began implementing responsive images, it wasn't at all clear how to size the in-betweens. Some people picked a **fixed-step size** between image widths:

<figure><img loading="lazy" decoding="async" src="https://res.cloudinary.com/indysigner/image/upload/v1544089109/breakpoints-constant-step-size_x4ywzn.svg" alt="Rectangles showing the relative dimensions of a group of srcset resources that use a fixed-step-size strategy, with the following widths: 300, 400, 500, 600, 700, 800, 900, 1000, 1100, and 1200" id="steps-fixed-size" /><figcaption>Rectangles showing the relative dimensions of a group of <code>srcset</code> resources that use a fixed-step-size strategy.</figcaption></figure>

Others picked a **fixed number of steps** and used it for every range:

<figure><img loading="lazy" decoding="async" src="https://res.cloudinary.com/indysigner/image/upload/v1544089131/breakpoints-constant-number-of-steps_asg8l2.svg" alt="Rectangles showing the relative dimensions of three groups of srcset resources that use a fixed-number-of-steps strategy. The first group has these widths: 300, 600, 900, 1200. The second: 300, 467, 633, 800. Third: 300, 867, 1433, 2000" id="steps-fixed-number" /><figcaption>Rectangles showing the relative dimensions of three groups of <code>srcset</code> resources that use a fixed-number-of-steps strategy.</figcaption></figure>

Some people picked **common display widths**:

<figure><img loading="lazy" decoding="async" src="https://res.cloudinary.com/indysigner/image/upload/v1544089152/breakpoints-common-displays_kqxzsf.svg" alt="Rectangles showing the relative dimensions of a group of srcset resources scaled to common display widths: 300, 512, 600, 768, 800, 1024, 1200" id="steps-common" /><figcaption>Rectangles showing the relative dimensions of a group of <code>srcset</code> resources scaled to common display widths.</figcaption></figure>

At the time, because I was lazy and didn't like managing many resources, I favored **doubling**:

<figure><img loading="lazy" decoding="async" src="https://res.cloudinary.com/indysigner/image/upload/v1544089177/breakpoints-doubling_ffywdy.svg" alt="Rectangles showing the relative dimensions of a group of srcset resources scaled using a doubling strategy, with these widths: 300, 600, 1200" id="steps-doubling" /><figcaption>Rectangles showing the relative dimensions of a group of <code>srcset</code> resources scaled using a doubling strategy.</figcaption></figure>

All of these strategies are essentially arbitrary. Jason thought there had to be a better way. And eventually he realized that we shouldn't be thinking about these steps in terms of **pixels** at all. We should be aiming for "sensible jumps in file size"; these steps should be [defined in terms of **bytes**](https://cloudfour.com/thinks/sensible-jumps-in-responsive-image-file-sizes/).

For example, let's say we have the following two JPEGs:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc3b957-0861-4036-aeec-933500c3e2b6/bike-big-300px-opt.jpg" width="300" height="200" alt="300 pixels wide (37 KB)" /><figcaption>300 pixels wide (37 KB)</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e88ce4ba-93a8-438c-9df3-422a4eccdfd0/bike-big-1200-opt.jpg" width="1200" height="800" alt="1200 pixels wide (333 KB)" /><figcaption>1200 pixels wide (333 KB)</figcaption></figure>

The biggest reason we don't want to send the 1200-pixel-wide resource to someone who only needs the small one isn't the extra pixels; it's the extra 296 KB of useless data. But different images compress differently; while a complex photograph like this might increase precipitously in byte size with every increase in pixel size, a simple logo might not add much weight at all. For instance, [this 1000-pixel-wide PNG](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04d38dcc-644a-42a8-86cc-2816fd30be36/cloudinary-logo-big.png) is only 8 KB larger than [the 200-pixel-wide version](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03679c90-bb55-4fc5-b9ae-47f78b81e48d/cloudinary-logo-small.png).

Sadly, there haven't been any readily useable tools to generate images at target byte sizes. And, ideally, you'd want something that could generate whole ranges of responsive image resources for you — not just one at a time. [Cloudinary has built that tool](https://cloudinary.com/blog/introducing_intelligent_responsive_image_breakpoints_solutions?utm_source=Smashing_Mag&utm_medium=Byline&utm_campaign=Art_direction_responsive_breakpoints)!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ba01b8-f887-4d51-a093-0f4945fe5759/generator-screenshot-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29fc7fc1-b7d3-45d2-a6cb-76b197563ce9/generator-screenshot-500-opt.png" width="500" height="467" alt="A screenshot of the Responsive Image Breakpoints Generator" id="generator-screenshot" /></a><figcaption>A screenshot of the Responsive Image Breakpoints Generator (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ba01b8-f887-4d51-a093-0f4945fe5759/generator-screenshot-large-opt.png">View large version</a>)</figcaption></figure>

And it has released it as a free [open-source](https://github.com/cloudinary/responsive_breakpoints_generator) web app.

But the people wanted more.

{{% ad-panel-leaderboard %}}

## The Next Frontier? Automatic Art Direction!

So, we had built a solution to the breakpoints problem and, in the process, built a tool that made generating **resolution-adaptable** images easy. Upload a high-resolution original, and get back a fully responsive `<img>` with sensible breakpoints and the resources to back it up.

That basic workflow — upload an image, get back a responsive image — is appealing. We'd been focusing on the breakpoints problem, but when we released our solution, people were quick to ask, "What else can it do?"

Remember when I said that resolution-based adaptation is what most developers need, most of the time? Sometimes, it's not enough. Sometimes, we want to adapt our images along an orthogonal axis: [art direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/).

Any time we alter our images **visually** to fit a different context, we're "art directing." A resolution-adaptable image will look identical everywhere — it only resizes. An art-directed image changes in visually noticeable ways. Most of the time, that means cropping, either to fit a new layout or to keep the most important bits of the image visible when it's viewed at small physical sizes.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e5ff8de-693f-4df3-be9d-ca2a654c5714/art-direction-example-image-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e887a19-042f-4f28-b4dc-dccd2d256a19/art-direction-example-image-preview-opt.jpg" width="500" height="325" alt="On small screens, we want to zoom in on the image's subject" id="art-direction-example-image" /></a><figcaption>On small screens, we want to zoom in on the image's subject.</figcaption></figure>

People asked us for automatic art direction &mdash; which is a hard problem! It requires knowing what the "most important" parts of an image are. Bits and bytes are easy enough to program around; computer vision and fuzzy notions of "importance" are something else entirely.

For instance, given this image:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea1852c7-05ba-4f64-a30b-3558bec10e92/smartdumb-uncropped-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5bedb5f-98b3-49b9-b342-7f5618bb8ec3/smartdumb-uncropped-preview-opt.jpg" alt="A white cat, off-center" width="500" height="333" id="smartdumb-uncropped" /></a><figcaption>(Image source: <a href="https://res.cloudinary.com/demo/image/upload/white_cat.jpg">Cloudinary</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea1852c7-05ba-4f64-a30b-3558bec10e92/smartdumb-uncropped-large-opt.jpg">View large version</a>)</figcaption></figure>

A dumb algorithm might simply crop in on the center:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75445cb9-6eb5-4f7c-8894-0a0604f001b3/dumbcrop-example-image-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff43e3f1-efab-4722-82ae-81656b226fba/dumbcrop-example-image-preview-opt.jpg" width="500" height="750" alt="The subject of the image has been cropped out of the frame" id="dumbcrop-example-image" /></a><figcaption>(Image source: <a href="https://res.cloudinary.com/demo/image/upload/c_fill,ar_4:6/white_cat.jpg">Cloudinary</a>)</figcaption></figure>

What you need is an algorithm that can somehow "see" the cat and intelligently crop in on it.

It took us a few months but we built this, too, and packaged it as a feature [available to all Cloudinary users](https://cloudinary.com/blog/smart_automatic_image_cropping_maybe_you_can_always_get_what_you_want?utm_source=Smashing_Mag&utm_medium=Byline&utm_campaign=Art_direction_responsive_breakpoints).

Here's how it works: When you specify that you want to crop your image with "automatic gravity" (`g_auto`), the image is run through a series of tests, including edge-detection, face-detection and visual uniqueness. These different criteria are then all used to generate a heat map of the "most important" parts of the image.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93b97772-4c41-4aee-961d-6d62eb7512ad/white-cat-g-auto-tests-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df2aa68-396b-4c91-a164-d9da5c770cb1/white-cat-g-auto-heatmap-opt.png" width="154" height="102" alt="The master rolled-up heat map" id="white-cat-g_auto-heatmap" /></a><figcaption>The master rolled-up heat map (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93b97772-4c41-4aee-961d-6d62eb7512ad/white-cat-g-auto-tests-large-opt.png">View large version</a>)</figcaption></figure>

A frame with the new proportions is then rolled over the image, possible crops are scored, and a winner is chosen. Here's a visualization of the rolling frame algorithm (using a [different source image](https://res.cloudinary.com/demo/image/upload/mountain_scene_panoramic.jpg)):

<figure><div class="aspect-ratio"><iframe loading="lazy" src="https://player.vimeo.com/video/184673130" frameborder="0" width="500" height="360" allowfullscreen></iframe></div><figcaption>The rolling frame, visualized. Bluer squares mean higher scores; the green square is the current pick.</figcaption><figure>

The result? Our cat, front and center:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee2e4bc7-cbb4-4c01-8658-251c0a9c37ef/smartcrop-example-image-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/695eff72-341d-4f2e-8f09-6e2ad19ba9a9/smartcrop-example-image-preview-opt.jpg" width="500" /></a><figcaption>(Image source: <a href="https://res.cloudinary.com/demo/image/upload/c_fill,ar_4:6,g_auto/white_cat.jpg">Cloudinary</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee2e4bc7-cbb4-4c01-8658-251c0a9c37ef/smartcrop-example-image-large-opt.jpg">View large version</a>)</figcaption></figure>

Neat!

<p>It was immediately obvious that we could and should use <code>g_auto</code>'s smarts to add automatic art direction to the Generator. After a few upgrades to the markup logic and some (surprisingly tricky) UX decisions, we did it: <a href="https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/">Version 2 of the tool</a> &mdash; now with art direction &mdash; is live.</p>

{{% ad-panel-leaderboard %}}

## Let's Take A Tour

How do you use the Responsive Image Breakpoints Generator?

<p>The workflow has been largely carried over from the first version: Upload an image (or pick one of the presets), and set your maximum and minimum resolutions, a step size (in bytes!), and a maximum number of resources (alternatively, you can simply use our pretty-good-most-of-the-time defaults). Click "Generate," <em>et voila!</em> You'll get a visual representation of the resulting image's responsive breakpoints, some sample markup, and a big honkin' "download images" button.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e90962a-61d8-4cca-8f33-a61b060dc66f/generator-screenshot-inputs-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1506ca41-ee16-470e-b0e0-acd0a5d0cedd/generator-screenshot-inputs-500-opt.png" height="560" width="500" alt="Screenshot of the tool's inputs" id="generator-screenshot-inputs" /></a><figcaption>Screenshot of the tool's inputs (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e90962a-61d8-4cca-8f33-a61b060dc66f/generator-screenshot-inputs-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/255ae8b1-c462-4bb6-ab97-870b777666e9/generator-screenshot-outputs-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5fcb8cc-e2ed-409d-8ac8-68fb0b32d590/generator-screenshot-outputs-500-opt.png" alt="Screenshot of the tool's outputs" id="generator-screenshot-outputs" /></a><figcaption>Screenshot of the tool's outputs (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5fcb8cc-e2ed-409d-8ac8-68fb0b32d590/generator-screenshot-outputs-500-opt.png">View large version</a>)</figcaption></figure>

The new version has a new set of inputs, though, which enable art direction. They're turned off by default. Let's turn a couple of them on and regenerate, shall we?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91d5725e-0a74-4d31-81e4-f220c3828258/generator-screenshot-art-direction-inputs-selected-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c0382a2-178d-4e8b-914a-3b356fdf015a/generator-screenshot-art-direction-inputs-selected-preview-opt.png" height="187" width="500" alt="Screenshot of the art-direction inputs, with 'Desktop' and 'Smartphone' selected" id="generator-screenshot-art-direction-inputs-selected" /></a><figcaption>Screenshot of the art-direction inputs, with "Desktop" and "Smartphone" selected (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91d5725e-0a74-4d31-81e4-f220c3828258/generator-screenshot-art-direction-inputs-selected-large-opt.png">View large version</a>)</figcaption></figure>

The first output section is unchanged: It contains our "desktop" (i.e. full) image, responsively breakpointed to perfection. But below it is a new section, which shows off our new, smartly cropped image:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e59fdf6-8a01-4be6-85bf-05376dd8e34f/generator-screenshot-square-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b0812bf-c935-49b2-add9-a326ed5aaff4/generator-screenshot-square-preview-opt.png" height="475" width="500" alt="Screenshot of the '1:1 Aspect Ratio' section" id="generator-screenshot-square" /></a><figcaption>Screenshot of the "1:1 Aspect Ratio" section (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e59fdf6-8a01-4be6-85bf-05376dd8e34f/generator-screenshot-square-large-opt.png">View large version</a>)</figcaption></figure>

<p>And below <em>that</em>, we now have all of the markup we need for an art-directed <code>&lt;picture&gt;</code> element that switches between the two crops at a layout breakpoint.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7362f81-30fd-429b-9da9-5eba270aab6e/generator-screenshot-picture-markup-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce223039-3d4e-4235-8cca-22f7f5bdfdca/generator-screenshot-picture-markup-preview-opt.png" width="500" height="307" alt="Screenshot of the picture markup section" id="generator-screenshot-picture-markup" /></a><figcaption>Screenshot of the <code>&lt;picture&gt;</code> markup section (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7362f81-30fd-429b-9da9-5eba270aab6e/generator-screenshot-picture-markup-large-opt.png">View large version</a>)</figcaption></figure>

<p>Finally, there's a live <code>&lt;picture&gt;</code> example that shows you what all of that markup actually does.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a5557fe-d524-4154-8200-c4ec976bb60d/generator-screenshot-picture-live-large-opt-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21babac1-9cea-4465-a93e-ae1847883ec3/generator-screenshot-picture-live-opt.png" width="500" height="371" alt="" /></a><figcaption>Screenshot of the "Live Picture Element in Action" section (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a5557fe-d524-4154-8200-c4ec976bb60d/generator-screenshot-picture-live-large-opt-1.png">View large version</a>)</figcaption></figure>

Let's circle back and look at the art direction inputs in a little more detail.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16b36f74-c302-4ead-923b-553d9f1e63bd/generator-screenshot-art-direction-inputs-annotated-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57ba2aeb-554d-4a8e-aebc-ea4ac5f061e8/generator-screenshot-art-direction-inputs-annotated-preview-opt.png" height="187" width="500" alt="Screenshot of the art direction inputs, annotated to point out what each thing does" id="generator-screenshot-picture-markup" /></a><figcaption>Screenshot of the art direction inputs, annotated to point out what each thing does (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16b36f74-c302-4ead-923b-553d9f1e63bd/generator-screenshot-art-direction-inputs-annotated-large-opt.png">View large version</a>)</figcaption></figure>

Each big box maps to a device type, and each device type has been assigned a layout breakpoint. The text under the device type's name shows the specific media query that, when true, will trigger this crop.

Below that, we can specify the aspect ratio that we want to crop to on this device type.

<p>Below <em>that</em>, we specify how wide the image will appear relative to the width of the viewport on this type of device. Will it take up the whole viewport (100%) or less than that? The tool uses this percentage to generate simple <a href="https://cloudfour.com/thinks/responsive-images-101-part-5-sizes/"><code>sizes</code> markup</a> &mdash; which specifies how large the image is in the layout. If you're using this code in production, you'll probably want to go back into the example markup and tailor these <code>sizes</code> values to match your particular layout more precisely. But depending on your layout, inputting rough estimates here might be good enough.</p>

And there you have it: simple, push-button art direction.

## Automation

<p>What if you want to work with more than one image at a time? If you're building entire websites with hundreds or thousands (or hundreds of thousands!) of images &mdash; especially if you're working with user-generated content &mdash; you'll want more than push-button ease; you'll need full automation. For that, there's Cloudinary's API, which you can use to call the smart-cropping and responsive image breakpoints functions that power the Generator, directly. With the API, you can create customized, optimized and <strong>fully automated</strong> responsive image workflows for projects of any shape or size.</p>

For instance, here's Ruby code that will upload an image to Cloudinary, smart-crop it to a 16:9 aspect ratio, and generate a set of downscaled resources with sensible responsive image breakpoints:

<pre><code class="language-ruby">
Cloudinary::Uploader.upload(&quot;sample.jpg&quot;,
    responsive_breakpoints: {
        create_derived: true,
        bytes_step: 20000,
        min_width: 200,
        max_width: 1000,
        transformation: {
            crop: :fill,
            aspect_ratio: &quot;16:9&quot;,
            gravity: :auto
        }
    }
)
</code></pre>

<p>If you work only on the front end, all of this functionality is available via URL parameters, too! Here's a URL powered by <a href="https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/">Client Hints</a> and smart-cropping that does the same thing on <em>download</em> that the Ruby code above does on <em>upload</em> &mdash; <em>and</em> it delivers different, dynamically optimized resources to different devices, responsively:</p>

<pre><code class="language-markup">
https://demo-res.cloudinary.com/sample.jpg/c_fill,ar_16:9,g_auto,q_auto/w_auto:breakpoints/sample.jpg
</code></pre>

A tremendous amount of smarts is packed into that little URL!

## Final Thoughts

<p>But back to the Generator. Now, it can do more than "just" pick your image breakpoints &mdash; it can pick your art-directed crops, too. And it will generate all of the tedious resources and markup for you; upload one high-resolution original, and get back all of the markup and downscaled resources you need to include a scalable <em>and</em> art-directed image on your web page.</p>

<p>Have I mentioned that the Responsive Image Breakpoints Generator is free? And <a href="https://github.com/cloudinary/responsive_breakpoints_generator">open-source</a>? <a href="https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/">Give it a whirl</a>, and please send us feedback. Who knows, maybe we'll be back again soon with version 3!</p>

{{< signature "vf, il, al" >}}