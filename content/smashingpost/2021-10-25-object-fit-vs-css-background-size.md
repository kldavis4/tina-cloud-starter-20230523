---
title: 'A Deep Dive Into object-fit And background-size In CSS'
slug: object-fit-background-size-css
author: ahmad-shadeed
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19e7f717-46d5-4949-96f4-671f4744d0e1/object-fit-background-size-css.jpg
date: 2021-10-25T13:00:00.000Z
summary: >-
  In this article, we will go through how `object-fit` and `background-size` work, when we can use them, and why, along with some practical use cases and recommendations. Let’s dive in.
description: >-
  In this article, we will go through how `object-fit` and `background-size` work, when we can use them, and why, along with some practical use cases and recommendations. Let’s dive in.
categories:
  - Tools
  - CSS
  - Browsers
  - Techniques
---

We’re not always able to load different-sized images for an HTML element. If we use a width and height that isn’t proportional to the image’s aspect ratio, the image might either be compressed or stretched. That isn’t good, and it can be solved either with `object-fit` for an `img` element or by using `background-size`.

First, let’s define the problem. Consider the following figure:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb4530e2-8132-4b2c-8571-5c17403b691c/1-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb4530e2-8132-4b2c-8571-5c17403b691c/1-object-fit-vs-css-background-size.jpg" width="800" height="339" sizes="100vw" caption="A good-looking photo that gets squeezed when used in a card component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb4530e2-8132-4b2c-8571-5c17403b691c/1-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="A good-looking photo and a squeezed image in comparison" >}}

Why is this happening?

An image will have an aspect ratio, and the browser will fill the containing box with that image. If the image’s aspect ratio is different than the width and height specified for it, then the result will be either a squeezed or stretched image.

We see this in the following figure:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9612f8-1aaf-48a1-ab7e-8602cffa254f/2-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9612f8-1aaf-48a1-ab7e-8602cffa254f/2-object-fit-vs-css-background-size.jpg" width="800" height="" sizes="100vw" caption="The image’s aspect ratio is different than the containing box, and the image gets stretched. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9612f8-1aaf-48a1-ab7e-8602cffa254f/2-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="A good-looking photo and a stretched image in comparison" >}}

## The Solution

We don’t always need to add a different-sized image when the aspect ratio of the image doesn’t align with the containing element’s width and height. Before diving into CSS solutions, I want to show you how we used to do this in photo-editing apps:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2592a2fd-4af4-463c-a923-36c7400d016a/3-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2592a2fd-4af4-463c-a923-36c7400d016a/3-object-fit-vs-css-background-size.jpg" width="800" height="438" sizes="100vw" caption="First, we would center the image vertically, and then clip in a mask. This retains the image’s aspect ratio and prevents it from being squeezed. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2592a2fd-4af4-463c-a923-36c7400d016a/3-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="Example of an image with top and bottom edges cropped in a mask" >}}

Now that we understand how that works, let’s get into how this works in the browser. (*Spoiler alert: It’s easier!*)

## CSS `object-fit`

The `object-fit` property defines how the content of a replaced element such as `img` or `video` should be resized to fit its container. The default value for `object-fit` is `fill`, which can result in an image being squeezed or stretched.

Let’s go over the possible values.

{{% feature-panel %}}

## Possible Values for `object-fit`

### `object-fit: contain`

In this case, the image will be resized to fit the aspect ratio of its container. If the image’s aspect ratio doesn’t match the container’s, it will be letterboxed.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b89f31a5-2331-4e8b-83b6-1e4236ab9c3f/4-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b89f31a5-2331-4e8b-83b6-1e4236ab9c3f/4-object-fit-vs-css-background-size.jpg" width="800" height="268" sizes="100vw" caption="When using <code>object-fit: contain</code>, the image will be either letterboxed or resized accordingly. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b89f31a5-2331-4e8b-83b6-1e4236ab9c3f/4-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="object-fit: contain" >}}

### `object-fit: cover`

Here, the image will also be resized to fit the aspect ratio of its container, and if the image’s aspect ratio doesn’t match the container’s, then it will be clipped to fit.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2014cca8-1d63-4ba4-972a-8df125d95ff1/5-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2014cca8-1d63-4ba4-972a-8df125d95ff1/5-object-fit-vs-css-background-size.jpg" width="800" height="268" sizes="100vw" caption="When using <code>object-fit: cover</code>, the image will be either clipped to fit or resized accordingly. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2014cca8-1d63-4ba4-972a-8df125d95ff1/5-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="object-fit: cover" >}}

