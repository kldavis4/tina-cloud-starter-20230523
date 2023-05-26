---
title: 'How To Start Using Sketch And Framer X'
slug: start-using-sketch-framer-x
author: martina-perez
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/770172c2-9c83-49ae-8c03-2b39866e4e0f/sketch-framer-x-guide.png
date: 2019-06-05T12:30:59+02:00
summary: >-
  This is a tutorial about how to build prototypes and interactions by making use of the <a href="https://www.framer.com/prototyping/">pre-built components</a> in Framer X and the ones available in the <a href="https://store.framer.com/">Framer Store</a>. It should be useful for web designers having none to very little coding experience, interested in learning more about how to better communicate the interactions in the user interfaces they are building.
description: >-
  When it comes to showing the transition, interaction and animation of elements in the user interface, a prototyping tool like Framer X can make a difference in the way you communicate your vision to the team and stakeholders and as a result, boost your efficiency as a designer.
categories:
  - UI
  - Framer X
  - Sketch
---
When it comes to showing the transition, interaction and animation of elements in the user interface, a prototyping tool like Framer X can make a difference in the way you communicate your vision to the team and stakeholders and as a result, boost your efficiency as a designer.

With the following example, I will illustrate how you can add interaction to static designs. To profit the most from this tutorial, some basic experience with Framer X are welcome.

To get started, you will need the following tools and assets:

<ul>
<li><a href="https://www.framer.com/">Framer X</a></li>
<li><a href="https://www.sketch.com/">Sketch</a></li>
<li>A sample <a href="https://drive.google.com/open?id=1Dhf-xOiHb4CNxdy-f66cH5inCi_OwNCG">Sketch file</a>: This Sketch file contains the design screens that we will use in the tutorial. The designs are part of the <a href="https://www.invisionapp.com/inside-design/design-resources/design-system-dashboard-ui-kit/">Velocity UI Kit</a> created by <a href="https://www.invisionapp.com/">InVision</a>.</li>
  </ul>
  
<p><strong>Note:</strong> <em>This tutorial is for designers using MacOS, as Framer X is for Mac (although this may <a href="https://www.framer.com/forms/windows/">change in the near future</a>), and Sketch app is also only for Mac.</em></p>

## Bringing Your Designs From Sketch

<p>We will bring our designs from Sketch into Framer X. You might also create your designs in Framer X as there is a full bunch of layout tools to do so, but there are some reasons whereby you can be interested in continuing designing your interfaces in Sketch:</p>

<ul>
<li>You are used to Sketch and not willing to learn a new design tool.</li>
<li>You have already some designs in Sketch and you want to build the interaction for them.</li>
<li>Sketch works much better with large files. Framer X seems to have some problems when moving elements around.</li>
<li>Framer X is still in his early stages as a design tool and there are not many tutorials about how to create some elements of design. On the other hand, there are plenty of tutorials about Sketch and also many plugins such as the Craft plugin for Sketch which allows you to speed up your design process.</li>
<li>You will find many more web design resources for Sketch than for Framer X.</li>
<li>There is still a lack of tutorials about some of the options available in Framer X, especially about how to use the Code components.</li>
</ul>

{{% feature-panel %}}

<p>So first of all, let’s create a new file in Framer X. The first thing we will do is to bring the design screen we have in Sketch into Framer X. To do so, just copy the Static artboard from Sketch and paste it in Framer X.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d77056b7-b4cc-40bc-94e4-005e8166633c/01-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d77056b7-b4cc-40bc-94e4-005e8166633c/01-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Copy your designs from Sketch and paste them into Framer X. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d77056b7-b4cc-40bc-94e4-005e8166633c/01-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Layout in Sketch and the same layout in Framer X, once imported." >}}

<p>As you can see in the <strong>Layers panel</strong>, we’ve got the same layers we had in Sketch.</p>

<p><strong>Note:</strong> <em>Sometimes, when bringing your designs into Framer X, some properties may be lost &mdash; in this case, it’s the border radius of the thumbnails. This is because we used a Mask in Sketch and Framer X doesn’t recognize it. To solve this, you can either select the Group in Sketch and <strong>Flatten it to Bitmap</strong> before pasting it into Framer X, or once you have brought the design into Framer X, double-click to reach the Frame element and manually change the <strong>Radius</strong> in the Properties panel.</em></p>

## Organize The Layout In Framer

<p>To work on the interaction of the elements in Framer X, we need to create a new Frame.</p>

<p><strong>Note:</strong> <em>A frame is similar to an Artboard in Sketch (or to the HTML <code>&lt;div&gt;</code> element), but is more powerful. Frames act more like <em>containers</em> as a frame can contain other frames.</em></p>

