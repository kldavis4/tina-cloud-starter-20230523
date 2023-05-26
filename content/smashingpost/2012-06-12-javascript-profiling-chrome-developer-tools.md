---
title: JavaScript Profiling With The Chrome Developer Tools
slug: javascript-profiling-chrome-developer-tools
image: null
date: 2012-06-12T09:21:53.000Z
author: zack-grossbart
description: >-
  Your website works. Now let’s make it work faster. Website performance is about two things: how fast the page loads, and how fast the code on it runs.
categories:
  - Coding
  - JavaScript
  - Browsers
---
Little changes in your code can have gigantic performance impacts. A few lines here or there could mean the difference between a blazingly fast website and the dreaded “Unresponsive Script” dialog. This article shows you a few ways to find those lines of code with Chrome Developer Tools.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">How To Write Fast, Memory-Efficient JavaScript</span>](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [Creating A “Save For Later” Chrome Extension With Modern Web Tools](https://www.smashingmagazine.com/2014/11/creating-save-later-chrome-extension-modern-web-tools/)
*   [Revisiting Firefox’s DevTools](https://www.smashingmagazine.com/2015/12/revisiting-firefox-devtools/)

## Establish A Baseline

We’ll look at a simple application called a color sorter, which presents a grid of rainbow colors that you can drag and drop to mix up. Each dot is a <code>div</code> tag with a little CSS to make it look like a circle.

{{% feature-panel %}}

<a href="https://zgrossbart.github.com/jsprofarticle/index1.htm"><img class="alignright size-full wp-image-119201" title="The Color Sorter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8693df67-9d9b-4995-a1c3-9c4f91f60b77/color-sorter.png" alt="The Color Sorter" width="400" height="459" /></a>

Generating my rainbow colors was a little tricky, so I got help from “<a href="https://krazydad.com/tutorials/makecolors.php">Making Annoying Rainbows in JavaScript</a>.”

The page loads pretty fast, but it still takes a moment and blinks a little before it paints. Time to profile the page and make it faster.

Always start performance-improvement projects with a baseline understanding of how fast or slow your application already is. The baseline will let you know whether you’re making improvements and help you make tradeoffs. For this article, we’ll use Chrome Developer Tools.

The profiler is part of Chrome Developer Tools, which is always available in Chrome. Click the “Tools” menu under the little wrench to open it. <a href="https://getfirebug.com">Firebug</a> has some profiling tools, too, but the WebKit browsers (Chrome and Safari) are best at profiling code and showing timelines. Chrome also offers an excellent tool for event tracing, called <a href="https://developers.google.com/web-toolkit/speedtracer/">Speed Tracer</a>.

To establish our baseline, we’ll start recording in the “Timeline” tab, load our page and then stop the recording. (To start recording once Chrome Developer Tools is open, click the “Timeline” tab, and then the small black circle icon for “Record” at the very bottom of the window.) Chrome is smart about not starting to record until the page starts to load. I run it three times and take the average, in case my computer runs slowly during the first test.

<img class="alignright size-full wp-image-119199" title="Performance baseline 1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b69c72c9-7957-48c8-b39e-6f5d3fac0e37/baseline1.png" alt="Performance baseline 1" width="500" height="562" />

My average baseline — i.e. the time between the first request for the page and the final painting of the page in the browser — is 1.25 seconds. That’s not bad, but it’s not great for such a small page.

I want to make my code run faster, but I’m not sure what’s making it slow. The profiler helps me find out.</p>

## Create A Profile

The timeline tells us how long our code took to run, but that doesn’t help us know what’s going on while it’s running. We could make changes and run the timeline again and again, but that’s just shooting in the dark. The “Profiles” tab gives us a better way to see what’s going on.

Profilers show us which functions take the most time. Let’s make our baseline profile by switching to the “Profiles” tab in Chrome Developer Tools, where three types of profiling are offered:

1.  **JavaScript CPU profile** Shows how much CPU time our JavaScript is taking.
2.  **CSS selector profile** Shows how much CPU time is spent processing CSS selectors.
3.  **Heap snapshot** Shows how memory is being used by our JavaScript objects.

We want to make our JavaScript run faster, so we’ll use the CPU profiling. We start the profile, refresh the page and then stop the profiler.

<img class="alignright size-full wp-image-119202" title="The first profile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b68ec18-f234-440a-9f43-005fbf02f247/profile1.png" alt="The first profile" width="500" height="562" />

The first thing that’s clear from the profile is that a lot is going on. The color sorter uses jQuery and jQuery UI, which are doing a lot of stuff like managing plugins and parsing regular expressions. I can also see that two of my functions are at the top of the list: <code>decimalToHex</code> and <code>makeColorSorter</code>. These two functions take a total of 13.2% of my CPU time, so they’re a good place to start making improvements.

We can click the arrow next to the function calls to open the complete function-call stack. Expanding them, I see that <code>decimalToHex</code> is called from <code>makeColorSorter</code>, and <code>makeColorSorter</code> is called from <code>$(document).ready</code>.

Here’s the code:

<pre><code class="language-javascript">$(document).ready(function() {
    makeColorSorter(.05, .05, .05, 0, 2, 4, 128, 127, 121);
    makeSortable();
});</code></pre>

Knowing where they’re called from also makes clear that making the colors sortable isn’t my biggest performance problem. Performance issues resulting from the addition of a lot of sortables <a href="https://37signals.com/svn/posts/3137-using-event-capturing-to-improve-basecamp-page-load-times">is common</a>, but my code is taking more time to add DOM elements than to make them sortable.

I want to start making those functions faster, but first I want to isolate my changes. A lot happens when the page loads, and I want to get all of that out of my profile.</p>

## Isolate The Problem

Instead of loading the color sorter when the document is ready, I’ll make a <a href="https://zgrossbart.github.com/jsprofarticle/index2.htm">second version</a> that waits until I press a button to load the color sorter. This isolates it from the document loading and helps me profile just the code. I can change it back once I’m done tuning performance.

Let’s call the new function <code>testColorSorter</code> and bind it to a clickable button:

<pre><code class="language-javascript">function testColorSorter() {
    makeColorSorter(.05, .05, .05, 0, 2, 4, 128, 127, 121);
    makeSortable();
}</code></pre>

<pre><code class="language-markup tmp-html">&lt;button id="clickMe" onclick="testColorSorter();"&gt;Click me&lt;/button&gt;</code></pre>

Changing the application before we profile could alter the performance of the application unexpectedly. This change looks pretty safe, but I still want to run the profiler again to see whether I’ve accidentally changed anything else. I’ll create this new profile by starting the profiler, pressing the button in the app and then stopping the profile.

<img class="alignright size-full wp-image-119203" title="The second profile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f964b92-f0e0-474b-b37a-4cd135caa1b0/profile2.png" alt="The second profile" width="500" height="562" />

The first thing to notice is that the <code>decimalToHex</code> function is now taking up 4.23% of the time to load; it’s what the code spends the most time on. Let’s create a new baseline to see how much the code improves in this scenario.

<img class="alignright size-full wp-image-119200" title="The second baseline" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/785f4df1-97c6-435f-87ee-3cb814c70734/baseline2.png" alt="The second baseline" width="500" height="562" />

A few events occur before I press the button, but I only care about how long it took between the times the mouse was clicked and the browser painted the color sorter. The mouse button was clicked at 390 milliseconds, and the paint event happened at 726 milliseconds; 726 minus 390 equals my baseline of 336 milliseconds. Just as with the first baseline, I ran it three times and took the average time.

At this point, I know where to look and how long the code takes to run. Now we’re ready to start fixing the problem.

## Make It Faster

The profiler only tells us which function is causing the problem, so we need to look into it and understand what it does.

<pre><code class="language-javascript">function decimalToHex(d) {
    var hex = Number(d).toString(16);
    hex = "00".substr(0, 2 - hex.length) + hex; 

    console.log('converting ' + d + ' to ' + hex);
    return hex;
}</code></pre>

Each dot in the color sorter takes a background color value in <a href="https://en.wikipedia.org/wiki/Hexadecimal">hex format</a>, such as <code>#86F01B</code> or <code>#2456FE</code>. These values represent the red, green and blue values of the color. For example, <img style="margin: 0px" title="Blue dot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c88429a9-12df-4a14-a152-dfc0387dc161/bluedot.png" alt="Blue dot" width="14" height="14" /> has a background color of <code>#2456FE</code>, which means a red value of 36, a green value of 86 and a blue value of 254. Each value must be between 0 and 255.

The <code>decimalToHex</code> function converts these <a href="https://en.wikipedia.org/wiki/Rgb">RGB</a> colors to hex colors that we can use on the page.

The function is pretty simple, but I’ve left a <code>console.log</code> message in there, which is just some debugging code we can remove.

The <code>decimalToHex</code> function also adds padding to the beginning of the number. This is important because some base-10 numbers result in a single hex digit; 12 in base 10 is C in hex, but CSS requires two digits. We can make the conversion faster by making it a little less generic. I know that the numbers to be padded each have one digit, so we can rewrite the function like this:

<pre><code class="language-javascript">function decimalToHex(d) {
    var hex = Number(d).toString(16);
    return hex.length === 1 ? '0' + hex : hex; }</code></pre>

<a href="https://zgrossbart.github.com/jsprofarticle/index3.htm">Version three</a> of the color sorter changes the string only when it needs the padding and doesn’t have to call <code>substr</code>. With this new function, our runtime is 137 milliseconds. By profiling the code again, I can see that the <code>decimalToHex</code> function now takes only 0.04% of the total time — putting it way down the list.

<img class="alignright size-full wp-image-119204" title="The third profile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44ce8375-bf9f-41f3-87e4-eded7fb49d57/profile3.png" alt="The third profile" width="500" height="562" />

We can also see that the function using the most CPU is <code>e.extend.merge</code> from jQuery. I’m not sure what that function does because the code is minimized. I could add the development version of jQuery, but I can see that the function is getting called from <code>makeColorSorter</code>, so let’s make that one faster next.</p>

## Minimize Content Changes

The rainbow colors in the color sorter are generated from a sine wave. The code looks at a center point in the color spectrum and creates a wave through that center point over a specified width. This changes the colors into a rainbow pattern. We can also change the colors in the rainbow by changing the frequency of the red, green and blue.

<pre><code class="language-javascript">function makeColorSorter(frequency1, frequency2, frequency3,
                         phase1, phase2, phase3,
                         center, width, len) {

    for (var i = 0; i &lt; len; ++i)
    {
       var red = Math.floor(Math.sin(frequency1 * i + phase1) * width + center);
       var green = Math.floor(Math.sin(frequency2 * i + phase2) * width + center);
       var blue = Math.floor(Math.sin(frequency3 * i + phase3) * width + center);

       console.log('red: ' + decimalToHex(red));
       console.log('green: ' + decimalToHex(green));
       console.log('blue: ' + decimalToHex(blue));

       var div = $('&lt;div class="colorBlock"&gt;&lt;/div&gt;');
       div.css('background-color', '#' + decimalToHex(red) + decimalToHex(green) + decimalToHex(blue));
       $('#colors').append(div);

    }
}</code></pre>

We could take out more <code>console.log</code> functions. The calls are especially bad because each is also calling the <code>decimalToHex</code> function, which means that <code>decimalToHex</code> is effectively being called twice as often as it should.

This function changes the DOM a lot. Every time the loop runs, it adds a new <code>div</code> to the <code>colors</code> div tag. This makes me wonder whether that’s what the <code>e.extend.merge</code> function was doing. The profiler makes it easy to tell with a simple experiment.

Instead of adding a new <code>div</code> each time the loop runs, I want to add all of the <code>div</code> tags at once. Let’s create a variable to hold them, and then add them once at the end.

<pre><code class="language-javascript">function makeColorSorter(frequency1, frequency2, frequency3,
                         phase1, phase2, phase3,
                         center, width, len) {

    var colors = "";
    for (var i = 0; i &lt; len; ++i)
    {
       var red = Math.floor(Math.sin(frequency1 * i + phase1) * width + center);
       var green = Math.floor(Math.sin(frequency2 * i + phase2) * width + center);
       var blue = Math.floor(Math.sin(frequency3 * i + phase3) * width + center);

       colors += '&lt;div class="colorBlock" style="background-color: #' + 
           decimalToHex(red) + decimalToHex(green) + decimalToHex(blue) + '"&gt;&lt;/div&gt;';
    }

    $('#colors').append(colors);
}</code></pre>

This small change in the code means that the DOM changes once, when it adds all of the <code>div</code> tags. Testing that with the timeline, we see that the runtime between the click and the paint events is now 31 milliseconds. This one DOM change has brought the time for <a href="https://zgrossbart.github.com/jsprofarticle/index4.htm">version four</a> down by about 87%. We can also run the profiler again and see that the <code>e.extend.merge</code> function now takes up such a small percentage of the time that it doesn’t show up on the list.

We could make the code one notch faster by removing the <code>decimalToHex</code> function entirely. CSS <a href="https://www.w3schools.com/cssref/css_colors.asp">supports RGB colors</a>, so we don’t need to convert them to hex. Now we can write our <code>makeColorSorter</code> function like this:

<pre><code class="language-javascript">function makeColorSorter(frequency1, frequency2, frequency3,
                         phase1, phase2, phase3,
                         center, width, len) {

    var colors = "";
    for (var i = 0; i &lt; len; ++i)
    {
       var red = Math.floor(Math.sin(frequency1 * i + phase1) * width + center);
       var green = Math.floor(Math.sin(frequency2 * i + phase2) * width + center);
       var blue = Math.floor(Math.sin(frequency3 * i + phase3) * width + center);

       colors += '&lt;div class="colorBlock" style="background-color: rgb(' + 
           red + ',' + green + ',' + blue + ')"&gt;&lt;/div&gt;';
    }

    $('#colors').append(colors);
}</code></pre>

<a href="https://zgrossbart.github.com/jsprofarticle/index5.htm">Version five</a> runs in only 26 milliseconds and uses 18 lines of code for what used to take 28 lines.</p>

## JavaScript Profiling In Your Application

Real-world applications are much more complex than this color sorter, but profiling them follows the same basic steps:

1.  **Establish a baseline** so that you know where you’re starting from.
2.  **Isolate the problem** from any other code running in the application.
3.  **Make it faster** in a controlled environment, with frequent timelines and profiles.

There are a few other rules to follow when tuning performance:

1.  **Start with the slowest parts first** so that you get the most improvement for the time spent tuning.
2.  **Control the environment.** If you switch computers or make any other major changes, always run a new baseline.
3.  **Repeat the analysis** to prevent anomalies on your computer from skewing the results.

Everyone wants their website to run faster. You have to develop new features, but new features usually make a website run slower. So, investing time in tuning the performance does pay off.

Profiling and tuning cut the <a href="https://zgrossbart.github.com/jsprofarticle/index6.htm">final color sorter</a>’s runtime by over 92%. How much faster could your website be?

<em>(al) (km)</em>

