---
title: 'How To Build A Real-Time Multiplayer Virtual Reality Game (Part 1)'
slug: real-time-multiplayer-virtual-reality-game-part-1
author: alvin-wan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e75ff479-845d-4743-927e-b7fc24804e3a/real-time-multiplayer-vr-game.png
date: 2019-08-20T15:30:59+02:00
summary: >-
  Virtual reality is a new immersive medium for exploring content, whether that content is a film (*Life of Pi*), a game (*Beat Saber*) or a social experience (as depicted in *Ready Player One*). Despite its novelty, VR doesn’t require a drastically different toolset to design for &mdash; the same tools we use for web game development, 3D modeling, and others are all still applicable. This tutorial leverages your familiarity with web development to get started with VR development.
description: >-
  In this first part of the series, you will learn how to create a virtual reality scene with interactive game elements. These game elements can later be used for a fully-fledged, multiplayer VR game.
categories:
  - Virtual Reality
  - Augmented Reality
  - User Interaction
  - UI
  - JavaScript
---
In this tutorial series, we will build a web-based multiplayer [virtual reality](https://www.smashingmagazine.com/category/virtual-reality) game in which players will need to collaborate to solve a puzzle. We will use [A-Frame](https://aframe.io/) for VR modeling, [MirrorVR](https://github.com/alvinwan/mirrorvr) for cross-device real-time synchronization, and [A-Frame Low Poly](https://github.com/alvinwan/aframe-low-poly) for low-poly aesthetics. At the end of this tutorial, you will have a fully functioning demo online that anyone can play.

Each pair of players is given a ring of orbs. The goal is to "turn on" all orbs, where an orb is "on" if it's elevated and bright. An orb is "off" if it's lower and dim. However, certain "dominant" orbs affect their neighbors: if it switches state, its neighbors also switch state. Only player 2 can control the dominant orbs while only player 1 can control non-dominant orbs. This forces both players to collaborate to solve the puzzle. In this first part of the tutorial, we will build the environment and add the design elements for our VR game.

The seven steps in this tutorial are grouped into three sections:

<ol>
  <li><a href="#setting-up-the-scene">Setting Up The Scene</a> (Steps 1&ndash;2)</li>
  <li><a href="#creating-the-orbs">Creating The Orbs</a> (Steps 3&ndash;5)</li>
  <li><a href="#making-the-orbs-interactive">Making The Orbs Interactive</a> (Steps 6&ndash;7)</li>
</ol>

{{% feature-panel %}}

This first part will conclude with a clickable orb that turns on and off (as pictured below). You will use A-Frame VR and several A-Frame extensions.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32da29c3-6033-4ea3-b0c5-ace5df7152fb/1-clickable-orb.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32da29c3-6033-4ea3-b0c5-ace5df7152fb/1-clickable-orb.gif" width="" height="" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32da29c3-6033-4ea3-b0c5-ace5df7152fb/1-clickable-orb.gif">Large preview</a>)</figcaption></figure>

## Setting Up The Scene

### 1. Let’s Go With A Basic Scene

