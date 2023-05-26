---
title: Introduction To Animation And The iMessage App Store With Shruggie
slug: animation-imessage-app-store-shruggie
author: simon-schmid
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16bd9057-bbdd-40bf-a397-1c26b41bce79/1-introduction-to-animation-800w.png
date: 2018-09-10T14:45:42+02:00
summary: >-
  Learn about the basics of animation in After Effects by animating one of the most famous type characters and the state of the iMessage App Store in 2018 when it comes to stickers.
description: >-
  Learn about the basics of animation in After Effects by animating one of the most famous type characters and the state of the iMessage App Store in 2018 when it comes to stickers.
categories:
  - Animation
  - Case Studies
---
<p>When the App Store for iMessage in late 2016 went live, I <a href="https://itunes.apple.com/app/id1148389257/">released</a> <a href="https://www.kaomotion.com">Kaomotion</a>, a sticker app with animated kaomoji inside. Ever since the release of this app, I wanted to write up a tutorial about how a simple text character like shruggie (i.e. <code>¯&#92;_(ツ)_&#47;¯</code>) can be animated to give it life-like features: </p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b5aae8-32f0-46e9-978a-1f57ec3be847/gif-preview.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b5aae8-32f0-46e9-978a-1f57ec3be847/gif-preview.gif" width="800" height="" alt="Shruggie animated" /></a><figcaption>The Shruggie animation we’re going to make. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b5aae8-32f0-46e9-978a-1f57ec3be847/gif-preview.gif">Large preview</a>)</figcaption></figure>

<p>What you are going to read in this article is a step-by-step guide of setting up a canvas in After Effects and then going through with the animation. You’ll also read about how well the app containing more than 30 animated stickers worked and what some of the specific issues are you might be having on the App Store for iMessage:</p>

<ol>
<li><a href="#canvas-setup">Canvas Setup</a></li>
<li><a href="#working-with-a-text-layer">Working With A (Text) Layer</a></li>
<li><a href="#working-with-rulers">Working With Rulers</a></li>
<li><a href="#understanding-the-puppet-pin-tool">Understanding The Puppet Pin Tool</a></li>
<li><a href="#animation-and-timeline">Animation And Timeline</a></li>
<li><a href="#further-reading-and-tools">Further Reading And Tools</a></li>
<li><a href="#bonus-reading">Bonus Reading: Life On The App Store For iMessage</a></li>
</ol>

<p>Without further ado, let’s jump right in.</p>

{{% feature-panel %}}

## 1. Canvas Setup

<p>We’re starting with setting up a new composition (<kbd>⌘</kbd> + <kbd>N</kbd>) within After Effects with the following settings:</p>

<ul>
<li>1000px &times; 1000px;</li>
<li>a frame rate of 30 frames per second;</li>
<li>a quarter on resolution;</li>
<li>a run time of 2 seconds.</li>
</ul>

<p>This is going to be the basic canvas we’re going to work with during the animation. We’re choosing a square since that is what you have to deal with within iMessage and Apple’s sticker implementation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27b507c9-b34f-4ca6-84b4-2bd92c11af17/step1-composition.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27b507c9-b34f-4ca6-84b4-2bd92c11af17/step1-composition.gif" width="800" height="" alt="After Effects canvas set up" /></a><figcaption>After Effects canvas set up. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27b507c9-b34f-4ca6-84b4-2bd92c11af17/step1-composition.gif">Large preview</a>)</figcaption></figure>

## 2. Working With A (Text) Layer

<p>Since kaomoji are simple text-based emoticons we’re going to copy-paste a a Shruggie “<code>¯&#92;_(ツ)_&#47;¯</code>” from the first source we can find being <a href="https://twitter.com/jeremyburge">Jeremy Burge</a>’s <a href="https://emojipedia.org/shrug/">Emojipedia via Google</a>.</p>

<p>After having found it on Emojipedia we’re pasting it as a text layer into After Effects. It’s time to utilise the <strong>text tool</strong>.</p>

### The Text Tool

