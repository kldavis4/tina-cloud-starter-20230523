---
title: >-
  Web Development Reading List #141: jQuery 3, Chillout.js, And How Technology
  Shapes Society
slug: web-development-reading-list-141
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4478e662-aad5-4b74-9bd4-0030021921db/wdrl-141-opt.png'
date: 2016-06-10T17:14:43.000Z
author: anselm-hannemann
description: >-
  There are weeks where I don’t find articles for the “Going Beyond” section of
  the Web Development Reading List at all. And then there are weeks like this
  one, where two brilliant pieces show up that reveal so much about **how we
  live together with new technology** and how this shapes our society.

  Along with a bunch of good tech articles, a great way to leave you for the
  next two weeks. Please note that I’ll be away on vacation next week, so there
  won’t be a summary next Friday.
categories:
  - Web Development Reading List
---
There are weeks where I don’t find articles for the “Going Beyond” section of the <a href="https://www.smashingmagazine.com/tag/web-development-reading-list/">Web Development Reading List</a> at all. And then there are weeks like this one, where two brilliant pieces show up that reveal so much about <strong>how we live together with new technology</strong> and how this shapes our society.

Along with a bunch of good tech articles, a great way to leave you for the next two weeks. Please note that I’ll be away on vacation next week, so there won’t be a summary next Friday.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Use Icons To Support Content In Web Design](https://www.smashingmagazine.com/2009/03/how-to-use-icons-to-support-content-in-web-design/)
*   [<span class="headline">Icons As Part Of A Great User Experience</span>](https://www.smashingmagazine.com/2016/10/icons-as-part-of-a-great-user-experience/)
*   [6 Easy Steps To Better Icon Design](https://www.smashingmagazine.com/2016/05/easy-steps-to-better-logo-design/)
*   [Easy Steps To Better Icon Design](https://www.smashingmagazine.com/2016/05/easy-steps-to-better-logo-design/)

## News

*   [Opera 38](https://dev.opera.com/blog/opera-38/) (and Chromium 51) brings a lot of new ES6 features: iterable array-like DOM interfaces, passive event listeners, and the Intersection Observer API to track when a given element in the DOM enters or leaves the visible viewport.
*   [Firefox 47 is out](https://developer.mozilla.org/en-US/Firefox/Releases/47). It’s shipping Service Worker debugging, support for [`::backdrop` pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/::backdrop), Widevine Content Decryption via EME for mp4, and the case-insensitive modifier `i` (like in `[foo=bar i]`) for CSS attribute selectors has also been added.
*   Finally, after months of waiting, GitHub announced [official and full HTTPS support for their github.io user pages](https://github.com/blog/2186-https-for-github-pages). While HTTPS itself has already worked for quite some time, the traffic from the CDN to the origin servers was not encrypted until now. With the update, you can now enjoy a fully encrypted site. Take care of mixed content, though, to not break pages in modern browsers.
*   WebKit now includes [memory debugging in its web inspector](https://webkit.org/blog/6425/memory-debugging-with-web-inspector/). The announcement post shares how you can make use of it in your applications.

{{% feature-panel %}}

<figure><a href="https://github.com/blog/2186-https-for-github-pages"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82701b0a-05a9-4843-a29e-c8817589e209/github-encryption-opt.png" alt="GitHub encryption" width="500" height="330" /></a><figcaption>GitHub now <a href="https://github.com/blog/2186-https-for-github-pages">officially supports HTTPS</a> for all github.io user sites. (Image credit: <a href="https://github.com/blog/2186-https-for-github-pages">GitHub</a>)</figcaption></figure>

## General

*   Maximiliano Firtman writes [how irresponsible usage of iOS-specific meta tags can break your website](https://medium.com/@firt/dont-use-ios-web-app-meta-tag-irresponsibly-in-your-progressive-web-apps-85d70f4438cb) for a lot of users.</p>

## Tools & Workflows

*   Firebug. The tool that has been replaced by [Firefox’ native developer tools](https://www.smashingmagazine.com/2015/12/revisiting-firefox-devtools/) but nevertheless has wide-spread acceptance among developers. With Firefox’ switch to e10s (multi-process Firefox), however, the extension will no longer work, and its authors now [announced that they won’t port it over](https://blog.getfirebug.com/2016/06/07/unifying-firebug-firefox-devtools/) as a new extension either. Instead, they will focus on providing a Firebug theme for native dev tools and improve those.
*   Andrey Okonetchnikov announced his [new tool `lint-staged`](https://medium.com/@okonetchnikov/make-linting-great-again-f3890e1ad6b8#.zer0si44h) which lets you lint all currently staged files in git.
*   Cloud Four announced [Drizzle](https://blog.cloudfour.com/introducing-drizzle/) yesterday, a tool for generating pattern libraries and style guides.</p>

## Security

*   With the recent password leaks at LinkedIn, MySpace, Tumblr, and Twitter, it has once again become clear that we tend to forget about old passwords. And that’s because passwords are not very useful for authentication, especially since there are two parties involved that could do something wrong (the service provider storing the password, and the user choosing it). [Drew Thomas elaborates on how we can improve authentication](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/). A useful article with a great conversation in the comments section.</p>

## JavaScript

*   [Chillout.js](https://github.com/polygonplanet/chillout) reduces the CPU usage in JavaScript by providing asynchronous iteration functions that have a Promise-based interface. No more “Warning: Unresponsive Script” alerts in the browser.
*   Firefox’ console tries to be more helpful with JavaScript errors. If it’s determinable, the [console will now add a link to MDN](https://hacks.mozilla.org/2016/06/helping-web-developers-with-javascript-errors/) (Mozilla Developer Network) to get more information about the error.
*   [jQuery 3.0 is finally out](https://blog.jquery.com/2016/06/09/jquery-3-0-final-released/). In the works since 2014 already, this is a huge step as it offers a slimmer, faster, and more modern approach than v1 and v2\. There’s an extensive [upgrade guide available](https://jquery.com/upgrade-guide/3.0/) as well as a new version of the [jQuery migrate plugin](https://code.jquery.com/jquery-migrate-3.0.0.js).
*   Jack Franklin shares why it’s important to [make your JavaScript “pure”](https://alistapart.com/article/making-your-javascript-pure). While we often use the easiest way to build a function, these approaches often fail in test scenarios. But they are avoidable by simple additions.
*   “[Promises: All The Wrong Ways](https://blog.getify.com/promises-wrong-ways/)” by Getify shows common approaches with Promises and clarifies how to do better. Worth reading for everyone who’s dealing with Promises.</p>

## CSS/Sass

*   Shaun Bent wrote about [how BBC Sport serves their core CSS with less than 9KB file size](https://medium.com/@shaunbent/css-at-bbc-sport-part-1-bab546184e66). A great in-depth story sharing the principles of their development and product strategy from which we can learn a lot.</p>

## Going Beyond…

*   There’s evidence that new types of media consumption shape our society, yet we don’t see how it happens, because we tend to forget thinking about it. Currently, if at any moment reality gets dull or boring, our phones offer something more enjoyable, more productive, and even more educational than whatever reality gives us. But it also changes us on the inside. We grow less and less patient for reality as it is, especially when it’s boring or uncomfortable. “[What’s at stake is our Agency. Our ability to live the lives we want to live](https://www.tristanharris.com/2016/03/tech-companies-design-your-life-heres-why-you-should-care/), choose the way we want to choose, and relate to others the way we want to relate to them — through technology. This is a design problem, not just a personal responsibility problem.”
*   “There are many reasons why we give away our identities so easily. As far as searching is concerned, we are not used to see ourselves as clusters of missing information. And so we struggle to realize that we may easily be defined negatively, by all our wants. […] Our digital technologies are designed to make us feel relaxed about our lack of privacy.” — Luciano Floridi in his essay “[The Self-Fulfilling Prophesy](https://www.schirn.de/en/magazine/context/the_self_fulfilling_prophesy/)”.

<figure><a href="https://www.schirn.de/en/magazine/context/the_self_fulfilling_prophesy/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e80f2dd-bcf5-4301-a8ce-de4613d23c06/the-self-fulfilling-prohesy-opt.png" alt="The Self-Fulfilling Prophesy" width="500" height="258" /></a><figcaption>“Algorithms have analyzed human identity for economic reasons. The result is dangerously removed from our reality.” A <a href="https://www.schirn.de/en/magazine/context/the_self_fulfilling_prophesy/">thought-provoking read by Luciano Floridi</a>, Professor of Philosophy and Ethics of Information at the University of Oxford.</figcaption></figure>

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}

