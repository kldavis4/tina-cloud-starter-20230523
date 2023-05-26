---
title: 99 Powerful New CSS- and JavaScript Techniques
slug: powerful-new-cssjavascript-techniques
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffa9b06f-c5d0-4607-b442-b5adda9868d5/css-roundup-004.jpg
date: 2012-06-21T12:38:26.000Z
author: vitaly-friedman
description: >-
  Since our [last round-up of useful CSS
  techniques](https://www.smashingmagazine.com/2011/04/18/powerful-new-css-techniques-and-tools/),
  we've seen a lot of truly remarkable CSS geekery out there.
categories:
  - CSS
  - JavaScript
  - Techniques
---
With CSS3, some of the older techniques now have become obsolete, others have established themselves as standards, and many techniques are still in the "crazy experimentation" stage.

Since the release of the previous post, we've been collecting, sorting, filtering and preparing a compact <strong>overview of powerful new CSS techniques</strong>. Today we finally present some of these techniques. Use them right away or save them for future reference.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [50 Useful Coding Techniques](https://www.smashingmagazine.com/2010/02/50-css-and-javascript-techniques-for-layouts-forms-and-visual-effects/)
*   [45 Powerful CSS and JavaScript Techniques](https://www.smashingmagazine.com/2010/01/12/45-powerful-css-javascript-techniques/)
*   [50 Brilliant CSS3/JavaScript Coding Techniques](https://www.smashingmagazine.com/2010/02/01/50-brilliant-css3-javascript-coding-techniques/)

Please note that many techniques are not only CSS-based, but also use HTML5 and JavaScript. We are going to present useful CSS tools and responsive design techniques in separate posts. Please don’t hesitate to comment on this post and let us know how exactly you are using them in your workflow. However, please avoid link dropping; share your insight and experience instead, and feel free to link to techniques that really helped you recently. Thanks to all of the featured designers and developers for their fantastic work!

{{% feature-panel %}}

### Table of Contents

1.  [CSS Transitions and Animations](#transitions)
2.  [Useful and Practical CSS Techniques](#practical)
3.  [CSS Typography and Text Techniques](#typography)
4.  [CSS Navigation Menus and Hover Effects](#navigation)
5.  [Visual Techniques With CSS](#visual)

## CSS Transitions And Animations

CSS transitions and animations are often used to make the user experience a bit more smooth and interesting, especially when it comes to interactive effects on hover or on click. Designers are experimenting with technology and create sometimes crazy, sometimes practical—but often innovative techniques which you could use to make your websites just a tiny bit more engaging.

<a href="https://attasi.com/labs/ipad/">Interactive CSS3 lighting effects</a>
An interesting effect to create interactive lighting effects with 3-D transforms, CSS gradients and masks; the cast shadow was created using box shadows and transforms.

<figure><a href="https://attasi.com/labs/ipad/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133580" title="Interactive CSS3 Lighting Effects" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41a6b663-6887-4c16-9fdd-003cbe57e045/result-css-048.jpg" alt="Interactive CSS3 Lighting Effects" width="498" height="298" /></a></figure>

<a href="https://themaninblue.com/experiment/dodecahedron/">CSS3 dodecahedron</a>
A fancy dodecahedron experiment, created using CSS Transforms and a tiny JavaScript snippet.

<figure><a href="https://themaninblue.com/experiment/dodecahedron/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133504" title="CSS3 Dodecahedron" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29506462-6798-42ac-98c9-36882dcd1a82/result-css-0361.jpg" alt="CSS3 Dodecahedron" width="498" height="298" /></a></figure>

<a href="https://photon.attasi.com/">CSS 3D Lighting Engine Photon</a>
Our editor Tom Giannattasio has created a JavaScript library that adds simple lighting effects to DOM elements in 3D space using the WebKitCSSMatrix object. It would be great to have an implementation for other rendering engines as well.

<figure><a href="https://photon.attasi.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc35715-9ebe-4263-a819-97b55882bd53/csstn-140.jpg" alt="CSS 3D Lighting Engine Photon" /></a></figure>

<a href="https://tympanus.net/codrops/2012/06/18/3d-thumbnail-hover-effects/">3D Thumbnail Hover Effects With CSS</a>
This technique produces 3D thumbnail hover effects with CSS 3D transforms. The code is quite verbose and probably could be optimized, but the effect is quite neat.

<figure><a href="https://tympanus.net/codrops/2012/06/18/3d-thumbnail-hover-effects/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af3adfb0-1066-42cc-ad6a-66e75a261116/csstn-139.jpg" alt="3D Thumbnail Hover Effects With CSS" /></a></figure>

<a href="https://css-tricks.com/snippets/css/slide-in-image-boxes/">Slide In Image Boxes</a>
A technique for creating a "slide in" effect for boxes on hover to make them a bit more interactive.

<figure><a href="https://css-tricks.com/snippets/css/slide-in-image-boxes/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9519c1fd-ecf5-43d5-8cad-9b1854b0f476/onhover.jpg" alt="Slide In Image Boxes" /></a></figure>

<a href="https://attasi.com/labs/picsselz/">CSS3 bitmap graphics</a>
The bitmap graphics is rendered with CSS: no images, no <code>canvas</code>, no data URIs and no extra markup. The pixels are drawn with CSS gradients, sized precisely to the pixel’s boundaries.

<figure><a href="https://attasi.com/labs/picsselz/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133568" title="Pure CSS3 Bitmap Graphics" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43942d1b-95f9-4e4a-93a3-60cf28ada79d/result-css-100.jpg" alt="Pure CSS3 Bitmap Graphics" width="498" height="298" /></a></figure>

<a href="https://developer.mozilla.org/en-US/demos/detail/paperfold-css">Paperfold CSS</a>
A visual folding effect for hidden comments by Felix Niklas. The plugin takes a DOM element, slices it into parts and arranges them like a folded paper in 3-D space.

<figure><a href="https://developer.mozilla.org/en-US/demos/detail/paperfold-css"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133623" title="Paperfold CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abddddc1-db0a-493c-8b18-e34d824377ee/css-roundup-018.jpg" alt="Paperfold CSS" width="500" height="300" /></a></figure>

Beercamp: An Experiment With CSS 3D
A CSS 3D popup book á la Dr. Seuss. The website was a test to see how far SVG and CSS 3D transforms could be pushed. This is the article about it.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133655" title="Beercamp: An Experiment With CSS 3D" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/603a2c54-0f39-484b-8e89-a8ac2b3186f8/css-roundup-042.jpg" alt="Beercamp: An Experiment With CSS 3D" width="500" height="300" /></figure>

<a href="https://bluedashed.com/covers/">Covers: A JS / CSS Experiment</a>
Now, that's quite an experiment: what if we combined a music song, stylesheet and beat detector to create animated... covers? Sure, we can do it with CSS3 and JavaScript! Covers does exactly that. The result is interesting, what can you do with this approach?

<figure><a href="https://bluedashed.com/covers/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6a964dd-ce27-4705-b74d-28292698d1c3/csstn-142.jpg" alt="Covers: A JS / CSS Experiment" /></a></figure>

<a href="https://johnbhall.com/iphone-4s/">Animation on Apple's page</a>
John B. Hall explains the CSS animation on Apple's Web page for the iPhone 4S.

<figure><a href="https://johnbhall.com/iphone-4s/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133349" title="An explanation of the CSS animation on Apple’s iPhone 4S webpage — John B. Hall" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c020f14e-8435-4944-9882-1503719cf254/result-css-008.jpg" alt="An explanation of the CSS animation on Apple’s iPhone 4S webpage — John B. Hall" width="498" height="298" /></a></figure>

<a href="https://tympanus.net/codrops/2011/12/19/experimental-css3-animations-for-image-transitions/">Experimental animations for image transitions</a>
A post about experimental 3-D image transitions that use CSS3 animations and jQuery. Only CSS3 transforms are used.

<figure><a href="https://tympanus.net/codrops/2011/12/19/experimental-css3-animations-for-image-transitions/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133576" title="Experimental CSS3 Animations for Image Transitions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a047575-40db-4624-aaf5-0c0042cb5e6e/css-roundup-004.jpg" alt="Experimental CSS3 Animations for Image Transitions" width="500" height="300" /></a></figure>

<a href="https://dabblet.com/gist/2076449">Maintaining CSS style states using “infinite” transition delays</a>
This demo allows you to move the character around with the D-pad, and notice how it always keeps its position after you stop moving. This demo doesn't use any JavaScript. The effect is made possible by using a virtually infinite transition delay, so that the CSS rules never return to their default state. The figure will be stuck in a transition and will move only when you hold down a button.

<figure><a href="https://dabblet.com/gist/2076449"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133473" title="Maintaining CSS Style States using “Infinite” Transition Delays" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b59b392-af0f-4e53-9d82-737b9dd94efc/result-css-166.jpg" alt="Maintaining CSS Style States using “Infinite” Transition Delays" width="498" height="298" /></a></figure>

<a href="https://www.clicktorelease.com/code/css3dclouds/">CSS 3-D clouds</a>
An experiment in creating 3-D-like clouds with CSS3 transforms and a bit of JavaScript.

<figure><a href="https://www.clicktorelease.com/code/css3dclouds/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133478" title="CSS3D Clouds" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/689e1829-667a-4c7e-90f4-908fe5fa6cc5/css3d-clouds.jpg" alt="CSS3D Clouds" width="500" height="281" /></a></figure>

<a href="https://www.cssflow.com/snippets/animated-profile-popover">Animated popover of profile box</a>
A technique for an animated profile popover menu, built using CSS transitions.

<a href="https://www.webinterfacelab.com/snippets/animated-profile-popover"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee52253a-4e50-492f-90ea-0d698eed4d35/csstn-129.jpg" alt="Animated Profile Popover With CSS" /></a>

<a href="https://lab.hakim.se/scroll-effects/">CSS3 scrolling effects</a>
A library of various scrolling effects, such as curl, wave, flip, fly, skew and helix, created with CSS3 and sometimes with JavaScript to spice up the scrolling behavior.

<a href="https://lab.hakim.se/scroll-effects/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79366015-2103-4fa9-936e-8ca2dccfdab4/csstn-102.jpg" alt="CSS3 Scroll Effects" /></a>

Spin those icons with CSS3
A simple technique for creating a neat effect that spins social icons with the help of a transform and transition when you hover over them. By Tom Kenny.

<a href="https://eng.wealthfront.com/2012/03/scrolling-z-axis-with-css-3d-transforms.html">Scrolling the Z Axis with CSS 3D Transforms</a>
This article explains how to create the z-scroll effect step by step.

## Useful and Practical CSS Techniques

<a href="https://thecodeplayer.com/walkthrough/css3-family-tree">CSS3 Family Tree</a>
Display organizational data or a family tree using just CSS, without Flash or JavaScript. The markup is very simple and uses just nested lists. Pseudo-elements are used to draw the connectors. It also has hover effects: hover over a parent element and the entire lineage will be stylized. Make sure to check Nicolas Gallagher's <a href="https://nicolasgallagher.com/an-introduction-to-css-pseudo-element-hacks/">Introduction to CSS Pseudo Element Hacks</a>.

<a href="https://thecodeplayer.com/walkthrough/css3-family-tree"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af06ba72-3cf7-4bb6-8ce7-0a48697f3d12/csstn-117.jpg" alt="CSS3 Family Tree" /></a>

<a href="https://www.cssflow.com/snippets/ios-style-popover/demo">iOS-style popover</a>
A simple technique for iOS-style custom checkboxes and a subtle hover effect. The technique is a bit buggy but a good starting point in case you need it. Also, check an excerpt from Lea Verou's <a href="https://vimeo.com/30379008">talk on customized checkboxes</a> and her article on <a href="https://lea.verou.me/2011/05/rule-filtering-based-on-specific-selectors-support/">rule filtering based on specific selector(s) support</a>.

<a href="https://demo.webinterfacelab.com/11-ios-style-popover/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb70f38-3cf0-4f73-befd-fc639780c03f/ios.jpg" alt="iOS-style Popover" width="500" height="249" /></a>

<a href="https://jsfiddle.net/necolas/vhZds/">Timeline-Style Comments</a>
Nicolas Gallagher developed a simple and clean technique to present comments in a timeline-alike overview.

<figure><a href="https://jsfiddle.net/necolas/vhZds/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c4e1f97-5b8a-41fc-a495-a039061f915c/timeline-snippet.jpg" alt="Timeline-Style Comments" /></a></figure>

<a href="https://jsfiddle.net/csswizardry/VqynK/">CSS Table Grid</a>
Here is a nice technique for aligning columns in a table, building a “table grid system” of sorts. The idea is to apply classes to <code>col</code> elements in a table’s <code>colgroup</code>; you always leave one <code>col</code> without a class so that it remains fluid and can “soak up” the effects of any breakages elsewhere in the table.

<a href="https://jsfiddle.net/csswizardry/VqynK/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/454af384-4a7b-4737-839f-5ac3ec99495f/css-pr.gif" alt="CSS Table Grid " width="494" height="324" /></a>

<a href="https://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/put-users-in-control-with-confirmation-feedback-buttons/">Confirmation Feedback Buttons</a>
This article explains how to create buttons that take on different states depending on the user’s interaction. This type of interaction is especially useful on links such as “Purchase” and “Delete” for which it’s wise to confirm that the user indeed wants to take the specific action. It looks too much like an iTunes button, though.

<figure><a href="https://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/put-users-in-control-with-confirmation-feedback-buttons/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134763" title="Confirmation Feedback Buttons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e4e0d60-5ed5-4c86-affe-77f048bafb5c/css-add-008.png" alt="" width="500" height="300" /></a></figure>

A calendar in CSS3 and jQuery
A step by step tutorial on how to create a CSS3 calendar with some jQuery animation. Also, check out <a href="https://dbushell.com/2012/01/04/responsive-calendar-demo/">David Bushell's responsive calendar demo</a>.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133365" title="A clean calendar in CSS3 &amp; jQuery : Finishing Touch" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/992871cd-e724-4aa7-9310-e3bb02a83c2a/result-css-024.jpg" alt="A clean calendar in CSS3 &amp; jQuery : Finishing Touch" width="498" height="298" /></figure>

Outdenting properties for debug CSS
Let's assume you are experimenting with CSS or debugging code. You add properties to figure out how things fit together. How often do you forget to remove all of them? A simple technique for this is to mark a CSS property as a temporary or debugging property by outdenting it and putting it at column 0 in the file. A small trick that can save a lot of time.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa223f9-c077-4201-a778-b91c327effbc/csstn-108.jpg" alt="Outdenting properties for debug CSS" />

<a href="https://css-tricks.com/show-markup-in-css-comments/">Show Markup in CSS Comments</a>
Chris Coyier discusses the idea of including the basic markup that you will be styling as a comment at the top of your CSS file.

<a href="https://css-tricks.com/show-markup-in-css-comments/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb2f77d-412b-42fe-8bdf-c5ae449b5d56/csstn-111.jpg" alt="Show Markup in CSS Comments" /></a>

<a href="https://filamentgroup.com/examples/rwd-table-patterns/">Selectively displaying data</a>
This technique shows how to selectively display content in a table and add responsive breakpoints to create an responsive, complex multi-column table.

<figure><a href="https://filamentgroup.com/examples/rwd-table-patterns/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134768" title="Selectively displaying data" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6946b648-4a47-4db8-af70-517e83a28e08/text.gif" alt="" width="500" height="332" /></a></figure>

<a href="https://css-tricks.com/snippets/css/remove-margins-first-element/">Remove Margins for First/Last Elements</a>
If you ever wanted to remove the top or left margin from the first element in a container, or the right or bottom margin from the last element in a container, you can do this by using pseudo-selectors <code>:first-child</code> and <code>:last-child</code>.

<a href="https://css-tricks.com/snippets/css/css-diagnostics/">CSS Diagnostics Stylesheet</a>
A very useful snippet to have nearby when you are debugging your CSS or want to find mistakes in HTML.

<figure><a href="https://css-tricks.com/snippets/css/css-diagnostics/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ed46800-5b9d-456b-9124-68e083c6113a/debugging.jpg" alt="CSS Diagnostics Stylesheet" width="498" height="250" /></a></figure>

<a href="https://css-tricks.com/radio-buttons-with-2-way-exclusivity/">Radio Buttons With Two-Way Exclusivity</a>
Learn about the <code>:empty</code> pseudo-class selector and jQuery to ensure that when a radio button is clicked, the area is determined and all other radio buttons in that column are turned off, and then is turned back on when clicked on.

<a href="https://css-tricks.com/radio-buttons-with-2-way-exclusivity/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c03efba-8ba0-4315-877d-3b5a23c0644a/csstn-124.jpg" alt="Radio Buttons with 2-Way Exclusivity" /></a>

<a href="https://www.cssflow.com/snippets/tabbed-navigation">Tabbed Navigation With CSS</a>
An elegant tabbed navigation menu with drop-down menus — no JavaScript, of course. Nothing new, but it's a quite clean solution.

<a href="https://www.webinterfacelab.com/snippets/tabbed-navigation"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/700871a5-bbc0-49e2-86b8-03db8e8aaee1/csstn-127.jpg" alt="Tabbed Navigation With CSS" /></a>

<a href="https://www.cssflow.com/snippets/menu-with-notification-badges">Menu With Notification Badges With CSS</a>
A ready-to-use snippet for a navigation menu with notification badges.

<a href="https://www.webinterfacelab.com/snippets/menu-with-notification-badges"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1afe291-4000-45d0-afdb-a7e0d3d18e41/notifications.jpg" alt="Menu with Notification Badges With CSS" /></a>

<a href="https://lea.verou.me/css3-secrets/#slide26">Styling based on sibling count (slides)</a>
A fantastic overview of the possibilities for styling based on sibling count. Also, make sure to click through the rest of the slide deck — valuable and useful techniques. Make sure to watch <a href="https://fronteers.nl/congres/2011/sessions/css3-secrets-lea-verou">Lea Verou's presentation</a> as well.

<a href="https://lea.verou.me/css3-secrets/#slide26"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb43fa8a-803e-4bd0-a46a-d068f41d513f/csstn-125.jpg" alt="Styling based on sibling count (Slides)" /></a>

<a href="https://css-tricks.com/the-checkbox-hack/">Stuff you can do with the “Checkbox Hack”</a>
Wiht the “checkbox hack,” you use a connected label and checkbox input and usually some other element that you are trying to control. Learn what you can do with it.

<a href="https://nicolasgallagher.com/lab/css3-facebook-buttons/">CSS3 Facebook Buttons</a>
Nicolas Gallagher presents a set of CSS buttons for Facebook with different colors and icons. You might want to check Nicolas' <a href="https://nicolasgallagher.com/lab/css3-social-signin-buttons/">CSS3 Social Sign-In buttons</a> as well as <a href="/2012/05/15/zocial-button-set-72-css3-buttons/">Free Social CSS3 Buttons</a> that we released earlier as well.

<a href="https://css-tricks.com/youtube-popup-buttons/">YouTube Popup Buttons</a>
This article explores the default state of YouTube buttons, which have a very subtle bevel but pop up on <code>:hover</code> and <code>:focus</code> states, eager to be clicked.

<a href="https://css-tricks.com/youtube-popup-buttons/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d46e8b2-8eed-47fd-8cb7-6cc7a3318fad/csstn-121.jpg" alt="YouTube Popup Buttons" /></a>

Centering in the Unknown
When it comes to centering things in Web design, the more information you have about the element being centered and its parent element, the easier it is. Chris Coyier shows how to do it when you do not know anything.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133358" title="Centering in the Unknown" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aca3714b-999f-4674-8901-caf24859a780/result-css-017.jpg" alt="Centering in the Unknown" width="498" height="298" /></figure>

<a href="https://daverupert.com/2012/04/uncle-daves-ol-padded-box/">Uncle Dave's Ol’ Padded Box</a>
What if you combined <code>background-size: cover</code> and Thierry Koblentz’ <a href="https://www.alistapart.com/articles/creating-intrinsic-ratios-for-video/">intrinsic ratios</a>. The result is images and video than maintain their aspect ratio; but you can also use <code>background-size: cover</code> to change the aspect ratio and auto-cropping of images with just a little CSS. And the great news is that the property is supported in all modern browsers and matches media-query support exactly.

<a href="https://css-tricks.com/snippets/css/clear-fix/">Micro Clearfix: Force Element To Self-Clear its Children</a>
Chris Coyier presents various technique for forcing elements to self-clear its children, including Nicolas Gallagher's short code snippet from 2011.

<figure><a href="https://css-tricks.com/snippets/css/clear-fix/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0920f4db-725f-402d-8e4d-4a65e7613f33/micro-clearfix.jpg" alt="Micro Clearfix: Force Element To Self-Clear its Children" height="285" /></a></figure>

<a href="https://adactio.com/journal/5429/">Conditional CSS</a>
A clever technique by Jeremy Keith to load additional content conditionally. The idea is that once a media query fires, the content on the <code>body</code> element is generated and can be detected by a JavaScript, prompting extra content to be loaded.

<a href="https://paulirish.com/2012/box-sizing-border-box-ftw/">* { box-sizing: border-box } FTW</a>
Once you start mixing and matching various units in CSS — such as <code>%</code> for the container width, <code>em</code> for padding and <code>px</code> for border — then you run right into the box-model problem because the width of the container doesn't include padding and border. We can easily solve this using <code>box-sizing: border-box</code>. And the best part: it is even supported in IE 8.

<a href="https://css-tricks.com/multiple-attribute-values/">Multiple Attribute Values</a>
How to treat multiple values in attributes rather than classes.

<figure><a href="https://css-tricks.com/multiple-attribute-values/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133562" title="Multiple Attribute Values" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9e9cef0-e257-4dcd-9a67-9198e493b9d9/css-roundup-003.jpg" alt="Multiple Attribute Values" width="500" height="300" /></a></figure>

<a href="https://www.aaronbarker.net/2010/07/diagonal-sprites/">Diagonal CSS Sprites</a>
If you build a sprite on a diagonal, there will be no components below or to the right of the component you are showing. This allows you to make the element using the sprite as wide or as tall as it needs to be, without worrying about exposing the next component. Also, check out <a href="https://demosthenes.info/blog/391/CSS-Sprites-for-the-Modern-Era-Refined-Animated-and-Semantic">David Storey's article on CSS sprites for the moder era</a>.

<a href="https://css-tricks.com/double-click-in-css/">Double Click in CSS</a>
Is there a way to detect whether a link is tapped or double-clicked on mobile devices? In fact, we can. However, the code requires some hardcore CSS nerdery. Also, check <a href="https://www.ryancollins.me/?p=1041">Pure CSS Clickable Events Without :target</a> by Ryan Collins.

<a href="https://www.zeldman.com/2012/03/01/replacing-the-9999px-hack-new-image-replacement/">Replacing the -9999px hack (new image replacement)</a>
In the beginning was FIR (Fahrner image replacement). Scott Kellum, design director at Treesaver, has now developed this refactored code for hiding text.

<figure><a href="https://www.zeldman.com/2012/03/01/replacing-the-9999px-hack-new-image-replacement/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133456" title="Replacing the -9999px hack (new image replacement)" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d6721f9-b8e3-462f-8d3c-4e8522d1442d/css-roundup-002.jpg" alt="Replacing the -9999px hack (new image replacement)" width="500" height="300" /></a></figure>

<a href="https://css-tricks.com/fighting-the-space-between-inline-block-elements/">Fighting the Space Between Inline Block Elements</a>
A series of inline-block elements formatted like you would normally format HTML will have spaces between them. But we often want the elements to butt up against each other, thus avoiding in the case of navigation) those awkward little unclickable gaps. How do you solve it? Chris Coyier has found a couple of solutions.

<a href="https://viget.com/inspire/css-pointer-events-and-a-pure-css3-animating-tooltip">CSS pointer-events and a pure CSS3 animating tooltip</a>
The pointer-events property allows you to specifiy how the mouse interacts with the element it is touching. See what you can do with it and what to consider when using them.

<a href="https://bradfrostweb.com/blog/mobile/anatomy-of-a-mobile-first-responsive-web-design/">Anatomy of a mobile-first responsive Web design</a>
An excellent article by Brad Frost about the different considerations for responsive designs. How do you start? What features would you implement and how? What about advanced optimization such as LocalStorage or AppCache? This article provide an excellent guide for getting started with future-friendly responsive designs.

<figure><a href="https://bradfrostweb.com/blog/mobile/anatomy-of-a-mobile-first-responsive-web-design/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134767" title="anatomy of a mobile-first responsive web design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/542dccaf-1df3-45ec-8877-3c402931d26f/css-add-012.png" alt="" width="500" height="300" /></a></figure>

<a href="https://github.com/filamentgroup/Southstreet">SouthStreet Progressive Enhancement Workflow</a>
A fantastic article by Scott Jehl and Filament Group in which they present a set of tools that form the core of an advanced responsive design workflow. Definitely useful to keep in mind for your next responsive design project.</p>

## Typography And Text With CSS

Advanced CSS techniques provide us with remarkable options to style text in very different ways. Not only can we make the typography look sharper and beautiful on the Web with tools such as <a href="https://letteringjs.com">Lettering.js</a>, <a href="https://kerningjs.com/">Kerning.js</a> and <a href="https://fittextjs.com/">FitText</a>; we can also play with glyphs, line breaks, font sizing, truncating text and styling lists. The typography can be adjusted and improved with just a couple of practical approaches.

<a href="https://tympanus.net/codrops/2011/11/09/interactive-html5-typography/">Interactive Typography effects with HTML5</a>
This techniques uses <code>canvas</code> and JavaScript to create ab interactive typography effect. Users can interact with the glyphs and as designer you can define forms or shapes of the word you'd like to present and how you'd like them to change on hover. Fancy!

<figure><a href="https://tympanus.net/codrops/2011/11/09/interactive-html5-typography/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133598" title="Interactive Typography Effects with HTML5" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e679187d-5fa2-4e43-83e6-351cb8434920/css-roundup-008.jpg" alt="Interactive Typography Effects with HTML5" width="500" height="300" /></a></figure>

<a href="https://tympanus.net/codrops/2011/12/28/with-rocking-letters-into-the-new-year/">Rocking letters with CSS3 and jQuery</a>
A simple animation of letters with CSS3 and jQuery.

<figure><a href="https://tympanus.net/codrops/2011/12/28/with-rocking-letters-into-the-new-year/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133507" title="With Rocking Letters into the New Year" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/855587cb-aa5b-4f82-b43d-c8892376e6e6/result-css-098.jpg" alt="With Rocking Letters into the New Year" width="498" height="298" /></a></figure>

<a href="https://webforfreaks.com/cssandtype/">CSS 3D Typography</a>
What about integrating stripes into glyphs and adjust the shadow on hover? This technique uses just that, creating a nice, subtle yet engaging visual effect. You can find more interesting type experiments in <a href="https://webforfreaks.com/cssandtype/">CSS3type Showcase</a>.

<figure><a href="https://webforfreaks.com/cssandtype/index.php?chemin=content/2011-01-01/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133468" title="cssandtype.com, gallery of css text effects" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8e5aee8-d279-49d2-9196-abf59d5ab35a/stripes.jpg" alt="cssandtype.com, gallery of css text effects" width="500" height="208" /></a></figure>

<figure><a href="https://webforfreaks.com/cssandtype/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133468" title="cssandtype.com, gallery of css text effects" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/904ef17e-1c81-438d-9adf-47512fe2226c/css-012.jpg" alt="cssandtype.com, gallery of css text effects" width="498" height="298" /></a></figure>

CSS3 animation and masking text
Chandler Van De Water had a challenge for Trent Walton after seeing the header animation in his “CSS3 in Transition” post. Noticing that he used a PNG image file with knockout transparency, he wanted to do the same CSS animation with selectable text. Trent was happy to oblige! At the moment, this works only in Safari and Chrome.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133582" title="CSS3 Animations and Masking Text" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/100ecd20-c0ea-44ad-a050-8cee19fd03d1/result-css-070.jpg" alt="CSS3 Animations and Masking Text" width="498" height="298" /></figure>

CSS mask-image and text
Trent Walton uses <code>background-clip: text</code> and <code>mask-image</code> to implement a subtle gray-flecked texture effect over white text. Hover over the box to see how it degrades in unsupported browsers. Make sure to check out Lea Verou's “<a href="https://lea.verou.me/2012/05/text-masking-the-standards-way/">Text Masking: The Standards Way</a>” as well.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/773c41d1-faeb-47eb-a0d9-acb66680de57/csstn-128.jpg" alt="CSS Mask-Image and Text" />

<a href="https://nimbupani.com/fake-bolding-of-web-fonts.html">Fake bolding of Web fonts</a>
Most browsers simulate bold weights for fonts that do not actually have bold weights. For example, Helvetica Neue Light does not have a bold weight. If you used <code>font-weight: bold</code> with it, browsers would artificially create a bold weight. This article explains how to avoid fake bolding of Web fonts in your designs. By Divya Manian.

<figure><a href="https://nimbupani.com/fake-bolding-of-web-fonts.html"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134756" title="Fake Bolding of Web Fonts" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c897e235-726d-4b43-8e67-a7e014a43499/css-add-001.png" alt="Fake Bolding of Web Fonts" width="500" height="300" /></a></figure>

<a href="https://elliotjaystocks.com/blog/say-it-with-a-swash/">Tomorrow’s Web type today: Say it With a Swash</a>
The excellent series "Tomorrow’s Web type today" by Elliot Jay Stocks provides insights into what will be possible with Web typography soon, e.g. swashes. In fact, you can already use them today if you include a swash subset of a font to achieve the desired effect.

<a href="https://elliotjaystocks.com/blog/say-it-with-a-swash/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134676" title="fonts" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586a4cb4-a347-4178-bd23-db521b79deab/fonts1.png" alt="OpenType Swashes" width="500" height="359" /></a>

<a href="https://css-tricks.com/snippets/css/internationalization-language-css/">Internationalization Language CSS</a>
A very handy CSS nippet with language-specific quotes. Perfect for international, multilingual projects.

<figure><a href="https://css-tricks.com/snippets/css/internationalization-language-css/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d83b7ef-532c-44e9-88f3-16cbf5ff06bc/international.jpg" alt="Internationalization Language CSS" width="498" height="305" /></a></figure>

<a href="https://tympanus.net/codrops/2011/12/12/experiments-with-background-clip-text/">Experiments with <code>background-clip: text</code></a>
With the CSS property <code>background-clip: text</code>, we can add a background image to a text element.

<figure><a href="https://tympanus.net/codrops/2011/12/12/experiments-with-background-clip-text/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133590" title="Experiments with background-clip: text" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9136306-b762-47dc-82ac-c5b7208e8a5f/result-css-050.jpg" alt="Experiments with background-clip: text" width="498" height="298" /></a></figure>

A Call for ::nth-everything
With CSS3, we have positional pseudo-class selectors to help us select a particular element when it has no distinguishing characteristics other than where it is in the DOM in relation to its siblings.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133352" title="A Call for ::nth-everything" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00622d69-bef4-4adb-b8e5-607782591eaf/result-css-011.jpg" alt="A Call for ::nth-everything" width="498" height="298" /></figure>

<a href="https://webforfreaks.com/cssandtype/index.php?chemin=content/2011-06-11/">Smooth font using the text-shadow property</a>
A common problem: is there a way smooth the appearance of glyphs on older machines, especially Windows XP (standard / ClearType rendering mode)? Yes, perhaps. You can give a try the <code>text-shadow</code>-property which adds text-shadow on the top-left and the bottom-right to smooth text.

<figure><a href="https://webforfreaks.com/cssandtype/index.php?chemin=content/2011-06-11/"><br>
<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133588" title="Smooth font using CSS3 text-shadow property" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/104fac6d-2a5a-43ab-9d46-9b39d738ab67/result-css-054.jpg" alt="Smooth font using CSS3 text-shadow property" width="498" height="298" /></a></figure>

<a href="https://trentwalton.com/2012/06/19/fluid-type/">Fluid Type</a>
Trent Walton explains his approach to fluid typography in which he asks himself how we can make sure that browser width and typographic settings such as measure or font-size and how should we handle panoramic viewports? An interesting article, especially if you use a typography-out approach in your designs.

<figure><a href="https://trentwalton.com/2012/06/19/fluid-type/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba3a6f8c-d8db-44e2-b6fa-04545abf1efc/csstn-141.jpg" alt="Fluid Type" /></a></figure>

<a href="https://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css/">Pragmatic, practical font sizing in CSS</a>
Harry Roberts shares his thoughts on how to size fonts more efficiently, writing your CSS differently in the process.

<a href="https://www.456bereastreet.com/archive/201204/automatic_line_breaks_in_narrow_columns_with_css_3_hyphens_and_word-wrap/">Automatic line breaks with CSS3 hyphens and word-wrap</a>
Roger Johansson shows how to solve a common problem: as columns of text become narrower, the risk of a single word being longer than the column’s width increases. When that happens, the text normally extends beyond the column. Luckily, CSS offers two properties to improve the situation: <code>word-wrap</code> and <code>hyphens</code>.

<a href="https://nicewebtype.com/notes/2012/02/03/molten-leading-or-fluid-line-height/">Molten leading (or fluid line height)</a>
When a responsive composition meets a viewport, there are different ways to fill space. Adjusting any one element without also adjusting the others is a recipe for uncomfortable reading, which is one reason why designers have such a difficult time with fluid Web layouts. Tim Brown started a discussion about this issue and provides a couple of techniques for opimization.

<figure><a href="https://nicewebtype.com/notes/2012/02/03/molten-leading-or-fluid-line-height/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133633" title="Molten leading (or, fluid line-height)" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/936572ec-84c8-4435-91bf-c30dab2f711f/mold2.jpg" alt="Molten leading (or, fluid line-height)" width="500" /></a></figure>

<a href="https://css-tricks.com/snippets/css/prevent-long-urls-from-breaking-out-of-container/">Prevent Long URL's From Breaking Out of Container</a>
Another snippet by Chris Coyier for keeping long URLs within the container. <code>word-wrap</code>, <code>word-break</code> and <code>hyphens</code> properties in use. Also, learn how to <a href="https://css-tricks.com/snippets/css/prevent-superscripts-and-subscripts-from-affecting-line-height/">Prevent Superscripts and Subscripts from Affecting Line-Height</a>.

<a href="https://css-tricks.com/viewport-sized-typography/">Viewport-sized typography</a>
This technique uses new CSS values for sizing elements relative to the viewport’s current size: <code>vw</code>, <code>vh</code> and <code>vmin</code>. This allows you to couple the size of, say, a typographic heading to the available screen space. Browser support is quite poor for now, so if you are looking for an alternative, check out <a href="https://fittextjs.com/">FitText.js</a>.

<a href="https://css-tricks.com/viewport-sized-typography/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/280414c4-d754-47bb-840f-b3f7afaeddbd/csstn-105.jpg" alt="Viewport Sized Typography" /></a>

<a href="https://css-tricks.com/minimum-paragraph-widths/">Minimum paragraph widths in fluid layouts</a>
This article shows how to solve the problem of paragraphs that are too narrow, by implementing a minimum paragraph width. If the space left a the floating image is less than this width, then the whole paragraph moves below the image.

<a href="https://www.456bereastreet.com/archive/201105/styling_ordered_list_numbers/">Styling ordered list numbers</a>
Roger Johansson shows how we can style ordered list numbers with the <code>:before</code> pseudo element, which can take a counter as a value through the <code>content</code> property. Also check out <a href="https://css-tricks.com/numbering-in-style/">Chris Coyier's post</a> and Louis Lazaris' <a href="https://www.impressivewebs.com/css-counter-increment/">CSS Counters: counter-increment and friends</a>.

<figure><a href="https://www.456bereastreet.com/archive/201105/styling_ordered_list_numbers/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133362" title="Styling ordered list numbers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd14c43f-0583-46bd-8e6e-686614eda881/list-item.jpg" alt="Styling ordered list numbers" width="500" height="261" /></a></figure>

<a href="https://www.impressivewebs.com/reverse-ordered-lists-html5/">Reverse ordered lists in HTML5</a>
The reverse attribute allows you to write a descending list of numbered items. Louis Lazaris summarizes what it does and offers a solution to get around a lack of browser support for this attribute.

<figure><a href="https://www.impressivewebs.com/reverse-ordered-lists-html5/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133594" title="Reverse Ordered Lists in HTML5" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1e39b5a-b280-4628-a9d5-c0798b5cbde8/reversed-lists.jpg" alt="Reverse Ordered Lists in HTML5" width="500" height="342" /></a></figure>

<a href="https://demosthenes.info/blog/442/Preserving-Whitespace-With-CSS3-tab-size-&amp;-3-Other-Solutions">Preserving white space with CSS3 tab size</a>
By default, HTML pages ignore anything more than a single space and collapses them. But there are occasions when you’ll want to preserve this space via one of several possible techniques.

Truncating text using only CSS
This code snippet can be used to shorten a line of text using nothing but CSS.

<a href="https://www.impressivewebs.com/new-css3-text-wrap/">New CSS3 properties to handle text and word wrapping</a>
Louis Lazaris explains the possibilities and problems of text-wrap, overflow-wrap, line-break and word-break, text-overflow and hyphens. Also worth reading: Kenneth Auchenberg <a href="https://blog.kenneth.io/blog/2012/03/04/word-wrapping-hypernation-using-css/">discusses the options for word wrapping and hyphenation</a> in combination with dynamic width elements.

<a href="https://css-tricks.com/snippets/css/end-articles-with-ivy-leaf/">End Articles with Ivy Leaf</a>
A clever technique for adding an extra touch to the end of your articles. <code>:last-child</code>, <code>:after</code> and <code>content</code> in use.</p>

## Hover Effects and Navigation Menus with CSS

We are used to classical navigation patterns such as tabbed navigation or drop-downs, but we can do a lot more to spice up our navigation menus with pleasant hover effects, often without extra images. Especially if you'd like to add a bit more polish to your portfolio, gallery or e-commerce website, these techniques can be quite useful. What about "over-the top" hover effect for your links,

<a href="https://tympanus.net/Tutorials/CircleNavigationEffect/">Circle Navigation Effect With CSS3</a>
A bubble-like thumbnail preview for your navigation with CSS3.

<figure><a href="https://tympanus.net/Tutorials/CircleNavigationEffect/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133581" title="Circle Navigation Effect with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d892fd21-160c-437b-9f59-9f489787a1d7/circle-navigation.jpg" alt="Circle Navigation Effect with CSS3" width="498" height="309" /></a></figure>

Create a CSS3 Image Gallery With a 3D Lightbox Animation
Tom Kenny has extended a CSS lightbox gallery by adding a few hover effects to the gallery grid itself and a 3D rotation to the lightbox content, all with CSS.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133357" title="Create a CSS3 Image Gallery with a 3D Lightbox Animation – Inspect Element" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53a65be6-c7f0-4a42-9913-f48a112b20f6/result-css-016.jpg" alt="Create a CSS3 Image Gallery with a 3D Lightbox Animation – Inspect Element" width="498" height="298" /></figure>

<a href="https://tympanus.net/codrops/2012/02/06/3d-gallery-with-css3-and-jquery/">3D Gallery With CSS3 and jQuery</a>
This article shares an experimental gallery that uses CSS 3D transforms. The idea is to create a circular gallery with an image in the center and two on the sides. Because perspective is being used, the two lateral images will appear three dimensional when rotated.

<figure><a href="https://tympanus.net/codrops/2012/02/06/3d-gallery-with-css3-and-jquery/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133515" title="3D Gallery with CSS3 and jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29794f70-884e-4d20-bf83-398caa6941e8/result-css-121.jpg" alt="3D Gallery with CSS3 and jQuery" width="498" height="298" /></a></figure>

<a href="https://tympanus.net/codrops/2011/10/24/creative-css3-animation-menus/">Creative CSS3 animation menus</a>
Mary Lou presents a couple of creative navigation menu hover effects. The idea is to have a simple composition of elements, an icon, a main title and a secondary title that will be animated on hover using only CSS transitions and animations.

<figure><a href="https://tympanus.net/codrops/2011/10/24/creative-css3-animation-menus/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133350" title="Creative CSS3 Animation Menus" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c8e0825-2966-403a-894d-0a11c8f117ef/result-css-009.jpg" alt="Creative CSS3 Animation Menus" width="498" height="298" /></a></figure>

<a href="https://tympanus.net/codrops/2012/01/22/how-to-spice-up-your-menu-with-css3/">How to spice up your menu with CSS3</a>
Yes, another technique by Tympanus: this tip shows how to spice up a menu by adding a neat hover effect to it. The idea is to slide an image out to the right when the menu item is hovered over.

<figure><a href="https://tympanus.net/codrops/2012/01/22/how-to-spice-up-your-menu-with-css3/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133512" title="How to spice up your menu with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4821a49-1fd3-4150-b4a4-2593bda76ec2/result-css-118.jpg" alt="How to spice up your menu with CSS3" width="498" height="298" /></a></figure>

<a href="https://www.netmagazine.com/node/1417">Create a zoomable user interface</a>
David DeSandro reveals how to use CSS transforms to create a zoomable user interface similar to that of <a href="https://2011.beercamp.com/">Beercamp 2011</a>. In this tutorial, you’ll also learn how to use JavaScript to hijack scrolling to manipulate the zoom.

<figure><a href="https://www.netmagazine.com/node/1417"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133584" title="Create a zoomable user interface with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50c9d46f-3024-4f18-bb81-9a805ab7a9de/result-css-058.jpg" alt="Create a zoomable user interface with CSS3" width="498" height="298" /></a></figure>

<a href="https://tympanus.net/Development/FlipboardPageLayout/?page=0">Flipboard Navigation</a>
An experimental page layout inspired by Flipboard's interface.

<figure><a href="https://tympanus.net/Development/FlipboardPageLayout/?page=0"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134761" title="Flipboard Page Layout" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/065f380e-d40c-4e04-9cf9-1f9a96b84ac3/css-add-006.png" alt="Flipboard Page Layout" /></a></figure>

<a href="https://jsfiddle.net/kizu/zfUyN/">Multi-direction hover</a>
This element shows different hover effects when hovering from different directions.

<figure><a href="https://jsfiddle.net/kizu/zfUyN/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133503" title="Multi-direction hover" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3748b8c-15da-4b73-b12c-3439035dcc6f/result-css-129.jpg" alt="Multi-direction hover" width="498" height="298" /></a></figure>

<a href="https://jsdo.it/ksk1015/cLLl">Experimental Hover Effects</a>
Original and innovative hover effects discovered via Twitter on what appears to be a Japanese code sharing website.

<figure><a href="https://jsdo.it/ksk1015/cLLl"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133346" title="Share JavaScript, HTML5 and CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bd1038a-bd2e-4ec0-b043-6f401047f7cf/result-css-005.jpg" alt="Share JavaScript, HTML5 and CSS" width="498" height="298" /></a></figure>

<a href="https://jsfiddle.net/hakim/Ht6Ym/">Over-the-top hover effect</a>
A CSS and JavaScript technique for creating an “over-the-top” hover effect using the <code>transform-origin</code> <code>transform-style</code> properties as well as 3-D transforms.

<a href="https://tympanus.net/codrops/2012/02/21/accordion-with-css3/">Accordion With CSS3</a>
Mary Lou experiments with the adjacent and general sibling combinator and the <code>:checked</code> pseudo-class. Using hidden inputs and labels, she creates an accordion that animates the content areas on opening and closing.

<figure><a href="https://tympanus.net/codrops/2012/02/21/accordion-with-css3/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133466" title="Accordion with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44663496-ec8c-45b4-bfe2-d4a5beeb439c/result-css-138.jpg" alt="Accordion with CSS3" width="498" height="298" /></a></figure>

<a href="https://www.alistapart.com/articles/expanding-text-areas-made-elegant/">Expanding Text Areas Made Elegant</a>
An expanding text area is a good choice when you don't know how much text the user will write and you want to keep the layout compact. In this article, Neil Jenkins explains how to do this simply. Also, you might want to take a look at <a href="https://www.impressivewebs.com/textarea-auto-resize/">Textarea Auto Resize</a>, another technique by Louis Lazaris, using a hidden clone element.

<a href="https://tympanus.net/codrops/2012/01/09/filter-functionality-with-css3/">Filter Functionality With CSS3</a>
Using the general sibling combinator and the <code>:checked</code> pseudo-class, we can toggle states of other elements by checking a box or radio button. This tutorial explores those CSS3 properties by creating a experimental portfolio filter that toggles the states of items of a specific type.

<figure><a href="https://tympanus.net/codrops/2012/01/09/filter-functionality-with-css3/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133565" title="Filter Functionality with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/988d842a-c8a5-4f8c-b243-5227d6244aab/result-css-108.jpg" alt="Filter Functionality with CSS3" width="498" height="298" /></a></figure>

<a href="https://www.456bereastreet.com/archive/201111/an_accessible_keyboard_friendly_custom_select_menu/">An accessible, keyboard-friendly custom select menu</a>
A new approach for more accessibility by Roger Johansson. He styles only the <code>select</code> element.</p>

## Visual Techniques with CSS

We used to heavily on images and visual elements to create basic visual effects on the Web. With CSS3, we can not only improved the loading speed of the content, but also make our visual elements more flexible and adaptive. Let's take a look on a couple of examples of how we can achieve that.

Create the Illusion of Stacked Elements with CSS3 Pseudo-Elements
Tom Kenny shows how to create a simple “stacked” look to a group of images.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133629" title="Create the Illusion of Stacked Elements with CSS3 Pseudo-Elements – Inspect Element" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4fdd30a-9885-43a4-afeb-0f272f050c66/css-roundup-023.jpg" alt="Create the Illusion of Stacked Elements with CSS3 Pseudo-Elements – Inspect Element" width="500" height="300" /></figure>

CSS3 Unfold Map with Pins
A handy snippet for placing pins on a map. The code looks a bit verbose, so you might want to remove a couple of visual "nice-to-have" elements.

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf6c043-4982-4ae7-bf0b-b46b121e7812/csstn-146.jpg" alt="CSS3 Unfold Map with Pins" /></figure>

<a href="https://demosthenes.info/blog/446/Turn-Pictures-Into-Postage-Stamps-With-CSS3-border-image">Turn Images Into Postage Stamps With CSS3 border-image</a>
Dudley Storey shows a simple way to create a postage stamp from a simple image with <code>border-image</code>.

<figure><a href="https://demosthenes.info/blog/446/Turn-Pictures-Into-Postage-Stamps-With-CSS3-border-image"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133595" title="Turn Images Into Postage Stamps With CSS3 border-image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e69df96-cb2e-4020-917e-e9b0201d488b/result-css-0371.jpg" alt="Turn Images Into Postage Stamps With CSS3 border-image" width="498" height="298" /></a></figure>

<a href="https://tympanus.net/codrops/2011/12/21/slopy-elements-with-css3/">Slopy elements with CSS3</a>
Angled shapes and diagonal lines can create an interesting visual flow and add some unexpected excitement. This tutorial shows some simple examples and ways how to create slopy, skewed elements with only CSS.

<figure><a href="https://tympanus.net/codrops/2011/12/21/slopy-elements-with-css3/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133566" title="Slopy Elements with CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/289e2f56-c582-49cb-9af7-fbcd89b722da/result-css-099.jpg" alt="Slopy Elements with CSS3" width="498" height="298" /></a></figure>

CSS Flip Clock
A code snippet for displaying a flip clock-alike time display using CSS.

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92e2ec0b-b5ee-4337-8d8c-25c7a534739a/csstn-145.jpg" alt="CSS Flip Clock" /></figure>

<a href="https://webdesignerwall.com/tutorials/css3-image-styles">CSS3 Image Styles</a>
When applying a CSS3 inset <code>box-shadow</code> or <code>border-radius</code> directly to an image element, the browser won’t render the CSS style perfectly. Here's a quick tutorial on how to use jQuery to make perfect rounded corner images dynamically. And check out <a href="https://webdesignerwall.com/tutorials/css3-image-styles-part-2">the second part</a>.

<figure><a href="https://webdesignerwall.com/tutorials/css3-image-styles-part-2"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133500" title="CSS3 Image Styles – Part 2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dcfe4cd-efb5-46ee-ab3f-b6bf6217f48d/css-image-styles1.jpg" alt="CSS3 Image Styles – Part 2" width="500" height="271" /></a></figure>

<a href="https://webdesignerwall.com/tutorials/creating-reusable-versatile-background-patterns">Creating Reusable and Versatile Background Patterns</a>
A simple tutorial on how to create reusable background patterns with Photoshop and CSS.

<figure><a href="https://webdesignerwall.com/tutorials/creating-reusable-versatile-background-patterns"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133587" title="Creating Reusable &amp; Versatile Background Patterns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/197d5396-eac6-4472-95ce-7fa3e997ce21/result-css-059.jpg" alt="Creating Reusable &amp; Versatile Background Patterns" width="498" height="298" /></a></figure>

<a href="https://jsfiddle.net/ChristopherBurton/MNMQM/">Diagonal Graph Paper Gradient</a>
A very nice CSS technique for creating diagonal graph paper gradients using <code>repeating-linear-gradient</code> property in CSS.

<a href="https://jsfiddle.net/ChristopherBurton/MNMQM/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bfe7591-d91a-4c00-a7df-86f383e12ba2/linen.jpg" alt="Diagonal Graph Paper Gradient" width="500" height="302" /></a>

Tucked Corner Effect
A clean CSS technique for producing tucked corners using the pseudo-elements <code>:after</code> and <code>:before</code> as well as data URI-coded images. Also, check out <a href="https://jsfiddle.net/chriscoyier/H6rQ6/1/">Corner Ribbon Effect with CSS</a>.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32cf20b5-a557-490a-a15e-3b7f2a9abffb/tucked.jpg" alt="CSS Tucked Corner Effect" width="500" />

<a href="https://lea.verou.me/2012/04/background-attachment-local/">Scrolling... shadows!</a>
An original technique by Roman Komarov to create CSS-only shadow-scrolling effect using <code>background-attachment: local</code>. Developed by Lea Verou, inspired by Roman Komarov.

<figure><a href="https://lea.verou.me/2012/04/background-attachment-local/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134758" title="Scrolling shadows" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17384e12-ba74-407f-83cc-2c21269fee82/css-add-003.png" alt="Scrolling shadows" width="500" height="300" /></a></figure>

<a href="https://www.webinterfacelab.com/snippets/multi-colored-progress-bars">Multi-colored CSS progress bars</a>
A quite verbose yet CSS-only solution for displaying multi-colored progress bars. It’s <code>linear-gradient</code> in action! Also, check out <a href="https://dipperstove.com/design/css3-progress-bars.html">CSS3 progress bars</a> that display data inside localized leaderboards for the new analytics platform at G5. They are lightweight and require no JavaScript or images.

<a href="https://www.webinterfacelab.com/snippets/multi-colored-progress-bars"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebecc830-5c25-458f-87b2-11c44443fd92/csstn-118.jpg" alt="Multi-colored CSS Progress Bars" /></a>

<a href="https://www.red-team-design.com/css3-breadcrumbs">CSS3 breadcrumbs</a>
Learn how to create your own cool CSS3 breadcrumbs. Also, check the CSS Breadcrumbs Example which uses only CSS linear gradients.

<figure><a href="https://www.red-team-design.com/css3-breadcrumbs"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133496" title="CSS3 breadcrumbs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a27fa28-ca9d-4b8d-b999-44c2da72000d/result-css-131.jpg" alt="CSS3 breadcrumbs" width="498" height="298" /></a></figure>

<a href="https://css-tricks.com/adobe-like-arrow-headers/">Adobe-like Arrow Headers</a>
A detailed article about the technique Adobe uses to create header bars for modules on its website.

<a href="https://css-tricks.com/adobe-like-arrow-headers/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd0416b0-1a57-4857-b73a-e047777ea6bd/csstn-122.jpg" alt="Adobe-like Arrow Headers" /></a>

<a href="https://css-tricks.com/snippets/css/top-shadow/">Adding a Top Shadow to a website</a>
If you ever wanted to add a shadow along the top edge of the website, you can easily do it by styling <code>body:before</code>.

<figure><a href="https://css-tricks.com/snippets/css/top-shadow/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7994f1fe-f38d-42dc-a43d-7aa7afc01e1a/depth.jpg" alt="Adding a Top Shadow to a website" height="285" /></a></figure>

<a href="https://devblog.xing.com/frontend/a-flexible-shadow-with-background-size/">A flexible shadow with background-size</a>
It's amazing what you can achieve when you combine different techniques—even when facing a challenge such as a flexible shadow. If you had to create an adaptive shadow effect, how would you create it?

<figure><a href="https://devblog.xing.com/frontend/a-flexible-shadow-with-background-size/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134811" title="A flexible shadow with background-size" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0683c3ce-10c1-4b13-b19b-038ba61b13ba/css-add-016.png" alt="" width="500" height="300" /></a></figure>

<a href="https://css-tricks.com/star-ratings/">Star Ratings With Very Little CSS</a>
Chris Coyier shows how to code star ratings done with very little CSS code and lots of a bit of Unicode madness.

<a href="https://demosthenes.info/blog/532/Convert-Images-To-Black--White-With-CSS">Convert Images to Black And White With CSS</a>
Filters allow us to visually process an image in the browser without needing to go through PhotoShop or use cycle-intensive, script-heavy methods in JavaScript or PHP. CSS3 filters are broadly supported in the most recent versions of Firefox and Chrome, and we can gain support in older versions and alternative browsers — even IE — by using a combination of techniques.

<figure><a href="https://demosthenes.info/blog/532/Convert-Images-To-Black--White-With-CSS"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134765" title="Convert Images To Black And White With CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65c31905-ea71-449a-8ee0-4a8ca57cfc04/css-add-010.png" alt="" width="500" height="300" /></a></figure>

<a href="https://jsfiddle.net/csswizardry/7BXUf/embedded/result,html,css,js/">Punching Holes With CSS</a>
A clever and simple technique to make a block in a container appear transparent and display a background image. Also, take a look at <a href="https://lea.verou.me/2011/08/accessible-star-rating-widget-with-pure-css/">Lea Verou's accessible star rating widget with CSS</a>.

<a href="https://css-tricks.com/simple-styles-for-horizontal-rules/">Simple Styles for Horizontal Rules</a>
With the help of a few contributors, Chris Coyier put together this page of simple styles for horizontal rules.

<figure><a href="https://css-tricks.com/simple-styles-for-horizontal-rules/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133561" title="Simple Styles for Horizontal Rules" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31aea7f7-699e-4283-976a-a55cba431260/result-css-126.jpg" alt="Simple Styles for Horizontal Rules" width="498" height="298" /></a></figure>

<a href="https://methodandcraft.com/videos/optimizing-graphics-with-css-masks">Optimizing Graphics With CSS Masks</a>
In this video, Aaron Bushnell shows how CSS masks can help make the process easier on you and how to make sure you have fallbacks in place for non-Webkit browsers.

<a href="https://paulirish.com/2009/browser-specific-css-hacks/">Browser-Specific CSS Hacks</a>
A useful, comprehensive list of browser-specific CSS hacks for targeting legacy browsers. Unfortunately, most of us will need them quite often.</p>

## Last Click

<a href="https://www.ryancollins.me/?p=539">CSS3 Lasers!</a>
Shows a laser shot effect when hovering over an element.

<figure><a href="https://www.ryancollins.me/?p=539"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133614" title="CSS3 Lasers!" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0010caba-f6f1-46fc-b461-88c90e20660d/lasers-new.jpg" alt="CSS3 Lasers!" width="513" height="433" /></a></figure>

<a href="https://hakim.se/experiments/css/domtree/">The DOM Tree</a>
This DOM tree is generated via JavaScript every time you visit the page, so you'll never see the same one twice. All of the forms are filled with holiday greetings in a variety of languages. CSS3 3D transforms are used to position and rotate, via <code>translate3d()</code> and <code>rotate3d()</code> respectively, the elements when the page loads. The infinitely looping rotation on the tree is controlled by an infinitely looping CSS3 animation. Just one word: crazy!

<figure><a href="https://hakim.se/experiments/css/domtree/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="133316" title="DOM Tree" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/836239bc-ded4-49c8-a486-78d284570218/the-dom-tree.jpg" alt="DOM Tree" /></a></figure>

## What's Your Favourite Technique?

We'd love to know your experience with some of the featured techniques, or perhaps you've stumbled upon another interesting CSS technique recently? Let us know in the comments to this post!

<a href="https://polldaddy.com/poll/6331943/">What kind of techniques would you like to see featured on SmashingMag?</a>

<em>(jvg) (al) (vf) (ml)</em>

