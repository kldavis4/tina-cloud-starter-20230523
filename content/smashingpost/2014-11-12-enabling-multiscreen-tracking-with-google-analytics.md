---
title: Enabling Multiscreen Tracking With Google Analytics
slug: enabling-multiscreen-tracking-with-google-analytics
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a94344e-2b95-43e5-864e-ac2cd2b852a9/illu-analytics.jpg'
date: 2014-11-12T18:00:20.000Z
author: jamesrosewell
description: >-
  We are increasingly using responsive design, responsive design with
  server-side components (RESS), adaptive design and combinations thereof to
  provide great high-performance multiscreen experiences. However, **analytics
  implementations often miss information** that is important to understanding
  how a website is being used on different devices.

  For example, a website that varies the navigation layout based on screen size
  or user preferences might provide different user flows through the website
  depending on the layout being used. By enhancing Google Analytics, you’ll be
  able to identify and optimize under-performing layouts and screen sizes to
  **improve performance on any device**.
categories:
  - Mobile
  - Devices
  - Analytics
  - Performance
---
We are increasingly using responsive design, responsive design with server-side components (RESS), adaptive design and combinations thereof to provide great high-performance multiscreen experiences. However, analytics implementations often miss information that is important to understanding how a website is being used on different devices.

For example, a website that varies the navigation layout based on screen size or user preferences might provide different user flows through the website depending on the layout being used. By enhancing Google Analytics, you’ll be able to identify and optimize under-performing layouts and screen sizes to <strong>improve performance on any device</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Is Your Responsive Design Working? Google Analytics Will Tell You](https://www.smashingmagazine.com/2014/08/responsive-web-design-google-analytics/)
*   [A Guide To Google Analytics And Useful Tools](https://www.smashingmagazine.com/2009/07/a-guide-to-google-analytics-and-useful-tools/)
*   [Keep Your Analytics Data Safe And Clean](https://www.smashingmagazine.com/2012/04/keep-your-analytics-data-safe-and-clean/)
*   [How To Use Analytics To Build A Smarter Mobile Website](https://www.smashingmagazine.com/2014/03/how-to-use-analytics-to-build-a-smarter-mobile-website/)

This article outlines common challenges and how to configure Google’s new <a title="About universal analytics" href="https://support.google.com/analytics/answer/2790010?hl=en">Universal Analytics</a> to efficiently overcome them, using features such as custom dimensions, enhanced link tracking and server-side data feeds. Information about the user’s layout preferences, the screen’s orientation, which link (of multiple) was used to arrive at a destination, and the physical size of the device’s screen can all be easily added. Universal Analytics enables data to be fed more efficiently from the web server, thus improving performance.

{{% feature-panel %}}

## Common Challenges

### Screen Size

Google Analytics categorizes devices as desktop, mobile or tablet. Information that is important to designers, such as physical screen size, is lost by such segmentation. Consider a web page that performs well on a modern 4.7-inch smartphone (such as the iPhone 6). Suppose a key message appears in the bottom quarter of the screen when displayed on such a device in portrait orientation. The same page on a 3.5-inch smartphone (such as the iPhone 4) would not show this key message without being scrolled down. The designer might not have been aware that this particular message is key to the success of the page. Different device-orientation preferences complicate the challenge further. Analytics tools provide the insight needed to drive continual understanding and improvement.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c71f820-9060-49ee-9569-46d883608c2d/01-multiple-screens-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15c1d7bd-2f27-4af5-9756-a721608d3089/01-multiple-screens-opt-500.png" alt="Information about device types and screen sizes is lost in the default configuration." width="500" height="117" /></a><figcaption>Information about device types and screen sizes is lost in the default configuration. (Image credit: <a title="51Degrees" href="https://51degrees.com/Products/Enhanced-Analysis">51Degrees</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c71f820-9060-49ee-9569-46d883608c2d/01-multiple-screens-opt.png">View large version</a>)</figcaption></figure>

Screen sizes also vary significantly by country. This difference can have a profound effect on a website’s success. The following chart shows average screen sizes of mobile devices in square inches by country, as measured from real web traffic.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d7d1724-fb0f-48c9-ae38-b3ffcbc3262e/02-average-screen-size-by-country-month-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/351dbd5d-c51c-4c9b-b681-7ed4790289f7/02-average-screen-size-by-country-month-opt-500.png" alt="Average mobile device screen size in square inches for South Africa, India and the UK by month" width="500" height="294" /></a><figcaption>Average mobile device screen size in square inches for South Africa, India and the UK by month. (Image credit: <a title="Source of aggregated web activity for custom analysis" href="https://51degrees.com/Products/MobileAnalytics">51Degrees</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d7d1724-fb0f-48c9-ae38-b3ffcbc3262e/02-average-screen-size-by-country-month-opt.png">View large version</a>)</figcaption></figure>

### Layout

Layout is different from physical screen size, although layout is often driven by screen information measured in pixels and device orientation. Understanding the layout being used when analyzing website activity is essential to continual design improvement.

First, consider advertising. Experience shows that a single persistent advert across the top of the web page that remains permanently in view will perform well on a smartphone. On a tablet, skyscraper and banner adverts might work more effectively because a persistent advert is considered annoying.

A commercially minded website owner would want their analytics solution to be able to tell how different ads perform based on the layout and screen size, so that they can identify over- or under-performing configurations and increase their advertising revenue.

The main content is even more important. Information about the active layout for the page — whether determined by media queries or via the user’s preference for a desktop-, smartphone- or tablet-optimized layout — can improve understanding. Consider a page with five primary action rectangles, which are laid out horizontally on a desktop but appear vertically on a smartphone in portrait orientation. The fifth rectangle at the bottom of the list would be viewed less frequently on smartphones. Understanding the impact of this difference in position and viewing probability could lead you to experiment with different positioning for smartphones.</p>

### Performance

Modern websites tend to put greater demand on the client device’s processor. Google Analytics is an example of a tool with small overhead that does not directly enhance the user experience. Additional processing capacity and network resources are needed to execute its functionality, consuming precious battery life. With Universal Analytics, data can now be fed from the server, rather than via JavaScript running in the web browser.</p>

## Bring On Universal Analytics

In late 2013, Universal Analytics left beta, and it is now available for all websites. Google now recommends upgrading to Universal Analytics from Classic. Universal Analytics has several advantages:

1.  The JavaScript snippet and include are more sensitive, improving the quality of the information obtained.
2.  Interacting with and customizing the snippet is easier.
3.  More custom dimensions and metrics are available in the free version.
4.  Options other than JavaScript are available to feed activity information, including from the web server and from Android and iOS applications.

Upgrading to Universal from Classic is a two-step process. First, upgrade the web property via Google Analytics’ administration website. If the property is not already using Universal, then an option will appear under the “Admin” menu advising of the option. However, Google is so keen to upgrade websites that it might have already applied the change for you! If so, then the “Tracking code” page will start with, “This is the Universal Analytics tracking code for this property.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7859bc8c-1b99-4a67-adf7-c77376c66672/03-fonecast-tracking-code-screen-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3087edd9-9e8a-4c46-8bba-483b4e3f635b/03-fonecast-tracking-code-screen-opt-500.png" alt="The screen that confirms a web property’s use of Universal Analytics" width="500" height="228" /></a><figcaption>The screen that confirms a web property’s use of Universal Analytics. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7859bc8c-1b99-4a67-adf7-c77376c66672/03-fonecast-tracking-code-screen-opt.png">View large version</a>)</figcaption></figure>

The second part you’ll have to do yourself: changing the JavaScript snippet on your website. The JavaScript snippet <em>must not</em> be upgraded before the property has been changed to Universal Analytics in the previous step. The simplest implementation is this:

<pre><code class="language-markup">&lt;script&gt; (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){ (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m) })(window,document,'script','//www.google-analytics.com/analytics.js','ga'); ga('create', '[TRACKING_ID]', 'auto'); ga('send', 'pageview'); &lt;/script&gt;
</code></pre>

You would replace <code>[TRACKING_ID]</code> with the unique tracking ID code for your web property.</p>

### Custom Dimensions

Once the upgrade to Universal is complete, you can add information to Google Analytics via “<a title="Developers guide to adding custom dimensions to Google" href="https://developers.google.com/analytics/devguides/platform/customdimsmets">Custom Dimensions</a>.”

Custom dimensions can be defined under the “Property” menu on the “Administration” screen. The following screenshot shows a property without any dimensions configured.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b7f737-cc33-4625-9dee-a655f15d8134/04-fonecast-empty-custom-dimensions-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/072f882c-b06f-43b9-8cc3-65174a29c18a/04-fonecast-empty-custom-dimensions-opt-500.png" alt="Empty list of custom dimensions" width="500" height="323" /></a><figcaption>Empty list of custom dimensions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b7f737-cc33-4625-9dee-a655f15d8134/04-fonecast-empty-custom-dimensions-opt.png">View large version</a>)</figcaption></figure>

Up to 20 dimensions may be added to a property in the free version of Google Analytics, which is 15 more than in the Classic version. The <a title="Information on benefits of Google Analytics Premium" href="https://www.google.com/analytics/premium/">paid version</a> enables 200.</p>

### Device Orientation

Device orientation can easily be calculated in JavaScript by determining the height and width of the window. If the height is larger than the width, then the device is in portrait orientation. If not, then it’s in landscape orientation. The following JavaScript returns an orientation string using this logic:

<pre><code class="language-javascript">window.innerHeight &gt; window.innerWidth ? 'Portrait' : 'Landscape'</code></pre>

By creating a custom dimension and feeding its value from this JavaScript, we can easily add this information about the page request to Google Analytics. The following screenshot shows the simple dialog that is displayed when the “New Custom Dimension” button is pressed. Because the orientation of the device can change during a session, the new custom dimension is added for it, with a scope of “Hit.”

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/605eb98f-838f-48ea-9389-2c63965c5688/05-new-custom-dimension-hit-screen-opt.png" alt="A custom dimension for orientation with a scope of Hit" width="303" height="329" /><br>
<figcaption>A custom dimension for orientation with a scope of “Hit”.</figcaption></figure>

The “Orientation” dimension has been added, with an index starting at “1.” The following screenshot shows the new dimension and its index. At the time of writing, I’m unaware of a way to remove custom dimensions in the free version of Google Analytics, so plan ahead!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a7811ad-c312-4683-b5ef-2112d19d3826/06-orientation-custom-dimension-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d82edc7-647d-4d0c-9f26-5451ea5b35b3/06-orientation-custom-dimension-opt-500.png" alt="Initial list of one custom dimension" width="500" height="113" /></a><figcaption>Initial list of one custom dimension. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a7811ad-c312-4683-b5ef-2112d19d3826/06-orientation-custom-dimension-opt.png">View large version</a>)</figcaption></figure>

