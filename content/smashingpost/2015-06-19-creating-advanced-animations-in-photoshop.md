---
title: How To Create An Advanced Photoshop Animation
slug: creating-advanced-animations-in-photoshop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af4f62a7-db95-498e-821f-66ffc5f468cf/p1-03-timeline-2-opt-small.jpg
date: 2015-06-19T07:12:27.000Z
author: stephenpetrany
description: >-
  While **animation in Photoshop** is not a new concept, it definitely has come
  a long way in the last few years: The Timeline panel has been overhauled,
  video layers have been introduced, as has the ability to create keyframe
  animation. These additions have really upped Photoshop’s game.

  Even though Photoshop is still a long way off from being able to create the
  high-end and cinematic animations of such programs as After Effects, it still
  **has enough power to create complex animation** — which is especially useful
  if you don’t want to spend time learning a new application.
categories:
  - Graphics
  - Tutorials
  - Photoshop
  - Animation
---
While <strong>animation in Photoshop</strong> is not a new concept, it definitely has come a long way in the last few years: The Timeline panel has been overhauled, video layers have been introduced, as has the ability to create keyframe animation. These additions have really upped Photoshop’s game.

Even though Photoshop is still a long way off from being able to create the high-end and cinematic animations of such programs as After Effects, it still <strong>has enough power to create complex animation</strong> — which is especially useful if you don’t want to spend time learning a new application.

In this article, I will share several advanced techniques to help you <strong>create complex animations</strong>. We’ll look at the Timeline panel and the different properties that can be animated. We’ll also explore the roles that adjustment layers, filters and smart objects can have in animation (and how to combine all three for some amazing effects). Because the topics and techniques in this article are advanced, a moderate level of Photoshop knowledge is expected.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Functional Animation In UX Design](https://www.smashingmagazine.com/2015/05/functional-ux-design-animations/)
*   [Free Photoshop Tools For Web Designers](https://www.smashingmagazine.com/2016/02/free-photoshop-tools-for-web-designers/)
*   [A Better Way To Design For Retina In Photoshop](https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/)
*   [Practical Techniques On Designing Animation](https://www.smashingmagazine.com/2015/06/practical-techniques-on-designing-animation/)

{{% feature-panel %}}

## Overview Of Timeline Panel

Opening the Timeline panel (“Window” → “Timeline”) allows you to select between two types of timelines: video and frame. The frame timeline is for frame-by-frame animation and can be very limiting. It generally works by converting the layers in your Layers panel to individual frames. I won’t go into any more detail on this timeline; I want to focus on the video timeline.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c228109-ddba-4c4a-8f72-3bad60306ff9/p1-01-overview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93702495-be34-4767-8bf6-8b5ae8a14672/p1-01-overview-opt-small.jpg" alt="Photoshop Animation - It has two timelines for you to choose from." width="500" height="231" /></a><figcaption>Photoshop has two timelines for you to choose from. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c228109-ddba-4c4a-8f72-3bad60306ff9/p1-01-overview-opt.jpg">View large version</a>)</figcaption></figure>

### Video Timeline

The video timeline allows for keyframe animation — which is an animation process in which you define key points of animation along a timeline and Photoshop will interpret the in-between frames to create a cohesive animation. Let’s go ahead and create a very simple animation to see how this works.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/057c2a79-f4d5-4f58-b32d-5fcd4f62b94f/p1-02-timeline-1-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9778e2c2-adf0-445a-9daa-0ef5ab0ff0fc/p1-02-timeline-1-opt-small.jpg" alt="Photoshop Animation - The Video Timeline panel shows a layer (1) with layer properties (2). The timeline shows the Current Time Indicator (3) and existing keyframes (4)." width="500" height="400" /></a><figcaption>The video timeline panel shows a layer (1) with layer properties (2). The timeline shows the current time indicator (3) and existing keyframes (4). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/057c2a79-f4d5-4f58-b32d-5fcd4f62b94f/p1-02-timeline-1-opt.jpg">View large version</a>)</figcaption></figure>

As you probably noticed from the image above, the video timeline shows a representation of layers in the Layers panel. Each layer in the timeline has a dropdown panel that exposes the layer properties (these are the properties that can be animated). To animate a layer property, simply click the stopwatch icon, which enables keyframe animation. Notice that a keyframe is automatically placed at the current time indicator.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742f8e02-b369-4e21-a01f-7176cd8610db/p1-03-timeline-2-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af4f62a7-db95-498e-821f-66ffc5f468cf/p1-03-timeline-2-opt-small.jpg" alt="The stopwatch icon has been selected for the Position property. A keyframe is automatically added to the timeline." /></a><figcaption>The stopwatch icon has been selected for the “Position” property. A keyframe is automatically added to the timeline. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742f8e02-b369-4e21-a01f-7176cd8610db/p1-03-timeline-2-opt.jpg">View large version</a>)</figcaption></figure>