<p>Copy <kbd>⌘</kbd> + <kbd>T</kbd> in with <kbd>⌘</kbd> + <kbd>V</kbd>:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e91b39-5bbe-4c0e-8417-6583303819e1/step2-texttool.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e91b39-5bbe-4c0e-8417-6583303819e1/step2-texttool.gif" width="863" height="711" alt="After Effects text layer" /></a><figcaption>Using the text layer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e91b39-5bbe-4c0e-8417-6583303819e1/step2-texttool.gif">Large preview</a>)</figcaption></figure>

<p>The Shruggie inside your canvas might not look exactly the way you’ve found him on Google, or on Emojipedia for that matter, that’s because of differences in font types. We’ve chosen a font that makes Shruggie look decent and made him stretch across the canvas to prepare him for his facelift: double-click on the <em>Source Name</em> to select all characters.</p>

### The Character Menu

<p>Double click <em>Name Source</em> and then get the font type in your <em>Character</em> menu.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5ea3e3a-39d5-41c6-a747-bb347d1fb3b6/step3-charactermenu.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5ea3e3a-39d5-41c6-a747-bb347d1fb3b6/step3-charactermenu.gif" width="800" height="" alt="After Effects character menu" /></a><figcaption>The character menu. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5ea3e3a-39d5-41c6-a747-bb347d1fb3b6/step3-charactermenu.gif">Large preview</a>)</figcaption></figure>

### Scaling A Layer

<p>Select <em>Layer</em>, then <kbd>S</kbd> + <em>Scale</em> (by sliding right for example).</p>

<p>To position the layer properly, we’re scaling it up to fill the canvas by selecting the layer by pressing <kbd>S</kbd>, then <em>Scale</em> and then finally moving the scale until it fits.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef7c775f-7591-4530-b8a2-b95f972ae015/step4-scale.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ab45da7-8c37-42c5-ae29-5da8c5cb615e/step-4-800w.gif" width="800" height="" alt="After Effects scale a layer" /></a><figcaption>Scaling a layer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef7c775f-7591-4530-b8a2-b95f972ae015/step4-scale.gif">Large preview</a>)</figcaption></figure>

<p>To further explore some smaller tweaks let’s look into making our Shruggie a little more connected. For that we’re looking into some <strong>kerning and height options</strong>. To adjust the gap between Shruggie’s arm and hand, we’ll use the kerning tool (V/A) either manually in the menu or with another keyboard shortcut:</p>

### Kerning

<p>Select <kbd>Space</kbd> + <kbd>ALT</kbd> + <kbd>&larr; &rarr;</kbd>. When we’re happy with the kerning gaps, we’ll adjust the height of the arms and make it look like the arms are actually connected. To join up the slashes with the underscore we’re going to play around with increasing the height of the slash/vertical scale, moving it vertically and potentially adjusting the baseline. In our case we’ve increased the height of the slash character to 120% and then adjusted vertically:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a532204b-7ba7-493b-9460-625b4615690b/step5-kerning.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a532204b-7ba7-493b-9460-625b4615690b/step5-kerning.gif" width="800" height="" alt="After Effects text kerning" /></a><figcaption>Text kerning in action. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a532204b-7ba7-493b-9460-625b4615690b/step5-kerning.gif">Large preview</a>)</figcaption></figure>

### Moving Vertically

<p>Make selection + <kbd>ALT</kbd> + <kbd>SHIFT</kbd> + <kbd>&uarr; &darr;</kbd></p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdaf95ec-a0e2-4a53-afa2-de9556bee624/step6-verticalmovement.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdaf95ec-a0e2-4a53-afa2-de9556bee624/step6-verticalmovement.gif" width="873" height="451" alt="After Effects move selection vertically" /></a><figcaption>Move selection vertically. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdaf95ec-a0e2-4a53-afa2-de9556bee624/step6-verticalmovement.gif">Large preview</a>)</figcaption></figure>

<p>If you repeat the steps above on the other side we’ll by now have a pretty looking Shruggie, but what’s that, we don’t like how it aligns at all, do we?</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac2c597-f38e-492b-9083-1f3216364d03/step7-alignment.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac2c597-f38e-492b-9083-1f3216364d03/step7-alignment.gif" width="800" height="" alt="After Effects align" /></a><figcaption>Unaligned Shruggy, can we fix it? (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac2c597-f38e-492b-9083-1f3216364d03/step7-alignment.gif">Large preview</a>)</figcaption></figure>

