---
title: 'How To Optimize Email Newsletters With CSS'
slug: from-monitor-to-mobile-optimizing-email-newsletters-with-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4961d5be-c1a0-40e6-b16d-4dfd144b2416/checkered-illustration.jpg
date: 2011-08-18T08:15:00.000Z
author: ros-hodgekiss
summary: >-
  Using CSS in email newsletters: what works, where it’s going and what you should do next? Ros Hodgekiss brings you a few ideas on how to start coding email designs with improved readability and usability when viewed in Web, mobile and email desktop clients alike. 
description: >-
  Thinking about using CSS in email newsletters? Find a few ideas on how to start coding email designs with improved readability and usability when viewed in Web, mobile and email desktop clients alike.
categories:
  - Mobile
  - CSS
  - Newsletters
  - Responsive Design
  - Content Strategy
  - Emails
---

HTML email has a reputation for being a particularly tough design medium. So tough, in fact, that many designers regard coding and testing even the simplest email design to be almost as bad as fixing display quirks in Internet Explorer 6, and only slightly better than a tooth extraction. So, it’s with much courage that I tell you today about using CSS in email newsletters: what works, where it’s going and what you should do next.

After reading this article, you will hopefully come away with a few ideas on how to start coding email designs with improved readability and usability when viewed in Web, mobile and email desktop clients alike. Also included are a variety of resources to get you on the right path with using CSS in email.

Then again, the shaky state of email standards today may convince you that plain-text email is the way to go. The choice is yours.

{{% feature-panel %}}

## CSS In HTML Email: The Good, The Bad And The Mobile-Ready

If you’re about to embark on your first HTML email coding job, then you probably come from a Web background and are keen to flex a little CSS3 muscle, get a little JavaScript action happening, drop those shadows…

Not so fast. As any old hat to the email game can tell you, what works on the Web and what works in email are about as far apart as Sydney and Stockholm. For the most part, this is because pretty much every email client has its own way of doing things; while there are perhaps half a dozen browsers to test against when coding a Web page, there are literally dozens of email clients, many of which feature radically different CSS implementations.

But before you give up hope, here’s some advice to get you through the night:

*   A lot of CSS properties (such as `font`, `color` and `border`) work fine across many of the most popular email clients. [Once you know which ones they are](https://www.campaignmonitor.com/css/), you can tailor your designs accordingly.
*   When a CSS property doesn’t work so well, there are often workarounds (such as using `cellpadding` in tables instead of `padding`).
*   When workarounds don’t exist, focus on graceful degradation.
*   Your design will never look exactly the same across all email clients, no matter how you use CSS. Once you (and your clients) make peace with this, I guarantee you will sleep better at night.
*   Keep it simple. The less complicated your design and layout, the less likely something will go wrong. Favor table layouts over divs, and make sure your message is readable (which means text, not images).

At this point, you may be saying to yourself, “Well, this all just sounds too hard.” So, perhaps I should remind you how beautiful an HTML email can look, with just a sprinkling of CSS:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f8cb7ba-07e2-450a-81ef-46ebd0b6de41/top100-email-opt.jpg" alt="HTML email with a sprinkling of CSS" width="500" height="407" /><figcaption>An HTML email example.</figcaption></figure>

For a more realistic view of what this design will look like in the inbox, here’s the same email in Gmail, a notoriously tricky email clients to work with:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fd144bf-20d6-407c-9859-e111d632f046/top100-gmail-desktop-opt.jpg" alt="HTML email in Gmail" width="500" height="407" /><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2a98598-b98e-405e-8102-42a35531be44/top100-gmail-expanded-opt.jpg">View expanded version</a>)</figcaption></figure>

See? Ain’t so bad after all. But what’s more exciting is how you can use CSS to adapt an HTML email for optimal display on mobile devices. Here’s the same newsletter as viewed on a smartphone:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d2dd2c6-e4cb-4dda-ac2a-0f188af7e98e/top100-iphone-opt.jpg" alt="Newsletter displayed on smartphone" width="500" height="407" /><figcaption>The same email viewed on a smartphone.</figcaption></figure>

Applying a mobile-specific style sheet has improved the readability of the email considerably, allowing us to remove unnecessary whitespace that would have taken up valuable real estate on a small screen.

