---
title: 'Reducing The Web’s Carbon Footprint: Optimizing Social Media Embeds'
slug: reducing-web-carbon-footprint-optimizing-social-media-embeds
author: michelle-barker
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/686a0218-bea0-4a0e-a2b9-aca40c29d412/reducing-web-carbon-footprint-optimizing-social-media-embeds.jpg
date: 2022-02-03T12:00:00.000Z
summary: >-
  In this article, we’ll look specifically at what we can do to reduce the impact of social media embeds and social sharing widgets &mdash; or even some strategies to avoid them altogether. While the spotlight is on reducing the environmental impact, many of these tips will be great for performance too.
description: >-
  In this article, we’ll look specifically at what we can do to reduce the impact of social media embeds and social sharing widgets &mdash; or even some strategies to avoid them altogether. While the spotlight is on reducing the environmental impact, many of these tips will be great for performance too.
categories:
  - UI
  - User Interaction
  - Performance
  - Optimization
---

The [COP26](https://ukcop26.org/) climate conference has thrown into a sharp light the importance of reducing carbon emissions in every area of our lives. Everyone can play a role in this, including those of us working on the web.

Measuring the carbon footprint of the web isn’t an exact science, but a [report by the BBC](https://www.bbc.com/future/article/20200305-why-your-internet-habits-are-not-as-clean-as-you-think) in 2020 estimates that all internet activity accounts for around 3.7% of global emissions (similar to the airline industry), and rising. The average web page size has been increasing steadily for years and is currently just over 2MB (according to [HTTP Archive](https://httparchive.org/reports/page-weight)), and much of that increase can be attributed to Javascript. This is clearly not just bad for the environment &mdash; it’s bad for performance and hurts our users too. But calculating carbon emissions takes into account much more than bytes over the wire: there’s the power used in development, the data centers that host our files, the power consumed by the end users’ devices, and more.

There’s a lot we can do to mitigate the environmental impact of the sites we build. Check out [this article](https://thoughtbot.com/blog/so-you-wanna-create-an-eco-friendly-website) by Eric Bailey for some ideas. For this article, we’re going to take a deeper dive into one particular area.

## The Impact Of Social Media Embeds

Third-party Javascript accounts for a lot of bloat on websites, with analytics, chatbots, and embedded widgets being common contributors. While working on a site recently, I noticed that an embedded YouTube video loaded around 600kB of JS for any visitor *regardless of whether that user even chose to watch the video*. This seems wasteful. I also became interested in [this analysis](https://fershad.com/writing/cop26-a-quick-sustainability-check/) of the COP26 website by Fershad Irani, which shows many things that could be improved to reduce the site’s (relatively large) carbon footprint.

Redesigning the social media coverage is briefly mentioned as one way to save approximately 1.4MB. However, when I visited the site, the amount of JS seemingly loaded from the Twitter feed section was higher even. On closer inspection, it appeared that other content embedded *within* tweets (video in particular) was contributing to this.

To analyze the impact of various types of embed, I’ve measured the JS loaded and [total blocking time](https://web.dev/tbt/) (TBT) on a mobile connection for a simple HTML page with some common embeds. The performance impact is be measured with [PageSpeed Insights](https://pagespeed.web.dev/). There’s also the number of requests to consider, which for a single Twitter embed is *a lot*.

### Twitter

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Description</th>
			<th>JS (uncached)</th>
      <th>TBT</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Single embed</td>
			<td>369 KB</td>
      <td>450 ms</td>
		</tr>
    <tr>
			<td>Two embeds</td>
			<td>736 KB</td>
      <td>1820 ms</td>
		</tr>
    <tr>
			<td>With video</td>
			<td>532 KB</td>
      <td>990 ms</td>
		</tr>
	</tbody>
</table>

### Instagram

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Description</th>
			<th>JS (uncached)</th>
      <th>TBT</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Single embed</td>
			<td>381 KB</td>
      <td>0 ms</td>
		</tr>
    <tr>
			<td>Two embeds</td>
			<td>630 KB</td>
      <td>180 ms</td>
		</tr>
	</tbody>
</table>

### YouTube

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Description</th>
			<th>JS (uncached)</th>
      <th>TBT</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Single embed</td>
			<td>679 KB</td>
      <td>920 ms</td>
		</tr>
    <tr>
			<td>Two embeds</td>
			<td>1.33 MB</td>
      <td>2110 ms</td>
		</tr>
	</tbody>
</table>

These numbers are based on first-page load &mdash; caching seems very efficient for subsequent page loads. We can see that some types of embeds are more efficient than others: Instagram embeds load asynchronously by default, so they don’t block the main thread. Nevertheless, it’s clear that a single page that contains several embeds can end up fairly weighty. With that in mind, let’s look at some of the ways we can reduce their impact.

{{% feature-panel %}}

## Do You Really Need An Embed?

The most obvious way to reduce the impact of these embeds is not to include them at all. Many CMSs make it very easy for clients to include as many embeds as they want. But that doesn’t mean they *should*. Ideally, the design process should take into account the ways in which clients might wish to share content from social media. What are the client’s objectives? Does an embedded Twitter feed actually add any value, or is it in fact a distraction from the important content of the page?

We should make clients aware of the trade-offs in performance and environmental impact if they choose to include embeds. It’s worth considering whether other design options might provide the same (or better) value. Some alternative options could include:

- **Curated testimonials**  
Does the client simply want to display feedback from happy customers? A selection of well-designed testimonials could be a better alternative.
- **Links**  
A simple text summary and link to the original social media post might be a viable option.
- **Webmentions**  
Implementing Webmentions on a site enables you to display data when someone mentions your URL online. [This article](https://daily-dev-tips.com/posts/goodbye-comments-welcome-webmentions/) from Daily Dev Tips walks through how to get started.

### Using An API

If you need to display (for example) the latest five tweets from your profile, it could be worth considering using the Twitter API. It will mean you’ll also have full control over how they’re displayed, so you could choose to only display the text content of a tweet, rather than associated images and videos, for example. This is quite a high-effort option and is beyond the scope of this article. Check out the tutorial [*Building an app to stream Tweets in real-time using the Twitter API*](https://dev.to/twitterdev/building-an-app-to-stream-tweets-in-real-time-using-the-twitter-api-o31) as an example.

### Video

If your video is short and sweet, you might consider using native HTML video in place of an embed from YouTube. This could be an especially good option for background videos, which often need to loop and allow full control over the playback with just a sprinkling of JS. A YouTube video, in contrast, won’t allow you to remove or customize the default player controls.

This might not be suitable for longer videos. YouTube does a lot of optimization, as well as serving content from a CDN, reducing the distance data has to travel &mdash; which, in turn, reduces carbon emissions. (Read about the benefits of CDNs in [this article](https://www.wholegraindigital.com/blog/how-using-a-cdn-is-better-for-people-and-the-planet/) by Wholegrain Digital.)

{{% ad-panel-leaderboard %}}

## Lazyloading

If we conclude that yes, social media embeds are essential to our site, the very least we can do is lazyload them. This means that the resources aren’t requested until the user scrolls to that point in the page. If they never get there, then the resource isn’t loaded at all.

[Lazyloading](https://web.dev/iframe-lazy-loading/) a video embed from YouTube is now trivially easy for browsers that support it: simply add the `loading="lazy"` attribute. Unfortunately, it’s not yet universally supported &mdash; at the time of writing Firefox only supports lazy loading for images, and Safari doesn’t support it at all. Adding `loading="lazy"` on Twitter embeds in the HTML isn’t possible, as the iframe is appended by the embedded script.

Libraries such as [`Lozad.js`](https://apoorv.pro/lozad.js/) enable us to lazyload content with cross-browser support. [This Codepen demo](https://codepen.io/17num/pen/NWxJzde) demonstrates how it can be used to lazyload a number of tweets.

You can also [lazyload HTML video](https://web.dev/lazy-loading-video/) if you’re using that in place of a video embed.

## WordPress

If you’re using WordPress, there are plenty of lazy loading plugins for embedded videos to choose from. The [Lazy Load](https://wordpress.org/plugins/rocket-lazy-load/) plugin by WP Rocket comes highly recommended, and [this article](https://sabrinazeidan.com/embed-youtube-video-wordpress-without-slowing/) by Sabrina Zeidan demonstrates the big difference it can make to performance. Unfortunately, I’m unable to find any WordPress plugins for lazyloading embeds from Twitter, Instagram and others.

## Facades / Import On Interaction

An alternative to an embedded post is to display a static image preview or a screenshot, known as a “facade”. Screenshots can be captured manually, or you could use a service such as [Tweetpik](https://tweetpik.com), which creates screenshots from tweet URLs (and has an API). Don’t forget to include `alt` text, so that users of assistive technologies can access the content of the image.

For interactive third-party content such as videos, we can use the `Import on interaction` pattern (detailed in [this article](https://www.patterns.dev/posts/import-on-interaction/) by Addy Osmani). The idea is similar to lazyloading: non-critical resources are only loaded when the user interacts with the UI component. It means that users who don’t interact with the content never have to bear the additional cost of loading the third-party script. Here’s a very basic demo of how we can do this using vanilla JS:

{{< codepen height="480" theme_id="light" slug_hash="abVzbXR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Click to load video [forked]](https://codepen.io/smashingmag/pen/abVzbXR) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}  

The technique can also be applied to other kinds of third-party scripts, such as chat widgets and map embeds. We successfully used it at [Atomic Smash](https://www.atomicsmash.co.uk/) to vastly improve the performance of a site with a chatbot. It has some clear limitations, however: once the video is loaded, the user has to click the second time to play it. There are some packages that handle this in a much more elegant way for YouTube and Vimeo embeds:

- [`lite-youtube-embed`](https://github.com/paulirish/lite-youtube-embed),
- [`lite-youtube`](https://github.com/justinribeiro/lite-youtube),
- [`lite-vimeo-embed`](https://github.com/luwes/lite-vimeo-embed),
- [`lite-vimeo`](https://github.com/slightlyoff/lite-vimeo).

{{% ad-panel-leaderboard %}}

## Social Sharing Widgets

On many websites, you’ll see “click to share” social media icons which, when clicked, invite the user to share the page in the social media app of choice. Unfortunately, much like social media embeds, these often come with a tonne of JS for the poor, unsuspecting user to download. If you care about the performance or the environmental impact of your site, it’s worth exploring alternatives.

### How Useful Are They?

Social share buttons are often requested by clients keen to increase engagement. They may have noticed them on the websites of their competitors, but the chances are they’re unaware of the performance impact. These widgets are heavily marketed by the companies that provide them, and it’s surprisingly hard to find any concrete statistics on how often users actually use them. But of the statistics I could find, most of them indicate that the overall use is very low. The consensus seems to be that users are far more likely to share content in other ways (i.e. by copying the URL and sharing in their app of choice) than to click the social sharing buttons. ([This post from 2017](https://www.layer0.co/post/anyone-use-social-sharing-buttons-mobile) outlines some stats and some possible reasons.) These factors combined may go some way to deterring clients from adding them to a site.

### The Web Share API

If you want to add a share button, but want to avoid any unnecessary JS, a leaner way to do it is with the [Web Share API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Share_API). It’s reasonably well-supported in mobile browsers but doesn’t yet have widespread desktop support. 

We can use the `navigator.share()` method to share a URL or files, such as images, videos or PDFs.

<pre><code class="language-javascript">navigator.share({
  title: 'Smashing Magazine',
  text: 'Web development news and tutorials',
  url: 'https://www.smashingmagazine.com/'
})</code></pre>

This demo provides a social sharing button for browsers that support it (and hides it for those that don’t) by calling the method on click. We can first test for support using `navigator.canShare()`:

{{< codepen height="480" theme_id="light" slug_hash="wvPBBBg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Web Share API [forked]](https://codepen.io/smashingmag/pen/wvPBBBg) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}} 

We can see that the Web Share API doesn’t provide the *same* experience as social sharing widgets, but allows the user to choose from their installed apps to share the content.

### NPM Packages

If you need share buttons that behave more like the aforementioned sharing widgets and have cross-browser compatibility, a better option is to use an NPM package. [`share-buttons`](https://www.npmjs.com/package/share-buttons) is one such package. It provides 19 different sharing options and loads far less JS. Another advantage is you can fully customize your share buttons.

### JS-free Buttons

It may come as a surprise that you actually don’t need JS at all to deliver social sharing links &mdash; a link URL is all you need. Knowing the correct URL to implement this is not exactly intuitive, but there are various helper sites available that build the link for you: [sharingbuttons.io](https://sharingbuttons.io/) and [simpleshare.io](https://simpleshare.io) are two of them. The former provides a CSS snippet to style them up just like the real thing too &mdash; although you’re free to customize them. As Max Stoiber’s Sharing Buttons site claims:

<blockquote>“They load incredibly fast (they only use a single HTTP request), don’t block your website from rendering, are accessible and don’t track the user”.</blockquote>

What’s not to like?

I genuinely can’t find any downsides to this approach, it seems like a clear winner. I guess *maybe* in the future, it’s possible that the URI used for sharing by any of the social media sites could change, meaning you would have to manually update (as opposed to say, updating a package or plugin). But I don’t know how likely this scenario is, and it seems well worth it for the benefits.

### Resources

You’ll find a lot of resources scattered throughout this article, but here are a few more links if you’re interested in diving deeper:

- “[How To Improve Social Engagement With The Web Share API](https://blog.logrocket.com/how-to-improve-social-engagement-with-the-web-share-api/)”, Craig Buckler
- [Fast Load Times](https://web.dev/fast), Performance resources from the web.dev team
- “[Lazy Load Embedded YouTube Videos](https://css-tricks.com/lazy-load-embedded-youtube-videos/)”, Chris Coyier  
An alternative technique than the one described in this article.
- [Web Share API Brings The Native Sharing Capabilities To The Browser](https://hospodarets.com/web-share-api), a tutorial on the Web Share API

{{< signature "vf, yk, il" >}}
