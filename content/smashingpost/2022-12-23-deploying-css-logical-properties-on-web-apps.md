---
title: 'Deploying CSS Logical Properties On Web Apps'
slug: deploying-css-logical-properties-on-web-apps
author: nicolashoffmann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd6913e4-e4eb-4bc9-8b51-0f8d596ee839/deploying-css-logical-properties-on-web-apps.jpg
date: 2022-12-23T13:00:00.000Z
summary: >-
  You may have already heard of CSS logical properties or RTL adaptations but are still deciding whether to deploy them widely. To help raise your awareness of their possibilities, Nicolas Hoffmann shares his experience of how he and his team at Proton carried out a massive move from CSS logical props to production and how you can consider them from a different perspective in your very own projects.
description: >-
  You may have already heard of CSS logical properties or RTL adaptations but are still deciding whether to deploy them widely. To help raise your awareness of their possibilities, Nicolas Hoffmann shares his experience of how he and his team at Proton carried out a massive move from CSS logical props to production and how you can consider them from a different perspective in your very own projects.
categories:
  - CSS
  - Browsers
  - Responsive Web Design
---

Localization is one of the most interesting fields in terms of user interface: text length may be different depending on the language, default alignments for text might vary, reading direction can be mirrored or vertical, and so many other different cases. In short, it’s an **incredible source of diversity**, which makes our interfaces and our front-end work way stronger, more reliable, and more challenging.

## The Need For Right-To-Left Interfaces

Most languages, like French or English, are meant to be read for Left-To-Right (LTR). However, in these cases, some languages like Farsi (Persian), Arabic, and Hebrew have a different reading direction &mdash; Right-To-Left (RTL).

The question is *how* can we adapt our interfaces to this huge change? 

### Before CSS Logical Properties

Before CSS Logical Properties, we could make RTL adaptations with different methods:

- Adding a dedicated CSS file only for RTL surcharge/layout;
- Surcharging only parts that need to be adapted in the same CSS, e.g. `[dir="rtl"] .float-left { float: right; }`.

