---
title: 'Modern Fluid Typography Using CSS Clamp'
slug: modern-fluid-typography-css-clamp
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f12f5a3d-f679-4b6b-b9c2-cb5a9d9166ae/modern-fluid-typography-css-clamp.jpg
date: 2022-01-17T13:00:00.000Z
summary: >-
  In this article, we’ll explore fluid typography principles, use-cases, best practices, implementation with CSS clamp function and how to calculate the right parameters. We’ll also learn how to address some accessibility concerns and watch out for one important issue that we cannot fix as of yet, but have to be aware of regardless.
description: >-
  We’ll explore fluid typography principles, use-cases, implementation with CSS clamp() and an interactive fluid typography calculator.
categories:
  - CSS
  - Typography
---

The concept of fluid typography in web development has been present for years, and developers had to rely on various workarounds to make it work in the browser. With the new CSS `clamp` function, creating fluid typography has never been more straightforward.

Usually, when we implement **responsive typography**, values change on specific breakpoints. They are explicitly defined. So designers often provide typographic values (font sizes, line heights, letter spacings, etc.) for two, three, or even more screen sizes, and developers usually implement these requirements by adding media queries to target specific breakpoints.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/987f13be-8b58-42ad-a4ca-47881170e66c/1-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/987f13be-8b58-42ad-a4ca-47881170e66c/1-modern-fluid-typography-css-clamp.png" width="800" height="441" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/987f13be-8b58-42ad-a4ca-47881170e66c/1-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="The graph shows the dependence between the viewport width and different typographic values with media query breakpoints." >}}

Although typography elements might look as good as on the designs, that might not be the case for some elements on viewport widths close to the breakpoints. As we already know, there are lots of different devices and screen sizes available to users beyond the ones addressed in the design. Adding more breakpoints in-between and style overrides might fix the issue, but we risk increasing complexity in code, creating more edge cases, and making the code less clear and maintainable.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5df82668-ff2e-424a-8a55-4f00c9ad2af8/2-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5df82668-ff2e-424a-8a55-4f00c9ad2af8/2-modern-fluid-typography-css-clamp.png" width="800" height="313" sizes="100vw" caption="Although typography on lower and higher viewport widths looks good, the size of the title near the breakpoint (center image) looks out of place because of fixed typography values and less whitespace. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5df82668-ff2e-424a-8a55-4f00c9ad2af8/2-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="An example of typography on three different devices with different screen sizes, namely: a phone, a tablet and a laptop." >}}

