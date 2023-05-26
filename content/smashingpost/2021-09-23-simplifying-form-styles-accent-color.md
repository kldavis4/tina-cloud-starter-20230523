---
title: 'Simplifying Form Styles With `accent-color`'
slug: simplifying-form-styles-accent-color
author: michelle-barker
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/195a9e83-5686-47fd-80d9-3c1d6dc4655a/simplifying-form-styles-accent-color.jpg
date: 2021-09-23T11:00:00.000Z
summary: >-
  The new CSS `accent-color` property makes it quick and easy to roll out our brand colors to certain form inputs by leveraging user agent styles. In this article we’ll take a look at what it does and how to use it alongside `color-scheme` for simple, accessible checkboxes and radio buttons &mdash; and imagine how we might use it in the future.
description: >-
  The new CSS `accent-color` property makes it quick and easy to roll out our brand colors to certain form inputs by leveraging user agent styles. In this article we’ll take a look at what it does and how to use it alongside `color-scheme` for simple, accessible checkboxes and radio buttons &mdash; and imagine how we might use it in the future.
categories:
  - CSS
  - Tools
  - Browsers
  - Accessibility
---

I don’t know about you, but I love it when new CSS properties arrive that make our daily lives as developers simpler and enable us to remove a whole lot of redundant code. `aspect-ratio` is one such property (recently eliminating the need for the [padding hack](https://css-tricks.com/aspect-ratio-boxes/)). `accent-color` just might be the next.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/670a7ef5-7695-42fb-b7dd-eca523c5020b/1-simplifying-form-styles-accent-color.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/670a7ef5-7695-42fb-b7dd-eca523c5020b/1-simplifying-form-styles-accent-color.jpg" width="800" height="441" sizes="100vw" caption="Checkboxes with <code>accent-color</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/670a7ef5-7695-42fb-b7dd-eca523c5020b/1-simplifying-form-styles-accent-color.jpg'>Large preview</a>)" alt="Multi-colored checkboxes on a dark background" >}}

## Styling Form Inputs

Let’s take checkboxes. In every browser, these are styled differently by the user agent stylesheet (responsible for the browser’s default styles).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a25eeddc-f485-44e4-b4db-fa0d259915f3/2-simplifying-form-styles-accent-color.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a25eeddc-f485-44e4-b4db-fa0d259915f3/2-simplifying-form-styles-accent-color.jpg" width="800" height="450" sizes="100vw" caption="Default checkbox styles in Chrome (top) and Safari (bottom). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a25eeddc-f485-44e4-b4db-fa0d259915f3/2-simplifying-form-styles-accent-color.jpg'>Large preview</a>)" alt="Screenshots of default checkboxes in Chrome and Safari. The Safari ones are smaller and lighter in color." >}}

Historically there hasn’t been any real way to style these inputs. Instead, many web developers resort to a well-known hack, which involves visually (but accessibly) hiding the input itself, then styling a pseudo-element on the label. (All this applies to radio buttons too.)

{{< codepen height="480" theme_id="light" slug_hash="QWgrrKp" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Old skool custom checkbox styling](https://codepen.io/smashingmag/pen/QWgrrKp) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

This is actually less verbose than past solutions. [ModernCSS](https://moderncss.dev/pure-css-custom-styled-radio-buttons) has a detailed tutorial on how to implement custom checkboxes and radio buttons using this technique.

This technique works cross-browser, and will still be necessary if checkboxes need to be fully custom (with animations, and so on). But in many cases we don’t need any fancy styling &mdash; we simply need to be able to apply a brand color and move on. Wouldn’t it be great to get rid of all that clunky CSS? Enter `accent-color`!

## Simple Use

For the simplest use case, we can set the `accent-color` property on the `:root` element and have it apply everywhere on our webpage:

<pre><code class="language-css">:root {
  accent-color: rgba(250, 15, 117);
}</code></pre>

This applies the chosen color to (at the time of writing) checkboxes, radio buttons, range and progress elements.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a05ed1bd-3b32-47b6-bc18-2496172f807e/3-simplifying-form-styles-accent-color.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a05ed1bd-3b32-47b6-bc18-2496172f807e/3-simplifying-form-styles-accent-color.jpg" width="800" height="450" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a05ed1bd-3b32-47b6-bc18-2496172f807e/3-simplifying-form-styles-accent-color.jpg'>Large preview</a>)" alt="Form with checkboxes, radio buttons, progress bar and range input, with lime accent color applied." >}}

### Accessibility

A pretty cool feature is that the browser will automatically determine the best color for the checkmark to ensure sufficient color contrast, using its own internal algorithms. That means no extra code styling is required to ensure our checkboxes are as accessible as they can be.

In the following demo, we’re applying two different accent colors. If you view this in Chrome, you should see that the checkmark of the one on the left is white, while the one on the right is black. Browsers use different algorithms for this, so you may experience different results in Chrome versus Firefox.

{{< codepen height="480" theme_id="light" slug_hash="jOwxxVm" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [accent-color – showing two different colours](https://codepen.io/smashingmag/pen/jOwxxVm) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

{{% feature-panel %}}

## Custom Properties

If we want to apply the same color to other UI elements, we could use a custom property. We can set our color as a custom property on the root element, then apply it to (for example) headings, or other form elements:

<pre><code class="language-css">:root {
  --brand: rgba(250, 15, 117);
  accent-color: var(--brand);
}</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="YzQLLpm" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [accent-color with custom property](https://codepen.io/smashingmag/pen/YzQLLpm) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

We can even create some fun effects. In the following demo, we’re assigning each checkbox group a custom property that corresponds to the element’s index (`--i`) using the `style` attribute in the HTML. Then we’re using it in our CSS to calculate the hue value in an HSL color function to determine the accent color. Rainbow checkboxes!

{{< codepen height="480" theme_id="light" slug_hash="mdqQyzv" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [accent-color w/custom properties](https://codepen.io/smashingmag/pen/mdqQyzv) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

### Other Form Elements

Unfortunately `accent-color` isn’t applied to other elements that we might expect, like select dropdowns. We might want to apply our chosen color to already-styleable form elements, like buttons and text inputs too. The custom property comes in useful here, as we can apply it to the border of our text inputs, and the background of buttons, for example:

{{< codepen height="480" theme_id="light" slug_hash="VwWxxPJ" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [accent-color with custom property](https://codepen.io/smashingmag/pen/VwWxxPJ) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

The [Web.dev documentation](https://web.dev/accent-color/) on `accent-color` includes this handy snippet by Adam Argyle for styling other elements not exclusive to forms, including list markers, text selection highlights and the focus ring:

<pre><code class="language-css">html { 
  --brand: hotpink;
  scrollbar-color: hotpink Canvas;
}

:root { accent-color: var(--brand); }
:focus-visible { outline-color: var(--brand); }
::selection { background-color: var(--brand); }
::marker { color: var(--brand); }

:is(
  ::-webkit-calendar-picker-indicator,
  ::-webkit-clear-button,
  ::-webkit-inner-spin-button, 
  ::-webkit-outer-spin-button
) {
  color: var(--brand);
}</code></pre>

{{% ad-panel-leaderboard %}}

## Color Schemes

To tailor our form elements further, the `color-scheme` property can assist us with styling them according to the user’s preference for light or dark mode. At the moment, we can provide dark mode styles according to the user’s system preferences with the `prefers-color-scheme` media query:

<pre><code class="language-css">/* 
    If the user's preference is set to 'dark', this renders white text on a black background
*/
@media (prefers-color-scheme: dark) {
  body {
    background-color: #000000;
    color: #ffffff;
  }
}</code></pre>

If we leave it at that, our checkboxes will still have a light background in their unchecked state.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a85843d-9026-437c-865c-2768db25480b/4-simplifying-form-styles-accent-color.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a85843d-9026-437c-865c-2768db25480b/4-simplifying-form-styles-accent-color.jpg" width="800" height="450" sizes="100vw" caption="Despite the light background of the page, the checkboxes have a light background by default. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a85843d-9026-437c-865c-2768db25480b/4-simplifying-form-styles-accent-color.jpg'>Large preview</a>)" alt="Checkboxes on a dark background" >}}

We can use `color-scheme` to ensure that our checkboxes take on a light or dark style according to preference. Setting it on the root element in our CSS ensures that it applies to the whole page:

<pre><code class="language-css">:root {
  color-scheme: light dark;
}</code></pre>

This expresses the color schemes in order of preference. Alternatively we could implement it using a meta tag in our HTML:

<pre><code class="language-html">&lt;meta name="color-scheme" content="light dark"&gt;</code></pre>

This is actually preferable, as it will be read by the browser immediately before the CSS file is parsed and executed &mdash; therefore could help us avoid a flash of unstyled content (FOUC).

In our rainbow checkbox demo, you might notice that the browser also adjusts the color of some of the checkmarks when we switch the color scheme, while still maintaining sufficient contrast. Pretty cool!

{{< vimeo id="607320608" breakout="true" >}}

`color-scheme` affects the user agent styles. If we use it without providing other background color or text color styles for the page, the default colors of the page will be inverted if the user selects a dark color scheme &mdash; so the default background color will be black, and the text color will be white. In practice, it’s quite likely we’ll want to override these with CSS. We can use `color-scheme` alongside the `prefers-color-scheme` media query. In this demo, I’m using `prefers-color-scheme` to set the text color only when a dark scheme is preferred.

{{< codepen height="480" theme_id="light" slug_hash="podQvQb" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [accent-color with color-scheme](https://codepen.io/smashingmag/pen/podQvQb) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

`color-scheme` can also be set on individual elements, which is useful if there are some areas in our design that we want to retain a specified color scheme, regardless of whether light or dark mode is toggled. In this demo, we have a form with a dark background even when the overall color scheme is light. We can specify a dark color scheme, to ensure our checkboxes are styled with a dark color at all times:

<pre><code class="language-css">.dark-form {
  color-scheme: dark;
}</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="JjJvvWw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [accent-color – showing two different colours](https://codepen.io/smashingmag/pen/JjJvvWw) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

{{% ad-panel-leaderboard %}}

## Limitations

As mentioned, there are several elements that are not currently affected by `accent-color`, for which this functionality would be useful. Another consideration is that we’re currently limited to only styling the checked state of the checkbox or radio button &mdash; aside from using `color-scheme`, which has some effect on the checkbox border, but doesn’t allow for full customization. It would be great to be able to style the border color and thickness for the input in its unchecked state or implement even more custom styling, such as changing the overall shape, but we’re not quite there yet. At the very least, allowing the checkbox border to inherit the body text color would be preferable.

It would also be useful to be able to extend the use of `accent-color` to other elements beyond forms, such as video controls. Currently for a developer to create custom controls entails a significant amount of work in order to re-create the accessibility of native ones. [This excellent article](https://www.smashingmagazine.com/2020/11/standardizing-select-native-html-form-controls/) by Stephanie Stimac details the work being done by [Open UI](https://open-ui.org) to standardize UI elements in order to make it easier for developers to style them.

## Alternatives

An alternative way to style a checkbox or radio button is to hide default styling with `-webkit-appearance: none` and replace it with a background image. (See [this demo](https://codepen.io/smashingmag/pen/ZEyooKx).) Modern browsers support this pretty well, but it has its limitations when compared to the first method of using a pseudo-element (described at the start of this article), as we can’t directly manipulate the background image with CSS (e.g. changing its color or opacity), or transition the image.

The CSS Paint API &mdash; part of the Houdini set of CSS APIs &mdash; opens up more options for customization, allowing us to pass in custom properties to manipulate a background image. Check out [this lovely demo](https://css-houdini.rocks/checkboxes/) (and accompanying worklet) by Matteo. Support is currently limited to Chromium browsers.

### Accessibility

We should take care to provide accessible focus styles when using hiding the default appearance of form controls. An advantage of `accent-color` is that it doesn’t hide the browser defaults, preserving accessibility.

## Browser Support

`accent-color` is currently supported in the latest versions of Chrome and Edge. It can be enabled in Firefox with the `layout.css.accent-color.enabled` flag, and is due to be supported in the next release. Unfortunately, there is no Safari support at present. That’s not to say you *can’t* start using it right away &mdash; browsers that don’t support `accent-color` will simply get the browser defaults, so it works great as progressive enhancement.

## Conclusion

We’ve mostly talked about checkboxes and radio buttons here, as they’re among the most common form elements requiring customization. But `accent-color` has the potential to provide quick and easy styling for many of our form elements, especially where extensive customization isn’t needed, as well as allowing the browser to pick the best options for accessibility.

### Further Reading

Some resources on `accent-color`, `color-scheme`, and styling form inputs:

- [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/accent-color)
- [CSS Tricks guide to accent-color](https://css-tricks.com/almanac/properties/a/accent-color/:)
- Web.dev: [CSS accent-color](https://web.dev/accent-color)
- Web.dev: [Improved dark mode with color-scheme](https://web.dev/color-scheme/)
- Modern CSS: [Custom CSS Styles for Form Inputs and Text Areas](https://moderncss.dev/custom-css-styles-for-form-inputs-and-textareas/)
- Modern CSS: [Pure CSS Custom Styled Radio Buttons](https://moderncss.dev/pure-css-custom-styled-radio-buttons/)

{{< signature "vf, yk, il" >}}