Move the current time indicator to another point in the timeline and reposition the layer. Again, another keyframe will automatically be added to the timeline.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3e7f53-9482-4656-8c53-b89290248880/p1-04-timeline-3-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52493f7f-d143-4e93-9ec0-c5db658a696a/p1-04-timeline-3-opt-small.jpg" alt="Moving the layer automatically adds a keyframe at the current time indicator's location on the timeline." /></a><figcaption>Moving the layer automatically adds a keyframe at the current time indicator’s location in the timeline. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3e7f53-9482-4656-8c53-b89290248880/p1-04-timeline-3-opt.jpg">View large version</a>)</figcaption></figure>

Playing back the animation shows how the object on the canvas moves from one position to the next.</p>

{{< vimeo id="129368066" >}}

Photoshop automatically creates the animation in between the keyframes.</p>

### Layer Types

Now that we have a good idea of how the animation process works in Photoshop, let’s take a closer look at the common layer types that can be animated. Because different layer types have different properties to animate, pay attention to which layer types are being used.

The <strong>standard (pixel) layer</strong> is a layer that contains pixel information. This is the most common (and most basic) layer in Photoshop. Layer properties include:

*   position,
*   opacity,
*   styles.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ce257be-696c-4d07-91e5-2ac1e5fed4b5/p1-06-layer-standard-opt.jpg" alt="A standard layer in the timeline with the layer properties exposed." /><br>
<figcaption>A standard layer in the timeline with the layer properties exposed.</figcaption></figure>

Adding a <strong>layer mask or vector mask</strong> to any layer will introduce additional properties specific to that mask. Layer properties that are added to the layer’s existing properties include:

*   layer or vector mask position
*   layer or vector mask enabling

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9b831b-beb0-4859-aa01-6932fdbe1f01/p1-07-layer-mask-opt.jpg" alt="A layer with a layer mask in the timeline" /><br>
<figcaption>A layer with a layer mask in the timeline.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e247a59-2eb5-4cbd-88b4-63631133767f/p1-08-layer-vector-mask-opt.jpg" alt="A layer with a vector mask in the timeline" /><br>
<figcaption>A layer with a vector mask in the timeline.</figcaption></figure>

A <strong>shape layer</strong> contains a shape (whether from one of the shape tools or the Pen tool) or a line segment. Because shapes and line segments are built with vector mask information, those mask properties will appear in addition to the other layer properties. Layer properties include:

*   position,
*   opacity,
*   styles,
*   vector mask position,
*   vector mask enabling.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/338ef190-2869-4ad8-9e19-550986aaa5d5/p1-09-layer-shape-opt.jpg" alt="A shape layer in the timeline with the layer properties exposed" /><br>
<figcaption>A shape layer in the timeline with the layer properties exposed.</figcaption></figure>

A <strong>text layer</strong> contains editable text. If text has been rasterized, then the layer will no longer be a text layer, but rather will be a standard layer with pixel information. Layer properties include:

*   transform,
*   opacity,
*   styles,
*   text warp.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14939263-938c-4abc-ba4a-b9f308dd6e4f/p1-10-layer-text-opt.jpg" alt="A text layer in the timeline with the layer properties exposed" /><br>
<figcaption>A text layer in the timeline with the layer properties exposed.</figcaption></figure>

A <strong>smart object</strong> can contain any one or combination of the above layer types. A smart object acts like a wrapper for any layer, preserving the original layer while using a new set of properties. These properties include:

*   transform,
*   opacity,
*   styles.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/784b2d75-ae87-4dbe-a961-86553db0143b/p1-11-layer-smart-object-opt.jpg" alt="A text layer in the timeline with the layer properties exposed" /><br>
<figcaption>A text layer in the timeline with the layer properties exposed.</figcaption></figure>

A word of warning when using smart objects. Because a smart object preserves the original quality of the layer or the set of layers it contains, it can be scaled and rescaled without losing quality. However, it cannot be scaled any larger than the size of the original layer it contains. Doing so would cause the smart object to lose quality.