### Feeding Custom Dimensions

Now that the dimension has been created for analysis, we need to populate it with data. This entails adding the JavaScript that returns the required data to Google Analytics’ data feed.

Setting an index of the dimension on the “Administration” screen that is the same as the dimension used in the code that sends data to Google Analytics is critical. In this case, the index is “1” and the key field, therefore, is <code>dimension1</code>. The following Google Analytics snippet has been enhanced to add the custom dimension data at an index of 1.</p>

<pre><code class="language-markup">&lt;script&gt;

(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){ (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m) })(window,document,'script','//www.google-analytics.com/analytics.js','ga');  
ga('create', '[TRACKING_ID]', 'auto'); 
<strong>ga('set', 'dimension1', window.innerHeight &gt; window.innerWidth ? 'Portrait' : 'Landscape');</strong>
ga('send', 'pageview');

&lt;/script&gt;</code></pre>

### New Field

A new custom dimension, named “Orientation,” will now be available for analysis. It will appear in the list of available fields under the main heading “Custom Dimensions,” and it can be accessed from segment conditions, as a secondary dimension, and from any other areas of the Google Analytics reporting interface that lists fields.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fba45dea-1783-4644-9961-f593d2c6e5f6/07-using-custom-dimensions-opt.jpg" alt="Custom dimensions included in fields list" width="254" height="336" /><br>
<figcaption>Custom dimensions included in fields list.</figcaption></figure>

### Let It Settle

Patience is a virtue, and time is needed to validate the results of changes. The following screenshot shows the percentage of users by orientation over a one-month period.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e857ae83-f4e8-4cda-a321-1648b3f92e50/08-user-by-orientation-opt.png" alt="Sample analysis of custom dimension orientation" width="313" height="316" /><br>
<figcaption>Sample analysis of custom dimension orientation.</figcaption></figure>

### Screen Size

Third-party data sources can also be used to feed custom dimensions. <a title="Information about 51Degrees" href="https://51degrees.com">51Degrees</a> (the company I founded) can detect information <a title="Device screen properties available with 51Degrees" href="https://51degrees.com/Resources/Property-Dictionary#Screen">about a screen’s physical size</a>, returning the number of square inches or the diagonal length, rounded to the nearest integer value.

Once enabled, segments can be created based on physical screen size to compare different outcomes, answering questions such as:

*   Does the bounce rate vary by physical screen size for particular pages?
*   How is goal completion affected by physical screen size?

