---
title: 'Monthly Web Development Update 09/2017: Functional CSS, Android 8 And iOS 11'
slug: monthly-web-development-update-09-2017
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/894274dd-dde6-4559-a28f-9f73b20e236d/monthly-web-development-update-09-2017-opt.png
date: 2017-09-15T20:52:46.000Z
author: anselm-hannemann
description: >-
  _Editor’s Note: Welcome to this month’s web development update. It’s actually
  the first one that we publish, and from now on, Anselm will summarize **the
  most important things that happened over the past month** in one handy list
  for you. So that you’re always up-to-date of what’s going on in the web
  community. Enjoy!_

  Today, I’d like to begin this update with a question I’m asking myself quite
  often, and that was fueled by the things I read lately: **Where do we see our
  responsibility**, where do we see other people’s responsibilities? And how do
  companies fit in here?
categories:
  - Web Development Reading List
---
Today, I’d like to begin this update with a question I’m asking myself quite often, and that was fueled by the things I read lately: **Where do we see our responsibility**, where do we see other people’s responsibilities? And how do companies fit in here?

With governments needing to make rules for [how autonomous cars should behave in case of an incident](https://thenextweb.com/cars/2017/08/24/germanys-self-driving-car-solution-kill-animals-damage-property-protect-humans/#.tnw_gEstLoIw), we can see how technological progress takes these questions to an entirely new dimension. Or take the Diesel gate affair that has been in the news all over the world these weeks. With software developers facing charges for their work, it showed us how important it is for employees to make their own decisions and to stand up for what’s right instead of blindly doing everything their bosses demand. Of course, this requires us to find our own position, our own path, and to stay true to it. An important thing we should reflect on more often if we want to make a change — not only in our work, but also in our community, and our lives.</p>

## News

*   [Google Chrome 61](https://developers.google.com/web/updates/2017/09/nic61) brings ECMAScript Modules, `navigator.share`, the WebUSB API, 8-digit alpha transparency hex-color codes, the CSS `scroll-behavior` property, and the Visual Viewport API to the browser.
*   Android 8, named “Oreo”, is now available and comes with picture-in-picture support, a system-wide autofill feature, and much more. But, unfortunately, it seems that the new version also brings along quite some issues for us web developers, especially [problems with Progressive Web Apps](https://medium.com/@firt/android-oreo-takes-a-bite-out-of-progressive-web-apps-30b7e854648f), as Maximiliano Firtman points out.
*   The latest update of Adobe XD ships with some [new features](https://blogs.adobe.com/creativecloud/august-update-of-adobe-xd/). There’s a new “reuse styles and assets” feature, and character styles created in Photoshop, Illustrator or other Creative Cloud applications can be reused in XD, too. The new version also comes with common UI resources for iOS, Google Material, and Windows.
*   Federico Viticci discovered that [Apple removed Google AMP versions of a link](https://mobile.twitter.com/viticci/status/900396684844433409) in iOS 11 and redirects users to the original source URL instead if they are using iMessage or Apple’s Reading List feature. A very interesting step that could be a reaction to users having trouble with AMP URLs or maybe Apple wants to avoid using a third-party proxy that could disappear any time or even change the content of the original URLs.
*   At this year’s developer event, Microsoft announced [what’s coming in Edge 16](https://docs.microsoft.com/en-us/microsoft-edge/dev-guide/whats-new/edgehtml-16): Updated CSS Grid Layout, `object-fit` and `object-position`, support for the Payment Request API, Service Workers, and WebVR.

{{% feature-panel %}}

<figure><a href="https://blogs.adobe.com/creativecloud/august-update-of-adobe-xd/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4926804f-be10-4224-bef9-4476efde41a1/adobe-xd-ui-resources-opt.png" width="800" height="530" alt="Adobe XD UI resources" /></a><figcaption>The <a href="https://blogs.adobe.com/creativecloud/august-update-of-adobe-xd/">new Adobe XD update</a> makes designing for iOS, Windows, and Material Design even easier thanks to platform-specific UI components. (<a href="https://blogs.adobe.com/creativecloud/august-update-of-adobe-xd/">Image source</a>)</figcaption></figure>

## UI/UX

*   Jason Fried from Basecamp shares [why and how they changed the interface of their Calendar schedule design](https://m.signalvnoise.com/new-in-basecamp-3-an-all-new-schedule-design-ad1bbf8e57f0). Interesting insights into why our idea of what _could_ work doesn’t always equal what _will_ work in practice.
*   [Feather Icons](https://feathericons.com/) is a set of 240 simply beautiful open-source icons that come in handy in all kinds of UI projects.
*   Thomas Payne shares [why the much-hated Comic Sans font isn’t such a bad font](https://blog.prototypr.io/you-hate-comic-sans-you-dont-know-anything-about-typography-5133fbd4c8c4) after all.

<figure><a href="https://feathericons.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e1da3c9-216e-4444-98db-7438b64fa3e6/feather-icons-opt.png" width="800" height="475" alt="Feather Icons" /></a><figcaption>Simple and minimalistic — that’s the open-source <a href="https://feathericons.com/">Feather Icon Set</a>. (<a href="https://feathericons.com/">Image source</a>)</figcaption></figure>

## Tooling

*   This article by Mozilla describes how you can [use Firefox in headless mode](https://developer.mozilla.org/en-US/Firefox/Headless_mode) and how to run automated tests with it.
*   [Subfont](https://www.npmjs.com/package/subfont) is a command line tool to statically analyze your page to generate the most optimal web font subsets, then inject them into your page. It’s also part of [assetgraph 3.8](https://github.com/assetgraph/assetgraph/releases/tag/v3.8.0).
*   Martin Tapia explains how you can [use headless Chrome to scrape websites](https://blog.phantombuster.com/web-scraping-in-2017-headless-chrome-tips-tricks-4d6521d695e8) and why it’s so much cooler than using curl.</p>

## JavaScript

*   Diogo Spínola wrote a transition guide for everyone using callbacks to [move their code to async/await functions](https://medium.com/@daspinola/javascript-from-callbacks-to-async-await-1cc090ddad99) in the future.</p>

## CSS

*   Adam Wathan summarized how [the way he writes CSS transitioned from a very “semantic” approach to what is called “functional CSS”](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/). In the article, he explains how the semantic approach works, which challenges it brings along and then compares the code example with functional approaches.
*   Darryl Pogue gives insights into [how we can fix website issues caused by the new kind of viewport that was introduced with iPhone X](https://ayogo.com/blog/ios11-viewport/) this week.

<figure><a href="https://ayogo.com/blog/ios11-viewport/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51b86d4b-48fa-41ed-8435-295ef2c8fdc1/ios11-viewport-opt.png" width="800" height="284" alt="Understanding the WebView Viewport in iOS 11" /></a><figcaption>How should we deal with fixed position header bars in combination with the new viewport that the iPhone X introduced? <a href="https://ayogo.com/blog/ios11-viewport/">Darryl Pogue sheds some light into the dark</a>. (<a href="https://ayogo.com/blog/ios11-viewport/">Image source</a>)</figcaption></figure>

## Web Performance

*   Jack Preston wrote up a nice visual explanation of [how compression works](https://unwttng.com/compression-decompressed).</p>

## Accessibility

*   Adrian Roselli explains [what’s new in WCAG2.1](https://adrianroselli.com/2017/08/whats-new-in-wcag-2-1.html) and what you need to know to match the latest accessibility criteria.
*   Russ Weakley shares [how to build an accessible auto-complete field](https://www.slideshare.net/maxdesign/building-an-accessible-autocomplete).</p>

## Security

*   Some researchers [found a way to control voice assistants](https://www.fastcodesign.com/90139019/a-simple-design-flaw-makes-it-astoundingly-easy-to-hack-siri-and-alexa) from Apple, Google, Amazon, Microsoft, Samsung, and Huawei. And this does not only affect the smart home boxes but also every iPhone, MacBook, Windows 10 PC, or Samsung Galaxy phone. By using ultrasonic frequencies, they could control the devices and call people, open websites, and even re-route a navigation system of an Audi Q3 car.
*   Stéphane Bortzmeyer shares the observations made during a technical attack against the WikiLeaks platform last week. This is [a good example of how DNS attacks work](https://www.bortzmeyer.org/observations-wikileaks.html).
*   Benjamin Caudill introduces CFire, [a script to evade Cloudflare’s “Cloud Security Protections”](https://rhinosecuritylabs.com/cloud-security/cloudflare-bypassing-cloud-security/). The article also shares some very interesting details of how Cloudflare’s security system works.</p>

## Privacy

*   If you’re embedding tweets on your site, [you can add](https://mobile.twitter.com/bcrypt/status/903724091143630848) `<meta name="twitter:dnt" content="on">` so [that Twitter doesn’t track your visitors](https://dev.twitter.com/web/overview/privacy#what-privacy-options-do-website-publishers-have).
*   Privacy International shares new [insights into how our data is being used against us](https://medium.com/@privacyint/invisible-manipulation-efb4243011ca). Think of scenarios like banks deciding on creditworthiness by using data from our transaction history or connected cars being hacked while the owner doesn’t know which data is recorded, evaluated or sent to whom.

<figure><a href="https://medium.com/@privacyint/invisible-manipulation-efb4243011ca"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f53ab62-b733-40f9-a613-1007c84f212d/invisible-manipulation-opt.png" width="800" height="419" alt="Invisible Manipulation" /></a>.<figcaption>Invisible Manipulation. Privacy International shares <a href="https://medium.com/@privacyint/invisible-manipulation-efb4243011ca">ten examples of how our data is being used against us</a> without us knowing. (<a href="https://medium.com/@privacyint/invisible-manipulation-efb4243011ca">Image source</a>)</figcaption></figure>

## Work & Life

*   Ted Neward shares how important it is that [we as developers make reasonable and legally correct decisions](https://mobile.twitter.com/tedneward/status/901135785969074177) in our work, regardless of what our bosses tell us to do.
*   Melinda Gates reveals that, even though she spent her entire career in technology, she [wasn’t prepared for how technology will affect her kids](https://www.washingtonpost.com/news/parenting/wp/2017/08/24/melinda-gates-i-spent-my-career-in-technology-i-wasnt-prepared-for-its-effect-on-my-kids/). If she had known and thought more about the effects technology has on children, she would have done a couple of things differently. An interesting story that we should care more about.
*   Victor Yocco shares [why project retrospectives are so important for a team](https://www.smashingmagazine.com/2017/09/importance-project-retrospectives-part-1/) and how to organize them so that they’re useful. An essential read for everyone who’s not doing retrospectives yet.
*   Neil Irwin [analyzed a janitors’ job conditions at two top companies](https://www.nytimes.com/2017/09/03/upshot/to-understand-rising-inequality-consider-the-janitors-at-two-top-companies-then-and-now.html), back in the 80s and today — namely at Kodak and Apple. A sad story about inequality and about how so-called “successful” companies achieve their success.

_We hope you’ve enjoyed this first monthly Web Development Update. The next one is scheduled for October 13th. Stay tuned!_

