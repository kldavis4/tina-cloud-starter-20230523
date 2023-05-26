---
title: 'How To Boost Media Performance On A Budget'
slug: boost-media-performance
author: akshay-ranganath
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ec28f16-47bc-4af6-b693-4c781f7f930a/1-boost-media-performance.png
date: 2021-03-25T13:00:00.000Z
summary: >-
  How do we get media performance right while staying within performance budgets? Let’s take a look at the recent stats and data around performance budgets, video playback performance issues and some techniques and tools to address these issues.
description: >-
  How do we get media performance right while staying within performance budgets? Let’s take a look at the recent stats and data around performance budgets, video playback performance issues and some techniques and tools to address these issues.
categories:
  - Business
  - Performance
  - Videos
  - Core Web Vitals
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Cloudinary
  link: https://cloudinary.com/state-of-visual-media-report/?utm_source=smashing_magazine&utm_medium=sponsored_post&utm_campaign=performance_budget
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e255398-3840-4aa3-a9d7-7ffd8949eaaa/cloudinary-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://srv.buysellads.com/ads/long/x/TCDZNLZTTTTTTTTFKHFNTTTTTTTVMA4GKTTTTTTT6T6WLYTTTTTTTEPWK7764ILV5QY6WB7LPRJIPNZLPRAMPKB6C6SE">Cloudinary</a> who help the community quickly and easily create, manage and deliver their digital experiences across any browser, device and bandwidth. <em>Thank you!</em>
---

American scholar Mason Cooley deftly described a hard fact of life: “A budget takes the fun out of money.” Unquestionably, media enlivens websites, adding appeal, excitement, and intrigue, let alone enticements to stay on a page and frequently revisit it. However, just as out-of-control spending bodes ill in the long run, so does unbudgeted digital media decimate site performance.