<p>To create a new Frame, go to the <strong>Layout tool panel</strong>, select <strong>Frame</strong> and drag and drop in any part of the canvas; or simply press <strong>F</strong>.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5eafd08-9c04-4b5d-a4a0-9d7cbbf2cbe9/02-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b4ca61a-931a-4103-9162-954d11db7011/02-how-to-start-using-sketch-and-framer-x-800w.gif" width=“800" height="499" alt="To create a Frame, select Frame and drag and drop in the canvas." /></a><figcaption>To create a new Frame, select Frame in the Layout tool panel. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5eafd08-9c04-4b5d-a4a0-9d7cbbf2cbe9/02-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

Second, we will set a device for the Frame. Select the Frame and in the <strong>Properties panel</strong>, <strong>Device</strong>, choose <em>Apple MacBook Pro</em>.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be0c30f0-4474-4482-aaca-570590af60a1/03-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be0c30f0-4474-4482-aaca-570590af60a1/03-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="To set a device for a Frame, select a Device in the Properties panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be0c30f0-4474-4482-aaca-570590af60a1/03-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Select a Frame, Device in the Properties panel and choose Apple MacBook Pro." >}}

<p>Take a look at the Static frame we’ve imported. We will build the following interactions:</p>

<ul>
<li>Header: Fade in when scrolling through the content.</li>
<li>Floating Action Button (FAB): Default, hover and pressed states.</li>
<li>Nav: It is displayed from right to left when clicking the FAB.</li>
<li>Content: It is resized when clicking the FAB.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d12d8ba5-db79-4fc4-a362-f3ff2aa06a1a/04-how-to-start-using-sketch-and-framer-x.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d12d8ba5-db79-4fc4-a362-f3ff2aa06a1a/04-how-to-start-using-sketch-and-framer-x.jpg" sizes="100vw" caption="We will build interactions for the header, nav, FAB, and content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d12d8ba5-db79-4fc4-a362-f3ff2aa06a1a/04-how-to-start-using-sketch-and-framer-x.jpg'>Large preview</a>)" alt="Highlighting the elements we will build the interaction for: header, nav, FAB and content." >}}

<p>First, create new Frames on top of the layers in such a way that you end up having one Frame for each of the abovemention interaction elements. For instance, we will add a new Frame to group all the layers that are part of the Header (<kbd>Cmd</kbd> + <kbd>Enter</kbd>) and name the Frame as <em>header</em>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4c43e41-bc2c-4f0d-a308-373185d0566d/05-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4c43e41-bc2c-4f0d-a308-373185d0566d/05-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Group the layers to have one Frame for each of our interactive elements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4c43e41-bc2c-4f0d-a308-373185d0566d/05-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Select the elements of the header and add a Frame on top of them." >}}

<p>For the sake of clarity, change the name of the Apple MacBook Pro frame to <em>Interactive</em>. In the following section we will create a <strong>Scroll component</strong>.</p>

## Scroll Through The Content

<p>First, we will duplicate (<kbd>Cmd</kbd> + <kbd>D</kbd>) the Content frame and take it out of the Static frame. Change the name of the new frame to <em>i_content</em>.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/449f070e-1396-4fb4-93af-f3949fa81b0f/06-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/449f070e-1396-4fb4-93af-f3949fa81b0f/06-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Duplicate the Content frame and take it out of the Static frame. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/449f070e-1396-4fb4-93af-f3949fa81b0f/06-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Content Frame has to be out of the Static frame." >}}

<p>Secondly, we will create a <strong>Scroll component</strong> in our Interactive frame. To do so, go to the <strong>Interactive tool panel</strong> and select <em>Scroll</em>. Drag and drop in any part of the Interactive frame.</p>

<p>In addition to that, modify the width of the Scroll component to 1141px (same as the Content) and position it in the same coordinates as the Content is on the Static frame (left: 149px, top: 140px). Apart from that, increase the height of the Scroll component as it reaches the bottom of the Interactive frame.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/805f732c-3db8-49aa-a114-c67b4367b8bf/07-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35357292-afd4-4f91-8411-39c9fc5b7161/07-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Position the Scroll component where it was on the Static frame." /></a><figcaption>Modify the width and height of the Scroll component and position it in the same coordinates as the Content frame. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/805f732c-3db8-49aa-a114-c67b4367b8bf/07-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>Next, we will connect the Scroll component to our <em>i_content</em>. To do so, click on the connector and connect it to <em>i_content</em>.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acb966ec-4553-456a-8da9-298554506131/08-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/400f5371-df83-44bc-8e09-2ec88fdd5424/08-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Connect the Scroll component to the i_content." /></a><figcaption>Connect the Scroll component to the <code>i_content</code>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acb966ec-4553-456a-8da9-298554506131/08-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>
  
