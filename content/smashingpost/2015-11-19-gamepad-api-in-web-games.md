---
title: Using The Gamepad API In Web Games
slug: gamepad-api-in-web-games
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0048f63-f08f-4004-834b-26a70541d851/01-gamepads-opt-preview1.jpg
date: 2015-11-19T02:17:01.000Z
author: charliewalter
description: >-
  The Gamepad API is a relatively new piece of technology that allows us to
  **access the state of connected gamepads using JavaScript**, which is great
  news for HTML5 game developers.

  A lot of game genres, such as racing and platform fighting games, rely on a
  gamepad rather than a keyboard and mouse for the best experience. This means
  these games can now be played on the web with the same gamepads that are used
  for consoles. A demo is available, and if you don’t have a gamepad, you can
  still enjoy the demo using a keyboard.
categories:
  - Coding
  - JavaScript
  - Games
  - HTML5
---
The Gamepad API is a relatively new piece of technology that allows us to access the state of connected gamepads using JavaScript, which is great news for HTML5 game developers.

A lot of game genres, such as racing and platform fighting games, rely on a gamepad rather than a keyboard and mouse for the best experience. This means these games can now be played on the web with the same gamepads that are used for consoles.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/10/design-your-own-mobile-game/#further-reading-on-smashingmag)

