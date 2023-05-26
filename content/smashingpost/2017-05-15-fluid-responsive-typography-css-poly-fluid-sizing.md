---
title: Fluid Responsive Typography With CSS Poly Fluid Sizing
slug: fluid-responsive-typography-css-poly-fluid-sizing
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/002f35b9-e7a6-4774-a03a-5a1ea1d4c957/poly-fluid-sizing-opt.png
date: 2017-05-15T20:24:42.000Z
author: jake-wilson
summary: >-
  In this article, we are going to examine how to create scalable, fluid typography across multiple breakpoints and predefined font sizes using well-supported browser features and some basic algebra. The best part is that you can automate it all by using Sass.
description: >-
  In this article, we are going to examine how to create scalable, fluid typography across multiple breakpoints and predefined font sizes using well-supported browser features and some basic algebra. The best part is that you can automate it all by using Sass.
categories:
  - Coding
  - Typography
  - CSS
  - Responsive Design
  - Sass
---

Fluid layouts have been a normal part of front-end development for years. The idea of fluid typography, however, is relatively new and has yet to be fully explored. Up until now, most developers’ idea of fluid typography is simply using Viewport units maybe with some minimum and maximum sizes.

When working with creative designers on web page designs, it’s fairly common to receive multiple Sketch or Photoshop artboards/layouts, one for each breakpoint. In that design, elements (like an <code>h1</code> heading) will usually be different sizes at each breakpoint. For example:

1.  The `h1` at the small layout could be `22px`
2.  The `h1` at the medium layout could be `24px`
3.  The `h1` at the large layout could be `34px`

The bare minimum CSS for this uses <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries">media queries</a>:

