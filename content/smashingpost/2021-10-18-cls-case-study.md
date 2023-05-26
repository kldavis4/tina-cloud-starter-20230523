---
title: 'Solving CLS Issues In A Next.js-Powered E-Commerce Website (Case Study)'
slug: nextjs-ecommerce-cls-case-study
author: arijit-mondal
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e522651-eaf2-45e7-a544-9da7beb7b23e/nextjs-ecommerce-cls-case-study.jpg
date: 2021-10-18T14:00:00.000Z
summary: >-
  Cumulative Layout Shift is one of the hardest core web vital to debug. In this article, we go through different tools to investigate CLS, when to use them(and when not), and solutions to some of the CLS issues we faced in our Next.js-based e-commerce website.
description: >-
  Cumulative Layout Shift is one of the hardest core web vital to debug. In this article, we go through different tools to investigate CLS, when to use them(and when not), and solutions to some of the CLS issues we faced in our Next.js-based e-commerce website.
categories:
  - Next.js
  - E-Commerce
  - Performance
  - Case Studies
---

Fairprice is one of the largest online grocery stores in Singapore. We are continuously looking out for areas of opportunities to improve the user’s online shopping experience. Performance is one of the core aspects to ensure our users are having a delightful user experience irrespective of their devices or network connection. 

There are many key performance indicators (KPI) that measure different points during the lifecycle of the web page (such as TTFB, `domInteractive`and `onload`), but these metrics don’t reflect how the end-user experiences the page.