At this point, I want to mention two <strong>other layer types</strong> — a video layer and a 3D layer. Both of these layers are completely unique from the other layer types mentioned. The video layer is actually a layer group that contains its own set of properties, while the 3D layer — besides containing a unique set of properties — is manipulated in an environment entirely separate from the other layers, adding to the level of complexity. Due to the uniqueness of these two layer types, I will not go into detail here. You can see how both layers are represented in the timeline below:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2d7f5e-0bb0-433f-b91e-bf3e7ef341d4/p1-12-layer-video-opt.jpg" alt="A video layer group in the timeline with the layer properties exposed" /><br>
<figcaption>A <strong>video layer</strong> group in the timeline with the layer properties exposed.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b8545e3-d19c-4a8e-b78d-df2be65c7b6e/p1-13-layer-3d-opt.jpg" alt="A 3D layer in the timeline with the layer properties exposed" /><br>
<figcaption>A <strong>3D layer</strong> in the timeline with the layer properties exposed.</figcaption></figure>

I encourage you to explore these two layer types on your own. For the rest of this article, I will be focusing only on the traditional layer types, excluding video and 3D.</p>

### Layer Properties

Now that we have a grasp of the different layer types, let’s examine the different properties that we are able to animate. Knowing how each property works is important to understanding their limitations and how to get around them. Let’s look at the common animation properties.

The <strong>Position</strong> property allows for movement along the X- and Y-axis. Manipulate the position of an object by using the Move Tool.</p>

{{< vimeo id="129368110" >}}

The object’s Position property was keyframed to move the ball back and forth along the x axis.</p>

<strong>Opacity</strong> allows you to keyframe the opacity of a layer. The Opacity control can be found in the Layers panel.</p>

{{< vimeo id="129227188" >}}

The object’s opacity was keyframed at 100% and 0% to create a fading animation.

The <strong>Style</strong> property allows you to keyframe the layer styles of a layer. Access the layer styles by double-clicking a layer in the Layers panel.</p>

{{< vimeo id="129227189" >}}

The object’s layer styles (Bevel &amp; Emboss, Color Overlay, and Drop Shadow) were all keyframed to create a pulsing animation.

The <strong>layer mask or vector mask position</strong> keyframes the x and y positions of each mask. It works best when the mask is not linked to the layer.</p>

{{< vimeo id="129227190" >}}

The mask’s position is keyframed to scrub across the layer, revealing the background layer.</p>

<strong>Enabling or disabling a layer or vector mask</strong> is also possible. To enable or disable a layer mask, go to “Layer” → “Layer Mask” and select either “Enable” or “Disable.” For vector masks, go to “Layer” → “Vector Mask.” Alternatively, you can “Shift + Click” the mask in the Layers panel to toggle on or off.</p>

{{< vimeo id="130180321" >}}

The mask is keyframed to be enabled, then disabled after a short time, causing a reveal.

Specific to text layers, the <strong>Text Warp</strong> property allows you to keyframe any text warp applied to a text layer. You can access a list of text warp effects by going to “Type” → “Warp Text.”

{{< vimeo id="129227193" >}}

A Flag warp was applied to the text and keyframed to create a warping animation.

The <strong>Transform</strong> property allows you to keyframe transformation to a layer. Various transformations (such as Rotate and Scale) can be accessed by going to “Edit” → “Transform,” or by pressing <code>Control + T</code> to enter Free Transform mode.</p>

{{< vimeo id="129227196" >}}

The object’s Scale and Rotation are keyframed to create a spinning star that grows and shrinks.</p>

## Learning Some New Techniques

In this next section, we will combine what we learned above to explore some new animation techniques. We’ll also explore how to manipulate animations with adjustment layers and filters, how to create complex movement by layering animations, and even how to create organic-looking effects.</p>

### Using Template Layers With Smart Object Animations

Because smart objects can contain multiple layers, we can create temporary layers that act as templates to help us create more complex animations. For example, in the animation below, I’ve created a red dot that moves around in a circle. Typically, this would be difficult to create, requiring many keyframes. With smart objects, we can use template layers to simplify the process. Let’s see how it’s done:

{{< vimeo id="129227102" >}}

A red dot moving around in a circle.

