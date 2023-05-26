---
title: 'A Complete Guide To HTML Email'
slug: complete-guide-html-email-templates-tools
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44bcbac0-67bb-4405-9f28-f4102877c4bd/16-html-email-templates-resources.png
date: 2021-04-12T12:30:00.000Z
summary: >-
  In a new short series of posts, we highlight some of the useful tools and techniques for developers and designers. Recently we’ve covered [CSS generators](/2021/03/css-generators/), [SVG generators](/2021/03/svg-generators/) and [accessible front-end components](/2021/03/complete-guide-accessible-front-end-components/). This time we look into templates and tools for building and designing HTML emails. [Don't miss the next one](/the-smashing-newsletter/).
description: >-
  A complete guide to HTML email templates, tools, resources and guides. Everything you need to know about designing and building HTML Email in 2021.
categories:
  - HTML Email
  - Generators
  - Tools
  - Templates
  - Round-Ups
  - Best Practices
last_updated: 2021-04-12T11:30:00.000Z
---


### Table of Contents

Below you’ll find quick jumps to particular components that you might need. Scroll down for a general overview. Or [skip the table of contents](#getting-started-with-html-email).

<ul class="toc-components">
<li><a href="#accessible-emails">accessibility</a></li>
<li><a href="#a-repository-for-email-bugs">bugs</a></li>
<li><a href="#dark-mode-in-gmail-and-outlook">dark mode</a></li>
<li><a href="#html-email-development-ide">editors and IDEs</a></li>
<li><a href="#html-email-feature-support-can-i-email">feature support</a></li>
<li><a href="#html-email-framework-based-on-tailwind-css">frameworks</a></li>
<li><a href="#getting-started-with-html-email">getting started</a></li>
<li><a href="#everything-html-email-resources">guides and resources</a></li>
<li><a href="#inline-css-and-transform-html-emails">inline CSS</a></li>
<li><a href="#email-inspiration">inspiration</a></li>
<li><a href="#mailto-link-generator">mailto link generator</a></li>
<li><a href="#mailto-selection-prompt">mailto selection prompt</a></li>
<li><a href="#email-marketing-resources">marketing</a></li>
<li><a href="#html-email-languages-and-frameworks">meta-languages</a></li>
<li><a href="#generate-a-full-page-email-preview">previews</a></li>
<li><a href="#making-email-better">productivity</a></li>
<li><a href="#remove-unused-css-from-email-templates">remove unused CSS</a></li>
<li><a href="#cheatsheet-for-targeting-email-clients">target email clients</a></li>
<li><a href="#bulletproof-html-email-templates">templates</a></li>
<li><a href="#mail-tracker-blocker">tracking blocker</a></li>
<li><a href="#inline-css-and-transform-html-emails">transform HTML</a></li>
</ul>

## Getting Started With HTML Email

If you’re just trying to understand everything that’s happening behind the scenes of a quirky world of HTML email, Caity G. O’Connor has published a wonderful guide on [how to start with email coding](https://explore.reallygoodemails.com/new-to-email-coding-heres-where-to-start-2494422f0bd4). The article features courses, tutorials, articles, and just general guidelines to keep in mind when building and designing emails &mdash; all in a comprehensive one-page-guide. On SmashingMag, Lee Munroe has published a [detailed guide to building and sending HTML emails](https://www.smashingmagazine.com/2017/01/introduction-building-sending-html-email-for-web-developers/) as well.

{{< rimg href="https://www.campaignmonitor.com/dev-resources/guides/coding-html-emails/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8de6f227-e945-4255-92d2-27d4b7685b10/07-email-article.jpeg" width="700" height="343" sizes="100vw" caption="If you are new to HTML Email coding, the <a href='https://explore.reallygoodemails.com/new-to-email-coding-heres-where-to-start-2494422f0bd4'>guide by Caity G. O’Connor</a> is a good place to start." alt="How to Code HTML Emails for Any Device" >}}

Alternatively, [How to Code HTML Emails for Any Device](https://www.campaignmonitor.com/dev-resources/guides/coding-html-emails/) is a very thorough guide on **building a reliable HTML email template**, and how to test it &mdash; along with a hands-on example of building a newsletter template from scratch. In general, that’s a very solid overview of everything you need to know to get started on the right foot.

Jason Rodriguez has a detailed [video course on HTML Email](https://thebetter.email/design/) (not free) with pretty much everything to know about them, from accessibility to troubleshooting, workflows and tools.

And if you find yourself struggling with an email issue or just looking out for some help from a community, [#emailgeeks](https://email.geeks.chat/) is a great starting point. It’s an invite-only Slack community with plenty of channels to discuss code, design, job openings, events and new tools and resources. You can also find many resources shared with the hashtag [#emailgeeks on Twitter](https://twitter.com/hashtag/emailgeeks). 

## HTML Email Languages and Frameworks

Coding clean, responsive emails that provide a solid experience in all popular email clients can be a time-consuming challenge. [HEML](https://heml.io/) is here to change that. The open-source **markup language** gives you the native power of HTML without having to deal with all of the email quirks. There are no special rules or styling paradigms to master, so if you know HTML and CSS, you are ready to start.

{{< rimg breakout="true" href="https://mjml.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e77de7a-d688-4b0c-b965-8fa7234b9da5/01-mjml.png" width="700" height="370" sizes="100vw" caption="<a href='https://mjml.io/'>MJML</a> makes the coding of responsive emails a little bit more convenient." alt="MJML" >}}

[MJML](https://mjml.io/) is based on the same idea of simplifying the process of creating responsive emails. The markup language is based on a **semantic syntax** that makes the process straightforward while an open-source engine does the heavy lifting and translates the MJML you wrote into responsive HTML. You can start out with a [step-by-step tutorial through MJML](https://mjml.io/getting-started-onboard).

A library of standard components saves you extra time and lightens your email codebase. And if you want to build your own, [Modular Template System Guide](https://blocksedit.com/email-template-guide/) might help, too.

Speaking of saving time: We all know that HTML email requires tables upon tables to work properly — and how tedious it can be to construct them. That’s where [Inky](https://get.foundation/emails/docs/inky.html) comes in. The templating language converts simple HTML tags like `<row>` and `<columns>` into complex table HTML so that you don’t need to bother.

## HTML Email Framework Based On Tailwind CSS
Making an HTML email work across email clients ain’t an easy task. Fortunately, there are plenty of reliable tools, templates and frameworks to make it easier to get your work done. For example, [Maizzle](https://maizzle.com/) is a framework that helps you quickly build HTML emails with Tailwind CSS and advanced, **email-specific post-processing**. It also provides a few ready-made projects ([Maizzle Starters](https://maizzle.com/starters/)) that you can start with right away.

{{< rimg breakout="true" href="https://maizzle.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f5ac31a-d009-415e-b2e3-ac7465c22ac6/08-maizzle.png" width="700" height="304" sizes="100vw" caption="An explanation of how Maizzle users ‘bring their own HTML’. (Image source: <a href='https://maizzle.com/'>Maizzle</a>" alt="BYOHTML coding with Maizzle" >}}

[Maizzle](https://maizzle.com/) uses the Tailwind CSS framework to enable designers and developers to easily prototype emails with HTML and CSS. It also comes with beautiful templates if you’d rather not develop every email from scratch. Alternatively, you might want to consider [MJML](https://mjml.io/) as well.

## HTML Email Framework Based On Sass

[Foundation for Emails](https://get.foundation/emails.html) helps you craft responsive HTML emails that play well with all major email clients, even Outlook. A grid-based approach ensures your email works on any device, UI patterns and a CSS inliner get the email into shape quickly, and Sass gives you control over common styles. No matter what you’re building, a selection of [responsive templates](https://get.foundation/emails/email-templates.html) for anything from transactional emails to drip campaigns and newsletters saves you time that you can spend on your copy or conversion funnels instead.

{{< rimg breakout="true" href="https://get.foundation/emails.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43b16188-287b-4c80-ac52-4f9cd480c081/foundation-for-email-opt.png" width="700" height="473" sizes="100vw" caption="<a href='https://get.foundation/emails.html'>Foundation for Emails</a> can be used with plain CSS or Sass, whatever you prefer." alt="Foundation for Emails" >}}

## Bulletproof HTML Email Templates

[Cerberus](https://tedgoas.github.io/Cerberus/) and [HTML Email](https://htmlemail.io/) provide small collections of **reliable, solid templates** for responsive HTML emails that are well-tested in 50+ email clients, including Gmail, Outlook, Yahoo, AOL, and many others. [EmailFrame.work](https://emailframe.work/) allows you to build responsive HTML email templates with pre-built grid options and basic components, supported in over 60+ email clients.

{{< rimg breakout="true" href="https://codedmails.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3fd74d8-9d95-4cea-a834-ab35c8acacb9/27-html-email-templates-resources.png" width="700" height="330" sizes="100vw" caption="<a href='https://codedmails.com'>Codedmails</a> includes 60 email templates and themes, all written in MJML, and tested for compatibility." alt="Codedmails" >}}

[Codedmails](https://codedmails.com/) includes 60 email templates and themes, all written in MJML, and tested for compatibility. The [code is all available on Github,](https://github.com/hunzaboy/CodedMailsFree) and the templates are free to use for non-commercial projects, while MJML source files are provided for an extra charge.

[Stripo](https://stripo.email/templates/), [Chamaileon](https://chamaileon.io/), [Postcards](https://designmodo.com/postcards/), [Topol.io](https://topol.io/), [GoodEmailCode](https://www.goodemailcode.com/), [Pixelbuddha](https://pixelbuddha.net/html) and [Bee Free](https://beefree.io/) all feature plenty of free HTML email templates, Litmus provides [Responsive Email Templates](https://litmus.com/resources/free-responsive-email-templates) for newsletters, product updates and receipts, and CampaignMonitor has a [free HTML email template builder](https://www.campaignmonitor.com/email-templates/) with drag’n’drop functionality. Another drag-and-drop editor worth considering is [Unlayer](https://unlayer.com/). It helps you create mobile-ready HTML email templates with just a few clicks — no coding involved.

## HTML Email Feature Support: Can I Email...?

A handy tool that belongs in everyone’s toolset who finds themselves wrangling HTML email &mdash; be it every now and then or regularly &mdash; is [caniemail.com](https://www.caniemail.com/). Inspired by the successful concept of [caniuse.com](https://caniuse.com/), *Can I email* lets you check support for 179 HTML and CSS features across 31 email clients.

{{< rimg breakout="true" href="https://www.caniemail.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78cbcb60-d754-4ab6-bf68-3cc51e265618/02-nth-last-child.png" width="700" height="414" sizes="100vw" caption="Can I email highlights web features and their support in HTML email clients." alt="Can I Email..." >}}

You can enter a feature to see **how well it is supported**, check the feature index, compare email clients, or view an email client support scoreboard that ranks email clients based on their support. The complete data is also available as a JSON file.

## A Repository For Email Bugs

Apple Mail not showing embedded SVGs, Gmail not displaying emails at full width, Outlook changing the behavior of animated Gifs &mdash; we all know how weirdly email clients sometimes behave.

{{< rimg breakout="true" href="https://github.com/hteumeuleu/email-bugs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2d6a864-8d1f-47a4-ace3-d22cb887d917/03-email-bugs.png" width="700" height="381" sizes="100vw" caption="Meet Email Bugs, a growing repository of, well, email bugs." alt="Email Bugs" >}}

To help you understand what’s going on when you come across bugs like these, Rémi Parmentier maintains [Email Bugs](https://github.com/hteumeuleu/email-bugs), a GitHub repository for **weird email client behaviors**. It not only makes the life of email designers easier by providing a place to discuss bugs but also tries to reporting each bug to the concerned company and fix them for good. But just in case it's not possible, [How to Target Email Clients](https://howtotarget.email/) provides an overview of workarounds to target specific email clients.

## Mailto Link Generator

Good old HTML links can do more than what we usually give them credit for. We might be used to `mailto:` prefix, but actually **generating the code** can be quite annoying. [Mailtolink.me](https://mailtolink.me/) does one thing, and it does it well: it generates the snippet for the `mailto` links including CC, BCC, subject line and body text.

{{< rimg breakout="true" href="https://mailtolink.me/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53cfbbcf-fbe1-423f-bc14-7209237cc8e0/9-html-email-templates-resources.jpeg" width="700" height="425" caption="A simple doing done one task well: Mailto Link Generator takes good care of mailto: links." sizes="100vw" alt="Mailto Link Generator" >}}

## Mailto Selection Prompt

Sometimes when you click on an email address, it might open an application that your customers aren’t really using. That’s why it’s common to copy-paste email addresses instead of clicking on the links directly. To avoid frustration on the other end, we can use [Mailgo](https://mailgo.dev/) and [MailtoUI](https://mailtoui.com/).

{{< rimg breakout="true" href="https://mailgo.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a10d6789-0e74-4210-ac91-b2f3be7a9a50/10-html-email-templates-resources.png" width="591" height="455" sizes="100vw" caption="<a href='https://mailgo.dev'>Mailgo</a> opens a prompt to allow customers to send email in their favorite client, or just copy the email address." alt="Mailgo" >}}

Instead of opening a native email client, both tools **prompt a modal window**, allowing the user to choose one of the preferred services, or copy-paste the link. Additionally, Mailgo can address all  `tel` links as well, allowing them to open Telegram, WhatsApp, Skype, call as default or copy the phone number &mdash; and it supports dark mode, too.

{{% ad-panel-leaderboard %}}

## Email Inspiration

It might seem like just because HTML email feels quite ancient and outdated, so are possibilities of what we can do with HTML email. However, [there are plenty of resources](https://airtable.com/shrJxffTnSHSdIwqN/tbltBA3AOkEaVg8wO), blogs and podcasts featuring new email techniques &mdash; some of them often being on the very creative side of things!

{{< rimg breakout="true" href="https://emaillove.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8455a787-e51a-4e82-b3ef-aaed1dc8eed6/12-html-email-templates-resources.png" width="700" height="343" sizes="100vw" caption="There is no shortage in HTML email showcases out there: <a href='https://emaillove.com'>Email Love</a> highlights thousands of them." >}}

[Litmus Blog](https://www.litmus.com/blog/), [CampaignMonitor blog](https://www.campaignmonitor.com/blog/) and [HTML Email](https://htmlemail.io/blog/) feature plenty of articles and podcasts with best practices, tips, resources, and even podcasts on HTML email. And if you need a bit of inspiration for recent emails, sorted by industry, [Really Good Emails](https://reallygoodemails.com/) and [EmailLove](https://emaillove.com/) have got your back, too.

- You don’t need to comb through your own email inbox to find HTML email design inspiration. [Email Love](https://emaillove.com/) has rounded up a fantastic selection of inspiring emails from top companies.
- [Really Good Emails](https://reallygoodemails.com/) makes it easy to search for HTML email inspiration. You have the choice of exploring the collection chronologically or you can narrow down the results based on what type of email it is (e.g. coupon, free trial), what the goal is (e.g. customer rewards, thank you), the company name or category and so on.
- Not enough? There is also [HTML Email Designs](https://htmlemaildesigns.com/) and [HTML Email Gallery](https://htmlemailgallery.com/).



{{< rimg breakout="true" href="https://reallygoodemails.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b045b179-dac4-4d32-989d-176c876921e9/13-html-email-templates-resources.png" width="700" height="369" sizes="100vw" caption="<a href='https://reallygoodemails.com/'>Really Good Emails</a> enables users to filter through over 7000  designs." alt="Really Good Emails" >}}

## Accessible Emails

With email, where do we stand in terms of *accessibility*? Do we announce emails properly to screen readers? What about dark mode? [Accessible Email repo](https://github.com/wilbertheinen/accessible-email-documentation) highlights a number of articles, tools, presentations and resources about accessibility &mdash; not only for email, but most specifically for it.

{{< rimg breakout="true" href="https://github.com/wilbertheinen/accessible-email-documentation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0a9f856-8785-4213-b9ca-5ee25adf7132/14-html-email-templates-resources.png" width="700" height="525" sizes="100vw" caption="<a href='https://github.com/wilbertheinen/accessible-email-documentation'>Accessible Email Repository</a> provides hundreds of resources and tools to test and improve the accessibility of your emails." alt="Accessible Email repo" >}}

With [Accessible-Email.org](https://www.accessible-email.org/), you can analyze sent campaigns and check for accessibility improvements. With [Dark Mode for Email Simulator](https://proofjump.com/dark-mode-simulator/), you can check how your email looks like in dark mode.

## Inline CSS and Transform HTML Emails

If all you need is a clean space to transform your HTML and CSS, [Alter.Email](https://alter.email/) is a reliable option. With the tool, you can choose a few “transformers” &mdash; e.g. **inline CSS and clean up the code**, remove unused CSS, as well as format HTML and even prevent widow words. Alternatively, you can also use [Postdrop](https://app.postdrop.io/) which also allows you to minify and inline CSS and send a test email as well.

{{< rimg breakout="true" href="https://alter.email/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44bcbac0-67bb-4405-9f28-f4102877c4bd/16-html-email-templates-resources.png" width="700" height="409" sizes="100vw" caption="A fantastic email tool when you need that level of details: <a href='https://alter.email/'>Alter.Email</a> allow you to change HTML on the fly. (Image source: <a href='https://alter.email/'>Alter.Email</a>)" alt="Alter.Email" >}}

## Remove Unused CSS From Email Templates

Writing CSS isn’t a particularly exciting task with HTML Email, scattered with `!important`  and inline styles all over the place. To **remove unused CSS** from email templates, there’s [Email Comb](https://emailcomb.com/). The tool allows you to add classes and IDs you'd like to ignore, choose if you'd like to minify it and remove comments, and it shows what exactly it has removed.

{{< rimg breakout="true" href="https://emailcomb.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3f70746-f835-4521-95ac-2c74ee9262c7/17-html-email-templates-resources.png" width="800" height="434" sizes="100vw" caption="Cleaning up your HTML email: <a href='https://emailcomb.com/'>Email Comb</a> removes what you don’t need, but you can add classes to ignore." alt="Email Comb" >}}

## Cheatsheet For Targeting Email Clients

Email clients modify and remove some of your HTML and CSS, often mercilessly. If one of the email clients doesn’t behave quite as expected, you might want to treat it separately. A [cheatsheet for targeting email clients](https://howtotarget.email/) allows you to pick a **target email client** and at least attempt to address it directly. It might not work all the time as email clients change all the time, but it’s something that’s worth giving a try.

{{< rimg breakout="true" href="https://howtotarget.email/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/365b48b8-7c25-4a07-a0db-f822cb913a84/28-html-email-templates-resources.png" width="800" height="392" caption="Just in case you really need it: <a href='https://howtotarget.email/'>targeting email clients</a> with hacky CSS selectors." sizes="100vw" alt="How To Target Email Clients" >}}

## Everything HTML Email Resources

[Thebetter.email](https://thebetter.email/resources/) provides a growing repository of useful email marketing resources, including people, learning sites, tools, details about email service providers, newsletters, code and interactive email resources. Hand-picked by Jason Rodriguez who’s been in the industry for years and has spent a lot of that time wading through the muck to find the good stuff.

{{< rimg breakout="true" href="https://thebetter.email/resources/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f74e00-cb23-4c2f-bde4-6a6c7976f2f1/20-html-email-templates-resources.png" width="800" height="460" sizes="100vw" caption="Everything from templates to marketing resources on <a href='https://thebetter.email/resources/'>TheBetter.email</a>." alt="Thebetter.email" >}}

## Email Marketing Resources

If you need to dive deep into the trenches of HTML email, best practices and email marketing, [CampaignMonitor Guides](https://www.campaignmonitor.com/resources/guides/) and [Mailchimp Guides](https://mailchimp.com/help/) have plenty of resources to get started. Indeed, some of them will be product-specific, but they're also more general guides around best practices for sending emails, design guides, delivery tips, anti-spam requirements and plenty of other topics along these lines.

{{< rimg breakout="true" href="https://blogs.oracle.com/marketingcloud/the-biggest-shifts-in-email-marketing-trends-for-2021-webinar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62bfceeb-54b6-4a72-814a-f3ed2bd9c981/23-html-email-templates-resources.png" width="700" height="466" sizes="100vw" caption="Thorough guides around building and marketing for email, as well as <a href='https://blogs.oracle.com/marketingcloud/the-biggest-shifts-in-email-marketing-trends-for-2021-webinar'>email marketing trends</a>, by Oracle. " alt="Oracle Email Marketing Trends" >}}

And if you are looking for ongoing trends in email marketing, [Oracle’s Email Marketing Trends](https://blogs.oracle.com/marketingcloud/the-biggest-shifts-in-email-marketing-trends-for-2021-webinar) includes plenty of videos around email deliverability, modular email architecture, email accessibility and also email marketing.

{{% ad-panel-leaderboard %}}
## Dark Mode In Gmail And Outlook

We’ve all got used to the dark mode in many apps and websites out there, but what about dark mode support in HTML email clients? We could, of course, serve the same email to all subscribers, but if you are used to dark mode on your operating system, a bright email might rather be offputting and **encourage abandonment**.

[The Developer’s Guide to Dark Mode in Email](https://www.campaignmonitor.com/resources/guides/dark-mode-in-email/) highlights some of the important guidelines to keep in mind when you are building a dark mode version of your HTML email. It explains how to target dark mode, how to deal with images and general browser support (which is pretty good!).

{{< rimg breakout="true" href="https://www.campaignmonitor.com/resources/guides/dark-mode-in-email/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4bd3ba1-c705-4040-8321-c5c12a8d7d5c/25-html-email-templates-resources.png" width="700" height="475" sizes="100vw" caption="<a href='https://www.campaignmonitor.com/resources/guides/dark-mode-in-email/'>The Developer’s Guide to Dark Mode in Email</a>: thorough and comprehensive." alt="The Developer’s Guide to Dark Mode in Email" >}}

Rémi Parmentier goes a little bit deeper, showing how to [fix Gmail’s dark mode issues with CSS Blend Modes](https://www.hteumeuleu.com/2021/fixing-gmail-dark-mode-css-blend-modes/). Gmail enforces a change of any light text color to dark text color. If you need to fix it, Rémi has come up with a creative use of `mix-blend-mode` (supported in Gmail) to maintain the light text color if you need to. And if you need to ensure that your emails respond to **Outlook.com**’s dark mode, Remi has got you [covered](https://www.hteumeuleu.com/2021/emails-react-outlook-com-dark-mode/), too. 

{{< rimg href="https://www.hteumeuleu.com/2021/emails-react-outlook-com-dark-mode/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6aff2d9d-391c-4232-9e87-d28fe632a0ff/24-html-email-templates-resources.png" width="750" height="1334" sizes="100vw" caption="Fixing Dark Mode in HTML emails: Rémi Parmentier get creative to <a href='https://www.hteumeuleu.com/2021/fixing-gmail-dark-mode-css-blend-modes/'>fix Gmail’s dark mode issues with CSS Blend Modes</a>." alt="Fixing Dark Mode in HTML emails" >}}

## HTML Email Development IDE

If you spend quite a bit of time with HTML email, you might want to use a dedicated HTML Email editor. [Parcel](https://useparcel.com/) is just that: a **code editor** built specifically for coding and designing emails. It provides live previews, so you can see in real-time what you are building, and it also has accessibility features out of the box, so you can check accessibility issues while you are building or designing the email. Plus, the tool also allows you to collaborate with your team and run email tests directly from the tool.

{{< rimg breakout="true" href="https://useparcel.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd45784e-bb81-4410-af77-348edd0952c5/15-html-email-templates-resources.png" width="700" height="367" sizes="100vw" caption="HTML Emails can be messy and difficult to build and maintain. HTML Email IDEs such as <a href='https://useparcel.com/'>Parcel</a> help you keep it all in order. (Image source: <a href='https://useparcel.com/'>Parcel</a>)" alt="Parcel" >}}

Alternatively, you can also take a look at [Mail Studio](https://mailstudio.app/), a sophisticated desktop application (for Windows, macOS and Linux) that combines visual and **code editing in one email IDE**.

The app comes with a library of components, from headings to navbars and accordions, a couple of responsive email templates, Google Fonts integrations, built-in Sass support, command palette, collaboration tools, email previews and even **integration with email service providers** such like MailChimp, Campaign Monitor and Sendgrid. Figma integration is supposed to be coming soon.

## Generate A Full-Page Email Preview

If you need a full-page preview of your HTML Email, [Emailpreview.io](https://emailpreview.io/) might be just what you need. You can copy/paste HTML, or **import an EML file** that you’ve just received, and the tool outputs a fully rendered image of your email. You can choose the device width as well. A helpful little tool to keep nearby.

{{< rimg href="https://emailpreview.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9213738f-bbc8-49f5-a583-c0a5375885bc/26-html-email-templates-resources.png" width="720" height="520" sizes="100vw" caption="Quick and easy: <a href='https://emailpreview.io/'>Emailpreview.io</a> generates a full-page preview of your emails." alt="Emailpreview.io" >}}

## Mail Tracker Blocker

Most marketing emails include trackers in HTML email, so they can track how often, when and where customers open emails. [MailTrackerBlocker](https://github.com/apparition47/MailTrackerBlocker) acts pretty much as an ad-blocker for browsers, but works with email clients. The tool labels who is tracking customers and removes tracking pixels before they can be displayed, so you can still load all remote content and keep your behavior private. Currently only available for Apple Mail on macOS 10.11 - 11.x (*shoutout to Jeremy Keith!*).

{{< rimg breakout="true" href="https://github.com/apparition47/MailTrackerBlocker" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95ee11c2-13dc-40d2-93f0-37e56d303363/28-html-email-templates-resources.jpeg" width="700" height="341" sizes="100vw" caption="You can use an ad-blocker to block third-party tracking, and for Apple Mail ther eis also MailTrackerBlocker to block tracking pixels in emails." alt="MailTrackerBlocker" >}}

## Making Email Better

Overflowing inboxes, spam with backlink requests, people emailing you on a Friday afternoon and following up on Monday morning &mdash; there are a lot of things that make dealing with email unpleasant. However, since there is no getting around email, there’s only one solution: Let’s improve the situation together. With that in mind, Chris Coyier is running “[Email is Good](https://email-is-good.com/)”, a site about **email productivity**.

{{< rimg breakout="true" href="https://email-is-good.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/456b5827-5001-4498-a13e-3a261045552c/06-email-is-good.png" width="700" height="368" sizes="100vw" caption="A fantastic little resource around email productivity. Emails might be difficult to code, but they aren’t inherently bad. " alt="Email Is Good" >}}

“Email is Good” takes a look at things that make emails annoying, **tips and ideas** on how we can do better, as well as little anecdotes that everyone can relate to. A great opportunity to reflect on how each one of us deals with email and the reactions that our email habits might provoke on the recipient’s side. 


## Wrapping Up

We probably have missed some important and valuable techniques and resources! So please leave a comment and refer to them &mdash; we’d love to update this post and keep it up-to-date for us all to be able to get back to it and build HTML email better and faster.

*Stay smashing!*

### Further Reading

- [CSS Auditing Tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/)
- [CSS Generators](https://www.smashingmagazine.com/2021/03/css-generators/)
- [SVG Generators](https://www.smashingmagazine.com/2021/03/svg-generators/)
- [An Introduction To Building And Sending HTML Email For Web Developers](https://www.smashingmagazine.com/2017/01/introduction-building-sending-html-email-for-web-developers/)
- Also, [subscribe to our newsletter](https://www.smashingmagazine.com/the-smashing-newsletter/) to not miss the next ones.

{{< signature "il" >}}