**Fluid typography** [scales smoothly](https://www.smashingmagazine.com/2021/04/designing-developing-fluid-type-space-scales/) between the minimum and maximum value depending on the viewport width. It usually starts with a minimum value and it maintains the constant value until a specific screen width point at which it starts increasing. Once it reaches a maximum value at another screen width, it maintains that maximum value from there on. We’ll see in this article that fluid typography can also flow in the reverse order &mdash; start with a maximum value and end with a minimum value.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/121943ab-55fa-4315-a0b0-e9283b2be0a3/3-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/121943ab-55fa-4315-a0b0-e9283b2be0a3/3-modern-fluid-typography-css-clamp.png" width="800" height="478" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/121943ab-55fa-4315-a0b0-e9283b2be0a3/3-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="The graph shows the dependence between the viewport width and different typographic values with minimum value end point and maximum value start point." >}}

This approach reduces or eliminates the fine-tuning for specific breakpoints and other edge cases. Although it’s mostly used in typography, this fluid sizing approach also works for margin, padding, gap, etc.

Notice how in the following example, title text scales smoothly and how it looks good on any viewport width. Also, notice how the content still retains the responsive typography, and the value changes only on a breakpoint. 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4a61d57-9dcb-4bf7-ade5-d4efa55b1cd5/4-modern-fluid-typography-css-clamp.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4a61d57-9dcb-4bf7-ade5-d4efa55b1cd5/4-modern-fluid-typography-css-clamp.gif" width="800" height="591" alt="Titles scales smoothly with the viewport width and we don’t have the sizing inconsistencies around the breakpoints like in the previous example." /></a><figcaption>Titles scales smoothly with the viewport width and we don’t have the sizing inconsistencies around the breakpoints like in the previous example.</figcaption></figure>

Although fluid typography addresses the aforementioned issues, it’s not ideal for all scenarios, and **fluid typography shouldn’t be treated as a replacement for responsive typography**. Each has its own set of best practices and proper use-cases and we’ll cover those later on in this article.

In this article, we are going to take a deep dive into fluid typography and check out various approaches that developers have used in the past. We’ll also cover CSS `clamp` function and how it simplified fluid typography implementation, and we’ll learn how to fine-tune `clamp` function parameters to control the starting and ending points for fluid behavior. We’ll also cover accessibility concerns, most of which can be addressed today, and one important accessibility issue which we can’t fix as of yet.

{{% feature-panel %}}
  
## First Attempts At Fluid Typography

As developers, we often use JavaScript to supplement the missing CSS features until they are developed and supported in major browsers. In the early days of the responsive web design, JavaScript libraries like [FlowType.JS](https://github.com/simplefocus/FlowType.JS) have been used to achieve fluid typography.

The first real CSS implementation of fluid typography came with the introduction of CSS `calc` and viewport units (`vw` and `vh`).

<pre><code class="language-css">/&#42; Fixed minimum value below the minimum breakpoint &#42;/
.fluid {
  font-size: 32px;
}

/&#42; Fluid value from 568px to 768px viewport width &#42;/
@media screen and (min-width: 568px) {
  .fluid {
    font-size: calc(32px + 16 &#42; ((100vw - 568px) / (768 - 568));
  }
}

/&#42; Fixed maximum value above the maximum breakpoint &#42;/
@media screen and (min-width: 768px) {
  .fluid {
    font-size: 48px;
  }
}</code></pre>

This snippet looks a bit complex and there are a lot of numbers involved in the calculation. So, let’s break this down into segments and have a high-level overview of what is going on. Let’s focus on selectors and media queries to see the cases they cover.

<div class="break-out">

<pre><code class="language-css">.fluid { /&#42; Min value &#42;/ }

@media screen and (min-width: [breakpoint-min]) {
.fluid { /&#42; Preferred value between the minimum and maximum bound &#42;/ }

@media screen and (min-width: [breakpoint-max]) { /&#42; Max value &#42;/ }</code></pre>
</div>

In the mobile-first approach, the first selector fixes the value to a minimum bound. The first media query handles fluid behavior between the two breakpoints. The final breakpoint fixes the value to a maximum bound. Now that we know what each selector and media query does, let’s see how minimum and maximum bound is applied and how the fluid value is being calculated.

<div class="break-out">

<pre><code class="language-css">.fluid {
 font-size: [value-min];
}

@media (min-width: [breakpoint-min]) {
  .fluid {
    font-size: calc([value-min] + ([value-max] - [value-min]) &#42; ((100vw - [breakpoint-min]) / ([breakpoint-max] - [breakpoint-min])));
  }
}

@media (min-width: [breakpoint-max]) {
  .fluid {
    font-size: [value-max]
  }
}</code></pre>
</div>

This is a lot of boilerplate code to achieve a very simple task of fixing a value between the minimum and maximum bounds and adding a fluid behavior between two breakpoints. 

Despite the amount of the required boilerplate, this approach became so popular for handling fluid sizing in general, that it became clear that a more streamlined approach was needed. This is where the CSS clamp function comes in.

## CSS `clamp` Function

CSS `clamp` function takes three values &mdash; a **minimum bound, preferred value, and a maximum bound**, and it clamps the current value between those bounds. The preferred value is used to determine the value between the bound. **Preferred value** usually includes viewport units, percentages, or other relative units to achieve the fluid effect. This is so robust and flexible function that alongside the fixed values, it can accept even math functions and expressions, and values from the `attr` function.

<pre><code class="language-css">clamp([value-min], [value-preferred], [value-max]);</code></pre>

This function can be applied to any attribute which accepts a valid value type like length, frequency, time, angle, percentage, number, and others, so it can be used beyond typography and sizing.

[Browser support](https://caniuse.com/mdn-css_types_clamp) for `clamp` function sits above 90% at the time of writing of this article, so it’s already well supported. For unsupported desktop browsers like Internet Explorer, it is enough to supply a fallback value as the unsupported browsers will ignore the entire `font-size` expression if they cannot parse the `clamp` function.

<pre><code class="language-css">font-size: [value-fallback]; /&#42; Fallback value &#42;/
font-size: clamp([value-min], [value-preferred], [value-max]);</code></pre>

{{% ad-panel-leaderboard %}}

## Fluid Typography With CSS `clamp`

Let’s use the CSS `clamp` function and populate it with the following values:

- **Minimum value** &mdash; equal to minimum font size.
- **Maximum value** &mdash; equal to maximum font size.
- **Preferred value** &mdash; determines how fluid typography scales &mdash; starting and ending points of fluid behavior and change speed. This value will depend on the viewport size, so we’ll use the viewport width unit `vw`.

Let’s take a look at the following example and set the font size to have a value between `32px` and `48px`. The following `font-size` has a set minimum of `32px` and a maximum of `48px`. The current value is determined by the viewport width unit or, more precisely, `4%` of current viewport width if that value sits between the minimum and maximum bound.

<pre><code class="language-css">font-size: clamp(32px, 4vw, 48px);</code></pre>

Let’s take a quick look at which value will be applied for this example depending on the viewport width, so we can get a good grasp of how the CSS clamp function works.

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Viewport width (px)</th>
			<th>Preferred value (px)</th>
      <th>Applied value (px)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>500</td>
			<td>20</td>
      <td>32 (clamped to a minimum bound)</td>
		</tr>
		<tr>
			<td>900</td>
			<td>36</td>
      <td>36 (preferred value between the bounds)</td>
		</tr>
		<tr>
			<td>1400</td>
			<td>56</td>
      <td>48 (clamped to a maximum bound)</td>
		</tr>
	</tbody>
</table>

We can notice two issues with this clamp function value:

- **Pixel values for min and max are not accessible.**  
Minimum and maximum bounds are expressed with pixel values, so they won’t scale if a user changes their preferred font size. 
- **Viewport value for preferred value is not accessible.**  
Same as the previous case. This value depends on the viewport width exclusively and it doesn’t take user preferences into account.
- **The preferred value is unclear.**  
We are using `4vw` which might look like a magic number at first. We need to know when the fluid behavior starts and ends so we can sync various fluid font size changes.

We can easily address the first issue by converting `px` values to `rem` values for minimum and maximum bounds by dividing the `px` values by 16 (default browser font size). By doing that, minimum and maximum values will adapt to user browser preferences.

<pre><code class="language-css">font-size: clamp(2rem, 4vw, 3rem);</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ab2553-8832-4053-b646-2e4d71c275b6/5-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ab2553-8832-4053-b646-2e4d71c275b6/5-modern-fluid-typography-css-clamp.png" width="800" height="530" sizes="100vw" caption="Pixel values do not adapt to browser font size preferences, but <code>rem</code> and <code>em</code> values do adapt. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ab2553-8832-4053-b646-2e4d71c275b6/5-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="Pixel values do not adapt to browser font size preferences, but rem and em values do adapt." >}}

We need to take a different approach with the preferred value, as this value needs to respond to the viewport size. However, we can easily mix in the relative `rem` value by turning it into a math expression.

<pre><code class="language-css">font-size: clamp(2rem, 4vw + 1rem, 3rem);</code></pre>

Please note that this is **not a foolproof solution for all accessibility issues**, so it’s still important to test if the fluid typography can be zoomed in enough and if it responds well enough to user accessibility preferences. We’ll cover these issues later on.

However, we still do not know how we got the preferred value from the example (`4vw + 1rem`) to achieve the required fluid behavior, so let’s take a look at how we can fine-tune the preferred value and fully understand the math behind it.

## Fluid Sizing Function

The preferred value **affects how fluid typography function behaves**. More precisely, we can change at which viewport width points the minimum value starts to change and at which viewport width point it reaches the maximum value.

For example, we might want the fluid behavior to start at `1200px` and end at `800px` of the viewport width. Please note that **different minimum and maximum bounds require different preferred values** (viewport value and relative size) to keep the various fluid typographies in sync.

For example, we usually do not want one fluid behavior to occur between `1200px` and `800px` of the viewport width and another to occur between `1000px` and `750px` of the viewport width. This can lead to sizing inconsistencies like in the following example.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a69cb7-6550-4127-99b8-227708a09b37/6-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a69cb7-6550-4127-99b8-227708a09b37/6-modern-fluid-typography-css-clamp.png" width="800" height="289" sizes="100vw" caption="In this example, we are setting four fluid typography values with different bounds and the same preferred size of <code>4vw</code>. Although the result on the left looks consistent, the fluid sizing (on the right) is inconsistent on some viewport widths because the change occurs at different viewport widths. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a69cb7-6550-4127-99b8-227708a09b37/6-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="In this example, we are setting four fluid typography values with different bounds and the same preferred size of 4vw. Although the result on the left looks consistent, the fluid sizing (on the right) is inconsistent on some viewport widths because the change occurs at different viewport widths." >}}

To avoid this issue, we need to figure out how the preferred value is calculated and assign the proper viewport and relative values to the clamp function preferred value. 

Let’s figure out a function that is used to calculate it.

<pre><code class="language-css">font-size: clamp([min]rem, [v]vw + [r]rem, [max]rem);
</code></pre>

$$y=\frac{v}{100}&#42;x + r$$

- **x** &mdash; current viewport width value (`px`).
- **y** &mdash; resulting fluid font size for a current viewport width value **x** (`px`).
- **v** &mdash; viewport width value that affects fluid value change rate (`vw`).
- **r** &mdash; relative size equal to browser font size. Default value is `16px`.

With this function, we can easily calculate starting and ending points of the fluid behavior. For our example, minimum value of `2rem` (`32px`) is constant until `400px` viewport width.

$$32=\frac{4}{100}&#42;x + 16$$

$$16=\frac{1}{25}&#42;x$$

$$x=400$$

We can apply the same function for the maximum value and see that it reaches a maximum value of `3rem` (`48px`) on an `800px` viewport width. 

The purpose of this example was just to demonstrate how the preferred value affects the fluid typography behavior. Let’s use the same function for a slightly more realistic scenario and solve a more practical real-world example. We’ll create accessible fluid typography based on required font sizes and specific points where we want the fluid behavior to occur.

### Calculating preferred value parameters based on specific starting and ending points

Let’s take a look at a practical example that comes up often in real-world scenarios. The designers have provided us the font sizes and breakpoints we, as developers, need to implement the fluid typography with the following parameters:

- Minimum font size is `36px` (y1)
- Maximum font size is `52px` (y2)
- Minimum value should end at `600px` viewport width (x1)
- Maximum value should start at `1400px` viewport width (x2)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03512735-8d5b-4486-90b5-c564aa43a06e/7-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03512735-8d5b-4486-90b5-c564aa43a06e/7-modern-fluid-typography-css-clamp.png" width="800" height="495" sizes="100vw" caption="Visualizing the fluid typography requirements from the example. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03512735-8d5b-4486-90b5-c564aa43a06e/7-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="Visualizing the fluid typography requirements from the example." >}}

Let’s take these values and add them to the fluid sizing function we’ve discussed previously.

$$y=\frac{v}{100} \cdot x + r$$

We end up with two equations with two parameters that we need to calculate &mdash; viewport width value `v` and relative size `r` .

$$(1)\;\;\; y_1=\frac{v}{100} \cdot x_1 + r$$

$$(2) \;\;\; y_2 =\frac{v}{100} \cdot x_2 + r$$

We can take the first equation and turn it into the following expression that we can use.

$$(1) \;\;\; r=y_1 - \frac{v}{100} \cdot x_1$$

We can replace `r` in the second equation with this expression and get the function to calculate `v`.

$$v=\frac{100 \cdot (y_2-y_1)}{x_2 - x_1}$$

$$v=\frac{100 \cdot (52-36)}{1400 - 600}$$

$$v=2$$

We get the viewport width value `2vw`. In a similar way, we can isolate `r` and calculate it using the available parameters.

$$r=\frac{x_1y_2 - x_2y_1}{x_1 - x_2}$$

$$r=\frac{600 \cdot 52 - 1400 \cdot 36}{600 - 1400}$$

$$r=24$$

**Note**: This value is in pixels and relative value needs to be expressed in `rem` so we divide the pixel value with `16` and end up with `1.5rem`.

We also need to convert the minimum bound of `36px` and maximum bound of `52px` to `rem` and add all values to the CSS `clamp` function.

<pre><code class="language-css">font-size: clamp(2.25rem, 2vw + 1.5rem, 3.25rem);</code></pre>

We can plot this function to confirm that the calculated values are correct.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a12e5db-28a5-44e6-b0fc-ee901fd6c3ed/8-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a12e5db-28a5-44e6-b0fc-ee901fd6c3ed/8-modern-fluid-typography-css-clamp.png" width="800" height="393" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a12e5db-28a5-44e6-b0fc-ee901fd6c3ed/8-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="" >}}

To summarize, we can use the following two functions to calculate preferred value parameters `v` (expressed in `vw` ) and `r` (expressed in `rem`) from font sizes and viewport width points.

$$v=\frac{100 \cdot (y_2-y_1)}{x_2 - x_1}$$

$$r=\frac{x_1y_2 - x_2y_1}{x_1 - x_2}$$

Now that we fully understand how the `clamp` function works and how the preferred value is being calculated, we can easily create consistent and accessible fluid typography in our projects and avoid the aforementioned pitfalls.

{{% ad-panel-leaderboard %}}

## Using negative viewport value for fluid sizing

We can also make the **size scale up as the viewport size decreases** by using a negative value for the viewport value. The negative viewport value will reverse the default fluid behavior. We also need to adjust the relative size so the fluid behavior starts and ends at certain points by solving the two aforementioned equations from the previous example.

<pre><code class="language-css">font-size: clamp(3rem, -4vw + 6rem, 4.5rem);</code></pre>

I haven’t used this reversed configuration in my projects, but you might find it interesting if you ever encounter this requirement in your project or the design.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f6ee475-9676-457e-8caf-27886d5a9dc9/9-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f6ee475-9676-457e-8caf-27886d5a9dc9/9-modern-fluid-typography-css-clamp.png" width="800" height="402" sizes="100vw" caption="Fluid sizing with negative value for viewport size. Notice that size decreases as the viewport width increases. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f6ee475-9676-457e-8caf-27886d5a9dc9/9-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="Fluid sizing with negative value for viewport size. Notice that size decreases as the viewport width increases." >}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7365aa6-ee2b-4b15-b3db-5588227d829a/10-modern-fluid-typography-css-clamp.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7365aa6-ee2b-4b15-b3db-5588227d829a/10-modern-fluid-typography-css-clamp.gif" width="800" height="385" alt="Fluid behavior starts with the maximum value until it reaches a certain point when it starts decreasing until it reaches the minimum value." /></a><figcaption>Fluid behavior starts with the maximum value until it reaches a certain point when it starts decreasing until it reaches the minimum value.</figcaption></figure>

### Fluid typography visualization tool

While I was working on a project, I had to create multiple different fluid typography configurations. I was testing the configurations in the browser and I had an idea to create a tool that would help developers visualize and fine-tune fluid typography behavior. I was inspired by one of the demos from Josh W. Comeau’s “CSS for JS developers” course and I’ve created [Modern Fluid Typography Tool](https://modern-fluid-typography.vercel.app/).

{{< rimg href="https://modern-fluid-typography.vercel.app/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c74263b-12d6-47cc-9b99-93afe428469e/11-modern-fluid-typography-css-clamp.png" width="800" height="575" sizes="100vw" caption="Graph view allows developers a general overview of fluid behavior. <a href='https://modern-fluid-typography.vercel.app/'>Jump to the calculator</a>." alt="Graph view allows developers a general overview of fluid behavior." >}}

Developers can use this tool to create and fine-tune fluid typography code snippets and visualize fluid behavior to keep multiple instances in sync. The tool can also generate a link to the config, so developers can include the link in code comments or documentation so others can easily check the fluid sizing behavior.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1ef7f7-8faf-4346-a0f3-2a94c509dc4d/12-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1ef7f7-8faf-4346-a0f3-2a94c509dc4d/12-modern-fluid-typography-css-clamp.png" width="800" height="465" sizes="100vw" caption="Table view allows developers to keep track of fluid sizes on a customizable list of breakpoints. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1ef7f7-8faf-4346-a0f3-2a94c509dc4d/12-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="Table view allows developers to keep track of fluid sizes on a customizable list of breakpoints." >}}

This project is free and [open-source](https://github.com/codeAdrian/modern-fluid-typography-editor), so feel free to report any bugs and contribute. I’m happy to hear your thoughts and feature requests!

## Accessibility Concerns

It’s important to reiterate that using `rem` values doesn’t automagically make fluid typography accessible for all users, it only allows the font sizes to respond to user font preferences. Using CSS `clamp` function in combination with the viewport units to achieve fluid sizing introduces **another set of drawbacks** that we need to consider.

Adrian Roselli has tested and [documented these issues extensively](https://adrianroselli.com/2019/12/responsive-type-and-zoom.html) in his blog post.

<blockquote>“When you use <code>vw</code> units or limit how large text can get with <code>clamp()</code>, there is a chance a user may be unable to scale the text to 200% of its original size. If that happens, it is WCAG failure under <a href="https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=144#resize-text">1.4.4 Resize text (AA)</a> so be certain to <a href="https://adrianroselli.com/2019/12/responsive-type-and-zoom.html">test the results with zoom</a>.”<br /><br />&mdash; Adrian Roselli</blockquote>

I wanted to tackle this issue from the get-go by using JavaScript to detect when zoom event occurs and apply a class that will override the fluid sizing with a regular `rem` value. 

<pre><code class="language-css">/&#42; Apply fluid typography for default zoom level (not zoomed) &#42;/
.title {
  font-size: clamp(2rem, 4vw + 1rem, 3rem);
}

/&#42; Revert to responsive typography if zoom is active &#42;/
body.zoom-active .title {
  font-size: 2rem;
}

@media screen and (min-width: 768px) {
  body.zoom-active .title {
    font-size: 3rem;
  }
}</code></pre>

You might be surprised as I was to find out that we [cannot reliably detect the zoom event](https://css-tricks.com/can-javascript-detect-the-browsers-zoom-level/) using JavaScript like we can detect any other regular viewport event like resize.

There is the [Visual Viewport API specification](https://wicg.github.io/visual-viewport/) with a [solid 92% browser support](https://caniuse.com/mdn-api_visualviewport_scale) at the time of writing this article, but the scale (zoom level) value **simply doesn’t work** &mdash; it returns the same value regardless of the zoom (scale) value. Not to mention that there is no documentation, working examples, or use-cases available. This is a bit odd, considering that this API has such solid browser support. Some [workarounds do exist](https://www.bennadel.com/blog/3811-looking-at-how-browser-zoom-affects-css-media-queries-and-pixel-density.htm), but they are not completely reliable either and cannot detect if the page has been zoomed in when it’s first loaded, only after the event has occurred.

If the Visual Viewport API worked as intended, we could easily toggle a CSS class on zoom event.

<div class="break-out">

<pre><code class="language-javascript">/&#42; This code won't work because visualViewport.scale is buggy
 &#42; and always returns the same value. This might be fixed in the future.
 &#42;/

function checkZoomLevel() {
  if (window.visualViewport.scale === 1) {
    document.body.classList.remove("zoom-active");
  } else {
    document.body.classList.add("zoom-active");
  }
}

window.addEventListener("resize", checkZoomLevel);</code></pre>
</div>

It’s unfortunate that by applying fluid sizing we are risking making the content inaccessible for some users that use zoom functionality while browsing. Until we can create a reliable and more accessible fallback for fluid typography, make sure to **use fluid sizing sparingly and test** if the zoom levels are according to the Web Content Accessibility Guidelines (WCAG).

## Recommended Use-cases

Fluid typography works best for **large and prominent text elements** with a larger difference between the minimum and maximum size. Large titles will look more jarring and out of place on smaller viewports if not scaled accordingly.

Fluid sizing is also recommended for the cases where we need to maintain consistent sizing.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4d028b5-0ccd-4bf3-823a-638ae04c3f61/13-modern-fluid-typography-css-clamp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4d028b5-0ccd-4bf3-823a-638ae04c3f61/13-modern-fluid-typography-css-clamp.png" width="800" height="515" sizes="100vw" caption="Title size and container grid gap are not scaled properly to the card dimensions on smaller desktop and larger tablet viewports. We can fix this by using fluid sizing. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4d028b5-0ccd-4bf3-823a-638ae04c3f61/13-modern-fluid-typography-css-clamp.png'>Large preview</a>)" alt="Title size and container grid gap are not scaled properly to the card dimensions on smaller desktop and larger tablet viewports. We can fix this by using fluid sizing." >}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01bc9222-abf5-41fb-be72-ec3302467420/14-modern-fluid-typography-css-clamp.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01bc9222-abf5-41fb-be72-ec3302467420/14-modern-fluid-typography-css-clamp.gif" width="800" height="506" alt="Fluid sizing can be used to maintain both the typography scaling and consistent grid gap" /></a><figcaption>Fluid sizing can be used to maintain both the typography scaling and consistent grid gap.</figcaption></figure>

Elise Hein reached a similar conclusion [in her article](https://elisehe.in/2021/03/13/fluid-type) on fluid typography best practices.

<blockquote>“I tried and failed to find many specific areas where viewport-relative typography does outperform breakpoint-based sizing in terms of readability. Here are two: <strong>setting display text</strong> and <strong>maintaining consistent measure</strong>.”<br /><br />&mdash; Elise Hein</blockquote>

Fluid typography is **not as effective or useful if the difference between the minimum and maximum is just a few pixels**, as it’s the usual case with the body text. Body text with a small difference between the minimum and maximum font sizes won’t look out of place on any viewport width, as it’s the case with larger font sizes. For those cases, it’s recommended to use regular responsive typography with breakpoints.

## Conclusion

Fluid typography shouldn’t serve as a replacement for responsive typography, but as an enhancement for specific use-cases instead. We should use fluid typography to smoothly scale text that has a larger difference between the minimum and maximum size and to maintain a consistent sizing.

When using multiple fluid typography elements with CSS `clamp` function, we must make sure that the fluid scaling is in sync. We can do that by calculating viewport width and relative value and using them as preferred values in the CSS `clamp` function. We must also keep in mind to use relative units like rem unit so that fluid typography adapts to user font size preferences.

We have also seen how **fluid typography can limit user zoom capabilities** which can cause accessibility issues. It’s important to test the fluid typography with zoom and revert it to regular responsive typography if the testing reveals that content is not zoomable enough.

We should be able to address this issue by overriding the fluid typography values when a zoom action occurs. However, it’s currently not possible to do that as Visual Viewport API is not working properly and doesn’t respond to user zoom events.

### References

- [`clamp()`](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp()), MDN
- “[Why Should Type Be Fluid, Anyway?](https://elisehe.in/2021/03/13/fluid-type),” Elise Hein
- “[Simplified Fluid Typography](https://css-tricks.com/simplified-fluid-typography/),” Chris Coyier
- “[Responsive Type And Zoom](https://adrianroselli.com/2019/12/responsive-type-and-zoom.html),” Adrian Roselli
- “[Responsive And Fluid Typography With `vh` And `vw` Units](https://www.smashingmagazine.com/2016/05/fluid-typography/),” Michael Riethmuller

{{< signature "vf, yk, il" >}}

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
