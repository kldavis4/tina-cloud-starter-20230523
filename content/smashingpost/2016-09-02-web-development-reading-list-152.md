---
title: >-
  Web Development Reading List #152: On Not Shipping, Pure JS Functions, And
  SameSite Cookies
slug: web-development-reading-list-152
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29fe974f-3b2a-419c-b62a-d7f7b42a925d/wdrl-152-opt.png'
date: 2016-09-02T16:35:36.000Z
author: anselm-hannemann
description: >-
  This week’s reading list consists of a lot of little, smart details that you
  can use on websites. From tweaking the user’s reading experience during page
  load to pure JavaScript functions and verifying the integrity of external
  assets. And finally, we see some articles on thinking differently about
  established working habits — be it working on AI without data or the virtue of
  not shipping a feature.

  Please note that I’ll be on vacation for the next four weeks, so **please
  don’t expect any new Web Development Reading List before October, 7th**. Enjoy
  September, your work, your life!
categories:
  - Web Development Reading List
---
This week’s reading list consists of a lot of little, smart details that you can use on websites. From tweaking the user’s reading experience during page load to pure JavaScript functions and verifying the integrity of external assets. And finally, we see some articles on thinking differently about established working habits — be it working on AI without data or the virtue of not shipping a feature.

Please note that I’ll be on vacation for the next four weeks, so **please don’t expect any new Web Development Reading List before October, 7th**. Enjoy September, your work, your life!

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Local Storage And How To Use It On Websites](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)
*   [Meet “Inclusive Front-End Design Patterns”, A New Smashing Book](https://www.smashingmagazine.com/inclusive-design-patterns/)
*   [Thinking Inside The Box With Vanilla JavaScript](https://www.smashingmagazine.com/2013/10/inside-the-box-with-vanilla-javascript/)
*   [Ways To Reduce Content Shifting On Page Load](https://www.smashingmagazine.com/2016/08/ways-to-reduce-content-shifting-on-page-load/)

## General

*   Jason Zimdars explains [why not shipping a feature can be a virtue](https://m.signalvnoise.com/not-shipping-is-a-virtue-b880badb623c). An article about hidden costs and why shipping does not equal success.
*   While many think Apple isn’t in the Artificial Intelligence game, [this exclusive look gives some insights](https://backchannel.com/an-exclusive-look-at-how-ai-and-machine-learning-work-at-apple-8dbfb131932b) into why Apple handles things differently. An interesting read that reveals how Apple tries to do Artificial Intelligence with less user data and without tracking you — contrary to the industry’s big players.

{{% feature-panel %}}

<figure><a href="https://m.signalvnoise.com/not-shipping-is-a-virtue-b880badb623c"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d67af6e9-abfc-4255-9a1c-284000e552f0/not-shipping-opt.png" width="500" height="297" alt="Cancel button" /></a><figcaption><a href="https://m.signalvnoise.com/not-shipping-is-a-virtue-b880badb623c">Not shipping can be a virtue</a>. Jason Zimdars shares how one of the most important features he ever designed for Basecamp didn’t make it into the product. (Image credit: <a href="https://m.signalvnoise.com/not-shipping-is-a-virtue-b880badb623c">Jason Zimdars</a>)</figcaption></figure>

## Concept & Design

*   [The Web Methodology Project](https://webmethodologyproject.com/guide/) is a fresh guide to building web projects, and even though it’s still a work in progress, it already looks very useful. So keep an eye on it.</p>

## Tools & Workflows

*   Google’s Closure Compiler is one of the best tools out there to compile JavaScript, but so far has only been available as a Java platform tool. Now, the team released a [JavaScript version of Closure Compiler](https://developers.googleblog.com/2016/08/closure-compiler-in-javascript.html) designed to run in Node.js environments. Available on [GitHub](https://github.com/google/closure-compiler-js) or [npm](https://www.npmjs.com/package/google-closure-compiler-js).</p>

## Security

*   It’s now possible to [mitigate MIME confusion attacks in Firefox](https://blog.mozilla.org/security/2016/08/26/mitigating-mime-confusion-attacks-in-firefox/) by sending the header `X-Content-Type-Options: nosniff` to the browsers.
*   I’ve already shared some thoughts on using <abbr title="Sub-Resource Integrity">SRI</abbr>, but now Troy Hunt explains [why it’s important to use it right now](https://www.troyhunt.com/protecting-your-embedded-content-with-subresource-integrity-sri/) if you reference external third-party scripts, for example jQuery, from its CDN.
*   When using cookies on a website, you should [set the `SameSite` option to stop cross-site timing attacks](https://www.igvita.com/2016/08/26/stop-cross-site-timing-attacks-with-samesite-cookies/).</p>

## Accessibility

*   Mischa Andrews on why [making websites and web apps accessible is not super-hard](https://medium.com/@MischaAndrews/the-inaccessible-web-how-we-got-into-this-mess-7cd3460b8e32) yet neglected so often and how we can get out of this mess.

<figure><a href="https://medium.com/@MischaAndrews/the-inaccessible-web-how-we-got-into-this-mess-7cd3460b8e32"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fdf4b5e-7388-48f1-a41f-fbcb9c94db4a/inaccessible-web-opt.png" width="500" height="290" alt="Illustration of a person being left behind as travellers speed away in a futuristic ship" /></a><figcaption>Don’t leave your users behind. Mischa Andrews shares thoughts on <a href="https://medium.com/@MischaAndrews/the-inaccessible-web-how-we-got-into-this-mess-7cd3460b8e32">how we can make the web more accessible</a>. (Original artwork by <a href="https://adamvanwinden.tumblr.com/">Adam Van Winden</a>)</figcaption></figure>

## JavaScript

*   André Staltz explains [the importance of pure functions](https://staltz.com/is-your-javascript-function-actually-pure.html) in JavaScript.
*   React.js comes with its own component model already built-in. However, it can still make sense to [use Web Components in React.js](https://staltz.com/react-could-love-web-components.html) applications as they offer some more advantages of the web platform and are a native web standard.</p>

## CSS/Sass

*   Michael Scharnagl shares some neat [techniques to reduce content shifting during page load](https://www.smashingmagazine.com/2016/08/ways-to-reduce-content-shifting-on-page-load/) to ensure a smooth reading experience for users. By setting intrinsic ratios for media, `font-size-adjust`, or new techniques such as scroll anchoring, you can improve the situation enormously.</p>

## Work & Life

*   Mercedes De Luca explains how [false urgency harms productivity](https://m.signalvnoise.com/its-urgent-really-8050dfe3b921).

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