<p>Lastly, select the Interactive frame and <kbd>Cmd + P</kbd> to enter the <strong>Preview Mode</strong>. You should be able to scroll through the content now.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56d71e2e-5fa5-4699-9025-eefa4c15414a/09-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e82e05-f0de-4493-9577-ccc801ff91a6/09-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Scrolling through the page on Preview Mode." /></a><figcaption>To access to Preview Mode, press <code>Cmd</code> + <code>P</code>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56d71e2e-5fa5-4699-9025-eefa4c15414a/09-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>Next, I will explain how to position the Header and the FAB (Floating Action Button) button to make them fixed while scrolling with no need for any special coding.</p>

{{% ad-panel-leaderboard %}}

## Fixed Elements

<p>We will position the elements so as they remain fixed when scrolling through the page. To that end, duplicate the Header frame and position it in the Interactive frame. As before, change the name to <em>i_header</em>. Do the same with the Floating Action Button button. Your Layers panel should look like this.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0346bf3d-1328-46ad-9699-291bcd8e226e/10-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0346bf3d-1328-46ad-9699-291bcd8e226e/10-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Duplicate the Header and the FAB frames and position them within the Interactive frame. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0346bf3d-1328-46ad-9699-291bcd8e226e/10-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="i_fab and i_header are in the Interactive frame." >}}

<p>As the Header and the FAB are out of the Scroll component, they will remain fixed while scrolling.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f59a393-f2a3-41bf-8804-f3f2aa91bdcc/11-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff945141-dc84-4503-b936-48e0f35dc91f/11-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="In Preview mode, Scroll through the content, whereas the header and FAB remain fixed." /></a><figcaption>You can scroll through the content, whereas the header and FAB remain fixed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f59a393-f2a3-41bf-8804-f3f2aa91bdcc/11-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>In the next section, I will explain how to build the transition of the Header.</p>

## Header Transition

<p>To build the transition of the Header we will make use of the <a href="https://store.framer.com/package/derlukas/scroll-away">Scroll away</a> component created by <a href="https://twitter.com/derlukasg">Lukas Guschlbauer</a>. To start using this component, go to the <strong>Framer Store</strong>, search for <em>Scroll</em> and install the Scroll Away component.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a19c6009-4085-4354-88d2-0c5979efee6b/12-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a19c6009-4085-4354-88d2-0c5979efee6b/12-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Search for 'Scroll' in the Framer Store and install the Scroll Away component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a19c6009-4085-4354-88d2-0c5979efee6b/12-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Framer store where you can search the Scroll Away component." >}}

<p>Next, go to the the <strong>Components panel</strong>, click the <strong>Scroll Away</strong> and drop it onto the canvas. Take the Header frame out of the Interactive frame and position the Scroll away component where the Header was. Change the component size as to be the same as the Header (1440x80px).</p> 

<p>Now, select the Scroll Away component and connect it to your <em>i_header</em> frame. You can change multiple properties of the component such as alignment, effect, direction, easing or timing in the Properties panel. We will change the effect to <em>Fade Move</em>. Once that is done, the options below will change accordingly.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36dd80da-722f-40fc-8f41-bcaf1628ae50/13-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36dd80da-722f-40fc-8f41-bcaf1628ae50/13-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Take the Header frame out of the Interactive frame and change the effect to Fade Move. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36dd80da-722f-40fc-8f41-bcaf1628ae50/13-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Applying the Fade Move effect in the Scroll Away component." >}}

<p>For the effect to work, we need one more thing. Select the Scroll Away Component and click the <strong>Override</strong> in the Properties panel. Click <strong>File</strong> and select <strong>New File</strong>. Then, click <strong>Override</strong> and select <em>useScrollData</em>. Next, click the Scroll component of your Interactive frame. Click Override again and select <em>getScrollData</em> in Override. To preview the result, press <kbd>Cmd</kbd> + <kbd>P</kbd>.</p>

<p><strong>Note:</strong> <em><a href="https://www.framer.com/docs/overrides/">Overrides are a unique concept to Framer X</a>. Code overrides are functions that allow components to communicate with each other. You can write them yourself in code and apply them to any Frame or component on your canvas. These functions allow you to override visual properties like opacity and fill, and allow for interactivity and animation. Code overrides can live in any code file in your project. Framer X interprets these based on the type. You can apply any code override to any Frame or component on the canvas by selecting Override from the Properties panel.</em></p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b944663-aec3-4e83-a565-74d3056116fb/14-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d9210ae-12db-4107-b229-f9bff34ef8da/14-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="There is a white space at top when scrolling through the content in Preview Mode" /></a><figcaption>The transition of the Header works, but there is a white space at the top. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b944663-aec3-4e83-a565-74d3056116fb/14-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>The transition works, but you will notice that there is a white space at the top. This is because the Scroll component is positioned at y: 140. Let’s change this. Increase the height of the Scroll component to occupy the whole height of the Interactive frame. Next, go to your <em>i_content</em> frame and position the elements 140px from the top of the frame.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/693a3207-2607-4f0f-a818-aca75dd7e26e/15-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/693a3207-2607-4f0f-a818-aca75dd7e26e/15-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="In the i_content frame, position the content 140px from top. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/693a3207-2607-4f0f-a818-aca75dd7e26e/15-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Positioning the content 140px from top in the i_content frame." >}}

