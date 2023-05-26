---
title: Tracking Internal Marketing Campaigns With Google Analytics
slug: tracking-internal-marketing-campaigns-google-analytics
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c31e4755-974b-4e95-ae90-52a607f5b606/pic-11-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png
date: 2017-08-10T20:25:13.000Z
author: christianebernickel
description: >-
  Many websites use internal advertising in the form of banners or personalized
  product recommendations to bring additional products and services to the
  attention of visitors and to increase conversions and leads. Naturally, the performance and effectiveness of internal marketing campaigns
  should be assessed, too, as this is one of the most powerful instruments for
  generating more leads, more conversions and more revenue on your website. In
  many cases, web analysts use Google Analytics' UTM campaign parameters to
  track internal advertising.
categories:
  - Coding
  - Mobile
  - Business
  - Advertising
  - Marketing
  - Analytics
---
Many websites use internal advertising in the form of banners or personalized product recommendations to bring additional products and services to the attention of visitors and to increase conversions and leads.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c4868e2-31c9-4be5-969e-3832498c842f/smag-ad-example-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b5a2725-e9e8-4861-b34f-7a78776c2b92/smag-ad-example-800w-opt.png" alt="Example: Some internal advertising on Amazon.com" width="800" height="640" /></a><figcaption>Example: Some internal advertising on smashingmagazine.com (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c4868e2-31c9-4be5-969e-3832498c842f/smag-ad-example-large-opt.png">View large version</a>)</figcaption></figure>

Naturally, the performance and effectiveness of internal marketing campaigns should be assessed, too, as this is one of the most powerful instruments for generating more leads, more conversions and more revenue on your website. In many cases, web analysts use <a href="https://support.google.com/analytics/answer/1033863?hl=en">Google Analytics' UTM campaign parameters</a> to track internal advertising.</p>

<p>For those of you who are not familiar with UTM parameters, this is what an internal link could look like if you add UTM parameters:</p>

{{% feature-panel %}}

<pre><code class="language-markup">
www.yourdomain.tld/superproduct.htm?utm_source=internal&amp;utm_medium=internal-ads&amp;utm_campaign=cross-selling
</code></pre>

<p><strong>The problem:</strong> UTM parameters are intended to be used in external campaigns (for example, promoted posts on Facebook). Unfortunately, they are <em>not suitable</em> for tracking internal campaigns. In this article, I'll explain why you would corrupt your Google Analytics data when using UTM parameters for internal tracking purposes.</p>

<p><strong>The solution:</strong> I have developed a set of URL parameters (called ITM parameters) that make tracking internal marketing just as simple and convenient as the familiar UTM parameters. Set-up takes a little time, but then you'd have a means of tracking internal marketing that both is easy to use and delivers accurate data. This article presents the solution and includes a <em>precise</em> description of all the necessary steps.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Collecting Data, The Powerful Way</h4>
<p>Did you know that CSS can be used for collecting statistics? Indeed, there's even a CSS-only approach for tracking UI interactions using Google Analytics. <a href="https://www.smashingmagazine.com/2014/10/css-only-solution-for-ui-tracking/" class="btn btn--medium btn--blue">Read a related article&nbsp;→</a></p>
</div>

## Can Internal Marketing Campaigns Be Tracked With UTM Parameters?

<p>Well, <strong>yes and no.</strong> There's no technical problem with using UTM parameters for internal links as well. However, in the context of web analytics, it is definitely <strong>not advisable</strong>! As soon as a visitor clicks on an internal link with UTM parameters, their current session in Google Analytics is ended and a new session is started with the <code>source</code> and <code>medium</code> information from the UTM parameters. This has disagreeable consequences for your data in Google Analytics:</p>

<ul>
<li>The number of <strong>sessions counted increases artificially</strong>, because every click on an internal link with UTM parameters results in a new session.</li>
</ul>
<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee0c6359-4cee-40df-88d0-eebdb622e993/pic-27-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f91e0365-8af3-498b-866d-92ded78d9800/pic-27-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Clicks on an internal link with UTM parameters results in a new session" width="800" height="576" /></a><figcaption>Clicks on an internal link with UTM parameters result in a new session. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee0c6359-4cee-40df-88d0-eebdb622e993/pic-27-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ul>
<li>A conversion can <strong>no longer be traced back to the original, external source of the traffic</strong>, because the new session uses the <code>source</code> and <code>medium</code> information from the UTM parameters, which makes it more difficult to quantify the contribution of various external traffic sources to your conversions.</li>
</ul>
<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f129a26-b21c-472b-8647-71b60790a5f2/pic-28-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d6ce83b-22aa-4292-86ef-ba727e5942a2/pic-28-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="New session uses the source and medium information from the UTM parameters" width="800" height="364" /></a><figcaption>New session uses the <code>source</code> and <code>medium</code> information from the UTM parameters. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f129a26-b21c-472b-8647-71b60790a5f2/pic-28-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ul>
<li>If a new visitor clicks on an internal link with UTM parameters right on the landing page, this immediately results in a new session. The upshot of this is that the <strong>bounce rate for visitors from external sources increases artificially</strong>.</li>
</ul>

<p>Naturally, you want to avoid these negative consequences, because they reduce the quality of your website's analytics.</p>