Unlike the orientation dimension, physical screen size does not change during a session, so it is added with the “Session” scope.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a37d575-b59a-4f0b-b464-2fcae5d17f04/09-new-custom-dimension-screen-opt.png" alt="Adding a custom dimension to a web property with a scope of Session" width="482" height="525" /><br>
<figcaption>Adding a custom dimension to a web property with a scope of “Session”.</figcaption></figure>

The “<a title="Meta data about the ScreenInchesDiagonalRounded property" href="https://51degrees.com/Resources/Property-Dictionary#ScreenInchesDiagonalRounded">ScreenInchesDiagonalRounded</a>” dimension has been added, with an index of “2.”

Now that the dimension has been created for analysis, we need to populate it with data. To make the examples in this article easy to follow, I’ve created a website that is configured to <a title="Explanation of server-side device detection" href="https://51degrees.com/Products/Device-Detection">detect devices</a> and provide the necessary JavaScript resources. The following snippet includes a resource that provides access to the “ScreenInchesDiagonalRounded” property.</p>

<pre><code class="language-markup">&lt;script src="https://js.51degrees.com/51Degrees.features.js?ScreenInchesDiagonalRounded" type="text/javascript"&gt;&lt;/script&gt;</code></pre>

With the snippet above added before the Google Analytics snippet, the “ScreenInchesDiagonalRounded” dimension (with an index of “2” in the list of custom dimensions) can be populated with the value returned by the “Fifty One Degrees features” include, exposed via the <code>FODF</code> object.</p>

<pre><code class="language-markup">&lt;script&gt;

(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){ (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m) })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', '[TRACKING_ID]', 'auto'); 
ga('set', 'dimension1', window.innerHeight &gt; window.innerWidth ? 'Portrait' : 'Landscape'); 
<strong>ga('set', 'dimension2', FODF.ScreenInchesDiagonalRounded);</strong> 
ga('send', 'pageview');

&lt;/script&gt;</code></pre>

The highlighted additional line of code sets the second dimension to a value of <code>FODF.ScreenInchesDiagonalRounded</code>, which is the screen’s diagonal length in inches, rounded to the nearest integer.</p>

### Insight

The following screenshot shows the percentage of users by physical screen size, measured in inches and over a one-month period.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd003fae-ab52-4cb4-bb94-1a8bea564dd9/10-user-by-screen-inches-diagonal-rounded-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4335ce05-29f0-438e-8812-6e74cfa3602d/10-user-by-screen-inches-diagonal-rounded-opt-500.png" alt="Sample data of custom dimension for screen diagonal" width="500" height="399" /></a><figcaption>Sample data of custom dimension for screen diagonal. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd003fae-ab52-4cb4-bb94-1a8bea564dd9/10-user-by-screen-inches-diagonal-rounded-opt.png">View large version</a>)</figcaption></figure>

We can now clearly identify usage by 3-, 4-, 5- and 6-inch screens within what Google would classify as the “mobile” device type. We can also see that 10-inch screens dominate the “tablet” device type.</p>

### Performance Is King

Measurement should have no impact on the activity being observed. Website analysis performed client-side, as shown earlier, does have a small impact on performance, because the relevant JavaScript needs to be downloaded, parsed and then executed. In both cases,a request is sent to Google Analytics to provide the information associated with the hit or event. While this overhead isn’t noticeable on a fast high-bandwidth data connection, minimize it as much as possible for mobile.

The network resource inspector in modern web browsers such as Chrome clearly shows the problem. The following screenshot shows the <code>51Degrees.features.js</code> request from the earlier example. We see that 76 milliseconds are wasted while the browser waits to send the request for the resource.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b205313f-8a64-4046-a11a-d4d48713af5d/11-blocking-javascript-opt.png" alt="Example of JavaScript being blocked" width="497" height="221" /><br>
<figcaption>Example of JavaScript being blocked.</figcaption></figure>

Fortunately, this problem can be eliminated easily in several ways.</p>

### Asynchronous JavaScript

One approach is to load both the <code>analytics.js</code> file and the features script asynchronously. The <code>onload</code> event of the features script can be used to load the Google Analytics script and set the custom dimensions needed by Google. The following code snippet would replace those provided earlier, including the <code>51Degrees.features.js</code> include.</p>

<pre><code class="language-markup">&lt;script type="text/javascript"&gt;

(function(d,t,s,a,p){ a = d.createElement(t); a.type = 'text/javascript'; a.async = true; a.src = s; p = d.getElementsByTagName(t)[0]; a.onload = function() { (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){ (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m) })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', '[TRACKING_ID]', 'auto'); 
ga('set', 'dimension1', window.innerHeight &gt; window.innerWidth ? 'Portrait' : 'Landscape'); 
ga('set', 'dimension2', FODF.ScreenInchesDiagonalRounded); 
ga('send', 'pageview'); }; 
p.parentNode.insertBefore(a,p); })(document,'script','https://js.51degrees.com/51Degrees.features.js?ScreenInchesDiagonalRounded');

&lt;/script&gt;</code></pre>

Using the network inspector, we can see the difference in the screenshot below.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/237ed270-ecba-4914-aec6-2ccada34eeb7/12-async-javascript-opt.png" alt="Example of JavaScript loading asynchronously" width="434" height="206" /><br>
<figcaption>Example of JavaScript loading asynchronously.</figcaption></figure>

For websites that use downstream caching to reduce the load on the server, this technique is a very efficient way to provide client-specific information to the browser.</p>

### Server-Side

The only way to eliminate the impact of processing and sending information from the client to Google Analytics is to perform this activity on the server. This technique only works when the web server can see all of the traffic and when the web pages are not publicly cached (although the content they contain could still be publicly cached or served from a content delivery network). As such, the technique cannot be used on all websites or all pages.

The Google Analytics code snippet makes a <code>GET</code> request that contains usage and tracking information in the query string. The network inspector reveals the output of Google Analytics’ JavaScript. We see a filter for requests to <code>https://www.google-analytics.com/collect</code> and a request similar to the following:

<pre><code class="language-markup">https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=123456789&amp;t=pageview&amp;_s=1&amp;dl=https%3A%2F%2Fexample.com%2FPage&amp;ul=en-us&amp;de=UTF-8&amp;dt=Page&amp;sd=24-bit&amp;sr=1280x720&amp;vp=1263x622&amp;je=1&amp;fl=14.0%20r0&amp;_u=eDCAgEQi~&amp;jid=&amp;cid=123456789.123456789&amp;tid=UA-123456789-1&amp;cd1=6&amp;z=459486931</code></pre>

Universal Analytics no longer requires that this information be sent from the web browser. It may be sent from anywhere, including the web server or a native application. Google refer to sending data in this way as the “<a title="Google's developer guide to the measurement protocol" href="https://developers.google.com/analytics/devguides/collection/protocol/v1/">measurement protocol</a>.” Sending usage data from the server has the immediate benefit of reducing the amount of processing and the number of web connections taken up by the browser.

