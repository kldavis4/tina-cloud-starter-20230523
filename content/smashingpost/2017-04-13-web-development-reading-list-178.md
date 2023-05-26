---
title: 'Web Development Reading List #178: On CAA, Pong.js, And Meaningful Work'
slug: web-development-reading-list-178
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1de5747a-d5d1-49af-b91e-4c97e43e7533/wdrl-178-opt.png'
date: 2017-04-13T23:18:06.000Z
author: anselm-hannemann
description: >-
  Looking at recent discussions, I feel that more and more people are starting
  to think about ethically and morally correct work. Many of us keep asking
  themselves if their work is meaningful or **if it matters at all**. But in a
  well-functioning society, we need a variety of things to live a good life. The
  people writing novels that delight us are just as important as those who fight
  for our civil rights.

  It’s important that we have people building services that ease other people’s
  lives and it’s time to set our sense of urgency right again. Once we start to
  value other people’s work, the view we have on our own work will start to
  change, too. As _we_ rely on book authors, for example, other people rely on
  _us_ to be able to buy the books via a nice, fast and reliable web service.
categories:
  - Web Development Reading List
---
It’s important that we have people building services that ease other people’s lives and it’s time to set our sense of urgency right again. Once we start to value other people’s work, the view we have on our own work will start to change, too. As _we_ rely on book authors, for example, other people rely on _us_ to be able to buy the books via a nice, fast and reliable web service.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Making A Service Worker: A Case Study](https://www.smashingmagazine.com/2016/02/making-a-service-worker/)
*   [How To Create A Responsive 8-Bit Drum Machine Using Web Audio, SVG And Multitouch](https://www.smashingmagazine.com/2016/08/how-to-create-a-responsive-8-bit-drum-machine-using-web-audio-svg-and-multitouch/)
*   [A Guide To Personal Side Projects](https://www.smashingmagazine.com/2016/05/a-guide-to-personal-side-projects/)
*   [Algorithm-Driven Design: How Artificial Intelligence Is Changing Design](https://www.smashingmagazine.com/2017/01/algorithm-driven-design-how-artificial-intelligence-changing-design/)

## News

*   Good news if you’re using PostgreSQL: The upcoming [PostgreSQL 10 offers some great new features](https://rhaas.blogspot.de/2017/04/new-features-coming-in-postgresql-10.html). It’ll support logical replication in addition to the already existing logical decoding, up to 4x faster parallel query, SCRAM Authentication, and a lot of other useful things.
*   Alexis Deveria creates the amazing project [caniuse.com](https://caniuse.com/), a site that we all use a lot. Now he accepts donations, and in return, you can also get an ad-free experience on the site. If you rely on caniuse.com for your work, consider showing your appreciation for the hard work that the author puts into it by [giving something back](https://www.patreon.com/caniuse).
*   With the [new Windows 10 Creators Update](https://docs.microsoft.com/en-us/microsoft-edge/dev-guide#whats-new-in-edgehtml-15), Edge 15 went live. It comes with a new tab management interface, a book reader mode, and better energy efficiency. But even more interesting for us are the implementation of the Web Payment Request API, CSS Custom Property support, Brotli support, WebRTC, `async`/`await`, and Intersection Observer.</p>

## General

*   André Staltz shares his most valuable piece of advice to be a better programmer: “Gain a deeper understanding of the system,” and he has [strong points in his article](https://staltz.com/the-single-tip-that-made-me-a-better-programmer.html) that reinforce this.</p>

## Security

*   There’s a new DNS resource record: `CAA`. The [Certificate Authority Authorization Record](https://ma.ttias.be/caa-checking-becomes-mandatory-ssltls-certificates/) lets you specify which certificate authority is allowed to issue a certificate for your domain. From September 2017 on, CAs are required to check against these records, so you should consider adding that record to your DNS records as soon as possible.
*   Andrew Reed and Michael Kranch explain how they managed to [identify HTTPS-protected Netflix videos in real time](https://www.mjkranch.com/docs/CODASPY17_Kranch_Reed_IdentifyingHTTPSNetflix.pdf) (PDF, 0.7MB). A technical write-up about HTTPS issues that aren’t easy to fix.</p>

## Web Performance

*   Phil Nash wrote a guide on how to use Service Workers and the Background Sync API to [send messages when a user is back online](https://www.twilio.com/blog/2017/02/send-messages-when-youre-back-online-with-service-workers-and-background-sync.html).

{{% feature-panel %}}

<figure><a href="https://www.twilio.com/blog/2017/02/send-messages-when-youre-back-online-with-service-workers-and-background-sync.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9c8e9e-061e-40ed-b7e1-5ba2c826040b/messages-with-service-worker-opt.png" width="800" height="296" alt="Send messages when you’re back online with Service Workers and Background Sync" /></a><figcaption>Sending messages when a user is back online — Phil Nash <a href="https://www.twilio.com/blog/2017/02/send-messages-when-youre-back-online-with-service-workers-and-background-sync.html">explains how to do it</a>. (<a href="https://www.twilio.com/blog/2017/02/send-messages-when-youre-back-online-with-service-workers-and-background-sync.html">Image credit</a>)</figcaption></figure>

## HTML & SVG

*   Ulrich-Matthias Schäfer shares how you can [recreate the beloved Pong game with SVG](https://css-tricks.com/pong-svg-js/) and some JavaScript.</p>

## JavaScript

*   Marcos Neves created a useful [Vue.js 2.2 API cheat sheet](https://vuejs-tips.github.io/cheatsheet/). It’s available as an interactive online as well as a PDF version.

<figure><a href="https://vuejs-tips.github.io/cheatsheet/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f31bb91c-0e70-4056-a712-bbd45b31bc1f/vue-cheatsheet-opt.png" width="800" height="459" alt="Vue.js cheatsheet" /></a><figcaption>Marcos Neves’ handy <a href="https://vuejs-tips.github.io/cheatsheet/">cheat sheet</a> has everything you need to know about Vue.js at one glance.</figcaption></figure>

## Work & Life

*   How can you [successfully manage a side project in a distributed team across the globe](https://colloq.io/blog/remote-managing-a-side-project-across-the-globe)? I wrote up how we did it at Colloq, my newest project, and share details on working remote, virtual office calls, and how to fix common Scrum issues.
*   Cassie Marketos shares her concerns and discoveries about “[What Makes Work Meaningful](https://blog.bigcartel.com/what-makes-work-meaningful/).” In search of the answer to the common question if what we do matters at all, this article reveals some thoughts that set our sense of urgency right again.</p>

## Going Beyond…

*   Linda Besner wrote about living in a globalized yet fragmented world, where [sleep is one of the few bodily experiences we seem to share](https://reallifemag.com/sleep-country/). A thoughtful piece about what the Internet achieved and where it struggles to connect people.
*   Josh Clark on why the smart algorithm systems that power Google, Siri, Alexa and other “intelligent” AI services [should know when they’re not smart enough](https://bigmedium.com/ideas/systems-smart-enough-to-know-theyre-not-smart-enough.html) and indicate that to users.
*   Microplastics are everywhere. They’re used in most creams, shower gels and a lot of other products we use every day. Scientists [now found microplastics in commercial salts](https://www.nature.com/articles/srep46173) from several countries, indicating how badly our seas are polluted with these particles. As we’re eating salt, this has a direct effect on our health, and it’s only stoppable if we achieve to not have microplastic particles in everyday products anymore.

Last but not least, if you’re in Europe or Germany, how about joining the awesome [CSSconf EU in Berlin on May, 5th](https://2017.cssconf.eu/)? There are still tickets available. I’ll be around at the sold-out beyondtellerrand in Düsseldorf again, and I’d love to meet you there. If you don’t have a ticket, maybe join [one of the side events](https://beyondtellerrand.com/events/duesseldorf-2017/side-events)? Or consider the [Material Conference](https://web.material.is/2017/) which will take place on August 17th in Iceland, a lovely island, and I’m sure the event will be great as well.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