<pre><code class="language-css">h1 {
  font-size: 22px;
}
@media (min-width:576px) {
  h1 {
    font-size: 22px;
  }
}
@media (min-width:768px) {
  h1 {
    font-size: 24px;
  }
}
@media (min-width:992px) {
  h1 {
    font-size: 34px;
  }
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8187a6f2-0c66-4b6f-81eb-81ed1309f4b7/media-query-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8187a6f2-0c66-4b6f-81eb-81ed1309f4b7/media-query-opt.gif" alt="" width="“780&quot;" height="112" /></a></figure>

This is a good first step, but you are limiting the <code>font-size</code> to only what was specified by the designer at the provided breakpoints. What would the designer say if you asked, "What should the <code>font-size</code> be at an 850px wide viewport?" The answer in most cases is that it would be somewhere between 24px and 34px. But right now, it's just 24px according to your CSS, which is probably not what the designer was envisioning.

Your option at this point is to calculate what that size should be and add another breakpoint. That's easy enough. But what about all the other resolutions? What should the <code>font-size</code> be at 800px wide? What about 900px? What about 935px? Obviously the designer is not going to provide you with a full layout for every single possible resolution. Even if they did, should you be adding dozens (or hundreds) of breakpoints for all the different <code>font-sizes</code> that are desired by the designer? Of course not.

Your layout is already fluidly scaling with the width of your viewport. Wouldn't it be nice if your typography predictably scaled with your fluid layout? What else can we do to improve upon this?

## Viewport Units To The Rescue?

<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/length#Viewport-percentage_lengths">Viewport units</a> are another step in the right direction. They allow your text to fluidly resize with your layouts. And the <a href="https://caniuse.com/#search=viewport">browser support</a> is great these days.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8384025b-c4de-4c39-a62d-d5bafb94e02a/1-can-i-use-viewports-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8384025b-c4de-4c39-a62d-d5bafb94e02a/1-can-i-use-viewports-opt.png" alt="Can I Use Viewport?" width="800" height="485" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8384025b-c4de-4c39-a62d-d5bafb94e02a/1-can-i-use-viewports-opt.png">View large version</a>)</figcaption></figure>

<em>But</em> the viability of Viewport units is <em>very dependent</em> on the original creative designs for a web page. It would be great to just set your <code>font-size</code> using <code>vw</code> and be done:

<pre><code class="language-css">h1 {
  font-size: 2vw;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e5e3137-b25f-43ad-8031-79faef7893de/viewport-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e5e3137-b25f-43ad-8031-79faef7893de/viewport-opt.gif" alt="" width="“780&quot;" height="112" /></a></figure>

But this only works if your creative art-boards take this into account. Did the designer choose a text size that was exactly 2% of the width of each of his art-boards? Of course not. Let’s calculate what the <code>vw</code> value would need to be for each of our breakpoints:

<blockquote><code>22px</code> size @ <code>576px</code> wide = 22/576&#42;100 = 3.82vw<br /><br /><code>24px</code> size @ <code>768px</code> wide = 24/768&#42;100 = 3.13vw<br /><br /><code>34px</code> size @ <code>992px</code> wide = 34/992&#42;100 = 3.43vw</blockquote>

They are close but they aren’t all the same. So you would still need to use media queries to transition between text sizes and there would still be jumps. And consider this weird side-effect:

@ 767px, 3.82% of the viewport width is 29px. If the viewport is 1-pixel wider the <code>font-size</code> sudden <strong>drops back down to 24px</strong>. This animation of a viewport being resized demonstrates this undesirable side effect:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb4c0d06-fd03-4889-bf4f-b9bec3b8abf7/viewport-2-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb4c0d06-fd03-4889-bf4f-b9bec3b8abf7/viewport-2-opt.gif" alt="" width="“780&quot;" height="112" /></a></figure>

This dramatic change in font-size is almost definitely not what the designer was envisioning. So how do we solve this problem?

{{% feature-panel %}}

## Statistical Linear Regression?

Wait. What? Yes, this is an article about CSS, but some basic math can go a long way towards an elegant solution to our problem.

First, lets plot our resolutions and corresponding text sizes on a graph:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dedb9d7f-0ca9-4639-bdfe-145430df3987/2-scatter-plot-font-size-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dedb9d7f-0ca9-4639-bdfe-145430df3987/2-scatter-plot-font-size-opt.png" alt="Scatter plot of font-size and corresponding Viewport width" width="800" height="495" /></a><figcaption>Scatter plot of <code>font-size</code> and corresponding Viewport width (Google Spreadsheets) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dedb9d7f-0ca9-4639-bdfe-145430df3987/2-scatter-plot-font-size-opt.png">View large version</a>)</figcaption></figure>

Here you can see a scatter plot of the designer’s specified text sizes at the defined viewport widths. The x-axis is the viewport width and the y-axis is the <code>font-size</code>. See that line? That’s called a <em>trendline</em>. It’s a way to find an interpolated <code>font-size</code> value for any viewport width, based on the data provided.</p>

### The Trendline Is The Key To All Of This

If you could set your <code>font-size</code> according to this trendline, you would have an h1 that smoothly scales on all resolutions that would <em>come close</em> to matching what the designer intended. First, let’s look at the math. The straight line is defined by this equation:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/689e4050-ee83-4107-aa88-07d6ec7eb9ca/3-linear-equation-definition-opt.png" alt="Linear equation definition" width="299" height="80" /><figcaption>Linear equation definition</figcaption></figure>

*   m = slope
*   b = the y-intercept
*   x = the current viewport width
*   y = the resulting `font-size`

The are several methods for determining the slope and y-intercept. When multiple values are involved, a common method is the <a href="https://en.wikipedia.org/wiki/Least_squares">Least Squares</a> fit:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed5908ea-66fa-46d6-9772-1cfb6d5023db/4-least-squares-fit-opt.png" alt="Least Squares" width="800" height="237" /></figure>

Once you run those calculations, you have your trendline equation.

## How Do I Use This In CSS?

Okay, this is getting pretty heavy on the math. How do we actually use this stuff in front-end web development? The answer is CSS <code>calc()</code>! Once again, a fairly new CSS technology that is <a href="https://caniuse.com/#search=calc">very well supported</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64aae50d-c84d-45fd-8150-88c79fbb2d91/5-can-i-use-calc-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64aae50d-c84d-45fd-8150-88c79fbb2d91/5-can-i-use-calc-opt.png" alt="Can I Use Calc?" width="800" height="495" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64aae50d-c84d-45fd-8150-88c79fbb2d91/5-can-i-use-calc-opt.png">View large version</a>)</figcaption></figure>

You can use the trendline equation like this:

<pre><code class="language-css">h1 {
  font-size: calc({slope}*100vw + {y-intercept}px);
}</code></pre>

Once you find your slope and y-intercept you just plug them in!

<strong>Note:</strong> You have to multiply the slope by <code>100</code> since you are using it as a <code>vw</code> unit which is 1/100th of the Viewport width.</p>

## Can This Be Automated?

I ported the least squares fit method into an easy-to-use Sass function:

<pre><code class="language-sass">/// least-squares-fit
/// Calculate the least square fit linear regression of provided values
/// @param {map} $map - A Sass map of viewport width and size value combinations
/// @return Linear equation as a calc() function
/// @example
///   font-size: least-squares-fit((576px: 24px, 768px: 24px, 992px: 34px));
/// @author Jake Wilson &lt;jake.e.wilson@gmail.com&gt;
@function least-squares-fit($map) {

  // Get the number of provided breakpoints
  $length: length(map-keys($map));

  // Error if the number of breakpoints is &lt; 2
  @if ($length &lt; 2) {
    @error "leastSquaresFit() $map must be at least 2 values"
  }

  // Calculate the Means
  $resTotal: 0;
  $valueTotal: 0;
  @each $res, $value in $map {
    $resTotal: $resTotal + $res;
    $valueTotal: $valueTotal + $value;
  }
  $resMean: $resTotal/$length;
  $valueMean: $valueTotal/$length;

  // Calculate some other stuff
  $multipliedDiff: 0;
  $squaredDiff: 0;
  @each $res, $value in $map {

    // Differences from means
    $resDiff: $res - $resMean;
    $valueDiff: $value - $valueMean;

    // Sum of multiplied differences
    $multipliedDiff: $multipliedDiff + ($resDiff * $valueDiff);

    // Sum of squared resolution differences
    $squaredDiff: $squaredDiff + ($resDiff * $resDiff);
  }

  // Calculate the Slope
  $m: $multipliedDiff / $squaredDiff;

  // Calculate the Y-Intercept
  $b: $valueMean - ($m * $resMean);

  // Return the CSS calc equation
  @return calc(#{$m*100}vw + #{$b});

}</code></pre>

Does this really work? <a href="https://codepen.io/jakobud/pen/LyZJRB">Open up this CodePen</a> and resize your browser window. It works! The font sizes are fairly close to what the original design was asking for and they smoothly scale with your layout.

{{< codepen height="265" theme_id="0" slug_hash="LyZJRB" data-default-tab="result" >}} Least Squares Fit SCSS test user="jakobud"]See the Pen <a href="https://codepen.io/jakobud/pen/LyZJRB">Least Squares Fit SCSS test</a> by Jake Wilson (<a href="https://codepen.io/jakobud">@jakobud</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

Now, admittedly, it’s not perfect. The values are close to the original design but they do not quite match up. This is because a linear trendline is an <strong>approximation</strong> of specific font sizes at specific viewport widths. This is inherit of linear regression. There is always some error in your results. It’s a trade-off of simplicity vs. accuracy. Also, keep in mind, the more varied your text sizes are, the more error there will be in your trendline.

Can we do better than this?

{{% ad-panel-leaderboard %}}

## Polynomial Least Squares Fit

In order to get a more accurate trendline, you need to look at more advanced topics, like a <a href="https://en.wikipedia.org/wiki/Polynomial_regression">polynomial regression</a> trendline that might look something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78c3ff8f-9e29-4941-ac77-bef4c1c38b4a/6-polynomial-regression-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78c3ff8f-9e29-4941-ac77-bef4c1c38b4a/6-polynomial-regression-opt.png" alt="Polynomial regression trendline" width="800" height="504" /></a><figcaption>Polynomial regression trendline (Google Spreadsheets) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78c3ff8f-9e29-4941-ac77-bef4c1c38b4a/6-polynomial-regression-opt.png">View large version</a>)</figcaption></figure>

Now <em>that</em> is more like it! Much more accurate than our straight line. A basic polynomial regression equation looks like this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd117aad-9533-4306-84f7-a9145d615c1e/7-polynomial-equation-opt.png" alt="A 3rd degree polynomial equation" width="587" height="125" /><figcaption>A 3rd degree polynomial equation</figcaption></figure>

The more accurate you want your curve, the more complicated the equation gets. <strong>Unfortunately, you can’t do this in CSS</strong>. <code>calc()</code> simply cannot do this type of advanced math. Specifically, you can’t calculate exponents:

<pre><code class="language-css">font-size: calc(3vw * 3vw); /* This doesn’t work in CSS */</code></pre>

So until <code>calc()</code> supports this type of non-linear math, we are stuck with <strong>linear equations only</strong>. Is there anything else we can do to improve upon this?

## Breakpoints And Multiple Linear Equations

What if we were only calculating a straight line between each pair of breakpoints? Something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b46bf77-d0c2-4418-a663-a6747067af39/8-linear-regression-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b46bf77-d0c2-4418-a663-a6747067af39/8-linear-regression-opt.png" alt="Linear Regression trendlines between multiple pairs of values" width="800" height="495" /></a><figcaption>Linear Regression trendlines between multiple pairs of values (Google Spreadsheets) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b46bf77-d0c2-4418-a663-a6747067af39/8-linear-regression-opt.png">View large version</a>)</figcaption></figure>