To get started, let’s take a look at how we can set up a simple scene with a ground:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee1d9f5-09f5-4326-8565-9e3441598439/2-simple-scene.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee1d9f5-09f5-4326-8565-9e3441598439/2-simple-scene.png" sizes="100vw" caption="Creating a simple scene (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee1d9f5-09f5-4326-8565-9e3441598439/2-simple-scene.png'>Large preview</a>)" alt="Creating a simple scene" >}}

The first three instructions below are excerpted from my [previous article](https://www.smashingmagazine.com/2019/03/virtual-reality-endless-runner-game-vr-part-1/#step-1-setting-up-a-basic-scene). You will start by setting up a website with a single static HTML page. This allows you to code from your desktop and automatically deploy to the web. The deployed website can then be loaded on your mobile phone and placed inside a VR headset. Alternatively, the deployed website can be loaded by a standalone VR headset.

Get started by navigating to [glitch.com](https://glitch.com). Then, do the following:

1. Click on "New Project" in the top right,
2. Click on "hello-webpage" in the drop-down,
3. Next, click on *index.html* in the left sidebar. We will refer to this as your "editor".

You should now see the following Glitch screen with a default HTML file.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/915368ce-0656-4593-a43e-5d11990470fe/3-glitch-project-index-html-file.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/915368ce-0656-4593-a43e-5d11990470fe/3-glitch-project-index-html-file.png" sizes="100vw" caption="Glitch project: the index.html file (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/915368ce-0656-4593-a43e-5d11990470fe/3-glitch-project-index-html-file.png'>Large preview</a>)" alt="Glitch project: the index.html file" >}}

As with the linked tutorial above, start by deleting all existing code in the current *index.html* file. Then, type in the following for a basic webVR project, using A-Frame VR. This creates an empty scene by using A-Frame’s default lighting and camera.

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Lightful&lt;/title&gt;
    &lt;script src="https://aframe.io/releases/0.8.0/aframe.min.js"&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;a-scene&gt;
    &lt;/a-scene&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

Raise the camera to standing height. Per A-Frame VR recommendations ([Github issue](https://github.com/aframevr/aframe/issues/3351)), wrap the camera with a new entity and move the parent entity instead of the camera directly. Between your `a-scene` tags on lines 8 and 9, add the following.

<pre><code class="language-html">&lt;!-- Camera! --&gt;
&lt;a-entity id="rig" position="0 3 0"&gt;
  &lt;a-camera wasd-controls look-controls&gt;&lt;/a-camera&gt;
&lt;/a-entity&gt;
</code></pre>

Next, add a large box to denote the ground, using `a-box`. Place this directly beneath your camera from the previous instruction.

<div class="break-out">

 <pre><code class="language-html">&lt;!-- Action! --&gt;
&lt;a-box shadow width="75" height="0.1" depth="75" position="0 -1 0" color="#222"&gt;&lt;/a-box&gt;
</code></pre>
</div>

Your *index.html* file should now match the following exactly. You can find the full source code [here, on Github](https://github.com/alvinwan/lightful/tutorial/step01.html).

<div class="break-out">

 <pre><code class="language-html">&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Lightful&lt;/title&gt;
    &lt;script src="https://aframe.io/releases/0.8.0/aframe.min.js"&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;a-scene&gt;
      &lt;!-- Camera! --&gt;
      &lt;a-entity id="rig" position="0 3 0"&gt;
        &lt;a-camera wasd-controls look-controls&gt;&lt;/a-camera&gt;
      &lt;/a-entity&gt;

      &lt;!-- Action! --&gt;
      &lt;a-box shadow width="75" height="0.1" depth="75" position="0 -1 0" color="#222"&gt;&lt;/a-box&gt;
    &lt;/a-scene&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

This concludes setup. Next, we will customize lighting for a more mysterious atmosphere.

### 2. Add Atmosphere

In this step, we will set up the fog and custom lighting.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9584a2b-9b23-488e-ad6d-f97380353789/4-preview-simple-scene-dark-mood.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9584a2b-9b23-488e-ad6d-f97380353789/4-preview-simple-scene-dark-mood.png" sizes="100vw" caption="A preview of a simple scene with a dark mood (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9584a2b-9b23-488e-ad6d-f97380353789/4-preview-simple-scene-dark-mood.png'>Large preview</a>)" alt="A preview of a simple scene with a dark mood" >}}

Add a fog, which will obscure objects far away for us. Modify the `a-scene` tag on line 8. Here, we will add a dark fog that quickly obscures the edges of the ground, giving the effect of a distant horizon.

<div class="break-out">

 <pre><code class="language-html">&lt;a-scene fog="type: linear; color: #111; near:10; far:15"&gt;&lt;/a-scene&gt;
</code></pre>
</div>

The dark gray `#111` fades in linearly from a distance of 10 to a distance of 15. All objects more than 15 units away are completely obscured, and all objects fewer than 10 units away are completely visible. Any object in between is partially obscured.

Add one ambient light to lighten in-game objects and one-directional light to accentuate reflective surfaces you will add later. Place this directly after the `a-scene` tag you modified in the previous instruction.

<div class="break-out">

 <pre><code class="language-html">&lt;!-- Lights! --&gt;
&lt;a-light type="directional" castshadow="true" intensity="0.5" color="#FFF" position="2 5 0"&gt;&lt;/a-light&gt;
&lt;a-light intensity="0.1" type="ambient" position="1 1 1" color="#FFF"&gt;&lt;/a-light&gt;
</code></pre>
</div>

Directly beneath the lights in the previous instruction, add a dark sky. Notice the dark gray `#111` matches that of the distant fog.

<pre><code class="language-html">&lt;a-sky color="#111"&gt;&lt;/a-sky&gt;
</code></pre>

This concludes basic modifications to the mood and more broadly, scene setup. Check that your code matches the [source code for Step 2](https://github.com/alvinwan/lightful/blob/master/tutorial/step02.html) on Github, exactly. Next, we will add a low-poly orb and begin customizing the orb's aesthetics.

{{% ad-panel-leaderboard %}}

## Creating The Orbs

### 3. Create A Low-Poly Orb

In this step, we will create a rotating, reflective orb as pictured below. The orb is composed of two stylized low-poly spheres with a few tricks to suggest reflective material.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6616f87f-e721-4dc1-9147-f52077eeb1f5/5-rotating-rreflective-orb.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6616f87f-e721-4dc1-9147-f52077eeb1f5/5-rotating-rreflective-orb.gif" width="" height="" alt="Rotating, reflective orb" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6616f87f-e721-4dc1-9147-f52077eeb1f5/5-rotating-rreflective-orb.gif">Large preview</a>)</figcaption></figure>

Start by importing the low-poly library in your `head` tag. Insert the following between lines 4 and 5.

<div class="break-out">

 <pre><code class="language-html">&lt;script src="https://cdn.jsdelivr.net/gh/alvinwan/aframe-low-poly@0.0.5/dist/aframe-low-poly.min.js"&gt;&lt;/script&gt;
</code></pre>
</div>

Create a carousel, wrapper, and orb container. The `carousel` will contain multiple orbs, the `wrapper` will allow us to rotate all orbs around a center axis without rotating each orb individually, and the `container` will &mdash; as the name suggests &mdash; contain all orb components.

<div class="break-out">

 <pre><code class="language-html">&lt;a-entity id="carousel"&gt;
  &lt;a-entity rotation="0 90 0" id="template" class="wrapper" position="0 0 0"&gt;
    &lt;a-entity id="container-orb0" class="container" position="8 3 0" scale="1 1 1"&gt;
      &lt;!-- place orb here --&gt;
    &lt;/a-entity&gt;
  &lt;/a-entity&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Inside the orb container, add the orb itself: one sphere is slightly translucent and offset, and the other is completely solid. The two combined mimic reflective surfaces.

<div class="break-out">

 <pre><code class="language-html">&lt;a-entity class="orb" id="orb0" data-id="0"&gt;
  &lt;lp-sphere seed="0" shadow max-amplitude="1 1 1" position="-0.5 0 -0.5"&gt;&lt;/lp-sphere&gt;
  &lt;lp-sphere seed="0" shadow max-amplitude="1 1 1" rotation="0 45 45" opacity="0.5" position="-0.5 0 -0.5"&gt;&lt;/lp-sphere&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Finally, rotate the sphere indefinitely by adding the following `a-animation` tag immediately after the `lp-sphere` inside the `.orb` entity in the last instruction.

<div class="break-out">

 <pre><code class="language-html">&lt;a-animation attribute="rotation" repeat="indefinite" from="0 0 0" to="0 360 0" dur="5000"&gt;&lt;/a-animation&gt;
</code></pre>
</div>

Your source code for the orb wrappers and the orb itself should match the following exactly.

<div class="break-out">

 <pre><code class="language-html">&lt;a-entity id="carousel"&gt;
  &lt;a-entity rotation="0 90 0" id="template" class="wrapper" position="0 0 0"&gt;
    &lt;a-entity id="container-orb0" class="container" position="8 3 0" scale="1 1 1"&gt;
      &lt;a-entity class="orb" id="orb0" data-id="0"&gt;
        &lt;lp-sphere seed="0" shadow max-amplitude="1 1 1" position="-0.5 0 -0.5"&gt;&lt;/lp-sphere&gt;
        &lt;lp-sphere seed="0" shadow max-amplitude="1 1 1" rotation="0 45 45" opacity="0.5" position="-0.5 0 -0.5"&gt;&lt;/lp-sphere&gt;
        &lt;a-animation attribute="rotation" repeat="indefinite" from="0 0 0" to="0 360 0" dur="5000"&gt;&lt;/a-animation&gt;
      &lt;/a-entity&gt;
    &lt;/a-entity&gt;
  &lt;/a-entity&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Check that your source code matches the full [source code for step 3](https://github.com/alvinwan/lightful/blob/master/tutorial/step03.html) on Github. Your preview should now match the following.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d614b09-bf3a-4c52-9d10-c6d44d357e60/6-rotating-reflective-orb.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d614b09-bf3a-4c52-9d10-c6d44d357e60/6-rotating-reflective-orb.gif" width="" height="" alt="Rotating, reflective orb" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d614b09-bf3a-4c52-9d10-c6d44d357e60/6-rotating-reflective-orb.gif">Large preview</a>)</figcaption></figure>

Next, we will add more lighting to the orb for a golden hue.

### 4. Light Up The Orb

In this step, we will add two lights, one colored and one white. This produces the following effect.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f970b3-2bfe-47de-8665-d817c676bb23/7-orb-lit-point-lights.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f970b3-2bfe-47de-8665-d817c676bb23/7-orb-lit-point-lights.gif" width="" height="" alt="Orb lit with point lights" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f970b3-2bfe-47de-8665-d817c676bb23/7-orb-lit-point-lights.gif">Large preview</a>)</figcaption></figure>

Start by adding the white light to illuminate the object from below. We will use a point light. Directly before `#orb0` but within `#container-orb0`, add the following offset point light.

<div class="break-out">

 <pre><code class="language-html">&lt;a-entity position="-2 -1 0"&gt;
    &lt;a-light distance="8" type="point" color="#FFF" intensity="0.8"&gt;&lt;/a-light&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

In your preview, you will see the following.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6616f87f-e721-4dc1-9147-f52077eeb1f5/5-rotating-rreflective-orb.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6616f87f-e721-4dc1-9147-f52077eeb1f5/5-rotating-rreflective-orb.gif" width="" height="" alt="Orb lit with white point light" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6616f87f-e721-4dc1-9147-f52077eeb1f5/5-rotating-rreflective-orb.gif">Large preview</a>)</figcaption></figure>

By default, lights do not decay with distance. By adding `distance="8"`, we ensure that the light fully decays with a distance of 8 units, to prevent the point light from illuminating the entire scene. Next, add the golden light. Add the following directly above the last light.

<div class="break-out">

 <pre><code class="language-html">&lt;a-light class="light-orb" id="light-orb0" distance="8" type="point" color="#f90" intensity="1"&gt;&lt;/a-light&gt;
</code></pre>
</div>

Check that your code matches the [source code for step 4](https://github.com/alvinwan/lightful/blob/master/tutorial/step04.html) exactly. Your preview will now match the following.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f970b3-2bfe-47de-8665-d817c676bb23/7-orb-lit-point-lights.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f970b3-2bfe-47de-8665-d817c676bb23/7-orb-lit-point-lights.gif" width="" height="" alt="Orb lit with point lights" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f970b3-2bfe-47de-8665-d817c676bb23/7-orb-lit-point-lights.gif">Large preview</a>)</figcaption></figure>

Next, you will make your final aesthetic modification to the orb and add rotating rings.


### 5. Add Rings

In this step, you will produce the final orb, as pictured below.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57283ba3-4888-4ace-bf1e-14d656390343/9-golden-orb-with-multiple-rings.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57283ba3-4888-4ace-bf1e-14d656390343/9-golden-orb-with-multiple-rings.gif" width="" height="" alt="Golden orb with multiple rings" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57283ba3-4888-4ace-bf1e-14d656390343/9-golden-orb-with-multiple-rings.gif">Large preview</a>)</figcaption></figure>

Add a ring in `#container-orb0` directly before `#orb0`.

<div class="break-out">

 <pre><code class="language-html">&lt;a-ring color="#fff" material="side:double" position="0 0.5 0" radius-inner="1.9" radius-outer="2" opacity="0.25"&gt;&lt;/a-ring&gt;
</code></pre>
</div>

Notice the ring itself does not contain color, as the color will be imbued by the point light in the previous step. Furthermore, the `material="side:double"` is important as, without it, the ring's backside would not be rendered; this means the ring would disappear for half of its rotation.

However, the preview with only the above code will not look any different. This is because the ring is currently perpendicular to the screen. Thus, only the ring's "side" (which has 0 thickness) is visible. Place the following animation in between the `a-ring` tags in the previous instruction.

<div class="break-out">

 <pre><code class="language-html">&lt;a-animation attribute="rotation" easing="linear" repeat="indefinite" from="0 0 0" to="0 360 0" dur="8000"&gt;&lt;/a-animation&gt;
</code></pre>
</div>

Your preview should now match the following:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f5cb249-04a7-4616-95e8-8a32be2a1435/8-golden-orb-with-ring.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f5cb249-04a7-4616-95e8-8a32be2a1435/8-golden-orb-with-ring.gif" width="" height="" alt="Golden orb with ring" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f5cb249-04a7-4616-95e8-8a32be2a1435/8-golden-orb-with-ring.gif">Large preview</a>)</figcaption></figure>

Create a variable number of rings with different rotation axes, speeds, and sizes. You can use the following example rings. Any new rings should be placed underneath the last `a-ring`.

<div class="break-out">

 <pre><code class="language-html">&lt;a-ring color="#fff" material="side:double" position="0 0.5 0" radius-inner="2.4" radius-outer="2.5" opacity="0.25"&gt;
  &lt;a-animation attribute="rotation" easing="linear" repeat="indefinite" from="0 45 0" to="360 45 0" dur="8000"&gt;&lt;/a-animation&gt;
&lt;/a-ring&gt;
&lt;a-ring color="#fff" material="side:double" position="0 0.5 0" radius-inner="1.4" radius-outer="1.5" opacity="0.25"&gt;
  &lt;a-animation attribute="rotation" easing="linear" repeat="indefinite" from="0 -60 0" to="-360 -60 0" dur="3000"&gt;&lt;/a-animation&gt;
&lt;/a-ring&gt;
</code></pre>
</div>

Your preview will now match the following.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57283ba3-4888-4ace-bf1e-14d656390343/9-golden-orb-with-multiple-rings.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57283ba3-4888-4ace-bf1e-14d656390343/9-golden-orb-with-multiple-rings.gif" width="" height="" alt="Golden orb with multiple rings" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57283ba3-4888-4ace-bf1e-14d656390343/9-golden-orb-with-multiple-rings.gif">Large preview</a>)</figcaption></figure>

Check that your code matches the [source code for step 5](https://github.com/alvinwan/lightful/blob/master/tutorial/step05.html) on Github. This concludes decor for the orb. With the orb finished, we will next add interactivity to the orb. In the next step, we will specifically add a visible cursor with a clicking animation when pointed at clickable objects.

{{% ad-panel-leaderboard %}}

## Making The Orbs Interactive

### 6. Add A Cursor

In this step, we will add a white cursor that can trigger clickable objects. The cursor is pictured below.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f85e4bb-c2a6-4915-a65f-b38f7c5b0b7d/10-clicking-on-orb.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f85e4bb-c2a6-4915-a65f-b38f7c5b0b7d/10-clicking-on-orb.gif" width="" height="" alt="clicking on orb" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f85e4bb-c2a6-4915-a65f-b38f7c5b0b7d/10-clicking-on-orb.gif">Large preview</a>)</figcaption></figure>

In your `a-camera` tag, add the following entity. The `fuse` attribute allows this entity the ability to trigger click events. The `raycaster` attribute determines how often and how far to check for clickable objects. The `objects` attribute accepts a selector to determine which entities are clickable. In this case, all objects of class `clickable` are clickable.

<div class="break-out">

 <pre><code class="language-html">&lt;a-entity cursor="fuse: true; fuseTimeout: 250"
      position="0 0 -1"
      geometry="primitive: ring; radiusInner: 0.03; radiusOuter: 0.04"
      material="color: white; shader: flat; opacity: 0.5"
      scale="0.5 0.5 0.5"
      raycaster="far: 20; interval: 1000; objects: .clickable"&gt;
    &lt;!-- Place cursor animation here --&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Next, add cursor animation and an extra ring for aesthetics. Place the following inside the entity cursor object above. This adds animation to the cursor object so that clicks are visible.

<div class="break-out">

 <pre><code class="language-html">&lt;a-circle radius="0.01" color="#FFF" opacity="0.5" material="shader: flat"&gt;&lt;/a-circle&gt;
&lt;a-animation begin="fusing" easing="ease-in" attribute="scale"
   fill="backwards" from="1 1 1" to="0.2 0.2 0.2" dur="250"&gt;&lt;/a-animation&gt;
</code></pre>
</div>

Next, add the `clickable` class to the `#orb0` to match the following.

<pre><code class="language-html">&lt;a-entity class="orb clickable" id="orb0" data-id="0"&gt;
</code></pre>

Check that your code matches the [source code for Step 6](https://github.com/alvinwan/lightful/blob/master/tutorial/step06.html) on Github. In your preview, drag your cursor off of them onto the orb to see the click animation in action. This is pictured below.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f85e4bb-c2a6-4915-a65f-b38f7c5b0b7d/10-clicking-on-orb.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f85e4bb-c2a6-4915-a65f-b38f7c5b0b7d/10-clicking-on-orb.gif" width="" height="" alt="clicking on orb" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f85e4bb-c2a6-4915-a65f-b38f7c5b0b7d/10-clicking-on-orb.gif">Large preview</a>)</figcaption></figure>

Note the clickable attribute was added to the orb itself and not the orb container. This is to prevent the rings from becoming clickable objects. This way, the user must click on the spheres that make up the orb itself.

In our final step for this part, you will add animation to control the on and off states for the orb.

### 7. Add Orb States

In this step, you will animate the orb in and out of an off state on click. This is pictured below.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2eba22-ac51-4b41-94e8-88f4cd27856a/11-interactive-orb-responding-clicks.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2eba22-ac51-4b41-94e8-88f4cd27856a/11-interactive-orb-responding-clicks.gif" width="" height="" alt="Interactive orb responding to clicks" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2eba22-ac51-4b41-94e8-88f4cd27856a/11-interactive-orb-responding-clicks.gif">Large preview</a>)</figcaption></figure>

To start, you will shrink and lower the orb to the ground. Add `a-animation` tags to the `#container-orb0` right after `#orb0`. Both animations are triggered by a click and share the same easing function `ease-elastic` for a slight bounce.

<div class="break-out">

 <pre><code class="language-html">&lt;a-animation class="animation-scale" easing="ease-elastic" begin="click" attribute="scale" from="0.5 0.5 0.5" to="1 1 1" direction="alternate" dur="2000"&gt;&lt;/a-animation&gt;
&lt;a-animation class="animation-position" easing="ease-elastic" begin="click" attribute="position" from="8 0.5 0" to="8 3 0" direction="alternate" dur="2000"&gt;&lt;/a-animation&gt;
</code></pre>
</div>

To further emphasize the off state, we will remove the golden point light when the orb is off. However, the orb's lights are placed outside of the orb object. Thus, the click event is not passed to the lights when the orb is clicked. To circumvent this issue, we will use some light Javascript to pass the click event to the light. Place the following animation tag in `#light-orb0`. The light is triggered by a custom `switch` event.

<div class="break-out">

 <pre><code class="language-html">&lt;a-animation class="animation-intensity" begin="switch" attribute="intensity" from="0" to="1" direction="alternate"&gt;&lt;/a-animation&gt;
</code></pre>
</div>

Next, add the following click event listener to the `#container-orb0`. This will relay the clicks to the orb lights.

<div class="break-out">

 <pre><code class="language-html">&lt;a-entity id="container-orb0" ... onclick="document.querySelector('#light-orb0').emit('switch');"&gt;
</code></pre>
</div>

Check that your code matches the [source code for Step 7](https://github.com/alvinwan/lightful/blob/master/tutorial/step07.html) on Github. Finally, pull up your preview, and move the cursor on and off the orb to toggle between off and on states. This is pictured below.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2eba22-ac51-4b41-94e8-88f4cd27856a/11-interactive-orb-responding-clicks.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2eba22-ac51-4b41-94e8-88f4cd27856a/11-interactive-orb-responding-clicks.gif" width="" height="" alt="Interactive orb responding to clicks" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2eba22-ac51-4b41-94e8-88f4cd27856a/11-interactive-orb-responding-clicks.gif">Large preview</a>)</figcaption></figure>

This concludes the orb's interactivity. The player can now turn orbs on and off at will, with self-explanatory on and off states.

## Conclusion

In this tutorial, you built a simple orb with on and off states, which can be toggled by a VR-headset-friendly cursor click. With a number of different lighting techniques and animations, you were able to distinguish between the two states. This concludes the virtual reality design elements for the orbs. In the next part of the tutorial, we will populate the orbs dynamically, add game mechanics, and set up a communication protocol between a pair of players. 

{{< signature "rb, dm, il" >}}
