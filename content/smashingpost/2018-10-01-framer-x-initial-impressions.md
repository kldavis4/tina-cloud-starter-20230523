---
title: 'The New Framer X: Initial Impressions'
slug: new-framer-x-initial-impressions
author: lachezarpetkov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bc31679-8f2a-47a5-bb3e-7a51c05fe179/framerx-store-800w.png
date: 2018-10-01T13:30:03+02:00
summary: >-
  The Framer team recently changed course with the announcement of a new prototyping tool, Framer X. Lachezar Petkov got to play with it during the beta phase and discusses its brand new features in this article.
description: >-
  The Framer team recently changed course with the announcement of a new prototyping tool, Framer X. Lachezar Petkov got to play with it during the beta phase and discusses its brand new features in this article.
categories:
  - Framer X
  - Sketch
  - Graphics
---
<p>The Framer team recently released a new prototyping tool, <a href="https://framer.com/x/">Framer X</a>, and I was lucky enough to be able to test it during the beta phase. In this article, I’d like to share my thoughts about this new tool and its features. I’ll make a comparison with the “legacy” Framer app as well as other tools, and I’ll discuss its brand new features such as <em>Stacks</em> and <em>Scroll</em>, and its new <em>Code</em> and <em>Design</em> components.</p>

<p>This article is intended for UI and UX designers who would like to learn more about Framer X’s prototyping abilities. Since it is (in many ways) a brand new product, you don’t need to be familiar with the <a href="https://www.smashingmagazine.com/2018/02/introduction-to-framer/">older Framer application</a> to read along. However, a little bit of familiarity with HTML, CSS, <a href="https://reactjs.org/tutorial/tutorial.html">React</a>, JavaScript and <a href="https://medium.freecodecamp.org/what-exactly-is-node-js-ae36e97449f5">Node.js</a> are beneficial.</p>

<p>For the purpose of this tutorial, I have also created a prototype which is a <a href="https://material.io/design/">Material</a> exploration of the <a href="https://www.khanacademy.org/">Khan Academy</a>’s app for Android.</p>

<p><strong>Note</strong>: <em>I’m in no way affiliated with Khan Academy; I just thought this would make a cool experiment &mdash; I hope you’ll agree.</em></p>

## Intro To Framer X

<p>Framer X goes a few steps further than its predecessor in trying to bridge the gap between interface design and software development. Here’s how:</p>

### Dear Designers, Meet React

<p>The key difference between the old and the new applications in this regard is the introduction of <a href="https://reactjs.org">React</a> and JavaScript / <a href="https://www.typescriptlang.org/">TypeScript</a>, as opposed to using CoffeeScript for programming microinteractions and animations, loading data, and so on.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1964809-2686-43ff-b0a9-496ec03b6009/framerx-react-logos.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1964809-2686-43ff-b0a9-496ec03b6009/framerx-react-logos.jpg" sizes="100vw" caption="Framer X’s most important feature: It integrates tightly with ReactJS. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1964809-2686-43ff-b0a9-496ec03b6009/framerx-react-logos.jpg'>Large preview</a>)" alt="Framer X and React logos" >}}

<p>During the beta phase, people wrote some React components that I think show us the potential of how far the tool can take us. For example, you can embed actual media players (that actually stream and play music and video) within your prototypes. Or, you can <a href="https://store.framer.com/package/marcopesani/sparkline">embed graphs</a> with real-time stock market data. Or how about a component that can <a href="https://store.framer.com/package/zach/translate">translate your prototype’s UI</a> into other languages. And that’s not all: Things are just getting started.</p>

{{% feature-panel %}}

<p>The same React code you write for a Framer X prototype could &mdash; at least hypothetically &mdash; be used in a production environment after the design phase. This can be especially useful for teams that do a lot of web development in React (and perhaps for teams who write mobile apps in React Native). Personally, I shudder at the thought of me, <em>a designer</em>, writing any code that goes into production, but that might work for others.</p>

<blockquote>“Framer X is more like Unity than like Photoshop. An IDE for design, if you will.”<br /><br />&mdash;The Framer X documentation</blockquote>

