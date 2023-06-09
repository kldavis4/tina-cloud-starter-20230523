---
title: 'Accessible SVGs: Inclusiveness Beyond Patterns'
slug: accessible-svgs-inclusiveness-beyond-patterns
author: carie-fisher
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242a8d07-b985-4d37-85fc-ec5ca598d094/accessible-svgs-inclusiveness-beyond-patterns.png
date: 2020-03-12T11:30:00.000Z
summary: >-
  We are fortunate to have robust patterns to choose from when optimizing accessibility in SVGs &mdash; but most people stop there, focusing on code compliance and not actual users and their needs. If true inclusiveness lies beyond patterns &mdash; what other factors should we consider when designing and developing accessible SVGs?
description: >-
  We are fortunate to have robust patterns to choose from when optimizing accessibility in SVGs &mdash; but most people stop there, focusing on code compliance and not actual users and their needs. If true inclusiveness lies beyond patterns &mdash; what other factors should we consider when designing and developing accessible SVGs?
categories:
  - SVG
  - Accessibility
---

<p>Scalable Vector Graphics (SVGs) became a <a href="https://en.wikipedia.org/wiki/Scalable_Vector_Graphics">W3C open standard</a> in 1999 &mdash; back when the new tech hotness was the Blackberry phone, Napster first invaded college dorms, and the Y2K bug sparked fear in us all. Fast forward to our modern digital world and you’ll notice that while the other tech trends have waned, SVGs are still around and thriving.</p>

<p>This is partly due to SVGs having a small footprint for such high visual fidelity, in a world where bandwidth and performance matter more than ever &mdash; especially on mobile devices and situations/locations where data is at a premium. But also because SVGs are so flexible with their integrated styles, interactivity, and animation options. What we can do with SVGs today goes way beyond the basic shapes of yesteryear.</p>

<p>If we focus on the accessibility aspect of SVGs, we have come a long way as well. Today, we have many robust patterns and techniques to help us optimize inclusiveness. This is true regardless if you are <a href="https://www.sarasoueidan.com/blog/accessible-icon-buttons">creating icons</a>, <a href="https://www.scottohara.me/blog/2019/05/22/contextual-images-svgs-and-a11y.html">simple images</a>, or more <a href="https://cariefisher.com/a11y-svg">complex images</a>.</p>

<p>While the specific pattern you decide to use might vary depending on your particular situation and targeted <a href="https://www.w3.org/WAI/standards-guidelines/wcag/">WCAG conformance level</a> &mdash; the reality is, most people stop there, focusing on code compliance and not actual end-users and their needs. If true inclusiveness lies beyond patterns &mdash; what other factors should we consider when designing and developing accessible SVGs?</p>

<div class="c-felix-the-cat">
<h4 class="h3">Styling And Animating SVGs With CSS</h4>
<p>Why is it so important to optimize your SVGs? Also, why even put in the effort to make them accessible? Sara Soueidan explais why and also how to style and animate with CSS. <a href="https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

## SVG Color And Contrast

<p>The primary focus of accessible SVGs is screen readers compliance &mdash; which is only part of the issue and part of the solution. Globally, people with low-vision and color blindness outnumber the people who are blind 14:1. We are talking a staggering 546 million in total (<a href="https://www.who.int/blindness/publications/globaldata/en/">246 million</a> low-vision users plus <a href="https://www.colourblindawareness.org/colour-blindness/">300 million</a> colorblind users) vs. <a href="https://en.wikipedia.org/wiki/Visual_impairment">39 million</a> users who are legally blind. Many people with low-vision and colorblindness do not rely on screen readers, but may instead use tools like <a href="https://www.bbc.co.uk/accessibility/guides/text_larger/">browser resizing</a>, <a href="https://www.sawtoothsoftware.com/help/lighthouse-studio/manual/custom-css.html">customized stylesheets</a>, or <a href="https://www.zoomtext.com/">magnification software</a> to help them see what is on the screen. To these 546 million people, screen reader output is probably not as important to them as making sure the color and contrast is great enough that they can see the SVG on the screen &mdash; but how do we go about checking for this?</p>

### Tools And Checks