In the scene below, I have created two layers: one with a red dot, labeled “Dot,” and the other with a large gray circle, labeled “Template Shape.” I’ve added hash marks to the large gray circle to better demonstrate movement.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb0d124a-fc12-4e81-a7a7-3afb0d10df1d/p2-02-template-step1-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf45a2ec-8034-48bf-8503-329ea17cb0e4/p2-02-template-step1-opt-small.jpg" alt="Scene consisting of two layers, a red dot and large, gray circle." /></a><figcaption>Step 1: Scene consisting of two layers, a red dot and a large gray circle. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb0d124a-fc12-4e81-a7a7-3afb0d10df1d/p2-02-template-step1-opt.jpg">View large version</a>)</figcaption></figure>

To start, I’ll select both layers and convert them to a smart object. This can be done by right-clicking one of the selected layers and choosing “Convert to Smart Object” from the pop-up list.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e22be62-97ad-4bc3-aeed-44c8a18a4beb/p2-03-template-step2-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ea9b21c-2218-4713-98da-36e9b501d8da/p2-03-template-step2-opt-small.jpg" alt="Convert layers to a smart object" /></a><figcaption>Step 2: Convert layers to a smart object. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e22be62-97ad-4bc3-aeed-44c8a18a4beb/p2-03-template-step2-opt.jpg">View large version</a>)</figcaption></figure>

Now, we can animate both objects as a single layer. Because this is a smart object, I have access to the Transform property in the Timeline panel, which allows me to keyframe rotation. I’ve added a keyframe at each half rotation, for one full rotation. The result is the circle, rotating 360 degrees.</p>

{{< vimeo id="129227104" >}}

Step 3: Both layers rotate as one.

Now that our animation is working, we’ll need to remove the template shape. To do this, double-click to edit the smart object’s thumbnail in the Layers panel. Once the smart object is open, we can hide the “Template Shape” layer.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74b65e7f-6981-4793-aa3c-9acdc5cec80d/p2-05-template-step4-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab523ae2-e484-4a64-8100-902965e06008/p2-05-template-step4-opt-small.jpg" alt="Hide the Template Shape layer." /></a><figcaption>Step 4: Hide the “Template Shape” layer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74b65e7f-6981-4793-aa3c-9acdc5cec80d/p2-05-template-step4-opt.jpg">View large version</a>)</figcaption></figure>

All we need to do now is save the smart object document and return to our original document. We can see that our red dot moves around in a circle without the gray shape in the background.</p>

{{< vimeo id="129227102" >}}

A red dot moving around in a circle.</p>

### Embedding Animations in Smart Objects

As I mentioned, smart objects can consist of any type (or multiple types) of layers — including layers that already contain keyframed animation. A smart object’s ability to hold animated layers makes it even easier to create complicated movements, such as the one below. Let’s explore how this is done.</p>

{{< vimeo id="129227107" >}}

A bouncing dot animation created with multiple sets of keyframes.

In the scene below, I have already set up a simple animation of a yellow dot rotating on a blue background.</p>

{{< vimeo id="129227110" >}}

Step 1: A yellow dot rotating on the canvas.

Next, I’ll go to the Layers panel, right-click the “Dot” layer, and select “Convert to Smart Object.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/319dd9a4-9c08-48ce-8736-038ee7badfcc/p2-08-embed-step2-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1083022f-518d-4669-bc20-81d41e89d78d/p2-08-embed-step2-opt-small.jpg" alt="Convert yellow dot layer to a smart object" /></a><figcaption>Step 2: Convert yellow dot layer to a smart object. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/319dd9a4-9c08-48ce-8736-038ee7badfcc/p2-08-embed-step2-opt.jpg">View large version</a>)</figcaption></figure>

Now that this is a new smart object layer, we can add a new set of keyframes to it. In the scene below, I’ve added a set of keyframes to animate the smart object up and down. When the animation is played back, we can see both sets of keyframes at work, creating a bouncing effect.</p>

{{< vimeo id="129227111" >}}

Step 3: New keyframes create a bouncing effect.

Let’s take this a little further. Convert this smart object layer into another smart object. This will give us a brand new smart object to edit. Next, we’ll add a transformation to this smart object. Go to “Edit” → “Free Transform,” and adjust the handles so that the smart object appears in perspective.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6325d714-c920-42b7-9f02-596b98c9f375/p2-10-embed-step4-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c89f07b8-8801-4ebe-adc2-4893864ab479/p2-10-embed-step4-opt-small.jpg" alt="Transform the animation." /></a><figcaption>Step 4: Transform the animation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6325d714-c920-42b7-9f02-596b98c9f375/p2-10-embed-step4-opt.jpg">View large version</a>)</figcaption></figure>

