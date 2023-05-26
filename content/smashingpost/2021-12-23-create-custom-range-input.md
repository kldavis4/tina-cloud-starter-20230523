---
title: 'Creating A Custom Range Input That Looks Consistent Across All Browsers'
slug: create-custom-range-input-consistent-browsers
author: alyssa-holland
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0deb2d53-1482-44c1-bf77-4dcc92ce3cd5/create-custom-range-input-consistent-browsers.jpg
date: 2021-12-23T11:00:00.000Z
summary: >-
  Range inputs have notoriously been a pain to style. Each browser renders the input differently requiring you to use vendor prefixes in order to create a cohesive look and feel. In this article, we’ll take a look at the quirkiness of the HTML range input and demonstrate how to style the input to look consistent across all major browsers.
description: >-
  Range inputs have notoriously been a pain to style. Each browser renders the input differently requiring you to use vendor prefixes in order to create a cohesive look and feel. In this article, we’ll take a look at the quirkiness of the HTML range input and demonstrate how to style the input to look consistent across all major browsers.
categories:
  - HTML
  - CSS
  - Browsers
  - Techniques
---

As one of the maintainers of a UI component library, I’ve implemented and styled myriads of input elements. One day I was assigned the task of adding a [range input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range) to the library and, I figured it would be a similar process to the other inputs I had implemented in the past. That assumption was correct until I began testing the range input across multiple browsers and quickly realized that I had a lot more work on my hands.

