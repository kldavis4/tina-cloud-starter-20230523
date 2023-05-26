---
title: Designing For A Browserless Web
slug: designing-for-a-browserless-web
author: mitch-lenton
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01df0ce9-10e1-45b9-8502-d39d5740a63c/5-designing-for-a-browserless-web-800w-opt.png
date: 2017-11-27T15:23:31+01:00
summary: >-
  Users couldn’t care less about whether a technology is native, an installed web app or a website. What makes users engage and makes shoppers convert is really the experience itself. In this article, Mitch takes a closer look at PWAs on Android devices and explains how we can pave the way for a new era of browserless web browsing.
description: >-
  Users couldn’t care less about whether a technology is native, an installed web app or a website. What makes users engage and makes shoppers convert is really the experience itself. In this article, Mitch takes a closer look at PWAs on Android devices and explains how we can pave the way for a new era of browserless web browsing.
draft: false
categories:
  - Browsers
  - Apps
  - Android
  - PWA
---
<p>What happens when we take the web browser out of web browsing? Google’s new "Add to Homescreen" feature delivers fast, focused web experiences that are indistinguishable from those of a native app. What can designers learn from the successes of early adopters such as Twitter, and how can we leverage app-like design patterns to tackle this brand new set of user experience challenges?</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff8d3a7-d553-4dd0-ba34-86dbd36d8176/1-addtohomescreen-chrome-devs.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff8d3a7-d553-4dd0-ba34-86dbd36d8176/1-addtohomescreen-chrome-devs.gif" width="800" height="535" alt="Add to Homescreen" /></a><figcaption>The "Add to Homescreen" installation process, as shown on Google Chrome Developer’s mobile website (<a href="https://developers.google.com/web/updates/2015/03/increasing-engagement-with-app-install-banners-in-chrome-for-android">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff8d3a7-d553-4dd0-ba34-86dbd36d8176/1-addtohomescreen-chrome-devs.gif">Large preview</a>)</figcaption></figure>

We’ve seen debates on the topic of <a href="https://www.lifewire.com/native-apps-vs-web-apps-2373133">native versus web experiences</a>. Both have their pros and cons, but very often the biggest downside of the in-browser experience is that it doesn’t feel as reliable, fast and immersive as the native app experience.</p>

<p>In this article, we will cover tips and tricks for designing and developing progressive web applications (PWAs), specifically the ones that are added to the home screen on Android devices. But first, let’s see a couple of examples and make a case for PWAs.</p>

<div class="c-felix-the-cat"><h4>From Web Apps To Desktop Apps</h4><p>Did you know that you can add “desktop app developer” to your resumé with just a little more effort? All you need to do is look over some API documentation and create your first modern desktop app.</p>
<p><a href="https://www.smashingmagazine.com/2017/03/beyond-browser-web-desktop-apps/?_ga=2.108757899.826330288.1511785587-310714952.1511785587" class="btn btn--small btn--green">Jump to a related article&nbsp;↬</a></p></div>

## The Rise Of The App-Like Experience

<p>PWAs are, simply put, websites that look and feel like native applications. In his talk at the Google I/O developer conference, Google’s VP of Product, Rahul Roy-Chowdhury, describes them as "a radically better web experience… which users love and are more engaged with."</p>

{{% feature-panel %}}

<p>The numbers back up Rahul’s claims. Forbes has seen its user engagement <a href="https://developers.google.com/web/showcase/2017/forbes">double since the launch</a> of its PWA. The numbers also continue to show growth in the e-commerce sector, with Lancôme seeing a <a href="https://developers.google.com/web/showcase/2017/lancome">large increase in conversion rates</a> following the launch of its new PWA.</p>

{{% pull-quote %}}Users couldn’t care less about whether a technology is native, an installed web app or a website. What makes users engage and makes shoppers convert is the experience itself.{{% /pull-quote %}}

<p>These kinds of fast, fluid, app-like mobile experiences are what users want and will come to expect as more PWAs emerge in the mainstream market. One feature that will seem to accelerate this wave is "Add to Homescreen," which is basically a PWA installation process. For the end user, adding a PWA to the home screen kicks off that app-like experience.</p>

## What Is &ldquo;Add To Homescreen,&rdquo; And Is It Worth It?