Now, when you play back the animation, it will animate within the distorted smart object.</p>

{{< vimeo id="129072096" >}}

Animation plays within the transformation.</p>

### Animating Filters

Now that we’ve learned how to embed animations inside smart objects, we can use this same technique to animate filters. If we add a filter to a smart object that contains an animated layer, the result will be an animation that plays through the filter. Let’s see how this works.

In the scene below, I have already set up a simple animation inside of a smart object that shows a dot moving over a red background.</p>

{{< vimeo id="129072097" >}}

Step 1: Smart object animation of a yellow dot moving across a red background.

Because our animation already resides in a smart object, I can add a filter directly to it. In this case, I’ll go to “Filter” → “Distort” → “Twirl.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8a9323c-bf0a-4d49-8810-7b43b91e6af4/p2-13-filter-step2-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc18cdb2-fd51-47df-8aa6-ab57105eaf70/p2-13-filter-step2-opt-small.jpg" alt="Applying the Twirl filter to the smart object animation" /></a><figcaption>Step 2: Applying the Twirl filter to the smart object animation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8a9323c-bf0a-4d49-8810-7b43b91e6af4/p2-13-filter-step2-opt.jpg">View large version</a>)</figcaption></figure>

When I preview the animation, I see some interesting things happening. The filter has been applied to the smart object itself, rather than pixels of its contents. Therefore, the movement of the animated pixels through the filter has a unique effect.</p>

{{< vimeo id="129072098" >}}

Animation of the Twirl filter.</p>

### Adding Layer Styles to Smart Object Animations

Layer styles can be applied to animated layers much like regular layers. They are also useful in other ways. I’ll show you what I mean.

In the scene below, I already have a smart object that contains a simple animation of a dot moving across a white background.</p>

{{< vimeo id="130180326" >}}

Step 1: Simple smart object animation.

My goal is to apply the Bevel &amp; Emboss layer syle to the dot. However, If I try to apply the layer style to the smart object at this point, it would affect the entire smart object, white background and all.</p>

{{< vimeo id="130180325" >}}

Step 2: Layer styles are applied to the image as a whole.

To fix this, I need to remove the white background. Earlier, I mentioned that we could edit the smart object to hide extra layers. In this example, I want to demonstrate another method.

As long as there is good tonal contrast between the layers, we can use the Blend If options in the Layer Styles panel to remove the background. Double-click the smart object layer to open the Layer Styles panel, and adjust the “Blend If” → “This Layer” slider until the background disappears.

Tip: Holding down <code>Option</code> will separate the sliders, causing a smoother transition.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd02df8e-e056-4680-b251-56a2db126df6/p2-17-layer-styles-step3-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c92ff646-ec23-4e75-ad9c-bf8a12521713/p2-17-layer-styles-step3-opt-small.jpg" alt="Adjust the Blend If sliders." /></a><figcaption>Step 3: Adjust the “Blend If” sliders. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd02df8e-e056-4680-b251-56a2db126df6/p2-17-layer-styles-step3-opt.jpg">View large version</a>)</figcaption></figure>

To finish this method, right-click the layer in the Layers panel and select “Convert to Smart Object.” This will create a new smart object that preserves the changes we’ve just made.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66fe9fd2-5de8-4c35-95ca-3e203f303a8f/p2-18-layer-styles-step4-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c4d197f-8bd1-4d56-8910-11df93185d95/p2-18-layer-styles-step4-opt-small.jpg" alt="Convert to a smart object." /></a><figcaption>Step 4: Convert to a smart object. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66fe9fd2-5de8-4c35-95ca-3e203f303a8f/p2-18-layer-styles-step4-opt.jpg">View large version</a>)</figcaption></figure>

Now, when we add a set of layer styles to our animation, the effect will be applied only to the object.</p>

{{< vimeo id="130180324" >}}

Layer styles have been added to the smart object animation.</p>

### Changing an Animation With Adjustment Layers

Adjustment layers act the same way with animated layers as they do with regular layers. As long as an adjustment layer is above the layer that contains the animated keyframes, the animation will inherit the adjustments. With this in mind, we can use adjustment layers to create some truly unique effects. Let’s explore this.

In the scene below, I have set up a simple grayscsale animation with two dots, one passing over the other.</p>

{{< vimeo id="130180320" >}}

Step 1: Grayscale animation of two dots.

