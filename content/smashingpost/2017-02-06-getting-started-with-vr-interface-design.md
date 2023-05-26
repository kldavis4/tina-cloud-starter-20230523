---
title: Getting Started With VR Interface Design
slug: getting-started-with-vr-interface-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3675371c-502e-40d3-bf09-e42dded374bc/16-cross-graph-preview-opt.png
date: 2017-02-06T23:25:11.000Z
author: samapplebee
description: >-
  The virtual realm is uncharted territory for many designers. In the last few
  years, we've witnessed **an explosion in virtual reality** (VR) hardware and
  applications. VR experiences range from the mundane to the wondrous, their
  complexity and utility varying greatly.
categories:
  - UX
  - User Interaction
  - UX
  - UI
  - Virtual Reality
---
Taking your first steps into VR as a UX or UI designer can be daunting. We know because we've been there. But fear not! In this article, we'll share a process for designing VR apps that we hope you'll use to start designing for VR yourself. You don't need to be an expert in VR; you just need to be willing to apply your skills to a new domain. Ultimately, as a community working together, we can accelerate VR to reach its full potential faster.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Developing For Virtual Reality: What We Learned](https://www.smashingmagazine.com/2016/09/developing-for-virtual-reality-what-we-learned/)
*   [Gamification And UX: Where Users Win Or Lose](https://www.smashingmagazine.com/2012/04/gamification-ux-users-win-lose/)
*   [True Lies Of Optimistic User Interfaces](https://www.smashingmagazine.com/2016/11/true-lies-of-optimistic-user-interfaces/)
*   [Designing Card-Based User Interfaces](https://www.smashingmagazine.com/2016/10/designing-card-based-user-interfaces/)

## What Kinds Of VR Apps Are There?

Generally speaking from a designer's perspective, VR applications are made up of two types of components: environments and interfaces.

{{% feature-panel %}}

You can think of an environment as the world that you enter when you put on a VR headset — the virtual planet you find yourself on, or the view from the <a href="https://www.youtube.com/watch?v=l3V8zeSljUU">rollercoaster</a> that you're riding.

An interface is the set of elements that users interact with to navigate an environment and control their experience. All VR apps can be positioned along two axes according to the complexity of these two components.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d602c9dc-237e-4fb1-bb7c-1a221804eb4b/16-cross-graph-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3675371c-502e-40d3-bf09-e42dded374bc/16-cross-graph-preview-opt.png" alt="" width="780" height="585" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d602c9dc-237e-4fb1-bb7c-1a221804eb4b/16-cross-graph-large-opt.png">View large version</a>)</figcaption></figure>

In the top-left quadrant are things like simulators, such as the rollercoaster experience linked to above. These have a fully formed environment but no interface at all. You're simply locked in for the ride.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b473a6f1-f551-47e3-97a5-26ef44b2cedf/18-samsung-store-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1ad8763-ddde-4657-8e8b-dd6d97781cc2/18-samsung-store-preview-opt.jpg" alt="" width="780" height="368" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b473a6f1-f551-47e3-97a5-26ef44b2cedf/18-samsung-store-large-opt.jpg">View large version</a>)</figcaption></figure>

In the opposite quadrant are apps that have a developed interface but little or no environment. Samsung's Gear VR home screen is a good example.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eadd7b67-67c7-44fd-b620-37132c98bdd4/17-oculus-store-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2abf692e-9389-44c0-9a9b-e21f23b2a5ca/17-oculus-store-preview-opt.jpg" alt="" width="780" height="417" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eadd7b67-67c7-44fd-b620-37132c98bdd4/17-oculus-store-large-opt.jpg">View large version</a>)</figcaption></figure>

Designing virtual environments such as places and landscapes requires proficiency with 3D modelling tools, putting these elements out of reach for many designers. However, there's a huge opportunity for UX and UI designers to apply their skills to designing user interfaces for virtual reality (or VR UIs, for short).

The first full VR UI design we did was an app for The Economist, created in collaboration with VR production studio <a href="https://visualise.com/">Visualise</a>. We did the design, while Visualise created the content and developed the app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1675021-5359-426d-9b00-85700bef7910/vr-working-example-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35158709-0e11-4443-9f68-dcc6374fa697/vr-working-example-780w-opt.png" width="780" height="603" alt="VR working example" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1675021-5359-426d-9b00-85700bef7910/vr-working-example-large-opt.png">Large preview</a>)</figcaption></figure>

We'll use this as a working example throughout the next section, in which we'll lay out an approach to designing VR apps, before getting into the nitty-gritty of designing interfaces for VR. You can download the <a href="https://www.oculus.com/experiences/gear-vr/1020752464669083/">Economist app for Gear VR</a> from the Oculus website.</p>

## A Process For VR UI Design

Whereas most designers have figured out their workflow for designing mobile apps, processes for designing VR interfaces are yet to be defined. When the first VR app design project came through our door, the logical first step was for us to devise a process.</p>

### Traditional Workflows, New Territory

When we first played with Gear VR by Samsung, we noticed similarities to traditional mobile apps. Interface-based VR apps work according to the same basic dynamic as traditional apps: Users interact with an interface that helps them navigate pages. We're simplifying here, but just keep this in mind for now.

Given the similarity to traditional apps, the tried-and-tested mobile app workflows that designers have spent years refining won't go to waste and can be used to craft VR UIs. You're closer to designing VR apps than you think!

Before describing how to design VR interfaces, let's step back and run through the process for designing a traditional mobile app.</p>

### 1. Wireframes

First, we'll go through rapid iterations, defining the interactions and general layout.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d619b87-0bba-48ec-8291-60ef196c9255/1-wireframes-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c718cd-85d0-43e8-8cc0-b624603900c3/1-wireframes-preview-opt.jpg" alt="" width="780" height="585" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d619b87-0bba-48ec-8291-60ef196c9255/1-wireframes-large-opt.jpg">View large version</a>)</figcaption></figure>

### 2. Visual Design

At this stage, the features and interactions have been approved. Brand guidelines are now applied to the wireframes, and a beautiful interface is crafted.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bf70a46-a1a1-42e5-99b4-281542367415/2-visual-design-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb3d9bed-7cd5-4631-9145-4db87a234d27/2-visual-design-preview-opt.jpg" alt="" width="780" height="585" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bf70a46-a1a1-42e5-99b4-281542367415/2-visual-design-large-opt.jpg">View large version</a>)</figcaption></figure>

### 3. Blueprint

Here, we'll organize screens into flows, drawing links between screens and describing the interactions for each screen. We call this the app's blueprint, and it will be used as the main reference for developers working on the project.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b4207b9-4aeb-43a6-bac0-349e1f573081/3-blueprint-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17bec366-7dc7-495c-aea2-f378b88e38ce/3-blueprint-preview-opt.jpg" alt="" width="780" height="585" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b4207b9-4aeb-43a6-bac0-349e1f573081/3-blueprint-large-opt.jpg">View large version</a>)</figcaption></figure>

