---
title: 'Web Development Reading List #104'
slug: web-development-list-104
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81e26f46-d400-4dc2-8f75-3429ccca49fe/think-outside-the-box.png
date: 2015-09-18T23:40:30.000Z
author: anselm-hannemann
description: >-
  _**What's happening in the industry?** What important techniques have emerged
  recently? What about new case studies, insights, techniques and tools? Our
  dear friend Anselm Hannemann is keeping track of everything in the [web
  development reading list](https://wdrl.info/), so you don't have to. The
  result is a carefully collected list of articles that popped up over the last
  week and which might interest you. — Ed._

  Hey, lovely to have you back here. It’s getting autumn here in Germany which
  means fog is back again and the trees are getting their lovely golden or red
  colors again. Time to spend the weekend out in the nature and take a deep
  breath, far away from your work. Just a few hours can help to get the
  refreshment you needed for days or a week already. And after that, start
  catching up with what I serve you in today’s list.
categories:
  - Web Development Reading List
---
<em><strong>What's happening in the industry?</strong> What important techniques have emerged recently? What about new case studies, insights, techniques and tools? Our dear friend <a href="https://www.smashingmagazine.com/author/anselm-hannemann/?rel=author">Anselm Hannemann</a> is keeping track of everything in the <a href="https://wdrl.info/">web development reading list</a> so you don't have to. The result is a carefully collected list of articles that popped up over the last week and which might interest you. — Ed.</em>

Hey, lovely to have you back here. It’s getting autumn here in Germany which means fog is back again and the trees are getting their lovely golden or red colors again. Time to spend the weekend out in the nature and take a deep breath, far away from your work. Just a few hours can help to get the refreshment you needed for days or a week already. And after that, start catching up with what I serve you in today’s list:

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)
*   [Introducing Responsive Web Typography With FlowType.JS](https://www.smashingmagazine.com/2013/09/introducing-flowtype-js/)
*   [Balancing Line Length And Font Size In RWD](https://www.smashingmagazine.com/2014/09/balancing-line-length-font-size-responsive-web-design/)
*   [A Case Study On Art-Directed Responsive Web Typography](https://www.smashingmagazine.com/2015/05/benton-modern-typography-case-study/)

## News

*   As iOS 9 is out since this week, there are a couple of new [things you can use now in iOS 9 Safari](https://www.mobilexweb.com/blog/ios9-safari-for-web-developers): Content Blockers arrived, Safari View Controller can be used instead of WKWebView, NavigationTiming API is back, Picture in Picture is available for iPad, proprietary Backdrop CSS filters, CSS Scroll Snapping and `@supports` is available, too.
*   Facebook announced that they built their first cross-platform React Native app. While iOS has been announced earlier this year, they now offer [React Native for Android](https://code.facebook.com/posts/1189117404435352/) as well.
*   If you want to try Service Worker from localhost or other insecure origins, you can start Chrome (starting in v44) [with the following flag](https://groups.google.com/a/chromium.org/d/msg/service-worker-discuss/C9LHhAcz7mw/fp4_lB8iRCYJ) via the command line: `./chrome --user-data-dir=/tmp/foo --unsafely-treat-insecure-origin-as-secure=https://your.insecure.host`. Of course you should use this only for development and don’t call other sites in this browser instance.
*   [Opera 32 is out](https://dev.opera.com/blog/opera-32/) and shares the news with Chromium 45: ES6 Arrow functions, further ES6 array and typed array functions are available now, `Object.assign()`, CSP Level 2 `self` rule is implemented and vibration notifications are now possible to trigger.
*   After nearly three years of development, [Modernizr 3 is out now](https://modernizr.com/news/modernizr-3-new-release-site). The new version is modular, has increased tests, no core test separation anymore and they also have new build steps to make it easier for you.</p>

## Concepts & Design

*   Forms are still hard to build. Especially when we need to ask for more than just the basics, a form can get messy and unusable due to clutter and a rubbish user interface. [Here are some tips to a better form UI](https://medium.com/@kubachrzecijanek/how-to-build-an-awesome-form-1e9b2c1bd00d).</p>

## Tools

*   Neocities tries to get back the platform that powered millions of websites in the early days of the web: Geocities. But they don’t want to do the same errors again, so they try to build it on an independent, redundant infrastructure. Now they shared [how they want to achieve their vision of the distributed web](https://blog.neocities.org/its-time-for-the-permanent-web.html). Baseline is to use [IPFS](https://ipfs.io/), a peer-to-peer hyper media protocol, with HTTP only as interim “fallback”.</p>

## Security

*   The recent Ashley Madison hack has shown [how to make your originally safe password hashing useless](https://cynosureprime.blogspot.de/2015/09/how-we-cracked-millions-of-ashley.html). Many passwords have been already decrypted that way and it again turns out that [most passwords are super simple and predictable](https://arstechnica.com/security/2015/09/new-stats-show-ashley-madison-passwords-are-just-as-weak-as-all-the-rest/). It shows that even if the passwords wouldn’t have been cracked, hackers could still run word-lists on the hashes and get access to the accounts easily. Always choose a strong password and use them only once.</p>

## Web Performance

*   James Avery, CEO of Adzerk, a big ad serving company, has published [an article](https://adexchanger.com/data-driven-thinking/ad-blocking-will-keep-growing-until-we-make-ads-better-2/) in which he shares the opinion of many users: People won’t stop using ad-blockers and privacy tools. And the ad industry will not stop ad-blockers. Instead the industry needs to stick to Do-Not-Track settings, needs to actively support privacy and stop making websites slow. It’s refreshing to read such encouragement and strong words against his own industry while others keep quiet or try to file lawsuits against ad-blockers.</p>

## HTML / SVG

*   Heydon Pickering explains [how to re-create the goodness of gifs in a vector format](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/) with SVG. A great source to dive deeper into animations and if you’re doing children books or playful graphical animations this is the resource to refer to.</p>

## Accessibility

*   In times where we inject animations on scroll, let elements fly in and make use of other playful animations on websites, we also need to think about users who get distracted or get ill by such “enhancements”. Val Head writes how you can really enhance your motion animated website with some [controllers that allow people to disable the animations](https://alistapart.com/article/designing-safer-web-animation-for-motion-sensitivity).

{{% feature-panel %}}

## JavaScript

*   [Jets.js](https://nexts.github.io/Jets.js/) is a live search/filter for your site that has great performance. Instead of handling class or style changes on each affected item, it uses dynamic inline CSS rules that are way faster when you have a lot of targets. A simple but great concept.
*   The series “[Let’s talk about the Web Animations API](https://danielcwilson.com/blog/2015/07/animations-intro/)” by Dan Wilson consists of five steps that introduce you to the new API, tell you what it is, how to use it, how to deal with timelines, player options, multiple animations, group or sequence effects, and motion paths.</p>

## CSS / Sass

*   While you probably used `currentColor` already, the way older `inherit` value gets ignored way too often. With “Back to the `:root`s”, simurai explains what is possible with CSS when you make effective use of the cascade and its specificity. And instead of trying to get rid of it you can use it in your components to be flexible and avoid maintenance work.
*   [Organizing CSS files can be quite challenging](https://thomasbyttebier.be/blog/less-css-mess). That is why so many people and especially larger teams choose techniques like BEM or ITCSS which help to stay organized with all the selectors being added over time in a project.</p>

## Work & Life

*   Seb Lester is a master calligrapher. [Jeff from Booooooom has talked to him](https://www.booooooom.com/2015/09/11/an-interview-with-master-calligrapher-seb-lester/) and asked him about calligraphy, his life and how to do great work by seeing client work as your own.

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81e26f46-d400-4dc2-8f75-3429ccca49fe/think-outside-the-box.png" alt="Think Outside The Box By Seb Lester" width="500" height="345" /><br>
<figcaption>Think outside the box by <a href="https://instagram.com/p/4RpJngzJ42/?taken-by=seblester">Seb Lester</a></figcaption></figure>

*   Jared Laham describes [the importance of doing real crafts to stay creative](https://dribbble.com/stories/2015/08/12/moonlighting) and how making knives helps him to be a better designer.
*   In the best work environments, we are better at what we do every day because we want it and our employers nurture the exploration. When interviewing job candidates, [you might not want to ask about strengths and weaknesses](https://the-pastry-box-project.net/dylan-wilbanks/2015-september-17) anymore but about the places that the candidate hasn’t explored, but wants to.</p>

## Go beyond…

*   The world wide fund for nature reports that a single generation of humans (ours) has [managed to wipe out nearly 50% of all world’s marine species](https://www.theage.com.au/environment/world-wide-fund-for-nature-says-nearly-half-the-worlds-marine-species-wiped-out-in-single-generation-20150915-gjn8o5.html). We finally need to recognize that this is reality and that for example the oceans will not at all be a healthy environment anymore without marine species living in there.
*   It’s nice to always have the latest gadget and I’m often not different here. We all like this but [what this means to our environment is quite awful](https://www.bbc.com/future/story/20150402-the-worst-place-on-earth?ocid=twfut). Maybe we should step back a bit and reconsider if we really need the newest gadget from Kickstarter (that we usually don’t use anyway). The article shows where the resources of our electronic devices are from and how the environment looks like over there.

By the way, I added Stripe as donation option now and you can <a href="https://wdrl.info/donate">support WDRL now easier than ever</a> with your favourite service!

And with that I’ll close for this week. Please share the list if you liked it and spread the word!

Thanks and all the best,

Anselm

<hr />

