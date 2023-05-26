---
title: >-
  How To Create A Responsive 8-Bit Drum Machine Using Web Audio, SVG And
  Multitouch
slug: >-
  how-to-create-a-responsive-8-bit-drum-machine-using-web-audio-svg-and-multitouch
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c0633a4-ebab-48b6-99e1-5dbf7b41b79c/drum-kit-demo-4-preview-opt.png
date: 2016-08-02T20:59:02.000Z
author: davidrousset
description: >-
  In this little tutorial, I’m going to share some tips I recently followed to
  build a fun demo for the _Build 2016_ conference. The idea was to create a
  small 8-bit drum machine, with 8-bit sounds and graphics:

  This small web app was used in one of our demos to illustrate how you can
  easily provide a temporary offline experience when your hosted web app loses
  Internet connectivity. It works in all desktop browsers as well as on all
  smartphones (iOS, Android and Windows Mobile).
categories:
  - Coding
  - Tools
  - SVG
  - Web Audio
---
In this little tutorial, I’m going to share some tips I recently followed to build a fun demo for the <a href="https://www.build2016.com/">Build 2016</a> conference. The idea was to create a <a href="https://david.blob.core.windows.net/build2016/8bitsdrummachine/index.html">small 8-bit drum machine</a>, with 8-bit sounds and graphics:

<figure><br>
<div class="iframe-container"><iframe loading="lazy" src="https://david.blob.core.windows.net/build2016/8bitsdrummachine/index.html" width="600" height="300" frameborder="0"></iframe></div>
<figcaption>You can click on the black drums to make some noise (make sure sound is on). However, please note that the demo may not work on certain devices. (<a href="https://david.blob.core.windows.net/build2016/8bitsdrummachine/index.html">Demo</a>)</figcaption></figure>

