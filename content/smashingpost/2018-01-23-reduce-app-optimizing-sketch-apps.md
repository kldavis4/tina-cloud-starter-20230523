---
title: >-
  Optimizing Sketch Files: Lessons Learned In Creating The Reduce App (Case
  Study)
slug: reduce-app-optimizing-sketch-files
author: ahmed-sulaiman
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f97c5830-62ec-4bf3-b5ff-fb0d98a2b2cc/design-reduce-3.png
date: 2018-01-23T13:00:27.000Z
summary: >-
  There are huge Sketch files that exist, and not only do they slow down Sketch,
  but also any designer's productivity. In this article, Ahmed introduces a menu
  bar application that is bound to help you get rid of this headache.
description: >-
  There are huge Sketch files that exist, and not only do they slow down Sketch,
  but also any designer's productivity. In this article, Ahmed introduces a menu
  bar application that is bound to help you get rid of this headache.
categories:
  - Performance
  - Sketch
  - Apps
---
<p>Sketch had brought totally new standards for file sizes. You no longer see 10 GB Photoshop files all over the place. Nevertheless, huge Sketch files exist, and they slow down Sketch. As a result, your productivity slows down as well.</p>

<p>Let’s be honest: It's not the design files that become bigger by magic. It’s designers who fill their files with unused, unoptimized and hidden elements that take unnecessary space.

<p>We have faced this problem in our startup, Flawless App. We tend to have a separate Sketch file for each product. By “product”, I mean our core menu-bar application, website, social materials, press kit, illustrations for the articles on our Medium blog, and so on. These files used to grow a lot over time because of constant iterations and testing of different design decisions. As a result, it became harder and harder for Sketch to manage them with proper performance.</p>

<p>As any other engineers would do, we decided to write a small script that cleans and optimizes Sketch files automatically.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f145f6a-6e39-41df-8047-3a70ba3ce439/design-reduce-1.png" sizes="100vw" caption="The very first version as a script in Terminal. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f145f6a-6e39-41df-8047-3a70ba3ce439/design-reduce-1.png'>Large preview</a>)" alt="The very first version as a script in Terminal" >}}

Scripts are great &mdash; that is, if you speak the same language as Terminal. Eventually, we decided that we needed a more human-like approach to allow more people from the team to use it. We also wanted to make it free and publicly available later on.</p>

{{% feature-panel %}}

## The First Prototype

<p>I had some abstract concepts in mind before drawing any UI. The main goal was to make something that would live right at our fingertips all the time and allow us to optimize files as quickly as possible. A menu bar application was an obvious choice:</p>

<ol>
<li>We already had an internal framework for menu bar applications, with a lot of custom functions implemented. To give you some background: our core product, Flawless App, is a menu bar application that compares the expected design with the developer's implementation in real time. This internal framework was built for our core product.
</li>
<li>You can use the menu bar application even when Sketch isn’t open.
</li>
<li>Developing a native macOS app was much faster for us than a Sketch plugin with CocoaScript (because of our previous experience).</li>
</ol>

<p>It was also crucial to give the user the ability to toggle different optimization options for different files.</p>

<p>Here is the very first wireframe, drawn on an old-fashioned paper, no fancy prototyping tools.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eae112e-31f4-4218-94e1-8e7b865015d9/design-reduce-2.jpg" sizes="100vw" caption="Initial Reduce app wireframe. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eae112e-31f4-4218-94e1-8e7b865015d9/design-reduce-2.jpg'>Large preview</a>)" alt="Initial Reduce app wireframe" >}}

### Lesson Learned #1

<p>Before doing any UI, prototypes in fancy tools or even wireframes on paper, think about what goals you need to accomplish with a design. Who would use it, and how would the user interact with the application.</p>

## Color Palette And Typography

<p>In discussion with the team, we didn't find any critical UX issues in the wireframes. I started by creating a color palette and choosing a font schema.</p>

<p>I wanted the application to be light and visually different from our core product, Flawless App. So, I came up with following palettes:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fddf24b6-7d8d-4248-8d68-e60a111655fd/design-reduce-5.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fddf24b6-7d8d-4248-8d68-e60a111655fd/design-reduce-5.png'>Large preview</a>" alt="palettes" >}}

<p>The first row is for the text colors (plus the light background at the beginning). The second row is for the accent colors. All colors were derived from one base accent color by applying simple rules for the HSB color system (H stands for hue, S for saturation and B for brightness).</p>

