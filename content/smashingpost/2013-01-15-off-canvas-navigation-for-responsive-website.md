---
title: How To Implement Off-Canvas Navigation For A Responsive Website
slug: off-canvas-navigation-for-responsive-website
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bda1e68-eaf3-437d-a07a-c1d8a6eded94/demo-1-5001.png'
date: 2013-01-15T16:42:49.000Z
author: david-bushell
description: >-
  The varying viewports that our websites encounter on a daily basis continue to
  demand more from responsive design. Not only must we continue to tackle the
  issues of content choreography — the art of maintaining order and context
  throughout the chaotic ebb and flow of the Web browser — but we must also
  **meet the expectations of users**.
categories:
  - Coding
  - Techniques
  - Navigation
  - Responsive Design
---
The varying viewports that our websites encounter on a daily basis continue to demand more from responsive design. Not only must we continue to tackle the issues of <a title="Content Choreography" href="https://trentwalton.com/2011/07/14/content-choreography/">content choreography</a> — the art of maintaining order and context throughout the chaotic ebb and flow of the Web browser — but we must also <strong>meet the expectations of users</strong>. They’re not sitting still.

With the likes of <a title="Firefox OS" href="https://www.mozilla.org/en-US/firefoxos/">Firefox OS</a> (Boot to Gecko), <a title="Chrome OS" href="https://www.google.com/intl/en/chrome/devices/">Chrome OS</a> and now <a title="Ubuntu for phones" href="https://www.ubuntu.com/devices/phone">Ubuntu for phones</a> — an OS that makes “Web apps” first-class citizens — delivering native app-like experiences on the Web may become a necessity if users begin to expect it. Many in our field have argued for a degree of separation between the Web and native platforms for both technical and philosophical reasons. They’re certainly wise to heed caution, but as consumer devices continue to blur the boundaries, it’s worth thinking about what we can learn from native app design.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Exploring The Potential Of The Off-Canvas Pattern](https://www.smashingmagazine.com/2014/02/off-the-beaten-canvas-exploring-the-potential-of-the-off-canvas-pattern/)
*   [When Off-Canvas Isn’t Good Enough](https://www.smashingmagazine.com/2016/05/smart-responsive-design-patterns-or-when-off-canvas-isnt-good-enough/)
*   [How To Keep Framework Development Simple And Bug-Free](https://www.smashingmagazine.com/2015/03/simple-real-and-bug-free-foundation-development/)
*   [<span class="headline">A Simple JavaScript Plugin For Responsive Navigation</span>](https://www.smashingmagazine.com/2013/04/javascript-plugin-for-responsive-navigation/)

## A Demonstration

In this article, I’ll be walking through a build demo that centers on two topics. The first is <a href="https://bradfrost.github.com/this-is-responsive/patterns.html">responsive design patterns</a> that embrace the viewport and that improve content discoverability beyond the basic hyperlink; in this case, <strong>off-canvas navigation</strong>. The second is the complexities of implementing such ideas in an accessible and highly performant manner. These are two topics that I believe are at the heart of the Web’s future.

{{% feature-panel %}}

With that in mind, let’s get building.</p>

## The Accessible Base

All good things begin with a solid foundation of semantic HTML and widely supported CSS. In theory, this baseline should function as a usable experience for all browsers that visit our website. (It might also be the <em>final</em> experience in less-capable browsers.)

As a starting point, I’ll use a technique very similar to Aaron Gustafson’s <a href="https://www.creativebloq.com/css3/build-smart-mobile-navigation-without-hacks-6122800">Smart Mobile Navigation Without Hacks</a>. It requires no JavaScript to function.

<a title="Demo 1" href="https://dbushell.github.com/Responsive-Off-Canvas-Menu/step1.html"><img loading="lazy" decoding="async" class="123973" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28a4bd4f-42d8-4db0-bfbd-e3e3515a9c4c/demo-1-500.png" alt="Responsive Off-Canvas Menu Demo 1" width="500" height="371" /></a><br>
<em>Step 1 of the responsive off-canvas menu. Short link: <a href="https://bit.ly/offcanvas1">bit.ly/offcanvas1</a></em>

*   **[View demo 1](https://dbushell.github.com/Responsive-Off-Canvas-Menu/step1.html "Demo 1")** Be sure to view on a mobile or small screen, and take a while to inspect the code. Although our final design will be significantly different, starting simple is vital; retrofitting accessibility isn’t trivial.

The HTML body looks like this (I’ve stripped a few attributes for semantic clarity):

<pre><code class="language-markup tmp-xml">&lt;header id="top" role="banner"&gt;
    &lt;h1&gt;Book Title&lt;/h1&gt;
    &lt;a href="#nav"&gt;Book navigation&lt;/a&gt;
&lt;/header&gt;
&lt;nav id="nav" role="navigation"&gt;
    &lt;h2&gt;Chapters&lt;/h2&gt;
    &lt;ul&gt;
        &lt;li&gt;&lt;a href="#"&gt;Chapter 1&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#"&gt;Chapter 2&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#"&gt;Chapter 3&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#"&gt;Chapter 4&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#"&gt;Chapter 5&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
    &lt;a href="#top"&gt;Return to content&lt;/a&gt;
&lt;/nav&gt;
&lt;article role="main"&gt;
    &lt;!-- [main content here] --&gt;
&lt;/article&gt;</code></pre>

You could consider the HTML alone, with little to no styling, as being “breakpoint zero.” If it’s not logical at this stage, then accessibility will not improve.</p>

### Demo 1 Breakdown

*   Media queries are based on a viewport width of `45em` (that’s content-dependent). Above this breakpoint, the navigation is permanently visible. I prefer em units because they allow breakpoints to maintain a relationship with text size. Lyza Gardner explains in detail in her post “[The EMs Have It: Proportional Media Queries FTW!](https://blog.cloudfour.com/the-ems-have-it-proportional-media-queries-ftw/ "The EMs have it: Proportional Media Queries FTW!")”
*   I’m using both `min-width` and `max-width` media queries to scope CSS. This adds a bit of complexity. Most people prefer a “mobile-first” build, using only progressively larger `min-width` queries. The downside with that technique is the amount of **resetting** required if an element has noticeably different visual states. Neither method is right or wrong.
*   The crux of this initial stage is the [:target pseudo-class](https://developer.mozilla.org/en-US/docs/Using_the_:target_selector "Using the :target selector - MDN") selector, utilized to show and hide the navigation. Only IE8 and lower lack support. However, this is a non-issue if you serve a semi-fluid desktop style sheet to old IEs. [Jake Archibald](https://jakearchibald.github.com/sass-ie/ "Writing mobile-first styles without leaving IE9 and lower behind"), [Nicolas Gallagher](https://nicolasgallagher.com/mobile-first-css-sass-and-ie/ "“Mobile first” CSS and getting Sass to help with legacy IE") and [Stuart Robson](https://www.alwaystwisted.com/post.php?s=2012-08-06-a-sass-mixin-for-media-queries-and-ie "A Sass mixin for media queries and IE") can tell you more.

As the demo takes shape, I’ll continue to introduce the main development principles. There’s a long way to go yet…

## Going Off-Canvas

For some websites, the above may suffice — but not for us! We’re experimenting with off-canvas patterns and striving for that native experience. Because we cannot ignore older browsers, it’s now time to <strong>progressively enhance</strong>.

<a href="https://dbushell.github.com/Responsive-Off-Canvas-Menu/step2.html"><img loading="lazy" decoding="async" class="123989" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/812550f5-0570-48cb-991d-7cbee7cb40f5/demo-2.png" alt="Responsive Off-Canvas Menu Demo 2" /></a><br>
<em>Step 2 of the responsive off-canvas menu. Short link: <a href="https://bit.ly/offcanvas2">bit.ly/offcanvas2</a></em>

*   **[View demo 2](https://dbushell.github.com/Responsive-Off-Canvas-Menu/step2.html "Demo 2")** You will see the restyled navigation with basic functionality.</p>

### Demo 2 Breakdown

*   I’m adding the class `js-ready` to the document element after the [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Mozilla_event_reference/DOMContentLoaded_(event) "DOMContentLoaded") event fires. The selector `.js-ready` is used as a hook to safely restyle the navigation off-canvas. If for whatever reason JavaScript _doesn’t_ load, then the original functionality from demo 1 still exists.
*   To show and hide the navigation, I’m toggling a class of `js-nav` on the document element when the user clicks (or taps) the relevant buttons. This simply applies a style of `left: 70%` to the `#inner-wrap` element (`#outer-wrap` is used to hide any overflow and to avoid scrollbars).

This is a fairly basic enhancement, but importantly it remains usable before JavaScript is ready. It’s also notable that no inline styles are written with JavaScript; only classes are used to manage states.

Jumping between open and closed navigation states makes for a jarring user experience. Users need to understand — or even <em>see</em> — how an interface has changed. This is often the point where developers let the Web down. To be fair, building user interfaces is incredibly difficult. What I’m going to show below is far from perfect, but it’s certainly a step in the right direction.

So, we have the set-up. Now let’s add transitions.</p>

## Transitioning (The Wrong Way)

I’ll start by getting it all wrong, because this is how I would have done it a few years ago, and learning from mistakes is important.

<a href="https://dbushell.github.com/Responsive-Off-Canvas-Menu/step3-jquery.html"><img loading="lazy" decoding="async" class="124008" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b52440b7-ba6b-4098-ac95-44d787163f85/demo-jquery.png" alt="Responsive Off-Canvas Menu Demo 3 (jQuery)" /></a><br>
<em>The responsive off-canvas menu using jQuery <code>.animate</code> for transitions. Short link: <a href="https://bit.ly/offcanvas3">bit.ly/offcanvas3</a></em>

jQuery is a resource that many front-end developers begin with to learn JavaScript. Personally, I am a big fan (never blame the tools), but unfortunately jQuery has a habit of making things look deceptively simple. It masks complexity and, with that, <em>understanding</em>.

Transitioning our off-canvas navigation with jQuery is very easy:

<pre><code class="language-javascript">$('#nav-open-btn').on('click', function() {
    $('#inner-wrap').animate({ left: '70%' }, 500);
});

$('#nav-close-btn').on('click', function() {
    $('#inner-wrap').animate({ left: '0' }, 500);
});</code></pre>

Visually, this achieves the effect we’re after, but test it on mobile and watch the frame rate stutter. Performance is dreadful.

This method is bad for several reasons:

<img loading="lazy" decoding="async" class="124094" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aeb2feae-a427-4626-af93-43579c68df85/jquery-animate.gif" alt="An animation of jQuery updating the DOM" width="456" height="32" />

*   jQuery’s `.animate` increments the element’s `style` attribute on every animation frame (as can be seen in the GIF above). This forces the browser to [recalculate the layout](https://developers.google.com/speed/articles/reflow "Minimizing browser reflow").
*   It leaves inline styles in the DOM that have very **high specificity** and that will override our well-maintained CSS. This is a big issue if the viewport is resized and triggers different breakpoints.
*   A **separation of concerns** is lost because styles are defined in JavaScript files.

Overall, it’s a performance and maintainability nightmare. There is a better way.

## Transitioning With CSS

Putting the jQuery experiment aside, I’m now building from the second demo again, this time using <strong>CSS transforms and transitions</strong>. These enable us to smoothly animate the off-canvas navigation with great performance.

<a href="https://dbushell.github.com/Responsive-Off-Canvas-Menu/step4.html"><img loading="lazy" decoding="async" class="124042" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d2726d2-eb46-4a2c-af31-3ae989985600/demo-final1.png" alt="Responsive Off-Canvas Menu Demo 4" /></a><br>
<em>The final responsive off-canvas menu using CSS transforms and transitions. Short link: <a href="https://bit.ly/offcanvas4">bit.ly/offcanvas4</a></em>

*   **[View final demo](https://dbushell.github.com/Responsive-Off-Canvas-Menu/step4.html "View Final Demo")** Performance has drastically improved compared to the jQuery example.</p>

### Final Demo Breakdown

*   Returning to CSS, I’m once again using the `.js-nav` class to toggle the navigation, while making no actual style alterations with JavaScript.
*   I’m progressively enhancing with the classes `.csstransforms3d` and `.csstransitions` (applied to the document element by [Modernizr](https://modernizr.com/ "Modernizr")).
*   Instead of moving the navigation with negative positioning (`left: -100%`), I’m using the `transform` property: `transform: translate3d(-100%, 0, 0)`.
*   CSS transitions are used to animate `transform` changes: `transition: transform 500ms ease`. And I’ve added a few more transforms to enhance the visual effect.

With the help of Modernizr, this will fall back to <a title="Demo 2" href="https://dbushell.github.com/Responsive-Off-Canvas-Menu/step2.html">demo 2</a> if browser support is lacking for CSS transforms and transitions. (In theory, I could fall back to jQuery animation, but it’s really not worth it.) When you <a title="Download Modernizr" href="https://modernizr.com/download/">download Modernizr</a>, you can include only the feature detection that you need. It also includes the HTML5 shiv for IE. All in all, it’s a very useful script.

The benefits here are immense. First and foremost, by transitioning elements with 3-D transforms, the browser can generate render layers that are <a title="Let’s Play With Hardware-Accelerated CSS" href="https://www.smashingmagazine.com/2012/06/21/play-with-hardware-accelerated-css/">hardware-accelerated</a>. Secondly, there’s no need for JavaScript to worry about style or media-query breakpoints. JavaScript need only interpret user interaction and apply classes to maintain states — CSS defines the visual changes.

We can look deeper into performance by using Chrome’s Developer Tools. The results below are from the desktop browser, but for mobile performance you could use <a title="Remote Debugging" href="https://developers.google.com/chrome/mobile/docs/debugging">USB Remote Debugging</a> on Android devices.</p>

### jQuery Animation Performance

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea953dbd-f7ce-4614-adb8-65fdde17ba34/demo-perf-jquery.png"><img loading="lazy" decoding="async" class="124133" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea953dbd-f7ce-4614-adb8-65fdde17ba34/demo-perf-jquery.png" alt="jQuery animation performance in Chrome Developer Tools" /></a>

The four events above represent the opening and closing of the navigation twice. In the diagram, yellow represents the JavaScript running, purple is the rendering (recalculating the style and layout), and green is the painting to the screen. On mobile, we’d be shooting way below that 30 FPS line. I also tested on an iPhone 3GS and could literally count 3 FPS with my own eyes — it’s that slow!

### CSS Transition Performance

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e7b412c-6415-4754-b9af-64c9fb013cb4/demo-perf-css.png"><img loading="lazy" decoding="async" class="124134" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e7b412c-6415-4754-b9af-64c9fb013cb4/demo-perf-css.png" alt="CSS transition performance in Chrome Developer Tools" /></a>

What a difference! The only JavaScript that exists is there to manage user interaction before and after the transition. The green we’re seeing is the minimum that the browser needs to repaint the transition at a respectable frame rate, using <a title="GPU Animation: Doing It Right" href="https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/">GPU acceleration</a>.</p>

### Possible Concerns

As with all new Web standards, nothing is inherently perfect.

In WebKit-based browsers, the <a title="Font Smoothing" href="https://www.usabilitypost.com/2012/11/05/stop-fixing-font-smoothing/">font smoothing</a> may switch to antialiased from the default subpixel-antialiased when CSS transforms or transitions are applied. This could result in visually thinner text, which many designers actually prefer — but <a title="Please Stop Fixing Font Smoothing" href="https://www.usabilitypost.com/2012/11/05/stop-fixing-font-smoothing/">not something you should “fix.”</a>

Flickering can also occur if an element goes between transform and no-transform. To avoid this, always start with a default like <code>translate3d(0,0,0)</code> on an element that will move later, so that the render layer is composed and ready.</p>

## The Next Step

Enhancing further, we could detect and take advantage of touch gestures, like swiping, to really bring this implementation closer to par with its native counterparts — “closer” being the operative word, but I do believe the gap is closer than many would have us believe.

It’s also — in my opinion — a gap that we <em>need</em> to bridge.

There are other clever ways to increase interaction speed. Mobile browsers tend to wait around 300 ms to fire click events.

<a title="CSS Transitions - timing function" href="https://www.w3.org/TR/css3-transitions/#transition-timing-function-property">Transition easing</a> can radically change the visual effect and the user’s perception of what’s happening. Whether elements need to spring, bounce or accelerate into action, Lea Verou has a useful <a title="Cubic Bezier" href="https://cubic-bezier.com/">cubic bezier</a> resource to generate custom easing functions.

Hopefully, this article has shown the improvements that can be made if we take extra care to understand the technology we’re using.</p>

### Download The Code

So, there we have it: a three-tiered responsive, interactive, off-canvas menu. I’ve set up a <a title="Responsive Off-Canvas Menu code repository on GitHub" href="https://github.com/dbushell/Responsive-Off-Canvas-Menu">GitHub repository</a> where you can view all the code. Have a play with it; there are a few bits and pieces I haven’t covered to avoid bloating this article.</p>

### Further Reading

To really understand why the techniques highlighted above are my preferred solution, I point you in the direction of these resources:

*   “[All You Need to Know About CSS Transitions](https://blog.alexmaccaw.com/css-transitions "All you need to know about CSS Transitions"),” _Alex MacCaw_ MacCaw gets into the specifics of CSS transitions and JavaScript.
*   “[Why Moving Elements With translate() Is Better Than pos:abs top/left](https://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/ "Why moving elements with translate() is better than pos:abs top/left"),” _Paul Irish_ A superb video and article examining the different movement techniques.
*   “[Improving the Performance of Your HTML5 App](https://www.html5rocks.com/en/tutorials/speed/html5/ "Improving the Performance of your HTML5 App"),” _Malte Ubl_ Looks deep into the intricacies of performance.
*   “[CSS3 vs jQuery Animations](https://dev.opera.com/articles/view/css3-vs-jquery-animations/ "CSS3 vs jQuery Animations"),” _Siddharth Rao_ This article puts both methods head to head.
*   “[Understanding Hardware Acceleration on Mobile Browsers](https://conferences.oreilly.com/velocity/velocity2012/public/schedule/detail/23298 "Understanding Hardware Acceleration on Mobile Browsers"),” _Ariya Hidayat_ Goes under the hood with a technical review.
*   “[Scrolling Performance](https://www.html5rocks.com/en/tutorials/speed/scrolling/ "Scrolling Performance"),” _Paul Lewis_ Looks at a related scenario.

{{< signature "al" >}}

