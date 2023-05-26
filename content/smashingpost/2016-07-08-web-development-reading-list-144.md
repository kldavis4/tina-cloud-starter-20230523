---
title: >-
  Web Development Reading List #144: CSP Mistakes, JS Debugging And Failure
  Testing
slug: web-development-reading-list-144
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/327103b9-e086-4d8a-b94d-a1bfc41a3fa2/svg-cat-preview-opt.png
date: 2016-07-08T16:51:25.000Z
author: anselm-hannemann
description: >-
  Every week is a learning week and this week I was reminded that viewport units
  are not all good to use. Also, choosing the right HTTP status code can be
  difficult and may not even be supported by the Apache version running on your
  server. I also learned how JavaScript error logging can be extended so that
  you can finally get easy-to-read and useful reports.

  As if that wasn’t enough, I learned a lot about accessibility and progressive
  enhancement again, and discovered a slidedeck on how you can bypass CSP and
  why browsers can render elements with known boundaries as well as layout
  limitations incredibly faster than unknown. Are you ready? It's now your turn
  to learn all of this as well.
categories:
  - Web Development Reading List
---
Every week is a learning week and this week I was reminded that viewport units are not all good to use. Also, choosing the right HTTP status code can be difficult and may not even be supported by the Apache version running on your server. I also learned how JavaScript error logging can be extended so that you can finally get easy-to-read and useful reports.

As if that wasn’t enough, I learned a lot about accessibility and progressive enhancement again, and discovered a slidedeck on how you can bypass CSP and why browsers can render elements with known boundaries as well as layout limitations incredibly faster than unknown. Are you ready? It's now your turn to learn all of this as well.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [iPhone Apps Design Mistakes: Over-Blown Visuals](https://www.smashingmagazine.com/2009/07/iphone-apps-design-mistakes-overblown-visuals/)
*   [Tale Of A Top-10 App, Part 1: Idea And Design](https://www.smashingmagazine.com/2013/07/top-ten-app-part-1-idea-and-design/)
*   [<span class="headline">How To Succeed With Your Mobile App</span>](https://www.smashingmagazine.com/2012/11/succeed-with-your-app/)
*   [The Building Blocks Of Progressive Web Apps](https://www.smashingmagazine.com/2016/09/the-building-blocks-of-progressive-web-apps/)

## Generic

*   These lovely flowcharts will help you decide [which proper HTTP status code your application should respond with](https://racksburg.com/choosing-an-http-status-code/).</p>

## Tools & Workflows

*   [WebPageTest](https://www.webpagetest.org/) is a great tool to test your website for performance issues. However, the tool can do much more than you possibly think. You can simulate a single point of failure (e.g. a 3rd party library timeout) with it, script logins for user-authenticated pages, and integrate it into your CI or run your own instance. Dean Hume has [collected a couple of these tricks](https://www.deanhume.com/Home/BlogPost/ten-things-you-didnt-know-about-webpagetest-org/10145) in his article.

{{% feature-panel %}}

<figure><a href="https://www.deanhume.com/Home/BlogPost/ten-things-you-didnt-know-about-webpagetest-org/10145"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e23476d7-5e2d-48da-9853-f4bdabf74d38/customize-waterfall-link-opt.jpg" alt="" width="500" height="191" /></a><figcaption>Did you know that you can customize the way the waterfall chart appears in WebPageTest? Once you've run a test, click on the waterfall image and scroll down a little bit. You'll notice a link entitled "customize waterfall". (<a href="https://www.deanhume.com/Home/BlogPost/ten-things-you-didnt-know-about-webpagetest-org/10145">Image source</a>)</figcaption></figure>

## Security

*   Content Security Policy [CSP] has great features but also brings its very own issues and risks. Michele Spagnuolo and Lukas Weichselbaum present most common problems, implementation mistakes, some bypasses and how [to make CSP great again](https://speakerdeck.com/mikispag/making-csp-great-again-michele-spagnuolo-and-lukas-weichselbaum) in their slide deck.</p>

## Web Performance

*   [PerfTool](https://devbridge.github.io/Performance/) by the devbridge people is a great npm package to display statistics about your web pages, including Google PageSpeed Insights score, resources count, recommendations how to fix performance issues, HTML errors and many more in one custom web page.</p>

## HTML & SVG

*   Sometimes designers oversimplify a form by removing the labels. The problem is that minimal does not always mean it’s simple — which is certainly the case for labels. [Labels, in fact, are an essential part of designing easy-to-use forms](https://medium.com/simple-human/always-use-a-label-a39ceab554e6).

<figure><a href="https://medium.com/simple-human/always-use-a-label-a39ceab554e6"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d51ffc2-b653-4897-b0f3-06d4e87b96a9/example-label-form-opt.png" alt="Larger hit area helps motor-impaired users activate a control" width="400" height="237" /></a><figcaption>Larger hit area helps motor-impaired users activate a control. (<a href="https://medium.com/simple-human/always-use-a-label-a39ceab554e6">Image source</a>)</figcaption></figure>

## Accessibility

*   Heydon Pickering is writing [a book about “Inclusive Design Patterns”](https://www.smashingmagazine.com/2016/06/inclusive-design-patterns/) and you can pre-order it now. I’ve been able to get some insights already and am quite impressed by the different angles on semantics, progressive enhancement and accessibility in the book and can recommend it if you’re even sightly interested in these topics.
*   Heather Migliorisi wrote [a huge compendium about creating accessible SVGs](https://css-tricks.com/accessible-svgs/) that you should definitely read if you use SVG files in your projects (and who doesn't it?).

{{< codepen height="350" theme_id="0" slug_hash="adQoOJ" data-default-tab="result" caption="A cool SVG cat by Heather Migliorisi" >}} A cool SVG cat by Heather Migliorisi user="hmig"]See the Pen <a href="https://codepen.io/hmig/pen/adQoOJ/">Simple Inline Accessible SVG Cat - using title and desc</a> by Heather Migliorisi (<a href="https://codepen.io/hmig">@hmig</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

## JavaScript

*   Daniel Reis published a few [practical console tricks](https://medium.com/outsystems-experts/beyond-console-debugging-tricks-f7d0d7f5df4) that help you debugging your applications a lot easier. And if you want to go further, [logerr](https://i-break-codes.github.io/logerr/) is an experimental error helper library that can give you manys insights.</p>

## CSS/Sass

*   The CSS layout composition is often quite slow in browsers due to unknown behavior of the elements. Now, if you have an element which, for example, has an `overflow: hidden` set already and is opaque, you can [help the browser to render way faster by supplying a CSS containment information](https://developers.google.com/web/updates/2016/06/css-containment). A similar optimization to `will-change` and likely only a temporary thing that we hopefully won’t need to use for too long or at all.
*   If you’re using `vw` or other viewport units for element sizing, always bear in mind that [viewport-unit sized elements are not user-zoomable](https://mobile.twitter.com/SaraSoueidan/status/749695520143093760). You can try on your own [with this demo](https://codepen.io/vcurd/full/ByerKw). An alternative could be to use `calc(1em + 0.25vw)` or similar calculations that don’t entirely depend on viewport units and therefore are scalable.
*   Firefox 49 arrives next week and with it, [6/8-digit alphatransparent-hex colors will be supported](https://www.fxsitecompat.com/en-CA/docs/2016/support-for-rgba-colour-values-may-validate-previously-invalid-values/) and therefore you should check your sites if you have any of such values by accident because they’ll suddenly be evaluated!

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}