### The Framer X Interface

<p>If you are already a Framer user, the first thing you’d notice is that the integrated code editor is gone. Instead, if you want to write any code, you can use an editor of your choice. Most people (including myself) seem to go with <a href="https://www.smashingmagazine.com/2018/09/visual-studio-live/">VS Code</a>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f945d8-23cc-4746-b5b8-96635a80202b/framerx-screenshot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f945d8-23cc-4746-b5b8-96635a80202b/framerx-screenshot.png" sizes="100vw" caption="Framer X (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f945d8-23cc-4746-b5b8-96635a80202b/framerx-screenshot.png'>Large preview</a>)" alt="Framer X screenshot" >}}

There are four tabs in the sidebar:

- **Tools**  
Opens all the layout and drawing tools everyone’s familiar with (shapes, path, text, <a href="https://help.framer.com/learning-framer/frames-and-shapes">frames</a>) as well as three new toys we’ll discuss a little later: Stacks, Link, and Scroll.
- **Layers**  
Contains, well, the layers of the selected frame, as well as its properties (color, position, border, shadow and so on). This bit is essentially the same as in the old Framer, and very similar to Sketch and Figma.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a4751f-b6ca-46fb-ae35-5e3bba22bc30/framerx-layers.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a4751f-b6ca-46fb-ae35-5e3bba22bc30/framerx-layers.jpg" sizes="100vw" caption="The Framer X Layers panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a4751f-b6ca-46fb-ae35-5e3bba22bc30/framerx-layers.jpg'>Large preview</a>)" alt="The Framer X layers panel" >}}

- **Components**  
This is for any Design or Code components you may have in the file you’ve opened.
- **Store**  
A new, huge feature in Framer X. It allows users to publish their creations &mdash; be it icons and illustrations or interactive code components for others to use. Currently, all components are free of charge, but I’d imagine people will be able to sell their stuff at the store in the future.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23a6c15-9283-4bce-9677-54d3a9eb08cb/framerx-store.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23a6c15-9283-4bce-9677-54d3a9eb08cb/framerx-store.png" sizes="100vw" caption="The Framer X Store (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23a6c15-9283-4bce-9677-54d3a9eb08cb/framerx-store.png'>Large preview</a>)" alt="The Framer X Store" >}}

<p>The <strong>Preview</strong> and <strong>Live Preview</strong> buttons are up at the top right corner. As with legacy Framer, you can preview your prototypes within a device picture for more realism, or preview them directly on an actual device, or in a browser.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/02/introduction-to-framer/">Learning Framer By Creating A Mobile App Prototype</a></em></p>

## Prototyping With Framer X

### A Few Thoughts On The Prototype We’ll Create

<p>The Khan Academy Android app isn’t a <a href="https://material.io/">Material app</a>, so let’s explore how it might look and behave if it was. I want to think of this as if it were a real-world project, so here are a couple of considerations that we’ll see how to handle in Framer X:</p>

1. The product’s goal is to provide free education for everyone, thus it must be able to run on old and cheap devices. What this means for the design of the prototype is, it has to work on `320dp` wide screens.
2. The design must adapt well when the app is translated into a language more verbose than English.

The first thing I’m going to do is mock up the *Home* screen. There are four things I want to be prominent:

- A search input;
- Something that will show me my most recent activity;
- Something that will show me my Missions;
- Something to notify me if there’s a new Mastery Challenge.

Let’s begin.

### Installing Components From The Store

<p>The first two elements I want to have here are the Android status bar and navigation bar. Instead of drawing them myself, I’ll quickly install a component bundle from the store called “<a href="https://store.framer.com/package/graz/android-kit">Android Kit</a>”. It contains all sorts of (static, not programmed in this case) elements like buttons, cards, switches, bars, keyboards and so on. I got my status bar and my nav bar in seconds:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d91f5a7b-e342-42af-a379-aeb7acfec0cb/add-component-store.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d91f5a7b-e342-42af-a379-aeb7acfec0cb/add-component-store.gif" width=“437" height="512" alt="Adding a component from the Store" /></a><figcaption>Adding a component from the Store</figcaption></figure>

<p><strong>Note</strong>: <em>Each component is installed per-project.</em></p>

### The Interactive Scroll Tool

<p>Now, if I were doing this in Sketch, I’d continue mocking up the rest of the elements on the same artboard, and if it can’t fit all elements, I’d make it taller. In Framer X, however, things work a little differently. I’ll have the <em>content</em> of the Home screen within a separate frame (screen/artboard) and <em>link</em> that frame so it scrolls beneath the navigation and status bars of the home screen:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33701655-7aa7-49bb-98f1-a248b0819dc6/new-scroll.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33701655-7aa7-49bb-98f1-a248b0819dc6/new-scroll.gif" width=“672" height="402" alt="Using the Scroll tool" /></a><figcaption>Using the Scroll tool</figcaption></figure>

<p>Now when I run a preview, my content is scrollable:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d23adf16-774b-476b-b146-d46246670fbd/new-scroll-scrolling.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d23adf16-774b-476b-b146-d46246670fbd/new-scroll-scrolling.gif" width=“376" height="690" alt="The Scroll tool in action" /></a><figcaption>The Scroll tool in action</figcaption></figure>

<p>Awesome! With the underlying work out of the way, I’m ready to increase the fidelity a little bit. First, I want the general style of the app to be soft and welcoming, so I’ll use <code>4dp</code> (display points) border-radius for my cards and buttons, and the <a href="https://material.io/tools/icons/?style=round">rounded Material icons</a>.</p>

<p>Since having an actual search input is super important for this screen, I don’t want the regular Android <a href="https://material.io/develop/android/components/app-bar-layout/">App bar</a> and search icon experience. I’ll go for an actual input with a CTA message along with a hamburger icon ala Google Maps.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce79cd74-8e85-4d82-886d-e0457cb91521/proto-appbar.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce79cd74-8e85-4d82-886d-e0457cb91521/proto-appbar.jpg" sizes="100vw" caption="The app bar and search input for this prototype (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce79cd74-8e85-4d82-886d-e0457cb91521/proto-appbar.jpg'>Large preview</a>)" alt="The app bar and search input for this prototype" >}}

<p>If I were to go deeper here, I’d make this bar a code component and write it so it expands to full width on scroll, like this:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af3f157b-1686-4dc6-92ee-ef55cda9a81e/proto-appbar-expanded.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af3f157b-1686-4dc6-92ee-ef55cda9a81e/proto-appbar-expanded.jpg" sizes="100vw" caption="The app bar, expanded on scroll (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af3f157b-1686-4dc6-92ee-ef55cda9a81e/proto-appbar-expanded.jpg'>Large preview</a>)" alt="The app bar, expanded on scroll" >}}

<p>I won’t do that for the purpose of this article, but I have to say I think something as simple would be easier to do in legacy Framer compared to Framer X &mdash; at least in this first version.</p>

### Linking

<p>Let’s add some basic interactivity to this thing! When I tap on the search input, I want it to pull out a keyboard from the bottom. When I tap on the menu icon, however, I want to pull out a <a href="https://material.io/design/components/navigation-drawer.html">Navigation drawer</a> from the left side.</p>

<p>Whereas in legacy Framer I’d have to write a <a href="https://framer.com/docs/#flow.flowcomponent">FlowComponent</a> for this type of thing, it’s now super easy in Framer X and with its new Link tool! It’s similar to other prototyping applications in which I’d select a UI element, link it to a frame, and choose the type of transition I want. I imported the keyboard from the Android Kit component and linked to it from the search input. I set the transition to <strong>Overlay</strong> and the direction to <em>bottom</em>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9788340-9055-4097-8f4f-0f5a86b6b390/linking.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9788340-9055-4097-8f4f-0f5a86b6b390/linking.jpg" sizes="100vw" caption="Once you link two frames, you can configure the link through the Links panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9788340-9055-4097-8f4f-0f5a86b6b390/linking.jpg'>Large preview</a>)" alt="The Links panel" >}}

<p>Because I have too many items in the navigation drawer to fit on a screen, I had to split it into two frames just like the <em>Home</em> screen: one container with a scroll layer linked to a frame with the actual content inside. Here’s how that looks:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bbf38f-16dc-4e18-9afb-f264339655b9/linked-frames.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bbf38f-16dc-4e18-9afb-f264339655b9/linked-frames.jpg" sizes="100vw" caption="The 'Birdseye' view of all linked frames in the prototype so far (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bbf38f-16dc-4e18-9afb-f264339655b9/linked-frames.jpg'>Large preview</a>)" alt="Linked frames" >}}

{{< vimeo id="291475598" >}}

<p><em>Interacting with the prototype</em></p>

<p>Neat! There is a problem with this approach, though, that the Framer team will hopefully fix. When the transition of a frame is set to <strong>Overlay</strong>, it covers and dims <em>everything</em> beneath it. This isn’t quite what we want when we prototype for Android: The nav bar and status bar have to be <em>above all</em> other screen elements &mdash; including the overlays.</p>

<p>Same goes for the Search interface: I don’t want any screen dimming if I want to have filtering options and/or a list of recent queries when the keyboard is pulled out. Hopefully, we’ll see some fixes for these issues in future Framer X versions.</p>

{{% ad-panel-leaderboard %}}

### Pinning, Positioning, And Responsiveness

<p>Back to the <em>Home</em> screen of the prototype. Below the search input, I want a list with my recent activity. Just as in legacy Framer and other design tools, you can pin elements within frames so they move and scale exactly as you want them to. Framer X also shows you distances and gaps between elements, snaps them together for you, and so on. Have a look:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5eafb86e-da7c-452e-9429-d06f219e7f57/pinning.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5eafb86e-da7c-452e-9429-d06f219e7f57/pinning.gif" width=“512" height="265" alt="A pinned frame." /></a><figcaption>Once my frames are pinned appropriately, designing responsively is very easy.</figcaption></figure>

### Design Components

<p>I want to add a few more things to the prototype home screen: A <em>Mastery Challenge</em> prompt, a streak counter, list of missions, bookmarks and some UI that allows the user to explore content they might find cool or useful.</p>

<p>Since the recent missions and the bookmarks are going to be cards with very similar content, the best solution Framer X has for me is to use <strong>design components</strong>. I already mentioned them above (the Material Kit component bundle). Framer X’s design components work similarly to Sketch’s symbols and Figma’s components.</p>

<p>To convert a frame to a component, simply press <kbd>Cmd</kbd> + <kbd>K</kbd>. This creates a Master from which you can create as many instances as you want:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e544e691-0bbc-4148-a254-69d7ef6d1952/master-instance.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e544e691-0bbc-4148-a254-69d7ef6d1952/master-instance.gif" width=“620" height="648" alt="A Master component and it’s instance." /></a><figcaption>A Master component and its instance: Any changes applied to the Master are applied to the Instance, but not the other way around.</figcaption></figure>

<p>Anything you do to a Master component will affect its instances, but whatever you do to the instances won’t affect the Master. You can also nest Master components and go as crazy as you like.</p>

<p>So, here are my <em>Recent</em> missions and <em>Explore</em> sections:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df7737a3-e6be-456c-b807-e71711f963dc/horizontal-scroll.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df7737a3-e6be-456c-b807-e71711f963dc/horizontal-scroll.jpg" sizes="100vw" caption="Recent missions and Explore sections as horizontally scrollable frames. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df7737a3-e6be-456c-b807-e71711f963dc/horizontal-scroll.jpg'>Large preview</a>)" alt="Horizontally scrollable frames" >}}

<p>Each section is a frame, connected to its own scroll component, and populated with components. The text strings (as well as the bitmap images in the instances) are overrides.</p>

### Stacks

<p>Now, what if I’m not sure how to position and distribute all these cards? Well, Framer X’s Stacks feature comes into play here:</p>

{{< vimeo id="291477573" >}}

<p>I only had to make sure that all items I wanted into a Stack are organized into frames. It works surprisingly well, and you can have components within a stack, as well as a stack within another stack, and so on. It’s huge for anyone mocking up and prototyping lists often!</p>

### Drawing Icons And Illustrations

<p>The drawing tools in Framer X are pretty much the same as in legacy Framer. They’re good enough to do a lot, but still somewhat lagging behind Sketch’s: There are no rulers; you can’t convert strokes to outlines; you can’t flatten shapes; there’s no scissors tool.</p>

{{< vimeo id="291477961" >}}

{{< vimeo id="291478285" >}}

### Code Components

#### Creating A Simple Code Component

<p>Finally, let’s take a closer look at the code components. Again, these are regular React components (both Stateless and Class) that can be written in either JavaScript or TypeScript (up to you). You can also install third-party libraries to use within your components in Framer.</p>

<p>Let’s try and use the popular <a href="https://www.styled-components.com/">styled-components</a> library. This will allow us to style our component using actual CSS syntax within the <em>.tsx</em> file.</p>

<p>First, go to the <strong>Components</strong> tab&nbsp;&rarr;&nbsp;<strong>New Component</strong>&nbsp;&rarr;&nbsp;<strong>from Code</strong>. After you name your component and confirm, your default system editor (in my case, VS Code) will open an example Framer X component file.</p>

<p>Now go to <strong>File</strong>&nbsp;&rarr;&nbsp;<strong>Show project folder</strong>, <a href="https://apple.stackexchange.com/questions/11323/how-can-i-open-a-terminal-window-directly-from-my-current-finder-location">open a terminal</a> in that same folder, install <a href="https://yarnpkg.com">yarn</a> if you haven’t already and add <code>styled-components</code> to your Framer project:

<pre><code class="language-javascript">$>yarn add styled-components
</code></pre>

<p>The library and its dependencies will be added to your <em>package.json</em> and you’re ready to go.</p>

<p>Here’s the source for my <code>styled-components</code> button, after I replaced the default code in my component’s <em>.tsx</em> file:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f94a6a9-72b6-430f-afe2-cbaeb3f6cd09/code-component.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f94a6a9-72b6-430f-afe2-cbaeb3f6cd09/code-component.jpg" sizes="100vw" caption="The Go button as a code component and its source (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f94a6a9-72b6-430f-afe2-cbaeb3f6cd09/code-component.jpg'>Large preview</a>)" alt="The Go button code component and its source" >}}

<p>Note that the button label is customizable directly through the Framer X interface (because of the Framer library’s <code>PropertyControls</code> feature). Having my button written in code obviously has many advantages. It is customizable, responsive, and interactive. Along with the responsive paddings, it’s super easy to test if the design breaks in other languages.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/823ca42a-ca80-4864-bae0-8ff4a660ef51/code-component-lang.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/823ca42a-ca80-4864-bae0-8ff4a660ef51/code-component-lang.jpg" sizes="100vw" caption="The responsive Go button, translated quickly by changing the Text property directly in the Framer X UI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/823ca42a-ca80-4864-bae0-8ff4a660ef51/code-component-lang.jpg'>Large preview</a>)" alt="The responsive Go button, translated quickly by changing the Text property directly in the Framer X UI." >}}

#### Importing A Code Component From The Store

<p>There’s a lot of video content on Khan Academy, so for my prototype, I want to open a video lesson. Instead of mocking up a ‘fake’ video player, I can directly embed an actual YouTube player in my prototype. There’s already a component in the Store for this purpose:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb0a15d6-8ec2-4191-b64a-2cc11a694f52/component-youtube.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb0a15d6-8ec2-4191-b64a-2cc11a694f52/component-youtube.gif" width=“394" height="738" alt="Playing a video with the YouTube code component." /></a><figcaption>Playing a Khan Academy video in a Khan Academy prototype</figcaption></figure>

<p>You can fork the code of any Store component and edit it as you like. For now, the only way to do this is to right-click on it in the sidebar, copy its code and paste it in a newly created components’ file.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55afd9c9-e6e3-4b06-a07e-d7bd78604d46/component-copy-code.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55afd9c9-e6e3-4b06-a07e-d7bd78604d46/component-copy-code.jpg" sizes="100vw" caption="You can copy every Store component’s code and play with it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55afd9c9-e6e3-4b06-a07e-d7bd78604d46/component-copy-code.jpg'>Large preview</a>)" alt="Copying a Store component’s code." >}}

### Code Overrides And The Framer library

<p><strong>The Framer JavaScript library</strong> has now been ported to work with Framer X and React. As with the legacy Framer library, it provides us with tools (helper functions) to animate our designs and to listen to events (simple things like onClick and onMove, but also advanced events like pinch, whether the device has been rotated or whether an animation has ended, and more).</p>

<p><strong>Code Overrides</strong> are bits of code (JS functions) that allow you to change any frame’s or component’s properties. Static changes such as color are applied before you run the preview, directly within the Framer app, and the animations/interactions can be seen in the Preview window or on your preview device.</p>

<p>Let’s have a quick look at one of the simplest and default examples. I drew this simple champions cup illustration for one of the prototype cards, and I decided to animate it:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7072f1f-80b4-4ed9-b0e9-b9352c8d5290/mastery-challenge.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7072f1f-80b4-4ed9-b0e9-b9352c8d5290/mastery-challenge.jpg" sizes="100vw" caption="The static Mastery Challenge card (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7072f1f-80b4-4ed9-b0e9-b9352c8d5290/mastery-challenge.jpg'>Large preview</a>)" alt="The static Mastery Challenge card" >}}

<p>To add an override, I have to select my target frame (in this case the illustration) and click on the <em>Code</em> menu item in the right sidebar. Now I need to select the override I want from Exampels (selected by default in the drop down):</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83096c08-0961-4bfd-a0d6-72bc6770db11/code-override-scale.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83096c08-0961-4bfd-a0d6-72bc6770db11/code-override-scale.gif" width=“226" height="336" alt="Choosing the Scale code override" /></a><figcaption>The Scale code override will provide me with a fun scale animation. I can edit it’s code and adjust as I like.</figcaption></figure>

<p>Remember, overrides are just blocks of code, therefore, they can live in any file within your project. What I just selected was the <em>Examples.tsx</em> file which contains multiple functions for Scale, Rotation, Fade, and so on. I can create my own file and write my own <code>Override</code> functions, or include them in my code components source code &mdash; just as long as I keep in mind to use the <code>Override</code> <a href="https://www.typescriptlang.org/docs/handbook/basic-types.html">type specifier</a> when I <code>export</code> them.</p>

{{% ad-panel-leaderboard %}}

<p>Here’s the source code for the Scale override I chose:</p>

<div class="break-out">

<pre><code class="language-javascript">export const Scale: Override = () => {
	return {
		scale: data.scale,
		onTap() {
			data.scale.set(0.6)
			animate.spring(data.scale, 1)
		},
	}
}
</code></pre></div>

<p>In plain English: Set the initial scale value of the frame down to 0.6, then animate the scale to 1 with spring curve. Finally, export it with name Scale and specify that it is an Override.</p>

<p>Once applied, this is the result:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fed47a4e-34fc-4c80-911f-f17d07847845/code-override-anim.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fed47a4e-34fc-4c80-911f-f17d07847845/code-override-anim.gif" width=“402" height="58" alt="The Mastery Challenge card with some animation" /></a><figcaption>The Mastery Challenge card with some animation</figcaption></figure>

### Design Responsiveness

<p>As I mentioned in the beginning, it is essential for this particular prototype to work on small device screens (<code>320dp</code>). This is very easy to test in Framer X (considering you’ve pinned your UI elements properly, as described above). Simply set the Preview mode to <strong>Canvas - Responsive</strong>:</p>

{{< vimeo id="291482276" >}}

<p><em>Framer X makes it easy to test my designs for different screens.</em></p>

<p>This is super helpful &mdash; I am now aware of what problems my designs have on smaller screens, and I’m ready to come up with fixes for the next iteration!</p>

### Day And Night Modes

<p>Finally, in Framer you have two themes: Light, called “Day” mode:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bda502f-cd59-4c33-bb15-3dc7d70a9e21/day-mode.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bda502f-cd59-4c33-bb15-3dc7d70a9e21/day-mode.jpg" sizes="100vw" caption="Framer X during the day (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bda502f-cd59-4c33-bb15-3dc7d70a9e21/day-mode.jpg'>Large preview</a>)" alt=" Framer X  day (light) mode" >}}

<p>And dark, called “Night” mode:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14a5b801-3452-4033-8dc8-6e6fc057fcb7/night-mode.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14a5b801-3452-4033-8dc8-6e6fc057fcb7/night-mode.jpg" sizes="100vw" caption="Framer X at night (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14a5b801-3452-4033-8dc8-6e6fc057fcb7/night-mode.jpg'>Large preview</a>)" alt="Framer X  dark (night) mode" >}}

<p>You can switch the two from the <em>Window</em> menu.</p>

## Protoype: Final Result

<p>Here are all my frames linked together:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b03a52b-eadd-4111-89e2-065ded1bb6b1/prototype-all-links.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b03a52b-eadd-4111-89e2-065ded1bb6b1/prototype-all-links.jpg" sizes="100vw" caption="All my frames linked together (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b03a52b-eadd-4111-89e2-065ded1bb6b1/prototype-all-links.jpg'>Large preview</a>)" alt="All my frames linked together" >}}

<p>And here’s the prototype in action:</p>

{{< vimeo id="291486609" >}}

## What I Like About Framer X

<p>The application performs fast (though the beta choked a little with large project files) and <strong>it feels well designed</strong>. It’s a new tool, yet at the same time, it feels familiar. It also does give me that sense of it being a ‘design IDE’ and I think the Framer team is taking things in a very interesting direction.</p>

<p>Framer X makes mundane things like linking screens and scrolling fast and easy, as they should be. Though I hope to see even more of that type of thing in the future: <strong>prototyping is supposed to be a quick and dirty process</strong>, after all. To spend too many hours on a prototype is to miss the point of prototyping.</p>

<p>Having a Components Store is a great idea, and will certainly speed up my design process. <strong>I no longer have to spend time hunting down the plugins I need</strong>. I can imagine a couple of years from now there will be thousands of components with basically everything I need to put something relatively advanced together &mdash; relatively quickly. It may need some moderation in the future, though. I can see people uploading too many simple buttons, each a fork of the other, just because they can.</p>

<p>I like the focus on design systems through the components and the <em>Private Store</em> features. We all know, <strong>many teams struggle to collaborate meaningfully</strong> and tools like these are an immense help.</p>

## What I’m Not Sure I Like About Framer X

<p>What worries me a little is that part of the “super easy playground for experimentation” experience of the original Framer tool is somewhat gone. The new features in X make it very easy to quickly prototype any “standard” feature or screen: you have all you need in the Store. But it is arguably <strong>more difficult to explore crazy and weird ideas for custom interactions</strong> &mdash; at least with this initial product release.</p>

<p>Learning React will be more intimidating to a lot of us, math and logic-impaired designers. For me personally, code reuse is not an option, since none of the projects I’m currently working on are built using web technologies. But even if it was an option, I’m thinking about programming in terms of it being a tool to express my design ideas. I’m not an engineer; <strong>using my code for anything but a prototype</strong> is not exactly a terrific idea.</p>

<p>Having said that, there’s <em>a lot</em> more documentation on JavaScript and React than on CoffeeScript. There’re also more people to help out, and the React community seems <a href="https://twitter.com/dan_abramov/status/1025540365435199488">pretty welcoming</a>. I’m very curious to see how Framer X will help designers and engineers collaborate more &mdash; if at all.</p>

## Framer X In My Toolset

<p>I’ll definitely be using Framer X in production, but I can’t see it completely replacing Sketch for me just yet. In my organization, each designer is allowed to use their favorite tool, as long as it integrates with <a href="https://zeplin.io">Zeplin</a>, and Framer X doesn’t. Other things it lacks compared to Sketch (for now) are the pages, the crazy amount of plugins, and the more powerful drawing tools.</p>

<p>I will continue to use the original Framer for custom interactions &mdash; at least for the foreseeable future. When prototyping, things need to be done fast, and I also still have much to learn about React.</p>

{{< signature "mb, ra, yk, il" >}}
