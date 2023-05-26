---
title: Photoshop-Inspired Techniques with 100% CSS
slug: photoshop-inspired-techniques-100-css
image: null
date: 2010-11-23T20:47:58.000Z
author: newsletter-team
description: >-
  Since the beginning of CSS3, Web designers have begun experimenting with different code-based solutions to add to design, and even to make up a design entirely. Even with older versions of CSS there are many design solutions that can be done with 100% code, no images necessary.
categories:
  - Coding
  - CSS
  - Photoshop
  - CSS3
---
In this article, we're going to take a look at some design solutions that are now possible with CSS, whether it be with the new, more advanced CSS3 or with prior versions. Everything from small details to entire features can be created with CSS and a bit of markup, and it's amazing to see the solutions created and advancements made in just the last few years.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Future Of CSS Typography](https://www.smashingmagazine.com/2010/03/css-and-the-future-of-text/)
*   [CSS Baseline: The Good, The Bad And The Ugly](https://www.smashingmagazine.com/2012/12/css-baseline-the-good-the-bad-and-the-ugly/)
*   [The Perfect Paragraph](https://www.smashingmagazine.com/2011/11/the-perfect-paragraph/)

Despite some of the interesting things we can do with CSS, how practical is it? We'll also take into consideration the practicality of some of these uses, and whether they should just be for fun and experimentation, or perhaps someday a real part of Web design. It's intriguing to think about what kind of imagery and Photoshop-inspired effects could soon be completely replaced with only code, and how this will affect the future of Web development.

{{% feature-panel %}}

## Typography Effects

We're beginning to see more design effects come to life with CSS, especially with the trend of beautiful typography. Using CSS to add to type is a fantastic use of CSS, replacing traditional means like images or just defaulting to a Web-based (and sometimes boring) font.</p>

### Inset (Letterpress) Type

<a href="https://line25.com/tutorials/create-a-letterpress-effect-with-css-text-shadow"><img loading="lazy" decoding="async" class="70600" title="Letterpress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b556f9b-a0aa-4734-b7dc-bb8f913d83cb/letterpress.jpg" alt="Letterpress" width="550" height="399" /></a>

This effect has been done by many of us before, in one form or another. When used in headings, quotes, or other forms of content meant to stand out, the result can be highly practical and beautiful. The <a href="https://line25.com/tutorials/create-a-letterpress-effect-with-css-text-shadow">tutorial on Line25</a> shares an efficient technique for this, with a few different design possibilities.</p>

### Text Rotation

<a href="https://www.thecssninja.com/css/real-text-rotation-with-css"><img loading="lazy" decoding="async" class="75480" title="Text Rotation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f253f0be-5036-4135-a9ab-2662d509ec87/textrotation.jpg" alt="" width="550" height="300" /></a>

Text at different angles can create unique design effects and also serve practical purposes. Once only available with the use of images, text can now be rotated to meet design needs. This is perfect for something like blog post dates, like in the example above, which would obviously be ever-changing and dynamic.</p>

### Custom Typography (@font-face)

<img loading="lazy" decoding="async" class="70602" title="@font-face" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e86b77e7-18f8-4d61-ab6b-196b431b09cc/fontface.jpg" alt="@font-face" width="550" height="300" />

In Photoshop we can use any font we wish to design with, as long as it's installed on our system. On the Web, that was not always possible. With CSS3's new @font-face though, we're beginning to see more interesting, design-complimenting fonts on the Web. @font-face makes it simple and purely CSS-based. However, sIFR and Cufón can also be used as a backup while we're all still waiting for other non-compatible browsers to catch up. For more on all of these font replacement methods, take a look at our post, <a href="https://www.smashingmagazine.com/2010/10/20/review-of-popular-web-font-embedding-services/">Review of Popular Web Font Embedding Services</a>.

Using @font-face can make a world of difference in the outcome of a design, is incredibly easy to implement, and is great for SEO and maintenance purposes as well.

A good, detailed and easy tutorial to follow in case one does not have experience with using @font-face yet can be found over at Zen Elements: CSS3 Embedding @font-face. As an additional resource, <a href="https://www.fontsquirrel.com/">Font Squirrel</a> has an @font-face generator, along with plenty of quality free fonts to use.</p>

### Drop-Shadow Text

<a href="https://owltastic.com/2009/12/shadows-and-css3/"><img loading="lazy" decoding="async" class="75481" title="Text Shadow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c82aa46b-1935-4e43-9724-05ee645c1703/text-shadow.jpg" alt="Text Shadow" width="550" height="300" /></a>

Text shadow is a simple effect many of us are also already using. It's a great effect to add some design detail, but also to help highlight text and add depth to a Web design. Quite simply, the code to create a CSS3 text shadow is as follows:

<pre><code class="language-css">text-shadow: 1px 1px 0 #000;</code></pre>

The best part is that while regaining the use of variable text with drop-shadows, the code is only one line and easy to customize. For a more detailed post and a couple of examples, be sure to read through Meagan Fisher's quick tutorial: <a href="https://owltastic.com/2009/12/shadows-and-css3/">Shadows and CSS3</a>.</p>

## Gradients

Gradients were also once only possible when placed in images, but now there is a set of tricks that use either smarter imagery, or even image-free techniques to create the same design effects we've been using for years.</p>

### Pure CSS3 Gradients

<a href="https://www.webdesignerwall.com/tutorials/cross-browser-css-gradient/"><img loading="lazy" decoding="async" class="70603" title="CSS Gradients" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc0f1d52-b98a-4b0c-b091-ff0457f1dfa3/gradientmenu.jpg" alt="CSS Gradients" width="550" height="300" /></a>

CSS3 and WebKit also come with pure CSS gradients, which can allow for the creation of many Web elements that once required images. Above is a demo of a <a href="https://www.webdesignerwall.com/demo/css3-dropdown-menu/css-gradient-dropdown.html">Pure CSS Menu</a> created by Nick La, with the use of CSS gradients and other features like drop shadows and rounded corners.

There is also a tutorial to accomplish many of the above gradient looks: <a href="https://www.webdesignerwall.com/tutorials/cross-browser-css-gradient/">Cross-Browser CSS Gradient</a>.</p>

### Gradient Over Text (Or Anything Else)

<a href="https://www.webdesignerwall.com/tutorials/css-gradient-text-effect/"><img loading="lazy" decoding="async" class="70604" title="Text Gradient" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a96c4a42-4b12-4b4f-80aa-3380aa8ad784/textgradient.jpg" alt="Text Gradient" width="550" height="300" /></a>

While this effect does include some images, it is still a very good CSS example especially because it is compatible in most browsers, unlike many CSS3 tricks. With a small pattern or gradient, we can recreate any text, div, image or whatever with the pattern overlying it.

## Fancy Borders

Borders around images and other block elements can be a fast, easy and effective way to add clean lines and detail to a Web design. There are a number of trends that have been used for years now, and even more possibilities are showing up with CSS3.

<a href="https://designshack.co.uk/articles/introduction-to-css3-part-2-borders"><img loading="lazy" decoding="async" class="75482" title="Borders" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d13df8e-e550-4a8e-acfa-d48f9a4dcac3/borders.jpg" alt="Borders" width="550" height="300" /></a>

There are plenty of unique ideas that can be created with just CSS 2.1, and therefore would be compatible with far more browsers. It really just takes some creativity and out-of-the-box thinking. In the post, 12 Creative and Cool Uses for the CSS Border Property, many effects are mimicked with minimal markup and pure CSS. Some may not be entirely practical for the everyday image border, but many could be applied to other uses of CSS, like CSS posters or images (see below).

Then, with CSS3 we have more possibilities, and more border capabilities for common border styles. CSS3 introduced the use of border images, gradient borders, and of course, rounded corners. Other techniques using the box-shadow property can create interesting effects as well. For examples and quick snippits check out Design Shack's <a href="https://designshack.co.uk/articles/introduction-to-css3-part-2-borders">Introduction to CSS3 - Part 2: Borders</a>.</p>

## Bigger Techniques and Tutorials

Some design techniques accomplished with CSS can be small details, while others can make up an entire design. Below are some experiments or uses of bigger solutions done with CSS. If any imagery or JavaScript has been applied in the effects below, it is for additional detail or functionality. However, for all of these the primary focus is still 100% CSS.</p>

### Overlapping Ribbons

<img title="3D Ribbons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d53b899-c315-414d-9eb4-96fd71b0d742/ribbons.jpg" alt="3D Ribbons" width="550" height="300" />

Again, with a mix of CSS3 and older CSS techniques, we can recreate a design feature that was once only possible with images. This design technique has long been used to add depth to a Web design and also to grab attention, by overlapping boundaries.

This tutorial works in just about every browser except for IE and some older versions of Opera. Despite this, the degraded version actually works well in its own respect, otherwise one can get the same look using imagery with an alternate stylesheet, and only be called when it encounters these browsers.

<strong>This effect works in:</strong> Chrome 4+, Firefox 3.5+, Safari 4+.

* Does not work correctly in IE or Opera, yet degrades gracefully.</p>

### Detailed Polaroids

<a href="https://www.zurb.com/article/305/easily-turn-your-images-into-polaroids-wi"><img loading="lazy" decoding="async" class="70606" title="Polaroids" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ecf8b4b-ad6f-41c5-a47e-346e39addb87/poloroids.jpg" alt="Polaroids" width="550" height="339" /></a>

The "Polaroid look" for photos and other imagery on the Web has long been a trend, and leans more towards a retro style. Before, this look involved using a background Polaroid image, and placing the photo on top. As an alternative, a CSS 2.1 version was (and is still) possible with the use of padding and borders, but we can definitely make it even more interesting with the advances of CSS3!

This tutorial and effect above uses some more advanced and modern CSS tricks to bring more life into the Polaroid look. Chris Spooner's <a href="https://line25.com/tutorials/how-to-create-a-pure-css-polaroid-photo-gallery">How To Create a Pure CSS Polaroid Photo Gallery</a> includes features like CSS drop-shadows, transformations and rotations, and even the classic z-index feature which has been around for a while, but doesn't seem to be used often enough. All of these effects come together to create what looks like several custom-made Polaroid images, but the only true images used are the photos themselves.

<strong>This effect works in:</strong> Chrome 4+, Firefox 3.5+, Safari 4+.

* Final transition effect added on hover does not work in Firefox yet.</p>

### 3D Cube using 2D CSS transformations

<a href="https://www.paulrhayes.com/2009-04/3d-cube-using-css-transformations/"><img title="3D Box CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76e0a089-bb6e-431e-9c44-0569b93d75a2/3dbox.jpg" alt="3D Box CSS" width="550" height="339" /></a>

In the old days of CSS, we were used to flat boxes on flat screens. However, with the newest release of WebKit, in many modern browsers we can use 3D transforms to create 3D boxes with regular text, padding, margins, borders, backgrounds, and more.

Be sure to check out <a href="https://www.paulrhayes.com/2009-04/3d-cube-using-css-transformations/">the tutorial</a> for a full explanation and a list of browsers that can currently render this effect correctly. Also, using WebKit animation, rotating cubes and other design and interactivity effects are possible without Flash or JavaScript. The best part about this technique is that the markup behind it is incredibly simple and semantic, and the CSS is fairly simple as well.

<strong>This effect works in:</strong> Chrome 4+, Firefox 3.5+, Safari 4+. (without transitions)

<strong>This effect works in:</strong> Chrome, Safari 4+. (with transitions)

### Windows 7 Start Menu

<a href="https://www.jankoatwarpspeed.com/post/2010/04/06/windows-7-start-menu-css3.aspx"><img loading="lazy" decoding="async" class="70608" title="Windows 7 CSS3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd3160af-b58f-47ef-aed5-b6b901a407c8/windows7.jpg" alt="Windows 7 CSS3" width="550" height="300" /></a>

This is a complete recreation of a Windows 7 menu with CSS only. The practicality of the recreation may be controversial, but regardless, this tutorial shows how many CSS effects can be used to imitate many common design effects, and can put them intelligently into practice.

Be sure to check out <a href="https://www.jankoatwarpspeed.com/examples/windows7menu/">the demo</a> to get a full feel of what this tutorial does. All effects are done with pure CSS, with the exception of the icons.

<strong>This effect works in:</strong> Chrome, Firefox 3.6+, Safari.

* Doesn't work in IE or Opera, but degrades gracefully.</p>

### Mac Dock

<a href="https://webexpedition18.com/articles/how-to-create-a-customizable-dock-with-css3-only/"><img loading="lazy" decoding="async" class="75483" title="Mac Dock" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf66d007-262c-4494-a203-8ac6b3eb7ece/macdock.jpg" alt="Mac Dock" width="550" height="300" /></a>

Along with the Windows 7 menu above, it'd only be fair to include a Mac Dock recreation as well. This tutorial uses images for the icons, and also for some of the background. In the end, it also uses a bit of jQuery to create a perfect effect, but the majority of it is done with CSS. Even when stripping out all of the additional imagery and scripting, we still come up with a great design solution with pure CSS.

<strong>This effect works in:</strong> Safari, Chrome, Opera, Firefox 3.7+

* In IE and Firefox 3.6 and lower, it degrades nicely but doesn't work completely because these browsers do not support transitions yet.</p>

### Speech Bubbles and Blockquotes

<a href="https://nicolasgallagher.com/pure-css-speech-bubbles/"><img loading="lazy" decoding="async" class="70610" title="Speech Bubbles" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42ac6917-032f-41d1-a367-aa2a88881401/speechbubbles.jpg" alt="Speech Bubbles" width="550" height="300" /></a>

CSS is nothing new to blockquotes, nor is it new to speech bubbles. However, Nicholas Gallagher decided to step it up a notch and create more design-oriented speech bubbles with pure CSS. Many effects work perfectly well with just CSS2.1, but include CSS3 techniques to enhance the effect.

The old alternative to this would have been to use background images in the shape of speech bubbles, and then struggle to use fixed positioning to fit text inside. Pure CSS speech bubbles and blockquotes allow for more flexibility when writing quotes, and at the same time, fewer images end up cluttering the Web server.

Be sure to take a look at the <a href="https://nicolasgallagher.com/pure-css-speech-bubbles/demo/">demo page</a> to see all of the variety and examples available, and then head on over to the <a href="https://nicolasgallagher.com/pure-css-speech-bubbles/">tutorial page</a> for an exact how-to.

<strong>This effect works in:</strong> Firefox 3.5+, Safari 4+, Chrome 4+, Opera 10+, IE8+

### Social Media Icons

<a href="https://nicolasgallagher.com/pure-css-social-media-icons/"><img loading="lazy" decoding="async" class="70611" title="Pure CSS Icons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d06639-0627-4fde-b9b6-17089be35f95/cssicons.jpg" alt="Pure CSS Icons" width="550" height="300" /></a>

As another experiment, many of the same techniques used for the speech bubbles above were used to create pure CSS social media icons. For this purpose, just using a small image rather than many lines of code would be far more practical, but again this is another experiment that shows the true power of CSS.

<strong>This effect works in:</strong> Firefox 3.5+, Safari 4+, Chrome 4+, Opera 10+, IE8+

## Full CSS Designs

While the above section features design effects, below are some experiments that have created full designs from pure CSS. The first is an experiment done by Design Informer on <a href="https://www.smashingmagazine.com/2010/05/css-posters/">CSS Posters</a>. The experiment and techniques used here could actually end up becoming very useful in the rising trend of print-inspired layouts in Web design.

<a href="https://www.smashingmagazine.com/2010/05/css-posters/"><img loading="lazy" decoding="async" class="70614" title="CSS Posters" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81f3a3a5-a532-46f2-957d-c8ceb55fd55e/posterdesigns.jpg" alt="CSS Posters" width="550" height="564" /></a>

There were also other CSS posters around the Web that were used as the inspiration for these designs:

### HTML CSS Rotation

<a href="https://www.everydayworks.com/css_typography/HTMLCSSrotation.html"><img loading="lazy" decoding="async" class="70615" title="CSS Rotation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/719a018f-924b-48d5-980d-6a6916e9bef4/cssrotation.jpg" alt="CSS Rotation" width="550" height="653" /></a>

### Laws of Robotics

<a href="https://graphicpush.com/css3/posters/3laws.html"><img loading="lazy" decoding="async" class="70616" title="Laws of Robotics" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e0ee5b7-a6ae-4216-93ad-e0a9f71b2d59/lawsofrobotics.jpg" alt="Laws of Robotics" width="550" height="709" /></a>

### CSS3 Hooray!

<a href="https://trentwalton.com/css3/type/"><img loading="lazy" decoding="async" class="70617" title="CSS3 Hooray" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33848aad-d7bd-4a6f-9337-601a7421543b/hooray.jpg" alt="CSS3 Hooray" width="550" height="312" /></a>

### Why Art?

<img loading="lazy" decoding="async" class="70618" title="Why Art?" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/180aebad-b50a-4ffb-a1b2-ae34d1c35957/whyart.jpg" alt="Why Art?" width="550" height="547" />

### All Human Beings are Born Free

<a href="https://neography.com/experiment/type1/"><img loading="lazy" decoding="async" class="70619" title="All Human Beings are Born Free" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c38262c-278d-41a2-b81b-9464b0606bae/allfree.jpg" alt="All Human Beings are Born Free" width="550" height="403" /></a>

Each of these designs use a variety of different CSS features and markup, but the creation process among them all is essentially the same. If interested, Chris Spooner wrote a tutorial on how to create a pure CSS poster, from design to final implementation: <a href="https://line25.com/tutorials/create-a-vibrant-digital-poster-design-with-css3">Create a Vibrant Digital Poster Design with CSS3</a>.</p>

## How Practical Is It?

While many of these effects can be interesting, unique, and can put our coding practices into perspective, there is no doubt that many of these design solutions may be better served in the traditional way: with images. How practical is it to use pure CSS for many design effects? Does it save server space, make pages load faster, and is the time put in (or time saved, depending on which effect is applied) worth the desired effect(s) in the end?

Many of the above techniques were created as examples and as an experiment to test the boundaries of CSS technology. That's all fine and well, but at the same time many of these effects are being recreated around the Web, and are being put to real, live use. Faruk Ates wrote an interesting article concerning this, entitled <a href="https://farukat.es/journal/2010/08/469-pure-css-icons-make-madness-stop">Pure CSS Icons: Make The Madness Stop</a>:
<blockquote>"People have been making things out of pure CSS for a long time now, and until recently that was a harmless exercise in pushing the limits of the technology whilst occasionally coming across production-friendly techniques and creations. It was something I wholeheartedly stood behind, because—again, until recently—the people making those things knew where to draw the line between "experimental technology demo" and "production-friendly technique or implementation."</blockquote>

<blockquote>"How usable are these snippets of CSS and markup, really? Is it easy to plug them into your website as you’re designing it? No. Is it easy to plug them into your website as you’re developing it? No. Is it easy to adjust them once they have been integrated into your website? No, no, no!"</blockquote>

_— Faruk Ates, Pure CSS Icons: Make The Madness Stop_

The main message here is to use CSS design effects responsibly and effectively. In the end, CSS3 and prior versions can remake some of our most commonly used design features without imagery, and do it more effectively than how we were doing it before. Simple things like drop-shadows, gradients and more can all be considered good uses if it enhances a design, and if an excessive amount of code is not required. In other situations as well, such as the blockquote and speech bubble example above, CSS is put to good use by helping to make speech bubbles more usable.

There are many more practical and smart uses of CSS, but in the end we must take some of the following into consideration:

*   **Browser compatibility:** Does the created design effect depend solely on CSS effects that may not be correctly viewed in many browsers? If so, make sure alternate stylesheets are available and that JavaScript solutions can step in if need be, or it may be best to just use traditional means. Pure CSS isn't the solution to all design features, even if it's technically possible.
*   **Semantic markup/CSS and code length:** Is the resulting code semantic and practical to use over the use of a few images? In some solutions we can see that it takes far too much code, or far too confusing code, and would therefore end up being less efficient than just using images.
*   **Maintenance:** Sometimes CSS-based design solutions can make maintenance easier compared to constantly altering images, but in other cases, it can make it far more difficult. How easy is it to change a small detail or content contained within the design effect?

Pure CSS designs and CSS design effects can be interesting solutions, but not always practical solutions. Also, some CSS design effects may be more practical in certain situations than in others. It can all just depend on the implementation of the effect, and when and where it is used.</p>

## Conclusion

There is no doubt that a wide variety of design techniques, once only possible with Photoshop or some other design program, can now be done in only code. In some situations, these solutions can be great for practice but highly inefficient when it comes to using images vs. code. In other cases, it may be more efficient to use CSS and markup to create a lot of effects. Especially with some of CSS3's common features like drop-shadows, opacity, and more, many "detail images" on the Web can now begin to be replaced.

Feel free to share thoughts on which of these solutions seem practical, and which do not. Some uses may need to wait for better browser compatibility, and others may never be practical, but may be good practice nonetheless.</p>

## Further Resources

*   [Take Your Design To The Next Level With CSS3](../2009/06/15/take-your-design-to-the-next-level-with-css3/) A more detailed look into CSS3 and into some of the design and/or functionality features it can now add, relative to previous versions.
*   [CSS3 Design Contest Results](../2010/07/12/css3-design-contest-results/) The SM CSS3-only design contest is a great place for inspiration for the design effects CSS can handle.
*   [CSS Button Maker](https://css-tricks.com/examples/ButtonMaker/) Buttons and other small elements are a great starting point for replacing imagery with CSS, and this handy tool can help.
*   [CSS3 Cookbook: 7 Super Easy CSS Recipes to Copy and Paste](https://designshack.co.uk/articles/css/css3-cookbook-7-super-easy-css-recipes-to-copy-and-paste) A collection of design-inspired pure CSS code snippets. Letterpress, small caps, a coupon design, stitched design, and overlying gloss are included.

