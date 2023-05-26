---
title: 'How To Create A Particle Trail Animation In JavaScript'
slug: particle-trail-animation-javascript
author: anna-prenzel
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57ed0818-d345-4d90-b7e9-e7b5e8dd3cc7/partical-trail-animation-javascript.png
date: 2020-04-14T11:00:00.000Z
summary: >-
  Particle animations belong to the most impressive animations that exist. In this article, Anna Prenzel will explain how you can to easily program a small trail of particles with <a href="https://animejs.com/">anime.js</a>.
description: >-
  Particle animations belong to the most impressive animations that exist. In this article, Anna Prenzel will explain how you can to easily program a small trail of particles with <a href="https://animejs.com/">anime.js</a>.
categories:
  - JavaScript
  - Animation
---

<p>Have you ever thought about distracting visitors of your website with a fancy, glittering particle animation for a few moments, while some data is loaded in the background? Fortunately, it’s not necessary to go very deep into graphics programming with 3D libraries like three.js. All you need instead is some basic knowledge of CSS and JavaScript and a lightweight animation library such as anime.js. In the end, we should have the following <a href="https://codepen.io/blaustern_fotografie/pen/vYEwwqx">result</a>:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4df8668-e60b-4767-9452-3f641c90dbd0/4-partical-trail-animation-javascript.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4df8668-e60b-4767-9452-3f641c90dbd0/4-partical-trail-animation-javascript.gif" width="791" height="605" alt="" /></a><figcaption>A spiral shaped particle trail animation</figcaption></figure>

## Download And Integration Of Anime.js

<p>You can download the anime.js library from the <a href="https://github.com/juliangarnier/anime/">official GitHub site</a>. Download the file <em>anime.js</em> or <em>anime.min.js</em> from the <a href="https://github.com/juliangarnier/anime/tree/master/lib"><code>lib/</code></a> folder.</p>

<p>In my example, the HTML part looks like this:</p>

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en" &gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;title&gt;Anime.js Particles&lt;/title&gt;
  &lt;!--or use anime.min.js--&gt;
  &lt;script src="anime.js"&gt;&lt;/script&gt;
  &lt;link rel="stylesheet" href="style.css"&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;div class="anime-container"&gt;
&lt;/div&gt;
&lt;script src="script.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

<p>The CSS file <em>styles.css</em> defines the background color for the page and for the individual particles. The position settings are necessary so that we can later position the particles freely on the page using the CSS properties <code>left</code> and <code>top</code>.</p>

<pre><code class="language-css">body {
 background-color: hsl(30, 3%, 14%);
}
.anime-container {
  position: relative;
}
 
.anime-container .dot{
  position: absolute;
  /*draw particles as circles:*/
  border-radius: 50%;
  background-color: hsl(60, 100%, 80%);
}</code></pre>

<p>The content of the file <em>script.js</em> is covered in the following section.</p>

{{% feature-panel %}}

## Generating The Particles

<p>As the name suggests, a particle animation consists of many small particles moving in space while following a certain pattern. All particles are generated simultaneously before the animation starts.</p>

<p><em>For the following explanation, the <a href="https://animejs.com/documentation/">official documentation of anime.js</a> will be useful.</em></p>

<p>In my example, the particles are located on an Archimedean spiral. The <code>x</code> and <code>y</code> position of a particle on the screen (aka <code>left</code> and <code>top</code> in CSS) is calculated from its position <code>angle</code> on the spiral:</p>

<pre><code class="language-css">x=a*angle*cos(angle)
y=a*angle*sin⁡(angle)
</code></pre>

<p>The number of angles and thus the length of the spiral is determined by the parameter <code>l</code>. With the parameter <code>a</code>, you can control the density of the spiral.</p>

<div class="break-out">

