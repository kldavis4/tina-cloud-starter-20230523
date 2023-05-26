---
title: Develop A One-Of-A-Kind CSS / JS-Based Game Portfolio
slug: develop-a-one-of-a-kind-cssjs-based-game-portfolio
image: null
date: 2012-05-28T09:03:25.000Z
author: daniel-sternlicht
description: >-
  A portfolio is a must-have for any designer or developer who wants to stake
  their claim on the Web. It should be as unique as possible, and with a bit of
  HTML, CSS and JavaScript, you could have a one-of-a-kind portfolio that
  capably represents you to potential clients.
categories:
  - Coding
  - CSS
  - JavaScript
  - HTML
---
A portfolio is a must-have for any designer or developer who wants to stake their claim on the Web. It should be as unique as possible, and with a bit of HTML, CSS and JavaScript, you could have a one-of-a-kind portfolio that capably represents you to potential clients. In this article, I’ll show you how I created my 2-D Web-based game portfolio.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4de27900-6ef5-46a0-9dc1-cbb0faddbc49/1.png" alt="Daniel Sternlicht Portfolio." width="500" /><br>
<em>The 2-D Web-based game portfolio of <a href="https://danielsternlicht.com">Daniel Sternlicht</a>.</em>

Before getting down to business, let’s talk about portfolios.

A portfolio is a great tool for Web designers and developers to show off their skills. As with any project, spend some time learning to develop a portfolio and doing a little research on what's going on in the Web design industry, so that the portfolio presents you as an up to date, innovative and inspiring person. All the while, keep in mind that going with the flow isn’t necessarily the best way to stand out from the crowd.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/10/design-your-own-mobile-game/#further-reading-on-smashingmag)

