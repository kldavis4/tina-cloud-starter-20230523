---
title: 'How To Create Advanced Animations With CSS'
slug: advanced-animations-css
author: yosra-emad
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6ff543a-4e47-4649-8e1d-fda5435d9a53/4-advanced-animations-using-css.png
date: 2022-10-29T12:00:00.000Z
summary: >-
  In this article, Yosra Emad explains how to create a rollercoaster path that a ball follows using cubic beziers and CSS transitions. You’ll also learn how the cubic-bezier function in CSS works in detail and how to stack multiple simple animations to create one complex one.<br /><br /><strong>Note</strong>: This article assumes that you have basic knowledge of CSS animations. If you don’t, please check out <a href="https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/">this guide by Tom Waterhouse</a> before proceeding with the article.
description: >-
  In this article, Yosra Emad explains how to create a rollercoaster path that a ball follows using cubic beziers and CSS transitions. You’ll also learn how the cubic-bezier function in CSS works in detail and how to stack multiple simple animations to create one complex one.
categories:
  - Animation
  - CSS
---

We surf the web daily, and as developers, we tend to notice subtle details on a website. The one thing I take note of all the time is how smooth the animations on a website are. Animation is great for UX and design purposes. You can make an interactive website that pleases the visitor and makes them remember your website.

Creating advanced animations sounds like a hard topic, but the good news is, in CSS, you can stack multiple simple animations after each other to create a more complex one!

In this blog post, you will learn the following:

- What cubic beziers are and how they can be used to create a “complex” animation in just one line of CSS;
- How to stack animations after each other to create an advanced animation;
- How to create a rollercoaster animation by applying the two points you learned above.

**Note**: *This article assumes that you have basic knowledge of CSS animations. If you don’t, please check out [this link](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/) before proceeding with this article.*

## Cubic Beziers: What Are They?