<p>Let’s further align this sorry looking Shruggie.</p>

<p>That’s what <strong>rulers</strong> are for.</p>

{{% ad-panel-leaderboard %}}

## 3. Working With Rulers

<p>To conjure up rulers we’re going to use another keyboard shortcut:</p>

### Display Rulers

<p><kbd>⌘</kbd> + <kbd>R</kbd></strong></p>

<p>This gives you the ruler view, from which you can practically drag rulers as visual cues into your canvas.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f835847e-7ac9-47f6-ac37-4dc5842fe038/step8-rulers.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f835847e-7ac9-47f6-ac37-4dc5842fe038/step8-rulers.gif" width="800" height="676" alt="After Effects set up rulers" /></a><figcaption> Setting up rulers. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f835847e-7ac9-47f6-ac37-4dc5842fe038/step8-rulers.gif">Large preview</a>)</figcaption></figure>

<p>The next steps are a repetition of what we’ve done before: we’re selecting the middle part and moving it down vertically to align with Shruggie’s arms, shoulders, and hands. It looks pretty good, but let’s double-check on that first impression by <strong>zooming in</strong>!</p>

### Zoom in

<p>You can zoom in by pressing <kbd>⌘</kbd> + <kbd>+</kbd>, and also by pressing on the <kbd>,</kbd> + <kbd>.</kbd> keys. In our case, we found we need to change it to properly align Shruggie’s face with his arms, which is another repetition of the above resizing and realigning skills.</p>

<p>Guess what? We’re now ready to animate! 🎊🎉🎈🚀🚀🚀🚀</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b667f9-62fb-4e48-83de-d119293155f1/step9-zoom.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b667f9-62fb-4e48-83de-d119293155f1/step9-zoom.gif" width="800" height="" alt="After Effects zoom" /></a><figcaption>Zooming into Shruggie. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b667f9-62fb-4e48-83de-d119293155f1/step9-zoom.gif">Large preview</a>)</figcaption></figure>

## 4. Understanding The Puppet Pin Tool

<p>In order to animate our base Shruggie, we’re going to use the <strong>Puppet Pin Tool</strong>. Essentially it lets us work on any vector elements within After Effects, which includes our text assets. Let’s start:</p>

### The Puppet Pin Tool

<p>Now what we’ll want to do is put pins where we want the joints to be: hands, elbows, shoulders, and so on. Press on <kbd>⌘</kbd> + <kbd>P</kbd> to do the trick:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fcb9f0a-efae-4312-8023-bf24247f9766/step10-puppetpinning.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac26f45f-c50a-4256-a323-9c9f97bdf69b/step10-800w.gif" width="800" height="" alt="After Effects puppet pinning" /></a><figcaption>Puppet pinning. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fcb9f0a-efae-4312-8023-bf24247f9766/step10-puppetpinning.gif">Large preview</a>)</figcaption></figure>

<p>Keep adding joints until we have him fully pinned up and gotten a fully functional human torso:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee245b08-4268-4569-bebd-90c852c5de53/step11-pinnedup.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee245b08-4268-4569-bebd-90c852c5de53/step11-pinnedup.gif" width="800" height="" alt="After Effects pins" /></a><figcaption>Finalized pins view. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee245b08-4268-4569-bebd-90c852c5de53/step11-pinnedup.gif">Large preview</a>)</figcaption></figure>

<p>When you get a yellow highlight, that means that everything has been well done and After Effects recognizes the element as a vector and therefore you can place your pins. One thing that’s worth looking out for is to make sure that your pins/keyframes are at time 0 in your timeline at this stage:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d39005f4-8490-4466-a8a8-1f4a06c1958e/after-effects-timeline.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c244614e-ddba-426b-8279-b645091de54e/after-effects-timeline-800w.png" width="800" height="" alt="After Effects timeline" /></a><figcaption>After Effects timeline. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d39005f4-8490-4466-a8a8-1f4a06c1958e/after-effects-timeline.png">Large preview</a>)</figcaption></figure>

## 5. Animation And Timeline

<p>The key to doing this effectively is to start with your main poses. We’re going to start with our start and end poses in place. We can do that by <strong>copying the keyframes</strong> that have been set up by our puppet pins in the <strong>beginning to our end state</strong>. The reason for this is simple: this is the start and our default pose, that’s the pose we want to return to in order to get a coherent animation.</p>