So in this example we would calculate the straight line between <code>22px</code> and <code>24px</code> and then another between <code>24px</code> and <code>34px</code>. The Sass would look like this:

<pre><code class="language-sass">// SCSS
h1 {
  @media (min-width:576px) {
    font-size: calc(???);
  }
  @media (min-width:768px) {
    font-size: calc(???);
  }
}</code></pre>

We could use the least squares fit method for those <code>calc()</code> values but since it’s just a straight line between 2 points, the math could be greatly simplified. Remember the equation for a straight line?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10ccf73-ba92-4479-991a-8574657bd39c/9-linear-equation-opt.png" alt="Linear equation definition" width="299" height="80" /><figcaption>Linear equation definition</figcaption></figure>

Since we are talking about just 2 points now, finding the slope (m) and y-intercept (b) is trivial:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5757003d-bd4e-4981-a10d-973c2c1e235a/10-slope-linear-equation-opt.png" alt=" Finding the slope and y-intercept of a linear equation" width="701" height="167" /><figcaption>Finding the slope and y-intercept of a linear equation</figcaption></figure>

Here is a Sass function for this:

<pre><code class="language-sass">/// linear-interpolation
/// Calculate the definition of a line between two points
/// @param $map - A Sass map of viewport widths and size value pairs
/// @returns A linear equation as a calc() function
/// @example
///   font-size: linear-interpolation((320px: 18px, 768px: 26px));
/// @author Jake Wilson &lt;jake.e.wilson@gmail.com&gt;
@function linear-interpolation($map) {
  $keys: map-keys($map);
  @if (length($keys) != 2) {
    @error "linear-interpolation() $map must be exactly 2 values";
  }
  // The slope
  $m: (map-get($map, nth($keys, 2)) - map-get($map, nth($keys, 1)))/(nth($keys, 2) - nth($keys,1));

  // The y-intercept
  $b: map-get($map, nth($keys, 1)) - $m * nth($keys, 1);

  // Determine if the sign should be positive or negative
  $sign: "+";
  @if ($b &lt; 0) {
    $sign: "-";
    $b: abs($b);
  }

  @return calc(#{$m*100}vw #{$sign} #{$b});
}</code></pre>

Now, just use the linear interpolation function on multiple breakpoints in your Sass. Also, lets throw in some min and max <code>font-sizes</code>:

<pre><code class="language-sass">// SCSS
h1 {
  // Minimum font-size
  font-size: 22px;
  // Font-size between 576 - 768
  @media (min-width:576px) {
    $map: (576px: 22px, 768px: 24px);
    font-size: linear-interpolation($map);
  }
  // Font-size between 768 - 992
  @media (min-width:768px) {
    $map: (768px: 24px, 992px: 34px);
    font-size: linear-interpolation($map);
  }
  // Maximum font-size
  @media (min-width:992px) {
    font-size: 34px;
  }
}</code></pre>

And it generates this CSS:

<pre><code class="language-css">h1 {
  font-size: 22px;
}
@media (min-width: 576px) {
  h1 {
    font-size: calc(1.04166667vw + 16px);
  }
}
@media (min-width: 768px) {
  h1 {
    font-size: calc(4.46428571vw - 10.28571429px);
  }
}
@media (min-width: 992px) {
  h1 {
    font-size: 34px;
  }
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb80427-9a0f-47a1-99a6-292990d281d5/holy-grail-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb80427-9a0f-47a1-99a6-292990d281d5/holy-grail-opt.gif" alt="" width="“780&quot;" height="112" /></a></figure>

## The Holy Grail Of CSS Sizing?

Lets wrap this all up in a nice Sass mixin (for the lazy and efficient!). I’m coining this method <em>Poly Fluid Sizing</em>:

<pre><code class="language-sass">/// poly-fluid-sizing
/// Generate linear interpolated size values through multiple break points
/// @param $property - A string CSS property name
/// @param $map - A Sass map of viewport unit and size value pairs
/// @requires function linear-interpolation
/// @requires function map-sort
/// @example
///   @include poly-fluid-sizing('font-size', (576px: 22px, 768px: 24px, 992px: 34px));
/// @author Jake Wilson &lt;jake.e.wilson@gmail.com&gt;
@mixin poly-fluid-sizing($property, $map) {
  // Get the number of provided breakpoints
  $length: length(map-keys($map));

  // Error if the number of breakpoints is &lt; 2
  @if ($length &lt; 2) {
    @error "poly-fluid-sizing() $map requires at least values"
  }

  // Sort the map by viewport width (key)
  $map: map-sort($map);
  $keys: map-keys($map);

  // Minimum size
  #{$property}: map-get($map, nth($keys,1));

  // Interpolated size through breakpoints
  @for $i from 1 through ($length - 1) {
    @media (min-width:nth($keys,$i)) {
      $value1: map-get($map, nth($keys,$i));
      $value2: map-get($map, nth($keys,($i + 1)));
      // If values are not equal, perform linear interpolation
      @if ($value1 != $value2) {
        #{$property}: linear-interpolation((nth($keys,$i): $value1, nth($keys,($i+1)): $value2));
      } @else {
        #{$property}: $value1;
      }
    }
  }

  // Maxmimum size
  @media (min-width:nth($keys,$length)) {
    #{$property}: map-get($map, nth($keys,$length));
  }
}</code></pre>

This Sass mixin requires a few Sass functions in the following Github gists:

*   [linear-interpolation](https://gist.github.com/Jakobud/7414f91142e0f540f221a3e3cafdf856)
*   [map-sort](https://gist.github.com/Jakobud/a0ac11e80a1de453cd86f0d3fc0a1410)
*   [list-sort](https://gist.github.com/Jakobud/744b98b629abe018766f6d506a2e92ae)
*   [list-remove](https://gist.github.com/Jakobud/ec056b52f3673cc369dc97f2c2428424)

The <code>poly-fluid-sizing()</code> mixin will perform linear interpolation on each pair of viewport widths and set a minimum and maximum size. You can import this into any Sass project and easily utilize it without needing to know any of the math behind it. Here is the final <a href="https://codepen.io/jakobud/pen/vmKLYb">CodePen</a> that uses this method.

{{< codepen height="265" theme_id="0" slug_hash="vmKLYb" data-default-tab="result" caption="Poly Fluid Sizing using linear equations, viewport units and calc()" >}} Poly Fluid Sizing using linear equations, viewport units and calc() user="jakobud"]See the Pen <a href="https://codepen.io/jakobud/pen/vmKLYb">Poly Fluid Sizing using linear equations, viewport units and calc()"] Poly Fluid Sizing using linear equations, viewport units and calc()</a> by Jake Wilson (<a href="https://codepen.io/jakobud">@jakobud</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

{{% ad-panel-leaderboard %}}

## A Few Notes

*   Obviously this method applies not only to `font-size` but to any unit/length property (`margin`, `padding`, etc). You pass the desired property name into the mixin as a string.
*   The Sass map of viewport width + size value pairs can be passed **in any order** into the `poly-fluid-sizing()` mixin. _It will automatically sort the map according to Viewport width from lowest to highest_. So you could pass in a map like this and it would work out just fine:

<pre><code class="language-sass">  $map: (576px: 22px, 320px: 18px, 992px: 34px, 768px: 24px);
  @include poly-fluid-sizing('font-size', $map);
</code></pre>

*   A limitation for this method is that you cannot pass in mixed units into the mixin. For example, `3em` @ `576px` width. Sass just won’t really know what to do mathematically there.</p>

## Conclusion

Is this the best we can do? Is Poly Fluid Sizing the Holy Grail of fluid unit sizing in CSS? Maybe. CSS currently supports non-linear <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function">animation</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function">transition</a> timing functions, so maybe <a href="https://i0.kym-cdn.com/photos/images/newsfeed/000/840/283/350.png">there is a chance</a> that <code>calc()</code> will also support it someday. If that happens, non-linear, polynomial regression might be worth a look again. But maybe not… Linear scaling might be superior anyways.</p>

<a href="https://stackoverflow.com/questions/42014594/linear-scaling-between-2-font-sizes-using-calc-and-vw">I began exploring this idea</a> in early 2017 and eventually developed the above solution. Since then, I’ve seen a few dev’s come up with similar ideas and different pieces of this puzzle. I thought it was time for me to share my method and how I got there. Viewport units. Calc(). Sass. Breakpoints. None of these things are new. They are all browser features that have existing for years (with varying degrees of support). I've only used them together in a way that hadn't been fully explored yet. Don't ever be afraid to look at the tools you use every day and think out-of-the-box on how you can utilize them better and grow your skill set.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)
*   [Typographic Patterns In HTML Email Newsletter Design](https://www.smashingmagazine.com/2015/08/typographic-patterns-in-html-newsletter-email-design/)
*   [The Good, The Bad And The Great Examples Of Web Typography](https://www.smashingmagazine.com/2014/12/the-good-the-bad-and-the-great-examples-of-web-typography/)
*   [Tools And Resources For A More Meaningful Web Typography](https://www.smashingmagazine.com/2016/03/meaningful-web-typography/)

{{< signature "vf, il" >}}
