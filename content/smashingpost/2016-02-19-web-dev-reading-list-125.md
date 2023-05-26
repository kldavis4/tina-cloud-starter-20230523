---
title: 'Web Dev. Reading List #125'
slug: web-dev-reading-list-125
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b462374a-233e-4049-9971-2e478020512d/wdrl-125-opt.png'
date: 2016-02-19T18:48:04.000Z
author: anselm-hannemann
description: >-
  It’s Friday again, and I found some interesting articles for you to read over
  the upcoming weekend. In projects, developer, manager and product leaders
  still try to put pressure on the people who work on a task. Somehow they feel
  relieved, more secure if they do that. On the other hand, the **people
  experiencing the pressure of urgency are struggling massively** with it.

  The fallacy here is that while the ones spreading the pressure feel better,
  the people experiencing it usually do a worse job than without the pressure.
  It leads to more bugs, unstructured work and, in the end, all people involved
  will suffer from the result. So instead, a team, which includes everyone from
  a developer to a manager, should focus on the purpose of the work. Give it a
  try, y’all, and now, enjoy your weekend!
categories:
  - Web Development Reading List
---
It’s Friday again, and I found some interesting articles for you to read over the upcoming weekend. In projects, developer, manager and product leaders still try to put pressure on the people who work on a task. Somehow they feel relieved, more secure if they do that. On the other hand, the <strong>people experiencing the pressure of urgency are struggling massively</strong> with it.