Even if these methods are doing the work &mdash; I used the second one to create [an Arabic version of the Stand Up for Human rights website](https://www.standup4humanrights.org/ar/) a few years ago &mdash; both of them are quite sub-optimal:

- You need to maintain another file for the first one;
- The CSS file for the second one is a bit heavier, and there might be some issues to deal with (specificity, more properties to add, and so on).

For sure, we can create huge machinery with Sass to produce several builds and use some tools like UnCSS to remove what is not needed, but let’s be honest: **this is boring, and it can lead to “non-natural” pieces of code**, like in the previous example.

### Why CSS Logical Properties Are A Perfect Fit/Promising 

This is where the [CSS Logical Properties](https://www.w3.org/TR/css-logical-1/) module comes into the game. The main idea of this CSS module is to have a **logical abstraction** that enables us to produce one layout that will adapt itself depending on the text direction and writing mode (properties like `writing-mode`, `direction`, and `text-orientation`, or `dir` attribute in HTML). This gives us possibilities like horizontal right-to-left or left-to-right, vertical RTL, and so on.

## Implementation In Practice

### How It Works

There are a few concepts to understand, already explained by Rachel Andrews here in “[Understanding Logical Properties And Values](https://www.smashingmagazine.com/2018/03/understanding-logical-properties-values/)”:

- We no longer think in terms of `left`/`right` but `start`/`end` (the same goes for `top`/`bottom`):
- We no longer say `width` or `height` but instead `inline` and `block` &mdash; quite classical. (You’ve probably heard of default `inline` or `block` elements. 😉)

This idea of `start`/`end` is not new. You use it probably every day with things like `justify-content: start`.

Congratulations, you now know &mdash; almost &mdash; everything! 🎉 Let’s see some practical examples.

### Examples

Let’s start with the basics:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Classical Property</th>
            <th>Logical Property</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>width</code></td>
            <td><code>inline-size</code></td>
        </tr>
        <tr>
            <td><code>height</code></td>
            <td><code>block-size</code></td>
        </tr>
        <tr>
            <td><code>min-width</code></td>
            <td><code>min-inline-size</code></td>
        </tr>
        <tr>
            <td><code>min-height</code></td>
            <td><code>min-block-size</code></td>
        </tr>
        <tr>
            <td><code>max-width</code></td>
            <td><code>max-inline-size</code></td>
        </tr>
        <tr>
            <td><code>max-height</code></td>
            <td><code>max-block-size</code></td>
        </tr>
    </tbody>
</table>

Margins follow the same logic:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Classical Property</th>
            <th>Logical Property</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>margin-top</code></td>
            <td><code>margin-block-start</code></td>
        </tr>
        <tr>
            <td><code>margin-bottom</code></td>
            <td><code>margin-block-end</code></td>
        </tr>
        <tr>
            <td><code>margin-left</code></td>
            <td><code>margin-inline-start</code></td>
        </tr>
        <tr>
            <td><code>margin-right</code></td>
            <td><code>margin-inline-end</code></td>
        </tr>
    </tbody>
</table>

The same goes for `padding`. Let’s move to the positioning:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Classical Property</th>
            <th>Logical Property</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>top</code></td>
            <td><code>inset-block-start</code></td>
        </tr>
        <tr>
            <td><code>bottom</code></td>
            <td><code>inset-block-end</code></td>
        </tr>
        <tr>
            <td><code>left</code></td>
            <td><code>inset-inline-start</code></td>
        </tr>
        <tr>
            <td><code>right</code></td>
            <td><code>inset-inline-end</code></td>
        </tr>
    </tbody>
</table>

Simple, isn’t it? `float`, `text-align`, and `border` follow the same path:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Classical Property/Value</th>
            <th>Logical Property</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>float: left;</code></td>
            <td><code>float: inline-start;</code></td>
        </tr>
        <tr>
            <td><code>float: right;</code></td>
            <td><code>float: inline-end;</code></td>
        </tr>
        <tr>
            <td><code>text-align: left;</code></td>
            <td><code>text-align: start;</code></td>
        </tr>
        <tr>
            <td><code>text-align: right;</code></td>
            <td><code>text-align: end;</code></td>
        </tr>
        <tr>
            <td><code>border-top</code></td>
            <td><code>border-block-start</code></td>
        </tr>
        <tr>
            <td><code>border-bottom</code></td>
            <td><code>border-block-end</code></td>
        </tr>
        <tr>
            <td><code>border-left</code></td>
            <td><code>border-inline-start</code></td>
        </tr>
        <tr>
            <td><code>border-right</code></td>
            <td><code>border-inline-end</code></td>
        </tr>
    </tbody>
</table>

I won’t detail some others like `resize` or `scroll-margin-top`, but instead, let’s look at the particular case of `border-radius`:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Classical Property</th>
            <th>Logical Property</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>border-top-left-radius</code></td>
            <td><code>border-start-start-radius</code></td>
        </tr>
        <tr>
            <td><code>border-top-right-radius</code></td>
            <td><code>border-start-end-radius</code></td>
        </tr>
        <tr>
            <td><code>border-bottom-left-radius</code></td>
            <td><code>border-end-start-radius</code></td>
        </tr>
        <tr>
            <td><code>border-bottom-right-radius</code></td>
            <td><code>border-end-end-radius</code></td>
        </tr>
    </tbody>
</table>

A bit different, but easily understandable anyway.

Some possibilities with values are really cool &mdash; you can simplify some notations. Here are some further examples:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Classical Property/Value</th>
            <th>Logical Property</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>margin-left: auto;</code><br> <code>margin-right: auto;</code></td>
            <td><code>margin-inline: auto;</code></td>
        </tr>
        <tr>
            <td><code>margin-top: 0;</code><br> <code>margin-bottom: 0;</code></td>
            <td><code>margin-block: 0;</code></td>
        </tr>
        <tr>
            <td><code>margin-top: 1em;</code><br> <code>margin-bottom: 2em;</code></td>
            <td><code>margin-block: 1em 2em;</code></td>
        </tr>
        <tr>
            <td><code>top: 0;</code><br> <code>left: 0;</code><br> <code>bottom: 0;</code><br> <code>right: 0;</code></td>
            <td><code>inset: 0;</code> 🎉</td>
        </tr>
        <tr>
            <td><code>left: 10%;</code><br> <code>right: 10%;</code></td>
            <td><code>inset-inline: 10%;</code></td>
        </tr>
    </tbody>
</table>

This is pure gold in the best world, right? Less code for perfect support of RTL languages! 🎉 

Now I’m sorry to brush away some of the stars in your eyes &mdash; there are indeed some limitations.

{{% feature-panel %}}

### Some Limitations 

#### Missing Syntaxes 

CSS Logical Properties are quite new, even if the support is good on recent browsers. However, the CSS Logical Properties module is kind of “young” and needs a level 2. 

To give a simple example: [our toggle component](https://github.com/ProtonMail/WebClients/blob/main/packages/styles/scss/base/forms/_toggle.scss#L106) is using CSS transforms between different states (loading, active, and so on), mostly because `transform` is a reliable way to have fluid transitions or animations. 

So, we have something like this: 

<pre><code class="language-css">.element {
   transform: translateX(#{$toggle-width - $toggle-width-button});
}
</code></pre>

Unfortunately, there is [no flow-relative syntax for `transform`](https://github.com/w3c/csswg-drafts/issues/1788). So, we have to do something like the following:

<pre><code class="language-css">[dir='rtl'] .element {
    transform: translateX(-#{$toggle-width - $toggle-width-button});
}
</code></pre>

If you want to get an idea of missing stuff like this, you can check [opened issues on CSS logical props](https://github.com/w3c/csswg-drafts/labels/css-logical-2).

#### Shorthand Properties 

Some shorthand notations are not supported for the moment, like the 2, 3, or 4 values for `margin`:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Classical Property/Value</th>
            <th>Logical Property</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>margin: 1em 2em;</code></td>
            <td><code>margin-block: 1em; /* top and bottom */</code> <br> <code>margin-inline: 2em /* left and right */</code></td>
        </tr>
        <tr>
            <td><code>margin: 1em 2em 3em;</code></td>
            <td><code>margin-block: 1em 3em; /* top, bottom */</code> <br> <code>margin-inline: 2em /* left, right */</code></td>
        </tr>
        <tr>
            <td><code>margin: 1em 2em 3em 4em;</code></td>
            <td><code>margin-block: 1em 3em; /* top, bottom */</code> <br> <code>margin-inline: 4em 2em /* left, right */</code></td>
        </tr>
    </tbody>
</table>

Don’t use these classic examples with logical needs. You will encounter issues as it’s actually not working. It’s better to be explicit. Also, it’s more readable, in my opinion.

{{% ad-panel-leaderboard %}}

## Showing Some Real Issues And Some Solutions

### Images Where Reading Direction Is Important

Some images have a direct meaning. Let’s take the example of theme cards:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be125ff8-ca58-4db4-b261-9db9e32c17b4/smashing-themes-ltr.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be125ff8-ca58-4db4-b261-9db9e32c17b4/smashing-themes-ltr.png" width="800" height="519" sizes="100vw" caption="Proton themes in LTR (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be125ff8-ca58-4db4-b261-9db9e32c17b4/smashing-themes-ltr.png'>Large preview</a>)" alt="Proton themes in LTR" >}}

In this case, if we just apply RTL stuff to this, we would get this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da4f9794-f58f-40d5-b994-85346d20bca4/smashing-themes-rtl-wrong.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da4f9794-f58f-40d5-b994-85346d20bca4/smashing-themes-rtl-wrong.png" width="800" height="395" sizes="100vw" caption="Proton themes in RTL, done wrong. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da4f9794-f58f-40d5-b994-85346d20bca4/smashing-themes-rtl-wrong.png'>Large preview</a>)" alt="Proton themes in RTL, done wrong" >}}

The order is RTL, but each image does not look like the interface of an RTL user. It’s the LTR version! In this case, it’s because the image reading direction conveys information.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c2093d6-542c-4100-b59e-87460d85a486/smashing-themes-rtl.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c2093d6-542c-4100-b59e-87460d85a486/smashing-themes-rtl.png" width="800" height="378" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c2093d6-542c-4100-b59e-87460d85a486/smashing-themes-rtl.png'>Large preview</a>)" alt="Proton themes in RTL" >}}

We have a CSS class helper that makes it really simple to achieve this fix:

<pre><code class="language-css">[dir="rtl"] .on-rtl-mirror {
  transform: rotateY(180deg);
}
</code></pre>

This also applies to any image with a reading direction, like an arrow or double chevron icon showing or pointing to something.

### Styles/Values Computed Via JavaScript

Let’s imagine you have a plugin that calculates some positioning in JavaScript and provides the value you can use in JS or CSS. The dropdown library that we’re using provides only the `left` value in both RTL/LTR contexts, and [we transfer to CSS](https://github.com/ProtonMail/WebClients/blob/main/packages/styles/scss/components/_dropdown.scss#L18) using a CSS Custom property.

So, if we were using this with Logical Properties, i.e. `inset-inline-start: calc(var(--left) * 1px);`, we would get the following by clicking on the user dropdown:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11c74e25-e6ba-4941-b2eb-c62a8e21fb95/smashing-dropdown-positionned-badly.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11c74e25-e6ba-4941-b2eb-c62a8e21fb95/smashing-dropdown-positionned-badly.png" width="800" height="443" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11c74e25-e6ba-4941-b2eb-c62a8e21fb95/smashing-dropdown-positionned-badly.png'>Large preview</a>)" alt="User dropdown is opened to the opposite side of the interface, not near its opening button" >}}

The solution is simple here. We keep the non-logical property:

<pre><code class="language-javascript">/&#42; stylelint-disable &#42;/
top: calc(var(--top) &#42; 1px);
left: calc(var(--left) &#42; 1px); // JS provide left value only
/&#42; stylelint-enable &#42;/
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7294a007-afdc-4c87-99e4-d4cae4e082f6/smashing-dropdown-positionned-correctly.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7294a007-afdc-4c87-99e4-d4cae4e082f6/smashing-dropdown-positionned-correctly.png" width="800" height="443" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7294a007-afdc-4c87-99e4-d4cae4e082f6/smashing-dropdown-positionned-correctly.png'>Large preview</a>)" alt="User dropdown is opened near its opening button" >}}

And we disable our linting for this particular case.

### Mixing RTL And LTR content

Even with the best CSS modules, anyone who has already made some RTL adaptations will say that mixing RTL and LTR content sometimes (often) gives crazy stuff. 

Let’s take an example on Proton Drive with a component called `MiddleEllipsis`. The goal of this component is to apply ellipsis before the extension of the file to get something like `my-filename-blahblahblah…blah.jpg`.

Nothing crazy: we split the content into two parts and apply `text-overflow: ellipsis` on the first one. You can check [the source of this `MiddleEllipsis` component](https://github.com/ProtonMail/WebClients/blob/main/packages/components/components/ellipsis/MiddleEllipsis.tsx). 

Let’s apply some good ol’ RTL &mdash; we should then get the following:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13d4f3a2-24e6-433e-9b20-d62e094c0210/smashing-drive-middle-ellipsis-done-wrong.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13d4f3a2-24e6-433e-9b20-d62e094c0210/smashing-drive-middle-ellipsis-done-wrong.png" width="800" height="306" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13d4f3a2-24e6-433e-9b20-d62e094c0210/smashing-drive-middle-ellipsis-done-wrong.png'>Large preview</a>)" alt="File display in Proton Drive, better displayed" >}}

Strange, right? This is simple to explain, however:

- `MiddleEllipsis` structure is RTL;
- And we inject LTR content. (Remember, we did RTL-cut this LTR content.)

The browser does its best, and what is displayed is not wrong from its point of view, but this makes no sense to a person. In this case, we chose to keep the LTR display to keep the purpose of the filenames but aligned it to the right:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7721d8c9-022c-4305-b7fa-3759ff9278ed/smashing-drive-middle-ellipsis-done-better.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7721d8c9-022c-4305-b7fa-3759ff9278ed/smashing-drive-middle-ellipsis-done-better.png" width="800" height="306" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7721d8c9-022c-4305-b7fa-3759ff9278ed/smashing-drive-middle-ellipsis-done-better.png'>Large preview</a>)" alt="File display in Proton Drive, better displayed" >}}

### Searching For Native LTR Patterns

The `MiddleEllipsis` example showed that if user-generated content is LTR, then it’s better to display it as LTR. 

But we can wonder if there are some patterns that are naturally LTR. The short answer is yes. Below you can find an example.

#### Phone Number 

The phone number might be the most obvious case here as it’s usually using western numbers, which are meant to be read LTR.

If we apply Logical props directly to it, it might give the following:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14c80d39-c7e3-49bf-98d1-7c1c7cdc2871/smashing-phone-rtl-wrong.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14c80d39-c7e3-49bf-98d1-7c1c7cdc2871/smashing-phone-rtl-wrong.png" width="800" height="168" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14c80d39-c7e3-49bf-98d1-7c1c7cdc2871/smashing-phone-rtl-wrong.png'>Large preview</a>)" alt="Phone input displayed in RTL, weird display" >}}

While it’s technically not false, it’s a bit weird to display `+33 6 12 34 56 78` like this. In this case, we decided to keep the LTR alignment by default to avoid this strange result.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0202bcc9-9f95-4e02-8703-dfd75fc699d1/smashing-phone-rtl.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0202bcc9-9f95-4e02-8703-dfd75fc699d1/smashing-phone-rtl.png" width="800" height="168" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0202bcc9-9f95-4e02-8703-dfd75fc699d1/smashing-phone-rtl.png'>Large preview</a>)" alt="Phone input displayed in LTR" >}}