At least two HTTP requests are eliminated for each page request because Google’s <code>analytics.js</code> script does not need to load and the resulting request to <code>/collect</code> is also avoided. You could argue that another benefit is that the user can no longer avoid being tracked by turning off requests sent to Google Analytics. Of course, consider the non-technical implications of this, too — namely, as it relates to your terms and conditions and your privacy policy.

The following C# snippet could be added to a .NET web page to send most information to Google Analytics.</p>

<pre><code class="language-c++">var parameters = new Dictionary&lt;string, string&gt;();  

// Add the basic header parameters. 
parameters.Add("v", "1"); 
parameters.Add("t", "pageview"); 
parameters.Add("tid", "INSERT TRACKING ID"); 
parameters.Add("z", Convert.ToBase64String(Guid.NewGuid().ToByteArray()));  

// Add client information. 
if (Request.Cookies[CLIENT_ID_COOKIE_NAME] != null) 
{ 
// Cookie already exists so use that one. 
parameters.Add("cid", 
Request.Cookies[CLIENT_ID_COOKIE_NAME].Value); 
} 
else 
{ 
// This is a new request so set the client ID.
var buffer = new List&lt;byte&gt;&gt;();

// Use the IP address of the client as the first part of the CID. 
IPAddress clientIP; 
if (IPAddress.TryParse(Request.UserHostAddress, out clientIP)) buffer.AddRange(clientIP.GetAddressBytes()); 
else 
buffer.AddRange(Encoding.ASCII.GetBytes(Request.UserHostAddress));  

// Use the date as the second part. 
buffer.AddRange(BitConverter.GetBytes((short)DateTime.UtcNow.Year)); 
buffer.AddRange(BitConverter.GetBytes((byte)DateTime.UtcNow.Month)); 
buffer.AddRange(BitConverter.GetBytes((byte)DateTime.UtcNow.Day)); 
buffer.AddRange(BitConverter.GetBytes((short)DateTime.UtcNow.TimeOfDay.TotalMinutes));  

// Use a hash code of the user agent for the final part. 
buffer.AddRange(BitConverter.GetBytes(Request.UserAgent.GetHashCode()));  

var clientIdCookie = new HttpCookie( 
CLIENT_ID_COOKIE_NAME, 
Convert.ToBase64String(buffer.ToArray()));  

clientIdCookie.HttpOnly = true; 
clientIdCookie.Expires = DateTime.UtcNow.AddYears(2); 
Response.Cookies.Add(clientIdCookie); 
parameters.Add("cid", clientIdCookie.Value); 
} 
parameters.Add("uip", Request.UserHostAddress);  

// If the session is new, indicate this to Google. if (Session != null &amp;&amp; 
Session.IsNewSession) 
{ 
parameters.Add("sc", "start"); 
}  

// Add user agent and device information. 
parameters.Add("ua", Request.UserAgent); 
parameters.Add("je", Request.Browser.JavaScript ? "1" : "0"); 
if (Request.Browser.IsMobileDevice) 
{ 
var screenSize = String.Format( 
"{0}x{1}", 
Request.Browser.ScreenPixelsWidth, 
Request.Browser.ScreenPixelsHeight); 
parameters.Add("sr", screenSize); 
parameters.Add("vp", screenSize); 
}  

// Add language information. 
if (Request.UserLanguages != null &amp;&amp; 
Request.UserLanguages.Length &gt; 0) 
parameters.Add("ul", Request.UserLanguages[0]);  

// Add page information. 
Uri page; 
if (Uri.TryCreate(Request.Url, Request.RawUrl, out page) == false) 
page = Request.Url; 
parameters.Add("dp", page.AbsolutePath); 
if (String.IsNullOrEmpty(Page.Title) == false) 
parameters.Add("dt", Page.Title); 
parameters.Add("dh", page.Host); 
parameters.Add("dl", page.ToString()); 
parameters.Add("de", 
Response.ContentEncoding.WebName.ToUpperInvariant());  

// Add referrer information. 
if (Request.UrlReferrer != null) 
parameters.Add("dr", Request.UrlReferrer.ToString());  

// Add campaign parameters. 
if (Request.QueryString["utm_campaign"] != null) 
parameters.Add("cn", Request.QueryString["utm_campaign"]); 
if (Request.QueryString["utm_content"] != null) 
parameters.Add("cc", Request.QueryString["utm_content"]); 
if (Request.QueryString["utm_term"] != null) 
parameters.Add("ck", Request.QueryString["utm_term"]); 
if (Request.QueryString["utm_medium"] != null) 
parameters.Add("cm", Request.QueryString["utm_medium"]);
if (Request.QueryString["utm_source"] != null) 
parameters.Add("cs", Request.QueryString["utm_term"]);  

// Add user ID information, if known. 
if (Page.User != null &amp;&amp; 
String.IsNullOrEmpty(Page.User.Identity.Name) == false) 
{ 
parameters.Add("uid", Page.User.Identity.Name); 
}  

// Finally, add our custom dimension! 
parameters.Add("dimension2", 
Request.Browser["ScreenInchesDiagonalRounded"]);  

// Build the URL for Google. 
var url = String.Concat( 
"https://ssl.google-analytics.com/collect?", 
String.Join("&amp;", parameters.Select(p =&gt; 
String.Format("{0}={1}", 
p.Key, 
HttpUtility.UrlEncode(p.Value, Encoding.UTF8))).ToArray())); 

// Send the request asynchronously. 
var request = HttpWebRequest.Create(url); 
request.CachePolicy = new 
RequestCachePolicy(RequestCacheLevel.NoCacheNoStore); 
request.Method = "GET"; 
request.Timeout = 20000; 
request.BeginGetResponse(YourCallBackFunction, request);
</code></pre>

That’s a lot of code because we need to do all of the things that the <code>analytics.js</code> snippet does client-side in JavaScript but on the server. At the time of writing, Google does not offer any official code for any platforms.

In the .NET snippet, a collection named <code>parameters</code> is populated with the key-value pairs that will form the query string (often called the “payload”) to be sent to Google Analytics. The following parameters are mandatory in every request:

*   `v` This is the protocol’s version and will always be `1`.
*   `tid` This is the tracking ID, which is the same as the one used in the JavaScript earlier.
*   `cid` The client ID is used to anonymously identify a device, browser or user.
*   `t` This is the type of hit being recorded and will usually be a page view.

Also setting the <code>dp</code> parameter is a good idea because it identifies the page being viewed and is essential to any practical analysis. A full <a title="Google's reference information for measurement protocol" href="https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters">list of the measurement protocol’s parameters</a> is available on Google.

