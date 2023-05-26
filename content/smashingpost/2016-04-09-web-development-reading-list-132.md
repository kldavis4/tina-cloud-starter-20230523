---
title: >-
  Web Development Reading List #132: The Challenges In Our Field, Debouncing And
  The Contain CSS Property
slug: web-development-reading-list-132
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d344c4a-8fb7-42de-9a87-bfd91cf556cc/gidole-opt.png'
date: 2016-04-09T01:30:42.000Z
author: anselm-hannemann
description: >-
  **What has been your biggest web development challenge recently?** Was it a
  development issue, a communication issue or an education issue in your team?

  Facing so many things that don't work as expected these days in many different
  teams and projects, I now realize that we all are part of a very young
  industry, and by challenging not only our technical foundations but also
  traditional working habits, we have yet to find how we want to work. Share
  your challenges in the comments to this post, and enjoy the weekend!
categories:
  - Web Development Reading List
---
<strong>What has been your biggest web development challenge recently?</strong> Was it a development issue, a communication issue or an education issue in your team? Facing so many things that don't work as expected these days in many different teams and projects, I now realize that we all are part of a very young industry, and by challenging not only our technical foundations but also traditional working habits, we have yet to find how we want to work. Share your challenges in the comments to this post, and enjoy the weekend!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Prioritizing Devices: Testing And Responsive Web Design](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [<span class="headline">Establishing An Open Device Lab</span>](https://www.smashingmagazine.com/2012/09/establishing-an-open-device-lab/)

## News

