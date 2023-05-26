---
title: Connecting The Dots With CSS3
slug: css-three-connecting-the-dots
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2268800d-b169-44b9-9a97-5ce48ac1f91f/css-25.png
date: 2010-05-27T09:18:21.000Z
author: trent-walton
description: >-
  As a web community, we’ve made a lot of exciting progress in regards to CSS3\. We’ve put properties like `text-shadow` & `border-radius` to good use while stepping into `background-clip` and visual effects like transitions and animations. We’ve also spent a great deal of time debating how and when to implement these properties. Just because a property isn’t widely supported by browsers or fully documented at the moment, it doesn’t mean that we shouldn’t be working with it.
categories:
  - Coding
  - CSS
  - Techniques
  - CSS3
---
In fact, I’d argue the opposite.

Best practices for CSS3 usage need to be hashed out in blog posts, during spare time, and outside of client projects. Coming up with creative and sensible ways to get the most out of CSS3 will require the kind of experimentation wherein developers gladly trade ten failures for a single success. Right now, there are tons of property combinations and uses out there waiting to be discovered. All we have to do is connect the dots. It’s time to get your hands dirty and innovate!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af117f71-6219-43d7-a014-e11cf5e9171a/connectingthedots1.png" alt="CSS Three: Connecting The Dots" width="500" height="300" />

{{% feature-panel %}}

## Where Do I Start?

One of my favorite things to do is to scan a list of CSS properties and consider which ones might work well together. What would be possible if I was to connect @font-face to <code>text-shadow</code> and the <code>bg-clip:text</code> property? How could I string a <code>webkit-transition</code> and <code>opacity</code> together in a creative way? Here are a few results from experiments I’ve done recently. While some may be more practical than others, the goal here is to spark creativity and encourage you to connect a few dots of your own.

<em>Note: While Opera and Firefox may soon implement specs for many of the CSS3 properties found here, some of these experiments will currently only work in Webkit-browsers like Google Chrome or Safari.</em>

## Example #1: CSS3 Transitions

A safe place to start with CSS3 visual effects is transitioning a basic CSS property like <code>color</code>, <code>background-color</code>, or <code>border</code> on hover. To kick things off, let’s take a link color CSS property and connect it to a .4 second transition.

<a href="https://trentwalton.com/css3/connecting_the_dots"><img loading="lazy" decoding="async" class="45952" title="example_1a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54bf5fbd-5d01-4166-8b39-4feb9940e06c/example-1a.jpg" alt="Screenshot" width="500" height="100" /></a>

Start with your link CSS, including the hover state:

<pre><code class="language-css">a { color: #e83119; }
a:hover { color:#0a99ae; }</code></pre>

Now, bring in the CSS3 to set and define which property you’re transitioning, duration of transition and how that transition will proceed over time. In this case we’re setting the color property to fade over .4 seconds with an <code>ease-out</code> timing effect, where the pace of the transition starts off quickly and slows as time runs out. To learn more about timing, check out the <a href="https://webkit.org/blog/138/css-animation/">Surfin’ Safari Blog post on CSS animations</a>. I prefer <code>ease-out</code> most of the time simply because it yields a more immediate transition, giving users a more immediate cue that something is changing.

<pre><code class="language-css">a {
-webkit-transition-property: color;
-webkit-transition-duration:.4s;
-webkit-transition-timing:ease-out;
}</code></pre>

You can also combine these into a single CSS property by declaring the property, duration, and timing function in that order:

<pre><code class="language-css">a { -webkit-transition: color .4s ease-out; }</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots">View the live example here</a>

The final product should be a red text link that subtly transitions to blue when users hover with their mouse pointer. This basic transitioning technique can be connected to an infinite amount of properties. Next, let’s let’s create a menu bar hover effect where border-thickness is combined with a .3 second transition.

<a href="https://trentwalton.com/css3/connecting_the_dots"><img loading="lazy" decoding="async" class="45953" title="example_1b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/116e1b8a-3e64-4d76-84da-b34f756a5379/example-1b.jpg" alt="Screenshot" width="500" height="123" /></a>

To start, we’ll set a series of navigation links with a 3 pixel bottom border, and a 50 pixel border on hover:

<pre><code class="language-css">border-nav a { border-bottom: 3px solid #e83119 }
border-nav a:hover { border-bottom: 50px solid #e83119 }</code></pre>

To bring the transition into the mix, let’s set a transition to gradually extend the border thickness over .3 seconds in a single line of CSS:

<pre><code class="language-css">border-nav a { -webkit-transition: border .3s ease-out; }</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots">View the live example here</a>

### Examples

This is just one example of how to use these transitions to enhance links and navigation items. Here are a few other sites with similar creative techniques:

<a href="https://teamexcellence.com">Team Excellence</a>
The webkit transition on all navigation items, including the main navigation set at .2s provides a nice effect without making visitors wait too long for the hover state.

<a href="https://teamexcellence.com/"><img loading="lazy" decoding="async" class="45971" title="team_excellence_transition" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/601065a1-c878-449d-8c4e-7d6a4beb9d6e/team-excellence-transition.jpg" alt="Screenshot" width="500" height="300" /></a>

<a href="https://www.ackernaut.com">Ackernaut</a>
Ackernaut has subtle transitions on all link hovers, and extends the property to fade the site header in/out.

<a href="https://www.ackernaut.com/"><img loading="lazy" decoding="async" class="45947" title="ackernaut_transitions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a30a7aa-40db-4407-92fb-f2fd461c80e6/ackernaut-transitions.jpg" alt="Screenshot" width="500" height="300" /></a>

<a href="https://simplebits.com">SimpleBits</a>
The SimpleBits main navigation transitions over .2 seconds with linear timing.

<a href="https://simplebits.com/"><img loading="lazy" decoding="async" class="45970" title="simplebits_transition" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdcc7fe4-d12d-4c46-a9a3-3338bc6d5ce6/simplebits-transition.jpg" alt="screenshot" width="500" height="169" /></a>

DesignSwap
On DesignSwap, all text links have a .2 second transitions on hover and the swapper profiles fade out to real details about the latest designs.

<img loading="lazy" decoding="async" class="45949" title="designswap_transitions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/717a9976-fbfc-4adc-b64f-3a115fee3e2a/designswap-transitions.jpg" alt="Design Swap" width="500" height="284" />

<a href="https://jackosborne.co.uk">Jack Osborne</a>
Jack Osborne transitions all of the blue links as well as the post title link on his home page.

<a href="https://jackosborne.co.uk/"><img loading="lazy" decoding="async" class="45963" title="jackosborne_transitions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84bdc7c7-26ec-4b76-b0b6-3a024c6ce1eb/jackosborne-transitions.jpg" alt="Jack Osborne" width="500" height="300" /></a>

<a href="https://esquareda.com">Eric E. Anderson</a>
Eric E. Andersion has taken CSS3 implementation even further by implementing a transition on his main navigation for background color and color alongside <code>border-radius</code> and <code>box-shadow</code>.

<a href="https://esquareda.com/"><img loading="lazy" decoding="async" class="45950" title="ericeanderson" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ee08b6-7f3f-4b03-a2b8-958e10cd6e11/ericeanderson.jpg" alt="E2A" width="500" height="270" /></a>

## Example #2: Background Clip

When connected to properties like <code>text-shadow</code> and @font-face, the <code>background-clip</code> property makes all things possible with type. To keep things simple, we’ll start with taking a crosshatch image and masking it over some text. The code here is pretty simple. Start by wrapping some HTML in a div class called <em>bg-clip</em>:

<pre><code class="language-markup tmp-xml">&lt;div class="bg-clip"&gt;
&lt;h3&gt;kablamo!&lt;/h3&gt;
&lt;/div&gt;</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots/#2"><img loading="lazy" decoding="async" class="45954" title="example_2a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0be38ba8-47a3-40c9-9b82-ba28337ea3ea/example-2a.jpg" alt="example 2a" width="500" height="123" /></a>

Now to the CSS. First, set the image you will be masking the text with as the background-image. Then, set the <code>-webkit-text-fill-color</code> to transparent and define the <code>-webkit-background-clip</code> property for the text.

<pre><code class="language-css">.bg-clip {
background: url(../img/clipped_image.png) repeat;
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
}</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots/#2">View the live example here</a>

This opens the door for you to start adding texture or other graphic touches to your type without resorting to using actual image files. For even more CSS3 text experimentation, we can add the transform property to rotate the text (or any element for that matter) to any number of degrees. All it takes is a single line of CSS code:

<pre><code class="language-css">-webkit-transform: rotate(-5deg);
-moz-transform: rotate(-5deg);
-o-transform: rotate (-5deg);</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots/#2"><img loading="lazy" decoding="async" class="45955" title="example_2b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9790fc4-053b-4863-ae7a-50029d67da8d/example-2b.jpg" alt="example 2b" width="500" height="136" /></a>

<em>Note: While <code>background-clip</code> isn’t available in Firefox or Opera, the transform property is, so we’ll set this for each browser.</em>

<a href="https://trentwalton.com/css3/connecting_the_dots/#2">View the live example here</a>

### Examples

This is a fairly simple implementation, but there are quite a few really interesting and innovative examples of this technique:

<a href="https://trentwalton.com/css3/type">Trent Walton</a>
An experiment of my own, combining <code>bg-clip</code> and @font-face to recreate a recent design.

<a href="https://trentwalton.com/css3/type"><img loading="lazy" decoding="async" class="45973" title="trentwalton_bgclip" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea69b679-8558-4c89-8327-1f12a01d76b2/trentwalton-bgclip.jpg" alt="Trent Walton" width="500" height="286" /></a>

<a href="https://neography.com/experiment/type1/">Neography</a>
An excellent example of what is possible when you throw <code>rotate</code>, <code>bg-clip</code> and @font-face properties together.

<a href="https://neography.com/experiment/type1/"><img loading="lazy" decoding="async" class="45965" title="neography_rotate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9ea6c41-f4bd-4c6d-b4e7-c0b19a3d1b3f/neography-rotate.jpg" alt="neography rotate" width="500" height="286" /></a>

<a href="https://www.everydayworks.com/?p=318">Everyday Works</a>
One of the earliest innovative implementations of CSS text rotation I’ve seen.

<a href="https://www.everydayworks.com/?p=318"><img loading="lazy" decoding="async" class="45951" title="everydayworks_rotate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4471b035-7cd4-4a39-a1d7-998f3a98baf4/everydayworks-rotate.jpg" alt="EveryDayWorks" width="500" height="286" /></a>

<a href="https://www.panic.com/blog">Panic Blog</a>
The Panic blog randomly rotates <code>div</code>s / posts. Be sure to refresh to see subtle changes in the degree of rotation.

<a href="https://www.panic.com/blog"><img loading="lazy" decoding="async" class="45967" title="panic_rotate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/045d054b-99ff-4f11-9c39-40bc1150403a/panic-rotate.jpg" alt="panic blog" width="500" height="300" /></a>

<a href="https://sam.brown.tc/">Sam Brown</a>
Sam's got a really nice text-rotate hover effect on the "stalk" sidebar links.

<a href="https://sam.brown.tc/"><img loading="lazy" decoding="async" class="45968" title="sambrown_rotate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61fbbfa1-64ea-4f64-a891-4a8744970448/sambrown-rotate.jpg" alt="Sam Brown" width="500" height="286" /></a>

## Example #3: CSS Transforms, Box Shadow and RGBa

What used to take multiple <code>div</code>s, pngs and extra markup can now be accomplished with a few lines of CSS code. In this example we’ll be combining the transform property from example 2 with <code>box-shadow</code> and RGBa color. To start things off, we’ll create 4 image files, each showing a different version of the Smashing Magazine home page over time with a class for the shadow and a specific class to achieve a variety of rotations.

<a href="https://trentwalton.com/css3/connecting_the_dots/#3"><img loading="lazy" decoding="async" class="45956" title="example_3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b2059e7-7120-4f77-9606-e692034a0d14/example-3.jpg" alt="3" width="500" height="300" /></a>

Here’s the HTML:

<pre><code class="language-markup tmp-xml">&lt;div class="boxes"&gt;
&lt;img class="smash1 shadowed" src="../img/smash1.jpg" alt="2007"/&gt;
&lt;img class="smash2 shadowed" src="../img/smash2.jpg" alt="2008"/&gt;
&lt;img class="smash3 shadowed" src="../img/smash3.jpg" alt="2009"/&gt;
&lt;img class="smash4 shadowed" src="../img/smash4.jpg" alt="2010"/&gt;
&lt;/div&gt;</code></pre>

Let’s set up the CSS for the RGBA Shadow:

<pre><code class="language-css">.shadowed {
border: 3px solid #fff;
-o-box-shadow: 0 3px 4px rgba(0,0,0,.5);
-moz-box-shadow: 0 3px 4px rgba(0,0,0,.5);
-webkit-box-shadow: 0 3px 4px rgba(0,0,0,.5);
box-shadow: 0 3px 4px rgba(0,0,0,.5);
}</code></pre>

Before moving forward, let’s be sure we understand each property here. The <code>box-shadow</code> property works just like any drop shadow. The first two numbers define the shadow’s offset for the X and Y coordinates. Here we’ve set the shadow to 0 for the X, and 3 for the Y. The final number is the shadow blur size, in this case it’s 4px.

RGBa is defined in a similar manner. RGBa stands for red, green, blue, alpha. Here we’ve taken the RGB value for black as 0,0,0 and set it with a 50% alpha level at .5 in the CSS.

Now, let's finish off the effect by adding a little CSS Transform magic to rotate each screenshot:

<pre><code class="language-css">.smash1 { margin-bottom: -125px;
-o-transform: rotate(2.5deg);
-moz-transform: rotate(2.5deg);
-webkit-transform: rotate(2.5deg);
}</code></pre>

<pre><code class="language-css">.smash2 {
-o-transform: rotate(-7deg);
-moz-transform: rotate(-7deg);
-webkit-transform: rotate(-7deg);
}</code></pre>

<pre><code class="language-css">.smash3 {
-o-transform: rotate(2.5deg);
-moz-transform: rotate(2.5deg);
-webkit-transform: rotate(2.5deg);
}</code></pre>

<pre><code class="language-css">.smash4 {
margin-top: -40px;
-o-transform: rotate(-2.5deg);
-moz-transform: rotate(-2.5deg);
-webkit-transform: rotate(-2.5deg);
}</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots/#3">View the live example here</a>

### Examples

Here are a few additional sites with these properties implemented right now:

<a href="https://butterlabel.com">Butter Label</a>
This site is jam packed with well-used CSS3. Notice the <code>transform</code> and <code>box-shadow</code> properties on the subscribe form.

<a href="https://butterlabel.com/"><img loading="lazy" decoding="async" class="45948" title="butter_boxshadow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd7b99c3-be78-4785-a45d-6c0c705ae33f/butter-boxshadow.jpg" alt="Butter Label" width="500" height="300" /></a>

Hope 140
Another site with plenty of CSS3 enhancements, Hope 140’s End Malaria campaign site features a collage of photographs that all have the same shadow &amp; <code>transform</code> properties outlined in our example.

<img loading="lazy" decoding="async" class="45962" title="hope140_boxshadow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8b89b50-2efd-4c93-b514-fb42c88d3562/hope140-boxshadow.jpg" alt="Hope 140" width="500" height="300" />

<a href="https://forabeautifulweb.com">For A Beautiful Web</a>
For A Beautiful Web utilizes RGBa and <code>box-shadow</code> for the overlay video clips boxes linked from their 3 master-class DVDs. While you’re there, be sure to note the transforms paired with the DVD packaging links.

<a href="https://forabeautifulweb.com/"><img loading="lazy" decoding="async" class="45959" title="forabeautifulweb_boxshadow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e368294d-3899-43cd-bea3-a39a2fdc57b9/forabeautifulweb-boxshadow.jpg" alt="For A Beautiful Web" width="500" height="300" /></a>

<a href="https://colly.com/">Simon Collison</a>
Simon Collison has implemented RGBa and <code>box-shadow</code> on each of the thumbnail links for his new website.

<a href="https://colly.com/"><img loading="lazy" decoding="async" class="45996" title="colly" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dc7f488-916b-420d-9bea-b00bf3696374/colly1.png" alt="Colly" width="500" height="300" /></a>

## Example #4: CSS3 Animations

If you really want to push the envelope and truly experiment with the latest CSS3 properties, you’ve got to try creating a CSS3 keyframe animation. As a simple introduction, let’s animate a circle .png image to track the outer edges of a rectangle. To begin, let’s wrap circle.png in a <code>div</code> class:

<pre><code class="language-markup tmp-xml">&lt;div class="circle_motion"&gt;
&lt;img src="/img/circle.png" alt="circle"/&gt;
&lt;/div&gt;</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots/#4"><img loading="lazy" decoding="async" class="45958" title="example_4a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a0088ef-6715-407c-a153-41f2ac8caa4f/example-4a.jpg" alt="4" width="500" height="134" /></a>

The first step in the CSS will be to set the properties for .circle_motion, including giving it an animation name:

<pre><code class="language-css">.circle_motion {
-webkit-animation-name: track;
-webkit-animation-duration: 8s;
-webkit-animation-iteration-count: infinite;
}</code></pre>

Now, all that remains is to declare properties for each percentage-based keyframe. To keep things simple here, I’ve just broken down the 8 second animation into 4 quarters:

<pre><code class="language-css">@-webkit-keyframes track {
0% {
margin-top:0px;
}
25% {
margin-top:150px;
}
50% {
margin-top:150px;
margin-left: 300px;
}
75% {
margin-top:0px;
margin-left: 300px;
}
100% {
margin-left:0px;
}
}</code></pre>

<a href="https://trentwalton.com/css3/connecting_the_dots/#4">View the live example here</a>

### Examples

A few examples of CSS3 animations online now:

Hope 140
Hope 140 subtly animates their yellow “Retweet to Donate $10” button’s box shadow.

<img loading="lazy" decoding="async" class="45961" title="hope_140_animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6f43d7f-e0ec-4850-b520-cd4b90cb5f8d/hope-140-animation.jpg" alt="Hope 140" width="500" height="264" />

<a href="https://hardboiledwebdesign.com">Hardboiled Web Design</a>
Andy Clarke puts iteration count, timing function, duration and delay properties to good use when animating a detective shadow across the background of Hardboiled Web Design.

<a href="https://hardboiledwebdesign.com/"><img loading="lazy" decoding="async" class="45960" title="hbwd_animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19d5edb2-cc7f-4b94-9ebf-1218731e1dbd/hbwd-animation.jpg" alt="Hard Boiled Web Design" width="500" height="300" /></a>

<a href="https://www.optimum7.com/css3-man/animation.html">Optimum7</a>
Anthony Calzadilla has recreated the Spider Man opening credits using CSS3 with JQuery and HTML5. You can also learn more about the process in his article <a href="https://www.optimum7.com/internet-marketing/web-development/pure-css3-spiderman-ipad-cartoon-jquery-html5-no-flash.html">"Pure CSS3 Spiderman Cartoon w/ jQuery and HTML5 – Look Ma, No Flash!"</a>.

<a href="https://www.optimum7.com/css3-man/animation.html"><img loading="lazy" decoding="async" class="45966" title="optimum7_animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26497c1d-348a-404c-a4c1-11295b0a4c24/optimum7-animation.jpg" alt="optimum7_animation" width="500" height="300" /></a>

<a href="https://themanyfacesof.com/four-oh-four/rickman.html">The Many Faces Of...</a>
The Many Faces Of... animates the background position of a <code>div</code> to create an effect where characters creep up from the bottom of the page.

<a href="https://themanyfacesof.com/four-oh-four/rickman.html"><img loading="lazy" decoding="async" class="45972" title="themanyfacesof_animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13200a33-98c1-4be6-97f4-64852c58a73e/themanyfacesof-animation.jpg" alt="The Many Faces Of..." width="500" height="283" /></a>

<a href="https://trentwalton.com/2010/03/22/css3-in-transition/">Trent Walton</a>
I recently wrote a post about CSS3 usage, and animated a blue to green to yellow background image for the masthead.

<a href="https://trentwalton.com/2010/03/22/css3-in-transition/"><img loading="lazy" decoding="async" class="45990" title="cssthree_in_transition" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed1d9e18-aead-4f81-b660-c8bba7be1941/cssthree-in-transition.png" alt="CSS Three In Transition" width="500" height="238" /></a>

## OK, Dots Connected! Now What?

Yes, all of this CSS3 stuff is insanely exciting. If you’re like me, you’ll want to start finding places to use it in the real world immediately. With each new experimental usage come even more concerns about implementation. Here are a few of my ever-evolving opinions about implementing these properties online for your consideration.

*   CSS3 enhancements will never take the place of solid user-experience design.
*   Motion and animation demands attention. Think about a friend waving to get your attention from across a crowded room or a flashing traffic light. Heavy-handed or even moderate uses of animation can significantly degrade user experience. If you are planning on implementing these techniques on a site with any sort of A to B conversion goals, be sure to consider the psychology of motion.
*   Don’t make people wait on animations. Especially when it comes to hover links, be sure there is an immediate state-change cue.
*   Many of these effects can be used in a bonus or easter-egg type of application. Find places to go the extra mile.

This is a group effort. Don’t be afraid of failure, enlist the help of other developers, join the online discussions, and above all, have fun!

## Further Reading

Also consider the following Smashing Magazine articles:

*   [Start Using CSS3 Today: Techniques and Tutorials](https://www.smashingmagazine.com/2010/06/start-using-css3-today-techniques-and-tutorials/)
*   [Why We Should Start Using CSS3 And HTML5 Today](https://www.smashingmagazine.com/2010/12/why-we-should-start-using-css3-and-html5-today/)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)
*   [Using CSS3 Transitions, Transforms and Animation](https://css3.bradshawenterprises.com/) A very extensive and detailed overview of CSS3 techniques for transitions, transforms and animations, with numerous examples.
*   Sexy Interactions with CSS Transitions many of us have never created animations in JavaScript, Flash or some other environment before, and are therefore not as well-versed in the unwritten rules of the animation world. This article explains how to create nice CSS transitions with CSS3.
*   [Examples of CSS3 in the Wild](https://sixrevisions.com/css/examples-of-css3-in-the-wild/) Showcase of sites using CSS3 properties.
*   [CSS3 Transitions – Are We There Yet?](https://samuli.hakoniemi.net/css3-transitions-are-we-there-yet/)
*   [Cross-Browser Animated CSS Transforms — Even in IE.](https://www.useragentman.com/blog/2010/04/05/cross-browser-animated-css-transforms-even-in-ie/)