Because the entire scene has been created in shades of gray, I will use the Gradient Map Adjustment layer to introduce color. Once I’ve added the adjustment layer, I can use the Properties panel to make the following adjustments.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8302ad6-88f5-4c22-ab9f-7ed83ba669e4/p2-21-adjust-step2-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5755d7ae-f0df-49c5-be59-8b9864e3311b/p2-21-adjust-step2-opt-small.jpg" alt="Settings for the Gradient Map Adjustment layer" /></a><figcaption>Step 2: Settings for the Gradient Map Adjustment layer (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8302ad6-88f5-4c22-ab9f-7ed83ba669e4/p2-21-adjust-step2-opt.jpg">View large version</a>)</figcaption></figure>

The resulting effect is an animation that has been colored based on the properties of the adjustment layer.</p>

{{< vimeo id="129675703" >}}

Animation has been colored by the adjustment layer.</p>

### Creating Organic Effects With Adjustment Layers

Now that we’ve learned several techniques to create animations, I want to combine a few of these to create the organic effect seen below.</p>

{{< vimeo id="129878087" >}}

Organic animation effect.

Let’s learn how this is done. To start, I’ve created another simple animation with two layers, one passing over the other. The only difference is that both layers have been blurred.</p>

{{< vimeo id="129878088" >}}

Step 1: Blurry dot animated over another.

Now, we’ll add the Levels Adjustment layer. Use the Properties panel to bring in the shadows and highlights sliders until the edges of the objects are crisp.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90d23f46-aa62-42bd-b88f-986d7fe48bad/p2-25-organic-step2-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8669057b-05a8-4db3-bd16-6655a1f609e3/p2-25-organic-step2-opt-small.jpg" alt="Edits to the Levels Adjustment layer" /></a><figcaption>Step 2: Edits to the Levels Adjustment layer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8302ad6-88f5-4c22-ab9f-7ed83ba669e4/p2-21-adjust-step2-opt.jpg">View large version</a>)</figcaption></figure>

Playing back the animation will give us a unique organic effect.</p>

{{< vimeo id="129878087" >}}

Organic animation effect.</p>

## Putting Everything Together

Now that we’ve learned the concepts behind more complex animations, it’s time to put them into practice. In this next section, we’ll explore three advanced animations and how to create them.</p>

### Create a Clock With Moving Hands

In this tutorial, we will be using the template layer technique to animate the spinning hands of the clock. We will also use layer styles with the animated elements to add depth to the objects in our scene. This is what we’ll be creating:

{{< vimeo id="129072095" >}}

Animation of the hands of a clock.

The scene starts with two new layers: One contains the shape of a minute hand (in red), and the other is our template object (in gray).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c5d6fe6-a0ec-4292-9600-977523ff0ae9/p3-02-clock-step1-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03ed84c1-ea6e-4e61-9e84-c47459c9ec07/p3-02-clock-step1-opt-small.jpg" alt="Two new layers: the minute hand and a template layer" /></a><figcaption>Step 1: Two new layers: the minute hand and a template layer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c5d6fe6-a0ec-4292-9600-977523ff0ae9/p3-02-clock-step1-opt.jpg">View large version</a>)</figcaption></figure>

Just as we learned earlier, we will convert these two layers into a smart object and animate the rotation.</p>

{{< vimeo id="128879461" >}}

Step 2: Layers combined as a smart object are animated as one.

To lock the animation, convert the layers into another smart object. This will allow us to transfrom (<code>Control + T</code>) the smart object so that it appears to be in perspective, as seen in the image below.</p>

{{< vimeo id="128879463" >}}

Step 3: Animation is transformed into perspective.

Next, we need to go back into the original smart object and hide the template layer. When we save and return to our working document, we should see our minute hand rotate without the template layer.</p>

{{< vimeo id="128879464" >}}

Step 4: Animation with template layer hidden.

Adding the Drop Shadow layer style with a “Spread” setting of 100% will simulate some depth.</p>

{{< vimeo id="128879468" >}}

Step 5: Drop Shadow simulates the edges of the clock hand.

Repeating these steps, we can create the hour hand. (I’ve readjusted the timing to fit in the animation of the hour hand.)

{{< vimeo id="128879470" >}}

Step 6: Hour and minute hand animating.

Lastly, we can create the rest of the clock using traditional Photoshop techniques. The result is a clock that animates in perspective.</p>

{{< vimeo id="129072095" >}}

Animation of the hands of a clock.

