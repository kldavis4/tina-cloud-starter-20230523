---
title: >-
  Web Development Reading List #161: Restyling Form Elements, HTTP/2 HPACK, And
  The Empathy Vacuum
slug: web-development-reading-list-161
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d5e5715-f4e1-4dc9-9397-a3912f1a2830/wdrl-161-opt.png'
date: 2016-12-02T19:49:01.000Z
author: anselm-hannemann
description: >-
  Are you afraid of refactoring code? I _love_ refactoring code. It’s nice
  to see a code base growing, but this also means that new quirks and suboptimal
  changes are introduced along the way. At some point, you might realize that
  there could be a huge opportunity in rewriting the code — to eliminate
  conflicts or to rename things.
categories:
  - Web Development Reading List
---
**Are you afraid of refactoring code?** I _love_ refactoring code. It’s nice to see a code base growing, but this also means that new quirks and suboptimal changes are introduced along the way. At some point, you might realize that there could be a huge opportunity in rewriting the code — to eliminate conflicts or to rename things.

For me, refactoring is both: It’s a challenge to master, but, in the end, also a relief to see how the code evolved. We can’t anticipate everything when we first build modules, and we shouldn’t try to do so either. So let’s not be afraid to set our hands to an already existing code base and improve our code over time instead.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing For Explicit Choice](https://www.smashingmagazine.com/2015/05/designing-for-explicit-choice/)
*   [Making A Service Worker: A Case Study](https://www.smashingmagazine.com/2016/02/making-a-service-worker/)
*   [Form Inputs: The Browser Support Issue You Didn’t Know You Had](https://www.smashingmagazine.com/2015/05/form-inputs-browser-support-issue/)
*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)

## Concept & Design

*   Gov.uk explains why they [enlarged their radio and checkbox buttons](https://designnotes.blog.gov.uk/2016/11/30/weve-updated-the-radios-and-checkboxes-on-gov-uk/). As it turned out, the enlarged versions performed better than default browser styles due to increased visibility and improved proportions between labels and form action elements.

{{% feature-panel %}}

<figure><a href="https://designnotes.blog.gov.uk/2016/11/30/weve-updated-the-radios-and-checkboxes-on-gov-uk/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c98c0a9-6f22-4516-b286-2a3715fa4901/govuk-checkboxes-opt.png" width="650" height="552" alt="Gov.uk checkboxes before and after" /></a><figcaption>Gov.uk explains <a href="https://designnotes.blog.gov.uk/2016/11/30/weve-updated-the-radios-and-checkboxes-on-gov-uk/">why they increased the size of their radio buttons and checkboxes</a>. Top: Before updating the styles. Bottom: The new and improved version.</figcaption></figure>

## Privacy

*   David Revoy shares why he wanted to [get rid of all the CDN libraries](https://peppercarrot.com/article390/my-fight-against-cdn-libraries) he was loading on his website. Even if it’s “just” a JavaScript file hosted on a Google CDN, for example, it will allow the CDN provider to log user data (e.g. browser version), user location data (the IP address of your site’s visitors) and even more as they can track a user’s path or history through all the websites that are also using their CDN.
*   I set up S/MIME this week for my primary email address to be able to send and receive encrypted emails. I’m already using PGP, but S/MIME comes with better cross-platform support, and by offering both, I maximize the chance to communicate securely via email. I wrote up a little introduction on [how to set up S/MIME on MacOS and iOS](https://helloanselm.com/notes/setting-up-s-mime-on-macos-sierra-ios/) if you’d like to learn more about it.</p>

## Web Performance

*   The GitLab team shares [why they left the cloud for their hosted infrastructure](https://about.gitlab.com/2016/11/10/why-choose-bare-metal/) and returned to dedicated servers instead. A nice case study about performance issues on servers and how to solve them properly.
*   Vlad Krasnov from Cloudflare explains [how HPACK works in HTTP/2](https://blog.cloudflare.com/hpack-the-silent-killer-feature-of-http-2/) and why they implemented the full feature set on their systems instead of relying on partial implementations in nginx and CDN servers.</p>

## JavaScript

*   Max Stoiber explains [how _styled-components_ was built](https://mxstbr.blog/2016/11/styled-components-magic-explained/) and how ECMAScript’s native template literals feature and some other tiny functions make it work.
*   Rich Harris built a new JavaScript framework: Svelte. However, [that’s not the important point in his article](https://svelte.technology/blog/frameworks-without-the-framework/); what’s more interesting are the insights he grants into how he built a system that reduces the complexity on the build step instead of the browser. And, what’s even better for us, his system supports interoperability for modules — no matter if you use React, Angular.js or any other tool.
*   Is Service Worker an alien to you? Mariko Kosaka gives a better understanding of [why it’s hard to grasp what we can do with Service Workers](https://kosamari.com/notes/Service-Worker-what-are-you). A refreshing explanation that is quite different from what we usually read in Service Worker tutorials.

<figure><a href="https://kosamari.com/notes/Service-Worker-what-are-you"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96997c26-f986-4ec7-8e89-b0c886abf87e/service-worker-what-are-you-opt.png" width="650" height="416" alt="Service worker, what are you? Mariko Kosaka sheds some light into the dark." /></a><figcaption>Service worker, what are you? Mariko Kosaka <a href="https://kosamari.com/notes/Service-Worker-what-are-you">sheds some light into the dark</a>. (Image credit: <a href="https://kosamari.com/notes/Service-Worker-what-are-you">Mariko Kosaka</a>)</figcaption></figure>

## CSS/Sass

*   [cssreference.io](https://cssreference.io/) is a new place to play around with and learn about CSS properties. It explains what the properties do and shows in demos how they affect a layout.</p>

## Going Beyond…

*   Greg S. Cassel introduced “[Peer-to-Peer Digital Networking](https://blog.p2pfoundation.net/peer-peer-digital-networking-internet-work/2016/10/28)” as a free digital book. As the title implies, the book contains a lot of information on how the Internet should work as a peer-to-peer network.
*   “It is time for our industry to pause and take a moment to think: as technology finds its way into our daily existence in new and previously unimagined ways, we need to learn about those who are threatened by it. Empathy is not a buzzword but something to be practiced. Let’s start by not raging on our Facebook feeds but, instead, taking a trip to parts of America where five-dollar lattes and freshly pressed juices are not perks but a reminder of haves and have-nots. Otherwise, come 2020, Silicon Valley will have become an even bigger villain in the popular imagination, much like its East Coast counterpart, Wall Street.” — [Om Malik in _The New Yorker_](https://www.newyorker.com/business/currency/silicon-valley-has-an-empathy-vacuum)

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