This small web app was used in one of our demos to illustrate how you can easily provide a temporary offline experience when your <a href="https://microsoftedge.github.io/WebAppsDocs/en-US/win10/HWA.htm">hosted web app</a> loses Internet connectivity.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Recreating Theremin With JS And Web Audio API](https://www.smashingmagazine.com/2016/06/make-music-in-the-browser-with-a-web-audio-theremin/)
*   [Guidelines For Designing With Audio](https://www.smashingmagazine.com/2012/09/guidelines-for-designing-with-audio/)
*   [How To Increase Workflow And Reduce Stress With Nature Sounds](https://www.smashingmagazine.com/2015/10/increase-workflow-reduce-stress-with-nature-sounds/)
*   [<span class="headline">Spotify Playlists To Fuel Your Coding And Design Sessions</span>](https://www.smashingmagazine.com/2016/11/playlists-fuel-coding-design-sessions/)

{{% feature-panel %}}

Building this drum machine might sound trivial, but it raises some interesting questions. For instance, how do you handle the hit testing for the various pads of this bitmap image? How do you guarantee the same experience across all devices and browsers, accounting for resolution and touch support?

## Options To Handle Hit Testing

Consider the image used in the demo just below. I built it by degrading the original image to 8-bit, as part of our little retro joke. The full online experience would provide the best graphics and sounds, while the offline experience would offer a degraded 8-bit version.

You’ll probably be tempted to press on the various black circles to make some noises. Let’s figure out how to handle clicks on those parts of the image using HTML.

The older folks among us might be tempted to use an <strong>image map</strong>, with the <code>map</code> and <code>area</code> tags. We can define areas of the image with various geometric shapes, including ellipses and circles. That might do the trick.

Unfortunately, this approach has two problems, the first one being major:

*   It’s **pixel-based**, so it won’t scale across resolutions and devices. Suppose your bitmap image had a fixed size of 600 × 400 pixels. If you defined areas inside it, you would build them based on this 600 × 400 resolution. As soon as you expand or contract the image to match the device’s resolution, the areas wouldn’t match the image any longer. The [jQuery RWD Image Maps](https://github.com/stowball/jQuery-rwdImageMaps) plugin will compute the area’s coordinates dynamically. But I thought that adding the jQuery library and this plugin just for this simple hit-testing demo would be too much. I was looking for something simpler.
*   The feature was originally **defined to enable navigation to URLs**. I’d rather call a JavaScript function to use web audio to play the sounds. Still, you could use this trick by defining an `href="#"` and registering the click event in the area.

My next idea was to put it in a <strong>2D canvas</strong>, which I could stretch to the current resolution using CSS. This solution might work, but it would be a really complex implementation for such a simple web app. Indeed, this would entail:

*   manually defining the hit zones by code;
*   handling the click event on the canvas, finding the exact x and y mouse coordinates of the click, and scaling that to the current resolution;
*   computing the hit-testing algorithm by checking whether those 2D coordinates are in one of the ellipses that we have defined in the code.

It’s not tremendously complex, but it’s a fair bit of math for something that should be simple to build. Also, if you’d like to keep the aspect ratio of the image, the 2D canvas method also entails resizing the canvas’ size by computing in the code the ratio during the loading phase and inside the <code>onresize</code> event.

Finally, I thought of what should be the most obvious solution. When you think about what <strong>scales across devices</strong>, facilitates <strong>hit-testing</strong> and handles <strong>aspect ratios</strong>, the answer is naturally <strong>SVG</strong>. The “S” stands for “scalable” — we can define a viewbox with some parameters to lock the aspect ratio.

Sure, but you’re probably going to say, “How does that help us define the hit zones in the image?” Not to mention that we’re working with a bitmap image, not a vector?

Let me show you what I’ve done. Follow these very same steps for any similar experience you’d like to build on top of a bitmap image.

Save the image above of the 8-bit drum machine on your computer.

We need a tool that will <strong>generate an XML of our SVG</strong> content. I’ll use <a href="https://inkscape.org/">InkScape</a>, a free application, but you can probably do the same thing with <a href="https://github.com/SVG-Edit/svgedit">SVG Edit</a> in the browser.

Open Inkscape, go to “File” → “Document Properties,” and change the “Custom size” values to 160 × 90.

Go to “File” → “Import,” and choose the <code>8bitsdrummachine.jpg</code> file that you’ve saved. Choose “Link” as the import type, and leave the other options as is. Then, stretch the image to map our drawing zone:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d87c460f-e444-424a-a3e8-09785acd60b4/drum-kit-demo-1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81e8993f-f012-4268-8ff2-1b74c341ee88/drum-kit-demo-1-preview-opt.png" alt="Creating A Small 8-bit Responsive Drum Machine Using Web Audio, SVG &amp; Multi-Touches Image" width="500" height="362" /></a></figure>

We’re now going to <strong>draw ellipses on top on our image</strong>. Choose red, and make sure that your ellipses perfectly cover the black drums:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f3dea67-3793-4f33-a724-e823564b06a1/drum-kit-demo-2.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52187fb7-3843-43e1-833e-bb8032dd4c3a/drum-kit-demo-2-preview-opt.png" alt="Creating A Small 8-bit Responsive Drum Machine Using Web Audio, SVG &amp; Multi-Touches Image" width="500" height="362" /></a></figure>

Those seven ellipses will be our hit zones.

To be able to find those SVG forms easily in our code, right-click on each of them, choose “Object Properties” and change its “ID” and “Label” properties to <code>button1</code> (up to <code>button7</code>) and <code>#button1</code> (up to <code>#button7</code>), respectively:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff2131b5-83ed-4e63-99df-79721a5426c3/drum-kit-demo-3.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79057918-5456-4a61-b07c-c2a65bf619c0/drum-kit-demo-3-preview-opt.png" alt="Creating A Small 8-bit Responsive Drum Machine Using Web Audio, SVG &amp; Multi-Touches Image" width="500" height="362" /></a></figure>

Now that we have defined the hit zones precisely, let’s make them <strong>transparent</strong>, rather than hiding them under the image. Right-click on each of them, choose “Fill and Stroke,” and set the alpha value (“A”) to <code>0</code>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/671b2898-1678-45a8-b4a1-51b4db44968d/drum-kit-demo-4.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c0633a4-ebab-48b6-99e1-5dbf7b41b79c/drum-kit-demo-4-preview-opt.png" alt="Creating A Small 8-bit Responsive Drum Machine Using Web Audio, SVG &amp; Multi-Touches Image" width="500" height="362" /></a></figure>

<strong>Note:</strong> We’re using simple ellipses here, but you could draw any complex shape allowed by SVG on top of the image to achieve a similar result.</p>

<strong>Save the result</strong> on your hard drive by going to “File” → “Save as…” in the menu.

Open this file with your favorite editor (Notepad++, Sublime, Visual Studio Code, whatever), and add the following line of XML just after the <code>viewBox</code> attribute:

<pre><code class="language-js">preserveAspectRatio="xMidYMin meet"</code></pre>

Mozilla’s documentation <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/preserveAspectRatio">explains what this SVG attribute does</a>.

You’re done with this part. This piece of SVG will embed the bitmap image, add a layer of a transparent vector form that can be clicked on, and scale across resolutions, keeping the aspect ratio, thanks to the <code>preserveAspectRatio</code> attribute.

Now, we need to set the code to tie those SVG ellipses to our event handler.

## What About Web Audio?

I’ve already <a href="https://www.davrous.com/2015/11/05/creating-fun-immersive-audio-experiences-with-web-audio/">covered web audio elsewhere</a> in detail. I’m reusing part of that code, including the <code>Sound</code> object:

<pre><code class="language-js">var Sound = (function () {
    function Sound(url, audioContext, masterGain, loop, callback) {
        this.url = url;
        this.audioContext = audioContext;
        this.masterGain = masterGain;
        this.loop = loop;
        this.callback = callback;
        this.gain = this.audioContext.createGain();
        this.gain.connect(this.masterGain);
        this.isReadyToPlay = false;
        this.loadSoundFile(url);
    }
    Sound.prototype.loadSoundFile = function () {
        if (canUseWebAudio) {
            var that = this;
            // make XMLHttpRequest (AJAX) on server
            var xhr = new XMLHttpRequest();
            xhr.open('GET', this.url, true);
            xhr.responseType = 'arraybuffer';
            xhr.onload = function (e) {
                // decoded binary response
                that.audioContext.decodeAudioData(this.response,
                function (decodedArrayBuffer) {
                    // get decoded buffer
                    that.buffer = decodedArrayBuffer;
                    that.isReadyToPlay = true;
                    if (that.callback) {
                        that.callback();
                    }
                }, function (e) {
                    console.log('Error decoding file', e);
                });
            };
            xhr.send();
        }
    };
    Sound.prototype.play = function () {
        if (canUseWebAudio &amp;&amp; this.isReadyToPlay) {
            // make source
            this.source = this.audioContext.createBufferSource();
            // connect buffer to source
            this.source.buffer = this.buffer;
            this.source.loop = this.loop;
            // connect source to receiver
            this.source.connect(this.gain);
            // play
            this.source.start(0);
        }
    };
    return Sound;
})();</code></pre>

Then, as I’ve also <a href="https://www.davrous.com/2016/02/05/discovering-sponza-by-babylon-js-and-sharing-tips-on-how-to-build-a-cross-platforms-webgl-game/">explained elsewhere</a>, we need to handle web audio in a special way for iOS, by unlocking the <code>AudioContext</code>:

<pre><code class="language-js">try {
    if (typeof AudioContext !== 'undefined') {
        audioContext = new AudioContext();
        canUseWebAudio = true;
    } else if (typeof webkitAudioContext !== 'undefined') {
        audioContext = new webkitAudioContext();
        canUseWebAudio = true;
    }
    if (/iPad|iPhone|iPod/.test(navigator.platform)) {
        this._unlockiOSaudio();
    }
    else {
        audioUnlocked = true;
    }
15.} catch (e) {
    console.error("Web Audio: " + e.message);
17.}
18. 
19.function unlockiOSaudio() {
    var unlockaudio = function () {
        var buffer = audioContext.createBuffer(1, 1, 22050);
        var source = audioContext.createBufferSource();
        source.buffer = buffer;
        source.connect(audioContext.destination);
        source.start(0);
        setTimeout(function () {
            if ((source.playbackState === source.PLAYING_STATE || source.playbackState === source.FINISHED_STATE)) {
                audioUnlocked = true;
                window.removeEventListener('touchend', unlockaudio, false);
            }
        }, 0);
    };
    window.addEventListener('touchend', unlockaudio, false);
}</code></pre>

## Handling Multitouch Across Devices

In my opinion, the best touch specification for the web is <a href="https://www.w3.org/TR/pointerevents/">pointer events</a>. I’ve already <a href="https://www.davrous.com/2015/08/10/unifying-touch-and-mouse-how-pointer-events-will-make-cross-browsers-touch-support-easy/">covered the specification in detail</a>. We’ll use it to wire our event handler to our SVG shapes.

In the code below, we’re referring to all of the SVG shapes that we built with InkScape — shapes with which we’ve associated IDs (<code>button1</code>, <code>button2</code>, etc.). Then, we’re loading the various 8-bit sounds from the web server and decoding them via our <code>Sound</code> object. Finally, using the <code>pointerdown</code> event, we’re playing each sound associated with each SVG shape:

<pre><code class="language-js">var soundsCollection = [];
var buttonsCollection = [];

	buttonsCollection.push(document.getElementById("button1"));
	buttonsCollection.push(document.getElementById("button2"));
	buttonsCollection.push(document.getElementById("button3"));
	buttonsCollection.push(document.getElementById("button4"));
	buttonsCollection.push(document.getElementById("button5"));
	buttonsCollection.push(document.getElementById("button6"));
	buttonsCollection.push(document.getElementById("button7"));

if (canUseWebAudio) {
    masterGain = audioContext.createGain();
    masterGain.connect(audioContext.destination);
    soundsCollection.push(new Sound("./8bits_sounds/clap.wav", audioContext, masterGain, false, newSoundLoaded));
    soundsCollection.push(new Sound("./8bits_sounds/cowbell.wav", audioContext, masterGain, false, newSoundLoaded));
    soundsCollection.push(new Sound("./8bits_sounds/hihat1.wav", audioContext, masterGain, false, newSoundLoaded));
    soundsCollection.push(new Sound("./8bits_sounds/kick1.wav", audioContext, masterGain, false, newSoundLoaded));
    soundsCollection.push(new Sound("./8bits_sounds/snare1.wav", audioContext, masterGain, false, newSoundLoaded));
    soundsCollection.push(new Sound("./8bits_sounds/tom1.wav", audioContext, masterGain, false, newSoundLoaded));
    soundsCollection.push(new Sound("./8bits_sounds/kick3.wav", audioContext, masterGain, false, newSoundLoaded));
}

var soundsLoaded = 0;

function newSoundLoaded() {
    soundsLoaded++;
    if (soundsLoaded == 7) {
        // Ready to rock &amp;amp;amp; roll!
        for (var i = 0; i &lt; 7; i++) {
            buttonsCollection[i].addEventListener("pointerdown", onPointerDown);
        }
    }
}
function onPointerDown(eventArgs) {
    var buttonClicked = eventArgs.currentTarget.id;
    var soundId = buttonClicked.substr(buttonClicked.length - 1) - 1;
    var soundToPlay = soundsCollection[soundId];
    soundToPlay.play();
}</code></pre>

With this code, we’re supporting multitouch in a simple way. But it has one drawback: it only works in the Microsoft Edge browser. To support all browsers and devices, you can use the jQuery-based <a href="https://github.com/jquery/PEP#why-pointer-events">Pointer Events Polyfill</a>.</p>

<pre><code class="language-js">&lt;script src="https://code.jquery.com/pep/0.4.1/pep.min.js"&gt;&lt;/script&gt;</code></pre>

Add the following property to the HTML element that contains the relevant UI (the <code>body</code> element in our demo):

<pre><code class="language-js">touch-action="none"</code></pre>

## Going Further With Synthesizing

In this small demo, I’ve downloaded recorded samples of 8-bit sounds. But web audio has some great features that could help you generate sounds via oscillators, for example, as <a href="https://dev.opera.com/articles/drum-sounds-webaudio/">Chris Lowis explains on Dev.Opera</a>.

I hope that you’ve enjoyed this little tutorial and that it helps you solve some of your issues or create cool experiences.
<blockquote style="border-radius: 8px;">This article is part of the web development series from Microsoft tech evangelists and engineers on practical JavaScript learning, open source projects, and interoperability best practices including <a href="https://blogs.windows.com/msedgedev/2015/05/06/a-break-from-the-past-part-2-saying-goodbye-to-activex-vbscript-attachevent/?wt.mc_id=DX_873181">Microsoft Edge</a> browser.

We encourage you to test across browsers and devices including Microsoft Edge – the default browser for Windows 10 – with free tools on <a href="https://dev.windows.com/en-us/?wt.mc_id=DX_873181">dev.microsoftedge.com</a>, including <a href="https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/?wt.mc_id=DX_873181">F12 developer tools</a> — seven distinct, fully-documented tools to help you debug, test, and speed up your webpages. Also, <a href="https://blogs.windows.com/msedgedev/?wt.mc_id=DX_873181">visit the Edge blog</a> to stay updated and informed from Microsoft developers and experts.</blockquote>

{{< signature "ms, il, al" >}}