*   [Building “Topple Trump”, An Interactive Web-Based Quiz Game](https://www.smashingmagazine.com/2016/10/building-topple-trump-an-interactive-web-based-quiz-game-case-study/)
*   [What Web Designers Can Learn From Video Games](https://www.smashingmagazine.com/2011/07/what-web-designers-can-learn-from-video-games/)
*   [Email Marketing For Mobile App Creators](https://www.smashingmagazine.com/2013/08/email-marketing-for-mobile-app-creators/)
*   [How To Build A SpriteKit Game In Swift 3](https://www.smashingmagazine.com/2016/11/how-to-build-a-spritekit-game-in-swift-3-part-1/)

{{% feature-panel %}}

One last thing before we dive into the mystery of my Web-based game portfolio. I use jQuery which has made my life much easier by speeding up development and keeping my code clean and simple.

Now, let’s get our hands dirty with some code.</p>

## The HTML

Let’s warm up with a quick overview of some very basic HTML code. It’s a bit long, I know, but let’s take it step by step.

<pre><code class="language-markup tmp-html">&lt;div id="wrapper"&gt;

    &lt;hgroup id="myInfo"&gt;
        &lt;h1&gt;DANIEL STERNLICHT&lt;/h1&gt;
        &lt;h2&gt;Web Designer, Front-End Developer&lt;/h2&gt;
    &lt;/hgroup&gt;

    &lt;div id="startCave" class="cave"&gt;&lt;/div&gt;
    &lt;div id="startCaveHole" class="caveHole"&gt;&lt;/div&gt;

    &lt;div id="mainRoad" class="road"&gt;&lt;/div&gt;
    &lt;div id="leftFence"&gt;&lt;/div&gt;
    &lt;div id="rightFence"&gt;&lt;/div&gt;

    &lt;div id="daniel"&gt;&lt;/div&gt;

    &lt;div id="aboutRoad" class="road side"&gt;&lt;/div&gt;
    &lt;div id="aboutHouse" class="house"&gt;
        &lt;div class="door"&gt;&lt;/div&gt;
        &lt;div class=”lightbox”&gt;…&lt;/div&gt;
    &lt;/div&gt;
    &lt;div id="aboutSign" class="sign"&gt;
        &lt;span&gt;About Me&lt;/span&gt;
    &lt;/div&gt;

    …

    …

    &lt;div id="rightTrees" class="trees"&gt;&lt;/div&gt;
    &lt;div id="leftGrass" class="grass"&gt;&lt;/div&gt;

    &lt;div id="endSea" class="sea"&gt;&lt;/div&gt;
    &lt;div id="endBridge" class="bridge"&gt;&lt;/div&gt;

    &lt;div id="boat" class="isMoored"&gt;
        &lt;div class="meSail"&gt;&lt;/div&gt;
    &lt;/div&gt;

&lt;/div&gt;</code></pre>

The HTML is not very complicated, and I could have used an <a href="https://sixrevisions.com/html/canvas-element/">HTML5 canvas</a> element for this game, but I felt more comfortable using simple HTML DOM elements.

Basically, we have the main <code>#wrapper</code> div, which contains the game’s elements, most of which are represented as div elements (I chose divs because they are easy to manipulate).

Have a <a href="https://danielsternlicht.com">quick look at my game</a>. Can you detect what makes up the game view?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c388f64-e05c-470e-9791-04cc3c4309d7/2.png" alt="The game view" width="500" /><br>
<em>The game view</em>

We have roads, trees, fences, water, caves, houses and so on.

Back to our HTML. You’ll find an element for each of these items, with the relevant class and ID. Which brings us to the CSS.</p>

## The CSS

First of all, note that I prepared the HTML to follow the principles of <a href="https://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/">object-oriented CSS</a> by determining global classes for styling, and not using IDs as styling hooks. For example, I used the class <code>.road</code> on each element that should look like a road. The CSS for the <code>.road</code> class would be:

<pre><code class="language-css">.road {
   position: absolute;
   background: url(images/road.png) repeat;
}</code></pre>

Take trees as another example:

<pre><code class="language-css">.trees {
   position: absolute;
   background: url(images/tree.png) repeat 0 0;
}</code></pre>

Note that almost all of the elements are absolutely positioned on the game’s canvas. Positioning the elements relatively would be impossible for our purposes, especially because we want the game to be as <strong>responsive</strong> as possible (within limits, of course — the minimum width that I deal with is 640 pixels). We can write a general rule giving all of the DOM elements in the game an absolute position:

<pre><code class="language-css">#wrapper * {
   position: absolute;
}</code></pre>

This snippet will handle all of the child elements inside the <code>#wrapper</code> div, and it frees us from having to repeat code.

One more word about the CSS. The animations in the game are done with <strong>CSS3 transitions and animations</strong>, excluding certain features such the lightboxes and player “teleporting.” There are two reasons for this.

The first is that one of the purposes of this portfolio is to demonstrate innovation and up-to-date development, and what’s more innovative than using the power of CSS3?

The second reason is performance. Upon reading Richard Bradshaw’s very interesting article “<a href="https://css3.bradshawenterprises.com/">Using CSS3 Transitions, Transforms and Animation</a>,” I came to the overwhelming conclusion: <strong>use CSS3 when you can</strong>.

A great example of the power of CSS3 animations in my portfolio is the pattern of movement of the water. The CSS looks like this:

<pre><code class="language-css">.sea {
   left: 0;
   width: 100%;
   height: 800px;
   background: url(images/sea.png) repeat 0 0;
   -webkit-animation: seamove 6s linear infinite;   /* Webkit support */
   -moz-animation: seamove 6s linear infinite;      /* Firefox support */
   animation: seamove 6s linear infinite;          /* Future browsers support */
}</code></pre>

And here is the code for the animation itself:

<pre><code class="language-css">/* Webkit support */
@-webkit-keyframes seamove {
   0% {
      background-position: 0 0;
   }
   100% {
      background-position: 65px 0;
   }
}

@-moz-keyframes seamove {…}   /* Firefox support */
@-keyframes seamove {…}       /* Future browsers support */</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30e40aa2-b7fe-4d66-9c35-739a20462491/3.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30e40aa2-b7fe-4d66-9c35-739a20462491/3.png" alt="Sea.png" width="500" /></a><br>
<em>The sea PNG is marked out.</em>

The repeating <code>sea.png</code> image is 65 pixels wide, so to give the sea a waving effect, we should move it by the same number of pixels. Because the background is repeating, it gives us the effect we want.

Another cool example of CSS3 animations happens when the player steps into the boat and sails off the screen.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60e41e10-88d4-45f8-88f0-6a62fe7032ad/4.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60e41e10-88d4-45f8-88f0-6a62fe7032ad/4.png" alt="Boat sails" width="500" /></a><br>
<em>The boat sails off the screen, revealing the “Contact” section.</em>

If the player gets back onto the road, you’ll notice that the boat moves in “reverse,” back to its original position. It sounds complicated, but you have no idea how easy it is with CSS3 transitions. All I did was capture the event with JavaScript to determine whether the user is “on board.” If the user is, then we add the class <code>.sail</code> to the boat element, which make it sail off; otherwise, we withhold this class. At the same time, we add a <code>.show</code> class to the <code>#contact</code> wrapper, which smoothly reveals the contact form in the water. The CSS of the boat looks like this:

<pre><code class="language-css">#boat {
   position: absolute;
   bottom: 500px;
   left: 50%;
   margin-left: -210px;
   width: 420px;
   height: 194px;
   background: url(images/boat.png) no-repeat center;
   -webkit-transition: all 5s linear 1.5s;
   -moz-transition: all 5s linear 1.5s;
   transition: all 5s linear 1.5s;
}</code></pre>

When we add the class <code>.sail</code> to it, all I’m doing is changing its <code>left</code> property.

<pre><code class="language-css">#boat.sail {
   left: -20%;
}</code></pre>

The same goes for the <code>#contact</code> wrapper with the class <code>.show</code>. Except here, I’m playing with the <code>opacity</code> property:

<pre><code class="language-css">#contact.show {
   opacity: 1;
}</code></pre>