<p>&ldquo;Add to Homescreen&rdquo; is a feature that installs a PWA to Android’s home screen, making the PWA instantly accessible without the user needing to open a browser and type the URL or use a search engine. (Side note: Even though a similar feature has been available on iOS Safari since the earliest iPhones, users were not offered much to simulate the behavior of an app. For this reason, Safari’s version is not a part of this article.)</p>

<p>As reflected in Google’s <a href="https://developers.google.com/web/tools/lighthouse/">Lighthouse checklist</a>, PWAs with this capability score higher and, as a result, are likely to rank better in search results.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df55b2dc-1021-462d-ba5a-10cb80d586e7/2-lighthouse-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3683449f-04d9-4d07-9340-1be1c9fe4b70/2-lighthouse-800w-opt.png" width="800" height="444" alt="Google Lighthouse" /></a><figcaption>"Add to Homescreen" as part of Google’s Lighthouse checklist (<a href="https://wpmobilepack.com/blog/building-progressive-web-apps-top-wordpress/">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df55b2dc-1021-462d-ba5a-10cb80d586e7/2-lighthouse-large-opt.png">Large preview</a>)</figcaption></figure>

Take Twitter Lite, a PWA. Traditionally, Twitter has found it difficult to re-engage its millions of users on the mobile web. Since introducing the "Add to Homescreen" prompt to its Twitter Lite PWA, it is seeing <a href="https://developers.google.com/web/showcase/2017/twitter">250,000 unique daily users</a> launch the web app from the home screen at an average of four times a day.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f59d0da-a0a1-45f1-87dd-19ccb53bdf80/3-twitter-lite-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/873b69ee-7e20-493c-a959-1d1392c887be/3-twitter-lite-800w-opt.png" width="800" height="553" alt="Twitter Lite" /></a><figcaption>Twitter Lite’s "Add to Homescreen" prompt and subsequent PWA launched in full-screen mode (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f59d0da-a0a1-45f1-87dd-19ccb53bdf80/3-twitter-lite-large-opt.png">Large preview</a>)</figcaption></figure>

The retail sector is also seeing success. Alibaba has reported a <a href="https://developers.google.com/web/showcase/2016/alibaba">four-times higher interaction rate</a> after users added the PWA to their device’s home screen, and Flipkart has seen a <a href="https://developers.google.com/web/showcase/2016/flipkart">70% increase in conversion rate</a> among shoppers who arrived via the home-screen icon.</p>

<p>Although "Add to Homescreen"’s user base is limited to Android Chrome, the feature rewards this highly engaged minority with an immersive, more exclusive experience &mdash; a role traditionally played by native apps.</p>

## Aren’t Progressive Web Applications Just Websites Wrapped Up As Apps?

<p>Essentially, yes, and why not? <a href="https://www.smartinsights.com/mobile-marketing/mobile-marketing-analytics/mobile-marketing-statistics/attachment/percentage-of-mobile-app-vs-browser-minutes/">90% of mobile minutes</a> are spent in apps, with <a href="https://marketingland.com/apps-convert-better-for-retailers-164753">120% better conversion rates</a> in the retail sector.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f30b487-78a3-4b08-802e-6da900d6366e/4-app-conversion-rates-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c31cff-b737-4188-beef-5c44abdcf162/4-app-conversion-rates-800w-opt.png" width="800" height="360" alt="" /></a><figcaption>Data: Criteo’s "<a href="https://www.criteo.com/resources/mobile-commerce-report/">The State of Mobile Commerce 2016</a>" report (<a href="https://jmango360.com/mobile_commerce_trends/">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f30b487-78a3-4b08-802e-6da900d6366e/4-app-conversion-rates-large-opt.png">Large preview</a>)</figcaption></figure>

These are the kind of statistics that would lead any retailer down the path of native app development. However, with the average cost of a native app <a href="https://blog.formotus.com/enterprise-mobility/figuring-the-costs-of-custom-mobile-business-app-development">sitting at around $270,000</a>, "Add to Homescreen" offers an attractive financial alternative.</p>

<p>Users couldn’t care less about whether a technology is native, an installed web app or a website. What makes users engage and makes shoppers convert is the experience itself:</p>

<ul>

<li>Does it load quickly?</li>

<li>Does it work offline?</li>

<li>Is navigation instant?</li>

<li>Does it integrate seamlessly with the device?</li>

