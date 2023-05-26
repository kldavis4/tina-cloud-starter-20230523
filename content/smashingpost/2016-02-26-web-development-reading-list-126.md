---
title: >-
  Web Development Reading List #126: Clever Interfaces, An Open AMP Alternative
  And The Art Of Slow Growth
slug: web-development-reading-list-126
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6861c43d-b361-4365-8164-1d96ed26d584/wdrl-126-futures-of-text-opt.png
date: 2016-02-26T18:46:54.000Z
author: anselm-hannemann
description: >-
  It’s interesting to see how user experience design advances now that we
  managed to understand what it means. I think artificial intelligence will
  become a huge part of user experience over time and that **we will spend more
  time on developing clever integrations to third parties** than developing our
  own “dumb” interfaces. That’s why I find it interesting to see research on how
  services can use unified interfaces like text messaging apps to become more
  intelligent. Enjoy your weekend!

  Why reinvent everything and ship your own application when you could use a
  messaging app as input and output of your API instead? For example, a schedule
  for the next bus could be delivered to the user via a text, WhatsApp or
  Telegram message.
categories:
  - Web Development Reading List
---
It’s interesting to see how user experience design advances now that we managed to understand what it means. I think artificial intelligence will become a huge part of user experience over time and that <strong>we will spend more time on developing clever integrations to third parties</strong> than developing our own “dumb” interfaces. That’s why I find it interesting to see research on how services can use unified interfaces like text messaging apps to become more intelligent. Enjoy your weekend!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Beyond The Boring: The Hunt For The Web’s Lost Soul](https://www.smashingmagazine.com/2015/07/hunt-for-the-webs-lost-soul/)
*   [Web Design Is Dead. No, It Isn’t.](https://www.smashingmagazine.com/2015/07/web-design-is-dead-no-it-isnt/)
*   [The “Wow” Factor in Web Design](https://www.smashingmagazine.com/2009/12/the-wow-factor-in-web-design/)
*   [Examining The Design Process: Clichés And Idea Generation](https://www.smashingmagazine.com/2011/02/clich-s-and-idea-generation-how-to-turn-clich-in-a-successful-visual-solution/)

## Concepts & Design

*   Why reinvent everything and ship your own application when you could use a messaging app as input and output of your API instead? For example, a schedule for the next bus could be delivered to the user via a text, WhatsApp or Telegram message. The “[Futures of text](https://whoo.ps/2015/02/23/futures-of-text)” article shares approaches that could be built way better as a text message service than as a standalone app. I can imagine services like a simple daily broadcast about avalanche risks that I receive via Telegram on my phone or information about the current traffic situation to be great examples where a simple text message reply could be way more useful than an app.
*   Robin Rendle wrote a lengthy but worth to read essay about “[The New Web Typography](https://robinrendle.com/essays/new-web-typography/)”. A fine, well-written wrap-up of what we can use now, what we should consider when doing so, and what matters when you need to choose a new typeface for a project.
*   [The way we approach designing with data has changed over time](https://medium.com/@preciousforever/designing-with-meaningful-data-5456b40e172e) and is still evolving. Given the amount of designs I’ve seen using dummy data that perfectly fit its environment, it’s very important that designers start to test their designs with meaningful and random data. A good way could be the [disco mode in the Pattern Lab demo](https://demo.patternlab.io/), the new [InVision Craft tool](https://www.invisionapp.com/craft) or the [Fluid Plugin for Sketch](https://github.com/matt-curtis/Fluid-for-Sketch).

{{% feature-panel %}}

<figure class="fwi"><a href="https://whoo.ps/2015/02/23/futures-of-text"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d0d9ef7-3de6-4d9a-9aca-b97bdda5f642/future-of-text-opt.png" alt="Apps and services integrated into text messages. Is this the future of text?" width="500" height="532" /></a><figcaption>Apps and services integrated into text messages. Is this the <a href="https://whoo.ps/2015/02/23/futures-of-text">future of text</a>?</figcaption></figure>

## Tools

*   For a long time we only had this one Ruby [scss-lint](https://github.com/brigade/scss-lint/) plugin to lint our Scss code. “[How to lint your Sass/CSS properly with Stylelint](https://www.creativenightly.com/2016/02/How-to-lint-your-css-with-stylelint/)” now explains how you can use another tool based on Node.js and PostCSS to lint not only Scss but also CSS files for coding consistency.
*   GitHub is down again? Here’s how you can [send a patch file over to a co-worker without the need for a host server](https://robots.thoughtbot.com/send-a-patch-to-someone-using-git-format-patch) to push and pull your repository from.</p>

## Security

*   Randall Degges explains how you can [use the new, recommended hashing algorithm Argon2 for password hashing in Node.js](https://stormpath.com/blog/secure-password-hashing-in-node-with-argon2/). It’s pretty easy to use, so if you store passwords somewhere, consider Argon2 before it’s too late and your customers’ data is exposed because of a weak storing solution.
*   Most of today’s software is delivered via package managers. While it’s an easy, and mostly reliable, way to distribute ready-to-use packages of source code, it also brings along a few security issues. Lukas Reschke shares why: [the whole system is based on trust](https://statuscode.ch/2016/02/distribution-packages-considered-insecure/). And since trust cannot be ensured, we should try to find alternative methods to provide a more open, secure, and reliable way to avoid scenarios like [the one that just happened to a Linux distribution](https://blog.linuxmint.com/?p=2994) this week, which served malware from the official package.
*   This series of infographics visualizes research findings on [how creators of software applications and their users perceive security](https://www.arxan.com/resources/state-of-application-security/). Interestingly, the creators feel more positive about it while users are indeed more realistic — but still far from the messy reality.</p>

## Web Performance

*   Tim Kadlec and Yoav Weiss came up with [a (web) standardized alternative](https://timkadlec.com/2016/02/a-standardized-alternative-to-amp/) to Google’s AMP project. They’ve started writing [an early draft of a specification](https://yoavweiss.github.io/ContentPerformancePolicy/#introduction), but they also need your feedback on that. The goal behind it is to achieve the same that [AMP](https://www.smashingmagazine.com/2016/12/progressive-web-amps/) wants to achieve but by using and keeping the openness of the web instead of inventing a different format. That is also the reason why it’s not called a “project” or “platform” but declared as “Content Performance Policy,” similar to a Content Security Policy that you can opt-in for as a creator.</p>

## HTML/SVG

*   You can use the `<time>` element to provide a machine readable date for a human date. But did you know you can also use [`<data>`](https://www.w3.org/TR/html5/text-level-semantics.html#the-data-element) to provide such data for other phrasing content? Pretty cool to markup your products on a page with your IDs, UPC codes or other reference numbers.
*   GitHub switched from using iconfont for its icons to using SVG. The interesting part about this is [how they explain the switch from a technical perspective](https://github.com/blog/2112-delivering-octicons-with-svg).</p>

## JavaScript

*   Chrome now has an event for [`notificationclose`](https://www.chromestatus.com/feature/5706570994286592) that is triggered when a user closes a notification without any other action such as allow or deny. This is useful to adjust your web application with that information or just to measure how many people click those alerts away and do not get the expected experience from your web application.</p>

## CSS/Sass

*   Coming to more and more browsers now, CSS Custom Properties are still not widely known, and many people are wondering what the difference is between a Scss Variable and CSS Custom Properties. Pawel Grzybek [explains it](https://pawelgrzybek.com/css-custom-properties-explained/).
*   Harry Roberts shares a [quick study on why Sass Mixins are better for performance](https://csswizardry.com/2016/02/mixins-better-for-performance/) than extends when you make use of gzip.</p>

## Work & Life

*   Sometimes we’re [too busy to pay attention to life](https://www.farnamstreetblog.com/2016/02/too-busy/). We tend to focus rather on looking at photos instead of on the moments themselves. We tend to call or instant message with people instead of meeting them at a place. And instead of paying attention to our surroundings and the people near us in the streets, we’re focusing on our phones.
*   Andy Budd examines [the benefits and challenges of running a slow-growing business](https://www.andybudd.com/archives/2016/02/the_benefits_and_challenges_of_running_a/) and compares them to the fast-growing start-up culture. While the challenges that fast growth and unstable company structures bring along are interesting, they also hurt the team culture and maybe even the products being built.</p>

## Going beyond…

*   “For us it’s about providing a product that is durable and affordable that will actually last,” states Karla Gallardo, co-founder of the ethical clothing retailer Cuyana, in this article about [the power of buying less by buying better](https://www.theatlantic.com/business/archive/2016/02/buying-less-by-buying-better/462639/). Interestingly, this corresponds with research that says it can make you happier to buy less.
*   “[I Documented Two Years of Travel By Painting In My Moleskine Notebook](https://www.boredpanda.com/100-landscape-paintings-sketchbook-missy-dunaway/)” is a lovely hand-crafted art collection created by a traveler during her visits to different places around the world. An alternative to taking thousands of photos that no one will look at afterwards anyway and a beautiful, more emotional representation of lovely places.</p>

<figure class="fwi"><a href="https://www.boredpanda.com/100-landscape-paintings-sketchbook-missy-dunaway/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00b2bb3f-faa3-49f1-8bdb-ed85ca4d1dba/travel-sketchbook-opt.jpg" alt="Travel sketchbook" width="500" height="407" /></a><figcaption>Keeping a sketchbook is a much more personal way of recording your travels than taking thousands of photos. (Image credit: <a href="https://www.missydunaway.com/">Missy H. Dunaway</a>)</figcaption></figure>

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</p>

<em>Thanks and all the best,
Anselm</em>