<p>Nevertheless, the use of UTM parameters to track banners ads and product recommendations is widespread. For one thing, many web analysts are unaware of the problem described above. But the deciding factor is something else: The UTM parameters are <strong>easy to use, very flexible and accessible</strong>, even for the less technically adept among us, which is why they are so <strong>often misused</strong> for internal campaigns.</p>

<p>In my blog post "<a href="https://www.ebernickel.de/blog/teaser-google-analytics-tracken/">Tracking Teasers and Internal Links in Google Analytics</a>" (in German only, unfortunately), I've already covered how clicks on internal banner ads can be monitored and evaluated using event tracking or enhanced e-commerce tracking.</p>

<p>In practice, I've discovered that setting up tracking is too much for many people and/or they don't follow through with it systematically. As a result, they fall back on using the UTM parameters for internal purposes.</p>

<p>So, I asked myself the following question: If the UTM parameters are so popular, can I find a way to track and evaluate internal marketing campaigns using URL parameters?</p>

## Tracking And Evaluating Internal Marketing Campaigns Using URL Parameters

<p>The answer is yes, it is possible!</p>

<p>Not with UTM parameters, because the type of evaluation you can do with these is predetermined in Google Analytics. What we can do, however, is <strong>define a new set of URL parameters that we then use to track internal marketing campaigns</strong>.</p>

<p>I call these parameters simply <strong>ITM parameters</strong>. Instead of using <code>utm_source</code>, <code>utm_medium</code> and so on, you would now use the parameters <code>itm_source</code>, <code>itm_medium</code> and so on for tracking your internal advertising. I consciously took the names of the UTM parameters, so that existing URLs can be easily modified with "find and replace."</p>

<p>OK, let's get started. I'll show you how to use Google Tag Manager and Google Analytics to create a set of URL parameters for tracking internal marketing campaigns and for analyses.</p>

## ITM Parameters At A Glance

<p>Drawing on the UTM parameters, we'll use the following ITM parameters to track internal marketing campaigns:</p>

<ul>
<li><code>itm_source</code>
This identifies the source of the traffic. In the case of internal ads, this is usually your own domain. However, if you employ cross-domain tracking or different ad servers, different traffic sources can appear in this field.</li>
<li><code>itm_medium</code>
This is the medium of the internal ad; for example, a banner or product recommendation.</li>
<li><code>itm_campaign</code>
This is the name of the internal marketing campaign.</li>
<li><code>itm_content</code>
This is a parameter to differentiate between similar content, or links in the same ad; for example, <code>text_link</code> or <code>banner_468x60</code>.</li>
<li><code>itm_term</code>
This is the search keyword that triggered the internal ad. Alternatively, it could be a keyword to categorize the ad by content.</li>
</ul>

<p>A URL that uses all five ITM parameters might look something like this:</p>

<pre><code class="language-markup">
https://www.mydomain.tld/superproduct.htm?<strong>itm_source</strong>=mydomain.tld&amp;<strong>itm_medium</strong>=banner_ad&amp;<strong>itm_campaign</strong>=sale-2017&amp;<strong>itm_content</strong>=banner_468x60&amp;<strong>itm_term</strong>=special_offers
</code></pre>

<p>Now we have to make sure that the information we are collecting with the ITM parameters is passed to Google Analytics and available for analysis.</p>

<p><strong>Note</strong>: To analyze ITM parameters in Google Analytics, we need to create customs reports. In this article, I'll show you how to create these reports, but I've uploaded them to Google Analytics' Solutions Gallery, too! You're free to download the reports <a href="https://analytics.google.com/analytics/web/template?uid=dXLuzPA4RKeeEY8_nFudCA">here</a> and <a href="https://analytics.google.com/analytics/web/template?uid=PNZqpRoqTv-8vk5amQnK5A">here</a>.</p>

## Creating Custom Dimensions In Google Analytics

<p>All of the information that we collect with the ITM parameters should be saved in Google Analytics. To this end, we'll create custom dimensions in Google Analytics. Here, we have to consider their scope: Should we create the new dimensions at the session or hit level?</p>

<p>Let's go back to the UTM parameters for a moment. The UTM parameters are session-level parameters — that is, the information regarding source, medium, campaign and so on applies to the entire session. What this means for internal campaign tracking is that only the information regarding the last link clicked is captured with UTM parameters.</p>

<p>However, if we want to measure the influence of internal ads on conversion rates, then we would be interested in all of the clicks on internal banners, not just the last one. For this reason, it is advisable to create the new dimensions in Google Analytics at the hit level (for example, pageviews) in order to record the individual clicks on banner ads accurately.</p>

<p>The catch is that session-based and hit-based dimensions can only be combined in custom reports in exceptional cases. That means that we can't combine conversions (session level) with individual clicks on banners (hit level), and it means that an internal promotion report, like the one we know from enhanced ecommerce, is not available as a custom report.</p>

<p>So, how do we solve this problem?</p>

