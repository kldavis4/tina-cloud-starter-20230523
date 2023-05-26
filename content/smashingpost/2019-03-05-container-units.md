---
title: 'Building Robust Layouts With Container Units'
slug: robust-layouts-container-units-css
author: russell-bishop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b35ec364-d1a3-4119-878c-519ec20f1b18/russell-bishop-container-units-sharing-card.png
date: 2019-03-05T15:00:17+01:00
summary: >-
  When inspecting most other grids in DevTools, you’ll notice that column widths are dependent on their parent element. This article will help you understand how to overcome these limitations using CSS variables and how you can start building with container units.
description: >-
  When inspecting most other grids in DevTools, you’ll notice that column widths are dependent on their parent element. This article will help you understand how to overcome these limitations using CSS variables and how you can start building with container units.
categories:
  - CSS
  - Layouts
  - Responsive Design
---
Container units are a specialized set of CSS variables that allow you to build grids, layouts, and components using columns and gutters. They mirror the layout functionality found in UI design software where configuring just three values provides your document with a global set of columns and gutters to measure and calculate from.

They also provide consistent widths *everywhere* in your document &mdash; regardless of their nesting depth, their parent’s width, or their sibling elements. So instead of requiring a repeated set of `.grid`  and `.row` parent elements, container units measure from the `:root` of your document &mdash; just like using a `rem` unit.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccf54496-d7a0-43fa-b0fc-44563c713527/container-units-make-grid.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccf54496-d7a0-43fa-b0fc-44563c713527/container-units-make-grid.gif" width="800" alt="container units measure from the root of your document just like using a rem unit" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccf54496-d7a0-43fa-b0fc-44563c713527/container-units-make-grid.gif">Large preview</a>)</figcaption></figure>

## What Makes Container Units Different?

