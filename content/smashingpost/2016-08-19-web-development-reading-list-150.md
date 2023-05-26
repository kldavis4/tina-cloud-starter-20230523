---
title: >-
  Web Development Reading List #150: Less Code, GitHub’s Security, And The
  Morals Of Science
slug: web-development-reading-list-150
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a20d9355-90ac-4f24-b7e3-323fd1ca644f/wdrl-150-opt.png'
date: 2016-08-19T17:35:37.000Z
author: anselm-hannemann
description: >-
  There is a lot to learn this week. It starts with non-technical things like
  going for a walk to refresh your mind and finishes with how to prevent reverse
  XSS attacks in forms.

  But it doesn’t matter whether you learn how to build self-contained web
  components using the new specification or to maximize the efficiency of your
  Angular 2 app or just how you can write less code. What matters is that you
  **keep asking questions** and that you try to get better and smarter at your
  craft.
categories:
  - Web Development Reading List
---
There is a lot to learn this week. It starts with non-technical things like going for a walk to refresh your mind and finishes with how to prevent reverse XSS attacks in forms. But it doesn’t matter whether you learn how to build self-contained web components using the new specification or to maximize the efficiency of your Angular 2 app or just how you can write less code. What matters is that you **keep asking questions** and that you try to get better and smarter at your craft.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Front-End Performance Checklist 2017 (PDF, Apple Pages)](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [Styled-Components: Enforcing Best Practices In Component-Based Systems](https://www.smashingmagazine.com/2017/01/styled-components-enforcing-best-practices-component-based-systems/)
*   [Making A Service Worker: A Case Study](https://www.smashingmagazine.com/2016/02/making-a-service-worker/)
*   [Mistakes Developers Make When Learning Design](https://www.smashingmagazine.com/2016/12/mistakes-developers-make-when-learning-design/)

## General

*   Heydon Pickering shares tips on [writing less code](https://www.heydonworks.com/article/on-writing-less-damn-code) to make your developer life easier. Something we all should remember.</p>

## Tools & Workflows

*   [Nucleus](https://holidaypirates.github.io/nucleus/) is certainly not the first living style guide generator but it’s still worth sharing. The Node.js module fits into existing projects, follows the Patternlab splitting by default, and has a nice layout where you easily find the things you’re looking for.
*   If you ever lost a stash in git, here are a few tips on [how to recover dropped stashes](https://stackoverflow.com/questions/89332/how-to-recover-a-dropped-stash-in-git/7844566).

{{% feature-panel %}}

<figure><a href="https://holidaypirates.github.io/nucleus/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/967156a4-67fd-4b76-936c-f8bf2da37bcb/nucleus-opt.png" width="500" height="345" alt="Nucleus" /></a><figcaption><a href="https://holidaypirates.github.io/nucleus/">Nucleus</a> is a living style guide generator that fits in well in both new and existing projects.</figcaption></figure>

## Security

*   Matthew Green asks himself [if Apple’s cloud key vault is a crypt backdoor](https://blog.cryptographyengineering.com/2016/08/is-apples-cloud-key-vault-crypto.html?m=1). In his explanatory answer, he shares why Apple’s method of using Hardware Security Modules is pretty clever and maybe worth learning more about if you’re interested in storing sensitive user data behind weak user-set passwords.
*   Using social engineering by pretending to be a valid website in the URL bar is easy with the <abbr title="right to left">RTL</abbr> feature of Chrome and Firefox and [this little trick](https://www.rafayhackingarticles.net/2016/08/google-chrome-firefox-address-bar.html). I’m sure this type of attack is successful since most normal users do check if a URL is correct but they can’t see anything bad in it. A good reminder that we need to find better ways to let users know that the URL they visit is safe.
*   When we look into the source code of forms at github.com, [we’ll find some interesting markup in there](https://chloe.re/2016/07/19/protect-against-html-extraction/). Its purpose: preventing XSS attacks. In [this blog post we can learn about the tricks that GitHub uses](https://chloe.re/2016/08/15/lets-look-at-some-of-the-security-at-github/) to maximize the security of their web application.
*   Troy Hunt wraps up [how our personal data is usually leaked](https://www.troyhunt.com/website-enumeration-insanity-how-our-personal-data-is-leaked/) and why security is a design process, not only an implementation process. Also a good primer on how to design a password recovery feature.

<figure><a href="https://www.rafayhackingarticles.net/2016/08/google-chrome-firefox-address-bar.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09fcf8e1-971b-490e-82e9-c30c09253422/security-tips-spoofing-opt.png" width="500" height="321" alt="Address bar spoofing" /></a><figcaption>Who’s really behind the URL? Ray Baloch uncovers an <a href="https://www.rafayhackingarticles.net/2016/08/google-chrome-firefox-address-bar.html">address bar spoofing vulnerability</a> in Chrome and Firefox. (Image credit: <a href="https://www.rafayhackingarticles.net/2016/08/google-chrome-firefox-address-bar.html">Rafay Baloch</a>)</figcaption></figure>

## Web Performance

*   Nolan Lawson wrote about [the cost of small modules](https://nolanlawson.com/2016/08/15/the-cost-of-small-modules/), analyzing how much code is used when you build your codebase with a lot of small modules. The article reveals interesting stats and compares modern minifiers and JavaScript bundlers, as well as execution times of such bundles in various browsers.</p>

## JavaScript

*   Minko Gechev shares how you can do [Ahead-of-time compilation in Angular 2](https://blog.mgechev.com/2016/08/14/ahead-of-time-compilation-angular-offline-precompilation/) to improve performance and reduce energy and bandwidth consumption to make your application more efficient.
*   Addy Osmani shares best practices on [how to use offline storage for your web application](https://medium.com/@addyosmani/offline-storage-for-progressive-web-apps-70d52695513c) to ensure the app stays usable when the network connection is flakey.
*   Eric Bidelman explains [the new Shadow DOM v1 standard](https://developers.google.com/web/fundamentals/primers/shadowdom/), the now de-facto standard for building self-contained web components.</p>

## Work & Life

*   Margaret Gould Stewart talks about how she learned that [making mistakes is crucial for a team’s morale](https://shift.newco.co/how-a-single-conversation-with-my-boss-changed-my-view-on-delegation-and-failure-ae5376451c8d) and why this prevents people from becoming bored, burning out, and from feeling annoyed about their manager.
*   Sometimes, [a long walk outside can refresh your mind](https://zenhabits.net/walk/). It can give you new inspiration and help you calm down if you’re feeling upset.</p>

## Going Beyond…

*   Bill Gates shares [what he learned from his school teacher](https://www.gatesnotes.com/Education/A-Teacher-Who-Changed-My-Life) and how only later he realized that students should ask teachers more questions. If we ask more, we will learn from others. It’s always harder to proactively communicate knowledge to other people than being asked for it.
*   Phillip Rogaway shares a paper on “[The Moral Character of Cryptographic Work](https://web.cs.ucdavis.edu/~rogaway/papers/moral-fn.pdf)” (PDF). An interesting read on the shift of power and why cryptography is often a political tool that demands high morals and ethical fundamentals of those who build it. Anyone who ever discussed the topic of morals and ethics in science should read this.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

