---
title: Keynote Animation – How To Prototype UI
slug: animating-in-keynote
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37b4d57d-bdd0-4869-800b-dab2842b2bee/10-html-export-opt-small.png
date: 2015-08-03T22:16:16.000Z
author: hamzasiddiqui
description: >-
  Whether it’s playful refresh states, subtle icon movements or complex
  transitions, **beautiful animation** is all around us. Once considered an
  aesthetic luxury, animation is now used so commonly in modern web and mobile
  applications that [entire](https://capptivate.co/)
  [websites](https://uigifs.com/) are dedicated to **UI animation patterns**.

  While animations may have great visual appeal, they also make app experiences
  more intuitive and engaging. Animation can make an app feel more fluid and
  responsive by providing feedback on user interaction. This means that, for
  designers, creating **authentic animations** is increasingly becoming a part
  of the job description.
categories:
  - Coding
  - Mobile
  - Tools
  - Workflow
  - Animation
---
Whether it’s playful refresh states, subtle icon movements or complex transitions, **beautiful animation** is all around us.

Once considered an aesthetic luxury, animation is now used so commonly in modern web and mobile applications that entire websites are dedicated to **UI animation patterns**.</p>

## <span class="rh">Further reading</span> on Smashing:

*   [UI Animation Guidelines and Examples](https://www.smashingmagazine.com/2015/05/functional-ux-design-animations/)
*   [How To Integrate Motion Design In The UX Workflow](https://www.smashingmagazine.com/2016/03/integrate-motion-design-animation-ux-workflow/)
*   [Smart Transitions In User Experience Design](https://www.smashingmagazine.com/2013/10/smart-transitions-in-user-experience-design/)
*   [Designing Navigation On Mobile: Prototyping With Keynote](https://www.smashingmagazine.com/2015/03/prototyping-navigation-on-mobile-with-keynote/)

While animations may have great visual appeal, they also make app experiences more intuitive and engaging. Animation can make an app feel more fluid and responsive by providing feedback on user interaction. This means that, for designers, creating **authentic animations** is increasingly becoming a part of the job description.

{{% feature-panel %}}

## The Right Tool For The Job

Traditionally, designers have had to learn complex animation tools from scratch to produce even the simplest of motion graphics. In recent years, a slew of software has come out vying for the attention of prototypers and motion designers, such as [Framer](https://framerjs.com/), [Origami](https://origami.design/) and [Pixate](https://www.pixate.com/), not to mention the old classics such as Adobe After Effects.

However, I found them all to be a bit of overkill for what I was trying to achieve. As a UI designer, I needed a **rapid, easy-to-learn, familiar tool** to animate my static designs. I needed to produce animations quickly, since my team was iterating quickly on a product we were working on. I also didn’t want to learn an entirely new software paradigm. A bonus would be a tool that integrates nicely in my existing static design workflow (I generally use Sketch and Photoshop).

In my quest to find a tool that is more suitable to these needs, I stumbled upon one that has been on my computer all along — **Apple’s Keynote**.</p>

### Keynote?

Most people know Apple’s Keynote as the PowerPoint equivalent on Mac OS X — presentation software. That is true, but it can also be used to produce surprisingly high-fidelity animations and prototypes. In fact, many employees at companies such as Google and [Apple use Keynote](https://developer.apple.com/videos/wwdc/2014/#223) on a daily basis for UI design, animation and prototyping.

Last year, Andrew Haskin, interaction designer at Frog, showed us just how powerful Keynote could be when he recreated Google’s material design animations entirely in Keynote.
{{< vimeo id="100377108" >}}

### Learning Keynote

Andrew’s video really piqued my interest in Keynote, and in the past year I’ve used the software to recreate many interactions seen in major apps, including Facebook Paper, Uber, Tinder, Snapchat and more. You can see a reel of that below.
<figure class="video-container"><iframe loading="lazy" width="500" height="281" src="https://www.youtube.com/watch?v=s8dFV-NiBbE" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

Keynote is fairly easy to pick up, because most people have used some sort of presentation software in their life. It is very much like PowerPoint if you're familiar with it, so the interface is recognizable and you will immediately understand how to create and edit slides.

One of my favorite aspects of animating in Keynote is that it is **straight to the point** — there is no code, complicated timelines with keyframes or unnecessary functionality for designers.

The major legwork of the animation is done with Keynote’s **“Magic Move”** transition effect. With Magic Move, all you need is a _beginning_ and _end_ slide, and you can edit any number of properties between them (scale, position, rotation, etc). Keynote takes care of the rest by intelligently filling in the gaps, creating a seamless transition from one slide to the next.
<figure class="video-container"><iframe loading="lazy" width="500" height="300"]https://blog.uxtree.io/wp-content/uploads/smashingmag/magic%20move%20example.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

Magic Move saves a ton of time, and complex animations that would have taken much longer in other tools take seconds with Keynote.</p>

## Overall Workflow

To demonstrate how to use Keynote, I’ll recreate a very simple interaction model popularized by Tinder: the left and right swipe animation. [Download the assets for this project](https://smashingmagazine.com/provide/2015-08_animating-in-keynote.zip) _(link fixed!)_ (ZIP, 360 KB).
<figure class="video-container"><iframe loading="lazy" width="500" height="300"]https://blog.uxtree.io/wp-content/uploads/smashingmag/Tinder%20swipe.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

The basic idea is to create the first screen of the animation (beginning) and the last screen of the animation (end). Keynote will intelligently take care of the rest with the Magic Move transition.</p>

### Set Up the Document

Open a blank white presentation. By default, Keynote will create a presentation-sized document (1024×768px). Let’s change that to more of an iPhone-sized document.

Go to the “Document” tab in the top right. Under the section “Slide Size,” go to “Custom Slide Size,” and make the size 350 (width) × 667 (height) pixels.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d87a3f6e-dd43-491a-9d32-5453a6b0ec32/01-document-size-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23b8e8ae-8261-420b-beef-d09428defad6/01-document-size-opt-small.png" alt="The “Custom Slide Size” in the “Document” menu" /></a><figcaption>Select the “Custom Slide Size” in the “Document” menu, and change it to 350 &#215; 667. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d87a3f6e-dd43-491a-9d32-5453a6b0ec32/01-document-size-opt.png">View large version</a>)</figcaption></figure>

Now, let’s import the images. This step is as simple as dragging the image files from your folder onto Keynote’s canvas.</p>

### First Slide

Once you’ve dragged your assets over, you can position them visually. Keynote has useful guidelines that appear contextually, helping you to align the design.
<figure class="video-container"><iframe loading="lazy" width="500" height="300"]https://blog.uxtree.io/wp-content/uploads/smashingmag/tinder%20workflow%201.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

Keynote will assign a **z-index to each asset** according to when it was imported — it doesn’t have a layers panel. In case you need to change the ordering of the stack, all you have to do is select the asset and right-click (`Cmd` + click) to bring up the menu, then select “Bring to Front.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d245909-aedf-4096-b92f-61727e7cbfda/02-bring-front-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39667317-e815-4ce1-8916-4835eccbf244/02-bring-front-opt-small.png" alt="Menu when selecting an asset" /></a><figcaption>Menu when selecting an asset. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d245909-aedf-4096-b92f-61727e7cbfda/02-bring-front-opt.png">View large version</a>)</figcaption></figure>

If you want to lay out assets with pixel-perfect values, rather than by eye, go to the “Format” → “Align” section and input exact numerical values.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9acbf097-960c-49f8-9ffa-075e26669233/03-format-arrange-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42fe4496-3f33-4571-9823-bf6fc432909d/03-format-arrange-opt-small.png" alt="Arrange menu" /></a><figcaption>Arrange menu. (<a href="//www.smashingmagazine.com/wp-content/uploads/2015/07/03-format-arrange-opt.png">View large version</a>)</figcaption></figure>

### End Slide

The second screen will be the last frame of the animation. Rotate the top image and position it off screen — this will be the end position.

The first thing to do is duplicate the first slide we’ve been working with. In the left-hand panel, right-click and select “Duplicate” in the menu.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2506507a-ea93-4d6e-8204-23e0ce32fb34/04-duplicate-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aefa8a1a-04dd-490b-90a7-7db5557fdf79/04-duplicate-opt-small.png" alt="Right-click or use Control + click to bring up the menu to duplicate." /></a><figcaption>Right-click or use Control + click to bring up the menu to duplicate. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2506507a-ea93-4d6e-8204-23e0ce32fb34/04-duplicate-opt.png">View large version</a>)</figcaption></figure>

Let’s begin by **rotating the top asset**. To rotate, hold down `Cmd`, and a rotated-arrow icon will appear in the corner of the selected asset. Then, click and drag to rotate.
<figure class="video-container"><iframe loading="lazy" width="500" height="300"]https://blog.uxtree.io/wp-content/uploads/smashingmag/rotating.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

</figure>

Now, position the tile off screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6f4ba6d-5d33-4906-9ff5-a8e9651a2d30/05-final-position-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6baa0992-4897-4cd0-a716-076bab8dce14/05-final-position-opt-small.png" alt="Move the asset to its final position" /></a><figcaption>Move the asset to its final position. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6f4ba6d-5d33-4906-9ff5-a8e9651a2d30/05-final-position-opt.png">View large version</a>)</figcaption></figure>

### Magic Move

Now that we have the start and end positions, let’s animate this.

Select the first slide, and go to the “Animate” tab on the left. Under “Transitions,” select “Add an Effect” and choose “Magic Move” in the dropdown.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c31692c-34e2-4553-9c5a-4cd21d7dcb83/06-magic-move-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/657995d8-9585-4821-a0ca-c48d456f7ba8/06-magic-move-opt-small.png" alt="The Magic Move transition effect in the “Animate” menu" /></a><figcaption>Select the Magic Move transition effect in the “Animate” menu. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c31692c-34e2-4553-9c5a-4cd21d7dcb83/06-magic-move-opt.png">View large version</a>)</figcaption></figure>

