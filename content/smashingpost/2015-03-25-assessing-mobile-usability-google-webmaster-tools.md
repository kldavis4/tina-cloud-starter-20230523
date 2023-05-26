---
title: Assessing Mobile Usability With Google Webmaster Tools
slug: assessing-mobile-usability-google-webmaster-tools
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35e31697-c872-4fe2-b587-6b3b52c409ca/excerpt-googletools.png
date: 2015-03-25T22:57:54.000Z
author: tim-jensen
description: >-
  Back in 2013, Google officially announced that it would begin to penalize
  websites that provide a faulty user experience on mobile devices. Specific
  examples included redirecting inner URLs to a home page when viewed in a
  mobile version of a website, as well as showing 404 errors to people
  attempting to access pages on mobile.

  Toward the end of 2014, a Google spokesperson hinted that the mobile user
  experience would become a ranking factor. In January 2015, a number of website
  owners received messages warning about mobile usability issues on their
  websites, linking to a section of Webmaster Tools where they could review the
  problems.
categories:
  - Mobile
  - SEO
  - Tools
  - Usability
---
Back in 2013, <a href="https://googlewebmastercentral.blogspot.com/2013/06/changes-in-rankings-of-smartphone_11.html">Google officially announced</a> that it would begin to penalize websites that provide a faulty user experience on mobile devices. Specific examples included redirecting inner URLs to a home page when viewed in a mobile version of a website, as well as showing 404 errors to people attempting to access pages on mobile.

Toward the end of 2014, a Google spokesperson hinted that the <a href="https://searchengineland.com/google-may-add-mobile-user-experience-ranking-algorithm-205382">mobile user experience would become a ranking factor</a>. In January 2015, a number of website owners received messages warning about mobile usability issues on their websites, linking to a section of Webmaster Tools where they could review the problems.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2980df73-26ec-469d-b990-3f0eaa42c1a6/01-message-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eb8ca3a-3b6f-4ebf-94d7-3508213f0def/01-message-opt-small.jpg" alt="Mobile usability warning sent to owners of sites registered in Webmaster Tools" /></a><figcaption>Mobile usability warning sent to owners of websites registered with Webmaster Tools. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2980df73-26ec-469d-b990-3f0eaa42c1a6/01-message-opt.jpg">View large version</a>)</figcaption></figure>

