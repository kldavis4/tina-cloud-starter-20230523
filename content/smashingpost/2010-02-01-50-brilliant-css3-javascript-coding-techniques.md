---
title: 50 Cool Javascript Examples And CSS3 Tricks
slug: 50-brilliant-css3-javascript-coding-techniques
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc4079c-93ce-41e4-95b2-06e7334ebe8e/css-buttons.jpg
date: 2010-02-01T13:26:37.000Z
author: vitaly-friedman
description: >-
  CSS3 is coming. Although the browser support of CSS 3 is still very
  limited, many designers across the globe
  experiment with new powerful features of the language, using graceful
  degradation for users with older browsers and using the new possibilites of
  CSS3 for users with modern browsers.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
  - Resources
---
Although the browser support of CSS 3 is <a href="https://www.findmebyip.com/litmus/" rel="nofollow">limited</a>, many designers across the globe experiment with new powerful features of the language, using graceful degradation for users with older browsers and using the new possibilites of CSS3 for users with modern browsers.

That's a reasonable solution — after all it doesn't make sense to avoid learning CSS3 (that will be heavily used in the future) only because these features are not supported yet. The point of this article is to give you a glimpse of what will be possible soon and what you will be using soon and provide you with an opportunity to learn about new CSS3 techniques and features.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Powerful New CSS- and JavaScript Techniques](https://www.smashingmagazine.com/2012/06/powerful-new-cssjavascript-techniques/)
*   [Building A Relationship Between CSS & JavaScript](https://www.smashingmagazine.com/2012/11/building-relationship-between-css-javascript/)
*   [Stronger, Better, Faster Design with CSS3](https://www.smashingmagazine.com/2009/12/stronger-better-faster-design-with-css3/)
*   [50 Useful Coding Techniques (CSS Layouts, Visual Effects and Forms)](https://www.smashingmagazine.com/2010/02/50-css-and-javascript-techniques-for-layouts-forms-and-visual-effects/)

<p>In this post we present <strong>50 useful and powerful CSS3/jQuery-techniques</strong> that can strongly improve user experience, improve designer's workflow and replace dirty old workarounds that we used in Internet Explorer 6 &amp; Co. Please notice that most techniques presented below are experimental, and many of them are not pure CSS3-techniques as they use jQuery or other JavaScript-library.</p>

{{% feature-panel %}}

## Visual Effects and Layout Techniques With CSS3

<a href="https://www.fofronline.com/2009-03/an-analogue-clock-using-only-css/" rel="nofollow">CSS3 Analogue Clock</a>
Analogue clock created using webkit transition and transform CSS. JavaScript is only used to pull in the current time.

<figure><a href="https://www.fofronline.com/2009-03/an-analogue-clock-using-only-css/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74fb475d-f628-4b90-83df-c30ba364bfcc/css-132.jpg" alt="Creating a clock in CSS" width="480" height="300" /></a></figure>

<a href="https://designlovr.com/use-css3-to-create-a-dynamic-stack-of-index-cards/" rel="nofollow">Use CSS3 to Create a Dynamic Stack of Index Cards</a>
We will create a dynamic stack of index cards solely with HTML and CSS3 and use such CSS3 features as transform and transition (for the dynamic effects) and @font-face, box-shadow and border-radius (for the styling).

<figure><a href="https://designlovr.com/use-css3-to-create-a-dynamic-stack-of-index-cards/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d94d27e2-9010-42ca-8ce4-ed9968f1bc64/css3-new-03.jpg" alt="Use CSS3 to Create a Dynamic Stack of Index Cards" width="480" height="300" /></a></figure>

<figure><a href="https://pushingpixels.at/experiments/dynamic_shadow/" rel="nofollow">dynamic PNG shadow position and opacity</a>
When the light is turned on, the position and opacity of the logo shadow will change dynamically, depending on the position and distance of the light bulb. Don't forget to drag the logo and/or the light bulb around!<figure><a href="https://pushingpixels.at/experiments/dynamic_shadow/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f610553c-6579-4a1f-a136-6f9ac8ac78b6/css3-new-00.jpg" alt="dynamic PNG shadow position and opacity" width="480" height="300" /></a></figure><a href="https://spyrestudios.com/how-to-create-a-sexy-vertical-sliding-panel-using-jquery-and-css3/" rel="nofollow">How To Create A Sexy Vertical Sliding Panel Using jQuery And CSS3</a>
So, what about a vertical sliding panel that would act as some sort of drawer instead of the usual top horizontal sliding panel that pushes everything else down when it opens? While thinking of alternatives to the usual horizontal panels, I thought it would be nice to create something that works in a similar way, but that is a bit more flexible.

<figure><a href="https://spyrestudios.com/how-to-create-a-sexy-vertical-sliding-panel-using-jquery-and-css3/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ab7aa69-d7cb-4c3e-904e-fbc93ef04535/css3-last-08.jpg" alt="How To Create A Sexy Vertical Sliding Panel Using jQuery And CSS3" width="481" height="300" /></a></figure><a href="https://www.zurb.com/playground/awesome-overlays" rel="nofollow">Awesome Overlays with CSS3</a>
The trick with these overlays is the gradient border, going form a lighter to darker orange as you go from top to bottom. To create that effect we used to the border-image property, which is a tricky little addition to CSS.

<figure><a href="https://www.zurb.com/playground/awesome-overlays" rel="nofollow"><img loading="lazy" decoding="async" title="Awesome Overlays with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f58a839c-a403-48ec-950b-8dbcb1a490a4/css3-last-11.jpg" alt="cool javascript examples" width="481" height="300" /></a></figure><a href="https://blog.seanmartell.com/2009/04/21/css3-flexible-ui-avoid-recutting-ui-graphics-for-mobile/" rel="nofollow">CSS3 and Flexible UI: Avoid Recutting UI Graphics for Mobile</a>
What if we could replace almost all of the graphical UI elements within Fennec with CSS created equivalents? As a designer, am I comfortable bypassing Photoshop and letting CSS run the pixel rodeo? After a few initial tests, the answer to both of those questions was a very solid “yes”. A solid “friggin’ right” if in Cape Breton.

<figure><a href="https://blog.seanmartell.com/2009/04/21/css3-flexible-ui-avoid-recutting-ui-graphics-for-mobile/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07e3ac34-e9a9-41b4-8a0c-b4b846857c94/css-144.jpg" alt="CSS3 and Flexible UI: Avoid Recutting UI Graphics for Mobile " width="480" height="300" /></a></figure><a href="https://www.queness.com/post/1696/create-a-beautiful-looking-custom-dialog-box-with-jquery-and-css3" rel="nofollow">Create a Beautiful Looking Custom Dialog Box With jQuery and CSS3</a>
This custom dialog box is one of the scripts in that website and I think it will be quite useful for all of us. The reason I have this custom dialog box is to overcome the inconsistencies across different browsers. And, of course, it uses CSS3 to style everything.

<figure><a href="https://www.queness.com/post/1696/create-a-beautiful-looking-custom-dialog-box-with-jquery-and-css3" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b0a1bd2-bfb9-471a-9074-67c50b35e52c/css3-last-00.jpg" alt="Create a Beautiful Looking Custom Dialog Box With jQuery and CSS3" width="481" height="300" /></a></figure><a href="https://www.zurb.com/playground/drop-in-modals" rel="nofollow">Drop-In Modals with CSS3</a>
For those using WebKit based browsers (Safari and Chrome), CSS3 effects and properties can help you create fast, simple modals by using transforms, animation, and some subtle design cues.

<figure><a href="https://www.zurb.com/playground/drop-in-modals" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44c961f8-d6b3-4d04-aaab-8b02f9c7010c/css3-last-13.jpg" alt="Drop-In Modals with CSS3" width="481" height="300" /></a></figure><a href="https://www.smashingmagazine.com/2009/12/16/stronger-better-faster-design-with-css3/" rel="nofollow">Newspaper Layouts with Columns and Image Masks</a>
The faux-newspaper look goes in and out of style online pretty frequently, but these tricks can be used for quite a few cool applications. What we’ll talk about here is using -webkit-mask-image and -webkit-column-count.

<figure><a href="https://www.smashingmagazine.com/2009/12/16/stronger-better-faster-design-with-css3/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0877e3f-4835-4de5-9c66-70b4f4e499e6/css3-last-14.jpg" alt="Newspaper Layouts with Columns and Image Masks" width="481" height="300" /></a></figure>

## Navigation Menus With CSS 3

<a href="https://tutorialzine.com/2010/01/sweet-tabs-jquery-ajax-css/" rel="nofollow">Sweet AJAX Tabs With jQuery 1.4 and CSS3</a>
This post is a tutorial of making an AJAX-powered tab page with CSS3 and the newly released jQuery 1.4.

<figure><a href="https://tutorialzine.com/2010/01/sweet-tabs-jquery-ajax-css/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ec327fe-7230-4740-808d-f7904c9cf223/sweet-tabs.jpg" alt=" Sweet Tabs" width="480" height="300" /></a></figure><a href="https://www.marcofolio.net/css/sweet_tabbed_navigation_using_css3.html" rel="nofollow">Sweet tabbed navigation bar using CSS3</a>
Although I don't understand why animations have been added in CSS3, this upcoming standard does have a couple of very neat features added to the CSS we're using today. I wanted to take a couple of these new things, and create a Sweet tabbed navigation using CSS3.

<figure><a href="https://www.marcofolio.net/css/sweet_tabbed_navigation_using_css3.html" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a7d7ffa-9637-4398-a929-e53e2bf05abe/css-041.jpg" alt="Sweet tabbed navigation bar using CSS3" width="480" height="300" /></a></figure><a href="https://tutorialzine.com/2010/01/halftone-navigation-menu-jquery-css/" rel="nofollow">Halftone Navigation Menu With jQuery and CSS3</a>
Today we are making a CSS3 and jQuery halftone-style navigation menu, which will allow you to display animated halftone-style shapes in accordance with the navigation links, and will provide a simple editor for creating additional shapes as well.

<figure><a href="https://tutorialzine.com/2010/01/halftone-navigation-menu-jquery-css/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c71d6ef6-e620-49c4-8a63-42aebbee4bf6/css3-last-05.jpg" alt="Halftone Navigation Menu With jQuery and CSS3" width="481" height="300" /></a></figure><a href="https://paulbakaus.com/2008/05/31/coverflow-anyone/" rel="nofollow">Building Coverflow With CSS Transforms</a>
I was able to create a coverflow effect that actually flows and animates in real-time, without using canvas or prerendered graphics.

<figure><a href="https://paulbakaus.com/2008/05/31/coverflow-anyone/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e87e5e8-3aab-416e-91e1-a8a61b9c2787/css3-last-04.jpg" alt="Building Coverflow With CSS Transforms" width="481" height="300" /></a></figure><a href="https://www.kamikazemusic.com/quick-tips/css3-hover-tabs-without-javascript/" rel="nofollow">CSS3 Hover Tabs without JavaScript</a>
With the new techniques in CSS3 and clever applications of existing CSS it is increasingly stepping on the toes of JavaScript. Which to be honest isn’t necessarily a bad thing. I thought I’d try my hand at something so here is a basic CSS tabbed content section that changes on hover.

<figure><a href="https://www.kamikazemusic.com/quick-tips/css3-hover-tabs-without-javascript/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbde2c29-3166-46a4-a2c0-6d5139829352/css-186.jpg" alt="CSS3 Hover Tabs without JavaScript " width="480" height="300" /></a></figure>

## CSS 3 Transitions and Animations

<a href="https://24ways.org/2009/going-nuts-with-css-transitions" rel="nofollow">Going Nuts with CSS Transitions</a>
I’m going to show you how CSS 3 transforms and WebKit transitions can add zing to the way you present images on your site.

<figure><a href="https://24ways.org/2009/going-nuts-with-css-transitions" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f545ccb7-0701-4b00-8524-512eab8fba59/css-010.jpg" alt="24 ways: Going Nuts with CSS Transitions" width="480" height="300" /></a></figure><a href="https://www.zurb.com/playground/sliding-vinyl" rel="nofollow">Sliding Vinyl with CSS3</a>
We take a standard album cover, a little HTML, and some CSS3 transitions and transforms to create a sliding vinyl effect for showing off the music you love.

<figure><a href="https://www.zurb.com/playground/sliding-vinyl" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b15692-494a-43a6-9a24-c7070fa2993e/css3-last-12.jpg" alt="Sliding Vinyl with CSS3 - ZURB Playground - ZURB.com" width="481" height="300" /></a></figure><a href="https://www.rickyh.co.uk/fun-with-css3-and-mootools/" rel="nofollow">Fun with CSS3 and Mootols</a>
These examples came about when experimenting with the extend property in MooTools. By extending the styles class I could add CSS3 properties into the Core MooTools framework and do CSS3 animations.

<figure><a href="https://www.rickyh.co.uk/fun-with-css3-and-mootools/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6b9cf14-d16d-4b43-8812-65747052f654/css3-last-171.jpg" alt="CSS3 Animations" width="481" height="300" /></a></figure><a href="https://ajaxian.com/archives/star-wars-html-and-css-a-new-hope" rel="nofollow">Star Wars HTML and CSS: A NEW HOPE</a>
There are a lot of CSS transitions experiments going on right now. Yesterday I discovered another HTML and CSS experiment which went "far far away", compared with my simple CSS gallery.
Guillermo Esteves presented a piece of history translated for tomorrows browsers: the Star Wars Episode IV opening crawl in HTML and CSS.

<figure><a href="https://ajaxian.com/archives/star-wars-html-and-css-a-new-hope" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51c4ebe7-0161-4308-a7da-83334bb74180/css-130.jpg" alt=" Star Wars HTML and CSS: A NEW HOPE" width="480" height="300" /></a></figure><a href="https://ajaxian.com/archives/fun-with-3d-css-and-video" rel="nofollow">Fun with 3D CSS and video</a>
Zach Johnson has been having fun with 3D effects via CSS such as his isocube above, which is brought to you with simple HTML (including a video tag for a playing video on the surface!) and some CSS.

<figure><a href="https://ajaxian.com/archives/fun-with-3d-css-and-video" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47b53040-7224-41a4-9cb4-2ebe32ede5bf/css-138.jpg" alt=" Fun with 3D CSS and video" width="480" height="300" /></a></figure><a href="https://www.marcofolio.net/css/css3_animations_and_their_jquery_equivalents.html" rel="nofollow">CSS3 animations and their jQuery equivalents</a>
This tutorial/these examples will show the use of the same HTML, with different classes for CSS3 and jQuery. You can compare both the codes and see which one you like more. Don't forget to check the demo/download the source code to view how everything is working under the hood.

<figure><a href="https://www.marcofolio.net/css/css3_animations_and_their_jquery_equivalents.html" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eeb8240-4faa-435f-b894-67c42b285075/css-040.jpg" alt="CSS3 animations and their jQuery equivalents" width="480" height="300" /></a></figure><a href="https://24ways.org/2009/css-animations" rel="nofollow">CSS Animations</a>
No matter how fast internet tubes or servers are, we’ll always need spinners to indicate something’s happening behind the scenes.

<figure><a href="https://24ways.org/2009/css-animations" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142ff45f-240f-4f12-84d6-dd9741d4ae16/css-009.jpg" alt="24 ways: CSS Animations" width="480" height="300" /></a></figure>Snowy CSS3 Animation
It’s cold and snowy down here in Brighton, so to celebrate the falling white stuff (and of course the various festivities at this time of year) Clearleft’s very own Natbat has made a snowy CSS3 animation surprise for all you Safari and Chrome users out there.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f520209-e2d2-42b6-882e-484d4e8397d7/css-005.jpg" alt="Merry Christmas" width="480" height="300" /></figure><a href="https://www.smashingmagazine.com/2009/12/19/what-you-need-to-know-about-behavioral-css/" rel="nofollow">What You Need To Know About Behavioral CSS</a>
In this article, we will take those properties a step further and explore transformations, transitions, and animations. We’ll go over the code itself, available support and some examples to show exactly how these new properties improve not only your designs but the overall user experience.

<figure><a href="https://www.smashingmagazine.com/2009/12/19/what-you-need-to-know-about-behavioral-css/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6dc47f9-99bc-4f6c-a7a7-207dd61eba28/css-038.jpg" alt="What You Need To Know About Behavioral CSS " width="480" height="300" /></a></figure><a href="https://ajaxian.com/archives/3d-cube-using-new-css-transformations" rel="nofollow">3D Cube using new CSS transformations</a>
The impression of a three dimensional cube can be created using modern CSS techniques, without the need for JavaScript, imagery, canvas or SVG. Using the proprietary transform property to skew and rotate shaded rectangles, individual cube faces can combine to form a 3D object.

<figure><a href="https://ajaxian.com/archives/3d-cube-using-new-css-transformations" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/930566ad-0029-42b6-b6fc-4fa3d433745c/css-139.jpg" alt=" 3D Cube using new CSS transformations" width="480" height="300" /></a></figure>Playing around with WebKit Animations
I’ve been playing around doing a KeyNote like animation done with CSS and some JS to hook up the necessary events. The animation is kind of like a deck of cards. When you go to the next one the current one zooms in and fades out, symbolizing getting closer to the viewer. The next card then zooms and fades in from the back and to give a fancy effect.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b964238-7f47-4c39-86cf-49f9da7aab72/css-133.jpg" alt=" Playing around with WebKit Animations" width="480" height="300" /></figure><a href="https://ajaxian.com/archives/more-on-3d-css-transforms" rel="nofollow">More on 3D CSS Transforms</a>
Various 3D CSS Transforms in an overview.

<figure><a href="https://ajaxian.com/archives/more-on-3d-css-transforms" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/444d450c-ebfe-4cb0-9633-0ccf7b8d9641/css3-last-15.jpg" alt=" More on 3D CSS Transforms" width="481" height="300" /></a></figure>

## Gradients, RGBA and HSL with CSS 3
<a href="https://24ways.org/2009/working-with-rgba-colour" rel="nofollow">Working With RGBA Colour</a>
CSS3 introduces a couple of new ways to specify colours, and one of those is RGBA. The A stands for Alpha, which refers to the level of opacity of the colour, or to put it another way, the amount of transparency. This means that we can set not only the red, green and blue values, but also control how much of what’s behind the colour shows through. Like with layers in Photoshop.

<figure><a href="https://24ways.org/2009/working-with-rgba-colour" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b65c5477-8b85-4c13-9fc2-71ba9157ea30/css-007.jpg" alt="24 ways: Working With RGBA Colour" width="480" height="300" /></a></figure><a href="https://girliemac.com/blog/2009/04/30/css3-gradients-no-image-aqua-button/" rel="nofollow">CSS3 Gradients: No Image Aqua Button</a>
I played around with WebKit CSS3 gradient and created a useless but fun stuff – an Aqua button with no images! Back in the time when Mac OS X was first announced, there’re a plenty of web tutorials that describe how to create the sexy aqua button with Photoshop, and now I can show how to create one with CSS!

<figure><a href="https://girliemac.com/blog/2009/04/30/css3-gradients-no-image-aqua-button/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b0b21a7-29ce-4783-ad54-872cf58b459c/css-164.jpg" alt=" CSS3 Gradients: No Image Aqua Button" width="480" height="300" /></a></figure>CSS3 HSL and HSLA
A tutorial on using the HSL and HSLA declarations along with the quick + / – guide to which browsers currently support the herein effect.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63404d0c-c8ee-49f7-95c1-6dd0ac999996/css3-last-06.jpg" alt="CSS3 HSL and HSLA" width="481" height="300" /></figure><a href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba" rel="nofollow">Super Awesome Buttons with CSS3 and RGBA</a>
One of our favorite things about CSS3 is the addition of RGBA, a color mode that adds alpha-blending to your favorite CSS properties. We've kicked the tires on it a bit with our own projects and have found that it helps streamline our CSS and makes scaling things like buttons very easy. To show you how, we've cooked up an example with some super awesome, scalable buttons.

<figure><a href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e306f421-0070-4f56-b086-03fc5d8ad50a/css-100.jpg" alt=" Super Awesome Buttons with CSS3 and RGBA" width="480" height="300" /></a></figure>

## Using the Shadow-Property in CSS3
<a href="https://line25.com/tutorials/create-a-letterpress-effect-with-css-text-shadow" rel="nofollow">Create a Letterpress Effect with CSS Text-Shadow</a>
The letterpress effect is becoming hugely popular in web design, and with a couple of modern browsers now showing support for the text-shadow CSS3 property it’s now simple and easy to create the effect with pure CSS. No Photoshop trickery here!

<figure><a href="https://line25.com/tutorials/create-a-letterpress-effect-with-css-text-shadow" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a308cdb9-7705-48d0-b286-006e25dc8b25/css-096.jpg" alt="Create a Letterpress Effect with CSS Text-Shadow" width="480" height="300" /></a></figure><a href="https://owltastic.com/2009/12/shadows-and-css3/" rel="nofollow">Shadows and CSS3</a>
I’m currently working on a design that uses text-shadow and box-shadow, with RGBA in place to create the shadow color. I wanted to tweet about this technique because it’s simple and awesome, but to my surprise I couldn’t find a good, quick tutorial that covered the use of both text and box-shadow, along with RGBA. So I decided to create one.
I learned this technique from Dan Cederholm’s Handcrafted CSS book, so if you’re able I’d recommend just going out and grabbing that, as he explains it much more elegantly and thoroughly than I ever could.

<figure><a href="https://owltastic.com/2009/12/shadows-and-css3/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0a1e279-6cce-4705-81bb-2d6793e81878/css-003.jpg" alt="Owltastic - by Meagan Fisher" width="480" height="300" /></a></figure>

## Learning New CSS3 Selectors
<a href="https://perishablepress.com/press/2010/01/11/css3-progressive-enhancement-smart-design/" rel="nofollow">CSS3 + Progressive Enhancement = Smart Design </a>
Progressive enhancement is a good thing, and CSS3 is even better. Combined, they enable designers to create lighter, cleaner websites faster and easier than ever before.

<figure><a href="https://perishablepress.com/press/2010/01/11/css3-progressive-enhancement-smart-design/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0697eb67-0819-4560-853b-8dcd021bec91/css3-new-01.jpg" alt="CSS3 + Progressive Enhancement = Smart Design " width="480" height="300" /></a></figure>A Look at Some of the New Selectors Introduced in CSS3
Here is a run-down of just some of the things that is possible with CSS3 selectors. Of course CSS3 isn’t supported at all by any IE browsers including IE8 but all latest versions of Safari, Firefox and Opera support most, if not all of them.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5fbbe34-87b0-45a9-9b0c-ede748b55719/css-168.jpg" alt="A Look at Some of the New Selectors Introduced in CSS3 " width="480" height="300" /></figure><a href="https://24ways.org/2009/cleaner-code-with-css3-selectors" rel="nofollow">Cleaner Code with CSS3 Selectors</a>
In this article I’m going to take a look at some of the ways our front and back-end code will be simplified by CSS3, by looking at the ways we achieve certain visual effects now in comparison to how we will achieve them in a glorious, CSS3-supported future. I’m also going to demonstrate how we can use these selectors now with a little help from JavaScript – which can work out very useful if you find yourself in a situation where you can’t change markup that is being output by some server-side code.

<figure><a href="https://24ways.org/2009/cleaner-code-with-css3-selectors" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59f3757-7901-42c1-8e7e-a70d89603419/css-008.jpg" alt="24 ways: Cleaner Code with CSS3 Selectors" width="480" height="300" /></a></figure><a href="https://webdesignernotebook.com/css/the-css3-target-pseudo-class-and-css-animations/" rel="nofollow">The CSS3 :target Pseudo-class And CSS Animations</a>
It’s no secret that I’m always looking for an easy way out using CSS instead of trying to replicate things with convoluted code — there are so many underused techniques that we could be applying to our designs as an enhancement layer! In this experience, I take a brief look into the :target pseudo-class and a very simple CSS animation.

<figure><a href="https://webdesignernotebook.com/css/the-css3-target-pseudo-class-and-css-animations/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eae20680-b936-4430-921c-5d67c21b09cb/css3-last-01.jpg" alt="The CSS3 :target Pseudo-class And CSS Animations" width="481" height="300" /></a></figure><a href="https://kilianvalkhof.com/2008/css-xhtml/the-css3-not-selector/" rel="nofollow">The CSS3 :not() selector</a>
There isn’t a lot of information to be found about the :not() selector. The specifications only offer 3 lines of text and a couple of examples. So lets see what it can do!

<figure><a href="https://kilianvalkhof.com/2008/css-xhtml/the-css3-not-selector/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17b57be8-3d1e-402f-a8df-298f509a1732/css3-last-02.jpg" alt="The CSS3 :not() selector" width="481" height="300" /></a></figure>IE CSS3 pseudo selectors
ie-css3.js allows Internet Explorer to identify CSS3 pseudo-class selectors and render any style rules defined with them. Simply include the script in your pages and start using these selectors in your style sheets — they'll work in IE... Honest...!

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88a197f1-8a5e-4467-9584-fe9608784f68/css3-new-02.jpg" alt="IE CSS3 pseudo selectors" width="480" height="300" /></figure>

## CSS3 Galleries
<a href="https://line25.com/tutorials/how-to-create-a-pure-css-polaroid-photo-gallery" rel="nofollow">How To Create a Pure CSS Polaroid Photo Gallery</a>
Magical things can be done by combining various CSS properties, especially when some of the new CSS3 tricks are thrown into the mix. Let’s take a look at building a cool looking stack of Polaroid photos with pure CSS styling.

<figure><a href="https://line25.com/tutorials/how-to-create-a-pure-css-polaroid-photo-gallery" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b05fc835-bb2d-4006-aaf8-5dfedf95562d/css-082.jpg" alt="How To Create a Pure CSS Polaroid Photo Gallery" width="480" height="300" /></a></figure><a href="https://tutorialzine.com/2009/11/hovering-gallery-css3-jquery/" rel="nofollow">An Awesome CSS3 Lightbox Gallery With jQuery</a>
In this tutorial we are going to create an awesome image gallery which leverages the latest CSS3 and jQuery techniques. The script will be able to scan a folder of images on your web server and build a complete drag and drop lighbox gallery around it.

<figure><a href="https://tutorialzine.com/2009/11/hovering-gallery-css3-jquery/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a59a68f1-0a2a-4501-afe9-3ae2c88738f9/css-155.jpg" alt="An Awesome CSS3 Lightbox Gallery With jQuery" width="480" height="300" /></a></figure><a href="https://ajaxian.com/archives/if-that-is-an-awesome-css3-gallery-how-would-you-call-mine" rel="nofollow">If That Is An Awesome CSS3 Gallery, How Would You Call Mine?</a>

<figure><a href="https://ajaxian.com/archives/if-that-is-an-awesome-css3-gallery-how-would-you-call-mine" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5aedfaf-e6fa-4916-85b0-9849aa264cf1/css-136.jpg" alt=" If That Is An Awesome CSS3 Gallery, How Would You Call Mine?" width="480" height="300" /></a></figure><a href="https://css-tricks.com/video-screencasts/74-editable-css3-image-gallery/" rel="nofollow">Editable CSS3 Image Gallery</a>
We build a pretty typical image gallery design pattern, a grid of images that pop up larger when clicked. But this image gallery page makes use of hot semantic HTML5 markup, loads of visual treats with CSS3 and jQuery, and made editable through the CMS PageLime. Quick reminder, the demo is awesome-est in a WebKit browser (Safari or Chrome).

<figure><a href="https://css-tricks.com/video-screencasts/74-editable-css3-image-gallery/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f45c40-a628-4110-8e62-9a26ab9126e3/css-163.jpg" alt="Editable CSS3 Image Gallery" width="480" height="300" /></a></figure>

## Replacing CSS Hacks with CSS 3

<a href="https://code.google.com/p/curved-corner/" rel="nofollow">Rounded corner HTML elements using CSS3 in all browsers</a>
This is a behavior htc file for Internet explorer to make CSS property " border-radius " work on all browsers. At present, all major browsers other than IE shows curved corner by adding 4 lines of css.

<figure><a href="https://code.google.com/p/curved-corner/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f08182e7-8d33-487a-b379-d18ae663568c/css3-last-03.jpg" alt="Rounded corner HTML elements using CSS3 in all browsers" width="481" height="300" /></a></figure><a href="https://buildinternet.com/2009/10/using-rounded-corners-with-css3/" rel="nofollow">Using Rounded Corners with CSS3</a>
As CSS3 gets closer to becoming the new standard for mainstream design, the days of rounded corners through elaborate background images is fading. This means less headache and time spent working out alternatives for each browser.

<figure><a href="https://buildinternet.com/2009/10/using-rounded-corners-with-css3/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6140c893-9dc4-467f-a446-a66fca603485/css-058.jpg" alt="Using Rounded Corners with CSS3 " width="480" height="300" /></a></figure><a href="https://perishablepress.com/press/2010/01/04/preload-images-css3/" rel="nofollow">Better Image Preloading with CSS3</a>
Using CSS3’s new support for multiple background images, we can use a single, existing element to preload all of the required images.

<figure><a href="https://perishablepress.com/press/2010/01/04/preload-images-css3/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b40e67d-0c0b-41e5-bcd6-70cf4471c97e/css-194.jpg" alt="Better Image Preloading with CSS3 " width="480" height="300" /></a></figure><span class="removed_link" title="https://aloestudios.com/2009/12/goodbye-overflow-clearing-hack/">Saying Goodbye to the overflow: hidden Clearing Hack</span>
I’m now saying goodbye to overflow: hidden and the deciding factor for me is CSS3. Specifically box-shadow. At least in the sense that box-shadow was the first property I noticed being negatively impacted by the use of overflow: hidden. Like the positioned child elements mentioned above, box-shadow can get clipped when the parent (or other ancestor) element has overflow applied. And there are several other things to consider as we move forward using more CSS3. Text-shadow and transform can also potentially be clipped by overflow: hidden.

<figure><span class="removed_link" title="https://aloestudios.com/2009/12/goodbye-overflow-clearing-hack/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a3bebfa-a2a1-4197-ad4e-cda6e9831845/css-184.jpg" alt="Saying Goodbye to the overflow: hidden Clearing Hack " width="480" height="300" /></span></figure>

## General articles about CSS 3

<span class="removed_link" title="https://welcome2thesky.com/2009/11/13/how-to-bring-css3-features-into-your-design/">How to bring CSS3 features into your design</span>
Top web browser (such as Firefox 3.5 and Safari 4) have introduce some cool features you can already use. Now, with just a few lines of css you can do things you used to do with images and javascript.

<figure><span class="removed_link" title="https://welcome2thesky.com/2009/11/13/how-to-bring-css3-features-into-your-design/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a5f161f-03e2-4ffc-be95-07f09d32d2ef/css-013.jpg" alt="How to bring CSS3 features into your design " width="480" height="300" /></span></figure><a href="https://www.viget.com/inspire/practical-uses-of-css3/" rel="nofollow">Practical Uses of CSS3</a>
In this article I'll show you some practical uses for CSS3.

<figure><a href="https://www.viget.com/inspire/practical-uses-of-css3/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db5b7345-0011-456c-8e9a-094d65f925fc/css-032.jpg" alt=" Practical Uses of CSS3" width="480" height="300" /></a></figure><a href="https://net.tutsplus.com/tutorials/html-css-techniques/11-classic-css-techniques-made-simple-with-css3/" rel="nofollow">11 Classic CSS Techniques Made Simple with CSS3</a>
We've all had to achieve some effect that required an extra handful of divs or PNGs. We shouldn't be limited to these old techniques when there's a new age coming. This new age includes the use of CSS3. In today's tutorial, I'll show you eleven different time-consuming effects that can be achieved quite easily with CSS3.

<figure><a href="https://net.tutsplus.com/tutorials/html-css-techniques/11-classic-css-techniques-made-simple-with-css3/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddb404c5-a7e6-4456-b410-4eb1915a10cd/css-122.jpg" alt="11 Classic CSS Techniques Made Simple with CSS3 " width="480" height="300" /></a></figure><a href="https://www.alexgdesign.co.uk/articles/mobile-optimised-websites-using-css3-media-queries/" rel="nofollow">Mobile optimised websites using CSS3 Media Queries</a>
A while ago I wrote about using CSS3 Media Queries on my website redesign to provide mobile visitors with an optimised view designed for smaller screens. I thought it might be useful if I went into a bit more detail on how I'm doing this.

<figure><a href="https://www.alexgdesign.co.uk/articles/mobile-optimised-websites-using-css3-media-queries/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7aaa773-e9e9-4a9c-8417-44ca27ebee87/css-023.jpg" alt="Mobile optimised websites using CSS3 Media Queries" width="480" height="300" /></a></figure>Code a Backwards Compatible, One Page Portfolio with HTML5 and CSS3
HTML5 is the future of web development but believe it or not you can start using it today. HTML5 is much more considerate to semantics and accessibility as we don’t have to throw meaningless div’s everywhere. It introduces meaningful tags for common elements such as navigations and footers which makes much more sense and are more natural. This is a run through of the basics of HTML5 and CSS3 while still paying attention to older browsers. Before we start, make note of the answer to this question. Do websites need to look exactly the same in every browser?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/136a36fa-2b31-4aa5-9f9a-fc67ae4895ed/css3-new-07.jpg" alt="Code a Backwards Compatible, One Page Portfolio with HTML5 and CSS3" width="480" height="300" /></figure><a href="https://www.netmag.co.uk/zine/develop-css/get-the-best-out-of-css3" rel="nofollow">Get the best out of CSS3</a>
Craig Grannell turns into a cross between Jeffrey Zeldman and Russell Grant, taking a peek at what the future of CSS has to offer – with a little help from Opera, Safari and Firefox

<figure><a href="https://www.netmag.co.uk/zine/develop-css/get-the-best-out-of-css3" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4d7917c-1b8a-44ac-ac37-e21cb8399dbf/css3-last-07.jpg" alt="Get the best out of CSS3" width="481" height="300" /></a></figure><a href="https://www.viget.com/articles/practical-uses-of-css3">Practical Uses of CSS3</a>
"One big item for me is how much we use CSS3. Yes I know, it is not fully supported across all browsers. If you still want everything to look exactly the same across all browsers, you should probably just close this article and not read about CSS for another 10 years. A user is not going to pull up your site in two different browsers to compare the experience, so they won't even know what they are missing. Just because something is not fully supported, that does not mean that we can't use it to an extent. In this article I'll show you some practical uses for CSS3."

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92330d8c-e850-4f60-afee-66e02ef8b744/css3-last-09.jpg" alt="Practical Uses of CSS3" width="481" height="300" /></figure><a href="https://code.tutsplus.com/articles/a-crash-course-in-advanced-css3-effects--net-6367">A Crash-Course in Advanced CSS3 Effects</a>
This video tutorial reviews a bunch of different neat effects that can be used in Safari 4, Chrome, and for all iPhone development.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01596dde-8f4b-4bf7-aca6-5a41b72e8fba/css3-last-10.jpg" alt="A Crash-Course in Advanced CSS3 Effects" width="481" height="300" /></figure>33 Must Read CSS3 Tips, Tricks, Tutorial Sites and Articles
An extensive overview of CSS3-techniques, tools, articles and resources.</figure>