<p>Your interaction should be now similar to this one.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c3b6c8f-92b7-4156-b6e0-0b10859bc471/16-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5776f055-0003-43cf-9c8e-86e68dc964fd/16-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Header goes away with Fade Move effect while scrolling through the content in Preview Mode." /></a><figcaption>Header transition when scrolling through the content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c3b6c8f-92b7-4156-b6e0-0b10859bc471/16-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p><strong>Note</strong>: <em>If you need it, download the <a href="https://drive.google.com/open?id=1vPFvGWz0Y3Y23OHEOwPHYZwsaDTh6m2E">source file</a> for this step.</em></p>

<p> Next, I will explain how to change the state of a button when interacting with it.</p>

## States For Buttons

<p>In this section, we will work on the different states for the Floating Action Button (FAB). We will make use of the <a href="https://store.framer.com/package/gusso/magic-move">Magic Move component</a> created by <a href="https://twitter.com/gusso?lang=en">Henrique Gusso</a>. So first of all, go to the <strong>Framer store</strong> and install this component. In the <strong>Components panel</strong>, select the component and drop it on the canvas.</p>

<p>At first, select the Floating Action Button frame and take it out of the Interactive frame. Next, position the Magic Move component where the FAB was. Change its size to 72&times;72px.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62200386-8e11-4a75-bab3-e4a19cb0f4fc/17-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62200386-8e11-4a75-bab3-e4a19cb0f4fc/17-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Take the FAB out of the Interactive frame and position the Magic Move component where the FAB was. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62200386-8e11-4a75-bab3-e4a19cb0f4fc/17-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="The i_fab is out of the Interactive frame and the Magic Move component is where the FAB was." >}}

<p>For some reason, the graphic imported from Sketch doesn’t work with this component, so we will create our own circle. In the <em>i_fab</em> frame, remove the frame that contains the graphic and create a circle with the same color and properties instead.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0bd73e9-f513-433d-b67a-90c33f85a63e/18-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0bd73e9-f513-433d-b67a-90c33f85a63e/18-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Remove the graphic imported from Sketch and create your own circle. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0bd73e9-f513-433d-b67a-90c33f85a63e/18-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Detail of the layers of the i_fab frame." >}}

<p>For the different states of the FAB, we need to create a <strong>Master</strong> and three <strong>Instances</strong> (default, hover, and pressed states). To do so, select the <em>i_FAB</em>, right-click on it, and select <strong>Create component</strong>.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4562a460-9b4d-4995-a900-254a3023635f/19-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4562a460-9b4d-4995-a900-254a3023635f/19-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="To create a Master, select the i_fab frame, right-click, Create component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4562a460-9b4d-4995-a900-254a3023635f/19-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Right click on the i_fab, Create component to get a Master of the element." >}}

<p><strong>Note:</strong> Design Components are similar to Symbols in Sketch. So if you want to create reusable components for your Design System this is a very useful tool. To change the properties of your instances all at once, just select the Master and modify the properties you want. For further information, take a look at the <a href="https://www.framer.com/blog/posts/creating-design-components/">Framer X guide to create Design Components</a>.</p>

<p>Now, duplicate the <em>i_fab</em> Master frame 3 times to get the instances. Change the name of the new frames to <em>i_fab_default</em>, <em>i_fab_hover</em>, and <em>i_fab_pressed</em>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69c7b115-b8f8-4240-8192-09a88a056ec9/20-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69c7b115-b8f8-4240-8192-09a88a056ec9/20-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="To create the Instances for the states of the button, duplicate the Master 3 times. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69c7b115-b8f8-4240-8192-09a88a056ec9/20-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="The Master and the three instances of the i_fab: default, hover and pressed." >}}

<p>Next, we need to connect the Magic Move component to the instances. Connect <em>Initial</em> to <em>i_fab_default</em>, <em>Hover Start</em> to <em>i_fab_hover</em>, <em>Tap</em> to <em>i_fab_pressed</em> and <em>Hover End</em> to <em>i_fab_default</em>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0627a729-fec6-42cc-8e66-9b9ba0874e65/21-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0627a729-fec6-42cc-8e66-9b9ba0874e65/21-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Connect the Magic Move component to the instances. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0627a729-fec6-42cc-8e66-9b9ba0874e65/21-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Connect the Magic Move component in the Interactive frame to the instances: default, hover and pressed." >}}

