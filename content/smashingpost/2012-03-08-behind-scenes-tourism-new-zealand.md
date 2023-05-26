---
title: Behind The Scenes Of Tourism New Zealand (Case Study)
slug: behind-scenes-tourism-new-zealand
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ac71e0c-7240-4cbc-919b-4c00b140e4df/newzealand-homepage.jpg
date: 2012-03-08T23:32:10.000Z
author: richard-shepherd
description: >-
  In 2011 we saw the rise in popularity of two relatively new trends: responsive
  Web design and the use of HTML’s canvas. While some websites had experimented
  with both, in the last 12 months we’ve seen these trends move from the fringes
  firmly into the mainstream.
categories:
  - Inspiration
  - Showcases
  - Design
  - Web Design
---
In 2011 we saw the rise in popularity of two relatively new trends: responsive Web design and the use of HTML’s canvas. While some websites had experimented with both, in the last 12 months we’ve seen these trends move from the fringes firmly into the mainstream.

Responsive Web design is more a concept than a technology — an ideal that many new websites aspire to. Canvas, on the other hand, is an HTML5-based technology that opens the door to a new wave of interactivity. In this article, we’ll look at a website that embraces both of these elements, one that has been nominated for a Technical Achievement award at SxSW Interactive 2012: [Tourism New Zealand](https://www.newzealand.com/int/).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [75 Instructive Case Studies – This Is How We Built It](https://www.smashingmagazine.com/2013/07/this-is-how-we-built-it-case-studies/)
*   [Showcase of Case Studies in Design Portfolios](https://www.smashingmagazine.com/2009/09/showcase-of-case-studies-in-design-portfolios/)
*   [15 Impressive Case Studies from Behance](https://www.smashingmagazine.com/2009/11/15-impressive-case-studies-behance/)
*   [Improving Smashing Magazine’s Performance: A Case Study](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

I spoke with the creative and technical teams at the New Zealand-based firms [Shift](https://www.shift.co.nz) and [Assembly](https://www.assemblyltd.com/) about the technology behind Tourism New Zealand’s home page, how it was made and how they balanced the breakthrough effect with bandwidth.

{{% feature-panel %}}

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd461a2-a27a-4776-8458-01294b8ebaa3/newzealand-homepage.png "NewZealand.com Homepage")

After we learn how Tourism New Zealand was built, we’ll look at the basics of putting together your own animated HTML5 canvas background.</p>

## The Inspiration

Tourism New Zealand has a history of strong media and advertising campaigns, particularly through TV commercials, and its destination marketing website has long featured these videos.

So, when a redesign of the website was planned without an accompanying TV commercial, the team at Shift had a new challenge: to showcase the landscape and breadth of activities in New Zealand to an audience that has come to interact with a website, not to watch a video.

Shift was inspired by, among other things, Nike’s Better World website (which [Smashing Magazine has covered](https://www.smashingmagazine.com/2011/07/12/behind-the-scenes-of-nike-better-world/)). But whereas that website used HTML5 animation to create an effect of parallax scrolling, Shift proposed a camera view that moves through the real world.

Shift’s first idea was to use video as a background, with the camera descending through some of New Zealand’s most exciting locations. The problem was bandwidth: at 25 frames per second, Shift would need to deliver thousands of full-screen frames. This was an impossible goal, so instead the team set a target of around 200 frames for the entire website. But 200 frames for the amount of footage they wanted worked out to about three frames per second, which doesn’t look particularly good.

At this point, they nearly abandoned the idea.

By chance, though, a solution was found. Scrubbing through a QuickTime video, Shift’s creative director, Mark Zeman, noticed that being able to control the frame rate as you move the play head gives the illusion of a smooth experience. He suspected that if the browser’s scroll bar could be used to scrub the footage, it would feel similarly smooth. And if the camera shot photographs as it moved through each scene, it would create the illusion that the user was practically controlling the camera as it descended through New Zealand.

The first prototype was made with a few images and some JavaScript, just to prove that the browser could handle this type of manipulation. Freelance front-end developer [Jeff Nusz](https://www.custom-logic.com/) was then tasked with turning this proof of concept into a working website. The brief was simple: no loading bar, and the first frame must load almost instantly. Furthermore, the website had to be usable even when the user doesn’t wait for all of the images to download.</p>

## On Location

With the prototype built and approved by Tourism New Zealand, it was time to load up the trucks with scaffolding and start shooting.

Shift worked with directors Damon Duncan and Matt von Trott of [Assembly](https://www.assemblyltd.com/) throughout development of the project, which enabled them to build the large motion-control rigs that were required for the shoot.

A 15-meter-high motion-control rig was built, with a vertical dolly track that housed a Canon 5D DSLR. The rig was set up at each location, and the camera travelled 12 meters down it, taking anywhere between 750 and 950 stills, a process that lasted at least two hours each time (and six hours at Milford Sound, the first location on the website), because the camera moved around 15 millimeters every 10 seconds.

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/def48549-7da7-4079-b6cc-79f3c1991e6c/milford-5.jpg "Milford Sound")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/def48549-7da7-4079-b6cc-79f3c1991e6c/milford-5.jpg)
_[Milford Sound](https://www.google.com/url?q=http%3A%2F%2Fwww.newzealand.com%2Fint%2Fmilford-sound%2F&sa=D&sntz=1&usg=AFQjCNFtSKivraHHvXVddMjjMVJXVZgIHA), New Zealand_

Each location took three days to shoot. The first day was spent building the tower and putting together the motion-control rig. The second day was usually spent rehearsing the scene, and the third would be for the actual shoot, which included multiple passes of the scene. Indeed, the scene for Waiheke Island is a combination of two takes.

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/36803041" width="550" height="309" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen=""></iframe>
_Time-lapse sequences from all four shoots ([watch on Vimeo](https://vimeo.com/36803041))_

Front-end developer Jeff Nusz had built a suite of tools to help the crew plan the photography. The directors also showed the original prototype to the cast and crew, which helped to demonstrate what they were filming and how the time-lapse footage would work.

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89b8abe1-568a-46c4-a74e-6db4bed0dbb0/waitomo-4.jpg "Waitomo")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89b8abe1-568a-46c4-a74e-6db4bed0dbb0/waitomo-4.jpg)

## Post-Production

There were only five days between the final day of shooting and the launch of the website. Most of the code had been written and ported to JavaScript using prototype images, and so it was now a matter of editing the hundreds of photos from each location down to 200 hand-optimized 1280 × 720-pixel frames.

The team spent time testing the website in each browser, noticing different memory quirks in Chrome and Firefox, and it worked on optimizing the website’s performance. Because many of New Zealand’s tourists come from China, the time was also spent making sure the website worked even in IE 6\. To better understand the toll of such a heavy home page, Shift used [WebPagetest](https://www.webpagetest.org/) to test it from various parts of the globe.</p>

## From 25 MB To 300 KB

Although the entire website weighs in at 25 MB, it enables a usable experience after the first 300 KB of data and images have loaded.

On the initial loading of the page, a 40 KB image is loaded that contains all 200 frames at a very low resolution. This means that as soon as the initial frame of Milford Sound has loaded, you can scrub through the entire website and get some approximation of the full experience. Then, when you stop scrubbing, the website loads the frame you’re on and starts loading the frames before and after it. Moreover, as you scroll the page, all downloading activity stop to ensure the smoothest possible scrolling experience. When you stop scrolling, all downloading resume.

Interestingly, Jeff’s background is mainly in working with Flash, so the initial website was built in Flash and then ported to HTML5 at the last minute. Jeff says that the similarities between ActionScript and JavaScript made this a relatively pain-free process:

<blockquote>
<p>ActionScript 3 is a lot like JavaScript. I did a lot of the work in Flash, and I wanted to see how well it would translate, and it was pretty much cut-and-paste for the most part. I just had to structure things in a similar way and make a few semantic changes. Ninety percent of the code ported as it was, which was great.</p>
</blockquote>

One of the team’s early breakthroughs was in figuring out how to split up the website’s elements. You can see in the sketch below how a website normally works: you have a long page and, conceptually speaking, the browser’s viewport moves up and down the page (i.e. the latter moving across the former).

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f338317-0d7f-4333-ae2d-66fbe0770314/scrolling-1.jpg "Traditional Scrolling")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f338317-0d7f-4333-ae2d-66fbe0770314/scrolling-1.jpg)

In this next sketch, the page itself is a giant empty GIF that you scroll up and down; but the website detects every time you scroll, calculates your position and then translates that to the frame you should be on. The height of the window also changes depending on how big your browser’s viewport is, because if the page is huge and your viewport is small, then the scroll bar would be tiny; Shift wanted to keep the size of the scroll bar consistent, regardless of the browser’s size.

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7a4ef55-61c6-4967-bfe6-66873933ba1c/scrolling-2.jpg "New scrolling paradigm")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7a4ef55-61c6-4967-bfe6-66873933ba1c/scrolling-2.jpg)

As Jeff notes, “Although it’s not exact, the goal was that one click of your mouse-wheel would be one frame”:

<blockquote>
<p>The tag layer and the UI layer is just HTML and CSS, but the background is either an HTML5 canvas that we draw to or it’s Flash. There’s about a 20-millisecond lag between the frames moving and the background changing in Flash, so the canvas version became the primary method used for browsers that support it.</p>
</blockquote>

The tags do not scroll in the conventional sense, but for each frame, they are assigned specific x and y coordinates based on the frame. This allows tags to be “glued” to background elements — a tree, mountain top, etc. — and these coordinates would be recalculated on the fly if the browser window was resized.

To create this effect, the team used Adobe After Effects to keyframe each tag and output the coordinates. Jeff built a PHP script into which the team could copy and paste the After Effects keyframe data, whereupon the script would generate JavaScript that the website could use. Jeff then tweaked the tags in JavaScript to make sure they scrolled as expected.

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14404044-8e85-4550-b835-a3fa949965ac/ae-shot2.jpg "Keyframing in After Effects")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14404044-8e85-4550-b835-a3fa949965ac/ae-shot2.jpg)

## Sprite Sheets

To create the illusion that the page loads quickly, Jeff came up with the idea of using sprite sheets. As he puts it, “The sprite sheets were the breakthrough that allowed us to make the website usable so quickly after the page loads”.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17757e7f-872e-46f2-91d1-c55a7a972783/sprite-96-0.jpg "Sprite Sheet")

The first frame (of the background image) is 90 KB. So, together with the first low-resolution sprite sheet (which is 30 KB), these images initially weigh only 130 KB. Once the page has loaded all of the content, it loads a higher-resolution sprite sheet, and then another, and then it loads in the full-resolution images one by one. Rather than loading these large images in sequence, it loads them based on your scroll position within the document.

You can check that the sprite sheets load before the full-resolution images by turning the Webkit Inspector on and watching the “Network” activity after the page has started to render.</p>

## Using Inline JavaScript

I asked the team at Shift why so much inline JavaScript was in the head of the document. Best practice would suggest it should be moved to a separate file. However, something more is going on here.

Shift’s solution architect, Glenn Wright, has been working on the website for the last six years. He explains:

<blockquote>
<p>The inline JavaScript is there to define the configuration for each page. We can cache each page’s configuration in JavaScript, then all the external libraries that the page loads utilize that data. It gives us an easy way to configure the responsive grid and all of the interactions that the page will have to use.</p>
</blockquote>

## Testing Mode

A testing mode on the website lets you see some of this loading process in action. Clear your browser’s cache, load Tourism New Zealand’s home page, and then hit the tilde (~) key five times to enable testing mode. You won’t see any change immediately, but once in this mode you can use the following keyboard commands:

*   `1`
    Turn on the visualizer for “frames loaded”
*   `3`
    Toggle tags on and off
*   `0`
    Toggle the high-resolution image on and off
*   `-`
    Go to the previous low-resolution sprite
*   `+`
    Go to the next high-resolution sprite

## Building Your Own Canvas Background Animation

While websites like Tourism New Zealand take months to design and build, creating your own animated canvas background is relatively straightforward. All it takes is a little JavaScript, a pinch of HTML5 and an enormous amount of imagination to dream up a worthwhile use.

Indeed, a word of caution is in order. We all know that with great power comes great responsibility, and just because we can load 50 high-resolution frames and animate them as the user scrolls the window doesn’t mean we should. As mentioned earlier, websites that use this technique are both lauded and criticized. Make sure that you are enriching the user experience rather than needlessly slowing it down.

First, we need to do a couple of things. Let’s grab some video (a time-lapse video works best for this), and then create our 50 frames. You can create as many frames as you like, but we’ll stick with 50 because this is how many Tourism New Zealand uses for each scene.

Next, let’s grab some royalty-free time-lapse footage from [Artbeats](https://www.artbeats.com/) and import it into iMovie, where you can export individual frames.

Choose `Share → Export Using QuickTime`, and in the pop-up dialog box select “Movie to Image Sequence.”

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/372f0090-658e-4e0a-b189-13cdd0db56d2/screen-shot-2012-01-27-at-13.41 "Export to Image Sequence")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/372f0090-658e-4e0a-b189-13cdd0db56d2/screen-shot-2012-01-27-at-13.41)