### `object-fit: fill`

With this, the image will be resized to fit the aspect ratio of its container, and if the image’s aspect ratio doesn’t match the container’s, it will be either squeezed or stretched. We don’t want that.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25952e19-9887-4c23-a82e-c99526abbc99/6-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25952e19-9887-4c23-a82e-c99526abbc99/6-object-fit-vs-css-background-size.jpg" width="800" height="253" sizes="100vw" caption="When using <code>object-fit: fill</code>, the image will be squeezed, stretched, or resized accordingly. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25952e19-9887-4c23-a82e-c99526abbc99/6-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="object-fit: fill" >}}

### `object-fit: none`

In this case, the image won’t be resized at all, neither stretched nor squeezed. It works like the `cover` value, but it doesn’t respect its container’s aspect ratio.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26496e78-d65c-4adb-a181-9f018552f3e9/7-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26496e78-d65c-4adb-a181-9f018552f3e9/7-object-fit-vs-css-background-size.jpg" width="800" height="253" sizes="100vw" caption="When using <code>object-fit: none</code>, the image won’t be resized if the its dimensions are not the same. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26496e78-d65c-4adb-a181-9f018552f3e9/7-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="object-fit: none" >}}

Aside from `object-fit`, we also have the `object-position` property, which is responsible for positioning an image within its container.

## Possible Values For `object-position`

The `object-position` property works similar to CSS’ `background-position` property:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59111ec-674f-40b0-9291-e33a51b5c595/8-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59111ec-674f-40b0-9291-e33a51b5c595/8-object-fit-vs-css-background-size.jpg" width="800" height="237" sizes="100vw" caption="Most of the time, the default value is used (i.e. `center` or `50% 50%`). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59111ec-674f-40b0-9291-e33a51b5c595/8-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="object-position center, left, right" >}}

The `top` and `bottom` keywords also work when the aspect ratio of the containing box is vertically larger:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e538d2-7f9e-464f-9859-3e8b9da4b8e7/9-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e538d2-7f9e-464f-9859-3e8b9da4b8e7/9-object-fit-vs-css-background-size.jpg" width="800" height="237" sizes="100vw" caption="Comparing <code>object-position: top</code> (left) and <code>object-position: bottom</code> (right). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e538d2-7f9e-464f-9859-3e8b9da4b8e7/9-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="object-position top and bottom" >}}

## CSS `background-size`

With `background-size`, the first difference is that we’re dealing with the background, not an HTML (`img`) element.

### Possible Values for `background-size`

The possible values for `background-size` are `auto`, `contain`, and `cover`.

### `background-size: auto`

With `auto`, the image will stay at its default size:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a07dc6-3ae3-4cfe-859f-87c3b75037fb/10-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a07dc6-3ae3-4cfe-859f-87c3b75037fb/10-object-fit-vs-css-background-size.jpg" width="800" height="268" sizes="100vw" caption="Keep in mind that the default size may sometimes result in a blurry image (if it’s too small). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a07dc6-3ae3-4cfe-859f-87c3b75037fb/10-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="background-size: auto" >}}

### `background-size: cover`

Here, the image will be resized to fit in the container. If the aspect ratios are not the same, then the image will be masked to fit.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a91ed8b-23f0-4e90-9b47-187fe742cfed/11-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a91ed8b-23f0-4e90-9b47-187fe742cfed/11-object-fit-vs-css-background-size.jpg" width="800" height="258" sizes="100vw" caption="When using <code>background-size: cover</code>, make sure to consider the aspect ratios of an image. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a91ed8b-23f0-4e90-9b47-187fe742cfed/11-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="background-size: cover" >}}

### `background-size: contain`

In this case, the image will be resized to fit in the container. If the aspect ratios are off, then the image will be letterboxed as shown in the next example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cdcccbf-88ae-46ac-98d9-7596fa160535/12-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cdcccbf-88ae-46ac-98d9-7596fa160535/12-object-fit-vs-css-background-size.jpg" width="800" height="258" sizes="100vw" caption="<code>background-size: contain</code> resizes the image to fit in the container. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cdcccbf-88ae-46ac-98d9-7596fa160535/12-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="background-size: contain" >}}

