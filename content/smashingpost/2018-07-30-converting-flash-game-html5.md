---
title: 'What Do You Need To Know When Converting A Flash Game Into HTML5?'
slug: converting-flash-game-html5
author: tomasz-grajewski
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98ddca1a-0ca3-4c81-a9a8-4217e0f1cb8c/overdraw-800w.png
date: 2018-07-30T14:00:26+02:00
summary: >-
  The tips presented in this article aim to help HTML5 game developers in avoiding common mistakes when converting their Flash games to JavaScript, as well as making the whole development process run as smooth as possible. Basic knowledge of JavaScript, WebGL, and the Phaser framework is required.
description: >-
  The tips presented in this article aim to help HTML5 game developers in avoiding common mistakes when converting their Flash games to JS and making the process run as smooth as possible. 
categories:
  - JavaScript
  - HTML5
  - Flash
  - Games
---
<p>With the rise of HTML5 usage, many companies start redoing their most popular titles to get rid of outdated Flash and match their products to the latest industry standards. This change is especially visible in the Gambling/Casino & Entertainment industries and has been happening for several years now, so a decent selection of titles has already been converted.</p>

<p>Unfortunately, when browsing the Internet, you can quite often stumble upon examples of a seemingly hasty job, which results in the lover quality of the final product. That's why it's a good idea for game developers to dedicate some of their time for getting familiar with the subject of Flash to HTML5 conversion and learning which mistakes to avoid before getting down to work.</p>

<p>Among the reasons for choosing JavaScript instead of Flash, apart from the obvious technical issues, is also the fact that changing your game design from SWF to JavaScript can yield a better user experience, which in turn give it a modern look. But how to do it? Do you need a dedicated JavaScript game converter to get rid of this outdated technology? Well, Flash to HTML5 conversion can be a piece of cake &mdash; here's how to take care of it.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2015/09/principles-of-html5-game-design/">Principles Of HTML5 Game Design</a></em></p>

## How To Improve HTML5 Game Experience

<p>Converting a game to another platform is an excellent opportunity to improve it, fix its issues, and increase the audience. Below are few things that can be easily done and are worth considering:</p>

<ul>
<li><p><strong>Supporting mobile devices</strong><br />Converting from Flash to JavaScript allows reaching a broader audience (users of mobile devices); support for touchscreen controls usually needs to be implemented into the game, too. Luckily, both Android and iOS devices now also support WebGL, so 30 or 60 FPS rendering usually can be easily achieved. In many cases, 60 FPS won't cause any problems, which will only improve with time, as mobile devices become more and more performant.</p></li>
<li><strong>Improving performance</strong><br />When it comes to comparing ActionScript and JavaScript, the latter is faster than the first one. Other than that, converting a game is a good occasion to revisit algorithms used in game code. With JavaScript game development you can optimize them or completely strip unused code that’s left by original developers.</li>
<li><strong>Fixing bugs and making improvements to the gameplay</strong><br />Having new developers looking into game’s source code can help to fix known bugs or discover new and very rare ones. This would make playing the game less irritating for the players, which would make them spend more time on your site and encourage to try your other games.</li>
<li><strong>Adding web analytics</strong><br />In addition to tracking the traffic, web analytics can also be used to gather knowledge on how players behave in a game and where they get stuck during gameplay.</li>
<li><strong>Adding localization</strong><br />This would increase the  audience and is important for kids from other countries playing your game. Or maybe your game is not in English and you want to support that language?</li>
</ul>

{{% feature-panel %}}

## Why Skipping HTML And CSS For In-Game UI Will Improve Game Performance

<p>When it comes to JavaScript game development, it may be tempting to leverage HTML and CSS for in-game buttons, widgets, and other GUI elements. My advice is to be careful here. It’s counterintuitive, but actually leveraging DOM elements is less performant on complex games and this gains more significance on mobile. If you want to achieve constant 60 FPS on all platforms, then resigning from HTML and CSS may be required.</p>

<p>Non-interactive GUI elements, such as health bars, ammo bars, or score counters can be easily implemented in Phaser by using regular images (the <code>Phaser.Image</code> class), leveraging the <code>.crop</code> property for trimming and the <code>Phaser.Text</code> class for simple text labels.</p>

<p>Such interactive elements as buttons and checkboxes can be implemented by using the built-in <code>Phaser.Button</code> class. Other, more complex elements can be composed of different simple types, like groups, images, buttons and text labels.</p>

<p><strong>Note:</strong> <em>Each time you instantiate a Phaser.Text or PIXI.Text object, a new texture is created to render text onto. This additional texture breaks vertex batching, so be careful not to have too many of them</em>.</p>

## How To Ensure That Custom Fonts Have Loaded