The important line for adding custom dimensions is towards the end, where the <code>dimension2</code> parameter is set. For this line to work, <a title="51Degrees' information about device detection and server side implementations" href="https://51degrees.com/Products/Device-Detection">51Degrees’ device-detection</a> solution must be available on the server. In .NET, the simplest way to add the library is via <a title="How to implement server side detection for .NET using NuGet" href="https://51degrees.com/Support/Documentation/NET/Distributions/Nuget">NuGet</a>. Using <a title="How to implement server side device detection using PHP" href="https://51degrees.com/Support/Documentation/PHP/Getting-Started">PHP device-detection</a>, you can add 51Degrees’ library by unzipping the necessary files and including the scripts in the PHP page. Other languages are supported, including <a title="Implement server side device detection with Java" href="https://51degrees.com/Support/Documentation/Java/Getting-Started">Java</a>, <a title="How to implement server side device detection in Python" href="https://51degrees.com/Support/Documentation/Python/Getting-Started">Python</a>, <a title="Implementing server side device detection with Perl" href="https://51degrees.com/Support/Documentation/Perl/Getting-Started">Perl</a> and <a title="C libraries for device detection" href="https://51degrees.com/Support/Documentation/C/Getting-Started">C</a>.

Another modification to make is to check that the device that is requesting the page is not a crawler. Google Analytics does a reasonable job of removing crawler traffic, but we could help it by checking whether a <a title="Determine if a device accessing a web page is a robot, spider or crawler" href="https://51degrees.com/Resources/Property-Dictionary#IsCrawler">device is a crawler, spider or bot</a> and, if so, not sending any data.</p>

## Tracking Multiple Links

So far, we’ve explored techniques to track page views. Another useful feature in Google Analytics is the capability to track precisely which link is used to navigate to a destination, to track elements that could have more than one destination (such as a search button) or to track actions that are managed in JavaScript. Google calls this feature “<a title="Google's documentation on enhanced link attribution" href="https://support.google.com/analytics/answer/2558867?hl=en">enhanced link attribution</a>.”

Consider a web page that contains three links to the same destination: one in the main navigation menu, one as part of a featured section and the last in the page’s footer. Knowing which of these three links was used to navigate to a destination could help you to improve the design of the page. When combined with data on screen size and (if relevant) the current layout, this information could improve our understanding of how users navigate the website.

Enhanced link tracking can be easily enabled in Universal Analytics via the “Property Settings” menu in the “In-Page Analytics” section, where a form similar to the following screenshot appears:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e08b8ba-5d58-4e01-ba64-168d3981e865/13-configure-enhanced-link-attribution-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3757eaa2-3587-44d3-998d-64e6e5adfa84/13-configure-enhanced-link-attribution-opt-500.png" alt="Configuring enhanced link attribution" width="500" height="171" /></a><figcaption>Configuring enhanced link attribution. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e08b8ba-5d58-4e01-ba64-168d3981e865/13-configure-enhanced-link-attribution-opt.png">View large version</a>)</figcaption></figure>

Simply turn the “Use enhanced link attribution” feature on, and add the following JavaScript line after the <code>create</code> parameter, which includes the tracking ID:

<pre><code class="language-javascript">ga('require', 'linkid', 'linkid.js');</code></pre>

Enhanced link attribution works best when every navigation element on the page has a unique ID attribute, like the one in the following line of code:

### Screen Size

Third-party data sources can also be used to feed custom dimensions. <a title="Information about 51Degrees" href="https://51degrees.com">51Degrees</a> (the company I founded) can detect information <a title="Device screen properties available with 51Degrees" href="https://51degrees.com/Resources/Property-Dictionary#Screen">about a screen’s physical size</a>, returning the number of square inches or the diagonal length, rounded to the nearest integer value.

Once enabled, segments can be created based on physical screen size to compare different outcomes, answering questions such as:

*   Does the bounce rate vary by physical screen size for particular pages?
*   How is goal completion affected by physical screen size?

Unlike the orientation dimension, physical screen size does not change during a session, so it is added with the “Session” scope.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a37d575-b59a-4f0b-b464-2fcae5d17f04/09-new-custom-dimension-screen-opt.png" alt="Adding a custom dimension to a web property with a scope of Session" width="482" height="525" /><br>
<figcaption>Adding a custom dimension to a web property with a scope of “Session”.</figcaption></figure>

The “<a title="Meta data about the ScreenInchesDiagonalRounded property" href="https://51degrees.com/Resources/Property-Dictionary#ScreenInchesDiagonalRounded">ScreenInchesDiagonalRounded</a>” dimension has been added, with an index of “2.”

Now that the dimension has been created for analysis, we need to populate it with data. To make the examples in this article easy to follow, I’ve created a website that is configured to <a title="Explanation of server-side device detection" href="https://51degrees.com/Products/Device-Detection">detect devices</a> and provide the necessary JavaScript resources. The following snippet includes a resource that provides access to the “ScreenInchesDiagonalRounded” property.</p>

<pre><code class="language-markup">&lt;script src="https://js.51degrees.com/51Degrees.features.js?ScreenInchesDiagonalRounded" type="text/javascript"&gt;&lt;/script&gt;</code></pre>

With the snippet above added before the Google Analytics snippet, the “ScreenInchesDiagonalRounded” dimension (with an index of “2” in the list of custom dimensions) can be populated with the value returned by the “Fifty One Degrees features” include, exposed via the <code>FODF</code> object.</p>

<pre><code class="language-markup">&lt;script&gt;

(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){ (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m) })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', '[TRACKING_ID]', 'auto'); 
ga('set', 'dimension1', window.innerHeight &gt; window.innerWidth ? 'Portrait' : 'Landscape'); 
<strong>ga('set', 'dimension2', FODF.ScreenInchesDiagonalRounded);</strong> 
ga('send', 'pageview');

&lt;/script&gt;</code></pre>

The highlighted additional line of code sets the second dimension to a value of <code>FODF.ScreenInchesDiagonalRounded</code>, which is the screen’s diagonal length in inches, rounded to the nearest integer.</p>

### Insight

The following screenshot shows the percentage of users by physical screen size, measured in inches and over a one-month period.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd003fae-ab52-4cb4-bb94-1a8bea564dd9/10-user-by-screen-inches-diagonal-rounded-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4335ce05-29f0-438e-8812-6e74cfa3602d/10-user-by-screen-inches-diagonal-rounded-opt-500.png" alt="Sample data of custom dimension for screen diagonal" width="500" height="399" /></a><figcaption>Sample data of custom dimension for screen diagonal. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd003fae-ab52-4cb4-bb94-1a8bea564dd9/10-user-by-screen-inches-diagonal-rounded-opt.png">View large version</a>)</figcaption></figure>

