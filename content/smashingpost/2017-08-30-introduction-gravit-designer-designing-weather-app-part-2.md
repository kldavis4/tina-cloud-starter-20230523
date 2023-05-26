---
title: 'An Introduction To Gravit Designer: Designing A Weather App (Part 2)'
slug: introduction-gravit-designer-designing-weather-app-part-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68618cad-6488-4eb4-b9b9-507db5a63947/gravit-designer-intro-500w-opt.jpg
date: 2017-08-30T19:52:53.000Z
author: christian-krammer
description: >-
  Welcome back to the second part of this tutorial on Gravit Designer. In the
  [first
  part](https://www.smashingmagazine.com/2017/08/introduction-gravit-designer-designing-weather-app-part-1/)
  we took a general look at Gravit and set everything up, created the background
  image in the weather app and the status bar, and then started to make the
  initial elements of the design’s content. Let's continue where we left off.

  Having created the main text layers of the content area in [part
  one](https://www.smashingmagazine.com/2017/08/introduction-gravit-designer-designing-weather-app-part-1/)
  of this tutorial, let’s continue with the weather conditions for the different
  times of day.
categories:
  - Graphics
  - Workflow
  - Tutorials
  - Gravit Designer
---
Let's continue where we left off.</p>

## Sunny With A Chance Of Rain

Having created the main text layers of the content area in [part one](https://www.smashingmagazine.com/2017/08/introduction-gravit-designer-designing-weather-app-part-1/) of this tutorial, let’s continue with the weather conditions for the different times of day.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/934d657d-88f0-462e-a5b3-3511dca17544/fig1-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/869ec447-8056-4655-a44b-b005b2ab62b6/fig1-gravit-design-tutorial-800w-opt.png" width="800" height="675" alt="" /></a><figcaption>Figure 1: The weather app, completed. (<a href="https://www.smashingmagazine.com/2017/08/introduction-gravit-designer-designing-weather-app-part-1/">Go to Part 1</a>)
</figcaption></figure>

{{% feature-panel %}}

Start with a simple circle of 56 pixels in diameter (remember to hold `Shift`), with a white 2-pixel inside border, with no fill outside of the “Status bar” group (figure 1a). Move it to “32” (X) and “368” (Y) in the “Position” fields in the Inspector.

Because we want to reuse this style for other shapes, we will create a new “Shared Style.” This allows you to sync all styling properties between various layers and to update changes with a click. To create a shared style, click on the dropdown field for “Style” in the Inspector that says “No shared style” and select “Create New Shared Style.” Now you can define which properties you want to take over — let’s keep everything checked. For the name, use “Icon outline.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc8d443-f039-4f3f-bfae-01157179f711/fig1a-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/663edeca-6af5-480b-aae0-d7b0c3181da1/fig1a-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 1a: The base for the different weather conditions is a white circle with a border. Create a “Shared Style” in the Inspector, so that you can bring over the styling to other elements. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc8d443-f039-4f3f-bfae-01157179f711/fig1a-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

Let’s turn to the icon itself now, a sun partly covered by a cloud. It consists of various shapes combined into a single form, and a few paths (for the rays).

First, the cloud (figure 2). Draw a rectangle (`R`) with a size of 28 × 14 pixels, with fully rounded corners (“7” — drag the slider all the way to the right) inside the circle. Because aligning the various parts of the icon to the grid wouldn’t make sense, switch it off for now with `Alt + Command + G` (on Windows and Linux, `Alt + Control + G`). Before we continue, use the zoom function with `Z` to zoom into the rectangle so that it’s easier to work on the following steps. If you intend to zoom in with `Command + +` instead, then select the shape beforehand so that Gravit Designer takes it as a reference when zooming and zooms to its center.

**Note:** Before drawing the rectangle, make sure that the circle isn’t selected or else it will take over all of the properties, including the shared style. This is important for when we add new shapes later: If another element is already selected, then all of its properties will be taken over; if nothing is selected, then the new element will be drawn with a default gray fill and no border. That’s also the style you can use for the rectangle for now.

Now add an ellipse (`E`) above the rectangle that is 15 × 15 pixels in size, that is away 3 pixels from the left edge of the rectangle and that juts out 7 pixels at the top. Clone it with `Shift + Command + D` (or, on Windows and Linux, `Shift + Control + D`), resize it to 12 × 12 in the Inspector, and offset it 10 pixels to the right and 3 pixels to the bottom. Looks like a cloud already!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31cffac3-0ed7-4721-a146-2f4991d669ab/fig2-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eb6bd9c-202f-4ec9-8990-ddb2f5d3cd4b/fig2-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 2: The cloud consists of a rectangle with fully rounded corners and two circles. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31cffac3-0ed7-4721-a146-2f4991d669ab/fig2-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

However, we want an outline instead of a solid fill, so we’ll need to bring the “Merge” function into play (also called Boolean operations in other applications, such as Sketch). Select the three shapes and click on “Merge” in the toolbar; this will combine everything into a single form and allow us to assign a border in its entirety later on (figure 3). The advantage here is that you can expand the “Compound Shape” group in the Layers panel and still move the elements individually. It’s even possible to adapt the type of merge function — for example, if you want to cut the right-most circle from the other shapes (“Subtract,” the third option). Have a look at “Boolean” in the Inspector to perform this change. The lesser used types here are “Intersect” and “Difference,” which just show the part where the shapes overlay or the exact opposite, respectively.

With the “Compound Shape” group selected, change from a fill to a white inside border with 1.5 pixel thickness. Remember that you can alter the position of the border in the “Advanced stroke settings.” Now it will become immediately apparent what the Merge function has done to the shapes.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb82a0b9-b77d-468a-8f92-7681f4eaa2c0/fig3-gravit-design-tutorial.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb82a0b9-b77d-468a-8f92-7681f4eaa2c0/fig3-gravit-design-tutorial.gif" width="600" height="338" alt="" /></a><figcaption>Figure 3: The “Merge” function combines multiple elements into a single shape but still allows you to modify them individually. After you have “merged” the shapes of the cloud, apply a white border. (Click to play <a href="https://vimeo.com/230184786">video</a>)
</figcaption></figure>

Complete the cloud by giving it a proper name.

On to the sun now. Create another circle with a 12-pixel diameter outside of the other big circle. With the cloud still selected, this will take over the styling. This time, however, we need a centered border (you will see why later). Switch to the Line tool with `L` and draw a vertical one 3 pixels in length above the circle. Make sure that the circle is already selected (to take over the styling yet again), and hold `Shift` while drawing to constrain the movement. The line should be centered to the circle horizontally and have a gap of 4 pixels in the vertical direction.

**Note:** To directly transfer the styling from one element to another, proceed as follows: Select the root element, press `Command + C` (on Windows and Linux, `Control + C`), click on the layer (object) that you want to take the styling over to, and hit `F4`. Done! Try it — it's a nice little time-saver!

## A Ray Of Light

How do we do the other rays now? We need to combine two techniques here (figure 4). An integral part is the “Transform” function in the top section of the Inspector, which is quite a handy tool to apply transformations to objects. It allows you not only to move, rotate and skew objects by a certain amount, but also to resize a layer relatively with percentages.

The thing that interests us most with the Transform feature at the moment, however, is the ability to adapt the rotation point of a shape — the orange rhombus at the center of the line. It defines the point around which a shape is rotated. To continue, perform the following steps:

1.  Clone the line (Mac: `Shift + Command + D`, Windows and Linux: `Shift + Control + D`) while it is selected.
2.  Switch to the Transform tool with a click on the button in the Inspector.
3.  Drag the rotation point (the orange rhombus) down so that it is at the center of the circle.
4.  Hold `Shift` to trigger the rotation mode, and drag the line until the “Angle” field in the Inspector says “-45°.” You might need to release `Shift` again to catch this exact value.

This rotated line will be the reference for the other rays. First, select and duplicate the initial unrotated line again, but this time with `Command + D` (on Windows and Linux, `Control + D`). Then, bring this duplicate to the exact same position and rotation as the other line we just adapted with the Transform function: Drag it there, and rotate it with the “Angle” field in the Inspector. (You might also need to switch off “Snap” in the toolbar for this to work.)

Now press `Command + D` again until all remaining six rays appear. You might need to align them individually afterward, so that all have the same distance and alignment. Also, delete the duplicate of the second ray.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1724593b-d102-4e3e-96a2-34ed61439869/fig4-gravit-design-tutorial.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1724593b-d102-4e3e-96a2-34ed61439869/fig4-gravit-design-tutorial.gif" width="600" height="338" alt="" /></a><figcaption>Figure 4: Use the “Transform” feature to change the rotation point of the line, so that it can be duplicated around the circle. (click to play <a href="https://vimeo.com/230185564">video</a>)
</figcaption></figure>

As with the cloud, we want to combine all of the elements of the sun into a single shape so that we are able to style it as a whole. Select everything (ideally in the Layers panel), and click on “Merge” again in the toolbar. Alternatively, you can press `Command + M` (on Windows and Linux, `Control + M`). Rename this group to “Sun.”

**Note:** Please make sure that the lines (i.e. the rays) are above the circle in the layer hierarchy. The styling of the bottom-most layer is always applied to the other layers when you use the “Merge” function.

One final touch is left for the sun: rounded ends for the rays. Open “Advanced stroke setting” in the Inspector again, and select the second option (“Round”) in “Ends.” Looks great!

The individual parts of the icon (the sun and cloud) are ready now, so let’s bring them together somehow. Be sure to switch on the snapping again in the toolbar. First, bring the sun to the top-right corner of the cloud, then move it about 9 pixels to the top and 8 pixels to the right with the arrow keys on the keyboard.

Now, clone both weather symbols so that we have a backup for later (Mac: `Shift + Command + D`, Windows and Linux: `Shift + Control + D`). Note: When selecting two groups, you might want to press `Command` (on Windows and Linux, `Control`) instead of `Shift`, to have everything working correctly. While the second sun can be hidden (use the eye symbol in the Layers panel), we will need to manipulate the copy of the cloud for the further steps. (see figure 5 for all of the steps.)

Right-click on the cloud shape and select “Convert to Path,” which will create a path with individual points instead of the compound shape. We also need to do something similar for the sun, but instead of converting the shape itself, we want to transform its border to a path. This is also possible with a right-click on the shape, but with “Vectorize Border.”

Now you can combine these two elements again to create the partly covered sun: Select both, click on the arrow next to the “Merge” icon in the toolbar, and pick “Subtract.” Just make sure that the sun is _behind_ the cloud in the layer hierarchy.

Name this new icon “Sun” again, and delete the rays that overlap with the cloud. The easiest way is to use the Lasso tool. It can be used to draw a selection of multiple vector points — which is quite different to how a Lasso tool will perform in other applications (like Photoshop, for example, where it serves to select parts of a bitmap image).

To use it for the removal of the rays, pick the “Compound Path” within the sun group, switch to the Lasso tool with `O`, and drag a selection around the redundant rays. Then, delete them with `Backspace` (on Windows and Linux, `Delete`).

Finally, combine this glimpse of the sun with the copy of the cloud into a group named “Cloudy,” and align it with the bigger circle. Group them again into an overarching “Icon” group.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2436f35-2d57-4bcb-9a9f-6bce2b911c31/fig5-gravit-design-tutorial.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2436f35-2d57-4bcb-9a9f-6bce2b911c31/fig5-gravit-design-tutorial.gif" width="600" height="338" alt="" /></a><figcaption>Figure 5: Subtract the sun from the cloud so that it looks as if it’s partly covered. (click to play <a href="https://vimeo.com/230186283">video</a>)
</figcaption></figure>

Once we have added a description of the weather condition, we will have finished our first daytime view (figure 6). Add a text layer above the icon (press `T`), with the following properties in the Inspector:

*   Color: white
*   Size: 14 pixels
*   Weight: Regular
*   Line spacing: 16 px (click on the “%” label to switch to pixels)
*   Content: “7:00” followed by a break, followed by “Few Clouds.”
*   Alignment: center (the second icon).

After that, select the time within the text layer, and give it a “Semi-Bold” weight. Make sure that it is horizontally centered to the icon, with a vertical distance of about 12 pixels. Show the grid again with `Alt + Command + G` (on Windows and Linux, `Alt + Control + G`) so that you can align everything properly. Create one last group from the text and the “Icon” group, named “Icon left,” and we will be ready.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa65ee1-4c26-4237-9ee4-aeb20d9bd1ba/fig6-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a625eb8e-e68e-42c6-9864-9a4241d1611e/fig6-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 6: The first weather condition is ready. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa65ee1-4c26-4237-9ee4-aeb20d9bd1ba/fig6-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

Before continuing, let’s bring some order to the Layers panel. Drag the “Status bar" group to the very top (or press `Shift + Command +` up arrow key on the Mac (on Windows and Linux, `Shift + Control +` up), followed by the three text layers, the copy of the sun and the “Icon left” group.

## From Bad To Worse

It’s easy to get the other weather symbols from here. Duplicate the current one (“Icon left”), center it to the page and move it to a Y position of “297,” which should align everything neatly to the grid. The group’s name of this new symbol should be “Icon middle”; for the text, use “14:00 Light rain.” Be sure that everything is centered again.

Because this one will represent the current weather condition, select the circle with a `Command`-click (on Windows and Linux, `Control`-click) to change from the border to a white fill. Create a new shared style named “Icon full.”

Now go to the Layers panel, where you will select the “Cloud” group within “Icon” → “Cloudy.” Enter the color dialog and use the color-picker symbol to pick a light-blue color for the surrounding of the icon. Now employ the “Mix” area at the bottom of the dialog to change to a darker shade, so that the icon comes to the fore against the white background. Align it to the center of the surrounding circle with the alignment icons, remove the “Cloudy” group with `Shift + Command + G` (on Windows and Linux, `Shift + Control + G`), and delete the redundant “Sun” group in the layers panel. See figure 7 for the entire process.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73940de3-fb34-4cea-a073-c19f3230a1ae/fig7-gravit-design-tutorial.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73940de3-fb34-4cea-a073-c19f3230a1ae/fig7-gravit-design-tutorial.gif" width="600" height="338" alt="" /></a><figcaption>Figure 7: Create a new shared style for the middle icon, adapt the cloud and delete the redundant sun. It’s supposed to rain soon! (Click to play <a href="https://vimeo.com/230449984">video</a>)
</figcaption></figure>

The first steps for the rain symbol are accomplished, but one vital part remains: the raindrops. Just like for the sun in the other icon, we need to convert the cloud to outlines first for the subsequent steps (figure 8). Right-click and select “Vectorize border” like before (which converts to a “Compound Path” group). Now we can create a rectangle of 16 × 6 pixels at the bottom, which will act as the hole for the raindrops. It should be 5 pixels away from the left edge of the cloud and overlap its bottom line. You might want to zoom (press `Z`) to have a better view and switch off the grid again.

Select the rectangle together with the “Compound Path” group, and create another “Subtract” operation from “Merge” in the toolbar. For it to work correctly, make sure that the rectangle is on top. After that, drag it into the “Icon middle” → “Icon” group again, and also reset its name to “Cloud.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9491e2f4-daae-4dd7-94af-35f3bbb2f54a/fig8-gravit-design-tutorial.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9491e2f4-daae-4dd7-94af-35f3bbb2f54a/fig8-gravit-design-tutorial.gif" width="600" height="338" alt="" /></a><figcaption>Figure 8: Vectorize the border of the cloud shape and cut away a rectangle. (Click to play <a href="https://vimeo.com/230450376">video</a>)
</figcaption></figure>

Next task: the raindrops (figure 9). They consist of three vertical lines — two 10 pixels long and one 15\. The distance from the first to the second should be 5 pixels, and from the second to the third 4 pixels. Start with the first one of 10 pixels in length: Switch to the Line tool with `L` and hold `Shift` to constrain the movement to the vertical axis. Assign a centered border with 1.5 pixel thickness and rounded ends (from “Advanced stroke settings”) and that has the same color as the cloud (either take it over with the color picker or use the “In use” area in the color dialog.)

Now follow these steps:

1.  Clone the line.
2.  Move it 4 pixels to the right with the arrow key.
3.  Switch to the Subselect tool with `D`, and move the bottom point down by 5 pixels with the arrow key.
4.  Select the first line again.
5.  Make a second copy and move it 9 pixels to the right.
6.  Now select and merge all of the lines (Mac: `Command + M`, Windows and Linux: `Control + M`), which will let you transform them all together with the Transform tool in the Inspector.
7.  Enter “-30°” for “Skew” and click on “Apply.” Make sure that all other fields are set to “0” or “100%.”
8.  Leave the tool with another click on “Transform,” so that you are able to align the skewed lines to the cloud, with a distance of 7 pixels to the left edge and 12 pixels to the top edge.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4b7908d-aba3-4db3-a528-a39e5b804af9/fig9-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d526fb3-2bcb-4581-b0a3-927877bab15c/fig9-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 9: Create the lines for the raindrops, and skew them with the “Transform” tool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4b7908d-aba3-4db3-a528-a39e5b804af9/fig9-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

For the correct measurement to show up, you might need to press `Command + Alt` (on Windows and Linux, `Control + Alt`) to drill into the group. To finish the icon, rename the “Compound Shape” group to “Raindrops” and create a new “Icon inner” container with the “Cloud” group. When selecting the two groups, make sure to use `Command` (on Windows and Linux, `Control`) instead of `Shift`. Also, drag it into the “Icon middle” → “Icon” group and align it properly to the circle again. With this, we have finished the second weather symbol. On to the third and last one!

## Still No Improvement

To start, zoom out to 100% (Mac: `Command + 0`, Windows and Linux: `Control + 0`) for a better view. Select the first symbol — the “Icon left” group — and clone it to an “Icon right” group. Move it to the right of the page with the fifth alignment icon (“Align Right”), and select the “Icon” group within. It should have a gap of 32 pixels from the right edge — the grid will definitely help you here. The text of this symbol should read “22:00 Cloudy.” Like before, make sure that it is centered to the icon. Because we have cloudy weather now, we don’t need the sun anymore. Select its group in the Layers panel and delete it. As well, center the cloud to the circle again in both dimensions. That’s it! We’ve just completed all of the daytimes (figure 10).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc2e2bf4-7f5b-4bc7-9b31-d4eb7913dcb3/fig10-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31fb83d7-3fae-4f8f-b50a-c58afe1578ea/fig10-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 10: All three daytimes are ready. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc2e2bf4-7f5b-4bc7-9b31-d4eb7913dcb3/fig10-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

## Full View

The last element of the weather app (actually, its center part) is the enlarged display of the current weather condition at the bottom of the screen, surrounded by some elegant half circles.

Create the first half circle with a diameter of 464 pixels (figure 11) — switching off the grid might help. Proceed here as follows:

1.  Switch to the Ellipse tool with `E`.
2.  Move the cursor to the bottom center of the page until the smart guides show this spot.
3.  Hold `Shift` to create a circle and `Alt` to start from the middle.
4.  Move this shape down by 16 pixels (add “+16” to the “Position” → “Y” field).
5.  Assign `#708AB5` as the fill color.
6.  Set the “Blending” to “Soft light.”
7.  Rename it to “Ellipse 1.”

To set it off from the background image, assign an Inner Shadow at the bottom of the Inspector with a click on the “+” icon on the right. Use the following properties:

*   X: 0
*   Y: 1
*   Blur: 1
*   Opacity: 70%
*   Color: black

As with the other styling properties, multiple shadows can be stacked on top of each other. Create another inner shadow in the same way as above: It should share all values with its sibling, except for the “Blur” — set this one to “20.” Before you continue, create a new layer in the Layers panel (in the top-right), name it “Bottom,” drag it right above the “Overlay” layers, and move this first circle in. If you’d like, you can also assign a different color to this layer so that it differs from the status bar.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06f157c3-4a71-4d47-b547-6566aeba6f77/fig11-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c4ed575-b0de-44b3-9004-b3e75bfaf966/fig11-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 11: The first half circle at the bottom of the screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06f157c3-4a71-4d47-b547-6566aeba6f77/fig11-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

We need three more circles (figure 12). Clone the first circle with `Shift + Command + D` (on Windows and Linux, `Shift + Control + D`), and resize it to 416 pixels from the center (hold `Shift + Alt` and drag the bottom-right handle). Style the second circle as follows:

*   Fill: #809AC6
*   First inner shadow: 0/1/1/50% (X/Y/blur/opacity)
*   Second inner shadow: 0/1/12/60%
*   Name: “Ellipse 2”

Create a copy from this second circle, this one with the following properties:

*   Size: 392 pixels in diameter
*   Fill: #CCE0FF
*   First inner shadow: 0/1/1/50%
*   Second inner shadow: 0/1/8/100%
*   Name: “Ellipse 3”

For the fourth and last circle, use these settings:

*   Size: 370 pixels in diameter
*   No fill
*   Blending: Normal
*   Just one inner shadow: 0/1/3/25%
*   Name: “Ellipse with image”

The reason why this last circle has no fill is that it will contain another image of a cloudy sky, alongside some dark overlays. [Grab the image](https://www.dropbox.com/s/mbppbb7xvyj1aa2/rainy2.png?dl=0) and bring it into Gravit Designer. Now move it so that it fully covers the last circle, and drag the image into it in the Layers panel, which will clip it automatically to the shape. Another way to create such a mask would be to select both — the shape and image — and pick “Mask with Shape” from the right-click menu. Just make sure that the mask (i.e. the circle) is above the to-be-masked content (the bitmap image) in the layer hierarchy.

After that, create a rectangle within this new mask group (drag it in after it has been created), which will also cover the circle, and give it a black fill with a “Soft light” blending. This will make the image darker; but we need more, so create a clone of this rectangle.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3e9b69c-8891-44bb-92fb-f882b5dce733/fig12-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b141ca45-a624-4e64-b201-672ef686ae49/fig12-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 12: The four half circles &mdash; the last one with the clipped image and the two dark overlays. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3e9b69c-8891-44bb-92fb-f882b5dce733/fig12-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

The last element here is an enlarged version of the rain symbol above (figure 13). Proceed as follows:

1.  Select it (“Icon inner” in “Icon middle” → “Icon”).
2.  Duplicate it and move the icon into the “Bottom” Layer group, in the top position.
3.  After that, drag it to the bottom of the page on the canvas (with the Pointer tool — `V`).
4.  To make it visible in front of the background image, select the “Raindrops” group and change the border color to white, as well as the fill color of the “Cloud” group.
5.  The final move is to enlarge the icon massively to 128 pixels in width and center it to the semi-circle. Make sure that “Keep Ratio” is switched on between the width and height fields in the Inspector and that “Autoscale Borders” is selected in the “Advanced stroke settings” of the raindrops. Otherwise, they will remain at the original border thickness.

To make the icon stand out from the background even more, we could also apply a drop shadow with the properties “-3/3/0/15%.” The same goes for the text layers, but with the values “-1/2/0/10%,” except for the temperature, which harmonizes better with “-2/3/0/5%.”

After so much work, we have finally finished the first screen of the app. Press `Command + 0` (on Windows and Linux, `Control + 0`) to set it in its full glory.

But we want more. In a second iteration, we want to show it with some friendlier conditions.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1225ee42-2b63-4b2b-aa41-205353fc4127/fig13-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ac641b8-4c8a-4ad9-ab46-209762630451/fig13-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 13: The finished enlarged icon at the bottom &mdash; and with it, the entire screen. Make sure to select “Keep Ratio” in the Inspector when resizing the icon. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1225ee42-2b63-4b2b-aa41-205353fc4127/fig13-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

## Finally Sunny

Up until now, we’ve worked exclusively in single-page mode, meaning that we’ve had only a single page on the canvas. For the iteration, we need another one (see figure 15 for the result). To enable multi-page mode, click on the toggle next to the “Pages” label (figure 14). Now you can select the current page on the canvas with a click on the title, and press `Command + D` (on Windows and Linux, `Control + D`) to duplicate it and keep working there. Rename the first one to “Light rain” with a double-click in the page list and the second to “Sunny” so that there is no ambiguity.

Pages are ideal if you want to create different versions of a screen, to try out variations or just to fiddle around and see all iterations next to each other.

The first task for the new page is to change the time in the status bar to “07:30,” to indicate that we are at another time of day now. Also, modify the day (“Saturday, Jun 16”), as well as the temperature (“28 °C”). Furthermore, we want to display other weather conditions: The left-most and middle should be “Sunny,” the right one “Cloudy.” Ensure that all text layers are centered again. Because we have sunny weather now, this should be reflected in the background image. Unlock the current one, delete it and drag in [the new image](https://www.dropbox.com/s/lidtmi4a794ai01/sunny1.png?dl=0). Ensure that it is at the bottom of the layer hierarchy again.

The easiest way to move it there is to press `Shift + Command +` down arrow on the keyboard (on Windows and Linux, `Shift + Control +` down arrow). Then, bring it back to the original size with the respective button in the Inspector (“Original size”), and center it to the page in both dimensions with the fourth and seventh alignment icons from the left in the Inspector. This time, the blur should have a slightly smaller radius of “15”; be sure to lock the image again. In addition to dark overlays, we will create a third one, with the full size of the page, a black fill and a “Soft light" blending. Name it “Overlay 3,” and put it right above the image in the layer hierarchy (also locked).

We also need an updated image for the semi-circle at the bottom, within the “Bottom” → “Ellipse with image” groups. Delete the old one and drag in a [new bitmap](https://www.dropbox.com/s/bfe0nb0m5wyycn4/sunny2.PNG?dl=0). It should be clipped and horizontally centered to the circle again and also be displayed at the original size. Drag it vertically until it shows a view that appeals to you. The two overlays are too dark now, so we need to adapt them. Change one to a fill color of `#000560` and a “Screen” blending, and the other to `#033572` with “Hard light” and an opacity of 12%.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f54a08d-344f-4fc6-bf2c-f6eb5c03b399/fig14-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ab990a2-30fc-486f-978c-6cc9170f6b62/fig14-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 14: A friendlier version of the screen, created on a separate page. Use the toggle in the “Pages” area to change from single- to multi-page mode. We’ve already started to adapt some of its parts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f54a08d-344f-4fc6-bf2c-f6eb5c03b399/fig14-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

## Fixer Of Icons

The only thing left to do is to fix the icons so that they match the text. You can switch to single-page mode again if you like. Because the left icon says “Sunny,” we just need the sun symbol — good that we saved it before tearing it apart earlier. Look for the hidden “Sun” group in the Layers panel and show it again. Delete the old “Cloudy” icon within “Icon left” → “Icon,” and drag the sunny pendant to its place (in the Layers panel and on the canvas). The icon could be a bit bigger, though, about 30 pixels. Continue as follows:

1.  Fully zoom into the icon with “View” → “Fit Selection” from the menu bar.
2.  Zoom out two steps again with `Command + -` (on Windows and Linux, `Control + -`).
3.  Grab the bottom handle, hold `Shift` and `Alt`, and drag until the width in the Inspector says about 30 pixels. Make sure that “Autoscale Borders” is selected in the “Advanced stroke settings” of the icon.

We also need to give the icon a selected state, because the current time is 7:30\. First, change the border color of the sun to the same as for 14:00 — the easiest way is to use the color picker in the color dialog. Now, select the outer circle and change it from the “Icon outline” shared style to “Icon full” in the Inspector. Do the same for the middle weather condition, but in reverse. You also need to replace the rainy icon (“Icon inner”) with the sun there, but with a white outline.

The third place where the sun should appear is within the half circle at the bottom, but at a much larger size. Copy the white version and paste it right above the “Ellipse with image” group. Follow the steps above to resize it to a width of 120 pixels. Finally, use the same shadow as before (-3/3/0/15%) to give it a stronger appearance against the background image.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8babb7c-e4c0-4911-ab55-75400e68db9c/fig15-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1986494-32a6-4780-8514-6a65aff88c7f/fig15-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 15: The finished iteration. It’s going to be very hot today! (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8babb7c-e4c0-4911-ab55-75400e68db9c/fig15-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

## Export It

We now have two versions of the app, showing different times of day and weather conditions (figure 16). Let’s export them in the final step, which is quite a snap in Gravit Designer. Either click on the export icon to the right of the toolbar or press `Shift + Command + E` (on Windows and Linux, `Shift + Control + E`) to enter the Export dialog. There, in the “Canvas” tab, you can already see the two pages, ready for exporting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9fe9a4-2067-49c9-a437-84e0e96b862f/fig16-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9d262e6-9cea-4952-9210-c056c9ff5683/fig16-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 16: The two pages, ready for exporting in the “Export” dialog. You can open the dialog with the respective icon in the toolbar. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9fe9a4-2067-49c9-a437-84e0e96b862f/fig16-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

While the default settings should work just fine, you have many different options here to tweak the output to your liking. The “Format” should be pretty self-explanatory, but the “Size” holds a few hidden values: “2x” lets you export at double size for high-resolution displays (“3x” and “4x” work, too), and you can define a fixed width or height (append “w” or “h”) or both dimensions. Lastly, it’s also possible to set the DPI resolution for print designs.

Besides exporting entire pages, you can also get individual layers (objects) out of Gravit Designer. If you select a layer before entering the export dialog, it will show up in the “Selection” tab; “Assets” can be defined when you click on the “+” icon in “Make exportable” in the bottom-left in the main window. There, you have similar options like in the export dialog and can also define multiple types at the same time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4f8c4a-baf8-42ff-ba11-6ce53e444821/fig17-gravit-design-tutorial-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/687407a5-fbba-4739-923b-ed360958d527/fig17-gravit-design-tutorial-800w-opt.png" width="800" height="452" alt="" /></a><figcaption>Figure 17: You can also export individual elements if you click on the “+” icon in “Make exportable.” They then show up in the “Assets” tab in the export dialog. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4f8c4a-baf8-42ff-ba11-6ce53e444821/fig17-gravit-design-tutorial-large-opt.png">View large version</a>)
</figcaption></figure>

I hope you have enjoyed this tutorial and that it has given you valuable insight into Gravit Designer. It was just a small glimpse into the application and its features, because Gravit is capable of creating many different types of designs. Go to [designer.io](https://designer.io/) to use it online or to download the desktop application.

If you have questions, feel free to ask in the comments below.

You can always reach out to the Gravit team on [Twitter](https://twitter.com/gravitdesigner) and [Facebook](https://www.facebook.com/GravitDesigner/), and there is also the very friendly [discussion board](https://discuss.gravit.io) where you can post your questions and ideas.

{{< signature "mb, al" >}}

