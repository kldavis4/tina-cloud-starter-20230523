---
title: Creating Well-Behaved Sites With The Page Visibility API
slug: creating-sites-with-the-page-visibility-api
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e362807-f072-4c1e-a5d5-133cdd4fb747/numebrs-table-illu-opt.png
date: 2015-01-20T22:34:39.000Z
author: dudley-storey
description: >-
  We’re all resigned to it: launching a browser reloads every tab you previously
  had open, blasting a cacophonous mix of sound and video. While browsers have
  made it easier to control this experience with tab icons and extensions like
  _MuteTab_, for most people this behavior presents a confusing and disorienting
  experience. As developers and designers **it’s our job to make the web
  welcoming**, not overwhelming.

  Doesn’t it make sense that sites should only be active when they are the
  primary focused tab? Why are we burning up batteries and processor cycles with
  animation that can’t be seen?
categories:
  - Coding
  - UX
  - API
  - Web Development
---
We’re all resigned to it: launching a browser reloads every tab you previously had open, blasting a cacophonous mix of sound and video. While browsers have made it easier to control this experience with tab icons and extensions like <em>MuteTab</em>, for most people this behavior presents a confusing and disorienting experience. As developers and designers it’s our job to make the web welcoming, not overwhelming.

Doesn’t it make sense that sites should only be active when they are the primary focused tab? Why are we burning up batteries and processor cycles with animation that can’t be seen?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Building A Cross-Platform WebGL Game</span>](https://www.smashingmagazine.com/2016/07/babylon-js-building-sponza-a-cross-platform-webgl-game/)
*   [CSS3 Transitions: Thank God We Have A Specification!](https://www.smashingmagazine.com/2013/04/css3-transitions-thank-god-specification/)
*   [Creating Responsive Shapes With Clip-Path](https://www.smashingmagazine.com/2015/05/creating-responsive-shapes-with-clip-path/)
*   [Hybrid Mobile Apps: Providing A Native Experience](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)

Thankfully, there is a solution: the HTML5 Page Visibility API. You can see it used particularly effectively in recent projects by Active Theory, such as their work for Under Armor and <a href="https://spacecraftforall.com/">A Spacecraft For All</a>: click to another tab and you’ll find that the multimedia presentation pauses and the music fades away. This behavior typifies what I like to call the “polite web”: sites that are considerate of users’ attention, bandwidth and abilities.

{{% feature-panel %}}

In the past developers have tried to create this behavior by adding <code>onblur()</code> and <code>onfocus()</code> window handlers. While they are considerably better than nothing, the approach is limited by the fact that it can’t tell if the window is actually hidden to the user. For example, having two browser windows side-by-side and switching between them would still register as <code>onblur()</code> or <code>onfocus()</code>, even though the content in each remains perfectly visible.</p>

## Implementing Page Visibility

While there are many possibilities for using the Page Visibility API, perhaps the most obvious use case is when a page contains video: there’s usually little point in continuing to play video content if the user can’t see it.

<pre><code class="language-markup">
&lt;video autoplay controls id="videoElement"&gt;
	&lt;source src="rar.mp4"&gt;
	&lt;source src="rar.webm"&gt;
&lt;/video&gt;

&lt;script&gt;</code>
<code class="language-javascript">var videoElement = document.getElementById("videoElement");
document.addEventListener("visibilitychange", function() {
if (document.hidden) {     
videoElement.pause();  
} else {
videoElement.play();   
} 
});</code>
<code class="language-markup">&lt;/script&gt;
</code></pre>

The one problem with this is that it’s a little abrupt: the audio on the video starts and stops as if cut off with a guillotine when the user switches tabs. The presentation could be improved significantly by fading the audio in and out as the tab is focused. If we’re using jQuery, we can employ a neat use of the <code>animate</code> method to do so.

<pre><code class="language-markup">&lt;script&gt;</code>
<code class="language-javascript">var videoElement = document.getElementById("videoElement");

document.addEventListener("visibilitychange", function() {
if (document.hidden) {     
$("#videoElement").animate({volume: 0}, 1000, "linear", function() {
videoElement.pause();
});
} else {
videoElement.play();  
$("#videoElement").animate({volume: 1}, 1000, "linear");
} 
});</code>
<code class="language-markup">&lt;/script&gt;
</code></pre>

## The Spec

The Page Visibility API spec is surprisingly simple, consisting of just two methods: <code>document.hidden</code> returns <code>true</code> or <code>false</code> depending on the status of the browser window; and those same states are reflected in string form for <code>document.visibilityState</code> (<code>hidden</code> and <code>visible</code>, respectively, with two optional values of <code>prerender</code> and <code>unloaded</code>), with <code>visibilitychange</code> available as an event. <code>document.visibilityState</code> can be useful in determining <em>why</em> a document is not visible, but otherwise <code>document.hidden</code> covers most needs.</p>

## Precautionary Principles And Browser Support

The Page Visibility API takes a deliberately conservative approach to reporting a hidden document: your page will be reported as hidden if the user switches to another tab in the same browser window, but not if you move another window to obscure your page. The API is not foolproof, and will return false positives in some circumstances, erring on the side of caution.

<a href="https://caniuse.com/#feat=pagevisibility">Support for the Page Visibility API is excellent</a>: all modern browsers, with the exception of Opera Mini, fully support the API, including IE10+. Vendor prefixes are also refreshingly absent from implementation of the spec: the only browsers that currently need a <code>–webkit</code> prefix are Android and Blackberry. For that reason (and for the sake of simplified illustration) I have not included any prefixes in the code samples above, although they are easy enough to include and test for.

The Page Visibility API is also an excellent example of progressive enhancement. If the browser doesn’t support the API, the script will be ignored, and the user will simply be subjected to the usual uncontrolled cacophony.

## Other Uses

While audio and video content are obvious candidates for using the Page Visibility API, there are many other possibilities: pausing a slider or presentation while the site remains out of focus, or changing the visual state of the page as it remains neglected.

Considerate use of the API can help make the web a better, greener, and more responsible place, and I would strongly encourage developers to consider how to integrate it into their projects.

{{< signature "il, og, ml" >}}