After a lot of research, I was finally able to pinpoint enough [blog posts](https://brennaobrien.com/blog/2014/05/style-input-type-range-in-every-browser.html), [articles](https://css-tricks.com/styling-cross-browser-compatible-range-inputs-css/), and [in-depth tutorials](https://css-tricks.com/sliding-nightmare-understanding-range-input/) to help me style the range input to render consistently. Instead of having to search around for multiple resources, the purpose behind this blog post is to provide a one-stop shop for learning how to properly style a range input that will look consistent across all browsers. It’s the article I wish I had when I had to do this myself and, I hope that it helps make this process faster and smoother for you.

## Anatomy Of A Range Input

The range input consists of two main parts:

1. **Track**  
This is the part of the slider that the thumb *runs* along. Or put another way, it’s the long element that represents the ranges of values that can be selected.
3. **Thumb**  
This is an element on the track that the user can move around to select varying range values.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024ce3fb-9e84-4f70-b9c5-83d76f73dc42/1-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024ce3fb-9e84-4f70-b9c5-83d76f73dc42/1-create-custom-range-input.png" width="800" height="210" sizes="100vw" caption="A range input is comprised of a track and thumb. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024ce3fb-9e84-4f70-b9c5-83d76f73dc42/1-create-custom-range-input.png'>Large preview</a>)" alt="A range input is comprised of a track and thumb." >}}

If it were a mathematical equation:

<blockquote>range input = track + thumb</blockquote>

The range input is sometimes referred to as a “slider” and throughout the rest of this article, I will be using those terms interchangeably.

## Browser Inconsistencies 

To demonstrate why we even need a tutorial on styling range inputs in the first place, we’ll take a look at some screenshots of the default HTML range input and how it gets rendered across the four major browsers (Chrome, Firefox, Safari, and Edge). Or, if you prefer, you can view this [CodeSandbox demo](https://37osw.csb.app/) in each of the respective browsers to see the browser inconsistencies in all their glory. 

**Note:** *These screenshots were taken as of September 2021 and may be subject to change as the respective browsers update.*

Let’s start things off by looking at Chrome which, in my opinion, renders the most user-friendly version of the input by default.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1b0ca6b-c21c-478d-af5e-ac071e0a8e54/2-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1b0ca6b-c21c-478d-af5e-ac071e0a8e54/2-create-custom-range-input.png" width="800" height="231" sizes="100vw" caption="Chrome demo of default HTML range input. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1b0ca6b-c21c-478d-af5e-ac071e0a8e54/2-create-custom-range-input.png'>Large preview</a>)" alt="Chrome demo of default HTML range input" >}}

Firefox is next up and looks different from the Chrome rendered input. In Firefox, the height of the track is slightly shorter. On the other hand, the height and width of the thumb are larger and do not have the same blue background color that the Chrome version has.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e41b8da4-4475-4d3a-b0ac-e0288ce1c299/3-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e41b8da4-4475-4d3a-b0ac-e0288ce1c299/3-create-custom-range-input.png" width="800" height="214" sizes="100vw" caption="Firefox demo of default HTML range input. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e41b8da4-4475-4d3a-b0ac-e0288ce1c299/3-create-custom-range-input.png'>Large preview</a>)" alt="Firefox demo of default HTML range input" >}}

The Safari slider is closest in looks to the Firefox version but, it is, yet again, still different. This time around the track seems to have a shadowy effect and, the height of the thumb and width is smaller than Chrome and Firefox’s renditions. If you look closely, you can also see that the thumb is not centered directly on the track giving it an unpolished look and feel.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd5cbf69-d2c2-4412-93b1-a14b1eee6b9f/4-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd5cbf69-d2c2-4412-93b1-a14b1eee6b9f/4-create-custom-range-input.png" width="800" height="221" sizes="100vw" caption="Safari demo of default HTML range input. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd5cbf69-d2c2-4412-93b1-a14b1eee6b9f/4-create-custom-range-input.png'>Large preview</a>)" alt="Safari demo of default HTML range input" >}}

Last but not least is Edge which, now that [Microsoft Edge is built off Chromium](https://support.microsoft.com/en-us/microsoft-edge/download-the-new-microsoft-edge-based-on-chromium-0f4a3dd7-55df-60f5-739f-00010dba52cf), is way more aligned with the other three browsers than its pre-Chromium predecessor. However, we can see that it is still rendering differently than the other three browsers. Edge’s rendition of its range input looks very similar to the Chrome version, except it has a darker grey background color for the thumb and left-hand side of the track before the thumb.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f263c31-7657-4e3c-add3-9c78026f0423/5-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f263c31-7657-4e3c-add3-9c78026f0423/5-create-custom-range-input.png" width="800" height="211" sizes="100vw" caption="Edge demo of default HTML range input. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f263c31-7657-4e3c-add3-9c78026f0423/5-create-custom-range-input.png'>Large preview</a>)" alt="Edge demo of default HTML range input" >}}

Now that we’ve seen how awfully inconsistent each browser renders the range input, we’ll take a look at how we can use CSS to uniform them.

{{% feature-panel %}}

## Range Reset (Baseline Styles)

Because the browser inconsistencies vary so greatly, we need to start from a level playing field. Once the default styles that each browser applies have been stripped away, we can start working towards making a more uniformed looking input. We’ll use the `input[type="range"]` element-attribute selector and the styles applied here will act like a CSS reset for the input. 

To apply the baseline styles we need four properties:

1. `-webkit-appearance: none;`  
This property is a [vendor prefix](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix) that applies to all the major browsers. By giving it the value of `none` this tells each respective browser to clear out any default styles. This allows us to be able to start from scratch and build up the look of the input from that point.
2. `background: transparent;`  
This clears out the default background that is applied to the input.
3. `cursor: pointer;`
4. `width`  
Sets the overall width of the input.

<pre><code class="language-css">input[type="range"] {
  -webkit-appearance: none;
  appearance: none;
  background: transparent;
  cursor: pointer;
  width: 15rem;
}</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76c6f3b4-4bae-4230-bcaf-130078760c7f/6-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76c6f3b4-4bae-4230-bcaf-130078760c7f/6-create-custom-range-input.png" width="800" height="282" sizes="100vw" caption="Range input in Chrome before background: transparent is applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76c6f3b4-4bae-4230-bcaf-130078760c7f/6-create-custom-range-input.png'>Large preview</a>)" alt="Range input in Chrome before background: transparent is applied." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b5ec91a-7594-4870-8557-60a772f74b3f/7-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b5ec91a-7594-4870-8557-60a772f74b3f/7-create-custom-range-input.png" width="800" height="237" sizes="100vw" caption="Range Input in Chrome after all reset styles have been applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b5ec91a-7594-4870-8557-60a772f74b3f/7-create-custom-range-input.png'>Large preview</a>)" alt="Range Input in Chrome after all reset styles have been applied." >}}

## Styling The Track

When styling the track (and the thumb) we will need to target the different browsers specific vendor prefixes in order to apply the proper styles in the relevant element. Going forward, any [pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements) prefixed with `-webkit` will be applied to the Chrome, Safari, Opera and Edge (post-Chromium) browsers. Anything prefixed with `-moz` pertains to Firefox.

Below are the pseudo-elements we will use to target the track:

- `::-webkit-slider-runnable-track`  
Targets the ***track*** in Chrome, Safari, and Edge Chromium.
- `::-moz-range-track`  
Targets the ***track*** in Firefox.

<pre><code class="language-css">                        /***** Track Styles *****/
/***** Chrome, Safari, Opera, and Edge Chromium *****/
input[type="range"]::-webkit-slider-runnable-track {
  background: #053a5f;
  height: 0.5rem;
}

/******** Firefox ********/
input[type="range"]::-moz-range-track {
  background: #053a5f;
  height: 0.5rem;
}</code></pre>

The only required properties for the track are the `height` and `background`. However, it is common to see a `border-radius` applied in order to round out the edges.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78914328-171c-4cb6-90f0-0cb3d4461f0f/8-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78914328-171c-4cb6-90f0-0cb3d4461f0f/8-create-custom-range-input.png" width="800" height="213" sizes="100vw" caption="Range Input in Firefox after the track styles have been applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78914328-171c-4cb6-90f0-0cb3d4461f0f/8-create-custom-range-input.png'>Large preview</a>)" alt="Range Input in Firefox after the track styles have been applied." >}}

## Styling The Thumb

Styling the thumb (the middle knob that the user moves) has more nuances that need to be considered since there are more inconsistencies between the browsers on that part of the range input. 

Below are the pseudo-elements we will use to target the thumb:

- `::-webkit-slider-thumb`  
Targets the ***thumb*** in Chrome, Safari, and Edge Chromium.
- `::-moz-range-thumb`  
Targets the ***thumb*** in Firefox.

Since Firefox and the Webkit browsers have different styling problems, I will address each issue individually and demonstrate how to handle each of the quirky defaults that get applied to the thumb.

{{% ad-panel-leaderboard %}}

### Chrome, Safari, Edge Chromium (Webkit)

The first style we need to apply to the `::-webkit-slider-thumb` pseudo-element is the `-webkit-appearance: none;` vendor prefix. We used this property within the “Baseline Styles” section to override the general default styles that are applied by the browser and it serves a similar purpose on the thumb. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c9b8ca4-812a-4225-98d2-f9ed194541a5/9-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c9b8ca4-812a-4225-98d2-f9ed194541a5/9-create-custom-range-input.png" width="800" height="165" sizes="100vw" caption="Range Input in Chrome after <code>-webkit-appearance: none;</code> is applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c9b8ca4-812a-4225-98d2-f9ed194541a5/9-create-custom-range-input.png'>Large preview</a>)" alt="Range Input in Chrome after <code>-webkit-appearance: none;</code> is applied" >}}

Once the default styles are removed, we can then apply our own custom styles. Assuming we apply a `height`, `width` and `background-color` to the thumb, here is an example of what we would have so far:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee69d2e5-e91c-4c48-8a34-10d1e16c17be/10-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee69d2e5-e91c-4c48-8a34-10d1e16c17be/10-create-custom-range-input.png" width="800" height="137" sizes="100vw" caption="Range input in Chrome with custom thumb styles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee69d2e5-e91c-4c48-8a34-10d1e16c17be/10-create-custom-range-input.png'>Large preview</a>)" alt="Range input in Chrome with custom thumb styles." >}}

By default, the WebKit browsers render the thumb so that it is not centered on the track.

In order to properly center the thumb on the track we can use the following formula and apply it to the [`margin-top`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top) property: 

<blockquote>margin-top = (track height in pixels / 2) - (thumb height in pixels /2)</blockquote>

Taking the styles we have applied in the previous sections and converting `rems` to pixels we would have a track height of 8px and a thumb height of 32px. This would mean that:

<blockquote>margin-top = (8/2) - (32/2) = 4 - 16 = -12px</blockquote>

Based on this, our finalized styles for the webkit browsers would look like the following code block:

<pre><code class="language-css">/***** Thumb Styles *****/
/***** Chrome, Safari, Opera, and Edge Chromium *****/
input[type="range"]::-webkit-slider-thumb {
   -webkit-appearance: none; /* Override default look */
   appearance: none;
   margin-top: -12px; /* Centers thumb on the track */
   background-color: #5cd5eb;
   height: 2rem;
   width: 1rem;    
}</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/772082cc-f388-4d25-b5d2-415fdf1a39a7/11-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/772082cc-f388-4d25-b5d2-415fdf1a39a7/11-create-custom-range-input.png" width="800" height="181" sizes="100vw" caption="Range Input in Chrome after all styles have been applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/772082cc-f388-4d25-b5d2-415fdf1a39a7/11-create-custom-range-input.png'>Large preview</a>)" alt="Range Input in Chrome after all styles have been applied." >}}

### Firefox

When applying styles to the thumb in Firefox, you will need to leverage the `::-moz-range-thumb` pseudo-element. Thankfully, Firefox does not suffer from the same centering issue as the Webkit browsers. However, it’s one gotcha is around the default border-radius and grey border that it applies to the thumb.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f0edf50-50a5-4b8c-bc9a-6138d060378c/12-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f0edf50-50a5-4b8c-bc9a-6138d060378c/12-create-custom-range-input.png" width="800" height="209" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f0edf50-50a5-4b8c-bc9a-6138d060378c/12-create-custom-range-input.png'>Large preview</a>)" alt="Range Input in Firefox with grey border and border-radius applied by default." >}}

