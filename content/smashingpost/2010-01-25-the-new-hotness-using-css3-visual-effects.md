---
title: 'The New Hotness: Using CSS3 Visual Effects'
slug: the-new-hotness-using-css3-visual-effects
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb68fe74-10fe-4b39-b260-36e404182355/sliding.jpg
date: 2010-01-25T13:48:16.000Z
author: dmitry-dragilev
summary: >-
  This article shows you how to effectively use the new CSS3 properties to speed up development and quickly create rich page elements.
description: >-
  This article shows you how to effectively use the new CSS3 properties to speed up development and quickly create rich page elements.
categories:
  - Coding
  - CSS
  - CSS3
---

Previously in this series on CSS3, we talked not only about [how to create scalable and compelling buttons](https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/) but about [how to effectively use new CSS3 properties](https://www.smashingmagazine.com/2009/12/16/stronger-better-faster-design-with-css3/) to speed up development and quickly create rich page elements. In this final article of the series, we’ll really get into it and use CSS3 visual effects to push the envelope.

Not everything in this article is practical, or even bug&ndash;free, but it’s a fun primer on what’s in the pipeline for Web design. To get the most from these examples, you’ll have to use Safari 4 or Chrome. (Firefox 3.5 can handle most of it, but not everything: WebKit is further along than Gecko in its tentative CSS support.) We’ll show you how to create impressive image galleries, build animated music players and overlay images like a pro. All set? Let’s rock.

## Create A Polaroid Image Gallery

[![Polaroid image gallery](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5406ad34-59ef-4057-9977-dc9257b8995d/hotness-1.png)](https://www.zurb.com/playground/css3-polaroids)

We always try to stay pretty active with [our Flickr feed](https://www.flickr.com/zurbinc); our chief instigator Bryan does a great job of capturing the day&ndash;to&ndash;day and special events and even some of our old work. We wanted a great way to show off these photos, so we turned to CSS3 to create a compelling, fun image gallery. The Polaroid style is pretty common, but we wanted not only to make it dead&ndash;simple to create the gallery in the markup but also to add styles that would have required Javascript just a year or two ago.

{{% feature-panel %}}

### The Polaroid Gallery Markup

First off, we created very simple markup for the gallery, something that would be easy to generate automatically using the Flickr API. The markup for the entire gallery looks like this:

<pre><code>&lt;ul&gt;
	&lt;li&gt;
	   &lt;a href="https://www.flickr.com/photos/zurbinc/3971679981/" title="Roeland!"&gt;
	   	&lt;img src="image-01.jpg" width="250" height="200" alt="Roeland!" /&gt;
	   &lt;/a&gt;																			  
	&lt;/li&gt;
	&lt;li&gt;
	   &lt;a href="https://www.flickr.com/photos/zurbinc/3985295842/" title="Discussion"&gt;
	   	&lt;img src="image-02.jpg" width="250" height="200" alt="Discussion" /&gt;
	   &lt;/a&gt;
	&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

We’ll be using the `title` element in a minute.

### The Base Style and Labels

Our next step was to create the simple Polaroid look. We placed our image inside an anchor with a white background and scaled the image container. This gave us space for the image labels, which we created using little&ndash;known CSS tricks: `:after` and `content: attr`.

<pre><code>ul.polaroids a:after {
	content: attr(title);
}</code></pre>

What we’re doing here is telling the browser that after it renders the given anchor content, add another piece of content. We then generate that piece of content with the `content: attr(title)` element, which pulls a specific attribute from the element, in this case the title attribute. Using `alt` would make more sense, but neither Safari nor Firefox has implemented it for the `content` element.

The snippet above tells the browser to take the `title` attribute and render it immediately after the content. Note that the `title` attribute will be rendered within the anchor, which is exactly what we want. We would have liked to have used the `alt` attribute, but Safari and Firefox do not support the use of content with it.

Our styling of the anchor element takes care of the formatting of the `title` attribute as well, and we’ve now placed the image `title` attribute below it so that we don’t have to replicate that content in the markup.

### Scattering the Pictures

A handful of Polaroids would never be in a perfect grid; they’d be scattered over the table. We compromised by messing up the grid a little bit for each image: a little rotation here, some displacement there. However, we did not want to have to manage that scattering on a per&ndash;image basis, so we used another new pseudo&ndash;class: `nth-child`.

<pre><code>/* By default, we tilt all images by -2 degrees */
ul.polaroids a {
	-webkit-transform: rotate(-2deg);
	-moz-transform: rotate(-2deg);
}

/* Rotate all even images 2 degrees */
ul.polaroids li:nth-child(even) a {
	-webkit-transform: rotate(2deg);
	-moz-transform: rotate(2deg);
}

/* Don’t rotate every third image, but offset its position */
ul.polaroids li:nth-child(3n) a {
	-webkit-transform: none;
	-moz-transform: none;
	position: relative;
	top: -5px;
}</code></pre>

These are only a few of the declarations we used; we actually added them for everything up to 11n, but you get the idea. As you can see, `nth-child` supports a few different arguments, including `even`, `odd` and `Xn` (where X can be any integer). The `even` and `odd` declarations are self&ndash;explanatory. Xn takes every Xth element and applies a particular style; in this example, every 3rd. Combining this with odd, even and some more Xn declarations means that even though the style won’t really be random, it will appear random enough to the average user. You can see the entire set of styles on our [demo page](https://www.zurb.com/playground/css3-polaroids).

We’re using a new CSS3 property here as well: the CSS `transform` (shown as `-webkit-` and `-moz-transform`). The transform property can take a number of arguments for different kinds of transformations; in this example, we’ll be using rotate and scale. You can see the complete (tentative) list in the [Safari Visual Effects Guide](https://developer.apple.com/library/archive/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Introduction.html).

{{% ad-panel-leaderboard %}}

### Some Final Animation

Our last touch was to give the image focus on hover; in this case, to enlarge and straighten out. We accomplish this using a `-webkit-transition` that is activated by the `:hover` pseudo&ndash;class. Check it out:

<pre><code>ul.polaroids a:hover {
	-webkit-transform: scale(1.25);
	-moz-transform: scale(1.25);
	-webkit-transition: -webkit-transform .15s linear;
	position: relative;
	z-index: 5;
}</code></pre>

What’s happening here is that we’re overriding the existing `-webkit-transform` to simply scale the image (this eliminates the rotation). The `-webkit-transition` tells Webkit&ndash;based browsers to animate the transform so that the move from one to another is smooth. `-webkit-transition` is actually extremely versatile, because it can just as easily support `color`, `position` (`top`, `right`, etc.) and most any other property.

That’s how we created our Polaroid gallery. Once you know these new tricks, putting them together is actually pretty easy, and the markup is dead simple.

#### [See the Live Demo &raquo;](https://www.zurb.com/playground/css3-polaroids)

We’ve created a live demo page for this gallery in our Playground, a place for us ZURBians to create small side projects and samples of cool toys. We’ll be linking to the Playground examples throughout this article.

<figure>
	<a href="https://www.zurb.com/playground/css3-polaroids">
	<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8e6fbaf-3ac6-4cc1-8233-4c18dac982ec/polaroid-images-th.jpg" alt="Polaroid image gallery" /></a>
</figure>

## Sliding Vinyl Albums With CSS Gradients

[![Vinyl albums](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e0d0455-09ea-4c0f-a958-e670e82ffe16/hotness-2.jpg)](https://www.zurb.com/playground/sliding-vinyl)

This example began as a simple experiment with CSS gradients and grew into a pretty detailed investigation not just of gradients but of new background properties and animation. We’ll show you how to create advanced gradients with no images and use layered backgrounds for some cool effects.

### Writing the Markup

What we’ve created here is a simple unordered list of albums with slide&ndash;out album controls. You could use something like this to present your band’s albums or to showcase a series of podcasts or any other kind of audio (or potentially video) media. Each item in the list is an album, with some fairly simple markup:

<pre><code>&lt;div class="album"&gt;
	&lt;a href=""&gt;&lt;img src="/playground/sliding-vinyl/muse-the-resistance.jpg" width="500" height="375" alt="Muse: The Resistance" /&gt;&lt;/a&gt;
	&lt;span class="vinyl"&gt;
		&lt;div&gt;&lt;/div&gt;
	&lt;/span&gt;
	&lt;ul class="actions"&gt;
		&lt;li class="play-pause"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
		&lt;li class="info"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
	&lt;/ul&gt;
	&lt;div&gt;
		&lt;h5&gt;Muse&lt;/h5&gt;
		&lt;small&gt;The Resistance&lt;/small&gt;
	&lt;/div&gt;
	&lt;span class="gloss"&gt;&lt;/span&gt;
&lt;/div&gt;
</code></pre>

It might look like a few extraneous elements are in there, but we’ll be using all of them to render our slide&ndash;out record and controller buttons.

### Creating the Record

[![Record](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21870132-5e3c-46f1-a3e7-d18a91032098/hotness-4.png)](https://www.zurb.com/playground/sliding-vinyl)

The real trick here was the album. We challenged ourselves to create the album without using any images at all (we ended up cheating a bit, but we’ll get to that). When it slides out, the album looks like the figure on the left: standard black vinyl with a slight shine to it and a couple of control buttons.

You’ll notice that the inside edge of the album is a little jagged, and that’s because the album isn’t an image but rather two layered gradients generated by the browser and set as the background of the same object. This required not only a bit of messing around with the new gradient objects in CSS3 but also another CSS3 trick: multiple backgrounds. Check out the CSS for the record:

<pre><code>ul.tunes li div.album span.vinyl div {
	display: block;
	border: solid 1px black;
	width: 112px;
	height: 112px;
	-webkit-border-radius: 59px;
	-moz-border-radius: 59px;
	-webkit-box-shadow: 0 0 6px rgba(0,0,0,.5);
	-webkit-transition: all .25s linear;
	background:
		-webkit-gradient(
			linear, left top, left bottom,
			from(transparent),
			color-stop(0.1, transparent),
			color-stop(0.5, rgba(255,255,255,0.25)),
			color-stop(0.9, transparent),
			to(transparent)),
		-webkit-gradient(
			radial, 56 56, 10, 56 56, 112,
			from(transparent),
			color-stop(0.01, transparent),
			color-stop(0.021, rgba(0,0,0,1)),
			color-stop(0.09, rgba(0,0,0,1)),
			color-stop(0.1, rgba(28,28,28,1)),
			to(rgba(28,28,28,1)));
	border-top: 1px solid rgba(255,255,255,.25);
}</code></pre>

We’ve omitted some of the positioning and other boring CSS pieces (check out the live demo for the complete markup). We want to focus here on the pieces that are critical to creating the album visually: `border-radius` and `-webkit-gradient`.

The simplest part was creating a round object: by setting the border radius to exactly half of the height and width of the object, the browser masks the object to a perfect circle. Watch out, though: unlike in Photoshop, if the border radius is higher than half the object’s height or width, the browser might simply ignore the declaration. That said, rounding the object is the easy part; the tricky part is controlling the gradients.

Two gradients are at work on the object: one creates the album itself (complete with the hole in the middle), and the other casts a light across it. We’ll start with the shine:

<pre><code>ul.tunes li div.album span.vinyl div {
	...
	background:
		-webkit-gradient(
			linear, left top, left bottom,
			from(transparent),
			color-stop(0.1, transparent),
			color-stop(0.5, rgba(255,255,255,0.25)),
			color-stop(0.9, transparent),
			to(transparent)),
			...
}</code></pre>

The shine gradient is a linear gradient from the top&ndash;left to bottom&ndash;left. We start with transparent so that the gradient fades in, then we shift the gradient to white at the 50% mark (halfway across the album), with 25% opacity. We’re using RGBa colors because they allow us to control both the color and opacity in the same declaration.

The album itself is more complicated, and it suffers a bit from early implementation of the radial gradient.

<pre><code>ul.tunes li div.album span.vinyl div {
	...
	background:
		...,
		-webkit-gradient(
			radial, 56 56, 10, 56 56, 112,
			from(transparent),
			color-stop(0.01, transparent),
			color-stop(0.021, rgba(0,0,0,1)),
			color-stop(0.09, rgba(0,0,0,1)),
			color-stop(0.1, rgba(28,28,28,1)),
			to(rgba(28,28,28,1)));
	...
}</code></pre>

Radial gradients are just as they sound, and just what you’d expect from gradients in Photoshop. They begin at the center of the object and track across the object in concentric circles. In our case, we wanted to start with transparency, then switch to a solid black, and end up with a very dark gray.

Perhaps the most difficult part of the gradient is declaring its size and position: `radial, 56 56, 10, 56 56, 112`. We have five pieces of data here: type, starting center, starting diameter, ending center and ending diameter. Here’s how they work:

- Radial is, of course, where we define this as a circular gradient rather than straight (linear) gradient.
- We begin at 56 56, which is exactly half the height and width of our 112&ndash;pixel&ndash;tall object. We want the gradient to end with the same center, so we repeat 56 56.
- The gradient begins with a diameter of 10 pixel.
- The ending center (56 56) ensures that this is a concentric gradient.
- 112 is our final diameter, the same width as the object.

The radial implementation was still a bit rough around the edges, so we played around with these values and the color&ndash;stop elements to get the effect we wanted. In the future, a more polished implementation won’t be quite so trial and error.

[![Album cover with disc](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef91cbd8-36f5-499d-9f14-6beee96bc0cb/hotness-3.png)](https://www.zurb.com/playground/sliding-vinyl)

From there, similar to the linear gradient, we created a series of color&ndash;stops to go from transparent to black to dark gray. The result of these two backgrounds (separated by a comma&mdash;thanks, CSS3) is our shiny record. Again, you’ll notice the center is a bit rough, but we’re sure future implementations of this new element will be cleaner.

The button controls are simply rounded anchors (using `border-radius`), with a couple of image glyphs (we told you we cheated a bit). The final touch was to add the animation so that the album would roll out of the sleeve on hover.

{{% ad-panel-leaderboard %}}

### Adding in the Final Animation

To achieve the rolling effect, we paired up a position shift and a rotation effect so that, as the object moves to the right, it rotates just the right amount to appear as if it’s rolling. Here’s what we did:

<pre><code>ul.tunes li div.album span.vinyl {
	-webkit-transition: all .25s linear;
}

ul.tunes li div.album:hover span.vinyl {
	-webkit-transform: translateX(60px);
}

ul.tunes li div.album:hover span.vinyl div { 
	-webkit-transform: rotate(120deg);
}</code></pre>

We’re using two transforms, `translateX` and `rotate`, on two objects. We use the translate instead of standard positioning because transforms don’t impact the DOM&mdash;from a layout perspective, the object never really moves, and so we don’t have to worry about floats going awry or objects pushing each other around. Transitions also work better on translation transforms than on actual position (`left: 20px`, etc.) changes.

Gradients have a ways to go, but there are already some cool uses for generated gradients. You can even control them at runtime using transitions or JavaScript, which opens up yet more possibilities.

#### [See the Live Demo &raquo;](https://www.zurb.com/playground/sliding-vinyl)

We’ve created a live demo page for this gallery in our Playground, so you can see it in action and delve deeper into the source code. Enjoy!

<figure>
	<a href="https://www.zurb.com/playground/sliding-vinyl">
	<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7915f05c-e4d4-47b9-ad5b-e6942c46d623/sliding-vinyl-th.jpg" alt="Sliding vinyl" /></a>
</figure>

## Sweet Overlays With Border&ndash;Image

[![Border image](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d739d0d-430f-4a3e-afcb-66177777afda/hotness-7.png)](https://www.zurb.com/playground/awesome-overlays)

This last part is perhaps the most practical. We use it in our feedback tool [Notable](https://www.notableapp.com) every day. The `border-image` property is new but has some really interesting applications. We’ll explain how it works and how we’re using it in our flagship application.

### The Overlay Markup

Overlays in Notable have two parts: the frame and the actual glass overlay. The markup for the overlay is pretty simple, consisting of two sibling DIVs:

<pre><code>&lt;div class="note" id="note1"&gt;
	&lt;div class="border"&gt;&lt;/div&gt;
	&lt;div class="overlay"&gt;&lt;/div&gt;
	&lt;span class="black circle note"&gt;1&lt;span class="wrap"&gt;&lt;/span&gt;&lt;/span&gt;
&lt;/div&gt;</code></pre>

When we created these overlays, we had a few goals:

- They shouldn’t overly obscure the content beneath them.
- They shouldn’t affect the hue of the content beneath them.
- They must look awesome.

To that end, we devised an overlay that would appear as a glass overlay, with a slight shine and a nice, fairly bold frame. For the purposes of this article, we’ll focus on the frame, which we created using the new `border-image` property.

### Using Border-Image

The new `border-image` property is a strange beast: very versatile, but takes a little getting used to. Here’s what the `border-image` declaration for our frame looks like in the CSS:

<pre><code>div.note div.border {
	border: 5px solid #feb515;
	-webkit-border-radius: 3px;
	-moz-border-radius: 3px;
	-webkit-border-image:
		url(/playground/awesome-overlays/border-image.png) 5 5 5 5 stretch;
	-moz-border-image:
		url(/playground/awesome-overlays/border-image.png) 5 5 5 5 stretch;
}</code></pre>

Let’s get the easy stuff out of the way. The `border` element is both required and a fallback: older browsers will still render a usable border for the overlay, but `border-image` requires a defined border width. While we’ve been fairly unconcerned with backwards&ndash;compatibility in our articles, in this case we needed it (Notable has to work in more than just cutting&ndash;vedge browsers). This is one of many examples of progressive enhancement (or graceful degradation, if you prefer): older browsers render something usable, just less pretty. The first progressive piece in here is the `border-radius`, which we’ve already discussed at length.

The `border-image` is what we’re interested in. Check out the figure to the right; notice the gradient on the frame that goes from top to bottom? It’s a simple touch, but adding it to an object that has to scale to many different sizes required that we use this new property. And we’re glad we did; learning how to use it opened up new possibilities in our coding repertoire. Let’s look at just the `border-image` code again:

<pre><code">url(/playground/awesome-overlays/border-image.png) 5 5 5 5 stretch;</code></pre>

The syntax is the same for WebKit and Gecko(Mox) browsers. The actual declaration is simple. What takes some effort is understanding how to create the image file itself.

Border image takes a single image and slices it into nine pieces, which it then stretches over the object. We’ve sketched a diagram to explain how this works, and we’ve blown up the actual border image file for you to compare. Check it out:

![Border image diagram sketch](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cb95e8-a3a2-4e77-8ab0-e1c548727067/hotness-5.jpg)

The browser takes the top&ndash;vleft corner and uses it for the top&ndash;vleft border, and then it stretches the top&ndash;middle to cover the entire top of the object, and so on around the image.

![Border image diagram](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a00bd32-be2f-4729-b2b2-cb2edbed44f1/hotness-6.png)

We created an image with transparent center, because `border-image` will stretch the center quadrant across the entire object (which seems counterintuitive for a "border" image, but it does make the style a bit more versatile). You’ll notice that the actual gradient is present only in quadrants 4 and 6, because those are the only pieces that will be stretched enough for us to see a gradient. The browser actually does a good job of stretching the image as long as it’s not too complex, so artifacts aren’t really an issue.

The last pieces of the `border-image` declaration are the size and style: `5 5 5 5 stretch`. The repeated 5s determine the size on each side of the object; because we wanted a 5&ndash;pixel border, we created an image that was 15 &times; 15\. If we had used a smaller image, the browser would have had to scale the corners as well, and no doubt it would have looked messier. The last property, `stretch`, dictates how the browser actually handles the pieces of the image. A great (and amusing) intro to the different styles can be found at [lrbabe](https://www.lrbabe.com/sdoms/borderImage/index.html#nogo).

### Putting It Together

Combining the frame with the glass overlay center (which is a semi&ndash;transparent PNG) gives us our frame. Using different border images, we actually created classes for our different colors (red, blue, etc.), while older browsers still get a usable frame without the gradient&ndash;edged niceties. This isn’t an incredibly complex example, but you can see how useful `border-image` can be, especially using an alpha&ndash;mapped image format such as PNG.

#### [See the Live Demo &raquo;](https://www.zurb.com/playground/awesome-overlays)

We’ve created a live demo page for this gallery in our Playground so that you can see it in action and delve deeper into the source code. You can also read up on why we created this overlay in our two&ndash;part Notable Behind the Scenes blog post: part 1 and part 2.

<figure>
	<a href="https://www.zurb.com/playground/awesome-overlays">
	<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcdc5cff-aa6c-4f14-a5fd-4feae9051973/awesome-overlays-th.jpg" alt="Overlay" /></a>
</figure>

## CSS 3 Is Totally Bad Ass

Right? We hope you’ve enjoyed this primer on what we can look forward to in the final CSS3 specification. Familiarize yourself with the properties and start using them&mdash;just be sure to account for browsers that, sadly, will never support all of these fun new tricks. You can see how we use CSS3 in our work for clients as well as in our own product, [Notable](https://www.notableapp.com). Found a super&ndash;awesome way to use these new properties? We’d love to hear about it in the comments!

### References and Resources

- [Introduction to CSS Animation at Surfin’ Safari](https://webkit.org/blog/138/css-animation/)
- [Introduction to CSS Transitions at CSS3.info](https://www.css3.info/webkit-introduce-more-new-features/)
- [Safari Visual Effects Documentation](https://developer.apple.com/safari/library/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Introduction/Introduction.html)

### Further Reading on SmashingMag:

- [Mastering CSS, Part 1: Styling Design Elements](https://www.smashingmagazine.com/2009/08/mastering-css-styling-design-elements/)
- [Designing CSS Buttons: Techniques and Resources](https://www.smashingmagazine.com/2009/11/designing-css-buttons-techniques-and-resources/)
- [Pushing Your Buttons with Practical CSS3](https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/)
- [Stronger, Better, Faster Design with CSS3](https://www.smashingmagazine.com/2009/12/16/stronger-better-faster-design-with-css3/)

{{< signature "al, lu, il" >}}