We can now clearly identify usage by 3-, 4-, 5- and 6-inch screens within what Google would classify as the “mobile” device type. We can also see that 10-inch screens dominate the “tablet” device type.</p>

### Performance Is King

Measurement should have no impact on the activity being observed. Website analysis performed client-side, as shown earlier, does have a small impact on performance, because the relevant JavaScript needs to be downloaded, parsed and then executed. In both cases,a request is sent to Google Analytics to provide the information associated with the hit or event. While this overhead isn’t noticeable on a fast high-bandwidth data connection, minimize it as much as possible for mobile.

The network resource inspector in modern web browsers such as Chrome clearly shows the problem. The following screenshot shows the <code>51Degrees.features.js</code> request from the earlier example. We see that 76 milliseconds are wasted while the browser waits to send the request for the resource.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b205313f-8a64-4046-a11a-d4d48713af5d/11-blocking-javascript-opt.png" alt="Example of JavaScript being blocked" width="497" height="221" /><br>
<figcaption>Example of JavaScript being blocked.</figcaption></figure>

Fortunately, this problem can be eliminated easily in several ways.</p>

### Asynchronous JavaScript

One approach is to load both the <code>analytics.js</code> file and the features script asynchronously. The <code>onload</code> event of the features script can be used to load the Google Analytics script and set the custom dimensions needed by Google. The following code snippet would replace those provided earlier, including the <code>51Degrees.features.js</code> include.</p>

<pre><code class="language-markup">&lt;script type="text/javascript"&gt;

(function(d,t,s,a,p){ a = d.createElement(t); a.type = 'text/javascript'; a.async = true; a.src = s; p = d.getElementsByTagName(t)[0]; a.onload = function() { (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){ (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m) })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', '[TRACKING_ID]', 'auto'); 
ga('set', 'dimension1', window.innerHeight &gt; window.innerWidth ? 'Portrait' : 'Landscape'); 
ga('set', 'dimension2', FODF.ScreenInchesDiagonalRounded); 
ga('send', 'pageview'); }; 
p.parentNode.insertBefore(a,p); })(document,'script','https://js.51degrees.com/51Degrees.features.js?ScreenInchesDiagonalRounded');

&lt;/script&gt;</code></pre>

Using the network inspector, we can see the difference in the screenshot below.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/237ed270-ecba-4914-aec6-2ccada34eeb7/12-async-javascript-opt.png" alt="Example of JavaScript loading asynchronously" width="434" height="206" /><br>
<figcaption>Example of JavaScript loading asynchronously.</figcaption></figure>

For websites that use downstream caching to reduce the load on the server, this technique is a very efficient way to provide client-specific information to the browser.</p>

### Server-Side

The only way to eliminate the impact of processing and sending information from the client to Google Analytics is to perform this activity on the server. This technique only works when the web server can see all of the traffic and when the web pages are not publicly cached (although the content they contain could still be publicly cached or served from a content delivery network). As such, the technique cannot be used on all websites or all pages.

The Google Analytics code snippet makes a <code>GET</code> request that contains usage and tracking information in the query string. The network inspector reveals the output of Google Analytics’ JavaScript. We see a filter for requests to <code>https://www.google-analytics.com/collect</code> and a request similar to the following:

<pre><code class="language-markup">https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=123456789&amp;t=pageview&amp;_s=1&amp;dl=https%3A%2F%2Fexample.com%2FPage&amp;ul=en-us&amp;de=UTF-8&amp;dt=Page&amp;sd=24-bit&amp;sr=1280x720&amp;vp=1263x622&amp;je=1&amp;fl=14.0%20r0&amp;_u=eDCAgEQi~&amp;jid=&amp;cid=123456789.123456789&amp;tid=UA-123456789-1&amp;cd1=6&amp;z=459486931</code></pre>

Universal Analytics no longer requires that this information be sent from the web browser. It may be sent from anywhere, including the web server or a native application. Google refer to sending data in this way as the “<a title="Google's developer guide to the measurement protocol" href="https://developers.google.com/analytics/devguides/collection/protocol/v1/">measurement protocol</a>.” Sending usage data from the server has the immediate benefit of reducing the amount of processing and the number of web connections taken up by the browser.

At least two HTTP requests are eliminated for each page request because Google’s <code>analytics.js</code> script does not need to load and the resulting request to <code>/collect</code> is also avoided. You could argue that another benefit is that the user can no longer avoid being tracked by turning off requests sent to Google Analytics. Of course, consider the non-technical implications of this, too — namely, as it relates to your terms and conditions and your privacy policy.

The following C# snippet could be added to a .NET web page to send most information to Google Analytics.</p>

<pre><code class="language-c++">var parameters = new Dictionary&lt;string, string&gt;();  

// Add the basic header parameters. 
parameters.Add("v", "1"); 
parameters.Add("t", "pageview"); 
parameters.Add("tid", "INSERT TRACKING ID"); 
parameters.Add("z", Convert.ToBase64String(Guid.NewGuid().ToByteArray()));  

// Add client information. 
if (Request.Cookies[CLIENT_ID_COOKIE_NAME] != null) 
{ 
// Cookie already exists so use that one. 
parameters.Add("cid", 
Request.Cookies[CLIENT_ID_COOKIE_NAME].Value); 
} 
else 
{ 
// This is a new request so set the client ID.
var buffer = new List&lt;byte&gt;&gt;();

// Use the IP address of the client as the first part of the CID. 
IPAddress clientIP; 
if (IPAddress.TryParse(Request.UserHostAddress, out clientIP)) buffer.AddRange(clientIP.GetAddressBytes()); 
else 
buffer.AddRange(Encoding.ASCII.GetBytes(Request.UserHostAddress));  

// Use the date as the second part. 
buffer.AddRange(BitConverter.GetBytes((short)DateTime.UtcNow.Year)); 
buffer.AddRange(BitConverter.GetBytes((byte)DateTime.UtcNow.Month)); 
buffer.AddRange(BitConverter.GetBytes((byte)DateTime.UtcNow.Day)); 
buffer.AddRange(BitConverter.GetBytes((short)DateTime.UtcNow.TimeOfDay.TotalMinutes));  

// Use a hash code of the user agent for the final part. 
buffer.AddRange(BitConverter.GetBytes(Request.UserAgent.GetHashCode()));  

var clientIdCookie = new HttpCookie( 
CLIENT_ID_COOKIE_NAME, 
Convert.ToBase64String(buffer.ToArray()));  

clientIdCookie.HttpOnly = true; 
clientIdCookie.Expires = DateTime.UtcNow.AddYears(2); 
Response.Cookies.Add(clientIdCookie); 
parameters.Add("cid", clientIdCookie.Value); 
} 
parameters.Add("uip", Request.UserHostAddress);  