*   [Grunt 1.0.0](https://gruntjs.com/blog/2016-04-04-grunt-1.0.0-released) has been released. Long time no hear, it’s still one of the most used task runners for front-end workflows. Now finally the stable release is out, and with it, many bugs and glitches have been fixed, making it now a robust solution for long-term projects. I’m excited to hear that the development roadmap has very nifty features for it to keep evolving in the future.</p>

## Concepts & Design

*   “[A Simple Web Developer's Guide To Color](https://www.smashingmagazine.com/2016/04/web-developer-guide-color/)” features great methods for finding a lovely color palette for your next project.
*   [Gidole](https://gidole.github.io/) is an open source font that claims itself as a modern DIN and looks pretty great.</p>

## Tools

*   If you use GitLab, the self-hosted alternative to GitHub, you can now also create [GitLab Pages](https://pages.gitlab.io/), using a static site builder of your choice (like Jekyll, Hexo, Middleman, or others). You can also easily set up HTTPS for them, and — even better — there are [plans to integrate Let’s Encrypt in it](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1096), so you get a "seamless" HTTPS experience along the way. This is quite amazing to see as it has strong potential now to replace many hosted services with just one self-hosted GitLab server for many people.</p>

## Security

*   [Last week](https://www.smashingmagazine.com/2016/04/web-development-reading-list-131/) I mentioned a social-engineering attack to repositories using Greenkeeper. The developers of the tool now reacted and offer users a method to [verify the identity of the Greenkeeper bot](https://greenkeeper.io/verify.html). As it turns out, the [new GitHub feature that shows verified commits using PGP signatures](https://github.com/blog/2144-gpg-signature-verification) isn't very helpful for that kind of attacks.
*   A spectacular announcement regarding content security has been made this week by Whatsapp: [all (group) messages, calls are now End-To-End encrypted](https://whispersystems.org/blog/whatsapp-complete/) with Open Whisper Systems’ protocol. While this is great to see as it enables encryption for over 1 billion users, you should be aware that your metadata attached to Whatsapp is still not encrypted and while your message content is encrypted for all in-between, Whatsapp is still closed source and they could theoretically build in a logger prior to when the content is encrypted without you noticing it.</p>

## Privacy

*   Today, as developers, we have many great features built into the browser. On the darker side, many of the features are affecting privacy and security of the user, as a site can read most of the information available even without user noticing anything. [A demonstration](https://webkay.robinlinus.com/) shows what information a site can get about you without your confirmation. An eye-opener to re-think browser UIs and how much responsibility we, as developers, have to do the right thing. Be it educating the product owners or your own product where you voluntarily display a dialog to give a choice and notice about sending such data to your servers, **we should embrace ethics**. As a user, I tried to access the demo with a default Chrome setting (revealing horribly much sensitive data) and Firefox with Strict Tracking Protection, uBlock Origin, Disconnect and 3rd party cookies disabled. Despite all blockers, the latter reveals ‘only’ the data about my browser, its active plugins, my hardware and my local and public IP address.</p>

## Web Performance

*   Bryan McQuade has shared his [insights on 2G Network issues observed in India](https://docs.google.com/presentation/d/1fZ7ftsJJ4adiPov4y_8AtV_zjqAmEASaSxRBHBwkiOw/edit). The most interesting fact around there could be that 2G users (which is also still a common state of network in the EU, and probably also in the U.S.) browse the Web with 100kbps and 200ms RTTs. Calibrate your assumptions and test your projects with similar settings.</p>

## Accessibility

*   Many of us are pretty hooked on Custom Elements, and that's because they offer us a great way to encapsulate widgets into a smaller portion of markup. On the other hand, the semantics of Custom Elements is really hard as the browser cannot add any information to the element itself. Now [a guide helps you understand what the browser does for you with a regular HTML element](https://www.paciellogroup.com/blog/2016/04/custom-element-semantics/) regarding semantics, accessibility, usability. So if you are using Custom Elements, don’t forget to do it properly and provide all the required information as well.
*   By now, many of you might have realized that while accessibility is quite important, it’s not always a simple task to achieve. Jamie Teh reviewed [some challenges when using ARIA attributes](https://blog.jantrid.net/2015/12/woe-aria-surprisingly-but-ridiculously.html). Once you got through it, it can make your application and your code better — if used appropriately, of course.</p>

## JavaScript

*   [React 15 is out](https://facebook.github.io/react/blog/2016/04/07/react-v15.html), and with it a couple of interesting changes: instead of setting `innerHTML` when mounting components, it now uses faster `document.createElement`, gets rid of the `data-reactid` attribute on every node and fixes SVG issues. In general, React now officially supports SVG, and produces cleaner markup by avoiding unnecessary `<span>` elements.
*   Seeing [so much code that does not use `debouncing` or `throttling` for scroll, resize or typing events](https://css-tricks.com/debouncing-throttling-explained-examples/), I can only recommend this article for everyone not yet using it. The article visually explains the differences between a normal event listener, debouncing and throttling and shows example code for most common use cases.

{{% feature-panel %}}

## CSS / Sass

*   Have you ever heard about the [CSS `contain` property](https://justmarkup.com/log/2016/04/css-containment/)? I didn't. Well, until I read the article by Michael Scharnagl, explaining that this little property will be soon helping us to solve a lot of use-cases for container queries. The property will allow authors to indicate that an element and its contents are, as much as possible, independent of the rest of the document tree.</p>

## Work & Life

*   “[Being tired isn’t a Badge of Honor](https://m.signalvnoise.com/being-tired-isn-t-a-badge-of-honor-fa6d4c8cff4e). Sustained exhaustion is not a rite of passage. It’s a mark of stupidity. In the long run, work is not more important than sleep. If you aren’t sure how important sleep is, think about this: You’ll die faster without sleep than you will without food.”

## Going beyond…

*   Last Sunday, my mother called me telling me about her issues when accessing her subscription management at a German newspaper "Sueddeutsche Zeitung" (SZ). She asked me because she thought something was wrong with her computer. Well, I checked it and it was the same for me. I noticed an extremely slow response from their server and then I saw something about “[Panama Papers](https://panamapapers.icij.org/)”. A data leak [reported to the SZ](https://panamapapers.sueddeutsche.de/articles/56febff0a1bb8d3c3495adf4/) has now been analyzed partially and the first reports are now published.
*   SZ’s site is a relatively heavy-weighted page with lots of scripts. The site was suffering several days from the massive amount of requests, being mostly inaccessible for many users. This could’ve been avoided by caring more about web performance and by stocking up the resources before such disclosures. On the other hand, it’s now clear that the leaked data has been obtained through vulnerabilities in old Outlook, WordPress and Drupal installations at the company managing the fake companies.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.

<em>Thanks and all the best,
Anselm</em>

