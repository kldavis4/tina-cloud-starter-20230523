---
title: 'An Introduction To Building And Sending HTML Email For Web Developers'
slug: introduction-building-sending-html-email-for-web-developers
author: lee-munroe
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee4b9d5-41e2-404c-b899-640575937744/14-responsive-preview-opt.png
date: 2017-01-10T21:37:18.000Z
summary: >-
  Email design and development is a beast. Email client vendors haven’t been as progressive as web browser vendors in adopting new standards. Here’s an insight into the world of building and sending email, and a couple of code snippets and resources that are sure to add some hours back into your life.
description: >-
  Email design and development is a beast. Email client vendors haven’t been as progressive as web browser vendors in adopting new standards. Here’s an insight into the world of building and sending email.
categories:
  - Coding
  - HTML
  - Emails
---
I've spent the past several years building development tools — two of those years as product design lead at [Mailgun](https://www.mailgun.com/), an email service for developers, where I learned a lot about how email works and the **problems that developers face** when building HTML email. In this post, I'll share some of my knowledge about the topic.

HTML email: Two words that, when combined, brings tears to a developer's eyes. If you're a web developer, it's inevitable that coding an email will be a task that gets dropped in your lap at some time in your career, whether you like it or not. **Coding HTML email is old school.** Think back to 1999, when we called ourselves "webmasters" and used Frontpage, WYSIWYG editors and tables to mark up our websites.

**Not much has changed in email design.** In fact, it has gotten worse. With the introduction of mobile devices and more and more email clients, we have even more caveats to deal with when building HTML email.</p>