// If the session is new, indicate this to Google. if (Session != null &amp;&amp; 
Session.IsNewSession) 
{ 
parameters.Add("sc", "start"); 
}  

// Add user agent and device information. 
parameters.Add("ua", Request.UserAgent); 
parameters.Add("je", Request.Browser.JavaScript ? "1" : "0"); 
if (Request.Browser.IsMobileDevice) 
{ 
var screenSize = String.Format( 
"{0}x{1}", 
Request.Browser.ScreenPixelsWidth, 
Request.Browser.ScreenPixelsHeight); 
parameters.Add("sr", screenSize); 
parameters.Add("vp", screenSize); 
}  

// Add language information. 
if (Request.UserLanguages != null &amp;&amp; 
Request.UserLanguages.Length &gt; 0) 
parameters.Add("ul", Request.UserLanguages[0]);  

// Add page information. 
Uri page; 
if (Uri.TryCreate(Request.Url, Request.RawUrl, out page) == false) 
page = Request.Url; 
parameters.Add("dp", page.AbsolutePath); 
if (String.IsNullOrEmpty(Page.Title) == false) 
parameters.Add("dt", Page.Title); 
parameters.Add("dh", page.Host); 
parameters.Add("dl", page.ToString()); 
parameters.Add("de", 
Response.ContentEncoding.WebName.ToUpperInvariant());  

// Add referrer information. 
if (Request.UrlReferrer != null) 
parameters.Add("dr", Request.UrlReferrer.ToString());  

// Add campaign parameters. 
if (Request.QueryString["utm_campaign"] != null) 
parameters.Add("cn", Request.QueryString["utm_campaign"]); 
if (Request.QueryString["utm_content"] != null) 
parameters.Add("cc", Request.QueryString["utm_content"]); 
if (Request.QueryString["utm_term"] != null) 
parameters.Add("ck", Request.QueryString["utm_term"]); 
if (Request.QueryString["utm_medium"] != null) 
parameters.Add("cm", Request.QueryString["utm_medium"]);
if (Request.QueryString["utm_source"] != null) 
parameters.Add("cs", Request.QueryString["utm_term"]);  

// Add user ID information, if known. 
if (Page.User != null &amp;&amp; 
String.IsNullOrEmpty(Page.User.Identity.Name) == false) 
{ 
parameters.Add("uid", Page.User.Identity.Name); 
}  

// Finally, add our custom dimension! 
parameters.Add("dimension2", 
Request.Browser["ScreenInchesDiagonalRounded"]);  

// Build the URL for Google. 
var url = String.Concat( 
"https://ssl.google-analytics.com/collect?", 
String.Join("&amp;", parameters.Select(p =&gt; 
String.Format("{0}={1}", 
p.Key, 
HttpUtility.UrlEncode(p.Value, Encoding.UTF8))).ToArray())); 

// Send the request asynchronously. 
var request = HttpWebRequest.Create(url); 
request.CachePolicy = new 
RequestCachePolicy(RequestCacheLevel.NoCacheNoStore); 
request.Method = "GET"; 
request.Timeout = 20000; 
request.BeginGetResponse(YourCallBackFunction, request);
</code></pre>

That’s a lot of code because we need to do all of the things that the <code>analytics.js</code> snippet does client-side in JavaScript but on the server. At the time of writing, Google does not offer any official code for any platforms.

In the .NET snippet, a collection named <code>parameters</code> is populated with the key-value pairs that will form the query string (often called the “payload”) to be sent to Google Analytics. The following parameters are mandatory in every request:

*   `v` This is the protocol’s version and will always be `1`.
*   `tid` This is the tracking ID, which is the same as the one used in the JavaScript earlier.
*   `cid` The client ID is used to anonymously identify a device, browser or user.
*   `t` This is the type of hit being recorded and will usually be a page view.

Also setting the <code>dp</code> parameter is a good idea because it identifies the page being viewed and is essential to any practical analysis. A full <a title="Google's reference information for measurement protocol" href="https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters">list of the measurement protocol’s parameters</a> is available on Google.

The important line for adding custom dimensions is towards the end, where the <code>dimension2</code> parameter is set. For this line to work, <a title="51Degrees' information about device detection and server side implementations" href="https://51degrees.com/Products/Device-Detection">51Degrees’ device-detection</a> solution must be available on the server. In .NET, the simplest way to add the library is via <a title="How to implement server side detection for .NET using NuGet" href="https://51degrees.com/Support/Documentation/NET/Distributions/Nuget">NuGet</a>. Using <a title="How to implement server side device detection using PHP" href="https://51degrees.com/Support/Documentation/PHP/Getting-Started">PHP device-detection</a>, you can add 51Degrees’ library by unzipping the necessary files and including the scripts in the PHP page. Other languages are supported, including <a title="Implement server side device detection with Java" href="https://51degrees.com/Support/Documentation/Java/Getting-Started">Java</a>, <a title="How to implement server side device detection in Python" href="https://51degrees.com/Support/Documentation/Python/Getting-Started">Python</a>, <a title="Implementing server side device detection with Perl" href="https://51degrees.com/Support/Documentation/Perl/Getting-Started">Perl</a> and <a title="C libraries for device detection" href="https://51degrees.com/Support/Documentation/C/Getting-Started">C</a>.

Another modification to make is to check that the device that is requesting the page is not a crawler. Google Analytics does a reasonable job of removing crawler traffic, but we could help it by checking whether a <a title="Determine if a device accessing a web page is a robot, spider or crawler" href="https://51degrees.com/Resources/Property-Dictionary#IsCrawler">device is a crawler, spider or bot</a> and, if so, not sending any data.</p>

## Tracking Multiple Links

So far, we’ve explored techniques to track page views. Another useful feature in Google Analytics is the capability to track precisely which link is used to navigate to a destination, to track elements that could have more than one destination (such as a search button) or to track actions that are managed in JavaScript. Google calls this feature “<a title="Google's documentation on enhanced link attribution" href="https://support.google.com/analytics/answer/2558867?hl=en">enhanced link attribution</a>.”

Consider a web page that contains three links to the same destination: one in the main navigation menu, one as part of a featured section and the last in the page’s footer. Knowing which of these three links was used to navigate to a destination could help you to improve the design of the page. When combined with data on screen size and (if relevant) the current layout, this information could improve our understanding of how users navigate the website.

