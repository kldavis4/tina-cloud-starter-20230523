---
title: 'Taking A Look At The State Of Progressive Images And User Perception'
slug: progressive-image-loading-user-perceived-performance
author: jmperezperez
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdbe7bf1-b1bf-4868-8df7-51c2b91bdd60/image-preview-800w.png
date: 2018-02-07T12:30:32+01:00
summary: >-
  We all want to load images fast on the web. Choosing the right image format, optimizing the quality and using responsive images are important tasks, but what can we do beyond that?
description: >-
  We all want to load images fast on the web. Choosing the right image format, optimizing the quality and using responsive images are important tasks, but what can we do beyond that?
categories:
  - Performance
  - Optimization
  - Media
---
“Progressive Images” is a hot topic these days. We often come across articles explaining techniques on how to avoid showing an empty space where an image will load. [Medium](https://medium.com/@jmperezperez/how-medium-does-progressive-image-loading-fd1e4dc1ee3d) and [Facebook](https://code.facebook.com/posts/991252547593574/the-technology-behind-preview-photos/) are examples of websites and mobile apps that apply this pattern.

I recently wrote about [different ways to use SVG as placeholders](https://medium.freecodecamp.org/using-svg-as-placeholders-more-image-loading-techniques-bed1b810ab2c), and this year’s [PerfPlanet’s Performance Calendar](https://calendar.perfplanet.com/2017/) included two posts that further describe SQIP, a technique based on blurred SVGs: [Progressive Image Loading using Intersection Observer and SQIP](https://calendar.perfplanet.com/2017/progressive-image-loading-using-intersection-observer-and-sqip/) and [SQIP &mdash; Vague Vectors for Performant Previews](https://calendar.perfplanet.com/2017/sqip-vague-vectors-for-performant-previews/).

When I first documented [Medium’s image loading technique](https://medium.com/@jmperezperez/how-medium-does-progressive-image-loading-fd1e4dc1ee3d), I was mostly interested in reverse-engineering their technique. I had seen the effect browsing Medium on a slow inflight connection. I thought that rendering a small image early, lazy-load and transition to the final version was a good idea.

**We assume these techniques improve a user’s perceived performance**. Fast rendering beats slow rendering. Putting something on the user’s screen early, even if it’s not the final content.

Are we sure about this?

Going through [some comments on Reddit](https://news.ycombinator.com/item?id=15696596), I found lots of insightful (and negative) opinions. Here are two of them:

<blockquote>“I hate websites that show a blurry version of an image before the final one loads. It plays with my eyes. I have to look away and peek to see if it’s done before I can read on. I wish there was a way to disable this functionality."<br />&mdash; <a href="https://news.ycombinator.com/item?id=15697660">rocky1138</a>, Hacker News</blockquote>

<blockquote>“How have people come to the conclusion that displaying a low-information version of the image to be loaded as a placeholder results in a quicker perceived load? To me all these effects just look rubbish and distracting, with no benefit at all &mdash; certainly not the perception of speed. It’s not like I can ever understand what the image really is before it’s fully loaded anyway, with our without fancy placeholder."<br />&mdash; <a href="https://news.ycombinator.com/item?id=15698518">dwb</a>, Hacker News</blockquote>

{{% feature-panel %}}

## Trying To Find Studies About Users' Perception

I wanted to find some scientific research that could support that these techniques to load images were (or not) beneficial. This proved to be a challenge. I couldn’t find any study proving that showing something like a blurry thumbnail before the image loads improves a user’s perception. Then I thought of progressive JPEGs.

### Back To Basis: Progressive JPEGs
In a certain way, we have had a similar “progressive image loading technique” backed into images for a long time. Progressive JPEG is a good example.

Progressive JPEGs have been proposed as a good practice for images, especially for sites used in slow networks. [Ann Robson](https://twitter.com/arobson) wrote a [post encouraging Progressive JPEGs](https://calendar.perfplanet.com/2012/progressive-jpegs-a-new-best-practice/), now five years ago, where she summarized why they were superior:

<blockquote>“Progressive JPEGs are better because they are faster. Appearing faster is being faster, and <strong>perceived speed is more important that actual speed</strong>. Even if we are being greedy about what we are trying to deliver, progressive JPEGs give us as much as possible as soon as possible."</blockquote>

A progressive JPEG encodes the image into several scans. The first scan renders the full image in low quality, and it is refined as more scans are rendered. An alternative is JPEG’s baseline mode in which the image is decoded top to bottom.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fbd8de4-7c06-468e-8318-662e06a7e406/1-ncstfh7ycfd0sssqwibkbw.png" sizes="100vw" caption="Baseline decoding of a JPEG image." alt="Baseline decoding of a JPEG image" >}}

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a03b6e34-bdda-4f22-9f88-63b2a3c50bbc/1-yyyjcgi1b4kgaenhobjblg.png" sizes="100vw" caption="Progressive decoding of a JPEG image." alt="Progressive decoding of a JPEG image" >}}

As a side note, JPEG encoding can be customized using different scan scripts. This can be used to [create images that are encoded in a hybrid mode between baseline and progressive](https://cloudinary.com/blog/progressive_jpegs_and_green_martians).

Progressive techniques like [Blur-up](https://css-tricks.com/the-blur-up-technique-for-loading-background-images/), [SQIP](https://github.com/technopagan/sqip) resemble progressive JPEGs from user’s perception point of view. The browser renders a low-quality image first and replaces it with the final image when it loads.

Interestingly the vast majority of JPEG images use the baseline mode. According to [some](https://blog.patrickmeenan.com/2013/06/progressive-jpegs-ftw.html) [sources](https://blog.radware.com/applicationdelivery/wpo/2014/09/progressive-image-rendering-good-evil/), progressive JPEGs represent at most 7% of all JPEGs. If we seem to agree that these techniques improve user’s perceived performance, why aren’t progressive JPEGs used more widely than baseline JPEGs?

### The Study

I could only find [a study called “Progressive Image Rendering - Good or Evil?”](https://blog.radware.com/applicationdelivery/wpo/2014/09/progressive-image-rendering-good-evil/), that tried to shed some light on this topic.

<blockquote>“When, as with the Progressive JPEG method, image rendition is a two-stage process in which an initially coarse image snaps into sharp focus, cognitive fluency is inhibited, and the brain has to work slightly harder to make sense of what is being displayed.”</blockquote>

According to the study, users find it more difficult to process progressive JPEGs, even though at first sight we would think the experience is better.

I recently [mentioned the study](https://twitter.com/jmperezperez/status/939487371543932928) in a conversation about LQIP (Low-Quality Image Placeholders). Soon, I got [some replies questioning the rigour of the study](https://twitter.com/soulislove/status/939571335742795776):

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Many people have questioned the validity of that study, though. It is contrary to everything we assume about the benefits of progressive rendering and nobody has come forth yet with a 2nd study with similar findings. We need more data.</p>&mdash; Tobias Baldauf 🥠 (@tbaldauf) <a href="https://twitter.com/tbaldauf/status/939491815463497729?ref_src=twsrc%5Etfw">December 9, 2017</a></blockquote>

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">The study was very limited and contentious. Large scale data to prove or disprove it is essential to draw any conclusions</p>&mdash; Yoav Weiss (@yoavweiss) <a href="https://twitter.com/yoavweiss/status/939500952243068928?ref_src=twsrc%5Etfw">December 9, 2017</a></blockquote>

So far, we have a single study which is received with skepticism. What else do we have? Can we use the existing tools to measure perceived performance as a proxy?

## Measuring Perceived Load Time

Imagine these two hypothetical filmstrips recorded from a site:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c22fa8bd-1bfb-4503-b2aa-fbae88291a73/1-1x1a1phgwrpvbyi7edw9ya.png" sizes="100vw" caption="A diagram showing 2 hypothetical filmstrips for the same site." alt="A diagram showing 2 hypothetical filmstrips for the same site. Version A renders blank pages and then all the content at once. Version B shows partial content as it loads.">}}

The general agreement is that **the user will perceive that Version B loads faster than Version A.** This is because parts of the page as rendered earlier than in Version A.

In some way, the situation is similar to that of progressive images, but at a larger scale. Partial content as early as possible, even though it’s not the final one.

A page load time of 1.2 seconds tells us part of the story, but doesn’t describe what the user sees during that time. These days we use metrics like [Speed Index](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index) to evaluate how fast a page loads. Speed Index measures the area of the page that is not visually completed. This is done on several screenshots taken at intervals. The lower the number, the better.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/700b7fd8-ede6-4fed-86c6-e7bd83ba05f8/1-b0t9uxxslyw5-yyczsxelw.png" sizes="100vw" caption="Speed Index formula (<a href='https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index'>Source</a>)" alt="Speed Index formula" >}}

If we think about progressive image loading techniques, how will Speed Index vary as the image loads? Will that area be considered “visually completed” if we use a low-quality placeholder?

Initially, Speed Index measured the progress comparing the distance of histograms, one per each primary color (red, green, blue). This is called Mean Histogram Difference. The goal is to prevent changes like reflows, where all elements on the page are shifted by a few pixels, from having a large impact on the calculation. For more information about the algorithm, read [the Measuring Visual Progress section of the Speed Index doc](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index#TOC-Measuring-Visual-Progress).

I decided to try Webpagetest against [a page that displays low-quality placeholders](https://medium.com/udacity/how-self-driving-cars-work-f77c49dca47e) (see [report on WebPageTest](https://www.webpagetest.org/video/compare.php?tests=171226_ZJ_5ddda9f0be7804d875203620d5b675bc-r%3A3-c%3A0&thumbSize=300&ival=1000&end=visual)):

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95ab94d3-c80b-4b5e-8fce-1240e03c5afe/1-iqdbby-z0vdra6orz4t-w.png" sizes="100vw" caption="Filmstrip showing visual completeness percentage (see <a href='https://www.webpagetest.org/video/compare.php?tests=171226_ZJ_5ddda9f0be7804d875203620d5b675bc-r%3A3-c%3A0&thumbSize=300&ival=1000&end=visual'>report on WebPageTest</a>)." alt="Filmstrip showing visual completeness percentage" >}}

We can notice that between second 8 and 10 the image loads. The blurry placeholder increases the visual completeness percentage from 75% to 83%. Loading the final image takes it from 83% to 93%.

We see that a placeholder contributes to the visual completeness of the page as measured by Speed Index. We can also observe that the placeholder doesn’t count as a fully visually complete area.

Speed Index is not the only metric that we can use to get a measure of how fast our page renders. Chrome Developer Tools includes an option to do a Performance audit. Go to `Audits` → `Perform an audit` → `Check 'Performance'` → `Run audit`.

Running an audit generates a report like this:

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cd71c7f-fc7e-4f48-8327-a71e5098cb04/1-bghn5cjxgydygsfu59aqdq.png" sizes="100vw" caption="Loading a story on Medium. Note that blurry image placeholder which later fades into the final image." alt="A photo of a phone loading a story on Medium, showing a blurry placeholder." >}}

One of the metrics reported is “Perceptual Speed Index.” In this run the value is `4,245`. But what exactly does this term mean? Is it the same as Webpagetest’s “Speed Index”?

Speed Index’s approach to measure pixel-wise similarity, also called “Mean Histogram Difference”, has some drawbacks. The MHD [doesn’t capture visual perception of shape, color or object similarity](https://www.slideshare.net/pahammad/psiabovefoldparvez201607pptx).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbf03317-cc22-4658-bad7-54f858424143/1-kyvjgimo-sy3q1-0d2uwlg.png" sizes="100vw" caption="Four different shapes with equal amount of black and white pixels." alt="Four different shapes with equal amount of black and white pixels." >}}

In most cases, this won’t make a big difference when running a visual completeness evaluation. In practice, the Speed Index as well as the Perceptual Speed Index have a high correlation:

<blockquote>“In large-scale empirical studies that we conducted (using 500+ Alexa top mobile webpage videos collected via WebPagetest), we find that SI and PSI are linearly correlated (at 0.91, to be precise).”  
&mdash; <a href="https://www.instartlogic.com/blog/perceptual-speed-index-psi-measuring-above-fold-visual-performance-web-pages">Perceptual Speed Index (PSI) for Measuring Above-the-Fold Web Performance</a></blockquote>

## Perceptual Speed Index

According to [Google’s Lighthouse documentation](https://developers.google.com/web/tools/lighthouse/audits/speed-index), the Perceptual Speed Index is calculated using a node module called [Speedline](https://github.com/pmdartus/speedline). This package calculates the perceptual speed index, based on the same principal as the original speed index, but **it computes the visual progression between frames using the SSIM instead of the histogram distance**.

[SSIM (Structural Similarity)](https://en.wikipedia.org/wiki/Structural_similarity) is used for measuring the similarity between two images. This method tries to model how human beings perceive images, and does capture shape, color and object similarity. SSIM has other interesting applications: One of them is optimizing image compression settings, such as [cjpeg-dssim](https://github.com/technopagan/cjpeg-dssim) which chooses the highest JPEG compression level and generates an image with a close enough SSIM.

Below you can see the [Image SSIM JS](https://darosh.github.io/image-ssim-js/test/browser_test.html) scores for [SVG images](https://medium.freecodecamp.org/using-svg-as-placeholders-more-image-loading-techniques-bed1b810ab2c#5b73) created using [Primitive](https://github.com/fogleman/primitive). The more shapes we use, the closer it is to the original image (SSIM = 1).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c71f666-0a4c-49a9-a65a-9b557495ad4e/s-4608003090976b9f9084569de88c180f67f102ec4e553fa4017363e77ac7ec4e-1515671638429-ssim-1.jpg" sizes="100vw" caption="Two images reproduced using triangles. More shapes makes the image more similar to the original one." alt="Two images reproduced using 100 and 10 triangles. More shapes makes the image more similar to the original one." >}}

More recent alternatives to SSIM are [butteraugli](https://github.com/google/butteraugli) (used by [Guetzli, Google’s Perceptually Guided JPEG Encoder](https://research.googleblog.com/2017/03/announcing-guetzli-new-open-source-jpeg.html)) and [SSIMULACRA](https://github.com/cloudinary/ssimulacra) ([used by Cloudinary](https://cloudinary.com/blog/detecting_the_psychovisual_impact_of_compression_related_artifacts_using_ssimulacra)).

## Conclusion

There is no simple way to synthesize a user’s perception of an image loading over time. We are driven by the gut feeling that showing earlier is better, even if it’s not the final content, though some users will disagree.

As developers, **we need to measure performance**. It’s the only way we can set targets to improve it, and know when we don’t meet a performance budget. The advantage of betting on progressive image loading is that we can measure it with tools that are based on user’s perception. They give us a score, they are reproducible and scalable. They fit in our workflow and tools, and are here to stay.

As web developers, we should care more about the loading experience of the websites we build. It's great that we now have tools such as WebPageTest and Lighthouse that can help us easily measure the effect of using progressive image loading techniques. No more excuses!

{{< signature "rb, ra, yk, il" >}}