The cubic-bezier function in CSS is an easing function that gives you complete control of how your animation behaves with respect to time. Here is the [official definition](https://www.w3.org/TR/css-easing-1/#cubic-bezier-easing-functions):

<blockquote>A cubic Bézier easing function is a type of <a href="https://www.w3.org/TR/css-easing-1/#easing-function">easing function</a> defined by four real numbers that specify the two control points, <code>P1</code> and <code>P2</code>, of a cubic Bézier curve whose end points <code>P0</code> and <code>P3</code> are fixed at (<code>0</code>, <code>0</code>) and (<code>1</code>, <code>1</code>) respectively. The <code>x</code> coordinates of <code>P1</code> and <code>P2</code> are restricted to the range [<code>0</code>, <code>1</code>].</blockquote>

**Note**: *If you want to learn more about easing functions, you can check out [this article](https://www.smashingmagazine.com/2021/04/easing-functions-css-animations-transitions/). It goes behind the scenes of how linear, cubic-bezier, and staircase functions work!*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edd8b473-78ae-4a1a-9460-d4bd266028f4/6-advanced-animations-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edd8b473-78ae-4a1a-9460-d4bd266028f4/6-advanced-animations-css.png" width="800" height="590" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edd8b473-78ae-4a1a-9460-d4bd266028f4/6-advanced-animations-css.png'>Large preview</a>)" alt="The cubic-bezier function" >}}

## But What Is An Easing Function?

### Let’s Start With A Linear Curve

Imagine two points _P<sub>0</sub>_ and _P<sub>1</sub>_, where _P<sub>0</sub>_ is the starting point of the animation and _P<sub>1</sub>_ is the ending point. Now imagine another point moving linearly between the two points as follows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26898019-0912-4ed4-b01d-8f138601b574/7-advanced-animations-css.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26898019-0912-4ed4-b01d-8f138601b574/7-advanced-animations-css.gif" width="360" height="150" alt="Animation of a linear Bezier curve" /></a><figcaption>Source: <a href="https://en.wikipedia.org/wiki/B%C3%A9zier_curve#Cubic_B%C3%A9zier_curves:~:text=%5Bedit%5D-,Linear,-curves%5Bedit">Wikipedia</a></figcaption></figure>

This is called a linear curve! It is the simplest animation out there, and you probably used it before when you started learning CSS.

### Next Up: The Quadratic Bezier Curve

Imagine you have three points: _P<sub>0</sub>_, _P<sub>1</sub>_ and _P<sub>2</sub>_. You want the animation to move from *P<sub>0</sub>* to *P<sub>2</sub>*. In this case, *P<sub>1</sub>* is a control point that controls the curve of the animation.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1bfb588-f075-4998-80a5-3861eaa2b34f/8-advanced-animations-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1bfb588-f075-4998-80a5-3861eaa2b34f/8-advanced-animations-css.png" width="360" height="150" sizes="100vw" caption="Source: <a href='https://en.wikipedia.org/wiki/B%C3%A9zier_curve#Cubic_B%C3%A9zier_curves:~:text=t%20in%20%5B0%2C1%5D-,Quadratic,-curves%5Bedit'>Wikipedia</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1bfb588-f075-4998-80a5-3861eaa2b34f/8-advanced-animations-css.png'>Large preview</a>)" alt="Construction of a quadratic Bézier curve" >}}

The idea of the quadratic bezier is as follows:

1. Connect imaginary lines between *P<sub>0</sub>* and *P<sub>1</sub>* and between *P<sub>1</sub>* and *P<sub>2</sub>* (represented by the gray lines).
2. Point *Q<sub>0</sub>* moves along the line between *P<sub>0</sub>* and *P<sub>1</sub>*. At the same time, Point *Q<sub>1</sub>* moves along the line between *P<sub>1</sub>* and *P<sub>2</sub>*.
3. Connect an imaginary line between *Q<sub>0</sub>* and *Q<sub>1</sub>* (represented by the green line).
4. At the same time *Q<sub>0</sub>* and *Q<sub>1</sub>* start moving, the point *B* starts moving along the green line. The path that point *B* takes is the animation path.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d3881be-db90-474b-bde1-5dd02e4de1bd/9-advanced-animations-css.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d3881be-db90-474b-bde1-5dd02e4de1bd/9-advanced-animations-css.gif" width="360" height="150" alt="Animation of a quadratic Bézier curve, t in [0,1]" /></a><figcaption>Source: <a href="https://en.wikipedia.org/wiki/B%C3%A9zier_curve#Cubic_B%C3%A9zier_curves:~:text=t%20in%20%5B0%2C1%5D-,Quadratic,-curves%5Bedit">Wikipedia</a></figcaption></figure>

Note that *Q<sub>1</sub>*, *Q<sub>2</sub>* and *B* do not move with the same velocity. They must all start at the same time and finish their path at the same time as well. So each point moves with the appropriate velocity based on the line length it moves along.

### Finally: The Cubic Bezier Curve

The cubic bezier curve consists of 4 points: *P<sub>0</sub>*, *P<sub>1</sub>*, *P<sub>2</sub>* and *P<sub>3</sub>*. The animation starts at *P<sub>0</sub>* and ends at *P<sub>3</sub>*. *P<sub>1</sub>* and *P<sub>2</sub>* are our control points.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9ea13d-2386-4066-a6a6-6bc2303d9f0e/10-advanced-animations-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9ea13d-2386-4066-a6a6-6bc2303d9f0e/10-advanced-animations-css.png" width="360" height="150" sizes="100vw" caption="Source: <a href='https://en.wikipedia.org/wiki/B%C3%A9zier_curve#Cubic_B%C3%A9zier_curves:~:text=t%20in%20%5B0%2C1%5D-,Higher,-%2Dorder%20curves%5B'>Wikipedia</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9ea13d-2386-4066-a6a6-6bc2303d9f0e/10-advanced-animations-css.png'>Large preview</a>)" alt="Construction of a cubic Bézier curve" >}}

The cubic bezier works as follows:

1. Connect imaginary lines between (*P<sub>0</sub>*, *P<sub>1</sub>*), (*P<sub>1</sub>*, *P<sub>2</sub>*) and (*P<sub>2</sub>*, *P<sub>3</sub>*). This is represented by the gray lines.
2. Points *Q<sub>0</sub>*, *Q<sub>1</sub>* and *Q<sub>2</sub>* move along the lines (*P<sub>0</sub>*, *P<sub>1</sub>*), (*P<sub>1</sub>*, *P<sub>2</sub>*) and (*P<sub>2</sub>*, *P<sub>3</sub>*) respectively.
3. Connect imaginary lines between (*Q<sub>0</sub>*, *Q<sub>1</sub>*) and (*Q<sub>1</sub>*, *Q<sub>2</sub>*). They are represented by the green lines.
4. Points *R<sub>0</sub>* and *R<sub>1</sub>* move along the lines (*Q<sub>0</sub>*, *Q<sub>1</sub>*) and (*Q<sub>1</sub>*, *Q<sub>2</sub>*) respectively.
5. Connect the line between *R<sub>0</sub>* and *R<sub>1</sub>* (represented by the blue line).
6. Finally, Point *B* moves along the line connecting between *R<sub>0</sub>* and *R<sub>1</sub>*. This point moves along the path of the animation.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/473e4b21-e920-4501-a959-84f1b8350d14/11-advanced-animations-css.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/473e4b21-e920-4501-a959-84f1b8350d14/11-advanced-animations-css.gif" width="360" height="150" alt="Animation of a cubic Bezier curve, t in [0,1]" /></a><figcaption>Source: <a href="https://en.wikipedia.org/wiki/B%C3%A9zier_curve#Cubic_B%C3%A9zier_curves:~:text=t%20in%20%5B0%2C1%5D-,Higher,-%2Dorder%20curves%5B">Wikipedia</a></figcaption></figure>

If you want to have a better feel for how cubic beziers work, I recommend checking out [this desmos link](https://www.desmos.com/calculator/7arefxmgfb). Play around with the control points and check how the animation changes through time. (Note that the animation in the link is represented by the black line.)

{{% feature-panel %}}

## Stacking Animations

Big animations with lots of steps can be broken down into multiple small animations. You can achieve that by adding the `animation-delay` property to your CSS. Calculating the delay is simple; you add up the time of all the animations before the one you are calculating the animation delay for. 

*For example:*

<pre><code class="language-css">animation: movePointLeft 4s linear forwards, movePointDown 3s linear forwards;
</code></pre>

Here, we have two animations, `movePointLeft` and `movePointDown`. The animation delay for `movePointLeft` will be zero because it is the animation we want to run first. However, the animation delay for `movePointDown` will be four seconds because `movePointLeft` will be done after that time.

Therefore, the `animation-delay` property will be as follows:

<pre><code class="language-css">animation-delay: 0s, 4s;
</code></pre>

Note that if you have two or more animations starting at the same time, their animation delay will be the same. In addition, when you calculate the animation delay for the upcoming animations, you will consider them as one animation.

*For example:*

<pre><code class="language-css">animation: x 4s linear forwards, y 4s linear forwards, jump 2s linear forwards;
</code></pre>

Assume we want to start `x` and `y` simultaneously. In this case, the animation delay for both `x` and `y` will be zero, while the animation delay for the jump animation will be four seconds (not eight!).

<pre><code class="language-css">animation-delay: 0s, 0s, 4s;
</code></pre>

## Creating The Rollercoaster

Now that we have the basics covered, it’s time to apply what we learned!

### Understanding The Animation

The rollercoaster path consists of three parts:

1. The sliding part,
2. The loop part,
3. There will also be some animation to create horizontal space between the two animations above.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d97e9290-b3ee-4aec-8631-0d154f286f72/3-advanced-animations-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d97e9290-b3ee-4aec-8631-0d154f286f72/3-advanced-animations-css.jpg" width="800" height="449" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d97e9290-b3ee-4aec-8631-0d154f286f72/3-advanced-animations-css.jpg'>Large preview</a>)" alt="The rollercoaster path" >}}

### Setting Things Up

We will start by creating a simple ball that will be our “cart” for the rollercoaster. 

1\. Add this to the body of your new HTML file:
 

<pre><code class="language-html">&lt;div id="the-cart" class="cart"&gt;&lt;/div&gt;
</code></pre>
    
2\. Add this to your CSS file:
 

<pre><code class="language-css">.cart {
  background-color: rgb(100, 210, 128);
  height: 50px;
  width: 50px;
  border: 1px solid black;
  border-radius: 50px;
  position: absolute;
  left: 10vw;
  top: 30vh;
}
</code></pre>

I’ll use viewport width (`vw`) and viewport height (`vh`) properties to make the animation responsive. You are free to use any units you want.

### The Sliding Part

Creating the part where the ball slides can be done using the cubic-bezier function! The animation is made up of 2 animations, one along the `x`-axis and the other along the `y`-axis. The `x`-axis animation is a normal linear animation along the `x`-axis. We can define its keyframes as follows:

<pre><code class="language-css">@keyframes x {
  to {
    left: 40vw;
  }
}
</code></pre>

Add it to your animation property in the ball path as follows:

<pre><code class="language-css">animation: x 4s linear forwards
</code></pre>

The `y`-axis animation is the one where we will use the cubic-bezier function. Let’s first define the keyframes of the animation. We want the difference between the starting and ending points to be so small that the ball reaches almost the same height.

<pre><code class="language-css">@keyframes y {
  to {
    top: 29.99vh;
  }
}}
</code></pre>