<p>Finally, we have to go into each one of the states and change the color and scale. Go into the <em>i_fab_hover</em> and change its color to #2244BF. To do so, double click until you see the Fill option in the Properties panel. Next, go into the <em>i_fab_pressed</em>, reduce its size to 56px and change its color to #172E80. Check the result in the Preview Mode.</p>

<p><strong>Note:</strong> If you see a black screen in the Preview Mode, check the compatibility of the component with your Framer Library Version. To do so, go to the page of the component in the Framer Store. If the package is not compatible with your version you will see a warning message. To <a href="https://help.framer.com/troubleshooting/changing-your-framer-library">change your Framer Library</a>, navigate to <strong>File → Framer Library Version</strong>.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b46881ca-c87d-4a6a-8d58-de1acd31c910/22-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1954e6dd-9bb6-4239-bdd2-6ff0f7f083f0/22-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Different states of the FAB in Preview Mode while hovering and clicking it." /></a><figcaption>To access the Preview mode, press <code>Cmd</code> + <kbd>P</kbd>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b46881ca-c87d-4a6a-8d58-de1acd31c910/22-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>In the next section I will explain how to display the nav from right to left by clicking the FAB  button.</p>

<p><strong>Note</strong>: <em> If you need it, download the <a href="https://drive.google.com/open?id=11WeQKN9Uj2-9aQ_xZoET40aDhAQh2-nk">source file</a> for this step.</em></p>

## Open The Nav When Clicking A Button

<p>Now, we will work on the interaction to display the Nav when clicking the FAB button. We will make use of the <strong>Link to</strong> and the <strong>Magic Move</strong> component again for the transition.</p>

<p>Go to the Static frame and duplicate the Nav frame. Position it in any part of the canvas and change its name to <em>i_nav</em>.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd174d15-74e8-4133-8542-a025775b4054/23-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd174d15-74e8-4133-8542-a025775b4054/23-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Duplicate the Nav frame, take it out of the Static frame and change its name to i_nav. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd174d15-74e8-4133-8542-a025775b4054/23-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="i_nav is out of the Static frame." >}}

<p>Now, we need to create two different states for the Nav. First, the initial state (no nav is shown) and second state, the nav is displayed. To do so, create a new Master with the <em>i_nav</em> (right-click and select <strong>Create component</strong>, or use the shortcut <kbd>Cmd</kbd> + <kbd>K</kbd>). Once you have the Master, duplicate two times to get the Instances. Name them <em>i_nav_default</em> and <em>i_nav_displayed</em>.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db69ccc-2267-45b9-90b4-bc34595601c5/24-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db69ccc-2267-45b9-90b4-bc34595601c5/24-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Duplicate the Master to get the instances of <em>i_nav</em>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db69ccc-2267-45b9-90b4-bc34595601c5/24-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="The master of i_nav with the two instances: default and displayed." >}}

<p>Next, position the elements of the <em>i_nav_default</em> out of the frame (Right: -80px).</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/770072ce-795a-463e-9440-070e82929a35/25-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/770072ce-795a-463e-9440-070e82929a35/25-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Position the <em>i_nav_default</em> out of the frame. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/770072ce-795a-463e-9440-070e82929a35/25-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="i_nav_default is positioned out of the frame." >}}

<p>So, the Nav will be displayed automatically from right to left when clicking the FAB. To build this animation, we need to create a new Frame. Duplicate the Interactive frame. Change the name of the new Frame to <em>Interactive02</em>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/132f2435-bdb6-4d07-b20d-35eef3cdd1c6/26-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/132f2435-bdb6-4d07-b20d-35eef3cdd1c6/26-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Duplicate the Interactive frame. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/132f2435-bdb6-4d07-b20d-35eef3cdd1c6/26-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Interactive frame and its duplicate: Interactive02 frame." >}}

<p>To display the Nav in this new Frame we will create a new <strong>Magic Move</strong> component. The size (80x392px) and the position (Top: 140, Right: 0) need to be the same as the Nav.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fd55ba6-38aa-4e5b-8f30-752a14609621/27-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fd55ba6-38aa-4e5b-8f30-752a14609621/27-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Add a new Magic Move component in the Interactive02 frame. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fd55ba6-38aa-4e5b-8f30-752a14609621/27-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Magic Move component in the Interactive02 frame." >}}

<p>Next, go to <em>Interactive02</em> frame, select the Magic Move Component and connect it to the instances. <em>i_nav_default</em> to the <em>Initital</em> state and <em>i_nav_displayed</em> to the <em>Automatic</em> state. By doing so, when entering on this second Frame, the Nav will be displayed automatically.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f86c45d7-9a80-4cf9-927d-b92dcfab45f9/28-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f86c45d7-9a80-4cf9-927d-b92dcfab45f9/28-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Connect the Magic Move component to the instances. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f86c45d7-9a80-4cf9-927d-b92dcfab45f9/28-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Connect the Magic Move component in Interactive02 frame to the instances of the i_nav." >}}