We export the images as JPEGs, which leaves us with hundreds of images. So, we have to do two things:

1.  Batch process the images in Photoshop to the required size (here, we went with 480 × 270 pixels to maintain the aspect ratio).
2.  Edit the number of images down to 50\. Shift was painstaking in doing this, retouching and editing thousands of images down to just 200\. To keep things easy for this tutorial, let’s just delete three photos out of every four.

You should now have 50 photos that, when played in sequence, make for a somewhat choppy time-lapse video.

On to the next couple of steps. First, we’ll figure out how to load the images in the browser and control them with the scroll bar. Secondly, we’ll create our own sprite sheet and use that instead. Open your code editor of choice, and create a new JavaScript file. Or why not head over to GitHub and [download the project](https://github.com/richardshepherd/Canvas-Background) to play around with?

You’ll also need an HTML file with a canvas element in it, which is as simple as this:

<pre><code class="language-markup tmp-html">&lt;canvas id="canvas"&gt;&lt;/canvas&gt;</code></pre>

Hopefully, the comments in the code sufficiently explain what’s going on, but here’s a breakdown anyway.

First, we set up the canvas element and use some basic maths to set start and end points:

<pre><code class="language-javascript">// Create our timeLapseVideo object and cache the window object
timeLapseVideo = new Image();
$window = $(window);

// Define the timeLapseVideo element
timeLapseVideo.onload = function(){
  videoContainer.width = 960;
  videoContainer.height = 540;
  videoContext.drawImage(timeLapseVideo, 0, 0, 960, 540);
}

// Load the first frame
timeLapseVideo.src = 'images/TimeLapse001.jpg';

// Calculate how far to scroll before changing a frame
var scrollDistance = $window.height() - $window.scrollTop(),
    totalHeight = $(document).height() - scrollDistance;
    frameDiff = totalHeight / (numberOfFrames - 1);</code></pre>

Then, when the window scrolls, we work out which frame needs to appear on screen:

<pre><code class="language-javascript">// Which frame do we need to show?
frameString = (Math.round($window.scrollTop()/frameDiff) + 1).toString();

// Change the image in the canvas
timeLapseVideo.src = 'images/TimeLapse' + frameString + '.jpg';</code></pre>

Make sure to go through the [full source code](https://github.com/richardshepherd/Canvas-Background) to see it in action. Be careful, because there is no check to determine whether an image has already loaded; you could end up hitting your server with hundreds of requests per page. So, like Tourism New Zealand, you need to build in a check to see whether an image has been cached.</p>

## Creating And Using A Sprite Sheet

We can also create our own sprite sheet with our image to emulate more of Tourism New Zealand’s behavior. Some apps and websites are available to help you do the job (see the “Related Links” section at the end), but it’s probably easier to run a simple script that pastes all of the images onto a canvas and then take a plain screenshot of that. The code for this script is [in the GitHub repository](https://github.com/richardshepherd/Canvas-Background) in case you want to take a look.

There are two main differences with this technique. First, we load only one image onto the canvas, which is the sprite sheet:

<pre><code class="language-javascript">timeLapseVideo.src = 'images/spritesheet.jpg';</code></pre>

When the window scrolls, we then draw part of this sprite to the canvas:

<pre><code class="language-javascript">videoContext.drawImage(timeLapseVideo, x, y, 80, 45, 0, 0, 960, 540);</code></pre>

In the line above, `x` and `y` are the starting coordinates of the sprite, which in turn are dictated by the frame. We’re using a simple loop to iterate through the sprite to find the right coordinates, but you could set up an array of values to look up. These tiny frames are 80 × 45 pixels, and they are drawn from 0,0 to 960 × 540 pixels. CSS then stretches this canvas to fit the entire window.

You can improve this script a great deal by, for example, preloading images when the user isn’t scrolling (some links are below to point you in the right direction). If you make improvements, please do share your work in the comments below.</p>

## Creativity In Design _And_ Development

Distilling 18 months of hard work into one article like this is an impossible task. Shift had the time and budget to fly around New Zealand and take thousands of beautiful photographs. This is not an option for the average Web designer!

However, what is perhaps most striking about Tourism New Zealand is the imagination in its concept and execution. By taking the leap from virtual to physical world (and back again!), the scroll bar has become a conduit by which the user can control their experience of New Zealand — if only for 200 frames.

Jeff’s ingenious loading techniques and the use of sprite sheets also kept away the loading bar that is so familiar with websites like this. On an average broadband connection, the experience is effortless and fun.

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a26f599-fb89-4ff8-b65e-eae418ea75c2/rotorua-opt.jpg "Rotorua")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faf862cf-e9f8-4813-8c78-4a5756843b24/rotorua-2.jpg)

Perhaps the biggest lesson to be learned here is this. Despite its many bells and whistles, Tourism New Zealand encourages the user to discover the website in much the same way they would discover the country.

Technology supports the great design, not the other way around. If we could all exercise this level of creativity, imagination and user engagement, then we, too, would create amazing websites that shape the future of Web design.</p>

### Related Links

*   “[Blowing Up HTML5 Video and Mapping It Into 3D Space](https://www.craftymind.com/factory/html5video/CanvasVideo3D.html)” (demo), Sean Christmann, Craftymind
*   “[How Browsers Work: Behind the Scenes of Modern Web Browsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/#The_canvas)” (“The Canvas”), Tali Garsiel, HTML5 Rocks Tutorials
*   [HTML5 Canvas Tutorials](https://www.html5canvastutorials.com/)
*   “[Load a Photo in a Canvas, Then Flip](https://www.phpied.com/photo-canvas-tag-flip/),” Stoyan Stefanov, phpied.com
*   “[How to Draw With HTML5 Canvas](https://thinkvitamin.com/code/how-to-draw-with-html-5-canvas/),” Jamie Newman, Think Vitamin
*   “[Preloading Images in HTML5/JavaScript](https://stackoverflow.com/questions/9334083/preloading-images-in-html5-javascript)” (using the canvas), StackOverflow
*   “Using Images” (canvas tutorial), Mozilla
*   Create sprite sheets easily in Mac and PC:
    *   [CSS Sprite Generator](https://spritegen.website-performance.org/), Project Fondue
    *   [Instant Sprite](https://instantsprite.com/), Brian Grinstead
    *   [Texture Packer](https://www.texturepacker.com/), Andreas Löw, code'n'web
    *   [Sprite Sheet Packer](https://spritesheetpacker.codeplex.com/), CodePlex

I must extend my very special thanks to Jeff (@jeffnusz), Glenn, Che and, in particular, Mark (@markzeman), who were patient with my intermittent Skype connection and who were so transparent in offering their thoughts and many of the images and resources featured in this article.

{{< signature "al" >}}

