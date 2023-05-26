---
title: CSS Sprites Revisited
slug: css-sprites-revisited
image: null
date: 2012-04-11T11:54:00.000Z
author: niels-matthijs
description: >-
  I’m pretty confident that I won’t surprise anyone here by saying that CSS
  sprites have been around for quite a while now, rearing their somewhat
  controversial heads in the Web development sphere as early as 2003.
categories:
  - Coding
  - CSS
  - Techniques
  - Essentials
  - Sprites
---
I’m pretty confident that I won’t surprise anyone here by saying that CSS sprites have been around for quite a while now, rearing their somewhat controversial heads in the Web development sphere as early as 2003.

Still, the CSS sprite hasn’t truly found its way into the everyday toolkit of the common Web developer. While the theory behind CSS sprites is easy enough and its advantages are clear, they still prove to be too bothersome to implement, especially when time is short and deadlines are looming. Barriers exist to be breached, though, and we’re not going to let a couple of tiny bumps in the road spoil the greater perks of the CSS sprite.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

If you want more background information on best practices and practical use cases, definitely read “<a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-CSS-sprites-techniques-tools-and-tutorials/">The Mystery of CSS Sprites: Techniques, Tools and Resources</a>.” If you’re the defensive type, I would recommend “<a href="https://www.smashingmagazine.com/2010/03/26/CSS-sprites-useful-technique-or-potential-nuisance/">CSS Sprites: Useful Technique, or Potential Nuisance?</a>,” which discusses possible caveats.

I won’t take a stance on the validity of CSS sprites. The aim of this article is to find out why people still find it difficult to use CSS sprites. Also, we’ll come up with a couple of substantial improvements to current techniques. So, start up Photoshop (or your CSS sprite tool of choice), put on your LESS and Sass hats, and brush up your CSS pseudo-element skills, because we’ll be mixing and matching our way to easier CSS sprite implementation.

{{% feature-panel %}}

## The Problem With CSS Sprites

While Photoshop is booting, take a moment to consider why CSS sprites have had such a hard time getting widespread acceptance and support. I’m always struggling to find the correct starting position for each image within a sprite. I’ll usually forget the exact coordinates by the time I need to write them down in the style sheet, especially when the image is located at <code>x:259</code>, <code>y:182</code> and measures 17×13 pixels.

I’m always switching back and forth between Photoshop and my CSS editor to write down the correct values, getting more and more frustrated with every switch. I know software is out there specifically tailored to help us deal with this, but I’ve never found an application that lets me properly structure its CSS output so that I can just copy and paste it into my CSS file.

Another important thing to realize is that CSS sprites are meant to be one part of our website optimization toolkit. Many of the people who write and blog about CSS sprites are comfortably wearing their optimization hats while laying out best practices, often going a little overboard and losing track of how much effort it requires to implement their methods of choice.

This is fine if you’re working on an optimization project, but it becomes counterproductive when you need to build a website from scratch while fighting tight deadlines. If you have time to truly focus on implementing a CSS sprite, it’s really not all that hard; but if you have to juggle 50 other priorities at the same time, it does turn into a nuisance for many developers. With these two factors in mind, we’ll try to find a way to make image targeting easier, while coming to terms with the fact that sometimes we have to sacrifice full optimization in the name of ease of development.

<img loading="lazy" decoding="async" title="CSS sprites in the wild: Amazon, Google and Facebook." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82597140-0867-4332-a9fa-f244f9024e0b/sprite-wild1.jpg" alt="CSS sprites in the wild: Amazon, Google and Facebook." width="500" height="340" /><br>
<em>CSS sprites in the wild: Amazon, Google and Facebook.</em>

## Preparing The Sprite

If you look online for examples of CSS sprites, you’ll see that most are optimized for an ideal use of real estate—gaps between images are kept to a minimum in order to keep the load of the entire sprite as low as possible. This reduces loading time considerably when the image is first downloaded, but it also introduces those horrible image coordinates that we mentioned earlier. So, why not take a slightly different approach? Let’s look for an easier way to target images while making sure the resulting sprite is not substantially bigger than the sum of its individual images.

Rather than try to stack the images in such a way that makes the resulting sprite as small as possible, let’s try a different layout. Instead of a random grid, we’re going to build a nice square grid, reserving the space of each square for one image (although larger images might cover multiple squares). The goal is to be able to target the starting point of every image (top-left corner) with a very simple mathematical function.

The size of the grid squares will depend on the average dimension of the images that you’ll be spriting. For my website, I used a 32×32 pixel grid (because only one image exceeds this dimension), but grid sizes will vary according to the situation. Another thing to take into account is the image bleeding that can occur when zooming a page; if you want to play it safe, add a little padding to each image within the sprite. For extra optimization, you could also use a rectangular grid instead of a square grid, further reducing any wasted space; while a tad more complex, this isn’t much different from what we’ll be doing. For this article, though, we’ll stick with the square grid.</p>