<p>Now, we will build the interaction between screens by linking the Frames. Go to the Interactive frame, select the FAB, <strong>right-click → Add Frame</strong>. Change the name of the new frame to <em>interactive_fab</em>. Press <strong>L</strong> (Link to) and connect it to the Interactive02 frame.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99fc327d-50bd-4a0e-b1cb-b75a8498de5a/29-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99fc327d-50bd-4a0e-b1cb-b75a8498de5a/29-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="On the Interactive frame, add a new Frame on top of the FAB and press L to connect it to the Interactive02 frame. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99fc327d-50bd-4a0e-b1cb-b75a8498de5a/29-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Linking the FAB to Interactive02 frame." >}}

<p>Change the transition to <em>Instant</em> and preview it. You can change the transition effect between screens in the Properties panel.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28d404f6-11cd-462b-b110-ba73a7e1d729/30-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7e38ce5-ea57-44b9-b43a-536998549a13/30-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Select the FAB and changing the transition to Instant." /></a><figcaption>Change the transition to Instant. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28d404f6-11cd-462b-b110-ba73a7e1d729/30-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>If you go to Preview Mode you will see that the Nav is shown when clicking the FAB button, but we need to reverse the interaction when clicking again on it. To do so, duplicate the Interactive02 frame (give the name <em>Interactive03</em> to the new Frame).</p>

{{% ad-panel-leaderboard %}}

<p>On Interactive03 frame, select the Magic Move component and assign <em>i_nav_displayed</em> to the <em>Initial State</em> and <em>i_nav_default</em> to the <em>Automatic State</em>.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/261c07c2-6407-41b7-875b-a82dd74d5639/31-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76c06d16-d17c-41b5-9041-c092b6cae64d/31-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Assigning states of the i_nav to the Magic Move Component on Interactive03 frame." /></a><figcaption>Assign <em>i_nav_displayed</em> to the <em>Initial State</em> and <em>i_nav_default</em> to <em>Automatic state</em> on Interactive03 frame. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/261c07c2-6407-41b7-875b-a82dd74d5639/31-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>Finally, press <strong>L</strong> (Link to) the <em>interactive_fab</em> in the Interactive02 frame to Interactive03 frame and the <em>interactive_fab</em> in Interactive03 frame to the Interactive02 frame. Remember to change the transition effect in the <strong>Link properties</strong> to <em>Instant</em>.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4d9742b-d822-4585-97e7-4b5929d70227/32-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd41454-e740-4a95-ae5a-c393b58b5227/32-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Linking screens with the FAB in Interactive02 frame and Interactive03 frame." /></a><figcaption>Link the <em>interactive_fab</em> in the Interactive02 frame to Interactive03 frame and the <em>interactive_fab</em> in Interactive03 to the Interactive02 frame. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4d9742b-d822-4585-97e7-4b5929d70227/32-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>Preview the interaction from the Interactive frame. The result should be as the one below:</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d4228fd-51a1-4a7c-bcce-772e379f4781/33-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4fab062-3b8e-466e-9f42-e659d23541da/33-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="When clicking the FAB button, the Nav is displayed from right to left." /></a><figcaption>When clicking the FAB button, the Nav is displayed from right to left. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d4228fd-51a1-4a7c-bcce-772e379f4781/33-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p><strong>Note</strong>: <em>If you need it, download the <a href="https://drive.google.com/open?id=1HQpMoIDdkb6yZABbNg1l03mScibqbsZo">source file</a> for this step.</em></p>

<p>Next, I will explain how to resize the content when clicking the FAB button.</p>

## Resize The Content When The Nav Is Displayed

<p>To resize the content when the Nav is displayed we will write some <a href="https://www.framer.com/docs/code">React code</a>. We will use <a href="https://www.framer.com/blog/posts/introducing-framer-playground/">Playground</a> (a code editor integrated in Framer X) that allows you to play with some <strong>React and HTML code</strong> to build advanced animations.</p>

<p><strong>Note:</strong> <em>If you are not familiar with React, you may be interested in taking a look at some <a href="https://www.framer.com/tutorials/#react">React tutorials</a>.</em></p>

<p>So first, go to each of the interactive frames, select the Scroll component and add a Frame on top of it.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd2918e-624c-4766-9e95-d13052648e82/34-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd2918e-624c-4766-9e95-d13052648e82/34-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Add a Frame on top of each of the Scroll components. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd2918e-624c-4766-9e95-d13052648e82/34-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="A Frame was added on top of the Scroll component." >}}

<p>Next, go to the Properties panel and click <strong>Override</strong>. On <strong>File</strong>, select <strong>App</strong>. If you don’t see it, select <strong>New file</strong>. Then, click <strong>Edit Code</strong>. The <strong>Playground</strong> will be opened automatically.</p>