A case in point: a page-load slowdown of a mere second could cost [Amazon $1.6 billion in annual sales](https://www.fastcompany.com/1825005/how-one-second-could-cost-amazon-16-billion-sales). Of the many factors that affect page-load speed, **media** is a significant one. Hence the dire need for prioritizing optimization of media. By spending your money right on that task and budgeting your media, you’ll reap significant savings and benefits in the long run.

{{< rimg href="https://twitter.com/jaffathecake/status/1149264880974913536" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ce9ac1-8617-4eaf-b55d-c4d79ef9b96d/usa-today-hoax.jpg" width="800" height="453" sizes="100vw" caption="Have you been in the same sitution as well? Illustration by Joel Pett, <a href='https://twitter.com/jaffathecake/status/1149264880974913536'>adapted by Jake Archibald</a>." alt="A web perf summit, with a slide on evidence showing positive impact of performance, and an attendee arguing it it's all a big hoax and we create a better user experience for nothing." >}}

## Performance Budgets

<blockquote><p>“A performance budget is ‘... just what it sounds like: you set a ‘budget’ on your page and do not allow the page to exceed that. This may be a specific load time, but it is usually an easier conversation to have when you break the budget down into the number of requests or size of the page.”<br /><br />&mdash; <a href="https://twitter.com/tkadlec">Tim Kadlec</a></p></blockquote>

A performance budget as a mechanism for planning a web experience and preventing performance decay might consist of the following yardsticks:

- Overall page weight,
- Total number of HTTP requests,
- Page-load time on a particular mobile network,
- First Input Delay (FID)
- First Contentful Paint (FCP),
- Cumulative Layout Shift (CLS),
- Largest Contentful Paint (LCP).

[Vitaly Friedman](https://www.smashingmagazine.com/author/vitaly-friedman/) has an excellent [checklist](https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/) that describes the components that affect web performance along with useful tips on optimization techniques. Becoming familiar with those components will enable you to **set performance goals**.

With clearly documented performance goals, various teams can have meaningful conversations about the optimal delivery of content. For example, a budget can help them decide if a page should contain five images &mdash; or three images and one video &mdash; and still remain within the planned limits.

{{< rimg breakout="true" href="https://speedcurve.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ec28f16-47bc-4af6-b693-4c781f7f930a/1-boost-media-performance.png" width="800" height="289" sizes="100vw" caption="Performance budget, as used on performance monitoring tools, such as <a href='https://speedcurve.com/'>SpeedCurve</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ec28f16-47bc-4af6-b693-4c781f7f930a/1-boost-media-performance.png'>Large preview</a>)" alt="budget speedcurve" >}}

However, having a performance budget as a standalone metric might not be of much help. That’s why we must correlate performance to organizational goals.

## Business Performance

If you splurge a lot of bytes on nonoptimal videos and images, the rich-media experience will not be so rich anymore. An organization exists to **achieve outcomes**, such as enticing people to buy, educating them, motivating them, or seeking help and volunteers. Anyone with a web presence would appreciate the relationship between the effect of various performance measures on business metrics.

[WPOStats](https://wpostats.com/) highlights literally hundreds of **case studies** showing how a drop in perfrmance — from a few hundreds of milliseconds to seconds — might result in a massive drop in annual sales. Drawing that kind of relationship greatly helps track the effect of performance on business and, ultimately, build a [performance culture for organizations](https://speedcurve.com/blog/web-performance-culture/).

Similarly, slow sites can have a dramatic impact on conversion. A tough challenge online businesses face is to find the right balance between engaging the audience while staying *within* the performance budget.

It’s not surprising then that a critical component for audience engagement is **optimized visual media**, e.g. a captivating video that weaves a story about your product or service along with relevant, interesting, and appealing visuals.

According to MIT neuroscientists, our brain can absorb and understand visual media in less than [13 milliseconds](https://cloudinary.com/state-of-visual-media-report/?utm_source=smashing_magazine&utm_medium=sponsored_post&utm_campaign=performance_budget), whereas text can take the average reader over 3.3 mins to comprehend, often after re-reading it and cross-referencing other places. No wonder then that [microvideo content](https://cloudinary.com/state-of-visual-media-report#the-power-of-video) (usually just 10–20 seconds long) often delivers big engagements and conversion gains.

## Appeal Of Videos

While shopping online, we expect to see **detailed product images**. For years, I’ve come to prefer browsing products that are complemented by videos that show, for example, how to use the product or maybe how to assemble it, or that demonstrate real-life use cases.

Apart from my personal experience, a lot of research attests to the importance of video content:

- [96% of consumers](https://www.webretailer.com/b/amazon-product-videos/#Why_should_I_use_video_in_my_Amazon_listings) find videos helpful when making online purchasing decisions.
- [79% of online shoppers](https://www.webretailer.com/b/amazon-product-videos/#Why_should_I_use_video_in_my_Amazon_listings) prefer to watch a video for information on a product rather than reading the text on a webpage.
- The right product video can raise conversions by [over 80%](https://www.webretailer.com/b/amazon-product-videos/#Why_should_I_use_video_in_my_Amazon_listings).

Speaking about the delivery of videos on the web,

<blockquote><p>“The average video weight is increasing dramatically every year, more so on mobile than on desktop. In some cases, that may be warranted since mobile devices often have high-resolution screens, but it may also be due to a lack of ability to offer different video sizes using HTML alone. Many large videos on the web are hand-placed in marketing pages and don’t have sophisticated media servers to deliver appropriate sizes, so I hope in the future we’ll see similar simple HTML features for video delivery that we see in responsive images.”<br /><br />&mdash; <a href="https://scottjehl.com/lfwp/">Scott Jehl</a></p></blockquote>

The same sentiment was conveyed by Conviva’s [Q4 2020 State of Streaming](https://www.conviva.com/state-of-streaming/) (registration required), which noted that mobile phones saw **20% more buffering issues**, a 19% higher video-start failure and 5% longer start-time than other devices.

Apart from rendering troubles, **video delivery** can also raise bandwidth costs, especially if you cannot deliver the [browser’s optimal formats](https://cloudinary.com/blog/automatic_video_transcoding?utm_source=smashing_magazine&utm_medium=sponsored_post&utm_campaign=performance_budget). Also, if you are not using a content delivery network (CDN) or multiple CDNs to map users to the closest edge regions for reduced latencies &mdash; a practice called suboptimal routing &mdash; you might slow down the start of the video.

Similarly, unoptimized images were the [leading cause of page bloat](https://almanac.httparchive.org/en/2019/page-weight#what-types-of-assets-does-the-http-archive-track-and-how-much-do-they-matter). According to the [Web Almanac](https://almanac.httparchive.org/en/2020/page-weight#image-bytes), the differential in image bytes sent to mobile or desktop devices is very small, which amounts to a further **waste of bandwidth** for devices that don’t really need all the extra bytes.

Doubtless, going overboard with an engaging yet unoptimized content hurts business goals, and that’s where the fine art of balancing comes into play.

## The Art Of Balancing Performance With Media Content

Even though rich media can promote user engagement, we need to balance the cost of delivering them with your website performance and business goals. One alternative is to host and deliver video through a third party like YouTube or Vimeo.

Despite bandwidth savings, however, that approach comes at a cost. As the content owner, you can’t build a fully **customized branded experience**, or offer personalization. And of course, you need to host and deliver your images.

You don’t have to offload your content. There are also other options available. Consider revamping your system for optimal media delivery by doing the following:

### Understand your current usage

Study the weight of your webpages and the size of their media assets. Web-research expert [Tammy Everts](https://twitter.com/tameverts) recommends ensuring that pages are less than 1 MB in size for mobile and less than 2 MB for everything else.
In addition, identify the resources that are displayed on critical pages.

For example, can you replace a paragraph of text and the associated images with a short video? How would that decision affect your business goals? At this stage, you might need to review your Real User Monitoring (RUM) and Analytics and identify the critical pages that lead to higher conversion and [engagement rates](https://ken-williams.com/guide/overview/where-did-bounce-rate-go-in-google-analytics-4/).

Also, be sure to synthetically track Google’s [Core Web Vitals](https://web.dev/vitals/) (CWVs) as part of your toolkit with tools like [LightHouse](https://developers.google.com/web/tools/lighthouse/). You can also measure CWVs through real-user monitoring (RUM) like [CrUX](https://developers.google.com/web/tools/chrome-user-experience-report). Since the CWVs will also be a [signal for Google](https://developers.google.com/search/blog/2020/11/timing-for-page-experience) to crawlers, it makes sense to [monitor and optimize for those metrics](https://simonhearne.com/2020/core-web-vitals/): Largest Contentful Paint (LCP), First Input Delay (FID), and Cumulative Layout Shift (CLS).

### Serve the right format

Serve images or videos in the most appropriate format in terms of size and resolution for the viewing device or browser. You might need an [image CDN](https://web.dev/image-cdns/) for that purpose. Alternatively, create variants like WebM, AVIF, JPEG-XL, HEIC, etc. and selectively serve the right content type based on the requesting User-Agent and Accept headers.

For one-off conversions, you can try tools like [Squoosh.app](https://squoosh.app/) or [avif.io](https://avif.io/).
A related practice is to convert animated GIFs to videos. For more insight, see this [Web.dev article](https://web.dev/replace-gifs-with-videos/). Want to try setting up a workflow to handle video publishing? See the great tips in the article [Optimizing Video For Size And Quality](https://www.smashingmagazine.com/2021/02/optimizing-video-size-quality/).

### Serve the right size

[Over 41%](https://almanac.httparchive.org/en/2020/mobile-web#images) of images on mobile devices are improperly sized. So, rather than serving a fixed width, crop your images and videos to fit the container size with tools like [Lazysizes](https://afarkas.github.io/lazysizes/index.html). Better yet, AI tools that can detect areas of interest while cropping images could save you a load of time and effort. You could also leverage [native lazy-loading](https://web.dev/browser-level-image-lazy-loading/) for images that are below the fold.

### Add subtitles to your videos

[Almost 85% of videos are played without sound.](https://cloudinary.com/state-of-visual-media-report?utm_source=smashing_magazine&utm_medium=sponsored_post&utm_campaign=performance_budget) Adding subtitles to them doesn’t only provide an accessible experience, but it would capture audience attention and boost engagement. However, transcribing videos could be a tedious job; you can work with an AI-based transcription service and improve it instead to automate the workflow.

### Deliver through multiple CDNs

CDNs can alleviate last-mile latency, shorten a video’s start time, and potentially reduce buffering issues. According to a [study by Citrix](https://www.citrix.com/content/dam/citrix/en_us/documents/white-paper/best-practices-for-evaluating-and-implementing-a-multi-cdn-strategy.pdf), a multi-CDN strategy can reduce latency even further and offer continued availability in case of localized outages in the CDN’s edge nodes.

Instead of leveraging multiple discreet tools, you could explore a product like [Cloudinary’s Media Optimizer](https://cloudinary.com/products/media_optimizer?utm_source=smashing_magazine&utm_medium=sponsored_post&utm_campaign=performance_budget), which effectively and efficiently optimizes media, delivering the right format and quality through multi-CDN edge nodes. In other words, Media Optimizer optimizes **both** quality and size, serving high visual fidelity in small files.

### Progressively render video

Auto-playing preview videos on YouTube [has shown](https://cloudinary.com/state-of-visual-media-report?utm_source=smashing_magazine&utm_medium=sponsored_post&utm_campaign=performance_budget) to increase video watch time by over 90%. Video auto-play has few benefits and [plenty of drawbacks](https://www.boia.org/blog/why-autoplay-is-an-accessibility-no-no), so it’s important to be careful when to use and when not to use it. It’s important to have the option to pause the video as a minimum.

A good way to balance the page-size budget would be to first serve AI-created **video previews and poster images only**, loading the full video only if the user clicks the video. That way, you can eliminate unnecessary downloads and accelerate page loads.

Alternatively, load a preview video at the beginning and let the player autoplay the full version. Once the preview completes, the player checks the connection type of the device with the [Network Connection API](https://developer.mozilla.org/en-US/docs/Web/API/Network_Information_API) and, if the user has good connectivity, swaps the source from preview to the actual video.

You can check a [sample page](https://gist.github.com/akshay-ranganath/d355a4d8ea7058d94a7036feac65d013) for a demo.
Here’s a **tip**: since CDNs can detect network connection types more reliably, your production-quality code could leverage the CDN to detect network speed, based on which your client code could progressively load the long-form video.

## Wrapping Up

Down the road, thanks to its remarkable ability to tell stories in a way that words can’t, visual media will continue to be a dominant element for websites and mobile apps. However, determining the right content to deliver depends on both your business strategy and site performance.

<blockquote><p>“A performance budget doesn’t guide your decisions about what content should be displayed. Rather, it’s about how you choose to display that content. Removing important content altogether to decrease the weight of a page is not a performance strategy.”<br /><br />&mdash; <a href="https://timkadlec.com/">Tim Kadlec</a></p></blockquote>

That’s sound advice to keep in mind.

{{< signature "vf, yk, il" >}}
