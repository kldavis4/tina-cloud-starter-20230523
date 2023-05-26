---
title: 'Picking A Mobile Support Strategy For Your Website'
slug: picking-a-mobile-support-strategy-for-your-website
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f71464d3-ff25-4bea-82f3-7fe34b8afd15/auto-text-adjustment-larger.jpg
date: 2011-07-11T11:35:36.000Z
author: matt-lawson
summary: >-
  Increasing mobile support for browser platforms could lead to a better experience, but at what cost? Mobile strategies can vary massively from website to website, depending on what the company wants to offer visitors. Matt Lawson takes a look at some of the more common approaches.
description: >-
  Mobile strategies for browser platforms can vary massively from website to website, depending on what the company wants to offer visitors. Matt Lawson takes a look at some of the more common approaches.
categories:
  - Mobile
  - UX
  - Design Patterns
  - Strategy
---

The number of people browsing the Web from a mobile device has more than tripled since 2009, and it is sure to continue growing, with browser platforms such as iOS and Android offering mobile browser support that is almost identical to what we have come to expect from a desktop experience. As the mobile consumer market continues to grow, so will the aspirations of individuals and companies who look to embrace what the mobile Web has to offer.

With this in mind, many website owners have begun to develop a strategy for providing information and services to their mobile visitors. However, mobile strategies can vary massively from website to website, depending on what the company wants to offer visitors. For example, eBay’s strategy will be very different from an individual’s strategy for a portfolio website, which might simply be to improve readability for those viewing on a mobile device.

So, as website owners define the level of support they aim to provide, a scale of support for mobile devices emerges. Picking where on the scale your website should sit can be quite tricky; each level of support is not without its pros and cons. Let’s take a look at some of the more common approaches:

{{% feature-panel %}}

## Approach A: Tweak What You Have

The most basic and, thus, quickest option is to do only what is required to get the website to work on mobile devices. I use the word “work” loosely here because it can be very subjective, but the main goal is to ensure that the website displays and functions properly on mobile devices and perhaps similarly to the desktop experience.

Sure, delivering a desktop experience on a mobile device is not ideal by any stretch of the imagination, but this option simply offers the **minimum** required to get the website to function and display **OK**. With modern mobile devices offering good CSS support and zooming functionality, visitors should at least be able to access the information they need.

### How to Implement This Approach?

Simple tweaks could include adjusting the viewport and text size, which will affect the way the website displays on a mobile device. The default viewport dimensions should work well for most layouts, but we can make adjustments using the <code>meta</code> element:

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=device-width" /&gt;</code></pre>

Text size can also be adjusted for some mobile devices using the CSS <code>text-size-adjust</code> property which specifies a size adjustment for displaying text content:

<pre><code class="language-css">html {
-webkit-text-size-adjust: auto; /* Automatically adjusted for Safari on iPhone. */
-ms-text-size-adjust: auto; }</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f71464d3-ff25-4bea-82f3-7fe34b8afd15/auto-text-adjustment-larger.jpg"><img loading="lazy" decoding="async"  class="97274 alignnone" title="iPhone text size adjustment example" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9883db89-eb35-4d12-9b18-e093c221c767/text-size-adjustment.gif" alt="An example of three iPhone screens with text size adjust set to auto, None and 200%" width="550" height="271" /></a><figcaption>Different text-size-adjust values demonstrated on the iPhone.</figcaption></figure>

More information on the <code>text-size-adjust</code> property is available in the <a href="https://developer.apple.com/library/safari/#documentation/appleapplications/reference/safariwebcontent/Introduction/Introduction.html#//apple_ref/doc/uid/TP40002079-SW1">Safari Developer Library</a>. With a small number of tweaks, you should be able to optimize your website to appear as usable as the desktop experience.

Be careful when making any adjustments to the CSS for mobile visitors: you do not want desktop users ending up with a 200% font size by default! If you think this might happen or you want to further improve the experience, consider putting the CSS in a separate file:

<pre><code class="language-markup tmp-html">&lt;link rel="stylesheet" href="…" media="handheld, only screen and (max-device width: 480px)" /&gt;</code></pre>

**Pros:**

*   Quick to implement;
*   Minimal work required to replicate the desktop design;
*   Strong brand identification with basic consideration for mobile visitors.

**Cons:**

*   Mobile users could suffer from a poor experience;
*   Slow due to users downloading styles and large assets;
*   Content and navigation path are not optimized for mobile visitors.

### Other Resources

