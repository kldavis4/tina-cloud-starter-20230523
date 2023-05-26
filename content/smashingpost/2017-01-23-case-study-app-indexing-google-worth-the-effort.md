---
title: Is App Indexing For Google Worth The Effort? A Case Study
slug: case-study-app-indexing-google-worth-the-effort
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b7f6976-97f6-4146-8316-9c96b1147f5d/research-app-indexing-opt.png
date: 2017-01-23T21:31:34.000Z
author: bryson-meunier
description: >-
  Will the resources spent implementing app indexing for Google search be a boon
  or a bust for your app’s traffic? In this article, I’ll take you through a
  case study for app indexing at our company, the results of which may
  surprise you.
categories:
  - Mobile
  - Business
  - Apps
  - Analytics
  - SEO
---
<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b7f6976-97f6-4146-8316-9c96b1147f5d/research-app-indexing-opt.png" width="500" height="335" alt="App Indexing" title="Is App Indexing For Google Worth The Effort? A Case Study" /></figure>

App indexing is one of the hottest topics in SEO right now, and in some sense for good reason. Google has only been <a href="https://webmasters.googleblog.com/2014/06/android-app-indexing-is-now-open-for.html">indexing apps for everyone</a> for a little more than two years, and <a href="https://searchengineland.com/searchmetrics-study-shows-most-apps-not-utilizing-google-app-indexing-api-244432">with only 30% of apps being indexed</a> there is huge potential for websites to draw additional search traffic to their apps.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Keep Your Google Analytics Data Safe And Clean](https://www.smashingmagazine.com/2012/04/keep-your-analytics-data-safe-and-clean/)
*   [Targeting Mobile Users Through Google AdWords](https://www.smashingmagazine.com/2014/08/targeting-mobile-users-through-google-adwords/)
*   [Technical SEO 2015: Wiring Websites for Organic Search](https://www.smashingmagazine.com/2015/11/technical-seo-2015-wiring-websites-organic-search/)
*   [SEO For Responsive Websites](https://www.smashingmagazine.com/2013/11/seo-for-responsive-websites/)

{{% feature-panel %}}

What’s more, Google has given <a href="https://searchengineland.com/google-adds-additional-ranking-boost-for-using-app-indexing-api-232018">not one but two ranking boosts</a> to websites that use app indexing and the <a href="https://firebase.google.com/docs/app-indexing/android/activity">app indexing API</a>; so, implementing app indexing for your website is likely to increase your search traffic.

However, when we did it, it was a bust. We <strong>got a lot more app traffic from Google search</strong> when we implemented app indexing, but it was so little traffic compared to web search at that point that it was almost not worth the effort. Read on to learn more about what we did and what effect it had on our overall traffic.</p>

## What Is App Indexing?

If you’re not familiar with <a href="https://firebase.google.com/docs/app-indexing/">app indexing</a>, it is basically the process by which your app appears in Google search results alongside relevant web results. By supporting HTTP URLs in your app and adding the App Indexing SDK, you allow Google to crawl and index your app as it would a web page, and you enable users to install or launch your app from search results when they search with relevant keywords.

If the app is already installed, you’ll see a button to launch it in the relevant search results:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9232fcb2-bf98-4e20-a7a4-18987e26bee9/view-of-an-indexed-app-on-a-nexus-6p-running-android-7.0-large-opt"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/820b913e-f4e7-485b-89d1-82786cadd9e7/view-of-an-indexed-app-on-a-nexus-6p-running-android-7.0-preview-opt" alt="View of an indexed app on a Nexus 6P running Android 7.0 when the app is installed on the device." width="250" height="" /></a><figcaption>View of an indexed app on a Nexus 6P running Android 7.0 when the app is installed on the device. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9232fcb2-bf98-4e20-a7a4-18987e26bee9/view-of-an-indexed-app-on-a-nexus-6p-running-android-7.0-large-opt">View large version</a>)</figcaption></figure>

If the searcher doesn’t have the app installed yet, they will see an “Install” button in search results:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f71cd510-12e7-436d-abcc-8e2b226b69e4/view-of-an-indexed-app-on-a-nexus-6p-running-android-7.0-when-the-app-is-not-installed-on-the-device-large-opt"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e722b0c-29f1-4a38-9a35-517cd44d9aae/view-of-an-indexed-app-on-a-nexus-6p-running-android-7.0-when-the-app-is-not-installed-on-the-device-preview-opt" alt="View of an indexed app on a Nexus 6P running Android 7.0 when the app is not installed on the device." width="250" height="" /></a><figcaption>View of an indexed app on a Nexus 6P running Android 7.0 when the app is not installed on the device. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f71cd510-12e7-436d-abcc-8e2b226b69e4/view-of-an-indexed-app-on-a-nexus-6p-running-android-7.0-when-the-app-is-not-installed-on-the-device-large-opt">View large version</a>)</figcaption></figure>

Theoretically, this is great for users because they can find relevant authoritative content in Google regardless of whether they prefer websites or apps, and it’s great for app developers and marketers because it allows apps to be exposed to a whole new audience outside of the app store, potentially increasing app usage and downloads. But “theoretically” doesn’t necessarily mean that app indexing brings a lot of real traffic from search.

While I have seen a lot of great info on <a href="https://searchengineland.com/smx-advanced-recap-advanced-google-app-deep-linking-253134">how</a> and <a href="https://searchengineland.com/app-indexing-new-frontier-seo-app-packs-app-store-search-242319">why</a> to implement app indexing, I haven’t yet seen a case study on the benefits of app indexing in terms of traffic (though Google does highlight <a href="https://firebase.google.com/docs/app-indexing/partners/case-study-one-pager.pdf">several other benefits</a>). So, I looked at our app indexing traffic at Vivid Seats so that marketers, developers and webmasters can get a better sense of how much traffic, realistically, they can expect from getting their app indexed.

I want to start the case study with a small caveat: <a href="https://www.vividseats.com/">Vivid Seats</a> is the largest independent ticket marketplace, and the number-three resale marketplace behind StubHub and Ticketmaster, <a href="https://www.bloomberg.com/gadfly/articles/2016-06-22/stubhub-ebay-s-next-ticket-to-ride">according to Bloomberg</a>. As such, we get a lot of web traffic. A website that doesn’t get as much web traffic as we do or an app that has no equivalent website will probably have different results than ours — especially if it’s in a different industry. That said, a lot of large websites might see similar results and might want to adjust their strategy accordingly.

This is also an Android-only case study, because we haven’t yet been given access to the iOS app-indexing beta in Google’s <a href="https://www.google.com/webmasters/">Search Console</a>, and we don’t have the same kind of visibility into our iOS app’s indexing and ranking.</p>

## Background

Vivid Seats has had an <a href="https://www.vividseats.com/app">Android app</a> indexed since September of 2015. However, Google had a difficult time finding the equivalent app URI for our web pages at first, and in February of this year we had about 18 app URIs indexed and more than 35,000 pages with the <a href="https://support.google.com/webmasters/answer/6216428?hl=en">“Intent URI not supported” error</a>. We had had different URIs for our app than for our website at the time, which was making it difficult for Google to find equivalent pages.

## Solution

Initially, we tried to add alternate tags to our web pages pointing to the equivalent app URIs, as instructed by <a href="https://developer.android.com/training/app-indexing/enabling-app-indexing.html">Google’s help section on the subject</a>.

For example, <a href="https://www.vividseats.com/concerts/adele-tickets.html">Adele’s Vivid Seats page</a> — <code>https://www.vividseats.com/concerts/adele-tickets.html</code> — had the following <code>rel="alternate"</code> tag, which was dynamically served to mobile user agents and which pointed to the equivalent app URI:

<pre><code class="language-markup">&lt;link rel="alternate" href="android-app://com.vividseats.android/vividseats/performer/15313"&gt;</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e01ee951-f861-4fe7-b031-9d253e1fa1b5/adele-tickets-alternate-tag-app-uri-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e01ee951-f861-4fe7-b031-9d253e1fa1b5/adele-tickets-alternate-tag-app-uri-preview-opt.png" alt="Mobile view of Adele's tickets page." width="250" height="" /></a><figcaption>Mobile view of Adele’s tickets page. (Image: Fawaad Ahmad)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e221039b-4a08-46eb-acd0-8767f4aeb943/adele-tickets-alternate-tag-code-view-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e221039b-4a08-46eb-acd0-8767f4aeb943/adele-tickets-alternate-tag-code-view-preview-opt.png" alt="View of the code for the same page with the alternate tag highlighted." width="400" height="524" /></a><figcaption>View of the code for the same page with the alternate tag highlighted. (Image: Fawaad Ahmad)</figcaption></figure>

We were initially hopeful that this solution would be all that was necessary, because Google recommended it in its help section as a solution to this problem. Unfortunately, weeks after implementation, it was clear that Google was still having a difficult time figuring it out, and it didn’t index many more app URIs.

And the crawl errors persisted because Google was assuming that a lot of web pages on our website had equivalent app views, which at the time wasn’t the case.

We <a href="https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html">supported universal links</a> in our iOS app and <a href="https://firebase.google.com/docs/app-indexing/android/app">HTTP URLs in Android</a> in April, which reduced the number of errors from 40,000 at its apex to about 85 today. As a result, we have seen the number of app URIs indexed go from 18 in February to about 35,000 today.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eddf4713-b1cb-417a-bfab-b96785c5f4dd/universal-links-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86c894f9-d803-4068-afdd-03bf1e603813/universal-links-preview-opt.jpg" alt="Screenshot of Search Console Crawl Status report from 5/31/2016 which shows the effect of implementing HTTP URLs in Android on pages with errors and pages indexed." width="500" height="195" /></a><figcaption>Screenshot of Search Console’s “Crawl Status” report from 31 May 2016, which shows the effect of implementing HTTP URLs in Android on pages with errors and pages indexed. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eddf4713-b1cb-417a-bfab-b96785c5f4dd/universal-links-large-opt.jpg">View large version</a>)</figcaption></figure>

To do this, we simply followed the procedure <a href="https://firebase.google.com/docs/app-indexing/android/app">outlined in the Firebase documentation</a>:

*   We made sure that each type of link on our website had an equivalent view and corresponding URI in our Android app. To do this, we designed templates for page types that were not included in our app previously, and we built them in our Android app. The unique information on each page is dynamically served from our RESTful endpoint, so it’s only necessary to design and code the templates, not individual pages.
*   We verified our website in Search Console and associated it with our website, since our website isn’t in SSL, as required by Digital Asset Links.
*   We [added an intent filter](https://developer.android.com/studio/write/app-link-indexing.html#intent) in our Android manifest file.
*   We called `getIntent` in the `onCreate` code and deployed the app to the Play store.</p>

## Results

Predictably, clicks and impressions grew exponentially from December, when 18 app URIs were indexed, to September, when 40,000 app URIs were indexed. Overall, clicks grew 919%, with clicks from non-brand queries (i.e. informational queries that don’t mention Vivid Seats, like “packers tickets”) growing 5,500%. The clickthrough rate (CTR) went down, predictably, as a result of the increase in impressions, specifically non-brand ones.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57ae21d-13e8-4b3e-a0e1-8c5c9d2888fb/traffic-growth-post-app-indexing-vivid-seats-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/115d8bd9-cc34-4388-911f-2535305f3fac/traffic-growth-post-app-indexing-vivid-seats-preview-opt.png" alt="Clicks to app from Google search grew 919% after getting additional URLs indexed, with non-brand traffic growing 5500%." width="500" height="75" /></a><figcaption>Traffic to the app from Google search grew 919% after getting additional URLs indexed, with non-brand traffic growing 5500%. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57ae21d-13e8-4b3e-a0e1-8c5c9d2888fb/traffic-growth-post-app-indexing-vivid-seats-large-opt.png">View large version</a>)</figcaption></figure>

While app traffic (defined in Search Console as “clicks”) grew exponentially as a result of the increase in app URIs getting indexed, relative to the website traffic, app traffic has been underwhelming to date.

Even with an additional 40,000 app URIs indexed, 99.82% of our traffic from search currently goes to web pages, with just 0.23% of total search traffic going to our app URIs.

A few reasons why this might be so low:

*   Android traffic is a lower percentage of our mobile traffic than iOS, which isn’t included in this study.
*   We also have fewer app pages indexed than web pages — more than three times fewer, in fact. Because we grew traffic exponentially by having more app URIs indexed, there’s probably more traffic out there to be had that we will see when Google finally indexes all of our app URIs.
*   But the biggest reason is that CTRs vary dramatically for app listings and web listings. Our brand term, which we usually rank in position 1 and for which we usually get around a 40% CTR on the web, has a CTR of less than 1% for the app equivalent. This suggests that, though the app buttons are prominent in Google for navigational terms, most people still prefer to click through to the website.

This last point could just be a matter of this being fairly new technology and searchers not fully understanding the new layout, and we could imagine this trend reversing sometime in the future. For now, however, it’s important that this point is understood by all who are looking to index their app pages in search results. It’s tempting to think that the presence of a large colorful button in search results will increase the CTR and traffic, but our research hasn’t found any evidence to support this.

In fact, we found just the opposite: The CTR to app content is less than half of what it is to web content, with our Android app pages getting a CTR of 1.55%, at an average position of 5.1, compared to our web content CTR of 4.67%, two positions below our app content, at 7.6.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a158d713-5009-4dd4-9b68-36cbfbd39f27/overall-ctr-by-content-type-web-and-apps-search-console-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28dddf93-3c26-43ee-a137-b218d303d4bc/overall-ctr-by-content-type-web-and-apps-search-console-preview-opt.png" alt="Breakdown of the CTR across all content types, as reported by Search Console." width="500" height="129" /></a><figcaption>Breakdown of the CTR across all content types, as reported by Search Console. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a158d713-5009-4dd4-9b68-36cbfbd39f27/overall-ctr-by-content-type-web-and-apps-search-console-large-opt.png">View large version</a>)</figcaption></figure>

Though app content in general has a lower CTR than web content, we found that navigational (or branded) search terms actually have a lower CTR for us than informational terms, which is the opposite of how it works for web content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80853848-e279-4ff6-9264-834c90dc42a1/brand-vs-non-brand-ctr-apps-web-preview-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80853848-e279-4ff6-9264-834c90dc42a1/brand-vs-non-brand-ctr-apps-web-preview-opt.png" alt="Branded navigational terms drove much less traffic to apps than web pages." width="330" height="118" /></a><figcaption>Branded navigational terms drove much less traffic to apps than to web pages. (Image: Bryson Meunier)</figcaption></figure>

56% of the app traffic we received came from branded queries, compared to just 40% of our web traffic.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfb549dd-40c7-414a-b1f6-55e79b9d4390/brand-non-brand-traffic-apps-web-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8bd6826-35f1-4e48-b0e5-9570e02682fb/brand-non-brand-traffic-apps-web-preview-opt.png" alt="The CTR varies significantly for web and app traffic by query type." width="500" height="71" /></a><figcaption>The CTR varies significantly for web and app traffic by query type. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfb549dd-40c7-414a-b1f6-55e79b9d4390/brand-non-brand-traffic-apps-web-large-opt.png">View large version</a>)</figcaption></figure>

Looking deeper into query type, we broke down queries into two distinct types: first, navigational queries that mention our brand (for example, “vivid seats”) and informational queries that don’t (for example, “packer tickets”), and secondly, queries that indicate the searcher is looking for a website (for example, “www.vividseats.com”) or an app (for example, “download vivid seats app”) specifically.

If the searcher hadn’t indicated in their query that they were looking for an app or a website, we recorded that the query was branded or not, and that the website or app preference was “Not Specified.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b66cd6b-30c6-4386-9023-a0b247e5a0f7/brand-device-breakdown-app-web-queries-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c08bc52d-cbe3-415e-8178-8c64fe34195a/brand-device-breakdown-app-web-queries-preview-opt.jpg" alt="In this chart of app and web impressions and traffic to Vivid Seats from Google search, 93% of web impressions came from non-brand queries that didn't specify an app or website preference, compared to just 12% for the same category in app impressions." width="500" height="108" /></a><figcaption>In this chart of app and web impressions and traffic to Vivid Seats from Google search, 93% of web impressions came from non-brand queries that didn’t specify an app or website preference, compared to just 12% for the same category in app impressions. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b66cd6b-30c6-4386-9023-a0b247e5a0f7/brand-device-breakdown-app-web-queries-large-opt.jpg">View large version</a>)</figcaption></figure>

4% of total app traffic specified that they’re looking for an app, compared to less than 1% for web traffic. This is important traffic to be aware of, because it doesn’t have an equivalent on the desktop, and it could be a new query type to optimize for, but it’s not representative of app traffic. The great majority of queries for both web (99%) and app (96%) do not use qualifiers to describe whether the searchers are looking for an app or website specifically.

The traffic to app content from search has so far been underwhelming, but the real reason most developers would index their app content would be to drive downloads.

Fortunately, with Search Console, we can see installations from search as well. It’s kind of hidden in the Search Console reports; to see it, go to “Search analytics” → “Search appearance” → “Filter search appearance” → “Install app button.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8ec7558-06b8-4c90-ab30-1cd634aa0e25/search-analytics-google-search-performance-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/655714ab-196c-404e-84ba-8f1d0bd7a350/search-analytics-google-search-performance-preview-opt.png" alt="View of Install App Button filter within Google Search Console's Search Analytics Report." width="500" height="135" /></a><figcaption>View of “Install app button” filter in Search Console’s “Search Analytics” report. (Image: Bryson Meunier) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8ec7558-06b8-4c90-ab30-1cd634aa0e25/search-analytics-google-search-performance-large-opt.png">View large version</a>)</figcaption></figure>

When we did that, we found that just 0.03% of our total search traffic led to an app installation from search in the last 90 days.

But when you take the total number of installations from the last 90 days and compare it to the installations we’ve gotten from search, it’s clear that about 2% of our total Android downloads came from users installing the downloads in search results. This isn’t terribly impressive, but when you consider that this represents many app installations from search that we may not have had otherwise, it justifies for us the little bit of work it took to implement it.

## Summary

If your resources are limited and you’re wondering if app indexing would deliver enough traffic and installations to justify the effort, our experience would suggest you should focus on web content instead. Even after growing our traffic from app indexing by 919%, web content still brings in more than 99.8% of the total traffic from search to our website. If you’re considering other high-value projects, you might want to do those instead.

Still, if you only have an app to index, or if you have resources on your team, then app indexing does bring traffic that you wouldn’t get otherwise, and it might be worth the long-term benefits to your website and to Google users.

Have you implemented app indexing with similar (or dissimilar) results? I’d love to hear about it in the comments.

Many thanks to the UX design and development group at Vivid Seats, including Fawaad Ahmad, who made a lot of this happen.

{{< signature "da, vf, il, yk, al" >}}

<em>Front page image credits: <a href="https://www.youtube.com/watch?v=C35OSHlTNwA">Introducing Firebase App Indexing</a></em>