<p>If you want to render text with a custom vector font (e.g. TTF or OTF), then you need to ensure that the font has already been loaded by the browser before rendering any text. Phaser v2 doesn’t provide a solution for this purpose, but another library can be used: <a href="https://github.com/typekit/webfontloader">Web Font Loader</a>.</p>

<p>Assuming that you have a font file and include the Web Font Loader in your page, then below is a simple example of how to load a font:</p>

<p>Make a simple CSS file that will be loaded by Web Font Loader (you don’t need to include it in your HTML):</p>

<pre><code class="language-css">@font-face {
    // This name you will use in JS
    font-family: 'Gunplay';
    // URL to the font file, can be relative or absolute
    src: url('../fonts/gunplay.ttf') format('truetype');
    font-weight: 400;
}
</code></pre>

<p>Now define a global variable named <code>WebFontConfig</code>. Something as simple as this will usually suffice:</p>

<pre><code class="language-javascript">var WebFontConfig = {
   'classes': false,
   'timeout': 0,
   'active': function() {
       // The font has successfully loaded...
   },
   'custom': {
       'families': ['Gunplay'],
       // URL to the previously mentioned CSS
       'urls': ['styles/fonts.css']
   }
};
</code></pre>

<p>It the end, remember to put your code in the ‘active’ callback shown above. And that’s it!</p>

## How To Make It Easier For Users To Save The Game

<p>To persistently store local data in ActionScript you would use the SharedObject class. In JavaScript, the simple replacement is <a href="https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage">localStorage API</a>, which allows storing strings for later retrieval, surviving page reloads.</p>

<p>Saving data is very simple:</p>

<pre><code class="language-javascript">var progress = 15;
localStorage.setItem('myGame.progress', progress);
</code></pre>

<p>Note that in the above example the <code>progress</code> variable, which is a number, will be converted to a string.</p>

<p>Loading is simple too, but remember that retrieved values will be strings or <code>null</code> if they don’t exists.</p>

<div class="break-out">

<pre><code class="language-javascript">var progress = parseInt(localStorage.getItem('myGame.progress')) || 0;
</code></pre></div>

<p>Here we’re ensuring that the return value is a number. If it doesn’t exist, then 0 will be assigned to the <code>progress</code> variable.</p>

<p>You can also store and retrieve more complex structures, for example, JSON:</p>

<div class="break-out">

<pre><code class="language-javascript">var stats = {'goals': 13, 'wins': 7, 'losses': 3, 'draws': 1};
localStorage.setItem('myGame.stats', JSON.stringify(stats));
…
var stats = JSON.parse(localStorage.getItem('myGame.stats')) || {};
</code></pre></div>

<p>There are some cases when the localStorage object won’t be available. For example, when using the <code>file://</code> protocol or when a page is loaded in a private window. You can use the try and catch statement to ensure your code will both continue working and use default values, what is shown in the example below:</p>

<div class="break-out">

<pre><code class="language-javascript">try {
    var progress = localStorage.getItem('myGame.progress');
} catch (exception) {
    // localStorage not available, use default values
}
</code></pre></div>

<p>Another thing to remember is that the stored data is saved per domain, not per URL. So if there is a risk that many games are hosted on a single domain, then it’s better to use a prefix (namespace) when saving. In the example above <code>'myGame.'</code> is such a prefix and you usually want to replace it with the name of the game.</p>

<p><strong>Note</strong>: <em>If your game is embedded in an iframe, then localStorage won’t persist on iOS. In this case, you would need to store data in the parent iframe instead</em>.</p>

{{% ad-panel-leaderboard %}}

## How To Leverage Replacing Default Fragment Shader

<p>When Phaser and PixiJS render your sprites, they use a simple internal fragment shader. It doesn’t have many features because it’s tailored for a speed. However, you can replace that shader for your purposes. For example, you can leverage it to inspect overdraw or support more features for rendering.</p>

<p>Below is an example of how to supply your own default fragment shader to Phaser v2:</p>

<div class="break-out">

<pre><code class="language-javascript">function preload() {
    this.load.shader('filename.frag', 'shaders/filename.frag');
}

function create() {
    var renderer = this.renderer;
    var batch = renderer.spriteBatch;
    batch.defaultShader = 
        new PIXI.AbstractFilter(this.cache.getShader('filename.frag'));
    batch.setContext(renderer.gl);
}
</code></pre></div>

<p><strong>Note:</strong> <em>It’s important to remember that the default shader is used for ALL sprites as well as when rendering to a texture. Also, keep in mind that using complex shaders for all in-game sprites will greatly reduce rendering performance</em>.</p>

## How To Change Tinting Method With A Default Shader

<p>Custom default shader can be used to replace default tinting method in Phaser and PixiJS.</p>