<ul>
<li><strong>We could capture the ITM parameters at the session level</strong>.<br/>This allows us to use the predefined campaign reports in Google Analytics as templates for reports on internal marketing campaigns. This is similar to tracking with UTM parameters, which also don't provide detailed information at the hit level. Not ideal, but easy to manage.</li>
<li><strong>Or we could capture the information from the ITM parameters at the hit level</strong>.<br/>Then, we can't establish a direct relationship between the ITM data and conversions. However, we can use data segments to analyze precisely those sessions in which internal banners were clicked and, thus, determine the influence of internal marketing campaigns on conversions.</li>
</ul>

<p>It's up to you which method to use. If you capture the information from the ITM parameters on a session basis, it will be easier to manage the reports in Google Analytics, but the data will be less precise. If you go with the second variant, you will capture very accurate click data for internal banners but will have to invest more time to link this data to your conversions.</p>

<p>Alternatively, you could employ both methods in parallel by creating two custom dimensions for each ITM parameter in Google Analytics: one at the session level, the other at the hit level. Then, you will be free to decide how you want to analyze the data. The disadvantage of this solution is that you need 10 custom dimensions in Analytics to implement it, rather than 5. This might be a critical point, since the free version of Analytics allows a maximum of 20 custom dimensions.</p>

## Creating Dimensions For The ITM Parameters

<p>In the following step, we'll create two sets of dimension: one at the hit level and one at the session level. If you've already decided whether to count clicks on internal ads in sessions only or as hits only, then you'll only need to create the one set that you require.</p>

### Creating New Dimensions at the Hit Level

<p>Click on "Admin" in Google Analytics. Select "Custom Dimensions" under "Custom Definitions" in the "Property" area.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36d0784d-50d7-4aaa-9c14-10d0f9890e84/pic-01-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36d0784d-50d7-4aaa-9c14-10d0f9890e84/pic-01-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Creating custom dimensions at the hit level, step 1." width="290" height="" /></a><figcaption>Creating custom dimensions at the hit level, step 1.</figcaption></figure>

Now click on "+ New Custom Dimension":</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/156d4f4a-70e3-4d25-8489-db341dcf6965/pic-02-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/156d4f4a-70e3-4d25-8489-db341dcf6965/pic-02-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Creating custom dimensions at the hit level, step 2" width="366" height="" /></a><figcaption>Creating custom dimensions at the hit level, step 2.</figcaption></figure>

<ol>
<li>Name the dimension <code>itm_source_h</code>. The <code>_h</code> at the end of the name indicates the scope "Hit."</li>
<li>Select "Hit" as the scope of the dimension.</li>
<li>Now just click "Create."</li>
</ol>

<p>Repeat these steps for the dimensions <code>itm_medium_h</code>, <code>itm_campaign_h</code>, <code>itm_content_h</code> and <code>itm_term_h</code>.</p>

<p>When you're done, you should have five new <strong>dimensions at the hit level</strong> in Google Analytics:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca083950-cd3c-4722-8f64-7fd11a114149/pic-03-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca083950-cd3c-4722-8f64-7fd11a114149/pic-03-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Custom Dimensions at hit level" width="729" height="" /></a><figcaption>Custom dimensions at the hit level</figcaption></figure>

### Creating New Dimensions at the Session Level

<p>Repeat the steps again for the second set of dimensions (at the session level):</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31e9452b-a497-47f2-b08a-9385f1a83cb1/pic-04tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31e9452b-a497-47f2-b08a-9385f1a83cb1/pic-04tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Creating custom dimensions at the session level, step 4" width="351" height="" /></a><figcaption>Creating custom dimensions at the session level, step 4.</figcaption></figure>

<ol>
<li>Name the dimension <code>itm_source_s</code>. The <code>_s</code> at the end of the name indicates the scope "Session."</li>
<li>Select "Session" as the scope of the dimension.</li>
<li>Again, just click "Create."</li>
</ol>

<p>Repeat these steps for the dimensions <code>itm_medium_s</code>, <code>itm_campaign_s</code>, <code>itm_content_s</code> and <code>itm_term_s</code>.</p>

<p>Now, you should have five new <strong>dimensions at the session level</strong> as well:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71c6b743-fea6-455e-a99a-aa0feb6865b2/pic-05-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71c6b743-fea6-455e-a99a-aa0feb6865b2/pic-05-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Custom dimensions at the session level" width="732" height="" /></a><figcaption>Custom dimensions at the session level</figcaption></figure>

## Google Analytics: Excluding Query Parameters

<p>When you add the ITM parameters to your URLs, these enhanced URLs will also be displayed in Google Analytics (for example, in the content reports). In this case, you would see the same page twice: once with the additional ITM parameters and once without. We want to prevent this, because the content of the pages with and without ITM parameters would be identical. Thankfully, Google Analytics provides a simple means of excluding query parameters.</p>

<p>First, select your "Property" in the "Admin" view, and then the desired "data view." Under the "View Settings" menu item, you'll find the section "Exclude URL Query Parameters":</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb13c833-9b81-47da-8f22-c89a93c913f5/pic-06-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb13c833-9b81-47da-8f22-c89a93c913f5/pic-06-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Excluding query parameters" width="706" height="" /></a><figcaption>Excluding query parameters</figcaption></figure>

Enter the ITM parameters that are to be used for tracking in the field provided: <code>itm_source</code>, <code>itm_medium</code>, <code>itm_campaign</code>, <code>itm_content</code>, <code>itm_term</code>.</p>