## Preparing The Sprite: A Photoshop Bonus

I’m no designer, so I’m not sure how applicable this section is beyond the realm of Photoshop, but there are still some noteworthy improvements that can be made before we get to the actual code. First of all, visualizing the grid can be of great help. Photoshop has guides to do this (so you don’t actually have to include the markers in your sprite), with the added bonus that layers will snap to these guides (making pixel-perfect positioning of each individual image much easier).

Manually adding these guides can be somewhat of a drag, though. Luckily, a colleague of mine (hats off to Filip Van Tendeloo) was kind enough to write and share a <a href="https://onderhond.com/sm/sprite-grid.jsx">little Photoshop script</a> that builds this grid of guides automatically based on the base size of your square. Pretty convenient, no? Just download the script, save it in the <code>PresetsScripts</code> directory, and choose <code>File → Scripts → Sprite Grid</code> from the Photoshop menu.

Finally, to really finish things off, you can add numbers to the x and y axes of your grid so that you can easily pinpoint every square in the grid. Don’t add these numbers to the actual sprite, though; just copy the sprite into a new image and add them there. These numbers are just for reference—but trust me, they will definitely come in handy in a minute.

<img loading="lazy" decoding="async" title="Example of a reference image." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e3088d-d434-4acc-9e03-f419b9bcd928/sprite-ref.jpg" alt="Example of a reference image." width="500" height="340" /><br>
<em>Example of a reference image.</em>

If you can’t (or don’t want to) use preprocessing languages such as LESS and Sass, just add the coordinates of each square instead.</p>

## LESS And Sass To The Rescue

With all of the images on the same square grid, we can now easily compute the top-left coordinate of each image (this coordinate is the exact match needed for the <code>background-position</code> values to reposition the sprite). Just take the base size of the grid and multiply it by the numbers that you just added to your reference image. Say you need to target the image at a position of (5,3), and your grid size is 32 pixels; the top-left position of your image will be 32 × (5,3) = (160,96). To add these values to your CSS file, just use their negative equivalents, like so:

<pre><code class="language-css">background-position: -160px -96px;</code></pre>

Leave your calculator where it is for the time being, because it would be too much of a hassle. If computers are good at anything, it’s doing calculations, so we’re going to make good use of that power. Plain CSS doesn’t allow us to do calculations (yet), but languages like LESS and Sass were made to do just that. If you need more background information, check out the article “<a href="https://www.smashingmagazine.com/2011/09/09/an-introduction-to-less-and-comparison-to-sass/">An Introduction to LESS and Comparison to Sass</a>.” While both languages offer similar functionality, their syntaxes are slightly different. I’m a LESS man myself, but if you’re used to Sass, converting the following examples to Sass code shouldn’t be too hard. Now for some advanced CSS magic:

<pre><code class="language-css">@spriteGrid: 32px;
.sprite(@x, @y) {
   background: url(img/sprite.png) no-repeat;
   background-position: -(@x*@spriteGrid) -(@y*@spriteGrid);
}</code></pre>

Nothing too exciting so far. First, we’ve defined the grid size using a LESS variable (<code>@spriteGrid</code>). Then, we made a mixin that accepts the numbers we added to the reference image earlier. This mixin uses the grid variable and the image’s coordinates to calculate the base position of the image that we want to target. It might not look fancy, but it sure makes the basic use of sprites a lot easier already. From now on, you can just use <code>.sprite(1,5)</code>, and that’s all there is to it. No more annoying calculations or finding random start coordinates.

Of course, the mixin above only works in our somewhat simplified example (using a square grid and just one sprite). Some websites out there are more complex and might require different sprites using rectangular grids for additional optimization. This isn’t exactly impossible to fix with LESS, though:

<pre><code class="language-css">.spriteHelper(@image, @x, @y, @spriteX, @spriteY) {
   background: url("img/@{image}.png") no-repeat;
   background-position: -(@x*@spriteX) -(@y*@spriteY);
}
.sprite(@image, @x, @y) when (@image = sprite1), (@image = sprite3){
   @spriteX: 32px;
   @spriteY: 16px;
   .spriteHelper(@image, @x, @y, @spriteX, @spriteY);
}
.sprite(@image, @x, @y) when (@image = sprite2){
   @spriteX: 64px;
   @spriteY: 32px;
   .spriteHelper(@image, @x, @y, @spriteX, @spriteY);
}</code></pre>