### Set Up Start And End Point

<p>Select the layout and press <kbd>U</kbd>, then copy-paste to the end state.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c36e69f9-2c80-456c-a60a-7c885f5abadb/step12-copykeyframes.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b14dc040-d1a0-412d-8b99-418959d27b89/step12-800w.gif" width="800" height="" alt="After Effects copy keyframes" /></a><figcaption>Copying keyframes from start state and end state. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c36e69f9-2c80-456c-a60a-7c885f5abadb/step12-copykeyframes.gif">Large preview</a>)</figcaption></figure>

<p>As you can see it in in the gif above selecting the layout and pressing <kbd>U</kbd> returns every property of a layer that has keyframes as little diamonds. These little 💠 now also constitute your end state.</p>

### Setting the Middle Stage

<p>In order to have a stage that we want to animate to and from, we’ll put that right in the middle:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb24f6cf-7b5e-4332-b65e-0cf7697e4953/step13-middlestage.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb24f6cf-7b5e-4332-b65e-0cf7697e4953/step13-middlestage.gif" width="800" height="450" alt="After Effects select timeline" /></a><figcaption>Select the timeline in the middle (1 sec in our example). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb24f6cf-7b5e-4332-b65e-0cf7697e4953/step13-middlestage.gif">Large preview</a>)</figcaption></figure>

<p>Now that we’re in the middle of our animation we’re going to make changes to our default state in such a way that we want to constitute our middle state:</p>

<p>This means we’re going to raise the shoulder puppet pin, get the elbow and arms a little closer to your body and give the hand a proper “shrug” movement. This will automatically create those keyframes at that point in time, which will then animate our two default stages between each other.</p>

<p>Here’s the demonstration of the animation we get when we manually move the timeline with our cursor:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3c5c10-c7fd-407d-afa9-f92587479406/step14-shoulderanimated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3c5c10-c7fd-407d-afa9-f92587479406/step14-shoulderanimated.gif" width="877" height="" alt="After Effects time ruler" /></a><figcaption>Shoulders on the time ruler. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3c5c10-c7fd-407d-afa9-f92587479406/step14-shoulderanimated.gif">Large preview</a>)</figcaption></figure>

<p>We’re following the exact same process for the right part of Shruggie’s shoulder and then add a bit of movement to Shruggies face which gives him a distinct look smirking over his shoulders and giving us the impression of: “Meh, you know, nothing to do about that”.</p>

### Space Bar To Play

<p>Select layer + <kbd>Space</kbd>. When you hit the <kbd>Space</kbd> key you can get a first impression of our animation:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c633e-52f7-406f-b112-220574a96814/step15-playanimation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c633e-52f7-406f-b112-220574a96814/step15-playanimation.gif" width="877" height="" alt="After Effects animation test" /></a><figcaption>First animation test. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1c633e-52f7-406f-b112-220574a96814/step15-playanimation.gif">Large preview</a>)</figcaption></figure>

<p>What you’ll notice immediately is that the character seems to miss character. That is mostly due to the fact that our animation plays at the same speed for the entire two seconds. That is the hallmark of mostly dodgy animation &mdash; you’ll want it to not just evenly move between two points.</p>

<p>The easiest way to fix it up and give Shruggie a bit more realism, believability is to use a technique called ease-in and ease-out (or cushioning or a number of other ways). It’s basically speeding up the animation and then speeding it down again before reaching the end of the animation timeline.</p>

<p>It’s a cheap way of breathing some more life into our Shruggie. To do that we’re using a great little After Effects plugin called <em>Ease and wiz</em> that lets us apply some easing without much work:</p>

<p>Select all keyframes and then apply <em>Ease and wizz</em> with the options most suitable for your animation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6eac81-4ef6-4271-9cba-3619060d71e5/step16-easeandwizz.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6eac81-4ef6-4271-9cba-3619060d71e5/step16-easeandwizz.gif" width="800" height="" alt="After Effects ease and wizz" /></a><figcaption>Applying Ease and wizz and some options. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6eac81-4ef6-4271-9cba-3619060d71e5/step16-easeandwizz.gif">Large preview</a>)</figcaption></figure>

