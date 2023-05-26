---
title: 'Smart CSS Solutions For Common UI Challenges'
slug: modern-css-solutions-for-common-problems
author: cosima-mielke
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3bf0115-0bc9-41b7-b027-3ea8b6b7e848/transition-css-gradients-opt.png
date: 2021-10-14T12:00:00.000Z
summary: >-
  Writing CSS has probably never been more fun and exciting than it is today. In this post we’ll take a look at common problems and use cases we all have to face in our work and how to solve them with modern CSS. If you’re interested, we’ve also just recently covered [CSS auditing tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/), [CSS generators](https://www.smashingmagazine.com/2021/03/css-generators/), [front-end boilerplates](https://www.smashingmagazine.com/2021/06/useful-frontend-boilerplates-starter-kits/) and [VS code extensions](https://www.smashingmagazine.com/2021/05/useful-vs-code-extensions-web-developers/) &mdash; you might find them useful, too.
description: >-
  Writing CSS has probably never been more fun and exciting than it is today. In this post we’ll take a look at common problems and use cases we all have to face in our work and how to solve them with modern CSS. If you’re interested, we’ve also just recently covered [CSS auditing tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/), [CSS generators](https://www.smashingmagazine.com/2021/03/css-generators/), [front-end boilerplates](https://www.smashingmagazine.com/2021/06/useful-frontend-boilerplates-starter-kits/) and [VS code extensions](https://www.smashingmagazine.com/2021/05/useful-vs-code-extensions-web-developers/) &mdash; you might find them useful, too.
categories:
  - Tools
  - CSS
  - Resources
  - Round-Ups
---

It’s incredible to see what we can do with CSS today, especially if you still remember how difficult it once was to figure out stacking contexts or why margins collapsed and why `top: float` didn’t work. In this post, we’ll look at just that: **exciting and fun things we can do with CSS**, exploring common problems and use cases we all have to face in our work.

{{< refs >}}
    <h3 style="margin-top: 1.25em">Related Articles On CSS:</h3>
    <ul>
    <li><a href="https://www.smashingmagazine.com/2021/03/css-generators/">CSS Generators</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/03/css-auditing-tools/">CSS Auditing Tools</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/css-z-index-large-projects/">Managing CSS Z-Index</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/things-you-can-do-with-css-today/">Things You Can Do With CSS Today</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/useful-chrome-firefox-devtools-tips-shortcuts/">Useful DevTools Tips and Shortcuts</a></li>
    <li>Also, <a href="/the-smashing-newsletter/">subscribe to our newsletter</a> to not miss the next ones.</li>
</ul>
{{< /refs >}}


## Richer, Life-Like Shadows With CSS

Shadows help convey meaning and add extra value to a UI. However, a lot of shadows that we see on the web these days don’t use their full potential. Let’s change that!

A comprehensive deep-dive into all things shadows comes from Rob O’Leary. His [article on CSS Tricks](https://css-tricks.com/getting-deep-into-shadows/) explores how light affects shadows and how to define a light source &mdash; the foundation to creating authentic shadow effects. Once that base is set, you’ll learn how to use shadows to evoke depth, elevate elements, and inset them, how to layer shadows, and, of course, which CSS property to use for which use case. Rob also takes a look at the accessibility and performance implications that shadows bring along, as well as how to animate them.

{{< rimg href="https://css-tricks.com/getting-deep-into-shadows/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53de3b82-28d7-44b3-9f5f-7e648a08eb7c/01-optimized-shadow-css.jpg" width="700" height="488" sizes="100vw" caption="Regular vs. irregular shadow. A <a href='https://www.joshwcomeau.com/css/designing-shadows/'>subtle change creates more depth</a>." alt="Getting Deep Into Shadows" >}}

Another [fantastic article on the topic](https://www.joshwcomeau.com/css/designing-shadows/) comes from Josh W Comeau. To put an end to those “fuzzy grey boxes that don’t really look much like shadows”, as Josh describes the current state of most shadows on the web, he shows how to transform typical box-shadows into beautiful, life-like ones. A little detail that makes any UI a lot more tactile.

## CSS Paper Cut-Out Effect

If you ever wanted to create a paper cut-out effect for a heading, you might have struggled quite a bit. Perhaps you need to set up two separate `div`s that then would be overlapped on top of each other. The spacing would need to be defined in relative units, of course, that might be a bit difficult to get right across screens.

{{< rimg href="https://css-tricks.com/getting-deep-into-shadows/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76ece241-3da9-4d44-a9ed-a7ee476bb4ba/02-paper-cut-out.jpg" width="700" height="488" sizes="100vw" caption="<a href='https://codepen.io/smashing-magazine/pen/dyzPQor'>CSS Paper Cut-Out</a>, with a pseudo-element and a data attribute." alt="CSS Paper Cut-Out" >}}

Stephanie Eckles’ [CSS Paper Cut-Out Effect](https://codepen.io/smashing-magazine/pen/dyzPQor) solves the problem for good with CSS custom properties, CSS Grid, CSS transforms and a good ol'-fashioned CSS function `attr()`. Stephanie is using a `data`-attribute on `h1` along with a `span` inside it. `attr()` picks up the value of the `data`-attribute, which is then used for the `content`-property in a `:after`-pseudo element. The highlights, shadows and colors can then be adjusted with CSS Custom Properties. Reusable and simple to maintain!

And if you are interested in more magic by Stephanie and other wonderful people who love CSS, take a look at [StyleStage](https://stylestage.dev/), where modern CSS gets the spotlight it deserves.

{{< rimg href="https://ishadeed.com/article/thinking-about-the-cut-out-effect/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95a80ce7-f235-4747-a303-f926b708c42e/transparent-elipse-diagram.png" width="800" height="379" sizes="100vw" caption="When do we use CSS, and when do we use SVG instead? Ahmad’s <a href='https://ishadeed.com/article/thinking-about-the-cut-out-effect/'>strategies on achieving the cut-out effect</a>." alt="Using a transparent ellipse to illustrate the cut-out effect" >}}

Also, take a look at Ahmad Shadeed’s piece on [Thinking About The Cut Out Effect](https://ishadeed.com/article/thinking-about-the-cut-out-effect/), which goes into all the fine detail of deciding when SVG might make more sense, and how to implement in a real-life scenario. The article also provides plenty of code examples to get started with!

## The Minimap For The Web

We’ve seen them before: tiny horizontal bars that usually live at the top of the page. As a user is scrolling down, the horizontal bar is filling up, so the user knows how much is actually left to scroll.

What if we make it **a bit more contextual** though? Perhaps the page includes some images and videos, or quotes and distinct sections &mdash; wouldn’t be interesting to highlight them differently, while also allowing readers to pin a position on the page and jump back if needed? Well, Rauno Freiberg thought so, too.

{{< rimg href="https://uiw.tf/minimap" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/396b5b84-9cb7-4a32-97d1-ac9fa715ddc0/03-progress.jpg" width="710" height="409" sizes="100vw" caption="What about a slightly more contextual minimap for the web? Rauno Freiberg <a href='https://uiw.tf/minimap'>has a suggestion</a>." alt="A screenshot of the Minimap landing page" >}}

Rauno’s [minimap for the web](https://uiw.tf/minimap) (currently works only in Firefox) makes it trivial to create a minimap representation of the entire page, while also allowing readers to pin section of the page and navigate between them. To achieve it, Rauno uses an experimental CSS property [`element()`](https://developer.mozilla.org/en-US/docs/Web/CSS/element()) to display a live image from an arbitrary HTML element (which currently only available in Firefox). 

## Conditional Border Radius In CSS

When designing cards, you might want a `border-radius` to have a quite sizeable value when there is enough space to display it along with other cards. Yet **when there is no space** and perhaps no margin either on the card &mdash; as it might be the case on smaller screens &mdash; you might want to reduce `border-radius` to `0`. How would you achieve that?

{{< rimg href="https://ishadeed.com/article/conditional-border-radius/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2609d7d3-4af3-4b92-a493-74635edb4f9e/conditional-border-rad.jpg" width="800" height="442" sizes="100vw" caption="What if you needed to reduce the border-radius on smaller screens, while making it larger on larger screens? Well, Ahmad <a href='https://ishadeed.com/article/conditional-border-radius/'>has a solution for just that</a>." alt="A comparison of how the same page looks like on mobile and desktop with border radius 0px and 8px" >}}

Ahmad Shadeed has looked into this problem in quite a bit of detail in his article on [Conditional Border Radius In CSS](https://ishadeed.com/article/conditional-border-radius/). The idea, originally suggested by Heydon Pickering and Naman Goel, is to use a large enough number to trigger one state or the other. On smaller screens, if the difference between `100vw` and `100%` is `0`, then the radius will be `0`, too; but if the difference is larger, a larger value would be used. You can [take a look at the CodePen](https://codepen.io/shadeed/pen/BaZezzv) as well.

{{% feature-panel id="vitaly-friedman" %}}

## CSS Grainy Gradients

What if you wanted to **add some noise** to bring a bit of texture to an image? Of course you could export images as PNGs, WebP or AVIFs, but ideally we’d want to add "noise" on top of SVGs, so we can always turn and off noise if we wanted to.

{{< rimg href="https://css-tricks.com/grainy-gradients/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa0f21e9-7cb1-4cf5-8313-6f2a2e7c3597/grainy-gradients-example.png" width="800" height="430" sizes="100vw" caption="Adding a bit of grainty texture to a gradient. Jimmy Chion <a href='https://css-tricks.com/grainy-gradients/'>shows how it works</a>." alt="SVG noise combined with a CSS filter on a CSS gradient " >}}

In his CSS-Tricks article on [grainy gradients](https://css-tricks.com/grainy-gradients/), Jimmy Chion explains how we can generate colorful noise to add texture to a gradient with just a sparkle of CSS and SVG. As Jimmy explains, the idea is to use an SVG filter to create the noise, then apply that noise as a background. Then we layer it underneath a gradient, refine the brightness and contrast, and &mdash; voilà &mdash; you have gradient that gradually dithers away.

Issue solved! You can also explore the [Grainy Gradient playground](https://grainy-gradients.vercel.app/) that Jimmy has set up.


## Multi-Line Background Gradient

Some things might seem impossible to do with CSS &mdash; well, until someone finds a hack to make it happen. Like in this case: Can you achieve a multi-line padded text with a gradient that doesn’t reset for each line?

{{< rimg href="https://twitter.com/m_ott/status/1069741458641600513" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c26aba8f-df0b-4053-93b5-a4e3c607e149/multi-padded-text-opt.png" width="700" height="232" sizes="100vw" caption="A <a href='https://twitter.com/m_ott/status/1069741458641600513'>multi-line background gradient</a> created with CSS. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c26aba8f-df0b-4053-93b5-a4e3c607e149/multi-padded-text-opt.png'>Large preview</a>)" alt="Multiline background gradient with mix-blend-mode" >}}

Yes, [as Matthias Ott shows](https://twitter.com/m_ott/status/1069741458641600513). Matthias’ solution is a bit hacky, but it leads to the desired result thanks to a pseudo-element that is added on top of the text. An interesting idea to tinker with.


## Form Field Focus Without Outlines

Who said forms need to be boring? Hakim El Hattab created a [demo](https://lab.hakim.se/focussss/) that proves that even something as simple as a form asking for name, email, and password is an occasion to think outside the box and cater for a spark of delight.

{{< rimg href="https://lab.hakim.se/focussss/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7018dabb-2448-43c6-a49c-a117e3a04401/focus-opt.png" width="700" height="473" sizes="100vw" caption="A <a href='https://lab.hakim.se/focussss/'>form field focus concept</a> that thinks outside the box. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7018dabb-2448-43c6-a49c-a117e3a04401/focus-opt.png'>Large preview</a>)" alt="Focusss" >}}

To achieve that, Hakim combines form focus and validation in a subtle yet surprising animation that gets by without any focus outlines on the fields themselves. Instead, a dot marks the field that is focused. When the focus switches to another field, the animation is triggered, and the dot jumps to the new active field, drawing a connection between the two. Form field validation is also integrated seamlessly, with the dot expanding and showing a checkmark. If you’d like to dive deeper into the code, Hakim also published a demo on [Codepen](https://codepen.io/hakimel/pen/YzZoVxx). Inspiring!

## Transitioning CSS Gradients

If you’ve ever tried to transition gradients in CSS, you probably have noticed that it actually doesn’t work. Instead of gradually fading from one gradient to another, the change is happening immediately, abruptly, with no smooth transition between the two.
  
{{< rimg href="https://keithjgrant.com/posts/2017/07/transitioning-gradients/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3bf0115-0bc9-41b7-b027-3ea8b6b7e848/transition-css-gradients-opt.png" width="700" height="453" sizes="100vw" caption="Transitioning gradients in CSS? Keith J. Grant shares a clever <a href='https://keithjgrant.com/posts/2017/07/transitioning-gradients/'>workaround</a> that gets the job done. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3bf0115-0bc9-41b7-b027-3ea8b6b7e848/transition-css-gradients-opt.png'>Large preview</a>)" alt="Transitioning CSS Gradients" >}}

As Keith J. Grant has [discovered](https://keithjgrant.com/posts/2017/07/transitioning-gradients/), we can achieve the transition with a **clever workaround** though. We use a pseudo-element and opacity transform for that. First, we apply one gradient to the element, then position its pseudo-element to fill the element, and then apply the second gradient to it. And we “transition” between two gradients by transitioning the opacity of the pseudo-element. You can check a [full working example on CodePen](https://codepen.io/keithjgrant/pen/OgEdgN).

## Improving Image Performance With `image-set()`

Have you heard of `image-set()` already? You can think of it as a CSS background equivalent to the HTML `srcset` attribute for `img` tags. Chromium-based browsers and Safari have supported it for some years now, Firefox followed just recently. Ollie Williams takes a look at [what we can and what we can’t do with it today](https://css-tricks.com/using-performant-next-gen-images-in-css-with-image-set/).

{{< rimg href="https://css-tricks.com/using-performant-next-gen-images-in-css-with-image-set/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7439d61-2cf3-4683-8a59-1397627249a7/image-set-2-opt.png" width="700" height="351" sizes="100vw" caption="<code>image-set()</code> can be used to <a href='https://css-tricks.com/using-performant-next-gen-images-in-css-with-image-set/'>serve different background images to different users</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7439d61-2cf3-4683-8a59-1397627249a7/image-set-2-opt.png'>Large preview</a>)" alt="Using Performant Next-Gen Images in CSS with image-set" >}}

As Ollie describes, one use case for `image-set()` is to provide multiple resolutions of a background image and leave it to the browser to decide which image is served to a user &mdash; a high-res version for users on fancy devices and a lower-res image for those on slow connections or screens with a lower pixel density, for example.

Another very promising use case is still lacking browser support, unfortunately: the idea to use new image formats like AVIF, WebP, or HEIF while adding a fallback for older browsers. If you want to achieve something like that already today and don’t need `background-image`, the `&lt;picture&gt;` element might be an alternative worth considering, as Ollie suggests. A great read to help you improve image performance.

{{% ad-panel-leaderboard %}}

## Clip-Path Pop-Out Effect

With `clip-path: path()` supported by major browsers, it’s time to get creative. Mikael Ainalem shows a beautiful use case for the rather new feature: a [buttery-smooth pop-out effect](https://codepen.io/ainalem/full/QWGNzYm).

{{< rimg href="https://codepen.io/ainalem/full/QWGNzYm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1540260-9d6a-489f-9110-01df256801ef/clip-path-opt.png" width="700" height="430" sizes="100vw" caption="A <a href='https://codepen.io/ainalem/full/QWGNzYm'>pop-out effect</a> created with <code>clip-path: path()</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1540260-9d6a-489f-9110-01df256801ef/clip-path-opt.png'>Large preview</a>)" alt="Pop-out effect" >}}

Mikael uses `clip-path: path()` to set a photo of a person apart from its circle-shaped background. As you hover over it, the person seems to rise from the inside of the circle, creating a cool 3D impression. Perfect for “About Us” pages.

## Whimsical 3D Button

Details matter. Designing a lovely button doesn’t seem to be a big complicated endeavor: a bit of padding here and there, a funky color, accessible text, and a few button states. Well, Josh Comeau has gone all the way to design a [truly whimsical 3D button](https://www.joshwcomeau.com/animation/3d-button/) that you might want to click more than once.

{{< rimg href="https://www.joshwcomeau.com/animation/3d-button/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e509cd52-e15a-4470-a768-82dceb05b1d0/3d-button-opt.png" width="700" height="317" sizes="100vw" caption="A technique for a <a href='https://www.joshwcomeau.com/animation/3d-button/'>3D button</a> you’ll want to push over and over again comes from Josh Comeau. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e509cd52-e15a-4470-a768-82dceb05b1d0/3d-button-opt.png'>Large preview</a>)" alt="3D Button" >}}

The idea is simple: we create two layers and offset the foreground layer a little bit at first. On hover, we shift the front layer down. Then, we adjust the focus outline with `outline-offset`, or use `:focus:not(:focus-visible)` to hide the outline when the button is focused and the user is using a pointer device.

Then we shift the button up by a few pixels when they hover, animate the transform a lil’ bit, adjust the Bezier curve for animation and add a bit of blurring, for a softer, more natural shadow. And voilà &mdash; we have a whimsical 3D button that is **accessible, works on mobile and on desktop**, and is a pleasure to tap and click on. Of course, you can find the [full code snippet](https://www.joshwcomeau.com/animation/3d-button/) on Josh’s blog.

## CSS Charts

Perhaps you need to design a column chart, or a bar chart, or even a multi-dataset column chart or stacked columns. Where do you even start? Perhaps with [Charts.css](https://chartscss.org/), a **CSS data visualization framework** that uses CSS utility classes to style HTML elements as charts.
  
{{< rimg href="https://chartscss.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a593b64-ef42-458c-8401-5e0ecfba584f/charts-css-opt.png" width="700" height="564" sizes="100vw" caption="<a href='https://chartscss.org/'>Charts.css</a> is a modern CSS framework for all things data visualization. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a593b64-ef42-458c-8401-5e0ecfba584f/charts-css-opt.png'>Large preview</a>)" alt="Charts CSS" >}}

Created by Lana Gordiievski and Rami Yushuvaev, the framework supports many chart types, has no dependencies, and is very lightweight. It also includes thorough documentation on its [components](https://chartscss.org/components/) and [built-in chart types](https://chartscss.org/charts/), plus the source code is [available on GitHub](https://github.com/ChartsCSS/charts.css) (licensed under MIT). And if you need slightly more creative approaches, Preethi explains [how to create CSS Charts with interesting shapes](https://css-tricks.com/how-to-create-css-charts-with-interesting-shapes-glyphs-and-emoji/) on CSS-Tricks as well.

## The New CSS Reset

What do you use to **normalize styles across browsers**? As of recently, there were new approaches to reduce the size of the global CSS reset, and perhaps they would be good candidates for your projects as well.
  
{{< rimg href="https://piccalil.li/blog/a-modern-css-reset/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee91222-6ab6-4c98-9577-ca0d57513394/css-reset-opt.png" width="700" height="366" sizes="100vw" caption="Andy Bell shares a <a href='https://piccalil.li/blog/a-modern-css-reset/'>strategy for reducing the CSS reset</a> to a minimum. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee91222-6ab6-4c98-9577-ca0d57513394/css-reset-opt.png'>Large preview</a>)" alt="CSS Reset" >}}

With his [Modern CSS Reset](https://piccalil.li/blog/a-modern-css-reset/), Andy Bell has reduced the CSS reset to its minimum by adding box-sizing rules, removing default margins, set core root default and body defaults. Along with it Andy removes all animations, transitions, and smooth scroll for people that prefer not to see them, and has added modern properties like `scroll-behavior` and `text-decoration-skip-ink` by default.

The [New CSS Reset](https://github.com/elad2412/the-new-css-reset) by Elad Shechter takes a slightly more aggressive approach. Elad removes all the default styles which we are getting on specific HTML elements except the `display property`. Both approaches are worth looking into!


## Stable Scrollbar Gutters With CSS

Ah, the good ol’ layout shifts! As Bramus Van Damme [explains](https://www.bram.us/2021/07/23/prevent-unwanted-layout-shifts-caused-by-scrollbars-with-the-scrollbar-gutter-css-property/), one of the slightly more obscure reasons for layout shifts comes due to **different types of scrollbars** on the web. While overlay scrollbars on iOS/macOS are placed *over* the content (and aren’t shown by default), other scrollbars are placed in the “scrollbar gutter”, i.e. the space between the inner border edge and the outer padding edge.
  
{{< rimg href="https://www.bram.us/2021/07/23/prevent-unwanted-layout-shifts-caused-by-scrollbars-with-the-scrollbar-gutter-css-property/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fab7f77-2708-4756-84f6-4bec6fe9f4f1/overflow-example-opt.png" width="700" height="979" sizes="100vw" caption="Bramus Van Damme shows how to prevent content shifts with <a href='https://www.bram.us/2021/07/23/prevent-unwanted-layout-shifts-caused-by-scrollbars-with-the-scrollbar-gutter-css-property/'>stable scrollbar gutters</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fab7f77-2708-4756-84f6-4bec6fe9f4f1/overflow-example-opt.png'>Large preview</a>)" alt="Overflow example" >}}

When the content of a box becomes too large, the browser will &mdash; by default &mdash; show a scrollbar. In the latter case, it will cause a layout shift. Fortunately, this problem might be gone for good soon. Meet a shiny new `scrollbar-gutter` property: by setting it to `stable`, we can have the browser always showing the scrollbar gutter, even if the box is not overflowing.

And to keep things symmetric, we can use `scrollbar-gutter: stable both-edges`. The feature isn’t available yet, but [coming in Chromium](https://www.bram.us/2021/07/23/prevent-unwanted-layout-shifts-caused-by-scrollbars-with-the-scrollbar-gutter-css-property/) very soon, with other rendering engines hopefully following soon.
## The Surprising Things That CSS Can Animate

When you think of animating CSS properties, which ones come to your mind? Will Boyd looked at the question from a different perspective and decided to explore the properties that don’t come to mind immediately, the ones that aren’t typically associated with animation, but turn out to be animatable.

{{< rimg href="https://codersblock.com/blog/the-surprising-things-that-css-can-animate/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b584490e-3fb1-4564-ad1e-5efff185aefd/animation-opt.png" width="700" height="447" sizes="100vw" caption="Animating overlapping cards with <code>z-index</code> is one of the <a href='https://codersblock.com/blog/the-surprising-things-that-css-can-animate/'>surprising things that CSS can do</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b584490e-3fb1-4564-ad1e-5efff185aefd/animation-opt.png'>Large preview</a>)" alt="The Surprising Things That CSS Can Animate" >}}

In his post “[The Surprising Things That CSS Can Animate](https://codersblock.com/blog/the-surprising-things-that-css-can-animate/)”, Will dives deep into these unexpectedly animatable properties &mdash; and, of course, the nifty things you can do by animating them. `z-index`, for example, can be used for layered animations, `opacity` helps you fade out a modal just with CSS. A great reminder of how powerful CSS is.

{{% ad-panel-leaderboard %}}

## Learning Resources

Learning never stops, right? Below we compiled some useful &mdash; and fun! &mdash; resources that are perfect to **take your CSS skills to the next level**. And if you’re already a CSS pro, there are also challenges to put your knowledge to the test. Enjoy!

### CSS Vocab And Cheatsheets

You might have been there before. Just when you are working on a **tight deadline**, you need to look up something quickly. For CSS, you will never go wrong with [CSS Tricks Almanac](https://css-tricks.com/almanac/), and you can also look up [CSS vocabulary](https://apps.workflower.fi/vocabs/css/en) gathered by Ville V. Vanninen from Finland as well.

{{< rimg href="https://apps.workflower.fi/vocabs/css/en" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/547afdd1-484d-4e8e-8dc3-b13f99e64c91/css-vocab-opt.png" width="700" height="461" sizes="100vw" caption="<a href='https://apps.workflower.fi/vocabs/css/en'>CSS Vocabulary</a> helps you find the right words when talking about CSS. (<a href='https://apps.workflower.fi/vocabs/css/en'>Large preview</a>)" alt="CSS Vocabulary" >}}

### Learn Flexbox The Fun Way

What do **frogs, zombies, and towers** have in common? Well, they are your best friends when learning Flexbox. Because, let’s be honest: Flexbox is very powerful once you understand it, but getting there can be quite hard. So let’s make learning a bit more fun.

{{< rimg href="https://flexboxfroggy.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181c9891-aff7-43e0-b46b-7fbf17bf94fb/flexbox-froggy-opt.png" width="700" height="360" sizes="100vw" caption="<a href='https://flexboxfroggy.com/'>Learning Flexbox made easy</a> &mdash; with a little help from some friendly little frogs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181c9891-aff7-43e0-b46b-7fbf17bf94fb/flexbox-froggy-opt.png'>Large preview</a>)" alt="Flexbox Froggy" >}}

In the game [Flexbox Froggy](https://flexboxfroggy.com/), you help a little frog and its friends **find their lilypads** by, you guessed it, writing CSS. The game consists of 24 levels that take you from the very basics of Flexbox positioning to more advanced challenges.

If zombies are more down your alley, [Flexbox Zombies](https://geddski.teachable.com/p/flexbox-zombies) is for you. Each section of the game unravels part of the plot, introduces a new Flexbox concept, and presents so-called **“zombie survival challenges”** that help you solidify your new skills.

Last but not least, you might also want to take a look at [Flexbox Defense](https://www.flexboxdefense.com/). Inspired by tower defense games, your job is to **stop incoming enemies** from getting past your defenses &mdash; by positioning your towers with CSS, of course. All three games run right in your browser. Happy flexbox’ing!

### CSS Grid, CSS Selectors, And Other Competitions

Do you want to take your CSS skills to the next level? These three little games help you do just that &mdash; quite literally. In [Grid Garden](https://cssgridgarden.com/), you’ll become the proud owner of a **carrot garden**. 28 levels are waiting for you in which you need to take good care of your crop with the help of CSS grid.

{{< rimg href="https://cssbattle.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5aa97ab-d7fe-4b7d-919b-5679c102c037/css-battle-opt.png" width="700" height="441" sizes="100vw" caption="If you want to put your CSS skills to the test, <a href='https://cssbattle.dev/'>CSS Battle</a> is the perfect place to do so. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5aa97ab-d7fe-4b7d-919b-5679c102c037/css-battle-opt.png'>Large preview</a>)" alt="CSSBattle" >}}

If you feel your CSS selectors skills could need some polishing, [CSS Diner](https://flukeout.github.io/) is for you. **Plates, apples, pickles** &mdash; in each of the 32 challenges, you’ll need to use a different CSS selector to select specific items on a table.

And if you’re up for some competition, be sure to also check out [CSSBattle](https://cssbattle.dev/). In the **CSS golfing game**, you’ll be using your CSS skills to visually replicate targets with smallest possible code to get to the top of the leaderboard. Each of the challenges is dedicated to a specific topic like `visibility`, `display`, `transition`, or `z-index`.

## Wrapping Up

Have you come across a CSS resources or technique recently that changed the way you approach a particular challenge? Let us know in the comments below! We’d love to hear about it.

{{< signature "vf" >}}