Now let’s think about the cubic-bezier function. We want our path to move slowly to the right first, and then when it slides, it should go faster.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0284f860-b608-4390-a5bf-991f10ee496c/2-advanced-animations-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0284f860-b608-4390-a5bf-991f10ee496c/2-advanced-animations-css.png" width="800" height="666" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0284f860-b608-4390-a5bf-991f10ee496c/2-advanced-animations-css.png'>Large preview</a>)" alt="The cubic-bezier function" >}}

- Moving slowly to the right means that $P1$ will be along the `x`-axis. So, we know it is at (`V`, `0`).
    - We need to choose a suitable V that makes our animation go slowly to the right but not too much so that it takes up the whole space. In this case, I found that `0.55` fits best.
- To achieve the sliding effect, we need to move `P2` down the `y`-axis (negative value) so `P2=(X, -Y)`.
    - `Y` should be a big value. In this case, I chose `Y=5000`.
    - To get `X`, we know that our animation speed should be faster when sliding and slower when going up again. So, the closer `X` is to zero, The steeper the animation will be at sliding. In this case, let `X = 0.8`.

Now you have your cubic-bezier function, it will be `cubic-bezier(0.55, 0, 0.2, -800)`.

Let’s add keyframes to our animation property:

<pre><code class="language-css">animation: x 4s linear forwards,
    y 4s cubic-bezier(0.55, 0, 0.2, -5000) forwards;