So, we’ve gone from an email layout that may have required a lot of pinching and zooming, to one that can be easily read with a linear scrolling motion, using CSS alone. We’ll look at how you can apply similar improvements to your email campaigns in a moment. But first, let’s start with some of the fundamentals of using CSS in your HTML email designs.

## The State Of CSS Support In Email Today

When I mentioned that a lot of CSS properties out there work fine in many email clients, I wasn’t trying to be vague. Thankfully, the research into what works and what doesn’t has already been done. You need only skim this <a href="https://www.campaignmonitor.com/css/">guide to CSS support in email clients</a> to see what properties are within and off limits. Or just know that most of your CSS rendering troubles will come from Outlook 2010, Lotus Notes and Gmail, due to their refusal to do anything useful with CSS style sheets.

These issues are nothing new. Indeed, the battle for market share between email clients that play nice with CSS versus those that don’t has been pitched for years now. But progress is being made. Looking at the <a href="https://www.campaignmonitor.com/guides/email-marketing-trends/">data from over 4 billion emails sent</a>, we found that mobile email clients have gained ground dramatically, with 42% of emails now opened on a mobile device. Here is how desktop, Web and mobile email clients have fared comparatively over the last five years:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/282e7769-c14d-46fe-84b8-0a46bb1d36df/email-marketing-trends-opt.png" alt="Desktop, Web and mobile email client market share, 2011 to 2014" width="500" height="364" /><figcaption>Desktop, Web and mobile email client market share, 2011 to 2014. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/311f861c-c52b-47c1-a099-790d476adad3/email-marketing-trends.png">View large version</a>)</figcaption></figure>

Mobile’s ascent is great news for email designers everywhere for one reason: nearly 90% of mobile email is read on an iOS device. iOS devices use the <a href="https://www.webkit.org/">WebKit rendering engine</a>, which means they can display really nice-looking HTML emails.

Our friends at <a href="https://panic.com/">Panic</a> (the creators of such popular Mac titles as Coda) were well aware of this when they got started on their email announcements. As purveyors of Mac software, they can pretty much always count on their emails being read in Webkit-powered email clients like Apple Mail and the iPhone. As a result, they’ve been able to pull a lot of CSS3 trickery out of the toolbox, including web fonts and SVG masks:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2080dfa3-7315-45e9-8915-e6de4a327ab7/diet-coda-opt.png" alt="Diet Coda’s newsletter" width="500" height="352" /><figcaption>CSS3 trickery.</figcaption></figure>

But what really impressed me was their <a href="https://www.dropbox.com/s/dlv9qgrmxf1bqrv/panic-example.mov?dl=0">use of CSS3 animation</a>. Here’s the code they used to achieve the "Ken Burns" zoom effect:

<pre><code class="language-css">@-webkit-keyframes kennethburns {
from { -webkit-transform: scale(1.5) }
to { -webkit-transform: scale(1) }
}</code></pre>

And you thought HTML email was a boring medium? Well, to temper things a bit, CSS3 still has very limited support beyond a handful of Webkit-powered email clients, so use it with discretion.

{{% ad-panel-leaderboard %}}

## Inside An HTML Email Builder’s Toolkit

Before we go charging in and dropping <code>@media</code> queries by the dozen, let’s make sure we have the tools for the job. We’ll need the following:

*   An email marketing service like [MailChimp](https://www.mailchimp.com) or [Campaign Monitor](https://campaignmonitor.com) to send HTML email campaigns (you can’t do this from desktop or Web email clients like Gmail &mdash; sorry);
*   Code editing software, such as [Coda](https://www.panic.com/coda) or [Sublime Text](https://www.sublimetext.com);
*   A mobile device to test on (like an iPhone or Android device);
*   A variety of Web and desktop email accounts to test, either set up individually or automated via a service such as [Litmus](https://www.litmusapp.com);
*   An intermediate-level understanding of HTML and CSS;
*   A lot of patience.

In addition, you’ll need a way to move your CSS inline, for the benefit of clients like Gmail, which strip out the <code>head</code> section of HTML email code. Many email marketing apps can do this automatically when you import your campaign, but if yours doesn’t, then you can use a service like <a href="https://inliner.cm">inliner.cm</a> for the job.

Now that you’re armed and dangerous, let’s launch into the theory and code behind mobile email design.

## Using CSS To Optimize Your Email For Mobile Devices

If you’ve created mobile style sheets for the Web or have read into responsive design, then you probably know a bit about <a href="https://alistapart.com/article/responsive-web-design"><code>@media</code> queries</a>. If not, then here’s the skinny: they allow you to provide targeted CSS style sheets that are triggered when a device’s capabilities match specific criteria. For example, you could use a media query to specify that a couple of lines of CSS be applied exclusively to devices with a display width of up to 480 pixels, in order to make your website or email easier to read on these screens.

The following is a snippet of code from the earlier newsletter, telling mobile email clients and browsers to scale down the width of the email layout to 300/325 pixels wide, so that it fits comfortably on displays that are no wider than 480 pixels (i.e. the width of an iPhone 5 in landscape mode):

<pre><code class="language-css">@media only screen and (max-device-width: 480px) {
   …
   table[class=table], td[class=cell] { width: 300px !important; }
   table[class=promotable], td[class=promocell] { width: 325px !important; }
   …
}</code></pre>

Note how we’re using attribute selectors here. This is to prevent <a href="https://www.campaignmonitor.com/blog/post/3457/media-query-issues-in-yahoo-mail-mobile-email/">Yahoo! Mail from accidentally calling this style sheet</a>.

One thing to note at this point is that, while you can shrink the dimensions of a design (or hide bits, as we’ll do later) using an <code>@media</code> query, the user will still be downloading all of the content. Adding mobile-specific styles shouldn’t be confused with providing a slimmer or faster-loading version of your content. Mobile-specific styles just make the content easier to read.

The great news is that mobile email clients such as iOS Mail and Android’s default mail client follow <code>@media</code> queries to the letter. So, for example, you could pop one into a style sheet in the head of your HTML email code to transform the design into an easily readable, mobile-friendly layout like the one pictured above. You can also do things like shrink the dimensions of images, and use <code>display: none</code> to hide visual elements that don’t work on small screens.

For a more hands-on look at mobile email design, I highly recommend the <a href="https://www.campaignmonitor.com/guides/mobile/">Guide to Responsive Email Design</a>, which includes both the fundamentals and some advanced techniques like <a href="https://www.campaignmonitor.com/guides/mobile/responsive/">progressive disclosure</a>.

## What’s Next For HTML Email Designers?

So, while CSS-unfriendly email clients like Outlook will always be here to rain on our parade, the good news is that the rise of mobile email has meant that we may soon be at liberty to create more Web-like email experiences. It has also meant that optimizing your newsletters for handheld and touch displays has gone from being a “nice thing to have” to a given. This doesn’t just affect email newsletters at the code level, but it also changes the way we display design elements. For example, in the following two mobile designs, which do you think is the more effective call-to-action (CTA) button?

<figure><img loading="lazy" decoding="async" src="https://stylecampaign.com/blog/blogimages/touch/em/touch6.jpg" alt="Call to action" /><figcaption>Call-to-action (CTA) buttons.</figcaption></figure>

Or consider the CTA in the following mobile-friendly email. If it’s not visible “above the fold,” as they say, then will it be seen at all? Or worse, will recipients end up accidentally tapping the toolbar instead?

<figure><img loading="lazy" decoding="async" src="https://stylecampaign.com/blog/blogimages/touch/em/touch4.jpg" alt=":Call" /></figure>

If designers aren’t asking these questions, they sure will be soon. You need only visit <a href="https://stylecampaign.com/blog/2011/07/finger-snafu/">Style Campaign’s blog</a> (which provided the examples above) or read up on “<a href="https://www.lukew.com/ff/entry.asp?1649">Optimizing for Touch Across Devices</a>” to grasp the importance designing good experiences for mobile.

Here are a few other important things to consider when designing adaptive layouts:

*   Single-column layouts that are no wider than 500 to 600 pixels work best on mobile devices. They’re easier to read, and if they fall apart, they’ll do so more gracefully.
*   Links and buttons should have a minimum target area of 44 × 44 pixels, as per Apple guidelines. Nothing sucks more than clouds of tiny links on touchscreen devices.
*   The minimum font size displayed on iPhones is 13 pixels. Keep this in mind when styling text, because anything smaller will be upscaled and could break your layout. Alternatively, you could [override this behavior](https://www.campaignmonitor.com/blog/post/3339/save-your-layout-by-overriding-the-minimum-font-size-on-the-iphone-and/) in your style sheet.
*   More than ever, keep your message concise, and place all important design elements in the upper portion of the email, if possible. Scrolling for miles is much harder on a touchscreen than with a mouse.

Now it’s your turn to design wicked HTML email newsletters that, with a dash of CSS, look just as effective on the small screen as they do in your Web browser or desktop inbox. I have no doubt that your readers will appreciate the effort.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72934f40-c2d4-4bf6-8ec9-d7fdcb02b110/invision-email-campaign-opt.jpg" alt="Mobile-friendly email design from InVision" width="500" height="376" /><figcaption>Example of a beautiful, mobile-friendly design from InVision.</figcaption></figure>

## Resources To Help You Make The Most Of CSS In Email

With funky CSS support and coding practices from circa 1994, designing HTML emails might seem like rocket science. Thankfully, quite a bit of solid documentation exists on effective HTML email design, so below is my recommended reading list if you want to take your newsletters to the next level.

### Getting Started with HTML Email

*   “[Creating a Simple Responsive HTML Email](https://webdesign.tutsplus.com/articles/creating-a-simple-responsive-html-email--webdesign-12978)”
*   “[5 top email designers share the tools they can’t live without](https://www.campaignmonitor.com/blog/post/4313/5-top-email-designers-share-the-essential-tools-they-cant-live-without)”
*   “[Coding your Emails](https://www.campaignmonitor.com/guides/coding/)” &mdash; An excellent starter tutorial
*   [Inliner.cm](https://inliner.cm/) &mdash; For moving CSS inline

### HTML and CSS in Email Clients

*   [Email Marketing Trends](https://www.campaignmonitor.com/guides/email-marketing-trends/)
*   “[Guide to CSS Support in Email Clients](https://www.campaignmonitor.com/css/)”

### Mobile Email Design

*   [Guide to Responsive Email Design](https://www.campaignmonitor.com/guides/mobile/)
*   [Style Campaign blog](https://stylecampaign.com/blog/)
*   “[CSS3 animation, SVG masks, web fonts and more in Panic’s newsletter](https://www.campaignmonitor.com/blog/post/4035/css3-animation-svg-masks-web-fonts-panics-newsletter)”
*   “[How We Create and Send a Newsletter to 175,000 Subscribers](https://www.campaignmonitor.com/blog/post/4271/create-send-monthly-email-newsletter)”
*   “[Responsive Navigation: Optimizing for Touch Across Devices](https://www.lukew.com/ff/entry.asp?1649)” &mdash; for those interested in mobile UX
*   “[Make your HTML Email 5&times; More Mobile Friendly](https://webdesignerwall.com/general/make-your-html-email-5-times-more-mobile-friendly)”

### Email Design Inspiration And Templates

*   [Campaign Monitor’s template builder](https://www.campaignmonitor.com/email-templates/#gallery)
*   [ThemeForest’s email template marketplace](https://themeforest.net/category/marketing/email-templates)
*   [MailChimp’s free templates](https://templates.mailchimp.com/)
*   [Campaign Monitor’s email design gallery](https://www.campaignmonitor.com/best-email-marketing-campaigns/)
*   [Beautiful Email Newsletters design gallery](https://beautiful-email-newsletters.com/)

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Design and Build Email Newsletters Without Losing Your Mind](https://www.smashingmagazine.com/2010/01/design-and-build-an-email-newsletter-without-losing-your-mind/)
*   [Email Newsletter Design: Guidelines And Examples](https://www.smashingmagazine.com/2010/02/email-newsletters-guidelines-and-examples/)
*   [Typographic Patterns In HTML Email Newsletter Design](https://www.smashingmagazine.com/2015/08/typographic-patterns-in-html-newsletter-email-design/)

{{< signature "al, il, mrn" >}}