</ul>

<p>These are the characteristics of app-like design that must be incorporated if "Add to Homescreen" is to deliver the kind of high engagement statistics commonly associated with native apps.</p>

## What Makes An Experience App-Like?

<p>"Add to Homescreen" creates an experience focused solely on the app in question. The website is launched via an app icon, without the browser’s URL bar or any navigation toolbar that would otherwise offer links to external websites.</p>

<p>It’s a good starting point, but we must also recognize and meet certain expectations of native app users if the experience is to feel truly app-like, including:</p>

<ul>

<li>instant page transitions;</li>

<li>high perceived performance;</li>

<li>offline accessibility;</li>

<li>full device integration;</li>

<li>app-style navigation;</li>

<li>back button;</li>

<li>sharing action;</li>

<li>copy URL, print, and go forward.</li>

</ul>

<p>Ready to dive in? Let’s look at each one.</p>

## Instant Page Transitions

<p>Users expect to be able to get in and around an app quickly, without waiting for new content to load after each interaction.</p>

### Solved With PWA

<p>For a PWA to pass the Lighthouse checklist, it must follow certain <a href="https://developers.google.com/web/fundamentals/performance/rail">performance-enhancing guidelines</a>. Content must be cached behind the scenes, and new pages must load so quickly that it feels like there was no loading event.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f0d2178-8ee0-4f3b-8068-4d0989f1d2ca/5-pf-instant-loads.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f0d2178-8ee0-4f3b-8068-4d0989f1d2ca/5-pf-instant-loads.gif" width="800" height="519" alt="Pure Formulas’ PWA" /></a><figcaption>Fast page transitions in Pure Formulas’ PWA (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f0d2178-8ee0-4f3b-8068-4d0989f1d2ca/5-pf-instant-loads.gif">Large preview</a>)</figcaption></figure>

## Perceived Performance

<p>Amazingly, the level of <a href="https://www.ericsson.com/assets/local/mobility-report/documents/2016/ericsson-mobility-report-feb-2016-interim.pdf">stress caused by mobile delays</a> is comparable to that of watching a horror movie! Users who download an app do not expect to have to wait for their content. Nor are they willing to suffer a disjointed experience caused by elements appearing asynchronously as they load.</p>

### Solved With PWA

<p>The "Add to Homescreen" PWA launch transition (see Flipkart example below) provides a visual bridge between loading and loaded content. This is an example of how "preloaded states" can enhance the perception of speed and seamlessness. A well-designed PWA will build on this idea by using <a href="https://medium.com/mobify-design-team/designing-for-the-appearance-of-speed-aaabc7f568c2">placeholders (skeletons)</a> that mimic the end state of the page and by using <a href="https://en.wikipedia.org/wiki/Lazy_loading">lazy-loading</a> to deprioritize elements that are out of view, making the initial loading seem faster.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d103b6e-69d5-4f64-87af-dae748174701/6-flipkart-launch.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d103b6e-69d5-4f64-87af-dae748174701/6-flipkart-launch.gif" width="800" height="476" alt="Flipkart PWA" /></a><figcaption>Built-in app loader provides a smooth transition to the content, as seen in Flipkart’s PWA. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d103b6e-69d5-4f64-87af-dae748174701/6-flipkart-launch.gif">Large preview</a>)</figcaption></figure>

## Works Offline

<p>Users who download native apps do not expect to have to rely on an Internet connection in order for the apps to function properly.</p>

### Solved With PWA

<p><a href="https://www.google.com/url?q=https://developers.google.com/web/fundamentals/getting-started/primers/service-workers&sa=D&ust=1509001514760000&usg=AFQjCNE-RkL4scBjaJ6hj6bTUwFfYBl_oA">Service workers</a> (a technology that improves the offline experience) can be used to instantly display online content in areas of low or no connectivity. Page content is cached behind the scenes, allowing it to be accessed where there would otherwise be a lag in the browsing experience, such as when entering a tunnel on a train.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f456b602-40e3-4a05-b055-771b9a419372/7-merlins-offline-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/764e5f5d-60c8-4d38-8700-46c3e58a8535/7-merlins-offline-800w-opt.png" width="800" height="553" alt="Merlin Potions" /></a><figcaption>Offline browsing, as shown on Merlin’s Potions (Mobify’s PWA demo) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f456b602-40e3-4a05-b055-771b9a419372/7-merlins-offline-large-opt.png">Large preview</a>)</figcaption></figure>

