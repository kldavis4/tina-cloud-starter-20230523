---
title: >-
  Web Development Reading List #137: The New Let’s Encrypt Client And SSH
  Shortcuts
slug: web-development-reading-list-137
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/753af1d3-a43e-4cce-934c-e750624bb25b/wdrl-137-opt.png'
date: 2016-05-13T19:10:37.000Z
author: anselm-hannemann
description: >-
  This week reminded me again of **how refreshing attending a conference can
  be**. As mentioned, I was at the beyond tellerrand conference and, apart from
  meeting new people, I mostly enjoyed the inspiration I got from listening to
  the great talks.

  I realized how I might be able to solve a few things that had led to me being
  unhappy with my work in the past. My trying-to-change-everything-at-once
  strategy always failed, and seeing that some people just change small things
  and succeed, I recognized that this is what I want to try over the next
  months. And I’m happy that I don’t need to do this alone but have some friends
  who spent nearly the entire Monday night talking with me about how to do more
  meaningful work.
categories:
  - Web Development Reading List
---
This week reminded me again of <strong>how refreshing attending a conference can be</strong>. As mentioned, I was at <a href="https://vimeo.com/channels/beyondtellerrand/">beyondtellerrand</a> and, apart from meeting new people, I mostly enjoyed the inspiration I got from listening to the great talks.

I realized how I might be able to solve a few things that had led to me being unhappy with my work in the past. My trying-to-change-everything-at-once strategy always failed, and seeing that some people just change small things and succeed, I recognized that this is what I want to try over the next months. And I’m happy that I don’t need to do this alone but have some friends who spent nearly the entire Monday night talking with me about how to do more meaningful work.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [World Wide Web, Not Wealthy Western Web](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/)
*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)

Big thanks to all people doing such events and to all of you who listen to me and who talk with me about all the topics that I feel are important! ♥

{{% feature-panel %}}

## Tools & Workflows

*   [Butteraugli](https://github.com/google/butteraugli) is a project that estimates the psychovisual similarity of two images. Y’all likely know that there are very different results from app to app if you use for example a JPEG-compression of `65` — in one app this looks still perfectly fine while others already create unbearable artifacts. Butteraugli tries to solve this by creating a standardized comparison of two images and even claims to work better than [SSIM](https://en.wikipedia.org/wiki/Structural_similarity).
*   Do you know [what to do when your SSH connection freezes](https://blog.infertux.com/2012/12/20/properly-close-a-frozen-ssh-session/)? There’s actually a simple solution for this: Press `[enter]`, then `~`, followed by a `.` to send an escape sequence to your local SSH client to terminate the connection.

<figure><a href="https://blog.infertux.com/2012/12/20/properly-close-a-frozen-ssh-session/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d631de1b-15a5-4d05-9991-f096edf2213d/close-ssh-sessions-opt.png" alt="Simple shortcuts help you close a frozen SSH connection properly." width="500" height="214" /></a><figcaption>Simple shortcuts help you <a href="https://blog.infertux.com/2012/12/20/properly-close-a-frozen-ssh-session/">close a frozen SSH connection properly</a>. (<a href="https://blog.infertux.com/2012/12/20/properly-close-a-frozen-ssh-session/">Image credit</a>)</figcaption></figure>

## Security

*   The Let’s Encrypt client is dead. It was replaced by its successor [certbot](https://certbot.eff.org/) which is a better, more compatible tool than the initial one. [Read here what has changed](https://www.eff.org/deeplinks/2016/05/announcing-certbot-new-tls-robot) and why this has been done.
*   GlobalSign has created a client-side PKI implementation to make certificates more secure. The [open-source JavaScript library pkijs](https://pkijs.org/) implements the formats that are used in PKI applications like signing, encryption, certificate requests, OCSP, and TSP requests/responses. It is built on WebCrypto (Web Cryptography API) and requires no plug-ins. And now, CloudFlare has built [Origin CA](https://blog.cloudflare.com/how-we-built-origin-ca-web-crypto/) with it to make it easier to secure the connection between CloudFlare and the origin server.
*   Sarah Jeong shares the problems with security on computers and [the internet affecting your life through a lack of security in modern banking](https://motherboard.vice.com/read/why-i-hate-security-computers-and-the-entire-modern-banking-system).

<figure><a href="https://blog.cloudflare.com/how-we-built-origin-ca-web-crypto/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e689a6ca-8a22-4edd-a872-f7caa659d497/cloudflare-opt.png" alt="With Origin CA you no longer need to go to a third-party certificate authority to protect the connection between CloudFlare and your origin server." width="500" height="369" /></a><figcaption>With <a href="https://blog.cloudflare.com/how-we-built-origin-ca-web-crypto/">Origin CA</a> you no longer need to go to a third-party certificate authority to protect the connection between CloudFlare and your origin server. (<a href="https://blog.cloudflare.com/how-we-built-origin-ca-web-crypto/">Image credit</a>)</figcaption></figure>

## Web Performance

*   Do you remember [when Facebook researched the efficiency of the browser’s cache](https://wdrl.info/archive/96)? Patrick McManus now made a reference implementation in Firefox to improve the situation by adding a new directive in the `Cache-Control`-header: `immutable`. It indicates that the response body will not change over time and is complementary to the lifetime cachability expressed by `max-age`. Thus, the browser will assume that, if not expired, it’s unchanged and should not be revalidated. The goal is to land support in Firefox 49 and tests have shown that this will make a big difference.
*   Alex Russell wrote up why Service Workers are about more than just an offline experience but also [about providing reliable performance](https://infrequently.org/2016/05/service-workers-and-pwas-its-about-reliable-performance-not-offline/).</p>

## CSS/Sass

*   Michael Riethmuller shares how you can achieve [responsive typography in your layouts with `vh/vw` units and the `calc()` function](https://www.smashingmagazine.com/2016/05/fluid-typography/).</p>

## Work & Life

*   Running good, meaningful, and effective meetings is one of the toughest things at work. And it’s actually a challenge to [run them being fair to introverts, women, remote workers](https://hbr.org/2016/04/run-meetings-that-are-fair-to-introverts-women-and-remote-workers). But there are a couple of tricks to solve these issues.</p>

## Going beyond…

*   “[If you want to be understood — listen.](https://tombartel.de/2016/05/05/if-you-want-to-be-understood-listen/)” Tom Bartel shares why it’s so important to listen to other people in order to be understood.
*   John Doe is the “name” of the source for the Panama Papers that reveal deceptive tax saving strategies. The [source now shared the reasons for leaking the data](https://panamapapers.sueddeutsche.de/articles/572c897a5632a39742ed34ef/): wide-spread income inequality which is supported by massive and pervasive corruption. This is a primer on ethics, corruption and being a whistleblower. There’s also an [organization working for more transparency and against corruption](https://www.transparency.org/) since years now and you can support them.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.

<em>Thanks and all the best,
Anselm</em>

