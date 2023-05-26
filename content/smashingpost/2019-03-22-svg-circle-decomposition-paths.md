---
title: 'SVG Circle Decomposition To Paths'
slug: svg-circle-decomposition-paths
author: bryan-rasmussen
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a66ccaa-4534-4e37-a9a6-96bcae2ae906/codepen-bryan-rasmussen-smashingmag.png
date: 2019-03-22T13:00:08+01:00
summary: >-
  This article will show you how to turn SVG circles into paths which you can use in animation and text paths, as well as how to turn paths into circles. Once you’ve figured out how it all works, you’ll be able to achieve some quite practical effects. Let’s dig in.
description: >-
  This article will show you how to turn SVG circles into paths which you can use in animation and text paths, as well as how to turn paths into circles. Once you’ve figured out how it all works, you’ll be able to achieve some quite practical effects. Let’s dig in.
categories:
  - SVG
  - CSS
  - Animation
---
This article starts with a confession: I like to hand-code SVG. It’s not always the case but often enough it could seem peculiar to people who do not share my predilection. There are a good number of benefits in being able to write SVG by hand, such as optimizing SVGs in ways a tool can’t (turning a path into a simpler path or shape), or by simply understanding how libraries like D3 or Greensock work.

With that said, I’d like to look more closely at circular shapes in SVG and things we can do with them when we move past a basic circle.  Why circles? Well, I love circles. They’re my favorite shape. 

First off (hopefully you’ve seen a basic circle in SVG before), here’s a pen that shows one:

{{< codepen height="480" theme_id="light" slug_hash="ZPqbWb" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/ZPqbWb/">circle</a> by <a href="https://codepen.io/bryanrasmussen/">Bryan Rasmussen</a>.{{< /codepen >}}

A lot of things can be done with a circle: it can be animated and it can have different colors applied to it. Still, there are two very nice things that you cannot have a circle do in SVG 1.1: You cannot make another graphical element move along the circle’s path (using the `animateMotion` element) and you cannot have shape a text along a circle’s path (this will only be allowed after SVG 2.0 is released).

{{% feature-panel %}}

## Turning Our Circle Into A Path

There is a little online tool that can help you create paths out of circles (you can try it out [here](https://complexdan.com/svg-circleellipse-to-path-converter/)), but we’re going to do be creating everything from scratch so we can find out what’s really going on behind the scenes. 

To make a circular path, we’re going to actually make two arcs, i.e. semicircles that complete the circle in one path. As you’ve probably noticed in the SVG above, the attributes `CX`, `CY`, and `R` respectively define where the circle is drawn along the X and Y axis, while `R` defines the radius of the circle. The `CX` and `CY` create the center of the circle, so the circle is drawn around that point. 

Replicating that circle could look like this:

<pre><code class="language-css">&lt;path
    d="
      M (CX - R), CY
      a R,R 0 1,0 (R &#42; 2),0
      a R,R 0 1,0 -(R &#42; 2),0
    "
/&gt;
</code></pre>

Note that `CX` is the same as the `cx` attribute of the circle; the same goes for `CY` and the `cy` attribute of the circle, as well as `R` and the `r` attribute of the circle. The small `a` character is used to define a segment of an elliptical arc. You can use an optional `Z` (or `z`) to close the path.

The lowercase letter `a` denotes the beginning of an elliptical arc drawn relatively to the current position &mdash; or in our specific case:

<pre><code class="language-css">&lt;path
  d="
    M 25, 50
    a 25,25 0 1,1 50,0
    a 25,25 0 1,1 -50,0
  "
/&gt;
</code></pre>

You can see the magic happening in this pen:

{{< codepen height="480" theme_id="light" slug_hash="jJebGE" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/jJebGE/">circle from path</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

Hidden underneath the path is a circle with a red fill. As you play around with values of the path, you’ll see that circle as long as the path totally covers the circle (the path itself is a circle of the same size), and we’ll know that we’re doing things right. 

One thing you should also know is that as long as you are drawing relative arcs, you don’t need to repeat the `a` command for each arc you draw. When your first 7 inputs are done for your arc, the second 7 inputs will be taken for the next arc.

You can try this out with the pen above by removing the second `a` in the path:

<pre><code class="language-css">a 25,25 0 1,1 50,0

25,25 0 1,1 -50,0
</code></pre>

This may look the same, but I prefer to leave it in until I am ready to finish a drawing, and this also helps me to keep track of where I am. 

{{% ad-panel-leaderboard %}}

### How This Path Works

First, we move to an absolutely positioned `X,Y` coordinate in the image. It does not draw anything there &mdash; it just moves there. Remember that for a circle element `CX`, `CY` denotes the center of the circle; but as it happens in the elliptical arc, the true `CX` and `CY` of the arc will be calculated from the other properties of that arc.

In other words, if we want our `CX` to be at `50` and our radius is `25`, then we need to move to `50 - 25` (if we are drawing from left to right, of course). This means that our first arc is drawn from `25 X, 50 Y` which results to our first arc being `25,25 0 1,0 50,0`.

Let’s break down what the value `25,25 0 1,0 50,0` of our arc actually means:

- `25`: The relative X radius of the arc;
- `25`: The relative Y radius of the arc;
- `0 1,0`: I’m not going to talk about the three middle values (rotation, large-arc-flag, and the sweep-flag properties) because they are not very important in the context of the current example as long as they are the same for both arcs;
- `50`: The ending X coordinate (relative) of the arc; 
- `0`: The ending Y coordinate (relative) of the arc.

The second arc is a `25,25 0 1,0 -50,0`. Keep in mind that this arc will start drawing from wherever the last arc stopped drawing. Of course, the X and Y radius are the same (`25`), but the ending X coordinate is `-50` of where the current one is. 

Obviously this circle could have been drawn in many different ways. This process of turning a circle into a path is known as decomposition. In the [SVG 2 spec decomposition of a circle](https://www.w3.org/TR/SVG/shapes.html#CircleElement) will be done with 4 arcs, however, the method it recommends is not possible to use yet, as it currently depends on a feature named [segment-completing close path](https://www.w3.org/TR/SVG2/paths.html#Segment-CompletingClosePath) which has not yet been specified. 

In order to show you that we can draw the circle in a lot of ways, I have prepared a little pen with various examples:

{{< codepen height="480" theme_id="light" slug_hash="mozNrY" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/mozNrY/">all circles</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

If you take a closer look, you’ll see our original circle along with five different examples of how to draw paths on top of that circle. Each path has a child `desc` element describing the use of `CX`, `CY` and `R` values to build the circle. The first example is the one we discussed here while three others use variations that should be comprehensible from reading the code; the last examples uses four semicircular arcs instead of two, replicating somewhat the process described in the SVG 2 spec linked above.

The circles are layered on top of each other using SVG’s natural z-indexing of placing elements that come later in the markup on top of the ones that come earlier. 

If you click on the circular paths in the pen, the first click will print out how the path is structured to the console and add a class to the element so that you will see the stroke color of how the circle is drawn (you can see that the first circle is drawn with a starting wedge from the stroke). The second click will remove the circle so you have the ability to interact with the circle below. 

Each circle has a different fill color; the actual circle element is yellow and will say “You clicked on the circle” to the console whenever it is clicked on. You can also, of course, simply read the code as the `desc` elements are quite straightforward.

{{% ad-panel-leaderboard %}}

## Going From A Path To A Circle

I suppose you’ve noticed that while there are many different ways to draw the circle, the paths used still look pretty similar. Often &mdash; especially in SVGs output from a drawing program &mdash; circles will be represented by paths. This is probably due to optimization of the graphics program code; once you have the code to draw a path you can draw anything, so just use that. This can lead to somewhat bloated SVGs that are hard to reason about.

<p><strong>Recommended reading</strong>: “<em><a href="https://sarasoueidan.com/blog/svg-tips-for-designers/">Tips For Creating And Exporting Better SVGs For The Web</a>” by Sara Soueidan</em></p>

Let’s take the following [SVG from Wikipedia](https://upload.wikimedia.org/wikipedia/commons/6/6a/Screw_Head_-_Clutch_Type_A.svg) as an example. When you look at the code for that file, you will see that it has a lot of editor cruft once you’ve run it through Jake Archibald’s [SVGOMG!](https://jakearchibald.github.io/svgomg/) (which you can read more about [here](https://www.smashingmagazine.com/2016/04/tools-and-resources-for-editing-converting-and-optimizing-svgs/)), you’ll end up with something like the following file which has been pretty optimized but the circles in the document are still rendered as paths:

{{< codepen height="480" theme_id="light" slug_hash="drgYaq" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/drgYaq/">Wikipedia Screw Head Clutch Type A</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

So, let’s see if we can figure out what those circles should be if they were actual circle elements given what we know about how paths work. The first path in the document is obviously not a circle while the next two are (showing just the `d` attribute):

<pre><code class="language-css">M39 20a19 19 0 1 1-38 0 19 19 0 1 1 38 0z
</code></pre>

<pre><code class="language-css">M25 20a5 5 0 1 1-10 0 5 5 0 1 1 10 0z
</code></pre>

So remembering that the second `a` can be left out, let’s rewrite these to make a little more sense. (The first path is the big circle.)

<pre><code class="language-css">M39 20
a19 19 0 1 1-38 0
a19 19 0 1 1 38 0z
</code></pre>

Those arcs are then obviously the following:

<pre><code class="language-css">aR R 0 1 1 - (R &#42; 2) 0
aR R 0 1 1 (R &#42; 2) 0
</code></pre>

This means that our circle radius is `19`, but what are our `CX` and `CY` values? I think our `M39` is actually `CX + R`, which means that `CX` is `20` and `CY` is `20` too. 

Let’s say you add in a circle after all the paths like this:

<pre><code class="language-css">&lt;circle
 fill="none"
 stroke-width="1.99975"
 stroke="red"
 r="19"
 cx="20"
 cy="20"
/&gt;
</code></pre>

You will see that is correct, and that the red stroked circle covers exactly the large circle. The second circle path reformulated looks like this:

<pre><code class="language-css">M25 20
a5 5 0 1 1-10 0 
5 5 0 1 1 10 0z
</code></pre>

Obviously, the radius is `5`, and I bet our `CX` and `CY` values are the same as before: `- 20`.

<p><strong>Note</strong>: <em>If</em> <code>CX = 20</code><em>, then</em> <code>CX + R = 25</code><em>. The circle is sitting inside the bigger one at the center, so obviously it should have the same </em><code>CX</code><em> and </em><code>CY</code> <em>values.</em></p>

Add the following circle at the end of the paths:

<pre><code class="language-css">&lt;circle
 fill="yellow"
 r="5"
 cx="20"
 cy="20"
/&gt;
</code></pre>

You can now see that this is correct by taking a look at the following pen:

{{< codepen height="480" theme_id="light" slug_hash="oVabMr" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/oVabMr/">Wikipedia Screw Head Clutch Type A_ with example circles</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

Now that we know what the circles should be, we can remove those unneeded paths and actually create the circles &mdash; as you can see here:

{{< codepen height="480" theme_id="light" slug_hash="RderqW" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/RderqW/">Wikipedia Screw Head Clutch Type A optimized</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

## Using Our Circular Path For Wrapping Text

So now that we have our circles in paths, we can wrap text on those paths. Below is a pen with the same paths as our previous “All Circles” pen, but with text wrapped on the path. Whenever you click on a path, that path will be deleted and the text will be wrapped on the next available path, like so:

{{< codepen height="480" theme_id="light" slug_hash="bZmEXr" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/bZmEXr/">all circles wrapped Text</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

Looking at the different paths, you’ll see tiny differences between each one (more on that in a bit), but first there is a little cross-browser incompatibility to be seen &mdash; especially noticeable in the first path:

<table>
  <tbody>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1bf0546-6936-4417-832b-01b5144e1b56/svg-multiarcwithtextlength.png"></td>
      <td>Firefox Developer</td>
    </tr>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/279406dc-6bad-41d8-b51c-abba6d54a3c8/svg-chrome-multiarcpath-smashingwrapped.png"></td>
      <td>Chrome</td>
    </tr>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a105df7b-8a8f-4cbe-9b2c-0fdb8d0c5035/svg-edgetextpathbug.png"></td>
      <td>Microsoft Edge</td>
    </tr>
  </tbody>
</table>

The reason why the starting “S” of “Smashing” is sitting at that funny angle in the Firefox solution is that it is where we actually started drawing our path at (due to the v-R command we used). This is more obvious in the Chrome version where you can clearly see the first pie-shaped wedge of our circle that we drew:

<table class="break-out">
  <tbody>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ecaa1f0-ad96-452e-8885-5a692bcd33c4/svg-chrome-multiarcpath-smashiing-nagazine.png"></td>
      <td>Chrome does not follow all the wedges, so this is the result when you change the text to be “Smashing Magazine”.</td>
    </tr>
  </tbody>
</table>

The reason is that Chrome has a bug regarding inheritance of the `textLength` attribute declared on the parent `text` element. If you want them both to look the same, put the `textLength` attribute on the `textPath` element as well as the text. Why? Because it turns out that Firefox Developer has the same bug if the `textLength` attribute is not specified on the `text` element (this has been the case for some [years](https://bugzilla.mozilla.org/show_bug.cgi?id=890692) now).

Microsoft Edge has a totally different bug; it can’t handle whitespace in between the `Text` and the child `TextPath` element. Once you have removed whitespace, and put the `textLength` attribute on both the `text` and `textPath` elements, they will all look relatively the same (with small variations due to differences in default fonts and so forth). So, three different bugs on three different browsers &mdash; this is why people often prefer to work with libraries!

The following pen shows how the problems can be fixed:

{{< codepen height="480" theme_id="light" slug_hash="EMdKVz" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/EMdKVz/">all circles wrapped Text fixed TextLength</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

I’ve also removed the various fill colors because it makes it easier to see the text wrapping. Removing the fill colors means that my little function to allow you to cycle through the paths and see how they look won’t work unless I add a `pointer-events="all"` attribute, so I’ve added those as well.

**Note**: *You can read more about the reasons for that in “[Managing SVG Interaction With The Pointer Events Property](https://www.smashingmagazine.com/2018/05/svg-interaction-pointer-events-property/)” explained by Tiffany B. Brown.*

We’ve already discussed the wrapping of the multiarc path, so let’s now look at the others. Since we have one path we are wrapping on, the text will always move in the same direction.

<table class="break-out">
  <thead>
    <tr>
      <th>Image</th>
      <th>Path</th>
      <th>Explanation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a00e0af4-7696-4901-8aa2-fa9509284adc/svg-circletext1.png"></td>
      <td><code class="language-css">M CX, CY</code><br /><code class="language-css">a R, R 0 1,0 -(R &#42; 2), 0</code><br /><code class="language-css">a R, R 0 1,0 R &#42; 2, 0</code><br />and uses the <code>translate</code> function to move <code>+R</code> on the X axis.</td>
      <td>The starting position for our <code>textPath</code> (since we have not specified it in any way) is determined by our first ending arc <code>-(R &#42; 2)</code>, given the radius that the arc itself has.</td>
    </tr>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c449e62-b0d6-4665-9535-6d1acdef553c/svg-circletext2.png"></td>
      <td><code class="language-css">M (CX + R), CY</code><br /><code class="language-css">a R,R 0 1,0 -(R &#42; 2),0</code><br /><code class="language-css">a R,R 0 1,0 (R &#42; 2),0</code></td>
      <td>Same applies as the previous path.</td>
    </tr>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad702630-ee12-434e-9f7f-0695d20c6f45/svg-circletext3.png"></td>
      <td><code class="language-css">M CX CY</code><br /><code class="language-css">m -R, 0</code><br /><code class="language-css">a R,R 0 1,0 (R &#42; 2),0</code><br /><code>a R,R 0 1,0 -(R &#42; 2),0</code></td>
      <td>Since we are ending at <code class="language-css">(R &#42; 2 )</code> in our first arc, we will obviously be starting at the opposite position. In other words, this one starts where our previous two paths ended.</td>
    </tr>
    <tr>
      <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65367867-cedc-449b-b500-9ae8aaedda3f/svg-circletext4.png"></td>
      <td><code class="language-css">M (CX - R), CY</code><br /><code class="language-css">a R,R 0 1,</code><code class="language-css" style="background-color: #fffbd7">1</code><code> (R &#42; 2),0</code><br /><code class="language-css">a R,R 0 1,</code><code class="language-css" style="background-color: #fffbd7">1</code><code class="language-css"> -(R &#42; 2),0</code></td>
      <td>This starts in the same position as the last one due to <code class="language-css">(R &#42; 2)</code>, but it is running clockwise because we have set the sweep-flag property (marked in yellow) to <code>1</code>.</td>
    </tr>
  </tbody>
</table>

We‘ve seen how to wrap text on a single path in a circle. Let’s now take a look at how we can break up that path into two paths and the benefits you can get from that.

## Breaking Our Paths Into Parts

There are a lot of things you can do with the text in your path, i.e. achieving stylistic effects with `tspan` elements, setting the offset of the text, or animating the text. Basically, whatever you do will be constrained by the path itself. But by breaking up our multiarc paths into single arc paths, we can play around with the direction of our text, the z-indexing of different parts of our text, and achieving more complex animations. 

First, we are going to want to use another SVG image to show some of the effects. I will be using the diamond from the [article on pointer events](https://www.smashingmagazine.com/2018/05/svg-interaction-pointer-events-property/) which I mentioned earlier. First, let’s show what it will look like with a single path circular text laid on top of it.

Let’s assume that our circle is `CX 295, CY 200, R 175`. Now, following the Circular path method, we now see the following:

<pre><code class="language-css">M (CX - R), CY
a R,R 0 1,1 (R &#42; 2),0
a R,R 0 1,1 -(R &#42; 2),0
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="WmawZK" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/WmawZK/">SVG Amethyst</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

I’m not going to talk about the path or the text size, fill or stroke color. We should all understand that by now, and be able to make it be whatever we want it to be. But by looking at the text, we can see some downsides or limitations right away:

- The text all runs in one direction;
- It might be nice to have some of the text go behind the amethyst, especially where it says MAGAZINE. In order to make the ‘M’ and ‘E’ line up on the circle, the ‘A’ has to be on the side lower point of the amethyst, which feels sort of unbalanced in another way. (I feel like the ‘A’ should be precisely positioned and pointing down at that point.)

If we want to fix these issues, we need to split our single path into two. In the following pen, I have separated the path into two paths, (and placed them into the `defs` area of the SVG for our `textPath`s to reference):

{{< codepen height="480" theme_id="light" slug_hash="VREaXP" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/VREaXP/">SVG Amethyst two paths</a> by <a href="https://codepen.io/Yakudoo">Bryan Rasmussen</a>.{{< /codepen >}}

Again, assuming our `CX` is `295, CY 200, R 175`, then the two paths are in the format of the following (for the top semicircular path):

<pre><code class="language-css">M (CX - R), CY
a R,R 0 1,1 (R &#42; 2),0
</code></pre>

And the following for the bottom:

<pre><code class="language-css">M (CX + R), CY
a R,R 0 1,1 -(R &#42; 2),0
</code></pre>

However, we still have circular text that moves all in the same direction. To fix that for everything but Edge, all you have to do is to add the `side="right"` attribute to the `text` element that holds the ‘MAGAZINE’ `textPath`.

### Making The Text Go Another Direction

If we want to support as many browsers as we can, we have to alter the path and not rely on the `side` attribute which is not fully supported. What we *can* do is to copy our top semicircle path, but change the sweep from `1` to `0`:

Before:

<pre><code class="language-css">M 120, 200
a 175,175 0 1,</code><code class="language-css" style="background-color: #fffbd7">1</code> <code>350,0
</code></pre>

After:

<pre><code class="language-css">M 120, 200
a 175,175 0 1,</code><code class="language-css" style="background-color: #fffbd7">0</code><code> 350,0
</code></pre>

But our text is now drawn on the inner circle defined by the sweep and it won’t look so nice in different browsers. This means that we’re going to have to move the position of our path to align with the ‘S’ of ‘Smashing’, make the ending X of the path greater, and set some offset to the text. As you can see, there is also a little text difference between Firefox and the others which we can improve by increasing the `textLength` attribute on the `text` element, as well as removing whitespace from the `textPath` (since Firefox evidently thinks whitespace is meaningful).

The solution:

{{< codepen height="480" theme_id="light" slug_hash="GeYOvX" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/GeYOvX/">SVG Amethyst two paths fixed</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

### Change The Z-Index Of Part Of Our Circular Text

Finally, we want to make our text goes both in front and behind the amethyst. Well, that’s easy. Remember that SVG’s z-indexing of element is based by where they are in the markup? So if we have two elements, element `1` will be drawn behind element `2`. Next, all we have to do is to move a `text` element up in our SVG markup so it is drawn before the amethyst.

You can see the result below in which parts of the word ‘MAGAZINE’ are hidden by the lower point of the amethyst.

{{< codepen height="480" theme_id="light" slug_hash="bZmYYy" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/bZmYYy/">SVG Amethyst two paths z-index</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

If you take a look at the markup, you can see that the lower semicircle of text has been moved to be before the path that draws the amethyst.

### Animating The Parts Of Our Circle

So now we have the ability to make circular text by completely controlling the directionality of the parts of our text by putting the text into two semicircles. This can, of course, also be exploited to make animations of the text. Making cross-browser SVG animations is really the subject of another article (or *a lot more* articles). These examples will only work in Chrome and Firefox because of using the SMIL-animations syntax instead of CSS keyframes or tools like Greensock. But it gives a good indicator of the effects you can achieve by animating the decomposed circle.

Take the following pen:

{{< codepen height="480" theme_id="light" slug_hash="MxPOVy" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/MxPOVy/">SVG Amethyst two paths animated</a> by <a href="https://codepen.io/bryanrasmussen">Bryan Rasmussen</a>.{{< /codepen >}}

Please press the ‘Rerun’ button on the codepen to see the animation in action. The two parts of our circular text begin animating at the same time, but have a different duration so they end at different times. Because we are animating the `textLength` attribute, we have put two `animate` directives under each text &mdash; one for the `text` element (so Firefox will work) and one for the `textpath` element (so Chrome will work).

## Conclusion

In this article, we’ve seen how to turn a circle into a path and back again, in order to better understand when we need to optimize a path and when not. We’ve seen how turning the circle into a path frees us up to placing the text on the circular path, but also how to further split the circular path into semicircles and gain fuller control over directionality and animation of the component parts of our circular text. 

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Rethinking Responsive SVG'" href="https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/" rel="bookmark">Rethinking Responsive SVG</a></li>
<li><a title="Read 'Animating SVG Files With SVGator'" href="https://www.smashingmagazine.com/2018/07/animating-svg-files-svgator/" rel="bookmark">Animating SVG Files With SVGator</a></li>
<li><a title="Read 'Styling And Animating SVGs With CSS'" href="https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/" rel="bookmark">Styling And Animating SVGs With CSS</a></li>
<li><a title="Read 'Managing SVG Interaction With The Pointer Events Property'" href="https://www.smashingmagazine.com/2018/05/svg-interaction-pointer-events-property/" rel="bookmark">Managing SVG Interaction With The Pointer Events Property</a></li>
</ul>

{{< signature "dm, ra, yk, il" >}}