As for `background-position`, it’s similar to how `object-position` works. The only difference is that the default position of `object-position` is different than that of `background-position`.

{{% ad-panel-leaderboard %}}

## When Not to Use `object-fit` or `background-size`

If the element or the image is given a fixed height and has either `background-size: cover` or `object-fit: cover` applied to it, there will be a point where the image will be too wide, thus losing important detail that might affect how the user perceives the image.

Consider the following example in which the image is given a fixed height:

<pre><code class="language-css">.card__thumb {
    height: 220px;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fad9813-b8a6-4b98-9f05-514c2100bfe4/13-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fad9813-b8a6-4b98-9f05-514c2100bfe4/13-object-fit-vs-css-background-size.jpg" width="800" height="328" sizes="100vw" caption="The image shown on the right is too wide because it has a fixed height while the card’s container is too wide. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fad9813-b8a6-4b98-9f05-514c2100bfe4/13-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="An example where an image is too wide as it has a fixed height, and the card’s container is too wide" >}}

If the card’s container is too wide, it will result in what we see on the right (an image that is too wide). That is because we are not specifying an aspect ratio.

There is only one of two fixes for this. The first is to use the [padding hack](https://alistapart.com/article/creating-intrinsic-ratios-for-video/) to create an intrinsic ratio.

<pre><code class="language-css">.card__thumb {
    position: relative;
    padding-bottom: 75%;
    height: 0;
}

.card__thumb img {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
}</code></pre>

The second fix is to use the new `aspect-ratio` CSS property. Using it, we can do the following:

<pre><code class="language-css">.card__thumb img {
    aspect-ratio: 4 / 3;
}</code></pre>

**Note**: *I’ve already written about the `aspect-ratio` property in detail in case you want to learn about it: “[Let’s Learn About Aspect Ratio In CSS](https://ishadeed.com/article/css-aspect-ratio/)”.*

{{% ad-panel-leaderboard %}}

## Use Cases And Examples

### User Avatars

A perfect use case for `object-fit: cover` is user avatars. The aspect ratio allowed for an avatar is often square. Placing an image in a square container could distort the image.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6370423-39f5-4ae9-b3c1-ea92a6492a91/14-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6370423-39f5-4ae9-b3c1-ea92a6492a91/14-object-fit-vs-css-background-size.jpg" width="800" height="258" sizes="100vw" caption="A comparison of a user avatar without <code>object-fit</code> and with <code>object-fit: cover</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6370423-39f5-4ae9-b3c1-ea92a6492a91/14-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="A user avatar without object-fit and with object-fit: cover" >}}

<pre><code class="language-css">.c-avatar {
    object-fit: cover;
}</code></pre>

### Logos List

Listing the clients of a business is important. We will often use logos for this purpose. Because the logos will have different sizes, we need a way to resize them without distorting them.

Thankfully, `object-fit: contain` is a good solution for that.

<pre><code class="language-css">.logo__img {
    width: 150px;
    height: 80px;
    object-fit: contain;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29bc3a9c-e2d7-4c8b-8a41-d12200edd257/15-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29bc3a9c-e2d7-4c8b-8a41-d12200edd257/15-object-fit-vs-css-background-size.jpg" width="800" height="195" sizes="100vw" caption="Using <code>object-fit: contain</code> can help us resize clients’ logos without distorting them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29bc3a9c-e2d7-4c8b-8a41-d12200edd257/15-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="A list of logos: Airbnb, Domino’s Pizza, Apple Pay, Amazon " >}}

### Article Thumbnail

This is a very common use case. The container for an article thumbnail might not always have an image with the same aspect ratio. This issue should be fixed by the content management system (CMS) in the first place, but it isn’t always.

<pre><code class="language-css">.article__thumb {
    object-fit: cover;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5a9bc9d-2446-4014-9a2a-9eb21cd5cd48/16-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5a9bc9d-2446-4014-9a2a-9eb21cd5cd48/16-object-fit-vs-css-background-size.jpg" width="800" height="339" sizes="100vw" caption="Adjusting article thumbnails with a bit of help from <code>object-fit: cover</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5a9bc9d-2446-4014-9a2a-9eb21cd5cd48/16-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="Article thumbnail" >}}

