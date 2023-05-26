---
title: 'How To Build A Virtual Reality Model With A Real-Time Cross-Device Preview'
slug: virtual-reality-model-real-time-cross-device-preview
author: alvin-wan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b73b0d3-d89b-49b0-a863-a0b24fa4e4be/shift-800w.png
date: 2018-11-06T23:50:16+01:00
summary: >-
  In this tutorial, we’ll program three-dimensional objects and add simple interactions to these objects. Additionally, you can learn how to build a simple message passing system between clients and servers.
description: >-
  In this tutorial, we’ll program three-dimensional objects and add simple interactions to these objects. Additionally, you can learn how to build a simple message passing system between clients and servers.
categories:
  - Virtual Reality
  - User Interaction
  - UX
  - UI
---
Virtual reality (VR) is an experience based in a computer-generated environment; a number of different VR products make headlines and its applications range far and wide: for the winter Olympics, the US team utilized virtual reality for athletic training; surgeons are experimenting with virtual reality for medical training; and most commonly, virtual reality is being applied to games.

We will focus on the last category of applications and will specifically focus on **point-and-click adventure games**. Such games are a casual class of games; the goal is to point and click on objects in the scene, to finish a puzzle. In this tutorial, we will build a simple version of such a game but in virtual reality. This serves as an introduction to programming in three dimensions and is a self-contained getting-started guide to deploying a virtual reality model on the web. You will be building with webVR, a framework that gives a dual advantage &mdash; users can play your game in VR and users without a VR headset can still play your game on a phone or desktop.

<div class="c-felix-the-cat">
<h4 class="h3">Developing For Virtual Reality</h4>
<p>Any developer can create content for VR nowadays. To get a better understanding of VR development, working a demo project can help. <a href="https://www.smashingmagazine.com/2016/09/developing-for-virtual-reality-what-we-learned/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

In the second half of these tutorial, you will then build a "mirror" for your desktop. This means that all movements the player makes on a mobile device will be mirrored in a desktop preview. This allows you see what the player sees, allowing you to provide guidance, record the game, or simply keep guests entertained.

## Prerequisites

To get started, you will need the following. For the second half of this tutorial, you will need a Mac OSX. Whereas the code can apply to any platform, the dependency installation instructions below are for Mac.

