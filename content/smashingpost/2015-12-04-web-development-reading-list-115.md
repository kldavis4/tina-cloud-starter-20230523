---
title: 'Web Development Reading List #115'
slug: web-development-reading-list-115
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84a588ba-52f3-482d-9035-1c5b94f221c4/php7-is-here.jpg'
date: 2015-12-04T19:44:12.000Z
author: anselm-hannemann
description: >-
  _**What’s going on in the industry?** What new techniques have emerged
  recently? What insights, tools, tips and tricks is the web design community
  talking about? [Anselm Hannemann](/author/anselm-hannemann/?rel=author) is
  collecting everything that popped up over the last week in his [web
  development reading list](https://wdrl.info/) so that you don’t miss out on
  anything. The result is a carefully curated list of articles and resources
  that are worth taking a closer look at. — Ed._

  Winter isn’t here yet, instead as you’re reading this, I’m out for another
  biking session in the mountains today. You might already have noticed how
  important nature is to me. So this week, seeing the international climate
  conference in Paris not aiming for an ambitious goal, a reader sent me this
  great article in which he questions [what we as people in the tech industry
  can personally do](https://worrydream.com/ClimateChange/) against global
  warming. If you’re caring only a bit about this, read it and think about it.
  Have a great week and try out some of the amazing web development stuff I
  collected for you this week.
categories:
  - Web Development Reading List
---
_**What’s going on in the industry?** What new techniques have emerged recently? What insights, tools, tips and tricks is the web design community talking about? [Anselm Hannemann](/author/anselm-hannemann/?rel=author) is collecting everything that popped up over the last week in his [web development reading list](https://wdrl.info/) so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at. — Ed._

Winter isn’t here yet, instead as you’re reading this, I’m out for another biking session in the mountains today. You might already have noticed how important nature is to me. So this week, seeing the international climate conference in Paris not aiming for an ambitious goal, a reader sent me this great article in which he questions [what we as people in the tech industry can personally do](https://worrydream.com/ClimateChange/) against global warming. If you’re caring only a bit about this, read it and think about it. Have a great week and try out some of the amazing web development stuff I collected for you this week:

## News

<ul><br>
<li>
Big news from Adobe: they rolled out updates for Photoshop and Illustrator. In Photoshop, you can now <a href="https://blogs.adobe.com/photoshop/2015/11/photoshop-cc-2015-and-fuse-cc-preview-available-today.html">import and export SVG</a> and asset export got an upgrade, too. Illustrator got <a href="https://helpx.adobe.com/illustrator/how-to/export-svg.html">better SVG export</a> and a <a href="https://blogs.adobe.com/adobeillustrator/2015/11/the-latest-release-of-illustrator-cc-is-here.html">new shaper tool</a>. And even bigger news: the Edge tools and services (Edge Animate, Reflow and Inspect) will <a href="https://blogs.adobe.com/creativecloud/update-about-edge-tools-and-services/?scid=social55826686">no longer be developed</a>. Instead, they renamed <a href="https://blogs.adobe.com/flashpro/welcome-adobe-animate-cc-a-new-era-for-flash-professional/">Flash Pro to Animate CC</a>, with plans to integrate Edge Animate’s features into the new tool in the future. Besides that, Adobe plans to bring Dreamweaver back to life, also integrating Brackets into it and de-cluttering the software.</li>
<li>As announced earlier this year, <a href="https://swift.org/">Apple finally open sourced its programming language Swift</a>. You can get the code on Github and find all information on the new website.</li>
<li>Since yesterday, <a href="https://letsencrypt.org/2015/12/03/entering-public-beta.html">Let’s Encrypt is in public beta</a>. So if you have a virtual server, you can <a href="https://timkadlec.com/2015/12/taking-lets-encrypt-for-a-spin/">give it a try by following this guide</a>. My hoster here in Germany will deploy it today, and I hope a lot of other hosting companies will follow soon.</li>
<li><a href="https://secure.php.net/ChangeLog-7.php#7.0.0">PHP 7.0 has finally been released</a> this week. If you aren’t familiar with its new features yet, <a href="https://laracasts.com/series/php7-up-and-running">this guide will tell you more</a>.</li>
<figure class="fwi"><a href="https://secure.php.net/archive/2015.php#id2015-12-03-1"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84a588ba-52f3-482d-9035-1c5b94f221c4/php7-is-here.jpg" width="500" height="289" alt="Alt-Text" /></a><figcaption>PHP7 is finally here. Make sure to check the <a href="https://php.net/manual/de/migration70.php">Migration Guide</a>. <a href="https://pixabay.com/es/elefante-plastilina-modelo-animales-20071/">Image Credit</a></figcaption></figure>

</ul>

## Tools

*   Wouldn’t it be awesome to detect faces in images with JavaScript? We can now do that with [smartcrop.js](https://github.com/jwagner/smartcrop.js). And if you prefer doing it on the server, here’s [a node.js implementation of it](https://www.npmjs.com/package/smartcrop-node).</p>

## Security

*   Stefan Viehböck analyzed thousands of devices and found out that [many of them share the same private keys](https://www.scmagazine.com/nine-percent-of-https-hosts-on-the-web-share-the-same-private-keys/article/456385/) for HTTPS in their firmware, often hard-coded. That, of course, undermines the security of HTTPS and makes the whole data connection unsafe.
*   A demo explains [why browsers show this “annoying” message when you go into fullscreen](https://feross.org/html5-fullscreen-api-attack/) mode. It’s there to let people detect phishing attacks.
*   Snyk analyzes your node.js application for vulnerabilities. And now they [open sourced their vulnerability database](https://github.com/Snyk/vulndb).</p>

## Privacy

*   “The borderless world of money and business is, ironically, a world of ever-more-imposing borders for humans. For example, governments have made ineffectual gestures at getting multinationals to pay their taxes, creating systems that assume an adversary with a huge and well-oiled accounting machine. [The resulting system is virtually impossible for individuals to understand or comply with](https://boingboing.net/2015/12/01/ironically-modern-surveillanc.html).”

## Web Performance

*   Rebecca Murphey shares [the fresh concepts of HTTP/2](https://rmurphey.com/blog/2015/11/25/building-for-http2) and how it will affect our tool and build chain for JavaScript applications. A few good thoughts in there that we can keep in mind to optimize the delivery of large-scale front-end applications.</p>

## Accessibility

*   Facebook seems to push on accessibility lately. Seeing the recent development for React Native, they now published a useful guide that will [bring you from accessibility zero to hero in very short time](https://accessibility.parseapp.com/).</p>

## JavaScript

*   Did you ever want to really understand [how promises work?](https://robotlolita.me/2015/11/15/how-do-promises-work.html) This guide is the definitive answer to probably all your questions.</p>

## CSS / Sass

*   Heydon Pickering shows [how to get a clean flexbox grid](https://medium.com/@Heydon/flexbox-grid-finesse-4d22b80bfee1#.urvo8w81x) that doesn’t look bad in the last row.
*   Style guides are a good thing to manage your components and designs in the company. They constantly evolve, and even [animations and transitions appear in style guides](https://24ways.org/2015/animating-your-brand/) lately. But keeping them up to date is sometimes a challenge. I’m glad there are tools like [DocumentCSS](https://documentcss.com/) that make things like these easier.
*   The `calc()` function in CSS is still pretty new but has good browser support now. So why don’t you start trying it out? Ana Tudor wrote up a few [handy use-cases that’ll solve common problems with CSS calculations](https://www.smashingmagazine.com/2015/12/getting-started-css-calc-techniques/).

{{% feature-panel %}}

## Work & Life

*   “As a leader, your goal should always be to build structures and processes that don't depend on you and ideally don't need you.” says Adam Pisoni in his great article on [how to scale yourself as a technology leader](https://firstround.com/review/the-keys-to-scaling-yourself-as-a-technology-leader/).</p>

## Go beyond…

*   Care about the environment? This week Elon Musk [held a talk to students in Paris](https://fortune.com/2015/12/02/elon-musk-carbon-tax-paris/) in which he reflected on how we can reduce carbon emissions. It’s interesting to read this different opinion on the topic, especially from someone who clearly knows how companies roll. Worth reading.

And with that I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via e-mail, RSS and online.

Thanks and all the best,  
Anselm