<p>In our case we’ve chosen to go with the following settings:</p>

<ul>
<li><strong>Easing:</strong> <em>Quart</em></li>
<li><strong>Type:</strong> <em>In and Out</em></li>
<li><strong>Keys:</strong> <em>All</em></li>
<li><strong>Curvaceous:</strong> <em>no</em></li>
</ul>

<p>If we now run our animation again with the space bar, you’ll notice you’ll get something very close to the animation embedded at the beginning of this post. This means that we’re done, and we can be very proud of our work.</p>

{{% ad-panel-leaderboard %}}

## 6. Further Reading About The Motion Basics

<p>The tutorial you’ve just read introduces only the very basics of animation by way of making Shruggie move. In order to progress in animation, you’ll need to dig in further into the basics of motion. Further reading on some of those basics will help you improve further.</p>

<p>Below you’ll find an article describing the basics of motion and then some that relate to motion/animation with UX and software to come back full circle on the web:</p>

<ul>
<li>“<a href="https://medium.com/ueno/dear-ueno-how-do-i-use-after-effects-to-create-motion-studies-56578782df93">Dear Ueno: How Do I Use After Effects To Create Motion Studies?</a>,” Kwok Yin Mak, Medium</li>
<li>“<a href="https://medium.com/ux-in-motion/creating-usability-with-motion-the-ux-in-motion-manifesto-a87a4584ddc">Creating Usability With Motion: The UX In Motion Manifesto</a>,” Issara Willenskomer, Medium</li>
<li>“<a href="https://medium.com/@pasql/sculpting-software-animation-7d818ddcd40a">Sculpting Software Animation</a>,” Pasquale D’Silva, Medium</li>
</ul>

## 7. Bonus Reading: Life On The App Store For iMessage

<p>The above tactics were applied to a <a href="https://www.kaomotion.com">whole bunch of kaomoji</a> for the already mentioned as stated in the introduction.</p>

<p>I’ve launched the sticker app to some early support on Product Hunt, however, the app itself failed to be picked up by Apple or any audience on the App Store at large. I’d like to point out two realities on the App Store that anyone trying to make a sticker app needs to face:</p>

<ul>
<li>Competition by big brands;</li>
<li>The wrath of users who don’t get the concept of stickers.</li>
</ul>

### Problem: Prevalence Of Brands

<p>If you want a shot at being consistently in the top 50 of the top paid iMessage stickers, then it helps to be a big brand or a notoriously known character. I’m not going to attach much meaning to this, just state it as a fact and provide the evidence below of screenshots collected in April 2018 (when I first wrote the draft on this article) on the Swiss App Store for iMessage.</p>

<p>Of the top 40 (that’s the <strong>top paid</strong> category), around 18 are likely to be well known characters turning that fact into downloads:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53c2c8bc-1f2f-4d9c-b800-b76f6e7f4d29/app-store-brands.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53c2c8bc-1f2f-4d9c-b800-b76f6e7f4d29/app-store-brands.png" sizes="100vw" caption="Top paid sticker apps. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53c2c8bc-1f2f-4d9c-b800-b76f6e7f4d29/app-store-brands.png'>Large preview</a>)" alt="iMessage Store top paid sticker apps" >}}

#### Top Paid Sticker Apps

<p>The subtitle of this section is somewhat provocatively chosen, as there is no intrinsic problem with this as these characters are uniquely suited for stickers, though it’s an issue as this is just what you’re up against. Of course, the economic reality also shows around curation:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1128e7e-00ef-42c6-9400-1d3b2ee1663e/curation-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1128e7e-00ef-42c6-9400-1d3b2ee1663e/curation-comparison.png" sizes="100vw" caption="Sticker app curation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1128e7e-00ef-42c6-9400-1d3b2ee1663e/curation-comparison.png'>Large preview</a>)" alt="iMessage Store sticker app curation" >}}

<p>The left shows a screenshot of the first batch of curated stickers (66% big brand) in April of 2018, the right shows a screenshot of late August of 2018, where I encountered the exact same setup.</p>