The fallacy here is that while the ones spreading the pressure feel better, the people experiencing it usually do a worse job than without the pressure. It leads to more bugs, unstructured work and, in the end, all people involved will suffer from the result. So instead, a team, which includes everyone from a developer to a manager, should focus on the purpose of the work. Give it a try, y’all, and now, enjoy your weekend!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [P Vs. NP: The Assumption That Runs The Internet](https://www.smashingmagazine.com/2015/11/p-vs-np-assumption-that-runs-internet/)
*   [Why Passphrases Are More User-Friendly Than Passwords](https://www.smashingmagazine.com/2015/12/passphrases-more-user-friendly-passwords/)
*   [The Current State Of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
*   [Obfuscating Blacklisted Words In WordPress With ROT13](https://www.smashingmagazine.com/2014/12/encrypting-blacklisted-words-in-wordpress-with-rot13/)

## General

*   [Imagining your future projects is holding you back](https://jessicaabel.com/2016/01/27/idea-debt/). Jessica Abel talks about the problem of idea debt, about thinking too much and making too little.</p>

## Tools

*   [Textlint](https://textlint.github.io/) lets you lint document text content using rules you specify. This is cool to check for grammar or formatting problems in Markdown files.
*   [GitHub now offers templates for issues and pull requests](https://github.com/blog/2111-issue-and-pull-request-templates). Oh, and they [enabled file uploads](https://help.github.com/articles/adding-a-file-to-a-repository/) as well.

{{% feature-panel %}}

<figure class="fwi"><a href="https://github.com/blog/2111-issue-and-pull-request-templates"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4c3ba04-a04e-4391-9211-7b13b38eeb34/github-templates-opt.png" alt="GitHub templates" width="500" height="303" /></a><figcaption>GitHub’s new <a href="https://github.com/blog/2111-issue-and-pull-request-templates">Issue and Pull Requests templates</a> help contributors add the right details at the start of a thread.</figcaption></figure>

## Security

*   [A bug in `glibc` has been disclosed](https://arstechnica.com/security/2016/02/extremely-severe-bug-leaves-dizzying-number-of-apps-and-devices-vulnerable/). As it’s a very bad and easy to exploit bug, you should patch every server (and clients) as soon as possible.
*   Never say “We’ll just use defaults, for now. That password will do, for now.” in the context of security. [It’ll be forgotten, and this is the most dangerous threat](https://paul.reviews/pwnphone-default-passwords-allow-covert-surveillance/) to your data, giving attackers the possibility to do anything with very little effort. Do you have a VoIP phone with a default password? A WiFi router? Change it to something secure. And please tell your friends and family as well. This is important.</p>

## Privacy

*   This week, Apple started a new discussion about privacy, encryption and built-in backdoors on their devices. They received an order to build a custom iOS built, signed by Apple, that lacks several security measurements so that the FBI could hack into phone data relatively easily. [In an open letter](https://www.apple.com/customer-letter/) Apple shared why they declined to do so. Luckily, a lot of companies seem to agree with Apple, and I hope we can find a good way to protect our privacy, and with that, our personal security. Because, as we all know, even if such a backdoor is kept secure, no one could assure that this piece of software won’t get stolen and abused by someone who shouldn’t have access to it.</p>

## Web Performance

*   Rachel Andrew wrote a great guide on how you should start to [make a plan for the transition of web projects to HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/). As the switch should be well planned, it’s a great idea to establish a process to migrate seamlessly and, for now, generate assets and pipelines for both, HTTP/1.1 and HTTP/2, so that a switch is easy.</p>

## JavaScript

*   So, this is nothing ground-breaking but if you ever wondered about a good cross-browser way to check if the document has loaded in pure JavaScript, [this code snippet is for you](https://www.jstips.co/en/detect-document-ready-in-pure-js/).
*   The still relatively new [ESLint has been released in version 2.0](https://eslint.org/blog/2016/02/eslint-v2.0.0-released). It breaks at some point with v1.x but now comes with an auto configuration feature and also introduces [code path analysis](https://eslint.org/docs/developer-guide/code-path-analysis.html).
*   [Hunt](https://jeremenichelli.github.io/hunt/) by Jeremias Menichelli is a JavaScript library that detects if an element becomes visible/invisible and acts on these events, by adding or removing classes, for example. This makes it a great tool to animate elements on scrolling and other interactions.</p>

## CSS / Sass

*   Rémi Parmentier shares a clever way to [build flexible, responsive containers without media queries](https://medium.freecodecamp.com/the-fab-four-technique-to-create-responsive-emails-without-media-queries-baf11fdfa848) which makes the technique a good option for email newsletters.
*   This huge Codepen gives you an [interactive playground for Flexbox](https://codepen.io/enxaneta/full/adLPwv/) properties and values so you can try out what you need for your use case.
*   To be honest, despite the usual `currentColor` use case for inheriting the current color into an SVG element, there are not a lot of ressources that explain how you can use this value. But this example shows you how to [use `currentColor` for colored elements with pseudo-element arrows in it](https://kushagragour.in/blog/2016/01/backgroundcolor-in-currentcolor/) in a clever way.
*   Michael Scharnagl shares how you can use the new custom properties (also known as CSS variables) to [build a theme switcher for your project](https://justmarkup.com/log/2016/02/theme-switcher-using-css-custom-properties/).

<figure class="fwi"><a href="https://medium.freecodecamp.com/the-fab-four-technique-to-create-responsive-emails-without-media-queries-baf11fdfa848"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f67deaa-8407-4db1-b8df-a582585cf30d/the-fab-four-opt.png" alt="Responsive containers in Gmail" width="500" height="312" /></a><figcaption>The <a href="https://medium.freecodecamp.com/the-fab-four-technique-to-create-responsive-emails-without-media-queries-baf11fdfa848#.glnp0tyg9">Fab Four technique</a> lets you create responsive emails without media queries.</figcaption></figure>

## Work & Life

*   Trying to create a sense of urgency almost always backfires. So why not [foster a sense of purpose](https://medium.com/@kimber_lockhart/don-t-create-a-sense-of-urgency-foster-a-sense-of-purpose-724e309ecdb0) instead, which is much better for our brains and our health?
*   As a founder of a company, [your most important skill should be hiring people](https://medium.com/@moritzplassnig/hiring-the-single-most-important-skill-as-a-founder-1028ccc5fc79). Moritz Plassnig from Codeship tells us why it’s so important to build a great team if you want to succeed with your product.</p>

## Going beyond…

*   Last week, I wrote that most of the time the software we write is not critical to people. But what happens if it is? For example, if you sell a smart thermostat and due to a bug in its software the heating is disabled entirely with no option to fix it yourself? [This happened to Nest users](https://www.nytimes.com/2016/01/14/fashion/nest-thermostat-glitch-battery-dies-software-freeze.html), showing the problems of ‘smart’ devices that control critical things in our lives.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>