Magic Move is a transition effect that moves an object from a position on one slide to a new position on the next slide. It intelligently fills the gaps between the slides by moving, fading and scaling the object.</p>

### Timing and Acceleration

Magic Move has only two settings, duration and acceleration, which really help your animation look the best it can.

Duration is self-explanatory — it refers to timing, and the correct value is determined case by case. I find that the sweet spot for UI animation is usually somewhere between 0.7 and 1.5 seconds.

The acceleration section has four options:
<figure class="video-container"><iframe loading="lazy" width="500" height="300"]https://blog.uxtree.io/wp-content/uploads/smashingmag/easing.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>Demonstration of the various animation types.</figcaption></figure>

*   **“none”**: Same speed throughout the animation
*   **“ease out”**: Starts slow, then speeds up
*   **“ease out”**: Starts fast, then slows down
*   **“ease out and ease in”**: Starts slow, speeds up, then slows down again

For our example, I am using 0.90 seconds for the duration, and “ease in and ease out” for the acceleration setting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65336d10-5119-418f-b145-d04a0c714dca/07-magic-move-settings-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea7f512-ec30-4c3e-aec8-9975cb82e5c9/07-magic-move-settings-opt-small.png" alt="Magic Move settings" /></a><figcaption>Magic Move settings. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65336d10-5119-418f-b145-d04a0c714dca/07-magic-move-settings-opt.png">View large version</a>)</figcaption></figure>