<p>Let’s say we have a base color of #4A90E2 (blue), which is (212, 67, 89) in HSB.
To get a bit darker color, we need to decrease the brightness, increase the saturation and move the hue just a bit. So, we’d get #2477C9, which is (210, 82, 79) in HSB. I used the same approach for all other colors.</p>

<p>Eventually, I had chosen the first color palette (orange). Sketch files and the Sketch logo are orange as well, so our application would look more organic with them.</p>

### Lesson Learned #2

<p>Colors were always tricky for me. I usually spend a lot of time finding just the right color. Here are a couple of resources that I use almost daily to help me explore colors:</p>

<ul>
<li><a href="https://color.adobe.com">Adobe Kuler</a> can help you find a color companion for any color.
</li>
<li><a href="https://khroma.co/">Khroma</a> is an AI-based tool to generate color palettes based on your preferences.</li>

<li>Erik Kennedy’s article, <a href="https://blog.marvelapp.com/color-ui-design-practical-framework/">"Color in UI Design: A (Practical) Framework"</a> is a pure gem. I read it about eight months ago, and since then I’ve used the HSB color system much more than RGB in Sketch.
</li>
</ul>

<p>Regarding typography, in most cases, using the default font for a native macOS application is best, unless you’re building something super-custom. Rendering time is faster, and it’s easier to implement during development. But I was so thrilled to try Montserrat in a native macOS app that I could not resist.</p>

### Lesson Learned #3

<p>There are many great resources to explore fonts. Nevertheless, I use old-fashioned Google Fonts to get a sense of a particular font.</p>

## First Design Iteration

<p>I started from exactly what I drew in the initial wireframe. Here is the general user flow in the application:</p>

<ol>
<li>Drag and drop a Sketch file.
</li>
<li>Choose optimization options.
</li>
<li>Reduce the selected file.
</li>
<li>Save it.
</li>
</ol>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bef4e64-9ca8-46cb-b750-08633de56922/design-reduce-3.png" sizes="100vw" caption="The first design iteration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bef4e64-9ca8-46cb-b750-08633de56922/design-reduce-3.png'>Large preview</a>)" alt="The first design iteration" >}}

<p>I was making designs in Sketch, and I was completely pleased with the overall UI. Because I had designed a menu bar applications before, the text sizing and margins were quite standard for me. Nevertheless, there were some noticeable issues with the first iteration, which I’ll describe later.</p>

### Lesson Learned #4

<p>If you have never designed anything for macOS before, then definitely check out the <a href="https://facebook.design/desktopkit">Facebook Desktop Design Kit</a>. You’ll find all of the common macOS UI elements there. And it will give you a sense of sizes and offsets for UI elements. For a macOS menu bar application, a 12 to 14-point font size is totally normal.</p>

## Issue #1: Missed State

<p>Everything was great except that I forgot to build a state in the middle when the application would be processing the Sketch file. As I know from experience, a missed state at the design stage equals a headache at the development stage.</p>

<p>How often do developers complain that designers design in a vacuum? You know, they’re talking about those problems with missing states in the middle, empty states, using perfect data sets and so on.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8027e10-ebf9-45bf-82d0-4cd8ca447b4c/design-reduce-4.png" sizes="100vw" caption="File-processing state in Reduce app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8027e10-ebf9-45bf-82d0-4cd8ca447b4c/design-reduce-4.png'>Large preview</a>)" alt="File-processing state in Reduce app" >}}

### Lesson Learned #5

<p>Before sending your design to the developers, make sure you haven't forgotten anything. Make sure you’ve specified all states, so that developers don’t ask you later, “How should this look in [some special condition]?” A good way to find these kinds of missed states is to use a prototyping tool. So far, the Craft plugin for Sketch (created by Invision), with its prototyping feature, is the fastest way to do such testing.</p>

<div class="video-container"><iframe loading="lazy" data-
src="https://player.vimeo.com/video/251130482"
  width="640" height="360" frameborder="0"
  webkitallowfullscreen mozallowfullscreen allowfullscreen>
</iframe></div>

## Issue #2: Too Many Custom Elements

<p>You will almost always be designing for a particular platform. In our case, it was macOS. And macOS has somewhat standard elements already in place. So, unless your product won’t work without a custom solution, use standard elements where they make sense. Developers will also thank you.</p>