<p>The very first step you should take when designing your SVG color palette is to review the <a href="https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html">WCAG color contrast ratio guidelines</a>. While SVGs and other icons were exempt from color contrast ratio requirements not too long ago (when targeting WCAG AA compliance), the recent update to the <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1">WCAG 2.1 guidelines</a> have made it so all <em>essential</em> non-text imagery must adhere to a contrast ratio of at least 3:1 against adjacent colors. By essential, it means if your SVG was to vanish, would it fundamentally change the information or functionality of the content? If you can answer “no,” then you are likely exempt from this guideline. If you can answer “yes” or “maybe,” then you need to make sure your SVG color contrast ratios are in check.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bc21535-5a87-4b26-968f-af28bc5982c5/accessible-svgs-housedemo.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bc21535-5a87-4b26-968f-af28bc5982c5/accessible-svgs-housedemo.png" sizes="100vw" caption="House icon used in demo with light outline vs dark outline &mdash; which is more accessible? (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bc21535-5a87-4b26-968f-af28bc5982c5/accessible-svgs-housedemo.png'>Large preview</a>)" alt="House icon used in demo with light outline vs dark outline" >}}

<p>One example of an essential non-text image is an SVG icon used as a CTA button or link &mdash; such as we see in this home button. In this SVG, we see a line drawing of a house with no visual text. When we look into the code, we see the text “Home” in a span with a class called "sr-only" (screen reader only) on it. This class, along with the related CSS, hides the span text from sighted users, but not from AT users <em>(this is just one example of an accessible image/graphic pattern)</em>.</p>

<p>This is a good first step, but choosing the correct SVG pattern is one piece of the puzzle &mdash; another piece is the color contrast between the icon and its background. Going back to the example, at first glance it seems like both SVGs could be accessible. Yet, when using a color contrast tool and testing the house icon against its background, we see the first SVG fails compliance with a color contrast ratio of 2:1 between the stroke (<code>#8f8f8f</code>) and the background (<code>#cccccc</code>), while the second SVG passes with a color contrast ratio of 3:1 between the stroke (<code>#717171</code>) and the background (<code>#cccccc</code>). By using the same accessible pattern, but taking an extra step and changing the stroke color to something a bit darker, we made our SVG more inclusive to a wider range of abilities.</p>

<p>To check for accessible color contrast ratios, there are many tools available for use. For a quick color contrast spot check, you could use the <a href="https://webdesign.tutsplus.com/articles/how-to-use-the-contrast-checker-in-chrome-devtools--cms-31504">Contrast Checker in Chrome DevTools</a>. For checking color contrast on non-coded designs, check out the <a href="https://developer.paciellogroup.com/resources/contrastanalyser/">Colour Contrast Analyser</a> tool. And for a full-color palette review, <a href="https://a11yrocks.com/colorPalette/">A11y Color Palette</a> is a great way to help you see which color combinations are the most accessible. Of course, make sure you try out a few of the tools and pick whatever works best for you and your team &mdash; the best tool is the one you actually use.</p>

{{% feature-panel %}}

### Light/Dark Mode

<p>Beyond checking for color contrast ratios, you should also consider the increasingly popular and supported media query called <a href="https://drafts.csswg.org/mediaqueries-5/#descdef-media-prefers-color-scheme"><code>@prefers-color-scheme</code></a> that allows a user to choose a light or dark themed version of the website or app they are visiting. While this media query <em>does not</em> replace checking for color contrast ratios, it can give your users more choice when it comes to the overall experience of your website or app.</p>

{{% pull-quote %}}
 Allowing your users to choose their experience is always better than assuming you know what they want.
{{% /pull-quote %}}

<p>As with other media queries, to see the light/dark theme changes, the website or app developer must add additional code targeting the query. Going back to the house icon example from earlier, you can see in the following code that the SVG’s stroke, fill, and background colors are controlled by the CSS. Since these style elements are externally controlled and not hard-coded in the SVG markup, we can add a few extra lines of CSS to make the SVG work in a dark theme.</p>

#### Light/default mode:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59294282-a3a4-4964-9bfe-486303349c5c/2-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5157ac6c-0f02-4aff-a2c2-cb56ee129730/housedemo2-whitespace.png" sizes="70vw" caption="House icon used in demo with a light background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59294282-a3a4-4964-9bfe-486303349c5c/2-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="House icon used in demo with a light background" >}}

<pre><code class="language-css">body {
  background: #cccccc;
}

.nav-home1 {
  stroke: #8f8f8f;
}

.nav-home2 {
  stroke: #717171;
}

#home-svg1,
#home-svg2 {
  fill: #64b700;
}