<p>Make sure your <strong>App file</strong> has the following line at the top. If not, add it:</p>

<pre><code class="language-css">import { Data, animate, Override, Animatable } from "framer"
</code></pre>

<p><strong>Note:</strong> <em>(*) This code works with Framer v. 25 and the latest API version v. 1.0.7. While this code works, keep in mind that Framer is now encouraging users to use React Hooks functions instead of class components. Learn more at the new <a href="https://www.framer.com/api">Framer API documentation</a> pages.</em></p>

We will declare a variable called <em>contentScaleValue</em> and indicate that it can be animated. Also, we will set the default toggle state as <em>true</em>.

<pre><code class="language-css">//Value by default
const contentScaleValue = Animatable(1);
let toggle = true;
</code></pre>

<p>Then, we will create a function <em>ResizeContent</em> for the Content to be scaled when clicking the FAB. Besides that, we have to set its originX and originY as so it scales from top left.</p>

<pre><code class="language-css">//Assign to content
export const ResizeContent: Override = props => {
 return {
   scale: contentScaleValue,
   originX: 0,
   originY: 0
 };
};
</code></pre>

<p>Next, we will create a second function <em>togglePosition</em> for the FAB. We will say that <em>onTap</em>, if toggle is <em>true</em>, Content will be rescaled and the toggle state will change to <em>false</em>. Otherwise, do the reverse animation.</p>

<div class="break-out">

<pre><code class="language-css">//Assign to FAB
export const togglePosition: Override = props => {
 return {
   onTap: () => {
     if (toggle) {
       animate.ease(contentScaleValue, 0.9, {duration: 0.2});
       toggle = false;
     } else {
       animate.ease(contentScaleValue, 1, {duration: 0.2});
       toggle = true;
     }
   }
 };
};
</code></pre>
</div>

<p>After writing this code, select the Frame you created on top of your Scroll components, go to the <strong>Override</strong> section in the properties panel and select <strong>File: App, Override: ResizeContent</strong>. Next, select the FAB, <strong>File: App, Override: togglePosition</strong>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f767965b-481c-4e03-bb60-7000804909c8/35-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f767965b-481c-4e03-bb60-7000804909c8/35-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Select the Frame on top of your Scroll components and set the Override as ResizeContent. Select the FAB and set the Override to togglePosition. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f767965b-481c-4e03-bb60-7000804909c8/35-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="The Override is set to ResizeContent on the Scroll component. The Override is set to togglePosition on the FAB component." >}}

<p>Check that the result works as the following.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26f24a6d-1fbd-4849-8d62-8c19488d9ddf/36-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7eabff1-95fe-4fff-af8b-0e48324f2ff1/36-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="The Content is resized when clicking the FAB in Preview Mode." /></a><figcaption>To preview the interaction, press <code>Cmd</code> + <code>P</code>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26f24a6d-1fbd-4849-8d62-8c19488d9ddf/36-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p><strong>Note</strong>: <em>If you need it, download the <a href="https://drive.google.com/open?id=14wVN2_KoICjCACSXuGePP7iq9NDS3FiO">source file</a> for this step.</em></p>

## Prototyping

<p>Go to the the Sketch file and import (copy and paste) the User profile artboard into Framer X. Once in Framer, duplicate the Frame. Give it the name <em>Interactive_user_profile</em>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae4555ee-1195-4efe-8844-b75606cc3679/37-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae4555ee-1195-4efe-8844-b75606cc3679/37-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Copy your User profile artboard in Sketch and paste it into Framer X. Then duplicate your frame and give it the name <em>'Interactive_user_profile'</em>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae4555ee-1195-4efe-8844-b75606cc3679/37-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="User profile artboard in Sketch and once imported in Framer X." >}}

<p>We will build automatic transitions for the right sidebar, the boxes at top and the content. Take each of the Frames out of the <em>Interactive_user_profile</em> frame.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36d59121-cd6e-4231-9a8b-aa3499f5cbd2/38-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36d59121-cd6e-4231-9a8b-aa3499f5cbd2/38-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="We will build automatic transitions for the right sidebar, the boxes at top and the content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36d59121-cd6e-4231-9a8b-aa3499f5cbd2/38-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Highlighting the elements that we will build the interaction for: right sidebar, boxes at top and content." >}}

<p>Create a <strong>Magic Move component</strong> for each of the elements and position them in the <em>Interactive_user_profile</em> frame.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baf3d1e8-da9a-494f-ad80-0d35e6f24070/39-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baf3d1e8-da9a-494f-ad80-0d35e6f24070/39-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Create a Magic Move component for the elements to be animated. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baf3d1e8-da9a-494f-ad80-0d35e6f24070/39-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="Magic Move components for the elements are in Interactive_user_profile frame." >}}

