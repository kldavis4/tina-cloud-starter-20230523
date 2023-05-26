---
title: 'How To Build An Endless Runner Game In Virtual Reality (Part 1)'
slug: virtual-reality-endless-runner-game-vr-part-1
author: alvin-wan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8858c709-72cc-40d3-a387-ed6c18021bdf/sharing-card-endless-runner-game-vr-alvin-wan.png
date: 2019-03-06T14:00:35+01:00
summary: >-
  Virtual reality (VR) is an experience based in a computer-generated environment, and following Alvin’s [introduction to programming in VR](https://www.smashingmagazine.com/2018/11/virtual-reality-model-real-time-cross-device-preview/), this article series aims to introduce more VR concepts in the context of building a game.
description: >-
  Virtual reality (VR) is an experience based in a computer-generated environment, and following Alvin’s [introduction to programming in VR](https://www.smashingmagazine.com/2018/11/virtual-reality-model-real-time-cross-device-preview/), this article series aims to introduce more VR concepts in the context of building a game.
categories:
  - Virtual Reality
  - User Interaction
  - UX
  - UI
---
Today, I’d like to invite you to build an endless runner VR game with webVR &mdash; a framework that gives a dual advantage: It can be played with or without a VR headset. I’ll explain the magic behind the gaze-based controls for our VR-headset players by removing the game control’s dependence on a keyboard.

In this tutorial, I’ll also show you how you can synchronize the *game state* between two devices which will move you one step closer to building a multiplayer game. I’ll specifically introduce more A-Frame VR concepts such as stylized low-poly entities, lights, and animation.

To get started, you will need the following:

- Internet access (specifically to [glitch.com](https://glitch.com));
- A new Glitch project;
- A virtual reality headset (optional, recommended). (I use Google Cardboard, which is offered at $15 a piece.)

**Note**: *A demo of the final product can be viewed [here](https://ergo-1.glitch.me).*

{{% feature-panel %}}

## Step 1: Setting Up A Basic Scene

In this step, we will set up the following scene for our game. It is composed of a few basic geometric shapes and includes custom lighting, which we will describe in more detail below. As you progress in the tutorial, you will add various animations and effects to transform these basic geometric entities into icebergs sitting in an ocean.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8613fc15-7f54-44bb-85c9-93769b3cb7d2/vr-endless-runner-game-0-p1-s1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8613fc15-7f54-44bb-85c9-93769b3cb7d2/vr-endless-runner-game-0-p1-s1.png" sizes="100vw" caption="A preview of the game scene’s basic geometric objects (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8613fc15-7f54-44bb-85c9-93769b3cb7d2/vr-endless-runner-game-0-p1-s1.png'>Large preview</a>)" alt="A preview of the game scene’s basic geometric objects" >}}

You will start by setting up a website with a single static HTML page. This allows you to code from your desktop and automatically deploy to the web. The deployed website can then be loaded on your mobile phone and placed inside a VR headset. Alternatively, the deployed website can be loaded by a standalone VR headset.

Get started by navigating to [glitch.com](https://glitch.com). Then, do the following:

<ol>
  <li>Click on “New Project” in the top right.</li>
  <li>Click on “hello-webpage” in the drop down.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4967a5fd-69eb-4514-9025-f45e888aa15e/vr-endless-runner-game-1-p1-s1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4967a5fd-69eb-4514-9025-f45e888aa15e/vr-endless-runner-game-1-p1-s1.png" sizes="100vw" caption="<a href='https://glitch.com'>Glitch.com</a>’s homepage (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4967a5fd-69eb-4514-9025-f45e888aa15e/vr-endless-runner-game-1-p1-s1.png'>Large preview</a>)" alt="Glitch.com’s homepage" >}}
</li>
<li>Next, click on <code>index.html</code> in the left sidebar. We will refer to this as your “editor”.</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18c9670f-8b15-499a-a5d4-52b5b7d50d6f/vr-endless-runner-game-2-p1-s1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18c9670f-8b15-499a-a5d4-52b5b7d50d6f/vr-endless-runner-game-2-p1-s1.png" sizes="100vw" caption="Glitch project: the index.html file (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18c9670f-8b15-499a-a5d4-52b5b7d50d6f/vr-endless-runner-game-2-p1-s1.png'>Large preview</a>)" alt="Glitch project index.html file" >}}

Start by deleting all existing code in the current *index.html* file. Then, type in the following for a basic webVR project, using A-Frame VR. This creates an empty scene by using A-Frame’s default lighting and camera.

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Ergo | Endless Runner Game in Virtual Reality&lt;/title&gt;
    &lt;script src="https://aframe.io/releases/0.7.0/aframe.min.js"&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;a-scene&gt;
    &lt;/a-scene&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

**Note**: *You can learn more about A-Frame VR at [aframe.io](https://aframe.io).*

To start, add a fog, which will obscure objects far away for us. Modify the `a-scene` tag on line 8.

<pre><code class="language-html">&lt;a-scene fog="type: linear; color: #a3d0ed; near:5; far:20"&gt;
</code></pre>

Moving forward, all objects in the scene will be added between the `<a-scene>...</a-scene>` tags. The first item is the sky. Between your `a-scene` tags, add the `a-sky` entity.

<pre><code class="language-html">&lt;a-scene ...&gt;
  &lt;a-sky color="#a3d0ed"&gt;&lt;/a-sky&gt;
&lt;/a-scene&gt;
</code></pre>

After your sky, add lighting to replace the default A-Frame lighting.

There are three types of lighting:

- **Ambient**  
This is an ever-present light that appears to emanate from all objects in the scene. If you wanted a blue tint on all objects, resulting in blue-ish shadows, you would add a blue ambient light. For example, the objects in this [Low Poly Island scene](https://alvinwan.com/vr/low-poly-island/) are all white. However, a blue ambient light results in a blue hue.
- **Directional**  
This is analogous to a flashlight which, as the name suggests, points in a certain direction.
- **Point**  
Again, as the name suggests, this emanates light from a point.

{{% ad-panel-leaderboard %}}

Just below your `a-sky` entity, add the following lights: one directional and one ambient. Both are light blue.

<div class="break-out">

 <pre><code class="language-html">&lt;!-- Lights --&gt;
&lt;a-light type="directional" castShadow="true" intensity="0.4" color="#D0EAF9;" position="5 3 1"&gt;&lt;/a-light&gt;
&lt;a-light intensity="0.8" type="ambient" color="#B4C5EC"&gt;&lt;/a-light&gt;
</code></pre>
</div>

Next, add a camera with a custom position to replace the default A-Frame camera. Just below your `a-light` entities, add the following:

<pre><code class="language-html">&lt;!-- Camera --&gt;
&lt;a-camera position="0 0 2.5"&gt;&lt;/a-camera&gt;
</code></pre>

Just below your `a-camera` entity, add several icebergs using low-poly cones.

<pre><code class="language-html">&lt;!-- Icebergs --&gt;
&lt;a-cone class="iceberg" segments-radial="5" segments-height="3" height="1" radius-top="0.15" radius-bottom="0.5" position="3 -0.1 -1.5"&gt;&lt;/a-cone&gt;
&lt;a-cone class="iceberg" segments-radial="7" segments-height="3" height="0.5" radius-top="0.25" radius-bottom="0.35" position="-3 -0.1 -0.5"&gt;&lt;/a-cone&gt;
&lt;a-cone class="iceberg" segments-radial="6" segments-height="2" height="0.5" radius-top="0.25" radius-bottom="0.25" position="-5 -0.2 -3.5"&gt;&lt;/a-cone&gt;
</code></pre>

Next, add an ocean, which we will temporarily represent with a box, among your icebergs. In your code, add the following after the cones from above.

<div class="break-out">

 <pre><code class="language-html">&lt;!-- Ocean --&gt;
&lt;a-box depth="50" width="50" height="1" color="#7AD2F7" position="0 -0.5 0"&gt;&lt;/a-box&gt;
</code></pre>
</div>

Next, add a platform for our endless runner game to take place on. We will represent this platform using the side of a large cone. After the box above, add the following:

<div class="break-out">

 <pre><code class="language-html">&lt;!-- Platform --&gt;
&lt;a-cone scale="2 2 2" shadow position="0 -3.5 -1.5" rotation="90 0 0" radius-top="1.9" radius-bottom="1.9" segments-radial="20" segments-height="20" height="20" emissive="#005DED" emissive-intensity="0.1"&gt;
  &lt;a-entity id="tree-container" position="0 .5 -1.5" rotation="-90 0 0"&gt;
  &lt;/a-entity&gt;
&lt;/a-cone&gt;
</code></pre>
</div>

Finally, add the player, which we will represent using a small glowing sphere, on the platform we just created. Between the `<a-entity id="tree-container" ...></a-entity>` tags, add the following:

<div class="break-out">

 <pre><code class="language-html">&lt;a-entity id="tree-container"...&gt;
  &lt;!-- Player --&gt;
  &lt;a-entity id="player" player&gt;
    &lt;a-sphere radius="0.05"&gt;
      &lt;a-light type="point" intensity="0.35" color="#FF440C"&gt;&lt;/a-light&gt;
    &lt;/a-sphere&gt;
  &lt;/a-entity&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Check that your code now matches the following, exactly. You can also view the full [source code for step 1](https://github.com/alvinwan/ergo/blob/master/tutorial/step_1_basic/index.html).

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Ergo | Endless Runner Game in Virtual Reality&lt;/title&gt;
    &lt;script src="https://aframe.io/releases/0.7.0/aframe.min.js"&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;a-scene fog="type: linear; color: #a3d0ed; near:5; far:20"&gt;

      &lt;a-sky color="#a3d0ed"&gt;&lt;/a-sky&gt;

      &lt;!-- Lights --&gt;
      &lt;a-light type="directional" castShadow="true" intensity="0.4" color="#D0EAF9;" position="5 3 1"&gt;&lt;/a-light&gt;
      &lt;a-light intensity="0.8" type="ambient" color="#B4C5EC"&gt;&lt;/a-light&gt;

      &lt;!-- Camera --&gt;
      &lt;a-camera position="0 0 2.5"&gt;&lt;/a-camera&gt;

      &lt;!-- Icebergs --&gt;
      &lt;a-cone class="iceberg" segments-radial="5" segments-height="3" height="1" radius-top="0.15" radius-bottom="0.5" position="3 -0.1 -1.5"&gt;&lt;/a-cone&gt;
      &lt;a-cone class="iceberg" segments-radial="7" segments-height="3" height="0.5" radius-top="0.25" radius-bottom="0.35" position="-3 -0.1 -0.5"&gt;&lt;/a-cone&gt;
      &lt;a-cone class="iceberg" segments-radial="6" segments-height="2" height="0.5" radius-top="0.25" radius-bottom="0.25" position="-5 -0.2 -3.5"&gt;&lt;/a-cone&gt;

      &lt;!-- Ocean --&gt;
      &lt;a-box depth="50" width="50" height="1" color="#7AD2F7" position="0 -0.5 0"&gt;&lt;/a-box&gt;

      &lt;!-- Platform --&gt;
      &lt;a-cone scale="2 2 2" shadow position="0 -3.5 -1.5" rotation="90 0 0" radius-top="1.9" radius-bottom="1.9" segments-radial="20" segments-height="20" height="20" emissive="#005DED" emissive-intensity="0.1"&gt;
        &lt;a-entity id="tree-container" position="0 .5 -1.5" rotation="-90 0 0"&gt;
          &lt;!-- Player --&gt;
          &lt;a-entity id="player" player&gt;
            &lt;a-sphere radius="0.05"&gt;
              &lt;a-light type="point" intensity="0.35" color="#FF440C"&gt;&lt;/a-light&gt;
            &lt;/a-sphere&gt;
          &lt;/a-entity&gt;
        &lt;/a-entity&gt;
      &lt;/a-cone&gt;
    &lt;/a-scene&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

To preview the webpage, click on “Preview” in the top left. We will refer to this as your *preview*. Note that any changes in your editor will be automatically reflected in this preview, barring bugs or unsupported browsers.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6d69bb7-6920-4fb2-bdd8-bf8c20c2372d/vr-endless-runner-game-3-p1-s1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6d69bb7-6920-4fb2-bdd8-bf8c20c2372d/vr-endless-runner-game-3-p1-s1.png" sizes="100vw" caption="“Show Live” button in glitch project (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6d69bb7-6920-4fb2-bdd8-bf8c20c2372d/vr-endless-runner-game-3-p1-s1.png'>Large preview</a>)" alt="“Show Live” button in glitch project" >}}

In your preview, you will see the following basic virtual reality scene. You can view this scene by using your favorite VR headset.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/627c40bd-d029-409f-a0d6-17f134912333/vr-endless-runner-game-4-p1-s2.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/627c40bd-d029-409f-a0d6-17f134912333/vr-endless-runner-game-4-p1-s2.gif" width="800" alt="Animating Ocean and Fixed White Cursor" /></a><figcaption>Animating <code>Ocean</code> and the fixed white <code>cursor</code> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/627c40bd-d029-409f-a0d6-17f134912333/vr-endless-runner-game-4-p1-s2.gif">Large preview</a>)</figcaption></figure>

This concludes the first step, setting up the game scene’s basic geometric objects. In the next step, you will add animations and use other A-Frame VR libraries for more visual effects.

## Step 2: Improve Aesthetics for Virtual Reality Scene

In this step, you will add a number of aesthetic improvements to the scene:

1. **Low-poly objects**  
You will substitute some of the basic geometric objects with their low-poly equivalents for more convincing, irregular geometric shapes.
2. **Animations**  
You will have the player bob up and down, move the icebergs slightly, and make the ocean a moving body of water.

Your final product for this step will match the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd377748-d885-41ae-af76-f18ba76baaa5/vr-endless-runner-game-5-p1-s2.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd377748-d885-41ae-af76-f18ba76baaa5/vr-endless-runner-game-5-p1-s2.gif" width="800" alt="Low-poly icebergs bobbing around" /></a><figcaption>Low-poly icebergs bobbing around (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd377748-d885-41ae-af76-f18ba76baaa5/vr-endless-runner-game-5-p1-s2.gif">Large preview</a>)</figcaption></figure>

To start, import A-Frame low-poly components. In `<head>...</head>`, add the following JavaScript import:

<div class="break-out">

 <pre><code class="language-javascript"> &lt;script src="https://aframe.io...&gt;&lt;/script&gt;
  &lt;script src="https://cdn.jsdelivr.net/gh/alvinwan/aframe-low-poly@0.0.2/dist/aframe-low-poly.min.js"&gt;&lt;/script&gt;
&lt;/head&gt;
</code></pre>
</div>

The **A-Frame low-poly** library implements a number *primitives*, such as `lp-cone` and `lp-sphere`, each of which is a low-poly version of an A-Frame primitive. You can learn more about A-Frame primitives over [here](https://aframe.io/docs/0.8.0/introduction/html-and-primitives.html).

Next, navigate to the `<!-- Icebergs -->` section of your code. Replace all `<a-cone>`s with `<lp-cone>`.

<pre><code class="language-javascript">&lt;!-- Icebergs --&gt;
&lt;lp-cone class="iceberg" ...&gt;&lt;/lp-cone&gt;
&lt;lp-cone class="iceberg" ...&gt;&lt;/lp-cone&gt;
&lt;lp-cone class="iceberg" ...&gt;&lt;/lp-cone&gt;
</code></pre>

We will now configure the low-poly primitives. All low-poly primitive supports two attributes, which control how exaggerated the low-poly stylization is:

1. `amplitude`
This is the degree of stylization. The greater this number, the more a low-poly shape can deviate from its original geometry.
2. `amplitude-variance`
This is how much stylization can vary, from vertex to vertex. The greater this number, the more variety there is in how much each vertex may deviate from its original geometry.

To get a better intuition for what these two variables mean, you can modify these two attributes in the [A-Frame low-poly demo](https://trees.alvinwan.com/).

For the first iceberg, set `amplitude-variance` to 0.25. For the second iceberg, set `amplitude` to 0.12. For the last iceberg, set `amplitude` to 0.1.

<pre><code class="language-javascript">&lt;!-- Icebergs --&gt;
&lt;lp-cone class="iceberg" amplitude-variance="0.25" ...&gt;&lt;/lp-cone&gt;
&lt;lp-cone class="iceberg" amplitude="0.12" ... &gt;&lt;/lp-cone&gt;
&lt;lp-cone class="iceberg" amplitude="0.1" ...&gt;&lt;/lp-cone&gt;
</code></pre>

To finish the icebergs, animate both position and rotation for all three icebergs. Feel free to configure these positions and rotations as desired.

The below features a sample setting:

<div class="break-out">

 <pre><code class="language-javascript">&lt;lp-cone class="iceberg" amplitude-variance="0.25" ...&gt;
        &lt;a-animation attribute="rotation" from="-5 0 0" to="5 0 0" repeat="indefinite" direction="alternate"&gt;&lt;/a-animation&gt;
        &lt;a-animation attribute="position" from="3 -0.2 -1.5" to="4 -0.2 -2.5" repeat="indefinite" direction="alternate" dur="12000" easing="linear"&gt;&lt;/a-animation&gt;
      &lt;/lp-cone&gt;
      &lt;lp-cone class="iceberg" amplitude="0.12" ...&gt;
        &lt;a-animation attribute="rotation" from="0 0 -5" to="5 0 0" repeat="indefinite" direction="alternate" dur="1500"&gt;&lt;/a-animation&gt;
        &lt;a-animation attribute="position" from="-4 -0.2 -0.5" to="-2 -0.2 -0.5" repeat="indefinite" direction="alternate" dur="15000" easing="linear"&gt;&lt;/a-animation&gt;
      &lt;/lp-cone&gt;
      &lt;lp-cone class="iceberg" amplitude="0.1" ...&gt;
        &lt;a-animation attribute="rotation" from="5 0 -5" to="5 0 0" repeat="indefinite" direction="alternate" dur="800"&gt;&lt;/a-animation&gt;
        &lt;a-animation attribute="position" from="-3 -0.2 -3.5" to="-5 -0.2 -5.5" repeat="indefinite" direction="alternate" dur="15000" easing="linear"&gt;&lt;/a-animation&gt;
      &lt;/lp-cone&gt;
</code></pre>
</div>

Navigate to your preview, and you should see the low-poly icebergs bobbing around.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif" width="800" alt="Bobbing player with fluctuating light" /></a><figcaption>Bobbing player with fluctuating light (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif">Large preview</a>)</figcaption></figure>

Next, update the platform and associated player. Here, upgrade the cone to a low-poly object, changing `a-cone` to `lp-cone` for `<!-- Platform -->`. Additionally, add configurations for `amplitude`.

<pre><code class="language-javascript">&lt;!-- Platform --&gt;
&lt;lp-cone amplitude="0.05" amplitude-variance="0.05" scale="2 2 2"...&gt;
    ...
&lt;/lp-cone&gt;
</code></pre>

Next, still within the platform section, navigate to the `<!-- Player -->` subsection of your code. Add the following animations for position, size, and intensity.

<div class="break-out">

 <pre><code class="language-javascript">&lt;!-- Player --&gt;
&lt;a-entity id="player" ...&gt;
  &lt;a-sphere ...&gt;
    &lt;a-animation repeat="indefinite" direction="alternate" attribute="position" ease="ease-in-out" from="0 0.5 0.6" to="0 0.525 0.6"&gt;&lt;/a-animation&gt;
    &lt;a-animation repeat="indefinite" direction="alternate" attribute="radius" from="0.05" to="0.055" dur="1500"&gt;&lt;/a-animation&gt;
    &lt;a-light ...&gt;
      &lt;a-animation repeat="indefinite" direction="alternate-reverse" attribute="intensity" ease="ease-in-out" from="0.35" to="0.5"&gt;&lt;/a-animation&gt;
    &lt;/a-light&gt;
  &lt;/a-sphere&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Navigate to your preview, and you will see your player bobbing up and down, with a fluctuating light on a low-poly platform.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif" width="800" alt="Bobbing player with fluctuating light" /></a><figcaption>Bobbing player with fluctuating light (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif">Large preview</a>)</figcaption></figure>

Next, let’s animate the ocean. Here, you can use a lightly-modified version of Don McCurdy’s ocean. The modifications allow us to configure how large and fast the ocean’s waves move.

Create a new file via the Glitch interface, by clicking on “+ New File” on the left. Name this new file *assets/ocean.js*. Paste the following into your new *ocean.js* file:

<div class="break-out">

 <pre><code class="language-javascript">/**
 * Flat-shaded ocean primitive.
 * https://github.com/donmccurdy/aframe-extras
 *
 * Based on a Codrops tutorial:
 * https://tympanus.net/codrops/2016/04/26/the-aviator-animating-basic-3d-scene-threejs/
 */
AFRAME.registerPrimitive('a-ocean', {
  defaultComponents: {
    ocean: {},
    rotation: {x: -90, y: 0, z: 0}
  },
  mappings: {
    width: 'ocean.width',
    depth: 'ocean.depth',
    density: 'ocean.density',
    amplitude: 'ocean.amplitude',
    'amplitude-variance': 'ocean.amplitudeVariance',
    speed: 'ocean.speed',
    'speed-variance': 'ocean.speedVariance',
    color: 'ocean.color',
    opacity: 'ocean.opacity'
  }
});

AFRAME.registerComponent('ocean', {
  schema: {
    // Dimensions of the ocean area.
    width: {default: 10, min: 0},
    depth: {default: 10, min: 0},

    // Density of waves.
    density: {default: 10},

    // Wave amplitude and variance.
    amplitude: {default: 0.1},
    amplitudeVariance: {default: 0.3},

    // Wave speed and variance.
    speed: {default: 1},
    speedVariance: {default: 2},

    // Material.
    color: {default: '#7AD2F7', type: 'color'},
    opacity: {default: 0.8}
  },

  /**
   * Use play() instead of init(), because component mappings – unavailable as dependencies – are
   * not guaranteed to have parsed when this component is initialized.
   * /
  play: function () {
    const el = this.el,
        data = this.data;
    let material = el.components.material;

    const geometry = new THREE.PlaneGeometry(data.width, data.depth, data.density, data.density);
    geometry.mergeVertices();
    this.waves = [];
    for (let v, i = 0, l = geometry.vertices.length; i < l; i++) {
      v = geometry.vertices[i];
      this.waves.push({
        z: v.z,
        ang: Math.random() * Math.PI * 2,
        amp: data.amplitude + Math.random() * data.amplitudeVariance,
        speed: (data.speed + Math.random() * data.speedVariance) / 1000 // radians / frame
      });
    }

    if (!material) {
      material = {};
      material.material = new THREE.MeshPhongMaterial({
        color: data.color,
        transparent: data.opacity < 1,
        opacity: data.opacity,
        shading: THREE.FlatShading,
      });
    }

    this.mesh = new THREE.Mesh(geometry, material.material);
    el.setObject3D('mesh', this.mesh);
  },

  remove: function () {
    this.el.removeObject3D('mesh');
  },

  tick: function (t, dt) {
    if (!dt) return;

    const verts = this.mesh.geometry.vertices;
    for (let v, vprops, i = 0; (v = verts[i]); i++){
      vprops = this.waves[i];
      v.z = vprops.z + Math.sin(vprops.ang) * vprops.amp;
      vprops.ang += vprops.speed * dt;
    }
    this.mesh.geometry.verticesNeedUpdate = true;
  }
});
</code></pre>
</div>

Navigate back to your *index.html* file. In the `<head>` of your code, import the new JavaScript file:

<pre><code class="language-javascript"> &lt;script src="https://cdn.jsdelivr.net..."&gt;&lt;/script&gt;
  &lt;script src="./assets/ocean.js"&gt;&lt;/script&gt;
&lt;/head&gt;
</code></pre>

Navigate to the `<!-- Ocean -->` section of your code. Replace the `a-box` to an `a-ocean`. Just as before, we set `amplitude` and `amplitude-variance` of our low-poly object.

<div class="break-out">

 <pre><code class="language-javascript">&lt;!-- Ocean --&gt;
&lt;a-ocean depth="50" width="50" amplitude="0" amplitude-variance="0.1" speed="1.5" speed-variance="1" opacity="1" density="50"&gt;&lt;/a-ocean&gt;
&lt;a-ocean depth="50" width="50" opacity="0.5" amplitude="0" amplitude-variance="0.15" speed="1.5" speed-variance="1" density="50"&gt;&lt;/a-ocean&gt;
</code></pre>
</div>

For your final aesthetic modification, add a white round cursor to indicate where the user is pointing. Navigate to the `<!-- Camera -->`.

<div class="break-out">

 <pre><code class="language-javascript">&lt;!-- Camera --&gt;
&lt;a-camera ...&gt;
  &lt;a-entity id="cursor-mobile" cursor="fuse: true; fuseTimeout: 250"
    position="0 0 -1"
    geometry="primitive: ring; radiusInner: 0.02; radiusOuter: 0.03"
    material="color: white; shader: flat"
    scale="0.5 0.5 0.5"
    raycaster="far: 50; interval: 1000; objects: .clickable"&gt;
  &lt;a-animation begin="fusing" easing="ease-in" attribute="scale"
    fill="backwards" from="1 1 1" to="0.2 0.2 0.2" dur="250"&gt;&lt;/a-animation&gt;
  &lt;/a-camera&gt;
</code></pre>
</div>

Ensure that your *index.html* code matches [the Step 2 source code](https://github.com/alvinwan/ergo/blob/master/tutorial/step_2_aesthetics/index.html). Navigate to your preview, and you’ll find the updated ocean along with a white circle fixed to the center of your view.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif" width="800" alt="Bobbing player with fluctuating light" /></a><figcaption>Bobbing player with fluctuating light (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3eb4ac-da6d-40a5-b354-484ccd329af8/vr-endless-runner-game-6-p1-s2.gif">Large preview</a>)</figcaption></figure>

This concludes your aesthetic improvements to the scene. In this section, you learned how to use and configure low-poly versions of A-Frame primitives, e.g. `lp-cone`. In addition, you added a number of animations for different object attributes, such as position, rotation, and light intensity. In the next step, you will add the ability for the user to control the player &mdash; just by looking at different lanes.

{{% ad-panel-leaderboard %}}

## Step 3: Add Virtual Reality Gaze Controls

Recall that our audience is a user wearing a virtual reality headset. As a result, your game cannot depend on keyboard input for controls. To make this game accessible, our VR controls will rely only on the user’s head rotation. Simply look to the right to move the player to the right, look to the center to move to the middle, and look to the left to move to the left. Our final product will look like the following.

**Note**: *The demo GIF below was recorded on a desktop, with user drag as a substitute for head rotation.*

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/730f6a49-28ad-4665-9a69-9789f51c882c/vr-endless-runner-game-7-p1-s3.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/730f6a49-28ad-4665-9a69-9789f51c882c/vr-endless-runner-game-7-p1-s3.gif" width="800" alt="Controlling game character with head rotation" /></a><figcaption>Controlling game character with head rotation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/730f6a49-28ad-4665-9a69-9789f51c882c/vr-endless-runner-game-7-p1-s3.gif">Large preview</a>)</figcaption></figure>

Start from your *index.html* file. In the `<head>...</head>` tag, import your new JavaScript file, `assets/ergo.js`. This new JavaScript file will contain the game’s logic.

<pre><code class="language-javascript"> &lt;script src=...&gt;&lt;/script&gt;
  &lt;script src="./assets/ergo.js"&gt;&lt;/script&gt;
&lt;/head&gt;
</code></pre>

Then, add a new `lane-controls` attribute to your `a-camera` object:

<pre><code class="language-javascript">&lt;!-- Camera --&gt;
&lt;a-camera lane-controls position...&gt;
&lt;/a-camera&gt;
</code></pre>

Next, create your new JavaScript file using “+ New File” to the left. Use *assets/ergo.js* for the filename. For the remainder of this step, you will be working in this new JavaScript file. In this new file, define a new function to setup controls, and invoke it immediately. Make sure to include the comments below, as we will refer to sections of code by those names.

<pre><code class="language-javascript">/************
 * CONTROLS *
 ************/

function setupControls() {
}

/********
 * GAME *
 ********/

setupControls();
</code></pre>

**Note**: *The setupControls function is invoked in the global scope, because A-Frame components must be registered before the* `<a-scene>` *tag. I will explain what a component is below.*

In your `setupControls` function, register a new A-Frame component. A component modifies an entity in A-Frame, allowing you to add custom animations, change how an entity initializes, or respond to user input. There are many other use cases, but you will focus on the last one: responding to user input. Specifically, you will read user rotation and move the player accordingly.

In the `setupControls` function, register the A-Frame component we added to the camera earlier, `lane-controls`. We will add an event listener for the `tick` event. This event triggers at every animation frame. In this event listener, hlog output at every tick.

<pre><code class="language-javascript">function setupControls() {
    AFRAME.registerComponent('lane-controls', {
        tick: function(time, timeDelta) {
            console.log(time);
        }
    });
}
</code></pre>

Navigate to your preview. Open your browser developer console by right-clicking anywhere and selecting "Inspect". This applies to Firefox, Chrome, and Safari. Then, select "Console" from the top navigation bar. Ensure that you see timestamps flowing into the console.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b129470e-f806-4c7a-8148-3516419faef2/vr-endless-runner-game-8-p1-s3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b129470e-f806-4c7a-8148-3516419faef2/vr-endless-runner-game-8-p1-s3.png" sizes="100vw" caption="Timestamps in console (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b129470e-f806-4c7a-8148-3516419faef2/vr-endless-runner-game-8-p1-s3.png'>Large preview</a>)" alt="Timestamps in console" >}}

Navigate back to your editor. Still in `assets/ergo.js`, replace the body of `setupControls` with the following. Fetch the camera rotation using `this.el.object3D.rotation`, and log the lane to move the player to.

<pre><code class="language-javascript">function setupControls() {
  AFRAME.registerComponent('lane-controls', {
    tick: function (time, timeDelta) {
      var rotation = this.el.object3D.rotation;

      if      (rotation.y > 0.1)  console.log("left");
      else if (rotation.y < -0.1) console.log("right");
      else                        console.log("middle");
    }
  })
}
</code></pre>

Navigate back to your preview. Again, open your developer console. Try rotating the camera slightly, and observe console output update accordingly.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23c3ae83-32bc-4519-bf5d-88dfea389976/vr-endless-runner-game-9-p1-s3.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23c3ae83-32bc-4519-bf5d-88dfea389976/vr-endless-runner-game-9-p1-s3.gif" width="800" alt="Lane log based on camera rotation" /></a><figcaption>Lane log based on camera rotation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23c3ae83-32bc-4519-bf5d-88dfea389976/vr-endless-runner-game-9-p1-s3.gif">Large preview</a>)</figcaption></figure>

Before the `controls` section, add three constants representing the left, middle, and right lane `x` values.

<pre><code class="language-javascript">const POSITION_X_LEFT = -0.5;
const POSITION_X_CENTER = 0;
const POSITION_X_RIGHT = 0.5;

/************
 * CONTROLS *
 ************/

...
</code></pre>

At the start of the `controls` section, define a new global variable representing the player position.

<pre><code class="language-javascript">/************
 * CONTROLS *
 ************/

// Position is one of 0 (left), 1 (center), or 2 (right)
var player_position_index = 1;

function setupControls() {
...
</code></pre>

After the new global variable, define a new function that will move the player to each lane.

<pre><code class="language-javascript">var player_position_index = 1;

/**
 * Move player to provided index
 * @param {int} Lane to move player to
 */
function movePlayerTo(position_index) {
}

function setupControls() {
...
</code></pre>

Inside this new function, start by updating the global variable. Then, define a dummy position.

<pre><code class="language-javascript">function movePlayerTo(position_index) {
  player_position_index = position_index;

  var position = {x: 0, y: 0, z: 0}
}
</code></pre>

After defining the position, update it according to the function input.

<pre><code class="language-javascript">function movePlayerTo(position_index) {
  ...
  if      (position_index == 0) position.x = POSITION_X_LEFT;
  else if (position_index == 1) position.x = POSITION_X_CENTER;
  else                          position.x = POSITION_X_RIGHT;
}
</code></pre>

Finally, update the player position.

<pre><code class="language-javascript">function movePlayerTo(position_index) {
    ...
document.getElementById('player').setAttribute('position', position);
}
</code></pre>

Double-check that your function matches the following.

<pre><code class="language-javascript">/**
 * Move player to provided index
 * @param {int} Lane to move player to
 */
function movePlayerTo(position_index) {
  player_position_index = position_index;

  var position = {x: 0, y: 0, z: 0}
  if      (position_index == 0) position.x = POSITION_X_LEFT;
  else if (position_index == 1) position.x = POSITION_X_CENTER;
  else                          position.x = POSITION_X_RIGHT;
  document.getElementById('player').setAttribute('position', position);
}
</code></pre>

Navigate back to your preview. Open the developer console. Invoke your new `movePlayerTo` function from the console to ensure that it functions.

<pre><code class="language-javascript">> movePlayerTo(2)  # should move to right
</code></pre>

Navigate back to your editor. For the final step, update your `setupControls` to move the player depending on camera rotation. Here, we replace the `console.log` with `movePlayerTo` invocations.

<pre><code class="language-javascript">function setupControls() {
  AFRAME.registerComponent('lane-controls', {
    tick: function (time, timeDelta) {
      var rotation = this.el.object3D.rotation;

      if      (rotation.y > 0.1)  movePlayerTo(0);
      else if (rotation.y < -0.1) movePlayerTo(2);
      else                        movePlayerTo(1);
    }
  })
}
</code></pre>

Ensure that your `assets/ergo.js` matches the [corresponding file in the Step 3 source code](https://github.com/alvinwan/ergo/blob/master/tutorial/step_3_controls/assets/ergo.js). Navigate back to your preview. Rotate the camera from side to side, and your player will now track the user’s rotation.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/730f6a49-28ad-4665-9a69-9789f51c882c/vr-endless-runner-game-7-p1-s3.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/730f6a49-28ad-4665-9a69-9789f51c882c/vr-endless-runner-game-7-p1-s3.gif" width="800" alt="Controlling game character with head rotation" /></a><figcaption>Controlling game character with head rotation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/730f6a49-28ad-4665-9a69-9789f51c882c/vr-endless-runner-game-7-p1-s3.gif">Large preview</a>)</figcaption></figure>

This concludes gaze controls for your virtual reality endless runner game.

In this section, we learned how to use A-Frame components and saw how to modify A-Frame entity properties. This also concludes part 1 of our endless runner game tutorial. You now have a virtual reality model equipped with aesthetic improvements like low-poly stylization and animations, in addition to a virtual-reality-headset-friendly gaze control for players to use.

## Conclusion

We created a simple, interactive virtual reality model, as a start for our VR endless runner game. We covered a number of A-Frame concepts such as primitives, animations, and components &mdash; all of which are necessary for building a game on top of A-Frame VR.

Here are extra resources and next steps for working more with these technologies:

- [A-Frame VR](https://aframe.io/docs)
Official documentation for A-Frame VR, covering the topics used above in more detail.
- [A-Frame Homepage](https://aframe.io)
Examples of A-Frame projects, exhibiting different A-Frame capabilities.
- [Low-Poly Island](https://alvinwan.com/vr/low-poly-island/)
VR model using the same lighting, textures, and animations as the ones used for this endless runner game.

In the [next part](https://www.smashingmagazine.com/2019/03/virtual-reality-endless-runner-game-vr-part-2/) of this article series, I’ll show you how you can implement the game’s core logic and use more advanced A-Frame VR scene manipulations in JavaScript.

{{< signature "rb, ra, il" >}}
