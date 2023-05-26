---
title: 'Making Music In A Browser: Recreating Theremin With JS And Web Audio API'
slug: make-music-in-the-browser-with-a-web-audio-theremin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2efabe6-4dd8-4ddd-b80d-77cc2ab35057/leon-theremin-demonstrating-the-thermenvox.jpg
date: 2016-06-08T21:31:14.000Z
author: stuartmemo
description: >-
  Petrograd, Russia, 1920\. Deep in his scientific laboratory, a young Léon
  Theremin accidentally notices that the sound coming from one of his
  high-frequency oscillators changes pitch when he moves his hand. Popular
  culture is changed forever. The theremin’s unique sound proves perfect for
  sci-fi soundtracks and Good Vibrations by the Beach Boys. The world is a
  better place.

  For the better part of a century, musicians have been waiting for a similar
  breakthrough technology to again change the way we create music. I’m delighted
  to announce it has already arrived. It’s called the Web Audio API.
categories:
  - Coding
  - CSS
  - JavaScript
  - Web Audio
---
Petrograd, Russia, 1920. Deep in his scientific laboratory, a young Léon Theremin accidentally notices that the sound coming from one of his high-frequency oscillators changes pitch when he moves his hand. Popular culture is changed forever. The theremin’s unique sound proves perfect for sci-fi soundtracks and Good Vibrations by the Beach Boys. The world is a better place.

For the better part of a century, musicians have been waiting for a similar breakthrough technology to again change the way we create music. I’m delighted to announce it has already arrived. It’s called the Web Audio API.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/04/designing-with-audio-what-is-sound-good-for/#further-reading-on-smashingmag)

