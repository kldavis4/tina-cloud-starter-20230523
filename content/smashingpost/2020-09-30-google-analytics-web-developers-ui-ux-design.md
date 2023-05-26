---
title: '5 Ways Google Analytics Helps Web Developers In UI/UX Design'
slug: google-analytics-web-developers-ui-ux-design
author: clara-buenconsejo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe222f1b-8c72-48ae-b866-d4467d58ed3f/4-google-analytics-web-developers-ui-ux-design.png
date: 2020-09-30T12:30:00.000Z
summary: >-
  Ever wondered what all those Google Analytics code snippets are for and why your marketing team regularly asks you to add a new one? In this article, we’ll look at 5 features in Google Analytics that can help web developers and designers in making a better user experience on their website.
description: >-
  In this article, we’ll look at 5 features in Google Analytics that can help web developers and designers in making a better user experience on their website.
categories:
  - UX
  - UI Design
  - Analytics
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

Google Analytics is one of the most popular marketing analytics platforms out there &mdash; and not just because its standard version is free. More than a million organizations worldwide use this platform to gain better insights on user behavior on their websites.

However, for most web developers, their involvement with Google Analytics ends with just installing the base code for pageviews. This code usually looks like this, when using the gtag.js version of the code:

<div class="break-out">

 <pre><code class="language-javascript">&lt;!-- Global site tag (gtag.js) - Google Analytics --&gt;
&lt;script async src="https://www.googletagmanager.com/gtag/js?id=UA-35169008-1"&gt;&lt;/script&gt;
&lt;script&gt;
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-35169008-1');
&lt;/script&gt;
</code></pre>
</div>

Or it looks like this, with the analytics.js implementation:

<div class="break-out">

 <pre><code class="language-javascript">&lt;!-- Google Analytics --&gt;
&lt;script&gt;
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXX-Y', 'auto');
ga('send', 'pageview');
&lt;/script&gt;
&lt;!-- End Google Analytics --&gt;
</code></pre>
</div>

While there’s already many data points made available with this basic implementation, they end up missing out on other key features. Due to the lack of available data to consult, there have even been cases where web developers or designers choose to remove a specific feature on the site, without realizing that most users use that feature regularly.

Hence, here are five of the most important features in Google Analytics that you can utilize to improve user experience &mdash; and separate you from the rest of the web developers and designers out there:
 
## 1. Use Events To Identify User Interactions On Specific Parts Of Your Website

As stated above, the basic Google Analytics code only tracks pageviews by default. If you want to track actions on your website, such as button clicks or form submissions, you’ll need to fire a separate Google Analytics event. These events can be implemented by adding the following code with the appropriate Event Category, Action, and Label information:

<pre><code class="language-javascript">ga('send', {
  hitType: 'event',
  eventCategory: 'Event Category',
  eventAction: 'Event Action',
  eventLabel: 'Event Label'
});</code></pre>

A shorthand version of the code is also available in this format:

<div class="break-out">

<pre><code class="language-javascript">ga('send', 'event', 'Event Category', 'Event Action', 'Event Label');</code></pre>
</div>

Once the events are set up, they will show up in the Google Analytics UI under the Behavior > Events > Top Events report:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f608259-2a26-4155-b5b8-2a9772ce17ce/1-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f608259-2a26-4155-b5b8-2a9772ce17ce/1-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Where to find the Top Events report in Google Analytics. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f608259-2a26-4155-b5b8-2a9772ce17ce/1-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Where to find the Behavior > Events > Top Events report in Google Analytics" >}}

As a best practice, you can use Event Category to group events based on a specific function (ex. Page Engagement, Ecommerce). Meanwhile, you can use Event Action to identify the exact action the user made (Click, Scroll, Form Submission) while you can use Event Label to get the URL where the event was fired.

Alternatively, a better way to implement these events would be to use Google Tag Manager instead. In lieu of the actual Google Analytics code, you will need to install the Google Tag Manager code instead:

<div class="break-out">

