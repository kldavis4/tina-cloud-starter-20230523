---
title: 'The State Of Mobile And Why Mobile Web Testing Matters'
slug: mobile-app-web-testing
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955732b9-9205-4369-bd21-ff57443d9d3a/mobile-test-example.png
date: 2021-03-02T16:30:00.000Z
summary: >-
  With mobile traffic accounting for over 50% of web traffic these days, leaving your mobile performance unoptimized isn’t really an option. In this article, we’ll discuss the complexity and challenges of mobile, and how mobile testing tools can help us with just that.
description: >-
  With mobile traffic accounting for over 50% of web traffic these days, leaving your mobile performance unoptimized isn’t really an option. In this article, we’ll discuss the complexity and challenges of mobile, and how mobile testing tools can help us with just that.
categories:
  - Apps
  - Mobile
  - Performance
  - Testing
  - Debugging
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Lambda
  link: https://www.lambdatest.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e4e2e6-fe71-4148-83d1-7bc76be21465/lambdatest-logo.svg
  width: 131
  height: 52
  description: >-
    This article has been sponsored by our dear friends at <a href="https://www.lambdatest.com/">LambdaTest</a> who are making the cross-browser testing experience smoother for so many folks around the globe. <em>Thank you!</em>
---

Things have changed quite a bit over the last decade when we just started exploring what we could do on a tiny, shiny mobile screen. These days, with mobile traffic accounting for [over 50% of web traffic](https://www.statista.com/statistics/277125/share-of-website-traffic-coming-from-mobile-devices/#:~:text=Mobile%20accounts%20for%20approximately%20half,since%20the%20beginning%20of%202017.), it’s fair to assume that the very first encounter of your prospect customers with your brand will happen on a mobile device.

Depending on the nature of your product, the share of your mobile traffic will vary significantly, but you will certainly have *some* mobile traffic — and being prepared for it can make or break the deal. This requires your website or application to be **heavily optimized for mobile**. This optimization is quite complex in nature though. Obviously, our experiences will be responsive &mdash; and we’ve learned how to do so well over the years — but it also has to be accessible and fast.

This goes way beyond basic optimizations such as color contrast and server response times. In the fragmented mobile landscape, our experiences have to be adjusted for [low data mode](https://twitter.com/colinbendell/status/1265675813204172810), [low memory, battery and CPU](https://umaar.com/dev-tips/242-considerate-javascript/), [reduced motion](https://css-tricks.com/introduction-reduced-motion-media-query/), [dark and light mode](https://css-tricks.com/a-complete-guide-to-dark-mode-on-the-web/) and so many other conditions.

Leaving these conditions out of the equation means **abandoning prospect customers** for good, and so we seek compromises to deliver a great experience within tight deadlines. And to ensure the quality of a product, we always need to test — on a number of devices, and in a number of conditions.

## State Of Mobile 2021

While many of us, designers and developers, are likely to have a relatively new mobile phone in our pockets, a vast majority of our customers isn’t quite like us. That might come a little bit unexpected. After all, when we look at our analytics, we will hardly find any customers browsing our sites or apps with a **mid-range device on a flaky 3G connection**.

The gotcha here is that, if your mobile experience isn’t optimized for various devices and network conditions, these customers will never appear in your analytics — just because your website or app will be barely usable on their devices, and so they are unlikely to return.

In the US and the UK, [Comscore’s Global State of Mobile 2020 report](https://www.comscore.com/Insights/Presentations-and-Whitepapers/2020/Global-State-of-Mobile) discovered in August 2020, that mobile usage accounted to 79% and 81% of total digital minutes respectively. Also, there was a 65% increase in video consumption on mobile devices in 2020. While a vast majority of the time is spent in just a few mobile apps, social media platforms provide a gateway to the web and your services &mdash; especially in education.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3077327c-a09e-4245-89f7-a263f1c5f45b/comscore-insights.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3077327c-a09e-4245-89f7-a263f1c5f45b/comscore-insights.png" width="800" height="450" sizes="100vw" caption="Globally, time spent on mobile continues to rise around the world, according to <a href='https://www.comscore.com/Insights/Presentations-and-Whitepapers/2020/Global-State-of-Mobile'>ComScore Global State of Mobile 2020 report</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3077327c-a09e-4245-89f7-a263f1c5f45b/comscore-insights.png'>Large preview</a>)" alt="Globally, time spent on mobile continues to rise around the world." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23363233-b86b-4a8f-adfa-0b7619ec48b1/comscore-insights-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23363233-b86b-4a8f-adfa-0b7619ec48b1/comscore-insights-2.png" width="800" height="450" sizes="100vw" caption="Some app categories skew toward mobile-only usage, while others (education, for example) see more desktop usage. <a href='https://www.comscore.com/Insights/Presentations-and-Whitepapers/2020/Global-State-of-Mobile'>ComScore Global State of Mobile 2020 report</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23363233-b86b-4a8f-adfa-0b7619ec48b1/comscore-insights-2.png'>Large preview</a>)" alt="Some app categories skew toward mobile-only usage, while others (education, for example) see more desktop usage." >}}

On the other hand, while devices do get better over time in terms of their capabilities and battery life, older devices don’t really get abandoned or disappear into the void. It’s not uncommon to see customers using devices that are 5-6 years old as these devices often [get passed through the generations](https://youtu.be/JvJ0v5OohNg?t=1477), serving as slightly older but "good enough" devices for simple, day-to-day tasks. In fact, an average consumer [upgrades their phone every 2 years](https://www.cnbc.com/2019/05/17/smartphone-users-are-waiting-longer-before-upgrading-heres-why.html), and in the US [phone replacement cycle is 33 months](https://www.mobileworldlive.com/devices/news-devices/us-phone-upgrade-cycle-stretches-to-33-months/).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1568df99-ec30-4402-a805-883bf4556635/tim-kadlec-android-devices.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1568df99-ec30-4402-a805-883bf4556635/tim-kadlec-android-devices.png" width="800" height="446" sizes="100vw" caption="What’s a representative device to test on in 2021? According to <a href='https://youtu.be/JvJ0v5OohNg?t=1477'>Tim Kadlec</a> (video), that’s an Android device that’s couple of years old, and costs around $200. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1568df99-ec30-4402-a805-883bf4556635/tim-kadlec-android-devices.png'>Large preview</a>)" alt="What’s a representative device to test on in 2021? An Android device that’s couple of years old, and costs around $200." >}}

Globally in 2020, [84.8% of all shipped mobile phones are Android devices](https://www.idc.com/promo/smartphone-market-share/os), according to the International Data Corporation (*IDC*). Average bestselling phones around the world cost just under $200. A representative device, then, is an Android device that is **at least 24 months old**, costing $200 or less, running on slow 3G, 400ms RTT and 400kbps transfer, just to be slightly more pessimistic.

This might be very different for your company, of course, but that’s a close enough approximation of a majority of customers out there. In fact, it might be a good idea to look into current [Amazon Best Sellers](https://www.amazon.co.uk/gp/bestsellers/electronics/356496011/ref=sr_bs_1) for your target market.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1436a0fc-40ed-4665-8fbb-bae8aa1ad740/amazon-bestsellers-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1436a0fc-40ed-4665-8fbb-bae8aa1ad740/amazon-bestsellers-opt.png" width="800" height="633" sizes="100vw" caption="When building a new site or app, always check current <a href='https://www.amazon.co.uk/gp/bestsellers/electronics/356496011/ref=sr_bs_1'>Amazon Best Sellers</a> for your target market first. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1436a0fc-40ed-4665-8fbb-bae8aa1ad740/amazon-bestsellers-opt.png'>Large preview</a>)" alt="When building a new site or app, always check current Amazon Best Sellers for your target market first" >}}

[Mobile is a spectrum](https://simplified.dev/performance/impact-of-web-performance), and a quite entrenched one. While the mobile landscape is very fragmented already, the gap between the experience on various devices will be [widening much further](https://www.filamentgroup.com/lab/5g/) with the growing adoption of 5G.

According to [Ericsson Mobility Visualizer](https://www.ericsson.com/en/mobility-report/mobility-visualizer?f=1&ft=1&r=2,3,4,5,6,7,8,9&t=8&s=1,2,3&u=1&y=2020,2026&c=1), we should be expecting a **15&times; increase in mobile 5G subscribers**, from 212 million in 2020, to 3.3 billion by 2026.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ac59974-774f-44fe-a541-798fbeefed93/mobile-subscriptions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ac59974-774f-44fe-a541-798fbeefed93/mobile-subscriptions.png" width="800" height="721" sizes="100vw" caption="According to <a href='https://www.ericsson.com/en/mobility-report/mobility-visualizer?f=1&ft=1&r=2,3,4,5,6,7,8,9&t=1&s=1,2,3&u=1&y=2019,2026&c=1'>Ericsson</a>, we should be expecting a 15&times; increase in mobile 5G subscribers, from 212 million in 2020, to 3.3 billion by 2026." alt="We should be expecting a 15&times; increase in mobile 5G subscribers, from 212 million in 2020, to 3.3 billion by 2026." >}}

If you’d like to dive deeper into the performance of Android and iOS devices, you can check [Geekbench Android Benchmarks](https://browser.geekbench.com/android-benchmarks/) for Android smartphones and tablets, and [iOS Benchmarks](https://browser.geekbench.com/ios-benchmarks) for iPhones and iPads.

It goes without saying that **testing** thoroughly on a variety of devices &mdash; rather just on a shiny new Android or iOS device &mdash; is *critical* for understanding and improving the experience of your prospect customers, and how well your website or app performs on a large scale.

## Making A Case For Business

While it might sound valuable to test on mobile devices, it might not be convincing enough to drive the management and entire organization towards mobile testing. However, there are quite a few [high-profile case studies](https://developers.google.com/web/showcase) exploring the impact of mobile optimization on key business metrics.

[WPO stats](https://wpostats.com/) collects literally hundreds of them — case studies and experiments demonstrating the impact of web performance optimization (WPO) across verticals and goals.

### Driving Business Metrics

One of the famous examples is [Flipkart](https://www.flipkart.com/), India’s largest e-commerce website. For a while, Flipkart adopted an app-only strategy and temporarily shut down its mobile website altogether. The company found it more and more difficult to provide a user experience that was as fast and engaging as that of their mobile app.

A few years ago, they’ve decided to unify their web presence and a native app into a mobile-optimized progressive web app, resulting in a **70% increase in conversion rate**. They discovered that customers were spending *three* times more time on the mobile website, and the re-engagement rate increased by 40%.

### Improving Search Engine Visibility

It’s not big news that search engines [have been considering mobile friendliness](https://developers.google.com/search/blog/2016/11/mobile-first-indexing) as a part of search engine ranking. With [Core Web Vitals](https://developers.google.com/search/blog/2020/05/evaluating-page-experience), Google has been pushing the experience factors on mobile further to the forefront.

In his article on [Core Web Vitals and SEO](https://simonhearne.com/2021/core-web-vitals-seo/), Simon Hearne discovered that Google’s index update on 31st of May 2021 will result in a positive ranking signal for page experience in **mobile search only**, for groups of similar URLs, which meet all three Core Web Vital targets. The impact of the signal is expected to be small, [similar to HTTPS ranking boost](https://twitter.com/methode/status/1255224116648476675).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c380575-7a95-48cc-bd49-08bbd2c006bd/lighthouse-ci-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c380575-7a95-48cc-bd49-08bbd2c006bd/lighthouse-ci-opt.png" width="800" height="575" sizes="100vw" caption="A performance benchmark Lighthouse is well-known. Its CI counterpart not so much. <a href='https://github.com/GoogleChrome/lighthouse-ci'>Lighthouse CI</a> is quite remarkable: a suite of tools to continuously run, save, retrieve, and assert against Lighthouse results. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c380575-7a95-48cc-bd49-08bbd2c006bd/lighthouse-ci-opt.png'>Large preview</a>)" alt="Lighthouse CI is quite remarkable: a suite of tools to continuously run, save, retrieve, and assert against Lighthouse results" >}}

One thing is certain though: your websites will rank better if they are better optimized for mobile, both in terms of speed and mobile-friendliness &mdash; it goes for accessibility as well.

### Improving Accessibility

Building accessible pages and applications isn’t easy. The challenges start with tiny hit targets, poor contrast and small font size, but it quickly gets much more complicated when we deal with complex single-page-applications. To ensure that we cater well for our customers in various situations &mdash; with  [permanent, temporary and situational disabilities](https://www.microsoft.com/design/inclusive/) — we need to test for accessibility.

That means considering [keyboard navigation](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/), how navigation landmarks are properly assigned, how updates are announced by a screen reader, [focus traps](https://css-tricks.com/focus-management-and-inert/), and whether we avoid any inaccessible libraries or third-party scripts. And then, for every component we are building, we need to ensure that we **keep them accessible over time**.

It shouldn’t be surprising that if a website isn’t accessible to a customer, they are unlikely to access your product either. The earlier you invest in accessibility testing, the more you’ll save down the road on expensive consultancy, expensive third-party services, or expensive lawyers.

## Mobile Web Testing

So, with all the challenges in the mobile space, how, then, do we test on mobile? Fortunately, there is no shortage of **mobile testing tools** out there. However, most times, when performing mobile testing, the focus is mostly on consistency and functionality but for a more thorough mobile test, we need to go a layer deeper into some not-so-obvious specifics of testing.

### Screen sizes

Screen sizes are one of the many things that are always changing in the realm of mobile devices. Year after year new screen sizes and pixel densities appear with new device releases. This poses a problem in testing websites and apps on these devices, making debugging more difficult and time-consuming.

### OS Version fragmentation

With iOS having a high adoption rate on its latest OS releases (a rate of 57% on its latest iOS 14), and the plethora of versions still being used by [Android devices](https://www.statista.com/statistics/271774/share-of-android-platforms-on-mobile-devices-with-android-os/) going as far back as Ice Cream Sandwich, one must make sure to account to this fragmentation when doing mobile testing.

### Browser fragmentation

With Chrome and Safari having a global usage of [62.63% and 24.55% on mobile](https://www.statista.com/statistics/263517/market-share-held-by-mobile-internet-browsers-worldwide/) respectively, one might be tempted to focus on just these browsers when performing mobile tests. However, depending on the region of the world, you are more likely to test in other, less-known browsers, or [proxy browsers](https://timkadlec.com/2015/07/understanding-proxy-browsers-architecture/), such as Opera Mini. Even though their percentage usage might be small, it might run into hundreds of thousands of usage globally.

## Performing Mobile Web Testing

To perform mobile web testing, one option is to [set up a device lab](https://www.smashingmagazine.com/2012/09/establishing-an-open-device-lab/), and run tests locally. In times of remote work, it’s quite challenging as you usually need a number of devices at your disposal. **Acquiring these devices** doesn’t have to be expensive, and experiencing the loading on your own is extremely valuable.

However, if you want to check how consistent the experience is, or conduct **automated tests**, it’s probably not going to be enough.

In such cases, a good starting point is [Responsively](https://responsively.app/), a free open-source tool with mirrored interactions, customizable layout, 30+ built-in device profiles, hot reloading and screenshot tools.

There are also other helpful tools that you may want to look into:

- [LT Browser](https://www.lambdatest.com/lt-browser)
LT Browser is a free-to-use desktop application that helps you build well-performing, responsive websites or web apps. It has 50+ built-in device resolutions &mdash; for mobile, tablet and desktop. You can check the [mobile view of your website](https://www.lambdatest.com/mobile-view-website) in a side by side comparison view with mirrored interactions and touch support.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955732b9-9205-4369-bd21-ff57443d9d3a/mobile-test-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955732b9-9205-4369-bd21-ff57443d9d3a/mobile-test-example.png" width="800" height="450" sizes="100vw" caption="Testing the Smashing Magazine website on different devices. <a href='https://www.lambdatest.com/lt-browser'>LT Browser</a> in action. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955732b9-9205-4369-bd21-ff57443d9d3a/mobile-test-example.png'>Large preview</a>)" alt="Testing the Smashing Magazine website on different devices" >}}

Once you have downloaded the browser and registered, you can build, test, and debug your website, as well as take screenshots and videos of bugs, assign them to specific devices, run a performance profiling and observe multiple devices side by side. By default, a free version provides 30 mins per day.

If you need something slightly more advanced, [LambdaTest](https://www.lambdatest.com/) allows you to run a cross-browser test on 2000+ devices on different operating systems with which you can even perform both manual and [automated browser testing](https://www.lambdatest.com/selenium-automation). (*Full disclosure and reminder: LambdaTest is a friendly sponsor of this article.*)

- [Sizzy](https://sizzy.co/)<br />
This tool supports sync scrolling, clicking and navigation across devices, as well as takes screenshots of all devices at once, with and without a device frame. Plus, it includes a Universal Inspect Element to inspect all devices at once.
- [Blisk](https://blisk.io/)<br />
Another little helpful tool that supports over 50 devices out of the box, along with sync scrolling. You can test touch support and preview devices side-by-side, working with the same piece of code across all opened devices. Hot-reloading is supported as well, as well as video recording and screenshots.
- [Polypane](https://polypane.app/)<br />The tool also allows you to preview your website on 27 devices, along with sync scrolling, clicks, touch, keyboard and *hovers*. It provides a comprehensive support of media queries (e.g. `prefers-reduced-data`) and a suite of debugging tools like accessibility review, CSS layout and link testing.
- [BrowserStack](https://www.browserstack.com/)<br />The service provides an option to automate testing as well as testing for low battery, abrupt power off, and interruptions such as calls or SMS.
- Also, if you wish to stick with device labs to automate testing then you can set up an in-house Selenium Grid with open-source solutions i.e. [Zalenium](https://opensource.zalando.com/zalenium/), [Aerokube](https://aerokube.com/).

## Conclusion

In this article, we have looked into the **state of mobile in 2021**. We’ve seen the growing usage of mobile devices as the primary means to access the web, and we’ve looked into some challenges related to that. We’ve also looked into mobile testing, and how some tools can help us find and fix bugs on mobile.

Keep in mind that your website is the face of your business and more and more users are going to access it via their mobile phones. It’s important to make sure that your users can access the services you provide on your website and have an **accessible and fast experience** on their devices as they do on the desktop version. This will ensure that the benefits of brand visibility get the attention they deserve.

{{< signature "vf, il" >}}
