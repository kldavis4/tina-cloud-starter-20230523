---
title: 'How To Configure Application Color Schemes With CSS Custom Properties'
slug: application-color-schemes-css-custom-properties
author: artur-basak
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f742cac-ca4a-4df3-8438-e8bc472e209a/application-color-schemes-css-custom-properties.png
date: 2020-08-11T10:00:00.000Z
summary: >-
  In this article,  Artur Basak introduces a modern approach on how to set up CSS Custom Properties that respond to the application colors. The idea of dividing colors into three levels can be quite useful: a palette (or scheme), functional colors (or theme), and component colors (local scope).
description: >-
 In this article,  Artur Basak introduces a modern approach on how to set up CSS Custom Properties that respond to the application colors. The idea of dividing colors into three levels can be quite useful: a palette (or scheme), functional colors (or theme), and component colors (local scope).
categories:
  - CSS
  - Techniques
---

Variables are a basic tool that help organize colors on a project. For a long time, front-end engineers used preprocessor variables to configure colors on a project. But now, many developers prefer the modern native mechanism for organizing color variables: [CSS Custom Properties](https://drafts.csswg.org/css-variables/). Their most important advantage over preprocessor variables is that they work in realtime, not at the compilation stage of the project, and have support for the cascade model which allows you to use inheritance and redefinition of values on the fly. 

When you’re trying to organize an application color scheme, you can always place all custom properties that relate to color in the root section, name them, and use it in all needed places.

{{< codepen height="480" theme_id="light" slug_hash="RwaNqxW" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Custom Properties for Colors](https://codepen.io/smashingmag/pen/RwaNqxW) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

That’s an option, but does it help you to resolve issues of application theming, white labeling, a brand refresh, or organizing a light or dark mode? What if you need to adjust the color scheme to increase contrast? With the current approach, you will have to update each value in your variables.

In this article, I want to suggest a more flexible and resistant approach on how to split color variables using custom properties, which can solve many of these issues.

{{% feature-panel %}}

## Setup Color Palette

The coloring of any website begins with the setup of a color scheme. Such a scheme is based on the [color wheel](https://en.wikipedia.org/wiki/Color_wheel). Usually, only a few primary colors form the basis of a palette, the rest are derived colors &mdash; tones and mid-tones. Most often, the palette is static and does not change while the web application is running.

According to the [color theory](https://www.w3.org/wiki/Colour_theory), there are only a few options for color schemes:

- Monochromatic scheme (one primary color)
- Complementary scheme (two primary colors)
- Triad scheme (three primary colors)
- Tetradic scheme (four primary colors)
- Adjacent pattern (two or three primary colors)

For my example, I will generate a triad color scheme using the [Paletton](https://paletton.com/#uid=3000u0kllllaFw0g0qFqFg0w0aF) service:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58939fb2-146f-4771-bf1f-91af136d4c59/paletton-application-color-schemes-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58939fb2-146f-4771-bf1f-91af136d4c59/paletton-application-color-schemes-css-custom-properties.png" sizes="100vw" caption="Paletton Service: Triadic Color Scheme. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58939fb2-146f-4771-bf1f-91af136d4c59/paletton-application-color-schemes-css-custom-properties.png'>Large preview</a>)" alt="Color wheel with the established triadic scheme: variation of green, blue and red." >}}

I now have three main colors. On the basis of these, I will calculate the tones and mid-tones (the HSL format in combination with the [`calc`](https://developer.mozilla.org/en-US/docs/Web/CSS/calc) function is a very useful tool for this). By changing the lightness value, I can generate several additional colors for the palette.

{{< codepen height="480" theme_id="light" slug_hash="OJNPaQW" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [HSL Palette](https://codepen.io/smashingmag/pen/OJNPaQW) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

Now if the palette is modified, then it will be necessary to change only the value of the primary colors. The rest will be recalculated automatically.

If you prefer HEX or RGB formats, then it does not matter; a palette can be formed at the stage of compiling the project with the corresponding functions of the preprocessor (e.g. with SCSS and the [`color-adjust`](https://sass-lang.com/documentation/modules/color#adjust) function). As I’ve mentioned before, this layer is mostly static; it’s extremely rare that the palette may be changed in a running application. That’s why we can calculate it with preprocessors.

**Note**: *I recommend also generating both HEX literal and RGB for each color. This will allow playing with the alpha channel in the future.*

{{< codepen height="480" theme_id="light" slug_hash="oNxgQqv" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [SCSS Palette](https://codepen.io/smashingmag/pen/oNxgQqv) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

The palette level is the only level where the color is encoded directly in the variable names, i.e. we can uniquely identify the color by reading the name.

## Define Theme Or Functional Colors

Once the palette is done, the next step is the level of **functional colors**. At this level, the value of the color is not so important as its purpose, the function it performs, and what it exactly colorizes. For example, the primary or app brand color, border color, color of the text on a dark background, the color of the text on a light background, button background color, link color, hover link color, hint text color, and so on.

These are extremely common things for almost any website or application. We can say that such colors are responsible for a certain color theme of the application. Also, the values of such variables are taken strictly from the palette. Thus, we can easily change application themes by simply operating with different color palettes.

Below, I have created three typical UI controls: a button, a link, and an input field. They are colored using functional variables that contain values from the palette that I previously generated above. The main functional variable that is responsible for the application theme (conditional brand) is the primary color variable.

Using the three buttons at the top, you can switch themes (change the brand color for controls). The change occurs by using the appropriate [CSSOM API (setProperty)](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/setProperty).

{{< codepen height="480" theme_id="light" slug_hash="poyvQLL" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Functional Colors](https://codepen.io/smashingmag/pen/poyvQLL) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

This approach is convenient not only for theming but also for configuring individual web pages. For example, on the [zubry.by](https://zubry.by/stamps.html) website, I used a [common stylesheet](https://github.com/zubr-collection/zubr-collection.github.io/blob/master/assets/css/common.css) and a functional variable `--page-color` to colorize the logo, headings, controls, and text selection for all pages. And in [the own styles](https://github.com/zubr-collection/zubr-collection.github.io/blob/master/src/templates/stamps.hbs) of each page, I just redefined this variable to set the page its individual primary color.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f325c47-9912-46f7-a888-441de1571c55/zubryby-application-color-schemes-css-custom-properties.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f325c47-9912-46f7-a888-441de1571c55/zubryby-application-color-schemes-css-custom-properties.jpeg" sizes="100vw" caption="ZUBRY.BY website where each page has individual primary color. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f325c47-9912-46f7-a888-441de1571c55/zubryby-application-color-schemes-css-custom-properties.jpeg'>Large preview</a>)" alt="3 web pages of ZUBRY.BY website: stamps page, postcards page and cards page." >}}

{{% ad-panel-leaderboard %}}

## Use Component Colors

Large web projects always contain decomposition; we split everything into small components and reuse them in many places. Each component usually has its own style meaning it doesn’t matter what we used to decompose BEM or CSS Modules, or another approach; it’s important that each such piece of code can be called local scope and reused.

In general, I see the point in using color variables at the **component level** in two cases.

The first is when components that according to application style guide are repeated with different settings, e.g. buttons for different needs like primary (brand) button, secondary button, tertiary, and so on.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4e175d4-8868-4167-882b-3d8b165fce75/buttons-application-color-schemes-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4e175d4-8868-4167-882b-3d8b165fce75/buttons-application-color-schemes-css-custom-properties.png" sizes="100vw" caption="Tispr application styleguide. Buttons. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4e175d4-8868-4167-882b-3d8b165fce75/buttons-application-color-schemes-css-custom-properties.png'>Large preview</a>)" alt="Different button styles for Tispr application." >}}

The second is when components that have several states with different colors, e.g. button hover, active and focus states; normal and invalid states for input or select field, and so on.

A more rare case when component variables may come in handy is the functionality of a "white label". [The "white label"](https://en.wikipedia.org/wiki/White-label_product) is a service feature that allows the user to customize or brand some part of the user interface to improve the experience of interacting with their clients. For example, electronic documents that a user shares with his customers through a service or email templates. In this case, the variables at the component level will help to configure certain components separately from the rest of the color theme of the application.

In the example below, I’ve now added controls for customizing colors of the primary (brand) button. Using color variables of the component level we can configure UI controls separately from each other.

{{< codepen height="480" theme_id="light" slug_hash="LYNEXdw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Component Colors](https://codepen.io/smashingmag/pen/LYNEXdw) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

## How To Determine What Level A Variable Has?

I came across the question of how to understand what can be put in the root (theme or functional level), and what to leave at the level of a component. This is an excellent question that is difficult to answer without seeing the situation you are working with.

Unfortunately, the same approach as in programming does not work with colors and styles, if we see three identical pieces of code then we need to refactor it.

Color can be repeated from component to component, but this does not mean that it is a rule. There can be no relation between such components. For example, the border of the input field and the background of the primary button. Yes, in my example above that’s the case, but let’s check following example:

{{< codepen height="480" theme_id="light" slug_hash="YzqPRLX" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Color Split: Only Palette](https://codepen.io/smashingmag/pen/YzqPRLX) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

The dark gray color is repeated &mdash; this is the border of the input field, the fill color of the close icon, and the background of the secondary button. But these components are in no way connected with each other. If the border color of the input field changes, then we will not change the background of the secondary button. For such a case we must keep here just the variable from the palette.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acba0f8b-a698-4633-b0d4-eda05367ec8f/color-split-application-color-schemes-css-custom-propertiespng.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acba0f8b-a698-4633-b0d4-eda05367ec8f/color-split-application-color-schemes-css-custom-propertiespng.png" sizes="100vw" caption="Application style guide example. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acba0f8b-a698-4633-b0d4-eda05367ec8f/color-split-application-color-schemes-css-custom-propertiespng.png'>Large preview</a>)" alt="UI Controls: buttons, link, head and regular texts, input field" >}}

What about green? We can clearly define it as the primary or brand color, most likely, if the color of the main button changes, then the color of the link and header of the first level will also change.

What about red? Invalid state of input fields, error messages, and the destructive buttons will have the same color at the whole application level. This is a pattern. Now I can define several common functional variables in the root section:

{{< codepen height="480" theme_id="light" slug_hash="MWyYzGX" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Color Split: Functional Level](https://codepen.io/smashingmag/pen/MWyYzGX) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

Regarding the level of component colors, we can easily identify components that can be customized using custom properties.

The button is repeated with different settings, the background color and text for different use cases change &mdash; primary, secondary, tertiary, destructive or negative case.

The input field has two states &mdash; incorrect and normal, where the background and border colors differ. And so, let’s put these settings into color variables at the level of the corresponding components.

For the rest of the components, it is not necessary to define local color variables, this will be redundant.

{{< codepen height="480" theme_id="light" slug_hash="BaKyGVR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Color Split: Component Level](https://codepen.io/smashingmag/pen/BaKyGVR) by <a href="https://codepen.io/arturbasak">Artur Basak</a>.{{< /codepen >}}

You need to dive into the pattern language of your project, which is, probably, being developed by the design team and UX. Engineers must fully understand the whole concept of a visual language, only then we can determine what is common and should live on a functional level, and what should remain in the local scope of visibility.

But everything is not so complicated, there are obvious things. The general background of the page, the background, and color of the main text, in most cases this is what sets the theme of your application. It is extremely convenient to collect such things that are responsible for the configuration of a particular mode (like dark or light mode).

{{% ad-panel-leaderboard %}}

## Why Not Put Everything In The Root Section?

I had such an experience. On [Lition](https://lition.de/) project, the team and I were faced with the fact that we needed to support IE11 for the web application, but not for the website and landings. A common UI Kit was used between the projects, and we decided to [put all the variables in the root](https://github.com/archik408/trading-platform-client/blob/master/src/index.css), this will allow us to redefine them at any level.

And also with this approach for the web application and IE11 case, we simply passed the code through the following [post-processor plugin and transformed](https://github.com/archik408/trading-platform-client/blob/master/scripts/postcss.js) these variables into literals for all UI components in the project. This trick possible only if all variables were defined in the root section because the post-processor can’t understand the specifics of the cascade model.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41cce14-162a-4d37-8a9e-ea75bd6d93bc/lition-application-color-schemes-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41cce14-162a-4d37-8a9e-ea75bd6d93bc/lition-application-color-schemes-css-custom-properties.png" sizes="100vw" caption="Lition SSR web-site. All variables in the root section. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41cce14-162a-4d37-8a9e-ea75bd6d93bc/lition-application-color-schemes-css-custom-properties.png'>Large preview</a>)" alt="Main page of Lition web-site with opened browser dev tools" >}}

Now I understand that this was not the right way. Firstly, if you put component colors into the root section, then you break the separation of concerns principle. As a result, you can end up with redundant CSS in the stylesheet. For example, you have [the folder of components](https://github.com/archik408/trading-platform-client/tree/master/src/components) where each component has its own styles. You also have a [common stylesheet](https://github.com/archik408/trading-platform-client/blob/master/src/index.css) where you describe color variables in the root section. You decide to remove the [button component](https://github.com/archik408/trading-platform-client/tree/master/src/components/Button); in this case, you must remember to also remove the variables associated with the button from the common styles file.

Secondly, this is not the best solution in terms of performance. Yes, a color change causes only the process of a repaint, not reflow/layout, this in itself is not too costly, but when you make some changes at the highest level, you will use more resources to check the entire tree than when these changes are in a small local area. I recommend reading [the performance benchmark](https://lisilinhart.info/posts/css-variables-performance) of CSS variables from Lisi Linhart for more details.

On my current project [Tispr](https://www.tispr.com/), the team and I use split and do not dump everything in the root, on the high level only a palette and functional colors. Also, we are not afraid of IE11, because this problem is solved by [the corresponding polyfill](https://github.com/nuxodin/ie11CustomProperties). Just install [npm module ie11-custom-properties](https://www.npmjs.com/package/ie11-custom-properties) and import library into your application JS bundle:

<pre><code class="language-bash">// Use ES6 syntax
import "ie11-custom-properties";
// or CommonJS
require('ie11-custom-properties');</code></pre>

Or add module by script tag:

<div class="break-out">

<pre><code class="language-javascript">&lt;script async src="./node_modules/ie11-custom-properties/ie11CustomProperties.js"&gt;</script></code></pre>
</div>

Also, you can add the library [without npm via CDN](https://github.com/nuxodin/ie11CustomProperties#usage). The work of this polyfill is based on the fact that IE11 has minimal support for custom properties, where properties can be defined and read based on the cascade. This is not possible with properties starting with double dashes, but possibly with a single dash (the mechanism similar to vendor prefixes). You can read more about this in [the repository documentation](https://github.com/nuxodin/ie11CustomProperties#how-it-works), as well as get acquainted with some limits. Other browsers will ignore this polyfill.

Below is a palette of the Tispr web application as well as the controls of the “white label” functionality for the e-documents (such as user contracts, invoices, or proposals).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4053dbb-7cee-4c57-becf-c292b2f0dbc3/tispr-palette-application-color-schemes-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4053dbb-7cee-4c57-becf-c292b2f0dbc3/tispr-palette-application-color-schemes-css-custom-properties.png" sizes="100vw" caption="Tispr Styleguide: Color Palette. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4053dbb-7cee-4c57-becf-c292b2f0dbc3/tispr-palette-application-color-schemes-css-custom-properties.png'>Large preview</a>)" alt="Grid with following columns: color, color name, color HEX, color RGB." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e694672-02df-4a9d-9145-31c8918674ed/white-label-application-color-schemes-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e694672-02df-4a9d-9145-31c8918674ed/white-label-application-color-schemes-css-custom-properties.png" sizes="100vw" caption="Tispr Styleguide: Brand Picker for White Label functionality. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e694672-02df-4a9d-9145-31c8918674ed/white-label-application-color-schemes-css-custom-properties.png'>Large preview</a>)" alt="Custom color picker UI component" >}}

## Why Not Store Color Variables On The JavaScript Side?

Another reasonable question: why not store the palette and function variables in JavaScript code? This can also be dynamically changed and later redefined colors through inline styles. This could be an option, but most likely this approach would be less optimal since you need to have access to certain elements and change their color properties. With CSS variables, you will only change a single property, i.e. the variable value.

In JavaScript, there are no native functions or API for working with colors. In the [CSS Color Module 5](https://www.w3.org/TR/css-color-5), there will be many opportunities to make derived colors or somehow calculate them. From the perspective of the future, CSS Custom Properties are richer and more flexible than JS variables. Also, with JS variables, there will be no possibility to use inheritance in cascade and that’s the main disadvantage.

## Conclusion

Splitting colors into three levels (palette, functional, and component) can help you be more adaptive to changes and new requirements while working on a project. I believe that CSS Custom Properties are the right tool for organizing color split &mdash; it does not matter what you use for styling: pure CSS, preprocessors, or CSS-in-JS approach.

I came to this approach through my own experience, but I’m not alone. Sara Soueidan described in [her article](https://www.sarasoueidan.com/blog/style-settings-with-css-variables/) a similar approach in which she split variables into global and component levels.

I would also like to suggest reading the [Lea Verou’s article](https://increment.com/frontend/a-users-guide-to-css-variables/) where she describes possible cases of applying CSS variables (not only in terms of color).

{{< signature "ra, yk, il" >}}
