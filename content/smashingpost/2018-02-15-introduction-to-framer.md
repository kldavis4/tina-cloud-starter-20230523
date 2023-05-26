---
title: 'Learning Framer By Creating A Mobile App Prototype'
slug: introduction-to-framer
author: gregrog
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0122629-a01c-4e39-a93e-155aca49dfac/20-introduction-to-framer-800w.jpg
date: 2018-02-15T13:30:22+01:00
summary: >-
  Designing interactive prototypes is the best approach to expressing your ideas and explaining them to clients and stakeholders. Learn how to create a mobile app prototype with Framer while also learning some CoffeeScript code.
description: >-
  Designing interactive prototypes is the best approach to expressing your ideas and explaining them to clients and stakeholders. Learn how to create a mobile app prototype with Framer while also learning some CoffeeScript code.
categories:
  - UX
  - Workflow
  - Tutorials
---
<p>The time of static user interfaces is long gone. Designing interactive prototypes is the <a href="https://boagworld.com/boagworks/strategy/prototyping/">best approach</a> to expressing your ideas and explaining them to clients and stakeholders. Or, as <a href="https://designshack.net/articles/graphics/how-why-prototypes-are-mandatory-for-good-design/">Jerry Cao of UXPin puts it</a>: "Nothing brings you closer to the functionality of the final product than prototyping. It is the prototype that brings to life the <em>experience</em> behind <em>user experience</em>."</p>

<p>Prototyping is an important part of the modern <a href="https://www.smashingmagazine.com/category/ux-design/">UX</a> design process. I have tried many tools, and I think <a href="https://framer.com/">Framer Studio</a> (powered by <a href="https://github.com/koenbok/Framer">Framer Library</a>) is one of the best when it comes to making user interface prototypes. So, in the following tutorial, I would like to teach you some Framer basics.</p>

<p>What will you learn? If you know what Framer is and would like to learn more about how to use it, or if you don't know what Framer is but would like to learn a bit more about advanced prototyping techniques, I believe this is the tutorial for you! By the end of the tutorial, you should be able to create a mobile app prototype, and you will also learn some CoffeeScript code. I will guide you along the way and will provide you with files to help you getting started more easily.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f660c0f9-705a-4ef7-b299-2973d3160fb1/19-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f660c0f9-705a-4ef7-b299-2973d3160fb1/19-introduction-to-framer.gif" width="1200" height="750" alt="Readymade prototype" /></a><figcaption>This is the prototype we'll be working on. You will be able to <a href="https://framer.cloud/FHCCk">download the complete Framer file</a>, too. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f660c0f9-705a-4ef7-b299-2973d3160fb1/19-introduction-to-framer.gif">View large version</a>)</figcaption></figure>

### A Note About Framer Studio, Framer Library, Platforms And Shortcuts