## Full Device Integration

<p>There are certain locations on a device where users expect to find and manage their apps.</p>

### PWA Solution

<p>PWAs added to the home screen now show up anywhere you’d expect an Android app to show up. This includes the app launcher, task switcher and system settings. This also ensures that any other app that links to a page on the PWA, such as a Google search or social media link, will open the app and not the browser. Push notifications even appear as if they come from a native app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4709691-7ef1-4330-8eda-4e5cbda0d2aa/8-trivago-app-manifest-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4777b6e4-f9d4-4c07-b929-0d088dc3688c/8-trivago-app-manifest-800w-opt.png" width="800" height="553" alt="Trivago PWA" /></a><figcaption>Trivago’s PWA, as shown in the app launcher, device search and system settings (<a href="https://www.youtube.com/watch?v=m-sCdS0sQO8">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4709691-7ef1-4330-8eda-4e5cbda0d2aa/8-trivago-app-manifest-large-opt.png">Large preview</a>)</figcaption></figure>

## App-Style Navigation

<p>Apps share a common approach to navigation. The header bar typically shows the title of the current section in the center; the back button is in the top left; and any contextual actions (favoriting, sharing, etc.) are in the top right.</p>

### No PWA Solution, Yet

<p>This pattern is not common on the mobile web. Instead, these actions are found in the browser’s built-in functionality (for example, the browser’s back button). The web works this way for a reason. An app will typically start from the same screen each time, whereas mobile web users are often referred from search or social media &mdash; any page can be their landing page. For this reason, the logo and other global actions take center stage in the header bar and remain there throughout the experience.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b649bd8-04c9-4623-b29d-2157fc9ea1e5/9-etsy-app-web-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c06d6966-402b-4dc2-88ae-c50fc953abba/9-etsy-app-web-800w-opt.png" width="800" height="508" alt="Etsy mobile website" /></a><figcaption>Etsy’s mobile website (left) and its Android app (right) illustrate how app headers typically differ in design &mdash; the latter favoring contextual actions such as sharing over global elements such as the logo and sign-in link. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b649bd8-04c9-4623-b29d-2157fc9ea1e5/9-etsy-app-web-large-opt.png">Large preview</a>)</figcaption></figure>

This expectation must be addressed if PWAs with "Add to Homescreen" are to really feel like apps. In order to do this, designers must figure out how to recover key navigation patterns now lost with the browser.</p>

## Back Button

<p>Some might argue that because Android provides a back button through the device itself, then there is no need to replace the browser’s back functionality. In fact, the two interactions do different things. Most apps continue to offer a back button in the header as an "up" action, to <a href="https://developer.android.com/design/patterns/navigation.html">navigate within the hierarchical relationship between pages</a>. The system’s back functionality might close a modal window or navigate to a different app entirely.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03aa9404-26fd-498d-a7b0-09b2e3779bbb/10-back-button-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd91f8a8-5abe-41d7-9ca6-7368bfb1b7f4/10-back-button-800w-opt.png" width="800" height="341" alt="back button" /></a><figcaption>The back button is a useful interaction in both Chrome iOS and Opera for Android’s web browsers. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03aa9404-26fd-498d-a7b0-09b2e3779bbb/10-back-button-large-opt.png">Large preview</a>)</figcaption></figure>

### Solution

<p>One possible solution is to replace the menu button in the top left with a back button once the user progresses past the initial page. This was validated when we put this pattern in front of users. Once participants had progressed through the initial home page (and a menu icon was no longer visible), we asked them to navigate to a new section. Six out of six intuitively used the back button to navigate to the home page, where they could open the menu.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9ff037c-d786-4873-b50a-80c53bcef6ec/11-merlins-back-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40e44b90-e8f7-4f4c-913e-60d7cf242234/11-merlins-back-800w-opt.png" width="800" height="393" alt="menu and back button placement" /></a><figcaption>Proposed menu and back-button placement in PWAs added to the home screen (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9ff037c-d786-4873-b50a-80c53bcef6ec/11-merlins-back-large-opt.png">Large preview</a>)</figcaption></figure>

## Sharing Action