<p>Tinting in Phaser and PixiJS works by multiplying texture pixels by a given color. Multiplication always darkens colors, which obviously is not a problem; it's simply different from the Flash tinting. For one of our games, we needed to implement tinting similar to Flash and decided that a custom default shader could be used. Below is an example of such fragment shader:</p>

<div class="break-out">

<pre><code class="language-css">// Specific tint variant, similar to the Flash tinting that adds
// to the color and does not multiply. A negative of a color
// must be supplied for this shader to work properly, i.e. set
// sprite.tint to 0 to turn whole sprite to white.
precision lowp float;

varying vec2 vTextureCoord;
varying vec4 vColor;

uniform sampler2D uSampler;

void main(void) {
    vec4 f = texture2D(uSampler, vTextureCoord);
    float a = clamp(vColor.a, 0.00001, 1.0);
    gl_FragColor.rgb = f.rgb * vColor.a + clamp(1.0 - vColor.rgb/a, 0.0, 1.0) * vColor.a * f.a;
    gl_FragColor.a = f.a * vColor.a;
}
</code></pre></div>

<p>This shader lightens pixels by adding a base color to the tint one. For this to work, you need to supply negative of the color you want. Therefore, in order to get white, you need to set:</p>

<div class="break-out">

<pre><code class="language-css">sprite.tint = 0x000000;  // This colors the sprite to white
Sprite.tint = 0x00ffff;  // This gives red
</code></pre></div>

<p>The result in our game looks like this (notice how tanks flash white when hit):</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769cf763-e726-465d-b76f-f97819ff3448/additive-tint.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769cf763-e726-465d-b76f-f97819ff3448/additive-tint.gif" width=“600" height="400" alt="Example of the custom default shader in game development" /></a><figcaption>Custom default shader (tanks flashing white).</figcaption></figure>

## How To Inspect Overdraw To Detect Fill Rate Issues

<p>Replacing default shader can also be leveraged to help with debugging. Below I've explained how overdraw can be detected with such a shader.</p>

<p>Overdrawing happens when many or all pixels on the screen are rendered multiple times. For example, many objects taking the same place and being rendered one over another. How many pixels a GPU can render per second is described as fill rate. Modern desktop GPUs have excessive fill rate for usual 2D purposes, but mobile ones are a lot slower.</p>

<p>There is a simple method of finding out how many times each pixel on the screen is written by replacing the default global fragment shader in PixiJS and Phaser with this one:</p>

<pre><code class="language-css">void main(void) {
    gl_FragColor.rgb += 1.0 / 7.0;
}
</code></pre>

<p>This shader lightens pixels that are being processed. The number 7.0 indicates how many writes are needed to turn pixel white; you can tune this number to your liking. In other words, lighter pixels on screen were written several times, and white pixels were written at least 7 times.</p>

<p>This shader also helps to find both “invisible” objects that for some reason are still rendered and sprites that have excessive transparent areas around that need to be stripped (GPU still needs to process transparent pixels in your textures).</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e922ec9a-9236-43b0-bb4f-7c2ef445204d/overdraw.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e922ec9a-9236-43b0-bb4f-7c2ef445204d/overdraw.png" sizes="100vw" caption="Overdraw shader in action. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e922ec9a-9236-43b0-bb4f-7c2ef445204d/overdraw.png'>Large preview</a>)" alt="Example of the Overdraw shader in action in game development" >}}

<p>The picture on the left shows how a player sees the game, while the one on the right displays the effect of applying the overdraw shader to the same scene.</p>

## Why Physics Engines Are Your Friends

<p>A physics engine is a middleware that's responsible for simulating physics bodies (usually rigid body dynamics) and their collisions. Physics engines simulate 2D or 3D spaces, but not both. A typical physics engine will provide:</p>

<ul>
<li>object movement by setting velocities, accelerations, joints, and motors;</li>
<li>detecting collisions between various shape types;</li>
<li>calculating collision responses, i.e. how two objects should react when they collide.</li>
</ul>

<p>At Merixstudio, we’re big fans of the Box2D physics engine and used it on a few occasions. There is a <a href="https://phaser.io/shop/plugins/box2d">Phaser plugin</a> that works well for this purpose. Box2D is also used in the Unity game engine and GameMaker Studio 2.</p>

<p>While a physics engine will speed-up your development, there is a price you'll have to pay: reduced runtime performance. Detecting collisions and calculating responses is a CPU-intensive task. You may be limited to several dozen dynamic objects in a scene on mobile phones or face degraded performance, as well as reduced frame rate deep below 60 FPS.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d39e63-9c0e-4235-bf56-8b3a3e3f5c8a/physics.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d39e63-9c0e-4235-bf56-8b3a3e3f5c8a/physics.png" sizes="100vw" caption="Phaser's physics debug overlay. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d39e63-9c0e-4235-bf56-8b3a3e3f5c8a/physics.png'>Large preview</a>)" alt="Example of the difference in the scene of a game with and withour Phaser physics debug overlay displayed on top" >}}