Yes, this looks a bit more daunting, but it’s still pretty basic if you take a minute to understand what’s going on. Most importantly, the added complexity is safely hidden away inside the LESS mixins, and we’re still able to use the same sprite mixin as before, only now with three parameters in total. We’ve just added an image parameter so that we can easily determine which sprite to use each time we call our mixin.

Different sprites might have different grid dimensions, though; so, for each grid dimension, we need to write a separate LESS mixin. We match each sprite to its specific dimension (the example above handles three different sprites and matches it to two different grid dimensions), and we define the dimensions (<code>@spriteX</code> and <code>@spriteY</code>) locally in each mixin. Once that is done, we offload the rest of the work to a little <code>.spriteHelper</code> mixin that does all of the necessary calculations and gives us the same result as before.

The “guards” (as LESS calls them—characterized by the keyword “when”) are quite new to the LESS vocabulary, so do make sure you’re using the latest version of the LESS engine if you attempt to run this yourself. It does offer a great way to keep the sprite mixin as clear and concise as possible, though. Just pass the sprite you want to use to the sprite mixin, and LESS will figure out the rest for you.</p>

## Common CSS Sprite Use Cases

With these mixins at our disposal, let’s see what different CSS sprite use cases we can identify and find out whether capturing these use cases in additional LESS mixins is possible. Once again, in order to minimize complexity in the upcoming sections, we’ll assume you’re working with a square grid sprite. If you need a rectangular grid, just add the image’s parameter to the LESS mixins we’ll be working with, and everything should be fine.

For each use case, we’ll define two mixins: one with and one without height and width parameters. If you’re like me and you keep misspelling the height and width keywords, the second mixin might come in handy. It does leave you the responsibility of learning the correct order of the parameters, though. LESS allows you to define these mixins in the same document, however, so there’s really no harm in listing them both, picking whichever is easiest for you.</p>

### 1. Replaced Text

This is probably the easiest use case, occurring when we have an <code>html</code> element at our disposal that can be given a fixed dimension (in order to ensure we can hide the unwanted parts of the sprite). We’ll also be hiding the text inside the <code>html</code> element, replacing it with an image from our sprite. Typical examples of this use case are action links (think delete icons, print links, RSS icons, etc.) and headings (although CSS3 and Web fonts are quickly making this technique obsolete).

<pre><code class="language-css">.hideText{
   text-indent: -999em;
   letter-spacing: -999em;
   overflow: hidden;
}
.spriteReplace(@x, @y) {
   .sprite(@x, @y);
   .hideText;
}
.spriteReplace (@x, @y, @width, @height) {
   .sprite(@x, @y);
   .hideText;
   width: @width;
   height: @height;
}</code></pre>

The <code>spriteReplace</code> mixin simply wraps our former sprite mixin and adds a small helper mixin to hide the text from view. It’s pretty basic, but it does save us the trouble of adding the <code>.hideText</code> mixin manually for every instance of this use case.

<img loading="lazy" decoding="async" class="118711" title="sprite-replaced" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d21d7507-91cd-46a9-9db0-eb05cf4aae54/sprite-replaced.png" alt="" width="500" height="42" /><br>
<em>Using sprites for replaced elements.</em>

In the example above, we have a list of sharing options. For whatever reason (theming or just personal preference), let’s say we decide to use CSS backgrounds instead of HTML images. Nothing to it with the mixins we just created. Here’s the code (assuming we’re using the reference image shown earlier):

<pre><code class="language-markup tmp-html">&lt;ul class="sharing"&gt;
   &lt;li class="twitter"&gt;&lt;a href="#"&gt;Share [article’s title] on Twitter&lt;/a&gt;&lt;/li&gt;
   …
&lt;/ul&gt;</code></pre>

<pre><code class="language-css">.sharing .twitter a {
   .spriteReplace(0, 0, 32px, 32px); display:block;
}</code></pre>

### 2. Inline Images

For the second use case, we’ll tackle inline images. The main problem we’re facing here is that we won’t be able to put fixed dimensions on the <code>html</code> element itself because we’re dealing with variable-sized content. Typical uses of inline images are for icons next to text links (for example, external links, download links, etc.), but this method can also be used for any other item that allows text to be wrapped around a sprite image.

<pre><code class="language-css">.spriteInline(@x, @y) {
   .sprite(@x, @y);
   display: inline-block;
   content: "";
}

.spriteInline(@x, @y, @width, @height) {
   .sprite(@x, @y);
   display: inline-block;
   content: "";
   width: @width;
   height: @height;
}</code></pre>

