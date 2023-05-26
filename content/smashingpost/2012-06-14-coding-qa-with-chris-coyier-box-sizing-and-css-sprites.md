---
title: 'Coding Q&A With Chris Coyier: Box-Sizing and CSS Sprites'
slug: coding-qa-with-chris-coyier-box-sizing-and-css-sprites
image: null
date: 2012-06-14T14:40:39.000Z
author: chris-coyier
description: >-
  Howdy, folks! Welcome to the new incarnation of Smashing Magazine’s Q&A. Your question could be about a very specific problem you are having, or it could be a question about philosophical approach. 
categories:
  - Coding
  - CSS
---
We’ve done a bit of this before with a wider scope, so if you enjoy reading the Q&A, check out [my author archive](https://www.smashingmagazine.com/author/chris-coyier/) for more of them.</p>

## Box Sizing

Question from Brad Frost:

<blockquote>
<p>What are your thoughts on <a href="https://paulirish.com/2012/box-sizing-border-box-ftw/">Paul Irish’s idea</a> to apply <code>box-sizing: border-box</code> to every element on the page?</p>

{{% feature-panel %}}

<p>Using <code>box-sizing</code> is super-helpful, especially for mobile and responsive design (for example, getting fully fluid form fields with fixed amounts of padding is awesome). But I’m leery of applying it to everything.</p>

<p>Besides browser support (I’ve already run into issues with some less-than-smart mobile browsers), can you think of any downsides to this technique?</p>
</blockquote>

An armchair critic of this technique would whine about the performance of the universal selector (`*`). This whine has been largely debunked. While this selector technically is “slower” than something like a class name selector, the difference is negligible, except in extreme cases of overuse or on pages with zillions of elements. Doing something that reduces one HTTP request makes at least an order of magnitude bigger difference than optimizing selectors.

For the record, the complete and recommended syntax is this:

<pre><code class="language-css">* {
   -webkit-box-sizing: border-box;
   -moz-box-sizing:    border-box;
   box-sizing:         border-box;
}</code></pre>

With this, you essentially get perfect browser support in everything — even the vast majority of mobile Webkits. The notable exception is IE 7 and below. I don’t want to open a can of worms, but IE 7 usage is already low and dropping much faster than IE 6 did, so supporting only IE 8+ will be commonplace very soon.

Here’s a quick primer on why using this box model is nice:

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85e2bc8e-bd15-4ff8-ae5c-f1468a1d1980/box-model.png "box-model")

*   Now, when you set a width and height, the element will always be that width and height, regardless of padding and borders.
*   This makes math a lot easier. For example, you could easily make a four-column grid by making the width of each column 25% and floating them. You could make gutters out of pixel padding and not worry that they will expand the columns and break the grid.
*   It’s also extra useful for text areas that you want to fill to their parent’s width, which you can only do by setting their width to 100%. But then you wouldn’t be able to have padding unless you used this box model, lest they expand beyond the parent’s width.

You mention a problem with a mobile browser but not exactly what the problem is or which mobile browser. It would be interesting to know which browser and what the problem is, so if you could follow up in the comments, that would be great.

For me, I’m using it on everything I build from here on out. It’s been fantastic so far, and I see no reason not to go with this empirically better box model.</p>

## CSS Sprites Workflow

Question from Matt Banks:

<blockquote>
<p>What’s your preferred method for creating and managing CSS sprites? Do you use Photoshop to manually create your own sprites, a Web service or an app like SpriteRight? For updating sprites with new images, what workflow is best and easiest?</p>
</blockquote>

