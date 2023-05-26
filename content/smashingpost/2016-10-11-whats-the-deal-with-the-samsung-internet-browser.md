---
title: >-
  What’s The Deal With The Samsung Internet Browser? An Interview With Jungkee
  Song
slug: whats-the-deal-with-the-samsung-internet-browser
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fae00207-e5d4-4f3a-81c0-5055625af149/samsung-example-opt.jpg
date: 2016-10-11T20:05:08.000Z
author: peterpaulkoch
summary: >-
  Peter-Paul Koch was granted access to Samsung’s browser engineers a few weeks in advance of the rest of the world, and because he wanted to get a grip on the non-Google Chromium market and understand Samsung’s goals and ideas, he interviewed [Jungkee Song](https://twitter.com/jungkees) from the Samsung Internet team.
description: >-
  An interview with Jungkee Song from the Samsung Internet team about the new Chromium-based Samsung browser.
categories:
  - Mobile
  - Browsers
  - Interviews
  - Apps
---
<p>According to browser statistics, Chrome for Android <a href="https://gs.statcounter.com/#mobile_browser-ww-monthly-201510-201609">is currently</a> the largest mobile browser, or is <a href="https://www.akamai.com/us/en/solutions/intelligent-platform/visualizing-akamai/internet-observatory/internet-observatory-explore-data.jsp">about to become so</a>. Still, too few web developers realize that these Chrome for Android numbers in fact contain several browsers, not just Google Chrome. After discussing the general state of affairs in this article, we'll focus on the Chromium-based Samsung browser specifically.</p>

<p><strong>Immediate and full disclosure</strong>: <em>Samsung paid me to write this article. Still, it's one I've wanted to write for 18 months, so it kind of evens out.</em></p>

## The Plural Of Chromium Is Chromia

In the past few years, just about all Android device vendors have upgraded their default browsers to Chromium… but not to Google Chrome. Instead, they took an older Chromium version of their choice, modified it somewhat, and added it to their devices as "Internet" or "Browser."

To make matters more complicated, most vendors are contractually obliged to install Google Chrome on their devices as well. Thus, most modern Android devices come with two Chromium-based browsers installed — but web developers test only in Google Chrome and tend to forget about Samsung Chromium, and HTC Chromium, and LG Chromium, and all of the others. To me, this is not a desirable situation.

At their core, these Chromium-based browsers are the same. There are no huge incompatibilities in the rendering layer lying in wait to trap the unaware web developer. Still, there are a few differences in certain CSS, JavaScript and interface features that web developers need to know about. See, for instance, <a href="https://caniuse.com/#compare=chrome+55,samsung+4">Can I Use's comparison</a> of the Samsung browser and the latest Chrome.

I became interested in this topic <a href="https://www.quirksmode.org/blog/archives/2015/02/chrome_continue.html">back in early 2015</a>, and apart from attempting to notify other web developers that there are several Chromia — which is the proper, Latinate plural of Chromium (my classical education <em>will</em> show from time to time) — and being met with total disinterest, I tried to find some solid numbers on how many people exactly are using a non-Google Chrome for Android.</p>

{{% feature-panel %}}

## Market Shares

Mobile browser market shares, unfortunately, are hard to obtain. Until this year, no public source has made any distinction between Google Chrome and the vendor-specific Chromia. On the other hand, the use of non-Google Chromia is clearly bound to device market share, and seeing that Samsung is by far the largest Android vendor, with <a href="https://communities-dominate.blogs.com/brands/2016/03/smartphone-wars-full-year-2015-final-top-10-by-brands-top-5-by-os-installed-base-dec-2015-and-q4-dat.html">about 37% market share</a>, the conclusion that the Samsung Chromium browser would be the largest of the non-Google ones was fairly obvious from the start.

Samsung Internet (which is the official, and quite boring, name of the Samsung Chromium browser) has about 400 million active users globally (source: the interview below). For comparison, Google Chrome for Android has <a href="https://thenextweb.com/insider/2016/04/21/google-just-hit-billion-monthly-active-chrome-users/">about 1 billion</a>.

But what percentage of Samsung device owners actually use Samsung Internet? The Google Chrome number spans all device types and is not directly comparable with the Samsung number, which is limited to Samsung devices. <a href="https://www.quirksmode.org/blog/archives/2015/02/counting_chromi.html">Research I did last year</a> suggests that about 65% of Samsung users use Samsung Internet — although these numbers are based on one day of statistics from a Dutch ad agency, so they should be taken with a grain of salt. Still, I'm willing to believe that a majority of Samsung device owners use Samsung Internet and not Google Chrome, which by default is hidden in the apps menu.

The reasons I believe so are illustrated by a hilarious encounter I had recently. I was speaking with a woman who is not involved in web development at all, and asked her which mobile browser she uses. "Internet Explorer," she said. "Oh," I replied, "so you have a Windows Phone?" "No," she said, "a Galaxy S7." And she pointed at the Samsung Internet icon, which clearly states "Internet." She was quite surprised to hear it was not Internet Explorer, and that Google Chrome was also installed on her device, although my attempt at explaining the relationship between all of these browsers failed miserably. (Then again, even some web developers don't get that bit.)

Anecdote, not data, yaddah yaddah, but I think this story highlights the point of view of consumers, and the reason why many will use Samsung Internet: They don't know they have a choice and are confused anyway. Also, it shows that Samsung should find a better name for its browser.

Back to stats. In January, StatCounter <a href="https://gs.statcounter.com/#mobile_browser-ww-monthly-201510-201609">started to count</a> Samsung Internet separately from the other Chromia, which allows us to conclude that Samsung Internet has a global market share of about 7%, while all other Chromia on Android combined, including Google's, sit on about 37%. Locally this market share may be higher; for instance in <a href="https://gs.statcounter.com/#mobile_browser-DE-monthly-201510-201609">Germany</a>, where it's 18%.

I wonder if 18%, or even 7%, of web developers bother to test in Samsung Internet as a browser distinct from Google Chrome. And for close to a year now, I've been debating about what to do about this state of affairs, particularly in light of the refusal of Asian companies to speak with web developers. (Believe me, I tried for seven years, and it wasn't fun.)

{{% ad-panel-leaderboard %}}

## Opening Up

Then, at the start of 2016, things changed. Samsung opened up and now wants to reach out and become a web citizen in good standing — and become a major player on the web. (Some major web players have less mobile market share than Samsung does, so I'm fundamentally sympathetic to this desire.)

This is good news for web developers: Any time a browser vendor opens up, the web becomes a touch more diverse, and, more importantly, we get one more browser vendor to send snarky comments to. What's not to like?

In fact, it turns out Samsung is taking this process of opening up very seriously indeed. It created a London-based developer relations group (<a href="https://twitter.com/samsunginternet">@samsunginternet</a> on Twitter) — among others, consisting of <a href="https://ada.is/">Ada Rose Edwards</a> of Financial Times fame — and a <a href="https://Medium.com/samsung-internet-dev/">Medium channel</a>. Also, if you want to get in touch directly with Samsung browser engineers, you can email them at browser[AT]samsung[DOT]com — but please remember to be polite and patient, as you would like other people to behave towards you.</p>

## Interview

Because I was granted access to Samsung's browser engineers a few weeks in advance of the rest of the world, and because I want to get a grip on the non-Google Chromium market and understand Samsung's goals and ideas, I interviewed <a href="https://twitter.com/jungkees">Jungkee Song</a> of the Samsung Internet team.

**Peter-Paul:** Hello, Jungkee. Could you briefly introduce yourself?

<strong>Jungkee:</strong> Hello. I'm a software engineer on the Samsung Internet team, working on the web platform and web standards. I'm one of the co-editors of the <a href="https://www.w3.org/TR/service-workers/">service workers spec</a> (along with Google's Alex Russell and Jake Archibald) and a Chromium contributor. Also, I'm trying to meet web developers as often as I can in order to evangelize and discuss progressive web app technologies — and our browser, of course.

**Peter-Paul:** Why did Samsung decide to create its own browser, instead of using Google Chrome?

<strong>Jungkee:</strong> First, Samsung aims to deliver a good mobile web experience to users based on device features such as bio sensors, payments and VR. We would like to bring such device technologies to the web, and we found the best way to do that is by creating our own browser.

Secondly, the web is a neutral platform, and no single browser vendor can make the web a better place alone. Diversity of and competition between browsers is a fundamental part of the web. Samsung intends to be one of the players that extend the open web as a common platform — thus, our involvement with service workers, progressive web apps, web and VR integration, and other web innovations.

Thirdly, Samsung provides many types of devices, including, but not limited to, smartphones, tablets, Gear VR, Gear Watch, smart TVs and home appliances. The web should be present on all such devices, which, again, requires us to create our own browser.

**Peter-Paul:** Can you give some examples of changes Samsung made to the default Chromium browser?

<strong>Jungkee:</strong> Most have to do with Samsung-specific hardware. Samsung Internet supports a <a href="https://developer.samsung.com/technical-doc/view.do?v=T000000202">secret mode</a> that uses the biometric sensor in Galaxy devices. We also allow users to use third-party plugins for content blocking. Another example is our Gear VR integration, which requires the WebVR API and seamless interaction between the phone browser and the Gear VR browser.

**Peter-Paul:** Have you ever considered using an engine other than Chromium?

<strong>Jungkee:</strong> Yes. When we started, we examined WebKit, Gecko and Blink. We found all of them have their pros and cons, but we selected the one that adopts the latest web features fastest, is well maintained, and has a huge developer community: the Chromium project.

It was around early 2013 when we made that decision. We shipped our first Chromium-based browser in one of the Galaxy S4 models released later in 2013.

**Peter-Paul:** How do you decide which Chromium version you're going to use?

<strong>Jungkee:</strong> This question has no easy answer. We try to balance adoption of the latest features with the stability of our software and our internal deadlines. Although we'd love to bring out new features as fast as possible, our products have to go through a rigorous QA process, and therefore we don't always work with the latest version.

Still, from time to time we cherry-pick important new features that were released in a later Chromium version than the one we use for our base branch. For example, Samsung Internet 4.0 is based on Chromium 44 but supports service worker features up to around Chromium 48. Also, we always backport major security patches to our browser.

{{% ad-panel-leaderboard %}}

**Peter-Paul:** Do you also work on the core Chromium project?

<strong>Jungkee:</strong> Certainly! Currently we have 2 owners and around 20 committers. We are mainly working on features that we think are important to extend the web. For instance, we have contributed a number of patches to the service workers API, the notification API, payments, canvas 2D and so on.

Standards we currently focus on include web payment, web VR and progressive web apps. We would like a chance to take on work on those, but right now we concentrate on core features that improve the user experience.

**Peter-Paul:** On how many device types does Samsung Internet run?

<strong>Jungkee:</strong> Samsung Internet 4.0 runs on <a href="https://developer.samsung.com/internet/android/releases">these Samsung devices</a>; and please note they're all high-end or mid-range smartphones. That's because of the speed and memory we need to run Samsung Internet: 768 MB of RAM and 1 GHz dual core of CPU clock. There are no differences between the Samsung Internet versions running on different devices.

Samsung Internet 4.0 also runs on the Samsung Gear VR devices, as well as on Android tablets, but there we don't support automatic updates yet. Also, Tizen 3.0, the OS for Samsung TVs, will come with Samsung Internet. It's possible our browser will also come to Gear Watch, but we have no concrete plans yet.

**Peter-Paul:** And how many users does it have?

<strong>Jungkee:</strong> We estimate Samsung Internet has about 400 milion global monthly active users.

**Peter-Paul:** Seeing that Samsung Internet is now an evergreen browser, how often do you think you're going to update it?

<strong>Jungkee:</strong> We provide two types of software updates: the update through OS and firmware updates, as all device vendors do, and updates through the app market, as Google, Mozilla and Opera do. We aim to provide updates twice a year through either Galaxy Apps or Play Store, but we are still working on the process. Nonetheless, we successfully deployed Samsung Internet 4.0 back in February, so we're starting to get somewhere.

**Peter-Paul:** Any chance of a beta channel?

<strong>Jungkee:</strong> We don't have any concrete plans for a beta channel yet, even though Samsung Internet 4.0 was available as a closed beta.

**Peter-Paul:** Do you plan to eventually ship the latest Samsung Internet version on all Samsung Android devices?

<strong>Jungkee:</strong> Ideally, yes. However, we ship so many different devices that the version upgrade will be provided in several ways: shipping in a new device, firmware updates (for example, with OS upgrades) and market updates.

**Peter-Paul:** Will we see Samsung Internet on non-Samsung devices?

<strong>Jungkee:</strong> We have no concrete plans at this time. Right now, we concentrate on our Galaxy smartphones, tablets and Gear VR, and after that on Tizen and Gear Watch. Once we've done that, we may start planning for a version for non-Samsung devices.

**Peter-Paul:** Apart from Samsung Internet, does Samsung create and maintain any other browsers for low-end devices?

<strong>Jungkee:</strong> We shipped some low-end Tizen devices that have a WebKit-based browser, but, as I said, we plan to ship a Chromium-based browser for Tizen 3.0.

**Peter-Paul:** In addition to Samsung Internet, Samsung devices also come with Google Chrome preinstalled. Why is that?

<strong>Jungkee:</strong> Choice is a good thing. We think users should be able to choose which browser they use to access the web. We think Samsung Internet brings some distinct advantages for Samsung device users that make the web more useful, but we don't feel we have to restrict the browsers on Samsung devices in order to artificially lock users into using our browser. Our growing market share numbers bear this out.

**Peter-Paul:** Thank you for your time.

<strong>Jungkee:</strong> You're welcome. And remember, if your readers have any questions for Samsung, they can use one of the following contact options:

*   Send an email to browser[AT]samsung[DOT]com.
*   Our newly-formed developer relations team in London has a Twitter account, [@samsunginternet](https://twitter.com/samsunginternet), and is posting articles on our [Medium channel](https://Medium.com/samsung-internet-dev/).
*   We're also monitoring [Stack Overflow](https://stackoverflow.com/) for Samsung Internet-related questions, so you can always ask there.

We are planning to open a forum or more channels to communicate with web developers, so stay tuned for our next move.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [The (Not So) Secret Powers Of The Mobile Browser](https://www.smashingmagazine.com/2016/12/the-not-so-secret-powers-of-the-mobile-browser/)
*   [The Mobile Web Handbook](https://shop.smashingmagazine.com/products/mobile-web-handbook)

{{< signature "vf, al, il" >}}