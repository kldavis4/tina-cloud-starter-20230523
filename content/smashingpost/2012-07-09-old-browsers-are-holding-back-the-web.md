---
title: Old Browsers Are Holding Back The Web
slug: old-browsers-are-holding-back-the-web
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/011425a1-4ef9-40c1-be4e-877253295ea8/iestats.jpg
date: 2012-07-09T23:51:53.000Z
author: louis-lazaris
description: >-
  Because of how far certain Web technologies like HTML5 and CSS3 have brought
  us, many would say that—from a Web platform perspective—the future is _now_.
  Sounds like a cliché, I know. At the very least, it feels like the future is
  starting to bubble up to the surface... but it's just not quite there yet.
categories:
  - Web Design
  - Browsers
  - Internet Explorer
---
Because of how far certain Web technologies like HTML5 and CSS3 have brought us, many would say that—from a Web platform perspective—the future is <em>now</em>. Sounds like a cliché, I know. At the very least, it feels like the future is starting to bubble up to the surface... but it's just not quite there yet.

When we use new DOM features, HTML5 APIs and the latest in CSS3, the possibilities that open up are astounding. These new technologies help us easily build Web applications with less reliance on hacks, plugins, images, and bloated scripts. This makes life easier not only for Web developers (for both building and maintaining these projects) but also for the end user who gets a faster and stronger overall experience.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [15 Impressive Alternative Browsers](https://www.smashingmagazine.com/2015/09/chrome-firefox-safari-opera-edge-impressive-web-browser-alternatives/)
*   [Dear Web User: Please Upgrade Your Browser](https://www.smashingmagazine.com/2012/07/dear-web-user-please-upgrade-your-browser/)
*   [Review Of Cross-Browser Testing Tools](https://www.smashingmagazine.com/2011/08/a-dozen-cross-browser-testing-tools/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)

But there is a huge road block preventing our "future" from truly becoming the now. What is this roadblock? It's <strong>old browsers</strong>. Let's delve into this topic a little bit so we can see why this is a problem and what we can do to help it.

{{% feature-panel %}}

## Internet Explorer's Usage Share

<a href="https://gs.statcounter.com/#mobile_vs_desktop-ww-monthly-201204-201204-bar">According to StatCounter estimates</a>, even with the recent mobile explosion, desktop usage still trumps mobile by a large margin. 90% of internet activity worldwide occurs on the desktop. Granted, some reports have mobile shares higher than the current 10% shown by StatCounter. Whatever the case is, the fact remains that a lot of people are accessing our websites and Web apps by using a desktop browser.

Which desktop browsers? Well, let's look at StatCounter's usage share for <a href="https://gs.statcounter.com/#browser_version-ww-monthly-201205-201205-bar">desktop browsers for May 2012</a>, with a specific focus on Internet Explorer:

<a href="https://gs.statcounter.com/#browser_version-ww-monthly-201205-201205-bar"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/011425a1-4ef9-40c1-be4e-877253295ea8/iestats.jpg" alt="Stats for desktop browsers in May 2012" width="500" height="380" /></a>

As shown above—to the joy of developers everywhere—worldwide stats for versions of Internet Explorer prior to IE8 are very low. IE6 is so low that it's not even showing up in some of StatCounter's charts anymore. If you find similar stats for your own projects, then, depending on the overall traffic numbers, you may be able to drop support for IE6 and IE7 and start using a number of features that those browsers don't support. But what about IE8 and IE9?

As you can see from the image and link above, worldwide usage for IE8 and IE9 is just about 30%, combined. But that might not be the full story. Compare those numbers to the ones taken from two other websites.

First, <a href="https://marketshare.hitslink.com/browser-market-share.aspx?qprid=2&amp;qpcustomd=0&amp;qptimeframe=M">Net Applications, from April of this year</a>:

<a href="https://marketshare.hitslink.com/browser-market-share.aspx?qprid=2&amp;qpcustomd=0&amp;qptimeframe=M"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c896b04-d8d3-4b26-954c-8029f1487cab/na-stats.jpg" alt="Net Applications browser stats" width="500" height="181" /></a>

Their stats show a whopping 38% of users still on IE6-8, with more than two thirds of those on IE8. In addition, IE9 holds another 16% share. That's more than 50% of users on IE6-9.

Now look at <a href="https://www.statowl.com/web_browser_usage_by_version.php?1=1&amp;timeframe=last_6&amp;interval=month&amp;chart_id=4&amp;fltr_br=&amp;fltr_os=&amp;fltr_se=&amp;fltr_cn=&amp;limit%5B%5D=ie&amp;limit%5B%5D=firefox&amp;limit%5B%5D=safari&amp;limit%5B%5D=chrome&amp;limit%5B%5D=opera&amp;limit%5B%5D=netscape&amp;timeframe=last_month">StatOwl's April 2012 report</a>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf353f5e-d755-4da2-a0bd-15acb3acbc2c/ie-large-view.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f907cb0-9da7-4381-bad8-3c1498df9554/ie-small-view.png" alt="StatOwl browser stats" width="500" height="303" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf353f5e-d755-4da2-a0bd-15acb3acbc2c/ie-large-view.png">Large preview</a>.</em>

Like Net Applications, StatOwl places IE8's and IE9's shares significantly higher than StatCounter's—this time about 20% for each. Combined with the 8% on IE6 and IE7, that's almost 50% on IE.

The debate about why these different browser usage stats are showing higher numbers for IE6-9 is something that's been in industry news of late. These details are certainly beyond the scope of this article, but you can check out the links below for more info:

*   Understanding Browser Usage Share Data (Windows Team Blog)
*   [Microsoft says Chrome didn't top Internet Explorer last weekend](https://blogs.computerworld.com/19925/microsoft_says_chrome_didnt_top_internet_explorer_last_weekend) (Computerworld Blogs)
*   [StatCounter to Microsoft: You're wrong, Chrome beat Internet Explorer last weekend](https://blogs.computerworld.com/19927/statcounter_to_microsoft_youre_wrong_chrome_beat_internet_explorer_last_weekend) (Computerworld Blogs)

## Why Does This Discussion Include IE9?

IE9 is a huge step forward from previous versions of Internet Explorer. But it's over a year old, and does not auto-update like other popular browsers do.

Thus, although IE9 is a much more stable and feature-rich browser, it's already starting to show its age. With each passing month, browsers like Chrome and Firefox continue to roll out new features automatically, and IE9 gets closer to becoming obsolete.</p>

## Why Is The Old Browser Problem Such A Big Deal?

Some people might be thinking "What's the big deal? Use progressive enhancement and you'll just give old browsers a lesser experience and the users <a href="https://24ways.org/2009/ignorance-is-bliss">won't know what they're missing</a>”. This might be true with certain CSS3 and HTML5 features for which it's easy to provide fallbacks and even some lightweight polyfills. But other more complex features are not that simple.

Let's first take a look at IE8. To give you an idea of how many features IE8 lacks, here's a list of what you gain as a developer when you stop supporting IE8:

*   Media Queries
*   `opacity` (without IE filters)
*   `border-radius`
*   `box-shadow`
*   RGBA, HSL/HSLA colors
*   HTML5 elements (that don't need the html5shiv)
*   Data URLs
*   `getElementsByClassName`
*   CSS Transforms
*   `<canvas>`
*   Cross­origin Resource Sharing
*   Lots of CSS3 selectors (:nth-child(), :target, :enabled, etc)
*   `matchesSelector`
*   Navigation Timing API (`performance.timing`)
*   Multiple backgrounds
*   `background-clip`, `background-origin`, `background-size`
*   Real HTML5 Video/Audio with no messy fallbacks
*   WOFF Fonts
*   SVG images, inline SVG, SVG in CSS backgrounds
*   Geolocation
*   Server ­Sent Events

Also, this list doesn't take into consideration the number of bugs and performance problems that occur in IE8. So when you consider all of the features above, along with bugs and performance issues, a high number of users still on IE8 becomes a major roadblock to progress on the Web.

Of course, this is not to say that support for these features is perfect in new browsers. Many of these features are still in flux in the spec. But a very high percentage of in-use browsers outside of IE8 have pretty good support for everything listed above.</p>

### What About IE9?

The problem, however, doesn't end with IE8. As mentioned, IE9 is likewise starting to fall behind the other browsers. Here's a list of the features you gain if you don't have to support IE9:

*   `text-shadow`
*   Linear and Radial Gradients
*   CSS Transitions
*   Keyframe Animations
*   Web Sockets
*   3D Transforms
*   flexbox layout
*   Multiple Columns
*   The `<datalist>` element
*   SVG Filters
*   Application Cache
*   `pushState`, `replaceState`
*   indexedDB
*   ECMAScript 5 Strict Mode
*   FileReader API
*   `requestAnimationFrame`
*   The `async` attribute for `<script>` elements
*   Many HTML5 form features
*   Native form validation
*   The `<progress>` element
*   Web Workers
*   XMLHttpRequestLevel 2
*   Typed Arrays
*   matchMedia
*   Blob URLs

As you can see from the two lists above, the old browser problem is a significant one. These new features (although still in progress) have the potential to help designers and developers innovate and push the Web forward in amazing ways.

## Is IE[x] The New IE6?

The notion that "IE[x] is the new IE6" has been <a href="https://infrequently.org/2010/10/ie-8-is-the-new-ie-6/">discussed</a> <a href="https://paulirish.com/2011/browser-market-pollution-iex-is-the-new-ie6/">before</a>, but it deserves more attention here. As of writing this, IE9 (the latest stable version of Internet Explorer), <a href="https://answers.microsoft.com/en-us/ie/forum/ie9-windows_other/ie9-for-xp-why-doesnt-internet-explorer-9-work-on/e8113f20-b149-4763-b4d4-562d1da524b6"> cannot be installed on Windows XP</a> and, <a href="https://gs.statcounter.com/#os-ww-monthly-201205-201205-bar">according to StatCounter</a>, about 31% of desktop internet usage is on that operating system.

Since a large number of IE8 users are essentially "trapped" in XP, there is no hope that those users are going to upgrade to a newer version of Internet Explorer unless they upgrade their OS.

For your own projects, I hope the stats for older browsers are much better. After all, the only stats that really matter <a href="https://css-tricks.com/the-stats-that-matter-your-sites-stats/">are your own</a>. Also, the worldwide stats showing high numbers for IE6-8 are probably a little skewed by some <a href="https://gs.statcounter.com/?PHPSESSID=40nvmolpmg8d460oc4mf66c5g0#browser_version-CN-monthly-201205-201205-bar">densely populated geographic areas</a>. Nonetheless, usage stats for IE6-9 are still a factor for many projects and may thus be holding back a lot of developers (due to client or corporate pressure) from using many new features.

The point here is that if the usage stats for browsers like IE8 and IE9 linger for anywhere nearly as long as IE6 did, then those of us who are building websites and Web apps for a larger and more diverse audience could be in for a long wait (before using dozens of new features).

<img title="IE" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e4d9b44-1c32-4f35-aeb7-53883dc973c6/ie.jpg" alt="IE" width="500" height="441" /><br>
<em>Usage stats for IE6–9 are still a factor for many projects and may thus be holding back a lot of developers.</em>

## Microsoft Provides A Glimmer Of Hope—Or Do They?

One positive development in this area is the recent announcement by Microsoft that XP, Vista, and Windows 7 users will be automatically upgraded to the latest version of Internet Explorer available for their operating system.

Unfortunately, while this news is better than nothing, it is not the ideal solution. A <a href="https://www.infoworld.com/t/applications/microsoft-warns-businesses-impending-autoupdate-ie7-628">similar announcement</a> was made back in 2008 regarding a so-called "auto-update" from IE6 to IE7. That 2008 update would only take place if a system was set to auto-approve Update Rollup packages. But a default setting in XP prevents this from happening—so this barely made a ripple in the IE6 problem at that time (as seen from the fact that <a href="https://gs.statcounter.com/#browser_version-ww-monthly-200901-200901-bar">IE6 usage was at 23% in January of 2009)</a>.

Similarly, this time around, users will be upgraded to a newer version of Internet Explorer only if they have turned on automatic updating via Windows Update. Also, the auto-update began in January and only for users in certain geographic regions. So again, although this is certainly good news, it's not the ideal solution.</p>

## What Real Options Are There For Users Of Older Browsers?

Aside from people that are on systems that, for security or compatibility reasons, cannot upgrade their browsers, everyone that is using IE8 (or lower) has one of two options to help alleviate this problem—even if they're on Windows XP. They are:

*   [Don't use Internet Explorer](https://browsingbetter.com/); unlike IE9, all the latest versions of the other major browsers (Chrome, Firefox, Safari, and Opera) will run on Windows XP or later.
*   Install Chrome Frame; it's easy to install and it makes IE function like Google Chrome.

With those two options there is no excuse for the high numbers of users still on older versions of Internet Explorer. Theoretically, everyone who is not on a locked-down system can upgrade to a non-IE browser or install Chrome Frame. This would likely bring the usage shares for older browsers down to a bare minimum, and would allow developers to bring even more of the latest technologies into common use.</p>

### A Note on Tracking IE with Chrome Frame

Some of the users still on old versions of Internet Explorer could have Chrome Frame installed, but in the browser usage stats referred to earlier in this post, those are still counted as Internet Explorer. It would be good to see Chrome Frame stats reflected in those applications.

Google Analytics, however, does include "IE with Chrome Frame" as a separate browser, and developers can check out the Chrome Frame developer documentation for info on how to detect Chrome Frame usage.</p>

## What Else Can We Do To Help?

If you have any friends or colleagues using an older version of Internet Explorer (or any old browser), help them upgrade to the latest version of Chrome, Firefox, Safari, or Opera. You might even want to show them a CSS3-rich or HTML5-rich website in a modern browser and compare it to IE8.

In other words, prove to them that their browser is an out-of-date, unstable, slow piece of software. You might even <a href="https://www.webdesignerdepot.com/2011/05/how-do-you-convince-the-average-web-user-to-switch-to-a-non-ie-browser/">have a little fun</a> trying to show them why non-IE browsers are better.</p>

### Display a Message to Users on Old Browsers

Another thing you can do is display a message to users if they're visiting your website in an older browser like IE8. Don't assume this is too intrusive. A couple of years ago, YouTube started <a href="https://support.google.com/youtube/bin/answer.py?hl=en&amp;answer=175292">phasing out support for many older browsers</a>. The message shown below is now displayed to users visiting the website with IE6:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/919d5384-98fa-4a06-9cc2-3b08eaa7da92/youtube-message.jpg" alt="YouTube's message for IE6 users" width="500" height="478" />

You could display a subtle yet noticeable message to encourage users to install Chrome Frame and make sure to include <a href="https://www.chromium.org/developers/how-tos/chrome-frame-getting-started#TOC-Making-Your-Pages-Work-With-Google-Chrome-Frame">the necessary code</a> that will enable Chrome Frame on pages that are being viewed with it. [<em>However, also provide an option to close the message bar so that users who are stuck in a locked-down system (and have to use your website) can actually use it. —Editorial</em>]

## Tomorrow: A Message For Non-Developers

Most people reading this article are probably thinking "Yeah, that's all fine and good, but you're preaching to the choir, dude." Many developers already know a lot of this stuff. And we also know that developers and designers are not the ones using older browsers like IE8 for everyday browsing. In fact, you'd be hard-pressed to find a Web developer that uses IE9.

That's why tomorrow Smashing Magazine will be publishing a special post (the article <a href="https://www.smashingmagazine.com/2012/07/10/dear-web-user-please-upgrade-your-browser/">is published now</a>) that will be targeted towards users who are not designers or developers, and who are not very tech savvy. We encourage everyone to share that article with as many people as possible so we can do everything we can to get the usage stats for old browsers as low as possible.

{{< signature "jvb" >}}