<p>Then, just save the changes, and we're done here.</p>

## Search Console: Adding ITM Parameters

<p>Remember that the Google Bot will also find your URLs with the ITM parameters. This could mean that these URLs will also land in Google's index and cause <strong>duplicate content</strong>. We can prevent duplicates from arising with a minor tweak in Google Search Console. Select "URL Parameters" from the "Crawl" section in Search Console:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81232c5e-2c3c-489d-a3dc-421a1328a150/pic-07-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81232c5e-2c3c-489d-a3dc-421a1328a150/pic-07-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Search Console: adding ITM parameters, step 1" width="226" height="" /></a><figcaption>Search Console: adding ITM parameters, step 1.</figcaption></figure>

Now click on the "Add Parameter" button to let Google know that the ITM parameter doesn't affect the page's content:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa3fe064-1f2e-4733-8047-e7060e3b2f2f/pic-08-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa3fe064-1f2e-4733-8047-e7060e3b2f2f/pic-08-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Search Console: adding ITM parameters, step 2" width="746" height="" /></a><figcaption>Search Console: adding ITM parameters, step 2.</figcaption></figure>

<ol>
<li>Enter <code>itm_source</code> in the "Parameter" field.</li>
<li>Select the entry "No: Doesn't affect page content (ex: tracks usage)" from the dropdown menu.</li>
<li>"Save."</li>
</ol>

<p>Repeat these steps for the parameters <code>itm_medium</code>, <code>itm_campaign</code>, <code>itm_content</code> and <code>itm_term</code> as well. When you're finished, all of the ITM parameters should be configured as follows:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd0b52bc-2988-4bc8-bd6f-d5f22bc7dd0b/pic-09-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c9bfcca-ca2e-4489-a400-39b68944f409/pic-09-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Search Console: ITM parameters added" width="800" height="324" /></a><figcaption>Search Console: ITM parameters added (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd0b52bc-2988-4bc8-bd6f-d5f22bc7dd0b/pic-09-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

## Setting Up Internal Campaign Tracking In Google Tag Manager

<p>Now that we have laid the groundwork, we finally come to the point that probably interests you the most: How will the ITM parameters be read with Google Tag Manager and be passed to the custom dimensions in Google Analytics?</p>

<p>This is surprisingly easy. All we need to do is store the content of the ITM parameters in user-defined variables and then send them to Google Analytics with the <code>pageview</code> tag. That's it!</p>

<p>Let's begin</p>

### Creating User-Defined Variables

<p>For each of the five ITM parameters, we're going to create a variable in Tag Manager. When a URL that contains one of these parameters is called, its value will be saved in the corresponding variable.</p>

<p>Click on "Variables" in the "Workspace" in Tag Manager and then on "New" under "User-Defined Variables".</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a7d65a8-c81c-4695-91d6-a2eca4bcfdb9/pic-10-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef7c9a45-a76f-4608-9a88-63404a46dfef/pic-10-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Creating user-defined variables, step 1" width="800" height="399" /></a><figcaption>Creating user-defined variables, step 1. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a7d65a8-c81c-4695-91d6-a2eca4bcfdb9/pic-10-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

In the window that opens, we'll define the first variable, <code>itm_source URL-Parameter</code>, where we'll be storing the value from the URL parameter <code>itm_source</code>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56352bd1-9fd5-4e4c-8bdb-0514dfb218d3/pic-11-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c31e4755-974b-4e95-ae90-52a607f5b606/pic-11-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Creating user-defined variables, step 2" width="800" height="417" /></a><figcaption>Creating user-defined variables, step 2. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56352bd1-9fd5-4e4c-8bdb-0514dfb218d3/pic-11-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>Name the variable <code>itm_source URL-Parameter</code>.</li>
<li>Select "URL" as the variable type.</li>
<li>Select "Query" as the component type.</li>
<li>The query key is <code>itm_source</code>. This is the name of the URL parameter that is going to be saved in this variable.</li>
<li>Make sure that "Page URL / Default" is selected under "URL Source."</li>
<li>Click "Save" to finish defining the variable.</li>
</ol>

<p>Repeat these steps for the four other parameters (<code>itm_medium</code>, <code>itm_campaign</code>, <code>itm_content</code> and <code>itm_term</code>).</p>

<p>Once you're finished, there will be five variables available in Tag Manager to save the values from the ITM parameters.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/117b8215-e14a-4f1d-ae65-9ff2d3c09361/pic-12-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c323d3d-06c7-499c-82d5-e0a3a3132650/pic-12-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="User-defined variables in Google Tag Manager" width="800" height="269" /></a><figcaption>User-defined variables in Google Tag Manager (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/117b8215-e14a-4f1d-ae65-9ff2d3c09361/pic-12-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

In this screenshot, you can see not only the five newly created variables (<code>itm_xxx URL-Parameter</code>), but also five additional variables with the type "Constant" (<code>itm_xxx Index</code>). Let's take a closer look at the variable <code>itm_source Index</code>:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36296c42-90b5-4ff3-8138-185860aef924/pic-13-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36296c42-90b5-4ff3-8138-185860aef924/pic-13-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="itm_xxx index variables" width="488" height="" /></a><figcaption><code>itm_xxx</code> index variables</figcaption></figure>