Enhanced link tracking can be easily enabled in Universal Analytics via the “Property Settings” menu in the “In-Page Analytics” section, where a form similar to the following screenshot appears:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e08b8ba-5d58-4e01-ba64-168d3981e865/13-configure-enhanced-link-attribution-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3757eaa2-3587-44d3-998d-64e6e5adfa84/13-configure-enhanced-link-attribution-opt-500.png" alt="Configuring enhanced link attribution" width="500" height="171" /></a><figcaption>Configuring enhanced link attribution. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e08b8ba-5d58-4e01-ba64-168d3981e865/13-configure-enhanced-link-attribution-opt.png">View large version</a>)</figcaption></figure>

Simply turn the “Use enhanced link attribution” feature on, and add the following JavaScript line after the <code>create</code> parameter, which includes the tracking ID:

<pre><code class="language-javascript">ga('require', 'linkid', 'linkid.js');</code></pre>

Enhanced link attribution works best when every navigation element on the page has a unique ID attribute, like the one in the following line of code:

<pre><code class="language-markup">&lt;a href='NewPage.html' id='NewPageLink1'&gt;Goto another page&lt;/a&gt;</code></pre>

If the ID attribute isn’t present, then Google Analytics will try to identify the element based on the position of the element in the DOM. However, this is not as reliable.</p>

## Multiple Views

Google’s <code>analytics.js</code> script automatically tracks the size of the screen and the active viewport via JavaScript detection. You can use this information to analyze how responsive web pages perform at different breakpoints without additional modification.

For websites that enhance responsive design with RESS or adaptive techniques (varying the page’s content or navigation based on the user’s preference for a particular view type), then this information should be provided to Google Analytics for subsequent analysis. When this preference is a part of the page’s URL structure (for example, prefixing the domain name with an <code>m.</code> for the mobile-optimized section), then the information will automatically be made available to Google Analytics.</p>

### Different Techniques

The main problem with URLs that vary based on characteristics such as device type is that they don’t work very well when shared. For example, someone on a phone who wants to tweet the URL of an interesting page might share the <code>m.</code> version of the URL. Followers who open the link would be presented with the <code>m.</code> variant of the page, which will be suboptimal if they’re on a tablet or desktop.

A far better technique is to vary the response of a URL according to the device type <em>and</em> the user’s preference for a particular view. All of Microsoft’s new web technologies now favour model-view-controller (MVC) design. RESS and adaptive design are particularly <a title="Information on using MVC5 to alter layout server side" href="https://51degrees.com/Blog/ArtMID/1641/ArticleID/254/Mobile-and-Tablet-Device-Detection-with-MVC5">easy to implement in MVC</a> because the view is designed to be altered based on knowledge of the client device or user preferences, thus improving performance and the user experience. For example, someone on a 4.5-inch phone might prefer to pinch and zoom on the desktop interface of a website if they’re more familiar with it or if it contains more information.

By default, Google Analytics does not provide this insight. It categorizes devices as desktop, mobile or tablet only. When a page’s layout changes, an enhancement is needed to provide information associated with the active view.

The following screenshots are of the same URL, featuring a table that compares device-detection options. The layouts for small-screen devices and for big-screen web browsers are obviously different.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe2eb1d9-07b5-4ffd-8404-e07f5099cf8f/14-device-detection-options-compared-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09cbf12-b335-4458-be25-67561dab8284/14-device-detection-options-compared-opt-500.png" alt="The table's layout changes according to the user's selected view." height="204" /></a><figcaption>The table’s layout changes according to the user’s selected view. (Image credit: <a title="Compare different device detection data sets from 51Degrees" href="https://51degrees.com/Products/Device-Detection/Compare-Device-Data">51Degrees</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe2eb1d9-07b5-4ffd-8404-e07f5099cf8f/14-device-detection-options-compared-opt.png">View large version</a>)</figcaption></figure>

If the user has not expressed a preference for a view type, then the URL will default to serving content that is optimized for the device type. The user may change the view at any time should they not be happy with the default. They might prefer the big-screen version and be content to pinch and zoom around the page. We need to track this information in Google Analytics because it provides important insight into the viewing preferences of users.</p>

### Custom Dimensions

Custom dimensions can be used to record this information. The following screen shows a “ViewType” custom dimension being added, with a scope of “Hit.”

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad806799-e3b9-4518-9e61-e282867e7a6f/15-edit-custom-dimension-screen-opt.png" alt="Editing a custom dimension in Google Analytics with scope of Hit" width="463" height="496" /><br>
<figcaption>Editing a custom dimension in Google Analytics with scope of “Hit”.</figcaption></figure>

Assuming that “ViewType” is given an index of “3,” the following lines of JavaScript could be added to determine the active view based on the presence of different menu element IDs on the page.</p>

<pre><code class="language-javascript">var activeView = 'Desktop'; 
if (document.getElementById('mobileHeader') != undefined) { activeView = 'SmartPhone'; 
} else if (document.getElementById('tabletHeader') != undefined) { activeView = 'Tablet'; 
} 
ga('set', 'dimension3', activeView);
</code></pre>

Once sufficient information is stored in Google Analytics, the activity can be segmented by different view types. The following screenshot shows an example of such a report.

Two view type segments compared

## Conclusion

It has been only three years since Ethan Marcotte published <a title="Ethan Marcotte response web design book" href="https://www.abookapart.com/products/responsive-web-design"><em>Response Web Design</em></a> and web designers started thinking “mobile first.” The techniques used to analyze website activity haven’t kept pace with the different approaches to creating user interfaces. By tracking user preferences, combining complementary data sources and making simple configuration changes, we can narrow the gap. We can use server-side techniques to improve efficiency, and we can use hard facts to make design decisions, rather than our perception alone.

Universal Analytics is a powerful tool, and it is prepared for a world in which designers get a single report of all interactions, including for websites, native applications and real-world events (such as visits to a physical store or interactions with a call center). We’ve explored the possibilities a bit in this article. Here are some features to consider exploring further:

*   **See how users interact across multiple sessions.**.  If unique and anonymous user IDs are available in your web application, then use the “[User ID](https://developers.google.com/analytics/devguides/collection/analyticsjs/user-id "Google's User ID tracking")” feature of Google Analytics to track users across multiple sessions. Be aware that your privacy policy must allow for this and must adhere to Google’s requirements for anonymity.
*   **Track activity beyond the web.**.  Integrate Google Analytics in [native applications](https://developers.google.com/analytics/devguides/collection/ios/ "Google's native application tracking developers guide for iOS") alongside websites for a complete view of digital user behavior.
*   **Track JavaScript events that don’t result in a full page refresh.** Use [events](https://developers.google.com/analytics/devguides/collection/gajs/eventTrackerGuide "Google's event tracking reference guide") to track activity on a web page that does not result in a new page being loaded.

Whatever you do next, a bit of simple customization and configuration can make a big difference to the insights you get from Google Analytics. Happy analyzing!

{{< signature "da, ml, al" >}}