<p>Before we continue, an <strong>important note</strong>: This tutorial is about <a href="https://framer.com/">Framer Studio</a>, which is a Mac-only app. Framer Studio is <a href="https://framergroup.com/posts/668244316635976.html">powered</a> by <a href="https://github.com/koenbok/Framer">Framer Library</a>, which is open-source and free. The Framer Library itself can be used on all operating systems (Mac, Windows and Linux). So far, no Windows version of Framer Studio is available; however, there is a way to make Framer Library work on Windows OS with Atom. (If you're curious about the Windows bit, read "<a href="https://medium.com/microsoft-design/how-to-run-framer-js-on-windows-94e6a06abfe4">How to Run Framer JS on Windows</a>" or "<a href="https://www.prototypingwithframer.com/framer-on-windows-with-atom/">Using Framer on Windows With Atom</a>.") Also, note that, because I am using Framer Studio on a Mac, in my tutorial I will be using the Mac notation for shortcuts.</p>

{{% feature-panel %}}

## What Is Framer?

<p>There are two main categories of prototyping tools (more on these later), but Framer is a tool that falls into a category of its own. You can use it for simple transitions and rapid prototyping, as well as for creating microinteractions and advanced animations. It gives you &mdash; the designer &mdash; the ultimate power to create interactions without any limitations imposed by a graphic user interface and predefined tools.</p>

### Learning Some Code

<p>In Framer, the <strong>code</strong> is your ultimate design superpower. Does it mean you have to learn to code? Yes. Should designers code? This topic is ages old, and there have been some good points for both "yes" and "no"; here, I would like to present you with a slightly different take on the question.</p>

<p>In a recent article, <a href="https://medium.com/sofa-blog/how-a-designer-built-and-shipped-an-ios-app-in-6-months-58258869b5fa">Shawn Hickman said</a>:</p>

<blockquote>"There’s a constant debate about whether or not designers should learn to code. While I’m happy to talk about that at length, I think it’s helpful to look at it from a different perspective. What are you trying to accomplish? In my case, I wanted to ship a product."</blockquote>

<p>And also:</p>

<blockquote>"Framer is such an amazing tool for designers to learn how to code. Being able to see the results of your code live helped to teach me what was actually happening. Framer taught me basic things like variables, for-loops and functions. Nothing fancy, but totally necessary."</blockquote>

<p>This brings me to my next important point. In my opinion, Framer is one of the most designer-friendly approaches to coding out there. And while prototypes are never made with production-ready code, programmers will still benefit and be able to use some information from your code. Finally, you will also get a better understanding of how everything works under the hood and will build some foundation for further development of your skills.</p>

### What Is CoffeeScript?

<p>The language used in Framer is <a href="https://coffeescript.org/">CoffeeScript</a>. Great news for beginners: It's a simplified version of JavaScript, and so the learning curve is not too steep.</p>

<p>According to the <a href="https://coffeescript.org/">official website</a>:</p>

<blockquote>CoffeeScript is a language that compiles into JavaScript. It is an attempt to expose the good parts of JavaScript in a simple way.</blockquote>

<p>There is one more great advantage to using CoffeeScript: It's essentially a web technology, so everything you create in Framer runs as JavaScript later on! To follow along in this tutorial, you'll have to know just a tiny bit of programming.</p>

### Useful Resources

<p>Because we'll be writing some CoffeeScript, if you need any help getting started, I recommend you check out the following resources first:</p>

<ul>
<li>"<a href="https://framer.com/getstarted/guides/code/">Code</a>," Framer<br />Framer's programming guide.</li>
<li>"<a href="https://learnux.io/course/framer/intro-to-coffeescript/">Framer Course</a>," Greg Rog<br />My video tutorial about CoffeeScript.</li>
<li>"<a href="https://www.sitepoint.com/an-introduction-to-coffeescript/">An Introduction to CoffeeScript</a>," Jeffrey Biles, SitePoint</li>
<li>"<a href="https://tutorials.jumpstartlab.com/topics/javascript/coffeescript.html">Brief Introduction to CoffeeScript</a>," JumpstartLab</li>
<li>"<a href="https://designcode.io/framer-intro">Intro to Framer</a>," Meng To<br />A <a href="https://twitter.com/framer/status/942061860576219136">highly recommended resource</a> for learning a few key basic things about Framer.</li>
</ul>

### Note On Framer Versions

<p>The tutorial runs (and was tested) on Framer <strong>version 111</strong>. If you haven't yet updated to 111, I strongly recommend you <a href="https://builds.framerjs.com/">download</a> it and update. As for future updates to Framer, it's likely that a future version of Framer will introduce more new features and could have an impact on the code of this tutorial.</p>

## Why Is Prototyping Important?

<p>Compare these approaches to presenting the same idea. You could use a wireframe, like this:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd6b7269-a33a-4e1c-847d-66ddbc444e1a/20-introduction-to-framer.jpg" sizes="100vw" caption="A set of static wireframes (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd6b7269-a33a-4e1c-847d-66ddbc444e1a/20-introduction-to-framer.jpg'>Large preview</a>)" alt="Messy wireframe" >}}

<p>Or the same idea could be presented with a simple yet powerful prototype:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f1a2a4-9f7d-41ee-a392-29e67dcbc54a/21-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f1a2a4-9f7d-41ee-a392-29e67dcbc54a/21-introduction-to-framer.gif" width="1200" height="600" alt="Working prototype" /></a><figcaption>A working prototype by Google's iOS team. Framer can help you make this type of live prototype. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f1a2a4-9f7d-41ee-a392-29e67dcbc54a/21-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>Imagine you're presenting this idea to a group of people. What do you think: Which one would perform better? Even if the wireframe contained more relevant information, it would have a lesser visual impact. And people tend not to read wireframe documentation carefully.</p>

<p>Explaining the idea with an interactive prototype would give them a better understanding of your vision. Sometimes, even a low-fidelity prototype speaks a thousand words. (The same idea was <a href="https://static.notion-static.com/bfe9dcdb-aee7-4d45-8011-872c38eabf40/People%20often%20have%20trouble%20imagining%20what%20%E2%80%98better%E2%80%99%20looks%20like.%20A%20prototype%20allows%20them%20to%20see%20it.%20It%20can%20sell%20the%20potential%20much%20better%20than%20any%20number%20of%20documents%20or%20presentations.">shared by Paul Boag</a>: "People often have trouble imagining what <em>better</em> looks like. A prototype allows them to see it. It can sell the potential much better than any number of documents or presentations.")</p>

<blockquote>If a picture is worth 1000 words, a prototype is worth 1000 meetings.<br /><br />&mdash; <a href="https://twitter.com/JessLHutton/status/940615321559244802">Daniel Burka</a>, <a href="https://twitter.com/search?q=%23aeadenver&amp;src=tyah">#aeadenver 2017</a></blockquote>

<p>It happens often that you have to convince people whose knowledge of the concept being presented is limited. On the other hand, having a working prototype before the actual app is developed can bring you really meaningful insight from the user testing stage. That's why I believe prototyping is so important and appealing.</p>

<p>In general, you can divide prototypes into two main categories. First is <strong>rapid prototyping</strong>, where you link static screens with hotspots in order to create simple transitions. This can be accomplished with tools such as <a href="https://marvelapp.com/">Marvel</a>, <a href="https://www.adobe.com/products/xd.html">Adobe XD</a> and <a href="https://figma.com/">Figma</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84ff113a-8ada-4693-8ac5-85ae375c0cc5/22-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84ff113a-8ada-4693-8ac5-85ae375c0cc5/22-introduction-to-framer.gif" width="1200" height="600" alt="Rapid Prototyping" /></a><figcaption>Rapid prototyping in Adobe XD (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84ff113a-8ada-4693-8ac5-85ae375c0cc5/22-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>The second category is <strong>detailed prototypes with microinteractions</strong>, such as animations focused on one task (for example, setting an alarm, picking an action, etc.). You can create this type of prototype with tools such as <a href="https://principleformac.com/">Principle</a>, <a href="https://www.flinto.com/">Flinto</a> and <a href="https://origami.design/">Origami</a>. Refining the prototype with animations gives you an opportunity to create a more engaging prototyping experience.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38eef0f8-a344-45b4-ba72-22bf2b899c23/23-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38eef0f8-a344-45b4-ba72-22bf2b899c23/23-introduction-to-framer.gif" width="800" height="600" alt="Microinteraction" /></a><figcaption>Microinteraction by Johny vino (<a href='https://dribbble.com/shots/3216088-Share-round-shape-transformation-Micro-interaction'>View original on Dribbble</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38eef0f8-a344-45b4-ba72-22bf2b899c23/23-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>Remember I said that Framer is a tool that falls into a category of its own? This is because you can use it for both rapid prototyping, as well as for creating microinteractions and quite advanced animations. Let's see how!</p>

## Your First Design Made With Framer

<p>Let's start with Framer's user interface.</p>

<p>Framer has two well integrated <strong>views</strong>: code and design. You create your layouts and imagery in the design view, and then add all needed interactivity in the code view. In the code view, you will then be able to add animations and microinteractions. Framer is not supposed to replace the design tool of your choice (although, with the recent December update, Framer is also starting to aim at the <a href="https://blog.framer.com/framer-is-now-the-best-tool-for-screen-design-heres-why-ebd9c29b3138">screen design tools</a> market, it seems; it posted an <a href="https://blog.framer.com/the-10-framer-design-features-you-may-have-missed-b39314716954">overview of the new design features</a>), but for quick prototypes, the design view feels just fine.</p>

<p>Later on, with more sophisticated designs, you'll also be able to import files from <a href="https://www.smashingmagazine.com/sketch-handbook/">Sketch</a> or <a href="https://blog.usejournal.com/30-days-deep-into-figma-full-review-7fffbb237c27">Figma</a>. But first, let's jump right into the design view and create a simple layout using some basic design tools.</p>

## Working In Design View

<p>When you first open Framer Studio, it will open in design view. You'll discover that most shortcuts you know from other design tools (such as Sketch) work here as well. Press <kbd>A</kbd> (or <kbd>F</kbd>) to switch to the Frame tool, and select a predefined iPhone 8 preset from the properties panel on the right.</p>

<p><strong>Note:</strong> In the latest Framer <a href="https://framer.com/updates/">update</a>, artboards were renamed to "<a href="https://blog.framer.com/the-10-framer-design-features-you-may-have-missed-b39314716954">frames</a>," and the whole concept has changed. What are frames exactly? Frames are smart layout containers that can be used as both screens and interface elements. Frames can also be used like slices to quickly export icons at specific sizes. If you know a bit of HTML, you could think of frames as <code>div</code> elements, and you can also nest frames inside of each other, to define layout elements such as navigation bars, tab bars, cards, buttons, etc. Later in the tutorial, sometimes I will refer to frames as "screens" (to give you a general idea that this is a separate screen of our app) &mdash; but, technically, screens are just frames.</p>

<p>You can read more about frames in the "<a href="https://help.framer.com/learning-framer/frames-vs-shapes">Frames vs Shapes</a>" help page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf19631f-e5c3-4275-859c-9d96b502f049/1-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf19631f-e5c3-4275-859c-9d96b502f049/1-introduction-to-framer.gif" width="1200" height="750" alt="Working with frames" /></a><figcaption>Working with frames in Framer (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf19631f-e5c3-4275-859c-9d96b502f049/1-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

### A Note On Units

<p>In Framer, we measure things in units called <strong>points</strong>. Each point can represent a different number of pixels, depending on the pixel density of the physical device you will be testing on. Because anything you design in Framer is created as a vector, there's little to worry about. Also, it's best to use vector SVG files, which are supported by Framer; if you have to import PNG or JPG files, make sure they are in a high enough resolution.</p>

<p>I've prepared the Smashing Magazine logo this way. To import it into Framer, I just drag and drop it on the canvas.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c41da6-e7fe-4262-bb60-9aa23b0d5d28/2-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c41da6-e7fe-4262-bb60-9aa23b0d5d28/2-introduction-to-framer.gif" width="1200" height="750" alt="Import images" /></a><figcaption>Import an image into Framer; Smart Guides will help you positioning it. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c41da6-e7fe-4262-bb60-9aa23b0d5d28/2-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>The last element in this frame is a simple button, made with the help of another nested frame (press <kbd>F</kbd> or <kbd>A</kbd>), with a text frame in it. Press <kbd>T</kbd> for the Text tool, and draw a text field from left to right, aligning the text to the center of the field in the properties panel, and adding some text.</p>

<p><strong>Useful tip</strong>: Text is automatically applied as a sublayer to the frame object that you have created. To access it directly on the canvas, hold <kbd>Command</kbd> while clicking on it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18debe7e-e658-41f8-baa1-08831f7b2cff/3-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18debe7e-e658-41f8-baa1-08831f7b2cff/3-introduction-to-framer.gif" width="1200" height="750" alt="Simple drawing" /></a><figcaption>Add text to the button (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18debe7e-e658-41f8-baa1-08831f7b2cff/3-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>Let's design the second screen (frame). We'll be using a generic header and footer, which will be automatically applied to our prototype (this means you will skip the height of both the header and footer while working on the design).</p>

<p>The main element on this screen will be the list of six buttons, 115 points in height each. In total, our frames should be <code>6 × 115 = 690 points</code> in height. Because it's slightly taller than the device itself, it will later scroll automatically in the preview. I used a hamburger icon from the icons panel:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a05638e-dbdc-48d9-8e32-12a7c5123015/4-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a05638e-dbdc-48d9-8e32-12a7c5123015/4-introduction-to-framer.gif" width="1200" height="750" alt="Icons selection" /></a><figcaption>Selecting an icon (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a05638e-dbdc-48d9-8e32-12a7c5123015/4-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>I've also added some text fields, as well as gradients as a fill. Here's how it looks:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5a33a28-a70a-433c-8dc1-0024e6bacc07/5-introduction-to-framer.jpg" sizes="100vw" caption="Changing the properties (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5a33a28-a70a-433c-8dc1-0024e6bacc07/5-introduction-to-framer.jpg'>Large preview</a>)" alt="Changing properties" >}}

<p>Let's select all of the buttons and press <kbd>Command</kbd> + <kbd>Return</kbd> to merge them into a new frame &mdash; a new container for these items (which I named "items"). Now, add top and bottom frames (which will be used for the header and footer), and then put them on top of the list items.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f1998c5-fae1-4760-a7df-9ee79cea9035/6-introduction-to-framer.jpg" sizes="100vw" caption="The header and footer (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f1998c5-fae1-4760-a7df-9ee79cea9035/6-introduction-to-framer.jpg'>Large preview</a>)" alt="header and footer" >}}