We have the same case for a 2FA input using western numbers. We don’t yet have the case but imagine a 4-part input to enter an IP address. This would not make sense to display it fully RTL as people would understand `1.0.163.192` instead of `192.163.0.1`.

### Compatibility

The biggest issue we faced was mostly in regards to compatibility. This can be seen on [Can I Use tables for Logical Props](https://caniuse.com/css-logical-props): 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90118ebb-00fd-4254-98fa-5aeb78a0ca4c/smashing-can-i-use-table-logical-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90118ebb-00fd-4254-98fa-5aeb78a0ca4c/smashing-can-i-use-table-logical-properties.png" width="800" height="479" sizes="100vw" caption="Can I Use tables for Logical Props (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90118ebb-00fd-4254-98fa-5aeb78a0ca4c/smashing-can-i-use-table-logical-properties.png'>Large preview</a>)" alt="Can I Use tables for Logical Props" >}}

If the target is only recent modern browsers, there is no problem. But if there is a need for older versions of Safari, for example, the support is pretty bad. And in this case, CSS Logical Properties are not gracefully degraded. Thus everything might look broken.

Several options are possible:

- Serve a CSS build for modern browsers and another one for older ones;
- Transpile everything for each case.

In Proton’s case, as we were not totally ready to ship an RTL language when we merged it, and for other reasons, the decision was taken to transpile everything to good ol’ classical CSS properties. Recently, we found [a solution](https://github.com/ProtonMail/WebClients/commit/ccc35cc6e7769a426702d94aebb8d213abda3252) for one case that did need RTL support for Farsi language (VPN account):

1. We build two CSS files: one modern with Logical props and one legacy;
2. We load the modern one;
3. We test the correct support of `border-start-start-radius`;
4. If it’s not supported, we fall back to legacy.

## Conclusion

Even if absolute perfection is out of this world, moving to CSS Logical properties is **a really interesting move and a good bet for the future**: we write less code with these CSS Logical Props, and we reduce the amount of future work by using them, so it really goes in an exciting direction.

As the last takeaway, and even if it would need more work, we did some tests of a vertical RTL display to test further CSS Logical properties.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5bac605-24bb-42dd-a649-c616f85f9de7/smashing-vertical-experiment.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5bac605-24bb-42dd-a649-c616f85f9de7/smashing-vertical-experiment.png" width="800" height="586" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5bac605-24bb-42dd-a649-c616f85f9de7/smashing-vertical-experiment.png'>Large preview</a>)" alt="Vertical Right-to-left display, using writing-mode" >}}