*   [<span class="headline">How To Design A Mobile Game With HTML5</span>](https://www.smashingmagazine.com/2012/10/design-your-own-mobile-game/)
*   [<span class="headline">Building A Cross-Platform WebGL Game With Babylon.js</span>](https://www.smashingmagazine.com/2016/07/babylon-js-building-sponza-a-cross-platform-webgl-game/)
*   [Rebuilding An HTML5 Game In Unity](https://www.smashingmagazine.com/2014/04/rebuilding-an-html5-game-in-unity/)
*   [What Web Designers Can Learn From Video Games](https://www.smashingmagazine.com/2011/07/what-web-designers-can-learn-from-video-games/)

A <a href="https://charliejwalter.net/gamepad/demos/main">demo is available</a>, and if you don’t have a gamepad, you can still enjoy the demo using a keyboard.

{{% feature-panel %}}

### Keyboard Fallback

There are also apps like <a href="https://getjoypad.com/legacy/">Joypad</a> (iOS) and <a href="https://play.google.com/store/apps/details?id=com.negusoft.ugamepad&amp;hl=en">Ultimate Gamepad</a> (Android) that allow you to connect a smartphone to the computer via a “receiver” app. Receiver applications simulate keyboard input, as opposed to a gamepad.</p>

## Which Gamepads Work?

Any gamepad that is understood by the operating system as either an XInput or DirectInput device will work with the Gamepad API. Getting other console controllers to work is possible, but that would require either hardware converters or additional software.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242c4103-7298-4f5b-9640-7925b636df87/01-gamepads-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6160bdf3-e552-4ccc-a29b-80cac03affcd/01-gamepads-opt-preview.jpg" alt="Gamepads" /></a><figcaption>Gamepads. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242c4103-7298-4f5b-9640-7925b636df87/01-gamepads-opt.jpg">View large version</a>)</figcaption></figure>

## Browser Support

Because this API is relatively new and experimental, <a href="https://caniuse.com/#feat=gamepad">browser support is limited</a> and the <a href="https://www.w3.org/TR/gamepad/">W3C documentation</a> is still a working draft.

Nevertheless, browser implementation is <a href="https://caniuse.com/#feat=gamepad">above 50%</a>, which includes all major browsers. The API is even making its way into the mobile world, with Chrome for Android being the first mobile browser to support it.

On Nintendo’s Wii U browser, the Wii U gamepad is accessible. Unfortunately, Nintendo hasn’t yet implemented the Gamepad API; instead, the <a href="https://www.nintendo.com/wiiu/built-in-software/browser-specs/extended-functionality/">device has its own property</a> on the window (<code>window.wiiu.gamepad</code>) and stores its button states as hexadecimal values, with specific flags for each button.</p>

### Feature Detection

We can check whether a browser supports the Gamepad API with this snippet:

<pre><code class="language-javascript">if(!!navigator.getGamepads){
    // Browser supports the Gamepad API
}</code></pre>

## Reading The Gamepad States

The <code>Gamepad</code> states are accessible with:

<pre><code class="language-javascript">var gamepads = navigator.getGamepads();</code></pre>

Currently, in Chrome and Opera, this will return a <code>GamepadList</code> of up to four <code>Gamepad</code> objects.</p>

<pre><code class="language-javascript">GamepadList {0: Gamepad, 1: Gamepad, 2: undefined, 3: undefined}</code></pre>

Firefox, instead, returns a JavaScript <code>Array</code> of <code>Gamepad</code>s, which, theoretically, is infinite. (I’ve had nine gamepads connected at the same time.)

<pre><code class="language-javascript">Array [ Gamepad, Gamepad ]</code></pre>

### Polling

We can poll the <code>Gamepad</code> states using <code>requestAnimationFrame</code>. Depending on the number of gamepads you want to support, this will increase the complexity of how you use the <code>Gamepad</code> states. If you want to support only one gamepad, you could poll for the first gamepad in the collection like so:

<pre><code class="language-javascript">var gamepad = navigator.getGamepads()[0];</code></pre>

This means it will grab the first gamepad that is connected or, if all gamepads are already connected, the first gamepad to have a button pressed.</p>

### Each `Gamepad` object looks like this:

<pre><code class="language-javascript">axes: Array[4]
buttons: Array[16]
connected: true
id: "Xbox 360 Controller (XInput STANDARD GAMEPAD)"
index: 0
mapping: "standard"
timestamp: 12</code></pre>

This is the <code>Gamepad</code> object of a <a href="https://www.microsoft.com/hardware/en-gb/p/xbox-360-controller-for-windows">Microsoft Xbox 360 controller for Windows</a>.</p>

<strong>Note:</strong> The <code>id</code> is not consistent across browsers. For example, it’s <code>45e-28e-Wireless 360 Controller</code> in <a href="https://www.mozilla.org/en-GB/firefox/new/">Mozilla Firefox</a>, which is different from what <a href="https://www.google.com/chrome/">Google Chrome</a> provides above.</p>

### Info

<table class="article-table two-columns">
<thead>
<tr>
<th>Property</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>connected</code></td>
<td>This is a boolean that indicates the gamepad’s connectivity</td>
</tr>
<tr>
<td><code>id</code></td>
<td>This string contains identifying information about the gamepad</td>
</tr>
<tr>
<td><code>index</code></td>
<td>This is a unique auto-incremented integer for each gamepad</td>
</tr>
<tr>
<td><code>mapping</code></td>
<td>This string tells us whether the browser has remapped the device to a known layout</td>
</tr>
<tr>
<td><code>timestamp</code></td>
<td>This increments when the device’s state changes. Some devices
constantly poll, which means the timestamp is constantly incrementing.</td>
</tr>
<tr>
<td><code>axes</code></td>
<td>This is a collection of numbers that represent the state of each analogue stick or button.</td>
</tr>
<tr>
<td><code>buttons</code></td>
<td>This collection of objects represents the state of each button.</td>
</tr>
</tbody>
</table>

### Axes

On gamepads that have analogue joysticks, the <code>axes</code> array will contain numbers that range between a minimum and maximum for each axis, usually <code>-1</code> and <code>1</code>.</p>

### Applying a Dead Zone

Because the analogue stick varies between <code>-1</code> and <code>1</code>, if the stick is not being touched and is in its center position, then, theoretically, the value should be <code>0</code>. However, this isn’t always the case on cheap controllers or gamepads that are worn or damaged or have “wiggly” thumb sticks (yes, that gamepad your friend always conveniently tries to give you).

A “dead zone” is a threshold used to prevent values below a certain amount from being used to control the game.

The following function applies a dead zone. The threshold is also subtracted from any value <em>above</em> the threshold, so that the value at the threshold is 0, rather than a sudden 0.25, for example.</p>

<pre><code class="language-javascript">var applyDeadzone = function(number, threshold){
   percentage = (Math.abs(number) - threshold) / (1 - threshold);

   if(percentage &lt; 0)
      percentage = 0;

   return percentage * (number &gt; 0 ? 1 : -1);
}</code></pre>

It can be used like this:

<pre><code class="language-javascript">var joystickX = applyDeadzone(gamepad.axes[0], 0.25);</code></pre>

This ignores values between -0.25 and +0.25 and calculates the decimal percentage, taking into consideration the given threshold. If you applied this to both the x and y axes, this would give a dead zone that looks something like this when graphed:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c823a35-5828-413b-8f98-46395538e64c/02-deepstream-console-output-opt-300x219.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9de449d-e1a2-40d2-97dd-90edd184d1a6/02-deadzone-opt-preview.png" alt="deadzone" /></a><figcaption>Dead zone. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c823a35-5828-413b-8f98-46395538e64c/02-deepstream-console-output-opt-300x219.png">View large version</a>)</figcaption></figure>

<strong>Note:</strong> Axes aren’t always analogue. Some controllers will toggle between values. For example, some D-pads toggle between a maximum, minimum and center value for each axis, such as <code>-1</code>, <code>0</code> and <code>1</code>.</p>

### Buttons

For the <code>buttons</code> array, a <code>GamepadButton</code> object is provided for each item. In most cases, the <code>value</code> property directly correlates with the <code>pressed</code> property. For example, <code>value</code> will toggle between <code>0</code> and <code>1</code> because <code>pressed</code> toggles between <code>false</code> and <code>true</code>.</p>

### Released Button

<pre class="language-none"><code class="language-none">GamepadButton
  pressed: false
  value: 0</code></pre>

### Pressed Button

<pre class="language-none"><code class="language-none">GamepadButton
  pressed: true
  value: 1</code></pre>

### Analogue Buttons

Most seventh-generation gamepads (like the Xbox 360 controller) have analogue buttons, such as the left and right triggers. In this case, <code>value</code> will range from 0 to 1, respectively. Although <code>pressed</code> works, using it isn’t recommended for non-digital buttons; instead, use a threshold against the <code>value</code>, which could be as simple as this:

<pre><code class="language-javascript">if(gamepad.buttons[7].value &gt; 0.5){
  // FIRE!
}</code></pre>

<strong>Note:</strong> Because the button is also analogue, a dead zone might need to be applied here, too.</p>

## Varying Layouts

Each controller is different, which means the length of the <code>axes</code> and <code>buttons</code> will vary; this also applies to different connection converters and/or drivers. According to the specification, browsers should map the <code>axes</code> and <code>buttons</code> as closely as possible to the suggested “<a href="https://www.w3.org/TR/gamepad/#remapping">standard gamepad</a>.” Not all gamepads will have all of these buttons; missing buttons will appear as being in an unpressed state (for buttons) or neutral state (for axes) in the object. Adding a “control settings” area to your game would be a good idea if you plan to support weird and wonderful gamepads, giving players the freedom to configure their gamepad how they want and giving users with different gamepads the opportunity to manually map their controls to your game.</p>

### Microsoft Xbox 360 Controller for Windows

The driver I use to connect to a Mac is <a href="https://github.com/d235j/360Controller/releases">available on GitHub</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72fca78c-7426-4ad9-8de4-d10559a0f4c2/03-360layout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1004938b-01db-4fa4-98a3-1b81adbe8afb/03-360layout-opt-preview.png" alt="360 Layout" /></a><figcaption>Microsoft Xbox 360 layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72fca78c-7426-4ad9-8de4-d10559a0f4c2/03-360layout-opt.png">View large version</a>)</figcaption></figure>

### NES Controller

Here is the layout of an original NES controller, using a 15-pin-to-USB converter (the layout may differ by manufacturer). This particular one uses axes for directional input, rather than buttons.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/490fc424-8fc2-4c18-b4b6-08dae5697601/04-neslayout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4b36ea9-0ad7-4e43-9060-3caffa1e4e30/04-neslayout-opt-preview.png" alt="Nes Layout" /></a><figcaption>NES layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/490fc424-8fc2-4c18-b4b6-08dae5697601/04-neslayout-opt.png">View large version</a>)</figcaption></figure>