<pre><code class="language-javascript">&lt;!-- Google Tag Manager --&gt;
&lt;script&gt;(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-5PLFVFV');&lt;/script&gt;
&lt;!-- End Google Tag Manager --&gt;</code></pre>
</div>

Then once Google Tag Manager is set up, all you need to do is to set up the Google Analytics Page View tag and the Event tags you need. Simply create a new Tag by clicking the “New” button, then click on Tag Configuration, and Google Analytics will be one of the default options available:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19c1e48f-c471-49ab-a858-75c3a1973960/2-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19c1e48f-c471-49ab-a858-75c3a1973960/2-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Creating a Google Analytics tag in Google Tag Manager. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19c1e48f-c471-49ab-a858-75c3a1973960/2-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Tag Manager - Creating a Google Analytics tag in Tag Configuration settings" >}}

You’ll then be able to select between the different Google Analytics tag types, which includes “Event” as one of them. Once you’ve filled in the Tag Configuration details, you’ll just need to set up the appropriate trigger to fire the event. There are already built-in triggers such as clicks on Google Tag Manager; you’ll just need to select the one suitable for your event.

Don’t forget to test the tag in Google Tag Manager’s preview mode, then click publish once the set up is complete.

Take note that it’s important to be careful when you’re implementing events via Google Tag Manager or by adding the actual code for events via Google Analytics. Whatever approach you choose for implementation should be the same all throughout the site. Either you go all the way with Google Tag Manager or with hard-coding the actual event code. 

Otherwise, you may end up tracking the same website action twice &mdash; once by adding the event code, another via Google Tag Manager &mdash; and recording duplicate data inside Google Analytics.

Adding events even become more important when it comes to setting up Ecommerce and Enhanced Ecommerce tracking for Google Analytics. While you do need to turn on these settings in the Google Analytics interface, you’ll need to go back to your tracking and add separate ecommerce events. These events are needed to send the complete set of e-commerce data back to the Google Analytics servers. 

## 2. Learn How Far Users Scroll Down The Page With Scroll Tracking Events

Other than tracking clicks and form submissions, events in Google Analytics can be also used for scroll tracking. This can be done by adding the Google Analytics event code to fire once a specific element appears in the viewport. You can also set the code to fire if the user has scrolled a specific percentage down the screen.

Alternatively, in Google Tag Manager, scroll tracking can be implemented much easier by using the Scroll Depth trigger. All you need to do is to create a new trigger, select the “Scroll Depth” trigger type, then fill in the necessary details.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e40b936b-b983-4fcc-80ef-90e0c369e1c4/3-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e40b936b-b983-4fcc-80ef-90e0c369e1c4/3-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="The Scroll Depth trigger type in Google Tag Manager. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e40b936b-b983-4fcc-80ef-90e0c369e1c4/3-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Tag Manager - Finding the Scroll Depth trigger option" >}}

So how can this feature help you in terms of user experience? For starters, this obviously can help you determine up to what part of the page are users willing to scroll down. Since that data is in Google Analytics, you can segment that data based on device or browser, time of day, location, etc. 

That way, if you’re deciding whether you can place a specific widget for a specific kind of user, you have some data to back up your decision. This can also eliminate the need to purchase separate scroll tracking software, as all you’ll need is a bit of time to implement this feature.

## 3. Get An Estimate Of How Much Time They Actually Spend On Your Website

Learning up to where people scroll is one thing; finding out how much time they spend on the site is another. Thankfully that’s also possible to measure with Google Analytics.

By default, after installing the Google Analytics pageview tag, users can already get a metric called Avg. Session Duration. This metric is generally understood to measure the amount of time that a user spends on each visit to your website (a session).

However, this metric can be inaccurate at times. After all, Google Analytics really only measures Avg. Session Duration based on the timestamps of the data (hits) that it receives.

This also explains why most bounces &mdash; or visits on the website with either only one pageview or event in them &mdash; have an Avg. Session Duration of 00:00:00.

So how would you get around this limitation? By firing timing hits. These can help accurately calculate the amount of time a user spends on a page without recording another pageview or event. You just need to send the timing hits by implementing this code to fire at specific intervals on your site:

<div class="break-out">

<pre><code class="language-javascript">ga('send', 'timing', [timingCategory], [timingVar], [timingValue], [timingLabel], [fieldsObject]);</code></pre>
</div>

A more detailed description of each field is available on [the Google Developers’ site](https://developers.google.com/analytics/devguides/collection/analyticsjs/user-timings).

Once implemented, these hits will be visible in the Behavior > Site Speed > User Timings section in Google Analytics.

Alternatively, since timing hits have a cap of 10,000 hits per day, you can create custom events that fire at specific intervals instead. Like other regular events, these would then be visible in the Behavior > Events > Top Events section.

A word of caution when setting up timing hits, however: make sure to add a “timeout” of sorts for them. That way these hits won’t continuously fire &mdash; and the data sent to Google Analytics &mdash; for too long, if the page was just left open on an unattended browser.


## 4. Find Out Where Users Get Stuck Or Other Pain Points On The Website

Once you’ve implemented events and timing hits on Google Analytics, you’d see them in the different sections of the platform. However, this introduces a new challenge: how can you unite these different data points into one report that shows the entire user journey on your website?

That’s where the Behavior Flow report in Google Analytics comes into play. This report, which appears as a flowchart, shows how users arrive at the site and the subsequent pageviews or actions they take before dropping off.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe222f1b-8c72-48ae-b866-d4467d58ed3f/4-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe222f1b-8c72-48ae-b866-d4467d58ed3f/4-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="The Behavior Flow report in Google Analytics. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe222f1b-8c72-48ae-b866-d4467d58ed3f/4-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics: Behavior Flow Report" >}}

By default, the Behavior Flow report uses the Landing Page and the specific pages that groups of users go to. 

You can also change the Behavior Flow report to focus more on events. Simply click to the dropdown menu below the report’s header and select “Events” or “Pages and Events.”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71cf32c9-2936-4378-be3e-6afe7a3d6396/5-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71cf32c9-2936-4378-be3e-6afe7a3d6396/5-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Google Analytics Behavior Flow Report &mdash; View Options. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71cf32c9-2936-4378-be3e-6afe7a3d6396/5-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics Behavior Flow Report - View Options" >}}

A little caveat with using the Behavior Flow reports, however: when looking at data for larger websites, such as those with millions of pageviews, sampling may occur. This sampling is set in place to help Google Analytics crunch through all the data in a specific amount of time. 

To minimize sampling, you can adjust the date range covered by the Behavior Flow report to reduce the amount of data that Google Analytics needs to analyze. In addition, you can also adjust the granularity of your analysis by clicking on the “Level of Detail” dropdown and setting it to “Show fewer connections.”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a68ad516-7777-4f21-a3f7-9e16bdbd0adc/6-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a68ad516-7777-4f21-a3f7-9e16bdbd0adc/6-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Adjust granularity in the Google Analytics Behavior Flow Report by selecting the 'Level of Detail' option. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a68ad516-7777-4f21-a3f7-9e16bdbd0adc/6-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics Behavior Flow Report - Level of Detail Options" >}}

If the Behavior Flow report is not enough, you can also set up Custom Reports in Google Analytics. To set these up, go to Customization > Custom Reports, then click the “New Custom Report” button. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab7acee1-22c5-4031-b04b-d5999add5753/7-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab7acee1-22c5-4031-b04b-d5999add5753/7-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Where to access Custom Reports in Google Analytics. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab7acee1-22c5-4031-b04b-d5999add5753/7-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics Custom Reports - How to access custom reports" >}}

Custom Reports can come in three different formats: 

- Explorer, which looks similar to the default Google Analytics reports.
- Flat Table.
- Map, best for geographic overlays.

You can also adjust the settings to filter based on specific metrics using exact match or regular expressions.

