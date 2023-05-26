---
title: How To Create Web Animations With Paper.js
slug: create-web-animations-with-paperjs
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81051cc9-4d78-403b-a6d3-4f804fac1d31/dandelion-1.jpg'
date: 2011-11-21T10:20:40.000Z
author: zack-grossbart
description: >-
  The Web is just starting to use animation well. For years, animated GIFs and
  Flash ruled. Text moved and flashed, but it was never seamless. Animations had
  boxes around them like YouTube videos. HTML5 canvas changes everything about
  Web animation.
categories:
  - Coding
  - JavaScript
  - HTML5
  - HTML
---
The Web is just starting to use animation well. For years, animated GIFs and Flash ruled. Text moved and flashed, but it was never seamless. Animations had boxes around them like YouTube videos. HTML5 <code>canvas</code> changes everything about Web animation.

The <code>canvas</code> element makes it possible to integrate drawings and animations with the rest of your page. You can combine them with text and make animations interactive. This drawing mechanism is powerful, but very low-level.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The State Of Animation 2014](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [We’re Gonna Need A Bigger API!](https://www.smashingmagazine.com/2013/03/animating-web-gonna-need-bigger-api/)
*   [UI Animation Guidelines and Examples](https://www.smashingmagazine.com/2015/05/functional-ux-design-animations/)
*   [Designing Animations In Photoshop](https://www.smashingmagazine.com/2015/06/creating-advanced-animations-in-photoshop/)

Animations get more power and need less coding when you combine the <code>canvas</code> tag with higher-level libraries such as <a href="https://paperjs.org/">Paper.js</a>. This article introduces HTML5 <a href="https://paperjs.org/tutorials/animation/creating-animations/">animation</a> and walks you through creating an animation of dandelion seeds blowing in the wind.

{{% feature-panel %}}

## Neat Is Easy, But Messy Is Hard

Computers love clean. They make spreadsheets, do statistics and plot multivariate curves; they always color inside the lines.

In the real world, even simple things are messy. Leaves falling from trees, water splashing — all the little interactions around us feel simple because we’re used to them; but little bursts of wind are actually messy and unpredictable.

For this article, we’ll animate dandelion seeds blowing in the breeze.

Dandelions are tricky because we all know what they look like: we’ve touched them and blown their seeds off. Commonplace objects produce instant recognition and feelings. I don’t have to tell you what dandelions are — you just know. Dandelions are a chaos of seeds piled on top of each other.

<img title="Messy Dandelion Seeds" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a717d52-491a-4852-acfe-729848a42384/messy-seeds2.jpg" alt="screenshot" width="450" height="450" />

<em>(Image: <a href="https://commons.wikimedia.org/wiki/User:Arnoldius">Arnoldius</a>)</em>

Our dandelion animation will never reproduce the complexity of the real thing, and it will work better if we don’t try: make it too close to real and it will feel funny. Instead, we’ll create a stylized dandelion that makes the right impression without all of the details.

<a href="https://zgrossbart.github.com/Dandelion/"><img title="See the animation running and edit the code" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c025898c-fc96-4ef4-9663-ddb7ec2cb26a/basic-dandelion.jpg" alt="screenshot" width="403" height="417" /></a>

## Paper.js

Drawing simple shapes with the <code>canvas</code> tag, without any special drawing libraries, is easy. Create your <code>canvas</code>:

<pre><code class="language-markup tmp-html">&lt;canvas id="canvas" width="300" height="300"&gt;&lt;/canvas&gt;</code></pre>

Then add a little JavaScript.

<pre><code class="language-javascript">// Get our canvas
var canvas = $('#canvas')[0].getContext("2d");

// Draw a circle
canvas.beginPath();
canvas.arc(100, 100, 15, 0, Math.PI*2, true);

// Close the path
canvas.closePath();

// Fill it in
canvas.fill();</code></pre>

<img title="Circle" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e20ef2c-48ec-4a7c-b958-2ace2704d502/circle.png" alt="screenshot" width="360" height="295" />

Cheat sheets for canvas show you the basics, but when you get into more serious drawing, you’ll want a higher-level library, such as <a href="https://paperjs.org/">Paper.js</a>.

Paper.js is a JavaScript library for drawings and animations. It’s based largely on <a href="https://scriptographer.org/">Scriptographer</a>, a scripting language for <a href="https://en.wikipedia.org/wiki/Adobe_Illustrator">Adobe Illustrator</a>. You can <a href="https://paperjs.org/tutorials/getting-started/using-javascript-directly/">write JavaScript with Paper.js</a>, but most of the time you’ll be working with a JavaScript variant called PaperScript.

Paper.js calls itself “<a href="https://paperjs.org/about/">The Swiss Army Knife of Vector Graphics Scripting</a>,” and the “<a href="https://paperjs.org/features/#vector-geometry">vector</a>” part is important.

There are two basic types of graphics, <a href="https://en.wikipedia.org/wiki/Vector_graphics">vectorized</a> and <a href="https://en.wikipedia.org/wiki/Raster_graphics">rasterized</a>. Rasterized graphics are like the pictures you take with your camera: big rectangles with maps denoting the color of each pixel. Enlarge them and you’ll get blurry dots.

Vector graphics are like connect-the-dots pictures: they’re sets of lines and shapes that give instructions on how to draw the image at any size. Using vector graphics, you can make an image of the letter Z really big and it will still look sharp. If you turned it into a rasterized graphic by taking a picture of it and then blowing it up, the letter would get all blurry.

<img title="Raster vs. Vector" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc8a5d1-409b-4f49-9d38-2ca458df7f37/rastervector.png" alt="" width="402" height="181" />

Vector graphics libraries are perfect for animation because they make resizing, rotating and moving objects easy. They’re also much faster, because the program has instructions for drawing each object instead of needing to figure it out.

The <a href="https://paperjs.org/examples/">Paper.js examples page</a> shows some of the amazing things you can do with vectorized graphics.

The dandelion is a complete functioning example, and you can see it all running on the <a href="https://zgrossbart.github.com/Dandelion/">example page</a>. You can also change the code by clicking the “Edit” button, see your changes live, and copy and paste the code to your own website. Over the course of the article, we’ll explain each part of the code in turn, but please note that in order to run the code yourself, you will need to head over to the example page and copy and paste it to your own environment.

## Drawing Our Dandelion

The first step is to import our JavaScript and PaperScript files.

<pre><code class="language-markup tmp-html">&lt;script src="paper.js" type="text/javascript" charset="utf-8"&gt;&lt;/script&gt;
&lt;script type="text/paperscript" canvas="canvas" src="dandelion.pjs" id="script"&gt;&lt;/script&gt;</code></pre>

The PaperScript code for running the animation is declared as <code>text/paperscript</code>. Now we’re ready to start drawing.

The first part of our dandelion is the stem. The stem is the green arc, with a circle on the top for the bulb. We’ll make both shapes with a <a href="https://paperjs.org/reference/path">path</a>, a list of shapes, points and lines that the browser is instructed to display.

Paths are the basic building blocks of animation. They render lines, curves and polygons. You can also fill them in to make complex shapes. Our path looks like this:

<pre><code class="language-javascript">var path = new Path();
path.strokeColor = '#567e37';
path.strokeWidth = 5;

var firstPoint = new Point(0, 550);
path.add(firstPoint);

var throughPoint = new Point(75, 400);
var toPoint = new Point(100, 250);
path.arcTo(throughPoint, toPoint);</code></pre>

Our path is an arc, so it needs three points: the start, the end and a midpoint to arc through. Three points are enough to define any arc we need. The <code>arcTo</code> function draws the line between them. The path item also supports styling information, such as stroke color and stroke width; <code>#567e37</code> and <code>5</code> will make our arcing line green and thick. Paper.js supports the same color definitions as CSS.

We can add a few more items to make it all easier to see:

<pre><code class="language-javascript">path.fullySelected = true;

var circle = new Path.Circle(throughPoint, 5);
circle.fillColor = '#CC0000';</code></pre>

Fully selecting the path will display some lines to show us the arc; the red circle shows us where the through point is.

<img title="Stem Paths" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4046a814-c0d3-4155-83d9-52a80e002cdf/stem-paths.png" alt="screenshot" width="360" height="295" />

The stem ends with a circle to show the bulb of the flower and give us a place to attach all of the seeds. Circles are much easier in Paper.js than in direct <code>canvas</code>.

<pre><code class="language-javascript">var bulb = new Path.Circle(toPoint, 10);
bulb.fillColor = '#567e37';</code></pre>

One line of code draws our circle, one more makes it green, and now we’re ready to add our seeds.</p>

## Drawing The Seeds

Each seed has a bulb, a little stem and a wispy part on top.

<a href="https://commons.wikimedia.org/wiki/File:Dandelionseed.JPG"><img title="Dandelion seed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87664130-0976-4c10-a842-ed0562dd0772/dandelionseed.jpg" alt="screenshot" width="450" height="450" /></a>

<em>(Image: <a href="https://commons.wikimedia.org/wiki/User:Hmbascom">Hmbascom</a>)</em>

Our seed starts with a small oval for the bulb and an arc for the stem. The oval is a rectangle with rounded corners:

<pre><code class="language-javascript">var size = new Size(4, 10);
var rectangle = new Rectangle(p, size);
var bottom = new Path.Oval(rectangle);
bottom.fillColor = '#d0aa7b';</code></pre>

The seed stem is another arc, but this one is much thinner than the flower stem:

<pre><code class="language-javascript">var stem = new Path();
stem.strokeColor = '#567e37';
stem.strokeWidth = 1;
stem.add(new Point(p.x + 2, p.y));

var throughPoint = new Point(p.x + 4, p.y - height / 2);
var toPoint = new Point(p.x + 3, p.y - height);
stem.arcTo(throughPoint, toPoint);</code></pre>

The wisps are more arcs with a circle at the end of each line. Each seed has a random number of wisps that start at the top of the stem arc and curve out in different directions. Randomness makes them look a little bit messy and thus more natural. Each seed gets a random number of wisps, between 4 and 10.

<pre><code class="language-javascript">for (var i = 0; i &lt; random(4, 10); i++) {
    path = new Path();
    path.strokeColor = '#fff3c9';
    path.strokeWidth = 1;

    var p1 = new Point(p.x, p.y);
    path.add(new Point(p1.x + 2, p1.y + 2));

    // Each flutter extends a random amount up in the air
    var y = random(1, 5);

    // We draw every other stem on the right or the left so they're
    // spaced out in the seed.
    if (i % 2 == 0) {
        throughPoint = new Point(p1.x + random(1, 3), p1.y - y);
        toPoint = new Point(p1.x + random(5, 35), p1.y - 20 - y);
    } else {
        throughPoint = new Point(p1.x - random(1, 3), p1.y - y);
        toPoint = new Point(p1.x - random(5, 35), p1.y - 20 - y);
    }

    path.arcTo(throughPoint, toPoint);

    // Now we put the circle at the tip of the flutter.
    circle = new Path.Circle(toPoint, 2);
    circle.fillColor = '#fff3c9';
}</code></pre>

Now that we’ve drawn the seed, we need to manage it; later, we’ll want to move and rotate it. The seed is made up of a lot of parts, and we don’t want to have to manage each one separately. Paper.js has a nice <a href="https://paperjs.org/reference/group">group</a> object. Groups associate a set of objects together so that we can manipulate them all at once.

<pre><code class="language-javascript">var group = new Group();
group.addChild(bottom);
group.addChild(stem);

this.group = group;</code></pre>

The last step is to package our seed into a reusable object called <code>Seed</code>. We add all of the code we’ve been writing to a new function with the name <code>Seed</code> and add a function to create the initial variables. This example calls that function <code>create</code>, but you can name it anything you want.

<pre><code class="language-javascript">function Seed() {

    this.create = function (/*Point*/ p, /*boolean*/ shortStem) {
    …</code></pre>

The <code>create</code> function draws the seed at the specified <a href="https://paperjs.org/reference/point">Point</a>, and the <code>shortStem</code> boolean tells us whether this is a short stem. We’ll look at short-stemmed seeds a little later.

These types of functions don’t work as <a href="https://en.wikipedia.org/wiki/Constructor_(object-oriented_programming)">constructors</a> in JavaScript, but are supported in PaperScript.

<pre><code class="language-javascript">var seed = new Seed()
seed.create(new Point(100, 100), false);</code></pre>

Our seeds will look like this when we draw them:

<img title="Dandelion seed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6657898b-6dbe-4b7a-92fb-c28296eb453c/seed.png" alt="screenshot" width="360" height="295" />

The <code>Seed</code> object draws our random dandelion seeds. Now we can add them to our flower.</p>

## Adding A Little Chaos

The seeds will look better when we space them out around the circle of our dandelion bulb to feel like a halo of seeds. The bulb is a circle, and the circle is a path, so we can get each point on the path.

<pre><code class="language-javascript">var bulb = new Path.Circle(toPoint, 10); bulb.fillColor = '#567e37';

var angle = 360 / bulb.length;
var seeds = [];

for (var i = 0; i &lt; bulb.length; i++) {
    var seed = new Seed()
    seed.create(bulb.getPointAt(i));

    // Rotate each seed so that it points out from the bulb
    seed.rotate(i * angle);
    seeds.push(seed);
}</code></pre>

This will make a circle of seeds around the bulb but leave a space in the middle. We’ll add a few more seeds to fill in the center. We’re giving the center seeds short stems so that they show the white of the wisps more than the beige of the stems.

<pre><code class="language-javascript">for (var i = 0; i &lt; 18; i++) {
    var seed = new Seed()
    var point = new Point(toPoint.x + random(-3, 3),
                          toPoint.y + random(-3, 3));
    seed.create(new Point(toPoint), true);
    seed.rotate(random(0, 360));
    seeds.push(seed);
}</code></pre>

The seeds in the middle will bunch randomly and make our dandelion look nicely messy. Now we can make them blow off.</p>

## Animating The Seeds

Wind pushes seeds in complex patterns, and two seeds will never blow off the same way. We want to make them look real, so we’ll need a little more randomness.

Reproducing real wind is much too complicated, so we’ll make the seeds float off in a random-looking pattern. Each seed is assigned a random point on the right side of the screen as a final destination:

<pre><code class="language-javascript">this.dest = new  Point(1800, random(-300, 1100));</code></pre>

The <code>rotateMove</code> function pushes each seed toward its destination point and rotates it. We can work with our Seed object as a group to rotate and move it with one function.

<pre><code class="language-javascript">this.rotateMove = function(/*int*/ angle) {
    if (this.group.position.x &lt; 850 &amp;&amp; this.group.position.y &lt; 650) {
        var vector = this.dest - this.group.position;
        this.group.position += vector / 150;

        this.angle += angle;
        this.group.rotate(angle);
    } else {
        this.isOffScreen = true
    }
}</code></pre>

This function will move the seed until it’s off the screen. Calling <code>rotateMove</code> for each frame of our animation will make the seed float across the screen.

Paper.js gives us an easy way to make animations with the <code>onFrame</code> function; when we implement <code>onFrame</code>, Paper.js will call it for every frame of our animation. With each frame, we iterate over each seed and move it across the screen.

<pre><code class="language-javascript">function onFrame(event) {
    for (var i = 0; i &lt; seedCount; i++) {
        if (!seeds[i].isOffscreen()) {
            seeds[i].rotateMove(random(2, 4));
        }
    }
}</code></pre>

The seeds slide and rotate a little closer to the destination point with each frame of the animation. Starting all of the seeds at the same point and ending them far apart makes them space out nicely as they move.

<img title="Dandelion seeds offscreen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12a658e6-a911-4832-8201-844fb233bc99/dandelion-seed-offscreen2.png" alt="screenshot" width="500" />

We don’t want all of the seeds to fall off at once, so we’ll use a timer to make them drift away.

<pre><code class="language-javascript">function start() {
    var id = setInterval(function() {
        seedCount++;
        if (seedCount === seeds.length) {
            clearInterval(id);
        }
    }, 1000);
}</code></pre>

The timer waits for one second before releasing the next seed, giving our dandelion a nice floaty feel.

Some green grass and blue sky as a background image for our <code>canvas</code> puts it all into context. Now we have a dandelion with seeds floating on the breeze.

<a href="https://zgrossbart.github.com/Dandelion"><img title="See the animation running and edit the code" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6781bab7-b8af-443d-8752-5a5868130a2e/dandelion.jpg" alt="screenshot" width="500" /></a>

See the dandelion <a href="https://zgrossbart.github.com/Dandelion/">running here</a>. You can edit and run the source code as part of the animation or download it from the <a href="https://github.com/zgrossbart/Dandelion">dandelion GitHub page</a>.</p>

## Paper.js In The Real World

Paper.js has some impressive examples and a nice coding model, but you should know a few gotchas before using it on your website.</p>

### It Doesn’t Work In Old Browsers

All Paper.js drawings use the <code>canvas</code> tag and require HTML5. This means that you need Internet Explorer 9+, Firefox 4+, Safari 5+ or Chrome. If your website must support older browsers, then you won’t be able to use <code>canvas</code>.

There’s no way around this requirement; if you need older browsers, you’re out of luck. As the Paper.js website says, “<a href="https://paperjs.org/about/#browser-support">Let’s go forward!</a>.”

### Performance Can Be Slow

Paper.js can make a browser grind to a halt even if the browser supports HTML5. Pixar renders Buzz and Woody on giant server farms — all you get is your user’s cheap MacBook.

Not only are laptops slower than server clusters, but browsers make things worse by rendering the <code>canvas</code> tag with the <a href="https://en.wikipedia.org/wiki/CPU">CPU</a> instead of the <a href="https://en.wikipedia.org/wiki/GPU">GPU</a>. Games like Halo and Rage take advantage of the graphics processor on your video card to render rocket launchers and mutants. The CPU is less efficient with graphics, so the same computer that handles complex video games smoothly can make floating dandelion seeds look slow and jerky.

Make sure to test all of your animations with slower hardware, and watch the CPU usage. Use groups to minimize the calculations, and be very careful about what you do in each invocation of the <code>onFrame</code> function.</p>

### Mobile Devices Are Slower

Mobile performance is even worse. Most mobile devices support <code>canvas</code>, but they are mostly too slow to render <code>canvas</code> animations well. Even more powerful devices, like the iPad 2, can’t handle the dandelion seeds smoothly.</p>

### It Doesn’t Support Object-Level Events

<pre><code class="language-javascript">var stem = new Path();
stem.strokeColor = '#567e37';
stem.strokeWidth = 1;
stem.add(new Point(p.x + 2, p.y));

var throughPoint = new Point(p.x + 4, p.y - height / 2);
var toPoint = new Point(p.x + 3, p.y - height);
stem.arcTo(throughPoint, toPoint);</code></pre>

The wisps are more arcs with a circle at the end of each line. Each seed has a random number of wisps that start at the top of the stem arc and curve out in different directions. Randomness makes them look a little bit messy and thus more natural. Each seed gets a random number of wisps, between 4 and 10.

<pre><code class="language-javascript">for (var i = 0; i &lt; random(4, 10); i++) {
    path = new Path();
    path.strokeColor = '#fff3c9';
    path.strokeWidth = 1;

    var p1 = new Point(p.x, p.y);
    path.add(new Point(p1.x + 2, p1.y + 2));

    // Each flutter extends a random amount up in the air
    var y = random(1, 5);

    // We draw every other stem on the right or the left so they're
    // spaced out in the seed.
    if (i % 2 == 0) {
        throughPoint = new Point(p1.x + random(1, 3), p1.y - y);
        toPoint = new Point(p1.x + random(5, 35), p1.y - 20 - y);
    } else {
        throughPoint = new Point(p1.x - random(1, 3), p1.y - y);
        toPoint = new Point(p1.x - random(5, 35), p1.y - 20 - y);
    }

    path.arcTo(throughPoint, toPoint);

    // Now we put the circle at the tip of the flutter.
    circle = new Path.Circle(toPoint, 2);
    circle.fillColor = '#fff3c9';
}</code></pre>

Now that we’ve drawn the seed, we need to manage it; later, we’ll want to move and rotate it. The seed is made up of a lot of parts, and we don’t want to have to manage each one separately. Paper.js has a nice <a href="https://paperjs.org/reference/group">group</a> object. Groups associate a set of objects together so that we can manipulate them all at once.

<pre><code class="language-javascript">var group = new Group();
group.addChild(bottom);
group.addChild(stem);

this.group = group;</code></pre>

The last step is to package our seed into a reusable object called <code>Seed</code>. We add all of the code we’ve been writing to a new function with the name <code>Seed</code> and add a function to create the initial variables. This example calls that function <code>create</code>, but you can name it anything you want.

<pre><code class="language-javascript">function Seed() {

    this.create = function (/*Point*/ p, /*boolean*/ shortStem) {
    …</code></pre>

The <code>create</code> function draws the seed at the specified <a href="https://paperjs.org/reference/point">Point</a>, and the <code>shortStem</code> boolean tells us whether this is a short stem. We’ll look at short-stemmed seeds a little later.

These types of functions don’t work as <a href="https://en.wikipedia.org/wiki/Constructor_(object-oriented_programming)">constructors</a> in JavaScript, but are supported in PaperScript.

<pre><code class="language-javascript">var seed = new Seed()
seed.create(new Point(100, 100), false);</code></pre>

Our seeds will look like this when we draw them:

<img title="Dandelion seed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6657898b-6dbe-4b7a-92fb-c28296eb453c/seed.png" alt="screenshot" width="360" height="295" />

The <code>Seed</code> object draws our random dandelion seeds. Now we can add them to our flower.</p>

## Adding A Little Chaos

The seeds will look better when we space them out around the circle of our dandelion bulb to feel like a halo of seeds. The bulb is a circle, and the circle is a path, so we can get each point on the path.

<pre><code class="language-javascript">var bulb = new Path.Circle(toPoint, 10); bulb.fillColor = '#567e37';

var angle = 360 / bulb.length;
var seeds = [];

for (var i = 0; i &lt; bulb.length; i++) {
    var seed = new Seed()
    seed.create(bulb.getPointAt(i));

    // Rotate each seed so that it points out from the bulb
    seed.rotate(i * angle);
    seeds.push(seed);
}</code></pre>

This will make a circle of seeds around the bulb but leave a space in the middle. We’ll add a few more seeds to fill in the center. We’re giving the center seeds short stems so that they show the white of the wisps more than the beige of the stems.

<pre><code class="language-javascript">for (var i = 0; i &lt; 18; i++) {
    var seed = new Seed()
    var point = new Point(toPoint.x + random(-3, 3),
                          toPoint.y + random(-3, 3));
    seed.create(new Point(toPoint), true);
    seed.rotate(random(0, 360));
    seeds.push(seed);
}</code></pre>

The seeds in the middle will bunch randomly and make our dandelion look nicely messy. Now we can make them blow off.</p>

## Animating The Seeds

Wind pushes seeds in complex patterns, and two seeds will never blow off the same way. We want to make them look real, so we’ll need a little more randomness.

Reproducing real wind is much too complicated, so we’ll make the seeds float off in a random-looking pattern. Each seed is assigned a random point on the right side of the screen as a final destination:

<pre><code class="language-javascript">this.dest = new  Point(1800, random(-300, 1100));</code></pre>

The <code>rotateMove</code> function pushes each seed toward its destination point and rotates it. We can work with our Seed object as a group to rotate and move it with one function.

<pre><code class="language-javascript">this.rotateMove = function(/*int*/ angle) {
    if (this.group.position.x &lt; 850 &amp;&amp; this.group.position.y &lt; 650) {
        var vector = this.dest - this.group.position;
        this.group.position += vector / 150;

        this.angle += angle;
        this.group.rotate(angle);
    } else {
        this.isOffScreen = true
    }
}</code></pre>

This function will move the seed until it’s off the screen. Calling <code>rotateMove</code> for each frame of our animation will make the seed float across the screen.

Paper.js gives us an easy way to make animations with the <code>onFrame</code> function; when we implement <code>onFrame</code>, Paper.js will call it for every frame of our animation. With each frame, we iterate over each seed and move it across the screen.

<pre><code class="language-javascript">function onFrame(event) {
    for (var i = 0; i &lt; seedCount; i++) {
        if (!seeds[i].isOffscreen()) {
            seeds[i].rotateMove(random(2, 4));
        }
    }
}</code></pre>

The seeds slide and rotate a little closer to the destination point with each frame of the animation. Starting all of the seeds at the same point and ending them far apart makes them space out nicely as they move.

<img title="Dandelion seeds offscreen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12a658e6-a911-4832-8201-844fb233bc99/dandelion-seed-offscreen2.png" alt="screenshot" width="500" />

We don’t want all of the seeds to fall off at once, so we’ll use a timer to make them drift away.

<pre><code class="language-javascript">function start() {
    var id = setInterval(function() {
        seedCount++;
        if (seedCount === seeds.length) {
            clearInterval(id);
        }
    }, 1000);
}</code></pre>

The timer waits for one second before releasing the next seed, giving our dandelion a nice floaty feel.

Some green grass and blue sky as a background image for our <code>canvas</code> puts it all into context. Now we have a dandelion with seeds floating on the breeze.

<a href="https://zgrossbart.github.com/Dandelion"><img title="See the animation running and edit the code" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6781bab7-b8af-443d-8752-5a5868130a2e/dandelion.jpg" alt="screenshot" width="500" /></a>

See the dandelion <a href="https://zgrossbart.github.com/Dandelion/">running here</a>. You can edit and run the source code as part of the animation or download it from the <a href="https://github.com/zgrossbart/Dandelion">dandelion GitHub page</a>.</p>

## Paper.js In The Real World

Paper.js has some impressive examples and a nice coding model, but you should know a few gotchas before using it on your website.</p>

### It Doesn’t Work In Old Browsers

All Paper.js drawings use the <code>canvas</code> tag and require HTML5. This means that you need Internet Explorer 9+, Firefox 4+, Safari 5+ or Chrome. If your website must support older browsers, then you won’t be able to use <code>canvas</code>.

There’s no way around this requirement; if you need older browsers, you’re out of luck. As the Paper.js website says, “<a href="https://paperjs.org/about/#browser-support">Let’s go forward!</a>.”

### Performance Can Be Slow

Paper.js can make a browser grind to a halt even if the browser supports HTML5. Pixar renders Buzz and Woody on giant server farms — all you get is your user’s cheap MacBook.

Not only are laptops slower than server clusters, but browsers make things worse by rendering the <code>canvas</code> tag with the <a href="https://en.wikipedia.org/wiki/CPU">CPU</a> instead of the <a href="https://en.wikipedia.org/wiki/GPU">GPU</a>. Games like Halo and Rage take advantage of the graphics processor on your video card to render rocket launchers and mutants. The CPU is less efficient with graphics, so the same computer that handles complex video games smoothly can make floating dandelion seeds look slow and jerky.

Make sure to test all of your animations with slower hardware, and watch the CPU usage. Use groups to minimize the calculations, and be very careful about what you do in each invocation of the <code>onFrame</code> function.</p>

### Mobile Devices Are Slower

Mobile performance is even worse. Most mobile devices support <code>canvas</code>, but they are mostly too slow to render <code>canvas</code> animations well. Even more powerful devices, like the iPad 2, can’t handle the dandelion seeds smoothly.</p>

### It Doesn’t Support Object-Level Events

Other drawing libraries, such as SVG (see below), support object-level mouse and keyboard events. Those events make it easy to respond when a path or a polygon is clicked, hovered over or touched.

The <code>canvas</code> tag doesn’t support object-level events. Paper.js has some basic functionality for <a href="https://paperjs.org/examples/hit-testing/">hit testing</a>, but it’s very low-level. You can listen for <a href="https://paperjs.org/tutorials/interaction/mouse-tool-events/">mouse</a> and <a href="https://paperjs.org/tutorials/interaction/keyboard-interaction/">keyboard</a> events on the whole canvas, but you’ll need to handle mapping those events to individual controls.</p>

## What About SVG?

The <a href="https://en.wikipedia.org/wiki/SVG">SVG</a> (Scalable Vector Graphics) specification was defined over 10 years ago, but came to the forefront with support libraries such as Raphaël.js, which make it easy to generate SVG images with JavaScript. SVG is powerful, works well for smaller images, and is supported all the way back to Internet Explorer 7 with conversion to <a href="https://en.wikipedia.org/wiki/VML">VML</a> (Vector Markup Language). SVG is the best choice if you need to support older browsers.

The real issues with SVG are speed, future support and mobile devices. Every browser maker is actively working on making <code>canvas</code> faster. Safari 5 already offers hardware acceleration with the GPU for <code>canvas</code>, and the rest are working on it. SVG is also unsupported on Android devices.

There’s a growing community around <code>canvas</code>, the new technology that vendors are focusing on. They’re adding new features, fixing bugs and making it better every day.</p>

## Other Canvas Drawing Libraries

Paper.js isn’t the only option for <code>canvas</code>. <a href="https://processingjs.org/">Processing.js</a>, from the <a href="https://ejohn.org/">creator of jQuery</a>, ports the <a href="https://en.wikipedia.org/wiki/Processing_(programming_language)">Processing</a> programming language to JavaScript. It supports animations and has <a href="https://processingjs.org/exhibition">many examples</a>.

The <a href="https://github.com/mrdoob/three.js/">three.js</a> engine supports <code>canvas</code> and the <a href="https://en.wikipedia.org/wiki/Webgl">WebGL</a> library, and it focuses more on 3-D drawings. <a href="https://www.dartlang.org/">Google Dart</a> will also support <code>canvas</code> with built-in rendering objects.

Paper.js is a mature library with a very supportive community on the <a href="https://groups.google.com/group/paperjs">Paper.js Google Group</a> and many impressive and well-documented examples. Check out some of the amazing things people are doing with it.</p>

## More Paper.js Examples

Our dandelion is just the beginning. Below are a few other impressive animations written in Paper.js.

*   [Examples](https://paperjs.org/examples/), Paper.js has a page full of incredible examples. [Voronoi](https://paperjs.org/examples/voronoi/) is one of the best. Make sure to press the space bar and see the paths. More examples are in the [GitHub folder](https://github.com/paperjs/paper.js/tree/master/examples).
*   [Nardove](https://nardove.com/), Ricardo Sánchez's Jellyfish are written with Paper.js and a koi pond written with Processing.js. Wait a minute, the jellies are shy.
*   “[Node Garden in Paper.js](https://barbariangroup.com/posts/8960-a_node_garden_in_paper_js),” Andrew Berg
*   “[The HBO Recycling Program](https://zgrossbart.github.com/hborecycling/)”An infographic that I created using Paper.js to show how often different HBO series use the same actors.
*   “[20 Multi-Touch Gestures You Should Learn Today](https://zgrossbart.github.com/touch_gestures/),” Zack Grossbart created the interactive tutorial with the help of Paper.js.

Where’s your Paper.js amazingness?

{{< signature "al" >}}