The variable <code>itm_source Index</code> is a constant and has the value <code>14</code>.</p>

<p>What is it good for?</p>

<p>In the next step, we're going to send the contents of the five <code>itm_xxx URL-Parameter</code> variables to the custom dimensions we prepared in Google Analytics. Each of these custom dimensions is addressed using an index number. In the example, the index number for the dimension <code>itm_source</code> is <code>14</code> (see the section "Creating Dimensions for the ITM Parameters"). In your case, the number will probably be different. If you use the custom dimensions in different tags, you will probably have to check the number of the relevant dimension every time in Google Analytics. That's why I like to save the dimension number in its own variable — so that I don't have to remember it. Saving the index numbers in separate variables is not necessary; you can also just address the dimensions in the tag directly with the respective number.</p>

### Enhancing the Pageview Tag for ITM Parameters

<p>Even with the most basic configuration of Google Analytics and Tag Manager, you will have at least one tracking tag activated — namely, the tag used to send the pageviews to Google Analytics. This tag is ideally suited to be enhanced for the ITM parameters.</p>

<p>Click on "Tags" in the "Workspace" in Tag Manager, and then select the tag with the trigger "All Pages":</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aab4953a-89c5-4ebf-b776-8f9cf458c822/pic-14-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6187962-f3fb-4541-85f7-ffc4867477de/pic-14-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Enhancing the Pageview tag, step 1" width="800" height="302" /></a><figcaption>Enhancing the Pageview tag, step 1. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aab4953a-89c5-4ebf-b776-8f9cf458c822/pic-14-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>Clicking on the name of the tag will display its details:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0419f395-3387-45a0-8104-4d69d8192b2f/pic-15-tracking-internal-marketing-campaigns-with-google-analytics-preview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0419f395-3387-45a0-8104-4d69d8192b2f/pic-15-tracking-internal-marketing-campaigns-with-google-analytics-preview.png" alt="Enhancing the Pageview tag, step 2" width="449" height="" /></a><figcaption>Enhancing the Pageview tag, step 2.</figcaption></figure>

Make sure that the "Track Type" is set to "Pageview." This is the tag used to send pageviews to Google Analytics.</p>

<p>Open the configuration page for the tag, and add the ITM parameters:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c86795-83ae-4b71-aa83-555fc7fd42ef/pic-16-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c97d7d-262e-4db1-ae96-3b85b02dae35/pic-16-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Enhancing the Pageview tag, step 3" width="800" height="637" /></a><figcaption>Enhancing the Pageview tag, step 3. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c86795-83ae-4b71-aa83-555fc7fd42ef/pic-16-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>Open the "Custom Dimensions" area.</li>
<li>Click on the button "+ Add Custom Dimension."</li>
<li>Enter the variable <code>{{itm_source Index}}</code> in the "Index" field and the variable <code>{{itm_source URL-Parameter}}</code> in the "Dimension Value" field. In this way, the content of the URL parameter <code>itm_source</code> — which we saved before in the variable <code>itm_source URL-Parameter</code> — will be passed to dimension number 14 in Analytics.</li>
<li>If you don't use variables to save the index numbers, you can simply enter the respective number here (for example, <code>15</code>). Add the four remaining dimensions for the variables <code>itm_medium-URL Parameter</code>, <code>itm_campaign URL-Parameter</code>,<code>itm_content URL-Parameter</code> and <code>itm_term-URL Parameter</code>.</li>
<li>"Save."</li>
</ol>

<p>Here, at the latest, you'll have to decide whether the information from the ITM parameters should be saved at the session or hit level in Google Analytics. In the example above, I used the index numbers of the session-based dimensions. You will have to adjust this according to your needs.</p>

<p>Now that we have enhanced the pageviews tag, don't forget to publish the changes in Tag Manager. Now, when the requested URL contains additional ITM parameters, Tag Manager will read them and pass the information to Google Analytics.</p>

## Evaluating Internal Marketing Campaigns In Google Analytics

<p>After you have finished setting up ITM parameter tracking in Tag Manager, it's time to take a closer look at the analysis options in Google Analytics. In doing so, we will have to decide whether to save the ITM parameters at the session or hit level (see the section "Creating Custom Dimensions in Google Analytics").</p>

## Session-Based Evaluation

<p>If you save the ITM parameters in custom dimensions with the scope "Session," then evaluation of the internal marketing campaign will work in much the same way as with UTM parameters. As I've already mentioned, the disadvantage of this method is that there is only one set of ITM data for the whole session, which is overwritten each time a URL with ITM parameters is clicked. As a result, you will only see the information relating to the last click on an internal banner. Of course, this was already the case when using UTM parameters.</p>

<p>Session-based tracking of ITM parameters is more convenient in terms of web analytics, but less accurate than capturing the ITM parameters at the hit level.</p>

### Creating a Custom Report

<p>The simplest way to create a custom report for evaluating internal marketing campaigns is via the standard reports for campaigns. In Google Analytics, select the report via "Acquisition" → "Campaigns" → "All Campaigns." You can then modify this report to suit your evaluation requirements by clicking on the "Customize" button.</p>