<p>Again, this is not to pass judgment at Apple as I think they’ve become much better at curation in the App Store in general. As a summary of this situation, I think it is fair to say that other sticker ecosystems such as LINE’s have allowed more creativity to flourish and that the sticker ecosystem on the App Store is hard to advance into successfully.</p>

<p>Users still don’t get (or do not want?) stickers and the next point is a testament to this:</p>

### Problem: Facing The Wrath Of Users

<p>The most annoying problem with the App Store for iMessage is still the fact that users do not know how to use them (i.e. stickers). That results in an abundance of one-star reviews.</p>

<p>In the case of Korea, Kaomotion got 80 one-star reviews in a matter of a few days by users complaining about the app not being there on their phone.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fef22d52-2215-405c-90ef-332790cd4bb6/dont-know-how.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fef22d52-2215-405c-90ef-332790cd4bb6/dont-know-how.png" sizes="100vw" caption="“아니 삭제하는갓두 업네요..삭제좀요 사용하는 법도 모르겟어요” translates to “I don’t know how to use it.” (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fef22d52-2215-405c-90ef-332790cd4bb6/dont-know-how.png'>Large preview</a>)" alt="App Store negative review" >}}

<p>This can then look like the next screenshot fast, and Apple doesn’t seem to care to help clean out the mess, even after trying to address the users in Korean:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88fc5a26-e20a-4add-8bba-49bc2957c362/1-star-reviews.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88fc5a26-e20a-4add-8bba-49bc2957c362/1-star-reviews.png" sizes="100vw" caption="What an abundance of 1 star reviews in Korean looks like. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88fc5a26-e20a-4add-8bba-49bc2957c362/1-star-reviews.png'>Large preview</a>)" alt="App Store 1 star reviews" >}}

<p>They’re essentially all saying the same: “The App isn’t on our phone.” Any one-star reviews are essentially also going to stay forever as no-one seems to care about what you have to say.</p>

### Solutions to the discoverability problem of stickers in the interface

<p>I’m not the first one or the only one <a href="https://medium.com/@kgellci/imessage-apps-have-a-serious-usability-issue-that-is-harming-developers-aefe036de589">to write about this problem</a>, however I’d like to offer some possible remedies below.</p>

<p>18 months after the introduction of the App Store for iMessage users still don’t know how to send and receive stickers (though I must say that Apple tried to stitch the interface up within iMessage).</p>

<p>In this regard, you can only try to fix these problems by attacking the problem head-on and giving as much information as possible to users.</p>

<ul>
<li><strong>Writing guides on the App Store page</strong><br />Use the (text) screen real estate Apple gives you to write a step to step guide about how stickers are sent.</li>
<li><strong>Writing more in-depth guides elsewhere</strong><br />Do a blog post or something similar about the same topic with screenshots, gifs, or a video (<a href="https://medium.com/@s2imon/how-to-install-use-and-uninstall-kaomotion-stickers-on-iphone-46cffa1a0079">I’ve made one here for Kaomotion</a>).</li>
<li><strong>Use a screenshot or app preview</strong><br />Finally, you may want to be explicit even on your screenshots about how your app is used. <em>Even Wonder Woman</em> seems to have been experiencing the same problem and used a screenshot to offer remedy:</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5fe91a5-7bfa-4c8b-be9a-da670e28d10c/wonder-woman-stickers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5fe91a5-7bfa-4c8b-be9a-da670e28d10c/wonder-woman-stickers.png" sizes="100vw" caption="Wonder Woman: “How to send stickers”. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5fe91a5-7bfa-4c8b-be9a-da670e28d10c/wonder-woman-stickers.png'>Large preview</a>)" alt="Wonder Woman stickers" >}}

<p>You will likely still get users complaining, this way you’ll have an easy way to describe to them what needs to be done in order to use your stickers.</p>

<p>Were I to go back to the launch of the sticker store, I probably wouldn’t go through the hardship of creating Kaomotion once again, however, I’m glad I got to write about animation basics for After Effects!</p>

<p>I hope this tutorial gave you an interesting glimpse at both After Effects and the iMessage App Store. If you’re into this, you might want to go hang out at this new animation community called <a href="https://keyframes.net/">Keyframes</a>.</p>

<p>ᕕ( ᐛ )ᕗ</p>

{{< signature "ra, yk, il" >}}