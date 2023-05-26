---
title: 'Web Development Reading List #100'
slug: web-development-reading-list-100
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dc6f58b-0d91-4b52-9a96-500693895bc2/howdnsworks-opt.png
date: 2015-08-21T16:16:26.000Z
author: anselm-hannemann
description: >-
  _What's happening in the industry? What important techniques have emerged
  recently? What about new case studies, insights, techniques and tools? Our
  dear friend Anselm Hannemann is keeping track of everything so you don't have
  to. The result is a carefully collected list of articles that popped up over
  the last week and which might interest you. Starting from today, we are happy
  and honored to feature a **bi-monthly web development reading list** here on
  Smashing Magazine. Now it should be a bit easier to stay up to date. — Ed._

  Welcome to the one hundredth edition of the [Web Development Reading
  List](https://wdrl.info/) and the first one to appear on Smashing Magazine. I
  am very happy to extend my audience and keep you up to date with the web
  development industry. If you have any feedback, please let me know in the
  comments or write me an email.
categories:
  - Web Development Reading List
---
<em>What's happening in the industry? What important techniques have emerged recently? What about new case studies, insights, techniques and tools? Our dear friend Anselm Hannemann is keeping track of everything so you don't have to. The result is a carefully collected list of articles that popped up over the last week and which might interest you. Starting from today, we are happy and honored to feature a <strong>bi-monthly web development reading list</strong> here on Smashing Magazine. Now it should be a bit easier to stay up to date. — Ed.</em>

Welcome to the one hundredth edition of the <a href="https://wdrl.info/">Web Development Reading List</a> and the first one to appear on Smashing Magazine. I am very happy to extend my audience and keep you up to date with what's going on in the web development industry. If you have any feedback, please let me know in the comments or write me an email.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Are We Thinking About Digital All Wrong?](https://www.smashingmagazine.com/2014/03/are-we-thinking-about-digital-all-wrong/)
*   [All You Need To Know About Customer Journey Mapping](https://www.smashingmagazine.com/2015/01/all-about-customer-journey-mapping/)
*   [How To Make Yourself Redundant](https://www.smashingmagazine.com/2013/11/making-yourself-redundant/)
*   [How To Spark A UX Revolution](https://www.smashingmagazine.com/2017/03/spark-ux-revolution/)

## News

*   You can now [test Microsoft’s new Edge browser in a virtual machine](https://blogs.windows.com/msedgedev/2015/08/17/windows-10-virtual-machines-now-available-on-microsoft-edge-dev/). Finally, a Windows 10 VM image is up on the testing website and you are able to natively test for compatibility.
*   The [`link rel="preconnect"`](https://codereview.chromium.org/1226203003/) meta property is now supported by Chromium, and will soon be available in Chrome and Opera.
*   The first feature-complete [beta of PHP7 has been released](https://www.hongkiat.com/blog/php7/) and it is great to see the massive performance impovements, better error handling, 64-bit support and many more cool things you should check out if you are using PHP as your language of choice.
*   [Ember 2.0 is out](https://emberjs.com/blog/2015/08/13/ember-2-0-released.html). It's less about new shiny features but much more about removing all the old cruft from the code without breaking older codebases. Very cool to read about their clever deprecation and release plan.
*   [Pointer Events have landed in Firefox Nightly](https://hacks.mozilla.org/2015/08/pointer-events-now-in-firefox-nightly/). They have been part of Firefox Mobile for a long time but now desktop has support, too, leaving only WebKit browsers not supporting it.
*   The [WebKit project now has a roadmap/feature status page](https://www.webkit.org/status.html) as well. This is great news as it suggests techniques that Apple might integrate into their OS X and iOS Safari browsers in near future. I am glad that social media pressure seems to work again and WebKit joins a more open process of development.</p>

## General

*   [The problem is not that we are moving too fast with the web platform](https://ponyfoo.com/articles/fast-forwarding-the-web-platform) but that we still lack ways of providing developers easy ways to do basic things. We’re focusing on the wrong stuff. And that is what we need to fix. Wise words by Nicolas Bevacqua.
*   Aaron Gustafson, meanwhile, has summed up [the quest for better interoperability instead of features](https://www.aaron-gustafson.com/notebook/ramblings-on-new-browser-features-interoperability-craft-and-the-future-of-the-web/).</p>

## Concepts And Design

*   Petro Salema’s beyondtellerrand video is up and it’s worth watching: “[Designing Interfaces That Think](https://beyondtellerrand.com/events/duesseldorf-2015/speakers/petro-salema)”. A good primer on user experience design and clever thought interfaces.
*   Why we should [take more time creating empty states](https://medium.com/@InVisionApp/why-empty-states-deserve-more-design-time-44b5adc7eb52) in our applications. They are key to user happiness.</p>

## Tools

*   [An introduction to Git](https://blog.mwaysolutions.com/2015/07/16/a-short-introduction-to-git/). If you haven’t used it yet or still don’t get the basics, this is a series worth reading. For example, learn the [differences between `git merge` and `rebase`](https://blog.mwaysolutions.com/2015/07/23/git-merge-and-rebase-part-2-of-3/) or [how to deal with conflicts](https://blog.mwaysolutions.com/2015/08/04/git-conflicts-part-3-of-3/).
*   [Never, ever expose your Git repository](https://thenextweb.com/insider/2015/07/27/a-simple-developer-error-is-exposing-private-information-on-thousands-of-websites/) on a public webserver. It will leak not only code but passwords, keys and more.
*   Most of us use npm or Bower together with Grunt or Gulp nowadays. But for some projects the latter are often not necessary. Within your npm package.json it is possible to run scripts and complete basic tasks without the additional abstraction of Gulp or Grunt. Hans Christian Reinl shares how he approaches task automation in projects using some simple scripts with just npm.
*   Hui Jing learned web languages three years ago. Now he is sharing why [it's important to know the basics of web development before you use a framework](https://www.chenhuijing.com/blog/people-are-the-problem/). The problem isn't with the frameworks but often the lazy people using them.
*   If you use Windows, you probably have a hard time with Node and npm. But now there is this little tool called [npm-windows-upgrade](https://www.npmjs.com/package/npm-windows-upgrade) that ensures your command line will find the new npm version right away.</p>

## Security/Privacy

*   To use several newer browser APIs it is essential to have an HTTPS connection. ServiceWorkers, for example, require a TLS connection to work. Andrea Giammarchi shares [how to set up a TLS certificate for your localhost](https://www.webreflection.co.uk/blog/2015/08/08/bringing-ssl-to-your-private-network).
*   Windows 10 has been out a few weeks now and while it finally nails user experience, it introduces [a couple of not so cool privacy issues](https://thenextweb.com/microsoft/2015/07/29/wind-nos/) you should be aware of, like the auto-backup of your private encryption key to OneDrive (you know that officials have access to Microsoft products), customized ad fingerprinting, and possible data disclosure. Take care if you upgrade.
*   The LetsEncrypt initiative shared [their new launch schedule](https://letsencrypt.org/2015/08/07/updated-lets-encrypt-launch-schedule.html) with general availability in the week of November 16th this year. While it's being pushed back a little, to me this is a good thing: more stability and probably a better product. I think the key to its success is that hosting companies are able to implement it seamlessly, which is going to be hard.
*   Mark McDonnell shares his research on what the [security basics of the web](https://www.integralist.co.uk/posts/security-basics.html) mean. He explains PGP, SSL, SSH, certificates, and the general purpose of public and private key methods.</p>

## Web Performance

*   DNS: the heart of the internet. If you never really understood how DNS works internally to resolve a domain name, you should be entertained by these comic strips on [how DNS works](https://howdns.works/).

<figure><a href="https://howdns.works/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dc6f58b-0d91-4b52-9a96-500693895bc2/howdnsworks-opt.png" alt="How DNS works" width="500" height="396" /></a><figcaption>If you've never really understood how DNS works to resolve a domain name, you should find these comic strips entertaining and educational: <a href="https://howdns.works/">How DNS Works</a>.</figcaption></figure>

{{% feature-panel %}}

*   An approach used not only by Facebook, but this article explains their [image optimization technique in detail](https://code.facebook.com/posts/991252547593574/the-technology-behind-preview-photos/): when a user loads a profile, first a 200byte preview image is loaded to bridge the time gap until the real image is loaded.
*   The web sucks. Well, maybe advertising-dependent websites suck: [a plea from Jeremy Keith to focus on users](https://adactio.com/journal/9312) and not blame the web for being slow and clunky. Meanwhile, Google opened [Contributor](https://www.google.com/contributor/welcome/) in the US. To be honest, I think replacing the ad canvas with a pattern or cat content and adding supercookies for paying users is not the way to reduce ads on the web.
*   “[The Difference Between Minification and Gzipping](https://css-tricks.com/the-difference-between-minification-and-gzipping/)” shows how important it is to properly configure your server and why minifying your resources gives the last bit to a performance boost.
*   Typekit is now pushing a [new font embed code that is set to asynchronous](https://blog.typekit.com/2015/08/04/new-embed-code-for-asynchronous-font-loading/) loading by default.</p>

## HTML/SVG

*   Lea Verou shows you how to [create pie charts with SVG and CSS](https://www.smashingmagazine.com/2015/07/designing-simple-pie-charts-with-css/).
*   I have written a bit about native or custom elements and why we need web components but shouldn’t misuse them for what they can’t do.</p>

## Accessibility

*   The accessibility tool [Tenon is now free for open source projects](https://us2.campaign-archive1.com/?u=db90adfcd71356341118b0a41&id=de77e18b90&e=4de96f8850). Big ups for that!
*   And while better tools for accessibility arrive, Yahoo, Facebook, Twitter, Adobe, LinkedIn and more just announced that they will [prefer people who do accessibility in their hiring process](https://www.washingtonpost.com/news/the-switch/wp/2015/07/23/this-small-change-could-make-a-big-difference-for-accessible-technology/). This is a great step in the right direction and I would love to see similar approaches in other companies around the world.
*   That said, it is a good idea to start implementing accessibility in incremental steps to your app or website. It's natural not to start off with 100% and it's not necessary, but if you [start with small steps](https://the-pastry-box-project.net/charlotte-spencer/2015-july-31) you will see how much fun it can be to implement accessibility in your project.</p>

## JavaScript

*   [Knwl.js](https://loadfive.com/os/knwl/) is a small script that parses natural language inputs into computer-readable formats. That way you can offer users the ability to input dates like "Tomorrow 9am." It works with dates, times, emails, URLs and phone numbers.
*   Dr Axel Rauschmayer has created a [quick introduction to ES6](https://www.2ality.com/2015/08/getting-started-es6.html) for beginners that is great to start learning it.
*   If you write about front-end browser compatibility, [caniuse](https://caniuse.com/) is our reference of choice. A clever script called [getCaniuse](https://github.com/tevko/getCaniuse) parses browser compatibility for you and adds a caniuse reference to the post.
*   It can be helpful to have a real-time search on your page. Osvaldas Valutis shares how he built a [simple JavaScript live search](https://osvaldas.info/real-time-search-in-javascript) without jQuery or other dependencies.
*   Nicolas Bevacqua explains why [plain JavaScript modules are better](https://ponyfoo.com/articles/why-i-write-plain-javascript-modules) than framework-dependent modules, sharing his approach on how to be framework-independent while not needing much more effort to create a module.
*   Kitty Giraudel wrote a great piece on how to [learn regular expressions in a practical way](https://hugogiraudel.com/2015/08/19/learning-regular-expressions-the-practical-way/). For people struggling with complex regular expressions (like me) this is a very helpful guide.</p>

## CSS/Sass

*   “[Constructing CSS Quantity Queries On The Fly](https://www.smashingmagazine.com/2015/07/constructing-css-quantity-queries-on-the-fly/)”. Tools are here to help.
*   I guess you have used the `float` property a couple times. And I bet you wondered about some of its weird behavior, too. “[How Floating Works](https://bitsofco.de/2015/how-floating-works/)” provides a very visual and clear explanation of floated element behavior.
*   “[What The Flexbox?!](https://flexbox.io/#/)” by Wes Bos is a series of twenty short videos teaching you the details of the flexbox technique.</p>

## Work life

*   Every one of us gets annoyed by our current job. But it isn’t easy to decide [when and if it's time to leave](https://alistapart.com/column/job-hunting-for-web-designers-and-developers) or if addressing the issues that concern us is enough.
*   [Working remotely isn’t always a dream](https://medium.com/digital-nomad-stories/working-remotely-isn-t-always-a-dream-151619ae45dc). But you can learn to get around most problems with some simple tricks.
*   [We can’t let our fear of the future rob us of the joy of the present](https://us3.campaign-archive1.com/?u=cefae11d379c411a337d2df24&id=979daa91ac&e=40d1d9694f). Next time you feel in need of a break and you hear your fear whispering that it could all fall apart, take that break anyway.
*   Rachel Andrew shares how important it is to [stay confident and deal with what seems overwhelming](https://rachelandrew.co.uk/archives/2015/08/14/confidence-and-overwhelm) in the massive amount of new technologies and the fast pace of change in web development. What's really important is to have solid core skills. Frameworks come and go, but understanding the basics and building sensible infrastructure will be helpful throughout your whole career.
*   While only a few years back people said ‘fire anyone who is not a workaholic, this is startup life,’ since then we have grown up and realized that we need to [help workaholics to avoid burn-out](https://signalvnoise.com/posts/902-fire-the-workaholics).</p>

## Go beyond…

*   We all try to learn new things. Sometimes this works fine, sometimes we get bored and give up. But there is a reason why you learn some things more easily than others: interest. [When you build something new, make sure it interests you](https://alistapart.com/blog/post/building-to-learn).
*   Reports about working for Amazon, the biggest online store in the world, are not new. But [this summary on The Next Web](https://thenextweb.com/opinion/2015/08/15/the-real-deathstar/), based on a [new report by the New York Times](https://www.nytimes.com/2015/08/16/technology/inside-amazon-wrestling-big-ideas-in-a-bruising-workplace.html) shows how bad it really is as an Amazon employee. People with cancer or caring for family members get fired. Maybe it's time to rethink the ‘just buy on Amazon, it’s convenient’ stance.
*   Agile: a term hated by many, loved by many. So, ask yourself [what agile is](https://blog.generalassemb.ly/agile/). Then [question if agile is agile](https://vimeo.com/131410262), and then decide which way to go with your projects.

And with that, I’ll close for this week. If you like this news round-up, please support me via <a href="https://goo.gl/dDWsTF">Flattr</a>, <a href="https://goo.gl/cnqtOc">gratipay</a> or share this resource with other people. You can also <a href="https://wdrl.info/">subscribe to the newsletter</a> and get the links right to your inbox.

Thanks and all the best,
Anselm