In this article, we’ll review how to flag mobile issues in Webmaster Tools, explain the most common issues and learn how to assess mobile usability problems on your website based on these flags.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [SEO For Responsive Websites](https://www.smashingmagazine.com/2013/11/seo-for-responsive-websites/)
*   [What The Heck Is SEO? A Rebuttal](https://www.smashingmagazine.com/2012/12/what-heck-seo-rebuttal/)
*   [How Content Creators Benefit From The New SEO](https://www.smashingmagazine.com/2012/06/content-creators-benefit-from-new-seo/)
*   [The Importance Of HTML5 Sectioning Elements](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/)

{{% feature-panel %}}

Because mobile usability has become a greater priority in Google’s ranking algorithm, ensuring an optimal mobile experience on every website has become more important than ever. See the search results below, where Google has marked a dedicated mobile website (DP Review) and a responsive website (CNET) as being mobile-friendly. The result for PC Magazine lacks this label.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bfce4a5-9f00-4fe1-80ce-a34628265701/02-mobile-results-opt-small-1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bfce4a5-9f00-4fe1-80ce-a34628265701/02-mobile-results-opt-small-1.jpg" alt="Example results from a Google search on a mobile device" /></a><figcaption>Results from a Google search on a mobile device. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bfce4a5-9f00-4fe1-80ce-a34628265701/02-mobile-results-opt-small-1.jpg">View large version</a>)</figcaption></figure>

Taking a look at each URL shows us clear reasons why DP Review and CNET earned mobile-friendly labels and why PC Magazine did not and ranks below the others. Not only does the PC Mag link not go to the proper mobile version of the website (which does exist), but it also delivers a popup promotion with a tiny close button that’s awkward to tap on mobile.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f41a1e0f-3002-4f2c-b17c-92afc6a40041/03-mobile-page-examples-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6570f3cb-c7d1-4cbd-905e-15f119401973/03-mobile-page-examples-opt-small.jpg" alt="Mobile pages for each search result from the previous image" /></a><figcaption>Mobile pages for each search result from the previous image. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f41a1e0f-3002-4f2c-b17c-92afc6a40041/03-mobile-page-examples-opt.jpg">View large version</a>)</figcaption></figure>

Setting aside the legitimate mobile issues, not only will people drop off of your website after a poor experience, but also your organic search traffic might decline because rankings can suffer in mobile search results. On the flip side, when you do improve a problematic website, you could see a vast improvement in organic search traffic, as we’ll see in the following example.

My agency built a new website to replace one that had many of the mobile problems we’ll review in this article. The original website contained a number of Flash elements, lacked any viewport configuration, and contained tiny text and touch elements when viewed on a mobile screen. The new website was built in a responsive format, eliminating these issues. Within two months of relaunching, the website saw a 44% increase in new users from organic Google searches on mobile devices, twice the increase seen on desktop. While a number of other factors certainly played a role, such as content refinement, the fact that mobile showed such a significant increase reflects the value Google ascribes to mobile usability.</p>

## Finding Mobile Problems In Webmaster Tools

In order to review mobile issues flagged on your website, you’ll first need to install Google Webmaster Tools. While many websites already run Webmaster Tools, some do not, and so here are brief instructions to set up. Navigate to the <a href="https://www.google.com/webmasters/tools/">Webmaster Tools</a> page, and log in with your Google account. You’ll see a field to enter your URL. Then, select “Add a Site.”

Next, you’ll need to verify the website. Webmaster Tools will show the various methods of doing so, including uploading an HTML file to your website, adding a meta tag or signing into your domain name’s provider. You can also verify via Google Analytics or Google Tag Manager if either code is in place on your website and you have access to the account. If you’re running a Wordpress website, a plugin such as Yoast’s WordPress SEO will allow you to verify Webmaster Tools easily by copying and pasting a number from the meta tag into a field in the plugin.

After setting up Webmaster Tools on your website, you might not see any data in the interface for a few days. <a href="https://support.google.com/sites/answer/100283?hl=en">Submitting a site map</a> could speed up the process of crawling and indexing your website.

You’ll find the “Mobile Usability” section under “Search Traffic” in the left navigation bar. This will show you what errors, if any, have been found on your website. Click any of the error categories to see specific URLs flagged for each.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f9413dc-8175-49bc-b991-8c2aab168b6b/04-mobile-usability-warnings-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e3b3f31-9ddc-444e-8f82-2cfd331235d5/04-mobile-usability-warnings-opt-small.jpg" alt="Mobile-specific warnings in Webmaster Tools" /></a><figcaption>Mobile-specific warnings in Webmaster Tools. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f9413dc-8175-49bc-b991-8c2aab168b6b/04-mobile-usability-warnings-opt.jpg">View large version</a>)</figcaption></figure>

Google shows mobile issues in six main categories:

*   Flash usage,
*   viewport not configured,
*   fixed-width viewport,
*   content not sized to viewport,
*   small font size,
*   touch elements too close.

To fix these issues, look at the flagged URLs and determine what edits need to be made.

Regarding “Flash usage,” any Flash elements will not render properly on most mobile devices. For example, when I try to access <a href="https://www.wechoosethemoon.org">We Choose the Moon</a> from an iPhone, it prompts me to download Flash to experience the website. Well, I obviously can’t install Flash on my iPhone, so I can’t experience this website at all on mobile.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/133a0d7f-7fcd-497c-86e4-560e452d8254/05-flash-site-opt-small.jpg" alt="This website contains Flash features unviewable on a mobile device" /><br>
<figcaption>This website contains Flash features that are unviewable on a mobile device. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/133a0d7f-7fcd-497c-86e4-560e452d8254/05-flash-site-opt-small.jpg">View large version</a>)</figcaption></figure>

Fixing this problem simply means restructuring the website to not include any Flash when served on a mobile device.

“Viewport not configured” means that the website is not scaling properly to the device’s size. See the website below, parts of which are cut off in small browsers.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0d6856-d5a2-4201-8b24-0baab858b683/06-viewport-problems.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc29d2ba-b0be-4ddf-8430-3817e5001322/06-viewport-problems-opt-small.jpg" alt="Site with improperly setup viewport" /></a><figcaption>A website that is improperly set up for the viewport. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0d6856-d5a2-4201-8b24-0baab858b683/06-viewport-problems.jpg">View large version</a>)</figcaption></figure>

