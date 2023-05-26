---
title: >-
  Web Development Reading List #172: On Reporting Bugs, DNS Subdomain Takeovers,
  And Sustainable UX
slug: web-development-reading-list-172
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa3b0be5-0e9e-4cb7-bcc0-bf92a133f0fd/wdrl-172-opt.png'
date: 2017-03-03T19:46:21.000Z
author: anselm-hannemann
description: >-
  As web developers, we all approach our work very differently. And even when
  you take a look at yourself, you’ll notice that **the way you do your work
  does vary all the time**. I, for example, have not reported a single bug to a
  browser vendor in the past year, despite having stumbled over a couple. I was
  just too lazy to write them up, report them, write a test case and care about
  follow-up comments.

  This week, however, when integrating the Internationalization API for dates
  and times, I noticed a couple of inconsistencies and specification violations
  in several browsers, and I reported them. It took me one hour, but now browser
  vendors can at least fix these bugs. Today, I filed two new issues, because
  I’ve become more aware again of things that work in one browser but not in
  others. I think it’s important to change the way we work from time to time.
  It’s as easy as caring more about the issues we face and reporting them back.
categories:
  - Web Development Reading List
---
This week, however, when integrating the Internationalization API for dates and times, I noticed a couple of inconsistencies and specification violations in several browsers, and I reported them. It took me one hour, but now browser vendors can at least fix these bugs. Today, I filed two new issues, because I’ve become more aware again of things that work in one browser but not in others. I think it’s important to change the way we work from time to time. It’s as easy as caring more about the issues we face and reporting them back.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Getting Ready For HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Front-End Performance Checklist 2017 (PDF, Apple Pages)](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [CSS Grid, Flexbox And Box Alignment: Our New System For Web Layout](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)
*   [Help The Community! Report Browser Bugs!](https://www.smashingmagazine.com/2011/09/help-the-community-report-browser-bugs/)

## News

*   [Web annotations](https://hypothes.is/blog/annotation-is-now-a-web-standard/) are now a [web standard](https://www.w3.org/blog/news/archives/6156), with a defined data model, vocabulary, and protocol. Let’s hope many of the browser vendors (Microsoft Edge) and service platforms will adopt the standard soon. For us developers it’s a huge opportunity, too, to build standardized annotations that are interoperable and to communicate with each other.

{{% feature-panel %}}

<figure><a href="https://hypothes.is/blog/annotation-is-now-a-web-standard/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa30826e-7080-4ef2-8d47-1c4d86ce13b9/web-annotation-architecture-opt.png" width="800" height="456" alt="Web Annotation Architecture" /></a><figcaption>The new <a href="https://hypothes.is/blog/annotation-is-now-a-web-standard/">Web Annotation standard</a> could make conversation happen anywhere on the web and make comment widgets a thing of the past. (<a href="https://hypothes.is/blog/annotation-is-now-a-web-standard/">Image credit</a>)</figcaption></figure>

## Security

*   Let’s have a look at [how Mr. Trump was hacked via DNS subdomain takeover](https://www.networkworld.com/article/3171732/security/iraqi-hacker-took-credit-for-hijacking-subdomain-and-defacing-trump-site.html), a [long-known technique](https://labs.detectify.com/2014/10/21/hostile-subdomain-takeover-using-herokugithubdesk-more/) that most people who configure DNS entries for a domain aren’t aware of.
*   Google Chrome now allows permitted site owners of a Chrome extension to [override selected user settings](https://developer.chrome.com/extensions/settings_override). This means that a browser extension vendor who verified their domain via Google Webmaster Tools can override user settings such as homepage or the default search provider via their website. After reading [this attack scenario](https://labs.detectify.com/2014/10/21/hostile-subdomain-takeover-using-herokugithubdesk-more/), I fear this could take the DNS subdomain attack to a new level.</p>

## Web Performance

*   Justin Avery shares how you can [configure HTTP/2 Server Push to work with Wordpress](https://responsivedesign.is/articles/configuring-http2-push-wordpress/).</p>

## CSS/Sass

*   Sometimes it’s the small things that help you a lot. Did you know that you can save time and avoid confusion in CSS by using the `:not(:last-of-type)` selector instead of two different selectors, for example? Timothy B. Smith [explains how this little trick works](https://theboldreport.net/2017/02/css-tip-use-not-to-save-time-and-lines-of-code/).
*   Jen Simmons wrote yet another great article about [the benefits of learning how to code layouts with CSS](https://jensimmons.com/post/feb-28-2017/benefits-learning-how-code-layouts-css).</p>

## Going Beyond…

*   Vicki Boykis wrote an excellent piece called “[Fix the internet by writing good stuff and being nice to people](https://blog.vickiboykis.com/2016/11/20/fix-the-internet/)” in which she points out one of the major issues on the internet: the fact that making money off content became worth more than the content itself.
*   The free Sustainable UX conference took place two weeks ago. To get some insights into how we can achieve sustainability in tech, you can now [watch the conference talks for free](https://www.youtube.com/playlist?list=PLrJVv8APJhWnHo_Gzt_cVwhLpABKtQi9R).

<figure><a href="https://blog.vickiboykis.com/2016/11/20/fix-the-internet/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0d77ef8-6b87-45ab-8027-e3261b8a58cf/write-good-stuff-opt.png" width="800" height="525" alt="Fix the internet by writing good stuff and being nice to people" /></a><figcaption><a href="https://blog.vickiboykis.com/2016/11/20/fix-the-internet/">Share and create good content</a>. A philosophy we all should live by.</figcaption></figure>

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

