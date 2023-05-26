---
title: 'Web Development Reading List #131: Git 2.8, CSS Grids And The Key To Good Code'
slug: web-development-reading-list-131
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc8f9069-23c2-4611-b9ee-47f43b2a9062/wdrl-131-opt.png'
date: 2016-04-01T19:34:16.000Z
author: anselm-hannemann
description: >-
  Although it’s April 1st, and people go all crazy making up jokes and spreading
  hoaxes, I’m sending out this edition to you without any April fools. Instead,
  I want to challenge you to **put more effort, more thoughts into your code**.

  Instead of blindly following a given path to build the solution with the least
  effort, what about thinking more about your users? Wouldn’t a lot more users
  benefit from you spending an additional hour on building a form on your own
  instead of relying on a third party that involves tracking? Wouldn’t they
  benefit from a smaller website that doesn’t contain big libraries?
categories:
  - Web Development Reading List
---
Although it’s April 1st, and people go all crazy making up jokes and spreading hoaxes, I’m sending out this edition to you without any April fools. Instead, I want to challenge you to <strong>put more effort, more thoughts into your code</strong>.

Instead of blindly following a given path to build the solution with the least effort, what about thinking more about your users? Wouldn’t a lot more users benefit from you spending an additional hour on building a form on your own instead of relying on a third party that involves tracking? Wouldn’t they benefit from a smaller website that doesn’t contain big libraries? Many people and crawling extensions could also benefit from a better document outline. In the end, it’s your product and your work that users see — and I bet you want to be proud of what you’ve just built.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Dealing With Loud And Silent Burnout</span>](https://www.smashingmagazine.com/2015/10/dealing-with-loud-silent-burnout/)
*   [You Are Not A Machine. You Are Not Alone.](https://www.smashingmagazine.com/2014/10/you-are-not-a-machine-you-are-not-alone/)
*   [Feeling Stuck? Design What You Don’t Know](https://www.smashingmagazine.com/2014/10/design-what-you-dont-know/)
*   [<span class="headline">Spotify Playlists To Fuel Your Coding And Design Sessions</span>](https://www.smashingmagazine.com/2016/11/playlists-fuel-coding-design-sessions/)

## News

*   The [git 2.8 release](https://github.com/blog/2131-git-2-8-has-been-released) lets you update submodules in parallel via `git fetch --recurse-submodules --jobs=4` and check <abbr title="End Of Line">EOL</abbr> issues with `git ls-files --eol FILENAME`. Also, it comes with better user management, improvements for Windows, and, finally, you can now speed up commands like `git status` by using a new caching. To [enable it, use `git config --system core.untrackedCache true`](https://news.ycombinator.com/item?id=11388479).
*   Big news from Apple again: They now have a [developer edition of Safari](https://developer.apple.com/safari/download/) for us (usually updated every two weeks) that you can run side by side with Safari or WebKit Nightly. Feature-wise, [see the release notes](https://developer.apple.com/safari/technology-preview/release-notes/) for more information.</p>

## General

*   What’s the key to good code? It’s not about great algorithms, or that the code is scalable. The [key to good code is reducing its cognitive load](https://chrismm.com/blog/how-to-reduce-the-cognitive-load-of-your-code/). Christian M. Mackeprang shares his approach on how to do that easily.
*   “I don’t always test my code, but when I do, it feels better.” But it’s not only about writing tests for your software. It’s also [about _how_ to write tests](https://mikbe.com/code/testing/dx/2016/03/11/why-and-how-testing-can-make-you-happier.html). Because the simpler a test, and the less brain power it needs to be written and to be read, the better it is.</p>

## Concepts & Design

*   Pedro Duarte shares the entire [process of The Times website redesign](https://medium.com/@peduarte/building-the-ui-for-the-new-the-times-website-26dc4e6569e). It’s quite interesting to see the process rather than only the technical details around it.
*   Sara Wachter-Boettcher shares why we should remember that, when planning a project, [it’s important not to let our excitement lull us into blithely ignoring life’s harsher realities](https://alistapart.com/article/design-for-real-life-interview-with-sara-wachter-boettcher). It can be inconvenient for users to fill out a form asking for personal details, and while it’s easier for us to use convenient standards, investing more work into thinking about a better solution can bring relief for hundreds of users.
*   Sometimes, less is more. Jonas Downey elaborates on [building what matters and skipping the rest](https://m.signalvnoise.com/you-aren-t-gonna-need-to-design-it-997349d7cc20).

{{% feature-panel %}}

<figure class="fwi"><a href="https://m.signalvnoise.com/you-aren-t-gonna-need-to-design-it-997349d7cc20"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11dd7a7e-b297-4417-8573-70741c9d41af/less-is-more-opt.png" alt="Build what matters" width="500" height="335" /></a><figcaption>Don’t try to foresee what you might eventually need. <a href="https://m.signalvnoise.com/you-aren-t-gonna-need-to-design-it-997349d7cc20">Build what matters</a>! (Image credit: <a href="https://m.signalvnoise.com/you-aren-t-gonna-need-to-design-it-997349d7cc20#.rju8svvj8">Jonas Downey</a>)</figcaption></figure>

## Tools

*   At Microsoft’s Build 2016 conference, the company announced the [availability of the Bash Shell on Windows 10](https://www.hanselman.com/blog/DevelopersCanRunBashShellAndUsermodeUbuntuLinuxBinariesOnWindows10.aspx) with the next major OS update.
*   Docker has always worked fine on Linux machines but on Windows and OS X there were a couple of annoying issues that made using it very hard. The authors now shipped [a beta for Docker for Mac and Windows](https://blog.docker.com/2016/03/docker-for-mac-windows-beta/), a new experience that finally works better with these systems. It does not need VirtualBox anymore, supports proper Volume mounting, better network profile support, and fits the OS X sandbox security model (which was probably the most annoying issue with Docker on Mac). The only drawback? The current sign-up process for the beta requires a 3rd party tracker to be enabled.
*   Do you remember Jenkins, the Continuous Integration server? [It’s back with an improved version 2.0](https://jenkins.io/2.0/). The update has better pipelines, much better git support and integration, a way better user experience with easier configuration pages, and it’s backwards-compatible so that there is no reason not to upgrade from a Jenkins 1.x version to the new one! As an alternative, [GitLab now has better Runners](https://about.gitlab.com/2016/03/29/gitlab-runner-1-1-released/) that allow it to be used not only as a version control management platform but as a full CI service as well.
*   As a result of recent unpublishing issues on npm, the [registry will from now on be stricter about if an author can unpublish a version](https://blog.npmjs.org/post/141905368000/changes-to-npms-unpublish-policy) from it. On the other hand, Nicolás Bevacqua [sums up the still remaining security risks](https://ponyfoo.com/articles/npm-meltdown-security-concerns) that come with using a package manager like npm. Finally, we should not forget that while we’re only talking about npm here, other package managers have at least some of the same issues.</p>

## Security

*   These days, we are using so many external services for our own products. Advertising, forms, CDNs, analytics, tracking, split testing — these are mostly done by third parties. But what does a user think about a website that serves malware/ransomware? The user does not know nor care which service’s fault that is. [He/She will make the creator of the website responsible and is entirely right about doing so](https://windowsitpro.com/troy-hunts-security-sense/security-sense-you-re-responsible-third-party-services-and-code-you-use).
*   [Malicious npm packages can execute a script](https://blog.npmjs.org/post/141702881055/package-install-scripts-vulnerability) that includes itself into a new package that is then published to the registry and to other packages owned by that user. Be careful and take action if you’re not sure about the package you install. And don’t trust all packages right away, especially if you’re logged into your npm account. Nathan Johnson [shares a npm hijack from his perspective as the hijacker](https://medium.freecodecamp.com/npm-package-hijacking-from-the-hijackers-perspective-af0c48ab9922).</p>

## Privacy

*   So indeed, [mass surveillance silences minority opinions](https://www.washingtonpost.com/news/the-switch/wp/2016/03/28/mass-surveillance-silences-minority-opinions-according-to-study/), as a new study reveals. And now think about what mass surveillance means: Is it just the governments’ actions or is it also corporate services like advertisers, tracking services, companies like Facebook or Google embedded into websites?

## Accessibility

*   You are in your mid-twenties and your vision is 20/20 or better. You are not color blind and all the devices you own have a ‘retina’ screen. You are standing in a major city and your internet is fast. [Now read on](https://mrmrs.io/writing/2016/03/23/the-veil-of-ignorance/).
*   Microsoft has [released CaptionBot](https://www.captionbot.ai/) at their Build conference. The tool analyzes images for their content and suggests a description of what is seen on the photo. It’s actually quite impressive how good the results work and how this could improve accessibility and help automate processes to provide alternative texts for images.
*   Kitty Giraudel seems to have done quite some research on accessibility lately. Now he has introduced an [outline audit tool for websites](https://dev.edenspiekermann.com/2016/03/29/introducing-outline-audit/) that lets you verify your document outline regarding proper semantics and accessible content.

<figure class="fwi"><a href="https://www.captionbot.ai/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe0008db-91ea-4e3b-8375-4b497553095a/captionbot-opt.png" alt="CaptionBot in action" width="500" height="331" /></a><figcaption>Microsoft’s <a href="https://www.captionbot.ai/">CaptionBot</a> in action.</figcaption></figure>

## CSS/Sass

*   So, one of the best resources to refer to when looking up some Flexbox property is the “[Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)” on CSS-Tricks. Now the same concept has been transfered to CSS Grids, making the “[Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)” the resource to remember for the future when this technology is ready to be widely used.
*   How scalable is CSS? And at scale, is CSS the problem or are we, the developers, the problem? What does `DRY` mean? And how do we define _CSS at scale_? This [essay about scaling CSS](https://mrmrs.io/writing/2016/03/24/scalable-css/) sheds some light on these matters.</p>

## Going beyond…

*   There isn’t a person amongst us who doesn’t have insecurities — [some are just better at dealing with them, or perhaps hiding them](https://zenhabits.net/insecurities/). But if you make yourself aware of the obstacles, you can get onto the road to overcoming the feeling of insecurity.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</p>

<em>Thanks and all the best,
Anselm</em>