<p>Built into the user interface of any web browser is the ability to share a page on social media and through other apps installed on the device.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85c070d2-1ded-464a-9735-29f936606a10/12-share-android-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2c2e3ed-29f5-43d9-bec6-2b0bdb1a5bbf/12-share-android-800w-opt.png" width="800" height="430" alt="chrome and samsung browsers" /></a><figcaption>Both Chrome and Samsung Internet browsers have a sharing action available behind a menu overlay. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85c070d2-1ded-464a-9735-29f936606a10/12-share-android-large-opt.png">Large preview</a>)</figcaption></figure>

### Solution

<p>Designers should provide more prompts to share commonly shared content within the page. We found during testing that users will typically look for sharing buttons around the page’s head or product image before opening any menus. If the functionality was not found, participants expected to find a sharing icon in the header bar.</p>

<p>The "More" icon is an <a href="https://material.io/guidelines/components/menus.html">Android-esque pattern</a> used to indicate an overflow of options. Try adding the sharing action behind a menu like this. It is even possible to trigger Android’s native sharing dialog using the <a href="https://developers.google.com/web/updates/2016/09/navigator-share">Web Share API</a> (which, at the time of writing, is a Chrome-only feature and still not standards-tracked).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c135d2d-55d4-4f8a-9a98-9af9e0cf4bfc/13-merlins-share-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fb568cb-55f1-4dfb-8734-7ecc7a6e500c/13-merlins-share-800w-opt.png" width="800" height="393" alt="proposed menu overlay" /></a><figcaption>Proposed menu overlay with global sharing prompt (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c135d2d-55d4-4f8a-9a98-9af9e0cf4bfc/13-merlins-share-large-opt.png">Large preview</a>)</figcaption></figure>

## Copy URL, Print, Go Forward

<p>Less common actions, such as copying the URL and printing, are basic functions of a browser and should not be overlooked.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f120f93-18a4-4b48-b475-790be3a53e49/14-copy-url-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/633543da-28d8-4386-9055-3fd880647c03/14-copy-url-800w-opt.png" width="800" height="372" alt="url copy" /></a><figcaption>Copying a URL is a useful interaction in many different situations. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f120f93-18a4-4b48-b475-790be3a53e49/14-copy-url-large-opt.png">Large preview</a>)</figcaption></figure>

### Solution

<p>An easy way to offer copy-URL and print functionality is by using the <a href="https://developers.google.com/web/updates/2016/09/navigator-share">Web Share API</a> (again, at the time of writing, supported only in Google Chrome). Alternatively, they can be presented as separate options in the <a href="https://material.io/guidelines/components/menus.html">overflow menu</a>. This menu can then be extended to include the forward action or anything else that would benefit from a persistent location in the header bar (logging in and out, for example).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62344eae-0d82-44eb-8f96-dc2dfc0ba9a3/15-merlins-copyurl-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbd25c53-9f2b-4d9e-bcd1-b927d76805d9/15-merlins-copyurl-800w-opt.png" width="800" height="393" alt="sharing option" /></a><figcaption>Actions such as copying a URL and sending to a printer can be accessed via the sharing option, demonstrated here using the Web Share API. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62344eae-0d82-44eb-8f96-dc2dfc0ba9a3/15-merlins-copyurl-large-opt.png">Large preview</a>)</figcaption></figure>

## How To Make It Work In The Real World

<p>It will take time for "Add to Homescreen" to develop into an accepted group of patterns. Below are some best practices that could help in this development.</p>

### Sticky Headers, Persistent Actions

<p>"Add to Homescreen" early adopters Flipkart and AliExpress both recognize the importance of learnability when introducing new patterns. They ensure that users always know where to find crucial global actions (back, cart, search): in a header bar that sticks to the top of the screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94cfed7a-48ac-445f-9c83-d4c07f80b16b/16-sticky-headers-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09699fc3-f366-4a55-9e7b-2c41e444f43b/16-sticky-headers-800w-opt.png" width="800" height="341" alt="sticky headers" /></a><figcaption>Modern PWAs AliExpress, Flipkart and Snapdeal share commonalities in the design of their header bars. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94cfed7a-48ac-445f-9c83-d4c07f80b16b/16-sticky-headers-large-opt.png">Large preview</a>)</figcaption></figure>

### Prompt Intelligently