</code></pre>

This is the first part of our animation, so the animation delay is zero. We should add an `animation-delay` property because starting from the following animation, the animations will start at a different time than the first animation.

<pre><code class="language-css">animation-delay: 0s, 0s;
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="VwxXBQb" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Rollercoaster sliding part [forked]](https://codepen.io/smashingmag/pen/VwxXBQb) by <a href="https://codepen.io/yosracodes">Yosra Emad</a>.{{< /codepen >}}

{{% ad-panel-leaderboard %}}

### Adding Horizontal Space

Before making the loop, the ball should move along the `x`-axis for a short while, so there is space between both animations. So, let’s do that!

- Define the keyframes:

<pre><code class="language-css">@keyframes x2 {
  to {
    left: 50vw;
  }
}
</code></pre>

- Add it to the animation property:

<pre><code class="language-css">animation: x 4s linear forwards,
    y 4s cubic-bezier(0.55, 0, 0.2, -5000) forwards, x2 0.5s linear forwards;
</code></pre>

This animation should start after the sliding animation, and the sliding animation takes four seconds; thus, the animation delay will be four seconds:

<pre><code class="language-css">animation-delay: 0s, 0s, 4s;
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="dyemExY" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Rollercoaster horizontal space [forked]](https://codepen.io/smashingmag/pen/dyemExY) by <a href="https://codepen.io/yosracodes">Yosra Emad</a>.{{< /codepen >}}

### The Loop Part

To create a circle (loop) in CSS, we need to move the circle to the center of the loop and start the animation from there. We want the circle’s radius to be `100px`, so we will change the circle position to `top: 20vh` (30 is desired radius (`10vh` here)). However, this needs to happen after the sliding animation is done, so we will create another animation with a zero-second duration and add a suitable animation delay. 

- Create the keyframes:

<pre><code class="language-css">@keyframes pointOfCircle {
  to {
    top: 20vh;
  }
}
</code></pre>

- Add this to the list of animations with duration = `0s`:

<pre><code class="language-css">animation: x 4s linear forwards,
    y 4s cubic-bezier(0.55, 0, 0.2, -5000) forwards, x2 0.5s linear forwards,
    pointOfCircle 0s linear forwards;
</code></pre>

- Add the animation delay, which will be `4.5s`:

<pre><code class="language-css">animation-delay: 0s, 0s, 4s, 4.5s;
</code></pre>

#### The Loop Itself

To create a loop animation:

- Create a keyframe that moves the ball back to the old position and then rotates the ball:

<pre><code class="language-css">@keyframes loop {
  from {
    transform: rotate(0deg) translateY(10vh) rotate(0deg);
  }
  to {
    transform: rotate(-360deg) translateY(10vh) rotate(360deg);
  }
}
</code></pre>

- Add the loop keyframes to the animation property:

<pre><code class="language-css">animation: x 4s linear forwards,
    y 4s cubic-bezier(0.55, 0, 0.2, -5000) forwards, x2 0.5s linear forwards,
    pointOfCircle 0s linear forwards, loop 3s linear forwards;
</code></pre>

- Add the animation delay, which will also be `4.5` seconds here:

<pre><code class="language-css">animation-delay: 0s, 0s, 4s, 4.5s, 4.5s;
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="mdLxZdR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Rollercoaster loop [forked]](https://codepen.io/smashingmag/pen/mdLxZdR) by <a href="https://codepen.io/yosracodes">Yosra Emad</a>.{{< /codepen >}}

### Adding Horizontal Space (Again)

We’re almost done! We just need to move the ball after the animation along the `x`-axis so that the ball doesn’t stop exactly after the loop the way it does in the picture above.

- Add the keyframes:

<pre><code class="language-css">@keyframes x3 {
  to {
    left: 70vw;
  }
}
</code></pre>

- Add the keyframes to the animation property:

<pre><code class="language-css">animation: x 4s linear forwards,
    y 4s cubic-bezier(0.55, 0, 0.2, -800) forwards, x2 0.5s linear forwards,
    pointOfCircle 0s linear forwards, loop 3s linear forwards,
    x3 2s linear forwards;
</code></pre>

- Adding the suitable delay, here it will be `7.5s`:

<pre><code class="language-css">animation-delay: 0s, 0s, 4s, 4.5s, 4.5s, 7.5s;
</code></pre>

{{% ad-panel-leaderboard %}}

## The Final Output

{{< codepen height="480" theme_id="light" slug_hash="wvjmLKp" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Rollercoaster Final [forked]](https://codepen.io/smashingmag/pen/wvjmLKp) by <a href="https://codepen.io/yosracodes">Yosra Emad</a>.{{< /codepen >}}

## Conclusion

In this article, we covered how to combine multiple keyframes to create a complex animation path. We also covered cubic beziers and how to use them to create your own easing function. I would recommend going on and creating your own animation path to get your hands dirty with animations. If you need any help or want to give feedback, you’re more than welcome to send a message to any of the [links here](https://yosracodes.bio.link/). Have a wonderful day/night!

{{< signature "vf, il, yk" >}}