I've spent the past several years building development tools — two of those years as product design lead at [Mailgun](https://www.mailgun.com/), an email service for developers, where I learned a lot about how email works and the **problems that developers face** when building HTML email. In this post, I'll share some of my knowledge about the topic.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Design And Build Email Newsletters Without Losing Your Mind](https://www.smashingmagazine.com/2010/01/design-and-build-an-email-newsletter-without-losing-your-mind/)
*   [18 Email Templates For Web Designers And Developers](https://www.smashingmagazine.com/2013/06/email-templates-web-designers-developers-pdf-odt-txt/)
*   [Making Responsive HTML Email Coding Easy With MJML](https://www.smashingmagazine.com/2017/01/making-responsive-html-email-coding-easy-with-mjml/)
*   [How To Improve Your Email Workflow With Modular Design](https://www.smashingmagazine.com/2014/08/improve-your-email-workflow-with-modular-design/)

{{% feature-panel %}}

## Introduction To Sending Email

As a developer responsible for an email campaign or all of the emails your company sends, you will need to know how email works, the legal requirements and how to actually get email delivered. Companies send a few different types of email. Let's take a look.</p>

### Marketing Email

A lot of email service providers (ESPs) specialize in marketing and promotional emails: [SendPulse Email](https://sendpulse.com/features/email), [Campaign Monitor](https://www.campaignmonitor.com), [MailChimp](https://mailchimp.com), [Emma](https://myemma.com/), [Constant Contact](https://www.constantcontact.com), to name just a few. They provide full solutions for managing subscribers, working with email templates, running bulk email campaigns and reporting.</p>

### Transactional Email

Transactional email includes receipts, alerts, welcome emails, password resets and so on, and it is typically implemented with development tools and APIs such as [SendPulse Transactional](https://sendpulse.com/features/transactional), [Mailgun](https://mailgun.com), [SendGrid](https://sendgrid.com) and [Postmark](https://postmarkapp.com/). These tools are more API-focused, less CMS- and WYSIWYG-based; however, combined with a service such as [Sendwithus](https://sendwithus.com), they can be made even more powerful.

An alternative to using a service is to roll your own email server with something like [Postfix](https://www.postfix.org/). The downside of this is that it's up to you to set up and configure it and to understand the technical details of sending email, implementing tracking and unsubscribing, and getting email delivered to inboxes.</p>

### Life-Cycle Email

Life-cycle and behavior-based email services help with onboarding, engagement and more. A lot of ESPs focused on marketing also offer this service, but I tend to group services such as [SendPulse Automation](https://sendpulse.com/features/email/automation-360), [Intercom](https://intercom.io), [Customer.io](https://customer.io), [Drip](https://www.drip.co/), [Vero](https://www.getvero.com/) and [ConvertKit](https://convertkit.com/) into this category.</p>

## Email List Best Practices

**Don't buy email lists.** Maybe a handful of legit services are out there, but you're best off staying away from buying lists altogether.

My experience is that anyone who buys an email list will suffer from a lot of bounces, give their Internet Protocol (IP) address a bad reputation, and get their emails blocked by Internet service providers (ISPs) or sent to spam. **85%** of the world's email is considered spam, according to [SenderBase](https://www.senderbase.org/); don't fall into this bucket.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3c3a997-28f8-4a4e-bde3-8e984d012fff/2-spam-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f69bdbf-ec06-41f7-a6fa-303b1a223b8f/2-spam-preview-opt.png" alt="html email - SenderBase spam stats" width="500" height="281" /></a></figure>

### Double Opt-In

A subscriber having to verify their email address adds an extra step to the process, but it makes sense and stops other people from abusing their email address by signing them up for lists without their permission. It also helps to **keep your subscription list clean** and is the “100% correct way to [validate an email address](https://hackernoon.com/the-100-correct-way-to-validate-email-addresses-7c4818f24643#.i22l0u4ny)”.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/073ed1fd-713f-4df6-964f-de0106387bc7/3-confirm-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64255926-b5d9-4f40-ba5c-193d1293efc4/3-confirm-preview-opt.png" alt="html email - Double opt in email" width="500" height="237" /></a></figure>

### CAN SPAM

These are your **legal requirements** for sending email, enforced by the [CAN-SPAM Act of 2003](https://en.wikipedia.org/wiki/CAN-SPAM_Act_of_2003):

*   Don't use false or misleading header information.
*   Don't use deceptive subject lines.
*   Identify the message as an ad.
*   Tell recipients where you're located.
*   Tell recipients how to opt out of future email from you.
*   Honor opt-out requests promptly.
*   Monitor what others are doing on your behalf.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/675af0bf-6a57-42e6-bbc1-5ea966401960/4-canspam-large-opt.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4873a381-38d9-4f69-a6e6-dde911ddf8d8/4-canspam-preview-opt.png" alt="CAN SPAM legal requirements" /></a></figure>

MailChimp has a good list of email [legal requirements by country](https://kb.mailchimp.com/accounts/compliance-tips/terms-of-use-and-anti-spam-requirements-for-campaigns).</p>

## Analytics And Measuring Performance

Measure everything. You need to measure to know whether your emails are improving. The numbers will differ vastly depending on what you do, your industry, the type of emails you send and the context. However, in general:

*   20% is a good open rate,
*   3 to 7% is a good clickthrough rate,
*   5% is a poor bounce rate,
*   0.01% is a poor spam rate,
*   1% is a poor unsubscribe rate.

Also, remember that open rates and clickthrough rates can be **vanity metrics** (read "they don't really matter"). At the end of the day, what you really want to track is that end goal or conversion. At Airbnb they track an [email quality score](https://medium.com/@chelucas/email-quality-score-explained-137d0871b4b5#.9uz3pyxny), which is a good indicator on engagement quality.

Google's [URL builder](https://ga-dev-tools.appspot.com/campaign-url-builder/) can help with tracking if you're using Google Analytics.</p>

{{% ad-panel-leaderboard %}}

## Sending Score And Reputation

Your emails have a **reputation and score associated with them**. This affects how ISPs and mailbox providers deal with your email, whether they **accept or reject it** and whether they send it to the recipient's inbox or straight to spam.

Some contributing factors are:

*   your IP reputation (check yours with [SenderScore](https://senderscore.org/)),
*   your domain name signature (see [DKIM](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail) and [SPF](https://en.wikipedia.org/wiki/Sender_Policy_Framework)),
*   bounce rates and complaint rates.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19622c17-4172-43f2-9f28-5f692ad01ecf/5-score-large-opt.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62ca1f32-c182-4007-8373-b379d9588f1b/5-score-preview-opt.png" alt="SenderScore example" /></a></figure>

## Sending Bulk Email

When you send a lot of emails (imagine a campaign with millions of emails), they are not all sent instantaneously. They can only be sent as fast as the servers and IP addresses can handle them. Keep in mind that your recipients might not receive the emails at _exactly_ the same time.

So, if you're sending millions of emails at once, you'll probably want quite a **few IPs** to handle the load.</p>

## Email Clients

Litmus keeps track of the [market share of email clients](https://emailclientmarketshare.com/), based on its own internal statistics. Keep in mind that this is probably not the same for your customer base, but it is a good indicator to go by.

Here are the statistics as of December 2016:

*   iPhone: 33%
*   Gmail: 19%
*   iPad: 12%
*   Android: 8%
*   Apple Mail: 7%

Bear in mind that **not all emails can be tracked**. Email tracking is done via pixel-tracking, so only those clients with images enabled will report back.</p>

## HTML Templates

Building HTML email templates can be a slog. As a result, a lot of poorly designed email is out there — clunky, themed, verbose, pointless, distracting. If you enjoy a challenge or want a unique look and feel, then building your own can actually be fun and rewarding. Alternatively, some good email templates are available:

*   [Litmus Templates](https://litmus.com/community/templates)
*   [Really Simple Responsive HTML Email Template](https://github.com/leemunroe/responsive-html-email-template)
*   [HTML Email Templates](https://htmlemail.io/)
*   [Foundation for Emails 2](https://foundation.zurb.com/emails.html)

## Building HTML Email Templates

Now you know how to properly set up and send emails. The next decision you'll make is whether to code your own HTML template. This is a bit more complex than coding the average web page. Let's dive in.</p>

### Client-Rendering Engines

Email design is still in the dark ages. Due to the numerous email clients and devices, your email will get rendered for users in a variety of ways.

Email clients use **different engines to render** HTML emails:

*   Apple Mail, Outlook for Mac, Android Mail and iOS Mail use **WebKit**.
*   Outlook 2000, 2002 and 2003 use **Internet Explorer**.
*   Outlook 2007, 2010 and 2013 use **Microsoft Word** (yes, Word!).
*   Web clients use their browser's respective engine (for example, Safari uses WebKit and Chrome uses Blink).

Clients will also add their **own flavor of styles** on top of yours. For example, Gmail sets all `<td>` fonts to `font-family: Arial,sans-serif;`.

Look at your own statistics so that you know what to design for.</p>

### Gmail Support for Inline CSS and Media Queries

Only [recently](https://gsuite-developers.googleblog.com/2016/09/your-emails-optimized-for-every-screen-with-responsive-design.html) did Google announce support for **embedded CSS and media queries** in Gmail. This is _huge_ for the email development industry.

Now, as of September 2016, Gmail will support a slew of [CSS properties](https://developers.google.com/gmail/design/reference/supported_css), which makes template development for Gmail a lot easier.</p>

## Using HTML Tables For Layout

Divs have positioning and box-model issues in different clients — in particular, those that use Microsoft Word to render (i.e. Outlook). You can use divs if you want, but it's safer to code like it's 1999 and **stick to tables**. This means:

*   `<table>` instead of `<div>`,
*   `#FFFFFF` instead of `#FFF`,
*   `padding` instead of `margin`,
*   CSS2 instead of CSS3,
*   HTML4 instead of HTML5,
*   `background-color` instead of `background`,
*   HTML attributes instead of CSS,
*   inline CSS instead of style sheets or `<style>` blocks.

These are best practices. You could certainly ignore the safe route and go above and beyond.

When using tables, don't forget `border="0" cellpadding="0" cellspacing="0"`. If you're using Premailer, it has [special CSS declarations](https://github.com/premailer/premailer#premailer-specific-css) for applying these HTML attributes.</p>

## Inline CSS

Some clients (most notably Gmail until recently) will **strip any CSS that isn't inlined**. You have a couple of options here:

*   write CSS inline as you go,
*   use a web-based CSS inliner,
*   use a programmatic CSS inliner,
*   let your ESP handle the inlining for you (if it supports it).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71ad84e1-8322-4dc7-ba23-4c004736616d/6-inline-large-opt.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c145177-9fc9-496a-a7fe-cb5a048c0cba/6-inline-preview-opt.png" alt="Inline CSS" /></a></figure>

Writing inline as you go isn't exactly a scalable or maintainable solution, so I tend not to recommend this, but I know that a lot of email developers prefer this in order to maintain 100% control. If you do write your CSS inline manually, then I recommend making use of [snippets](https://www.hongkiat.com/blog/sublime-code-snippets/) and/or a templating language with [partials and helpers](https://blog.teamtreehouse.com/handlebars-js-part-2-partials-and-helpers). This will save you from having to repeat yourself.

Web-based inliners include HTML Email's [Responsive CSS Inliner](https://htmlemail.io/inline/) and Foundation for Email’s Responsive Email Inliner.

For a programmatic inliner, I recommend the Node.js module [Juice](https://github.com/Automattic/juice). The [Premailer gem](https://github.com/premailer/premailer) and [Roadie](https://github.com/Mange/roadie) are good Ruby alternatives.</p>

## Buttons

Trying to achieve the perfect cross-client button is painful. As mentioned, you should be using tables and table cells for pretty much everything, including buttons.

My preference is to use the following solution. Here is how you might normally style a button for the web:

<pre><code class="language-bash">
&lt;a href="#" class="btn btn-primary"&gt;Click Here&lt;/a&gt;
</code></pre>

Instead, write it like this:

<div class="break-out">

<pre><code class="language-bash">
&lt;table border="0" cellpadding="0" cellspacing="0" class="btn btn-primary"&gt;
  &lt;tr&gt;
    &lt;td align="center"&gt;
      &lt;table border="0" cellpadding="0" cellspacing="0"&gt;
        &lt;tr&gt;
          &lt;td&gt; &lt;a href="" target="_blank"&gt;Take action now&lt;/a&gt; &lt;/td&gt;
        &lt;/tr&gt;
      &lt;/table&gt;
    &lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;
</code></pre></div>

Then, once your CSS is inlined, it will look like this:

<div class="break-out">

<pre><code class="language-bash">
&lt;table border="0" cellpadding="0" cellspacing="0" class="btn btn-primary" style="border-collapse: separate; mso-table-lspace: 0pt; mso-table-rspace: 0pt; width: 100%; box-sizing: border-box; min-width: 100% !important;" width="100%"&gt;
  &lt;tr&gt;
    &lt;td align="center" style="font-family: sans-serif; font-size: 14px; vertical-align: top; padding-bottom: 15px;" valign="top"&gt;
      &lt;table border="0" cellpadding="0" cellspacing="0" style="border-collapse: separate; mso-table-lspace: 0pt; mso-table-rspace: 0pt; width: auto;"&gt;
        &lt;tr&gt;
          &lt;td style="font-family: sans-serif; font-size: 14px; vertical-align: top; background-color: #3498db; border-radius: 5px; text-align: center;" valign="top" bgcolor="#3498db" align="center"&gt; &lt;a href="" style="display: inline-block; color: #ffffff; background-color: #3498db; border: solid 1px #3498db; border-radius: 5px; box-sizing: border-box; cursor: pointer; text-decoration: none; font-size: 14px; font-weight: bold; margin: 0; padding: 12px 25px; text-transform: capitalize; border-color: #3498db;"&gt;Take action now&lt;/a&gt; &lt;/td&gt;
        &lt;/tr&gt;
      &lt;/table&gt;
    &lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;
</code></pre></div>

<figure><a href="https://litmus.com/builder/ac11b59"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85331bf-cf76-4ca0-808b-0d8e16e701c8/10-button-preview-opt.png" alt="Button in email" /></a></figure>

What's going on here? The first `<td>` is a wrapper to help us center the button. The second `<td>` is the size of the button. Some clients (such as Outlook) don't recognize the padding on the `<a>` tag, so we fill in the background color of the table cell. The `<a>` tag then takes up space available in the second `<td>`, and the whole area becomes clickable. Check out the [code and client tests on Litmus](https://litmus.com/builder/ac11b59).

This is just one way to implement buttons in email. Admittedly, it doesn't always look identical in every client, but the web is not always pixel-perfect either. I prefer this because it's simpler and doesn't involve using image assets or VML.

What's **VML?** If you've spent any time developing emails, you've likely come across some reference to it. Vector Markup Language (VML) is supported by **old versions of Outlook**. [According to Microsoft](https://msdn.microsoft.com/library/hh801223), as of Internet Explorer (IE) 10, VML is obsolete, which means that it is no longer supported in new versions of IE. However, as long as Outlook 2007, 2010 and 2013 are around, you will see it being used, typically for **background images**.</p>

## Typography

In general, sticking with standard system fonts is easiest. This includes Helvetica, Arial and so on. However, we **can use web fonts**, such as Google Fonts. Put them behind a **WebKit conditional media query**, so that Outlook doesn't mess them up:

<div class="break-out">

<pre><code class="language-css">&lt;style&gt;
@import url(https://fonts.googleapis.com/css?family=Pacifico);

/* Type styles for all clients */
h1 {
 font-family: Helvetica, Arial, serif;
}

/* Type styles for WebKit clients */
@media screen and (-webkit-min-device-pixel-ratio:0) {
  h1 {
    font-family: Pacifico, Helvetica, Arial, serif !important;
  }
}
&lt;/style&gt;
</code></pre></div>

Remember to **include a font family, font size and color** for every `<td>`, or else you risk the client overwriting your carefully chosen type styles.</p>

## Conditionals

We can apply specific CSS styles and show or hide elements and content for different versions of Outlook.

The following targets all Microsoft Word-based versions of Outlook:

<div class="break-out">

<pre><code class="language-html">&lt;!--[if mso]&gt;
Only Microsoft Word-based versions of Outlook will see this.
&lt;![endif]--&gt;
</code></pre></div>

This next snippet targets all IE-based versions of Outlook:

<div class="break-out">

<pre><code class="language-html">&lt;!--[if (IE)]&gt;
Only IE-based versions of Outlook will see this.
&lt;![endif]--&gt;
</code></pre></div>

We can also target specific version numbers of Outlook:

<div class="break-out">

<pre><code class="language-html">&lt;!--[if mso 12]&gt;
Only Outlook 2007 will see this.
&lt;![endif]--&gt;
</code></pre></div>

We can target WebKit-based clients with a media query:

<div class="break-out">

<pre><code class="language-css">.special-webkit-element {
  display: none;
}

@media screen and (-webkit-min-device-pixel-ratio:0) {
  .special-webkit-element {
    display: block !important;
  }
}
</code></pre></div>

## Images And Media

### Images in Email

Some clients will show images by default. Some won't. Keep this in mind when including images in your email content. This also affects tracking metrics, because images will typically be used to track opens.

*   **Outlook blocks image-rendering** by default.
*   Apple Mail doesn't.
*   Gmail doesn't (anymore).

Remember to include good `alt` text for all of your images. The text could either tell the user what the image says or just describe what it is (for example, "company logo"). You can get [creative with `alt` text](https://www.emailmonks.com/blog/email-marketing/creative-use-of-alt-text-in-email-learn-more-with-our-easter-campaign/) for clients that turn off images, as Email Monks does:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61f5d908-d209-43fb-ab0f-e37d6cbf0d6f/7-images-large-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9591d177-f197-4d57-b2cc-d5a0c1534817/7-images-preview-opt.jpg" alt="Creative alt text" /></a></figure>

Remember to include a basic reset for all images:

<div class="break-out">

<pre><code class="language-bash">
&lt;img src="https://www.smashingmagazine.com/wp-content/uploads/2016/11/" alt="" width="" height="" border="0" style="border:0; outline:none; text-decoration:none; display:block;"&gt;
</code></pre></div>

Animated **GIFs are supported** in most clients. Outlook versions 2007 to 2013 do not support animated GIFs, instead falling back to the first frame.

Remember to compress your media assets and upload them to a content delivery network (CDN), such as Amazon Web Services, [Cloudinary](https://cloudinary.com/) or [imgix](https://www.imgix.com/). Most marketing ESPs will handle this for you.

Scalable vector graphics (SVGs) have a lot of advantages on the web. As you would expect, email support varies, and SVG requires a couple of fallback hacks or conditionals. I typically recommend staying away from SVG in email, but if you want to get serious about it, then CSS-Tricks has a guide on [SVG support in email](https://css-tricks.com/a-guide-on-svg-support-in-email/).

For Retina-ready images, supply a larger image (1.5× to 3×) and resize it. I'll typically save a low-quality image that has 2× dimensions, which works well. (I've written [more on this technique](https://www.leemunroe.com/designing-for-high-resolution-retina-displays/).)

Keep in mind that, for Outlook, you need to declare how wide an image should be with the `width` attribute. Otherwise, Outlook might render the actual width of the image and break your email.</p>

{{% ad-panel-leaderboard %}}

### Video in Email

Video is supported in iOS, Apple Mail and Outlook.com. You can use media queries to show or hide a video based on the client. Email on Acid has more on [email video support](https://www.emailonacid.com/blog/details/C13/a_how_to_guide_to_embedding_html5_video_in_email).

For inspiration, check out Kevin Mandeville's tutorial on [coding HTML5 video](https://litmus.com/blog/how-to-code-html5-video-background-in-email) as a background in an email — impressive stuff and worth a look.</p>

## Forms In Email

Support for form elements varies. Try to steer clear, and **link to an external form** if you need one. Campaign Monitor offers some [advice on forms](https://www.campaignmonitor.com/resources/guides/email-forms/).

Obviously, it depends on your objectives. Staying away from forms is safer, but [Rebelmail](https://www.rebelmail.com/) and [Mixmax](https://mixmax.com/) have done interesting things with forms for surveys and e-commerce, with good fallback support.</p>

## Gmail Actions

Google makes handy [actions available for Gmail](https://developers.google.com/gmail/markup/actions/actions-overview). You've probably seen them on GitHub for issues or on Amazon for orders.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b265981-0eec-4f7b-a995-f5ae87dd1732/8-actions-large-opt.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c14b74d0-722f-410d-957b-a37fb90400ce/8-actions-preview-opt.png" alt="Gmail actions" /></a></figure>

Adding the code is straightforward. You have [two options](https://developers.google.com/gmail/markup/actions/declaring-actions):

*   JSON-LD
*   microdata

Getting whitelisted involves a [few more steps](https://developers.google.com/gmail/markup/registering-with-google). You can test Gmail actions with an `@gmail.com` address.</p>

## Preheader Text

Something important but often forgotten is preheader text. Some clients show preview text **next to or under the subject line**. These clients include iOS, Apple Mail, Outlook 2013, Gmail and AOL.

Clients will grab the first bit of text they find in your email's body and display it here. Make the most of this and add a hidden element to your body's content that appears first. This text should provide an extra incentive for the user to open your email. Hide the text like so:

<div class="break-out">

<pre><code class="language-bash">
&lt;span style="color: transparent; display: none !important; height: 0; max-height: 0; max-width: 0; opacity: 0; overflow: hidden; mso-hide: all; visibility: hidden; width: 0;"&gt;Preheader text goes here&lt;/span&gt;
</code></pre></div>

Use Austin Woodall's [subject and preheader tool](https://codepen.io/awoodall/full/XbpMbo/) to preview your email subjects and preheaders.</p>

## Testing Email

I don't think I've ever sent an email successfully the first time. There is always something to fix, always a typo, always a rendering issue in Outlook, always something I've forgotten to add.

You can test your email in a few ways:

*   Send an email to yourself and check it on a desktop client (Outlook), a web client (Gmail) and a mobile client (iOS Mail).
*   Automate tests using [Litmus](https://litmus.com/) or [Email on Acid](https://www.emailonacid.com/).
*   Proofread the content, and check the layout renders.
*   A/B test various types of content, lengths of content and subject lines.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03b8da45-ebab-4d21-bbae-c57ae0bd8acd/9-litmus-large-opt.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/020a90fb-6f4d-47ae-b1ab-8c2212044b23/9-litmus-preview-opt.png" alt="Litmus" /></a></figure>

How do you **send HTML emails to yourself?** Good question. It's harder than you think. [PutsMail](https://putsmail.com/) lets you do this quite easily, and [Thunderbird](https://www.mozilla.org/en-US/thunderbird/) lets you compose with its HTML editor.</p>

## MIME Multi-Part

A plain-text email is just that, plain text. An HTML email is just HTML. Most emails you send or receive are MIME (Multipurpose Internet Mail Extensions) multi-part emails (not to be confused with [MIME type](https://en.wikipedia.org/wiki/Media_type)). This standard combines both plain text and HTML, leaving it up to the recipient to decide which to render.

When you send an email, whether transactional or bulk, **include both the HTML and plain-text** versions. Even if, in your mind, every one uses a client that renders HTML, still send plain text.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8b47e46-2ece-4667-a1c0-e9a157652428/12-mime-large-opt.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84d5d742-f95e-4f06-9beb-ed0daef1fb7b/12-mime-preview-opt.png" alt="MIME multi-part" width="300" /></a></figure>

Also, note that some clients render plain-text email as HTML; for example, Gmail will add some default styles and turn URLs into links. Most ESPs will construct the MIME for you, so you don't really need to worry about it. Some will also create a plain-text version, based on your HTML.

Pro tip: In Gmail, select "Show original" from the dropdown menu to see the full MIME.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d94b4d0-cbc2-462d-8666-e84d24b9d818/13-gmail-large-opt.gif"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d94b4d0-cbc2-462d-8666-e84d24b9d818/13-gmail-large-opt.gif" alt="View original" /></a></figure>

A new MIME part has surfaced: `text/watch-html`. This content will only be displayed in [Apple Watch](https://litmus.com/blog/how-to-send-hidden-version-email-apple-watch) (and any other clients that support this MIME type going forward).</p>

## Accessibility

On the web, if you follow standards and best practices and use **semantic markup and valid HTML syntax**, you tend to get basic accessibility out of the box. Unfortunately, with email, due to our excessive hacks and the poor support for HTML, accessibility is often ignored.

I've seen little discussion on email accessibility, but one that stands out is Mark Robbins' [post on accessibility](https://blog.rebelmail.com/accessibility-in-email-part-ii/). He recommends the following:

*   Add `role="presentation"` to each table so that it's clear the table is being used for layout.
*   Provide `alt` text with meaningful descriptions.
*   If you don't need or want `alt` text, then use `alt=""` so that screen readers know it is meant to be blank.
*   Use semantic HTML tags, such as `<p>` and `<h1>`, where applicable.
*   Use the `role` attribute for elements such as headers and footers (for example, `role="header"`).</p>

## Responsive Email Design

*   Email opens on mobile are at [50% and rising](https://www.emailmonday.com/mobile-email-usage-statistics). The exact metric depends on which report you check and which audience you cater to, but I think we can all agree that this is important.
*   [Email Client Market Share](https://emailclientmarketshare.com/), as of August 2016, puts iPhone at 33%, iPad at 11% and Android at 10% (that's over 50%!).
*   [MailChimp](https://mailchimp.com/resources/research/impact-of-mobile-use-on-email-engagement/) found that unique clicks among mobile users for responsive campaigns rose from 2.7 to 3.1% — a nearly 15% increase.

"Responsive web design" is a phrase [coined by Ethan Marcotte](https://alistapart.com/article/responsive-web-design) back in 2010:

<blockquote>By marrying fluid, grid-based layouts and CSS3 media queries, we can create one design, that, well, responds to the shape of the display rendering it.</blockquote>

In the email world, we can still make use of **fluid design, grid-based layouts and media queries**. The problem is that not all clients support these. Therefore, we need some **hacks** along the way.

Until recently, Gmail did not support media queries. Thankfully, as of September 2016, [most of its clients do](https://gmail.googleblog.com/2016/09/better-emails-tailored-to-all-your-devices.html). However, several mobile clients still do not, including Yahoo, Windows Phone 8 and Gmail for Android.

Several techniques are used in the email world to get around a lack of support for media queries. Some of the terms you'll hear are "fluid," "adaptive," "responsive," "hybrid" and "spongy."

### Fluid

The easiest solution is to stick to a single column and make your emails fluid. This means that as the viewport shrinks, your content area shrinks.

<pre><code class="language-css">.container {
  max-width: 600px;
  width: 100%;
}
</code></pre>

### Responsive and Adaptive

Using media queries and breakpoints, we can provide alternate styles for different-sized viewports. We can also hide or show elements.

This starts to get complicated once you introduce a grid and columns. You could have a two-column layout and then switch to a stacked one-column layout below a certain viewport width.

_But_, as we've seen, media queries aren't supported everywhere, so this isn't always reliable.</p>

### Hybrid and Spongy

This technique uses a bit of fluid, a bit of responsive and a couple of hacks for Outlook support. We also get to ensure that the columns stack without media queries.

This technique is [outlined by ActionRocket](https://labs.actionrocket.co/the-hybrid-coding-approach), and Nicole Merlin has written a great [step-by-step tutorial](https://webdesign.tutsplus.com/tutorials/creating-a-future-proof-responsive-email-without-media-queries--cms-23919) on it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2309eacc-2b5b-4583-a4ee-27b417b12b46/14-responsive-large-opt.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee4b9d5-41e2-404c-b899-640575937744/14-responsive-preview-opt.png" alt="Hybrid/Spongy technique" /></a></figure>

Here is a snippet of the code I use to build most of my emails.

<div class="break-out">

<pre><code class="language-bash">
&lt;!--[if (gte mso 9)|(IE)]&gt;

&lt;table align="left" border="0" cellspacing="0" cellpadding="0" width="100%"&gt;
  &lt;tr&gt;
    &lt;td align="left" valign="top" width="50%"&gt;
    &lt;![endif]--&gt;
      &lt;div class="span-3" style="display: inline-block; Margin-bottom: 40px; vertical-align: top; width: 100%; max-width: 278px;"&gt;...&lt;/div&gt;
    &lt;!--[if (gte mso 9)|(IE)]&gt;
    &lt;/td&gt;
    &lt;td align="left" valign="top" width="50%"&gt;
    &lt;![endif]--&gt;
      &lt;div class="span-3" style="display: inline-block; Margin-bottom: 40px; vertical-align: top; width: 100%; max-width: 278px;"&gt;...&lt;/div&gt;
    &lt;!--[if (gte mso 9)|(IE)]&gt;
    &lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;

&lt;![endif]--&gt;
</code></pre></div>

<pre><code class="language-css">
@media only screen and (max-width: 620px) {
  .span-3 {
    max-width: none !important;
    width: 100% !important;
  }
  .span-3 &gt; table {
    max-width: 100% !important;
    width: 100% !important;
  }
}
</code></pre>

Take a look at Fabio Carneiro's [spongy open-source repository](https://github.com/fcarneiro/tedc15_template) on GitHub and read Stig's take on [coding mobile-first emails](https://medium.com/cm-engineering/coding-mobile-first-emails-1513ac4673e#.nbpmobgvq). Rémi Parmentier also has [another responsive technique](https://medium.freecodecamp.com/the-fab-four-technique-to-create-responsive-emails-without-media-queries-baf11fdfa848#.j6lqi5axh) that doesn't need media queries and makes use of `calc()` function.</p>

### Responsive Images

As mentioned, use Retina images at 1.5× to 3×, and set image dimensions inline.

<div class="break-out">

<pre><code class="language-bash">
&lt;img src="https://www.smashingmagazine.com/wp-content/uploads/2016/11/logo.png" height="100" width="600" alt="Company Logo" style="max-width: 100%;"&gt;
</code></pre></div>

We can't rely on `max-width: 100%;` because some clients ignore it. You will also want to embed the following CSS:

<pre><code class="language-css">
@media only screen and (max-width: 620px) {
  img {
    height: auto !important;
    max-width: 100% !important;
    width: auto !important;
  }
}
</code></pre>

## Automating Your Workflow

The process of putting together a bulletproof email is complex. There are a lot of steps, and there is room for a lot of things to go wrong.

Like any monotonous task with steps, I recommend automating what you can, so that you build the system once and make it easier for future work.

Brian Graves has a good post on [making your email modular](https://www.smashingmagazine.com/2014/08/improve-your-email-workflow-with-modular-design/). Just as you have a **design system and pattern library** for a website or application, you should do so for email, making components **reusable and emails consistent** across your product and company.

Kevin Mandeville recommends [using snippets of reusable code](https://litmus.com/blog/the-ultimate-guide-to-using-snippets-in-email-design) to optimize your workflow, so that you're **not constantly rewriting code**. In his post, he outlines how to use snippets in modern editors (such as Atom and Sublime), and he points to the community-contributed [library of snippets](https://litmus.com/community/snippets) hosted by Litmus.

For my own part, I've put together and open-sourced a Grunt workflow for [automating email builds](https://github.com/leemunroe/grunt-email-workflow). It **runs various tasks, such as inlining CSS**, compressing images, uploading images to a CDN, sending a preview, and testing with Litmus, all with one command. If you're new to Grunt, I've written a [detailed tutorial](https://webdesign.tutsplus.com/tutorials/using-grunt-to-make-your-email-design-workflow-fun-again--cms-22223) on how it works. [Foundation for Email](https://foundation.zurb.com/emails.html) also has some great automation tools for developers, as does Mailjet with its responsive email framework [MJML](https://mjml.io/).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76809480-c71f-427f-9d32-d1f0505841ab/15-grunt-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76809480-c71f-427f-9d32-d1f0505841ab/15-grunt-preview-opt.jpg" alt="Automated email workflow" width="300" /></a></figure>

## Looking To The Future

Google just recently rolled out [support for media queries](https://gsuite-developers.googleblog.com/2016/09/your-emails-optimized-for-every-screen-with-responsive-design.html); Microsoft has just [partnered with Litmus](https://litmus.com/blog/litmus-and-microsoft-partner-to-make-email-better) to "make email better"; and AOL's Alto now [supports responsive email](https://twitter.com/M_J_Robbins/status/679639156868431872). So, the future is looking much brighter.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d662d3a6-61a4-4510-9060-e8174066ecee/11-geo-large-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d92205ab-80e8-495c-9aec-2ccc3a48b132/11-geo-preview-opt.gif" alt="Email shopping cart" /></a></figure>

More and more companies and developers are experimenting with what's possible with email technology: [CSS animation](https://apps.balloondog.co.uk/emails/disney/WOE/production/), [audio](https://actionrocket.cmail20.com/t/ViewEmail/j/499D33718086CE64/2696DD450C6A11ABA0F01D70678E0DEE), [shopping carts in email](https://www.webdesignerdepot.com/2015/10/punched-card-coding-the-secret-of-interactive-email/). Expect more instances of interactive and [kinetic email](https://freshinbox.com/blog/the-dawn-of-kinetic-email/) emerge in 2017.</p>

## Conclusion

Email design and development is a beast. It is a lot **like building a web page… 10 years ago**. Email client vendors haven't been as progressive as web browser vendors in adopting new standards, and we users and companies don't adopt new email clients like we do with web browsers. Add to that the rise of mobile, and we're left in this state of having to support a **convoluted mix of clients and versions**.

My introduction here is a high-level overview; you could dive deep into every one of these points. Hopefully, it's given you good insight into the world of building and sending email, and the code snippets and resources have added some hours back to your life.</p>

### Recommended Resources

*   [Really Simple Responsive HTML Email Template](https://github.com/leemunroe/responsive-html-email-template), Lee Munroe (my free open-source email template)
*   [_Professional Email Design_](https://professionalemaildesign.com/), Jason Rodriguez
*   "[Unmasking HTML Emails](https://www.codeschool.com/courses/unmasking-html-emails)" (course), Dan Denney, Code School
*   "[The Best Email Designs in the Universe (That Came Into My Inbox)](https://reallygoodemails.com/)," Really Good Emails
*   "[Dynamic and Interactive (Kinetic) Email Examples and Techniques](https://freshinbox.com/resources/techniques.php)," Justin Khoo

### Blogs to Follow

*   [Campaign Monitor](https://www.campaignmonitor.com/guides/)
*   [MailChimp](https://mailchimp.com/resources/)
*   [Litmus](https://litmus.com/blog/)
*   [Email on Acid](https://www.emailonacid.com/blog)

{{< signature "il, vf, al" >}}
