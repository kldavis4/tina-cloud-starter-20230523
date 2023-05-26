---
title: 'Core Web Vitals Tools To Boost Your Web Performance Scores'
slug: core-web-vitals-tools-boost-performance
author: zara-cooper
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3b91182-5474-4e02-855c-30c0887948c1/core-web-vitals-tools-boost-performance.jpg
date: 2022-08-09T14:00:00.000Z
summary: >-
  Identify, compare, analyze and fix your Core Web Vitals scores to boost web performance of your sites. These tools will help you to do just that.
description: >-
  Identify, compare, analyze and fix your Core Web Vitals scores to boost web performance of your sites. These tools will help you to do just that.
categories:
  - Web Core Vitals
  - Performance
  - Resources
---

The success of your website depends on the impression it leaves on its users. By optimizing your [Core Web Vitals](https://web.dev/vitals/#core-web-vitals) scores, you can **gauge and improve user experience**. Essentially, a *web vital* is a quality standard for UX and web performance set by Google. Each web vital represents a discrete aspect of a user’s experience. It can be measured based on real data from users visiting your sites ([field metric](https://web.dev/lab-and-field-data-differences/#field-data)) or in a lab environment ([lab metric](https://web.dev/lab-and-field-data-differences/#lab-data)).

In fact, several **user-centric metrics** are used to quantify web vitals. They keep evoling, too: as there were conversations around slowly adding accessibility and responsiveness as web vitals as well. In fact, **Core Web Vitals** are just a part of this large set of vitals.

It’s worth mentioning that good Core Web Vitals scores [don’t necessarily mean](https://philipwalton.com/articles/my-challenge-to-the-web-performance-community/) that your website scores in high 90s on Lighthouse. You might have a pretty suboptimal Lighthouse score while having green Core Web Vitals scores. Ultimately, for now it seems that it’s only the latter that [contribute to SEO ranking](https://developers.google.com/search/blog/2021/11/bringing-page-experience-to-desktop) — both on mobile and on desktop.

While most of the tools covered below only rely on field metrics, others use a mix of both field and lab metrics. 
1
## PageSpeed Compare

[PageSpeed Compare](https://pagespeed.compare) is a page speed evaluation and benchmarking tool. It measures the web performance of a single page using [Google PageSpeed Insights](https://pagespeed.web.dev/). It can also compare the performance of multiple pages of your site or those of your competitors’ websites. It evaluates lab metrics, field metrics, page resources, DOM size, CPU time, and potential savings for a website. PageSpeed Compare measures vitals like FCP, LCP, FID, CLS, and others using land and field data.

{{< rimg href="https://pagespeed.compare" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2921a25d-a7ea-4afb-ab9a-9b358287d1f5/pagespeed-compare-01.png" width="782" height="409" sizes="100vw" caption="You can compare your website against your competitors in a film stripes on Pagespeed Compare. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2921a25d-a7ea-4afb-ab9a-9b358287d1f5/pagespeed-compare-01.png'>Large preview</a>)" alt="Filmstripes: render timelines" >}}

The report it generates lists the resources loaded by a page, the overall size for each resource type category, and the number of requests made for each type. Additionally, it examines the number of **third-party requests** and resources a page makes. It also lists cached resources and identifies unused Javascript. PageSpeed Compare checks the DOM of the page and breaks down its size, complexity, and children. It also identifies unused images and layout shifts in a graph. 

When it comes to **CPU time**, the tool breaks down CPU time spent for various tasks, Javascript execution time, and CPU blocking. Lastly, it recommends optimizations you can make to improve your page. It graphs server, network, CSS, Javascript, critical content, and image optimizations to show the potential savings you could gain by incorporating fixes into your site. It gives resource-specific suggestions you could make to optimize the performance of your page. For example, it could recommend that you remove unused CSS and show you the savings this would give in a graph.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fc149cd-fbc5-4c99-9896-308caf7e38f6/pagespeed-compare-02.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fc149cd-fbc5-4c99-9896-308caf7e38f6/pagespeed-compare-02.png" width="782" height="636" sizes="100vw" caption="PageSpeed Compare web performance report for Toshiba, Dell and Acer. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fc149cd-fbc5-4c99-9896-308caf7e38f6/pagespeed-compare-02.png'>Large preview</a>)" alt="PageSpeed Compare pulls data from Google’s CrUX report and shows the distribution of experiences for multiple websites." >}}

PageSpeed Compare provides **web performance reports** in a dashboard-alike overview with a set of graphs. You can compare **up to 12 pages at once** and presents the report in a simple and readable way since it uses PageSpeed Insights to generate reports. Network and CPU are throttled for lab data tests for more realistic conditions.

## Bulk Core Web Vitals Check

[Experte's Bulk Core Web Vitals Check](https://www.experte.com/web-vitals) is a free tool that crawls up to 500 pages of the entire domain and provides an overview of the Core Web Vitals scores for them. Once the tool has crawled all the pages, it starts performing a **Core Web Vitals check** for each page and returns the results in a table. Running the test takes a while, as each web page test is done one at a time. So it’s a good idea to let it run for **15-30 mins** to get your results.

{{< rimg href="https://www.experte.com/web-vitals" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad48d47f-74c8-4fc8-9c03-c3287a07f274/core-web-vitals-bulk-checker.png" width="781" height="388" sizes="100vw" caption="<a href='https://www.experte.com/web-vitals'>Bulk Core Web Vitals Check</a> crawls your domain and reports Core Web Vitals scores for up to 500 pages. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad48d47f-74c8-4fc8-9c03-c3287a07f274/core-web-vitals-bulk-checker.png'>Large preview</a>)" alt="Bulk Core Web Vitals check" >}}

What’s the benefit then? As a result, you get a full overview of the pages that perform best, and **pages that perform worst** — and can compare the values over time. Under the hood, the tool uses Pagespeed Insights to measure Core Web Vitals.

You can **export the results as a CSV file** for Excel, Google Sheets or Apple Pages. The table format in which the results are returned makes it easy to compare web vitals across different pages. The tests can be run for both mobile and desktop.

Alternatively, you can also check David Gossage's article on [How to review Core Web Vitals scores in bulk](https://seogreetings.com/blogs/news/review-core-web-vitals-scores-in-bulk), in which he shares the scripts and how to get an API key to run the script manually without any external tools or services.
## Treo

If you’re looking for a slightly more advanced option for bulk Core Web Vitals check, this tool will cover your needs well. [Treo Site Speed](https://treo.sh/sitespeed) also performs site speed audits using data from the Chrome UX Report, [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) and [PageSpeed Insights](https://pagespeed.web.dev/).

{{< rimg href="https://treo.sh/sitespeed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d686916-e6f9-4fd9-92da-5d6d7ca00770/treo.png" width="781" height="425" sizes="100vw" caption="<a href='https://treo.sh/sitespeed'>Treo</a> provides a very detailed overview of your performance metrics, including geography and experimental metrics, such as Interaction to Next Paint. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d686916-e6f9-4fd9-92da-5d6d7ca00770/treo.png'>Large preview</a>)" alt="Treo Site Speed" >}}

The audits can be performed across **various devices and network conditions**. Additionally though, with [Treo](https://treo.sh/), you can track the performance of all your pages across your sitemap, and even set up **alerts for performance regressions**. Additionally, you can receive monthly updates on your website’s performance.

{{< rimg href="https://treo.sh" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5af1ab7-14b3-4fb9-874d-fc9ffc31d8d5/treo-core-web-vitals-sitemap-scan.jpeg" width="781" height="575" sizes="100vw" caption="<a href='https://treo.sh'>Treo</a> crawls the entire site and highlights outliers for your Core Web Vitals scores. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5af1ab7-14b3-4fb9-874d-fc9ffc31d8d5/treo-core-web-vitals-sitemap-scan.jpeg'>Large preview</a>)" alt="Treo Site Speed" >}}

With Treo Site Speed, you can also **benchmark a website against competitors**. [The reports Treo generates](https://treo.sh/sites) are comprehensive, broken down by devices and geography. They are granular and available at domain and page levels. You can export the reports or access their data using an API. They are also **shareable**.

{{< rimg href="https://treo.sh" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aac6dfb7-0fe7-4ab1-a719-9c1f1011c76f/treo-sitemap-scan.png" width="781" height="477" sizes="100vw" caption="<a href='https://treo.sh'>Treo</a> crawls the entire site and highlights outliers for your Core Web Vitals scores. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aac6dfb7-0fe7-4ab1-a719-9c1f1011c76f/treo-sitemap-scan.png'>Large preview</a>)" alt="Treo Site Speed" >}}

{{% feature-panel %}}


## WebPageTest Core Web Vitals Test

[WebPageTest](https://www.webpagetest.org/) is, of course, a performance testing suite on its own. Yet one of the useful features it provides is a detailed breakdown of [Core Web Vitals metrics](https://www.webpagetest.org/webvitals) and pointers to problematic areas and how to fix them.

{{< rimg href="https://www.webpagetest.org/webvitals" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ab12dbc-2453-487c-8e3b-fb10bc7f18c9/webpagetest.png" width="781" height="264" sizes="100vw" caption="<a href='https://www.webpagetest.org/'>WebPageTest</a> reports the Core Web Vitals scores — along with suggestions for improvements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ab12dbc-2453-487c-8e3b-fb10bc7f18c9/webpagetest.png'>Large preview</a>)" alt="WebPageTest: observed web vitals metrics" >}}

There are also plenty of Core Web Vitals-related details in the [actual performance audit](https://www.webpagetest.org/result/220808_BiDcMJ_6EY/3/experiments/), along with suggestions for improvements which you can turn on without changing a line of code. For some, you will need a pro account though.

## Cumulative Layout Shift Debuggers

Basically, the [CLS Debugger](https://webvitals.dev/cls) **helps you visualize CLS**. It uses the [Layout Instability API](https://developer.mozilla.org/en-US/docs/Web/API/Layout_Instability_API) in Chromium to load pages and calculate their CLS. The CLS is calculated for both mobile and desktop devices and takes a few minutes to complete. The network and CPU are throttled during the test, and the pages are requested from the US.

The **CLS debugger generates a GIF image** with animations showing how the viewport elements shift. The generated GIF is important in practically visualizing layout shifts. The elements that contribute most to CLS are marked with squares to see their size and layout shift visually. They are also listed in a table together with their CLS scores.

<figure>
<a href="https://webvitals.dev/cls"><img style="max-width: 450px; height: auto;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c87c902f-e267-4ded-90ee-af9407a33c4d/webvitals-dev.gif" /></a><br /><figcaption><a href="https://webvitals.dev/cls">CLS debugger</a> in action: highlighting the shifts frame by frame.</figcaption>
</figure>

Although the CLS is calculated as a lab metric initially, the CLS debugger receives CLS measurements from the Chrome UX Report as well. The CLS, then, is a rolling average of the past 28 days. The CLS debugger allows you to ignore cookie interstitials — plus, you can generate reports for specific countries, too.

Alternatively, you can also use the [Layout Shift GIF Generator](https://defaced.dev/tools/layout-shift-gif-generator/). The tool is available on [its webpage](https://defaced.dev/tools/layout-shift-gif-generator/) or as a [command line tool](https://www.npmjs.com/package/layout-shift-gif). With the CLI tool, you can specify additional options, such as the **viewport width and height**, cookies to supply to the page, the GIF output options, and the CLS calculation method.

{{% ad-panel-leaderboard %}}
## Polypane Web Vitals

If you want to keep your Core Web Vitals scores nearby during development, [Polypane Web Vitals](https://polypane.app/docs/web-vitals/) is a fantastic feature worth looking into. [Polypane](https://polypane.app/) is a standalone browser for web development, that includes tools for accessibility, responsive design and, most recently, performance and Core Web Vitals, too.

{{< rimg href="https://polypane.app/docs/web-vitals/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba2d4fc2-6c40-4cd5-a87b-7161376d5755/core-web-vitals-largest-contentful-paint.png" width="781" height="557" sizes="100vw" caption="<a href='https://polypane.app/docs/web-vitals/'>Polypane</a> strikes again, now with the Core Web Vitals feature. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba2d4fc2-6c40-4cd5-a87b-7161376d5755/core-web-vitals-largest-contentful-paint.png'>Large preview</a>)" alt="" >}}

You can automatically gather Web Vitals scores for each page, and these are then shown at the bottom of your page. The tool also provides LCP visualization, and shows layout shifts as well.
## Noteable Mentions

- [Calibre’s Core Web Vitals Checker](https://calibreapp.com/tools/core-web-vitals-checker) allows you to check Core Web Vitals for your page with one click. It uses data from the Chrome UX Report and measures LCP, CLS, FID, TTFB, INP and FCP.

{{< rimg href="https://calibreapp.com/tools/core-web-vitals-checker" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ef5d053-91ca-431b-88b3-c7d4fd9b6cec/calibre.png" width="781" height="349" sizes="100vw" caption="<a href='https://calibreapp.com/tools/core-web-vitals-checker'>Calibre</a> displays Core Web Vitals as well: just enter the URL, and get the results. Easy. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ef5d053-91ca-431b-88b3-c7d4fd9b6cec/calibre.png'>Large preview</a>)" alt="" >}}

- [CrUX Compare](https://crux-compare.netlify.app/) is a little free tool that allows you to add a few sites and compare their Core Web Vitals scores side-by-side.

- [Web Vitals JavaScript library](https://github.com/GoogleChrome/web-vitals) is a tiny library for measuring all the Web Vitals metrics on real users on your site.

- [An In-Depth Guide To Measuring Core Web Vitals](https://www.smashingmagazine.com/2021/04/complete-guide-measure-core-web-vitals/) is a guide by Barry Pollard on how to measure Core Web Vitals, detect issues and solve them, on Smashing Magazine.

{{< signature "vf, yk, il" >}}