<p>I've made the <a href="https://analytics.google.com/analytics/web/template?uid=dXLuzPA4RKeeEY8_nFudCA">report for session-based evaluation of internal marketing available</a> in the Google Analytics Solutions Gallery.</p>

<p>This is what it looks like:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87eb6855-1d10-411b-aa23-2cf19a7b9aed/pic-17-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2a4fc67-7fae-4b19-bf8f-79ef8b0cbd64/pic-17-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Custom report: internal marketing campaigns (session-based), 1" width="800" height="640" /></a><figcaption>Custom report: internal marketing campaigns (session-based), 1. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87eb6855-1d10-411b-aa23-2cf19a7b9aed/pic-17-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>I named the report "Internal Marketing Campaigns (session-based)."</li>
<li>The report has two <strong>tabs</strong>: an "Explorer," which you can see here, and a "Flat Table," which is visible in the next screenshot.</li>
<li>The "Explorer" tab can have various freely customizable <strong>metric groups</strong>.</li>
<li>The "Explorer" <strong>drills down</strong> through the dimensions <code>itm_campaign_s</code> → <code>itm_content_s</code> → <code>itm_term_s</code>. So, the internal marketing campaign level is immediately visible in this report. The two other dimensions, <code>itm_source_s</code> and <code>itm_medium_s</code>, can be added easily as required.</li>
<li>I included a <strong>filter</strong>, so that the report only displays sessions where the <code>dimension itm_campaign_s</code> is <strong>not empty</strong>.</li>
</ol>

<p>Let's look at the second tab in the report:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57afa709-295e-4b97-8700-e86b8eb567f1/pic-18-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4e01bc3-632d-4ae4-94b4-55668c1c62a2/pic-18-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Custom report: internal marketing campaigns (session-based), 2" width="800" height="500" /></a><figcaption>Custom report: internal marketing campaigns (session-based), 2. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57afa709-295e-4b97-8700-e86b8eb567f1/pic-18-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>This tab features a <strong>flat table</strong> which is well suited for exporting the data.</li>
<li>The table uses all of the session-based <strong>dimensions</strong> that store ITM parameters: <code>itm_source_s</code>, <code>itm_medium_s</code>, <code>itm_campaign_s</code>, <code>itm_content_s</code> and <code>itm_term_s</code>.</li>
<li>The specified <strong>metrics</strong> are freely customizable.</li>
</ol>

<p><strong>Important tip</strong>: The table only displays sessions that have values in all five(!) ITM dimensions. If, for example, you don't use the parameter <code>itm_term</code>, then the dimension <code>itm_term_s</code> will remain empty, which means that no sessions would be displayed in the table. We can eliminate this restriction in two ways: either by removing the unused dimensions from the report or by using Google Tag Manager to set a default value in the dimension if the corresponding ITM parameter is empty. The second option necessitates more work in Tag Manager, as we would then have to distinguish between mandatory parameters and optional parameters.</p>

### Session-Based Evaluation of Internal Marketing Campaigns

<p>With the aid of some simple example data, I'd like to illustrate how the data from internal marketing campaigns is presented in this report.</p>

<p>In the "Explorer" tab, it is possible to combine various dimensions with one another; for example, <code>itm_campaign_s</code> (marketing campaign) and <code>itm_content_s</code> (ad content):</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f781dd-54d4-4c02-bd65-0ff5ac56ad2a/pic-19-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f0ee8a4-d34d-4cd4-ae4d-457f7ba9666c/pic-19-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Session-based evaluation of internal marketing campaigns, 1" width="800" height="235" /></a><figcaption>Session-based evaluation of internal marketing campaigns, 1 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f781dd-54d4-4c02-bd65-0ff5ac56ad2a/pic-19-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

Or you can analyze the effectiveness of internal marketing campaigns in relation to the external traffic sources. This, for instance, is <strong>not possible with UTM parameters</strong>:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7115e786-6f06-4e0a-82cc-a1b551280675/pic-20-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a67f3b36-30ad-48b1-87e5-6e40d18c8bac/pic-20-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Session-based evaluation of internal marketing campaigns, 2" width="800" height="288" /></a><figcaption>Session-based evaluation of internal marketing campaigns, 2 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7115e786-6f06-4e0a-82cc-a1b551280675/pic-20-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

The table contained in the report provides you with a session-based view of all the ITM parameters and makes it simple to export data for further processing in Excel, Google Docs, etc.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a19c59a8-c654-467a-b5c5-8ea501aeed4b/pic-21-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89f0bf77-b456-4777-87e0-5bbbc23d7f23/pic-21-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Session-based evaluation of internal marketing campaigns, 3" width="800" height="219" /></a><figcaption>Session-based evaluation of internal marketing campaigns, 3 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a19c59a8-c654-467a-b5c5-8ea501aeed4b/pic-21-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

## Hit-Based Evaluation

<p>Hit-based evaluation of internal marketing campaigns provides you with an accurate overview of how often specific advertising content has been clicked. However, an additional step is necessary in order to establish the relationship to the conversions achieved. This makes this method of analysis more time-consuming than session-based evaluation. However, it enables more sophisticated analyses.</p>

### Creating a Custom Report