<p>With these thoughts in mind, I removed the custom checkboxes and replaced them with the default ones. I also simplified the progress window by removing all unnecessary custom indicators.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7925724-6424-4ad6-baf1-44270b3892dc/design-reduce-6.png" sizes="100vw" caption="New optimization list window with macOS default elements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7925724-6424-4ad6-baf1-44270b3892dc/design-reduce-6.png'>Large preview</a>)" alt="New optimization list window with macOS default elements" >}}

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87803b22-e5de-4b30-886d-ee64a4af7755/design-reduce-7.png" sizes="100vw" caption="New file-processing window with macOS default elements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87803b22-e5de-4b30-886d-ee64a4af7755/design-reduce-7.png'>Large preview</a>)" alt="New file-processing window with macOS default elements" >}}

### Lesson Learned #6

<p>To get a sense of the default elements for each platform, I’d suggest looking at these materials:</p>

<ul>
<li>iOS: <a href="https://developer.apple.com/design/resources/">Apple UI Design Resources</a>, available for Sketch, Photoshop and Adobe XD
</li>
<li>Android: <a href="https://materialdesignkit.com/android-gui/">Material Design Kit</a></li>
<li>macOS: <a href="https://facebook.design/desktopkit">Facebook Desktop Kit
</a></li>
</ul>

## Issue #3: Not Enough Emphasis At The End

<p>After a couple of feedback sessions with the team, it was clear that the final screen was overloaded. There was no indication of how much a file size had changed from optimization. So, I made a separate screen with a nice illustration of the compressed file and the label with file size information.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61ac2cc9-1e71-4129-b3ef-c3d064213bd3/design-reduce-8.png" sizes="100vw" caption="New final screen on the right, and the old one on the left. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61ac2cc9-1e71-4129-b3ef-c3d064213bd3/design-reduce-8.png'>Large preview</a>)" alt="New final screen on the right, and the old one on the left" >}}

### Lesson Learned #7

<p>We use Slack as our main place for communication. <a href="https://github.com/shahruz/Send-to-Slack">Send to Slack</a> is a little plugin that shares an artboard from Sketch directly to a Slack channel. It was really handy for team feedback sessions. Share more, share often.</p>

## Issue #4: Big Little Details

<p>The issues below were found during development. But I’ll place them here anyway to keep the article’s structure consistent.</p>

<p>I started implementing the design. Right after the first launch, I realized there was no way for the user to Quit the application.</p>

<p>We also wanted to distribute our application via our own channels, instead of the Mac App Store. So, it was critical for us to add an auto-update system to the application. And the user should be able to see the current version and to check for updates. I ended up with a menu that presents this information and secondary actions in one place.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1024ec7d-41ec-4adc-b67c-ed7aab06327f/design-reduce-9.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1024ec7d-41ec-4adc-b67c-ed7aab06327f/design-reduce-9.png'>Large preview</a>" alt="updates" >}}

<p>The last missed detail was a function to close an optimized file and return to the main screen without any saving. I added the same “close” button as appears in the “optimizations list” window in the upper-right corner.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb04d437-174c-4ece-b621-9cd3b75d2833/design-reduce-10.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb04d437-174c-4ece-b621-9cd3b75d2833/design-reduce-10.png'>Large preview</a>" alt="optimization" >}}

### Lesson Learned #8

<p>Working closely with developers is always rewarding. Even in my case, with the same person doing design and development, it's challenging to see all issues right away. I had to actually start building in order to see these functional issues. In any case, try to get the developers involved as soon as possible. You can get a lot of valuable insight about functional things.</p>

## Prepare The Design For Development

<p>Eventually, the design iterations were over. Well, technically speaking, design iterations are never over. So, let’s say we reached a good enough state, where we could move to development.</p>

<p>Before implementing the design, I fixed the spacing of elements, making sure all elements aligned to the 4-pixel guides. This guides-driven mindset will pay off at the development stage.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a99c8985-f0b7-4345-861c-a5ce8bdd01d3/design-reduce-11.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a99c8985-f0b7-4345-861c-a5ce8bdd01d3/design-reduce-11.png'>Large preview</a>" alt="4-pixel guides" >}}

### Lesson Learned #9

<p>When all elements are lined up properly, your development time will significantly decrease. Because I was responsible for development as well, I got all of the properties directly from Sketch. But it definitely makes sense to ensure that all elements are in the right spots, that all colors are from the same palette and that the assets are ready for multiple resolutions.</p>

## Logo And Name

<p>Last but not least, the name for our application came pretty quickly. Two words came to my mind: “reduce” and ”shrink.” I checked a Product Hunt, and “shrink” was already in use, so we went with “reduce.”</p>