### Our Animation

Below is the final animation, with some added effects. You can [download the Keynote file](https://www.dropbox.com/s/aebcpokvto659eg/Tinder%20-%20Design%20%2B%20Animation.key?dl=0) (ZIP) to see how the rest was done.
<figure class="video-container"><iframe loading="lazy" width="500" height="300"]https://blog.uxtree.io/wp-content/uploads/smashingmag/Tinder%20swipe.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

## What Else Is Possible?

Obviously it's a very, very simple example. We’ve just scratched the surface of what can be done in Keynote. Magic Move is the simplest of techniques. For more finesse, you can use Keynote’s **build ins and build outs**.</p>

### Build Ins and Build Outs

Build in refers to how an object **appears for the first time**, and build out refers to how an animation **leaves the screen**. These are both _object-based_ animations, rather than slide-based (like Magic Move). In other words, every asset can have its own independent animation.

For example, if you want an animation to scale in and bounce a bit, you would use a build-in effect called “Pop.” If you want the object to fade out, you would use the build-out effect “Dissolve.”

To apply a build-in or build-out effect, select any object on the screen and go to the “Animate” tab. There should be three sections: “Build In,” “Actions” and “Build Out.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955f6dca-c936-4a4e-b0a4-b935c969eb34/08-build-in-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8324d08-b1bf-42a6-a0fc-f022a689191c/08-build-in-opt-small.png" alt="Accessing the build-in section.
" /></a><figcaption>Accessing the build-in section. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955f6dca-c936-4a4e-b0a4-b935c969eb34/08-build-in-opt.png">View large version</a>)</figcaption></figure>