CSS3 transitions do the rest of the work.

## The JavaScript

Because we are dealing with a <strong>2-D game</strong>, we might want to base it on a JavaScript game engine, perhaps an existing framework. But the thing about frameworks (excluding jQuery, which I’m using as a base) is that they are usually good for a head start, but they probably won’t fit your needs in the long run.

A good example is the lightboxes in my portfolio, which provide information about me and are activated when the user enters a house.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f50fc977-9123-4dc6-b533-4dfadaa31c3b/5.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f50fc977-9123-4dc6-b533-4dfadaa31c3b/5.png" alt="An example of a lightbox in the game" width="500" /></a><br>
<em>An example of a lightbox in the game. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f50fc977-9123-4dc6-b533-4dfadaa31c3b/5.png">Large image</a>)</em>

This kind of functionality doesn’t exist in a regular JavaScript game engine. You could always improve an existing framework with your own code, but diving into someone else’s code sometimes takes longer than writing your own. Moreover, if you rewrite someone else’s code, it could become a problem when a new version is released.

After passing over libraries such as <a href="https://craftyjs.com/">Crafty</a>, <a href="https://www.limejs.com/">LimeJS</a> and <a href="https://impactjs.com/">Impact</a>, which really are great game engine frameworks, I felt I had no choice but to build my own engine to fit my needs.

Let’s quickly review the main methods that I’m running in the game.

To handle the keyboard arrow events, I use the following code:

<pre><code class="language-javascript">$(window).unbind('keydown').bind('keydown', function(event) {
    switch (event.keyCode) {
        event.preventDefault();
        case 37: // Move Left
            me.moveX(me.leftPos - 5, 'left');
        break;

        case 39: // Move Right
            me.moveX(me.leftPos + 5, 'right');
        break;

        case 38: // Move Up
            me.moveY(me.topPos - 5, 'up');
        break;

        case 40: // Move Down
            me.moveY(me.topPos + 5, 'down');
        break;
    }
});</code></pre>

As you can see, the code is very simple. When the user presses the up or down arrow, I call the <code>moveY()</code> function, and when they press right or left, I call <code>moveX()</code>.

A quick peek at one of them reveals all the magic:

<pre><code class="language-javascript">moveX: function(x, dir) {
    var player = this.player;
    var canMove = this.canImove(x, null);
    if(canMove){
        this.leftPos = x;
        player.animate({'left': x + 'px'}, 10);
    }
    if(dir == 'left') {
        this.startMoving('left', 2);
    }
    else {
        this.startMoving('right', 3);
    }
}</code></pre>