<p>The logo was a real struggle for me. Because it’s a menu bar application, I had to create an icon for the menu bar first.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/461cb16e-7c67-457e-8547-3771b56f4151/design-reduce-12.png" sizes="100vw" caption="First menu bar icon iteration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/461cb16e-7c67-457e-8547-3771b56f4151/design-reduce-12.png'>Large preview</a>)" alt="First menu bar icon iteration" >}}

<p>Because the menu bar icon has to be 16 × 16 pixels, it’s better not to use any tiny elements. The icon should be distinctive and legible at the same time.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3891f58a-3f5f-4a50-b1ee-460d664770b2/design-reduce-13.png" sizes="100vw" caption="Second menu bar icon iteration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3891f58a-3f5f-4a50-b1ee-460d664770b2/design-reduce-13.png'>Large preview</a>)" alt="Second menu bar icon iteration" >}}

<p>After several days of fighting with simple shapes, I gave up and opened the <a href="https://fonts.google.com/featured">“Featured” section</a> of Google Fonts. I was looking for a nice curved font that would be a good fit for a logo (as well as for the menu bar icon). Eventually, Pacifico font came into view, and it was perfect for our goals.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72a1d9f0-a027-4d76-a903-9dc1cdd9c889/design-reduce-14.png" sizes="100vw" caption="Final menu bar icon iteration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72a1d9f0-a027-4d76-a903-9dc1cdd9c889/design-reduce-14.png'>Large preview</a>)" alt="Final menu bar icon iteration" >}}

### Lesson Learned #10

<p>Remember that there are two versions of the menu bar in macOS: dark and light. Prepare your menu bar icon for both. Also, test how your icon works with the default selection background. By default, when the user presses on the menu bar icon, macOS will highlight it with whatever color the user has selected in their general settings. (Apple has a great guide on <a href="https://developer.apple.com/macos/human-interface-guidelines/visual-design/color/">colors in macOS.</a>) To test it, I created symbols for all of the default colors, so that I could switch between them and see how the icon looks with different backgrounds.</p>

<div class="video-container"><iframe loading="lazy" data-
src="https://player.vimeo.com/video/251144081"
  width="640" height="360" frameborder="0"
  webkitallowfullscreen mozallowfullscreen allowfullscreen>
</iframe></div>

<p>Using accent colors from the initial color palette, I put an “R” in a circle with a tiny curved border. At that point, the logo was good enough for me.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6678574b-bd48-499d-b836-0a0d893fa6a2/design-reduce-15.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6678574b-bd48-499d-b836-0a0d893fa6a2/design-reduce-15.png'>Large preview</a>" alt="logo" >}}

## Conclusion

<p>There is still a lot of room for improvement. As I mentioned, design iteration never ends. But if you keep iterating forever, the product will stay as a mockup forever. Shipping fast is better. Short iterations mean faster feedback, and faster feedback means a better product. The Reduce app was made in a week and a half because our main objective was to make it fast and useful.</p>

<p>We received plenty of positive feedback from our team. It turns out that the menu bar application is much faster and more understandable to use than the Terminal script. Also, during our public launch, the community gave us a lot of ideas for features we could implement next and how we can improve the app.</p>

<p>Here is a wrap up of the things we learned in creating the Reduce app:</p>

<ul>
<li>Think about the product's goals and use cases before doing any wireframes or prototypes.</li>
<li>Use a tool such as <a href="https://color.adobe.com/">Adobe Color</a> and <a href="https://khroma.co">Khroma</a> to choose the right color palette faster. A <a href="https://blog.marvelapp.com/color-ui-design-practical-framework/">basic understanding of the HSB color system</a> will also help.
</li>
<li>Don't be afraid to experiment with custom fonts.</li>
<li>Every platform has its own set of standards. Learn them before designing.
</li>
<li>Use a prototyping tool to get a sense of the complete flow.</li>
<li>Don't overwhelm your design with custom elements. Sometimes it's better to stick to the default controls for the given platform.
</li>
<li>Get feedback on your design as early as possible.</li>
<li>Get the developers involved as early as possible. You can get a lot of valuable insight about functional elements and about how much time it would take to implement that “little gradient button with the spiral animation.”
</li>
<li>Use a platform-standard grid to line up all elements. The developers will thank you for it later.
</li>
<li>Test your design for different use cases (like a light and dark menu bar) before finalizing the UI.</li>
</ul>

<p>If you feel that the Reduce app could simplify your life as well (and your Sketch files), you can <a href="https://flawlessapp.io/reduce">download it for free</a>. And please give us some feedback. We believe it’s the most valuable thing one can get from users.</p>

{{< signature "ra, al, yk, il" >}}

