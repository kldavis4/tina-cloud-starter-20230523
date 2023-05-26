---
title: A Quick Look Into The Math Of Animations With JavaScript
slug: quick-look-math-animations-javascript
image: null
date: 2011-10-04T10:24:38.000Z
author: christian-heilmann
description: >-
  In school, I hated math. It was a dire, dry and boring thing with stuffy old books and very theoretical problems. Even worse, a lot of the tasks were repetitive, with a simple logical change in every iteration (dividing numbers by hand, differentials, etc.). It was exactly the reason why we invented computers. Suffice it to say, a lot of my math homework was actually done by my trusty Commodore 64 and some lines of Basic, with me just copying the results later on.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
  - Animation
---
These tools and the few geometry lessons I had gave me the time and inspiration to make math interesting for myself. I did this first and foremost by creating visual effects that followed mathematical rules in demos, intros and other seemingly pointless things.

There is a lot of math in the visual things we do, even if we don’t realize it. If you want to make something look natural and move naturally, you need to add a bit of physics and rounding to it. Nature doesn’t work in right angles or linear acceleration. This is why zombies in movies are so creepy. This was <a href="https://www.smashingmagazine.com/2011/09/14/the-guide-to-css-animation-principles-and-examples/">covered here before in relation to CSS animation</a>, but today let’s go a bit deeper and look at the simple math behind the smooth looks.

{{% feature-panel %}}

## Going From 0 To 1 Without Being Boring

If you’ve just started programming and are asked to go from 0 to 1 with a few steps in between, you would probably go for a <code>for</code> loop:

<pre><code class="language-javascript">for ( i = 0; i &lt;= 1; i += 0.1 ) {
  x = i;
  y = i;
…
}</code></pre>

This would result in a line on a graph that is 45 degrees. Nothing in nature moves with this precision:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b39fe442-f795-482f-bedb-64b1f7533f3f/forloop.png" alt="45 degree graph, a result of a simple for loop" width="300" height="300" />

A simple way to make this movement a bit more natural would be to simply multiply the value by itself:

<pre><code class="language-javascript">for ( i = 0; i &lt;= 1; i += 0.1 ) {
  x = i;
  y = i * i;
}</code></pre>

This means that <code>0.1</code> is <code>0.01</code>, <code>0.2</code> is <code>0.04</code>, <code>0.3</code> is <code>0.09</code>, <code>0.4</code> is <code>0.16</code>, <code>0.5</code> is <code>0.25</code> and so on. The result is a curve that starts flat and then gets steeper towards the end:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26fe77c9-05b0-450f-b515-bb03f91b623b/multiply.png" alt="graph of the value multiplied with itself" width="300" height="300" />

You can make this even more pronounced by continuing to multiply or by using the “to the power of” <code>Math.pow()</code> function:

<pre><code class="language-javascript">for ( i = 0; i &lt;= 1; i += 0.1 ) {
  x = i;
  y = Math.pow( i, 4 );
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbe53a27-5fae-4a0e-b261-ea6313fa1e60/powerto.png" alt="graph with several multiplications" width="300" height="300" />

This is one of the tricks of the easing functions used in libraries such as jQuery and YUI, as well as in CSS transitions and animations in modern browsers.

You can use this the same way, but there is an even simpler option for getting a value between 0 and 1 that follows a natural motion.</p>

## Not A Sin, Just A Natural Motion

<a href="https://en.wikipedia.org/wiki/Sine_wave">Sine waves</a> are probably the best thing ever for smooth animation. They happen in nature: witness a spring with a weight on it, ocean waves, sound and light.
In our case, we want to move from 0 to 1 smoothly.

To create a movement that goes from 0 to 1 and back to 0 smoothly, we can use a sine wave that goes from 0 to π in a few steps. The full sine wave going from 0 to π × 2 (i.e. a whole circle) would result in values from -1 to 1, and we don’t want that (yet).

<pre><code class="language-javascript">var counter = 0;

// 100 iterations
var increase = Math.PI / 100;

for ( i = 0; i &lt;= 1; i += 0.01 ) {
  x = i;
  y = Math.sin(counter);
  counter += increase;
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b22e6652-777e-4e46-a4bb-79861149951d/sine.png" alt="half a sine wave" width="300" height="300" />

<strong>A quick aside on numbers for sine and cosine:</strong> Both <code>Math.sin()</code> and <code>Math.cos()</code> take as the parameter an angle that should be in <a href="https://en.wikipedia.org/wiki/Radian">radians</a>. As humans, however, degrees ranging from 0 to 360 are much easier to read. That’s why you can and should convert between them with this simple formula:

<pre><code class="language-javascript">var toRadian = Math.PI / 180;
var toDegree = 180 / Math.PI;

var angle = 30;

var angleInRadians = angle * toRadian;
var angleInDegrees = angleInRadians * toDegree;</code></pre>

Back to our sine waves. You can play with this a lot. For example, you could use the absolute value of a full 2 × π loop:

<pre><code class="language-javascript">var counter = 0;
// 100 iterations
var increase = Math.PI * 2 / 100;

for ( i = 0; i &lt;= 1; i += 0.01 ) {
  x = i;
  y = Math.abs( Math.sin( counter ) );
  counter += increase;
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27ffc61d-3e1f-4410-b9db-5471063e2b32/msine.png" alt="absolute value of a sine wave" width="300" height="300" />

But again, this looks dirty. If you want the full up and down, without a break in the middle, then you need to shift the values. You have to half the sine and then add 0.5 to it:

<pre><code class="language-javascript">var counter = 0;
// 100 iterations
var increase = Math.PI * 2 / 100;

for ( i = 0; i &lt;= 1; i += 0.01 ) {
  x = i;
  y = Math.sin( counter ) / 2 + 0.5;
  counter += increase;
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/137d3e15-0286-48c4-8541-533b022118de/shiftingup.png" alt="halfed and moved sine wave" width="300" height="300" />

So, how can you use this? Having a function that returns -1 to 1 to whatever you feed it can be very cool. All you need to do is multiply it by the values that you want and add an offset to avoid negative numbers.

For example, check out <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85f653c-d2a9-4093-994f-bff1fd460e88/sinejump.html">this sine movement demo</a>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85f653c-d2a9-4093-994f-bff1fd460e88/sinejump.html"> </a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85f653c-d2a9-4093-994f-bff1fd460e88/sinejump.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0f92665-dae3-48d8-a85b-52d9beaa9d88/sinejump.png" alt="Sine jump demo" width="224" height="222" /></a>

Looks neat, doesn’t it? A lot of the trickery is already in the CSS:

<pre><code class="language-css">.stage {
  width:200px;
  height:200px;
  margin:2em;
  position:relative;
  background:#6cf;
  overflow:hidden;
}

.stage div {
  line-height:40px;
  width:100%;
  text-align:center;
  background:#369;
  color:#fff;
  font-weight:bold;
  position:absolute;
}</code></pre>

The <code>stage</code> element has a fixed dimension and is positioned relative. This means that everything that is positioned absolutely inside it will be relative to the element itself.

The div inside the stage is 40 pixels high and positioned absolutely. Now, all we need to do is move the div with JavaScript in a sine wave:

<pre><code class="language-javascript">var banner = document.querySelector( '.stage div' ),
    start = 0;
function sine(){
  banner.style.top = 50 * Math.sin( start ) + 80 + 'px';
  start += 0.05;
}
window.setInterval( sine, 1000/30 );</code></pre>

The start value changes constantly, and with <code>Math.sin()</code> we get a nice wave movement. We multiply this by 50 to get a wider wave, and we add 80 pixels to center it in the stage element. Yes, the element is 200 pixels high and 100 is half of that, but because the banner is 40 pixels high, we need to subtract half of that to center it.

Right now, this is a simple up-and-down movement. Nothing stops you, though, from making it more interesting. The multiplying factor of 50, for example, could be a sine wave itself with a different value:

<pre><code class="language-javascript">var banner = document.querySelector( '.stage div' ),
    start = 0,
    multiplier = 0;
function sine(){
  multiplier = 50 * Math.sin( start * 2 );
  banner.style.top = multiplier * Math.sin( start ) + 80 + 'px';
  start += 0.05;
}
window.setInterval( sine, 1000/30 );</code></pre>

The <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac952270-5519-49cc-95e5-19e66e01ae4d/growingsinejump.html">result of this</a> is a banner that seems to tentatively move up and down. Back in the day and on the very slow Commodore 64, calculating the sine wave live was too slow. Instead, we had tools to generate sine tables (arrays, if you will), and we plotted those directly. One of the tools for creating great sine waves so that you could have bouncing scroll texts was the Wix Bouncer:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a706dd63-5435-461e-b0eb-2adc53a1bc2e/wixbouncer.png" alt="Wixbouncer - a tool to create sine waves" width="384" height="282" />

## Circles In The Sand, Round And Round…

Circular motion is a thing of beauty. It pleases the eye, reminds us of spinning wheels and the earth we stand on, and in general has a “this is not computer stuff” feel to it. The math of plotting something on a circle is not hard.

It goes back to <a href="https://en.wikipedia.org/wiki/Pythagoras">Pythagoras</a>, who, as rumor has it, drew a lot of circles in the sand until he found his famous <a href="https://en.wikipedia.org/wiki/Pythagorean_theorem">theorem</a>. If you want to use all the good stuff that comes from this theorem, then try to find a triangle with a right angle. If this triangle’s hypothenuse is 1, then you can easily calculate the horizontal leg as the cosine of the angle and the vertical leg as the sine of the angle:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a20c7707-f7c9-4c81-82c4-b46c5907b47f/sincos.png" alt="Sincos" width="300" height="300" />

How is this relevant to a circle? Well, it is pretty simple to find a right-angle triangle in a circle to every point of it:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0b53bf7-8fc5-499d-b286-7d819613b62d/circle.png" alt="Circle" width="300" height="300" />

This means that if you want to plot something on a circle (or draw one), you can do it with a loop and sine and cosine. A full circle is 360°, or 2 × π in radians. We could have a go at it — but first, some plotting code needs to be done.</p>

## A Quick DOM Plotting Routine

Normally, my weapon of choice here would be canvas, but in order to play nice with older browsers, let’s do it in plain DOM. The following helper function adds div elements to a stage element and allows us to position them, change their dimensions, set their color, change their content and rotate them without having to go through the annoying style settings on DOM elements.

<pre><code class="language-javascript">Plot = function ( stage ) {

  this.setDimensions = function( x, y ) {
    this.elm.style.width = x + 'px';
    this.elm.style.height = y + 'px';
    this.width = x;
    this.height = y;
  }
  this.position = function( x, y ) {
    var xoffset = arguments[2] ? 0 : this.width / 2;
    var yoffset = arguments[2] ? 0 : this.height / 2;
    this.elm.style.left = (x - xoffset) + 'px';
    this.elm.style.top = (y - yoffset) + 'px';
    this.x = x;
    this.y = y;
  };
  this.setbackground = function( col ) {
    this.elm.style.background = col;
  }
  this.kill = function() {
    stage.removeChild( this.elm );
  }
  this.rotate = function( str ) {
    this.elm.style.webkitTransform = this.elm.style.MozTransform =
    this.elm.style.OTransform = this.elm.style.transform =
    'rotate('+str+')';
  }
  this.content = function( content ) {
    this.elm.innerHTML = content;
  }
  this.round = function( round ) {
    this.elm.style.borderRadius = round ? '50%/50%' : ’;
  }
  this.elm = document.createElement( 'div' );
  this.elm.style.position = 'absolute';
  stage.appendChild( this.elm );

};</code></pre>

The only things that might be new here are the transformation with different browser prefixes and the positioning. People often make the mistake of creating a div with the dimensions <code>w</code> and <code>h</code> and then set it to <code>x</code> and <code>y</code> on the screen. This means you will always have to deal with the offset of the height and width. By subtracting half the width and height before positioning the div, you really set it where you want it — regardless of the dimensions. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b178ffa5-59ca-4b37-88b2-833d44263ea9/offsetissue1.html">Here’s a proof</a>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/264b4079-ab2c-4c29-b08e-db1692adc65d/offsetissue.html"> </a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/264b4079-ab2c-4c29-b08e-db1692adc65d/offsetissue.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79604a96-e447-4ce2-8f12-45e38b5527cc/offsetissue.png" alt="offset issue" width="481" height="229" /></a>

Now, let’s use that to <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de2a75e7-adda-4440-b9d7-43ee45e5216b/simplecircle.html">plot 10 rectangles in a circle</a>, shall we?

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de2a75e7-adda-4440-b9d7-43ee45e5216b/simplecircle.html"> </a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de2a75e7-adda-4440-b9d7-43ee45e5216b/simplecircle.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856d3329-84a3-4005-ae06-c5470d76eb4a/simplecircle.png" alt="Simple circle" width="414" height="419" /></a>

<pre><code class="language-javascript">var stage = document.querySelector('.stage'),
    plots = 10;
    increase = Math.PI * 2 / plots,
    angle = 0,
    x = 0,
    y = 0;

for( var i = 0; i &lt; plots; i++ ) {
  var p = new Plot( stage );
  p.setBackground( 'green' );
  p.setDimensions( 40, 40 );
  x = 100 * Math.cos( angle ) + 200;
  y = 100 * Math.sin( angle ) + 200;
  p.position( x, y );
  angle += increase;
}</code></pre>

We want 10 things in a circle, so we need to find the angle that we want to put them at. A full circle is two times <code>Math.PI</code>, so all we need to do is divide this. The x and y position of our rectangles can be calculated by the angle we want them at. The x is the cosine, and the y is the sine, as explained earlier in the bit on Pythagoras. All we need to do, then, is center the circle that we’re painting in the stage (<code>200,200</code> is the center of the stage), and we are done. We’ve painted a circle with a radius of 100 pixels on the canvas in 10 steps.

The problem is that this looks terrible. If we really want to plot things on a circle, then their angles should also point to the center, right? For this, we need to calculate the tangent of the right-angle square, as explained in this <a href="https://www.mathsisfun.com/algebra/trig-finding-angle-right-triangle.html">charming “Math is fun” page</a>. In JavaScript, we can use <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Math/atan2"><code>Math.atan2()</code></a> as a shortcut. The result looks much better:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a940e7e-4308-4848-95d4-70fdc97339f3/tancircle.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67590f32-62e8-4cc6-9e34-cb8245b88be1/tancircle.png" alt="Tancircle" width="411" height="414" /></a>

<pre><code class="language-javascript">var stage = document.querySelector('.stage'),
    plots = 10;
    increase = Math.PI * 2 / plots,
    angle = 0,
    x = 0,
    y = 0;

for( var i = 0; i &lt; plots; i++ ) {
  var p = new Plot( stage );
  p.setBackground( 'green' );
  p.setDimensions( 40, 40 );
  x = 100 * Math.cos( angle ) + 200;
  y = 100 * Math.sin( angle ) + 200;
  p.rotate( Math.atan2( y - 200, x - 200 ) + 'rad' );
  p.position( x, y );
  angle += increase;
}</code></pre>

Notice that the rotate transformation in CSS helps us heaps in this case. Otherwise, the math to rotate our rectangles would be much less fun. CSS transformations also take radians and degrees as their value. In this case, we use <code>rad</code>; if you want to rotate with degrees, simply use <code>deg</code> as the value.

How about animating the circle now? Well, the first thing to do is change the script a bit, because we don’t want to have to keep creating new plots. Other than that, all we need to do to <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42501aab-9c8a-48f0-9f86-23746aa34514/rotatingcircle.html">rotate the circle is to keep increasing the start angle</a>:

<pre><code class="language-javascript">var stage = document.querySelector('.stage'),
    plots = 10;
    increase = Math.PI * 2 / plots,
    angle = 0,
    x = 0,
    y = 0,
    plotcache = [];

for( var i = 0; i &lt; plots; i++ ) {
  var p = new Plot( stage );
  p.setBackground( 'green' );
  p.setDimensions( 40, 40 );
  plotcache.push( p );
}

function rotate(){
  for( var i = 0; i &lt; plots; i++ ) {
    x = 100 * Math.cos( angle ) + 200;
    y = 100 * Math.sin( angle ) + 200;
    plotcache[ i ].rotate( Math.atan2( y - 200, x - 200 ) + 'rad' );
    plotcache[ i ].position( x, y );
    angle += increase;
  }
  angle += 0.06;
}

setInterval( rotate, 1000/30 );</code></pre>

Want more? How about a <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/797cf9af-3df6-4f10-af2e-afad8e9dfc69/rotatingmessage.html">rotating text message</a> based on this? The tricky thing about this is that we also need to turn the characters 90° on each iteration:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/797cf9af-3df6-4f10-af2e-afad8e9dfc69/rotatingmessage.html"> </a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/797cf9af-3df6-4f10-af2e-afad8e9dfc69/rotatingmessage.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98ea4557-f685-4ea9-9e98-1d3a8e856b6a/rotatedmessage.png" alt="Rotated message" width="410" height="413" /></a>

<pre><code class="language-javascript">var stage = document.querySelector('.stage'),
    message = 'Smashing Magazine '.toUpperCase(),
    plots = message.length;
    increase = Math.PI * 2 / plots,
    angle = -Math.PI,
    turnangle = 0,
    x = 0,
    y = 0,
    plotcache = [];

for( var i = 0; i &lt; plots; i++ ) {
  var p = new Plot( stage );
  p.content( message.substr(i,1) );
  p.setDimensions( 40, 40 );
  plotcache.push( p );
}
function rotate(){
  for( var i = 0; i &lt; plots; i++ ) {
    x = 100 * Math.cos( angle ) + 200;
    y = 100 * Math.sin( angle ) + 200;
    // rotation and rotating the text 90 degrees
    turnangle = Math.atan2( y - 200, x - 200 ) * 180 / Math.PI + 90 + 'deg';
    plotcache[ i ].rotate( turnangle );
    plotcache[ i ].position( x, y );
    angle += increase;
  }
  angle += 0.06;
}

setInterval( rotate, 1000/40 );</code></pre>

Again, nothing here is fixed. You can make the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49a760c1-f74e-4da5-ad69-c932010ece6c/growrotatingmessage.html">radius of the circle change constantly</a>, as we did with the bouncing banner message earlier (below is only an excerpt):

<pre><code class="language-javascript">multiplier = 80 * Math.sin( angle );
for( var i = 0; i &lt; plots; i++ ) {
  x = multiplier * Math.cos( angle ) + 200;
  y = multiplier * Math.sin( angle ) + 200;
  turnangle = Math.atan2( y - 200, x - 200 ) * 180 / Math.PI + 90 + 'deg';
  plotcache[ i ].rotate( turnangle );
  plotcache[ i ].position( x, y );
  angle += increase;
}
angle += 0.06;</code></pre>

And, of course, you can <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/671321e5-abcf-4bbc-9c63-5476c79eca6f/rotaterotatingmessage.html">move the center of the circle</a>, too:

<pre><code class="language-javascript">rx = 50 * Math.cos( angle ) + 200;
ry = 50 * Math.sin( angle ) + 200;
for( var i = 0; i &lt; plots; i++ ) {
  x = 100 * Math.cos( angle ) + rx;
  y = 100 * Math.sin( angle ) + ry;
  turnangle = Math.atan2( y - ry, x - rx ) * 180 / Math.PI + 90 + 'deg';
  plotcache[ i ].rotate( turnangle );
  plotcache[ i ].position( x, y );
  angle += increase;
}
angle += 0.06;</code></pre>

For a final tip, how about <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65059e30-1c6d-420b-9585-48ee68c739af/boxedrotatingmessage.html">allowing only a certain range of coordinates</a>?

<pre><code class="language-javascript">function rotate() {
  rx = 70 * Math.cos( angle ) + 200;
  ry = 70 * Math.sin( angle ) + 200;
  for( var i = 0; i &lt; plots; i++ ) {
    x = 100 * Math.cos( angle ) + rx;
    y = 100 * Math.sin( angle ) + ry;
    x = contain( 70, 320, x );
    y = contain( 70, 320, y );
    turnangle = Math.atan2( y - ry, x - rx ) * 180 / Math.PI + 90 + 'deg';
    plotcache[ i ].rotate( turnangle );
    plotcache[ i ].position( x, y );
    angle += increase;
  }
  angle += 0.06;
}
function contain( min, max, value ) {
  return Math.min( max, Math.max( min, value ) );
}</code></pre>

### Summary

This was just a quick introduction to using exponentials and sine waves and to plotting things on a circle. Have a go with the code, and play with the numbers. It is amazing how many cool effects you can create with a few changes to the radius or by multiplying the angles. To make it easier for you to do this, below are the examples on JSFiddle to play with:

*   [Sine bouncing message](https://jsfiddle.net/codepo8/tgEx6/11/)
*   [Double sine bouncing message](https://jsfiddle.net/codepo8/tgEx6/2/)
*   [Offset issue with plotting](https://jsfiddle.net/codepo8/tgEx6/4/)
*   [Distributing elements on a circle](https://jsfiddle.net/codepo8/tgEx6/8/)
*   [Distributing elements on a circle with correct angles](https://jsfiddle.net/codepo8/tgEx6/9/)
*   [Rotating a circle of boxes](https://jsfiddle.net/codepo8/tgEx6/7/)
*   [Oscillating rotating message](https://jsfiddle.net/codepo8/tgEx6/10/)
*   [Rotating message in a circle movement](https://jsfiddle.net/codepo8/tgEx6/5/)
*   [Boxed rotated message scroller](https://jsfiddle.net/codepo8/tgEx6/)

## Further reading

*   [SVG and CSS animations with clip-path](https://www.smashingmagazine.com/2015/12/animating-clipped-elements-svg/)
*   [Creating 'hand-drawn' Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)
*   [The new Web Animation API](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [Practical Animation Techniques](https://www.smashingmagazine.com/2015/06/practical-techniques-on-designing-animation/)
*   [UI Animation Guidelines and Examples](https://www.smashingmagazine.com/2015/05/functional-ux-design-animations/)
*   [Designing Animations In Photoshop](https://www.smashingmagazine.com/2015/06/creating-advanced-animations-in-photoshop/)
*   [Fast Prototyping UI Animations In Keynote](https://www.smashingmagazine.com/2015/08/animating-in-keynote/)