### Saitek SP550 USB Stick and Pad

This has 12 buttons (14 on the device, with the two pad triggers having the same functionality as the joystick’s trigger and thumb button) and three axes (the third axis being the throttle slider next to the joystick). The joystick part of the controller can be detached, leaving just the pad. Doing this will disconnect the controller and reconnect it as a different controller, meaning that details about the returned <code>Gamepad</code> object will change, too: The <code>id</code> will change from <code>SP550 Stick &amp; Pad Combo (Vendor: 06a3 Product: 100a)</code> to <code>SP550 Pad (Vendor: 06a3 Product: 100b)</code>, and the layout will be different also. In “stick and pad” mode, the directional pad is in the <code>buttons</code> array (four buttons), but in “pad” mode, the directional pad is in the <code>axes</code> array (two axes).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/447f9c63-5950-45f5-8118-685e82dd01eb/05-sp550layout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e90167a-4eac-4979-afd5-621f0cc10992/05-sp550layout-opt-preview.png" alt="Saitek SP550" /></a><figcaption>Saitek SP550. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/447f9c63-5950-45f5-8118-685e82dd01eb/05-sp550layout-opt.png">View large version</a>)</figcaption></figure>

### N64 Controller

This is one of my favorite controllers, mainly because of nostalgia, not ergonomics.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11c4fcc0-fa98-4ce3-82dd-66310f63fa38/06-n64layout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0bcf81b-31e0-4f00-80df-f6dab45fe186/06-n64layout-opt-preview.png" alt="N64 Controller" /></a><figcaption>N64 controller. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11c4fcc0-fa98-4ce3-82dd-66310f63fa38/06-n64layout-opt.png">View large version</a>)</figcaption></figure>