<p>There is no standard report for hit-based evaluation that we can take and customize for our purposes, so we'll have to create our own report that will provide us with information on how often the individual pieces of ad content have been clicked. Based on this report, we will then infer the data segments that we need for our analysis. But first, the report.</p>

<p>I've also <a href="https://analytics.google.com/analytics/web/template?uid=PNZqpRoqTv-8vk5amQnK5A">made this report available</a> in the Google Analytics Solutions Gallery.</p>

<p>This is what it looks like:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81acdd81-3307-413a-ae39-bf2230524125/pic-22-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f04b904b-03d4-4e2c-86e8-174e7416a5fc/pic-22-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Custom report: internal marketing campaigns (hit-based), 1" width="800" height="611" /></a><figcaption>Custom report: internal marketing campaigns (hit-based), 1 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81acdd81-3307-413a-ae39-bf2230524125/pic-22-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>I named it "Internal Marketing Campaigns (hit-based)."</li>
<li>The report has two <strong>tabs</strong>: an "Explorer," which you can see here, and a "Flat Table," which is visible in the next screenshot.</li>
<li>I kept the "Explorer" tab simple; it should provide you with an overview of the usage of internal advertising over time. That's why it only contains a single <strong>metric group</strong> with the metric "Hits."</li>
<li>The "Explorer" <strong>drills down</strong> through the dimensions <code>itm_source_h</code> → <code>item_medium_h</code> → <code>itm_campaign_h</code> → <code>itm_content_h</code> → <code>itm_term_h</code>.</li>
<li>I included a <strong>filter</strong> so that the report only displays sessions in which the <code>dimension itm_source_h</code> is <strong>not empty</strong>.</li>
</ol>

<p>Let's look at the second tab in the report:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc62032-4f7c-4c2f-9228-8335c5d31d89/pic-23-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c2e5668-69f5-4f7f-8ccc-6fac7d480514/pic-23-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Custom report: internal marketing campaigns (hit-based), 2" width="800" height="437" /></a><figcaption>Custom report: internal marketing campaigns (hit-based), 2 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc62032-4f7c-4c2f-9228-8335c5d31d89/pic-23-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>This tab features a <strong>flat table</strong> that provides you with an overview of the clicks on different advertising content and that is well suited for exporting the data.</li>
<li>The table uses all of the hit-based dimensions that store ITM parameters: <code>itm_source_h</code>, <code>itm_medium_h</code>, <code>itm_campaign_h</code>, <code>itm_content_h</code> and <code>itm_term_h</code>.</li>
<li>I only used the metric "<strong>Hits</strong>." The session-based metrics such as number of conversions <strong>cannot be combined</strong> with the selected dimensions.</li>
</ol>

<p><strong>Important tip</strong>: This table also only displays hits that have values in all five(!) ITM dimensions. If, for example, you don't use the parameter <code>itm_term</code>, then the dimension <code>itm_term_h</code> would remain empty, which means that no hits would be displayed in the table. In this case, you would either have to remove the unused dimensions from the table or use default values for the parameters (see above).</p>

### Hit-Based Evaluation of Internal Marketing Campaigns

<p>As I already mentioned, combining hit-based data (such as clicks on internal ads) and session-based data (such as conversions) directly is not possible in Google Analytics. That's why we first use the custom report "Internal Marketing Campaigns (hit-based)" to identify data segments that we can then apply to the acquisition reports, for example.</p>

<p>Let's look at the report, jumping straight to the table this time:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63043097-2ed2-4f96-8839-8b0720eb84e6/pic-24-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f94f683-2d52-4e10-a6c9-d8871811e233/pic-24-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Hit-based evaluation of internal marketing campaigns, 1" width="800" height="396" /></a><figcaption>Hit-based evaluation of internal marketing campaigns, 1 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63043097-2ed2-4f96-8839-8b0720eb84e6/pic-24-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

In the table, we see the number of clicks (hits) on internal ads. The data is grouped based on the combinations of ITM parameters that occurred. In a sense, this is our raw data. Now we have to consider which data segments we can identify:</p>

<ol>
<li>In this example, there is only one internal marketing campaign, but this is already interesting as a data segment. We want to examine more closely how the number of conversions differs between sessions <strong>with and without clicks</strong> on internal ad content.</li>
<li>Then, we drill down a little deeper and differentiate based on the dimension <code>itm_term_h</code>, which identifies ad content with a relationship to web analytics (<code>webanalyse</code>) or AdWords (<code>adwords</code>).</li>
</ol>

<p>Even with so little data, we can continue to slice it up into new segments. For example, you could create segments from the dimensions <code>itm_term_h</code> and <code>itm_content_h</code> to examine which type of ad content works better for <code>itm_term_h = "webanalyse"</code> or <code>itm_term_h = "adwords"</code>. But that's just a side note.</p>

<p>I'm not going to go into the details of creating the data segments. You can see the definition of the segments in their names.</p>

