---
title: 'How To Build An Endless Runner Game In Virtual Reality (Part 2)'
slug: virtual-reality-endless-runner-game-vr-part-2
author: alvin-wan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8858c709-72cc-40d3-a387-ed6c18021bdf/sharing-card-endless-runner-game-vr-alvin-wan.png
date: 2019-03-13T12:00:35+01:00
summary: >-
  If you’ve ever wondered how games with keyboard-less support for VR headsets are built, then this tutorial explains just what you’re looking for. Here’s how you too can bring a basic, functioning VR game to life.
description: >-
  If you’ve ever wondered how games with keyboard-less support for VR headsets are built, then this tutorial explains just what you’re looking for. Here’s how you too can bring a basic, functioning VR game to life.
categories:
  - Virtual Reality
  - User Interaction
  - UX
  - UI 
---
In [Part 1](https://www.smashingmagazine.com/2019/03/virtual-reality-endless-runner-game-vr-part-1/) of this series, we’ve seen how a virtual reality model with lighting and animation effects can be created. In this part, we will implement the game’s core logic and utilize more advanced A-Frame environment manipulations to build the “game” part of this application. By the end, you will have a functioning virtual reality game with a real challenge.

This tutorial involves a number of steps, including (but not limited to) collision detection and more A-Frame concepts such as mixins.

- [Demo of the final product](https://ergo-2.glitch.me)

## Prerequisites

Just like in the previous tutorial, you will need the following:

- Internet access (specifically to [glitch.com](https://glitch.com));
- A Glitch project completed from [part 1](https://www.smashingmagazine.com/2019/03/virtual-reality-endless-runner-game-vr-part-1/). (You can continue from the finished product by navigating to [https://glitch.com/edit/#!/ergo-1](https://glitch.com/edit/#!/ergo-1) and clicking “Remix to edit”;
- A virtual reality headset (optional, recommended). (I use Google Cardboard, which is offered at $15 a piece.)

{{% feature-panel %}}

## Step 1: Designing The Obstacles

In this step, you design the trees that we will use as obstacles. Then, you will add a simple animation that moves the trees towards the player, like the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d89663-74dc-4ab5-b4e7-75440e270272/2-how-to-build-an-endless-runner-game-in-virtual-reality.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d598e2f3-5336-41ff-9738-7323b4667a27/2-how-t0-build-an-endless-runner-game-in-virtual-reality-800w.gif" width="800" height="368" alt="Template trees moving towards player" /></a><figcaption>Template trees moving towards player (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d89663-74dc-4ab5-b4e7-75440e270272/2-how-to-build-an-endless-runner-game-in-virtual-reality.gif">Large preview</a>)
</figcaption></figure>

These trees will serve as templates for obstacles you generate during the game. For the final part of this step, we will then remove these "template trees".

To start, add a number of different **A-Frame mixins**. Mixins are commonly-used sets of component properties. In our case, all of our trees will have the same color, height, width, depth etc. In other words, all your trees will look the same and therefore will use a few shared mixins.

**Note**: *In our tutorial, your only assets will be mixins. Visit the [A-Frame Mixins page](https://aframe.io/docs/0.8.0/core/mixins.html) to learn more.*

In your editor, navigate to *index.html*. Right after your sky and before your lights, add a new A-Frame entity to hold your assets:

<pre><code class="language-html">&lt;a-sky...&gt;&lt;/a-sky&gt;

&lt;!-- Mixins --&gt;
&lt;a-assets&gt;
&lt;/a-assets&gt;

&lt;!-- Lights --&gt;
...
</code></pre>

In your new `a-assets` entity, start by adding a mixin for your foliage. This mixins defines common properties for the foliage of the template tree. In short, it is a white, flat-shaded pyramid, for a low poly effect.

<pre><code class="language-css">&lt;a-assets&gt;
  &lt;a-mixin id="foliage" geometry="
      primitive: cone;
      segments-height: 1;
      segments-radial:4;
      radius-bottom:0.3;"
     material="color:white;flat-shading: true;"&gt;&lt;/a-mixin&gt;
&lt;/a-assets&gt;
</code></pre>

Just below your foliage mixin, add a mixin for the trunk. This trunk will be a small, white rectangular prism.

<pre><code class="language-css">&lt;a-assets&gt;
  ...
  &lt;a-mixin id="trunk" geometry="
      primitive: box;
      height:0.5;
      width:0.1;
      depth:0.1;"
     material="color:white;"&gt;&lt;/a-mixin&gt;
&lt;/a-assets&gt;
</code></pre>

Next, add the template tree objects that will use these mixins. Still in *index.html*, scroll down to the platforms section. Right before the player section, add a new tree section, with three empty tree entities:

<pre><code class="language-html">&lt;a-entity id="tree-container" ...&gt;

  &lt;!-- Trees --&gt;
  &lt;a-entity id="template-tree-center"&gt;&lt;/a-entity&gt;
  &lt;a-entity id="template-tree-left"&gt;&lt;/a-entity&gt;
  &lt;a-entity id="template-tree-right"&gt;&lt;/a-entity&gt;

  &lt;!-- Player --&gt;
  ...
</code></pre>

Next, reposition, rescale, and add shadows to the tree entities.

<div class="break-out">

<pre><code class="language-css">&lt;!-- Trees --&gt;
&lt;a-entity id="template-tree-center" shadow scale="0.3 0.3 0.3" position="0 0.6 0"&gt;&lt;/a-entity&gt;
&lt;a-entity id="template-tree-left" shadow scale="0.3 0.3 0.3" position="0 0.6 0"&gt;&lt;/a-entity&gt;
&lt;a-entity id="template-tree-right" shadow scale="0.3 0.3 0.3" position="0 0.6 0"&gt;&lt;/a-entity&gt;
</code></pre>
</div>

Now, populate the tree entities with a trunk and foliage, using the mixins we defined previously.

<div class="break-out">

<pre><code class="language-css">&lt;!-- Trees --&gt;
&lt;a-entity id="template-tree-center" ...&gt;
  &lt;a-entity mixin="foliage"&gt;&lt;/a-entity&gt;
  &lt;a-entity mixin="trunk" position="0 -0.5 0"&gt;&lt;/a-entity&gt;
&lt;/a-entity&gt;
&lt;a-entity id="template-tree-left" ...&gt;
  &lt;a-entity mixin="foliage"&gt;&lt;/a-entity&gt;
  &lt;a-entity mixin="trunk" position="0 -0.5 0"&gt;&lt;/a-entity&gt;
&lt;/a-entity&gt;
&lt;a-entity id="template-tree-right" ...&gt;
  &lt;a-entity mixin="foliage"&gt;&lt;/a-entity&gt;
  &lt;a-entity mixin="trunk" position="0 -0.5 0"&gt;&lt;/a-entity&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Navigate to your preview, and you should now see the following template trees.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/668ec49c-6ce9-478b-9f65-e1a5c38f927a/3-how-to-build-an-endless-runner-game-in-virtual-reality.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/668ec49c-6ce9-478b-9f65-e1a5c38f927a/3-how-to-build-an-endless-runner-game-in-virtual-reality.png" sizes="100vw" caption="Template trees for obstacles (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/668ec49c-6ce9-478b-9f65-e1a5c38f927a/3-how-to-build-an-endless-runner-game-in-virtual-reality.png'>Large preview</a>)" alt="Template trees for obstacles" >}}

Now, animate the trees from a distant location on the platform towards the user. As before, use the `a-animation` tag:

<div class="break-out">

<pre><code class="language-css">&lt;!-- Trees --&gt;
&lt;a-entity id="template-tree-center" ...&gt;
  ...
  &lt;a-animation attribute="position" ease="linear" from="0 0.6 -7" to="0 0.6 1.5" dur="5000"&gt;&lt;/a-animation&gt;
&lt;/a-entity&gt;
&lt;a-entity id="template-tree-left" ...&gt;
  ...
  &lt;a-animation attribute="position" ease="linear" from="-0.5 0.55 -7" to="-0.5 0.55 1.5" dur="5000"&gt;&lt;/a-animation&gt;
&lt;/a-entity&gt;
&lt;a-entity id="template-tree-right" ...&gt;
  ...
  &lt;a-animation attribute="position" ease="linear" from="0.5 0.55 -7" to="0.5 0.55 1.5" dur="5000"&gt;&lt;/a-animation&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Ensure that your code matches the following.

<div class="break-out">

<pre><code class="language-css">&lt;a-entity id="tree-container"...&gt;

&lt;!-- Trees --&gt;
&lt;a-entity id="template-tree-center" shadow scale="0.3 0.3 0.3" position="0 0.6 0"&gt;
  &lt;a-entity mixin="foliage"&gt;&lt;/a-entity&gt;
  &lt;a-entity mixin="trunk" position="0 -0.5 0"&gt;&lt;/a-entity&gt;
  &lt;a-animation attribute="position" ease="linear" from="0 0.6 -7" to="0 0.6 1.5" dur="5000"&gt;&lt;/a-animation&gt;
&lt;/a-entity&gt;

&lt;a-entity id="template-tree-left" shadow scale="0.3 0.3 0.3" position="-0.5 0.55 0"&gt;
  &lt;a-entity mixin="foliage"&gt;&lt;/a-entity&gt;
  &lt;a-entity mixin="trunk" position="0 -0.5 0"&gt;&lt;/a-entity&gt;
  &lt;a-animation attribute="position" ease="linear" from="-0.5 0.55 -7" to="-0.5 0.55 1.5" dur="5000"&gt;&lt;/a-animation&gt;
&lt;/a-entity&gt;

&lt;a-entity id="template-tree-right" shadow scale="0.3 0.3 0.3" position="0.5 0.55 0"&gt;
  &lt;a-entity mixin="foliage"&gt;&lt;/a-entity&gt;
  &lt;a-entity mixin="trunk" position="0 -0.5 0"&gt;&lt;/a-entity&gt;
  &lt;a-animation attribute="position" ease="linear" from="0.5 0.55 -7" to="0.5 0.55 1.5" dur="5000"&gt;&lt;/a-animation&gt;
&lt;/a-entity&gt;

&lt;!-- Player --&gt;
...
</code></pre>
</div>

Navigate to your preview, and you will now see the trees moving towards you.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d89663-74dc-4ab5-b4e7-75440e270272/2-how-to-build-an-endless-runner-game-in-virtual-reality.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d598e2f3-5336-41ff-9738-7323b4667a27/2-how-t0-build-an-endless-runner-game-in-virtual-reality-800w.gif" width="800" height="368" alt="Template trees moving towards player" /></a><figcaption>Template trees moving towards playerTemplate trees moving towards player (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d89663-74dc-4ab5-b4e7-75440e270272/2-how-to-build-an-endless-runner-game-in-virtual-reality.gif">Large preview</a>)
</figcaption></figure>

Navigate back to your editor. This time, select *assets/ergo.js*. In the game section, setup trees after the window has loaded.

<pre><code class="language-javascript">/********
 * GAME *
 ********/

...

window.onload = function() {
  setupTrees();
}
</code></pre>

Underneath the controls but before the Game section, add a new `TREES` section. In this section, define a new `setupTrees` function.

<pre><code class="language-javascript">/************
 * CONTROLS *
 ************/

...

/*********
 * TREES *
 *********/

function setupTrees() {
}

/********
 * GAME *
 ********/

...
</code></pre>

In the new `setupTrees` function, obtain references to the template tree DOM objects, and make the references available globally.

<div class="break-out">

<pre><code class="language-javascript">/*********
 * TREES *
 *********/

var templateTreeLeft;
var templateTreeCenter;
var templateTreeRight;

function setupTrees() {
  templateTreeLeft    = document.getElementById('template-tree-left');
  templateTreeCenter  = document.getElementById('template-tree-center');
  templateTreeRight   = document.getElementById('template-tree-right');
}

</code></pre>
</div>

Next, define a new `removeTree` utility. With this utility, you can then remove the template trees from the scene. Underneath the `setupTrees` function, define your new utility.

<pre><code class="language-javascript">function setupTrees() {
    ...
}

function removeTree(tree) {
  tree.parentNode.removeChild(tree);
}
</code></pre>

Back in `setupTrees`, use the new utility to remove the template trees.

<pre><code class="language-javascript">function setupTrees() {
  ...

  removeTree(templateTreeLeft);
  removeTree(templateTreeRight);
  removeTree(templateTreeCenter);
}
</code></pre>

Ensure that your tree and game sections match the following:

<div class="break-out">

<pre><code class="language-javascript">/*********
 * TREES *
 *********/

var templateTreeLeft;
var templateTreeCenter;
var templateTreeRight;

function setupTrees() {
  templateTreeLeft    = document.getElementById('template-tree-left');
  templateTreeCenter  = document.getElementById('template-tree-center');
  templateTreeRight   = document.getElementById('template-tree-right');

  removeTree(templateTreeLeft);
  removeTree(templateTreeRight);
  removeTree(templateTreeCenter);
}

function removeTree(tree) {
  tree.parentNode.removeChild(tree);
}

/********
 * GAME *
 ********/

setupControls();  // TODO: AFRAME.registerComponent has to occur before window.onload?

window.onload = function() {
  setupTrees();
}
</code></pre>
</div>

Re-open your preview, and your trees should now be absent. The preview should match our game at the start of this tutorial.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a112e7e5-c79b-4ce9-8d07-812efadc9cab/1-how-to-build-an-endless-runner-game-in-virtual-reality.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3a6b409-beae-4e89-a4b8-42001cf0aef1/01-how-to-build-an-endless-runner-game-in-virtual-reality-800w.gif" width="800" height="368" alt="Part 1 finished product" /></a><figcaption>Part 1 finished product (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a112e7e5-c79b-4ce9-8d07-812efadc9cab/1-how-to-build-an-endless-runner-game-in-virtual-reality.gif">Large preview</a>)
</figcaption></figure>

This concludes the template tree design.

In this step, we covered and used A-Frame mixins, which allow us to simplify code by defining common properties. Furthermore, we leveraged A-Frame integration with the DOM to remove objects from the A-Frame VR scene.

In the next step, we will spawn multiple obstacles and design a simple algorithm to distribute trees among different lanes.

{{% ad-panel-leaderboard %}}

## Step 2 : Spawning Obstacles

In an endless runner game, our goal is to avoid obstacles flying towards us. In this particular implementation of the game, we use three lanes as is most common.

Unlike most endless runner games, **this game will only support movement left and right**. This imposes a constraint on our algorithm for spawning obstacles: we can’t have three obstacles in all three lanes, at the same time, flying towards us. If that occurs, the player would have zero chance of survival. As a result, our spawning algorithm needs to accommodate this constraint.

In this step, all of our code edits will be made in *assets/ergo.js*. The HTML file will remain the same. Navigate to the `TREES` section of *assets/ergo.js*.

To start, we will add utilities to spawn trees. Every tree will need a unique ID, which we will naively define to be the number of trees that exist when the tree is spawned. Start by tracking the number of trees in a global variable.

<pre><code class="language-javascript">/*********
 * TREES *
 *********/

...
var numberOfTrees = 0;

function setupTrees() {
...
</code></pre>

Next, we will initialize a reference to the tree container DOM element, which our spawn function will add trees to. Still in the `TREES` section, add a global variable and then make the reference.

<pre><code class="language-javascript">...
var treeContainer;
var numberOfTrees ...

function setupTrees() {
    ...
    templateTreeRight   = ...
    treeContainer       = document.getElementById('tree-container');
    
    removeTree(...);
    ...
}
</code></pre>

Using both the number of trees and the tree container, write a new function that spawns trees.

<pre><code class="language-javascript">function removeTree(tree) {
    ...
}

function addTree(el) {
  numberOfTrees += 1;
  el.id = 'tree-' + numberOfTrees;
  treeContainer.appendChild(el);
}

...
</code></pre>

For ease-of-use later on, you will create a second function that adds the correct tree to the correct lane. To start, define a new `templates` array in the `TREES` section.

<div class="break-out">

<pre><code class="language-javascript">var templates;
var treeContainer;
...

function setupTrees() {
    ...
    templates           = [templateTreeLeft, templateTreeCenter, templateTreeRight];

    removeTree(...);
    ...
}
</code></pre>
</div>

Using this templates array, add a utility that spawns trees in a specific lane, given an ID representing left, middle, or right.

<pre><code class="language-javascript">function function addTree(el) {
    ...
}

function addTreeTo(position_index) {
  var template = templates[position_index];
  addTree(template.cloneNode(true));
}
</code></pre>

Navigate to your preview, and open your developer console. In your developer console, invoke the global `addTreeTo` function.

<pre><code class="language-javascript">> addTreeTo(0);  # spawns tree in left lane
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d13455db-2b8d-4082-bfbf-82fda93d1de7/4-how-to-build-an-endless-runner-game-in-virtual-reality.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/771ce734-6968-4a84-80df-7710c759ca00/4-how-to-build-an-endless-runner-game-in-virtual-reality-800w.gif" width="800" height="368" alt="Invoking addTreeTo manually" /></a><figcaption>Invoke <code>addTreeTo</code> manually (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d13455db-2b8d-4082-bfbf-82fda93d1de7/4-how-to-build-an-endless-runner-game-in-virtual-reality.gif">Large preview</a>)
</figcaption></figure>

Now, you will write an algorithm that spawns trees randomly:

1. Pick a lane randomly (that hasn’t been picked yet, for this timestep);
2. Spawn a tree with some probability;
3. If the maximum number of trees has been spawned for this timestep, stop. Otherwise, repeat step 1.

To effect this algorithm, we will instead shuffle the list of templates and process one at a time. Start by defining a new function, `addTreesRandomly` that accepts a number of different keyword arguments.

<pre><code class="language-javascript">function addTreeTo(position_index) {
    ...
}

/**
 * Add any number of trees across different lanes, randomly.
 **/
function addTreesRandomly(
  {
    probTreeLeft = 0.5,
    probTreeCenter = 0.5,
    probTreeRight = 0.5,
    maxNumberTrees = 2
  } = {}) {
}
</code></pre>

In your new `addTreesRandomly` function, define a list of template trees, and shuffle the list.

<pre><code class="language-javascript">function addTreesRandomly( ... ) {
  var trees = [
    {probability: probTreeLeft,   position_index: 0},
    {probability: probTreeCenter, position_index: 1},
    {probability: probTreeRight,  position_index: 2},
  ]
  shuffle(trees);
}
</code></pre>

Scroll down to the bottom of the file, and create a new utilities section, along with a new `shuffle` utility. This utility will shuffle an array in place.

<pre><code class="language-javascript">/********
 * GAME *
 ********/

...

/*************
 * UTILITIES *
 *************/

/**
 * Shuffles array in place.
 * @param {Array} a items An array containing the items.
 */
function shuffle(a) {
   var j, x, i;
   for (i = a.length - 1; i > 0; i--) {
       j = Math.floor(Math.random() * (i + 1));
       x = a[i];
       a[i] = a[j];
       a[j] = x;
   }
   return a;
}
</code></pre>

Navigate back to the `addTreesRandomly` function in your Trees section. Add a new variable `numberOfTreesAdded` and iterate through the list of trees defined above.

<pre><code class="language-javascript">function addTreesRandomly( ... ) {
  ...
  var numberOfTreesAdded = 0;
  trees.forEach(function (tree) {
  });
}
</code></pre>

In the iteration over trees, spawn a tree only with some probability and only if the number of trees added does not exceed `2`. Update the for loop as follows.

<div class="break-out">

<pre><code class="language-javascript">function addTreesRandomly( ... ) {
  ...
  trees.forEach(function (tree) {
    if (Math.random() < tree.probability && numberOfTreesAdded < maxNumberTrees) {
      addTreeTo(tree.position_index);
      numberOfTreesAdded += 1;
    }
  });
}
</code></pre>
</div>

To conclude the function, return the number of trees added.

<pre><code class="language-javascript">function addTreesRandomly( ... ) {
  ...
  return numberOfTreesAdded;
}
</code></pre>

Double check that your `addTreesRandomly` function matches the following.

<div class="break-out">

<pre><code class="language-javascript">/**
 * Add any number of trees across different lanes, randomly.
 **/
function addTreesRandomly(
  {
    probTreeLeft = 0.5,
    probTreeCenter = 0.5,
    probTreeRight = 0.5,
    maxNumberTrees = 2
  } = {}) {

  var trees = [
    {probability: probTreeLeft,   position_index: 0},
    {probability: probTreeCenter, position_index: 1},
    {probability: probTreeRight,  position_index: 2},
  ]
  shuffle(trees);

  var numberOfTreesAdded = 0;
  trees.forEach(function (tree) {
    if (Math.random() < tree.probability && numberOfTreesAdded < maxNumberTrees) {
      addTreeTo(tree.position_index);
      numberOfTreesAdded += 1;
    }
  });

  return numberOfTreesAdded;
}
</code></pre>
</div>

Finally, to spawn trees automatically, setup a timer that runs triggers tree-spawning at regular intervals. Define the timer globally, and add a new teardown function for this timer.

<pre><code class="language-javascript">/*********
 * TREES *
 *********/
...
var treeTimer;

function setupTrees() {
...
}

function teardownTrees() {
  clearInterval(treeTimer);
}
</code></pre>

Next, define a new function that initializes the timer and saves the timer in the previously-defined global variable. The below timer is run every half a second.

<pre><code class="language-javascript">function addTreesRandomlyLoop({intervalLength = 500} = {}) {
  treeTimer = setInterval(addTreesRandomly, intervalLength);
}
</code></pre>

Finally, start the timer after the window has loaded, from the Game section.

<pre><code class="language-javascript">/********
 * GAME *
 ********/
...
window.onload = function() {
  ...
  addTreesRandomlyLoop();
}
</code></pre>

Navigate to your preview, and you’ll see trees spawning at random. Note that there are never three trees at once.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ade6de6-ec8e-4327-88e6-d061f597b8c3/5-how-to-build-an-endless-runner-game-in-virtual-reality.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d10e82c0-1c8a-4a4b-8943-206477281c1c/5-how-to-build-an-endless-runner-game-in-virtual-reality-800w.gif" width="800" alt="Tree spawning at random" /></a><figcaption>Tree randomly spawning (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ade6de6-ec8e-4327-88e6-d061f597b8c3/5-how-to-build-an-endless-runner-game-in-virtual-reality.gif">Large preview</a>)
</figcaption></figure>

This concludes the obstacles step. We’ve successfully taken a number of template trees and generated an infinite number of obstacles from the templates. Our spawning algorithm also respects natural constraints in the game to make it playable.

In the next step, let’s add collision testing. 

{{% ad-panel-leaderboard %}}

## Step 3: Collision Testing

In this section, we’ll implement the collision tests between the obstacles and the player. These collision tests are simpler than collision tests in most other games; however, the player only moves along the x-axis, so whenever a tree crosses the x-axis, check if the tree’s lane is the same as the player’s lane. We will implement this simple check for this game.

Navigate to *index.html*, down to the `TREES` section. Here, we will add lane information to each of the trees. For each of the trees, add `data-tree-position-index=`, as follows. Additionally add `class="tree"`, so that we can easily select all trees down the line:

<div class="break-out">

<pre><code class="language-html">&lt;a-entity data-tree-position-index="1" class="tree" id="template-tree-center" ...&gt;
&lt;/a-entity&gt;
&lt;a-entity data-tree-position-index="0" class="tree" id="template-tree-left" ...&gt;
&lt;/a-entity&gt;
&lt;a-entity data-tree-position-index="2" class="tree" id="template-tree-right" ...&gt;
&lt;/a-entity&gt;
</code></pre>
</div>

Navigate to *assets/ergo.js* and invoke a new `setupCollisions` function in the `GAME` section. Additionally, define a new `isGameRunning` global variable that denotes whether or not an existing game is already running.

<pre><code class="language-javascript">/********
 * GAME *
 ********/

var isGameRunning = false;

setupControls();
setupCollision();

window.onload = function() {
...
</code></pre>

Define a new `COLLISIONS` section right after the `TREES` section but before the Game section. In this section, define the setupCollisions function.

<pre><code class="language-javascript">/*********
 * TREES *
 *********/

...

/**************
 * COLLISIONS *
 **************/

const POSITION_Z_OUT_OF_SIGHT = 1;
const POSITION_Z_LINE_START = 0.6;
const POSITION_Z_LINE_END = 0.7;

function setupCollision() {
}

/********
 * GAME *
 ********/
</code></pre>

As before, we will register an AFRAME component and use the `tick` event listener to run code at every timestep. In this case, we will register a component with `player` and run checks against all trees in that listener:

<div class="break-out">

<pre><code class="language-javascript">function setupCollisions() {
  AFRAME.registerComponent('player', {
    tick: function() {
      document.querySelectorAll('.tree').forEach(function(tree) {
      }
    }
  }
}
</code></pre>
</div>

In the `for` loop, start by obtaining the tree’s relevant information:

<div class="break-out">

<pre><code class="language-javascript"> document.querySelectorAll('.tree').forEach(function(tree) {
  position = tree.getAttribute('position');
  tree_position_index = tree.getAttribute('data-tree-position-index');
  tree_id = tree.getAttribute('id');
}
</code></pre>
</div>

Next, still within the `for` loop, remove the tree if it is out of sight, right after extracting the tree’s properties:

<div class="break-out">

<pre><code class="language-javascript"> document.querySelectorAll('.tree').forEach(function(tree) {
  ...
  if (position.z > POSITION_Z_OUT_OF_SIGHT) {
    removeTree(tree);
  }
}
</code></pre>
</div>

Next, if there is no game running, do not check if there is a collision.

<div class="break-out">

<pre><code class="language-javascript"> document.querySelectorAll('.tree').forEach(function(tree) {
  if (!isGameRunning) return;
}
</code></pre>
</div>

Finally (still in the `for` loop), check if the tree shares the same position at the same time with the player. If so, call a yet-to-be-defined `gameOver` function:

<div class="break-out">

<pre><code class="language-javascript">document.querySelectorAll('.tree').forEach(function(tree) {
  ...
  if (POSITION_Z_LINE_START < position.z && position.z < POSITION_Z_LINE_END
      && tree_position_index == player_position_index) {
    gameOver();
  }
}
</code></pre>
</div>

Check that your `setupCollisions` function matches the following:

<div class="break-out">

<pre><code class="language-javascript">function setupCollisions() {
  AFRAME.registerComponent('player', {
    tick: function() {
      document.querySelectorAll('.tree').forEach(function(tree) {
        position = tree.getAttribute('position');
        tree_position_index = tree.getAttribute('data-tree-position-index');
        tree_id = tree.getAttribute('id');

        if (position.z > POSITION_Z_OUT_OF_SIGHT) {
          removeTree(tree);
        }

        if (!isGameRunning) return;

        if (POSITION_Z_LINE_START < position.z && position.z < POSITION_Z_LINE_END
            && tree_position_index == player_position_index) {
          gameOver();
        }
      })
    }
  })
}
</code></pre>
</div>

This concludes the collision setup. Now, we will add a few niceties to abstract away the `startGame` and `gameOver` sequences. Navigate to the `GAME` section. Update the `window.onload` block to match the following, replacing `addTreesRandomlyLoop` with a yet-to-be-defined `startGame` function.

<pre><code class="language-javascript">window.onload = function() {
  setupTrees();
  startGame();
}
</code></pre>

Beneath the setup function invocations, create a new `startGame` function. This function will initialize the `isGameRunning` variable accordingly, and prevent redundant calls.

<pre><code class="language-javascript">window.onload = function() {
    ...
}

function startGame() {
  if (isGameRunning) return;
  isGameRunning = true;

  addTreesRandomlyLoop();
}
</code></pre>

Finally, define `gameOver`, which will alert a “Game Over!” message for now.

<pre><code class="language-javascript">function startGame() {
    ...
}

function gameOver() {
  isGameRunning = false;

  alert('Game Over!');
  teardownTrees();
}
</code></pre>

This concludes the collision testing section of the endless runner game.

In this step, we again used A-Frame components and a number of other utilities that we added previously. We additionally re-organized and properly abstracted the game functions; we will subsequently augment these game functions to achieve a more complete game experience.

## Conclusion

In [part 1](https://www.smashingmagazine.com/2019/03/virtual-reality-endless-runner-game-vr-part-1/?_ga=2.254726144.945251289.1552293602-640474844.1551793279), we added VR-headset-friendly controls: Look left to move left, and right to move right. In this second part of the series, I’ve shown you how easy it can be to build a basic, functioning virtual reality game. We added game logic, so that the endless runner matches your expectations: run forever and have an endless series of dangerous obstacles fly at the player. Thus far, you have built a functioning game with keyboard-less support for virtual reality headsets.

Here are additional resources for different VR controls and headsets:

- [A-Frame for VR Headsets](https://aframe.io/docs/0.8.0/introduction/vr-headsets-and-webvr-browsers.html)  
A survey of browsers and headsets that A-Frame VR supports.
- [A-Frame for VR Controllers](https://aframe.io/docs/0.8.0/introduction/interactions-and-controllers.html)  
How A-Frame supports no controllers, 3DoF controllers and 6DoF controllers, in addition to other alternatives for interaction.

In the [next part](https://www.smashingmagazine.com/2019/03/virtual-reality-endless-runner-game-vr-part-3/), we will add a few finishing touches and synchronize *game states*, which move us one step closer to multiplayer games. 

{{< signature "rb, ra, yk, il" >}}