### Hero Background

In this use case, the decision of whether to use an `img` element or a CSS background will depend on the following:

- Is the image important? If CSS is disabled for some reason, would we want the user to see the image?
- Or is the image’s purpose merely decorative?

Based on our answer, we can decide which feature to use. If the image is **important**:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6ed2e85-f185-4387-9ebf-33a148bcf911/17-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6ed2e85-f185-4387-9ebf-33a148bcf911/17-object-fit-vs-css-background-size.jpg" width="800" height="339" sizes="100vw" caption="Let’s suppose that the image is important, because it’s a food-related website. 😉 (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6ed2e85-f185-4387-9ebf-33a148bcf911/17-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="Use case with a hero background" >}}

<pre><code class="language-html">&lt;section class="hero"&gt;
    &lt;img class="hero__thumb" src="thumb.jpg" alt="" /&gt;
&lt;/section&gt;</code></pre>

<pre><code class="language-css">.hero {
    position: relative;
}

.hero__thumb {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;    
}</code></pre>

If the image is **decorative**, we can go with `background-image`:

<pre><code class="language-css">.hero {
    position: relative;
    background-image: linear-gradient(to top, #a34242, rgba(0,0,0,0), url("thumb.jpg");
    background-repeat: no-repeat;
    background-size: cover;
}</code></pre>

The CSS is shorter in this case. Make sure that any [text placed over the image](https://ishadeed.com/article/handling-text-over-image-css/) is readable and accessible.

### Adding a Background to an Image With `object-fit: contain`

Did you know that you can add a background color to `img`? We would benefit from that when also using `object-fit: contain`.

In the example below, we have a grid of images. When the aspect ratios of the image and the container are different, the background color will appear.

<pre><code class="language-css">img {
    object-fit: contain;
    background-color: #def4fd;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7f0ee22-0621-4329-aa03-2ac78f55bbd5/18-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7f0ee22-0621-4329-aa03-2ac78f55bbd5/18-object-fit-vs-css-background-size.jpg" width="800" height="261" sizes="100vw" caption="We can use <code>object-fit: contain</code> to add a background color to an image. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7f0ee22-0621-4329-aa03-2ac78f55bbd5/18-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="Adding a background color to an image with object-fit: contain" >}}

### Video Element

Have you ever needed a `video` as a background? If so, then you probably wanted it to take up the full width and height of its parent.

<pre><code class="language-css">.hero {
    position: relative;
    background-color: #def4fd;
}

.hero__video {
    position: aboslute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3bb7a1-b82c-4459-849f-a0dbb81fbbee/19-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3bb7a1-b82c-4459-849f-a0dbb81fbbee/19-object-fit-vs-css-background-size.jpg" width="800" height="414" sizes="100vw" caption="The default <code>object-fit</code> value for the <code>video</code> element is <code>contain</code>. As you can see here, the video doesn’t cover the hero background, even though it has <code>position: absolute</code>, <code>width: 100%</code>, and <code>height: 100%</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3bb7a1-b82c-4459-849f-a0dbb81fbbee/19-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="A figure where the video doesn’t cover the hero background" >}}

To make it fully cover the width and height of its parent, we need to override the default `object-fit` value:

<pre><code class="language-css">.hero__video {
    /* other styles */
    object-fit: cover;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b524670a-5a57-44f7-a0b8-53c5b0d00108/20-object-fit-vs-css-background-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b524670a-5a57-44f7-a0b8-53c5b0d00108/20-object-fit-vs-css-background-size.jpg" width="800" height="414" sizes="100vw" caption="Now the video covers the full width and height of its parent. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b524670a-5a57-44f7-a0b8-53c5b0d00108/20-object-fit-vs-css-background-size.jpg'>Large preview</a>)" alt="A figure where the video covers the full width and height of its parent." >}}

## Conclusion

As we’ve seen, both `object-fit` and `background-size` are very useful for handling different image aspect ratios. We won’t always have control over setting the perfect dimensions for each image, and that’s where these two CSS features shine.

A friendly reminder on the accessibility implications of choosing between an `img` element and a CSS background: If the image is purely decorative, then go for a CSS background. Otherwise, an `img` is more suitable.

I hope you’ve found this article useful. Thank you for reading.

{{< signature "vf, yk, il, al" >}}
