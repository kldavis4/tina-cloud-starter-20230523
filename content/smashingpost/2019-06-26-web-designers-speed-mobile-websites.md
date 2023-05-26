---
title: 'What Web Designers Can Do To Speed Up Mobile Websites'
slug: web-designers-speed-mobile-websites
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a024e13c-72db-448f-bd62-6a1bacfeb197/design-speed-river-north-hotel-pwa.png
date: 2019-06-26T14:00:59+02:00
summary: >-
  Web developers know what they’re doing in terms of optimizing a website for page speed, but is it enough in Google’s eyes? When it comes to mobile loading speeds, your website can always be faster. And if you’ve implemented all of the caching, minification and other optimizations you possibly can, it’s time for the web designer to step in and get creative.
description: >-
  Web developers know what they’re doing in terms of optimizing a website for page speed, but is it enough in Google’s eyes? When it comes to mobile loading speeds, your website can always be faster. Find out how.
categories:
  - Mobile
  - Performance
  - Optimization
---
I recently wrote a blog post for a web designer client about page speed and why it matters. What I didn’t know before writing it was that her agency was struggling to optimize their mobile websites for speed. As a result, she came back to me concerned with publishing a post on a strategy her agency had yet to adopt successfully.

She was torn though. She understood how important mobile page speeds were to the user experience and, by proxy, SEO. However, their focus has always been on making a great-looking and effective design. Something like page speed optimization was always left to the developers to worry about. 

In the end, we decided to hold on publishing it until they could get their own website as well as their clients’ sites properly optimized. In the meantime, it got me thinking: 

**Is there anything designers can do when creating mobile websites to help developers optimize for speed?**