At each step the player takes, I check with a special method named <code>canImove()</code> (i.e. “Can I move?”) to determine whether the character may move over the game canvas. This method include screen boundaries, house positions, road limits and so on, and it gets two variables, including the x and y coordinates of where I want the player to move to. In our example, if I wanted the player to move left, I’d pass to the method their current left position plus 5 pixels. If I wanted them to move right, I’d pass its current position minus 5 pixels.

If the character “can move,” I return <code>true</code>, and the character keeps moving; or else, I return <code>false</code>, and the character remains in their current position.

Note that in the <code>moveX()</code> method, I’m also checking the direction in which the user wants to go, and then I call a method named <code>startMoving()</code>:

<pre><code class="language-javascript">if(dir == 'left') {
   this.startMoving('left', 2);
}
else {
   this.startMoving('right', 3);
}</code></pre>

You’re probably wondering how the walking effect on the character is achieved. You might have noticed that I’m using CSS sprites. But how do I activate them? It’s actually quite simple, with the help of a jQuery plugin called <a href="https://www.spritely.net/">Spritely</a>. This amazing plugin enables you to animate CSS sprites simply by calling the method on the relevant element and passing it your properties (such as the number of frames).

Back to our <code>startMoving()</code> method:

<pre><code class="language-javascript">startMoving: function(dir, state) {
   player.addClass(dir);
   player.sprite({fps: 9, no_of_frames: 3}).spState(state);
}</code></pre>

I simply add a direction class to the player element (which sets the relevant sprite image), and then call the <code>sprite()</code> method from Spritely’s API.

Because we are dealing with the Web, I figured that being able to move with the keyboard arrows would not be enough. You always have to think of the user, your client, who might not have time to hang out in your world. That is why I added both a navigation bar and an option to “teleport” the character to a given point in the game — again, using the <code>canImove()</code> method to check whether the player may move to this point.

Next we’ve got the lightboxes. Recall what the HTML looks like for each house:

<pre><code class="language-markup tmp-html">&lt;div id="aboutHouse" class="house"&gt;
   &lt;div class="door"&gt;&lt;/div&gt;
   &lt;div class="lightbox"&gt;
      &lt;div class="inner about"&gt;
         Lightbox content goes here…
      &lt;/div&gt;
   &lt;/div&gt;
&lt;/div&gt;</code></pre>

Did you notice the <code>.lightbox</code> class in the <code>house</code> div? We will use it later. What I basically did was define a “hot spot” for each house. When the player gets to one of those hot spots, the JavaScript activates the <code>lightboxInit(elm)</code> method, which also gets the relevant house’s ID. This method is very simple:

<pre><code class="language-javascript">lightboxInit:  function(elm) {
   // Get the relevant content
   var content = $(elm).find('.lightbox').html();

   // Create the lightbox
   $('&lt;div id="dark"&gt;&lt;/div&gt;').appendTo('body').fadeIn();
   $('&lt;div id="lightbox"&gt;' + content + '&lt;span id="closeLB"&gt;x&lt;/span&gt;&lt;/div&gt;').insertAfter("#dark").delay(1000).fadeIn();
}</code></pre>

First, I get the relevant content by finding the <code>div.lightbox</code> child of the house element. Then, I create and fade in a blank div, named <code>dark</code>, which gives me the dark background. Finally, I create another div, fill it up with the content (which I had already stored in a variable), and insert it right after the dark background. Clicking the “x” will call another method that fades out the lightbox and removes it from the DOM.

One good practice that I unfortunately learned the hard way is to <strong>keep the code as dynamic as possible</strong>. Write your code in such a way that if you add more content to the portfolio in future, the code will support it.</p>

## Conclusion

As you can see, developing a 2-D Web-based game is fun and not too complicated a task at all. But before rushing to develop your own game portfolio, consider that it doesn’t suit everyone. If your users don’t have any idea what HTML5 is or why IE 5.5 isn’t the “best browser ever,” then your effort will be a waste of time, and perhaps this kind of portfolio would alienate them. Which is bad.

Nevertheless, I learned a lot from this development process and I highly recommend, whatever kind of portfolio you choose, that you invest a few days in developing your <em>own</em> one of a kind portfolio.

{{< signature "al" >}}

