---
title: >-
  The Front-End Performance Challenge: Make Your Site Blazingly Fast And Win Some Smashing Prizes
slug: front-end-performance-challenge
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95c42c97-fb1e-45f0-8e08-cdf7da89789d/performance-challenge-500w-opt.png
date: 2017-10-24T21:24:19.000Z
author: cosima-mielke
description: >-
  Not too long ago, front-end performance was a mere afterthought. Something that was postponed to the end of a project and that didn’t go much beyond minification, asset optimization, and maybe a few adjustments on the server’s `config` file. But things have changed.
categories:
  - Performance
---
Not too long ago, front-end performance was a mere afterthought. Something that was postponed to the end of a project and that didn’t go much beyond minification, asset optimization, and maybe a few adjustments on the server’s `config` file. But things have changed. We have become more conscious of the [impact performance has on the user experience](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/), and the tools and techniques that help us cater for snappy experiences have improved and are widely supported now as well.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e75711f-1456-4bce-b4bb-d8c117ed55db/performance-challenge-800w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e75711f-1456-4bce-b4bb-d8c117ed55db/performance-challenge-800w-opt.png" width="800" height="588" alt="It's time for a new challenge! Are you ready?" /></a><figcaption>It's time for a new challenge! Are you ready?</figcaption></figure>

Time to roll up your sleeves and make use of these possibilities! A while ago, we challenged your coding skills in the [CSS Grid Challenge](https://www.smashingmagazine.com/2017/10/css-grid-challenge-2017-winners/), now we have something new to tickle your brains: The **Front-End Performance Challenge**. A perfect opportunity to apply everything you’ve learned about Service Workers, HTTP/2, Brotli and Zopfli, resource hint and other optimization techniques in one project. And, of course, there’ll be a _smashing_ prize waiting for one lucky winner in the end.</p>

## The Challenge

Show off the performance of your site or your project — use everything you can to **make your website perform blazingly fast**! Please note that the final **visual appearance should be identical before and after** (font loading might differ and reflows are acceptable but should be kept to a minimum). You can use this [checklist](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/) as a guideline and dive into performance optimization for everything from image assets and web fonts delivery to HTTP/2 and Service Workers.

{{% feature-panel %}}

The deadline is the **24<sup>th</sup> of November**, 2017.

Here are a few things you can do to **enhance your chances of winning**:

*   Optimize as much as you can: We’ll be looking into Lighthouse and WebPageTest as well as the complexity of the site you’re working on.
*   You don’t have to optimize a personal blog: The more advanced the project is, the better chances of winning you have.
*   The most critical metrics are the first meaningful paint and the time to interactive.</p>

## So, What Can You Win?

After the deadline has ended, we’ll award a _smashing_ prize to one lucky winner. It has to do with web performance, but see for yourself:

*   A **roundtrip flight to London**,
*   Full accommodation in a fancy hotel,
*   A ticket to [SmashingConf London 2018](https://smashingconf.com/), a new front-end, performance-focused conference, taking place Feb 7–8, 2018,
*   A Smashing workshop of your choice.</p>

## Join In!

Ready to take on the challenge? We’d love to see how you’ll tackle it!

### What You Need To Deliver

*   Performance results before and after (using WebPageTest and Lighthouse).
*   A brief description/strategy of the work you did.

Once you have everything together, please send us your entry to **challenge@smashingmagazine.com**. The deadline is the **24<sup>th</sup> of November**. The winner will be announced on the 4<sup>th</sup> of December, 2017.</p>

## Resources To Get Started

Last but not least, here are some resources to kick-start your performance optimization endeavor. Have fun!

*   **Improving Web Fonts Delivery**  
    Zach Leatherman’s “[Comprehensive Guide To Font Loading Strategies](https://www.zachleat.com/web/comprehensive-webfonts/)” explains the ins and outs of approaches such as FOUT with a Class and Critical FOFT.
*   **Improving CSS Delivery**  
    Dean Hume summarized an easy way to [inline critical CSS](https://www.smashingmagazine.com/2015/08/understanding-critical-css/) into the `<head>` of your pages, even when your site contains different templates.
*   **Getting Started With Service Workers**  
    Lyza Danger Gardner wrote up her gotchas and the bugs she ran into when [making a Service Worker](https://www.smashingmagazine.com/2016/02/making-a-service-worker/). Also be sure to check out her “[Pragmatist’s Guide to Service Workers](https://github.com/lyzadanger/pragmatist-service-worker),” a GitHub repository with Service Worker code examples.
*   **Dealing With Third-Party Scripts**  
    Damien Jubeau shares useful [tips and techniques to deal with third-party content](https://blog.dareboost.com/en/2017/03/third-party-content-performance-security/) such as social network widgets, advertising and tracking scripts, and explains their impact on performance.
*   **Moving To HTTP/2**  
    HTTPS is a must for websites. Vladislav Denishev’s [complete guide to switching from HTTP to HTTPS](https://www.smashingmagazine.com/2017/06/guide-switching-http-https/) helps you master the transition.
*   **HTTP/2 Server Push**  
    Server Push allows you to send site assets to the user before they’ve even asked for them. Jeremy Wagner’s [comprehensive guide to Server Push](https://www.smashingmagazine.com/2017/04/guide-http2-server-push/) explains everything from how it works to the problems it solves.
*   **Progressive Web App**  
    Progressive Web Apps can replace all of the functions of native apps and websites at once. Ada Rose Edwards summarized [do’s and don’ts on how to make them](https://www.smashingmagazine.com/2016/09/the-building-blocks-of-progressive-web-apps/).
*   **Brotli/Zopfli Compression**  
    Do you already use Brotli or Zopfli compression? The lossless data format [Brotli](https://github.com/google/brotli) appears to be more effective than Gzip and Deflate, while [Zopfli](https://blog.codinghorror.com/zopfli-optimization-literally-free-bandwidth/) is a good solution for resources that don’t change much and are designed to be compressed once and downloaded many times.
*   **Resource Hints**  
    [Resource hints](https://w3c.github.io/resource-hints/) are a good way to warm up the connection and speed up delivery, saving time on `dns-prefetch`, `preconnect`, `prefetch`, `prerender` and `preload`.
*   **CDNs Supporting HTTP/2**  
    Concerns over performance have long been a common excuse to avoid security obligations. In reality, TLS has only one performance problem: It’s not used widely enough. [Everything else can be optimized](https://istlsfastyet.com/).
*   **Responsive Images**  
    Eric Portis wrote up [how to get responsive images right](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/) — with `<picture>` and `srcset`.
*   **Caching**  
    If you need a little refresher on caching, [Ilya Grigorik](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=en) and [Jake Archibald](https://jakearchibald.com/2016/caching-best-practices/) have got you covered.
*   **Optimizing For First Meaningful Paint**  
    [First Meaningful Paint](https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint) is the paint after which the biggest above-the-fold layout change has happened. The lower its score, the faster that the page appears to display its primary content.

With all of this, you should be well-equipped for the challenge. Need a checklist? [Here we go.](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/) We’re already looking forward to your submissions and to hearing your optimization stories!

{{< signature "il" >}}