Use the <strong>meta viewport</strong> tag to ensure that the height and width of the website change based on the size of the phone or tablet’s screen. Inserting the following code into the head of the website will cause it to resize and rearrange elements to fit various screen sizes.</p>

<pre><code class="language-markup">&lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;</code></pre>

In this code, <code>width=device-width</code> will automatically size the width of the website to the size of the window in which it is being viewed. And <code>initial-scale=1</code> will set the zoom level of the website to 100%, scaling the website to fill the window regardless of the screen’s size. With this attribute in place, content will reflow when the phone or tablet is flipped from vertical to horizontal orientation.

“Fixed-width viewport” refers to pages that are set up to show at a specific pixel width. This is problematic when a website does not properly scale to an unexpected screen size. So, utilizing <code>device-width</code> in the <code>viewport</code> meta tag, as in the previous example, will enable the website to scale based on any device’s screen size.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1f851bd-e439-4c33-826b-e10e8aeb5883/07-fixed-width-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62b1312d-69e1-4415-9158-20a84bac8c8a/07-fixed-width-opt-small.jpg" alt="Site with fixed viewport" /></a><figcaption>Website with fixed viewport. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1f851bd-e439-4c33-826b-e10e8aeb5883/07-fixed-width-opt.jpg">View large version</a>)</figcaption></figure>

For instance, note how the navigation cuts off on the right side of Anthem’s website, shown in the screenshot above. This website includes the <code>viewport</code> meta tag but uses it to define a specific width.</p>

<pre><code class="language-markup">&lt;meta name="viewport" content="width=1100" /&gt;</code></pre>

Replacing <code>width=1100</code> with <code>device-width</code> would cause the website to scale to the width of the browser, fixing the issue. Of course, the developer would likely want to address issues with how elements on the website adapt to changes in size, as well.

“Content not sized to viewport” indicates that the users with small browsers need to scroll from side to side to view elements (as in both the fitness and Anthem examples). This can prove annoying, especially on a phone. Replacing absolute positioning with relative positioning in the CSS would likely help to fix this problem. For example, note how elements in the website below are side by side in a larger browser but stack on top of each other when the browser is smaller.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dda767e-3373-4949-9522-6ddf71fdc127/08-site-scaling-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a74ab621-6241-4cc5-b7ae-5c3131c72055/08-site-scaling-opt-small.jpg" alt="Scaling the placement of elements on a responsive website based on screen size" /></a><figcaption>Scaling the placement of elements on a responsive website based on screen size. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dda767e-3373-4949-9522-6ddf71fdc127/08-site-scaling-opt.jpg">View large version</a>)</figcaption></figure>

“Small font size” flags text too small to easily read on a page. This can occur both from fonts that are too small as well as from insufficient vertical spacing between text. To avoid this, <a href="https://developers.google.com/speed/docs/insights/UseLegibleFontSizes">Google recommends</a> starting with a base size of 16 CSS pixels and modifying up or down from there.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77bca537-437f-4e35-97d2-892d37044075/09-small-font-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087c8165-5e71-4525-be39-be87f49084ec/09-small-font-opt-small.jpg" alt="This website with a small font size is practically illegible on an iPhone without zooming." /></a><figcaption>This website with a small font size is practically illegible on an iPhone without zooming. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77bca537-437f-4e35-97d2-892d37044075/09-small-font-opt.jpg">View large version</a>)</figcaption></figure>

“Touch elements too close” indicates that a user might have trouble tapping a specific button, navigation element or form field if it’s too small and jammed next to other clickable elements. This problem can cause frustration because a user might select a different button than intended. For example, see how several links in the following image are stacked close together, making it difficult to select a particular one on a phone.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d6e4faf-3234-41b1-9ce1-39c90847f5aa/10-touch-elements-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e17faff-36ba-46be-8213-c3408b75683a/10-touch-elements-opt-small.jpg" alt="Webite with touch elements too close on a phone" /></a><figcaption>Website with touch elements too close on a phone. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d6e4faf-3234-41b1-9ce1-39c90847f5aa/10-touch-elements-opt.jpg">View large version</a>)</figcaption></figure>