Looks quite interesting, doesn’t it? 😉

{{% ad-panel-leaderboard %}} 

### Related Resources

- “[W3C i18n resources](https://www.w3.org/International/)”, W3C.org
- “[RTL Styling 101](https://rtlstyling.com/)”, Ahmad Shadeed
- “[What Languages Use RTL Scripts?](https://www.w3.org/International/questions/qa-scripts.en.html#directions)”, Richard Ishida, W3C
- “[Opened Issues On CSS Logical Props](https://github.com/w3c/csswg-drafts/labels/css-logical-2)”, W3C, GitHub
- “[CSS Logical Properties and Values](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties)”, MDN Web Docs
- “[Unicode Bidirectional Algorithm Basics](https://www.w3.org/International/articles/inline-bidi-markup/uba-basics)”, Richard Ishida, W3C
- “[CSS Logical Properties and Values Level 1](https://www.w3.org/TR/css-logical-1/),” W3C Working Draft
- “[Multilingual Desktop Publishing: Tips & Tricks #3](https://intext.eu/blog/dtp_3.html)”, Kirill Fedotov, InText
- “[Understanding Logical Properties And Values](https://www.smashingmagazine.com/2018/03/understanding-logical-properties-values/)”, Rachel Andrew
  
{{< signature "yk, il" >}}
