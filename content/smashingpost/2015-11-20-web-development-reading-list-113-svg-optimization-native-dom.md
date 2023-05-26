---
title: >-
  Web Development Reading List #113: SVG Optimization and Native DOM Selection
  Tricks
slug: web-development-reading-list-113-svg-optimization-native-dom
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a635bad-c7f0-4777-9a41-78aac0451090/bonjour-optim.png'
date: 2015-11-20T20:05:51.000Z
author: anselm-hannemann
description: >-
  _**What’s going on in the industry?** What new techniques have emerged
  recently? What insights, tools, tips and tricks is the web design community
  talking about? [Anselm Hannemann](/author/anselm-hannemann/?rel=author) is
  collecting everything that popped up over the last week in his [web
  development reading list](https://wdrl.info/) so that you don’t miss out on
  anything. The result is a carefully curated list of articles and resources
  that are worth taking a closer look at. — Ed._

  Autumn is nearly over, winter is coming to Germany and on the weekend the
  forecast predicted the first snow for the Bavarian Alps which is near where I
  live. Time to read about Service Workers, and some abstract topics like
  teaching complex algorithms, and how to be more objective.
categories:
  - Web Development Reading List
---
<em><strong>What’s going on in the industry?</strong> What new techniques have emerged recently? What insights, tools, tips and tricks is the web design community talking about? <a href="/author/anselm-hannemann/?rel=author">Anselm Hannemann</a> is collecting everything that popped up over the last week in his <a href="https://wdrl.info/">web development reading list</a> so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at. — Ed.</em>

Autumn is nearly over, winter is coming to Germany and on the weekend the forecast predicted the first snow for the Bavarian Alps which is near where I live. Time to read about Service Workers, and some abstract topics like teaching complex algorithms, and how to be more objective.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Recreating Theremin With JS And Web Audio API](https://www.smashingmagazine.com/2016/06/make-music-in-the-browser-with-a-web-audio-theremin/)
*   [Guidelines For Designing With Audio](https://www.smashingmagazine.com/2012/09/guidelines-for-designing-with-audio/)
*   [How To Increase Workflow And Reduce Stress With Nature Sounds](https://www.smashingmagazine.com/2015/10/increase-workflow-reduce-stress-with-nature-sounds/)
*   [<span class="headline">Spotify Playlists To Fuel Your Coding And Design Sessions</span>](https://www.smashingmagazine.com/2016/11/playlists-fuel-coding-design-sessions/)

<figure><a href="https://aerotwist.com/blog/the-cost-of-frameworks/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e10e375-33b1-4673-ae9a-e70532890d7e/time-to-interactive-opt1.jpg" width="500" height="375" /></a><figcaption><a href="https://aerotwist.com/blog/the-cost-of-frameworks/">The cost of Frameworks</a> explains what obvious and hidden costs using a framework incurs, and how to balance it against (or with) its advantages.</figcaption></figure>

{{% feature-panel %}}

## General

*   Paul Lewis’ “[The Cost of Frameworks](https://aerotwist.com/blog/the-cost-of-frameworks/)” analyzes the benefits and costs of frameworks but also takes developer's experience into account. This gives the article a perspective that’s often left out.</p>

## Concepts & Design

*   Looking at great products that have context-aware content, like Google Now, we realize that anticipatory design is not an easy thing to craft well. Often, less options are more and can provide a better result than too many features prominently displayed in an interface. Aaron Shapiro also shares why less choice can help our brain make better decisions and why the real innovation isn't about having the best idea but solving real problems.</p>

## Tools

*   [Mapzen](https://mapzen.com/) is an open source mapping lab that offers you great options to build software based on maps. For example, it gives you a client-side routing service or a real-time 3-D map rendering engine.
*   Sara Soueidan shares the best practices [how to build and export graphics as SVG](https://sarasoueidan.com/blog/svg-tips-for-designers/) in your favourite tool as a designer. These are simple tips that make SVGs much better and cleaner.</p>

## CSS / Sass

*   It always has been a pain to highlight text blocks line-by-line. With some hacks, we achieved some solutions but today we can use a much easier solution by [using `box-decoration-break: clone;` to decorate text lines](https://codepen.io/anon/pen/qOvqWy) with a custom background color (also check [zick-zack stripes with `box-decoration-break: clone`](https://codepen.io/df/pen/KdENZv?editors=110).

<figure><a href="https://codepen.io/df/pen/KdENZv?editors=110"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a635bad-c7f0-4777-9a41-78aac0451090/bonjour-optim.png" alt="Zick-zack line endings with CSS" width="500" height="360" /></a><figcaption><a href="https://codepen.io/df/pen/KdENZv?editors=110">Zick-zack line endings with CSS</a>, using <code>box-decoration-break: clone</code></figcaption></figure>

## Privacy

*   With [TLS 1.3 we get big improvements](https://timtaubert.de/blog/2015/11/more-privacy-less-latency-improved-handshakes-in-tls-13/) of the TLS protocol. It enhances privacy and has less latency due to improved handshakes. With it, forward secrecy will be the default and I can’t wait to see it established on the web.
*   With the growing usage of algorithms in our everyday lives, [we need to raise the question of ethics](https://cihr.eu/eoa2015web/). Our human brain can make irrational and emotional decisions. And sometimes that is a necessary and good thing. But algorithms and computers can’t. This being the biggest challenge for artificial intelligence, we need to face this fact for already existing mechanisms like the Facebook news feed collection, or hiring algorithms. A good way would be to make such algorithms transparent, to give users a possibility to improve them and to make them more objective.</p>

## Web Performance

*   We all know that performance matters, but Steve Souders’ new article shares practical insights in how to [measure real front-end performance](https://speedcurve.com/blog/user-timing-and-custom-metrics/) with the User Timing and Custom Metrics API. Learn how your blocking stylesheets, scripts, fonts or hero images are loaded.</p>

## HTML / SVG

*   Craig Hockenberry examines the new Safari 9 feature called "pinned tabs". While that is nothing new for Firefox and Chrome users, it looks and acts slightly different in Safari. But the article is entirely about [how to serve the best icon quality for pinned tabs](https://blog.iconfactory.com/2015/11/the-new-favicon/). Because a nice feature of Safari is that you can reference an SVG file and add a mask on top of it to dynamically style the icon. That could be handy if, for example, you wanted to indicate on which page the user is or to notify the user about dynamic changes. And certainly we want to have that feature in all browsers and for favicons as well.</p>

## Accessibility

*   Jennison Asuncion explains [why applications should never rely on swipe gestures entirely](https://www.linkedin.com/pulse/why-implementing-swipe-gestures-causes-mobile-issue-jennison-asuncion) and why it’s important to have a fallback. Assistive technologies (like VoiceOver) will simply overwrite your custom gestures.
*   Léonie Watson shares a list of easy [tricks to improve accessibility for SVGs](https://www.sitepoint.com/tips-accessible-svg/)

## JavaScript

*   The AngularConnect 2015 took place this month and there were some [notable announcements](https://angularjs.blogspot.hr/2015/11/highlights-from-angularconnect-2015.html) made of the framework: with ngUpgrade you now can seamlessly upgrade from Angular 1 to 2, Angular 2 is much faster due to better start-up times, server-side prerendering and other cool technologies.
*   Working with native DOM still seems to many people like a pain. But today, native JavaScript APIs for the DOM offer you a lot of tiny cool functions to select elements which you probably don’t know of. Louis Lazaris shares practical tips on how to [select children and siblings with native DOM methods](https://www.sitepoint.com/dom-tips-techniques-parent-child-siblings/)
*   [keycode.info](https://keycode.info/) is a little handy tool that returns the JavaScript keycode for a key you press.
*   Ian Feather reflects on [What Vanilla JS means today](https://ianfeather.co.uk/what-even-is-vanilla-js-these-days/) by going through examples like a “vanilla todoMVC implementation” that still makes use of tiny libraries and uses abstractions for DOM handlers.
*   David Walsh introduces Mozilla’s new “[Service Worker Cookbook](https://serviceworke.rs/)”, which is a great resource containing lots of useful Service Worker examples. In his blog post he also [shares the most common code examples](https://hacks.mozilla.org/2015/11/offline-service-workers/) to help you get started.</p>

## Go beyond…

*   These days, having GPS devices, smartphones, geo trackers, interactive maps and guides, we can’t get lost anymore. While for many of us this is a thing of joy, [Stephen Smith asks if we may be missing out](https://www.bbc.com/news/magazine-34473588). When I read that article, I immediately remembered about Vitaly Friedman [sharing a similar experience](https://www.smashingmagazine.com/smashing-newsletter-issue-147/) just a few days earlier. It’s interesting to see that we as human beings try to get some uncertainty back to our lives that are so predictable nowadays due to intelligent technology.
*   From time to time I think we should remember to not always think about money. It seems the happiest people in this world have found a way to [distance themselves from shopping addictions and unnecessary spending](https://elitedaily.stfi.re/news/world/people-spend-money-experiences-instead-things-much-happier/983208/?sf=vnldao). Because life is about memories, not diamonds.
*   When Mike Ellis left his job at Waterstone's Online, his boss told him that it’s okay and that “Leaving a job lets you literally and metaphorically clear your desk, an absolutely vital part of moving through your working life.”. Still today, this sentence was left in Mike’s mind and [he keeps thinking about it periodically](https://the-pastry-box-project.net/mike-ellis/2015-november-18). Just removing stuff, ruthlessly, with no remorse, no looking back, no what-if's can sometimes be the best way to clear one's life and mind.
*   There’s a part of today’s consumerist world that drives us to want more, buy more, act on our impulses, hoard, spend to solve our problems, create comfort through shopping, seek thrills through travel, do more, be more. What would happen if we broke from our addiction to wanting and buying more? Now, [I’m not saying we can free ourselves of all desire but we should try a little harder](https://zenhabits.net/wantnot/)

And this was it again for the current week. In case you like what I write here, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>

{{< signature "ah, vf, ms" >}}