That said, some dimensions and metrics may appear off when combined with each other. This may be due to these metrics having different scopes--one metric may be measured at the user level, while another metric may be measured at the session (website visit) level. For more information about Google Analytics scopes, you can check out the Processing section of this [Google Analytics Help Center article](https://support.google.com/analytics/answer/2709828?hl=en).


## 5. Discover The Kinds Of User Behavior That Lead To Conversions And Which Actions Don’t

At the end of the day, a client or your employer is having a website made to achieve a tangible objective. This can be as diverse as selling your company’s products online (ecommerce), generating sign-ups for a service (lead generation), or even just to promote the company’s services (awareness).

That’s where the true strength of Google Analytics lies. By collecting data based on a combination of pageviews and different events, you can get more in-depth insights into what users actually do on your website. In addition, you can isolate specific key actions as conversions on your website by creating goals.

To do so, simply go to Admin > Goals, and then click New Goal. You can then choose from a template or set up a custom goal based on a destination ‘pageview of a specific page), events, duration, or even a number of pageviews.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eb25ac0-5c81-45d1-b751-669db16cf911/8-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eb25ac0-5c81-45d1-b751-669db16cf911/8-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Access goals in Google Analytics by going to Admin > Goals. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eb25ac0-5c81-45d1-b751-669db16cf911/8-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics Goals - Accessing Goals in Admin Section" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8ffa539-abc1-4850-8110-861d5f07bec6/9-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8ffa539-abc1-4850-8110-861d5f07bec6/9-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Set up conversions with Google Analytics goal settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8ffa539-abc1-4850-8110-861d5f07bec6/9-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics - Goal Settings" >}}

Once you’ve set up your goals, you can then use Google Analytics segments to analyze the actions that users with conversions have, versus those who did not convert. This is available by default &mdash; simply select the Converters or the Non-Converters segments to apply on your reports.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f8d0b70-098c-4ebd-a0ae-f087464344b3/10-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f8d0b70-098c-4ebd-a0ae-f087464344b3/10-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Google Analytics Segments: Selecting the Converters Segment. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f8d0b70-098c-4ebd-a0ae-f087464344b3/10-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics Segments: Selecting the Converters Segment" >}}

If you want more specific segments regarding conversions, you can click on the Actions option to copy the segment and add your own criteria. For example, you can add age, gender, location, or language for further filtering based on demographics. You can also create segments based on how users got to your site (source and medium), the device they’re using, or even based on the chain of actions they took on your site (under Advanced > Sequences).

Of course, you can always create segments from scratch in Google Analytics. Simply open the Segments dropdown then click on the red New Segment button to make your own.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11af2105-b172-47cb-9c6a-7d7efafd486c/11-google-analytics-web-developers-ui-ux-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11af2105-b172-47cb-9c6a-7d7efafd486c/11-google-analytics-web-developers-ui-ux-design.png" sizes="100vw" caption="Google Analytics Segments &mdash; Segment Options. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11af2105-b172-47cb-9c6a-7d7efafd486c/11-google-analytics-web-developers-ui-ux-design.png'>Large preview</a>)" alt="Google Analytics Segments - Segment Options" >}}

With all these features available for free, Google Analytics is truly one of the most powerful tools that any web developer or designer can utilize. However, adding these features to your site is just the tip of the iceberg. There are so many other functionalities there to explore, such as the Measurement Protocol that allows Google Analytics to collect data from IoT devices.

To know more about Google Analytics, you can check out these official Google resources:

- [Google Developers &mdash; Google Analytics Documentation](https://developers.google.com/analytics)
- [Analytics Help &mdash; Google Support](https://support.google.com/analytics/?hl=en#topic=3544906)
- [Google Analytics Academy](https://analytics.google.com/analytics/academy/course/6)

Lastly, before implementing Google Analytics, make sure to double-check the data privacy regulations in your region to avoid any unintentional violations. For more information about ensuring compliance with these regulations, please consult [this Google Support article](https://support.google.com/analytics/answer/6004245?hl=en&ref_topic=2919631).

By balancing the end user’s data privacy rights plus the need to collect data for actionable insights, Google Analytics is definitely one of the finest tools for UI/UX design that’s out in the market.

{{< signature "ra, yk, il" >}}
