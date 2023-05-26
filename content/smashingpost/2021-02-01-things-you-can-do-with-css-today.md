---
title: 'Things You Can Do With CSS Today'
slug: things-you-can-do-with-css-today
author: andy-bell
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd843e63-2b5a-4c91-b390-2057ba966991/present-future-css-techniques.jpg
date: 2021-02-01T11:30:00.000Z
summary: >-
  The present and future of CSS are very bright indeed and if you take a pragmatic, progressive approach to your CSS, then things will continue to get better and better on your projects, too. In this article, we'll look into masonry layout, <code>:is</code> selector, <code>clamp()</code>, ch and ex units, updated text decoration, and a few other useful CSS properties.
description: >-
  The present and future of CSS are very bright indeed and if you take a pragmatic, progressive approach to your CSS, then things will continue to get better and better on your projects, too.
categories:
  - CSS
  - Tools
  - Workflow
---

CSS is great and getting better all the time. Over recent years, especially, it has evolved really fast, too. Understandably, some of the really handy powers CSS gives you might have slipped you by because of this, so in this article, I’m going to show you some really handy **stuff you can do with modern CSS today**, and also share some stuff that we can look forward to in the future.

Let’s dig in.

## Masonry Layout

Masonry layouts became very popular with Pinterest, Tumblr and Unsplash, and up until recently, we tended to [rely on JavaScript to assist with our layout](https://masonry.desandro.com/), which is almost never a good idea.

Sure, you can use [CSS multicol](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Columns/Basic_Concepts_of_Multicol) pretty darn effectively to achieve a masonry layout, but that approach can be problematic with tabbed-focus as it lays content out in *columns*. This creates a disconnect between the visual layout and the tabbing index.

Fast forward to today (well, *very* [*shortly in the future*](https://www.smashingmagazine.com/native-css-masonry-layout-css-grid/)) and a masonry layout is pretty trivial, thanks to an [update to CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Masonry_Layout). Here’s a complete masonry layout, with gutters, in 6 lines of CSS:

<pre><code class="language-css">.masonry {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: masonry;
  grid-gap: 1rem;
}</code></pre>

The magic is in `grid-template-rows` set as `masonry`, which turns it into the “masonry axis”, thus providing the “filled in” layout we’ve all come accustomed to.

Let’s expand on this and explore a quick demo of creating a **responsive masonry layout**. Using a slightly modified version of the above CSS, we can replace the `grid-template-columns` line to use this [auto grid method](https://piccalil.li/tutorial/create-a-responsive-grid-layout-with-no-media-queries-using-css-grid) instead:

<pre><code class="language-css">.masonry {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(16rem, 1fr));
  grid-template-rows: masonry;
  grid-gap: 1rem;
}</code></pre>

The `minmax()` function allows us to define what the smallest size is for our items, which for us, is `16rem`. Then we tell `minmax()` what the maximum size should be for each item. We declare that as 1fr, **which takes 1 portion of the remaining available space**.

This definition of `grid-template-columns` allows our layout to break and stack if it runs out of horizontal space which the **masonry axis** then automatically sorts our remaining elements for us.

**Note**: *Right now, masonry is [only working in Firefox Nightly](https://twitter.com/MiriSuzanne/status/1255567501359853570), or behind a flag, but the grid layout will still work perfectly in non-supporting browsers, making it a decent progressive enhancement target.*

{{< codepen height="480" theme_id="light" slug_hash="OJbJzVB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Native Masonry Layout With CSS Grid](https://codepen.io/smashingmag/pen/OJbJzVB) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

[Rachel Andrew](https://twitter.com/rachelandrew) [wrote a great article about CSS Grid Masonry](https://www.smashingmagazine.com/native-css-masonry-layout-css-grid/) and you can also read the [CSS Grid Layout Module Level 3 editor’s draft here](https://drafts.csswg.org/css-grid-3/) for technical details.

Masonry support is [currently very low](https://caniuse.com/?search=masonry), but as anything on the web, working out what your [minimum viable experience](https://piccalil.li/blog/a-minimum-viable-experience-makes-for-a-resilient-inclusive-website-or-app) is, then building up with progressive enhancement is a resilient way to build things. If you **must** use a masonry layout, though: I would recommend sticking with the [tried-and-tested](https://masonry.desandro.com) [Masonry.js](https://masonry.desandro.com) for now, but stick a ticket in your backlog to replace with native CSS in the future!

### Resources

- [Native CSS Masonry in CSS Grid](https://www.smashingmagazine.com/native-css-masonry-layout-css-grid/)
- [CSS Grid Layout Level 2: Masonry Layout](https://www.bram.us/2020/05/04/css-grid-layout-module-level-2-masonry-layout/)
- [Masonry JavaScript library](https://masonry.desandro.com/)
- [Editor’s spec draft](https://drafts.csswg.org/css-grid-3/)

{{% feature-panel %}}

## The `:is` Selector

I imagine a lot of us have had to write some gnarly CSS like this in the past:

<pre><code class="language-css">.post h1,
.post h2,
.post h3 {
    line-height: 1.2;
}

.post img,
.post video {
    width: 100%;
}</code></pre>

Thankfully, CSS has *got our back* again with the [`:is`](https://developer.mozilla.org/en-US/docs/Web/CSS/:is) [pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:is).

That CSS can now be hugely simplified into this instead:

<pre><code class="language-css">.post :is(h1, h2, h3) {
    line-height: 1.2;
}

.post :is(img, video) {
    width: 100%;
}</code></pre>


When things get more complex, it gets even more useful, because you can chain other selectors, such as `:not` and `:first-child`, just like in the following demo:

{{< codepen height="480" theme_id="light" slug_hash="rNMXYGx" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [:is selector demo](https://codepen.io/smashingmag/pen/rNMXYGx) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

The `:is()` pseudo-class works by taking a passed selector list then translating it into an expanded selector list for us. This allows us to write more compact code and for the browser to do what it does already.

If you have a complex project where specificity is *crucial,* then the `:where()` pseudo-class could be useful. The main difference between `:is()` and `:where()` is that `:where()` has zero specificity, whereas the `:is()` pseudo-class uses the most specific selector in the passed selectors collection. This becomes useful if you think that rules set in your `:is()` block might need to be overridden out-of-context. [This MDN article shows a great example of that](https://developer.mozilla.org/en-US/docs/Web/CSS/:where#comparing_where_and_is).

This `:is()` pseudo-class has [fantastic browser support](https://caniuse.com/css-matches-pseudo) &mdash; aside from IE11 and Opera Mini &mdash; so I would absolutely recommend that you start using it **today.** I would suggest caution with the `:where()` pseudo-class, though, because right now, [only Firefox and Safari support it](https://caniuse.com/?search=where).

### Resources

- [CSS :is() and :where() are coming to browsers](https://webplatform.news/issues/2020-06-04)
- [How slick is :is?](https://twitter.com/argyleink/status/1316143837903896577), a Twitter Thread
- [Comparing :where and :is on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:where#comparing_where_and_is)
- [Browser support for :is() and :where()](https://caniuse.com/css-matches-pseudo)

{{% ad-panel-leaderboard %}}

## Logical CSS Functions For Sizing

Responsive design has evolved into intrinsic design over the years as designers rightly push the boundaries of design on the web. There have been lots of hacks in the past &mdash; especially with fluid typography &mdash; that have been rather fragile, to put it lightly.

We do have some really useful CSS functions that help with sizing: `min()`, `max()` and `clamp()`. The `min()` function gets the **smallest** value from two passed parameters and `max()` does the opposite: grabs the **largest** value.

The `clamp()` function is even handier as it allows you to pass a **minimum**, a **maximum** and an **ideal** value. Because of this “locking”, ideal value, `clamp()` is being used more and more in fluid typography, like [Dave Rupert’s legendary FitText](https://codepen.io/davatron5000/pen/mddmRJe) because you get a guaranteed baseline, which prevents unpredictable outcomes. It’s the basis of all of these functions because if you set a good baseline as the minimum for `min()` and a good baseline as the maximum in `max()`, you’re getting that needed flexibility, insured by a sensible level of control.

These logical functions are way more useful than that though. Here’s a demo where I’m using them not just for a bit of fluid typography sizing, but also to size an avatar image effectively.

{{< codepen height="480" theme_id="light" slug_hash="YzGmEee" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Min and Clamp demo](https://codepen.io/smashingmag/pen/YzGmEee) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

In the demo, I’m using `min()` to size the image and also, calculate the border-radius in the same way. It’s incredibly subtle, but really helps to achieve high design detail on the web, which is great!

[Una Kravets](https://twitter.com/una) has [written a fantastically useful article](https://web.dev/min-max-clamp/) on the use cases of these functions. I also use it to [create a flexible wrapper](https://piccalil.li/quick-tip/use-css-clamp-to-create-a-more-flexible-wrapper-utility).

### Resources

- [min(), max(), clamp()](https://web.dev/min-max-clamp/)
- [min(), max(), and clamp() CSS Functions](https://ishadeed.com/article/css-min-max-clamp/)
- [min(), max(), and clamp() are CSS magic!](https://css-tricks.com/min-max-and-clamp-are-css-magic/)
- [Scale font-size with clamp()](https://css-tricks.com/linearly-scale-font-size-with-css-clamp-based-on-the-viewport/)
- [Handy demo](https://codepen.io/una/pen/bGpoGdJ) by Una Kravets
- [Browser support for min(), max(), clamp()](https://caniuse.com/css-math-functions)

## Specific Responsive Units For Typography

There are so many units in CSS that all cater to specific use cases. Did you know that there are units specifically for typography? Of course `em` and `rem` are font-size related, but `ch` and `ex` are based on the size of the letters themselves.

The `ch` unit is equal to the width of the `0` character of your rendered font in its size. This scales with the font too, so it’s a really handy way to [limit the width of your text, which helps with readability](https://piccalil.li/quick-tip/line-length). Also, keep in mind that in proportional typefaces, `1ch` is usually **wider than the average character width**, [often by around 20-30%](https://meyerweb.com/eric/thoughts/2018/06/28/what-is-the-css-ch-unit/).

The `ex` unit is equal to the height of the lowercase `x` character &mdash; also known as the “x-height” in more traditional typography. This is really useful for working accurately and responsively with the vertical axis of your typography. One really handy use case for this is making an SVG icon the same height as your text.

In the following demo, I’ve solved two problems with these units. First, I’ve limited the text length with `ch` and then used the `ex` unit to position a `<sup>` and `<sub>` element, more effectively. This has long been a pain in web design!

{{< codepen height="480" theme_id="light" slug_hash="YzGmELa" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CH and EX units demo](https://codepen.io/smashingmag/pen/YzGmELa) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

### Resources

- [Useful article on responsive units](https://every-layout.dev/rudiments/units/)
- [Quick tip on using `ch`](https://piccalil.li/quick-tip/line-length) to improve readability
- [`ch` browser support](https://caniuse.com/ch-unit)
- [`ex` browser support](https://caniuse.com/mdn-css_types_length_ex)

## Updated Text Decoration Control

Text decoration is no longer boring. You can do *loads* now, thanks to some updates in [Text Decoration Level 4](https://drafts.csswg.org/css-text-decor-4/). My favourite trick with this is creating a highlight style with `text-decoration-thickness`, `text-decoration-skip-ink` and `text-decoration-color`.

{{< codepen height="480" theme_id="light" slug_hash="WNGVXKV" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Text decoration demo](https://codepen.io/smashingmag/pen/WNGVXKV) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

I also like using these new properties to better control underline thickness for heading elements, as they can get pretty heavy in certain fonts.

I strongly recommend you [watch this video](https://www.youtube.com/watch?v=sZS-7RX_c7g) by [Jen Simmons](https://twitter.com/jensimmons) where, as always, she explains CSS properties in a friendly easy-to-understand manner.

### Resources

- [New CSS for Styling Underlines on the Web](https://www.youtube.com/watch?v=sZS-7RX_c7g), by Jen Simmons
- [Spec](https://drafts.csswg.org/css-text-decor-4/)
- [Browser support for `text-underline`](https://caniuse.com/?search=text-underline)

{{% ad-panel-leaderboard %}}

## Scroll Margin

This snippet of CSS will vastly improve your websites:

<pre><code class="language-css">[id] {
  scroll-margin-top: 2ex;
}</code></pre>

When a browser skips to an element with an `id` &mdash; often a heading in a long article like this one &mdash; the targeted element would sit flush to the top of the viewport. Not only did this not look great, but it caused issues for fixed headers too.

This property &mdash; `scroll-margin-top` &mdash; is the antidote to all of that and is incredibly useful. Check out this demo where I combine it with smooth scrolling:

{{< codepen height="480" theme_id="light" slug_hash="XWjvzop" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Scroll margin demo](https://codepen.io/smashingmag/pen/XWjvzop) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

### Resources

- [scroll-margin on CSS Tricks Almanac](https://css-tricks.com/almanac/properties/s/scroll-margin/)
- [Prevent content from being hidden underneath a fixed header by using `scroll-margin-top`](https://www.bram.us/2020/03/01/prevent-content-from-being-hidden-underneath-a-fixed-header-by-using-scroll-margin-top/)
- [Browser support for `scroll-margin-top`](https://caniuse.com/mdn-css_properties_scroll-margin)

## Aspect Ratio

If there was ever something we needed *desperately* in responsive design, it was native aspect ratio. This is especially needed for embedded media, such as YouTube videos. There’s long been the ol’ [padding hack](https://piccalil.li/tutorial/build-a-responsive-media-browser-with-css#heading-responsive-video-player) for these containers, but a hack should only be a temporary thing.

Thankfully, we will have [`aspect-ratio`](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio) support in major browsers soon.

If you enable `layout.css.aspect-ratio.enabled` in Firefox, the following demos will be a perfect square and a perfectly responsive YouTube video, respectively:

### Square (1:1)

Below is a square that’s always going to keep the same aspect ratio, 1:1 &mdash; achieve by defining <code class="language-css">aspect-ratio: 1 / 1</code>.

{{< codepen height="480" theme_id="light" slug_hash="zYKgPbw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Perfect square with aspect ratio](https://codepen.io/smashingmag/pen/zYKgPbw) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

### Video (16:9)

For videos, a square would be a quite uncommon format. Instead, we can use 16:9 be defining <code class="language-css">aspect-ratio: 16 / 9</code> on the box.

{{< codepen height="480" theme_id="light" slug_hash="oNzKoOq" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Perfect video embed with aspect ratio](https://codepen.io/smashingmag/pen/oNzKoOq) by <a href="https://codepen.io/piccalilli">Andy Bell</a>.{{< /codepen >}}

Even though `aspect-ratio` isn’t quite here yet, you should definitely start thinking about it &mdash; especially with images, as the following is likely to appear in all browsers as default styles, and is already in Firefox (69 onwards):

<div class="break-out">

<pre><code class="language-css">img, input[type="image"], video, embed, iframe, marquee, object, table {
  aspect-ratio: attr(width) / attr(height);
}</code></pre>
</div>

This is going to be really helpful in reducing page load *jank* because elements like `<img />` will generate a correctly sized box for themselves **before** they load. My advice is to start adding `width` and `height` attributes to elements in the above code sample to give your users a better loading experience. You can find [more details about this particular issue on MDN](https://developer.mozilla.org/en-US/docs/Web/Media/images/aspect_ratio_mapping).

Also, speaking about useful articles: take a look at a [handy article about the aspect-ratio unit](https://www.smashingmagazine.com/2019/03/aspect-ratio-unit-css/) here on Smashing Magazine, written by Rachel Andrew &mdash; I highly recommend you to read it.

### Resources

- [Old, trusty padding hack](https://piccalil.li/tutorial/build-a-responsive-media-browser-with-css#heading-responsive-video-player)
- [Article using the padding hack to create an aspect-ratio utility](https://piccalil.li/tutorial/creating-an-aspect-ratio-css-utility)
- [Browser support for `aspect-ratio`](https://caniuse.com/mdn-css_properties_aspect-ratio)

## Content-Visibility And `contain-intrinsic-size`

The last one on our tour is content visibility and how it can give us a huge performance boost. Because CSS lets you pretty much do *anything*, a browser has to calculate *everything* to render one single element. If you have a huge, complex page, it can result in some reasonably sluggish render and paint times.

The new `content-visibility` and `contain-intrinsic-size` properties have arrived to help this and they are *great*.

With `content-visibility: auto`, you can tell the browser not to worry about rendering the elements in there while they are **outside of the viewport**, which can have a massive impact on initial loading speeds. The only problem is that the element with `content-visibility: auto` set on it loses its height, so we set `contain-intrinsic-size` to something like `0 400px` to **hint** at what sort of size the element **will be** when it’s loaded.

These properties allow the browser to skip the initial rendering and instead, as the elements with `content-visibility: auto` set on them scroll near the viewport, the browser will start to render them. Proper progressive loading!

This video by Jake Archibald demos it really well:

{{< rimg breakout="true" href="https://www.youtube.com/watch?v=Z6wjUOSh9Tk" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/539ffdf6-24b7-4111-b012-287fdf2b661a/jake-archibald-beyond-fast-chrome-dev-summit-2020.png" with="800" height="500" sizes="100vw" caption="A <a href='https://www.youtube.com/watch?v=Z6wjUOSh9Tk'>talk by Jake Archibald</a> explaining some of the useful CSS features that were released in Chrome recently. Notably, <code>content-visibility</code>." alt="Jake Archibald gives a whirlwind tour in a video presenting the new features and proposals to help users improve the performance of their pages" >}}

You can also [read this great article, too](https://web.dev/content-visibility/).

### Resources

- [Content-visibility on web.dev](https://web.dev/content-visibility/)
- [Another video explaining what happens under the hood](https://www.youtube.com/watch?v=FFA-v-CIxJQ)
- [A handy article with some useful notes to know about `content-visibility`](https://css-tricks.com/more-on-content-visibility/)

## Wrapping Up And What’s Coming Up

That’s a pretty cool new CSS, right? There’s loads more arriving soon and loads in the long-term pipeline too. We can look forward to [Media Queries Level 5](https://www.w3.org/TR/mediaqueries-5/) which let us target the current ambient light level and whether or not the user prefers reduced data.

We’ve also got [CSS Nesting in draft](https://drafts.csswg.org/css-nesting-1/), which will give us Sass-like nesting capabilities like this:

<pre><code class="language-css">.my-element {
    background: red;

    & p {
        background: yellow;
    }
}</code></pre>

We’re getting even more control too, with [font metrics override descriptors](https://gist.github.com/xiaochengh/da1fa52648d6184fd8022d7134c168c1) and [Cascade Level 5](https://www.w3.org/TR/css-cascade-5/), which introduces layers to the cascade. [Prototyping is happening with container queries too](https://groups.google.com/a/chromium.org/g/blink-dev/c/u1AKdrXhPGI/m/wrJb-unhAgAJ?pli=1)!

Lastly, there are some cool new tricks on the horizon, like [scroll-linked animations](https://twitter.com/argyleink/status/1349051923912036355), which will open the door wide-open to a new generation of creative work on the web.

In conclusion, the present and future of CSS are very bright indeed and if you take a pragmatic, progressive approach to your CSS: things will continue to get better and better on your projects too.

{{< signature "vf, yk, il" >}}