Now, how can we apply this workflow to virtual reality?

## Set Up

### Canvas Size

The simplest problems can be the most challenging. Faced with a 360-degree canvas, one might find it difficult to know where to begin. It turns out that UX and UI designers only need to focus on a certain portion of the total space.

We spent weeks trying to figure out what canvas size would make sense for VR. When you work on a mobile app, the canvas size is determined by the device's size: 1334 × 750 pixels for the iPhone 6 and roughly 1280 × 720 pixels for Android.

To apply this mobile app workflow to VR UIs, you first have to figure out a canvas size that makes sense.

Below is what a 360-degree environment looks like when flattened. This representation is called an equirectangular projection. In a 3D virtual environment, these projections are wrapped around a sphere to mimic the real world.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae8c6c86-8f9e-491a-8eeb-bdfd6a88cd6b/4-equirectangular-image-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46c18e38-dd18-4bb6-ab34-7474a89f3089/4-equirectangular-image-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae8c6c86-8f9e-491a-8eeb-bdfd6a88cd6b/4-equirectangular-image-large-opt.jpg">View large version</a>)</figcaption></figure>

The full width of the projection represents 360 degrees horizontally and 180 degrees vertically. We can use this to define the pixel size of the canvas: 3600 × 1800.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95c2e1e0-86d9-4931-95a9-1fdbe9af2bcc/5-equirectangular-image-dimensions-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bd08daa-4ba8-4b83-9871-a5f457164281/5-equirectangular-image-dimensions-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95c2e1e0-86d9-4931-95a9-1fdbe9af2bcc/5-equirectangular-image-dimensions-large-opt.jpg">View large version</a>)</figcaption></figure>