In this tutorial, we’ve learned how to use template layers to create more complicated movements. We’ve also learned how to use transformations and layer styles to create the illusion of perspective in our animation.</p>

### Create a Revolving Globe

In this tutorial, we will apply filters to animated smart objects in order to create a new effect. This is what we’ll be creating:

{{< vimeo id="128879314" >}}

Animation of a revolving globe.

Below is the base image we’ll be using. Notice that it repeats itself. This is important because it will help us to create a looping animation in the next step.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1de330c-ade3-4cf6-853b-07fe86bb2d5d/p3-09-world-step1-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f25541e-2d72-4d04-9422-296511ee716e/p3-09-world-step1-opt-small.jpg" alt="Image of the repeating graphic that will be animated." /></a><figcaption>Step 1: Image of the repeating graphic that will be animated. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1de330c-ade3-4cf6-853b-07fe86bb2d5d/p3-09-world-step1-opt.jpg">View large version</a>)</figcaption></figure>

I’ve created a new square document and added the graphic of the world map as a new layer. I’ve gone ahead and animated the Position property so that the world map scrolls across the scene. It’s been timed to loop when it starts over.</p>

{{< vimeo id="128879317" >}}

Step 2: Simple looping animation.

Next, convert this layer into a smart object.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a56efdc-7e27-4983-80a5-b697b8da56cd/p3-11-world-step3-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87dda021-55b3-45c8-a6d2-7ab2e0d51c9c/p3-11-world-step3-opt-small.jpg" alt="Convert simple animation into a smart object" /></a><figcaption>Step 3: Convert simple animation into a smart object. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a56efdc-7e27-4983-80a5-b697b8da56cd/p3-11-world-step3-opt.jpg">View large version</a>)</figcaption></figure>

Before we do anything else, I want to show you what’s going on with the layer. If I go to “View” → “Show” → “Layers Edges,” we can see the bounding box of the layer as it animates. This will be important when we add filters. Also, notice that our animation loop seamlessly.</p>

{{< vimeo id="130855634" >}}

Step 4: Layer boundaries visible during animation.

At this point, our scene is still not ready for us to add a filter. But let’s take a moment to explore why — we’ll add the Spherize filter to see what happens. When the filter is added, we can see that it’s not being applied within the confines of our canvas; rather, it’s being applied directly to the whole layer. The result is a distorted map that moves through the canvas. Also, notice how this disrupts the looping that we saw in the previous step. This is not the effect we are after.</p>

{{< vimeo id="128879321" >}}

Step 5: Filter applied to the layer boundaries.

We now know that we have a little more work to do in order for the filter to be applied correctly. To make sure that the filter applies only to the boundaries of the canvas, we need to create a layer mask. First, go to “Select” → “All” to select the entire canvas. Next, click the “Add Layer Mask” icon in the Layers panel. We should now have a layer mask applied to our layer.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba5616f7-5dc8-4213-93c9-3006a22fe41f/p3-14-world-step6-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8828af47-c29a-4f35-bf5c-e328dc5f8f8d/p3-14-world-step6-opt-small.jpg" alt="New layer mask added" /></a><figcaption>Step 6: New layer mask added. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba5616f7-5dc8-4213-93c9-3006a22fe41f/p3-14-world-step6-opt.jpg">View large version</a>)</figcaption></figure>

Convert this layer to a new smart object. Our resulting smart object layer will now animate within the boundaries of the canvas. If we add the Spherize filter again, we can see that it’s being applied correctly when we play the animation. Go ahead and add the Spherize filter a second time to increase its effect.</p>

{{< vimeo id="128879322" >}}

Step 7: Filter applied to the boundaries of the canvas.

Now that our effect is working properly, we can create another layer mask in the shape of a circle to hide unwanted pixels.</p>

{{< vimeo id="128733032" >}}

Step 8: Layer Mask hides everything outside of the globe shape.

To finish, you can now add layer styles directly to the smart object animation for embellishments.</p>

{{< vimeo id="128879314" >}}

Animation of a revolving globe.

In this tutorial, we’ve learned how to use smart objects to contain animated layers, to which we then add effects, such as filters, layer masks and layer styles. Hopefully, this tutorial has shown you how easy it is to create complicated effects using animated layers in Photoshop.</p>

### Create a Flame Animation

In this tutorial, we’ll use multiple adjustment Layers and filters, with smart object animations, to create a truly unique flame effect. This is what our final animation will look like.</p>

{{< vimeo id="130855635" >}}

