---
title: 'Web Development Reading List #171: Leaks, SHA-1 Collision, And Brotli'
slug: web-development-reading-list-171
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3813e480-fcae-4333-8256-16a355b0ca0d/wdrl-171-opt.png'
date: 2017-02-24T21:51:12.000Z
author: anselm-hannemann
description: >-
  Phew, what a week! Due to an HTML-parsing bug, Cloudflare experienced a major
  **data leak**, and the first practical collision for SHA-1 was revealed as
  well.

  We should take these events as an occasion to reconsider if a centralized
  front-end load balancer that modifies your traffic is a good idea after all.
  And it’s definitely time to upgrade your TLS-certificate if you still serve
  SHA-1, too. Here’s what else happened this week.
categories:
  - Web Development Reading List
---
### <span class="rh">Further Reading</span> on SmashingMag:

*   [Next Generation Server Compression With Brotli](https://www.smashingmagazine.com/2016/10/next-generation-server-compression-with-brotli/)
*   [Making Accessibility Simpler, With Ally.js](https://www.smashingmagazine.com/2015/12/making-accessibility-simpler/)
*   [Team Collaboration And Closing Efficiency Gaps In Responsive Design](https://www.smashingmagazine.com/2014/05/team-collaboration-closing-efficiency-gaps-responsive-design/)
*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)

## News

*   Cloudflare experienced a [memory leak caused by its document parser](https://bugs.chromium.org/p/project-zero/issues/detail?id=1139). [Here is the incident report by Cloudflare](https://blog.cloudflare.com/incident-report-on-memory-leak-caused-by-cloudflare-parser-bug/).
*   The fresh [Safari Technology Preview 24](https://webkit.org/blog/7423/release-notes-for-safari-technology-preview-24/) added support for PerformanceObserver and added `<link preload>` as an experimental feature. Furthermore, they implemented the dynamic JavaScript `import` operator and suspended SVG animations on hidden pages.
*   It was just a matter of time until browsers would stop accepting SHA-1 certificates. But this week, things took a sudden turn as Google researchers revealed the first practical collision for SHA-1, affirming the insecurity of the algorithm. As a result of this, starting from today, Mozilla will [remote-update Firefox to not accept SHA-1 in certificates anymore](https://blog.mozilla.org/security/2017/02/23/the-end-of-sha-1-on-the-public-web/).</p>

## General

*   How does your team review code? Ana Balica shares a useful [checklist for reviewing your and your teammates code](https://ana-balica.github.io/2017/02/21/code-review-checklist/).</p>

## Tools & Workflows

*   Joseph Zimmerman [introduces us to Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/). What I really like about this article is that it’s not another article sharing pre-built sets of configurations but that it explains every detail step-by-step.
*   [_Oh shit, git!_](https://ohshitgit.com/) Don’t be afraid of git anymore thanks to this emergency guide that helps you solve the most common problems with the versioning system.

{{% feature-panel %}}

<figure><a href="https://ohshitgit.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33021cd0-3aff-4569-8f42-9e085ff4b875/git-guide-opt.png" width="800" height="335" alt="Oh shit, git!" /></a><figcaption>Something went wrong in Git, but you don’t know how to get yourself out of the mess? “<a href="https://ohshitgit.com/">Oh shit, git!</a>” has got your back.</figcaption></figure>

## Security

*   Mitigating Cross-Site Request Forgery attacks has never been easy. Luckily, it seems that we now got a proper solution for it: [Same-Site Cookies](https://scotthelme.co.uk/csrf-is-dead/). The only thing you need to do to make it work is adding `SameSite` to your existing `Set-Cookie` header. Of course, you should know how same-site cookies differ from “normal” cookies, but for most sites this should be easy to implement.
*   A joint-venture of five journalists researched how the private security industry works and [what price we as citizens pay for our security](https://thecorrespondent.com/10221/security-for-sale-the-price-we-pay-to-protect-europeans).</p>

## Privacy

*   It’s not your computer that is the most vulnerable device, it’s your smartphone. In fact, for a small amount of money, [everyone can easily buy spyware](https://motherboard.vice.com/en_us/article/i-tracked-myself-with-dollar170-smartphone-spyware-that-anyone-can-buy) that works on most Android phones. For iOS, things look a bit better unless the device is jailbroken. But this doesn’t necessarily mean that spyware doesn’t exist for that system as well.</p>

## Web Performance

*   Thadee Trompetter shares insights into [how Brotli can improve your site’s performance](https://www.voorhoede.nl/en/blog/static-site-implosion-with-brotli-and-gzip/) and why he relies on pre-compressing rather than doing it on the fly on the server.

<figure><a href="https://www.voorhoede.nl/en/blog/static-site-implosion-with-brotli-and-gzip/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa2cd6f8-ada3-4192-8389-52a3d9b32c26/brotli-support-opt.png" width="800" height="408" alt="Brotli support" /></a><figcaption>With support for Chrome, Firefox, Opera and the Android browser, <a href="https://www.voorhoede.nl/en/blog/static-site-implosion-with-brotli-and-gzip/">Brotli does a better job at compressing resources</a> than its predecessor Gzip.</figcaption></figure>

## JavaScript

*   Manuel Matuzovic explains [how to write JavaScript with accessibility in mind](https://medium.com/@matuzo/writing-javascript-with-accessibility-in-mind-a1f6a5f467b9).

## Going Beyond…

*   A team at the MIT Media Lab invented a device that captures air pollution and [turns the pollution into safe, high-quality ink for art](https://www.kickstarter.com/projects/1295587226/air-ink-the-worlds-first-ink-made-out-of-air-pollu).
*   The Institute For Energy Efficiency’s computing solutions group has a couple of interesting projects and data to share. For example, they try to figure out solutions to selectively shut down unnecessary components while retaining access to critical data. This is only one of their ambitious projects and shows [how much potential there is when it comes to improving energy efficiency in our networks](https://transit.iee.ucsb.edu/research/computing/projects).

<figure><a href="https://www.kickstarter.com/projects/1295587226/air-ink-the-worlds-first-ink-made-out-of-air-pollu"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34990999-781c-4104-a10c-c094ebbbe90d/airink-opt.png" width="679" height="383" alt="AirInk" /></a><figcaption>Turn something ugly into something beautiful: A team at the MIT Media Lab developed <a>artist’s ink made from air pollution</a>. (<a href="https://www.kickstarter.com/projects/1295587226/air-ink-the-worlds-first-ink-made-out-of-air-pollu">Image credit</a>)</figcaption></figure>

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