<p>Since the Google Chrome team announced that it would be giving PWAs full control of when to prompt users, "Add to Homescreen" installations have increased. Flipkart saw a <a href="https://www.youtube.com/watch?v=m-sCdS0sQO8&feature=youtu.be&t=13m44s">threefold increase</a> in engagement when prompting users after they had made a purchase.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc6d5a1b-69d5-411b-a5a1-e05c9585ec0c/17-flipkart-add-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc5ed4f-5499-4f90-9974-a5d604748727/17-flipkart-add-800w-opt.png" width="800" height="452" alt="add to Homescreen in Flipkart" /></a><figcaption>Example of Flipkart’s "Add to Homescreen" prompt on the order-confirmation page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc6d5a1b-69d5-411b-a5a1-e05c9585ec0c/17-flipkart-add-large-opt.png">Large preview</a>)</figcaption></figure>

### Stress and Test

<p>Part of the validation process for any new pattern is to stress test it in multiple applications. We found that the pattern stood up well to the edgiest of edge cases. The header bar in Lancome’s PWA contains many calls to action. Lancome identified the overflow menu as a great opportunity to simplify its user interface, while offering exclusives to power users whom it expected to use "Add to Homescreen," exclusives such as a link to its loyalty program.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bf82916-2aca-4696-aede-b4a48f112cf2/18-add-to-home-testing.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bf82916-2aca-4696-aede-b4a48f112cf2/18-add-to-home-testing.gif" width="800" height="560" alt="add to home testing" /></a><figcaption>This interactive prototype was used to test the proposed pattern. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bf82916-2aca-4696-aede-b4a48f112cf2/18-add-to-home-testing.gif">Large preview</a>)</figcaption></figure>

## Where Is "Add To Homescreen" Supported?

<p>Apple has announced it <a href="https://twitter.com/webmaxru/status/893027996659060738">will support service workers</a>, but it has also made a commitment to making the App Store an attractive place for native app developers to spend their time and money. This could be the reason why iOS’ Safari browser has been slow to adopt PWAs and browserless web browsing, despite <a href="https://www.youtube.com/watch?v=_ssDaecATCM&feature=youtu.be&t=16m7s">advances from competitors</a>.</p>

<p>Samsung Internet browser has developed a persistent "Add to Homescreen" prompt within the browser bar, so that users always know where to find it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e18ff4-b172-4f42-804a-d0a495c6be46/19-samsung-prompt-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/832a8878-9e0c-4063-ad74-90cc8e98a9cc/19-samsung-prompt-800w-opt.png" width="800" height="476" alt="Samsung prompt" /></a><figcaption>"Add to Homescreen"’s persistent location in the new Samsung Internet browser (<a href="https://www.youtube.com/watch?v=m-sCdS0sQO8">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e18ff4-b172-4f42-804a-d0a495c6be46/19-samsung-prompt-large-opt.png">Large preview</a>)</figcaption></figure>

Windows takes "Add to Homescreen" one step further. Any PWA with this ability will now be listed in the Windows Store as a downloadable app. These apps are light and can be installed on desktop and tablet devices quickly, running the websites as convenient, browserless experiences.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/883ee236-7a45-4596-ad96-33459693967a/20-jigspace-windows-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75cfd2e8-a9b1-4f5a-8445-a05337c3b3ff/20-jigspace-windows-800w-opt.png" width="800" height="538" alt="jigspace windows" /></a><figcaption>Jig.space’s PWA is shown as a downloadable desktop app in the Windows store. (<a href="https://www.youtube.com/watch?v=m-sCdS0sQO8">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/883ee236-7a45-4596-ad96-33459693967a/20-jigspace-windows-large-opt.png">Large preview</a>)</figcaption></figure>

## Conclusion

<p>"Add to Homescreen" offers an immersive, exclusive experience to the highly engaged, converting user. While adoption grows, both in user base and the devices that support the feature, validation can be found in early <a href="https://developers.google.com/web/showcase/2017/twitter">success stories, such as Twitter Lite</a>. These stories show how a more modern, app-like web can have a positive effect on engagement when it meets user expectations of performance and design.</p>

<p>These expectations are met by combining PWA performance enhancements with intuitive design patterns in navigation and app-like user experiences. With this, we can pave the way for a new era of browserless web browsing.</p>

{{< signature "md, yk, al, ra, il" >}}
