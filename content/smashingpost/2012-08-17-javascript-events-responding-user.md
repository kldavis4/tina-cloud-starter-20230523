---
title: JavaScript Events And Responding To The User
slug: javascript-events-responding-user
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9296b18-ab11-4c02-8cac-2c9d78a51fa7/nodejs-illu-grey.jpg
date: 2012-08-17T11:34:22.000Z
author: christian-heilmann
description: >-
  Whenever people ask me about the most powerful things in JavaScript and the DOM, I quickly arrive at events. The reason is that events in browsers are incredibly useful.
categories:
  - Coding
  - CSS
  - JavaScript
  - Programming
---
Furthermore, decoupling functionality from events is a powerful idea, which is why <a href="https://nodejs.org/">Node.js</a> became such a hot topic.

Today, let’s get back to the basics of events and get you in the mood to start playing with them, beyond applying click handlers to everything or breaking the Web with <code>&lt;a href="javascript:void(0)"&gt;</code> links or messing up our HTML with <code>onclick="foo()"</code> inline handlers (I explained in detail in 2005 <a href="https://www.onlinetools.org/articles/unobtrusivejavascript/chapter4.html">why these are bad ideas</a>).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Seven Deadly Sins Of JavaScript Implementation](https://www.smashingmagazine.com/2010/02/the-seven-deadly-sins-of-javascript-implementation/)
*   [Browser Input Events: Can We Do Better Than The Click?](https://www.smashingmagazine.com/2015/03/better-browser-input-events/)
*   [Making A Service Worker: A Case Study](https://www.smashingmagazine.com/2016/02/making-a-service-worker/)
*   [7 JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)

Note: This article uses plain JavaScript and not any libraries. A lot of what we’ll talk about here is easier to achieve in jQuery, YUI or Dojo, but understanding the basics is important because you will find yourself in situations where you cannot use a library but should still be able to deliver an amazing solution.

{{% feature-panel %}}

<strong>Disclaimer</strong>: The event syntax we’ll be using here is <a href="https://developer.mozilla.org/en/DOM/element.addEventListener">addEventListener()</a>, as defined in the “<a href="https://dev.w3.org/2006/webapi/DOM-Level-3-Events/html/DOM3-Events.html#events-EventTarget-addEventListener">DOM Level 3 Events</a>” specification, which works in all browsers in use now except for Internet Explorer below version 9. A lot of the things we’ll show can be achieved with jQuery, though, which also supports legacy browsers. Come to think of it, one simple <code>addEventListener()</code> on <code>DOMContentLoaded</code> is a great way to make sure your script does not run on legacy browsers. This is a good thing. If we want the Web to evolve, we need to stop giving complex and demanding code to old browsers. If you build your solutions the right way, then IE 6 would not need any JavaScript to display a workable, albeit simpler, solution. Think of your product as an escalator: if your JavaScript does not execute, the website should still be usable as stairs.

Before we get into the details of events and how to use them, check out a few demos that use scroll events in a clever way to achieve pretty sweet results:

*   In its search for a designer, Wealthfront Engineering uses [scrolling and shifting content along the Z axis](https://www.wealthfront.com/designerwanted). This was a big part of the [Beercamp 2011 website](https://2011.beercamp.com/). Wealthfront [blogged in detail](https://eng.wealthfront.com/2012/03/scrolling-z-axis-with-css-3d-transforms.html) about how it achieved this.
*   [Stroll.js](https://lab.hakim.se/scroll-effects/) takes a slightly similar approach, showing how lovely transitions can be when the user scrolls a list.
*   [jQuery Scroll Path](https://joelb.me/scrollpath/) is a plugin to move content along a path when the user scrolls the page.

All of this is based on event handling and reading out what the browser gives us. Now, let’s look at repeating the basics of that.</p>

## Basics: What Is An Event?

<pre><code class="language-javascript">var log = document.getElementById('log'),
    i = ’, 
    out = [];
for (i in window) {
  if ( /^on/.test(i)) { out[out.length] = i; }
}
log.innerHTML = out.join(', ');</code></pre>

In my case, running Firefox, I get this:

onmouseenter, onmouseleave, onafterprint, onbeforeprint, onbeforeunload, onhashchange, onmessage, onoffline, ononline, onpopstate, onpagehide, onpageshow, onresize, onunload, ondevicemotion, ondeviceorientation, onabort, onblur, oncanplay, oncanplaythrough, onchange, onclick, oncontextmenu, ondblclick, ondrag, ondragend, ondragenter, ondragleave, ondragover, ondragstart, ondrop, ondurationchange, onemptied, onended, onerror, onfocus, oninput, oninvalid, onkeydown, onkeypress, onkeyup, onload, onloadeddata, onloadedmetadata, onloadstart, onmousedown, onmousemove, onmouseout, onmouseover, onmouseup, onmozfullscreenchange, onmozfullscreenerror, onpause, onplay, onplaying, onprogress, onratechange, onreset, onscroll, onseeked, onseeking, onselect, onshow, onstalled, onsubmit, onsuspend, ontimeupdate, onvolumechange, onwaiting, oncopy, oncut, onpaste, onbeforescriptexecute, onafterscriptexecute

That is a lot to play with, and the way to do that is by using <code>addEventListener()</code>:

<pre><code class="language-javascript">element.addEventListener(event, handler, useCapture);</code></pre>

For example:

<pre><code class="language-javascript">var a = document.querySelector('a'); // grab the first link in the document
a.addEventListener('click', ajaxloader, false);</code></pre>

The <code>element</code> is the element that we apply the handler to; as in, “Hey you, link! Make sure you tell me when something happens to you.” The <code>ajaxloader()</code> function is the event listener; as in, “Hey you! Just stand there and keep your ears and eyes peeled in case something happens to the link.” Setting the <code>useCapture</code> to <code>false</code> means that we are content to capture the event on bubbling, rather than the capturing phase. This is a <a href="https://www.w3.org/TR/DOM-Level-3-Events/#event-flow">long and arduous topic</a>, well explained on Dev.Opera. Let’s just say that by setting the <code>useCapture</code> to <code>false</code>, you will be fine in 99.7434% of cases (a rough approximation). The parameter is actually optional in all browsers but Opera.

Now, the event handler function gets an object as a parameter from the event, which is full of awesome properties that we can play with. If you <a href="https://thewebrocks.com/demos/smashing-events/eventproperties.html">try out my example</a>, you’ll see what the following code does:

<pre><code class="language-javascript">var log = document.getElementById('log'),
    out = ’;

document.addEventListener('click', logeventinfo, false);
document.addEventListener('keypress', logeventinfo, false);

function logeventinfo (ev) {
  log.innerHTML = ’;
  out = '&lt;ul&gt;';
  for (var i in ev) {
    if (typeof ev[i] === 'function' || i === i.toUpperCase()) {
      continue;
    }
    out += '&lt;li&gt;&lt;span&gt;'+i+'&lt;/span&gt;: '+ev[i]+'&lt;/li&gt;';
  }
  log.innerHTML += out + '&lt;/ul&gt;';
}</code></pre>

You can assign several event handlers to the same event, or the same handler to various events (as shown in this demo).

The <code>ev</code> is what we get back from the event. And (again, in my case, in Firefox) a lot of interesting things are in it:

<pre><code class="language-javascript">originalTarget: [object HTMLHtmlElement]
type: click
target: [object HTMLHtmlElement]
currentTarget: [object HTMLDocument]
eventPhase: 3
bubbles: true
cancelable: true
timeStamp: 574553210
defaultPrevented: false
which: 1
rangeParent: [object Text]
rangeOffset: 23
pageX: 182
pageY: 111
isChar: false
screenX: 1016
screenY: 572
clientX: 182
clientY: 111
ctrlKey: false
shiftKey: false
altKey: false
metaKey: false
button: 0
relatedTarget: null
mozPressure: 0
mozInputSource: 1
view: [object Window]
detail: 1
layerX: 182
layerY: 111
cancelBubble: false
explicitOriginalTarget: [object HTMLHtmlElement]
isTrusted: true
originalTarget: [object HTMLHeadingElement]
type: click
target: [object HTMLHeadingElement]
currentTarget: [object HTMLDocument]
eventPhase: 3
bubbles: true
cancelable: true
timeStamp: 574554192
defaultPrevented: false
which: 1
rangeParent: [object Text]
rangeOffset: 0
pageX: 1
pageY: 18
isChar: false
screenX: 835
screenY: 479
clientX: 1
clientY: 18
ctrlKey: false
shiftKey: false
altKey: false
metaKey: false
button: 0
relatedTarget: null
mozPressure: 0
mozInputSource: 1
view: [object Window]
detail: 1
layerX: 1
layerY: 18
cancelBubble: false
explicitOriginalTarget: [object Text]
isTrusted: true</code></pre>

It also differs from event to event. Try clicking the demo and pressing keys, and you will see that you get different results. You can also refer to the <a href="https://developer.mozilla.org/en/DOM/event#Properties">full list of standard <code>event</code> properties</a>.</p>

## The Last Of The Basics: Preventing Execution And Getting The Target

Two more things are important when it comes to events in the browser: we have to stop the browser from carrying out its default action for the event, and we have to find out which element the event fired on. The former is achieved with the <code>ev.preventDefault()</code> method, and the latter is stored in <code>ev.target</code>.

Say you want to know that a link has been clicked, but you don’t want the browser to follow it because you have a great idea of what to do with that event instead. You can do this by subscribing to the click event of the link, and you can stop the browser from following it by calling <code>preventDefault()</code>. Here is the HTML:

<pre><code class="language-markup tmp-html">&lt;a class="prevent" href="https://smashingmagazine.com"&gt;Smashing, my dear!&lt;/a&gt;
&lt;a class="normal" href="https://smashingmagazine.com"&gt;Smashing, my dear!&lt;/a&gt;</code></pre>

And the JavaScript:

<pre><code class="language-javascript">var normal = document.querySelector('.normal'),
    prevent = document.querySelector('.prevent');

prevent.addEventListener('click', function(ev) {
  alert('fabulous, really!');
  ev.preventDefault();
}, false);

normal.addEventListener('click', function(ev) {
  alert('fabulous, really!');
}, false);</code></pre>

Note: <code>document.querySelector()</code> is the standard way to get an element in the DOM. It is what the <code>$()</code> method in jQuery does. You can read the <a href="https://www.w3.org/TR/selectors-api/">W3C’s specification</a> for it and get some <a href="https://developer.mozilla.org/En/Code_snippets/QuerySelector">explanatory code snippets</a> on the Mozilla Developer Network (MDN).

If you now click the link, you will get an alert. And when you hit the “OK” button, nothing more happens; the browser does not go to <code>https://smashingmagazine.com</code>. Without the <code>preventDefault()</code>, the browser will show the alert and follow the link. <a href="https://thewebrocks.com/demos/smashing-events/preventdefault.html">Try it out.</a>

The normal way to access the element that was clicked or hovered over or that had a key pressed is to use the <code>this</code> keyword in the handler. This is short and sweet, but it’s actually limiting because <code>addEventListener()</code> gives us something better: the event target. It could also be confusing because <code>this</code> might already be bound to something else, so using <code>ev.currentTarget</code> as noted in the specification is a safer bet.

## Event Delegation: It Rocks. Use It!

Using the <code>target</code> property of the event object, you can find out which element the event occurred on.

Events happen by going down the whole document tree to the element that you interacted with and back up to the main window. This means that if you add an event handler to an element, you will get all of the child elements for free. All you need to do is test the event target and respond accordingly. <a href="https://thewebrocks.com/demos/smashing-events/eventdelegation.html">See my example of a list</a>:

<pre><code class="language-javascript">&lt;ul id="resources"&gt;
  &lt;li&gt;&lt;a href="https://developer.mozilla.org"&gt;MDN&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://html5doctor.com"&gt;HTML5 Doctor&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://html5rocks.com"&gt;HTML5 Rocks&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://beta.theexpressiveweb.com/"&gt;Expressive Web&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://creativeJS.com/"&gt;CreativeJS&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

Hover your mouse over the list in this example and you will see that one event handler is enough to get the links, the list item and the list itself. All you need to do is compare the <code>tagName</code> of the event target to what you want to have.

<pre><code class="language-javascript">var resources = document.querySelector('#resources'),
    log = document.querySelector('#log');

resources.addEventListener('mouseover', showtarget, false);

function showtarget(ev) {
  var target = ev.target;
  if (target.tagName === 'A') {
    log.innerHTML = 'A link, with the href:' + target.href;
  }
  if (target.tagName === 'LI') {
    log.innerHTML = 'A list item';
  }
  if (target.tagName === 'UL') {
    log.innerHTML = 'The list itself';
  }
}</code></pre>

This means you can save a lot of event handlers — each of which is expensive to the browser. Instead of applying an event handler to each link and responding that way — as most people would do in jQuery with <code>$('a').click(...)</code> (although jQuery’s <code>on</code> is OK) — you can assign a single event handler to the list itself and check which element was just clicked.

The main benefit of this is that you are independent of the HTML. If you add more links at a later stage, there is no need to assign new handlers; the event handler will know automatically that there is a new link to do things with.</p>

## Events For Detection, CSS Transitions For Smoothness

If you remember the list of properties earlier in this article, there is a lot of things we can use. In the past, we used events for simple hover effects, which now have been replaced with effects using the <code>:hover</code> and <code>:focus</code> CSS selectors. Some things, however, cannot be done with CSS yet; for example, finding the mouse’s position. With an event listener, this is pretty simple. First, we define an element to position, like a ball. The HTML:

<pre><code class="language-markup tmp-html">&lt;div class="plot"&gt;&lt;/div&gt;</code></pre>

And the CSS:

<pre><code class="language-css">.plot {
  position:absolute;
  background:rgb(175,50,50);
  width: 20px;
  height: 20px;
  border-radius: 20px;
  display: block;
  top:0;
  left:0;
}</code></pre>

We then assign a click handler to the document and position the ball at <code><a href="https://developer.mozilla.org/en/DOM/event.pageX">PageX</a></code> and <code>pageY</code>. Notice that we need to subtract half the width of the ball in order to center it on the mouse pointer:

<pre><code class="language-javascript">var plot = document.querySelector('.plot'),
    offset = plot.offsetWidth / 2;
document.addEventListener('click', function(ev) {
  plot.style.left = (ev.pageX - offset) + 'px';
  plot.style.top = (ev.pageY - offset) + 'px';
}, false);</code></pre>

Clicking anywhere on the screen will now move the ball there. However, it’s not smooth. If you <a href="https://thewebrocks.com/demos/smashing-events/mouseposition.html">enable the checkbox in the demo</a>, you will see that the ball moves smoothly. We could animate this with a library, but browsers can do better these days. All we need to do is add a transition to the CSS, and then the browser will move the ball smoothly from one position to another. To achieve this, we define a new class named <code>smooth</code> and apply it to the plot when the checkbox in the document is clicked. The CSS:

<pre><code class="language-css">.smooth {
  -webkit-transition: 0.5s;
     -moz-transition: 0.5s;
      -ms-transition: 0.5s;
       -o-transition: 0.5s;
          transition: 0.5s;
}</code></pre>

The JavaScript:

<pre><code class="language-javascript">var cb = document.querySelector('input[type=checkbox]');
cb.addEventListener('click', function(ev) {
  plot.classList.toggle('smooth');
}, false);</code></pre>

The interplay between CSS and JavaScript events has always been powerful, but it got even better in newer browsers. As you might have guessed, CSS transitions and animations have their own events.</p>

## How Long Was A Key Pressed?

As you might have seen in the list of available events earlier, browsers also give us a chance to respond to keyboard entry and tell us when the user has pressed a key. Sadly, though, key handling in a browser is hard to do properly, as <a href="https://unixpapa.com/js/key.html">Jan Wolter explains in detail</a>. However, as a simple example, let’s look how we can measure in milliseconds how long a user has pressed a button. See <a href="https://thewebrocks.com/demos/smashing-events/keytime.html">this keytime demo</a> for an example. Press a key, and you will see the output field grow while the key is down. Once you release the key, you’ll see the number of milliseconds that you pressed it. The code is not hard at all:

<pre><code class="language-javascript">var resources = document.querySelector('#resources'),
    log = document.querySelector('#log'),
    time = 0;

document.addEventListener('keydown', keydown, false);
document.addEventListener('keyup', keyup, false);

function keydown(ev) {
  if (time === 0) { 
    time = ev.timeStamp; 
    log.classList.add('animate');
  }
}
function keyup(ev) {
  if (time !== 0) {
    log.innerHTML = ev.timeStamp - time;
    time = 0;
    log.classList.remove('animate');
  }
}</code></pre>

We define the elements we want and set the <code>time</code> to <code>0</code>. We then apply two event handlers to the document, one on <code>keydown</code> and one on <code>keyup</code>.

In the <code>keydown</code> handler, we check whether <code>time</code> is <code>0</code>, and if it is, we set <code>time</code> to the <code>timeStamp</code> of the event. We assign a CSS class to the output element, which starts a CSS animation (see the CSS for how that is done).

The <code>keyup</code> handler checks whether <code>time</code> is still <code>0</code> (as <code>keydown</code> gets fired continuously while the key is pressed), and it calculates the difference in the time stamps if it isn’t. We set <code>time</code> back to <code>0</code> and remove the class to stop the animation.</p>

## Working With CSS Transitions (And Animations)

<a href="https://developer.mozilla.org/en/CSS/CSS_transitions">CSS transitions</a> fire a single event that you can listen for in JavaScript called <code>transitionend</code>. The event object then has two properties: <code>propertyName</code>, which contains the property that was transitioned, and <code>elapsedTime</code>, which tells you how long it took.

Check out <a href="https://thewebrocks.com/demos/smashing-events/transitionevent.html">the demo</a> to see it in action. The code is simple enough. Here is the CSS:

<pre><code class="language-css">.plot {
  background:rgb(175,50,50);
  width: 20px;
  height: 20px;
  border-radius: 20px;
  display: block;
  -webkit-transition: 0.5s;
     -moz-transition: 0.5s;
      -ms-transition: 0.5s;
       -o-transition: 0.5s;
          transition: 0.5s;
}

.plot:hover {
  width: 50px;
  height: 50px;
  border-radius: 100px;
  background: blue;
}</code></pre>

And the JavaScript:

<pre><code class="language-javascript">plot.addEventListener('transitionend', function(ev) {
  log.innerHTML += ev.propertyName + ':' + ev.elapsedTime + 's ';
}, false);</code></pre>

This, however, works only in Firefox right now because Chrome, Safari and Opera have vendor-prefixed events instead. As <a href="https://gist.github.com/702826">David Calhoun’s gist</a> shows, you need to detect what the browser supports and define the event’s name that way.

<a href="https://developer.mozilla.org/en/CSS/CSS_animations">CSS animation events</a> work the same way, but you have three events instead of one: <code>animationstart</code>, <code>animationend</code> and <code>animationiteration</code>. <a href="https://developer.mozilla.org/samples/cssref/animations/animevents.html">MDN has a demo</a> of it.</p>

## Speed, Distance And Angle

Detecting events happening is one thing. If you want to do something with them that is a beautiful and engaging, then you need to go further and put some math into it. So, let’s have a go at using a few mouse handlers to calculate the angle, distance and speed of movement when a user drags an element across the screen. <a href="https://thewebrocks.com/demos/smashing-events/speeddistanceangle.html">Check out the demo first.</a>

<pre><code class="language-javascript">var plot = document.querySelector('.plot'),
    log = document.querySelector('output'),
    offset = plot.offsetWidth / 2,
    pressed = false,
    start = 0, x = 0, y = 0, end = 0, ex = 0, ey = 0, mx = 0, my = 0, 
    duration = 0, dist = 0, angle = 0;

document.addEventListener('mousedown', onmousedown, false);
document.addEventListener('mouseup', onmouseup, false);
document.addEventListener('mousemove', onmousemove, false);

function onmousedown(ev) {
  if (start === 0 &amp;&amp; x === 0 &amp;&amp; y === 0) {
    start = ev.timeStamp;
    x = ev.clientX;
    y = ev.clientY;
    moveplot(x, y);
    pressed = true;
  }
}
function onmouseup(ev) {
  end = ev.timeStamp;
  duration = end - start;
  ex = ev.clientX;
  ey = ev.clientY;
  mx = ex - x;
  my = ey - y;
  dist = Math.sqrt(mx * mx + my * my);
  start = x = y = 0;
  pressed = false;
  angle = Math.atan2( my, mx ) * 180 / Math.PI;
  log.innerHTML = '&lt;strong&gt;' + (dist&gt;&gt;0) +'&lt;/strong&gt; pixels in &lt;strong&gt;'+
                  duration +'&lt;/strong&gt; ms ( &lt;strong&gt;' +
                  twofloat(dist/duration) +'&lt;/strong&gt; pixels/ms)'+
                  ' at &lt;strong&gt;' + twofloat(angle) +
                  '&lt;/strong&gt; degrees';
}
function onmousemove (ev) {
  if (pressed) {
    moveplot(ev.pageX, ev.pageY);
  }
}
function twofloat(val) {
  return Math.round((val*100))/100;
}
function moveplot(x, y) {
  plot.style.left = (x - offset) + 'px';
  plot.style.top = (y - offset) + 'px';
}</code></pre>

OK, I admit: quite a lot is going on here. But it is not as hard as it looks. For both <code>onmousedown</code> and <code>onmouseup</code>, we read the mouse’s position with <code>clientX</code> and <code>clientY</code> and the <code>timeStamp</code> of the event. Mouse events have time stamps that tell you when they happened. When the mouse moves, all we check is whether the mouse button has been pressed (via a boolean set in the <code>mousedown</code> handler) and move the plot with the mouse.

The rest is geometry — good old <a href="https://en.wikipedia.org/wiki/Pythagorean_theorem">Pythagoras</a>, to be precise. We get the speed of the movement by checking the number of pixels traveled in the time difference between <code>mousedown</code> and <code>mouseup</code>.

We get the number of pixels traveled as the square root of the sum of the squares of the difference between x and y at the start and end of the movement. And we get the angle by calculating the arctangent of the triangle. All of this is covered in “<a href="https://www.smashingmagazine.com/2011/10/04/quick-look-math-animations-javascript/">A Quick Look Into the Math of Animations With JavaScript</a>”; or you can play with the following JSFiddle example:

## Media Events

Both video and audio fire a lot of events that we can tap into. The most interesting are the time events that tell you how long a song or movie has been playing. A nice little demo to look at is the <a href="https://hacks.mozilla.org/2012/03/making-the-dino-roar-syncing-audio-and-css-transitions/">MGM-inspired dinosaur animation</a> on MDN; I recorded a <a href="https://youtube.com/watch?v=aFIJ_ZpV-8Q">six-minute screencast</a> explaining how it is done.

If you want to see a demo of all the events in action, the JPlayer team has a great <a href="https://www.jplayer.org/HTML5.Media.Event.Inspector/">demo page showing media events</a>.</p>

## Input Options

Traditionally, browsers gave us mouse and keyboard interaction. Nowadays, this is not enough because we use hardware that offers more to us. <a href="https://developer.mozilla.org/en/DOM/DeviceOrientationEvent">Device orientation</a>, for example, allows you to respond to the tilting of a phone or tablet; <a href="https://developer.mozilla.org/en/DOM/Touch_events">touch events</a> are a big thing on mobiles and tablets; <a href="https://hacks.mozilla.org/2011/12/paving-the-way-for-open-games-on-the-web-with-the-gamepad-and-mouse-lock-apis/">the Gamepad API</a> allows us to read out game controllers in browsers; <a href="https://developer.mozilla.org/en/DOM/window.postMessage">postMessage</a> allows us to send messages across domains and browser windows; <a href="https://developer.mozilla.org/en/DOM/Using_the_Page_Visibility_API">pageVisibility</a> allows us to react to users switching to another tab. We can even detect <a href="https://developer.mozilla.org/en/DOM/window.onpopstate">when the history object of the window has been manipulated</a>. Check the list of events in the window object to find some more gems that might not be quite ready but should be available soon for us to dig into.

Whatever comes next in browser support, you can be sure that events will be fired and that you will be able to listen to them. The method works and actually rocks.</p>

## Go Out And Play

And that is it. Events are not hard; in most cases, you just need to subscribe to them and check what comes back as the event object to see what you can do with it. Of course, a lot of browser hacking is still needed at times, but I for one find incredible the number of ways we can interact with our users and see what they are doing. If you want to get really creative with this, stop thinking about the use cases we have now and get down into the nitty gritty of what distances, angles, speed and input can mean to an interface. If you think about it, playing Angry Birds to the largest degree means detecting the start and end of a touch event and detecting the power and direction that the bird should take off in. So, what is stopping you from creating something very interactive and cool?

<em><a href="https://www.flickr.com/photos/opensourceway/6554315319/">Image source</a> of picture on front page.</em>

{{< signature "al" >}}