<p>Next, create a Master and two instances for each of the components. For the sidebar, position the first instance out of the Frame. For the boxes and the content, change the opacity of the first instance to 0.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d1bb7fb-8973-46a3-b08c-4115520226ae/40-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d1bb7fb-8973-46a3-b08c-4115520226ae/40-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Create a Master and two instances for each of the components. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d1bb7fb-8973-46a3-b08c-4115520226ae/40-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="A Master and two instances for each of the components. The opacity of the second instance is set to 0." >}}

<p><strong>Connect the Magic Move component</strong> to each of the instances. Assign the first instance to the <em>Initial State</em> and the second instance to the <em>Automatic State</em>.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f382503-772a-484c-981d-8f9671cbf9bd/41-how-to-start-using-sketch-and-framer-x.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f382503-772a-484c-981d-8f9671cbf9bd/41-how-to-start-using-sketch-and-framer-x.png" sizes="100vw" caption="Connect the Magic Move components to the instances. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f382503-772a-484c-981d-8f9671cbf9bd/41-how-to-start-using-sketch-and-framer-x.png'>Large preview</a>)" alt="The Magic Move components are connected to the instances of the elements." >}}

<p>In the Properties panel, you can change the <strong>delay</strong> of each of the <strong>Move Magic components</strong> to set up the order to be shown. Assign the next delays:</p>

<ul>
<li>Sidebar: no delay</li>
<li>First box: 0.4 delay</li>
<li>Second box: 0.6 delay</li>
<li>Third box: 0.8 delay</li>
<li>Content: 1 delay.</li>
</ul>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea0c295-f0a9-4144-add6-5e6fb0c911b8/42-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ef2b71f-f8ba-4728-8a46-c629a58c22e5/42-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Selecting one of the boxes and setting a delay of 0.4." /></a><figcaption>Change the delay of the components in the Properties panel. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea0c295-f0a9-4144-add6-5e6fb0c911b8/42-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p>Go to the <em>Interactive03</em> frame, select the header and <strong>Link to</strong> the <em>Interactive_user_profile</em> frame. In this frame, select the header and <strong>Link to</strong> Interactive frame. Remember to change the transition between the screens to <em>Instant</em>. Check the results.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4592672-d5ef-4cfd-a9cd-bf695c63d70f/43-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a35b77-1450-4c36-9050-c1e65f1bb5fb/43-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Linking Interactive03 frame to Interactive_user_profile frame." /></a><figcaption>Prototyping with the Link tool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4592672-d5ef-4cfd-a9cd-bf695c63d70f/43-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

<p><strong>Note</strong>: <em>If you need it, download the <a href="https://drive.google.com/open?id=11o_dJy2iVDG0pcq4LSCjOkAWXVDKTc4l">source file</a> for this step.</em></p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a9939a2-ad94-4fc0-b2af-fe1babbc5f9e/44-how-to-start-using-sketch-and-framer-x.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec0f21c-032b-4bc8-8a4f-11fd5f2aed54/44-how-to-start-using-sketch-and-framer-x-800w.gif" width="800" height="" alt="Clicking on the header leads you to User profile frame where the elements are displayed with an automatic animation." /></a><figcaption><code>Cmd</code> + <code>P</code> to check the result. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a9939a2-ad94-4fc0-b2af-fe1babbc5f9e/44-how-to-start-using-sketch-and-framer-x.gif">Large preview</a>)</figcaption></figure>

## Sharing The Prototype

<p>To share the prototype, click <strong>File</strong> → <strong>Export Web Preview</strong> (<kbd>Cmd</kbd> + <kbd>E</kbd>). To see the prototype, open the <em>index.html</em>. It will launch the prototype in a web browser.</p>

## Conclusion And Takeaways

<p>If you are looking for a design tool specialized in interaction, Framer X is the perfect one. Framer X allows you to build simple transitions between screens, micro interactions, but also to design complex interactions making use of React code.</p>

<p>By using Framer X, you will speed up your design process and will be able to better communicate the interaction of your designs to the team and stakeholders.</p>

<ul>
<li>You can still design the interface in Sketch and paste your designs into Framer X to build the interaction of the elements there.</li>
<li>For this tutorial, I have have been using a design imported from Sketch, but you can create your layouts in Framer X as well.</li>
<li>There are multiple UI kits available in the Framer Store to help you build your design systems.</li>
<li>There is no single approach on how to build an interaction in Framer X. Experiment and learn.</li>
<li>To build some quick interactions faster, make use of the pre-built components in the Framer Store.</li>
<li>You just need a minimal coding knowledge in order to start building complex interactions in Framer X and there are multiple tutorials available online to start learning how to do it.</li>
</ul>
  
{{< signature "mb, yk, il" >}}