*   [Guidelines For Designing With Audio](https://www.smashingmagazine.com/2012/09/guidelines-for-designing-with-audio/)
*   [<span class="headline">How To Create A Responsive 8-Bit Drum Machine</span>](https://www.smashingmagazine.com/2016/08/how-to-create-a-responsive-8-bit-drum-machine-using-web-audio-svg-and-multitouch/)
*   [How To Increase Workflow And Reduce Stress With Nature Sounds](https://www.smashingmagazine.com/2015/10/increase-workflow-reduce-stress-with-nature-sounds/)
*   [<span class="headline">Spotify Playlists To Fuel Your Coding And Design Sessions</span>](https://www.smashingmagazine.com/2016/11/playlists-fuel-coding-design-sessions/)

The Web Audio API is a high-level, high-performance way of making and manipulating sound in the browser. That’s right, <strong>we can make sound in the browser without a plugin or MP3 in sight</strong>. What’s more, I’m going to show you how to recreate Léon Theremin’s amazing invention with a bit of <a href="https://www.smashingmagazine.com/tag/javascript">JavaScript</a>.

{{% feature-panel %}}

<figure><a href="https://commons.wikimedia.org/wiki/File:Termen_demonstrating_Termenvox.jpg"><img title="Léon Theremin demonstrating the Termenvox." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57665cbf-8728-49cb-9abb-523ce4bcaa8a/leon-theremin-demonstrating-the-thermenvox-opt.jpg" alt="Léon Theremin demonstrating the Termenvox." width="500" height="302" /></a><figcaption>Léon Theremin demonstrating the Termenvox. (Image credit: <a href="https://commons.wikimedia.org/wiki/File:Termen_demonstrating_Termenvox.jpg">Wikimedia Commons</a>)</figcaption></figure>

## The Web Audio API

Currently, the Web Audio API is supported in <a href="https://caniuse.com/#search=web%20audio%20api">all major browsers except Internet Explorer</a>, but that’s currently being remedied by <a href="https://www.microsoft.com/en-gb/windows/microsoft-edge">Microsoft Edge</a>. Imagine an electric guitar player. They might take a lead from their guitar, connect it to an effects pedal, then connect it to an amplifier. This concept of chaining things together is central to the API.

To make a sound, we’ll first need a simple web page with a reference to a JavaScript file, something like this:

<pre><code class="language-markup">
&lt;!doctype html&gt;
&lt;html&gt;
    &lt;head&gt;
        &lt;meta charset="utf-8" /&gt;
        &lt;title&gt;My Theremin&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;h1&gt;My Theremin&lt;/h1&gt;
        &lt;script src="theremin.js"&gt;&lt;/script&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

Then, in <code>theremin.js</code> we’ll create an <code>AudioContext</code>. An <code>AudioContext</code> is how we access the Web Audio API’s various methods. We’ll also want an oscillator, which generates a continuous tone.

<pre><code class="language-javascript">var context = new AudioContext(),
  oscillator = context.createOscillator();</code></pre>

Note: The Web Audio API is still prefixed in Safari 9.1, using <code>new webkitAudioContext()</code> instead of <code>new AudioContext()</code>.

To continue our guitar analogy, we need to take a lead from the oscillator and connect it to our speakers. This is done using the <code>connect</code> method. We can access our speakers by using <code>context.destination</code>.

<pre><code class="language-javascript">oscillator.connect(context.destination);</code></pre>

Now that everything is connected, we need to start the oscillator to generate a tone. This is as easy as writing the following:

<pre><code class="language-javascript">oscillator.start(context.currentTime);</code></pre>

You can see we’ve passed <code>context.currentTime</code> here. This means we are telling the browser to start the oscillator now. To stop it, we simply say this:

<pre><code class="language-javascript">oscillator.stop(context.currentTime + 1);</code></pre>

This will stop the oscillator playing 1 second from now. Save and open your page in the <a href="https://www.smashingmagazine.com/2015/09/chrome-firefox-safari-opera-edge-impressive-web-browser-alternatives/">browser</a> to hear a lovely 440 Hz tone play for a second. Beautiful.</p>

## Mouse Control

Now, a sound that plays when we load the page is one thing, but if we want to turn this into an instrument, we’ll have to have to have control over when it starts and stops.

Let’s make the entire page our playing area. Add some simple styles to the page to make sure the <code>body</code> element covers the entire visible area and that it’s more interesting than plain white.

<pre><code class="language-css">html, body {
  background: darkmagenta;
  height: 100%;
}</code></pre>

Next, we’ll add some click event listeners to the <code>body</code> element:

<pre><code class="language-javascript">document.body.addEventListener('mousedown', function () {
  // Mouse has been pressed
});

document.body.addEventListener('mouseup', function () {
  // Mouse has been released
});</code></pre>

You may be thinking, “OK, let’s stick the <code>start</code> call in <code>mousedown</code>, and <code>stop</code> in <code>mouseup</code>.” It’s slightly more complicated than that. Oscillators, by design, are only able to be started and stopped exactly once. Think of them as some sort of weird audio firework. This is actually better for performance, because it means they won’t be hanging around in memory waiting to be used when they don’t need to be. Luckily, oscillators are cheap and easy to make, so we’ll create one every time the user holds down the mouse button.

<pre><code class="language-javascript">var context = new AudioContext(),
  oscillator = null;

document.body.addEventListener('mousedown', function () {
  oscillator = context.createOscillator();
  oscillator.connect(context.destination);
  oscillator.start(context.currentTime);
});

document.body.addEventListener('mouseup', function () {
  oscillator.stop(context.currentTime);
  oscillator.disconnect();
});</code></pre>

Note that in order stop the oscillator that we’ve created in the <code>mousedown</code> event listener, we need to maintain a reference to it outside of the scope of the function, so that <code>mouseup</code> knows to stop that exact oscillator.

Also, just to be on the safe side, we should check that the oscillator has actually been created before we call <code>stop</code> on it. While having a <code>mouseup</code> event without a <code>mousedown</code> preceding it is rare, it is a good programming practice to check that an object exists before performing operations on it.

<pre><code class="language-javascript">document.body.addEventListener('mouseup', function () {
  if (oscillator) {
      oscillator.stop(context.currentTime);
      oscillator.disconnect();
  }
});</code></pre>

Refresh the browser to be amazed by sound playing in response to your mouse clicks! Be disappointed when you realize that all you can do is tap out incomprehensible morse code! Let’s fix that.

## Frequency And Pitch

A theremin changes pitch when the position of the player’s hand changes. Pitch is how high or low a note is, which is technically the speed at which the instrument that is producing the note is vibrating. The frequency of these vibrations is measured in hertz, and luckily the Web Audio API allows us to specify the frequency of an oscillator to change the pitch in exactly this way.

Just after the line in which we create the oscillator, change the frequency like so:

<pre><code class="language-javascript">oscillator.frequency.value = 600;</code></pre>

You’ll now be able to tap away at a different pitch. What we want to do, though, is to alter the pitch depending on where on the screen the mouse is, without repeated clicking.

Our <code>mousedown</code> event listener passes the mouse event to us in the callback, which we’ll label <code>e</code>. We can get the x-coordinate from this by using the <code>clientX</code> property.

<pre><code class="language-javascript">document.body.addEventListener('mousedown', function (e) {
  console.log(e.clientX);
});</code></pre>

So, what do we have to do to convert this coordinate into a frequency suitable for a theremin? Let’s start by creating a <code>calculateFrequency</code> function that takes the x-coordinate and returns a frequency.

<pre><code class="language-javascript">var calculateFrequency = function (mouseXPosition) {

};</code></pre>

The very left x-coordinate of the browser window is 0, while the very right coordinate is the width of the browser in pixels. Without doing anything, this is actually a fairly good range. The range of human hearing goes from 20 to 20,000 Hz, although things start to get unpleasant at around 2,000 Hz, so we don’t want to go any higher than that. That said, we can’t use this range as is because it would limit small devices to producing low notes at low frequencies. Instead, we should use the ratio of the width from the left side of the screen to where the mouse click occurs.

First, we set our minimum and maximum frequencies.

<pre><code class="language-javascript">var minFrequency = 20,
  maxFrequency = 2000;</code></pre>

To calculate the ratio, we divide <code>mouseXPosition</code> by the width of the browser’s window. Then, to get the frequency, multiply this ratio by the maximum frequency. This gives us a frequency of 0 to 2000 Hz. 0 Hz is inaudible, so we’ll just add 20 to get it over the threshold for human hearing.

<pre><code class="language-javascript">var calculateFrequency = function (mouseXPosition) {
  var minFrequency = 20,
      maxFrequency = 2000;

  return ((mouseXPosition / window.innerWidth) * maxFrequency) + minFrequency;
};</code></pre>

Next, replace the hardcoded frequency in our <code>mousedown</code> function with this:

<pre><code class="language-javascript">oscillator.frequency.value = calculateFrequency(e.clientX);</code></pre>

This will calculate the frequency based on the position of the mouse click, but it will do it fairly abruptly. We want our theremin to smoothly slide between frequencies. To do this, we use the Web Audio API’s automation methods. These methods allow us to schedule such changes at some future point in time, but, more importantly for us, it will transition the frequency to its new value <em>smoothly</em>. To automate the frequency change, we delete our previous line and write this:

<pre><code class="language-javascript">oscillator.frequency.setTargetAtTime(calculateFrequency(e.clientX), context.currentTime, 0.01);</code></pre>

What we’re saying here is, smoothly transition the frequency of the oscillator over time. The first parameter is the frequency to change the oscillator to, the second says when to do it (now), and the third is the rate at which it should change. For this value, we want the transition to happen quickly, so a small value is appropriate.

Try it out in your browser by clicking on different areas to hear the pitch change.

A distinct feature of the theremin’s sound is the way it slides from note to note. We can achieve this very same effect by tracking the position of the mouse and updating the frequency as it moves. We’ll use the <code>mousemove</code> event and set up a listener in the same manner as the others. In it, we’ll set the oscillator’s frequency as before.

<pre><code class="language-javascript">document.body.addEventListener('mousemove', function (e) {
  oscillator.frequency.setTargetAtTime(calculateFrequency(e.clientX), context.currentTime, 0.01);
});</code></pre>

This code will cause an error, however, because <code>mousemove</code> will fire even if the mouse isn’t depressed. This means that the oscillator specified here might not even exist yet. We can make sure that an oscillator is actively accepting frequency values by keeping track of whether the mouse has been clicked.

<pre><code class="language-javascript">var context = new AudioContext(),
  mousedown = false,
  oscillator;

var calculateFrequency = function (mouseXPosition) {
  var minFrequency = 20,
      maxFrequency = 2000;

  return ((mouseXPosition / window.innerWidth) * maxFrequency) + minFrequency;
};

document.body.addEventListener('mousedown', function (e) {
  mousedown = true;
  oscillator = context.createOscillator();
  oscillator.frequency.setTargetAtTime(calculateFrequency(e.clientX), context.currentTime, 0.01);
  oscillator.connect(context.destination);
  oscillator.start(context.currentTime);
});

document.body.addEventListener('mouseup', function () {
  mousedown = false;
  oscillator.stop(context.currentTime);
  oscillator.disconnect();
});

document.body.addEventListener('mousemove', function (e) {
  if (mousedown) {
      oscillator.frequency.setTargetAtTime(calculateFrequency(e.clientX), context.currentTime, 0.01);
  }
});</code></pre>

That’s pitch sorted now. But the theremin has one other feature that makes it so expressive. The player can alter the volume of the instrument simply by moving their other hand up or down to make it louder or quieter. We can add this functionality to our web theremin quite easily by approaching volume in a similar manner to the frequency.

First, we’ll need to add a <code>gainNode</code>. Remember the guitar analogy? A gain node is a simple effect we can add to our chain to change the volume of an incoming signal. We’ll create it up at the top with our other variables.

<pre><code class="language-javascript">var gainNode = context.createGain();</code></pre>

Now, we need to add it to the correct position in our chain. Remove the line connecting the oscillator to <code>context.destination</code>, and in its place write the following:

<pre><code class="language-javascript">oscillator.connect(gainNode);
gainNode.connect(context.destination);</code></pre>

Here, we’re taking the connection from the oscillator to our gain node, and then connecting it to our speakers.

Next, duplicate the <code>calculateFrequency</code> function, and rename the copy as <code>calculateGain</code>. This function will instead accept the cursor’s y-position as its only argument. And instead of a minimum and maximum frequency, these values will represent gain. Gain is the value by which you wish to multiply the volume of the incoming signal. So, if you set the gain to 0.5, then that would be half the volume of our oscillator. We don’t want our instrument to be any louder than it already is, so the minimum value will be 0 and the maximum 1. The last tweak to the function will be to subtract our calculation from 1. This means the volume will get louder at the top of the screen and quieter at the bottom. The final function looks like this:

<pre><code class="language-javascript">var calculateGain = function (mouseYPosition) {
  var minGain = 0,
      maxGain = 1;

  return 1 - ((mouseYPosition / window.innerHeight) * maxGain) + minGain;
};</code></pre>

Great! Now all we need to do is set the gain as the mouse moves. Again, duplicate the two lines that specify the <code>frequency.setTargetAtTime</code> lines, and update the copy to refer to the <code>gainNode</code> instead. Oh, and remember to use the y-position of the cursor.

<pre><code class="language-javascript">gainNode.gain.setTargetAtTime(calculateGain(e.clientY), context.currentTime, 0.01);</code></pre>

Behold, <a href="https://stuartmemo.com/smashing-magazine/theremin/">our lovely theremin</a>! If you look at the source code of my version, you’ll see I’ve added listeners for touch events, too, meaning that you can annoy others on public transportation as you perform your theremin masterpiece.

Lovely. Léon Theremin would be proud — a musical instrument in the browser without a plugin in sight.

This tutorial has only touched on the Web Audio API, but I hope it shows you how simple getting something musical up and running fairly quickly can be. You can even use the techniques we’ve learned here to make a synthesizer. I’ve created a little HTML keyboard called <a href="https://stuartmemo.com/qwerty-hancock/">Qwerty Hancock</a> to help you do this very thing. Feel free to show off your own creation in the comments, or <a href="https://twitter.com/stuartmemo">send me a tweet</a>. I’d love to see what you make.

{{< signature "rb, ml, al, il" >}}