### Nintendo Wiimote and Nunchuck

With these drivers, it was possible to use the Wiimote and Nunchuk with the Gamepad API. Different drivers will result in different layouts.

For <strong>Windows</strong>, see Julian Löhr’s “<a href="https://julianloehr.de/educational-work/hid-wiimote/">HID Wiimote: A Windows Device Driver for the Nintendo Wii Remote</a>.”

For <strong>Mac</strong>, see <a href="https://github.com/alxn1/wjoy">Wjoy</a>, a Nintendo Wiimote driver for Mac OS X.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7635ba42-2994-48a4-90c7-cbcba6ad471c/07-wiimotelayout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3db8521f-043e-44fc-8656-c33e384948dd/07-wiimotelayout-opt-preview.png" alt="Wiimote Layout" /></a><figcaption>Wiimote layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7635ba42-2994-48a4-90c7-cbcba6ad471c/07-wiimotelayout-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb7982f4-654d-4c57-95f4-d1d34418be3c/08-wiimotenunchucklayout-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a14858d-6269-4ac5-b8df-1cf664608a58/08-wiimotenunchucklayout-opt-preview.png" alt="Wiimote Nunchuck Layout" /></a><figcaption>Wiimote Nunchuck layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb7982f4-654d-4c57-95f4-d1d34418be3c/08-wiimotenunchucklayout-opt.png">View large version</a>)</figcaption></figure>

Charlie J. Walter has a <a href="https://charliejwalter.net/gamepad/demos/wiimote/car/">demo for Wiimote</a>, which works only with the Windows driver.

For this demo, I created a <strong>calibration</strong> feature, because the drivers think that the Wiimote gyroscope’s neutral position (dead center) is the value when the controller is connected. This means you have to connect the controller when the controller is on a flat surface. However, you can recalibrate the controller easily enough by reading the value of the gyroscope (a value in <code>axes</code>) when the controller is on a flat surface, and then storing that value and subtracting it from any further readings.</p>

## Events

The Gamepad API comes with two window events, <code>gamepadconnected</code> and <code>gamepaddisconnected</code>, which trigger on connection and disconnection, respectively. The user must press a button on the connected gamepad in order for a <code>gamepadconnected</code> event to be recognized. The relevant <code>Gamepad</code> object is available on both event objects with <code>e.gamepad</code>.</p>

### Connection Events

<pre><code class="language-javascript">window.addEventListener("gamepadconnected", function(e) {

  // Gamepad connected
  console.log("Gamepad connected", e.gamepad);
});</code></pre>

<pre><code class="language-javascript">window.addEventListener("gamepaddisconnected", function(e) {

  // Gamepad disconnected
  console.log("Gamepad disconnected", e.gamepad);
});</code></pre>

### State Change Events

State change events haven’t made it into the specification yet and require more discussion. However, Firefox already has three state change events: <code>gamepadbuttondown</code>, <code>gamepadbuttonup</code> and <code>gamepadaxismove</code>. These event names take on a similar naming convention to keyboard and mouse events. (Other suggestions include <code>gamepadchanged</code> and <code>gamepadaxischanged</code>.)

<pre><code class="language-javascript">window.addEventListener("gamepadbuttondown", function(e){
   // Button down
   console.log(

      "Button down",
      e.button, // Index of button in buttons array
      e.gamepad

   );
});

