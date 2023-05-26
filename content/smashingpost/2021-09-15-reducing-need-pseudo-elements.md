---
title: 'Reducing The Need For Pseudo-Elements'
slug: reducing-need-pseudo-elements
author: marcel-moreau
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c994e024-5695-4cf7-b9b6-dc589e547f19/reducing-need-pseudo-elements.jpg
date: 2021-09-15T10:00:00.000Z
summary: >-
  For years, pseudo-elements have faithfully helped front-end developers implement creative designs. While they still have an important place, we can now leave pseudo-elements behind in some scenarios, thanks to newer CSS properties.
description: >-
  For years, pseudo-elements have faithfully helped front-end developers implement creative designs. While they still have an important place, we can now leave pseudo-elements behind in some scenarios, thanks to newer CSS properties.
categories:
  - CSS
  - Tools
  - Techniques
---

Per the [W3C spec](https://www.w3.org/TR/selectors-4/#pseudo-element), “a pseudo-element represents an element not directly present in the document tree". They have been around since version 1 of the CSS specification, when [`::first-letter`](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-letter) and [`::first-line`](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-line) were introduced. The popular [`::before`](https://developer.mozilla.org/en-US/docs/Web/CSS/::before) and [`::after`](https://developer.mozilla.org/en-US/docs/Web/CSS/::after) pseudo-elements were added in version 2 &mdash; these represent content that does not exist in the source document at all. They can be thought of as two extra elements you can “tack onto” their originating element. When front-end developers hear “pseudo-elements”, we think of `::before` and `::after` more often than not, as we use them in various ways to add decorations to our elements.

There are additional pseudo-elements beyond these. They are listed in the spec across three categories: [typographic](https://www.w3.org/TR/css-pseudo-4/#typographic-pseudos), [highlight](https://www.w3.org/TR/css-pseudo-4/#highlight-pseudos), and [tree-abiding](https://www.w3.org/TR/css-pseudo-4/#treelike).

Interestingly, after years of web development, I never found myself using `::first-line`, but it’s pretty neat and responds well to window resizing! Check it out.

{{< codepen height="480" theme_id="light" slug_hash="gORgXxN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [`::first-line`](https://codepen.io/smashingmag/pen/gORgXxN) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}

`::selection` is another pseudo-element many reach to. When a user highlights text, the highlight color will be a color that you specify.

{{< codepen height="480" theme_id="light" slug_hash="rNwjYGz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [`::selection`](https://codepen.io/smashingmag/pen/rNwjYGz) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}

<blockquote><strong>Quick Tip</strong><br /><br /><span style="font-style: normal">Pseudo-elements used one colon in versions 1 and 2 of the CSS spec, but have used two colons from version 3. This differentiates them from pseudo-classes, which describe an element’s state. Pseudo-classes use one colon. 
<ul>
  <li>Use two colons for pseudo-elements (e.g. <code>::before</code>, <code>::after</code>, <code>::marker</code>).</li>
  <li>Use one colon for pseudo-classes (e.g. <code>:hover</code>, <code>:focus</code>).</li>
</ul></span></blockquote>

## Pseudo-Elements Aren’t Always Needed

Pseudo-elements still have a place. This article is not “never use pseudo-elements” but rather “we no longer have to use pseudo-elements as much”. We can style a number of popular user interface elements without the need for pseudo-elements. By relying less on pseudo-elements, we can write less CSS, eliminate nested elements, ignore stacking context issues, and forget about positioning.

{{% feature-panel %}}

## Take Another Look At Trusted Techniques With New CSS Properties

For years, we waited patiently for browsers to adopt CSS technology faster. A turning point for many front-end developers came when some major players announced they would cease Internet Explorer (IE11) support: 

- All Microsoft 365 web apps stopped supporting IE11 on [August 21, 2021](https://techcommunity.microsoft.com/t5/microsoft-365-blog/microsoft-365-apps-say-farewell-to-internet-explorer-11-and/ba-p/1591666).
- Google Workspace (*Gmail*, *Calendar*, *Drive*, etc) stopped IE11 support on [March 15, 2021](https://workspaceupdates.googleblog.com/2020/12/ending-support-for-ie11-for-all-google-workspace.html).

This has allowed many of us to explore newer CSS technologies more freely: CSS Grid, `clamp()`, `background-blend-mode`, [and more](https://caniuse.com/?compare=ie+11,chrome+90&compareCats=CSS). The state of CSS property support is great. And with updatable browsers, support is accelerating.

## Bring On The Examples!

### Angled Buttons

Many front-end developers are familiar with using `::before` and `::after` pseudo-elements and CSS border rules to create shapes. There are many generator tools dedicated to this purpose &mdash; [this is one](https://codepen.io/yukulele/full/KLnhJ) that I have bookmarked. These tools guide you in choosing a shape (often triangles), giving you the proper CSS rules.

{{< vimeo id="595771763" caption="Angle buttons need to be able to handle word wrapping." breakout="true" >}}

These tools are life-savers when creating angled buttons. For angled buttons, they’re no longer necessary.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9180b600-6062-410f-ac44-44f11e67d0f4/angle-arrow-anatomy-01.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9180b600-6062-410f-ac44-44f11e67d0f4/angle-arrow-anatomy-01.png" width="800" height="464" sizes="100vw" caption="Angle buttons with pseudo-elements can require more HTML elements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9180b600-6062-410f-ac44-44f11e67d0f4/angle-arrow-anatomy-01.png'>Large preview</a>)" alt="Comparison of building-block pieces for angle buttons with pseudo-elements vs. without pseudo-elements" >}}

#### Pseudo-Element Version

Many of you reading this will be accustomed to a pseudo-element version:

- We use a relatively positioned wrapper element with large right padding to accommodate our angle &mdash; this is our `<button>`;
- Many of us, students of the [sliding doors technique](https://alistapart.com/article/slidingdoors/), are accustomed to nesting an element to take on the button’s background-color;
- Finally, we absolutely position a pseudo-element with its border rules into our `<button>`’s right padding empty space &mdash; we use `::before` for this.

Aside from those steps, our hover styles must account for both our nested element and pseudo-element. This might seem manageable for you, but the more complicated our button designs get, the more overhead we have with hover styles. Also, with this version, buttons with word wrapping just plain fail. 

{{< codepen height="480" theme_id="light" slug_hash="xxrgPpj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Button angle with pseudo-element](https://codepen.io/smashingmag/pen/xxrgPpj) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}

#### No Pseudo-Element Version

This is much easier without a pseudo-element. 

- We use one wrapper element &mdash; our `<button>`.
- We reach for the `clip-path` property to only show the parts of our button we want, using `calc()` along with a CSS custom property to size our angle &mdash; these sets of points correspond to top left, top right, middle right, bottom right, and bottom left: `polygon(0% 0%, calc(100% - var(--angle-width)) 0%, 100% 50%, calc(100% - var(--angle-width)) 100%, 0% 100%)`

In the CodePen example, you change the `--angle-width` custom property from `2rem` to another value to see our button’s angle adjust accordingly.

Our hover styles only need to account for one element &mdash; our button. Also, buttons with word wrapping act in a more graceful manner.

{{< codepen height="480" theme_id="light" slug_hash="PojWOQY" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Button angle with NO pseudo-element](https://codepen.io/smashingmag/pen/PojWOQY) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}

#### More Angled Button Styles In The Showcase

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef8ea684-c65f-4988-99a7-911b1a0e11a4/1-reducing-need-pseudo-elements.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef8ea684-c65f-4988-99a7-911b1a0e11a4/1-reducing-need-pseudo-elements.png" width="800" height="137" sizes="100vw" caption="The final showcase codepen has additional angle button examples. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef8ea684-c65f-4988-99a7-911b1a0e11a4/1-reducing-need-pseudo-elements.png'>Large preview</a>)" alt="Two additional angle buttons with more complex angles." >}}

Visit the [final showcase](https://codepen.io/smashingmag/pen/YzQNEeB) to see these other button styles made easier without pseudo-elements. In particular, the blue bevel button’s pseudo-element version is pretty brutal. The amount of overall work is greatly reduced thanks to `clip-path`.

{{% ad-panel-leaderboard %}}

### Button Wipes

A wiping effect is a popular button style. I’ve included left-to-right and top-to-bottom wipes. 

{{< vimeo id="595779353" caption="Sometimes, a wiping effect is desired." breakout="true" >}}

#### Pseudo-Element Version

This can be achieved by `transitioning` a pseudo-element’s `transform`. 

- We absolutely position a `::before` pseudo-element and give it a `transform: scaleX(0)` so it’s not visible.
- We also must explicitly set its `transform-origin: 0 0` to ensure the wipe comes in from the left rather than center ([`transform-origin` defaults to center](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin#formal_definition)).
- We set up `transitions` on the `transform` for some smooth jazz animation on/off hover.
- Because our pseudo-element is absolutely positioned, we require a nested element to hold the button’s text, `position: relative` on this nested element creates a new stacking context so our text stays on top of our wiping pseudo-element.
- On hover, we can target our pseudo-element and `transition` its `scaleX` to now be `1 (transform: scaleX(1))`.

{{< codepen height="480" theme_id="light" slug_hash="KKqayGW" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Button wipe with pseudo-element](https://codepen.io/smashingmag/pen/KKqayGW) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}

#### No Pseudo-Element Version

Why worry about nested elements, pseudo-element positioning, stacking contexts, and sprawling hover rules if we don’t have to? 

We can reach for `linear-gradient()` and `background-size` to nail this down.

- We give our `<button>` a `background-color` for its default state, while also setting up a `linear-gradient` via `background-image` &mdash; but the `background-size` will be `0`, so we won’t see anything by default.
- On hover, we transition the `background-size` to `100% 100%` which gives us our wipe effect!

Remember, `linear-gradient()` uses the `background-image` property and `background-image` supersedes `background-color`, so this is what takes precedence on hover.

That’s it. *No nested element required.* Want a vertical wipe? Just change the `linear-gradient` direction and the `background-size` values. I’ve changed those via CSS custom properties.

{{< codepen height="480" theme_id="light" slug_hash="MWoJOVo" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Button wipe with NO pseudo-element](https://codepen.io/smashingmag/pen/MWoJOVo) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}


### Tiles With Screen Color Overlays

{{< vimeo id="595785378" caption="Tiles often contain a background-image, color overlay, and text content." breakout="true" >}}

This is a common pattern where a semi-transparent color overlays a tile/card. Our example’s tile also has a background-image. It’s often important in this pattern to retain a set aspect-ratio so that tiles look uniform if more than one appears in a set.

#### Pseudo Version

Some of the same things come into play with our pseudo-element version:

- We use the [aspect-ratio “padding-trick”](https://alistapart.com/article/creating-intrinsic-ratios-for-video/), setting a 60% padding-top value (5:3 ratio) for our tile.
- We must position our screen color overlay pseudo-element, giving it a 100% `width` and `height` to fill the tile &mdash; we target this pseudo-element on hover to change its `background-color`.
- Due to the pseudo-element’s absolute positioning, we must use a nested element for our text content, also giving it `position: absolute` in order for it to appear *above* our screen color overlay in the stacking order and to ensure it appears where it should within the tile.

{{< codepen height="480" theme_id="light" slug_hash="YzQNEOM" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Tile screen color overlay with pseudo-element](https://codepen.io/smashingmag/pen/YzQNEOM) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}

#### No Pseudo-Element Version

It can be much simpler thanks to the [aspect-ratio](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio) and [background-blend-mode](https://developer.mozilla.org/en-US/docs/Web/CSS/background-blend-mode) properties.

**Note**: `aspect-ratio` does not work in Safari 14.x, but will in version 15. 

That said, as of this writing, [caniuse lists it](https://caniuse.com/?search=aspect-ratio) with 70%+ global support.

- The “padding-trick” is replaced by `aspect-ratio: 400/240` (we could use any 5:3-based value here).
- We use both `background-image` and `background-color` properties in conjunction with `background-blend-mode` &mdash; simply change the `background-color` of our tile element on hover.

{{% ad-panel-leaderboard %}}

##### `Background-blend-mode`

`background-blend-mode` blends a `background-color` with an element’s `background-image`. Any Photoshop users reading this will find `background-blend-mode` reminiscent of Photoshop’s blending modes. Unlike [`mix-blend-mode`](https://developer.mozilla.org/en-US/docs/Web/CSS/mix-blend-mode), `background-blend-mode` does not create a new stacking context! So no `z-index` hell!

{{< vimeo id="595806290" caption="CSS now provides Photoshop-like effects." breakout="true" >}}

{{< codepen height="480" theme_id="light" slug_hash="mdwRqjN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Tile screen color overlay with NO pseudo-element](https://codepen.io/smashingmag/pen/mdwRqjN) by <a href="https://codepen.io/marcelmoreau">Marcel</a>.{{< /codepen >}}

- You can find the [full showcase demo here&nbsp;&rarr;](https://codepen.io/smashingmag/pen/YzQNEeB)

## Conclusion

Front-end development is exciting and fast-moving. With newer CSS properties, we can brush the dust off our old techniques and give them another look. Doing this helps foster reduced and simpler code. Pseudo-elements are helpful, but we don’t need to reach for them as much. 

{{< signature "vf, yk, il" >}}