Working with such a big size can be a challenge. But because we're primarily interested in the interface aspect of VR apps, we can concentrate on a segment of this canvas.

Building on <a href="https://www.youtube.com/watch?v=iR4iRyLoJlg">Mike Alger's early research</a> on comfortable viewing areas, we can isolate a portion where it makes sense to present the interface.

The area of interest represents one ninth of the 360-degree environment. It's positioned right at the centre of the equirectangular image and is 1200 × 600 pixels in size.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96eac460-3b5d-434b-af94-98891114c962/7-dual-canvas2-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86faaf1d-73da-4b1f-89c0-e7b4cb2ae0e6/7-dual-canvas2-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96eac460-3b5d-434b-af94-98891114c962/7-dual-canvas2-large-opt.jpg">View large version</a>)</figcaption></figure>

Let's sum up:

*   "**360 View**": 3600 × 1800 pixels
*   "**UI View**": 1200 × 600 pixels

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25f0081d-9da3-49d5-b6df-d413cb0bf35f/6-dual-canvas-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c7af5b3-af09-4363-a253-38ff7f45cb14/6-dual-canvas-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25f0081d-9da3-49d5-b6df-d413cb0bf35f/6-dual-canvas-large-opt.jpg">View large version</a>)</figcaption></figure>

### Testing

The reason for using two canvases for a single screen is testing. The "UI View" canvas helps to keep our focus on the interface we're crafting and makes it easier to design flows.

Meanwhile, the "360 View" is used to preview the interface in a VR environment. To get a real sense of proportions, testing the interface with a VR headset is necessary.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34e8abc5-7d4b-45f4-bd95-bb525c8afb49/using-avocode.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34e8abc5-7d4b-45f4-bd95-bb525c8afb49/using-avocode.gif" width="800" height="600" alt="Using Avocode" /></a><figcaption>Using Avocode, you can visually compare revisions of designs easily.</figure>

### Tools

Before we get started with the walkthrough, here are the tools we'll need:

*   [Sketch](https://www.sketchapp.com/) We'll use Sketch to design our interfaces and user flows. If you don't have it, you can download a trial version. Sketch is our preferred interface design software, but if you're more comfortable using Photoshop or anything else, that would work, too.
*   [GoPro VR Player](https://www.kolor.com/kolor-eyes/) GoPro VR Player is a 360-degree content viewer. It's provided by GoPro and is free. We'll use it to preview our designs and test them in context.
*   [Oculus Rift](https://www3.oculus.com/en-us/rift/) Hooking Oculus Rift into the GoPro VR Player will enable us to test the design in context.</p>

## A Process For VR Interface Design

In this section, we'll run through a short tutorial on how to design a VR interface. We'll design a simple one together, which should take five minutes tops.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b452ddaf-7645-4cba-84e3-c920016df9da/vr-result-preview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b452ddaf-7645-4cba-84e3-c920016df9da/vr-result-preview.gif" width="750" height="422" alt="result preview" /></a></figure>

Download the <a href="https://www.dropbox.com/s/i73fot0fevv436c/Kickpush_VRDemo_Assets.zip?dl=0">assets pack</a>, which contains presized UI elements and the background image. If you want to use your own assets, go for it; it won't be a problem.</p>

### 1. Set Up "360 View"

First things first. Let's create the canvas that will represent the 360-degree view. Open a new document in Sketch, and create an artboard: 3600 × 1800 pixels.

Import the file named <code>background.jpg</code>, and place it in the middle of the canvas. If you're using your own equirectangular background, make sure its proportions are 2:1, and resize it to 3600 × 1800 pixels.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a397fca-1eb1-44f4-8128-694a182f3588/9-create360-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93a97a1a-ce9c-4ccf-a09f-1eb40931fc63/9-create360-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a397fca-1eb1-44f4-8128-694a182f3588/9-create360-large-opt.jpg">View large version</a>)</figcaption></figure>

### 2. Set Up Artboard

As mentioned above, the "UI View" is a cropped version of the "360 View" and focuses on the VR interface only.

Create a new artboard next to the previous one: 1200 × 600 pixels. Then, copy the background that we just added to our "360 View," and place it in the middle of our new artboard. Don't resize it! We want to keep a cropped version of the background here.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49a1ec77-f6e6-42e4-87bf-67ae7897ab2e/10-create-ui-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6ca1ba2-ac11-4d86-911f-675ea4c04fb5/10-create-ui-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49a1ec77-f6e6-42e4-87bf-67ae7897ab2e/10-create-ui-large-opt.jpg">View large version</a>)</figcaption></figure>

### 3. Design the Interface

We're going to design our interface on the "UI View" canvas. We'll keep things simple for the sake of this exercise and add a row of tiles. If you're feeling lazy, just grab the file named <code>tile.png</code> in the assets pack and drag it into the middle of the UI view.

Duplicate it, and create a row of three tiles.

Grab <code>kickpush-logo.png</code> from the assets pack, and place it above the tiles.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab7e789d-8dcc-4447-98e5-006f612d9931/11-design-interface-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef6c2e45-591a-43e0-a328-9bd26bffabce/11-design-interface-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab7e789d-8dcc-4447-98e5-006f612d9931/11-design-interface-large-opt.jpg">View large version</a>)</figcaption></figure>

Looking pretty good, eh?

### 4. Merge Artboards and Export

Now for the fun stuff. Make sure the "UI View" artboard is above the "360 View" artboard in the layers list on the left.

Drag the "UI View" artboard to the middle of the "360 View" artboard. Export the "360 View" artboard as a PNG; the "UI View" will be on top of it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13f0d552-bc1a-48bb-a9b8-0803841bdf05/12-drag-ui-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0926dbef-91c7-46ac-bf9c-7514ed22c7e0/12-drag-ui-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13f0d552-bc1a-48bb-a9b8-0803841bdf05/12-drag-ui-large-opt.jpg">View large version</a>)</figcaption></figure>

### 5. Test It in VR

Open the GoPro VR Player and drag the "360 View" PNG that you just exported into the window. Drag the image with your mouse to preview your 360-degree environment.

We're done! Pretty simple when you know how, right?

If you have an Oculus Rift set up on your machine, then the GoPro VR Player should detect it and allow you to preview the image using your VR device. Depending on your configuration, you might have to mess around with the display settings in MacOS.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1f12f1-44a8-410c-9b94-34935e1f6b27/13-oculus-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ae6387-a1e3-4c5a-8268-a0c7bbfa43af/13-oculus-preview-opt.jpg" alt="" width="780" height="390" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1f12f1-44a8-410c-9b94-34935e1f6b27/13-oculus-large-opt.jpg">View large version</a>)</figcaption></figure>

## Technical Considerations

### Low Resolution

The resolution of the VR headset is pretty bad. Well, that's not entirely true: It's equivalent to your phone's resolution. However, considering the device is 5 centimeters from your eyes, the display doesn't look crisp.

To get a crisp VR experience, we would need an 8K display per eye. That's a 15,360 × 7680-pixel display. We're pretty far off from that, but we'll get there eventually.</p>

### Text Readability

Because of the display's resolution, all of your beautifully crisp UI elements will look pixelated. This means, first, that text will be difficult to read and, secondly, that there will be a high level of aliasing on straight lines. Try to avoid using big text blocks and highly detailed UI elements.</p>

## Finishing Touches

### Blueprint

Remember the blueprint from our mobile app design process? We've adapted this practice to VR interfaces. Using our UI views, we map and organize our flows into a comprehensible blueprint, ideal for developers to understand the overall architecture of the app we've designed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8324564c-5c91-4657-bfc3-ef2ab1522408/14-vr-blueprint-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7285062d-f96c-4820-a5dc-4844e575b242/14-vr-blueprint-preview-opt.jpg" alt="" width="780" height="863" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8324564c-5c91-4657-bfc3-ef2ab1522408/14-vr-blueprint-large-opt.jpg">View large version</a>)</figcaption></figure>

### Motion Design

Designing a beautiful UI is one thing, but showing how it's supposed to animate is a different story. Once again, we've decided to approach it with a two-dimensional perspective.

Using our Sketch designs, we animate the interface with <a href="https://www.adobe.com/ca/products/aftereffects.html">Adobe After Effects</a> and <a href="https://principleformac.com">Principle</a>. While the outcome is not a 3D experience, it's used as a guideline for the development team and to help our clients understand our vision at an early stage of the process.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f154974-4b68-4c6a-98f4-9cbe0a2caca4/first-vr-ui.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f154974-4b68-4c6a-98f4-9cbe0a2caca4/first-vr-ui.gif" width="800" alt="your first VR UI" /></a><figcaption>You've just designed your first VR UI. Check you out! Booty shake.</figcaption></figure>

We know what you're thinking, though: "That's cool, but VR apps can get <em>way</em> more complicated." Yes, they can. The question is, to what extent can we apply our current UX and UI practices to this new medium?

## How Far Can VR UIs Go?

### Inter-Your-Faces

Some VR experiences rely so heavily on the virtual environment that a traditional interface that sits on top might not be the optimal way for the user to control the app. In this case, you might want users to interact directly with the environment itself.

Imagine that you're making an app for a luxury travel agent. You'd want to transport the user to potential holiday destinations in the most vivid way possible. So, you invite the user to put on the headset and begin the experience in your swanky Chelsea office.

To transition from the office to some far away place, the user needs to choose where they want to go. They could pick up a travel magazine and flick through it until they land on an appealing page. Or there could be a collection of interesting objects on your desk that whisk the user to different locations depending on which one they pick up.

This is definitely cool, but there are some drawbacks. To get the full effect, you'd need a more advanced VR headset with handheld controllers. Plus, an app like this takes quite a bit more effort to develop than a set of well-presented options organized like in a traditional app interface.</p>

### Viva la Revolución!

The reality is that these immersive experiences are not commercially viable for most companies. Unless you've got virtually unlimited resources, like Valve and Google, creating an experience like the one described above is probably too costly, too risky and too time-consuming.

This kind of experience is brilliant for showing off that you're at the cutting edge of media and technology, but not so great for taking your product to market through a new medium. Accessibility is important.

Usually, when a new format emerges, it's pushed to the limit by early adopters: the creators and innovators of this world. In time, and with enough learning and investment, it becomes accessible to a wider range of potential users.

As VR headsets become more commonplace, companies will start to spot opportunities to integrate VR into the ways that they engage with customers.

From our perspective, VR apps with intuitive UIs — that is, UIs closer to what people are already accustomed to with their wearables, phones, tablets and computers — are what will make VR an affordable and worthwhile investment for the majority of companies that pursue it.</p>

### Time to Board the Rocketship

We hope we've made the VR space a bit less scary with this article and inspired you to start designing for VR yourself.

They say that if you want to travel fast, go alone. But if you want to travel far, travel together. We want to travel far. At Kickpush, we think that every company will have a VR app someday, just like every company now has a mobile website (or should have — it's 2017, dang it!).

So, we're building a rocketship, a joint effort by designers around the globe to boldly go where no designer has gone before. The sooner that producing VR apps make sense for companies, the sooner the whole ecosystem will blow up.

Our next challenges as digital product designers are more complex applications and handling other types of input through controllers. To begin to tackle this we'll need robust prototyping tools that let us create and test designs quickly and easily. We'll be writing a follow up article that looks at some of the early attempts to do this, and at some of the new tools in development.

Stay tuned!

### Useful Links

*   [The UX of VR](https://www.uxofvr.com/), Max Glenister "A curated list of resources to help you on your journey into the user experience of virtual reality."
*   [Mike Alger](https://www.youtube.com/channel/UCdnvAn8YIcUs0XfUNiHKz0A) (research vlog), YouTube channel
*   [AR & VR Weekly](https://tinyletter.com/vrweekly) (newsletter), Josh Anon "A curated list of AR/VR/MR news and interesting pieces sent about once a week."
*   [Kickpush blog](https://blog.kickpush.co)
*   "[Virtual Reality Glossary](https://www.freeflyvr.com/virtual-reality-glossary/)," Freefly VR

{{< signature "km, il, al" >}}