Build-in animations have a number of options. I use only a handful for UI design most of the time:
<figure class="video-container"><iframe loading="lazy" width="500" height="500"]https://blog.uxtree.io/wp-content/uploads/smashingmag/Build-in%20Animations%20copy.m4v" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

Complicated animations can have many build ins and build outs, and timing when each one appears is important. To do this, open the “Build Order” menu at the bottom of the “Animate” tab, and adjust the timing in the menu.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/062fb866-10ef-4ee6-b626-89ae92d2d76f/09-build-order-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fc32940-7595-4187-9d8a-842669a476eb/09-build-order-opt-small.png" alt="Build order menu" /></a><figcaption>Build order menu. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/062fb866-10ef-4ee6-b626-89ae92d2d76f/09-build-order-opt.png">View large version</a>)</figcaption></figure>

### Sketch and Photoshop Integration

Keynote integrates in my design workflow nicely. Importing from Photoshop, Sketch or Illustrator is as simple as copying and pasting into Keynote. I often design in Sketch and copy and paste over to Keynote to quickly infuse some motion into my static mockups.
<figure class="video-container"><iframe loading="lazy" width="500" height="281"]https://blog.uxtree.io/wp-content/uploads/sketch%20and%20PS%20copy.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

A few tips. **Copy and paste layer by layer**, or else Keynote will combine them, which you don’t want in most cases, especially if you’re animating individual pieces.

Also, if you copy and paste text, it will not retain its text properties, and you will not be able to edit it anymore. When dealing with text, make sure that your copy has been finalized or that you are able to recreate the text in Keynote.</p>

### Prototypes on Device

You can also create a prototype and **put it on your device** using the Keynote app for iOS. It’s as simple as using the “Adding Links” tool to link to different slides in a presentation. Below is an example of an app designed, animated and prototyped in Keynote.
<figure class="video-container"><iframe loading="lazy" width="500" height="281"]https://blog.uxtree.io/wp-content/uploads/paper%20on%20phone%20copy.mp4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

When sharing prototypes with clients and stakeholders, you can **export them as HTML** and they will be clickable in a browser. Note that the code will not be production-ready; the design will have to be recreated for the final product.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec2ed757-b03e-4759-b594-717e766f1c8c/10-html-export-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37b4d57d-bdd0-4869-800b-dab2842b2bee/10-html-export-opt-small.png" alt="Exporting to HTML from Keynote" /></a><figcaption>Exporting to HTML from Keynote. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec2ed757-b03e-4759-b594-717e766f1c8c/10-html-export-opt.png">View large version</a>)</figcaption></figure>

## Conclusion

Whether you’re a designer, product manager, developer or anyone else working on a product, Keynote is a great way to communicate ideas quickly. The speed, gentle learning curve and quality of output all make it an ideal tool for your arsenal.

To recap, Magic Move is the simplest and quickest of animation types in Keynote; it is used between slides to animate from a beginning state to an end state. Build ins, actions and build outs are used on individual objects in a slide; they control how things are presented for the first time and how they leave the screen.

With enough practice, you can do virtually any type of animation in Keynote. Many [other](https://vimeo.com/129807396) [examples](https://www.elizabethylin.com/khan/) show Keynote being used to create high-fidelity animations.

Keynote comes free with Mac OS X Yosemite and above. Give it a try, and happy animating!

{{< signature "da, ml, al" >}}