window.addEventListener("gamepadbuttonup", function(e){
   // Button up
   console.log(

      "Button up",
      e.button, // Index of button in buttons array
      e.gamepad

   );
});</code></pre>

<strong>Note:</strong> Currently, these events work only in Firefox.</p>

<pre><code class="language-javascript">window.addEventListener("gamepadaxismove", function(e){

   // Axis move
   console.log(

      "Axes move",
      e.axis, // Index of axis in axes array
      e.value,
      e.gamepad

   );
});</code></pre>

<strong>Note:</strong> Currently this event works only in Firefox Nightly.</p>

## Using The API In A Game

However you render your game, you can get the state of the gamepad in every game loop and apply it to a controllable entity. Below is a very simple demo where the <code>value</code> of <code>axes[0]</code> is applied to the CSS <code>left</code> property.

See the Pen [Gamepad API - DOM Element Demo](https://codepen.io/cjonasw/pen/MwRQQW/) by Charlie Walter ([@cjonasw](https://codepen.io/cjonasw)) on [CodePen](https://codepen.io).

Of course, a complex game would be very demanding, so this approach probably isn’t the best idea. Instead, you could use WebGL or Canvas or use a rendering library such as <a href="https://threejs.org/">Three.js</a> or <a href="https://www.babylonjs.com/">Babylon.js</a>. If the element doesn’t move, then your controller is probably mapped differently. This means <code>axes[0]</code> does not represent the joystick or analogue button that you are wiggling or is simply not mapped at all; try changing <code>axes[0]</code> to another element in the array. <a href="https://html5gamepad.com/">HTML5 Gamepad Tester</a> has a visual breakdown of your connected gamepads and their properties.</p>

### Control Settings and Mapping Problems

Mapping differences can be fixed with a “control settings” utility as shown in <a href="https://charliejwalter.net/gamepad/demos/main">Charlie J. Walter’s demo</a>.</p>

### How the Demo’s Control Settings Work

In the demo, the user clicks on an input box relating to their gamepad and the control they want to change or remap. The gamepad’s state is stored and constantly compared to the current state of that gamepad until an axis or button has changed more than <code>0.5</code> of its stored state. At that time, we will know which input the user wants to use for that game action (for example, “left,” “right,” “jump”) and the way they want to use it to represent that game action. The reason I say this is because the “left” and “right” actions will most likely be on the same axis, but the user will use the joystick in a slightly different way to represent a different action (for example, moving the joystick left for left and moving it right for right). This can be figured out by using the stored state of the changed button (but rounded, so that it is <code>-1</code>, <code>0</code> or <code>1</code>) to represent the game action’s minimum state, and using the new (also rounded) state to be its maximum. These states are halved for <code>buttons</code> thresholds, the result being <code>-0.5</code>, <code>0</code> or <code>0.5</code>.</p>

## How To Provide A Keyboard Fallback

The window events, <code>onkeydown</code> and <code>onkeyup</code>, make it easy to provide a keyboard fallback. We could add the code to make the player do something in these events, but because we are reading the gamepad’s <code>each</code> loop and using the <code>axes</code> and <code>buttons</code> arrays from the gamepad to then make the player do something, putting it here, too, makes sense. It also means less duplicate code.

One way we can do this is by having a <code>keys</code> collection to store the current keys down, which gets updated by <code>onkeydown</code> and <code>onkeyup</code>, respectively.

We can then do simple checks in the game loop to action the player.</p>

<pre><code class="language-javascript">// If right key down
if(keys[39]){

   // Move player right
}</code></pre>

## Wrapping Up

As with all experimental technologies, results with the Gamepad API are unstable. However, by using it (and providing feedback), you are sculpting the future of the technology.

This represents a huge opportunity for the game industry. Many games already use front-end technologies like <a href="https://nwjs.io/">NW.js</a> to create native apps; coupling them with the Gamepad API will make for games with a close-to-native experience. However, this is just one element of a rapidly growing gaming platform. Web technologies are now capable of many of the features we see in native games, including audio manipulation (via the Web Audio API), mouse movement input without screen restrictions (via the Pointer Lock API), touch gestures (via the Touch Event APIs) and many more.

In the future, I hope the Gamepad API will be able to access things like the rumble, internal speaker, microphone and other inputs.

To contribute to the future of the API, get involved in discussions and announce bugs when you find them in a given browser. I’d love to hear what you create with it!

{{< signature "ds, ml, al, jb" >}}