To fix this problem, put enough space between buttons and links so that even on the smallest devices users will not have trouble selecting one. Adequate spacing is least <a href="https://developers.google.com/speed/docs/insights/SizeTapTargetsAppropriately">at least 7 millimeters or 48 CSS pixels</a> for these elements. Tweak this spacing to ensure that users do not encounter annoyances on a mobile device. In addition, think about what elements you will actually need to show phone users. In the example shown above, these users likely wouldn’t need to see all of the links and could have a much simpler experience with a few important links.

## Beware Of False Flags

In the example shown earlier, I took a closer look at URLs flagged for “Flash usage." I found that several of these pages include blog posts with embedded YouTube videos, whose content is served within an iframe (via the default embedding code). While these videos do show up as Flash at times, such as when viewed on a desktop page, they appear in HTML5 format on phones, playing with no problem. Ironically, even though it owns YouTube, Google has not picked up on the fact that YouTube changes the format of videos served when embedded on websites, depending on the device.

So, be sure to actually check the flagged pages to see whether issues are indeed legitimate. Keep in mind that Google’s automated crawling might not always show 100% accurate results. Although you can’t keep warnings about these pages from showing up, you could select an issue and choose to recheck the live version. Over time, Google will likely refine its methods for testing to filter out false flags.</p>

## Don’t Rely Completely On Google

On the other hand, don’t expect Google to pick up all potential problems with mobile usability. Just because you don’t see any errors, your website might not necessarily appear perfectly on all mobile devices. Test your website thoroughly across multiple devices and browsers to ensure a positive experience with website speed, appearance and interactivity.

Keep an eye on mobile metrics in Google Analytics to find potential usability issues. A key report to watch is found in “Audience” → “Mobile” → “Overview,” showing data for mobile, tablet and desktop traffic and engagement. For example, watch to see whether a high percentage of users on mobile devices are bouncing, especially if this number is much higher than for the desktop. Also, look at the average session duration for mobile devices to see whether the experience seems abnormally short or long. Overly brief or lengthy time spent on a website could indicate that people are either leaving right away out of frustration or are confused, taking too long to find what they wanted.

In addition, use heatmapping tools such as <a href="https://crazyegg.com">CrazyEgg</a> and <a href="https://hotjar.com">HotJar</a> to analyze website usage beyond what Google’s tools can tell you. All of these tools show how users interact with mobile specifically, including data such as where they click and how far they scroll. This data could reveal problems, such as users not scrolling all the way to the bottom on a long mobile page or not clicking buttons that appear too small on a mobile device.

For instance, based on heatmap data, we discovered that few users on phones were scrolling down to a form on a particular landing page. We then added functionality to allow users to tap a button at the top, causing the page to immediately scroll to the form. Afterward, we experienced an increase in form submissions.

Google Webmaster Tools is a helpful starting point for analyzing mobile issues on your website. If you receive warnings, don’t ignore them. Take time to look at the problems and identify opportunities to improve your website’s mobile usability. Ultimately, your goal is to make the website the best experience possible for mobile users, not just to obsess over your rankings in Google. However, Google will reward positive user experiences.</p>

### Final Notes

*   “[Building Your Mobile-Friendly Site: The Distilled Best Practice Guide](https://www.distilled.net/training/mobile-seo-guide/),” Distilled
*   “[New Google Mobile Algo: Google Begins Reducing Visibility for Non-Mobile Friendly Sites That Received Warnings](https://www.thesempost.com/new-google-mobile-algo-google-begins-reducing-visibility-non-mobile-friendly-sites-received-warnings/),” Jennifer Slegg, The SEM Post
*   “[Google: The Mobile-Friendly Ranking Factor Runs in Real Time and Is on a Page-By-Page Basis](https://searchengineland.com/google-mobile-friendly-ranking-factor-runs-real-time-page-page-basis-216100),” Barry Schwartz, Search Engine Land
*   “[Quick Tip: Don’t Forget the Viewport Meta Tag](https://webdesign.tutsplus.com/articles/quick-tip-dont-forget-the-viewport-meta-tag--webdesign-5972),” Ian Yates, Tuts+ An overview about properly implementing the `viewport` meta tag on your website.
*   “[How Bing and Your Mobile Device Became Friends](https://blogs.bing.com/webmaster/2014/11/20/bing-and-mobile-friends/),” Bing Blogs Here is Bing’s approach to crawling and ranking mobile results.

{{< signature "da, al, ml" >}}