I have an [article from 2010](https://css-tricks.com/css-sprites-workflow/) about my workflow for CSS sprites, in which step 1 is this:

<blockquote>
<p>Ignore sprites entirely. Make every background image its own separate image and reference them as such in the CSS.</p>
</blockquote>

Of course, I’m not suggesting that you don’t use sprites. Quite the contrary: I think using sprites and having a good workflow are paramount to being a good front-end coder and often the number one thing you can do to optimize Web performance. What I was trying to say is **don’t pre-optimize**. Pre-optimization is quicksand for developers: you spend a lot of time flailing your arms but not getting anywhere. You know that sprites are good, and so you start building with them right away, spending all kinds of time tweaking and adjusting and calculating the sprites to be just right during development.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e127a1c-6e76-49a1-835c-71820c53cb08/2666030594-e0e4782b0c-z.jpeg "2666030594_e0e4782b0c_z")  
_(Image: [electricnerve](https://www.flickr.com/photos/electricnerve/2666030594/sizes/z/in/photostream/))_

This is a waste of time. Instead, ignore sprites on new projects until you have reached a comfortable level of maturity with your CSS or are just about to go live. Then, take the time to go through and get yourself all sprited up. It will be easier and quicker.

In terms of workflow, I’m still a fan of [SpriteMe](https://spriteme.org/), which is a bookmarklet that finds images in use on your page and suggests or creates a sprite for you and even helps you with the CSS. SpriteMe only works on one page at a time, though, which might not be good enough for complex apps. I’m also a big fan of [SpriteCow](https://www.spritecow.com/), in which you handcraft your own sprite (in Photoshop or some other image-editing program), and then it helps you identify the parts with a really great UI and gives you the CSS needed to use a particular image inside the sprite. I think the SpriteCow workflow is a bit better because you are working from a sprite that you made yourself by looking through your images directory, so it’s more comprehensive and to your own style.

To take things to the next level with your CSS sprites workflow, you should really check out how [Compass](https://compass-style.org/) [handles it](https://compass-style.org/help/tutorials/spriting/). [RailsCasts has a screencast](https://railscasts.com/episodes/334-compass-css-sprites) that teaches you about it. It’s pretty awesome. You just use individual images as normal (remember, with no pre-optimization) and drop them into an images directory. Compass will see the new image and automatically add it to a master sprite image. It creates a class name for the new image, with all of the correct sizing and positioning. Then, anywhere you want to use this new image as a sprite, either use that class in your HTML or `@extend` that class in your CSS. Efficient, easy and super-fancy.</p>

## Triangles

Question from Jakob Cosoroaba:

<blockquote>
<p>All boxes are square to the browser. What’s the best way to fake a triangle box?</p>
</blockquote>

To set the stage here, you can “fake” a triangle in a number of ways. The most common is by exploiting the fact that borders end at an angle when they touch each other at corners. So, by collapsing a box to a width and height of `0` and setting the color for only one border, we can make a triangle. A lot of examples of this are on [Shapes of CSS](https://css-tricks.com/examples/ShapesOfCSS/). We could draw a triangle with SVG or canvas. We could even make a triangle, with `linear-gradient` as the background of an element, as easily as this: `background: linear-gradient(45deg, white 90%, blue 90%);` (with all of the vendor prefixes, of course).

But none of these techniques will help us here. In his original question, Jakob Cosoroaba lists two techniques that he has tried. [One](https://jsfiddle.net/cosoroaba/nCEwv/) involves `rotate` transformations and the `clip` property; the problem being that IE 9 has [too large of a rollover area](https://www.screenr.com/ikos) (i.e. it’s not limited to the triangle). The [second technique](https://jsfiddle.net/exKJK/) uses slightly less markup, using only `rotate` transformations; the problem here being that you cannot add content inside. This made clear what he needs:

1.  The ability to put content inside;
2.  The ability to make the triangle (and only the triangle) a link.

Jakob, you should have taken your already clever work just a step further! By combining your two techniques, you could make the link the correct size (even in IE) and put content inside. Just make the link sit on top with `z-index`.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d125a45-e6bf-4070-92fa-7e293f096ce3/triangle.png "triangle")

Here’s a [demo of the combined techniques](https://jsfiddle.net/chriscoyier/xtCb9/1/).

Yep, doing this with markup feels a bit hacky. This is just one of those things that CSS isn’t great at right now.

## Server-Side Optimization

Question from Patrick Schreiner:

<blockquote>
<p>I was wondering if you could provide some insight into what one should keep in mind for server-side optimization and performance when it comes to CSS? Are there any red flags to look out for? What’s your approach to making sure that code performs well and that it’s optimized for heavy server-side optimization?</p>
</blockquote>

I’m not a great server-side guy, but I can list some tips that might be helpful. Perhaps some server folks can help out in the comments.

*   **Just serve CSS straight up.**  
    … Not PHP that has to be run and that then serves as a CSS content type, and not LESS that needs to be interpreted client side — just plain old CSS.
*   **Serve it compressed.**  
    There is no reason for CSS to be optimized for human readability. Strip out all non-relevant white space and comments.
*   **Gzip it.**  
    If you’re running an Apache server (fairly likely), you could put an `.htaccess` file at the root of your website that tells the server to serve your CSS Gzip’ed. Check out the code starting at line 162 in HTML5 Boilerplate’s `.htaccess` file for how to do that.
*   **Cache it.**  
    The fastest file is one you don’t have to serve at all. So, when you do serve a CSS file, tell the browser to keep it around for a long time (a year is a good rule of thumb). Then, if you change the CSS, you can break the cache by changing the file’s name (for example, `global.v23453.css`). Check out the code starting at line 267 in HTML5 Boilerplate’s `.htaccess` file for how to do that.
*   **Keep it small.**  
    If your CSS file is 2 MB, you’re doing it wrong. Maybe you need to get a bit more [OOCSS](https://github.com/stubbornella/oocss/) in your approach, doing things more modularly with very reusable bits of style.
*   **One, two or three**  
    That’s how many CSS files should be loaded on any given page. One if the website is one page. Two for websites of medium complexity, using a global CSS file that all pages need and a second file for subsections of the website that are different enough to warrant one. Three for fairly complex websites that need global, section-specific and page-specific styles.</p>

## Onward!

Keep up the great questions, folks! Got a good one? Send it in, and we’ll pick the best for the next edition.

{{< signature "al" >}}

