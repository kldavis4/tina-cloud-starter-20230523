---
title: >-
  Web Development Reading List #138: Accessible Web Components And CSS And Sass
  Precision
slug: web-development-reading-list-138
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6732e764-ad91-48e8-ae1b-4ddbfe6d7992/webdev-reading-list-138-opt.png
date: 2016-05-20T15:53:37.000Z
author: anselm-hannemann
description: >-
  From time to time you need to **recalibrate your brain by experimenting** with
  new technologies, by tracing down the performance of a certain feature or by
  reconsidering the environment of your project. While I’m generally not a
  proponent of inlined CSS, we now will use it for a third-party script we are
  providing to avoid style leakages. The point here is that this decision won’t
  harm performance as it’s an asynchronously loaded script.

  The other thing I always assumed but never got confirmed was that CSS filters
  slow down the rendering of a page massively. But as it turns out, when you
  research this properly, there’s only a barely noticeable difference to
  unfiltered images. Don’t hesitate to try out new things, only make sure that
  it’s the best solution when you put it to production.
categories:
  - Web Development Reading List
---
From time to time you need to <strong>recalibrate your brain by experimenting</strong> with new technologies, by tracing down the performance of a certain feature or by reconsidering the environment of your project. While I’m generally not a proponent of inlined CSS, we now will use it for a third-party script we are providing to avoid style leakages. The point here is that this decision won’t harm performance as it’s an asynchronously loaded script.

The other thing I always assumed but never got confirmed was that CSS filters slow down the rendering of a page massively. But as it turns out, when you research this properly, there’s only a barely noticeable difference to unfiltered images. Don’t hesitate to try out new things, only make sure that it’s the best solution when you put it to production.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Currency Design – Designing The Most Desirable Product](https://www.smashingmagazine.com/2016/01/learn-from-the-history-of-banknote-design-most-desirable-product/)
*   [Testing Credit-Card Numbers In Checkouts](https://www.smashingmagazine.com/2016/07/testing-credit-card-numbers-in-e-commerce-checkouts-cheat-sheet/)
*   [Getting Started With The PayPal API](https://www.smashingmagazine.com/2011/09/getting-started-with-the-paypal-api/)
*   [Free PNG Credit Card, Debit Card and Payment Icons Set](https://www.smashingmagazine.com/2010/10/free-png-credit-card-debit-card-and-payment-icons-set-18-icons/)

## General

*   Have an open-source project that needs to figure out a user’s country by IP? Here’s a free, [simple geolocation API](https://ip2country.info/) to do the job.</p>

## Privacy

*   Privacy International published an interesting [privacy 101 collection](https://privacyinternational.org/privacy-101) on various topics.
*   This guide explains [how websites and apps can comply with the do-not-track settings](https://baycloud.github.io/DNTGuide/) of users and how to use the Consent API to let people opt out of tracking. I would love to see every website that tracks something providing it.</p>

## Web Performance

*   If you [lazy load your images, you shouldn’t rely on JavaScript](https://robinosborne.co.uk/2016/05/16/lazy-loading-images-dont-rely-on-javascript/).</p>

## Accessibility

*   When we talk about accessibility, we usually think about users with well-known disabilities and diseases. However, there’s much more to it than we usually think and this article covers [how to design a dementia-friendly website](https://www.smashingmagazine.com/2016/05/designing-a-dementia-friendly-website/), a topic I haven’t thought about before.
*   Web components received a lot of negative feedback in the past. One major point is that developers need to implement accessibility features completely on their own. Now Artem Tabalin shares [how to make accessible web components](https://www.sitepoint.com/accessible-web-components/) using a multi-select field as an example.

{{% feature-panel %}}

<figure><a href="https://www.sitepoint.com/accessible-web-components/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdb357ed-6210-41f0-bbcc-d0fb8a084913/accessible-web-components-opt.png" alt="Accessibility is vital. To make your web components accessible, too, Artem Tabalin wrote up a brief guide on how to do so." width="500" height="360" /></a><figcaption>Accessibility is vital. To <a href="https://www.sitepoint.com/accessible-web-components/">make your web components accessible</a>, too, Artem Tabalin wrote up a brief guide on how to do so. (Image credit: <a href="https://www.sitepoint.com/accessible-web-components/">Artem Tabalin</a>)</figcaption></figure>

## JavaScript

*   When working with complex animations, doing this entirely in CSS can be quite challenging and messy. “[Getting started with the Web Animations API](https://pawelgrzybek.com/intro-to-the-web-animations-api/)” is a great article introducing an alternative to the CSS-driven approach that you can soon use cross-browser or already now with a polyfill.
*   There are a couple of JavaScript video players out there already. But [Plyr](https://plyr.io/) is a simple, lightweight and accessible media player that you can use for most projects to embed YouTube, Vimeo or self-hosted videos.
*   For React, there are two modules worth mentioning that help you build more accessible applications: The first one is [react-a11y](https://github.com/reactjs/react-a11y) and the second one a [linting config for eslint from the AirBNB React Coding Guidelines](https://github.com/airbnb/javascript/blob/master/packages/eslint-config-airbnb/rules/react-a11y.js).
*   [react-boilerplate v3](https://github.com/mxstbr/react-boilerplate/releases/tag/v3.0.0) is finally out, and if you think about a new React project, I highly recommend to consider using it. It has Service Worker support, a great developer experience and routing included.
*   If you have ever wondered [when to use the `===` or `==` comparison operator in JavaScript](https://bytearcher.com/articles/equality-comparison-operator-javascript/), this article will explain it.</p>

## CSS/Sass

*   What does a browser do when you let it calculate values like `1/3`? In the end, it needs to map it to pixels, and that can sometimes result in small glitches in the design due to sub-pixel interpolation. Learn [what you can do in CSS](https://www.sitepoint.com/a-tale-of-css-and-sass-precision/) and how to set up Sass to get better results.
*   Una Kravets researched [what impact CSS filters, SVG filters, and canvas filters have on images](https://www.smashingmagazine.com/2016/05/web-image-effects-performance-showdown/) compared to pre-edited images. The result is quite interesting as it shows canvas being slowest and SVG and CSS not being notably slower than the no-filter image.</p>

<figure><a href="https://www.sitepoint.com/a-tale-of-css-and-sass-precision/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56bd74e1-f9fc-4937-8aef-2f9c004acda3/css-and-sass-precision-opt.png" alt="Using percentages in CSS can sometimes result in small glitches. Kitty Giraudel tells a tale of CSS and Sass precision and what you can do to get better results." width="500" height="404" /></a><figcaption>Using percentages in CSS can sometimes result in small glitches in the design. Kitty Giraudel tells a <a href="https://www.sitepoint.com/a-tale-of-css-and-sass-precision/">tale of CSS and Sass precision</a> and what you can do to get better results.</figcaption></figure>

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.

<em>Thanks and all the best,
Anselm</em>