#home-door-svg1,
#home-door-svg2 {
  fill: #b426ff;
}
</code></pre>

#### Dark mode:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bcc36ea-77ab-4cba-a024-f328b6c2f17f/1-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cd29687-9403-434a-8213-fbb058345dae/housedemodark-whitespace.png" sizes="70vw" caption="House icon used in demo with a dark background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bcc36ea-77ab-4cba-a024-f328b6c2f17f/1-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="House icon used in demo with a dark background" >}}

<pre><code class="language-css">@media (prefers-color-scheme: dark) {

  body {
    background: #333333;
  }

  .nav-home1 {
    stroke: #606060;
  }

  .nav-home2 {
    stroke: #7C7C7C;
  }
}</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="MWwQpze" default_tab="result" user="smashingmag" editable="true" breakout="true"  data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/MWwQpze/">Light/Dark mode with SVGs</a> by <a href="https://codepen.io/cariefisher">Carie Fisher</a>.{{< /codepen >}}

<p>As this example shows, setting up your designs to use CSS to control style elements means that creating a dark theme version of your SVG can be relatively simple. Conversely, if you have hard-coded styles into the SVG markup, you may need to reimagine your SVG in a way that allows CSS to have more control over the design. Or you may want to consider creating a completely new dark version of your SVG and swap out the light version when the theme preferences change. Just remember, if you do plan to show/hide different images based on the user mode, you also need to <a href="https://www.w3.org/WAI/tutorials/images/decorative/">hide the nonvisible SVG from AT users</a>!</p>

<p><em><strong>Note:</strong> in this particular example, the default theme was already light so it made sense to also make that the default experience and build a dark theme for an alternate experience. Otherwise, if we started with a dark theme, we could have done the opposite making the dark theme the default experience and using <code>@media (prefers-color-scheme: light)</code> to create a light theme.</em></p>

<p>In the next example, we are looking at a more complex SVG with both light and dark mode versions via the <code>@prefers-color-scheme</code> media query. Our friend Karma Chameleon (in SVG form) has both a dark theme and a light/default theme. By changing your light/dark preference settings (<a href="https://support.apple.com/en-us/HT208976">Mac OS</a> + <a href="https://www.howtogeek.com/222614/how-to-enable-windows-10s-hidden-dark-theme/">Win OS</a> dark mode settings) and navigating to a browser that supports <code>@prefers-color-scheme</code> media query, you can see the environment change. In the light/default mode, Karma Chameleon is sitting on a branch in a green forest surrounded by a fluttering red butterfly. In dark mode, she is sitting on a branch in space with a blue rocket zooming past. In both environments, her colors automatically change and her eyes move around.</p>