We wanted to use a few KPIs which correspond closely to the actual experience of the end-users so we know that if any of those KPIs are not performing well, then it will be directly impacting the end-user experience. We found out [user-centric performance metrics](https://web.dev/user-centric-performance-metrics/) to be the perfect fit for this purpose.

There are many user-centric performance metrics to measure different points in a page’s life cycle such as FCP, LCP, FID, CLS, and so on. For this case study, we are mainly going to focus on CLS.

{{% pull-quote %}}
CLS measures the total score of all unexpected layout shifts happening between when the page starts loading and till it is unloaded.
{{% /pull-quote %}}

Therefore having a low CLS value for a page ensures there are no random layout shifts causing user frustration. [Barry Pollard](https://twitter.com/tunetheweb) has written an [excellent in-depth article](https://www.smashingmagazine.com/2021/06/how-to-fix-cumulative-layout-shift-issues/) about CLS.

## How We Discovered CLS Issue In Our Product Page

We use Lighthouse and WebPagetest as our synthetic testing tools for performance to measure CLS. We also use the [web-vitals library](https://github.com/GoogleChrome/web-vitals) to measure CLS for real users. Apart from that, we check the Google Search Console Core Web Vitals Report section to get an idea of any potential CLS issues in any of our pages. While exploring the report section, we found many URLs from the product detail page had more than **0.1** CLS value hinting there is some major layout shift event happening there.

{{% feature-panel %}}

## Debugging CLS Issue Using Different Tools

Now that we know that there is a CLS issue on the product detail page, the next step was to identify which element was causing it. At first, we decided to run some tests using synthetic testing tools.

So we ran the lighthouse to check if it could find any element which could be triggering a major layout shift, it [reported](https://www.webpagetest.org/lighthouse.php?test=210107_DiRV_60b8ba6d013639239b13e1de189dd0b8&run=2) CLS to .004 which is quite low.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8ecbff-1e39-4089-8017-a43ac59a25bf/1-cls-case-study.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8ecbff-1e39-4089-8017-a43ac59a25bf/1-cls-case-study.png" width="750" height="122" sizes="100vw" caption="CLS showed a low CLS result of <code>.004</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8ecbff-1e39-4089-8017-a43ac59a25bf/1-cls-case-study.png'>Large preview</a>)" alt="CLS is .004" >}}

The Lighthouse report page has a diagnostic section. That also did not show any element causing a high CLS value.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0ea0aed-4442-4840-bcf3-e205bd3ad70e/3-cls-case-study.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0ea0aed-4442-4840-bcf3-e205bd3ad70e/3-cls-case-study.png" width="800" height="371" sizes="100vw" caption="A preview of the report page including the CLS contribution results. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0ea0aed-4442-4840-bcf3-e205bd3ad70e/3-cls-case-study.png'>Large preview</a>)" alt="Lighthouse report page" >}}

Then we ran WebpageTest and decided to check the filmstrip view:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58045ece-9507-4da3-9532-fbd6b738665f/2-cls-case-study.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58045ece-9507-4da3-9532-fbd6b738665f/2-cls-case-study.png" width="800" height="125" sizes="100vw" caption="The filmstrip view shows any frame which has a visual change and layout shift with a yellow dotted line. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58045ece-9507-4da3-9532-fbd6b738665f/2-cls-case-study.png'>Large preview</a>)" alt="the filmstrip view" >}}

We find this feature very helpful since we can find out which element at which point in time caused the layout to shift. But when we run the [test](https://www.webpagetest.org/video/compare.php?tests=210107_DiRV_60b8ba6d013639239b13e1de189dd0b8-r%3A1-c%3A0&highlightCLS=1&thumbSize=600&ival=100&end=visual) to see if any layout shifts are highlighted, there wasn’t anything contributing to the huge LCS:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1bae325-a97a-4977-8213-514b04ddbf83/7-cls-case-study.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1bae325-a97a-4977-8213-514b04ddbf83/7-cls-case-study.png" width="800" height="117" sizes="100vw" caption="You can find out whether any layout shifts had taken place by simply taking a quick glance at the frames. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1bae325-a97a-4977-8213-514b04ddbf83/7-cls-case-study.png'>Large preview</a>)" alt="test to see which element at which point in time caused a layout shift" >}}

{{% pull-quote %}}
The quirk with CLS is that it records individual layout shift scores during the entire lifespan of the page and adds them.
{{% /pull-quote %}}

**Note**: *How CLS is measured has been [changed](https://web.dev/evolving-cls/) since June 2021.*

Since Lighthouse and WebpageTest couldn’t detect any element that triggered a major layout shift which means it was happening after the initial page load possibly due to some user action. So we decided to use [Web Vitals Google Chrome extension](https://chrome.google.com/webstore/detail/web-vitals/ahfhijdlegdabablpippeagghigmibma?hl=en) since it can record CLS on a page while the user is interacting with it. After performing different actions we found the layout shift score is getting increased when the user uses the image magnify feature.

{{< vimeo id="622680593" breakout="true" >}}

To cross verify if layout shift is occurring while mouseover is on the image, we used the below code snippet from [https://web.dev/cls/](https://web.dev/cls/) which adds `console.log` when layout shift occurs:

<pre><code class="language-javascript">let cls = 0;

new PerformanceObserver((entryList) =&gt; {
 for (const entry of entryList.getEntries()) {
   if (!entry.hadRecentInput) {
     cls += entry.value;
     console.log('Current CLS value:', cls, entry);
   }
 }}).observe({type: 'layout-shift', buffered: true});</code></pre>

On further investigation, we found that ASDA faced a similar kind of issue and [raised it](https://bugs.chromium.org/p/chromium/issues/detail?id=1161025#c6) for chrome.

## Root Cause

On the product detail page, users can move the mouse over the product image to view a zoomed section of the image side by side of the actual product image as this video shows exactly what we are talking about.

{{< vimeo id="622687646" breakout="true" >}}

The image magnify feature helps our users to get the look and feel of the product as well as ensure that it is the right variant of the product they want to buy.

We have used [`react-image zoom`](https://github.com/malaman/react-image-zoom) library to build this image magnify functionality.

Image Magnify libraries usually have a lense (a square that moves when the mouse moves within the image). Since this lens changes its top and left position with mouse movement, it is being detected as a layout shift triggering CLS. We checked the library page as well as other similar react libraries ([`react-image-magnify`](https://www.npmjs.com/package/@vorld/react-image-magnify), [`react-image-zoom`](https://www.npmjs.com/package/react-image-zoom), [`react-image-magnifiers`](https://www.npmjs.com/package/react-image-magnifiers)) and found that all of them are suffering from the same CLS issue.

{{% ad-panel-leaderboard %}}

## How We Fixed It

We noticed that `react-image-zoom` was using the [`js-image-zoom`](https://github.com/malaman/js-image-zoom) library. So we had to modify the [`js-image zoom`](https://github.com/malaman/js-image-zoom) library to fix the issue.

The solution is pretty straightforward. While the mouse moves on of the product image, the image lens element moves by changing its left and top position. To fix the problem, we used `transform translate` which moves the element to a new layer, i.e. any movement that takes place on this new layer doesn’t cause layout shift anymore:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa02dea2-1413-4b73-be38-2a1fe9fa5ff4/4-cls-case-study.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa02dea2-1413-4b73-be38-2a1fe9fa5ff4/4-cls-case-study.png" width="800" height="46" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa02dea2-1413-4b73-be38-2a1fe9fa5ff4/4-cls-case-study.png'>Large preview</a>)" alt="managing the lense movement by using transform translate" >}}

I have also created a [PR](https://github.com/malaman/js-image-zoom/pull/31) to the original repo so that other developers using this library can get rid of the CLS issue.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8582f573-1036-40de-8505-cce9c022dff7/6-cls-case-study.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8582f573-1036-40de-8505-cce9c022dff7/6-cls-case-study.png" width="800" height="194" sizes="100vw" caption="PR created to help get rid of the CLS issue. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8582f573-1036-40de-8505-cce9c022dff7/6-cls-case-study.png'>Large preview</a>)" alt="creating a PR to the original repo" >}}

## The Impact Of The Change

After the code was deployed to production, the CLS was fixed on the product details page and the number of pages impacted with CLS was reduced by 98%:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6491824c-8f20-402a-acd1-c394c8cf58f5/5-cls-case-study.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6491824c-8f20-402a-acd1-c394c8cf58f5/5-cls-case-study.jpg" width="800" height="312" sizes="100vw" caption="<code>transform</code> has a performance advantage over position manipulation using left and top. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6491824c-8f20-402a-acd1-c394c8cf58f5/5-cls-case-study.jpg'>Large preview</a>)" alt="a graphic which shows the impact of the change." >}}

Since we used `transform`, it also helped to make the image magnify a smoother experience to the users.

**Note**: *Paul Irish has written an excellent [article](https://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/) on this topic.*

## Other Key Changes We Made For CLS

There are also some other issues we faced through many pages in our website which contribute to CLS. Let’s go through those elements and components and see how we tried to mitigate layout shifts arising from them.

- **Web-fonts:**  
We have noticed that late loading of fonts causes user frustrations since the content flashes and it also causes some amount of layout shifts. To minimize this we have done few changes:
  - We have self-hosted the fonts instead of loading from 3rd party CDN.
  - We preload the fonts.
  - We use font-display optional.

- **Images:**  
Missing height or width value in the image causes the element after the image to shift once the image is loaded. This ends up becoming a major contributor to CLS. Since we are using Next.js, we took advantage of the built-in image component called [`next/images`](https://nextjs.org/docs/api-reference/next/image). This component incorporates several image-related best practices. It is built on top of `<img>` HTML tag and can help to improve LCP and CLS. I highly recommend reading this [RFC](https://github.com/vercel/next.js/discussions/16832) to find out the key features and advantages of using it.

- **Infinite Scroll:**  
On our website, product listing pages have infinite scrolling. So initially, when users scroll to the bottom of the page they see a footer for a fraction of seconds before the next set of data is loaded, this causes layout shifts. To solve this we took few steps:
  - We call the API to load data even before the user reaches the absolute bottom of the list.
  - We have reserved enough space for the loading state and we show product skeletons during the loading status. So now when the user scrolls, they don’t see the footer for a fraction of seconds while the products are getting loaded.  

Addy Osmani has written a detailed [article](https://addyosmani.com/blog/infinite-scroll-without-layout-shifts/) on this approach which I highly recommend checking.

{{% ad-panel-leaderboard %}}

## Key Takeaways

- While Lighthouse and WebpageTest help to discover performance issues happening till page load, they can’t detect performance issues after page load.
- Web Vitals extensions can detect CLS changes triggered by user interactions so if a page has a high CLS value but Lighthouse or WebpageTest reports low CLS then the Web Vitals extension can help to pinpoint the issue.
- Google Search Console data is based on real users' data so that also can point to potential perf issues happening at any point in the life cycle of a page. Once an issue is detected and fixed, checking the report section again can help verify the effectiveness of the performance fix. The changes are reflected within days in the web vitals report section.

## Final Thoughts

While CLS issues are comparatively harder to debug, using a combination of different tools till page load (Lighthouse, WebPageTest) and Web Vitals extension (after page load) can help us pinpoint the issue. It is also one of the metrics which is going through lots of active development to cover a wide range of scenarios and this means that how it is measured is going to be changed in the future. We are following [https://web.dev/evolving-cls/](https://web.dev/evolving-cls/) to know about any upcoming changes.

As for us, we are continuously working to improve other Core Web Vitals too. Recently, we have implemented responsive image preload and started serving images in WebP format which helped us to reduce 75% of image payload, reduce LCP by 62%, and Speed Index by 24%. You can read more details of [optimization for improving LCP and Speed Index](https://medium.com/ne-digital/how-to-improve-lcp-and-speed-index-for-next-js-websites-f129ae776835) or follow our [engineering blog](https://medium.com/ne-digital) to know about other exciting work we are doing.
 
*We would like to thank [Alex Castle](https://twitter.com/atcastle) for helping us debug the CLS issue on the product page and solve the quirks in the `next/images` implementation.*

{{< signature "vf, yk, il" >}}