*   [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
*   [Responsible Considerations For Responsive Web Design](https://www.smashingmagazine.com/2013/03/responsible-web-design/)
*   [Losing Users If Responsive Web Design Is Your Only Strategy](https://www.smashingmagazine.com/2014/07/responsive-web-design-should-not-be-your-only-mobile-strategy/)

## Approach B: Adaptive Layout (Media Queries)

Media-dependent styling has been around for a long time; you will almost certainly have used “media types” before:

<pre><code class="language-markup tmp-html">&lt;link rel="stylesheet" href="…" media="print" /&gt;</code></pre>

Media queries, on the other hand, have really started to gain popularity since browser vendors began to support the <a href="https://www.w3.org/TR/css3-mediaqueries">W3C’s CSS3 “Media Queries” specification</a>.

Recommended reading: [Responsively Retrofitting An Existing Site With RWD Retrofit](https://www.smashingmagazine.com/2013/03/18/retrofit-a-website-to-be-responsive-with-rwd-retrofit/)

Most modern browsers, including mobile ones, should now be able to query such things as width, height, device width and height, orientation and more. This has led to more people using media queries to provide responsive designs to their visitors:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/161b2088-74e0-407e-bb52-132f3842916f/hicks-larger.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="97277" title="adaptive layout on hicks design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8f75ebc-6b97-4b12-8f77-9d908a050095/hicks-design.gif" alt="Screenshots of the Hicksdesign website, demonstrating adaptive layouts using media queries" width="550" height="273" /></a><figcaption>Hicksdesign demonstrates adaptive layouts using media queries.</figcaption></figure>

For older browsers, including Internet Explorer 6 to 8, several solutions are available that add some level of support for media queries, such as <a href="https://github.com/scottjehl/Respond">Respond.js</a> by Scott Jehl.

### How to Implement This Approach?

We can target specific resolutions and device sizes. For example, we could target mobile devices with a maximum device width of 480 pixels, such as the iPhone:

<pre><code class="language-markup tmp-html">&lt;link rel="stylesheet" media="only screen and (max-device-width: 480px)" href="mobile.css" /&gt;</code></pre>

Or we could put the same media query in our CSS file:

<pre><code class="language-css">@media only screen and (max-device-width: 480px) {
    // insert styling here…
}</code></pre>

Adaptive layouts need to work with the content already available on your website. This means that the source order and mark-up can play a vital role in providing a logical order to content when linearized for narrow layouts. You will also need to take into account that images will need to scale to fit as their containing elements adapt to different layouts. One way to achieve this is to specify a maximum width:

<pre><code class="language-css">img { max-width: 100%; }</code></pre>

You could consider providing the mobile experience as the default and the desktop experience through media queries, an idea discussed by both <a href="https://www.lukew.com/presos/preso.asp?26">Luke Wroblewski</a> and <a href="https://www.broken-links.com/2011/02/21/using-media-queries-in-the-real-world/">Peter Gasston</a>. Combining this approach with something like <a href="https://host.sonspring.com/adaptive_css/">Adapt.js</a> or <a href="https://stuffandnonsense.co.uk/projects/320andup/">320 and up</a> could improve performance for mobile visitors.

However, making the mobile experience the default isn’t without its own problems. Always consider your audience, and review visitor data before finalizing your approach.

**Pros:**

*   Quick to develop, especially when considered from the start;
*   Cheap to produce because minimal additional design is required;
*   Can result in improved readability and experience for mobile visitors.

**Cons:**

*   Older mobile and desktop browsers, including Internet Explorer 8, do not natively support media queries;
*   Visitors could face a short learning curve if the navigation and layout are altered;
*   Rendering could potentially be slower as images and non-critical content in the HTML are being downloaded.

Both approach A and approach B beautifully embrace the <a href="https://adactio.com/journal/1716/">"One Web"</a> philosophy which sees the Web as one universal medium that should adjust itself to the different environment of its users. Using mobile tweaks and media queries can help to keep the website a standalone, universal entity optimized for both mobile and desktop user experiences. As Jeremy Keith writes in his article,
<blockquote>“Recent developments in areas like <a href="https://stevesouders.com/">performance</a> and <a href="https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/">responsive design</a> means that we can realistically pursue that vision of serving up content at a URL to everyone to the best ability of their device. At the same time, the opposite approach&mdash;creating multiple, tailored URLs&mdash;is currently a popular technique.”

&mdash; Jeremy Keith, <a href="https://adactio.com/journal/1716/">One Web</a></blockquote>

We will discuss the latter approach in the next sections of this article.

{{% ad-panel-leaderboard %}}

### Other Resources

*   [Responsive Web Design: What It Is and How To Use It](https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/)
*   [How to Use CSS3 Media Queries to Create a Mobile Version of Your Website](https://www.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/)
*   [High-Performance Mobile](https://calendar.perfplanet.com/2010/high-performance-mobile/)

## Approach C: A Dedicated Mobile Website

A website dedicated to mobile users aims to deliver an optimized, and often very different, experience to visitors. These micro or mobile websites can take on a life of their own and often require a lot of research and analysis in order to prioritize and deliver the most important content to users.

Mobile websites from the likes of eBay and Amazon show a very different strategy than their desktop equivalents because screen space and file sizes are at a premium.

### How to Implement This Approach?

A dedicated mobile website will normally reside on its own domain or sub-domain, such as <a href="https://mobile.twitter.com">mobile.twitter.com</a>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e7d8d5a-c2e0-4cff-bcd7-102ab8c62820/twitter-larger.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="97278" title="twitter full vs mobile website" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e7c96fa-1e6a-4aa9-9256-9b97739b8920/twitter.gif" alt="The full and mobile version of Twitter demonstrated on an iPhone" width="550" height="346" /></a><figcaption>The main Twitter home page and the mobile version on an iPhone.</figcaption></figure>

Redirecting mobile traffic to a dedicated website ensures that visitors arrive in the right place. But if you do this, provide a link to **allow visitors to access to the full version**! Also make sure that mobile users are redirected to the correct page when deep linking from another source.

Assets such as images should be kept to a minimum. And popular content, common tasks and key navigational paths should be highlighted to give users exactly what they want. More often than not, there is no room for advertisements in mobile versions.

Despite the extra work, the result can be a faster, more streamlined experience that puts the most important features and content at the user’s fingertips.

**Pros:**

*   Greatly improved performance;
*   Optimized paths make it easy and fast for users;
*   Enhances your support of and appeal to growing mobile consumer market.

**Cons:**

*   Relatively expensive to build and maintain;
*   Time-consuming because assets must be optimized and content prioritized;
*   Higher learning curve if the layout and content are very different from the desktop versions.

### Other Resources

*   [A Study of Trends in Mobile Design](https://www.smashingmagazine.com/2010/12/02/a-study-of-trends-in-mobile-design/)
*   [Lessons From Mobile Web Design](https://www.webdesignerdepot.com/2011/04/lessons-from-mobile-web-design/)
*   [How to Build a Mobile Website](https://www.smashingmagazine.com/2010/11/03/how-to-build-a-mobile-website/)

## Approach X: Native Apps

Finally, another option to consider is a native app. Apps can be the ultimate in an optimized, streamlined journey for visitors, and they often have native controls. Several properties, such as eBay, Twitter and Amazon, have clear user goals and have therefore invested time and effort into creating native apps that provide the best possible experience on a wide range of devices.

### How to Implement This Approach?

A native app should provide the best possible experience for users on the go, while taking full advantage of device-specific features and controls. This approach is very different from the others described, and the project could be considered “ad hoc” development, correlating more closely to the user’s goals than the content or features on your website.

If this appeals to you, consider using an SDK, such as the ones available from PhoneGap and Appcelerator. These SDKs enable developers with a Web background to create applications and tap into native APIs that are not always available in the browser. Native app development can be quite bespoke and is sometimes undertaken parallel to the main website.

Facebook, which offers a native app, is a good example of how a integrated approach can ensure that content is accessible through full, mobile, touch and app versions, each optimized for the best possible experience.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dc98c40-0d85-47b9-af7d-2ff7fc4ad312/facebook-larger.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="97298" title="The different faces of facebook" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/633cd5c5-8019-4ffd-a78e-27184cf25cbb/fb1.gif" alt="Screen shots demonstrating the full, mobile, touch and app version of Facebook as seen on an iPhone" width="550" height="192" /></a><figcaption>Facebook can be accessed through full, mobile, touch and native app interfaces.</figcaption></figure>

**Pros:**

*   Streamlined journeys;
*   Device controls are native and optimized for platform in terms of speed and performance;
*   Incredibly lightweight, with minimal bandwidth usage.

**Cons:**

*   Requires bespoke development;
*   Creating and maintaining apps for a range of devices is time-consuming;
*   Third-party approval is required before the app is available in stores.

## Which Approach Is Right For You?

**Approach A** and **Approach B** offer varying levels of support and often could be considered as a “quick win” strategy. Consider them if you want to improve the experience and optimize readability for mobile visitors at minimal cost.

A strongly related design strategy would be to start with a mobile layout of the website first, having a strong focus on content and navigation and then extend the mobile experience to larger desktop experiences. You can find some interesting workflow techniques for this strategy in Luke Wroblewski’s conference notes of Ethan Marcotte’s talk <a href="https://www.lukew.com/ff/entry.asp?1314">The Responsive Designer’s Workflow</a>. For instance, you might need to consider using server-side media queries as well as fluid images in the development process.

**Approach C** requires considerably more time to develop and maintain but results in a faster, more streamlined website for task-oriented visitors. **Approach X** requires significantly more time to develop and approval from third-party app stores. But it might be ideal if your brand has many mobile users who expect a flawless experience. The main problem with these two approaches is that they aren’t scalable as new mobile devices might require new versions of the websites which increases costs and makes maintenance more difficult.

Ultimately, your approach should be guided by your content, objectives and visitors. What might work in theory doesn’t necessarily work in practice. A bit of digging in your analytics might show that a large proportion of visitors are on mobile devices, and so the extra time spent improving their experience would be worth it. Once you have all of the data, you can make an informed decision about which approach will benefit you &mdash; and more importantly &mdash; your visitors.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Supporting Your Product: How To Provide Technical Support](https://www.smashingmagazine.com/2011/10/supporting-product-providing-technical-support/)
*   [How To Deliver Exceptional Client Service](https://www.smashingmagazine.com/2012/01/how-to-deliver-exceptional-client-service/)
*   [Improving Customer Service with UX](https://www.smashingmagazine.com/2011/11/improving-customer-experience-meet-problem-users/)
*   [Taking A Customer From Like To Love](https://www.smashingmagazine.com/2011/08/taking-a-customer-from-like-to-love-the-ux-of-long-term-relationships/)

{{< signature "mrn" >}}