In order to remediate the default grey border we can add the `border: none;` property. To remove the default border-radius that gets applied, we can add the `border-radius: 0` property and now the thumb will look consistent across all the browsers. 

Based on this our finalized styles for the Firefox browser would look like this:

<pre><code class="language-css">/***** Thumb Styles *****/
/***** Firefox *****/
input[type="range"]::-moz-range-thumb {
    border: none; /*Removes extra border that FF applies*/
    border-radius: 0; /*Removes default border-radius that FF applies*/
    background-color: #5cd5eb;
    height: 2rem;
    width: 1rem;
}</code></pre>

**Note:** *The Webkit browsers do not automatically apply this radius to the border so if you find that you do want to apply some form of border-radius to the thumb, as opposed to canceling it out as we’ve done above, you will need to apply the desired `border-radius` dimensions to both the `-webkit-slider-thumb` and `::-moz-range-thumb` pseudo-elements.*

## Focus Styles

Because the range input is an interactive element, it is imperative to add focus styles to comply with accessibility best practices and standards. When focus styles are applied, it provides a visual indicator to users and is especially important for those using a keyboard to navigate a page.

According to the [WAI-ARIA: Slider documentation](https://w3c.github.io/aria-practices/#slider), it is recommended that: 

> Focus is placed on the slider (the visual object that the mouse user would move, also known as the thumb).

The first thing we will want to do is remove the default focus styles so that we can override them with custom styles. In order to target the thumbs focus styles, we can leverage the `::-webkit-slider-thumb` and `::-moz-range-thumb` pseudo-elements that we used in the previous section and combine them with the [`:focus`](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus) [psuedo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus). We can then use the CSS [outline](https://developer.mozilla.org/en-US/docs/Web/CSS/outline) and [outline-offset](https://developer.mozilla.org/en-US/docs/Web/CSS/outline-offset) properties to style it the way we want.

<pre><code class="language-css">/***** Focus Styles *****/
/* Removes default focus */
input[type="range"]:focus {
  outline: none;
}

/***** Chrome, Safari, Opera, and Edge Chromium *****/
input[type="range"]:focus::-webkit-slider-thumb {
  border: 1px solid #053a5f;
  outline: 3px solid #053a5f;
  outline-offset: 0.125rem;
}

/******** Firefox ********/
input[type="range"]:focus::-moz-range-thumb {
  border: 1px solid #053a5f;
  outline: 3px solid #053a5f;
  outline-offset: 0.125rem;     
}</code></pre>

**Note**: *If a `border-radius` is applied to the thumb, Firefox renders an outline in the* ***shape of the thumb*** *while the other browsers display a blocky outline. Unfortunately, there is not a simple CSS fix for this and it is the only inconsistency that will be present. However, the main purpose of adding these styles is for accessibility purposes and the main goal, providing a visual indicator when the element is focused, is still achieved.*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa725e79-ffbb-4df6-9686-4780c5a32349/13-create-custom-range-input.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa725e79-ffbb-4df6-9686-4780c5a32349/13-create-custom-range-input.png" width="800" height="207" sizes="100vw" caption="Range Input in Chrome with custom focus styles applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa725e79-ffbb-4df6-9686-4780c5a32349/13-create-custom-range-input.png'>Large preview</a>)" alt="Range Input in Chrome with custom focus styles applied." >}}

{{% ad-panel-leaderboard %}}

## Putting It All Together

Now that we’ve covered all the styles needed to uniform the range input, here’s what the final CSS stylesheet will look like:

<pre><code class="language-css">/********** Range Input Styles **********/
/*Range Reset*/
input[type="range"] {
   -webkit-appearance: none;
    appearance: none;
    background: transparent;
    cursor: pointer;
    width: 15rem;
}

/* Removes default focus */
input[type="range"]:focus {
  outline: none;
}

/***** Chrome, Safari, Opera and Edge Chromium styles *****/
/* slider track */
input[type="range"]::-webkit-slider-runnable-track {
   background-color: #053a5f;
   border-radius: 0.5rem;
   height: 0.5rem;  
}

/* slider thumb */
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none; /* Override default look */
   appearance: none;
   margin-top: -12px; /* Centers thumb on the track */

   /*custom styles*/
   background-color: #5cd5eb;
   height: 2rem;
   width: 1rem;
}

input[type="range"]:focus::-webkit-slider-thumb {   
  border: 1px solid #053a5f;
  outline: 3px solid #053a5f;
  outline-offset: 0.125rem; 
}

/******** Firefox styles ********/
/* slider track */
input[type="range"]::-moz-range-track {
   background-color: #053a5f;
   border-radius: 0.5rem;
   height: 0.5rem;
}

/* slider thumb */
input[type="range"]::-moz-range-thumb {
   border: none; /*Removes extra border that FF applies*/
   border-radius: 0; /*Removes default border-radius that FF applies*/

   /*custom styles*/
   background-color: #5cd5eb;
   height: 2rem;
   width: 1rem;
}

input[type="range"]:focus::-moz-range-thumb {
  border: 1px solid #053a5f;
  outline: 3px solid #053a5f;
  outline-offset: 0.125rem; 
}
</code></pre>
    
## Conclusion

In addition to the methods outlined throughout the article, you can also take advantage of the [range input CSS generator](https://range-input-css.netlify.app/) I created called **range-input.css**. The crux of this project was to create a tool that makes this process simpler for developers. The CSS generator allows you to quickly style common CSS properties and provides a demo slider that displays a real-time preview of the styles you want to apply. 

Hopefully, styling range inputs will be simpler in the future. However, until that day comes, knowing which pseudo-elements and vendor prefixes to target will help you get well on your way to styling sliders to suit your needs.

### Further Resources On Smashing Magazine

- [CSS Generators](https://www.smashingmagazine.com/2021/03/css-generators/)
- [Simplifying Form Styles With `accent-color`](https://www.smashingmagazine.com/2021/09/simplifying-form-styles-accent-color/)
- [Smart CSS Solutions For Common UI Challenges](https://www.smashingmagazine.com/2021/10/modern-css-solutions-for-common-problems/)
- [A Deep Dive Into `object-fit` And `background-size` In CSS](https://www.smashingmagazine.com/2021/10/object-fit-background-size-css/)

{{< signature "vf, yk, il" >}}
