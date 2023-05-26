---
title: Email Marketing For Mobile App Creators
slug: email-marketing-for-mobile-app-creators
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4812fb4-e2c9-4919-81fb-40074bf815f0/illu-email.jpg'
date: 2013-08-14T08:03:49.000Z
author: ros-hodgekiss
description: >-
  If you’ve developed mobile applications or have just started building one,
  then you probably realize that marketing should be as much of an ongoing
  concern as the product’s design and development. After all, what’s the point
  in creating a beautiful, valuable app if no one knows about it?
categories:
  - Mobile
  - Business
  - Apps
  - Marketing
  - Newsletters
  - Content Strategy
  - Emails
---
If you’ve developed mobile applications or have just started building one, then you probably realize that marketing should be as much of an ongoing concern as the product’s design and development. After all, what’s the point in creating a beautiful, valuable app if no one knows about it?

Assuming that promotion on <a href="https://play.google.com/store?hl=en">Google Play</a> or Apple’s <a href="https://www.apple.com/iphone/from-the-app-store/">App Store</a> will take your app from beta to bestseller is… well, <strong>magical thinking</strong>. In reality, most successful developers kick off their marketing efforts months before release.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Design And Build Email Newsletters Without Losing Your Mind](https://www.smashingmagazine.com/2010/01/design-and-build-an-email-newsletter-without-losing-your-mind/)
*   [An Introduction To Building And Sending HTML Email](https://www.smashingmagazine.com/2017/01/introduction-building-sending-html-email-for-web-developers/)
*   [Typographic Patterns In HTML Email Newsletter Design](https://www.smashingmagazine.com/2015/08/typographic-patterns-in-html-newsletter-email-design/)
*   [Making Responsive HTML Email Coding Easy With MJML](https://www.smashingmagazine.com/2017/01/making-responsive-html-email-coding-easy-with-mjml/)

In this post, we’ll focus on how to get a head start with email marketing, not only by wrangling testers and staying in touch with users, but by successfully building hype for your app. Then, we’ll move on to how to announce the launch and measure results. Along the way, we’ll share techniques and code snippets from solid marketing campaigns, spanning different stages of an app’s lifecycle.

{{% feature-panel %}}

While this article isn’t heavy on coding and development, you’ll find an assortment of practical suggestions that you can apply to your projects. But if all you get is a little perspective on how important it is to actively work on getting the word out about your app from the get-go, then still consider this time well spent!

## Why Email Marketing?

First, why focus on email and not, say, social media or word of mouth? Simply put, email gives you the most bang for your buck. With a <a href="https://litmus.com/blog/email-preferred-more-clicks-conversions-roi">return of $40 for every $1 spent</a>, email marketing stands head and shoulders above other methods, such as keyword advertising ($17 for every $1) or banner advertising ($2). Email also generates superior conversion rates, while giving you full control over your message. And we haven’t even mentioned the big-picture goals, such as using it to keep your most valuable users in the loop — for example, when recruiting testers, announcing launch day or requesting feedback.</p>

## But HTML Email Is Hard, Right?

To be fair, creating and sending HTML email has always been a tricky sport. If your background is Web design and development (as it is for many app creators), then you’re likely aware that designing, coding and testing for the inbox is significantly different from doing that for the Web. A skim of Campaign Monitor’s “<a href="https://campaignmonitor.com/css">CSS Support</a>” chart quickly reveals that providing a consistent experience across multiple email clients is truly a minefield.

Yet feel consoled that, if you’re primarily targeting mobile users (for example, by encouraging them to download an app directly to their phones), mobile email clients such as iOS Mail are powered by <a href="https://en.wikipedia.org/wiki/WebKit">WebKit</a>. This offers the luxury of a browser-like experience — including solid HTML5 and CSS3 support — in the inbox. Secondly, a number of email service providers, including Campaign Monitor and MailChimp, offer HTML email builders that not only whip up campaigns quickly and painlessly, but produce templates that make the most of mobile email clients, with media query support. In the email marketing business, we call these <strong>responsive email templates</strong>.

While we’ll touch on some of the code that goes into tailoring a better mobile email experience, we won’t dive too deep into responsive email design. To get up to speed on both the concept and code behind it, I highly recommend reading Smashing Magazine’s “<a href="https://www.smashingmagazine.com/2011/08/18/from-monitor-to-mobile-optimizing-email-newsletters-with-css/">From Monitor to Mobile: Optimizing Email Newsletters With CSS</a>” and “<a href="https://campaignmonitor.com/guides/mobile">Responsive Email Design</a>.”

But before all that exciting stuff, let’s start with the fundamentals: building a mailing list of email addresses (i.e. subscribers). Without this, you’ll have no one to email — and let’s be clear, <a href="https://blog.hubspot.com/blog/tabid/6307/bid/32892/Why-Purchasing-Email-Lists-Is-Always-a-Bad-Idea.aspx">buying a list is never the right option</a>.</p>

## An App Marketing War Plan

When you’re elbow-deep in designing or coding a mobile app, it’s hard to step back, change tack and focus on the equally important yet arguably less fun tasks of putting together a promotional website, a trailer and, yes, email campaigns. That’s why it’s best to make a marketing plan and execute it early on, instead of waiting until App Store approval anxiety has kicked in.

A marketing plan doesn’t have to be complex. For email, it could be something as informal as the following.</p>

### Pre-Launch

1.  Choose an email service provider, and create a subscription list.
2.  Build a pre-launch page with an email sign-up form.
3.  Encourage people to visit the pre-launch page and subscribe for email updates.
4.  Build an email subscription form into the app.

### Beta Testing

*   **One week prior to beta testing**.  Create an email campaign, inviting subscribers to a first look at the app in beta. Explain how they can download the app and provide feedback.
*   **Three days after beta launching**.  Email your beta testers to request feedback.</p>

### Launch

*   **One week before launch**.  Email subscribers to let them know the app is close to launching. Include positive reviews and encourage subscribers to spread the word.
*   **Launch day**.  Email subscribers to announce the launch, and link to the app’s download page in the App Store, Google Play, Windows Store, etc.</p>

### Post-Launch

*   **One week after launch**.  Thank your subscribers, and encourage them to leave feedback on the app’s download page.
*   **After major updates**.  Email a summary of what’s new and improved, and encourage subscribers to spread the word.

It’s that straightforward — just jot down a rough outline of what you plan to do, on a napkin if need be. You can be as creative as you like with your email marketing strategy. Just make sure to make good on it!

## Choose An Email Service Provider

If you’ve never fooled around with email marketing, choosing the right provider will likely be a touch confounding. Many services are out there for creating and running email campaigns, from Web-based ones such as <a href="https://mailchimp.com">MailChimp</a> and <a href="https://campaignmonitor.com/">Campaign Monitor</a>, to self-hosted apps such as <a href="https://sendy.co/">Sendy</a>. My advice is to talk to other designers and app creators about what they’ve tried, and then open free accounts with some of the Web-based DIY services. The differences in the experiences (not to mention the features and pricing) between apps will soon become clear. Cheapest doesn’t mean best in this game, so shop around and run a few trial campaigns.

The benefit of a Web-based email marketing app is that getting started is generally quick and easy. Remember that if your needs change, you should be able to migrate your lists to another service.</p>

## Pull Together A Pre-Launch Page

Even when your project is in an early stage, it really pays to create a simple pre-launch, or landing, page with a few details about the app, perhaps some concept art and, of course, an email subscription form. After all, if visitors to your website like the concept, they’ll be keen to sign up for email updates and find out when your app is launching. These will also likely be your most valuable, passionate users for giving feedback and spreading the word when you launch. Below is the pre-launch page for the upcoming mobile game <a href="https://www.thedrowning.com/">The Drowning</a>, by <a href="https://dena.com/intl/">DeNA</a>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc10661e-7b67-4eac-b627-16cc815742c5/the-drowning-mini.png"><img loading="lazy" decoding="async" class="alignnone size-medium wp-image-137319" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a50b79-3cce-439b-9144-cc7dac5cc335/the-drowning-500-mini.png" alt="Subscription page for The Drowning" width="500" /></a>

I like The Drowning’s pre-launch page for its sophistication yet simplicity. The artwork and trailer for this ominous first-person shooter are polished and persuasive. There’s even a nice incentive to sign up to the mailing list: email updates <em>and</em> a free wallpaper. Above all, the entire page is geared to getting visitors to subscribe, and the subscription form is unmissable. You’ll find a couple of other great examples in the post “<a href="https://www.smashingmagazine.com/2011/05/24/building-an-effective-coming-soon-page-for-your-product/">Building An Effective ‘Coming Soon’ Page For Your Product</a>.”

Now back to your page. One thing your email service provider should be able to do is generate a <strong>snippet of code with which you can add a subscription form to your website</strong> and automatically push new email addresses to a list. Alternatively, a number of simple services and plugins not only enable you to build good-looking pre-launch pages, but integrate with some of the major email service providers. Popular ones include out-of-the-box apps like LaunchRock and <a href="https://unbounce.com/">Unbounce</a>; if you’re already running a CMS such as WordPress, then the <a href="https://wordpress.org/plugins/launchpad-by-obox/">Launchpad</a> plugin for WordPress is worth a look. Or you could create your own self-hosted launch page using a template such as Launching.me.

With a pre-launch page up and running, you can get back to focusing on your app for a while. Or you could start communicating with your new subscribers, using <a href="https://www.copyblogger.com/email-autoresponders/">autoresponders</a>.

## Add An Email Subscription Form To Your App

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c0e79a9-9bb3-4408-b436-514b113292c6/createsendexample.png"><img loading="lazy" decoding="async" class="size-medium wp-image-137324" style="padding-left: 1.5em" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95024f45-d673-41d6-a287-3cd132c7feed/createsendexample-148x300.png" alt="Add a subscription form to your mobile app" width="148" height="300" align="right" /></a>

While it might sound a bit odd, nothing is wrong with boosting your ongoing marketing efforts by adding a subscription form to your mobile app itself. You could collect email addresses from early adopters to inform them of updates. Or perhaps you’re planning a really great newsletter for your audience and feel that in-app sign-ups would give the app a real boost.

If <a href="https://www.google.com/search?q=cocoa+language&amp;oq=cocoa+language&amp;aqs=chrome.0.57j0l3j62l2.6479j0&amp;sourceid=chrome&amp;ie=UTF-8">Cocoa</a> is your language of choice and you are using Mailchimp, then check an <a href="https://github.com/mailchimp/ChimpKit2">unofficial Objective-C wrapper for Mailchimp</a> and <a href="https://carpeaqua.com/2010/01/17/sgmimimailer-a-cocoa-wrapper-for-mad-mimi/">Mad Mimi</a>. If you are using CampaignMonitor, make sure to check the <a href="https://github.com/campaignmonitor/createsend-objectivec">Objective-C wrapper on GitHub</a> which can be used to create in-app subscription forms. With an <a href="https://www.campaignmonitor.com/api/">extensive API</a>, it’s also well documented and comes with usage examples. Just something to think about.</p>

## Experiment With Other List-Building Tactics

Creating a pre-launch page and adding an email sign-up form to your app are both great ways to bring more people into the loop with your current mobile app and future ones. While these tactics tend to be rather set-and-forget, you could try other things to actively build interest in your title:

*   **Collect email addresses at events.**.  Do you attend developer meetups or conferences? If you’re going to be talking about your upcoming app, you might as well give attendees a way to track its progress. Pretty much every email service provider comes with a customizable mobile app to collect email addresses and push them to your lists. Campaign Monitor’s is [Enlist](https://www.campaignmonitor.com/enlist/), and MailChimp’s is [Chimpadeedoo](https://mailchimp.com/features/mobile-signup-forms/).
*   **Offer something valuable.**.  One effective tactic is to offer teaser content via a blog, such as concept art or even posts on what you’ve learned during development. Smack a subscription form onto your blog posts or even [in your videos](https://wistia.com/doc/email-marketing) (using a service such as [Wistia](https://wistia.com/)), with the promise of useful content and updates via your email newsletter.
*   **Offer a discount on the app.**.  If you’re building a paid app, offering a generous discount to early adopters wouldn’t hurt — if they agree to sign up to your email newsletter, that is. Slipping in an incentive is always a reliable tactic, especially when it demands very little effort.

Now that new subscribers are rolling in, let’s look at what it takes to send out emails.</p>

## Create Your First Email Campaign

Some time has passed and, after a little promotion, your pre-launch page has collected quite a few email addresses. You might have some cool teaser artwork to share now, or you might feel it’s time to invite some subscribers to join the beta phase — heaven forbid, you might be a week out from launch! Scary stuff.

At this stage, you might be tempted to obsess over the <a href="https://24ways.org/2009/rock-solid-html-emails/">technical details</a> of creating HTML email campaigns (which are important), but, ultimately, this is a marketing exercise. What matters above all is your message and ensuring that readers are hooked at first glance. Smashing Magazine’s “<a href="https://www.smashingmagazine.com/2013/04/08/rise-your-email-above-inbox-noise/">How to Raise Your Email Above Inbox Noise</a>” is a great primer on how to creating relevant and all-round “sticky” email content.

Another thing that folks regularly obsess over is figuring out the best time to launch a campaign. While <a href="https://econsultancy.com/us/blog/62688-six-case-studies-and-infographics-on-the-optimal-time-to-send-emails">some (albeit conflicting) evidence</a> shows that the hour or day of the week you choose does make some difference, I think the advantages of emailing at 7:00 pm over, say, 10:00 am are marginal, especially if your subscribers are international. Even <a href="https://www.copyblogger.com/email-marketing-timing/">public holidays</a> seem to work for some creators, so relax and follow a schedule that suits you. Your content will make the big difference, after all.

Having gone through all of this heavy stuff, let’s take an inspiration break and look at a couple of email newsletters from app developers, sent at certain milestones prior to launch. Click on each design to see the large version and to view the source code.</p>

### “Visit Our Pre-Launch Page”

<span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/AD3769CCC3AE17612540EF23F30FEDED"><img loading="lazy" decoding="async" class="137330" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ac29850-967e-406c-8d6f-58ba4cb298cd/pre-launch-drowning-500-mini.png" alt="Teaser email: The Drowning" width="500" height="700" /></span>
<em><span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/AD3769CCC3AE17612540EF23F30FEDED">The Drowning</span>, by <a href="https://dena.com/intl/">DeNA</a>.</em>

Now that you’ve got a shiny new promotional website, what better way to drive visitors to it than by running a campaign for your existing email lists? As an established mobile game developer, DeNa is in the fortunate position of having an established community of dedicated gamers, many of whom would probably be interested in this title. This email’s narrow format makes it comfortable to read on mobile devices, too.</p>

### “Invitation to Beta Test”

<span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/AD273323F926C89C"><img loading="lazy" decoding="async" class="137332" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4433f9d-6681-4475-aa32-605130959aaf/beta-invite-echograph-mini.png" alt="Beta Invite: Echograph" width="500" height="670" /></span>
<em><span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/AD273323F926C89C">Echograph</span>, by <a href="https://clear-media.com/">Clear Media</a>.</em>

I like this invitation to beta test <a href="https://echograph.com">Echograph</a> because it’s as clear as it gets. There’s no waffling about this awesome animated GIF builder for the iPad — just a couple images that show beta testers what they need, a sample GIF and step-by-step instructions for installing the app during the beta phase.</p>

### “Thank You for Beta Testing”

<span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/0B7BBD857F05383B/"><img loading="lazy" decoding="async" class="137333" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ba569ac-b515-42be-93ee-b215f17f3d7c/beta-thank-you-dropmark-mini.png" alt="Beta thank you: Dropmark" width="500" height="660" /></span>
<em><span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/0B7BBD857F05383B/">Dropmark</span>, by <a href="https://oak.is/">Oak</a>.</em>

Once beta testing has wrapped up, <strong>it’s nice to say “Thank you”</strong> and offer a little something for the effort and feedback your audience has volunteered. <a href="https://dropmark.com/">Dropmark</a>’s thoughtful email campaign does this with class, by providing a discounted upgrade for beta testers. It’s a great way to ensure that they keep using the service.

I hope you’ve enjoyed that visual interlude. Now, let’s discuss how to announce your app’s launch. Hold tight!

## Launch Your App With Email

So, the big reveal is imminent. You’ve probably just submitted your app to the App Store or published it on Google Play. Either way, it’s time to focus on getting the word out.

Whether you announce the launch in a newsletter or via a standalone email announcement, you need to do two things: first, make an impact, and secondly, make it very easy to download the app from the newsletter itself. To achieve both, you’ll need to get the logo and branding for your app store of choice, as well as the link to the download page and, of course, some compelling content to get subscribers excited about the app.

At our company we announced the release of our subscription form app for the iPad, <a href="https://campaignmonitor.com/">Enlist</a>, via our monthly newsletter:

<span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/y/78AABCA56BB82CF8"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="137334" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d816344f-170a-435a-bf10-b95f343cbd06/launch-enlist-mini.png" alt="Launch email: Enlist" width="500" height="490" /></span>

The images are crisp and inviting. But the real magic happens when you view the newsletter on an iPad. A “Get it from the App Store” link appears, allowing users to download the app to their device in two taps.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4c8c534-d25b-4627-8c71-ca3311aae7f2/launch-enlist-ipad-mini.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="137335" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d187c39f-5c02-4361-a492-88ad43fe26a9/launch-enlist-ipad-500-mini.png" alt="Enlist launch email on the iPad:" width="500" /></a>

As you might have guessed, we are using media queries to reveal the App Store link when the email is viewed on an iPad. While I don’t want to go too deep into code, this neat trick is worth sharing. Below is an abridged version of the HTML and CSS.</p>

### CSS

<pre><code class="language-css">
p.ipad {
    font-size: 0px;
}
…
@media only screen and (min-device-width : 768px) and (max-device-width : 1024px) {

    a[id="reveal"] {
        display: block !important;
        background: url('https://yourdomain.com/images/appstore.png') no-repeat center center !important;
        background-size: 232px 49px !important;
        width: 232px !important;
        height: 49px !important;
    }
}
</code></pre>

### HTML

<pre><code class="language-markup">
&lt;p class="ipad"&gt;&lt;a id="reveal" href="https://campaignmonitor.createsend1.com/t/y-l-jidkuht-l-p/" title="Get Enlist from the App Store"&gt;&lt;/a&gt;&lt;/p&gt;
</code></pre>

You might be curious why we use <code>font-size: 0px</code> to hide the App Store link when the email is viewed on anything other than an iPad. This strange choice is explained in the blog post “<a href="https://www.campaignmonitor.com/blog/post/3948/hiding-content-in-both-desktop-and-web-email-clients">How to Display Content on Mobile Devices Only</a>.” It gives a taste of the quirkiness involved in designing HTML emails.

On to the content. Let’s go to the second launch campaign for Echograph, which features a prominent download link, plus a video and animated GIF that walk viewers through the app:

<span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/82811D0144EB6496"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="137336" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89aea4d9-0d64-473c-9060-d1db3d26c88e/walkthrough-echograph.gif" alt="Animated walkthrough: Echograph" width="500" height="505" /></span>
<em>Second launch campaign for <span class="removed_link" title="https://gallery.campaignmonitor.com/ViewEmail/r/82811D0144EB6496">Echograph</span>.</em>

Nicely done. Overall, the best thing you can do with your launch email is have fun and be creative — while staying concise. And before any of you mentions it in the comments, TechCrunch reckons that <a href="https://techcrunch.com/2011/12/19/sunday-is-the-best-day-to-launch-your-mobile-app/">Sunday is the best day to launch an app</a>.</p>

## So, What Next?

Once your app has launched, you might be tempted to take a break from campaigns, but then you’d miss out on a big opportunity. By continuing to grow your email lists and stay in touch with subscribers — whether to collect feedback, announce updates or simply share your successes — you’ll find email to be a valuable tool in your marketing arsenal. If this sounds like work, consider going on autopilot <a href="https://mailchimp.com/features/autoresponders/">with</a> <a href="https://help.campaignmonitor.com/topic.aspx?t=171">autoresponders</a>, which are email campaigns that are automatically run when set off by certain triggers, such as a date (“send two weeks after visitor signs up”) or an action (“send whenever a user upgrades”). To learn more, read Smashing Magazine’s guide on “<a href="https://www.smashingmagazine.com/2010/03/03/how-to-market-your-mobile-app/">How to Market Your Mobile Application</a>,” and, of course, talk to your fellow developers.

This post hasn’t been code-heavy, but it could have been — designing for mobile, let alone email, is a surprisingly demanding process, regardless of your aptitude as a designer or coder. However, I wanted to focus on helping you make the most of your marketing milestones by engaging with users via email.

If you walk away from this post with one thing, it should be a desire to <strong>get your planning in the bag as soon as possible</strong>. Otherwise, you risk missing out on the opportunity to build an audience that is as committed to your project as you are. Best of luck with your email marketing journey. We’d love to hear from you in the comments.

<em>(al) (ea)</em>

