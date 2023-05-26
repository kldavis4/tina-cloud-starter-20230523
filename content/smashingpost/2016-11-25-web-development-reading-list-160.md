---
title: >-
  Web Development Reading List #160: Real Stories About HTTP/2, Cascading Style
  Sheets, And Code Of Shame
slug: web-development-reading-list-160
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33dfc646-e2f6-4412-a573-f8536b9dac56/wdrl-160-opt.png'
date: 2016-11-25T19:40:23.000Z
author: anselm-hannemann
description: >-
  We have great new technology available to enhance our websites. But while
  theoretical articles explain well what the technologies do, we often struggle
  to find real use cases or details on **how things worked out in actual
  projects**.

  This week I stumbled across a couple of great posts that share exactly these
  precious real-life insights: stories about HTTP/2 implementation, experiences
  from using the Cascade of CSS in large-scale projects, and insights into
  employing Service Worker and BackgroundSync to build solid forms.
categories:
  - Web Development Reading List
---
We have great new technology available to enhance our websites. But while theoretical articles explain well what the technologies do, we often struggle to find real use cases or details on **how things worked out in actual projects**.

This week I stumbled across a couple of great posts that share exactly these precious real-life insights: stories about HTTP/2 implementation, experiences from using the Cascade of CSS in large-scale projects, and insights into employing Service Worker and BackgroundSync to build solid forms.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/)
*   [Getting Ready For HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [CSS Inheritance, The Cascade And Global Scope: Your New Old Worst Best Friends](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)
*   [Rekindling Your Passion For Web Design](https://www.smashingmagazine.com/2015/05/rekindling-your-passion-for-web-design/)

## News

*   Support for [style input type “checkbox” and “radio” via CSS](https://bugzilla.mozilla.org/show_bug.cgi?id=418833) landed in Firefox Nightly. Also new in Firefox Nightly is the [date picker](https://bugzilla.mozilla.org/show_bug.cgi?id=1283385). A time picker was already added a few weeks ago.
*   [GitLab 8.14](https://about.gitlab.com/2016/11/22/gitlab-8-14-released/) brings Time Tracking, Chat commands, merge prevention until a review is done, and many other small improvements.
*   Firefox will soon [warn people if they are about to enter a password in insecure (HTTP) contexts](https://mobile.twitter.com/ryanfeeley/status/801539237682302987). It’s time to secure every login with an HTTPS connection and enforce this as a best practice.

{{% feature-panel %}}

<figure><a href="https://mobile.twitter.com/ryanfeeley/status/801539237682302987"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d5c5731-181c-4f9d-a287-f5845943f5c1/password-http-opt.png" width="650" height="442" alt="Coming soon to Firefox: a feature that will warn users when they type a password into an insecure (HTTP) page or form." /></a><figcaption>Coming soon to Firefox: a feature that will warn users when they type a password into an insecure (HTTP) page or form. (Image credit: <a href="https://mobile.twitter.com/ryanfeeley/status/801539237682302987">Ryan Feeley</a>)</figcaption></figure>

## Web Performance

*   Kazuho Oku’s slide deck about [reorganizing website architecture for HTTP/2](https://www.slideshare.net/kazuho/reorganizing-website-architecture-for-http2-and-beyond) shares real experiences of implementing HTTP/2 and valuable details on browser implementation.</p>

## Accessibility

*   Tim Wright explains the [difference between `role="presentation"` and `aria-hidden="true"`](https://csskarma.com/blog/difference-rolepresentation-aria-hiddentrue/).</p>

## JavaScript

*   Michael Scharnagl explains [how you can enhance a basic form](https://justmarkup.com/log/2016/10/enhancing-a-comment-form/) (i.e. a login or comment form) with custom validation, AJAX requests, auto-expansion of a textarea, and, finally, Service Worker and BackgroundSync to store input when a connection is unstable.</p>

## CSS/Sass

*   Heydon Pickering wrote about “[CSS Inheritance, The Cascade And Global Scope: Your New Old Worst Best Friends](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/).”

## Work & Life

*   Justin White shares [his story of becoming a programmer](https://m.signalvnoise.com/how-i-left-behind-my-silicon-dream-for-a-saner-place-to-work-3c58c9bc24ab?token=s6h9qOA5om9p_dG7), his job hunt in the Silicon Valley, and why he chose not to work for an average startup.
*   The CTO of Basecamp critizes [Microsoft’s new advertising campaign for Office 365](https://m.signalvnoise.com/microsoft-reboots-war-on-sleep-a90da0396fb5#.9n97f0gam). A good read on why sleep and dedicated non-work matter and why we shouldn’t endorse companies that don’t value these needs.
*   I don’t want to write too much about this weird Black Friday thing that causes millions of people to buy stuff they’ll never use or need, but Jason Koebler has the best Black Friday deal ever: [repair a gadget you already own](https://motherboard.vice.com/read/the-best-black-friday-deal-repairing-a-gadget-you-already-own) instead of buying new stuff.

<figure><a href="https://m.signalvnoise.com/how-i-left-behind-my-silicon-dream-for-a-saner-place-to-work-3c58c9bc24ab?token=s6h9qOA5om9p_dG7#.k5z3axtkf"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9219f202-4dc2-452e-bf41-e13027aef91f/saner-place-to-work-opt.png" width="650" height="486" alt="For a lot of designers and developers Silicon Valley seems to be the promised land. Justin White shares how he left behind his Silicon Valley dream to find a saner place to work." /></a><figcaption>For a lot of designers and developers Silicon Valley seems to be the promised land. Justin White shares <a href="https://m.signalvnoise.com/how-i-left-behind-my-silicon-dream-for-a-saner-place-to-work-3c58c9bc24ab?token=s6h9qOA5om9p_dG7#.k5z3axtkf">how he left behind his Silicon Valley dream</a> to find a saner place to work.</figcaption></figure>

## Going Beyond…

*   Bill Sourour’s article “[The Code I’m Still Ashamed Of](https://medium.freecodecamp.com/the-code-im-still-ashamed-of-e4c021dff55e)” points out an important aspect of our jobs as developers: responsibility. An incredibly important story.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

