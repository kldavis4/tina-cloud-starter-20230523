---
title: 'Web-Drawing Throwdown: Paper.js Vs. Processing.js Vs. Raphael'
slug: web-drawing-throwdown-paper-processing-raphael
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5670e6c8-178c-4ecd-8a95-b5faca4c06fb/poll-results-orange-illu.jpg
date: 2012-02-22T11:02:15.000Z
author: zack-grossbart
description: >-
  Paper.js, Processing.js and Raphaël are the leading libraries for drawing on
  the Web right now. A couple of others are up and coming, and you can always
  use Flash, but these three work well with HTML5 and have the widest support
  among browser vendors.
categories:
  - Coding
  - JavaScript
---
Before drawing anything in a browser, ask yourself three questions:

1.  **Do you need to support older browsers?** If the answer is yes, then your only choice is Raphaël. It handles browsers all the way back to IE 7 and Firefox 3\. Raphaël even has some support for IE 6, although some of its underlying technology cannot be implemented there.
2.  **Do you need to support Android?** Android doesn’t support SVG, so you’ll have to use [Paper.js](https://paperjs.org/) or [Processing.js](https://processingjs.org/). Some rumors say that Android 4 will handle SVG, but the majority of Android devices won’t support it for years.
3.  **Is your drawing interactive?** Raphaël and Paper.js focus on interaction with drawn elements through clicking, dragging and touch. Processing.js doesn’t support any object-level events, so responding to user gestures is very difficult. Processing.js can draw a cool animation on your home page, but the other tools are better for interactive applications.

Paper.js, Processing.js and Raphaël are the leading libraries for drawing on the Web right now. A couple of others are up and coming, and you can always use Flash, but these three work well with HTML5 and have the widest support among browser vendors.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Best Of Both Worlds: Mixing HTML5 And Native Code](https://www.smashingmagazine.com/2013/10/best-of-both-worlds-mixing-html5-native-code/)
*   [Web-Drawing Throwdown: Paper.js Vs. Processing.js Vs. Raphael](https://www.smashingmagazine.com/2012/02/web-drawing-throwdown-paper-processing-raphael/)
*   [How To Create Web Animations With Paper.js](https://www.smashingmagazine.com/2011/11/create-web-animations-with-paperjs/)
*   [Love Generating SVG With JavaScript? Move It To The Server!](https://www.smashingmagazine.com/2014/05/love-generating-svg-javascript-move-to-server/)

{{% feature-panel %}}

Choosing the right framework will determine the success of your project. This article covers the advantages and disadvantages of each, and the information you need to make the best choice.

All of the code in this article is open source and can be run on the <a href="https://zgrossbart.github.com/3gears/">demo page</a> that accompanies this article.

.toc {
width: 100%;
margin: 1em 0;
border: 1px solid rgba(0,0,0,0.1); }
.toc td, .toc th {
padding: 4px 10px;
border-bottom: 1px solid #eee;
border-right: 1px solid #eee;
border-collapse: collapse;
text-align: left;
}
.toc th {
background-color: #ECECEC;
}

## Overview

<table class="toc"><br>
<tbody>
<tr>
<th></th>
<th>Paper.js</th>
<th>Processing.js</th>
<th>Raphaël</th>
</tr>
<tr>
<th>Technology</th>
<td><code>canvas</code> tag</td>
<td><code>canvas</code> tag</td>
<td>SVG</td>
</tr>
<tr>
<th>Language</th>
<td>PaperScript</td>
<td>Processing script</td>
<td>JavaScript</td>
</tr>
<tr>
<th>Browsers</th>
<td>IE 9</td>
<td>IE 9</td>
<td>IE 7</td>
</tr>
<tr>
<th>Mobile</th>
<td>Yes</td>
<td>Yes</td>
<td>iOS only</td>
</tr>
<tr>
<th>Model</th>
<td>Vector and raster</td>
<td>Raster</td>
<td>Vector</td>
</tr>
<tr>
<th>Size</th>
<td>56 KB</td>
<td>64 KB</td>
<td>20 KB</td>
</tr>
</tbody>
</table>
&nbsp;

It’s all JavaScript once the page runs, but the frameworks take different paths to get there. Raphaël is written directly in JavaScript, but Paper.js uses PaperScript, and Processing.js uses its own script. They all support Firefox, Chrome and Safari, but Internet Explorer is an issue — Paper.js and Processing.js use the <code>canvas</code> tag and thus require IE 9.

PaperScript is a JavaScript extension that makes it possible to write scripts that don’t pollute the global namespace. This cuts down on JavaScript conflicts. PaperScript also supports direct math on objects such as <a href="https://paperjs.org/reference/point"><code>Point</code></a> and <a href="https://paperjs.org/reference/size"><code>Size</code></a>: you can add two points together as if they were numbers.

Processing.js is based on a framework named <a href="https://processing.org/">Processing</a>, which runs in the Java Virtual Machine. You define <code>int</code> and <code>float</code> instead of <code>var</code>, and you can use classes with Java-style inheritance. While the Processing.js script looks a little like Java, it’s more like JavaScript and doesn’t require many of the more complex features of Java.

Using all three libraries is easy if you have some familiarity with JavaScript.</p>

## Getting Started

Start by importing each library. The process for setting each up is a little different.</p>

### Setting Up Paper.js

<pre><code class="language-markup tmp-html">&lt;head&gt;
&lt;script src="paper.js" type="text/javascript" charset="utf-8"&gt;&lt;/script&gt;
&lt;script type="text/paperscript" canvas="paperCircle" src="paper_circle.pjs" id="script"&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;canvas id="paperCircle" class="canvas" width="200" height="200" style="background-color: white;"&gt;&lt;/canvas&gt;</code></pre>

Paper.js specifies a script type of <code>text/paperscript</code> and the ID of the <code>canvas</code> tag that you’ll draw on. It uses that ID to know where to draw.</p>

### Setting Up Processing.js

<pre><code class="language-markup tmp-html">&lt;head&gt;
&lt;script src="processing.js" type="text/javascript" charset="utf-8"&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;canvas width="200" height="200" class="canvas" data-processing-sources="processing_circle.java"&gt;&lt;/canvas&gt;</code></pre>

Processing.js uses the <code>data-processing-sources</code> attribute of the <code>canvas</code> tag to import your drawing. I use a <code>.java</code> extension for Processing’s source file so that my editor color-codes it properly. Some authors use a <code>.pde</code> or <code>.pjs</code> extension. It’s up to you.</p>

### Setting Up Raphaël

<pre><code class="language-markup tmp-html">&lt;head&gt;
&lt;script src="raphael-min.js" type="text/javascript" charset="utf-8"&gt;&lt;/script&gt;
&lt;script src="raphael_circle.js" type="text/javascript" charset="utf-8"&gt;&lt;/script&gt;
&lt;/head&gt;</code></pre>

Raphaël is imported like any other JavaScript file. It works well with jQuery’s <a href="https://api.jquery.com/ready/"><code>ready</code></a> function or any other JavaScript framework.

Now we can start drawing.</p>

## Object-Oriented Drawing

Both Paper.js and Raphaël use object-oriented drawing: you draw a circle and get back a circle object. Processing.js draws the circle and doesn’t give you anything back. The following simple example makes it clear. Let’s start with a circle in the middle of the screen at point <code>100,100</code>.

<a href="https://zgrossbart.github.com/3gears/"><img style="border: 0px initial initial" title="Circle" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21858a30-369c-415a-8e07-f2a5c3f17a5a/circle.png" alt="" width="215" height="215" /></a>

<strong>Paper.js:</strong>

<pre><code class="language-javascript">var circle = new Path.Circle(new Point(100, 100), 10);
circle.fillColor = '#ee2a33';</code></pre>

<strong>Raphaël:</strong>

<pre><code class="language-javascript">var paper = Raphael('raphaelCircle', 200, 200);
var c = paper.ellipse(100, 100, 10, 10);
c.attr({'fill': '#00aeef', 'stroke': '#00aeef'});</code></pre>

<strong>Processing.js:</strong>

<pre><code class="language-javascript">void setup() {
   size(200, 200);
}

void draw() {
   background(#ffffff);
   translate(100, 100);
   fill(#52b755);
   noStroke();
   ellipse(0, 0, 20, 20);
}</code></pre>

Each code snippet draws the same circle. The difference is in what you can do with it.

Paper.js creates the circle as a <a href="https://paperjs.org/reference/path">path</a> object. We can hold onto the object and change it later. In Paper.js, <code>circle.fillColor = 'red';</code> fills our circle with red, and <code>circle.scale(2)</code> makes it twice as big.

Raphaël follows Paper.js’ object-oriented model. In Raphaël, we can change the color of our circle with <code>circle.attr('fill', 'red');</code>, and scale it up with <code>circle.scale(2, 2);</code>. The point is that the circle is an object that we can work with later.

Processing.js doesn’t use objects; the <code>ellipse</code> function doesn’t return anything. Once we’ve drawn our circle in Processing.js, it’s part of the rendered image, like ink on a page; it’s not a separate object that can be changed by modifying a property. To change the color, we have to draw a new circle directly on top of the old one.

When we call <a href="https://processingjs.org/reference/fill_"><code>fill</code></a>, it changes the fill color for every object we draw thereafter. After we call <a href="https://processingjs.org/reference/translate_"><code>translate</code></a> and <code>fill</code>, every shape will be filled with green.

Because functions change everything, we can easily end up with unwanted side effects. Call a harmless function, and suddenly everything is green! Processing.js provides the <a href="https://processingjs.org/reference/pushMatrix_"><code>pushMatrix</code></a> and <a href="https://processingjs.org/reference/popMatrix_"><code>popMatrix</code></a> functions to isolate changes, but you have to remember to call them.

Processing.js’ no-objects philosophy means that complex drawings run faster. Paper.js and Raphaël contain references to everything you draw, and so the memory overhead created by complex animations will slow down your application. Processing.js contains no references to drawn elements, so each shape takes up a tiny amount of memory. Memory overhead pays off if you need to access an object later, but it’s overkill if you don’t. Paper.js gives you a way out of this with the <a href="https://paperjs.org/features/#symbols"><code>Symbol</code></a> object and by rasterizing objects, but you have to plan ahead to keep the app running fast.

The object-oriented versus no-objects philosophy has implications for everything you do with these libraries. It shapes the way each library handles animations.

## Let’s Make It Move

Rotating circles aren’t very interesting, so we’ll make a square rotate around a circle.

<a href="https://zgrossbart.github.com/3gears/"><img style="border: 0px initial initial" title="Animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/314e21fa-03b8-4cf2-bf96-082b2af70971/anim.png" alt="" width="213" height="213" /></a>

### Animation in Processing.js

Processing.js supports animation with the predefined <a href="https://processingjs.org/reference/setup_"><code>setup</code></a> and <a href="https://processingjs.org/reference/draw_"><code>draw</code></a> functions, like this:

<pre><code class="language-javascript">float angle = 0.0;
void setup() {
   size(200, 200);
   frameRate(30);
}

void draw() {
   background(#ffffff);
   translate(100, 100);
   fill(#52b755);
   noStroke();
   ellipse(0, 0, 20, 20);

   rotate(angle);
   angle += 0.1;
   noFill();
   stroke(#52b755);
   strokeWeight(2);
   rect(-40, -40, 80, 80);
}</code></pre>

The <code>setup</code> function is called once when the application starts. We tell Processing.js to animate with a frame rate of 30 frames per second, so our <code>draw</code> function will be called 30 times every second. That rate might sound high, but it’s normal for making an animation look smooth.

The <code>draw</code> function starts by filling in the background of the <code>canvas</code>; it paints over anything left over from previous invocations of the <code>draw</code> function. This is a major difference with Processing.js: we are not manipulating objects, so we always have to clean up previously drawn shapes.

Next, we translate the coordinate system to the <code>100,100</code> point. This positions the drawing at 100 pixels from the left and 100 pixels from the top of the canvas for every drawing until we reset the coordinates. Then, we rotate by the specified angle. The angle increases with every <code>draw</code>, which makes the square spin around. The last step is to draw a square using the <a href="https://processingjs.org/reference/fill_"><code>fill</code></a> and <a href="https://processingjs.org/reference/rect_"><code>rect</code></a> functions.

The <code>rotate</code> function in Processing.js normally takes <a href="https://en.wikipedia.org/wiki/Radians">radians</a> instead of <a href="https://en.wikipedia.org/wiki/Degree_(angle)">degrees</a>. That’s why we increase the angle of each frame by 0.2, rather than a higher number such as 3. This is one of many times when trigonometry shows up in this method of drawing.</p>

### Animation in Paper.js

Paper.js makes this simple animation easier than in Processing.js, with a persistent rectangle object:

<pre><code class="language-javascript">var r;

function init() {
   var c = new Path.Circle(new Point(100, 100), 10);
   c.fillColor = '#ee2a33';

   var point = new Point(60, 60);
   var size = new Size(80, 80);
   var rectangle = new Rectangle(point, size);
   r = new Path.Rectangle(rectangle);
   r.strokeColor = '#ee2a33';
   r.strokeWidth = 2;
}

function onFrame(event) {
   r.rotate(3);
}

init();</code></pre>

We maintain the state of our square as an object, and Paper.js handles drawing it on the screen. We rotate it a little for each frame. Paper.js manages the path, so we don’t have to redraw everything for each frame or keep track of the angle of rotation or worry about affecting other objects.</p>

### Animation in Raphaël

Animations in Raphaël are written in standard JavaScript, so Raphaël doesn’t have specific functions for handling animation frames. Instead, we rely on JavaScript’s <code>setInterval</code> function.

<pre><code class="language-javascript">var paper = Raphael('raphaelAnimation', 200, 200);
var c = paper.ellipse(100, 100, 10, 10);
c.attr({
   'fill': '#00aeef',
   'stroke': '#00aeef'
});

var r = paper.rect(60, 60, 80, 80);
r.attr({
   'stroke-width': 2,
   'stroke': '#00aeef'
});

setInterval(function() {
   r.rotate(6);
}, 33);</code></pre>

Raphaël is similar to Paper.js in its object-oriented approach. We have a square, and we call a <code>rotate</code> function on it. Thus, we can easily spin the square with a small amount of code.</p>

## Interaction

Raphaël shines when you need to enable interactivity in a drawing. It provides an event model similar to JavaScript’s, making it easy to detect clicks, drags and touches. Let’s make our square clickable.

<a href="https://zgrossbart.github.com/3gears/"><img style="border: 0px initial initial" title="Square" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83902da8-b7c6-411f-8e18-0fe36c0f30f4/square.png" alt="" width="212" height="212" /></a>

### Interactions With Raphaël

<pre><code class="language-javascript">var paper = Raphael('raphaelInteraction', 200, 200);
var r = paper.rect(60, 60, 80, 80);
r.attr({'fill': '#00aeef', 'stroke': '#00aeef'});

var clicked = false;

r.click(function() {
   if (clicked) {
      r.attr({'fill': '#00aeef', 'stroke': '#00aeef'});
   } else {
      r.attr({'fill': '#f00ff0', 'stroke': '#f00ff0'});
   }
   clicked = !clicked;
});</code></pre>

The <code>click</code> function in Raphaël works like jQuery, and you can add it to any object. Once we get the click event, changing the color of the square is easy. Raphaël has more functions to support dragging, hovering and all of the other user interactions you expect from JavaScript.</p>

### Interactions With Paper.js

Paper.js has a different way of managing interactions, but it’s still pretty easy:

<pre><code class="language-javascript">var hitOptions = {
   fill: true,
   tolerance: 5
};

function init() {
   var point = new Point(60, 60);
   var size = new Size(80, 80);
   var rectangle = new Rectangle(point, size);
   r = new Path.Rectangle(rectangle);
   r.fillColor = '#ee2a33';
}

function onMouseUp(event) {
   var hitResult = project.hitTest(event.point, hitOptions);

   if (hitResult &amp;&amp; hitResult.item) {
      if (hitResult.item.clicked) {
         hitResult.item.fillColor = '#ee2a33';
      } else {
         hitResult.item.fillColor = '#f00ff0';
      }

      hitResult.item.clicked = !hitResult.item.clicked;
   }
}

init();</code></pre>

Paper.js deals with mouse gestures through a concept called “<a href="https://paperjs.org/examples/hit-testing/">hit testing</a>.” A hit finds the point under the mouse cursor and figures out which object it lies above. Hit options enable you to define how the hit works: you can set options for such things as how close the mouse has to be, and whether the middle of the object counts or only the edge. We can extend this hit test to any object or group of objects in Paper.js.

The Paper.js team added object-level events similar to Raphaël’s a few weeks ago. The events should show up in the next release.</p>

### Interactions With Processing.js

Processing.js makes detecting mouse clicks tricky. It doesn’t support object-level events or hit testing, so we’re pretty much on our own.

<pre><code class="language-javascript">float bx;
float by;
int bs = 20;
boolean bover = false;
boolean clicked = false;

void setup() {
   size(200, 200);
   bx = width/2.0;
   by = height/2.0;
   noStroke();
   fill(#52b755);
   frameRate(10);
}

void draw() {
   background(#ffffff);

   // Test if the cursor is over the box
   if (mouseX &gt; bx-bs &amp;&amp; mouseX &lt; bx+bs &amp;&amp;        mouseY &gt; by-bs &amp;&amp; mouseY &lt; by+bs) {
      bover = true;
   } else {
      bover = false;
   }

   translate(100, 100);
   rect(-40, -40, 80, 80);
}

void mousePressed() {
   if (bover) {
      if (clicked) {
         fill(#52b755);
      } else {
         fill(#f00ff0);
      }
      clicked = !clicked;
   }
}</code></pre>

Once Processing.js draws the square, it forgets about it. We want the color of the square to change when we click on it, but the script doesn’t know that, so we have to do all of the calculations ourselves. The <code>draw</code> function detects the mouse cursor’s position and does the math to determine whether it lies within the square.

The code is not too bad for the square, but our circle would need <code>pr<sup>2</sup></code>. And more complex shapes such as ovals, curves and compound shapes would require even more math.</p>

## No Clear Winner

Each framework has its advantages. Between them, the features make for cool demos and even cooler applications.</p>

### Showing Off Paper.js

Paper.js excels at manipulating complex shapes. It can turn, twist and transform any object in hundreds of ways. These transforms make it easy to convert objects based on interactive gestures. The new Google Music Tour, which makes colored lines beat in time to music, shows how one can make complex changes on simple shapes.

The other wow factor in Paper.js is its support of <a href="https://en.wikipedia.org/wiki/Raster_graphics">raster graphics</a>. Paper.js can completely change the way images are drawn — including by turning them into <a href="https://paperjs.org/examples/spiral-raster/">spirals</a> and <a href="https://paperjs.org/examples/q-bertify/">Q*bert</a> boards.

<a href="https://paperjs.org/examples/spiral-raster/"><img title="Mona Lisa Spiral Raster" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dbb9a2c-2b3b-4866-a529-83a354a9c5fb/lisa.png" alt="" width="450" height="450" /></a>

### Showing Off Processing.js

Processing.js’ biggest feature is speed, making it possible to draw complex animations on slower machines. <a href="https://processingjs.org/exhibition">Many examples</a> are out there, but the fluidity of Processing.js animations shows up best in Ricardo Sánchez’s <a href="https://nardove.com/">koi pond</a>.

<a href="https://nardove.com/"><img class="aligncenter size-full wp-image-118838" title="Koi Pond" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/217097dc-c8e6-4629-8473-f81767733460/fish2.png" alt="" width="398" height="398" /></a>

The swishing of the tails and waving of the bodies make the koi look very natural. Processing.js makes this easy, with support for curves and customized animations.

Processing.js also supports complex drawing elements such as shading, lighting and 3-D transforms. If you want to create complex animations in <code>canvas</code> very quickly, then Processing.js is the clear winner.</p>

### Showing Off Raphaël

The best feature of Raphaël is its support for Internet Explorer 7 and 8. If your application has to run on older browsers, then Raphaël is the only option.

The other big feature of Raphaël is its community. Raphaël is older than Paper.js and Processing.js and thus has had more time to build examples, tutorials and user support. It has built-in support for easing, animation transforms and the event handlers that we saw in the interaction example; it also has a comprehensive charting library.

<img title="Raphael Graphs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dde175c4-344e-4db9-8cb0-abb0679fba6b/graphs.png" alt="" width="450" height="341" />

Raphaël also has the best tooling support.</p>

## The Tools

If you’ve worked with Flash, the lack of tools for these frameworks will disappoint you. Many of the frameworks will edit SVG images, but none of them offer a drag-and-drop method for creating applications.

A few simple tools are out there, but they are more like proofs of concept than actual products. Adobe is working on a tool named <a href="https://success.adobe.com/en/na/sem/products/edge.html?sdid=JAPEL&amp;skwcid=TC|23230|HTML5%20animation%20tools||S|b|8325947226">Edge</a>, but it has a long way to go.

If you want to drag and drop, then Web animations aren’t for you yet. Right now, this method of drawing is more like video-game programming. Writing code to draw a circle is tougher than clicking and dragging, but it scales to more complex applications and some fun stuff.</p>

## Let’s Build Something Real

So far, we’ve looked at some simple examples, seen the best features of each platform and looked at how to choose the right one. Each framework has pluses and minuses, but judging them is difficult until you create an actual application.

To compare each framework, I’ve drawn some gears. Each gear is made up of two circles, with a set of teeth around the outer circle.

<img title="Gear" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bfe4266-3023-4e70-95d1-4f8196203f8b/gear.png" alt="" width="206" height="206" />

When the shapes are all given the same color, they look just like a gear.

<pre><code class="language-javascript">var paper = Raphael('raphaelAnimation', 200, 200);
var c = paper.ellipse(100, 100, 10, 10);
c.attr({
   'fill': '#00aeef',
   'stroke': '#00aeef'
});

var r = paper.rect(60, 60, 80, 80);
r.attr({
   'stroke-width': 2,
   'stroke': '#00aeef'
});

setInterval(function() {
   r.rotate(6);
}, 33);</code></pre>

Raphaël is similar to Paper.js in its object-oriented approach. We have a square, and we call a <code>rotate</code> function on it. Thus, we can easily spin the square with a small amount of code.</p>

## Interaction

Raphaël shines when you need to enable interactivity in a drawing. It provides an event model similar to JavaScript’s, making it easy to detect clicks, drags and touches. Let’s make our square clickable.

<a href="https://zgrossbart.github.com/3gears/"><img style="border: 0px initial initial" title="Square" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83902da8-b7c6-411f-8e18-0fe36c0f30f4/square.png" alt="" width="212" height="212" /></a>

### Interactions With Raphaël

<pre><code class="language-javascript">var paper = Raphael('raphaelInteraction', 200, 200);
var r = paper.rect(60, 60, 80, 80);
r.attr({'fill': '#00aeef', 'stroke': '#00aeef'});

var clicked = false;

r.click(function() {
   if (clicked) {
      r.attr({'fill': '#00aeef', 'stroke': '#00aeef'});
   } else {
      r.attr({'fill': '#f00ff0', 'stroke': '#f00ff0'});
   }
   clicked = !clicked;
});</code></pre>

The <code>click</code> function in Raphaël works like jQuery, and you can add it to any object. Once we get the click event, changing the color of the square is easy. Raphaël has more functions to support dragging, hovering and all of the other user interactions you expect from JavaScript.</p>

### Interactions With Paper.js

Paper.js has a different way of managing interactions, but it’s still pretty easy:

<pre><code class="language-javascript">var hitOptions = {
   fill: true,
   tolerance: 5
};

function init() {
   var point = new Point(60, 60);
   var size = new Size(80, 80);
   var rectangle = new Rectangle(point, size);
   r = new Path.Rectangle(rectangle);
   r.fillColor = '#ee2a33';
}

function onMouseUp(event) {
   var hitResult = project.hitTest(event.point, hitOptions);

   if (hitResult &amp;&amp; hitResult.item) {
      if (hitResult.item.clicked) {
         hitResult.item.fillColor = '#ee2a33';
      } else {
         hitResult.item.fillColor = '#f00ff0';
      }

      hitResult.item.clicked = !hitResult.item.clicked;
   }
}

init();</code></pre>

Paper.js deals with mouse gestures through a concept called “<a href="https://paperjs.org/examples/hit-testing/">hit testing</a>.” A hit finds the point under the mouse cursor and figures out which object it lies above. Hit options enable you to define how the hit works: you can set options for such things as how close the mouse has to be, and whether the middle of the object counts or only the edge. We can extend this hit test to any object or group of objects in Paper.js.

The Paper.js team added object-level events similar to Raphaël’s a few weeks ago. The events should show up in the next release.</p>

### Interactions With Processing.js

Processing.js makes detecting mouse clicks tricky. It doesn’t support object-level events or hit testing, so we’re pretty much on our own.

<pre><code class="language-javascript">float bx;
float by;
int bs = 20;
boolean bover = false;
boolean clicked = false;

void setup() {
   size(200, 200);
   bx = width/2.0;
   by = height/2.0;
   noStroke();
   fill(#52b755);
   frameRate(10);
}

void draw() {
   background(#ffffff);

   // Test if the cursor is over the box
   if (mouseX &gt; bx-bs &amp;&amp; mouseX &lt; bx+bs &amp;&amp;        mouseY &gt; by-bs &amp;&amp; mouseY &lt; by+bs) {
      bover = true;
   } else {
      bover = false;
   }

   translate(100, 100);
   rect(-40, -40, 80, 80);
}

void mousePressed() {
   if (bover) {
      if (clicked) {
         fill(#52b755);
      } else {
         fill(#f00ff0);
      }
      clicked = !clicked;
   }
}</code></pre>

Once Processing.js draws the square, it forgets about it. We want the color of the square to change when we click on it, but the script doesn’t know that, so we have to do all of the calculations ourselves. The <code>draw</code> function detects the mouse cursor’s position and does the math to determine whether it lies within the square.

The code is not too bad for the square, but our circle would need <code>pr<sup>2</sup></code>. And more complex shapes such as ovals, curves and compound shapes would require even more math.</p>

## No Clear Winner

Each framework has its advantages. Between them, the features make for cool demos and even cooler applications.</p>

### Showing Off Paper.js

Paper.js excels at manipulating complex shapes. It can turn, twist and transform any object in hundreds of ways. These transforms make it easy to convert objects based on interactive gestures. The new Google Music Tour, which makes colored lines beat in time to music, shows how one can make complex changes on simple shapes.

The other wow factor in Paper.js is its support of <a href="https://en.wikipedia.org/wiki/Raster_graphics">raster graphics</a>. Paper.js can completely change the way images are drawn — including by turning them into <a href="https://paperjs.org/examples/spiral-raster/">spirals</a> and <a href="https://paperjs.org/examples/q-bertify/">Q*bert</a> boards.

<a href="https://paperjs.org/examples/spiral-raster/"><img title="Mona Lisa Spiral Raster" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dbb9a2c-2b3b-4866-a529-83a354a9c5fb/lisa.png" alt="" width="450" height="450" /></a>

### Showing Off Processing.js

Processing.js’ biggest feature is speed, making it possible to draw complex animations on slower machines. <a href="https://processingjs.org/exhibition">Many examples</a> are out there, but the fluidity of Processing.js animations shows up best in Ricardo Sánchez’s <a href="https://nardove.com/">koi pond</a>.

<a href="https://nardove.com/"><img class="aligncenter size-full wp-image-118838" title="Koi Pond" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/217097dc-c8e6-4629-8473-f81767733460/fish2.png" alt="" width="398" height="398" /></a>

The swishing of the tails and waving of the bodies make the koi look very natural. Processing.js makes this easy, with support for curves and customized animations.

Processing.js also supports complex drawing elements such as shading, lighting and 3-D transforms. If you want to create complex animations in <code>canvas</code> very quickly, then Processing.js is the clear winner.</p>

### Showing Off Raphaël

The best feature of Raphaël is its support for Internet Explorer 7 and 8. If your application has to run on older browsers, then Raphaël is the only option.

The other big feature of Raphaël is its community. Raphaël is older than Paper.js and Processing.js and thus has had more time to build examples, tutorials and user support. It has built-in support for easing, animation transforms and the event handlers that we saw in the interaction example; it also has a comprehensive charting library.

<img title="Raphael Graphs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dde175c4-344e-4db9-8cb0-abb0679fba6b/graphs.png" alt="" width="450" height="341" />

Raphaël also has the best tooling support.</p>

## The Tools

If you’ve worked with Flash, the lack of tools for these frameworks will disappoint you. Many of the frameworks will edit SVG images, but none of them offer a drag-and-drop method for creating applications.

A few simple tools are out there, but they are more like proofs of concept than actual products. Adobe is working on a tool named <a href="https://success.adobe.com/en/na/sem/products/edge.html?sdid=JAPEL&amp;skwcid=TC|23230|HTML5%20animation%20tools||S|b|8325947226">Edge</a>, but it has a long way to go.

If you want to drag and drop, then Web animations aren’t for you yet. Right now, this method of drawing is more like video-game programming. Writing code to draw a circle is tougher than clicking and dragging, but it scales to more complex applications and some fun stuff.</p>

## Let’s Build Something Real

So far, we’ve looked at some simple examples, seen the best features of each platform and looked at how to choose the right one. Each framework has pluses and minuses, but judging them is difficult until you create an actual application.

To compare each framework, I’ve drawn some gears. Each gear is made up of two circles, with a set of teeth around the outer circle.

<img title="Gear" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bfe4266-3023-4e70-95d1-4f8196203f8b/gear.png" alt="" width="206" height="206" />

When the shapes are all given the same color, they look just like a gear.

<img title="Solid gear" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af01c938-d4dd-430f-ab06-95eac8c85f20/gear-solid.png" alt="" width="206" height="206" />

Every gear will rotate a little with each frame of the animation. The first gear will be given a speed, and the rest will move relative to it. The gears will arrange, mesh and rotate together with a crazy amount of trigonometry. Put them together and you’ve got a complex gear system.

Paper.js:

<a href="https://zgrossbart.github.com/3gears/paper_gears.html"><img title="Paper.js gears" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f20e5742-447d-4fde-a2f6-3d60b1279e50/paper-gears.png" alt="" width="450" height="306" /></a>

Processing.js:

<a href="https://zgrossbart.github.com/3gears/processing_gears.html"><img title="Processing.js gears" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98595e13-90c3-4f66-ab3d-d025cfcc2b1a/processing-gears.png" alt="" width="450" height="305" /></a>

Raphaël:

<a href="https://zgrossbart.github.com/3gears/raphael_gears.html"><img title="Raphael gears" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64fb189c-29c8-4f8a-b483-fc4dd24ac52e/raphael-gears2.png" alt="" width="219" height="219" /></a>

Well, that wasn’t quite Raphaël. The <code>rotate</code> function work different in Raphaël than it does in Paper.js and Processing.js. Raphaël doesn’t support rotation around a fixed point. Instead, the teeth of the gears are drawn and redrawn independently, and they fly through the air instead of rotating around the center. The only way to really turn the gear would be to draw the entire gear as a single path, and that takes more math than I’m willing to write. If anyone wants to give it a try, everything is open source.</p>

## The Future Of Web Drawing

We gamble on every new technology that we learn: we hope that it catches on and that our investment pays off. Technologies rise and fall on their respective merits, but other factors comes into play, such as vendor support and business uses. The future of our industry is almost a guessing game.

Right now, Flash looks like a bad investment. Flash has great tools, years of development and a large community, but even Adobe is moving away from it.

SVG is in a similar situation. Browsers support it now, but it isn’t getting a lot of attention.

Every browser vendor is working hard to render <code>canvas</code> faster, to use hardware acceleration and to better support libraries such as Paper.js and Processing.js. All mobile devices support <code>canvas</code>, and their developers are working to improve it.</p>

## Update

After hearing from a few Raphaël fans <a href="https://dmitry.baranovskiy.com/">Dmitry Baranovskiy</a> the creator of the framework took a look and showed me what I was missing to make the gears rotate in Raphaël. Check out the <a href="https://zgrossbart.github.com/3gears/raphael_gears.html">rotating gears in Raphaël</a>.

{{< signature "al" >}}

