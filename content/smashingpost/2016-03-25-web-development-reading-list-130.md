---
title: >-
  Web Development Reading List #130: Opera Mini, Workflow Fragility And Happy
  Work
slug: web-development-reading-list-130
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/853b28e2-282f-4f11-8465-31a4a7c9f46c/opera-mini-opt.png'
date: 2016-03-25T21:43:27.000Z
author: anselm-hannemann
description: >-
  What a week! Some people were debating over our **npm workflows** and security
  attacks (and sadly not just virtual social engineering ones but real ones in
  Brussels), we've also seen some great new articles that feature the better
  parts of our community and society. I'm happy to share them with you over this
  longer Easter-weekend. Cheers!

  iOS9.3 and OS X 10.11.4 is finally being delivered to users, and with it,
  [Safari 9.1 is
  out](https://developer.apple.com/library/mac/releasenotes/General/WhatsNewInSafari/Articles/Safari_9_1.html)
  with `<picture>` element support, CSS Custom Properties, `will-change`
  property, `unset` value and unprefixed `filter`.
categories:
  - Web Development Reading List
---
What a week! Some people were debating over our <strong>npm workflows</strong> and security attacks (and sadly not just virtual social engineering ones but real ones in Brussels), we've also seen some great new articles that feature the better parts of our community and society. I'm happy to share them with you over this longer Easter-weekend. Cheers!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Fight The System: Battling Bureaucracy](https://www.smashingmagazine.com/2010/09/fight-the-system-battling-bureaucracy/)
*   [How To Spark A UX Revolution](https://www.smashingmagazine.com/2017/03/spark-ux-revolution/)
*   [Hold A Kickoff Meeting Before Diving Into The Design](https://www.smashingmagazine.com/2015/01/hold-a-kickoff-meeting-before-diving-into-the-design/)
*   [Why You Should Include Your Developer In The Design Process](https://www.smashingmagazine.com/2014/11/why-you-should-include-your-developer-in-the-design-process/)

## News

*   iOS9.3 and OS X 10.11.4 is finally being delivered to users, and with it, [Safari 9.1 is out](https://developer.apple.com/library/mac/releasenotes/General/WhatsNewInSafari/Articles/Safari_9_1.html) with `<picture>` element support, CSS Custom Properties, `will-change` property, `unset` value and unprefixed `filter`.

{{% feature-panel %}}

<figure><a href="https://www.brucelawson.co.uk/2016/one-weird-trick-to-get-online-designers-hate-it/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/853b28e2-282f-4f11-8465-31a4a7c9f46c/opera-mini-opt.png" alt="Why Opera Mini Matters" width="500" height="333" /></a><figcaption><a href="https://www.brucelawson.co.uk/2016/one-weird-trick-to-get-online-designers-hate-it/">Why Opera Mini matters</a> for designers and developers in the Western world. By Bruce Lawson.</figcaption></figure>

## General

*   “I ran the stats today. Of more than 250 million Opera Mini users, 50% are on Android/iOS and 50% are on feature phones. The second group of people almost certainly have no choice in which browser to use to get a full web experience. That’s **125 million people** that the designer-on-stage doesn’t care about.” says Bruce Lawson in his article about [why Opera Mini matters](https://www.brucelawson.co.uk/2016/one-weird-trick-to-get-online-designers-hate-it/) for designers and developers in the Western world.
*   In her presentation, Kendra Skeene shares why [access by default](https://www.slideshare.net/KendraSkeene/access-by-default) should be your goal — primarily because accessible code is literally better for everybody.</p>

## Tools

*   I bet most of you have already heard about it: This week, many of the most popular open source packages broke due to one author [pulling all his packages from npm](https://medium.com/@azerbike/i-ve-just-liberated-my-modules-9045c06be67c) due to a [trademark dispute with kik](https://medium.com/@mproberts/a-discussion-about-the-breaking-of-the-internet-3d4d2a83aa4d). Finally, [npm restored the package](https://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm) without the author’s consent to fix the Internet. This event shows how fragile our development workflow has become these days. If just one person pulls a package, millions are affected. If npm itself pulls the registry, most dev workflows will break. If npm changes the authorship of a module and lets a new author ship another unrelated package under the same old name, things will break. Let’s fix our workflows again and not rely on single points of failure.
*   [GSX2JSON](https://gsx2json.com/) is a useful tool to convert Google Spreadsheet to JSON data, available as a simple API.</p>

## Security

*   This week has been troublesome for some people. And while some people’s CI builds broke because of missing npm modules, people using the awesome [greenkeeper service](https://greenkeeper.io/), [experienced a social engineering attack](https://medium.com/@boennemann/your-just-considered-harmful-679db7366b95). Someone has created a GitHub account `greenkeeperlo-bot` that’s very similar to `greenkeeperio-bot`, copied the avatar and sent around a couple of useless Pull Requests. Gladly it didn't end up becoming a malicious attack but shows that even experienced developers just trusted it and merged it without reviewing the changes. Be careful and review your code extensively, all the time!

## Accessibility

*   The W3C published a new document summarizing what is needed to [meet WCAG 2.0](https://www.w3.org/WAI/WCAG20/quickref/) requirements within your website or application.
*   How do you implement media to be accessible for a variety of users? Tricks for writing better alternative texts, or when to provide an empty `alt=""` attribute, how to add video captions, or create transcripts are [shared by Megan Zlock](https://www.viget.com/articles/how-to-create-more-accessible-content-part-2).</p>

<figure><a href="https://www.viget.com/articles/how-to-create-more-accessible-content-part-2"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24bb8dbd-eded-4887-ac50-287d79423f48/accessibility-opt.png" alt="How to Create More Accessible Content" width="500" height="255" /></a><figcaption><a href="https://www.viget.com/articles/how-to-create-more-accessible-content-part-2">How to Create More Accessible Content</a>, an article by Megan Zlock on how to deal with media in terms of accessibility. Worth reading.</figcaption></figure>

## JavaScript

*   Tired of using Mocha or Jasmine for testing your JavaScript modules? Nicolás Bevacqua shows us [how to test our modules with tape](https://ponyfoo.com/articles/testing-javascript-modules-with-tape).
*   The folks from Basecamp just shared how they implemented a [‘Snapback Cache’ to make infinite scrolling feeds at Highrise awesome](https://m.signalvnoise.com/snapback-cache-what-we-use-to-make-our-infinite-scrolling-feeds-at-highrise-awesome-a789128e807a). It’s basically covering a technique to allow visitors to open a link in the infinite scrolling page and then want to read on from the previous position, so the scroll position needs to be restored.</p>

## CSS / Sass

*   Using `object-fit`, some tricks like a lens-vignette won’t work anymore as expected. But [there’s a trick how to make these effects work again](https://fvsch.com/code/object-fit-decoration/).
*   After Jonathan Neal took over the development for the Normalize.css project this month, [version 4.0.0](https://github.com/necolas/normalize.css/releases/tag/4.0.0) has been published, [adding a lot of useful normalizations](https://github.com/necolas/normalize.css/blob/master/CHANGELOG.md) and fixing a couple of bugs.
*   [StickyState](https://github.com/soenkekluth/sticky-state) is a high performance module making native `position:sticky` stateful and polyfilling the missing sticky browser feature.

## Work & Life

*   After years of intensive analysis, Google has discovered that the [key to good teamwork is being nice](https://qz.com/625870/after-years-of-intensive-analysis-google-discovers-the-key-to-good-teamwork-is-being-nice/). Who would’ve thought that, but on the other hand, if Google needs years to get this right, other companies don’t know this either. Maybe it's a chance to change it and finally treat everyone at work and at home nicely.
*   To be creative, you sometimes need to [leave your desk behind](https://www.helpscout.net/blog/creativity-at-work/). By the way, Zoran Jambor, author of CSS Weekly, started an [inspiration newsletter](https://inspiration-bits.com/).

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.

_Thanks and all the best, Anselm_

