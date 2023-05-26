---
title: 'A Guide To Newly Supported, Modern CSS Pseudo-Class Selectors'
slug: guide-supported-modern-css-pseudo-class-selectors
author: stephanie-eckles
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17ca589e-3e26-4648-a27c-5228ff0e5852/guide-supported-modern-css-pseudo-class-selectors.jpg
date: 2021-04-23T08:30:00.000Z
summary: >-
  The CSS Working Group Editor’s Draft for [Selectors Level 4](https://drafts.csswg.org/selectors-4/) includes several pseudo-class selectors that already have proposal candidates in most modern browsers. This guide will cover ones that currently have the best support along with examples to demonstrate how you can start using them today!
description: >-
  The CSS Working Group Editor’s Draft for [Selectors Level 4](https://drafts.csswg.org/selectors-4/) includes several pseudo-class selectors that already have proposal candidates in most modern browsers. This guide will cover ones that currently have the best support along with examples to demonstrate how you can start using them today!
categories:
  - CSS
  - Guides
  - Browsers
  - Accessibility
---

Pseudo-class selectors are the ones that begin with the colon character “`:`” and match based on a *state* of the current element. The state may be relative to the document tree, or in response to a change of state such as `:hover` or `:checked`.

## `:any-link`

Although [defined in Selectors Level 4](https://drafts.csswg.org/selectors-4/#the-any-link-pseudo), this pseudo-class has had [cross-browser support](https://caniuse.com/css-any-link) for quite some time. The `any-link` pseudo-class will match an anchor hyperlink as long as it has a `href`. It will match in a way equivalent to matching both `:link` and `:visited` at once. Essentially, this may reduce your styles by one selector if you are adding basic properties such as `color` that you’d like to apply to all links regardless of their visited status.

<pre><code class="language-css">:any-link {
  color: blue;
  text-underline-offset: 0.05em;
}
</code></pre>

An important note about specificity is that `:any-link` will win against `a` as a selector even if `a` is placed lower in the cascade since it has the specificity of a class. In the following example, the links will be purple:

<pre><code class="language-css">:any-link {
  color: purple;
}

a {
  color: red;
}
</code></pre>

So if you introduce `:any-link`, be aware that you will need to include it on instances of `a` as a selector if they will be in direct competition for specificity.

## `:focus-visible`

I’d bet that one of the most common accessibility violations across the web is removing `outline` on interactive elements like links, buttons, and form inputs for their `:focus` state. One of the main purposes of that `outline` is to serve as a visual indicator for users who primarily use keyboards to navigate. **A visible focus state is critical** as a way-finding tool as those users tab across an interface and to help reinforce what is an interactive element. Specifically, the visible focus is covered in the [WCAG Success Criterion 2.4.11: Focus Appearance (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance-minimum.html).

The `:focus-visible` pseudo-class is intended to only show a focus ring when the user agent determines via heuristics that it should be visible. Put another way: **browsers will determine** when to apply `:focus-visible` based on things like input method, type of element, and context of the interaction. For testing purposes via a desktop computer with keyboard and mouse input, you should see `:focus-visible` styles attached when you tab into an interactive element but not when you click it, with the exception of text inputs and textareas which should show `:focus-visible` for all focus input types.

**Note**: *For more details, review [the working draft of the](https://drafts.csswg.org/selectors-4/#the-focus-visible-pseudo) [`:focus-visible` spec](https://drafts.csswg.org/selectors-4/#the-focus-visible-pseudo).*

The latest versions of Firefox and Chromium browsers seem to now be handling `:focus-visible` on form inputs according to the spec which says that the UA should remove `:focus` styles when `:focus-visible` matches. Safari is not yet supporting `:focus-visible` so we need to ensure a `:focus` style is included as a fallback to avoid removing the `outline` for accessibility.

{{% feature-panel %}}

Given a button and text input with the following set of styles, let’s see what happens:

<pre><code class="language-css">input:focus,
button:focus {
  outline: 2px solid blue;
  outline-offset: 0.25em;
}

input:focus-visible {
  outline: 2px solid transparent;
  border-color: blue;
}

button:focus:not(:focus-visible) {
  outline: none;
}

button:focus-visible {
  outline: 2px solid transparent;
  box-shadow: 0 0 0 2px #fff, 0 0 0 4px blue;
}
</code></pre>

### Chromium and Firefox

- `input`  
Correctly remove `:focus` styles when elements are focused via mouse input in favor of `:focus-visible` resulting in changing the `border-color` and hiding the `outline` on keyboard input
- `button`  
Does not only use `:focus-visible` without the extra rule for `button:focus:not(:focus-visible)` that removes the outline on `:focus`, but will allow visibility of the `box-shadow` only on keyboard input

### Safari

- `input`  
Continues using only the `:focus` styles
- `button`  
This *seems* to now be partially respecting the intent of `:focus-visible` on the button by hiding the `:focus` styles on click, but still showing the `:focus` styles on keyboard interaction

So for now, the recommendation would be to continue including `:focus` styles and then progressively enhance up to using `:focus-visible` which the demo code allows. Here’s a CodePen for you to continue testing with:

{{< codepen height="480" theme_id="light" slug_hash="MWJZbew" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Testing application of :focus-visible](https://codepen.io/smashingmag/pen/MWJZbew) by <a href="https://codepen.io/5t3ph">Stephanie Eckles</a>.{{< /codepen >}}

## `:focus-within`

The `:focus-within` pseudo-class has support among all modern browsers, and acts *almost* like a parent selector but only for a very specific condition. When attached to a containing element and a child element matches for `:focus`, styles can be added to the containing element *and/or* any other elements within the container.

A practical enhancement to use this behavior for is **styling a form label** when the associated input has focus. For this to work, we wrap the label and input in a container, and then attach `:focus-within` to that container as well as selecting the label:

<pre><code class="language-css">.form-group:focus-within label {
  color: blue;
}
</code></pre>

This results in the label turning blue when the input has focus.

This CodePen demo also includes adding an outline directly to the `.form-group` container:

{{< codepen height="480" theme_id="light" slug_hash="xxgmREq" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Testing application of :focus-within](https://codepen.io/smashingmag/pen/xxgmREq) by <a href="https://codepen.io/5t3ph">Stephanie Eckles</a>.{{< /codepen >}}

## `:is()`

Also known as the “matches any” pseudo-class, `:is()` can take a list of selectors to try to match against. For example, instead of listing heading styles individually, you can group them under the selector of `:is(h1, h2, h3)`.

A couple of unique behaviors about the  `:is()`  selector list:

- If a listed selector is invalid, the rule will continue to match the valid selectors. Given `:is(-ua-invalid, article, p)` the rule will match `article` and `p`.
- The computed specificity will equal that of the passed selector with the highest specificity. For example,  `:is(#id, p)` will have the specificity of the `#id` &mdash; 1.0.0 &mdash; whereas `:is(p, a)` will have a specificity of 0.0.1.

The first behavior of ignoring invalid selectors is a key benefit. When using other selectors in a group where one selector is invalid, the browser will throw out the whole rule. This comes into play for a few instances where vendor prefixes are still necessary, and grouping prefixed and non-prefixed selectors causes the rule to fail among all browsers. With `:is()` you can safely group those styles and they will apply when they match and be ignored when they don’t.

To me, **grouping heading styles** as previously mentioned is already a big win with this selector. It’s also the type of rule that I would feel comfortable using without a fallback when applying non-critical styles, such as:

<pre><code class="language-css">:is(h1, h2, h3) {
  line-height: 1.2;
}

:is(h2, h3):not(:first-child) {
  margin-top: 2em;
}
</code></pre>

In this example (which comes from [the document styles in my project SmolCSS](https://smolcss.dev/#smol-document-styles)), having the greater `line-height` inherited from base styles or lacking the `margin-top` is not really a problem for non-supporting browsers. It’s simply less than ideal. What you wouldn’t want to use `:is()` for quite yet would be **critical layout styles** such as Grid or Flex that significantly control your interface.

Additionally, when chained to another selector, you can test whether the base selector matches a descendent selector within `:is()`. For example, the following rule selects only paragraphs that are direct descendants of articles. The universal selector is being used as a reference to the `p` base selector.

<pre><code class="language-css">p:is(article > *)
</code></pre>

For the [best current support](https://caniuse.com/css-matches-pseudo), if you’d like to start using it you’ll also want to **double-up on styles** by including duplicate rules using `:-webkit-any()` and `:matches()`. Remember to make these individual rules, or even the supporting browser will throw it out! In other words, include all of the following:

<pre><code class="language-css">:matches(h1, h2, h3) { }

:-webkit-any(h1, h2, h3) { }

:is(h1, h2, h3) { }
</code></pre>

Worth mentioning at this point is that along with the newer selectors themselves is an updated variation of `@supports` which is `@supports selector`. This is also available as `@supports not selector`.

**Note**: *At present (of the modern browsers), only Safari does not support this at-rule.*

You could check for `:is()` support with something like the following, but you’d actually be losing out on supporting Safari since Safari supports `:is()` but doesn’t support `@supports selector`.

<pre><code class="language-css">@supports selector(:is(h1)) {
  :is(h1, h2, h3) {
    line-height: 1.1;
  }
}
</code></pre>

{{% ad-panel-leaderboard %}}

## `:where()`

The pseudo-class `:where()` is almost identical to `:is()` except for one critical difference: it will *always* have zero-specificity. This has incredible implications for **folks who are building frameworks, themes, and design systems**. Using `:where()`, an author can set defaults and downstream developers can include overrides or extensions without specificity clashing.

Consider the following set of `img`  styles. Using `:where()`, even with a higher specificity selector, the specificity remains zero. In the following example, which color border do you think the image will have?

<pre><code class="language-css">:where(article img:not(:first-child)) {
    border: 5px solid red;
}

:where(article) img {
  border: 5px solid green;
}

img {
  border: 5px solid orange;
}
</code></pre>

The first rule has zero specificity since its wholly contained within `:where()`. So directly against the second rule, the second rule wins. Introducing the `img` element-only selector as the last rule, it’s going to win due to the cascade. This is because it will compute to the same specificity as the `:where(article) img` rule since the `:where()` portion does not increase specificity.

Using `:where()` alongside fallbacks is a little more difficult due to the zero-specificity feature since that feature is likely why you would *want* to use it over `:is()`. And if you add fallback rules, those are likely to beat `:where()` due to its very nature. And, it has **better overall support** than the `@supports selector` so trying to use that to craft a fallback isn’t likely to provide much (if any) of a gain. Basically, be aware of the inability to correctly create fallbacks for `:where()` and carefully check your own data to determine if it’s safe to begin using for your unique audience.

You can further test `:where()` with the following CodePen that uses the `img` selectors from above:

{{< codepen height="480" theme_id="light" slug_hash="jOyXVMg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Testing `:where()` specificity](https://codepen.io/smashingmag/pen/jOyXVMg) by <a href="https://codepen.io/5t3ph">Stephanie Eckles</a>.{{< /codepen >}}

## Enhanced `:not()`

The base `:not()` selector has been supported since Internet Explorer 9. But Selectors Level 4 enhances `:not()` by allowing it to take a selector list, just like `:is()` and `:where()`.

The following rules provide the same result in supporting browsers:

<pre><code class="language-css">article :not(h2):not(h3):not(h4) {
  margin-bottom: 1.5em;
}

article :not(h2, h3, h4) {
  margin-bottom: 1.5em;
}
</code></pre>

The ability of `:not()` to accept a selector list [has great modern browser support](https://caniuse.com/css-not-sel-list). 

As we saw with `:is()`, enhanced `:not()` can also contain a reference to the base selector as a descendent using `*`. This CodePen demonstrates this ability by selecting links that are *not* descendants of `nav`.

{{< codepen height="480" theme_id="light" slug_hash="BapvQQv" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Testing :not() with a descendent selector](https://codepen.io/smashingmag/pen/BapvQQv) by <a href="https://codepen.io/5t3ph">Stephanie Eckles</a>.{{< /codepen >}}

**Bonus**: The previous demo also includes an example of chaining `:not()` and `:is()` to select images that are not adjacent siblings of either `h2` or `h3` elements.

## Proposed but “at risk” &mdash; `:has()`

The final pseudo-class that is a very exciting proposal but has no current browser implementing it even in an experimental way is `:has()`. In fact, it is listed in the [Selector Level 4 Editor’s Draft](https://drafts.csswg.org/selectors-4/#has-pseudo) as “at-risk” which means that it is recognized to have difficulties in completing its implementation and so it *may* be dropped from the recommendation.

If implemented, `:has()` would essentially be the “parent selector” that many CSS folks have longed to have available. It would work with logic similar to a combination of both `:focus-within` and `:is()` with descendent selectors, where you are looking for the **presence of descendants** but the applied styling would be to the parent element.

Given the following rule, if navigation contained a button, then the navigation would have decreased top and bottom padding:

<pre><code class="language-css">nav {
  padding: 0.75rem 0.25rem;

nav:has(button) {
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
}
</code></pre>

Again, this is *not* currently implemented in any browser even experimentally &mdash; but it is fun to think about! Robin Rendle provided [additional insights into this future selector](https://css-tricks.com/did-you-know-about-the-has-css-selector/) over on CSS-Tricks.

{{% ad-panel-leaderboard %}}

## Honorable Mention from Level 3: `:empty`

A useful pseudo-class you may have missed from Selectors Level 3 is `:empty` which matches an element when it has *no* child elements, including text nodes. 

The rule `p:empty` will match `<p></p>` but not `<p>Hello</p>`.

One way you can use `:empty` is to hide elements that are perhaps placeholders for dynamic content that is populated with JavaScript. Perhaps you have a div that will receive search results, and when it’s populated it will have a border and some padding. But with no results yet, you don’t want it to take up space on the page. Using `:empty` you can hide it with:

<pre><code class="language-css">.search-results:empty {
  display: none;
}
</code></pre>

You may be thinking about adding a message in the empty state and be tempted to add it with a pseudo-element and `content`. The pitfall here is that messages may not be available to users of assistive technology which are inconsistent on whether they can access `content`. In other words, to **make sure a “no results” type of message is accessible**, you would want to add that as a real element like a paragraph (an `aria-label` would no longer be accessible for a hidden div).

### Resources for Learning About Selectors

CSS has many more selectors inclusive of pseudo-classes. Here are a few more places to learn more about what’s available:

- [MDN CSS selectors documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors) includes a comprehensive categorized list;
- I’ve written a two-part guide to advanced CSS selectors, you can [start with part one](https://moderncss.dev/guide-to-advanced-css-selectors-part-one/);
- Have fun learning about CSS selectors with the game [CSS Diner](https://flukeout.github.io/);
- Kitty Giraudel created a [selector explanation tool](https://kittygiraudel.github.io/selectors-explained/) that will break down and describe parts of a provided selector.

{{< signature "vf, il" >}}