Developers are already [optimizing front end performance](https://www.smashingmagazine.com/2019/01/front-end-performance-checklist-2019-pdf-pages/) with: 

*   Fast web hosting
*   CDNs
*   Clean coding practices
*   [Caching](https://www.smashingmagazine.com/2018/12/caching-smartly-gutenberg/ )
*   Minification
*   Image optimization
*   And more

So, is there anything left? 

To me, this is a lot like how search optimization is handled. As a writer, I take care of the on-page optimizations while the developer I hand content over to does the technical SEO stuff. Web designers and developers can easily tackle the parts of speed optimization that are in each of their wheelhouses. 

{{% feature-panel %}}

## Understanding What “Slow” Means On The Mobile Web

There are a number of tools to help you analyze page speeds and implement various fixes to improve them. One tool that’s particularly helpful is called [Lighthouse](https://www.smashingmagazine.com/2018/04/mobile-first-optimization-tools/). The only thing is, it’s meant for web developers. 

Instead, I suggest that web designers use another Google testing tool called [Test My Site](https://www.thinkwithgoogle.com/feature/testmysite). 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea981ffb-2632-46cd-b4df-a2b270f99003/design-speed-test-my-site.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea981ffb-2632-46cd-b4df-a2b270f99003/design-speed-test-my-site.jpg" sizes="100vw" caption="Test My Site is a mobile page speed testing tool from Think with Google. (Source: <a href='https://www.thinkwithgoogle.com/feature/testmysite'>Test My Site</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea981ffb-2632-46cd-b4df-a2b270f99003/design-speed-test-my-site.jpg'>Large preview</a>)" alt="Test My Site speed test" >}}

This is strictly for those who want to get a quick evaluation of their **mobile site speed**. All you need to do is enter your domain name into the field and let the test run. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3109e56b-977c-404b-8de7-d0a08562d243/design-speed-test-my-site-score.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3109e56b-977c-404b-8de7-d0a08562d243/design-speed-test-my-site-score.jpg" sizes="100vw" caption="An example of your page speed test results from Test My Site. (Source: <a href='https://www.thinkwithgoogle.com/feature/testmysite'>Test My Site</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3109e56b-977c-404b-8de7-d0a08562d243/design-speed-test-my-site-score.jpg'>Large preview</a>)" alt="Test My Site results example" >}}

What I like about this tool compared to other site speed tests is that it’s all spelled out for you in layman’s terms. In this case, my website is “slow”, even when served on 4G networks. Although we’ve been told for years that **visitors are willing to wait three seconds for a web page to load**, Google considers 2.9 seconds too long. (Which I wholeheartedly agree with.)

You can get an expanded report from Google that tells you how to speed up your mobile loading times, but the suggestions are no different than the updates you’d make on the development side. For example: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b4f9b58-6ae5-418c-9e20-c12df78279d8/design-speed-think-with-google-report.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b4f9b58-6ae5-418c-9e20-c12df78279d8/design-speed-think-with-google-report.jpg" sizes="100vw" caption="Think with Google suggests the typical page speed optimizations. (Source: <a href='https://www.thinkwithgoogle.com/feature/testmysite'>Test My Site</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b4f9b58-6ae5-418c-9e20-c12df78279d8/design-speed-think-with-google-report.jpg'>Large preview</a>)" alt="Think with Google report suggestions" >}}

We already know this. However, if you (or your developer) haven’t yet implemented any of these fixes, this is a good checklist to work off of. 

That said, I didn’t point you to this tool so you could keep doing the same optimizations over and over again, expecting the same result. What is it they always say about the definition of insanity? 

Instead, I think you should use this as a quick gut check: 

{{% pull-quote %}}
 Is my mobile site fast enough in Google’s eyes? No? Then, it won’t be fast enough in your visitors’ eyes either.
{{% /pull-quote %}}

And if you want to really drive that point home, scroll to the bottom of the Test My Site analysis page and run your numbers through the impact analysis calculator: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db5e8fd3-441b-4c91-bc7b-7318016d23e5/design-speed-test-my-site-impact-analysis.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db5e8fd3-441b-4c91-bc7b-7318016d23e5/design-speed-test-my-site-impact-analysis.jpg" sizes="100vw" caption="Test My Site’s revenue impact assessment.  (Source: <a href='https://www.thinkwithgoogle.com/feature/testmysite'>Test My Site</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db5e8fd3-441b-4c91-bc7b-7318016d23e5/design-speed-test-my-site-impact-analysis.jpg'>Large preview</a>)" alt="Test My Site revenue impact calculator" >}}

If you aren’t completely convinced that you need to take your 3-second mobile speed down any further, look at the financial impact just .5 seconds would have on your monthly bottom line. 

## What Web Designers Can Do To Optimize Mobile Sites For Speed

Let the web developer handle all of the necessary speed optimizations like caching and file minification while you take on the following design tips and strategies:

### 1. Host Fonts From A CDN

There’s enough you have to worry about when it comes to [designing fonts for the mobile experience](https://www.smashingmagazine.com/2018/06/reference-guide-typography-mobile-web-design/) that you probably don’t want to hear this… but custom web fonts suck when it comes to loading. In fact, there are two recent case studies that demonstrate why custom web fonts are detrimental to page loading speeds. 

Thankfully, a CDN could end up being your saving grace. 

#### The Downtime Monkey Example

The first comes from [Downtime Monkey](https://downtimemonkey.com/blog/how-we-boosted-page-load-speed.php). In this case study, Downtime Monkey boasts a page speed improvement of 58% through a variety of optimizations &mdash; two of which pertained to how they served fonts to their site. 

For their Font Awesome icons, they decided to host them from a CDN. However, Font Awesome’s own CDN proved unreliable, so they switched to the Bootstrap CDN. As a result, this **saved them between 200 and 550 milliseconds per page load**.

For their Google Font “Cabin”, they decided to host it from the Google CDN. What’s funny to note, however, is that when they ran a page speed test on the site afterwards, they received an optimization suggestion related to the font. 

It seems that the link they put in the head of their site was slowing down the rendering of the page. So, they had to implement a workaround that would allow the font to load asynchronously without harming the display of the page as it loaded. They used Web Font Loader to fix the issue and ended up **saving between 150 and 300 milliseconds per page load** as a result.

#### Brian Jackson’s Test

Brian Jackson, the Chief Marketing Officer at Kinsta, [wrote a post for KeyCDN](https://www.keycdn.com/blog/web-font-performance) that demonstrates the best way to serve custom web fonts on a website. 

You can see in his example that he suggests a number of optimizations, like limiting which styles and character sets are available for use on the website. However, it’s his experimentation with CDN hosting that’s really interesting. 

First, he isolated the most popular Google Fonts and tested how quickly they loaded through Google’s CDN: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c6f9f57-5fdb-4513-babe-23794b84847b/design-speed-keycdn-top-10.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c6f9f57-5fdb-4513-babe-23794b84847b/design-speed-keycdn-top-10.jpg" sizes="100vw" caption="Open Sans was the fast Google Font. (Source: <a href='https://www.keycdn.com/blog/web-font-performance'>KeyCDN</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c6f9f57-5fdb-4513-babe-23794b84847b/design-speed-keycdn-top-10.jpg'>Large preview</a>)" alt="Google font loading speeds" >}}

Open Sans loaded the fastest. 

But that shouldn’t automatically make Open Sans the best choice if you’re trying to speed up your website. After all, Opens Sans is a Google Font that has to be served from Google’s servers. When compared against Arial, a web-safe font that _isn’t_ pulled from an external source, this is what happened: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e9da06-d89d-42cd-a704-b2546cf59c2f/design-speed-keycdn-web-safe-font-vs-google-font.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e9da06-d89d-42cd-a704-b2546cf59c2f/design-speed-keycdn-web-safe-font-vs-google-font.jpg" sizes="100vw" caption="A comparison of loading speeds between Arial and Open Sans. (Source: <a href='https://www.keycdn.com/blog/web-font-performance'>KeyCDN</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e9da06-d89d-42cd-a704-b2546cf59c2f/design-speed-keycdn-web-safe-font-vs-google-font.jpg'>Large preview</a>)" alt="Arial vs Open Sans loading speeds" >}}

Arial beat Open Sans by almost 200 milliseconds. 

Before we move on, I’ll just say that this is one way to solve the slow-loading font dilemma: rather than use externally hosted fonts, use your system ones. **They might not be as exciting to design with, but they won’t force users to sit around and wait for your website to load, costing you visitors and customers in the process.**

You might be thinking that downloading and hosting your Google font would make more sense then. That way, you don’t have to compromise on which fonts you use and it’ll shave time off of their normal loading speeds. Right? 

Well, Brian was curious about that, too, so he did a test: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e31aa0ae-c45f-4cf8-8770-62542670083b/design-speed-keycdn-local-vs-google-cdn.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e31aa0ae-c45f-4cf8-8770-62542670083b/design-speed-keycdn-local-vs-google-cdn.jpg" sizes="100vw" caption="A comparison between Open Sans hosted locally vs. hosted on Google CDN. (Source: <a href='https://www.keycdn.com/blog/web-font-performance'>KeyCDN</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e31aa0ae-c45f-4cf8-8770-62542670083b/design-speed-keycdn-local-vs-google-cdn.jpg'>Large preview</a>)" alt="Opens Sans - local host vs Google CDN" >}}

When served from a local server, Open Sans took 0.530 milliseconds to load. It’s not a huge difference, but it’s obviously not the right direction to go in. 

So, what’s the conclusion? Well, you have a few options. 

1. You can use a web safe font and avoid the issues that come with using externally hosted fonts in the first place. 
2. You can use a Google font and make sure it’s hosted through Google’s CDN. 
3. You can download a Google font and upload it to your own CDN (if you can get it loading faster from there, that is). 

Either way, hosting your fonts and icons from a location where they’ll load more quickly can help you optimize your website for performance. 

{{% ad-panel-leaderboard %}}

### 2. Stop Using Cumbersome Design Elements

The following list is somewhat of a rehashing of topics that have been covered before, so I don’t want to waste your time trying to recreate the wheel here. However, I do think this strategy of removing unnecessary design elements (especially weightier ones) to optimize the mobile experience is one worth summarizing here: 

#### Stop with On-Page Ads

When I wrote about [elements you should ditch on mobile websites](https://www.smashingmagazine.com/2018/12/elements-ditch-repurpose-mobile/), I called out advertisements as one of the things you could easily toss out. I still stand by that conviction. 

For starters, advertisements are served from a third party. Any time you have to call on another party’s servers, you’re further increasing your own loading times as you wait for them to deliver the content to your page. 

Secondly, [over 26% of the U.S. population alone uses ad-blocking technology](https://www.statista.com/statistics/804008/ad-blocking-reach-usage-us/) on their devices, so they’re not likely to see your on-page ads anyway. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6781d02a-1045-4326-875e-6f2532d0539d/design-speed-statista-ad-blocking.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6781d02a-1045-4326-875e-6f2532d0539d/design-speed-statista-ad-blocking.jpg" sizes="100vw" caption="Statista data on the usage of ad-blocking technology in the U.S. (Source: <a href='https://www.statista.com/statistics/804008/ad-blocking-reach-usage-us/'>Statista</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6781d02a-1045-4326-875e-6f2532d0539d/design-speed-statista-ad-blocking.jpg'>Large preview</a>)" alt="Statista - ad-blocking tech data" >}}

Instead, use monetization methods that move the advertising away from your website, increase your own on-site conversions and won’t drain your server’s resources:

*   **Remarketing**  
Let your tracking pixel follow visitors around the web and then serve your own ads on someone else’s site. 
*   **PPC**  
There’s good money to be made if you can nail the pay-per-click advertising formula in Google. 
*   **Social media ads**  
These are especially easy to run if your site is publishing new content on a regular basis and you have a compelling offer. 

#### Stop With Pop-Ups

I know that Google says that [mobile pop-ups](https://www.smashingmagazine.com/2018/04/mobile-pop-up-ads/) are okay in certain instances. However, if you’re building a website with WordPress or another content management system and you’re using a plugin to create those pop-ups, that’s going to slow down your loading times. It might not be by much, but you’ll notice the difference. 

[ThemeIsle](https://themeisle.com/blog/plugins-affect-wordpress-performance/) decided to do some analysis of how certain plugins affect WordPress website speeds. Here is what happened when they tested the effects each of these plugins had on the loading time: 

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist"></th>
            <th>Base loading time (in seconds)</th>
            <th>Loading time after install (in seconds)</th>
            <th>Change in %</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Security plugins</td>
            <td>0.93 s</td>
            <td>1.13 s</td>
            <td>21.50%</td>
        </tr>
        <tr>
            <td>Backup plugins</td>
            <td>0.93 s</td>
            <td>0.94 s</td>
            <td>1.07%</td>
        </tr>
        <tr>
            <td>Contact form plugins</td>
            <td>0.93 s</td>
            <td>0.96 s</td>
            <td>3.22%</td>
        </tr>
        <tr>
            <td>SEO plugins</td>
            <td>0.93 s</td>
            <td>1.03 s</td>
            <td>10.75%</td>
        </tr>
        <tr>
            <td>E-commerce plugins</td>
            <td>0.93 s</td>
            <td>1.22 s</td>
            <td>31.10%</td>
        </tr>
    </tbody>
</table>

Granted, some plugins are coded to be more lightweight than others, but there will always be some sort of difference felt in your loading times. Based on this data, the difference could be as small as .01 and as much as .29 seconds.

If you know that pop-ups aren’t really kosher on the mobile web anyway, why push your luck? Instead, take that promotional offer, cookie notice or announcement and place it on your web pages. 

#### Stop With Cumbersome Contact Channels

Don’t forget about your website’s contact channels. In particular, you have to be careful about designing [mobile forms](https://www.smashingmagazine.com/2018/08/best-practices-for-mobile-form-design/). Of course, part of that has to do with how long it actually takes a user to fill one out. However, there’s also what a lengthy or multi-page form does to your loading speeds that you should think about. 

In general, your mobile forms should be lean &mdash; only include what’s absolutely necessary. 

There is an alternate school of thought to consider as well. 

You could ditch the contact form altogether, something I discussed when talking about the trend of [replacing mobile forms with chatbots](https://www.smashingmagazine.com/2019/05/chatbots-forms-mobile/). There are websites that have removed their forms and left information like FAQs, email addresses and phone numbers for visitors to use if they need to get in touch. That would certainly lighten things up from a loading standpoint. I just don’t know if it would be ideal for the user experience. 

{{% ad-panel-leaderboard %}}

### 3. Create A Single-Page Website

The above tips are going to be the simplest and quickest ones to implement, so you should definitely start there if a client or web developer comes to you with issues of too-slow websites. However, if page speed tests still show that a site takes more than 2.5 seconds to load, consider a different approach to redesigning a website for the purposes of speed optimization.

As Adam Heitzman said in [an article for Search Engine Journal](https://www.searchenginejournal.com/single-page-websites-good-bad-seo/190095/#close): 

<blockquote>“Single page sites typically convert much easier to mobile and users find them simple to navigate.”</blockquote>

But does that mean that a single-page website will always load more quickly than a multi-page website? Of course not. However, most professional designers choose a single-page design over multi-page for very specific purposes. [DevriX](https://devrix.com/tutorial/one-page-vs-multi-page-website/) has a nice graphic that sums this up: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81188ae0-2f74-488f-91d1-f0c9d61220aa/design-speed-devrix-single-page-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81188ae0-2f74-488f-91d1-f0c9d61220aa/design-speed-devrix-single-page-design.png" sizes="100vw" caption="DevriX sums up the limitations of single-page websites. (Source: <a href='https://devrix.com/tutorial/one-page-vs-multi-page-website/'>DevriX</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81188ae0-2f74-488f-91d1-f0c9d61220aa/design-speed-devrix-single-page-design.png'>Large preview</a>)" alt="DevriX graphic - single-page websites" >}}

To be clear, I’m not suggesting that you turn your website into a single-page application (SPA). If you want to speed up your client’s digital property with service workers, a PWA is a better solution. (More info on that in the next point.) 

Instead, what I’m suggesting is that you convert a multi-page website into a single-page one if your client fulfills certain criteria:

*   Businesses with an extremely narrow and singular focus. 
*   Websites that don’t require much content to get their point across. 
*   A limited range of keywords you need to rank for. 

That said, if you are designing a website that fits within those three criteria (or at least two out of three), you could realistically move your website to a more simplistic single-page design. 

Because single-page websites force you to do more with less, the limited content and features naturally create a lightweight website. Even if you did push the limits slightly, you could still create a faster-loading website for mobile as [Tempus](https://tempusturner.com.au/) does: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1594c5cf-0679-48e1-a720-93708c585400/design-speed-tempus-page-speed.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1594c5cf-0679-48e1-a720-93708c585400/design-speed-tempus-page-speed.jpg" sizes="100vw" caption="Test My Site reports that the Tempus website loads in 2.1 seconds. (Source: <a href='https://www.thinkwithgoogle.com/feature/testmysite'>Test My Site</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1594c5cf-0679-48e1-a720-93708c585400/design-speed-tempus-page-speed.jpg'>Large preview</a>)" alt="Test My Site report for Tempus" >}}

What’s cool about this single-page website is that it doesn’t skimp on the extensive imagery needed to sell luxury homes. And, yet, its mobile site loads in 2.1 seconds. 

On the other hand, not all single-page websites are built with speed in mind. Take developer [Davide Marchet](https://www.davidemarchet.com/)’s website:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11a5dbfb-fc3b-406a-9d2e-ad182637c186/design-speed-david-marchet-page-speeds.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11a5dbfb-fc3b-406a-9d2e-ad182637c186/design-speed-david-marchet-page-speeds.jpg" sizes="100vw" caption="Test My Site reports that Davide Marchet’s website loads in 5.4 seconds. (Source: <a href='https://www.thinkwithgoogle.com/feature/testmysite'>Test My Site</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11a5dbfb-fc3b-406a-9d2e-ad182637c186/design-speed-david-marchet-page-speeds.jpg'>Large preview</a>)" alt="Test My Site report for Davide Marchet" >}}

Because it’s overloaded with animations, it takes 5.4 seconds for the page to load on mobile. You can even see this from the screenshot presented by Think with Google. The image seen there is actually the message that appears while the first animation loads in the background. 

So, I would suggest being careful if you’re hoping to use a single-page design to solve your website’s performance woes. The design needs to be simple, super focused and unencumbered by scripts and animation effects that undo the benefits of trimming your content down to one page.

### 4. Turn Your Mobile Site Into A PWA

According to Google, there are [three characteristics that define every PWA](https://developers.google.com/web/progressive-web-apps/): 

1. Reliable
2. Fast
3. Engaging

Speed is an inherent part of [progressive web apps](https://www.smashingmagazine.com/2018/12/pwa-native-mobile-apps/) thanks to the service workers they’re built with. Because service workers exist outside of the web browser and are not contingent on the speed of the user’s network, they load cached content for visitors more quickly. 

I would also say that because the design of a PWA more closely resembles that of a native mobile app (at least the shell of it), this forces the design itself to be more trimmed-back than a mobile website.

If you’re struggling to speed up your website after implementing all of the traditional performance optimizations you’re supposed to, now would be a good time to turn your mobile website into a PWA. 

Let me show you why: 

Imagine you are planning a trip to Chicago with a friend. You’re out at a bar or coffee shop discussing the trip, then realize you have no idea where to stay. So, you do a search for “downtown Chicago hotels” on one of your smartphones. 

You’re not thinking about purchasing a room yet; you just want to research your options. So, you click on the website links for two of the top listings Google provides you. 

This is the progressive web app for the [Best Western River North Hotel](https://www.rivernorthhotel.com/):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a024e13c-72db-448f-bd62-6a1bacfeb197/design-speed-river-north-hotel-pwa.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a024e13c-72db-448f-bd62-6a1bacfeb197/design-speed-river-north-hotel-pwa.png" sizes="100vw" caption="The home page of the Best Western River North Hotel PWA. (Source: <a href='https://www.rivernorthhotel.com/'>Best Western River North Hotel</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a024e13c-72db-448f-bd62-6a1bacfeb197/design-speed-river-north-hotel-pwa.png'>Large preview</a>)" alt="River North Hotel PWA" >}}

This is the website of the [Palmer House Hilton](https://www.palmerhousehiltonhotel.com/), a nearby hotel in downtown Chicago: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9d24d2-ca88-45dd-a260-ebb77ce39a0d/design-speed-palmer-house-hilton-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9d24d2-ca88-45dd-a260-ebb77ce39a0d/design-speed-palmer-house-hilton-website.png" sizes="100vw" caption="The home page of the Palmer House Hilton website. (Source: <a href='https://www.palmerhousehiltonhotel.com/'>Palmer House Hilton</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9d24d2-ca88-45dd-a260-ebb77ce39a0d/design-speed-palmer-house-hilton-website.png'>Large preview</a>)" alt="Palmer House Hilton website" >}}

For starters, the PWA is a much better looking and easier to navigate on your smartphone, so it’s going to win major points there. There’s also the matter of speed:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/060331f5-d1b6-4318-b5e3-efee15c158fb/design-speed-hotel-speed-comparison.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/060331f5-d1b6-4318-b5e3-efee15c158fb/design-speed-hotel-speed-comparison.jpg" sizes="100vw" caption="Test My Site compares the two competing hotels’ loading speeds. (Source: <a href='https://www.thinkwithgoogle.com/feature/testmysite'>Test My Site</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/060331f5-d1b6-4318-b5e3-efee15c158fb/design-speed-hotel-speed-comparison.jpg'>Large preview</a>)" alt="Test My Site website speed comparison" >}}

The River North Hotel loads in 2.4 seconds on mobile whereas its Hilton competitor loads in 4 seconds. (You can actually see in the Hilton screenshot that the site hadn’t completely loaded yet.) That’s a difference that visitors are sure to notice.

Even if we’re not doing a side-by-side comparison between the competing websites, the River North Hotel’s PWA blows its former mobile website out of the water. 

[Brewer Digital Marketing](https://www.brewerdigitalmarketing.com/blog/case-study-bw-river-north), the agency that developed the PWA for them, shared what happened after they made the switch over. The hotel saw a 300% increase in earnings and a 500% increase in nights booked with the PWA. 

### 5. Convert Your Website Or Blog Into AMP

We have Google to thank for another speedy design trick for the mobile web. This one is called Accelerated Mobile Pages, or AMP, for short. 

Initially, AMP was released to help publishers strip down their blog or news pages for faster loading on mobile devices. However, AMP is a web component framework you can use to design whole websites or just specific parts of them (like blog posts). Once implemented, pages load almost instantaneously from search.

Why is AMP so fast to load? There are a number of reasons:

[With AMP](https://amp.dev/about/how-amp-works), you can only load asynchronous JavaScript and inline CSS on your website, which means that your code won’t block or delay page rendering. 

Images are also another source of slower loading times. However, AMP solves that issue by automatically loading the page layout before the resources (e.g. images, ads, etc.) Think of it as a form of lazy loading. 

There’s a lot more to it, but the basic idea is that it cuts out the elements that tend to drag websites down and forces designers to mostly depend on lightweight HTML to build their pages. 

If you want to see an example of this in action, you can look at pretty much any leading digital magazine or news site. If you’re unfamiliar with AMP content, simply look for the lightning bolt icon that appears next to the web page name in Google search. Like this: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cd1ae26-d139-42fd-ac90-830ee2741540/design-speed-amp-lightning-bolt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cd1ae26-d139-42fd-ac90-830ee2741540/design-speed-amp-lightning-bolt.png" sizes="100vw" caption="Pages with the recognizable lightning bolt symbol were created using Google AMP. (Source: <a href='https://amp.dev/'>Google AMP</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cd1ae26-d139-42fd-ac90-830ee2741540/design-speed-amp-lightning-bolt.png'>Large preview</a>)" alt="The AMP lightning bolt symbol in search" >}}

[Gizmodo](https://gizmodo.com/) is a good example of AMP content: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e62a7de-26ae-40e7-8989-ec39602550de/design-speed-gizmodo-amp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e62a7de-26ae-40e7-8989-ec39602550de/design-speed-gizmodo-amp.png" sizes="100vw" caption="This Gizmodo AMP page loaded almost instantly from search results. (Source: <a href='https://gizmodo.com/'>Gizmodo</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e62a7de-26ae-40e7-8989-ec39602550de/design-speed-gizmodo-amp.png'>Large preview</a>)" alt="Gizmodo AMP" >}}

In fact, when [Gizmodo made the transition to AMP](https://amp.dev/success-stories/gizmodo) back in 2016, it saw huge lifts in terms of performance. Its page speeds increased by 300% and it got 50% more page impressions as a result. 

If you really want to get the most out of AMP speeds, [Mobify suggests pairing AMP with your PWA](https://resources.mobify.com/2018Q2MobileCommerceInsightsReport.html). That way, you can load your web pages lightning-fast for visitors: 

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <caption class="center red"><strong>First Page Load With AMP</strong></caption>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">Percent of Websites</th>
            <th>Load Time (seconds)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>10%</td>
            <td>0.3</td>
        </tr>
        <tr>
            <td>20%</td>
            <td>0.5</td>
        </tr>
        <tr>
            <td>50%</td>
            <td>1.1</td>
        </tr>
        <tr>
            <td>60%</td>
            <td>1.4</td>
        </tr>
        <tr>
            <td>80%</td>
            <td>2.2</td>
        </tr>
        <tr>
            <td>90%</td>
            <td>3.4</td>
        </tr>
        <tr>
            <td>95%</td>
            <td>5.2</td>
        </tr>
    </tbody>
</table>
<p class="center">Mobify reports on the loading times of AMP (Source: <a href="https://resources.mobify.com/2018Q2MobileCommerceInsightsReport.html">Mobify</a>)</em></p>

Then, sustain those fast-loading times with the PWA: 

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <caption class="center red"><strong>Subsequent Page Loads On PWA</strong></caption>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">Percent of Websites</th>
            <th>Load Time (seconds)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>10%</td>
            <td>0.6</td>
        </tr>
        <tr>
            <td>20%</td>
            <td>0.8</td>
        </tr>
        <tr>
            <td>50%</td>
            <td>1.4</td>
        </tr>
        <tr>
            <td>60%</td>
            <td>1.8</td>
        </tr>
        <tr>
            <td>80%</td>
            <td>3.0</td>
        </tr>
        <tr>
            <td>90%</td>
            <td>4.5</td>
        </tr>
        <tr>
            <td>95%</td>
            <td>6.2</td>
        </tr>
    </tbody>
</table>
<p class="center"><em>Mobify reports on the loading times of PWAs (Source: <a href="https://resources.mobify.com/2018Q2MobileCommerceInsightsReport.html">Mobify</a>)</></em></p>

Just be careful with AMP and PWAs. 

Look at the tables above and you’ll see that some sites have implemented these speedy design tactics and they still don’t beat Google’s 2.5-second benchmark for mobile loading. Just because there is a promise of faster-loading web pages with both, that doesn’t necessarily mean your website will automatically be lightning-fast. 

## Wrapping Up

As Google does more to reward mobile websites over desktop, this isn’t really a matter you can table for much longer. All versions of your website &mdash; but mobile especially &mdash; must be optimized for the user experience. 

That means the design, the code, the content and everything else within and around it must be optimized. Once the developer has taken care of the traditional performance optimizations to speed up the website, it’s time for the designer to make some changes of their own. In some cases, simple changes like how fonts are served through the website will help. In other cases, more drastic matters may need to be considered, like redesigning your website as a PWA. 

First, consider how slowly your client’s website is loading. Then, examine what’s causing the biggest issue on mobile. Trim the fat, bit by bit, and see what you can do as a designer to complement the developer’s technical speed optimizations.

{{< signature "ra, il" >}}