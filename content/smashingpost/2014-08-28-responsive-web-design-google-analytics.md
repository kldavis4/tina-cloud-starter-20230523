---
title: Is Your Responsive Design Working? Google Analytics Will Tell You
slug: responsive-web-design-google-analytics
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dfb74f9-edf5-4b03-bc9e-fa99d2e06611/18-google-analytics-opt.png
date: 2014-08-28T22:03:39.000Z
author: jon-arne-and-luca-passani
description: >-
  Responsive web design has become the dominant method of developing and
  designing websites. It makes it easier to think “mobile first” and to **create
  a website that is viewable on mobile devices**. In the early days of
  responsive web design, creating breakpoints in CSS for particular screen sizes
  was common, like 320 pixels for iPhone and 768 pixels for iPad, and then we
  tested and monitored those devices.

  As responsive design has evolved, we now more often start with the content and
  then set breakpoints when the content “breaks.” This means that you might end
  up with quite a few content-centric breakpoints and no particular devices or
  form factors on which to test your website.
categories:
  - Mobile
  - JavaScript
  - Data Visualization
  - Analytics
  - Responsive Design
---
Responsive web design has become the dominant method of developing and designing websites. It makes it easier to think “mobile first” and to create a website that is viewable on mobile devices.

In the early days of responsive web design, creating breakpoints in CSS for particular screen sizes was common, like 320 pixels for iPhone and 768 pixels for iPad, and then we tested and monitored those devices. As responsive design has evolved, we now more often start with the content and then set breakpoints when the content “breaks.” This means that you might end up with quite a few content-centric breakpoints and no particular devices or form factors on which to test your website.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Guide To Google Analytics And Useful Tools](https://www.smashingmagazine.com/2009/07/a-guide-to-google-analytics-and-useful-tools/)
*   [Keep Your Analytics Data Safe And Clean](https://www.smashingmagazine.com/2012/04/keep-your-analytics-data-safe-and-clean/)
*   [Enabling Multiscreen Tracking With Google Analytics](https://www.smashingmagazine.com/2014/11/enabling-multiscreen-tracking-with-google-analytics/)
*   [How To Use Analytics To Build A Smarter Mobile Website](https://www.smashingmagazine.com/2014/03/how-to-use-analytics-to-build-a-smarter-mobile-website/)

However, we are just guessing that our designs will perform well with different device classes and form factors and across different interaction models. <strong>We need to continually monitor a design’s performance with real traffic</strong>.

{{% feature-panel %}}

Content-centric breakpoints are definitely the way to go, but they also mean that monitoring your website to identify when it breaks is more important. This information, when easily accessible, provides hints on what types of devices and form factors to test further.

Google Analytics has some <a href="https://www.smashingmagazine.com/2014/03/03/how-to-use-analytics-to-build-a-smarter-mobile-website/">great multi-device features</a> built in; however, with responsive design, we are really designing for form factors, not for devices. In this article, we’ll demonstrate how <a href="https://wurfl.io">WURFL.js</a> and Google Analytics can work together to show performance metrics across form factors. No more guessing.</p>

## Why Form Factor?

Speeding up and optimizing the user experience for a particular device or family of devices is always easier. In reality, though, creating a <a href="https://developers.facebook.com/blog/post/2012/01/24/device-experiences---responsive-design/">device-specific experience</a> for all types of devices is not feasible, given that the diversity of web-enabled devices will just continue to grow. However, every device has a particular form factor. <a href="https://www.lukew.com/">Luke Wroblewski</a>, author of <a href="https://www.lukew.com/resources/mobile_first.asp"><em>Mobile First</em></a>, outlines <a href="https://developers.facebook.com/blog/post/2012/01/24/device-experiences---responsive-design/">three categories to identify device experiences</a>:

*   usage or posture,
*   input method,
*   output or screen.

Because devices vary between these categories, we get different form factors. Hence, treating form factor as the primary dimension through which to monitor a responsive website makes sense. This will indicate which type of device to test for usability.

The examples in this article all use WURFL.js, including the form factors provided by it, which are:

*   desktop,
*   app,
*   tablet,
*   smartphone,
*   feature phone,
*   smart TV,
*   robot,
*   other non-mobile,
*   other mobile.</p>

## Feeding Data To Google Analytics

The first step is to put WURFL.js on the pages that you want to track. Simply paste this line of code into your markup:

<pre><code class="language-markup">&lt;script type="text/javascript" src="//wurfl.io/wurfl.js"&gt;&lt;/script&gt;
</code></pre>

This will create a global WURFL object that you can access through JavaScript:

<pre><code class="language-javascript">console.log(WURFL.form_factor);
</code></pre>

Now that the <code>script</code> tag is in place, the only other thing to do is add the highlighted lines of code to Google Analytics’ tracking code:

<pre><code class="language-javascript">/* Google Analytics' standard tracking code */
_gaq.push(['_setAccount', 'UA-99999999-1']);
_gaq.push(['_setDomainName', example.com']);
_gaq.push(['_trackPageview']);

/* Tell Google Analytics to log WURFL.js' data */
 _gaq.push(['_setCustomVar',	1,’complete_device_name’,WURFL.complete_device_name,1]);
 _gaq.push(['_setCustomVar',	2,'form_factor',WURFL.form_factor,1]);
 _gaq.push(['_setCustomVar',	3,'is_mobile',WURFL.is_mobile,1]);

/* The rest of Analytics' standard tracking code */
(function() {
var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
</code></pre>

Or, if you have updated to Google Analytics’ new <a href="https://support.google.com/analytics/answer/2790010?hl=en">“Universal Analytics</a><span style="text-decoration: underline;">"</span>, you would add this:

<pre><code class="language-javascript">/* Google Analytics' new universal tracking code */
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','//www.google-analytics.com/analytics.js','ga');
ga('create', 'UA-99999999-1, 'auto');

/* Define the custom dimensions */
ga('send', 'pageview', {
  'dimension1': WURFL.complete_device_name,
  'dimension2': WURFL.form_factor,
  'dimension3': WURFL.is_mobile
});

</code></pre>

Further, if you are using GA Universal Analytics, you must remember to define the custom dimensions. You do that by clicking <code>Admin</code> → <code>Custom Definitions</code> → <code>Custom Dimensions</code>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12a32334-0bc5-4d49-a91c-98061121c18e/gacustomdim-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f93a71c-d98c-4d5e-acbd-37a4378d9cb9/gacustomdim-preview-opt.png" alt="GAcustomdim-preview-opt" width="500" height="136" /></a><figcaption>For Universal Analytics you need to define the custom dimensions in the <code>Admin</code> section. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12a32334-0bc5-4d49-a91c-98061121c18e/gacustomdim-large-opt.png">Large preview</a>)</figcaption></figure>

## Analyzing The Data In Google Analytics

Now that the data is in Google Analytics, we need to make it available for inspection. We can use custom variables in Analytics in a number of ways, the most obvious being to look in the menu on the left and click <code>Audience</code> → <code>Custom</code> → <code>Custom Variables</code>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/709867a0-91f2-4cd1-aef3-da5f28d5047d/image01-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05022f70-e95c-4733-8abe-961304272635/image01-preview-opt.png" alt="Custom Variables Report" width="500" height="192" /></a><figcaption>“Custom Variables” report. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/709867a0-91f2-4cd1-aef3-da5f28d5047d/image01-large-opt.png">Large version</a>)</figcaption></figure>

If you are are using Universal Analytics, you'll have the custom dimensions available as any other dimension in all reports in GA:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6512f1b-6c85-4aef-9c50-e064cead5bbc/gauicustomdim-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c620ebd-078a-40a7-ab34-50d3e657acb4/gauicustomdim-preview-opt.png" alt="GAUIcustomdim-preview-opt" width="500" height="182" /></a><figcaption>Accessing custom dimensions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6512f1b-6c85-4aef-9c50-e064cead5bbc/gauicustomdim-large-opt.png">Large preview</a>)</figcaption></figure>

Already, we’re getting a pretty good picture of how form factors behave differently. The best metrics to focus on will obviously depend on your website, but in general, pay attention to bounce rate and pages per visit.</p>

### Big Picture With Dashboard Widgets

With <a href="https://support.google.com/analytics/answer/1068216?hl=en">dashboards</a> in Google Analytics, we get a high-level overview of the most important metrics. This is a good place to monitor how your website performs across form factors. Once again, bounce rate and page impressions per visit are good metrics to start with. The purpose of the dashboard widgets is to alert you and to visualize how your website’s performance changes for certain form factors.

Let’s create a few widgets to display the status of different form factors. First, create a pie-chart widget that shows how much your website is being used by different form factors.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f71806a1-a227-49bd-b2f4-a84d38a47627/image05-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5910dce7-6a90-4c72-8e79-0e5a01156860/image05-preview-opt.png" alt="Widget displaying form factors" width="500" height="269" /></a><figcaption>Widget displaying form factors. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f71806a1-a227-49bd-b2f4-a84d38a47627/image05-large-opt.png">Large version</a>)</figcaption></figure>

In the Dashboard, click <code>Add Widget</code>, select <code>Pie</code>, then the <code>Sessions</code> metric, and group it by the <code>form factor</code> custom variable. Note that the label in the green drop-down list is <code>Custom Variables</code>, not the actual name. In our example, the <code>form factor</code> variable is in the second slot, but make sure to choose the right slot if you’ve implemented it in a different order. Again, if you have converted to Universal analytics, the procedure is similar, but in stead of selecting custom variables, you simply add the name of your custom dimension as you would with any other dimension.

Next, create a few widgets to display visits and <a href="https://support.google.com/analytics/answer/1009409?hl=en">bounce rates</a> per form factor. The widgets will indicate whether changes to the website have had a positive or negative impact. Obviously, you want higher visits and a lower bounce rate.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/057aafdf-e784-4aa2-a031-de1ebb5e6a58/image00-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e02b9ec5-d987-4b6e-88c5-d54a6e068e87/image00-preview-opt.png" alt="Creating a “form factor” widget" width="500" height="285" /></a><figcaption>Creating a “form factor” widget. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/057aafdf-e784-4aa2-a031-de1ebb5e6a58/image00-large-opt.png">Larger version</a>)</figcaption></figure>

Create this widget by adding a filter to the standard metrics. Choose a timeline diagram and filter the data with your custom variable where you have stored the form factor. Create one widget for each of the form factors that you want to monitor:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd4b9da-1b2b-452e-ab71-e4a1b0acc832/image04-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1388ac90-1c3d-4730-8ca6-a89f77cc4dc9/image04-preview-opt.png" alt="“Form factor” widgets in the dashboard" width="500" height="169" /></a><figcaption>“Form factor” widgets in the dashboard. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd4b9da-1b2b-452e-ab71-e4a1b0acc832/image04-large-opt.png">Large version</a>)</figcaption></figure>

You might find that some form factors disappear in the statistics for global bounce rates because the data set is now bigger (as in the example above). As indicated by the red arrows, something dramatic has happened with smartphones and feature phones. Specifically, some changes were made to the landing page to increase traffic from tablets, and the changes clearly had a negative impact on traffic from smartphones and feature phones. Identifying the reason for the drop in traffic requires more fine-grained Analytics reports, and the drop might not have been easy to spot without having monitored form factors.</p>

### Form Factor Segments

Any custom variable that you put into Google Analytics is, of course, available in most reports as filters or dimensions, so tweaking them to your needs is quite easy. Another way to keep form factors at the top of mind is to put them in <a href="https://support.google.com/analytics/topic/3123779?hl=en&amp;ref_topic=1727148">segments</a> by creating conditions. Here is one segment per form factor that you’ll want to track:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417da339-56e7-487c-9a3b-2b8f1f8d389e/image03-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd48f1d8-60d7-4d89-9255-6f48d190ed59/image03-preview-opt.png" alt="Configure a segment" width="500" height="187" /></a><figcaption>Configure a segment. If you're using Universal Analytics, you must use your custom dimensions rather than the custom variables. (<a title="Larger image" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417da339-56e7-487c-9a3b-2b8f1f8d389e/image03-large-opt.png">Large version</a>)</figcaption></figure>

The same, but in Universal Analytics:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a6b147a-7d30-4ac2-9185-ed1fa909b5c9/gacustomin2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b810a8a5-94a1-4481-9e49-22e4331775fa/gacustomin2-preview-opt.png" alt="GAcustomin2-preview-opt" width="500" height="191" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a6b147a-7d30-4ac2-9185-ed1fa909b5c9/gacustomin2-large-opt.png">Large preview</a>)</figcaption></figure>

Google Analytics will show these segments in most of its standard reports as separate dimensions in charts and tables:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a884b7e-75f8-4f35-bd29-155d410d4be6/image02-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/568e064b-7d24-447a-a8dd-2c00be4c54ec/image02-preview-opt.png" alt="Segments chart" width="500" height="157" /></a><figcaption>Segments chart. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a884b7e-75f8-4f35-bd29-155d410d4be6/image02-large-opt.png">Large version</a>)</figcaption></figure>

You can make “form factor” a dimension in most reports. As mentioned, bounce rate and general engagement are key metrics to follow, but goals and conversion rate are obviously interesting, too. You might find the need to create new goals or at least review your funnel for certain form factors.

After monitoring form factors for a while, you might conclude that you need to offer different user experiences for one or more form factors. Furthermore, you might need to tweak goals, funnels and advertising campaigns to account for differences in usage per form factor or device type.

We have used Google Analytics here, but WURFL.js is, of course, compatible with other analytics tools, as long as custom variables like the ones above are allowed.</p>

## Conclusion

In this article, we have looked at how performance per form factor is a key metric for monitoring a website and how WURFL.js and Google Analytics help to visualize this data. Once you put WURFL.js’ data into Analytics, it will be available in most standard reports as filters or dimensions, so tweaking the reports to your needs is quite straightforward. And the dashboard widgets will give you a high-level overview of their status. Also, bounce rate and page impressions per visit are key metrics, at least to start; so, defining form factors as segments will give you nice visualizations in most standard reports.

As a next step, look into conversions and goals in Google Analytics to see how to integrate and monitor form factors, which will vary according to the website’s function and purpose. To give you a head start, we have made a <a href="https://www.google.com/analytics/web/template?uid=gUP6PNubRZ6qlqhq4M2g2Q">template that you can install</a> in your Google Analytics dashboard (This template uses custom variables, not custom dimensions). Just follow the instructions to assign an Analytics property, which will then appear under <code>Dashboards</code> → <code>Private.</code>

{{< signature "al, ml, il" >}}