Grids from popular frameworks (such as [Bootstrap](https://getbootstrap.com/docs/4.0/layout/grid/) or [Bulma](https://bulma.io/documentation/columns/basics/)) share the same fundamental limitation: they rely on relative units such as ‘percentages’ to build columns and gutters.

This approach ties developers to using a specific HTML structure whenever they want to use those measurements and requires `parent > child` nesting for widths to calculate correctly.

Not convinced? Try for yourself:

- [Open](https://getbootstrap.com/docs/4.0/layout/grid/) [any](https://foundation.zurb.com/sites/docs/flex-grid.html) [CSS](https://bulma.io/documentation/columns/sizes/) [framework’s](https://daneden.github.io/Toast/) [grid](https://www.responsivegridsystem.com/) [demo](https://getskeleton.com/);
- Inspect a column and note the width;
- Using DevTools, drag that element somewhere else in the document;
- Note that the column’s width has changed in transit.

{{% feature-panel %}} 

## Freedom Of Movement (*...Not Brexit*)

Container units allow you more freedom to size elements using a set of global units. If you want to build a sidebar the width of three columns, all you need is the following:

<pre><code class="language-css">.sidebar {
  width: calc(3 * var(--column-unit));
  /* or columns(3) */
}
</code></pre>

Your `...class="sidebar">...` element can live anywhere inside of your document &mdash; without specific parent elements or nesting.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417f032f-9fbd-4ab9-be4d-cd69aa0eba30/3-column-modal-looping.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417f032f-9fbd-4ab9-be4d-cd69aa0eba30/3-column-modal-looping.gif" width="800" alt="Measuring three columns and using them for a sidebar." /></a><figcaption>Measuring three columns and using them for a sidebar (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417f032f-9fbd-4ab9-be4d-cd69aa0eba30/3-column-modal-looping.gif">Large preview</a>)</figcaption></figure>

## Sharing Tools With Designers

Designers and developers have an excellent middle-ground that helps translate from design software to frontend templates: **numbers**. 

[Modular scales](https://www.modularscale.com/) are exceptional not just because they help designers bring harmony to their typography, but also because developers can replicate them as a *simple system*. The same goes for [Baseline Grids](https://blog.prototypr.io/the-8pt-grid-consistent-spacing-in-ui-design-with-sketch-577e4f0fd520): superb, self-documenting systems with tiny configuration (one root number) and massive consistency.

Container units are set up in the same way that designers use Sketch to configure [Layout Settings](https://sketchapp.com/docs/canvas/rulers-guides-grids/#layout-grid):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3900f5c4-d661-47b4-a6a3-25fbfe0a6097/container-units-layout-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e095a39-8f3d-4eed-a34d-6e080a1ab91f/container-units-layout-settings-columns.png" sizes="100vw" caption="Layout settings (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3900f5c4-d661-47b4-a6a3-25fbfe0a6097/container-units-layout-settings.png'>Large preview</a>)" alt="Layout settings" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ba779b8-801a-411d-9b8a-0c5c9f531223/container-units-sketch-gridlines.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ba779b8-801a-411d-9b8a-0c5c9f531223/container-units-sketch-gridlines.png" sizes="100vw" caption="Sketch gridlines (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ba779b8-801a-411d-9b8a-0c5c9f531223/container-units-sketch-gridlines.png'>Large preview</a>)" alt="Sketch gridlines" >}}

Any opportunity for designers and developers to build with the same tools is a huge efficiency boost and fosters new thinking in both specialisms.

## Start Building With Container Units

Define your grid proportions with three values:

<pre><code class="language-css">:root {
  --grid-width: 960;
  --grid-column-width: 60;
  --grid-columns: 12;
}
</code></pre>

These three values define how wide a column is in proportion to your grid. In the example above, a column’s width is `60 / 960`. Gutters are calculated automatically from the remaining space.

Finally, set a width for your container:

<pre><code class="language-css">:root {
  --container-width: 84vw;
}
</code></pre>

**Note**: `--container-width` *should be set as an absolute unit. I recommend using* `viewport units` *or* `rems`.

You can update your `--container-width` at any breakpoint (all of your container units will update accordingly):

<pre><code class="language-css">@media (min-width: 800px) {
  --container-width: 90vw;
}

@media (min-width: 1200px) {
  --container-width: 85vw;
}

/* what about max-width? */
@media (min-width: 1400px) {
  --container-width: 1200px;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bc6e302-4613-498c-bc57-e59188abb4e8/container-units-breakpoints.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bc6e302-4613-498c-bc57-e59188abb4e8/container-units-breakpoints.gif" width="800" alt="breakpoints" /></a><figcaption>Breakpoints (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bc6e302-4613-498c-bc57-e59188abb4e8/container-units-breakpoints.gif">Large preview</a>)</figcaption></figure>

You’ve now unlocked two very robust units to build from:

1. `--column-unit`
2. `--gutter-unit`

{{% ad-panel-leaderboard %}}

## Column Spans: The Third And Final Weapon

More common than building with either columns or gutters is to span across both of them:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2259a08-1882-4f28-9f6f-145750d853aa/6-columnspan-looping.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2259a08-1882-4f28-9f6f-145750d853aa/6-columnspan-looping.gif" width="800" alt="6 column span = 6 columns + 5 gutters" /></a><figcaption>6 column span = 6 columns + 5 gutters (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2259a08-1882-4f28-9f6f-145750d853aa/6-columnspan-looping.gif">Large preview</a>)</figcaption></figure>

Column spans are easy to calculate, but not very pretty to write. For spanning across columns, I would recommend using a pre-processor:

<pre><code class="language-css">.panel {
  /* vanilla css */
  width: calc(6 * var(--column-and-gutter-unit) - var(--gutter-unit));

  /* pre-processor shortcut */
  width: column-spans(6);  
}
</code></pre>

Of course, you can use pre-processor shortcuts for every container unit I’ve mentioned so far. Let’s put them to the test with a design example.

## Building Components With Container Units

Let’s take a design example and break it down:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbaf41cb-0cb6-4862-8032-1ae8167c2034/container-units-explorers-welcome.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbaf41cb-0cb6-4862-8032-1ae8167c2034/container-units-explorers-welcome.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbaf41cb-0cb6-4862-8032-1ae8167c2034/container-units-explorers-welcome.jpg'>Large preview</a>)" alt="design example" >}}

This example uses columns, gutters and column spans. Since we’re just storing a value, container units can be used for other CSS properties, like defining a height or providing padding:

<div class="break-out">

 <pre><code class="language-css">.background-image {
  width: column-spans(9);
  padding-bottom: gutters(6);
  /* 6 gutters taller than the foreground banner */
}

.foreground-banner {
  width: column-spans(8);
  padding: gutters(2);
}

.button {
  height: gutters(3);
  padding: gutters(1);
}
</code></pre>
</div>

## Grab The Code

- CSS: [container-units-css.css](https://gist.github.com/RussellBishop/4f6ed077878a9c15f76de41c201c4e5d#file-container-units-css-css)
- SCSS Functions: [container-units-css-fuctions.scss](https://gist.github.com/RussellBishop/f5b14ab213c6ecb35cc6ba9b3ec3071a)
- Demos and Documentation: [Container Units](https://russellbishop.co.uk/container-units/)

<div class="break-out">

 <pre><code class="language-css">:root {
  /* Grid proportions */
  --grid-width: 960;
  --grid-column-width: 60;
  --grid-columns: 12;

  /* Grid logic */
  --grid-gutters: calc(var(--grid-columns) - 1);

  /* Grid proportion logic */
  --column-proportion: calc(var(--grid-column-width) / var(--grid-width));
  --gutter-proportion: calc((1 - (var(--grid-columns) * var(--column-proportion))) / var(--grid-gutters));

  /* Container Units */
  --column-unit: calc(var(--column-proportion) * var(--container-width));
  --gutter-unit: calc(var(--gutter-proportion) * var(--container-width));
  --column-and-gutter-unit: calc(var(--column-unit) + var(--gutter-unit));

  /* Container Width */
  --container-width: 80vw;
}

@media (min-width: 1000px) {
  :root {
    --container-width: 90vw;
  }
}

@media (min-width: 1400px) {
  :root {
    --container-width: 1300px;
  }
}
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Why Use CSS Variables?

<blockquote>“Pre-processors have been able to do that for years with <code>$variables</code> &mdash; why do you need CSS variables?”</blockquote>

Not... quite. Although you can use variables to run calculations, you cannot avoid compiling unnecessary code when one of the variables *updates* it’s value.

Let’s take the following condensed example of a grid:

<pre><code class="language-css">.grid {
  $columns: 2;
  $gutter: $columns * 1rem;
  display: grid;
  grid-template-columns: repeat($columns, 1fr);
  grid-gap: $gutter;

  @media (min-width: $medium) {
    $columns: 3;
    grid-template-columns: repeat($columns, 1fr);
    grid-gap: $gutter;
  }

  @media (min-width: $large) {
    $columns: 4;
    grid-template-columns: repeat($columns, 1fr);
    grid-gap: $gutter;
  }
}
</code></pre>

This example shows how **every reference to a SASS/LESS variable has to be re-compiled** if the variable changes &mdash; duplicating code over and over for each instance.

But CSS Variables share their logic *with the browser*, so browsers can do the updating *for you*.

<pre><code class="language-css">.grid {
  --columns: 2;
  --gutter: calc(var(--columns) * 1rem);
  display: grid;
  grid-template-columns: repeat(var(--columns), 1fr);
  grid-gap: var(--gutter);

  @media (min-width: $medium) {
    --columns: 3;
  }

  @media (min-width: $large) {
    --columns: 4;
  }
}
</code></pre>

This concept helps form the logic of container units; by storing logic once at the root, every element in your document watches those values as they update, and responds accordingly.

Give it a try!

### <span class="rh">Recommended Reading</span>

<ul>
<li>“<a title="Read 'What is the difference between CSS variables and preprocessor variables?'" href="https://css-tricks.com/difference-between-types-of-css-variables/#article-header-id-2" rel="bookmark">What Is The Difference Between CSS Variables And Preprocessor Variables?</a>” by Chris Coyier</li>
<li>“<a title="Read 'When And How To Use CSS Multi-Column Layout'" href="https://www.smashingmagazine.com/2019/01/css-multiple-column-layout-multicol/" rel="bookmark">When And How To Use CSS Multi-Column Layout</a>,” by Rachel Andrew</li>
<li>“<a title="Read 'Common CSS Issues For Front-End Projects'" href="https://www.smashingmagazine.com/2018/12/common-css-issues-front-end-projects/" rel="bookmark">Common CSS Issues For Front-End Projects</a>,” by Ahmad Shadeed</li>
<li>“<a title="Read 'Table Design Patterns On The Web'" href="https://www.smashingmagazine.com/2019/01/table-design-patterns-web/" rel="bookmark">Table Design Patterns On The Web</a>,” by Chen Hui Jing</li>
</ul>

{{< signature "dm, ra, il" >}}
