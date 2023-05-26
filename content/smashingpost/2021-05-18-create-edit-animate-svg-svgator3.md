---
title: 'How To Create, Edit And Animate SVGs All In One Place With SVGator 3.0'
slug: create-edit-animate-svg-svgator3
author: mikolaj-dobrucki
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e69194b-9e57-4713-bed2-d2f18dd6c914/create-animate-svg-graphics-svgator3-image-7.png
date: 2021-05-18T10:30:00.000Z
summary: >-
  Today, we are taking a closer look at [SVGator 3.0](https://www.svgator.com/?utm_source=article&utm_medium=smashingmag&utm_campaign=svgator3_smashing), a new major release of the popular SVG application that lets you create, edit and animate SVG files and make the best out of what SVG has to offer &mdash; from start to finish.
description: >-
  Today, we are taking a closer look at [SVGator 3.0](https://www.svgator.com/?utm_source=article&utm_medium=smashingmag&utm_campaign=svgator3_smashing), a new major release of the popular SVG application that lets you create, edit and animate SVG files and make the best out of what SVG has to offer &mdash; from start to finish.
categories:
  - SVG
  - Apps
  - Graphics
  - Animation
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: SVGator
  link: https://www.svgator.com/?utm_source=article&utm_medium=smashingmag&utm_campaign=svgator3_smashing
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51a44025-8df4-4ccc-81be-9225b6b1a449/svgator-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.svgator.com/?utm_source=article&utm_medium=smashingmag&utm_campaign=svgator3_smashing">SVGator</a> who are passionate about designing and producing unique, high-quality, and unforgettable animations. <em>Thank you!</em>
---

SVGator is evolving and it’s evolving a lot. Three years ago, we published a comprehensive introduction to the basic use of SVGator. At that time it was an app meant solely for animating SVG files created in other apps. [Two years ago](https://www.smashingmagazine.com/2019/06/unleash-power-path-animations-svgator/), we introduced you to a new version of SVGator and its improved animation capabilities. This time, we are introducing a [new major version of SVGator](https://www.svgator.com/?utm_source=article&utm_medium=smashingmag&utm_campaign=svgator3_smashing) that offers a matured, complete environment for drawing from scratch and animating SVG graphics.

**Note**: *Some of the SVGator’s features covered in this tutorial are paid. On the free plan, you can create and export an unlimited number of SVG graphics. You can also use basic animation features and export 3 animations per month. Advanced animation features are available under a paid plan, starting at 11 USD/month.*

In this article, we will follow a process of creating a custom SVG loader, from drawing it from scratch and applying various visual effects, through creating different types of animations, to exporting your file and preparing it for use on the web.

{{< vimeo id="551556487" caption="A custom loader made with pure SVG, drawn and animated in SVGator." breakout="true" >}}

We begin by creating a new blank file and changing its background color.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470e81f5-a6a2-4540-b7a5-83f1f8984a5b/create-animate-svg-graphics-svgator3-image-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470e81f5-a6a2-4540-b7a5-83f1f8984a5b/create-animate-svg-graphics-svgator3-image-1.png" width="800" height="" sizes="100vw" caption="Changing the color of the canvas. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470e81f5-a6a2-4540-b7a5-83f1f8984a5b/create-animate-svg-graphics-svgator3-image-1.png'>Large preview</a>)" alt="Changing the color of the canvas" >}}

From here, we can start drawing the illustration we are going to animate later. SVGator allows you to draw all the standard SVG shapes such as ellipses, rectangles and polygons as well as use a Pen and Pencil tools to draw your own. You can also use boolean functions to combine shapes with one another.

To make it easier for me to create the desired shape, I started by drawing a circle as a guide in the center of the canvas. Fortunately, SVGator makes it dead simple to align and measure elements, thanks to a smart system of guides and snapping functions. You can also use grids and rulers for better precision and fidelity.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cea4626-fa91-4799-b423-6f52ed4f077a/create-animate-svg-graphics-svgator3-image-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cea4626-fa91-4799-b423-6f52ed4f077a/create-animate-svg-graphics-svgator3-image-2.png" width="800" height="" sizes="100vw" caption="Using smart guides to align the circle to the centre. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cea4626-fa91-4799-b423-6f52ed4f077a/create-animate-svg-graphics-svgator3-image-2.png'>Large preview</a>)" alt="Using smart guides to align the circle to the centre" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cf132d8-d812-4828-bafd-3ea0411d00e9/create-animate-svg-graphics-svgator3-image-3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cf132d8-d812-4828-bafd-3ea0411d00e9/create-animate-svg-graphics-svgator3-image-3.png" width="800" height="" sizes="100vw" caption="Did you know? Apart from basic shapes and drawing functionalities, SVGator also offers a library of premade assets to fasten your workflow. You can choose from a vast variety of shapes, icons and illustrations. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cf132d8-d812-4828-bafd-3ea0411d00e9/create-animate-svg-graphics-svgator3-image-3.png'>Large preview</a>)" alt="Did you know? Apart from basic shapes and drawing functionalities, SVGator also offers a library of premade assets to fasten your workflow. You can choose from a vast variety of shapes, icons and illustrations" >}}

Next, using a Pen Tool, we draw the first blob roughly following the shape of the circle underneath. The Pencil Tool would also do well for that purpose. What is really cool about this one is that SVGator’s Pencil Tool usually creates shapes with much fewer node points than comparable tools in other apps, which makes the result not only look smoother but also be much lighter on file size.

{{< vimeo id="551558599" caption="Using a Pen Tool to draw a blob shape. Note that as you keep adding new points to the path, you can always modify the already existing points and curves on the fly by moving and dragging them. No need to get in and out of the drawing mode to adjust the lines you already created." breakout="true" >}}

Creating and editing shapes in SVGator might feel a bit different than in other vector tools but once you’ve got used to it, it’s truly a breeze. It’s also important to note that all the drawing features of SVGator are completely free so you can use it as your SVG-creating software as much as you want for no cost. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d75be929-493d-4402-a811-32626ab6f30d/create-animate-svg-graphics-svgator3-image-4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d75be929-493d-4402-a811-32626ab6f30d/create-animate-svg-graphics-svgator3-image-4.png" width="800" height="" sizes="100vw" caption="If you need more space for drawing you can easily hide and show the app’s sidebars by pressing. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d75be929-493d-4402-a811-32626ab6f30d/create-animate-svg-graphics-svgator3-image-4.png'>Large preview</a>)" alt="If you need more space for drawing you can easily hide and show the app’s sidebars by pressing" >}}

With a first blob ready, it’s time to style it a bit. Here, we’re stumbling upon one of the biggest competitive advantages of the app. Other popular vector graphics applications that allow you to export SVG files usually have to leverage their features to fit a plethora of formats and use cases. At the same time, apps focused primarily on user interfaces, cater mostly for what’s possible with HTML and CSS properties, rarely giving much love to SVG-specific features such as stroke markers or filters.

SVGator, being solely aimed at creating SVG files, takes full advantage of what this format, in particular, has to offer. This includes options specific to how SVG handles strokes, fills, gradient elements (have you heard about the `spreadMethod` attribute of SVG gradients?), filters (such as blur, shadow or sepia), and many others.

It also allows you to style (your fills, strokes, effects, and so on) with confidence that the final result will be as expected, as all these features have been created especially for SVG files. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5159a85-f112-4fce-821a-bc6f0f441ab2/create-animate-svg-graphics-svgator3-image-5.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5159a85-f112-4fce-821a-bc6f0f441ab2/create-animate-svg-graphics-svgator3-image-5.png" width="800" height="" sizes="100vw" caption="Modifying the gradient fill of the shape. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5159a85-f112-4fce-821a-bc6f0f441ab2/create-animate-svg-graphics-svgator3-image-5.png'>Large preview</a>)" alt="Modifying the gradient fill of the shape" >}}

In our case, a single gradient fill and a gradient stroke will do. I also applied a light blur filter on the element as a final touch. Notice that as SVGator uses native SVG filters instead of CSS, it allows you to control the blur properties for both axes separately. In this case, I only applied an x-axis blur. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b809a5d-b0dc-4465-8e2e-25cbbfdf5186/create-animate-svg-graphics-svgator3-image-6.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b809a5d-b0dc-4465-8e2e-25cbbfdf5186/create-animate-svg-graphics-svgator3-image-6.png" width="800" height="" sizes="100vw" caption="Adding a filter to the selected object. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b809a5d-b0dc-4465-8e2e-25cbbfdf5186/create-animate-svg-graphics-svgator3-image-6.png'>Large preview</a>)" alt="Adding a filter to the selected object" >}}

Next, we can duplicate the blob and use the Pen Tool again to create two more different blobs. The way Pen Tool works makes it really easy to modify the shape without losing the smooth, continuous line of it.

{{< vimeo id="551563162" caption="Playing with the shapes to get a few different irregular shapes" breakout="true" >}}

As a final element of the illustration, we add a few randomly placed glowing dots. They are no more than circles with a gradient fill applied.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e69194b-9e57-4713-bed2-d2f18dd6c914/create-animate-svg-graphics-svgator3-image-7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e69194b-9e57-4713-bed2-d2f18dd6c914/create-animate-svg-graphics-svgator3-image-7.png" width="800" height="" sizes="100vw" caption="Using ellipses with a gradient fill to create glowing sparkles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e69194b-9e57-4713-bed2-d2f18dd6c914/create-animate-svg-graphics-svgator3-image-7.png'>Large preview</a>)" alt="Using ellipses with a gradient fill to create glowing sparkles" >}}

Our loader in its initial state is ready. Now, it’s time for the most fun part: animation! 

It doesn’t really matter which element of the illustration we will animate first. In my case, I started with animating the sparkles. By adding a Position animator to each element, we can create complex path animations. Path animations allow us to make an element follow a path of any shape over time. In our case, will make the sparkles circulate around the canvas to create an impression of flying around the center elements of the illustration. We can also use Scale and Opacity Animators to make the sparkle seem to wander further and closer from the viewer and strengthen an illusion of movement in 3-dimensional space. 

{{< vimeo id="551564681" caption="Creating a path animation for one of the sparkles." breakout="true" >}}

**Note**: *If you’d like to learn more about creating path animations I would recommend watching this tutorial: “[Motion Path Animation &mdash; Animate Any Object Along a Custom Path](https://www.svgator.com/tutorials/motion-path-animate-any-object-along-a-custom-path).”*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebca4fc-e0f8-4590-a598-189487bcea1c/create-animate-svg-graphics-svgator3-image-8.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebca4fc-e0f8-4590-a598-189487bcea1c/create-animate-svg-graphics-svgator3-image-8.png" width="800" height="" sizes="100vw" caption="The final path of one of the sparkles to follow. My goal was to give an impression of the sparkle flying around the blobs in the middle. Combining the path animation with minor adjustments to size and opacity helps to make the element seem to change its distance from the viewer and make an impression of circling around the blobs, once being on top of them and then behind them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebca4fc-e0f8-4590-a598-189487bcea1c/create-animate-svg-graphics-svgator3-image-8.png'>Large preview</a>)" alt="The final path of one of the sparkles to follow. My goal was to give an impression of the sparkle flying around the blobs in the middle" >}}

To animate the blobs, a Morph animator can be used. It allows us to modify a shape in time and create smooth transitions between those states. To achieve a nice, clean transition between two shapes, we add a keyframe to the Morph animator’s timeline and modify the shape with a Pen Tool &mdash; just like we did when we drew the additional blobs.

{{< vimeo id="551565809" caption="Creating a morphing animation of the blob." breakout="true" >}}

If you’d like to learn more about creating morph animations, this tutorial not only will introduce you to the basics but also take it to a whole new level: “[Advanced Morph Animation Tutorial](https://www.svgator.com/tutorials/advanced-morph-animation).”

An important part of each and every animation is its timing function. For sparkles, I mostly used Ease In Out timing functions. That allows the dots to slow down when they reach a narrow turn of the orbit and speed up on straight stretches, helping the movement to look closer to what it would seem in such a perspective of multi-dimensional space. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d907aa6-c662-4228-bc43-18462865219d/create-animate-svg-graphics-svgator3-image-9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d907aa6-c662-4228-bc43-18462865219d/create-animate-svg-graphics-svgator3-image-9.png" width="800" height="" sizes="100vw" caption="A timing function used for the sparkles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d907aa6-c662-4228-bc43-18462865219d/create-animate-svg-graphics-svgator3-image-9.png'>Large preview</a>)" alt="A timing function used for the sparkles" >}}

For blobs, I also used an Ease In Out function. You can notice that both timing functions are different from how Ease In Out functions look like by default. I “sharpened” them up a bit using the bezier curve interface. This allowed me to make the movements look smooth and natural, without sudden turns and hiccups but also without too visible slowdowns.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b211c47a-e64b-4ce6-9484-f89511d87172/create-animate-svg-graphics-svgator3-image-10.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b211c47a-e64b-4ce6-9484-f89511d87172/create-animate-svg-graphics-svgator3-image-10.png" width="800" height="" sizes="100vw" caption="A timing function used for the blobs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b211c47a-e64b-4ce6-9484-f89511d87172/create-animate-svg-graphics-svgator3-image-10.png'>Large preview</a>)" alt="A timing function used for the blobs" >}}

After a few more minor adjustments, the file is ready to be exported. The new version of SVGator combines the preview functionality with exporting functionalities. Thanks to that you can have a real-time browser preview of your animations while you are also testing and changing the export settings.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/221840a9-e9f5-40f8-a611-6d813e073f2f/create-animate-svg-graphics-svgator3-image-11.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/221840a9-e9f5-40f8-a611-6d813e073f2f/create-animate-svg-graphics-svgator3-image-11.png" width="800" height="" sizes="100vw" caption="The export window of SVGator (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/221840a9-e9f5-40f8-a611-6d813e073f2f/create-animate-svg-graphics-svgator3-image-11.png'>Large preview</a>)" alt="" >}}

In our case, we want the animation to act as an infinite loop. You can also control the behavior of the graphic, to show on load or upon user’s action such as click or scroll. 

The exported file perfectly matches the animation we created within the app and is ready to use on the web.

{{< codepen height="480" theme_id="light" slug_hash="wvJzWgp" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [SVGator Loader](https://codepen.io/smashingmag/pen/wvJzWgp) by <a href="https://codepen.io/mikolajdobrucki">Mikołaj</a>.{{< /codepen >}}

I hope you enjoyed this article and that it will inspire you to create the most amazing things with SVG in your work!

Where next? Below you can find a few useful resources to continue your journey with SVG and SVGator:

- [SVGator tutorials](https://www.svgator.com/tutorials)  
*A series of short video tutorials to help you get started with SVGator.*
- [SVGator Help Centre](https://www.svgator.com/help)  
*Answers to the most common questions about SVGator, its features, and membership plans.*
- [Unleash The Power Of Path Animations With SVGator](https://www.smashingmagazine.com/2019/06/unleash-power-path-animations-svgator/)  
*An extensive introduction to path animations and how to create them with SVGator.*

{{< signature "vf, il" >}}