<p>We'll start with the segment <code>itm_campaign_h = marketing2017</code>. To make the difference clearer, I also defined a segment that includes all of the users who didn't click on internal ads. This segment is named <code>itm_campaign_h != marketing2017</code>. <code>!=</code> is the operator for "not equal to."</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/092d8610-e890-4bbe-9178-a1180953adc8/pic-25-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a6998fb-ce16-4121-a9dc-82806ad00377/pic-25-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Hit-based evaluation of internal marketing campaigns, 2" width="800" height="564" /></a><figcaption>Hit-based evaluation of internal marketing campaigns, 2 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/092d8610-e890-4bbe-9178-a1180953adc8/pic-25-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>Even with these two simple segments, we can distinguish between <strong>users who clicked</strong> on internal advertising and <strong>those who didn't</strong>.</li>
<li>We can see significant differences in the number of conversions and the conversion rate.</li>
<li>We can examine the effectiveness of the internal marketing campaign in relation to the traffic sources. This data provides us with valuable starting points for better targeting and optimizing our internal marketing campaigns. Performing this kind of analysis is <strong>impossible if you use UTM parameters</strong>!</li>
</ol>

<p>In the second short analysis, we'll consider the segments <code>itm_term_h = webanalyse</code> and <code>itm_term_h = adwords</code>. These segments enable us to differentiate based on the context of the internal ad with regard to content — in this example, therefore, AdWords (<code>adwords</code>) and Web Analytics (<code>webanalyse</code>).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddab0039-fdf1-4afa-888e-be47404c1afd/pic-26-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd25a51a-05e3-4183-8c48-e69d062816fd/pic-26-tracking-internal-marketing-campaigns-with-google-analytics-800w-opt.png" alt="Hit-based evaluation of internal marketing campaigns, 3" width="800" height="579" /></a><figcaption>Hit-based evaluation of internal marketing campaigns, 3 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddab0039-fdf1-4afa-888e-be47404c1afd/pic-26-tracking-internal-marketing-campaigns-with-google-analytics-large-opt.png">View large version</a>)</figcaption></figure>

<ol>
<li>We can now distinguish between internal ads with the subjects AdWords (<code>adwords</code>) and Web Analytics (<code>webanalyse</code>). Once again, I've activated the segment <code>itm_campaign_h != marketing2017</code> (users without clicks on internal ads) as a control group.</li>
<li>If we look at the number of conversions, we'll notice that the total of the individual segments (3 + 4 + 2 = 9) is <strong>greater than the total number of conversions</strong>. Here we might have expected that the sum of <code>itm_term_h = webanalyse</code> and <code>itm_term_h = adwords</code> would be six conversions, but it is actually seven conversions. This is a <strong>consequence of hit-based evaluation</strong>. It is possible that users click on banner ads for AdWords and banner ads for Web Analytics during a single session. These users would, then, be <strong>part of both data segments</strong>!</li>
</ol>

<p>Naturally, these examples are just a taste of the many analyses that are possible with data segments. But they clearly show how much more the potential for analysis is when clicks on internal ads are captured at the hit level.</p>

## Recommendations

<ul>
<li><strong>Don't use UTM parameters</strong> to track internal marketing campaigns. They are intended for external campaigns. If you use these parameters internally, you'll lose information about the sources of the users' traffic. Moreover, you'll only ever have information about a user's <strong>last click</strong> on an ad.</li>
<li>If you already employ ecommerce tracking on your website, you should check whether you can monitor your internal marketing with <strong>enhanced ecommerce tracking</strong>.</li>
<li>If enhanced ecommerce tracking is not an option for you or you are looking for a solution that's easy to manage, then consider <strong>implementing tracking using ITM parameters</strong>.</li>
<li>A little technical know-how is required to implement this method of tracking, but later on the parameters will be <strong>as easy to use as the UTM parameters</strong>.</li>
<li>Give some thought to <strong>capturing data</strong>: Should clicks on internal banners be saved at the <strong>hit or session level</strong>? Both options have their advantages and disadvantages (<strong>data quality versus the time and effort of analysis</strong>). If necessary, you could even use both options in parallel. Then, you'd need ten custom dimensions in Analytics instead of five. Using both methods in parallel would allow you to compare them directly.</li>
<li>The five ITM parameters that I presented here are not set in stone. I chose them because they make the switch from UTM parameters simple. If you require additional data, <strong>adding further tracking parameters is easy</strong>.</li>
</ul>

<p>All done! This article ended up being much longer than I originally planned.</p>

<p>Thanks for sticking with me right to the end and for taking on the challenges of tracking and analyzing internal marketing campaigns with me. As you've seen, there are a number of decisions to be made and various settings to be configured.</p>

<p>But they're worth the effort — internal advertising is one of the most powerful instruments for generating <strong>more leads, more conversions and more revenue</strong> on your website. In order to employ this instrument profitably, you'll need data that allows for the evaluation and optimization of your internal marketing campaigns. Particularly if you're offering personalized product recommendations and the like, detailed data is indispensable for identifying jumping-off points for optimizations.</p>

<p>All the best in the analysis of your internal marketing campaigns!</p>

### Related Links
<ul>
<li>The reports presented in the article have been uploaded to the <a href="https://analytics.google.com/analytics/gallery/#posts/search/%3F_.term%3Dchristian%20ebernickel%26_.start%3D0/">Google
Analytics Solutions Gallery</a>.</li>
<li>"<a href="https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce">Enhanced Ecommerce</a>" (tracking), Google Analytics</li>
</ul>

{{< signature "da, yk, vf, al, il" >}}