<p>The left part of the image is a scene from a game, while the right side shows the same scene with Phaser physics debug overlay displayed on top.</p>

{{% ad-panel-leaderboard %}}

## How To Export Sounds From A <em>.fla</em> File

<p>If you have a Flash game sound effects inside of a <em>.fla</em> file, then exporting them from GUI is not possible (at least not in Adobe Animate CC 2017)  due to the lack of menu option serving this purpose. But there is another solution &mdash; a dedicated script that does just that:</p>

<div class="break-out">

<pre><code class="language-javascript">function normalizeFilename(name) {
   // Converts a camelCase name to snake_case name
   return name.replace(/([A-Z])/g, '_$1').replace(/^_/, '').toLowerCase();
}

function displayPath(path) {
   // Makes the file path more readable
   return unescape(path).replace('file:///', '').replace('|', ':');
}

fl.outputPanel.clear();

if (fl.getDocumentDOM().library.getSelectedItems().length > 0)
   // Get only selected items
   var library = fl.getDocumentDOM().library.getSelectedItems();
else
   // Get all items
   var library = fl.getDocumentDOM().library.items;

// Ask user for the export destination directory
var root = fl.browseForFolderURL('Select a folder.');
var errors = 0;

for (var i = 0; i < library.length; i++) {
   var item = library[i];
   if (item.itemType !== 'sound')
       continue;

   var path = root + '/';

   if (item.originalCompressionType === 'RAW')
       path += normalizeFilename(item.name.split('.')[0]) + '.wav';
   else
       path += normalizeFilename(item.name);

   var success = item.exportToFile(path);
   if (!success)
       errors += 1;
   fl.trace(displayPath(path) + ': ' + (success ? 'OK' : 'Error'));
}

fl.trace(errors + ' error(s)');
</code></pre></div>

<p>How to use the script to export sound files:</p>

<ol>
<li>Save the code above as a <em>.jsfl</em> file on your computer;</li>
<li>Open a <em>.fla</em> file with Adobe Animate;</li>
<li>Select ‘Commands’ &rarr; ‘Run Command’ from the top menu and select the script in the dialogue that opens;</li>
<li>Now another dialogue file pops up for selecting export destination directory.</li>
</ol>

<p>And done! You should now have WAV files in the specified directory. What’s left to do is convert them to, for example, MP3’s, OGG, or AAC.</p>

## How To Use MP3s In Flash To HTML5 Convertions

<p>The good old MP3 format is back, as some patents have expired and now every browser can decode and play MP3’s. This makes development a bit easier since finally there's no need to prepare two separate audio formats. Previously you needed, for instance, OGG and AAC files, while now MP3 will suffice.</p>

<p>Nonetheless, there are two important things you need to remember about MP3:</p>

<ul>
<li>MP3’s need to decode after loading, what can be time-consuming, especially on mobile devices. If you see a pause after all your assets have loaded, then it probably means that MP3’s being decoded;</li>
<li>gaplessly playing looped MP3’s is a little problematic. The solution is to use mp3loop, about which you can read in <a href="https://www.compuphase.com/mp3/mp3loops.htm">the article posted by Compu Phase</a>.</li>
</ul>

## So, Why Should You Convert Flash To JavaScript?

<p>As you can see, Flash to JavaScript conversion is not impossible if you know what to do. With knowledge and skill, you can stop struggling with Flash and enjoy the smooth, entertaining games created in JavaScript. Don't try to fix Flash &mdash; get rid of it before everyone is forced to do so!</p>

## Want To Learn More?

<p>In this article, I was focused mainly on Phaser v2. However, a newer version of <a href="https://github.com/photonstorm/phaser">Phaser</a> is now available, and I strongly encourage you to check it out, as it introduced a plethora of fresh, cool features, such as multiple cameras, scenes, tilemaps, or Matter.js physics engine.</p>

<p>If you are brave enough and want to create truly remarkable things in browsers, then WebGL is the right thing to learn from the ground up. It’s a lower level of abstraction than various game-building frameworks or tools but allows to achieve greater performance and quality even if you work on 2D games or demos. Among many websites which you may find useful when learning the basics of WebGL would be <a href="https://webglfundamentals.org/">WebGL Fundamentals</a> (uses interactive demos). In addition to that, to find out more about WebGL feature adoption rates, check <a href="https://webglstats.com/">WebGL Stats</a>.</p>

<p>Always remember that there's no such thing as too much knowledge &mdash; especially when it comes to game development!</p>

{{< signature "rb, ra, yk, il" >}}