Flame animation using the organic technique.

To begin, we’ll need to create an extremely tall scene. In this case, I have a scene that’s approximately 500 × 10,000 pixels. On a new layer, I’ve drawn a very rough line using the Brush tool.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aea787a-9ca2-486c-b697-427a765fde37/p3-18-fire-step1-opt.jpg" alt="A tall white line with soft edges" /><br>
<figcaption>Step 1: A tall white line with soft edges</figcaption></figure>

Next, create a new scene sized to 500 × 500 pixels, with a black background. Bring the tall line that we just created into this new scene, and create a simple scrolling animation.</p>

{{< vimeo id="128733034" >}}

Step 2: Simple animation of scrolling line.

Add a new layer mask in the shape of an upside-down teardrop to the animated layer. Make sure that the mask has soft edges. The result will reveal a portion of the line as it animates through the mask.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7358f444-e00a-479f-ba5c-05639cc87b4d/p3-20-fire-step3-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27622fe5-db13-4b96-b57c-38ac505cf40d/p3-20-fire-step3-opt-small.jpg" alt="Dotted line represents the shape of the layer mask" /></a><figcaption>Step 3: Dotted line represents the shape of the layer mask. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7358f444-e00a-479f-ba5c-05639cc87b4d/p3-20-fire-step3-opt.jpg">View large version</a>)</figcaption></figure>

Play back the animation to see the flame take shape. Notice how the shape of our mask is causing the top of the animation to jump around while the base generally stays in the same spot.</p>

{{< vimeo id="128732971" >}}

Step 4: Simple animation with a layer mask.

Next, add the Levels Adjustment layer. In the Properties panel, move the two outside sliders inward until the edges of the flame are crisp. Playing back the animation will show us a smoother flame.</p>

{{< vimeo id="128732973" >}}

Step 5: Adjustment layer refines the shape.

At this point, we can further smooth out the flame. First, convert all layers to another smart object. Then, blur the layer, followed by a repeat of the Levels Adjustment layer.</p>

{{< vimeo id="128732975" >}}

Step 6: Blurring the smart object and then repeating the Levels Adjustment layer creates a more fluid looking movement.

There are several ways to introduce color. I want to show one way that has worked well for me. Create a new layer, and use the Brush tool to paint blue (on the base) and yellow (towards the top) highlights on the flame. Changing this layer’s blending mode to “Hard Mix” will give us some vibrant bands of color.</p>

{{< vimeo id="128732976" >}}

Step 7: Using blend modes to add color.

Because the transitions between colors are too harsh, we’ll need to soften them. To do this, select all layers again (<code>Alt + Control + A</code>) and convert to another smart object. We can now add the Motion Blur filter to blend the colors better.</p>

{{< vimeo id="128732977" >}}

Step 8: Adding Motion Blur blends the colors.

Almost done! Because this object is a smart object, we can treat it like a normal layer and use simple photo composition techniques to add it to another photo. The final image shows our flame dancing on a lighter.</p>

{{< vimeo id="130855635" >}}

Flame animation using the organic technique.

In this tutorial, we’ve learned how to make use of multiple adjustment layers and smart filters by layering smart objects within smart objects to create and refine an organic effect inside Photoshop.</p>

## Photoshop Animation Conclusion

By now, you should be familiar with all of the common layer types and how each of their properties can be animated. Also, we now know that <strong>Photoshop is well equipped to produce some amazing animations</strong>. We’ve explored how to use smart objects to extend the animation capabilities by acting as templates or enabling us to stack multiple animations. We’ve also seen how to enhance our animations with filters and layer styles. We’ve even learned how to create some new — and seemingly impossible effects (for Photoshop) — by leveraging the Levels Adjustment layer. Lastly, we’ve put everything together to create some polished animations.

The techniques presented in this article demonstrate how Photoshop can be a reliable tool for creating animations. There will always be applications out there that are dedicated to creating animation. However, owning — or even learning — other software isn’t always feasible. Instead, you can <strong>stay within a program you are comfortable with</strong> and still create effects that were once deemed impossible in Photoshop.</p>

### Additional Reading

*   [Texture Trickster](https://blog.stephenpetrany.com/category/animation/), Stephen Petrany Additional animation tutorials and tricks on my blog
*   [Animation in Adobe Photoshop](https://design.tutsplus.com/series/animation-in-adobe-photoshop--cms-753), Tuts+ A tutorial series on animation

{{< signature "ml, al" >}}