<pre><code class="language-javascript">var container = document.querySelector(".anime-container");
var n = 15;
var a = 20;
var l = 110;
for (var i = 0; i <= l; i += 1) {
  var angle = 0.1 * i;
  //shift the particles to the center of the window 
  //by adding half of the screen width and screen height
  var x = (a*angle) * Math.cos(angle) + window.innerWidth / 2;
  var y = (a*angle) * Math.sin(angle) + window.innerHeight / 2;
  var dot = document.createElement("div");
  dot.classList.add("dot");
  container.appendChild(dot);
  var size = 5;
  dot.style.width = size + "px";
  dot.style.height = size + "px";
  dot.style.left = x + "px";
  dot.style.top = y + "px";
  dot.style.backgroundColor = "hsl(60, 100%, 80%)";
  }
}</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45f106a4-57ba-426d-8be9-bdb8f89ab9a3/5-partical-trail-animation-javascript.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45f106a4-57ba-426d-8be9-bdb8f89ab9a3/5-partical-trail-animation-javascript.png" sizes="100vw" caption="First version of our spiral (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45f106a4-57ba-426d-8be9-bdb8f89ab9a3/5-partical-trail-animation-javascript.png'>Large preview</a>)" alt="" >}}

<p>This way, we get a spiral with exactly one particle per position, but a real trail effect can only be achieved if more than one particle is generated at each position. For the trail to look bushy, the positions of the individual particles must be slightly different. The anime-library provides a practical helper function for this:

<pre><code class="language-markup">anime.random(minValue, maxValue);
</code></pre>

<p>The size of the particles also varies randomly:</p>

<div class="break-out">

<pre><code class="language-javascript">for (var i = 0; i <= l; i += 1) {
  var angle = 0.1 * i;
  //shift particles to the center of the window 
  //by adding half of the screen width and screen height
  var x = (a*angle) * Math.cos(angle) + window.innerWidth / 2;
  var y = (a*angle) * Math.sin(angle) + window.innerHeight / 2;
  var n = 15;
  
  //create n particles for each angle
  for (var j = 0; j < n; j++) {
    var dot = document.createElement("div");
    dot.classList.add("dot");
    container.appendChild(dot);
    var size = anime.random(5, 10); 
    dot.style.width = size + "px";
    dot.style.height = size + "px";
    dot.style.left = x + anime.random(-15, 15) + "px";
    dot.style.top = y + anime.random(-15, 15) + "px";
    dot.style.backgroundColor = "hsl(60, 100%, 80%)";
  }
}</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06a78c08-5c54-4ef0-a688-4a218dee3073/3-partical-trail-animation-javascript.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06a78c08-5c54-4ef0-a688-4a218dee3073/3-partical-trail-animation-javascript.png" sizes="100vw" caption="The spiral with randomly placed particles (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06a78c08-5c54-4ef0-a688-4a218dee3073/3-partical-trail-animation-javascript.png'>Large preview</a>)" alt="" >}}

<p>Here you can play around with the intermediate result:</p>

{{< codepen height="480" theme_id="light" slug_hash="JjdqBve" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [anime js particles wip](https://codepen.io/smashingmag/pen/JjdqBve) by <a href="https://codepen.io/blaustern_fotografie">Anna Prenzel</a>.{{< /codepen >}}

<p>Before the animation starts, all particles have to be invisible. So I will add:</p>

<pre><code class="language-javascript">dot.style.opacity = "0";</code></pre>

## Animation Of The Particles

### Basic Settings Of The Animation

<p>The basic settings of my animation are made up as follows:</p>

<ul>
<li>The animation is to be repeated continuously (loop: true),</li>
<li>The easing is linear (but you can try <a href="https://animejs.com/documentation/#linearEasing">different values</a>),</li>
<li>The targets are all elements with the class "dot".</li>
</ul>

<pre><code class="language-javascript">anime({
  loop: true,
  easing: "linear",
  targets: document.querySelectorAll(".dot"),
});</code></pre>

<p>In the next step I will animate various CSS properties of my targets. The basic steps for CSS animation can be found <a href="https://animejs.com/documentation/#cssProperties">in the properties chapter</a> of the anime.js documentation.</p>

{{% ad-panel-leaderboard %}}

### Animation Of Opacity

<p>This is what our first property animation looks like, in which all particles are slowly made visible within 50ms:</p>

<pre><code class="language-javascript">anime({
  loop: true,
  easing: "linear",
  targets: document.querySelectorAll(".dot"),
  opacity: { value: 1, duration: 50}
});</code></pre> 

<p>And now I will finally reveal the trick that creates a spiral movement of the particles! The idea is to make the particles visible with a certain time delay (e.g. in an interval of 2ms). The particles in the middle of the spiral are made visible at first, followed by all the other particles from inside to outside. The <a href="https://animejs.com/documentation/#staggeringBasics">stagger function</a> of anime.js is perfectly suited for this. In my opinion, staggering is one of the biggest strengths of the library that allows you to achieve great effects.</p>

<pre><code class="language-javascript">opacity: { value: 1, duration: 50, delay: anime.stagger(2) }
</code></pre>

<p>To create the illusion of a flying trail, the particles must start disappearing slowly <em>as soon as they have appeared</em>. Fortunately anime.js provides a <a href="https://animejs.com/documentation/#propertyKeyframes">keyframe notation for properties</a>:</p>

<pre><code class="language-javascript">opacity: [
    { value: 1, duration: 50, delay: anime.stagger(2) },
    { value: 0, duration: 1200}
  ],
</code></pre>

<p>Here you can see the intermediate result:</p>

{{< codepen height="480" theme_id="light" slug_hash="ZEGNjjv" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [anime js particles wip 2](https://codepen.io/smashingmag/pen/ZEGNjjv) by <a href="https://codepen.io/blaustern_fotografie">Anna Prenzel</a>.{{< /codepen >}}

### Animation Of Size

<p>My comet trail should appear larger at the front end than at the back end. For this purpose, I let the particles shrink within 500ms to a diameter of 2px. It is important to choose the same time delay as for the opacity animation, so that each particle starts to shrink only after it has appeared:</p>

<pre><code class="language-javascript">width: { value: 2, duration: 500, delay: anime.stagger(2) },
height: { value: 2, duration: 500, delay: anime.stagger(2) },</code></pre>

{{% ad-panel-leaderboard %}}

### Individual Movement Of The Particles

<p>The typical thing about a particle animation is the individual, unpredictable behavior of the particles. I finally bring the particles to life with an individual movement in the <code>x</code> and <code>y</code> direction:</p>

<pre><code class="language-javascript">translateX: {
    value: function() {
      return anime.random(-30, 30);
    },
    duration: 1500,
    delay: anime.stagger(2)
  },

translateY: {
    value: function() {
      return anime.random(-30, 30);
    },
    duration: 1500,
    delay: anime.stagger(2)
  }</code></pre>

<p>Again, it is important that the movement starts with the same time delay as the appearance of the particles.</p>

<p>Furthermore, it is absolutely necessary in this case to have <code>functions</code> calculating the values for <code>translateX</code> and <code>translateY</code>. Here we are using the parameters as <a href="https://animejs.com/documentation/#functionBasedParameters">function-based parameters</a> whose values are determined <em>for each target individually</em>. Otherwise all targets would be shifted by the same (albeit randomly determined) amount.</p>

## Final Thoughts

<p>You can see the final result over here:</p>

{{< codepen height="480" theme_id="light" slug_hash="yLNWqRP" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [anime js particles](https://codepen.io/smashingmag/pen/yLNWqRP) by <a href="https://codepen.io/blaustern_fotografie">Anna Prenzel</a>.{{< /codepen >}}

<p>You can modify the animation to your own taste by simply tweaking all the values. I have a little tip for the final touches: Now that we are familiar with function-based parameters, the opacity animation can be improved a bit:</p>

<div class="break-out">

<pre><code class="language-javascript">opacity: [
    { value: 1, duration: 50, delay: anime.stagger(2) },
    { value: 0, duration: function(){return anime.random(500,1500);}}
],</code></pre>
</div>

<p>The duration before a particle disappears is now set for each particle individually. This makes our animation visually even more sophisticated.</p>

<p>I hope you are now as excited as I am about the possibilities that anime.js offers for particle animations! I recommend a visit to <a href="https://codepen.io/collection/XLebem/">CodePen</a> where you can see many more impressive examples.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Including Animation In Your Design System'" href="https://www.smashingmagazine.com/2019/02/animation-design-system/" rel="bookmark">Including Animation In Your Design System</a></li>
<li><a title="Read 'HTML5 SVG Fill Animation With CSS3 And Vanilla JavaScript'" href="https://www.smashingmagazine.com/2019/01/html5-svg-fill-animation-css3-vanilla-javascript/" rel="bookmark">HTML5 SVG Fill Animation With CSS3 And Vanilla JavaScript</a></li>
<li><a title="Read 'Introduction To Animation And The iMessage App Store With Shruggie'" href="https://www.smashingmagazine.com/2018/09/animation-imessage-app-store-shruggie/" rel="bookmark">Introduction To Animation And The iMessage App Store With Shruggie</a></li>
<li><a title="Read 'Exploring Animation And Interaction Techniques With WebGL (A Case Study)'" href="https://www.smashingmagazine.com/2017/09/animation-interaction-techniques-webgl/" rel="bookmark">Exploring Animation And Interaction Techniques With WebGL (A Case Study)</a></li>
</ul>

{{< signature "ra, yk, il" >}}