We might be lacking a structural element to visualize our image, but 2011 taught us that pseudo-elements are the perfect hack to overcome this problem (Nicolas Gallagher’s eye-opening article on <a href="https://nicolasgallagher.com/css-background-image-hacks/">using pseudo-elements for background images</a> explains everything in detail). This is why the <code>spriteInline</code> mixin was especially developed to be used within a <code>:before</code> or <code>:after</code> selector (depending on where the image needs to appear). We’ll add an <code>inline-block</code> declaration to the pseudo-element so that it behaves like an inline element while still allowing us to add fixed dimensions to it, and we’ll add the <code>content</code> property, which is needed just for visualizing the pseudo-element.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="118712" title="sprite-inline" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/374862b3-ada5-40b9-afea-60c7eaf3ab1a/sprite-inline.png" alt="" width="500" height="103" /><br>
<em>Using sprites for inline images.</em>

The example above shows a list of affiliate links. The design demands that each link be limited to one line, so we can safely use the <code>.spriteInline</code> mixin to display the icons in front of each link:

<pre><code class="language-markup tmp-html">&lt;ul class="affiliates"&gt;
   &lt;li class="amazon"&gt;&lt;a href="#"&gt;Buy on Amazon.com&lt;/a&gt;&lt;/li&gt;
   …
&lt;/ul&gt;</code></pre>

<pre><code class="language-css">.affiliates .amazon a:before {
   .spriteInline(4, 1, 22px, 16px);
}</code></pre>

### 3. Padded Images

The third and final use case comes up when text isn’t allowed to wrap around a sprite image. Typical examples are list items that span multiple lines, and all kinds of visual notifications that bare icons. Whenever you want to reserve space on a multi-line element to make sure the text lines up neatly next to the image, this is the method you’ll want to use.

<pre><code class="language-css">.spritePadded(@x, @y) {
   .sprite(@x, @y);
   position: absolute;
   content: "";
}
.spritePadded(@x, @y, @width, @height) {
   .sprite(@x, @y);
   position: absolute;
   content: "";
   width: @width;
   height: @height;
}</code></pre>

Again we’ll try our luck with pseudo-elements; this time, though, we’ll be performing some positioning tricks. By applying a <code>position: absolute</code> to the pseudo-element, we can place it right inside the space reserved by its parent element (usually by applying padding to the parent—hence, the name of the mixin). The actual position of the image (the <code>left</code>, <code>right</code>, <code>top</code> and <code>bottom</code> properties) is not added to the <code>spritePadded</code> mixin and should be done in the selector itself to keep things as clean and simple as possible (in this case, by maintaining a low parameter count).

Because we’re using absolute positioning, either the <code>:before</code> or <code>:after</code> pseudo-element will do the job. Keep in mind, though, that the <code>:after</code> element is a likely candidate for CSS clearing methods, so if you want to avoid future conflicts (because the clearing fix won’t work if you add a <code>position: absolute</code> to the <code>:after</code> pseudo-element), you’d be safest applying the sprite style to the <code>:before</code> element.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="118713" title="sprite-padded" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d439e5b-550b-4e86-9674-2e7a21613c38/sprite-padded.png" alt="" width="500" height="62" /><br>
<em>Using sprites for padded elements.</em>

Let’s assume we need to indicate that our article is available in other languages (probably on a different page or even website). We’ll add a little notification box, listing the different translations of the current article. If the text breaks onto a second line, though, we do not want it to crawl below our little icon, so we’ll use the <code>spritePadded</code> mixin:

<pre><code class="language-markup tmp-html">&lt;section class="notification translated"&gt;
   &lt;p&gt;Translation available…&lt;/p&gt;
&lt;/section&gt;</code></pre>

<pre><code class="language-css">.translated p {
   padding-left: 22px;
   position: relative;
}
.translated p:before {
   .spritePadded(5, 5, 16px, 14px);
   left: 0;
   top: 0;
}</code></pre>

## The Ideal Sprite

So, have we achieved CSS sprite wizardry here? Heck, no! If you’ve been paying close attention, you might have noticed that the use cases above offer no solution for adding repeating backgrounds to a sprite. While there are some ways around this problem, none of them are very efficient or even worthy of recommendation.

What CSS sprites need in order to truly flourish is a CSS solution for cropping an image. Such a property should define a crop operation on a given background image before the image is used for further CSS processing. This way, it would be easy to crop the desired image from the sprite and position it accordingly, repeating it as needed; we’d be done with these <code>:before</code> and <code>:after</code> hacks because there wouldn’t be anything left to hide. A solution has been proposed in the Editor’s Draft of the <a href="https://dev.w3.org/csswg/css3-images/#url">CSS Image Values and Replaced Content Module Level 3</a> (section 3.2.1), but it could take months, even years, for this to become readily available.

For now, the LESS mixins above should prove pretty helpful if you plan to use CSS sprites. Just remember to prepare your sprite well; if you do, things should move ahead pretty smoothly, even when deadlines are weighing on you.

{{< signature "al" >}}