<p>For the other frames, use similar simple shapes and tools to create the structure that you see below.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00eca82e-278d-4094-b224-93583c0df1ac/7-introduction-to-framer.jpg" sizes="100vw" caption="The structure of the prototype (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00eca82e-278d-4094-b224-93583c0df1ac/7-introduction-to-framer.jpg'>Large preview</a>)" alt="Readymade structure" >}}

<p>I won't go into the details of each design element because of the basic nature of the tools you'll be using. However, if you want to start with a ready-to-use Framer file, <a href="https://framer.cloud/AJBfb">you can download one</a>.</p>

<p>Before we continue, there are some things I'd like you to check out:</p>

<ul><li>The third screen with the menu has to be the same height as the tallest one (you can easily duplicate the previous frame by pressing <kbd>Command</kbd> + <kbd>D</kbd>).</li>

<li>The naming convention for elements in the layers panel is critical. Please, keep it <strong>as is</strong> in my design file, or pay attention to how I bring their names.</li></ul>

## Transition From Design To Code

<p>To put things into motion, you'll need to access the code view. You can switch between views by pressing <kbd>Command</kbd> + <kbd>1</kbd> and <kbd>Command</kbd> + <kbd>2</kbd>. Before you start coding interactions, you’ll have to enable frames from the design view to be available in the code view (they are not enabled by default). To enable a frame for working in code view, click on the target icon next to its name in the layers panel.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85beca55-c86a-4de3-90c0-35bb20e712b7/8-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85beca55-c86a-4de3-90c0-35bb20e712b7/8-introduction-to-framer.gif" width="1200" height="750" alt="Click on the target icon" /></a><figcaption>Click on the target icon (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85beca55-c86a-4de3-90c0-35bb20e712b7/8-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>Now you can target this frame in the code simply by using its name.</p>

<p><strong>Useful tip:</strong> Keep the naming convention for elements in the layers panel simple; try to avoid spaces and special signs; don't start a name with a digit. Using camelCase or underscores (<code>_</code>) is a good idea. But if you use dashes (<code>-</code>), you'll have to replace them with underscores (<code>_</code>) in the code.</p>

<p>First, make sure that all of the frames have been enabled for targeting them in the code view with the target icon (to see the full frames list, click anywhere on the blank canvas outside of any frame). Also, enable all of the frames inside the first frame for code view. Now, press <kbd>Command</kbd> + <kbd>2</kbd>, and let's run some code!</p>

<p><strong>Important update:</strong> As of the 20 December 2017 update of Framer (<strong>version 108</strong>), you could target in code only frames and text objects; but in a more recent update (<strong>version 109</strong>, released on 23 January 2018), the Framer team added the option to also target shapes and paths. While my tutorial uses only frames and text objects, it's also good to know that shapes and paths can now be targeted in code as well. You will also note that (as mentioned already) the Artboard tool was replaced with the Frame tool, so the tools sidebar might look slightly different than in the screenshots; this is because the bulk of the article was prepared before the 20 December 2017 update of Framer.</p>

## Adding Interactivity In Framer

<p>It's not my intention to teach you CoffeeScript in this article, but I'll try my best to explain the code I used in this example. Hopefully, you'll be able to understand it even without prior CoffeeScript experience. That being said, if you're new to CoffeeScript or JavaScript, I strongly suggest you go through the <a href="https://framer.com/getstarted/guides/code/">help guide</a> first.</p>

<p>Now, let's create our first animations. We’ll explore simple transitions by creating an intro animation for the first screen. What we set up in the design view is how our app is supposed to look after elements are animated. For our first screen, we want to animate the logo's <code>scale</code> and <code>rotation</code> properties. First, we set the scale property to 0 (which will make the logo invisible), and then we set its rotation to <code>-360</code>:</p>

<pre><code class="language-javascript">logo.scale = 0
logo.rotation = -360
</code>
</pre>

<p>After that, we'll animate them to their original values. Here's the block of code you can use:</p>

<pre><code class="language-javascript">logo.animate
    properties:
        scale: 1
        rotation: 0

</code>
</pre>

<p>Keep in mind the <strong>indentation</strong>. Properties that animate should be indented on new lines, and we're using the <code>animate</code> method to set them in motion. Now, you should be able to see your first animation working! You can tweak it a bit by creating more natural motion. We'll do this thanks to easing &mdash; a concept that enables us to change motion so that it feels more life-like. Let's add one more line at the bottom:</p>

<pre><code class="language-javascript">logo.animate
    properties:
        scale: 1
        rotation: 0
    curve: "spring(100,15)"
</code>
</pre>

<p>Again, please note the indentation. Experiment with the values in the parentheses to get different results. You can read more on easing in <a href="https://framer.com/getstarted/guides/code/#animate">Framer's documentation</a>.</p>

<p>The animation should now look like this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d347675-61cd-4e97-b446-f280429fe6f7/9-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d347675-61cd-4e97-b446-f280429fe6f7/9-introduction-to-framer.gif" width="1200" height="750" alt="Logo animation" /></a><figcaption>Logo animation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d347675-61cd-4e97-b446-f280429fe6f7/9-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>Let's set a few more starting properties:</p>

<pre><code class="language-javascript">bg.backgroundColor = "black"
button.scale = 2
button.y = button.y + 200
</code>
</pre>

<p>On the last line, we set the position of the button so that it is below the canvas &mdash; we first check the current position with <code>button.y</code>, and then add <code>200</code> more points on the vertical axis to move it down. The next step is to create some animation; let's do it for the background first:</p>

<pre><code class="language-javascript">bg.animate
    backgroundColor: "#FF7744"
</code></pre>

<p>And now, we want to wait until the logo animation has finished and then run the animation of the button. One approach would be to delay the animation, like this:</p>

<pre><code class="language-javascript">button.animate
    properties:
        scale: 1
        y: button.y - 200
    delay: .5
</code></pre>

<p>This delays it by half a second. A much nicer solution would be to wait for the logo animation to finish and then run the code. That piece of code introduces Framer events (which we'll explore a bit more later in this article). It looks like this:</p>

<pre><code class="language-javascript">logo.onAnimationEnd -&gt;
    button.animate
        scale: 1
        y: button.y - 200
</code></pre>

<p>As you can see, you can even skip the <code>properties:</code> line when not using easing; but if you want to add some cool easing, it has to be there. Let's finish with something like this:</p>

<pre><code class="language-javascript">logo.onAnimationEnd -&gt;
    button.animate
        properties:
            scale: 1
            y: button.y - 200
        curve: "spring"
</code></pre>

<p>So, this is one way to create animations in Framer; others would be to use animation objects or <a href="https://framer.com/getstarted/guides/code/#states">states</a>. One additional tip would be to explore properties by clicking on the little icon next to the line number, where you can tweak different values.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ee34ec2-a557-4efb-9307-338ddae2f146/10-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ee34ec2-a557-4efb-9307-338ddae2f146/10-introduction-to-framer.gif" width="1200" height="750" alt="Animation properties" /></a><figcaption>Animation properties (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ee34ec2-a557-4efb-9307-338ddae2f146/10-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>OK, the animation now looks like this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8adeeed6-2b58-45e7-94f5-973e791d450a/11-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8adeeed6-2b58-45e7-94f5-973e791d450a/11-introduction-to-framer.gif" width="1200" height="750" alt="Logo animation" /></a><figcaption>Logo animation, new and improved. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8adeeed6-2b58-45e7-94f5-973e791d450a/11-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

## Scripting The Interactions

<p>In Framer, there are plenty of ready-made components and <strong>snippets</strong> &mdash; pieces of code that you can use in your prototypes. One of them is the flow component, which enables the auto-transition of screens, as well as enables some extra features, such as defining the header and footer that will appear on each screen. Let's start by creating a flow component:</p>

<pre><code class="language-javascript">flow = new FlowComponent
flow.showNext(home)
</code></pre>

<p>The first line is like a declaration of a variable. But the value here actually creates a new <code>FlowComponent</code> object. Now, we can use this custom name, <code>flow</code>, to access the flow component at any time. The second line uses one of the methods built into the flow component &mdash; <code>showNext</code>, which, as the name suggests, displays the screen that we want to see next. In this case, it will show us the first screen of our prototype. We pass the name of the first frame as a parameter. That's all it takes to wrap it into the flow component and display the first screen.</p>

<p>Next, we define the header and footer. If you haven't enabled them in the design view, you’ll have to go back with <kbd>Command</kbd> + <kbd>1</kbd> and, in the design view, click on the target icon for the "top-bar" and "bottom-bar" frames. As you see, you can also group content together in the design view <kbd>Command</kbd> + <kbd>Return</kbd>) and, afterward, enable the new frame to be accessible in the code. Back in the code view, you can now use the following lines:</p>

<pre><code class="language-javascript">flow.header = top_bar
flow.footer = bottom_bar
</code></pre>

<p>You've probably noticed that when you call <code>flow</code> and put the dot afterward, Framer displays a list of common methods and properties that you can use. It's worth going through the list and checking out suggestions for methods and properties. And, if you want to learn more, a small icon leads to the documentation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc2fc5cc-5fe8-4be1-8255-b67246d797a9/12-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc2fc5cc-5fe8-4be1-8255-b67246d797a9/12-introduction-to-framer.gif" width="1200" height="750" alt="Documentation shortcut" /></a><figcaption>A list of common methods and properties that you can use and the documentation shortcut icon. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc2fc5cc-5fe8-4be1-8255-b67246d797a9/12-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>In object-oriented programming, this concept is very important. Take a car object as an example; the properties would be things like color, make, horsepower and so on. The methods would be ready-made functions that you can run when appropriate (for example, <code>startTheEngine()</code>). You can recognize the method by the parentheses, and sometimes you might want to pass some parameters to this particular function (for example, <code>startTheEngine(gear1)</code>). We've already used the <code>showNext()</code> method in this context; now we're using the <code>header</code> and <code>footer</code> properties and setting them on the appropriate layers.</p>

<p>Another technique you will use often in Framer is hiding and revealing layers. For example, as a design decision, we want to hide the header and footer on the first screen. You can do this with the following lines of code:</p>

<pre><code class="language-javascript">flow.header.visible = false
flow.footer.visible = false
</code></pre>

<p>Here, we are using the <code>visible</code> property in the header and footer of the flow component. CoffeeScript is meant to be as intuitive and close to plain English as possible; so, instead of <code>false</code>, you could even say <code>no</code> to hide it and <code>yes</code> to reveal it (instead of <code>true</code>).</p>

<p><strong>Tip:</strong> Try selecting any lines of code and press <kbd>Command</kbd> + <kbd>/</kbd> to comment them out so that they're not executed.</p>

<p>It's time to use the power of the flow component to travel to the next screen of our app. First, make sure that the next frame is available in the code view as well as the <code>button_get_started</code> frame that we will use to get to this next screen. The following code does just this:</p>

<pre><code class="language-javascript">button_get_started.onTap -&gt;
    flow.showNext(list)
    flow.header.visible = true
    flow.footer.visible = true
</code></pre>

<p>What we're doing here is another convention: We can respond to user input and interact with so-called <strong>events</strong>. There are different events to choose from, such as tapping, clicking, force tapping, hovering and much more. You can catch such events and execute some code as the user is performing the action. We're using the <code>onTap</code> event, and in response to that (<code>-&gt;</code>), we're executing the code that is indented below. In the flow component, we show the list frame, as well as reveal the header and footer.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b51803f-d794-4c58-bc67-65c654c87cc9/13-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b51803f-d794-4c58-bc67-65c654c87cc9/13-introduction-to-framer.gif" width="1200" height="750" alt="Second page transition" /></a><figcaption>Second screen transition (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b51803f-d794-4c58-bc67-65c654c87cc9/13-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>Now that you know about both events and animations, you can tweak the home screen even more and experiment with the events. For example, you can add a tap animation to the button:</p>

<pre><code class="language-javascript">button.onTouchStart -&gt;
    this.animate
        properties:
            scale: 1.1
            backgroundColor: "#f1f1f1"
        curve: "spring"
</code></pre>

<p>Here, I used the <code>onTouchStart</code> event in order to see the animation before going to the next screen, which is triggered when the user releases their finger (the <code>onTap</code> or <code>onClick</code> event).</p>

<p>You have already discovered some potential of the flow component, such as the automatic transition to this next screen. But the magic has just begun! As you can see, the list automatically scrolls. The problem is that we can see black (the flow component's background) when we reach the top or bottom and scroll even more. You can change the color simply by setting this (the gray color we have in the header and footer):</p>

<pre><code class="language-javascript">flow.backgroundColor = "#555555"
</code></pre>

<p>Now it's time to show the menu. Make sure you’ve enabled <code>menu_button</code> for the code, and execute these next lines of code:</p>

<pre><code class="language-javascript">menu_button.onTap -&gt;
    flow.showOverlayLeft(menu)
</code></pre>

<p class="c-pre-sidenote--left">We're using the <code>showOverlayLeft()</code> method and passing the name of the frame as a parameter. As a result, the screen animates from the left side, and the menu is hidden with another tap and is even hidden with a tap outside the menu itself. All of this with a single line of code!</p><p class="c-sidenote c-sidenote--right">Apple does not seem to encourage the use of <a href="https://blog.manbolo.com/2014/06/30/apple-on-hamburger-menus">hamburger menus in iOS apps</a>, so I've used the menu merely as an example of what Framer can do quickly and efficiently. If you create a prototype for a real iOS app, consider following closely <a href="https://developer.apple.com/ios/human-interface-guidelines/overview/themes/">Apple's interface guidelines</a>.</p> ￼

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14ed2189-0613-483a-be55-8e9f7e49338a/14-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14ed2189-0613-483a-be55-8e9f7e49338a/14-introduction-to-framer.gif" width="1200" height="750" alt="Menu animation" /></a><figcaption>Menu animation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14ed2189-0613-483a-be55-8e9f7e49338a/14-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>You can access this cool presentation mode by clicking on the full-screen icon in the preview window. It is also possible to test your prototype directly on a mobile device! You can use the live preview with the free app, available for both <a href="https://itunes.apple.com/us/app/framer-preview/id1124920547?mt=8">iOS</a> and <a href="https://play.google.com/store/apps/details?id=com.framerjs.android&amp;hl=en">Android</a>. Testing your prototypes on real devices is essential because it gives you the most accurate preview of how the design will look and feel.</p>

<p>If you're a beginner, you probably understand most of the tutorial so far but might not think you can do it on your own yet. So, here's a small assignment.</p>

<p>As you saw, I closed the menu simply by clicking in the blank area on the right side (demonstrating the magic of the flow component). Now, take a look at the flow component's documentation, and try to figure out how to accomplish the following task: We want to make the “x” button close the menu <em>and</em> show the previous screen. Before going any further, try to discover what is the right way to do this, and write the lines of code on your own.</p>

<p>If it's still not clear at this point, don't worry! By the end of the tutorial, it will have become easier to understand. The CoffeeScript we'll use here (after enabling the <code>close_button</code> element for the code view) is this:</p>

<pre><code class="language-javascript">close_button.onTap -&gt;
    flow.showPrevious()
</code></pre>

<p>Here, <code>showPrevious()</code> is just a method of flow component that will let you go to the last screen. Now, try to write some code on your own again. You’ll need to link <code>article_list</code> and <code>arrow_button</code> with the code and make <code>article_list</code> show the appropriate screen, as well as make <code>arrow_button</code> go to the previous one. Also, we’ll need to hide and show the header and footer where appropriate.</p>

<p>Congratulations if you managed to do it! Here's the code that I used:</p>

<pre><code class="language-javascript">article_list.onTap -&gt;
    flow.showNext(detail)
    flow.header.visible = false
    flow.footer.visible = false

arrow_button.onTap -&gt;
    flow.showPrevious()
    flow.header.visible = true
    flow.footer.visible = true
</code></pre>

## Fetching Data For Our Prototype

<p class="c-pre-sidenote--left">Now that we have the backbone of our prototype, it's time to explore some more advanced features of Framer. This is going to be fun! We'll actually use the real data from our app. It will look so much more meaningful than generating some dummy filler content. And it might sound a bit frightening, too, but fear not &mdash; this is the next thing in your skill set. If you find this part of the article difficult, just stick with the static data. This is intended to show some more advanced users that they can deal with real data in Framer.</p><p class="c-sidenote c-sidenote--right">This approach is similar to the one used when working with variables and data sets in Adobe Photoshop. If you’re curious, read more: "<a href="https://helpx.adobe.com/photoshop/using/creating-data-driven-graphics.html">Create Data-Driven Graphics in Photoshop</a>."</p> ￼

<p>In fact, first I'd like to introduce you to an easier solution, but still one that will give you control over your text from the code! Go back to the design view and put the text in the fields in braces, like this: <code>{item_1} {item_2} ... </code></p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c69e441b-de01-4b07-a04e-e1b97a52a0c4/introduction-to-framer-ad5.jpg" sizes="100vw" caption="Dynamic text in design view. " alt="Dynamic text in design" >}}

<p>Make sure the text fields are enabled for the code view, and in the code view you can put all of your predefined strings in an <strong>array</strong>. (I recommend reading "<a href="https://medium.com/the-school-of-do/framer-cheat-sheet-loops-arrays-f5c3aaa802e9">Framer Cheat Sheet: Loops &amp; Arrays</a>" if you want to learn more about arrays.)</p>

<p>In short, an array acts as a variable that can contain more than one item:</p>

<pre><code class="language-javascript">categories = ["Graphic Design", "Mobile Apps", "Web Design", "User Experience", "Front-End Dev", "User Research"]
</code></pre>

<p>Now that we have our array, let's try to display the data. To do this, we will first use the <code>print</code> command, which outputs the result to the console. You can test it out right away:</p>

<pre><code class="language-javascript">print "Hello World"
</code></pre>

<p>The console can be refreshed by pressing <kbd>Command</kbd> + <kbd>R</kbd>. Accessing the data is as simple as this:</p>

<pre><code class="language-javascript">print categories
</code></pre>

<p>This line of code will display all of the data in the <code>categories</code> array. With arrays, you can easily access individual items that are indexed in the array by putting the number in brackets, like this:</p>

<pre><code class="language-javascript">print categories[2]
</code></pre>

<p>This will return the third item in the collection, because we start counting from zero. Now let's use Framer's TextLayer template functionality to update the first two strings:</p>

<pre><code class="language-javascript">item1_txt.template = categories[0]
item2_txt.template = categories[1]
</code></pre>

<p>You can fill in the rest of the fields! This easy example lets us manage the text fields directly from code so that we can change the text dynamically!</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad562feb-06f5-4117-932e-2130338ad3f5/introduction-to-framer-ad4.jpg" sizes="100vw" caption="Dynamic text from code" alt="Dynamic text from code" >}}

## Where To Go From Here

<p>Well done! At this point, you should be able to find your way around Framer and create some simple prototypes.</p>

<p><strong>Note:</strong> I encourage you to try out my own <a href="https://learnux.io/course/framer/">video course on Framer</a> &mdash; you can watch some lessons for free. Also, the <a href="https://framerbook.com/">Framer book</a> by <a href="https://twitter.com/cptv8">Tes Mat</a> is an excellent resource for learning and understanding Framer and CoffeeScript. The book is not free, but you can read a <a href="https://framerbook.com/#sr-sectionsix">sample chapter</a> from it (before deciding whether you'd like to buy it).</p>

<p>I hope you’ve found this part of the article useful. Up to this point, we have been following simple ways to make our prototype work. But Framer is much more than that! This is why I’ve written an additional bonus section with more advanced techniques. If you're up for the challenge, then proceed to the next part: JSON!</p>

## Accessing The Data From JSON (Bonus Tutorial Section)

<p>As a powerful alternative to the previous solution, you can use an external API and connect to it directly. While it's a bit of overkill for this particular example, more advanced users will benefit from the idea. First, comment out the code that is responsible for filling the text fields (select the code and press <code>Command + /</code>). The easy way is to have the file locally and load it into Framer. Preferably, this would be a JSON file, and you can get it in different ways, such as:</p>

<ul><li>use my <a href="https://edu3.home.pl/Smashing2/feed.json">sample JSON file</a>,</li>

<li>create it from scratch using a tool such as <a href="https://dummi.io/">Dummi</a> or <a href="https://jsoneditoronline.org/">JSON Editor Online</a>,</li>

<li>use some dummy data from Lists,</li>

<li>get the relevant file from the developer you're working with.</li></ul>

<p>But wait, what is <a href="https://www.json.org/">JSON</a>?</p>

<p class="c-pre-sidenote--left">JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language.</p><p class="c-sidenote c-sidenote--right">You can use real data for the entire design process! If you use <a href="https://static.notion-static.com/bfe9dcdb-aee7-4d45-8011-872c38eabf40/sketchapp.com">Sketch</a>, this can be done with <a href="https://www.invisionapp.com/craft">InVision's Craft extension</a>. It can load a local or remote JSON file and fetch the data for use in the layout. To learn more, check out Christian Krammer’s detailed article "<a href="https://www.smashingmagazine.com/2017/02/design-with-real-data-sketch-using-craft-plugin/">Craft for Sketch Plugin: Designing With Real Data</a>." Also, read Wojciech Dobry’s Framer tutorial, "<a href="https://www.toptal.com/designers/ui/framer-tutorial-using-real-data">Prototyping with Real Data</a>."</p> ￼

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fab8371a-b9c9-482c-b873-7c19661c26a3/15-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fab8371a-b9c9-482c-b873-7c19661c26a3/15-introduction-to-framer.gif" width="1200" height="750" alt="Logo animation" /></a><figcaption>Working with real data in Sketch with Craft. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fab8371a-b9c9-482c-b873-7c19661c26a3/15-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>Now, let's put this file in the project’s folder. Each time you save a new Framer project, it creates a folder with the name of your project. Access it in the Finder, and put the JSON file next to the <code>.coffee</code> file in this structure.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6055fdcf-fe98-4843-b678-f39c1b70567d/16-introduction-to-framer.jpg" sizes="100vw" caption="The file structure (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6055fdcf-fe98-4843-b678-f39c1b70567d/16-introduction-to-framer.jpg'>Large preview</a>)" alt="File structure" >}}

<p>The JSON file I'm working with looks like this:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e519e16-aac3-4141-84e8-b2a2111e3837/17-introduction-to-framer.jpg" sizes="100vw" caption="The JSON file (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e519e16-aac3-4141-84e8-b2a2111e3837/17-introduction-to-framer.jpg'>Large preview</a>)" alt="JSON file" >}}

<p>We're going to use the categories data in Framer and replace the dummy content we have in the buttons on the list screen. Just make sure you’ve given proper names to the fields (in my case, <code>item1-txt</code>, <code>item2-txt</code>, etc.) and that you’ve enabled them for the code view with the target icon.</p>

<p>Let's load the feed into Framer:</p>

<pre><code class="language-javascript">data = JSON.parse Utils.domLoadDataSync "feed.json"
</code></pre>

<p>We're using <code>JSON.parse</code> as well as the <code>Utils</code> class &mdash; a pairing that will do all of the hard work of translating JSON into a human language and putting it all in <code>data</code> (the name that we’ve used). To display data from the top of our <code>.json</code> file now, we can print it out:</p>

<pre><code class="language-javascript">print data.categories
</code></pre>

<p>From the data object, we can extract particular items, like in the previous example.</p>

<pre><code class="language-javascript">print data.categories[2]
</code></pre>

<p>Let's create an array with all of the text fields:</p>

<pre><code class="language-javascript">textfields = [item1_txt, item2_txt, item3_txt, item4_txt, item5_txt, item6_txt]
</code></pre>

<p>This is a simplified example, so that even if you are less experienced, you should be able to follow along. You could try to do better by running the loop if you feel more confident. Speaking of loops, we're going to use one, either way, to put the items into the text fields. It goes like this:</p>

<pre><code class="language-javascript">for i in [0...6]
    textfields[i].text = data.categories[i]
</code></pre>

<p>Loops enable you to run the same code many times. It starts with <code>for</code>, and then we define a variable, which I’ve called <code>i</code>. This variable will hold whatever information we pass and then will increment with each loop. In this case, we pass numbers from 0 to 5 &mdash; <code>[0...6]</code> is just a way of saying this. You can check out the values of <code>i</code> in the loop by doing the following:</p>

<pre><code class="language-javascript">print i
</code></pre>

<p>We need it to loop exactly six times (0,1,2,3,4,5), so that we can address each fild on one iteration. Putting <code>i</code> at the end of <code>textfields</code> will return <code>textfields[0]</code>, <code>textfields[1]</code>, and so on; this way, we can address all of the text fields in the array. Again, if you want to double-check, print it! Put more simply, what we've done here is just an easier way of saying this:</p>

<pre><code class="language-javascript">item1_txt.text = data.categories[0]
item1_txt.text = data.categories[1]
item1_txt.text = data.categories[2]
...
</code></pre>

<p>It's easier to grasp, but code-wise, this solution is not elegant at all. That is why we were using a loop here.</p>

<p>The result of our work is that all of the data is populated in the text fields:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d799dfc-8c40-406f-b965-f2566c0a3ded/18-introduction-to-framer.jpg" sizes="100vw" caption="The populated data (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d799dfc-8c40-406f-b965-f2566c0a3ded/18-introduction-to-framer.jpg'>Large preview</a>)" alt="Populated data" >}}

<p>Let's add some links to these items so that we can go to the detail screen. Doing it in the loop is a smart move because we can again add it all at once. Here is the next part of the <code>for in</code> loop (remember to keep the indentation).</p>

<pre><code class="language-javascript">textfields[i].onTap -&gt;
    flow.showNext(detail)
    flow.header.visible = false
</code></pre>

<p>If you want to be more elegant, you can make the items tappable, not only the text. Remember, however, that you have to add them to an array first; so, just before the loop, you can put this:</p>

<pre><code class="language-javascript">items = [item1, item2, item3, item4, item5, item6]
</code></pre>

<p>Then, in the loop, change <code>textfields[i]</code> to <code>items[i]</code>. This whole code block will now look like this:</p>

<pre><code class="language-javascript">textfields = [item1_txt, item2_txt, item3_txt, item4_txt, item5_txt, item6_txt]

items = [item1, item2, item3, item4, item5, item6]

for i in [0...data.categories.length]
    textfields[i].text = data.categories[i]
    items[i].onTap -&gt;
        flow.showNext(detail)
        flow.header.visible = false
</code></pre>

<p>If you want to take this to the next level and display different data depending on the button clicked, my hint is to use this in the event, or get the information from the event by putting <code>(e)</code> next to <code>onTap</code>. I do not recommend doing that now, though: Going crazy with the data is not necessary here. Our main goal is to create a prototype, not a real complex application. Keep that in mind. This JSON example was merely to demonstrate that it is possible to use real data in a Framer prototype.</p>

<p>You probably noticed that we're hiding the header here. That is because we've created a separate header for the detail view. There is a simple arrow icon that we want to link back to the previous screen. This is the block of code we'll use:</p>

<pre><code class="language-javascript">arrow_button.onTap -&gt;
    flow.showPrevious()
    flow.header.visible = true
    flow.footer.visible = true
</code></pre>

<p>Again, <code>showPrevious()</code> is a ready-made method of the flow component, and I just looked it up in the docs!</p>

<p>Our simple prototype is ready, and it looks like this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22ca27f0-9024-4ad0-ae22-0f5bdbb1eab7/19-introduction-to-framer.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22ca27f0-9024-4ad0-ae22-0f5bdbb1eab7/19-introduction-to-framer.gif" width="1200" height="750" alt="Readymade prototype" /></a><figcaption>The final prototype (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22ca27f0-9024-4ad0-ae22-0f5bdbb1eab7/19-introduction-to-framer.gif">Large preview</a>)</figcaption></figure>

<p>You can download the complete <a href="https://framer.cloud/FHCCk">Framer file</a>. Surely, you can tweak it with extra animations, screens and even more data (loaded from a JSON file). I did not want to make it more complex because I wanted to keep the tutorial concise. But trust me, you have enough information to finish this prototype yourself. Just start experimenting with it and you'll see: It's so much fun. Happy coding!</p>

{{< signature "mb, ra, al, yk, il" >}}

