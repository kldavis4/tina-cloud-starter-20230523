---
title: 'Modern CSS Layouts, Part 2: The Essential Techniques'
slug: modern-css-layouts-part-2-the-essential-techniques
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d1d4e1-6900-476d-a3a6-429e04566899/css-31.jpg
date: 2010-05-06T11:57:25.000Z
author: zoe-mickley-gillenwater
description: >-
  In [Modern CSS Layouts, Part 1: The Essential
  Characteristics](https://www.smashingmagazine.com/2009/10/26/modern-css-layouts-the-essential-characteristics/),
  you learned that modern, CSS-based web sites should be progressively enhanced,
  adaptive to diverse users, modular, efficient and typographically rich. Now
  that you know _what_ characterizes a modern CSS web site, _how_ do you build
  one? Here are dozens of essential techniques and tools to learn and use to
  achieve the characteristics of today's most successful CSS-based web pages.

  Just as in the previous article, we're not going to be talking about design
  trends and styles; these styles are always changing. Instead, we're focusing
  on the specific techniques that you need to know to create modern CSS-based
  web pages of any style. For each technique or tool, we'll indicate which of
  the five characteristics it helps meet. To keep this shorter than an
  encyclopedia, we'll also just cover the basics of each technique, then point
  you to some useful, hand-picked resources to learn the full details.
categories:
  - Coding
  - Layouts
  - CSS
  - Techniques
  - Essentials
---
In [Modern CSS Layouts, Part 1: The Essential Characteristics](https://www.smashingmagazine.com/2009/10/26/modern-css-layouts-the-essential-characteristics/), you learned that modern, CSS-based web sites should be progressively enhanced, adaptive to diverse users, modular, efficient and typographically rich. Now that you know _what_ characterizes a modern CSS web site, _how_ do you build one? Here are dozens of essential techniques and tools to learn and use to achieve the characteristics of today's most successful CSS-based web pages.

Just as in the previous article, we're not going to be talking about design trends and styles; these styles are always changing. Instead, we're focusing on the specific techniques that you need to know to create modern CSS-based web pages of any style. For each technique or tool, we'll indicate which of the five characteristics it helps meet. To keep this shorter than an encyclopedia, we'll also just cover the basics of each technique, then point you to some useful, hand-picked resources to learn the full details.

You can jump straight to:

*   [CSS3](#moderncss-css3)
*   [HTML5](#moderncss-html5)
*   [IE Filtering](#moderncss-ie)
*   [Flexible Layouts](#moderncss-flexible)
*   [Layout Grids](#moderncss-grids)
*   [Efficient CSS Development Practices](#moderncss-efficient)
*   [CSS Performance](#moderncss-performance)
*   [Font Embedding and Replacement](#moderncss-fonts)

## CSS3

CSS3, the newest version of CSS that is now being partially supported by most browsers, is the primary thing you need to know in order to create modern CSS web sites, of course. CSS is a styling language, so it's no surprise that most of what's new in CSS3 is all about visual effects. But CSS3 is about more than progressive enhancement and pretty typography. It can also aid usability by making content easier to read, as well as improve efficiency in development and page performance.

{{% feature-panel %}}

There are too many CSS3 techniques to cover in a single article, let alone an article that isn't just about CSS3! So, we'll go through the basics of the most important or supported CSS3 techniques and point you to some great resources to learn more in-depth.</p>

### CSS3 Visual Effects

**Semi-transparent Color**  
_Aids in: progressive enhancement, efficiency_

[RGBA](https://www.w3.org/TR/css3-color/#rgba-color) allows you to specify a color by not only setting the values of red, green, and blue that it's comprised of, but also the level of opacity it should have. An alternative to RGBA is [HSLA](https://www.w3.org/TR/css3-color/#hsla-color), which works the same way, but allows you to set values of hue, saturation, and lightness, instead of values of red, green, and blue. The article [Color in Opera 10 — HSL, RGB and Alpha Transparency](https://dev.opera.com/articles/view/color-in-opera-10-hsl-rgb-and-alpha-transparency/) explains how HSLA can be more intuitive to use than RGBA.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ade4425-1f58-4710-ac34-8288649dac80/part2-rgba.jpg)](https://www.24ways.org/)  
_The [24 Ways web site](https://www.24ways.org/) makes extensive use of RGBA to layer semi-transparent boxes and text over each other._

RGBA or HSLA isn't just about making things look cool; it can also improve your web site's efficiency. You don't have to take time to make alpha-transparent PNGs to use as backgrounds, since you can just use a color in the CSS, and the user agent doesn't have to download those images when loading the site.

For more on how to use RGBA and HSLA, including fallback methods for browsers that don't support it, see:

*   [Working With RGBA Colour](https://24ways.org/2009/working-with-rgba-colour) (24 ways)
*   [RGBa Browser Support](https://css-tricks.com/rgba-browser-support/) (includes a hack for IE, by CSS-Tricks)
*   [Flexible Color Schemes in Layouts with RGBa](https://buildinternet.com/2010/02/flexible-color-schemes-in-layouts-with-rgba/) (Build Internet!)
*   [Is CSS3 RGBa ready to rock? (screencast)](https://forabeautifulweb.com/blog/about/is_css3_rgba_ready_to_rock) (For a Beautiful Web)
*   [Playing Around with CSS3 Colors](https://www.lateralcode.com/playing-with-css3-colors/) (Lateral Code)
*   [Color in Opera 10 — HSL, RGB and Alpha Transparency](https://dev.opera.com/articles/view/color-in-opera-10-hsl-rgb-and-alpha-transparency/) (Opera Developer Community)
*   CSS3 HSL & HSLA (Zen Elements)

**Styling Backgrounds and Borders**  
_Aids in: progressive enhancement, efficiency_

CSS3 offers a whole host of new ways to style backgrounds and borders, often without having to use images or add extra `div`s. Most of these new techniques already have good browser support, and since they're mainly used for purely cosmetic changes, they're a good way to get some progressive enhancement goodness going in your sites right away.

Here are some of the new things CSS3 lets you do with backgrounds:

*   **Multiple backgrounds on a single element:** You can now add [more than one background image](https://www.w3.org/TR/css3-background/#layering) to an element by listing each image, separated by commas, in the `background-image` property. No more nesting extra `div`s just to have more elements to attach background images onto!
*   **More control over where backgrounds are placed:** The new [`background-clip`](https://www.w3.org/TR/css3-background/#the-background-clip) and [`background-origin`](https://www.w3.org/TR/css3-background/#the-background-origin) properties let you control if backgrounds are displayed under borders, padding, or just content, as well as where the origin point for `background-position` should be.
*   **Background sizing:** You can scale background images using the new [`background-size` property](https://www.w3.org/TR/css3-background/#background-size). While scaling won't look good on many background images, it could be really handy on abstract, grunge-type backgrounds, where tiling can be difficult and where some image distortion would be unnoticeable.
*   **Gradients:** While just part of a CSS3 [draft spec](https://dev.w3.org/csswg/css3-images/#gradients-), Safari, Chrome and Firefox support declaring multiple color and placement values in the `background-image` property to create gradients without images. This allows the gradients to scale with their container — unlike image gradients — and eliminates the need for page users to download yet another image while viewing your site.

CSS3 lets you do the following with borders:

*   **Rounded corners:** Use the [`border-radius`-property](https://www.w3.org/TR/css3-background/#the-border-radius) to get rounded corners on `div`s, buttons, and whatever else your heart desires — all without using images or JavaScript.
*   **Images for borders:** With CSS 2.1, the only way to create a graphic border was to fake it with background images, often multiple ones pieced together on multiple `div`s. You can now add unique borders without having to use background images by adding the images to the borders directly, using the new [`border-image` property](https://www.w3.org/TR/css3-background/#border-images), which also allows you to control how the images scale and tile.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e96d36e6-4132-4f67-b398-7b74491e6b2f/part2-borderradius.jpg)](https://www.stunningcss3.com/)  
_The `border-radius` property can be used to round corners and even create circles out of pure CSS, with no images needed. ([Stunning CSS3 web site](https://www.stunningcss3.com/))_

These background and border techniques have already been covered well in a lot of great articles and tutorials, so check these out for the details:

*   [Backgrounds In CSS: Everything You Need To Know](https://www.smashingmagazine.com/2009/09/02/backgrounds-in-css-everything-you-need-to-know/)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)
*   [CSS3 borders, backgrounds and box-shadows](https://dev.opera.com/articles/view/css3-border-background-boxshadow/) (Opera Developer Community)
*   Background images no longer restricted to original size: explore the space with background-size (Mozilla Developer Center)
*   [Multiple Backgrounds and CSS Gradients](https://snook.ca/archives/html_and_css/multiple-bg-css-gradients) (Snook.ca)
*   [Quick Tip: Understanding CSS3 Gradients](https://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-understanding-css3-gradients/) (Nettuts+)
*   [Using gradients](https://developer.mozilla.org/en/Using_gradients) (Mozilla Developer Center)
*   [Speed Up with CSS3 Gradients](https://css-tricks.com/css3-gradients/) (CSS-Tricks)
*   Gradient syntax generators are available from westciv.com ([linear](https://westciv.com/tools/gradients/index.html) and [radial](https://westciv.com/tools/radialgradients/index.html)) and [glrzad.com](https://gradients.glrzad.com/)
*   [The CSS3 border-radius property](https://www.bloggingcss.com/en/tutorials/the-css3-border-radius-property/) (Blogging CSS)
*   [CSS: border-radius and -moz-border-radius](https://www.the-art-of-web.com/css/border-radius/) (The Art of Web)
*   [Table of CSS3 border-radius Compliance](https://muddledramblings.com/table-of-css3-border-radius-compliance) (Muddled Ramblings and Half-Baked Ideas)
*   [border-image in Firefox](https://ejohn.org/blog/border-image-in-firefox/) (John Resig)
*   Meet a ninja living in browsers (on `border-image`, from lrbabe.com)
*   [The New Hotness: Using CSS3 Visual Effects](https://www.smashingmagazine.com/2010/01/25/the-new-hotness-using-css3-visual-effects/) (see third tutorial on `border-image`)

**Drop Shadows**  
_Aids in: progressive enhancement, adaptability, efficiency_

Drop shadows can provide some visual polish to your design, and now they're possible to achieve without images, both on boxes and on text.

The [`box-shadow` property](https://www.w3.org/TR/css3-background/#the-box-shadow) has been temporarily removed from the CSS3 spec, but is supposed to be making its re-appearance soon. In the meantime, it's still possible to get image-free drop shadows on boxes in Firefox and Safari/Chrome using the `-moz-box-shadow` and `-webkit-box-shadow` properties, respectively, and in Opera 10.5 using the regular `box-shadow` property with no prefix. In the property, you set the the shadow's horizontal and vertical offsets from the box, color, and can optionally set blur radius and/or spread radius.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72266764-f606-4773-ac2d-fc74c39615d8/part2-boxshadow.jpg)](https://www.becherry.be/)  
_The [Cherry web site](https://www.becherry.be/) uses drop shadows created with `box-shadow` on many boxes and buttons._

The [`text-shadow` property](https://www.w3.org/TR/css3-text/#text-shadow) adds drop shadows on — you guessed it — text. It's supported by all the major browsers except — you guessed it — Internet Explorer. This makes it the perfect progressive enhancement candidate — it's simply a visual effect, with no harm done if some users don't see it. Similarly to `box-shadow`, it takes a horizontal offset, vertical offset, blur radius and color.

Using `text-shadow` keeps you from resorting to Flash or images for your text. This can speed up the time it takes you to develop the site, as well as speed up your pages. Avoiding Flash and image text can also aid accessibility and usability; just make sure your text is still legible with the drop shadow behind it, so you don't inadvertently _hurt_ usability instead!

For more on box and text drop shadows, see:

*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)
*   [Shadow boxing with -moz-box-shadow](https://hacks.mozilla.org/2009/06/moz-box-shadow/) (relevant to non-Mozilla browsers to, from hacks.mozilla.org)
*   <span class="removed_link" title="https://placenamehere.com/article/372/CSS3TrialsBoxShadowAndMore">CSS3 Trials: Box-Shadow And More</span> (Chris Casciano's Place Name Here)
*   <span class="removed_link" title="https://placenamehere.com/article/384/CSS3BoxShadowinInternetExplorerBlurShadow">CSS3 Box Shadow in Internet Explorer [Blur-Shadow]</span> (Chris Casciano's Place Name Here)
*   [Mozilla Developer Center text-shadow](https://developer.mozilla.org/en/CSS/text-shadow) (includes browser support chart and notes)
*   [Text-Shadow Exposed: Make cool and clever text effects with css text-shadow](https://www.kremalicious.com/2008/04/make-cool-and-clever-text-effects-with-css-text-shadow/) (Kremalicious)
*   Using Text Shadow in HTML/CSS (includes a hack for IE, by admixWeb)
*   Westciv's [box-shadow](https://westciv.com/tools/boxshadows/index.html) and [text-shadow generators](https://westciv.com/tools/shadows/index.html)

**Transforms**  
_Aids in: progressive enhancement, adaptability, efficiency_

CSS3 makes it possible to do things like rotate, scale, and skew the objects in your pages without resorting to images, Flash, or JavaScript. All of these effects are called [“transforms.”](https://www.w3.org/TR/css3-3d-transforms/) They're supported in Firefox, Safari, Chrome, and Opera 10.5.

You apply a transform using the `transform` property, naturally (though for now you'll need to use the browser-specific equivalents: `-moz-transform`, `-webkit-transform`, and `-o-transform`). You can also use the `transform-origin` property to specify the point of origin from which the transform takes place, such as the center or top right corner of the object.

In the `transform` property, you specify the type of transform (called “transform functions”), and then in parentheses write the measurements needed for that particular transform. For instance, a value of `translate(10px, 20px)` would move the element 10 pixels to the right and 20 pixels down from its original location in the flow. Other supported transform functions are `scale`, `rotate`, and `skew`.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48c2c62c-1547-4e14-8a92-6ec8d393e6af/part2-transform.gif)  
_The BeerCamp SXSW 2010 site scales and rotates the sponsor logos on hover._

For the full syntax on these transform functions, as well as examples of how to use them, see:

*   [What You Need To Know About Behavioral CSS](https://www.smashingmagazine.com/2009/12/19/what-you-need-to-know-about-behavioral-css/)
*   [CSS3 transitions and 2D transforms](https://dev.opera.com/articles/view/css3-transitions-and-2d-transforms/) (Opera Developer Community)
*   [CSS: Animation Using CSS Transforms](https://www.the-art-of-web.com/css/css-animation/) (The Art of Web)
*   [Mozilla Developer Center -moz-transform](https://developer.mozilla.org/en/CSS/-moz-transform) (includes notes and links on using the more complicated matrix function)
*   [Going Nuts with CSS Transitions](https://24ways.org/2009/going-nuts-with-css-transitions) (24 Ways)
*   [Text Rotation with CSS](https://snook.ca/archives/html_and_css/css-text-rotation) (Snook.ca)
*   [The New Hotness: Using CSS3 Visual Effects](https://www.smashingmagazine.com/2010/01/25/the-new-hotness-using-css3-visual-effects/)
*   [3D Transforms](https://webkit.org/blog/386/3d-transforms/) (Surfin' Safari)
*   [Westciv's transforms generator](https://westciv.com/tools/transforms/index.html)

**Animation and Transitions**  
_Aids in: progressive enhancement, efficiency_

Animation is now no longer the solely the domain of Flash or JavaScript — you can now create animation in pure HTML and CSS. Unfortunately, CSS3 animation and transitions do not have very good browser support, but as with most of the effects we've talked about so far, they're great for adding a little non-essential flair.

[CSS3 transitions](https://www.w3.org/TR/css3-transitions/) are essentially the simplest type of animation. They smoothly ease the change between one CSS value to another over a specified duration of time. They're triggered by changing element states, such as hovering. They're supported by Safari, Chrome, and Opera 10.5.

To create a transition, all you have to do is specify which elements you want to apply the transition to and which CSS properties will transition, using the `transition-property` property. You'll also need to add a `transition-duration` value in seconds (“s” is the unit), since the default time a transition takes is 0 seconds. You can add them both in the `transition` shorthand property. You can also specify a delay or a timing function to more finely tune how the two values switch.

Transitions are easiest to understand with live examples, so check out:

*   [What You Need To Know About Behavioral CSS](https://www.smashingmagazine.com/2009/12/19/what-you-need-to-know-about-behavioral-css/)
*   [CSS3 Transitions – Are We There Yet?](https://samuli.hakoniemi.net/css3-transitions-are-we-there-yet/) (hakoniemi)
*   [CSS3 transitions and 2D transforms](https://dev.opera.com/articles/view/css3-transitions-and-2d-transforms/) (Opera Developer Community)
*   [CSS Transitions 101](https://www.webdesignerdepot.com/2010/01/css-transitions-101/) (Webdesigner Depot)
*   [CSS: Transition Timing Functions](https://www.the-art-of-web.com/css/timing-function/) (The Art of Web)
*   [The New Hotness: Using CSS3 Visual Effects](https://www.smashingmagazine.com/2010/01/25/the-new-hotness-using-css3-visual-effects/)

Beyond transitions, full-fledged [animations](https://www.w3.org/TR/css3-animations/) with multiple keyframes are also possible with CSS3 (but currently only supported in Safari/Chrome). First, you give the animation a name and define what the animation will do at different points (keyframes, indicated with percentages) through its duration. Next, you apply this animation to an element using the `animation-name`, `animation-duration`, and `animation-interation-count` properties. You could also set a delay and timing function, just like with transitions. For details, see:

*   [What You Need To Know About Behavioral CSS](https://www.smashingmagazine.com/2009/12/19/what-you-need-to-know-about-behavioral-css/)
*   [Pushing Your Buttons With Practical CSS3](https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/)
*   [CSS Animations](https://24ways.org/2009/css-animations) (24 Ways)
*   [CSS Animation](https://webkit.org/blog/324/css-animation-2/) (Surfin' Safari)
*   [CSS3 In Transition](https://trentwalton.com/2010/03/22/css3-in-transition/) (a brief article on the usability considerations of animation and transitions, by Trent Walton)
*   [50 Awesome Animations made with CSS3](https://www.1stwebdesigner.com/development/50-awesome-css3-animations/ "50 Awesome Animations made with CSS3") [](https://designshack.co.uk/articles/css/10-amazing-examples-of-innovative-css3-animation)(1stwebdesigner)

### CSS3 Usability / Readability Enhancements

Most the CSS3 techniques we've gone over so far have been purely cosmetic effects that aid progressive enhancement. But CSS3 can also be used to improve the usability of your pages.

**Creating Multiple Columns of Text**  
_Aids in: progressive enhancement, adaptability_

Some pieces of text are more readable in narrow, side-by-side columns, similar to traditional newspaper layout. You can tell the browser to arrange your text into [columns](https://www.w3.org/TR/css3-multicol/) by either defining a width for each column (the `column-width` property) or by defining a number of columns (the `column-count` property). Other new properties let you control gutters/gaps, rule lines, breaking between columns and spanning across columns. (For now, you need to use the browser-specific prefixes of `-moz` and `-webkit`.) This is another one of those techniques that can harm instead of aid usability if used improperly, as explained in “[CSS3 Multi-column layout considered harmful](https://www.456bereastreet.com/archive/200509/css3_multicolumn_layout_considered_harmful/),” so use it judiciously.

For details, see:

*   [Remembering: The CSS3 Multi-Column Layout Module](https://webdesignernotebook.com/css/remembering-the-css3-multi-column-layout-module/) (Web Designer Notebook)
*   [Columns](https://www.quirksmode.org/css/multicolumn.html) (quirksmode)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)

**Controlling Text Wrapping and Breaking**  
_Aids in: adaptability_

CSS3 gives you more control over how blocks of text and individual words break and wrap if they're too long to fit in their containers. Setting [`word-wrap`](https://www.w3.org/TR/css3-text/#word-wrap) to `break-word` will break a long word and wrap it onto a new line (particularly handy for long URLs in your text). The [`text-wrap`](https://www.w3.org/TR/css3-text/#text-wrap) property gives you a number of options for where breaks may and may not occur between words in your text. The CSS2 [`white-space`](https://www.w3.org/TR/css3-text/#white-space) property has now in CSS3 become a shorthand property for the new [`white-space-collapse`](https://www.w3.org/TR/css3-text/#white-space-collapse) and `text-wrap` properties, giving you more control over what spaces and line breaks are preserved from your markup to the rendered page. Another property worth mentioning, even though it's not currently in the CSS3 specification, is `text-overflow`, which allows the browser to add an ellipsis character (…) to the end of a long string of text instead of letting it overflow.

For details, see:

*   Mozilla Developer Center's reference on [`word-wrap`](https://developer.mozilla.org/en/CSS/word-wrap) and [`white-space`](https://developer.mozilla.org/En/CSS/white-space) (relevant to non-Mozilla browsers, and includes notes on browser compatibility)
*   [How to prevent HTML tables from becoming too wide](https://www.456bereastreet.com/archive/200704/how_to_prevent_html_tables_from_becoming_too_wide/) (using `word-wrap` and `overflow` for various browsers, from 456 Berea Street)
*   [Wrapping Text Inside Pre Tags](https://www.longren.org/2006/09/27/wrapping-text-inside-pre-tags/) (using `white-space` and `word-wrap` for various browsers, from Unwakeable)
*   [The 'white-space' Property In CSS](https://safalra.com/web-design/html-and-css/white-space-property/) (Safalra's Website)
*   [CSS text-overflow](https://www.css3.com/css-text-overflow/) (css3.com)
*   [Using ellipsis with HTML and CSS](https://www.electrictoolbox.com/ellipsis-html-css/) (The Electric Toolbox)
*   [The Future Of CSS Typography](https://www.smashingmagazine.com/2010/03/01/css-and-the-future-of-text/)

**Media Queries**  
_Aids in: adaptability, efficiency_

CSS2 let you apply different styles to different media types — screen, print, and so on. CSS3's [media queries](https://www.w3.org/TR/css3-mediaqueries/) take this a step further by letting you customize styles based on the user's viewport width, display aspect ratio, whether or not his display shows color, and more. For instance, you could detect the user's viewport width and change a horizontal nav bar into a vertical menu on wide viewports, where there is room for an extra column. Or you could change the colors of your text and backgrounds on non-color displays.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86f75464-fa03-4bab-ab8c-0c6be0e12432/part2-mediaqueries1.jpg)](https://devfiles.myopera.com/articles/1541/mediaqueries-example-basic.html)

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b72b74e-6d96-4752-aa32-1a611111484c/part2-mediaqueries2.jpg)](https://devfiles.myopera.com/articles/1541/mediaqueries-example-basic.html)  
_This [demo file from Opera](https://devfiles.myopera.com/articles/1541/mediaqueries-example-basic.html) uses media queries to rearrange elements and resize text and images based on viewport size._

Media queries couldn't come at a better time — there is more variety in the devices and settings people use to browse the web than ever before. You can now optimize your designs more precisely for these variations to provide a more usable and attractive design, but without having to write completely separate style sheets, use JavaScript redirects, and other less efficient development practices.

Media queries are supported to some degree by all the major browsers except IE, and there are lots of great articles and tutorials explaining how to use them right now:

*   [A short introduction to media queries in Firefox 3.5](https://hacks.mozilla.org/2009/06/media-queries/) (applies to other browsers too, from Mozilla Hacks)
*   Safe media queries (Opera Developer Community)
*   [The bleeding edge of web: media queries](https://helephant.com/2008/07/the-bleeding-edge-of-web-media-queries/) (Helephant.com)
*   [Media Queries and CSS3 Experiments — Varying Columns](https://www.unintentionallyblank.co.uk/2007/11/27/media-queries-and-css3-experiments-varying-columns/) (Unintentionally Blank)
*   CSS3 – a big storm is coming (Reinhold Weber) and Using CSS3 media queries to achieve multiple columns on browser resize (mindgarden) show how to use the new multiple columns technique described above in conjunction with media queries
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)
*   Test your browser's media queries support at [Virtuelvis](https://virtuelvis.com/gallery/mediaqueries/)

Media queries are particularly helpful in serving alternate styles to small-screen mobile devices, as these articles and tutorials explain:

*   [Return of the Mobile Stylesheet](https://www.alistapart.com/articles/return-of-the-mobile-stylesheet/) (A List Apart)
*   Coding for the mobile web (Think Vitamin)
*   How to serve the right content to mobile browsers (Opera Developer Community)
*   [Optimizing Web Content](https://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariWebContent/OptimizingforSafarioniPhone/OptimizingforSafarioniPhone.html) (on iPhone, from Safari Web Content Guide)
*   [Mobile optimised websites using CSS3 Media Queries](https://www.alexgdesign.co.uk/articles/mobile-optimised-websites-using-css3-media-queries/) (Alex Gibson)
*   [Determine iPhone orientation using CSS](https://www.thecssninja.com/css/iphone-orientation-css) (The CSS Ninja)

For other options on how to deal with mobile devices, see [Mobile Web Design Trends For 2009](https://www.smashingmagazine.com/2009/01/13/mobile-web-design-trends-2009/).</p>

### Improving Efficiency Through CSS3

Many of the visual effect properties of CSS3 that we've gone over have a great bonus in addition to making your design look great: they can improve efficiency, both in your development process and in the performance of the pages themselves.

Any CSS3 property that keeps you from having to create and add extra images is going to reduce the time it takes you to create new pages as well as re-skin existing ones. Less images also mean less stuff for the server to have to send out and less stuff for the users to download, both of which increase page loading speed.

CSS3 properties that keep you from having to add extra `div`s or extra classes can also reduce your development time as well as file size. We've already gone over some great techniques that help with this, but there are a few more worth mentioning.

**The `box-sizing` Property**  
_Aids in: efficiency_

In addition to the `div`-conserving properties we've already talked about, the [`box-sizing`](https://www.w3.org/TR/css3-ui/#box-sizing) property can also help limit your `div` use in certain situations.

In the traditional W3C box model of CSS 2.1, the value you declare for a width or height controls the width or height of the _content area_ only, and then the padding and border are _added_ onto it. (This is called the content-box model.) If you've worked with CSS for a while, you're probably used to the content-box box model and don't really think much about it. But, it can lead you to add extra `div`s from time to time. For instance, if you want to set a box's width and padding in different units of measurement from each other, like ems for the width and pixels for the padding, it's often easiest to nest another `div` and apply the padding to this instead, to make sure you know how much total space the box will take up. In small doses, nesting additional `div`s simply to add padding or borders is not a great sin. But in complicated designs, the number of extra `div`s can really add up, which adds to both your development time and the file size of the HTML and CSS.

Setting the new `box-sizing` property to `border-box` instead of `content-box` solves this problem so you can get rid of all those extra `div`s. When a box is using the border-box box model, the browser will _subtract_ the padding and border from the width of the box instead of adding it. You always know that the total space the box takes up equals the width value you've declared.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1a8b97d-208c-4856-a161-3e6bf4c09e90/part2-boxsizing.gif)  
_In the traditional box model (bottom image), padding and border are added onto the declared width. By setting `box-sizing` to `border-box` (top image), the padding and border are subtracted from the declared width._

The `box-sizing` property has good [browser support](https://a.deveria.com/caniuse/#eat=css3-boxsizing), with the exception of IE 6 and IE 7\. Unlike the more decorative CSS3 properties, however, lack of support for `box-sizing` could cause your entire layout to fall apart. You'll have to determine how serious the problem would be in your particular case, whether it's worth living with or hacking, or whether you should avoid using `box-sizing` for now.

For details, see:

*   [CSS3 box-sizing attribute](https://helephant.com/2008/10/css3-box-sizing-attribute/) (Helephant.com)
*   CSS3 ‘box-sizing’ concept (James Hopkins)

**CSS3 Pseudo-Classes and Attribute Selectors**  
_Aids in: progressive enhancement, efficiency, modularity, rich typography_

CSS has several really useful [selectors](https://www.w3.org/TR/css3-selectors/) that are only now coming into common use. Many of these are new in CSS3, but others have been around since CSS2, just not supported by all browsers (read: IE) until recently, and thus largely ignored. IE still doesn't support them all, but they can be used to add non-essential visual effects.

Taking advantage of these newer, more advanced selectors can improve your efficiency and make your pages more modular because they can reduce the need for lots of extra classes, `div`s, and `span`s to create the effects you want to see. Some selectors even make certain effects possible that you can't do with classes, such as styling the first line of a block of text differently. These types of visual effects can improve the typography of your site and aid progressive enhancement.

For details, see:

*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)
*   [Taming Advanced CSS Selectors](https://www.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/)
*   [CSS 3 selectors explained](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/) (456 Berea Street)
*   Browser support charts from [kimblim.dk](https://kimblim.dk/css-tests/selectors/) and [l-c-n.com](https://dev.l-c-n.com/CSS3-selectors/browser-support.php)
*   Keith Clark's ie-css3.js emulates support for all CSS3 pseudo selectors to IE, via JavaScript

Read these articles and tutorials for examples of how to put advanced selectors to practical use right now:

*   [Cleaner Code with CSS3 Selectors](https://24ways.org/2009/cleaner-code-with-css3-selectors) (24 Ways)
*   A Look at Some of the New Selectors Introduced in CSS3 (Inspect Element)
*   [Image management, naming and attribute selectors](https://forabeautifulweb.com/blog/about/image_management_naming_and_attribute_selectors/) (For a Beautiful Web)
*   [CSS 3 attribute selectors](https://dev.opera.com/articles/view/css-3-attribute-selectors/) (Opera Developer Community)
*   [Styling a Poem with Advanced CSS Selectors](https://webdesignernotebook.com/css/styling-a-poem-with-advanced-css-selectors/) (Web Designer Notebook)

## HTML5

Although this article is focused on modern CSS techniques, you can't have great CSS-based web pages without great markup behind them. Although [HTML5](https://dev.w3.org/html5/spec/Overview.html) is still in development, and although debate continues about its strengths and weaknesses, some web developers are already using it in their web pages. While HTML 4.01 and XHTML 1.0 are still great choices for the markup of your pages, it's a good idea to start learning what HTML5 has to offer so you can work with it comfortably in the future and perhaps start taking advantage of some of its features now. So, here is a brief overview of how HTML5 can help with our five modern CSS-based web design characteristics (progressive enrichment, adaptive to diverse users, modular, efficient, typographically rich).

Note: Many of these techniques are not supported in enough browsers yet to make their benefits really tangible, so think of this section as, perhaps, “here's how HTML5 _can_ aid these five characteristics in the _future_.”

### New Structural Markup

_Aids: adaptability, modularity, efficiency_ HTML5 introduces a number of new semantic elements that can add more structure to your markup to increase modularity. For instance, inside your main content <code>div</code> you can have several <code>article</code> elements, each a standalone chunk of content, and each can have its own <code>header</code>, <code>footer</code>, and heading hierarchy (<code>h1</code> through <code>h6</code>). You can further divide up an <code>article</code> element with <code>section</code> elements, again with their own <code>header</code>s and <code>footer</code>s. Having clearer, more semantic markup makes it easier to shuffle independent chunks of content around your site if needed, or syndicate them through RSS on other sites and blogs.

In the future, as user agents build features to take advantage of HTML5, these new elements could also make pages more adaptable to different user scenarios. For instance, web pages or browsers could generate table of contents based on the richer hierarchy provided by HTML5, to assist navigation within a page or across a site. Assistive technology like screen readers could use the elements to help users jump around the page to get straight to the important content without needing “skip nav” links.

Although many of these benefits won't be realized until some unforeseen time in the future, you can start adding these new elements now, so that as soon as tools pop up that can take full advantage of them, you'll be ready. Even if your browser doesn't recognize an element, you can still style it — that's standard browser behavior. Well, in every browser but IE. Luckily, you can easily trick IE into styling these elements using a very simple piece of JavaScript, handily provided by [Remy Sharp](https://remysharp.com/2009/01/07/html5-enabling-script/).

Of course, you usually can't depend on all your users having JavaScript enabled, so the very safest and most conservative option is to not use these new structural elements just yet, but use `div`s with corresponding `class` names as if they were these new elements. For instance, where you would use an `article` element, use a `div` with a `class` name of “article.” You can still use the HTML5 doctype — HTML5 pages work fine in IE, as long as you don't use the new elements. You can then later convert to the new HTML5 elements easily if desired, and in the meantime, you can take advantage of the more detailed [HTML5 validators](https://html5.validator.nu/). Also, using these standardized class names can make updating the styles easier for both you and others in your team, and having consistent naming conventions across sites makes it easier for users with special needs to set up user style sheets that can style certain elements in a needed way.

For more on HTML5 markup, see:

*   [HTML5 and The Future of the Web](https://www.smashingmagazine.com/2009/07/16/html5-and-the-future-of-the-web/)
*   [HTML 5 Cheat Sheet (PDF)](https://www.smashingmagazine.com/2009/07/06/html-5-cheat-sheet-pdf/)
*   [Coding A HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/04/designing-a-html-5-layout-from-scratch/)
*   [HTML5 id/class name cheatsheet](https://boblet.tumblr.com/post/60552152/html5) (@boblet)
*   [HTML 5 structure — HTML 4 and XHTML 1 to HTML 5](https://boblet.tumblr.com/post/141239118/html5-structure4) (@boblet)
*   HTML5 Doctor's articles on [header](https://html5doctor.com/the-header-element/), [section](https://html5doctor.com/the-section-element/), [aside](https://html5doctor.com/aside-revisited/), [nav](https://html5doctor.com/nav-element/), [footer](https://html5doctor.com/the-footer-element-update/)
*   @boblet's articles on [div, section, and article](https://boblet.tumblr.com/post/130610820/html5-structure1); [nav, aside, figure, and footer](https://boblet.tumblr.com/post/134732913/html5-structure3); and [header, hgroup, and h1-h6](https://boblet.tumblr.com/post/134276674/html5-structure2)
*   Bruce Lawson's articles on converting his blog to HTML5, [part 1](https://www.brucelawson.co.uk/2009/redesigning-with-html-5-wai-aria/) and [part 2](https://www.brucelawson.co.uk/2009/marking-up-a-blog-with-html-5-part-2/)

### Reducing JavaScript and Plug-in Dependence

_Aids in: adaptability, efficiency_

A number of the new elements and features in HTML5 make effects possible with pure markup that used to be possible only with JavaScript or various third-party plug-ins, like Flash or Java. By removing the need for JavaScript and plug-ins, you can make your pages work on a wider variety of devices and for a wider variety of users. You may also make your development process quicker and more efficient, since you don't have to take the time to find the right script or plug-in and get it all set up. Finally, these techniques may be able to boost the speed of your pages, since extra files don't have to be downloaded by the users. (On the other hand, some may decrease performance, if the built-in browser version is slower than a third-party version. We'll have to wait and see how browsers handle each option now and in the future.)

Some of the features that reduce JavaScript and plug-in dependence are:

*   **New form elements and attributes.**.  HTML5 offers a bunch of new `input` types, such as `email`, `url`, and `date`, that come with built-in client-side validation without the need for JavaScript. There are also many new form attributes that can accomplish what JavaScript used to be required for, like `placeholder` to add suggestive placeholder text to a field or `autofocus` to make the browser jump to a field. The new `input` types degrade to regular inputs in browsers that don't support them, and the new attributes are just ignored, so it doesn't hurt unsupporting browsers to start using them now.

    Of course, you'll have to put in fallback JavaScript for unsupporting browsers, negating the “no JavaScript” benefits for the time being. (Or, depend on server-side validation—which you always ought to have in place as a backup behind client-side validation anyway—to catch the submissions from unsupporting browsers.) Still, they offer a nice usability boost for users with the most up to date browsers, so they're good for progressive enhancement.

*   **The `canvas` element.** The `canvas` element creates a blank area of the screen that you can create drawings on with JavaScript. So, it _does_ require the use of JavaScript, _but_ it removes the need for Flash or Java plug-ins. It's supported in every major browser but IE, but you can make it work in IE easily using the [ExplorerCanvas](https://code.google.com/p/explorercanvas/) script.

  *   **The `video` and `audio` elements.** HTML5 can embed [video](https://dev.w3.org/html5/spec/Overview.html#video) and [audio](https://dev.w3.org/html5/spec/Overview.html#audio) files directly, just as easily as you would add an image to a page, without the need for any additional plug-ins.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df82987e-ab2e-4558-b714-367098171437/part2-html5form.png)](https://www.456bereastreet.com/lab/html5-input-types/)  
_Some of the new input types in HTML5 will bring up widgets, such as the calendar date picker seen with the `datetime` `input` type in Opera, without needing any JavaScript. ([HTML5 input types test page](https://www.456bereastreet.com/lab/html5-input-types/))_

For more on these features, see:

*   [Get Ready for HTML 5](https://www.alistapart.com/articles/get-ready-for-html-5/) (covers forms and `canvas`, from A List Apart)
*   [A Form of Madness](https://diveintohtml5.org/forms.html) (Dive Into HTML5)
*   [Have a Field Day with HTML5 Forms](https://24ways.org/2009/have-a-field-day-with-html5-forms) (24 Ways)
*   The [webforms2](https://code.google.com/p/webforms2/) script adds support for the new form elements and attributes to browsers that don't currently support them.
*   How to Draw with HTML 5 Canvas (Carsonified)
*   [Canvas tutorial](https://developer.mozilla.org/en/Canvas_tutorial) (Mozilla Developer Center)
*   [HTML 5 canvas - the basics](https://dev.opera.com/articles/view/html-5-canvas-the-basics/) (Opera Developer Community)
*   [The video element](https://html5doctor.com/the-video-element/) (HTML5 Doctor)
*   [Introduction to HTML5 video](https://dev.opera.com/articles/view/introduction-html5-video/) (Opera Developer Community)
*   [Native audio in the browser](https://html5doctor.com/native-audio-in-the-browser/) (HTML5 Doctor)

## IE Filtering

_Aids in: progressive enhancement_

IE 6 doesn't seem to be going away anytime soon, so if you want to really make sure your pages are progressively enhanced, you're going to have to learn how to handle it. Beyond ignoring the problem or blocking IE 6 altogether, there are a number of stances you can take:

*   **Use [conditional comments](https://msdn.microsoft.com/en-us/library/ms537512(VS.85).aspx) to fix IE's bugs:** You can create separate style sheets for each version of IE you're having problems with and make sure only that version sees its sheet. The IE sheets contain only a few rules with hacks and workarounds that the browser needs.
*   **Hide all main styles from IE and feed it very minimal styles only:** This is another conditional comment method, but instead of fixing the bugs, it takes the approach of hiding all the complex CSS from IE 6 to begin with, and only feeding it very simple CSS to style text and the like. Andy Clarke calls this [Universal Internet Explorer 6 CSS](https://forabeautifulweb.com/blog/about/universal_internet_explorer_6_css/).
*   **Use JavaScript to “fix” IE:** There are a number of scripts out there that can make IE 6 emulate CSS3, alpha-transparent PNGs, and other things that IE 6 doesn't support. Some of the most popular are [ie7-js](https://code.google.com/p/ie7-js/), [Modernizr](https://www.modernizr.com/), and ie-css3.js.

In addition to the resources linked in the text above, you can learn more about how to handle IE at:

*   [How To Support Internet Explorer and Still Be Cutting Edge](https://www.smashingmagazine.com/2009/12/01/how-to-support-internet-explorer-and-still-be-cutting-edge/)
*   [CSS3 Solutions for Internet Explorer](https://www.smashingmagazine.com/2010/04/28/css3-solutions-for-internet-explorer/)
*   How to Handle IE6: Aggressive Graceful Degradation (Monday by Noon)
*   [Definitive Guide to Taming the IE6 Beast](https://sixrevisions.com/web-development/definitive-guide-to-taming-the-ie6-beast/) (Six Revisions)
*   [Ultimate IE6 Cheatsheet: How To Fix 25+ Internet Explorer 6 Bugs](https://www.virtuosimedia.com/tutorials/ultimate-ie6-cheatsheet-how-to-fix-25-internet-explorer-6-bugs) (Virtuosi Media)
*   [Conditional comments](https://www.quirksmode.org/css/condcom.html) (quirksmode)
*   [Wrapping Your Head around Downlevel Conditional Comments](https://perishablepress.com/press/2007/07/18/wrapping-your-head-around-downlevel-conditional-comments/) (Perishable Press)

## Flexible Layouts

_Aids in: adaptability_

One of the main ways you can make your sites adaptable to your users' preferences is to create flexible instead of fixed-width layouts. We've already gone over how media queries can make your pages more adaptable to different viewport widths, but creating liquid, elastic, or resolution-dependent layouts can be used instead of or in conjunction with media queries to further optimize the design for as large a segment of your users as possible.

*   **Liquid layouts:** Monitor sizes and screen resolutions cover a much larger range than they used to, and mobile devices like the iPhone and iPad let the user switch between portrait and landscape mode, changing their viewport width on the fly. Liquid layouts, also called fluid, change in width based on the user's viewport (eg, window) width so that the entire design always fits on the screen without horizontal scrollbars appearing. The `min-width` and `max-width` properties and/or media queries can and should be used to keep the design from getting too stretched out or too squished at extreme dimensions.
*   **Elastic layouts:** If you want to optimize for a particular number of text characters per line, you can use an elastic layout, which changes in width based on the user's text size. Again, you can use `min-` and `max-width` and/or media queries to limit the degree of elasticity.

  <li><strong>Resolution-dependent layouts:</strong> This type of layout, also called adaptive layout, is similar to media queries, but uses JavaScript to switch between different style sheets and rearrange boxes to accommodate different viewport widths.</li>

For details on creating flexible layouts, see:

*   [70+ essential resources for creating liquid and elastic layouts](https://zomigi.com/blog/essential-resources-for-creating-liquid-and-elastic-layouts/) (zomigi.com)
*   [Fixed vs. Fluid vs. Elastic Layout: What’s The Right One For You?](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/)
*   [Adaptive CSS-Layouts: New Era In Fluid Layouts?](https://www.smashingmagazine.com/2009/06/09/smart-fixes-for-fluid-layouts/)
*   [Resolution dependent layout update](https://www.themaninblue.com/writing/perspective/2006/01/19/) (The Man in Blue)
*   Dynamic Layout (Fortes)
*   [Create Your Own Sliding Resizable Grid](https://www.zackgrossbart.com/hackito/slidegrid/) (Hackito Ergo Sum)

## Layout Grids

_Aids in: modularity, efficiency_

Designing on a grid of (usually invisible) consistent horizontal and vertical lines is not new — it goes back for centuries — but its application to web design has gained in popularity in recent years. And for good reason: a layout grid can create visual rhythm to guide the user's eye, make the design look more clean and ordered, and enforce design consistency.

Grids can also make your designs more modular and your development more efficient because they create a known, consistent structure into which you can easily drop new elements and rearrange existing ones without as much thought and time as it would take in a non-grid layout. For instance, all of your elements must be as wide as your grid's column measurement, or some multiple of it, so you can easily move an element to another spot on the page or to another page and be assured that it will fit and look consistent with the rest of the design. At worst, you'll need to adjust the other elements' widths around it to a different multiple of the column measurements to get the new element to fit, but even this is not too work-intensive, as there is only a handful of pre-determined widths that any element can have.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef6d988e-542b-4c0c-aa76-f1bcd8166c39/part2-grid.jpg)](https://www.nytimes.com/)  
_All of the content of [The New York Times site](https://www.nytimes.com/) falls into a grid of five columns, plus a thin column on the left for navigation._

To learn how to use grids, see:

*   [Designing With Grid-Based Approach](https://www.smashingmagazine.com/2007/04/14/designing-with-grid-based-approach/)
*   [Grid-Based Design: Six Creative Column Techniques](https://www.smashingmagazine.com/2008/03/26/grid-based-design-six-creative-column-techniques/)
*   [Grid design basics: Grids for Web page layouts](https://dev.opera.com/articles/view/grid-design-basics-grids-for-web-page-l/) (Opera Developer Community)
*   Five simple steps to designing grid systems — Preface (five-part series, with tutorials on how to create fixed-width and fluid grids, by Mark Boulton)
*   [Fluid Grids](https://www.alistapart.com/articles/fluidgrids) (A List Apart)
*   [Grid-Based Web Design, Simplified](https://www.smashingmagazine.com/2010/04/grid-based-web-design-simplified/) (Design Informer)
*   [The Grid System](https://www.thegridsystem.org/) (portal to articles, tools, templates, forum, and more)
*   <span class="removed_link" title="https://www.webdesigntoolslist.com/2009/07/webmastertools/roundup-of-css-grid-generators-css-grid-layout-generators/">Roundup of CSS Grid Generators & CSS Grid Layout Generators</span> (also includes list of grid articles, from Web Design Tools)
*   Inspiration galleries [Design By Grid](https://www.designbygrid.com/) and Grid Based Designs

## Efficient CSS Development Practices

_Aids in: modularity, efficiency_

Layout grids and many of the CSS3 techniques we've gone over have the side benefit of making your CSS more modular and helping you write and maintain CSS more efficiently. There are also a few CSS development practices that you can use with _any_ of the techniques we've already covered in order to reduce the time it takes you to write the CSS for those techniques in the first place, as well as save you time reusing components in your pages.</p>

### CSS Frameworks

A CSS framework is a library of styles that act as building blocks to create the standard pieces you might need in your site. While CSS frameworks differ greatly in depth and breadth, most popular, publicly-distributed frameworks contain some sort of layout grid, as well as standard styles for text, navigation, forms, images, and more. It's a good idea to create your own CSS framework, perhaps based on one of the most popular ones; it can be as simple as standardizing the IDs and classes you tend to use on every project and creating a starter style sheet for yourself.

Good CSS frameworks provide you with a solid starting point for your designs, cutting down your time spent developing, testing, tweaking, and updating. They can also reduce the time others (your team members or those who inherit your sites) spend modifying your CSS, as everyone is working from a standard set of conventions. Frameworks can make your designs more modular by giving you a standard set of classes that can be reused from page to page easily, breaking the styles down into separate sheets that can be applied independently to pages on an as-needed basis, or allowing you to plug in various types of content without needing to invent new classes for it.

But, frameworks have their share of problems too. For instance, publicly-distributed (as opposed to your own private) frameworks tend to have large file sizes, as they need to work for any type of site with any type of content; if they're separated into multiple sheets, they can further damage page speed since every HTTP request takes time. We won't get into the full list of pros and cons here, but there are ways to work around many of them, so check out the following articles for the details. You'll also find links to the most popular CSS frameworks.

*   [CSS Frameworks + CSS Reset: Design From Scratch](https://www.smashingmagazine.com/2007/09/21/css-frameworks-css-reset-design-from-scratch/)
*   [Jump-start Your Development With CSS Frameworks](https://www.cssnewbie.com/css-frameworks-described/) (CSS Newbie)
*   [What Are The Benefits of Using a CSS Framework?](https://css-tricks.com/what-are-the-benefits-of-using-a-css-framework/) (CSS-Tricks)
*   [CSS Frameworks](https://www.webdirections.org/resources/kevin-yank-css-frameworks/) (presentation from Web Directions South 2009)
*   [Frameworks for Designers](https://www.alistapart.com/articles/frameworksfordesigners/) (considerations when making your own framework, from A List Apart)
*   <span class="removed_link" title="https://www.w3avenue.com/2009/04/01/guidelines-for-developing-your-own-css-framework/">Guidelines for Developing Your Own CSS Framework</span> (W3Avenue)
*   Creating a Time Saving CSS Template (Arbenting)
*   Why I don’t use CSS Frameworks (Warpspire)
*   Please do not Use CSS Frameworks (Monday by Noon)
*   What's not to love about CSS frameworks? (JeffCroft.com)
*   [Making Modular Layout Systems](https://24ways.org/2008/making-modular-layout-systems) (24 Ways)
*   <span class="removed_link" title="https://www.w3avenue.com/2009/04/29/definitive-list-of-css-frameworks-pick-your-style/">Definitive List of CSS Frameworks – Pick Your Style</span> (W3Avenue)
*   Compare CSS frameworks at [bestwebframeworks.com](https://www.bestwebframeworks.com/css/)

### Object-oriented CSS (OOCSS)

Nicole Sullivan coined the term [object-oriented CSS (OOCSS)](https://www.stubbornella.org/content/2009/02/28/object-oriented-css-grids-on-github/) for her method of creating self-contained chunks of HTML (modules) that can be reused anywhere in the page or site and that any class can be applied to. Some of the main principles of OOCSS are:

*   using primarily classes instead of IDs
*   creating default classes with multiple, more specific classes added on to elements
*   avoiding dependent selectors and class names that are location-specific
*   leaving dimensions off module styles so the modules can be moved anywhere and fit
*   styling containers separately from content

OOCSS aims to make your CSS development more efficient, as well as to make the CSS itself more modular and less redundant, which reduces file sizes and loading speed.

*   [Object Oriented CSS](https://www.stubbornella.org/content/2009/02/28/object-oriented-css-grids-on-github/) (the original blog post, presentation, and framework, at stubbornella.com)
*   Object Oriented CSS (OOCSS): The Lowdown (TYPESETT)
*   [Object-Oriented CSS: What, How, and Why](https://net.tutsplus.com/tutorials/html-css-techniques/object-oriented-css-what-how-and-why/) (Nettuts)

### CSS Generation

When it comes to writing CSS quickly, what could be quicker than having some piece of software write it for you? Now, please don't think that I'm advocating not learning CSS and having a tool write a complete style sheet for you. That is a bad, bad idea. But, there are some quality tools out there that can give you a _headstart_ with your CSS, just to shave a _little_ time off the front of your CSS development process. Most good CSS generators are focused on creating styles for one particular area of your design, such as the layout structure or type styles, not the whole style sheet.

There are far too many tools to link to individually here, so remember when you're finding your own tools to carefully review the CSS it outputs. If it's invalid, bloated, or just plain ugly, don't use the tool! Here are some articles that include lists of and links to CSS generators:

*   [50 Extremely Useful And Powerful CSS Tools](https://www.smashingmagazine.com/2008/12/09/50-really-useful-css-tools/)
*   [35 CSS-Lifesavers For Efficient Web Design](https://www.smashingmagazine.com/2009/06/25/35-css-lifesavers-for-efficient-web-design/)
*   [50 Useful Design Tools For Beautiful Web Typography](https://www.smashingmagazine.com/2009/01/27/css-typographic-tools-and-techniques/)
*   [Zen Coding: A Speedy Way To Write HTML/CSS Code](https://www.smashingmagazine.com/2009/11/21/zen-coding-a-new-way-to-write-html-code/)
*   [50 Useful Tools and Generators for Easy CSS Development](https://speckyboy.com/2009/07/15/50-useful-tools-and-generators-for-easy-css-development/) (speckyboy)
*   <span class="removed_link" title="https://www.w3avenue.com/2009/05/04/list-of-really-useful-tools-for-css-developers/">List of Really Useful Tools for CSS Developers</span> (W3Avenue)

## CSS Performance

_Aids in: efficiency_

Note: Many of these techniques are not supported in enough browsers yet to make their benefits really tangible, so think of this section as, perhaps, “here's how HTML5 _can_ aid these five characteristics in the _future_.”

### New Structural Markup

_Aids: adaptability, modularity, efficiency_ HTML5 introduces a number of new semantic elements that can add more structure to your markup to increase modularity. For instance, inside your main content <code>div</code> you can have several <code>article</code> elements, each a standalone chunk of content, and each can have its own <code>header</code>, <code>footer</code>, and heading hierarchy (<code>h1</code> through <code>h6</code>). You can further divide up an <code>article</code> element with <code>section</code> elements, again with their own <code>header</code>s and <code>footer</code>s. Having clearer, more semantic markup makes it easier to shuffle independent chunks of content around your site if needed, or syndicate them through RSS on other sites and blogs.

In the future, as user agents build features to take advantage of HTML5, these new elements could also make pages more adaptable to different user scenarios. For instance, web pages or browsers could generate table of contents based on the richer hierarchy provided by HTML5, to assist navigation within a page or across a site. Assistive technology like screen readers could use the elements to help users jump around the page to get straight to the important content without needing “skip nav” links.

Although many of these benefits won't be realized until some unforeseen time in the future, you can start adding these new elements now, so that as soon as tools pop up that can take full advantage of them, you'll be ready. Even if your browser doesn't recognize an element, you can still style it — that's standard browser behavior. Well, in every browser but IE. Luckily, you can easily trick IE into styling these elements using a very simple piece of JavaScript, handily provided by [Remy Sharp](https://remysharp.com/2009/01/07/html5-enabling-script/).

Of course, you usually can't depend on all your users having JavaScript enabled, so the very safest and most conservative option is to not use these new structural elements just yet, but use `div`s with corresponding `class` names as if they were these new elements. For instance, where you would use an `article` element, use a `div` with a `class` name of “article.” You can still use the HTML5 doctype — HTML5 pages work fine in IE, as long as you don't use the new elements. You can then later convert to the new HTML5 elements easily if desired, and in the meantime, you can take advantage of the more detailed [HTML5 validators](https://html5.validator.nu/). Also, using these standardized class names can make updating the styles easier for both you and others in your team, and having consistent naming conventions across sites makes it easier for users with special needs to set up user style sheets that can style certain elements in a needed way.

For more on HTML5 markup, see:

*   [HTML5 and The Future of the Web](https://www.smashingmagazine.com/2009/07/16/html5-and-the-future-of-the-web/)
*   [HTML 5 Cheat Sheet (PDF)](https://www.smashingmagazine.com/2009/07/06/html-5-cheat-sheet-pdf/)
*   [Coding A HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/04/designing-a-html-5-layout-from-scratch/)
*   [HTML5 id/class name cheatsheet](https://boblet.tumblr.com/post/60552152/html5) (@boblet)
*   [HTML 5 structure — HTML 4 and XHTML 1 to HTML 5](https://boblet.tumblr.com/post/141239118/html5-structure4) (@boblet)
*   HTML5 Doctor's articles on [header](https://html5doctor.com/the-header-element/), [section](https://html5doctor.com/the-section-element/), [aside](https://html5doctor.com/aside-revisited/), [nav](https://html5doctor.com/nav-element/), [footer](https://html5doctor.com/the-footer-element-update/)
*   @boblet's articles on [div, section, and article](https://boblet.tumblr.com/post/130610820/html5-structure1); [nav, aside, figure, and footer](https://boblet.tumblr.com/post/134732913/html5-structure3); and [header, hgroup, and h1-h6](https://boblet.tumblr.com/post/134276674/html5-structure2)
*   Bruce Lawson's articles on converting his blog to HTML5, [part 1](https://www.brucelawson.co.uk/2009/redesigning-with-html-5-wai-aria/) and [part 2](https://www.brucelawson.co.uk/2009/marking-up-a-blog-with-html-5-part-2/)

### Reducing JavaScript and Plug-in Dependence

_Aids in: adaptability, efficiency_

A number of the new elements and features in HTML5 make effects possible with pure markup that used to be possible only with JavaScript or various third-party plug-ins, like Flash or Java. By removing the need for JavaScript and plug-ins, you can make your pages work on a wider variety of devices and for a wider variety of users. You may also make your development process quicker and more efficient, since you don't have to take the time to find the right script or plug-in and get it all set up. Finally, these techniques may be able to boost the speed of your pages, since extra files don't have to be downloaded by the users. (On the other hand, some may decrease performance, if the built-in browser version is slower than a third-party version. We'll have to wait and see how browsers handle each option now and in the future.)

Some of the features that reduce JavaScript and plug-in dependence are:

*   **New form elements and attributes.**.  HTML5 offers a bunch of new `input` types, such as `email`, `url`, and `date`, that come with built-in client-side validation without the need for JavaScript. There are also many new form attributes that can accomplish what JavaScript used to be required for, like `placeholder` to add suggestive placeholder text to a field or `autofocus` to make the browser jump to a field. The new `input` types degrade to regular inputs in browsers that don't support them, and the new attributes are just ignored, so it doesn't hurt unsupporting browsers to start using them now.

    Of course, you'll have to put in fallback JavaScript for unsupporting browsers, negating the “no JavaScript” benefits for the time being. (Or, depend on server-side validation—which you always ought to have in place as a backup behind client-side validation anyway—to catch the submissions from unsupporting browsers.) Still, they offer a nice usability boost for users with the most up to date browsers, so they're good for progressive enhancement.

*   **The `canvas` element.** The `canvas` element creates a blank area of the screen that you can create drawings on with JavaScript. So, it _does_ require the use of JavaScript, _but_ it removes the need for Flash or Java plug-ins. It's supported in every major browser but IE, but you can make it work in IE easily using the [ExplorerCanvas](https://code.google.com/p/explorercanvas/) script.

  *   **The `video` and `audio` elements.** HTML5 can embed [video](https://dev.w3.org/html5/spec/Overview.html#video) and [audio](https://dev.w3.org/html5/spec/Overview.html#audio) files directly, just as easily as you would add an image to a page, without the need for any additional plug-ins.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df82987e-ab2e-4558-b714-367098171437/part2-html5form.png)](https://www.456bereastreet.com/lab/html5-input-types/)  
_Some of the new input types in HTML5 will bring up widgets, such as the calendar date picker seen with the `datetime` `input` type in Opera, without needing any JavaScript. ([HTML5 input types test page](https://www.456bereastreet.com/lab/html5-input-types/))_

For more on these features, see:

*   [Get Ready for HTML 5](https://www.alistapart.com/articles/get-ready-for-html-5/) (covers forms and `canvas`, from A List Apart)
*   [A Form of Madness](https://diveintohtml5.org/forms.html) (Dive Into HTML5)
*   [Have a Field Day with HTML5 Forms](https://24ways.org/2009/have-a-field-day-with-html5-forms) (24 Ways)
*   The [webforms2](https://code.google.com/p/webforms2/) script adds support for the new form elements and attributes to browsers that don't currently support them.
*   How to Draw with HTML 5 Canvas (Carsonified)
*   [Canvas tutorial](https://developer.mozilla.org/en/Canvas_tutorial) (Mozilla Developer Center)
*   [HTML 5 canvas - the basics](https://dev.opera.com/articles/view/html-5-canvas-the-basics/) (Opera Developer Community)
*   [The video element](https://html5doctor.com/the-video-element/) (HTML5 Doctor)
*   [Introduction to HTML5 video](https://dev.opera.com/articles/view/introduction-html5-video/) (Opera Developer Community)
*   [Native audio in the browser](https://html5doctor.com/native-audio-in-the-browser/) (HTML5 Doctor)

## IE Filtering

_Aids in: progressive enhancement_

IE 6 doesn't seem to be going away anytime soon, so if you want to really make sure your pages are progressively enhanced, you're going to have to learn how to handle it. Beyond ignoring the problem or blocking IE 6 altogether, there are a number of stances you can take:

*   **Use [conditional comments](https://msdn.microsoft.com/en-us/library/ms537512(VS.85).aspx) to fix IE's bugs:** You can create separate style sheets for each version of IE you're having problems with and make sure only that version sees its sheet. The IE sheets contain only a few rules with hacks and workarounds that the browser needs.
*   **Hide all main styles from IE and feed it very minimal styles only:** This is another conditional comment method, but instead of fixing the bugs, it takes the approach of hiding all the complex CSS from IE 6 to begin with, and only feeding it very simple CSS to style text and the like. Andy Clarke calls this [Universal Internet Explorer 6 CSS](https://forabeautifulweb.com/blog/about/universal_internet_explorer_6_css/).
*   **Use JavaScript to “fix” IE:** There are a number of scripts out there that can make IE 6 emulate CSS3, alpha-transparent PNGs, and other things that IE 6 doesn't support. Some of the most popular are [ie7-js](https://code.google.com/p/ie7-js/), [Modernizr](https://www.modernizr.com/), and ie-css3.js.

In addition to the resources linked in the text above, you can learn more about how to handle IE at:

*   [How To Support Internet Explorer and Still Be Cutting Edge](https://www.smashingmagazine.com/2009/12/01/how-to-support-internet-explorer-and-still-be-cutting-edge/)
*   [CSS3 Solutions for Internet Explorer](https://www.smashingmagazine.com/2010/04/28/css3-solutions-for-internet-explorer/)
*   How to Handle IE6: Aggressive Graceful Degradation (Monday by Noon)
*   [Definitive Guide to Taming the IE6 Beast](https://sixrevisions.com/web-development/definitive-guide-to-taming-the-ie6-beast/) (Six Revisions)
*   [Ultimate IE6 Cheatsheet: How To Fix 25+ Internet Explorer 6 Bugs](https://www.virtuosimedia.com/tutorials/ultimate-ie6-cheatsheet-how-to-fix-25-internet-explorer-6-bugs) (Virtuosi Media)
*   [Conditional comments](https://www.quirksmode.org/css/condcom.html) (quirksmode)
*   [Wrapping Your Head around Downlevel Conditional Comments](https://perishablepress.com/press/2007/07/18/wrapping-your-head-around-downlevel-conditional-comments/) (Perishable Press)

## Flexible Layouts

_Aids in: adaptability_

One of the main ways you can make your sites adaptable to your users' preferences is to create flexible instead of fixed-width layouts. We've already gone over how media queries can make your pages more adaptable to different viewport widths, but creating liquid, elastic, or resolution-dependent layouts can be used instead of or in conjunction with media queries to further optimize the design for as large a segment of your users as possible.

*   **Liquid layouts:** Monitor sizes and screen resolutions cover a much larger range than they used to, and mobile devices like the iPhone and iPad let the user switch between portrait and landscape mode, changing their viewport width on the fly. Liquid layouts, also called fluid, change in width based on the user's viewport (eg, window) width so that the entire design always fits on the screen without horizontal scrollbars appearing. The `min-width` and `max-width` properties and/or media queries can and should be used to keep the design from getting too stretched out or too squished at extreme dimensions.
*   **Elastic layouts:** If you want to optimize for a particular number of text characters per line, you can use an elastic layout, which changes in width based on the user's text size. Again, you can use `min-` and `max-width` and/or media queries to limit the degree of elasticity.

  <li><strong>Resolution-dependent layouts:</strong> This type of layout, also called adaptive layout, is similar to media queries, but uses JavaScript to switch between different style sheets and rearrange boxes to accommodate different viewport widths.</li>

For details on creating flexible layouts, see:

*   [70+ essential resources for creating liquid and elastic layouts](https://zomigi.com/blog/essential-resources-for-creating-liquid-and-elastic-layouts/) (zomigi.com)
*   [Fixed vs. Fluid vs. Elastic Layout: What’s The Right One For You?](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/)
*   [Adaptive CSS-Layouts: New Era In Fluid Layouts?](https://www.smashingmagazine.com/2009/06/09/smart-fixes-for-fluid-layouts/)
*   [Resolution dependent layout update](https://www.themaninblue.com/writing/perspective/2006/01/19/) (The Man in Blue)
*   Dynamic Layout (Fortes)
*   [Create Your Own Sliding Resizable Grid](https://www.zackgrossbart.com/hackito/slidegrid/) (Hackito Ergo Sum)

## Layout Grids

_Aids in: modularity, efficiency_

Designing on a grid of (usually invisible) consistent horizontal and vertical lines is not new — it goes back for centuries — but its application to web design has gained in popularity in recent years. And for good reason: a layout grid can create visual rhythm to guide the user's eye, make the design look more clean and ordered, and enforce design consistency.

Grids can also make your designs more modular and your development more efficient because they create a known, consistent structure into which you can easily drop new elements and rearrange existing ones without as much thought and time as it would take in a non-grid layout. For instance, all of your elements must be as wide as your grid's column measurement, or some multiple of it, so you can easily move an element to another spot on the page or to another page and be assured that it will fit and look consistent with the rest of the design. At worst, you'll need to adjust the other elements' widths around it to a different multiple of the column measurements to get the new element to fit, but even this is not too work-intensive, as there is only a handful of pre-determined widths that any element can have.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef6d988e-542b-4c0c-aa76-f1bcd8166c39/part2-grid.jpg)](https://www.nytimes.com/)  
_All of the content of [The New York Times site](https://www.nytimes.com/) falls into a grid of five columns, plus a thin column on the left for navigation._

To learn how to use grids, see:

*   [Designing With Grid-Based Approach](https://www.smashingmagazine.com/2007/04/14/designing-with-grid-based-approach/)
*   [Grid-Based Design: Six Creative Column Techniques](https://www.smashingmagazine.com/2008/03/26/grid-based-design-six-creative-column-techniques/)
*   [Grid design basics: Grids for Web page layouts](https://dev.opera.com/articles/view/grid-design-basics-grids-for-web-page-l/) (Opera Developer Community)
*   Five simple steps to designing grid systems — Preface (five-part series, with tutorials on how to create fixed-width and fluid grids, by Mark Boulton)
*   [Fluid Grids](https://www.alistapart.com/articles/fluidgrids) (A List Apart)
*   [Grid-Based Web Design, Simplified](https://www.smashingmagazine.com/2010/04/grid-based-web-design-simplified/) (Design Informer)
*   [The Grid System](https://www.thegridsystem.org/) (portal to articles, tools, templates, forum, and more)
*   <span class="removed_link" title="https://www.webdesigntoolslist.com/2009/07/webmastertools/roundup-of-css-grid-generators-css-grid-layout-generators/">Roundup of CSS Grid Generators & CSS Grid Layout Generators</span> (also includes list of grid articles, from Web Design Tools)
*   Inspiration galleries [Design By Grid](https://www.designbygrid.com/) and Grid Based Designs

## Efficient CSS Development Practices

_Aids in: modularity, efficiency_

Layout grids and many of the CSS3 techniques we've gone over have the side benefit of making your CSS more modular and helping you write and maintain CSS more efficiently. There are also a few CSS development practices that you can use with _any_ of the techniques we've already covered in order to reduce the time it takes you to write the CSS for those techniques in the first place, as well as save you time reusing components in your pages.</p>

### CSS Frameworks

A CSS framework is a library of styles that act as building blocks to create the standard pieces you might need in your site. While CSS frameworks differ greatly in depth and breadth, most popular, publicly-distributed frameworks contain some sort of layout grid, as well as standard styles for text, navigation, forms, images, and more. It's a good idea to create your own CSS framework, perhaps based on one of the most popular ones; it can be as simple as standardizing the IDs and classes you tend to use on every project and creating a starter style sheet for yourself.

Good CSS frameworks provide you with a solid starting point for your designs, cutting down your time spent developing, testing, tweaking, and updating. They can also reduce the time others (your team members or those who inherit your sites) spend modifying your CSS, as everyone is working from a standard set of conventions. Frameworks can make your designs more modular by giving you a standard set of classes that can be reused from page to page easily, breaking the styles down into separate sheets that can be applied independently to pages on an as-needed basis, or allowing you to plug in various types of content without needing to invent new classes for it.

But, frameworks have their share of problems too. For instance, publicly-distributed (as opposed to your own private) frameworks tend to have large file sizes, as they need to work for any type of site with any type of content; if they're separated into multiple sheets, they can further damage page speed since every HTTP request takes time. We won't get into the full list of pros and cons here, but there are ways to work around many of them, so check out the following articles for the details. You'll also find links to the most popular CSS frameworks.

*   [CSS Frameworks + CSS Reset: Design From Scratch](https://www.smashingmagazine.com/2007/09/21/css-frameworks-css-reset-design-from-scratch/)
*   [Jump-start Your Development With CSS Frameworks](https://www.cssnewbie.com/css-frameworks-described/) (CSS Newbie)
*   [What Are The Benefits of Using a CSS Framework?](https://css-tricks.com/what-are-the-benefits-of-using-a-css-framework/) (CSS-Tricks)
*   [CSS Frameworks](https://www.webdirections.org/resources/kevin-yank-css-frameworks/) (presentation from Web Directions South 2009)
*   [Frameworks for Designers](https://www.alistapart.com/articles/frameworksfordesigners/) (considerations when making your own framework, from A List Apart)
*   <span class="removed_link" title="https://www.w3avenue.com/2009/04/01/guidelines-for-developing-your-own-css-framework/">Guidelines for Developing Your Own CSS Framework</span> (W3Avenue)
*   Creating a Time Saving CSS Template (Arbenting)
*   Why I don’t use CSS Frameworks (Warpspire)
*   Please do not Use CSS Frameworks (Monday by Noon)
*   What's not to love about CSS frameworks? (JeffCroft.com)
*   [Making Modular Layout Systems](https://24ways.org/2008/making-modular-layout-systems) (24 Ways)
*   <span class="removed_link" title="https://www.w3avenue.com/2009/04/29/definitive-list-of-css-frameworks-pick-your-style/">Definitive List of CSS Frameworks – Pick Your Style</span> (W3Avenue)
*   Compare CSS frameworks at [bestwebframeworks.com](https://www.bestwebframeworks.com/css/)

### Object-oriented CSS (OOCSS)

Nicole Sullivan coined the term [object-oriented CSS (OOCSS)](https://www.stubbornella.org/content/2009/02/28/object-oriented-css-grids-on-github/) for her method of creating self-contained chunks of HTML (modules) that can be reused anywhere in the page or site and that any class can be applied to. Some of the main principles of OOCSS are:

*   using primarily classes instead of IDs
*   creating default classes with multiple, more specific classes added on to elements
*   avoiding dependent selectors and class names that are location-specific
*   leaving dimensions off module styles so the modules can be moved anywhere and fit
*   styling containers separately from content

OOCSS aims to make your CSS development more efficient, as well as to make the CSS itself more modular and less redundant, which reduces file sizes and loading speed.

*   [Object Oriented CSS](https://www.stubbornella.org/content/2009/02/28/object-oriented-css-grids-on-github/) (the original blog post, presentation, and framework, at stubbornella.com)
*   Object Oriented CSS (OOCSS): The Lowdown (TYPESETT)
*   [Object-Oriented CSS: What, How, and Why](https://net.tutsplus.com/tutorials/html-css-techniques/object-oriented-css-what-how-and-why/) (Nettuts)

### CSS Generation

When it comes to writing CSS quickly, what could be quicker than having some piece of software write it for you? Now, please don't think that I'm advocating not learning CSS and having a tool write a complete style sheet for you. That is a bad, bad idea. But, there are some quality tools out there that can give you a _headstart_ with your CSS, just to shave a _little_ time off the front of your CSS development process. Most good CSS generators are focused on creating styles for one particular area of your design, such as the layout structure or type styles, not the whole style sheet.

There are far too many tools to link to individually here, so remember when you're finding your own tools to carefully review the CSS it outputs. If it's invalid, bloated, or just plain ugly, don't use the tool! Here are some articles that include lists of and links to CSS generators:

*   [50 Extremely Useful And Powerful CSS Tools](https://www.smashingmagazine.com/2008/12/09/50-really-useful-css-tools/)
*   [35 CSS-Lifesavers For Efficient Web Design](https://www.smashingmagazine.com/2009/06/25/35-css-lifesavers-for-efficient-web-design/)
*   [50 Useful Design Tools For Beautiful Web Typography](https://www.smashingmagazine.com/2009/01/27/css-typographic-tools-and-techniques/)
*   [Zen Coding: A Speedy Way To Write HTML/CSS Code](https://www.smashingmagazine.com/2009/11/21/zen-coding-a-new-way-to-write-html-code/)
*   [50 Useful Tools and Generators for Easy CSS Development](https://speckyboy.com/2009/07/15/50-useful-tools-and-generators-for-easy-css-development/) (speckyboy)
*   <span class="removed_link" title="https://www.w3avenue.com/2009/05/04/list-of-really-useful-tools-for-css-developers/">List of Really Useful Tools for CSS Developers</span> (W3Avenue)

## CSS Performance

_Aids in: efficiency_

Your efficiently _created_ CSS-based web sites also need to _perform_ as efficiently as possible for your users. Many of the CSS3 techniques we've covered can reduce file sizes and HTTP requests to increase the speed of your pages. There are some additional CSS techniques you can use to boost performance.</p>

### CSS Compression

Writing clean CSS that takes advantage of shorthand properties, grouped selectors, and other efficient syntax is nothing new, but it remains very important for improving performance. There are also tricks some CSS developers employ to further reduce CSS file sizes, such as writing each rule on one line to reduce all the line breaks. Although you can do some of this manually, there are a number of tools that can optimize and compress your CSS for you.

For more on methods and tools to optimize and compress your CSS, see:

*   [7 Principles Of Clean And Optimized CSS Code](https://www.smashingmagazine.com/2008/08/18/7-principles-of-clean-and-optimized-css-code/)
*   [How To Automate Optimization and Deployment Of Static Content](https://www.smashingmagazine.com/2009/07/19/how-to-automate-optimization-and-deployment-of-static-content/)
*   [10 Online Tools and Apps to Help Optimize and Format CSS](https://speckyboy.com/2009/11/20/10-online-tools-and-apps-to-help-optimize-and-format-css/) (Speckyboy)
*   <span class="removed_link" title="https://vandelaydesign.com/blog/css/clean-css-code/">23 Resources for Clean and Compressed CSS</span> (Vandelay Design Blog)
*   [Tools for concatenating and minifying CSS and JavaScript files in different development environments](https://robertnyman.com/2010/01/19/tools-for-concatenating-and-minifying-css-and-javascript-files-in-different-development-environments/) (Robert's talk)
*   [Make your pages load faster by combining and compressing javascript and css files](https://rakaz.nl/2006/12/make-your-pages-load-faster-by-combining-and-compressing-javascript-and-css-files.html) (rakaz)
*   Single Line CSS (Ordered List)

### CSS Sprites

CSS Sprites is a CSS technique named by [Dave Shea](https://www.alistapart.com/articles/sprites) of combining many (or all) of your site's images into one big master image and then using `background-position` to shift the image around to show only a single image at a time. This greatly improves your pages' performance because it greatly reduces the number of HTTP requests to your server. This is not a new technique, but it's becoming increasingly important in modern CSS-based web sites as page performance becomes more and more important.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c30fee8a-8ce2-459e-90a1-c7b0bb3b37f0/part2-sprites.jpg)](https://www.apple.com/)

The [Apple site](https://www.apple.com/) uses CSS sprites for various states of its navigation bar.

For details, see:

*   [The Mystery Of CSS Sprites: Techniques, Tools And Tutorials](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/)
*   [CSS Sprites: What They Are, Why They’re Cool, and How To Use Them](https://css-tricks.com/css-sprites/) (CSS-Tricks)
*   [Case Study: The Power of CSS Sprites](https://www.project83.com/blog/case-study-the-power-of-css-sprites/) (Project83 Blog)

Not everyone is a fan of CSS sprites, however. For some opposing arguments, as well as alternative methods of reducing image HTTP requests, see:

*   [CSS Sprites: Useful Technique, or Potential Nuisance?](https://www.smashingmagazine.com/2010/03/26/css-sprites-useful-technique-or-potential-nuisance/)
*   CSS Sprites are Stupid – Let's Use Archives Instead! (Firefox Demo) (kaioa.com)
*   [How to reduce the number of HTTP requests](https://robertnyman.com/2010/01/15/how-to-reduce-the-number-of-http-requests/) (Robert's talk)

## Font Embedding and Replacement

_Aids in: progressive enhancement, rich typography_

Until recently, web designers were limited to working with the fonts on their end users' machines. We now have a number of techniques and technologies that make unique but still readable and accessible text possible.</p>

### The @font-face Rule

The [`@font-face` rule](https://www.w3.org/TR/css3-fonts/#the-font-face-rule), part of CSS3, allows you to link to a font on your server, called a “web font,” just as you can link to images, and displays text on your site in this font. You can now make use of your beautiful, unique fonts instead of just the fonts that most people already have installed on their machines. Fortunately, `@font-face` has good browser support. But alas, it's not as simple as that. Different browsers support different types of fonts, different platforms and browsers anti-alias very differently, you can get a flash of unstyled text before the font loads, your font may not allow `@font-face` embedding in its license, and on and on it goes. To break through the confusion, see these articles:

*   [Beautiful fonts with @font-face](https://hacks.mozilla.org/2009/06/beautiful-fonts-with-font-face/) (Mozilla Hacks)
*   [@font-face in Depth](https://www.useragentman.com/blog/2009/09/20/font-face-in-depth/) (User Agent Man)
*   [How to use CSS @font-face](https://nicewebtype.com/notes/2009/10/30/how-to-use-css-font-face/) (includes links to articles on performance, from Nice Web Type)
*   Mo’ Bulletproofer @Font-Face CSS Syntax (Readable Web)
*   [Becoming a Font Embedding Master](https://snook.ca/archives/html_and_css/becoming-a-font-embedding-master) (Snook.ca)
*   Font Squirrel's [@font-face kits](https://www.fontsquirrel.com/fontface) contain multiple versions of free fonts to accommodate different browsers, plus the CSS to make it work. They also have an [@font-face generator](https://www.fontsquirrel.com/fontface/generator) to create your own kit.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b74ea9-49c9-4e8f-8f25-608f19e01191/part2-fontface.png)](https://samhowat.com/)  
_[Sam Howat's site](https://samhowat.com/) uses `@font-face` to get attractive non-standard fonts into the headings and intro blocks of text._

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b284c7-3e72-4032-ac9c-6a27495e0f16/part2-fontface2.jpg)](https://www.blueskyresumes.com/)  
_[Blue Sky Resumes](https://www.blueskyresumes.com/) uses `@font-face` extensively in headings, feature copy, and the main nav bar of the site._

### Other Font Embedding and Replacement Techniques

If the pure CSS solution of `@font-face` is making your head spin, you can use a font embedding service or font replacement technique.

*   **Font embedding services:** There are a number of third-party font embedding services available that make use of `@font-face`, such as [Typekit](https://typekit.com/) and [Kernest](https://www.kernest.com/), but make implementation easier by helping you work around the browser differences. They also all get around the legal issue of font embedding by providing you with a set of fonts that are licensed for this type of use and impossible or difficult for end users to steal. Most of these services are not free, but some have free options that give you access to a limited set of fonts.
*   **Font replacement techniques:** These free techniques, such as sIFR and [Cufón](https://cufon.shoqolate.com/generate/), do not make use of `@font-face`, but instead use scripting and/or Flash to display fonts that are not on the user’s machine. None of them directly address the licensing issue, but none of them link directly to ready-to-use fonts, so copyright legality is not clear-cut.

For links to these services and techniques, see:

*   [Rich Typography On The Web: Techniques and Tools](https://www.smashingmagazine.com/2009/10/22/rich-typography-on-the-web-techniques-and-tools/)
*   [Roundup of Font Embedding and Replacement Techniques](https://zomigi.com/blog/roundup-of-font-embedding-and-replacement-techniques/) (zomigi.com)

## Conclusion

You're now equipped with the basic knowledge and a slew of links to create modern CSS-based web pages that are progressively enriched, adaptive to diverse users, modular, efficient, and typographically rich. Go out and create great, modern work!

