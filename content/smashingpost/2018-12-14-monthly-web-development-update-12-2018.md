---
title: 'Monthly Web Development Update 12/2018: WebP, The State Of UX, And A Low-Stress Experiment'
slug: monthly-web-development-update-12-2018
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae5c3cab-0db0-4398-b26d-b691a8174095/state-of-ux-opt.png
date: 2018-12-14T12:20:03+01:00
summary: >-
  For his last monthly update in 2018, Anselm summarized what has happened in the web development community in the past few weeks. Get ready for browser news, handy tools, lessons learned, and thought-provoking reads.
description: >-
  For his last monthly update in 2018, Anselm summarized what has happened in the web development community in the past few weeks. Get ready for browser news, handy tools, lessons learned, and thought-provoking reads.
categories:
  - Web Development Reading List
---
It’s the last edition of this year, and I’m pretty stoked what 2018 brought for us, what happened, and how the web evolved. Let’s recap that and **remind us of what each of us learned this year**: What was the most useful feature, API, library we used? And how have we personally changed?

For this month’s update, I’ve collected yet another bunch of articles for you. If that’s not enough reading material for you yet, you can always find more in [the archive](https://www.smashingmagazine.com/category/web-development-reading-list) or [the Evergreen list](https://wdrl.info/evergreen) which contains the most important articles since the beginning of the Web Development Reading List. I hope your days until the end of the year won’t be too stressful and wish you all the best. See you next year!

## News

- [Microsoft just announced that they’ll change their Edge strategy](https://blogs.windows.com/windowsexperience/2018/12/06/microsoft-edge-making-the-web-better-through-more-open-source-collaboration/#Mxl8BD0OvJcDF1xt.97): They’re going to use Chromium as the new browser engine for Desktop instead of EdgeHTML and might even provide Microsoft Edge for macOS. They’ll also help with development on the Blink engine from now on.
- [Chrome 71 is out](https://developers.google.com/web/updates/2018/12/nic71) and brings relative time support via the Internationalization API. Also new is that speech synthesis now requires user activation.
- [Safari Technology Preview 71 is out](https://webkit.org/blog/8517/release-notes-for-safari-technology-preview-71/), bringing `supported-color-schemes` in CSS and adding Web Authentication as an experimental feature.
- Firefox will soon offer users a [browser setting to block all permission requests automatically](https://webplatform.news/issues/2018-11-27). This will affect autoplaying videos, web notifications, geolocation requests, camera and microphone access requests. The need to auto-block requests shows how horribly wrong developers are using these techniques. Sad news for those who rely on such requests for their services, like WebRTC calling services, for example.

## General

- We’ve finally come up with ways to access and use websites offline with amazing technology. But one thing we forgot about is that [for the past thirty years we taught people that the web is online](https://paulbakaus.com/2018/12/06/learning-to-unlearn/), so most people don’t know that offline usage even exists. A lesson in user experience design and the importance of reminding us of the history of the medium we’re building for.

## UI/UX

- Matthew Ström wrote about [the importance of fixing things later](https://matthewstrom.com/writing/fix-it-later.html) and not trying to be perfect.
- A somewhat satiric resource about [the state of UX in 2019](https://trends.uxdesign.cc/2019).
- Erica Hall shows us examples of [why most of ‘UX design’ is a myth](https://medium.com/mule-design/a-three-part-plan-to-save-the-world-98653a20a12f) and why not only design makes a great product but also the right product strategy and business model. The best example why you should read this is when Erica writes “Virgin America. Rdio. Google Reader. Comcast. Which of these offered a good experience? Which of these still exists?” A truth you can’t ignore and, luckily, this is not a pessimistic but very thought-provoking article with great tips for how we can use that knowledge to improve our products. With strategy, with design, with a business model that fits.

{{< rimg href="https://trends.uxdesign.cc/2019" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae5c3cab-0db0-4398-b26d-b691a8174095/state-of-ux-opt.png" sizes="100vw" caption="After curating and sharing 2,239 links with 264,016 designers around the world, the folks at UX Collective have isolated a few <a href='https://trends.uxdesign.cc/2019'>trends in what the UX industry is writing, talking, and thinking about</a>. (<a href='https://trends.uxdesign.cc/2019'>Image credit</a>; illustration by <a href='https://www.instagram.com/camixvx/'>Camilla Rosa</a>)" alt="Illustration of a woman with a tablet running some design software where her face should be." >}}

## Tooling

- Sandip Devarkonda explains how we can [build a real-time app with GraphQL subscriptions on Postgres](https://www.smashingmagazine.com/2018/12/real-time-app-graphql-subscriptions-postgres/).

## HTML &amp; SVG

- Michael Scharnagl on why [bashing people because they prefer one coding language over the other](https://justmarkup.com/log/2018/11/just-markup/) needs to stop.

## Accessibility

- Scott O'Hara reminds us of how important it is to [not forget about the inherent functionality and accessibility](https://24ways.org/2018/inclusive-considerations-when-restyling-form-controls/) that many provide when we strive for custom-styled controls.

## CSS

- [CSS Environment Variables are coming](https://bitsofco.de/css-environment-variables/), and here’s why we need them in addition to Custom Properties.
- Andy Bell explains how we can [use CSS Custom Properties to manage flow and rhythm in our layouts](https://24ways.org/2018/managing-flow-and-rhythm-with-css-custom-properties/). An excellent example that goes beyond using Custom Properties for color values.

{{% ad-panel-leaderboard %}}

## JavaScript

- Google is about to bring us yet another API: the [Badging API allows Web Desktop Apps to indicate new notifications or similar](https://developers.google.com/web/updates/2018/12/badging-api). The spec is still in discussion, and they’d be happy to hear your thoughts about it.
- Hidde de Vries explains how we can use modern JavaScript APIs to [scroll an element into the center of the viewport](https://hiddedevries.nl/en/blog/2018-12-10-scroll-an-element-into-the-center-of-the-viewport).
- Available behind flags in Chrome 71, [the new `Background Fetch`](https://developers.google.com/web/updates/2018/12/background-fetch) makes it possible to fetch resources that take a while to load — movies, for example — in the background.
- Pete LePage explains how we can use the Web Share Target API to [register a service as Share Target](https://developers.google.com/web/updates/2018/12/web-share-target).
- Is it still a good idea to use JavaScript for loading web fonts? Zach Leatherman shares [why we should decide case by case](https://www.filamentgroup.com/lab/js-web-fonts.html) and why it’s often best to use modern CSS and `font-display: swap;`.
- [Doka](https://pqina.nl/doka/?ref=producthunt) is a new standalone JavaScript image editor worth keeping in mind. While it’s not a free product, it features very handy methods for editing with a pleasant user experience, and by paying an annual fee, you ensure that you get bugfixes and support.
- “[The Power of Web Components](https://hacks.mozilla.org/2018/11/the-power-of-web-components/)” shares the basic concepts, how to start using them, and why using your own HTML elements instead of gluing HTML, the related CSS classes, and a JavaScript trigger together can simplify things so much.

## Security

- Scott Helme shares information about a new security header that we can make use of: [`Clear Site Data` allows site owners to clear data](https://scotthelme.co.uk/a-new-security-header-clear-site-data/) from cache, (local/session/permanent) storage, or cookies. This could be useful to delete sensitive or private data stored in localStorage or authentication cookies easily.
- We know by now that [using `rel=noopener` is a good idea for `target=_blank` link elements](https://wdrl.info/archive/151/the-target-blank-vulnerability-by-example). Now Firefox experiments with [automatically substituting `rel=noopener` in the browser](https://www.ghacks.net/2018/11/30/firefox-security-relnoopener-for-target_blank/) to ensure the security attack can’t be abused.
- Terence Eden explores how a lot of [big sites offering payment are including unauthenticated, unverified JavaScript](https://shkspr.mobi/blog/2018/11/major-sites-running-unauthenticated-javascript-on-their-payment-pages/) from third parties. He elaborates what this means, why it’s so harmful, and how we could solve the issue. That said, the Stripe JavaScript bundle that you need to include isn’t offering Sub Resource Integrity either.
- Another security incident happened with a very popular npm package: [`event-stream` was published with malware](https://blog.npmjs.org/post/180565383195/details-about-the-event-stream-incident) code that steals specific Bitcoin wallets from computers. Please check the dependencies on your machine and ensure you update to the latest package versions. `npm audit` also helps identify such issues.

## Privacy

- Do you have a husband or wife? Kids? Other relatives? Then [this essential guide to protecting your family’s data](https://web.archive.org/web/20181130081659/https://blog.mozilla.org/internetcitizen/2018/11/25/the-bare-minimum-you-should-do-to-protect-your-familys-data/) is something you should read and turn into action. The internet is no safe place, and you want to ensure your relatives understand what they’re doing — and it’s you who can protect them by teaching them or setting up better default settings.

{{% ad-panel-leaderboard %}}

## Web Performance

- How do WebP image file sizes compare to the best performing JPEG optimizations? Daniel Aleksandersen presents the numbers and concludes that [WebP does a fantastic job at beating other optimized formats](https://www.ctrl.blog/entry/webp-vs-guetzli-zopfli) nearly every time.
- Ire Aderinokun [shows how we can use WebP images today](https://bitsofco.de/why-and-how-to-use-webp-images-today/). This becomes even more relevant now that Firefox offers WebP support in their Nightly builds and Edge supports the format [since the last release](https://blogs.windows.com/msedgedev/2018/10/04/edgehtml-18-october-2018-update/), too.
- [Amazon’s cloud unit launches Arm-based server chips](https://www.cnbc.com/2018/11/26/aws-launches-arm-based-server-chips.html), and by that, they’re able to reduce costs by about 45% (e.g. for web servers). This means that the energy consumption is much lower and overall efficiency is higher which is a good sign for our planet as well. We need more of these evolutionary infrastructure upgrades that lower the impact of tech on our climate.

{{< rimg href="https://bitsofco.de/why-and-how-to-use-webp-images-today/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8255b6d3-8f2e-4372-9fe9-33b4d8467af0/how-to-use-webp-images-opt.png" sizes="100vw" caption="WebP offers both performance and features. Ire Aderinokun shares <a href='https://bitsofco.de/why-and-how-to-use-webp-images-today/'>why and how to use it</a>. (<a href='https://bitsofco.de/why-and-how-to-use-webp-images-today/'>Image credit</a>)" alt="Comparison of the quality of JPG and WebP images" >}}

## Work &amp; Life

- Shana Lynch tells us [what makes someone an ethical business leader](https://www.fastcompany.com/90275433/how-to-know-if-youre-an-ethical-leader), which values are important, how to stand upright when things get tough, and how to prepare for uncomfortable situations upfront.
- Ozoemena Nonso [tries to explain why we often aren’t happy](https://medium.com/@Nonso_Ozoemena/i-will-be-happy-when-i-why-we-are-unhappy-a2070a34c986). The thief of our happiness is not comparing ourselves with others; it’s that we struggle to get the model of comparison right. An incredibly good piece of life advice if you compare yourself with others often and feel that your happiness suffers from it.
- A rather uncommon piece of advice: Why [forcing others to leave their comfort zone might be a bad idea](https://www.theguardian.com/us-news/2018/nov/16/comfort-zone-mental-health).
- Sandor Dargo on how he managed to [avoid distractions during work time](https://dev.to/sandordargo/reconquering-my-job-in-15-steps-5ee5) and do his job properly again.
- Paul Robert Lloyd [writes about Cennydd Bowles’ book “Future Ethics”](https://paulrobertlloyd.com/2018/11/future_ethics_by_cennydd_bowles) and while explaining what it is about, he also points out the challenges of ethics with a simple example.
- Jeffrey Silverstein is a teacher and struggled a lot with finding time for side projects while working full-time. Now he found a solution which he shares with us in this great article about “[How to balance full-time work with creative projects](https://thecreativeindependent.com/guides/how-to-balance-full-time-work-with-creative-projects/).” An inspiring read that I can totally relate to.
- Ben Werdmüller shares his thoughts on [why lifestyle businesses are massively underrated](https://werd.io/2018/keeping-it-small-is-okay-too). But what’s a lifestyle business? He defines them as non-venture-funded businesses that allow their owners to maintain a certain level of income but not more. As a fun sidenote, this article shows how crazy rental prizes have become on the U.S. West Coast.
- Jake Knapp shares how he [survived six years with a distraction-free smartphone](https://medium.com/@jakek/six-years-with-a-distraction-free-iphone-8cf5eb4f97e3) — no emails, no notifications. And he has some great tips for us and an exercise to try out. I recently moved all my apps into one folder on the second screen to ensure I need to search for the app which usually means I really want to open it and don’t just do it to distract myself.
- Ryan Avent wrote about [why we work so hard](https://www.1843magazine.com/features/why-do-we-work-so-hard). This essay is well-researched and explains why we see work as crucial, why we fall in love with it, and why our lifestyle and society embraces to work harder all the time.

{{< rimg href="https://medium.com/s/story/six-years-with-a-distraction-free-iphone-8cf5eb4f97e3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a38f6418-9631-408b-8223-49272819b639/distraction-free-phone-opt.png" sizes="100vw" caption="Jake Knapp spent <a href='https://medium.com/s/story/six-years-with-a-distraction-free-iphone-8cf5eb4f97e3'>six years with a distraction-free phone</a>: no email, no social media, no browser. Now he shares what he learned from it and how you can try your own low-stress experiment. (<a href='https://medium.com/s/story/six-years-with-a-distraction-free-iphone-8cf5eb4f97e3'>Image credit</a>)" alt="An illustration of a hand holding a phone. The phone shows a popup saying: Wait seriously? You wanna delete Gmail? Are you nuts?" >}}

## Going Beyond…

- “[Who Do Designers Really Work For](https://theblog.adobe.com/design-ethics-who-designers-really-work-for/)” is a masterpiece about responsibility.
- Maryanne Wolf shares research showing that [when our reading brain skims texts, we don’t have time to grasp complexity](https://www.theguardian.com/commentisfree/2018/aug/25/skim-reading-new-normal-maryanne-wolf), to understand feelings, or to perceive beauty. A trend that has grown worse over the last decades.
- Global investors managing $32tn issued a stark warning to governments at the UN climate summit, demanding urgent cuts in carbon emissions and the phasing out of all coal burning. Without these, [the world faces a financial crash several times worse than the 2008 crisis](https://www.theguardian.com/environment/2018/dec/10/tackle-climate-or-face-financial-crash-say-worlds-biggest-investors), they said.
- In some ways, the planet’s worst mass extinction — 250 million years ago, at the end of the Permian Period — [may parallel climate change today](https://www.nytimes.com/2018/12/07/science/climate-change-mass-extinction.html).

{{< signature "cm" >}}