- Internet access, specifically to [glitch.com](https://glitch.com);
- A virtual reality headset (optional, recommended). I use Google Cardboard, which is offered at $15 a piece.

{{% feature-panel %}}

## Step 1: Setting Up A Virtual Reality (VR) Model

In this step, we will set up a website with a single static HTML page. This allows us to code from your desktop and automatically deploy to the web. The deployed website can then be loaded on your mobile phone and placed inside a VR headset. Alternatively, the deployed website can be loaded by a standalone VR headset. Get started by navigating to [glitch.com](https://glitch.com/). Then,

1. Click on "New Project" in the top-right.
2. Click on "hello-express" in the drop-down.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b74faa49-00f9-4551-aa3a-1d04b02d4fb2/1-glitch-create.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b74faa49-00f9-4551-aa3a-1d04b02d4fb2/1-glitch-create.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b74faa49-00f9-4551-aa3a-1d04b02d4fb2/1-glitch-create.png'>Large preview</a>)" alt="Get started by navigating to glitch.com" >}}

Next, click on *views/index.html* in the left sidebar. We will refer to this as your “editor”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ac9e4ed-ebdb-48c4-bba4-18e849b7078a/1-glitch-index.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ac9e4ed-ebdb-48c4-bba4-18e849b7078a/1-glitch-index.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ac9e4ed-ebdb-48c4-bba4-18e849b7078a/1-glitch-index.png'>Large preview</a>)" alt="The next step would be to click on views/index.html in the left sidebar which will be referred to this as your “editor”." >}}

To preview the webpage, click on "Preview" in the top left. We will refer to this as your *preview*. Note that any changes in your editor will be automatically reflected in this preview, barring bugs or unsupported browsers.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59257af-1efa-46cb-8d50-559db30bd228/01-building-a-point-and-click-virtual-reality-game.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59257af-1efa-46cb-8d50-559db30bd228/01-building-a-point-and-click-virtual-reality-game.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59257af-1efa-46cb-8d50-559db30bd228/01-building-a-point-and-click-virtual-reality-game.png'>Large preview</a>)" alt="To preview the webpage, click on “Preview” in the top left. We will refer to this as your preview. Note that any changes in your editor will be automatically reflected in this preview, barring bugs or unsupported browsers." >}}

Back in your editor, replace the current HTML with the following boilerplate for a VR model.

<div class="break-out">

<pre><code class="language-html">&lt;!DOCTYPE html>
&lt;html>
  &lt;head>
      &lt;script src="https://aframe.io/releases/0.7.0/aframe.min.js">&lt;/script>
  &lt;/head>
  &lt;body>
    &lt;a-scene>

      &lt;!-- blue sky -->
      &lt;a-sky color="#a3d0ed">&lt;/a-sky>

      &lt;!-- camera with wasd and panning controls -->
      &lt;a-entity camera look-controls wasd-controls position="0 0.5 2" rotation="0 0 0">&lt;/a-entity>

      &lt;!-- brown ground -->
      &lt;a-box shadow id="ground" shadow="receive:true" color="#847452" width="10" height="0.1" depth="10">&lt;/a-box>

      &lt;!-- start code here -->
      &lt;!-- end code here -->
    &lt;/a-scene>
  &lt;/body>
&lt;/html>
</code></pre></div>

Navigate see the following.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6252192-ff00-48dc-bac2-3759bbd0c8f8/1-preview.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6252192-ff00-48dc-bac2-3759bbd0c8f8/1-preview.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6252192-ff00-48dc-bac2-3759bbd0c8f8/1-preview.png'>Large preview</a>)" alt="When navigating back to your preview, you will see the bakground colors blue and brown." >}}

To preview this on your VR headset, use the URL in the omnibar. In the picture above, the URL is `https://point-and-click-vr-game.glitch.me/`. Your working environment is now set up; feel free to share this URL with family and friends. In the next step, you will create a virtual reality model.

{{% ad-panel-leaderboard %}}

## Step 2: Build A Tree Model

You will now create a tree, using *primitives* from [aframe.io](https://aframe.io). These are standard objects that Aframe has pre-programmed for ease of use. Specifically, Aframe refers to objects as *entities*. There are three concepts, related to all entities, to organize our discussion around:

1. Geometry and material,
2. Transformation Axes,
3. Relative Transformations.

First, **geometry** and **material** are two building blocks of all three-dimensional objects in code. The geometry defines the "shape" &mdash; a cube, a sphere, a pyramid, and so on. The material defines static properties of the shape, such as color, reflectiveness, roughness.

Aframe simplifies this concept for us by defining primitives, such as `<a-box>`, `<a-sphere>`, `<a-cylinder>` and many others to make a specification of a geometry and its material simpler. Start by defining a green sphere. On line 19 in your code, right after `<!-- start code here -->`, add the following.

<div class="break-out">

<pre><code class="language-css">
      &lt;!-- start code here -->
      &lt;a-sphere color="green" radius="0.5">&lt;/a-sphere>  &lt;!-- new line -->
      &lt;!-- end code here -->
</code></pre></div>

Second, there are three axes to **transform** our object along. The `x` axis runs horizontally, where x values increase as we move right. The `y` axis runs vertically, where y values increase as we move up. The `z` axis runs out of your screen, where z values increase as we move towards you. We can translate, rotate, or scale entities along these three axes.

For example, to translate an object "right," we increase its x value. To spin an object like a top, we rotate it along the y-axis. Modify line 19 to move the sphere "up" &mdash; this means you need to increase the sphere's y value. Note that all transformations are specified as `<x> <y> <z>`, meaning to increase its y value, you need to increase the second value. By default, all objects are located at position 0, 0, 0. Add the `position` specification below.

<div class="break-out">

<pre><code class="language-css">
      &lt;!-- start code here -->
      &lt;a-sphere color="green" radius="0.5" position="0 1 0">&lt;/a-sphere> &lt;!-- edited line -->
      &lt;!-- end code here -->
</code></pre></div>

Third, all transformations are **relative** to its parent. To add a trunk to your tree, add a cylinder inside of the sphere above. This ensures that the position of your trunk is relative to the sphere's position. In essence, this keeps your tree together as one unit. Add the `<a-cylinder>` entity between the `<a-sphere ...>` and `</a-sphere>` tags.

<div class="break-out">

<pre><code class="language-css">
      &lt;a-sphere color="green" radius="0.5" position="0 1 0">
        &lt;a-cylinder color="#84651e" position="0 -0.9 0" radius="0.05">&lt;/a-cylinder> &lt;!-- new line -->
      &lt;/a-sphere>
</code></pre></div>

To make this treeless barebones, add more foliage, in the form of two more green spheres.

<div class="break-out">

<pre><code class="language-css">
      &lt;a-sphere color="green" radius="0.5" position="0 0.75 0">
        &lt;a-cylinder color="#84651e" position="0 -0.9 0" radius="0.05">&lt;/a-cylinder>
        &lt;a-sphere color="green" radius="0.35" position="0 0.5 0">&lt;/a-sphere> &lt;!-- new line -->
        &lt;a-sphere color="green" radius="0.2" position="0 0.8 0">&lt;/a-sphere> &lt;!-- new line -->
      &lt;/a-sphere>
</code></pre></div>

Navigate back to your preview, and you will see the following tree:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3d4c67a-4c16-4c50-9a78-66f7c34c54df/2-tree.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3d4c67a-4c16-4c50-9a78-66f7c34c54df/2-tree.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3d4c67a-4c16-4c50-9a78-66f7c34c54df/2-tree.png'>Large preview</a>)" alt="When navigating back to your preview, you will now be able to see a green tree placed in your background." >}}

Reload the website preview on your VR headset, and check out your new tree. In the next section, we will make this tree interactive.

{{% ad-panel-leaderboard %}}

## Step 3: Add Click Interaction To Model

To make an entity interactive, you will need to:

- Add an animation,
- Have this animation trigger on click. 

Since the end user is using a virtual reality headset, clicking is equivalent to staring: in other words, stare at an object to "click" on it. To effect these changes, you will start with the cursor. Redefine the camera, by replacing line 13 with the following.

<div class="break-out">

<pre><code class="language-html">&lt;a-entity camera look-controls wasd-controls position="0 0.5 2" rotation="0 0 0"&gt;
  &lt;a-entity cursor="fuse: true; fuseTimeout: 250"
            position="0 0 -1"
            geometry="primitive: ring; radiusInner: 0.02; radiusOuter: 0.03"
            material="color: black; shader: flat"
            scale="0.5 0.5 0.5"
            raycaster="far: 20; interval: 1000; objects: .clickable"&gt;
    &lt;!-- add animation here --&gt;
  &lt;/a-entity&gt;
&lt;/a-entity&gt;
</code></pre></div>

The above adds a cursor that can trigger the clicking action. Note the `objects: .clickable` property. This means that all objects with the class "clickable" will trigger the animation and receive a "click" command where appropriate. You will also add an animation to the click cursor, so that users know when the cursor triggers a click. Here, the cursor will shrink slowly when pointing at a clickable object, snapping after a second to denote an object has been clicked. Replace the comment `<!-- add animation here -->` with the following code:

<div class="break-out">

<pre><code class="language-html">&lt;a-animation begin="fusing" easing="ease-in" attribute="scale"
  fill="backwards" from="1 1 1" to="0.2 0.2 0.2" dur="250"&gt;&lt;/a-animation&gt;
</code></pre></div>

Move the tree to the right by 2 units and add class "clickable" to the tree, by modifying line 29 to match the following.

<div class="break-out">

<pre><code class="language-html">&lt;a-sphere color="green" radius="0.5" position="2 0.75 0" class="clickable"&gt;
</code></pre></div>

Next, you will:

* Specify an animation,
* Trigger the animation with a click. 

Due to Aframe's easy-to-use animation entity, both steps can be done in quick succession.

Add an `<a-animation>` tag on line 33, right after the `<a-cylinder>` tag but before the end of the `</a-sphere>`.

<div class="break-out">

<pre><code class="language-html">&lt;a-animation begin="click" attribute="position" from="2 0.75 0" to="2.2 0.75 0" fill="both" direction="alternate" repeat="1"&gt;&lt;/a-animation&gt;
</code></pre></div>

The above properties specify a number of configurations for the animation. The animation:

- Is triggered by the `click` event
- Modifies the tree's `position`
- Starts from the original position `2 0.75 0`
- Ends in `2.2 0.75 0` (moving 0.2 units to the right)
- Animates when traveling to and from the destination
- Alternates animation between traveling to and from the destination
- Repeats this animation once. This means the object animates twice in total &mdash; once to the destination and once back to the original position.

Finally, navigate to your preview, and drag from the cursor to your tree. Once the black circle rests on the tree, the tree will move to the right and back.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd4c95c-63e1-45d6-8bd4-e0c234014623/3-click.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac3c18f0-3c20-4443-b281-a2db67a26a5e/3-click-800w.gif" width=“800" height="469" alt="Once the black circle rests on the tree, the tree will move to the right and back." /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd4c95c-63e1-45d6-8bd4-e0c234014623/3-click.gif">Large preview</a></figcaption></figure>

This concludes the basics needed to build a point-and-click adventure game, in virtual reality. To view and play a more complete version of this game, see the following [short scene](https://alvinwan.com/shift/scenes/1/). The mission is to open the gate and hide the tree behind the gate, by clicking on various objects in the scene.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81b2a884-a89a-4d14-9189-8c78498f5f51/shift.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81b2a884-a89a-4d14-9189-8c78498f5f51/shift.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81b2a884-a89a-4d14-9189-8c78498f5f51/shift.png'>Large preview</a>)" alt="The mission is to open the gate and hide the tree behind the gate, by clicking on various objects in the scene." >}}

Next, we set up a simple nodeJS server to serve our static demo.

## Step 4: Setup NodeJS Server

In this step, we will set up a basic, functional nodeJS server that serves your existing VR model. In the left sidebar of your editor, select `package.json`. 

Start by deleting lines 2-4.

<div class="break-out">

<pre><code class="language-javascript">"//1": "describes your app and its dependencies",
"//2": "https://docs.npmjs.com/files/package.json",
"//3": "updating this file will download and update your packages", 
</code></pre></div>

Change the name to `mirrorvr`.

<pre><code class="language-javascript">{
  "name": "mirrorvr", // change me
  "version": "0.0.1",
  ...
</code></pre>

Under `dependencies`, add `socket.io`.

<pre><code class="language-javascript">"dependencies": {
  "express": "^4.16.3",
  "socketio": "^1.0.0",
},
</code></pre>

Update the repository URL to match your current glitch's. The example glitch project is named `point-and-click-vr-game`. Replace that with your glitch project's name.

<div class="break-out">

<pre><code class="language-javascript">"repository": {
  "url": "https://glitch.com/edit/#!/point-and-click-vr-game"
},
</code></pre></div>

Finally, Change the `"glitch"` tag to `"vr"`.

<pre><code class="language-javascript">"keywords": [
  "node",
  "vr",  // change me
  "express"
]
</code></pre>

Double check that your `package.json` now matches the following.

<div class="break-out">

<pre><code class="language-javascript">{
  "name": "mirrorvr",
  "version": "0.0.1",
  "description": "Mirror virtual reality models",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.16.3",
    "socketio": "^1.0.0"
  },
  "engines": {
    "node": "8.x"
  },
  "repository": {
    "url": "https://glitch.com/edit/#!/point-and-click-vr-game"
  },
  "license": "MIT",
  "keywords": [
    "node",
    "vr",
    "express"
  ]
}
</code></pre></div>

Double check that your code from the previous parts matches the following, in `views/index.html`.

<div class="break-out">

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
      &lt;script src="https://aframe.io/releases/0.7.0/aframe.min.js"&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;a-scene&gt;

      &lt;!-- blue sky --&gt;
      &lt;a-sky color="#a3d0ed"&gt;&lt;/a-sky&gt;

      &lt;!-- camera with wasd and panning controls --&gt;
      &lt;a-entity camera look-controls wasd-controls position="0 0.5 2" rotation="0 0 0"&gt;
        &lt;a-entity cursor="fuse: true; fuseTimeout: 250"
                  position="0 0 -1"
                  geometry="primitive: ring; radiusInner: 0.02; radiusOuter: 0.03"
                  material="color: black; shader: flat"
                  scale="0.5 0.5 0.5"
                  raycaster="far: 20; interval: 1000; objects: .clickable"&gt;
            &lt;a-animation begin="fusing" easing="ease-in" attribute="scale"
               fill="backwards" from="1 1 1" to="0.2 0.2 0.2" dur="250"&gt;&lt;/a-animation&gt;
        &lt;/a-entity&gt;
      &lt;/a-entity&gt;

      &lt;!-- brown ground --&gt;
      &lt;a-box shadow id="ground" shadow="receive:true" color="#847452" width="10" height="0.1" depth="10"&gt;&lt;/a-box&gt;

      &lt;!-- start code here --&gt;
      &lt;a-sphere color="green" radius="0.5" position="2 0.75 0" class="clickable"&gt;
        &lt;a-cylinder color="#84651e" position="0 -0.9 0" radius="0.05"&gt;&lt;/a-cylinder&gt;
        &lt;a-sphere color="green" radius="0.35" position="0 0.5 0"&gt;&lt;/a-sphere&gt;
        &lt;a-sphere color="green" radius="0.2" position="0 0.8 0"&gt;&lt;/a-sphere&gt;
        &lt;a-animation begin="click" attribute="position" from="2 0.75 0" to="2.2 0.75 0" fill="both" direction="alternate" repeat="1"&gt;&lt;/a-animation&gt;
      &lt;/a-sphere&gt;
      &lt;!-- end code here --&gt;
    &lt;/a-scene&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre></div>

Modify the existing `server.js`.

Start by importing several NodeJS utilities.

- **Express**  
This is the web framework we will use to run the server.
- **http**  
This allows us to launch a daemon, listening for activity on various ports.
- **socket.io**  
The sockets implementation that allows us to communicate between client-side and server-side in nearly real-time.

While importing these utilities, we additionally initialize the ExpressJS application. Note the first two lines are already written for you.

<pre><code class="language-javascript">var express = require('express');
var app = express();

/* start new code */
var http = require('http').Server(app);
var io = require('socket.io')(http);
/* end new code */

// we've started you off with Express, 
</code></pre>

With the utilities loaded, the provided server next instructs the server to return `index.html` as the homepage. Note there is no new code written below; this is simply an explanation of the existing source code.

<pre><code class="language-javascript">// https://expressjs.com/en/starter/basic-routing.html
app.get('/', function(request, response) {
  response.sendFile(__dirname + '/views/index.html');
});
</code></pre>

Finally, the existing source code instructs the application to bind to and listen to a port, which is 3000 by default unless specified otherwise.

<div class="break-out">

<pre><code class="language-javascript">// listen for requests :)
var listener = app.listen(process.env.PORT, function() {
  console.log('Your app is listening on port ' + listener.address().port);
});
</code></pre></div>

Once you are finished editing, Glitch automatically reloads the server. Click on "Show" in the top-left to preview your application.

Your web application is now up and running. Next, we will send messages from the client to the server.

## Step 5: Send Information From Client To Server

In this step, we will use the client to initialize a connection with the server. The client will additionally inform the server if it is a phone or a desktop. To start, import the soon-to-exist Javascript file in your `views/index.html`.

After line 4, include a new script.

<div class="break-out">

<pre><code class="language-html">&lt;script src="/client.js" type="text/javascript"&gt;&lt;/script&gt;
</code></pre></div>

On line 14, add `camera-listener` to the list of properties for the camera entity.

<pre><code class="language-html">&lt;a-entity camera-listener camera look-controls...&gt;
    ...
&lt;/a-entity&gt;
</code></pre>

Then, navigate to `public/client.js` in the left sidebar. Delete all Javascript code in this file. Then, define a utility function that checks if the client is a mobile device.

<div class="break-out">

<pre><code class="language-javascript">/**
 * Check if client is on mobile
 */
function mobilecheck() {
  var check = false;
  (function(a){if(/(android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox|netfront|opera m(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows ce|xda|xiino/i.test(a)||/1207|6310|6590|3gso|4thp|50[1-6]i|770s|802s|a wa|abac|ac(er|oo|s\-)|ai(ko|rn)|al(av|ca|co)|amoi|an(ex|ny|yw)|aptu|ar(ch|go)|as(te|us)|attw|au(di|\-m|r |s )|avan|be(ck|ll|nq)|bi(lb|rd)|bl(ac|az)|br(e|v)w|bumb|bw\-(n|u)|c55\/|capi|ccwa|cdm\-|cell|chtm|cldc|cmd\-|co(mp|nd)|craw|da(it|ll|ng)|dbte|dc\-s|devi|dica|dmob|do(c|p)o|ds(12|\-d)|el(49|ai)|em(l2|ul)|er(ic|k0)|esl8|ez([4-7]0|os|wa|ze)|fetc|fly(\-|_)|g1 u|g560|gene|gf\-5|g\-mo|go(\.w|od)|gr(ad|un)|haie|hcit|hd\-(m|p|t)|hei\-|hi(pt|ta)|hp( i|ip)|hs\-c|ht(c(\-| |_|a|g|p|s|t)|tp)|hu(aw|tc)|i\-(20|go|ma)|i230|iac( |\-|\/)|ibro|idea|ig01|ikom|im1k|inno|ipaq|iris|ja(t|v)a|jbro|jemu|jigs|kddi|keji|kgt( |\/)|klon|kpt |kwc\-|kyo(c|k)|le(no|xi)|lg( g|\/(k|l|u)|50|54|\-[a-w])|libw|lynx|m1\-w|m3ga|m50\/|ma(te|ui|xo)|mc(01|21|ca)|m\-cr|me(rc|ri)|mi(o8|oa|ts)|mmef|mo(01|02|bi|de|do|t(\-| |o|v)|zz)|mt(50|p1|v )|mwbp|mywa|n10[0-2]|n20[2-3]|n30(0|2)|n50(0|2|5)|n7(0(0|1)|10)|ne((c|m)\-|on|tf|wf|wg|wt)|nok(6|i)|nzph|o2im|op(ti|wv)|oran|owg1|p800|pan(a|d|t)|pdxg|pg(13|\-([1-8]|c))|phil|pire|pl(ay|uc)|pn\-2|po(ck|rt|se)|prox|psio|pt\-g|qa\-a|qc(07|12|21|32|60|\-[2-7]|i\-)|qtek|r380|r600|raks|rim9|ro(ve|zo)|s55\/|sa(ge|ma|mm|ms|ny|va)|sc(01|h\-|oo|p\-)|sdk\/|se(c(\-|0|1)|47|mc|nd|ri)|sgh\-|shar|sie(\-|m)|sk\-0|sl(45|id)|sm(al|ar|b3|it|t5)|so(ft|ny)|sp(01|h\-|v\-|v )|sy(01|mb)|t2(18|50)|t6(00|10|18)|ta(gt|lk)|tcl\-|tdg\-|tel(i|m)|tim\-|t\-mo|to(pl|sh)|ts(70|m\-|m3|m5)|tx\-9|up(\.b|g1|si)|utst|v400|v750|veri|vi(rg|te)|vk(40|5[0-3]|\-v)|vm40|voda|vulc|vx(52|53|60|61|70|80|81|83|85|98)|w3c(\-| )|webc|whit|wi(g |nc|nw)|wmlb|wonu|x700|yas\-|your|zeto|zte\-/i.test(a.substr(0,4))) check = true;})(navigator.userAgent||navigator.vendor||window.opera);
  return check;
};
</code></pre></div>

Next, we will define a series of initial messages to exchange with the server side. Define a new socket.io object to represent the client's connection to the server. Once the socket connects, log a message to the console.

<pre><code class="language-javascript">var socket = io();

socket.on('connect', function() {
  console.log(' * Connection established');
});
</code></pre>

Check if the device is mobile, and send corresponding information to the server, using the function `emit`.

<pre><code class="language-javascript">if (mobilecheck()) {
  socket.emit('newHost');
} else {
  socket.emit('newMirror');
}
</code></pre>

This concludes the client's message sending. Now, amend the server code to receive this message and react appropriately. Open the server `server.js` file.

Handle new connections, and immediately listen for the type of client. At the end of the file, add the following.

<pre><code class="language-javascript">/**
 * Handle socket interactions
 */

io.on('connection', function(socket) {

  socket.on('newMirror', function() {
    console.log(" * Participant registered as 'mirror'")
  });

  socket.on('newHost', function() {
    console.log(" * Participant registered as 'host'");
  });
});
</code></pre>

Again, preview the application by clicking on "Show" in the top left. Load that same URL on your mobile device. In your terminal, you will see the following.

<pre><code class="language-javascript">listening on *: 3000
 * Participant registered as 'host'
 * Participant registered as 'mirror'
</code></pre>

This is the first of simple message-passing, where our client sends information back to the server. Quit the running NodeJS process. For the final part of this step, we will have the client send camera information back to the server. Open `public/client.js`.

At the very end of the file, include the following.

<pre><code class="language-javascript">var camera;
if (mobilecheck()) {
  AFRAME.registerComponent('camera-listener', {
    tick: function () {
      camera = this.el.sceneEl.camera.el;
      var position = camera.getAttribute('position');
      var rotation = camera.getAttribute('rotation');
      socket.emit('onMove', {
        "position": position,
        "rotation": rotation
      });
    }
  });
}
</code></pre>

Save and close. Open your server file `server.js` to listen for this `onMove` event.

Add the following, in the `newHost` block of your socket code. 

<pre><code class="language-javascript">socket.on('newHost', function() {
    console.log(" * Participant registered as 'host'");
    /* start new code */
    socket.on('onMove', function(data) {
      console.log(data);
    });
    /* end new code */
  });
</code></pre>

Once again, load the preview on your desktop and on your mobile device. Once a mobile client is connected, the server will immediately begin logging camera position and rotation information, sent from the client to the server. Next, you will implement the reverse, where you send information from the server back to the client.

## Step 6: Send Information From Server To Client

In this step, you will send a host's camera information to all mirrors. Open your main server file, `server.js`.

Change the `onMove` event handler to the following:

<pre><code class="language-javascript">socket.on('onMove', function(data) {
  console.log(data);  // delete me
  socket.broadcast.emit('move', data)
});
</code></pre>

The `broadcast` modifier ensures that the server sends this information to all clients connected to the socket, except for the original sender. Once this information is sent to a client, you then need to set the mirror's camera accordingly. Open the client script, `public/client.js`.

Here, check if the client is a desktop. If so, receive the move data and log accordingly.

<pre><code class="language-javascript">if (!mobilecheck()) {
  socket.on('move', function(data) {
    console.log(data);
  });
}
</code></pre>

Load the preview on your desktop and on your mobile device. In your desktop browser, open the developer console. Then, load the app on your mobile phone. As soon as the mobile phone loads the app, the developer console on your desktop should light up with camera position and rotation.

Open the client script once more, at `public/client.js`. We finally adjust the client camera depending on the information sent.

Amend the event handler above for the `move` event.

<pre><code class="language-javascript">socket.on('move', function(data) {
  /* start new code */
  camera.setAttribute('rotation', data["rotation"]);
  camera.setAttribute('position', data["position"]);
  /* end new code */
});
</code></pre>

Load the app on your desktop and your phone. Every movement of your phone is reflected in the corresponding mirror on your desktop! This concludes the mirror portion of your application. As a desktop user, you can now preview what your mobile user sees. The concepts introduced in this section will be crucial for further development of this game, as we transform a single-player to a multiplayer game.

## Conclusion

In this tutorial, we programmed three-dimensional objects and added simple interactions to these objects. Additionally, you built a simple message passing system between clients and servers, to effect a desktop preview of what your mobile users see.

These concepts extend beyond even webVR, as the notion of a geometry and material extend to SceneKit on iOS (which is related to ARKit), Three.js (the backbone for Aframe), and other three-dimensional libraries. These simple building blocks put together allow us ample flexibility in creating a fully-fledged point-and-click adventure game. More importantly, they allow us to create any game with a click-based interface.

Here are several resources and examples to further explore:

- [MirrorVR](https://mirrorvr.alvinwan.com)  
A fully-fledged implementation of the live preview built above. With just a single Javascript link, add a live preview of any virtual reality model on mobile to a desktop.
- [Bit by Bit](https://littlebitbybit.org/gallery/)  
A gallery of kids’ drawings and each drawing's corresponding virtual reality model.
- [Aframe](https://aframe.io)  
Examples, developer documentation, and more resources for virtual reality development.
- [Google Cardboard Experiences](https://edu.google.com/expeditions/#about)  
Experiences for the classroom with custom tools for educators.

Next time, we will build a complete game, using web sockets to facilitate real-time communication between players in a virtual reality game. Feel free to share your own models in the comments below.

{{< signature "rb, ra, yk, il" >}}