{{< codepen height="480" theme_id="light" slug_hash="rNVJyoj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Light/Dark mode + reduced motion with SVGs (Karma Chameleon)](https://codepen.io/smashingmag/pen/rNVJyoj) by <a href="https://codepen.io/cariefisher">Carie Fisher</a>.{{< /codepen >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3516e299-ec62-44b7-a8fd-5290d0a78699/10-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3516e299-ec62-44b7-a8fd-5290d0a78699/10-accessible-svgs-inclusiveness-beyond-patterns.png" sizes="100vw" caption="Karma Chameleon in light mode. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3516e299-ec62-44b7-a8fd-5290d0a78699/10-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="In the light/default mode, Karma Chameleon is sitting on a branch in a green forest surrounded by a fluttering red butterfly. In both environments, her colors automatically change and her eyes move around." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fbc70fe-44b4-4736-a442-5b71d412ae11/9-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fbc70fe-44b4-4736-a442-5b71d412ae11/9-accessible-svgs-inclusiveness-beyond-patterns.png" sizes="100vw" caption="Karma Chameleon in dark mode. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fbc70fe-44b4-4736-a442-5b71d412ae11/9-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="In dark mode, she is sitting on a branch in space with a blue rocket zooming past. In both environments, her colors automatically change and her eyes move around." >}}

{{% ad-panel-leaderboard %}}

### Color And Contrast Accessibility

<p>While the above examples are fun ways to show what you can do with color and contrast and the <em>@prefers-color-scheme</em> media query, there are some really great real-world reasons to consider adding a dark theme including:</p>

<ul>
<li>Dark themes are helpful to people with <a href="https://www.webmd.com/eye-health/photophobia-facts">photophobia</a>, or light sensitivity. People with photophobia can trigger headaches and migraines when they view a website or app that is too bright.</li>
<li>Some people find the text on a website or app <a href="https://www.wired.com/story/give-yourself-to-dark-mode-side/">easier to read in dark mode</a> while others might find <a href="https://www.wired.com/story/do-you-need-dark-mode/">lighter themes are easier to read</a> &mdash; it essentially comes down to giving your user a <em>choice</em> and allowing them to set their preference.</li>
<li>Unlike some other color or contrast based media queries like <a href="https://drafts.csswg.org/mediaqueries-5/#descdef-media-inverted-colors"><code>@inverted-colors</code></a> (currently only <a href="https://caniuse.com/#search=inverted-colors">supported by Safari</a>) and <a href="https://drafts.csswg.org/mediaqueries-5/#descdef-media-forced-colors"><code>@forced-colors</code></a> (developed by Edge/IE engineers with Chromium support coming soon), the browser support is pretty universal for <a href="https://caniuse.com/#search=prefers-color-scheme"><code>@prefers-color-scheme</code></a> &mdash; so this media query is useful out of the box today and it should be sticking around for awhile. Plus with the recent changes to <a href="https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/master/Accessibility/HighContrast/explainer.md">MS Edge using Chromium</a> under the hood, there is even more support for this media query going forward (R.I.P. <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@media/-ms-high-contrast"><code>-ms-high-contrast-mode</code></a>).</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/532b410e-3e4a-48bb-b238-f1acb388d9a6/5-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/532b410e-3e4a-48bb-b238-f1acb388d9a6/5-accessible-svgs-inclusiveness-beyond-patterns.png" sizes="100vw" caption="Graph showing which browsers utilize the CSS at-rule: <code>@media: prefers-color-scheme</code> media feature. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/532b410e-3e4a-48bb-b238-f1acb388d9a6/5-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="Graph showing which browsers utilize the CSS at-rule: @media: prefers-color-scheme media feature - IE and Opera mobile being the only major non-supporting browsers at this time." >}}

## SVG Animation

<p>In conjunction with color and contrast, how your SVG moves on the screen is another aspect to consider when designing and developing with inclusiveness in mind. The <a href="https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html">WCAG motion guidelines</a> are clear: non-essential moving, blinking, or scrolling information that starts automatically, lasts more than five seconds, and is part of other page elements must allow the user to pause, stop, or hide it. But why do we need this rule?</p>

<p>For some users, moving, blinking, or scrolling content can be very distracting. People with <a href="https://www.nimh.nih.gov/health/publications/attention-deficit-hyperactivity-disorder-adhd-the-basics/index.shtml">ADHD</a> and other attention deficit disorders might be so distracted by your animated SVGs they forget why they even went to your website/app in the first place. While for other people, motion can trigger physical reactions. For example, people with <a href="https://vestibular.org/understanding-vestibular-disorder/symptoms">vestibular issues</a> can become nauseous and dizzy when viewing movement. While others can be <a href="https://alistapart.com/article/designing-safer-web-animation-for-motion-sensitivity/ https://developer.mozilla.org/en-US/docs/Web/Accessibility/Seizure_disorders">triggered to have a seizure</a> when viewing content that flashes or is bright &mdash; a situation you obviously want to avoid.</p>

{{% pull-quote %}}
 While we all like being “delighted” with interesting website and app features — we need to strike a balance between being creative versus distracting (or harming) our users during their interaction with moving content.
{{% /pull-quote %}}

### Manual/Auto Stop

<p>Since SVG animations, like other moving content, must not auto-play for more than five seconds, you must create a way for users to pause or stop the animation. One way to do this is to create a JS toggle button to play/pause the animation.</p>

<p>If your SVG is large or is the main feature of your website (e.g. animations that pop in and out as you scroll down a page) a pause/play button at the top of the screen might be a realistic option to control the entire experience of the page. If your SVGs are smaller in scale or related to user input (e.g. an animation happens when a user submits a form), a pause/play button might not be realistic for each individual image, so an alternative option is to code the animation to stop at five seconds vs. playing it on an infinite loop.


### Reduced Motion

<p>In addition to using a pause/play option or creating a finite animation loop, you may also consider adding <a href="https://www.w3.org/WAI/WCAG21/Techniques/css/C39.html"><code>@prefers-reduced-motion</code></a> media query to address the animation in your SVGs. Similar to the light/dark theme example, the <code>@prefers-reduced-motion</code> media query checks the user’s settings for motion restrictions and then implements a visual experience based on their preference. In the case of <code>@prefers-reduced-motion</code>, a user can choose to minimize the amount of animation or motion they see.</p>

<p>In the following example, the animated SVG “writes out” a word as the page loads &mdash; this is its default animation. In the reduced motion version, the SVG is stationary and the word loads without the animation. Depending on the complexity of your SVG animation and how you want the reduced motion experience to look, the amount of extra code involved can vary.</p>

{{< codepen height="480" theme_id="light" slug_hash="dyodvqm" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Reduced motion with SVGs](https://codepen.io/smashingmag/pen/dyodvqm) by <a href="https://codepen.io/cariefisher">Carie Fisher</a>.{{< /codepen >}}

#### Default motion:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b31ce1-8c0e-4e3c-852d-d3885a9ab99c/svg-a11y-write.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b31ce1-8c0e-4e3c-852d-d3885a9ab99c/svg-a11y-write.gif" width="800" alt="Movie depicting text being written out via code not adhering to WCAG best practices on movement" /></a><figcaption>The default motion version of the text script (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b31ce1-8c0e-4e3c-852d-d3885a9ab99c/svg-a11y-write.gif">Large preview</a>)</figcaption></figure>

<pre><code class="language-css">.svg-color {
  stroke: #ff4b00;
}

#a11y-svg {
  stroke-linecap: round;
  padding: 0.25rem;
  stroke-dasharray: 1000;
  stroke-dashoffset: 0;
  -webkit-animation: dash 5s linear forwards;
  animation: dash 5s linear forwards;
  overflow: visible;
  font-size: 100px;
  height: 0;
  margin: 10rem 0 5rem;
  position: relative;
}

#a11y-svg-design {
  cursor: pointer;
  stroke-width: 2px;
}

@-webkit-keyframes dash {
  from {
    stroke-dashoffset: 1000;
    fill: transparent;
  }

  to {
    stroke-dashoffset: 0;
    fill: #ff4b00;
  }
}</code></pre>

#### Reduced motion:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6128f4b-bbef-4df0-867d-ddd5b3139aea/6-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6128f4b-bbef-4df0-867d-ddd5b3139aea/6-accessible-svgs-inclusiveness-beyond-patterns.png" sizes="100vw" caption="The reduced motion version of the text script. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6128f4b-bbef-4df0-867d-ddd5b3139aea/6-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="Still screenshot of the word accessibility in orange with no movement." >}}

<pre><code class="language-css">@media (prefers-reduced-motion: reduce) {
  #a11y-svg {
    animation: none;
    fill: #ff4b00;
  }
}</code></pre>

<p>Keep in mind, having <code>@prefers-reduced-motion</code> code in place is one step in making your SVGs more accessible, but you also need to consider the <em>way</em> the motion is reduced. For example, let’s say you create a slowed-down version of your SVG animation using <code>@prefers-reduced-motion</code>. However, the slower version is on an infinite loop so the animation lasts more than five seconds, which violates one part of the WCAG rules on motion. If you instead create a reduced motion version of your animated SVG that <em>stops</em> the animation at five seconds, then it would pass that part of the rule. This subtle code change equals two completely different user experiences.</p>

<p>In the next example, Karma Chameleon is back with a <code>@prefers-reduced-motion</code> media query and related code. By changing your motion settings (<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion">Mac, Win, Android, and iOS settings</a>) and using a browser that supports <code>@prefers-reduced-motion</code> media query, you can see the animation change. In the light mode with reduced motion, Karma Chameleon in a forest with a stationary red butterfly. In dark mode with reduced motion, she is in space with a stationary blue rocket in the background. In both environments, her colors and eyes are also stationary, as the original SVG animation is completely removed.</p>

{{< codepen height="480" theme_id="light" slug_hash="rNVJyoj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Light/Dark mode + reduced motion with SVGs (Karma Chameleon)](https://codepen.io/smashingmag/pen/rNVJyoj) by <a href="https://codepen.io/cariefisher">Carie Fisher</a>.{{< /codepen >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e90ae013-6fce-46c2-8162-ea92d0a74c5b/7-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e90ae013-6fce-46c2-8162-ea92d0a74c5b/7-accessible-svgs-inclusiveness-beyond-patterns.png" sizes="100vw" caption="Karma Chameleon in light mode + no movement. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e90ae013-6fce-46c2-8162-ea92d0a74c5b/7-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="In light mode + reduced motion, Karma Chameleon is in a forest with a stationary red butterfly. In both environments, her colors and eyes are also stationary, as the original SVG animation is completely removed." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f017d30-7752-4d6b-bc28-bd4744762c75/8-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f017d30-7752-4d6b-bc28-bd4744762c75/8-accessible-svgs-inclusiveness-beyond-patterns.png" sizes="100vw" caption="Karma Chameleon in dark mode + no movement. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f017d30-7752-4d6b-bc28-bd4744762c75/8-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="In dark mode + reduced motion, Karma Chameleon is in space with a stationary blue rocket in the background. In both environments, her colors and eyes are also stationary, as the original SVG animation is completely removed" >}}

{{% ad-panel-leaderboard %}}

### Animation Accessibility

<p>From an accessibility standpoint, there are some great reasons to consider limiting the movement on your screen or providing alternative animations in your SVGs including:</p>

<ul>
<li>Less is more! Keeping your SVG animations simple for people with cognitive and attention disorders can help with your overall user experience. This is especially true for SVGs critical to the content or functionality of your website or app &mdash; such as navigation, buttons, links, or any animation triggered by user input.</li>
<li>Don’t make people sick! Some people with seizure, vestibular, and vision disorders can <a href="https://css-tricks.com/introduction-reduced-motion-media-query/">trigger physical reaction by motion in your SVGs</a>, so please be responsible with your designs and code. Note: you should double-check any animated SVGs that could be problematic in the flashing/blinking area, by using the free <a href="https://trace.umd.edu/peat">Photosensitive Epilepsy Analysis Tool</a> (PEAT) to ensure you don’t trigger seizures with your content.</li>
<li>Most major browsers now support <a href="https://caniuse.com/#search=prefers-reduced-motion"><code>@prefers-reduced-motion media query</code></a> both on desktop and mobile devices &mdash; meaning that more people can limit their exposure to unwanted movement on their screens. Unlike the media query <code>@prefers-color-scheme</code> which has a lot of competitors, there is currently no other motion reducing media query available.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcf42c7a-fc26-4923-8f7d-d3db29e40327/4-accessible-svgs-inclusiveness-beyond-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcf42c7a-fc26-4923-8f7d-d3db29e40327/4-accessible-svgs-inclusiveness-beyond-patterns.png" sizes="100vw" caption="Graph showing which browsers utilize the CSS at-rule: <code>@media: prefers-reduced-motion</code> media feature (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcf42c7a-fc26-4923-8f7d-d3db29e40327/4-accessible-svgs-inclusiveness-beyond-patterns.png'>Large preview</a>)" alt="Graph showing which browsers utilize the CSS at-rule: @media: prefers-reduced-motion media feature - IE and Opera mobile being the only major non-supporting browsers at this time; globally accepted 82.47%" >}}

## Wrapping Up

<p>Color, contrast, and animation is at the heart of every SVG. Studies report that these visual elements hold intrinsic meaning, contribute to brand recognition, and are tied to a company’s perceived value &mdash; making SVGs a very large area where designers and developers can have a direct and immediate impact on our users.</p>

<p>But it is also important that we don’t just think of SVG accessibility as something to help “other people” &mdash; because who hasn’t found themselves in a situation where they have to battle glare on a device screen? Or you have a migraine and SVGs keep floating on and off the screen making you sick instead of “delighted”. Or maybe you visit a website in a low-light setting and the text is hard to read due to the gray-on-gray color scheme?</p>

<p>With the use of accessibility tools, WCAG guidelines, and the continued addition and support of new CSS media queries to allow for more choice, we can impact all people in a more responsible and inclusive way.</p>

{{% pull-quote %}}
 For true digital inclusivity is understanding that every single one of us can benefit from more accessible designs and code.
{{% /pull-quote %}}

{{< signature "dm, yk, il" >}}
