---
title: 'Web Development Reading List #114'
slug: black-friday-ui-stack-accessibility-performance
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0848ae95-9de5-46b9-bdd6-1d6956d8e0cb/the-ui-stack-opt1.png
date: 2015-11-27T19:50:49.000Z
author: anselm-hannemann
description: >-
  “Black Friday” has many explanations and various historical reasons. Besides
  that, every year it leads to people buying things just because retailers give
  huge discounts. But do you really need more? **If you wouldn't have bought
  something at its full price, you probably don’t need it at all**.

  In a world where most of us have many things in their home untouched for
  months or years, **we should focus on what is important**. It’s not having the
  newest products, using the latest tools, using the latest cool startup
  service. It’s about helping other people, sharing real experiences and stories
  with your friends. Thank them and yourself this year without a bought gift.
categories:
  - Web Development Reading List
---
<em><strong>What’s going on in the industry?</strong> What new techniques have emerged recently? What insights, tools, tips and tricks is the web design community talking about? <a href="/author/anselm-hannemann/?rel=author">Anselm Hannemann</a> is collecting everything that popped up over the last week in his <a href="https://wdrl.info/">web development reading list</a> so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at. — Ed.</em>

“Black Friday” has many explanations and various historical reasons. Besides that, every year it leads to people buying things just because retailers give huge discounts. But do you really need more? <strong>If you wouldn't have bought something at its full price, you probably don’t need it at all</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Building A Cross-Platform WebGL Game</span>](https://www.smashingmagazine.com/2016/07/babylon-js-building-sponza-a-cross-platform-webgl-game/)
*   [CSS3 Transitions: Thank God We Have A Specification!](https://www.smashingmagazine.com/2013/04/css3-transitions-thank-god-specification/)
*   [Creating Responsive Shapes With Clip-Path](https://www.smashingmagazine.com/2015/05/creating-responsive-shapes-with-clip-path/)
*   [Hybrid Mobile Apps: Providing A Native Experience](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)

In a world where most of us have many things in their home untouched for months or years, we should focus on what is important. It’s not having the newest products, using the latest tools, using the latest cool startup service. It’s about helping other people, sharing real experiences and stories with your friends. Thank them and yourself this year without a bought gift.

{{% feature-panel %}}

I want to thank you for all your support this year!

{{< signature "ah" >}}

## Concepts & Design

*   There are many web applications that fail to deliver a great experience to the user. And that’s because [we often miss out to follow a normal user’s workflow](https://scotthurff.com/posts/why-your-user-interface-is-awkward-youre-ignoring-the-ui-stack). Thus, we miss to design and think about blank, loading, partial, error and ideal states, empty pages.

<figure><a href="https://scotthurff.com/posts/why-your-user-interface-is-awkward-youre-ignoring-the-ui-stack"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0848ae95-9de5-46b9-bdd6-1d6956d8e0cb/the-ui-stack-opt1.png" alt="The User Interface Stack" width="500" height="249" /></a><figcaption><a href="https://scotthurff.com/posts/why-your-user-interface-is-awkward-youre-ignoring-the-ui-stack">The user interface stack</a> includes the blank state, the loading state, the partial state, the error state and eventually the ideal state.</figcaption></figure>

## Tools

*   If you’re like me, you sometimes have a hard time figuring out how to build a query in bash or zsh. Instead, you can easily [use node.js to build command line tools](https://developer.atlassian.com/blog/2015/11/scripting-with-node/).
*   [mention-bot](https://github.com/facebook/mention-bot) automatically mentions potential reviewers on pull requests by using `git blame` to identify who worked on the affected code. Pretty awesome and handy!
*   [Mosh](https://mosh.mit.edu/) is a shell optimized for unstable network connections. You can replace SSH with it and use it if you want a persistent, seamless connection to a server when you’re on the go.</p>

## Security

*   Certificate revocation is an imminent problem and Firefox now shares how they [plan to improve certificate revocation in their browser](https://blog.mozilla.org/security/2015/11/23/improving-revocation-ocsp-must-staple-and-short-lived-certificates/) without affecting HTTPS performance due to the certificate check (OCSP).
*   Yahoo has used Content Security Policy over quite some time now and [now they share what they learned from it](https://www.slideshare.net/BinuRamakrishnan/content-security-policy-lessons-learned-at-yahoo-55438493), so you don’t make the same mistakes and can provide your users with a safe web application.</p>

## Privacy

*   Detectify just found out that your Chrome extensions might spy on you, without you being able to do anything about it. With Chrome making it very easy for extensions to hide requests, a lot of very popular extensions [indeed track your internet traffic and behavior and sell that data](https://labs.detectify.com/post/133528218381/chrome-extensions-aka-total-absence-of-privacy). The team was able to buy access to browsing histories from employees of specified companies, internal network URLs, and could trace it 100% back to a Chrome extension sending that data. That’s pretty bad and you should either switch your browser now or disable all extensions that are not open source and verified to not do that if you don’t want to be tracked.
*   The [relationship between users and companies is based primarily on trust](https://www.privacyinternational.org/node/679). However, many recent developments have the potential to undermine this trust and to question companies loyalties to their users.</p>

## Web Performance

*   Theoretically, in http/2 you should not concatenate your files anymore but serve files in as small modules as possible. However, the engineers of the Khan academy tested this out with a large JavaScript application and [found out it’s not entirely true](https://engineering.khanacademy.org/posts/js-packaging-http2.htm). On the one side they found out that their server http/2 implementation had issues and delayed a couple of requests for no obvious reason. Secondly, the current JavaScript bundler like webpack or browserify can save a lot more bytes by concatenating the sources in comparison to serving individual modules.

## Accessibility

*   Rodney Rehm started to research a little bit on accessibility and its consistency in browsers over a year ago. Now he released [ally.js](https://allyjs.io/), a JavaScript library that helps you make a website or web application accessible. It’s great to see that as it makes optimizing the accessibility of your project much easier.
*   By now, SVG browser support is pretty amazing so there is no reason to use icon fonts anymore. Tyler Sticka shows why it’s actually [a harm to accessibility to use icon fonts](https://blog.cloudfour.com/seriously-dont-use-icon-fonts/). As it’s a webfont, it’s also likely to fail quite often under various network conditions and in data-saving browsers like Opera Mini.
*   The React team shares [how you make React Native apps accessible](https://code.facebook.com/posts/435862739941212/making-react-apps-accessible/). It’s also great to see that they designed the React Accessibility API to look and feel similar to the iOS and Android APIs.

<figure><a href="https://www.etsy.com/teams/7720/bugs/discuss/14559563/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d14e79c9-a7e0-49cd-8216-9b654d62a685/icon-fonts-opt.png" alt="Icon Fonts Bug" /></a><figcaption>Usually we rely on automated tools to choose which Unicode characters are assigned to which icon. But Unicode’s also where our beloved emoji live. If you aren’t careful, they can overlap in confusing (albeit hilarious) ways. <a href="https://www.etsy.com/teams/7720/bugs/discuss/14559563/">Etsy’s “four stars and a horse” bug.</a></figcaption></figure>

## JavaScript

*   You can [detect a user’s app and progress state by using the Page Visibility API](https://www.igvita.com/2015/11/20/dont-lose-user-and-app-state-use-page-visibility/). Ilya Grigorik shares how to do that properly in web applications and shows some of the limits with current browser implementations.</p>

## Work & Life

*   Clearleft's Andy Budd reflects how our industry evolved and why [it’s important to build digital capacity to attract talent](https://www.smashingmagazine.com/2015/11/building-digital-capacity-attracting-talent/). He shares how to build a great team, how to find the right people and what you should do so people want to join your team.
*   We live in an industry that relies on Open Source projects. Yet, [we fail to understand the value of open source projects](https://writing.jan.io/2015/11/20/sustainable-open-source.html) and why it’s toxic to not support people financially who maintain the projects we work with. Jan Lehnhardt shares his views on how we can make open source projects sustainable and why building a great team around it makes everything better.
*   “Energy can be neither created nor destroyed, only transferred or transformed from one form to another.” writes Ben Callahan in a great article on [how to balance your life, prioritize carefully and equally while avoiding to burn-out](https://the-pastry-box-project.net/ben-callahan/2015-November-22).
*   Glenn Garriock asked a few people working in our industry [how they switch off](https://beyondtellerrand.com/blog/how-do-you-switch-off). It’s interesting to see that many people did never consider that question while others tend to do something outdoors or manual work to balance out their virtual all-day work.
*   None of us can deliver outstanding performance every day. And it’s totally fine to do mediocre work. [This one is the practical expression](https://the-pastry-box-project.net/kate-kiefer-lee/2015-november-23) to the previous article about limited amounts of energy and how to balance that in your life.
*   Buffer, known for their remote-working team and open salary policy, now revised the salary formula and you can now even use the formula in their [salary calculator](https://open.buffer.com/transparent-salaries/). I’d still love to see more companies applying such formulae and share their data.</p>

## Go beyond…

*   If you have an opinion, you should be able to back it up. And if you can, please add it to your opinion so people can understand why you have that opinion. By applying that principle you not only avoid putting yourself in a weak position but also avoid unnecessary fights.

I want to leave you with this inspiring quote for the weekend, that, in my opinion, is applicable to every job in the world so I stripped the job so you can fill in your job:
<blockquote>“I firmly believe that <code>_______</code> can change the world and that we, as <code>_______</code>, should be responsible for what we build, what we design, and the impact it has.”—Vina Lustado in <a href="https://readlagom.com/issues/lagom-3">Lagom 3</a></blockquote>

And this was it again for the current week. In case you like what I write here, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>

&nbsp;

