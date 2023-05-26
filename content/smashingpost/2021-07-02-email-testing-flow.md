---
title: 'Email Testing Flow As It Should Be'
slug: email-testing-flow
author: andriy-zapisotskyi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57a53d31-9651-4d88-b2fe-f8de70c08da1/email-testing-flow.jpg
date: 2021-07-02T10:30:00.000Z
summary: >-
  Email sending functionality is an integral part of every digital product that involves communication with its users (read: any online service). With so many tools and approaches, email still has quite a few pain points, both for developers and email marketers. Email is difficult because it has too many aspects to set and a few instances with no common rules to follow.
description: >-
  With so many tools and approaches, email still has quite a few pain points, both for developers and email marketers. Email is difficult because it has too many aspects to set and a few instances with no common rules to follow.
categories:
  - Email
  - Tools
  - User Experience
---

We spend a lot of time and effort crafting emails with a specific purpose: to make their recipients read them and take the desired actions. The three known bottlenecks of every email sequence include:

1. **Deliverability** 
Emails are going to spam folders and are never read.
3. **Display issues** 
Email content is broken or not properly rendered and as a result, such emails are read but don’t prompt the reader to take action.
5. **Engagement** 
This is a whole set of reasons, such as vague email subject or unclear email copy, which can cause both not reading and not taking action.

How can we address these challenges? It is recommended to follow rules and [best practices of building](https://www.smashingmagazine.com/2018/03/email-marketing-programming-best-practices/) and sending emails.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af383d39-902f-4a56-ae72-ce26baf8dff2/2-email-testing-flow.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af383d39-902f-4a56-ae72-ce26baf8dff2/2-email-testing-flow.png" width="800" height="533" sizes="100vw" caption="The three known bottlenecks of every email sequence: deliverability, display issues, and engagement. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af383d39-902f-4a56-ae72-ce26baf8dff2/2-email-testing-flow.png'>Large preview</a>)" alt="email bottlenecks" >}}

But how do we know that they work?

By testing every single email aspect! Unfortunately, email testing is often underestimated and leads to email testing mistakes that kill all your effort spent on creating a great email sequence.

Let’s talk email testing! In this article, we’ll explain how a proper email testing workflow can help you improve email sending efficiency. We’ll describe **common testing approaches and mistakes**, and demystify the seamless email testing flow.

With this article, you will enhance your testing workflows by covering all the important aspects, and saving time and stress with suitable email testing methods and tools.

## Are You Keeping On Top Of Your Email Metrics?

While there’s always something to be improved, it’s important to understand when you underperform and need to take action right away.

With any type of email you send, you need to track at least these metrics:

<table class="tablesaw">
  <tbody>
    <tr>
      <td><strong>Open rate</strong></td>
      <td>How many messages you sent vs. how many of them were opened.</td>
    </tr>
    <tr>
      <td><strong>Bounce rate</strong></td>
      <td>How many emails were returned to you?</td>
    </tr>
    <tr>
      <td><strong>Click-through rate</strong></td>
      <td>For those emails that contain links, how many links were clicked?</td>
    </tr>
    <tr>
      <td><strong>Unsubscribe rate</strong></td>
      <td>For marketing email campaigns, the unsubscribe option is required.</td>
    </tr>
  </tbody>
</table>

When sending marketing messages (such as newsletters, special offers, [abandoned cart emails](https://sixads.net/blog/abandoned-cart-email-examples/), and so on), you can **compare your rates to the industry standards**. However, they will also change over time and in different circumstances.

According to [Hubspot](https://blog.hubspot.com/sales/average-email-open-rate-benchmark), the average email rates are:

- Open rate varies from 19% to 26% depending on the industry.
- Click-through rate is naturally lower, from 6.82% to 9.31%.
- Hard bounce rate should be as low as 0.3% to 0.9%.
- Unsubscribe rate is fine when it’s between 0.3% and 0.6%.

The research conducted by [Constant Contact](https://knowledgebase.constantcontact.com/articles/KnowledgeBase/5409-average-industry-rates?lang=en_US) shows the following numbers:

- The average open rate across all industries is 17.13%, with the highest value of 28.84% for religious organizations and the lowest of 10.25% for automotive services.
- Click-through rate is 10.25% on average &mdash; the highest is 17.35% for publishing and the lowest is 5.54% for real estate.
- Both hard and soft bounce rates are about 10.28% &mdash; as low as 6.47% for civic/social membership and as high as 15.47% for legal services.

With [transactional emails](https://mailtrap.io/blog/transactional-emails/), it’s a bit trickier, because the open rate you should strive for **depends on the type of email you send**. For example, reset password emails should be opened by the majority of your recipients, let’s say up to 90%. Order confirmation emails won’t have such a high open-rate but will receive much more interest than a marketing campaign, even with an exclusive offer.

The other side of the coin for transactional emails is that they should be opened by the right people at the right time. Otherwise, such emails are useless or even harmful. Imagine that John has just signed up for a financial service to create a tax report. To proceed, he needs to click a button in the confirmation email. After three hours, when John’s working day has already finished, he receives an email welcoming someone named Jack. Will he move on with that service? It’s doubtful.

We are pretty sure that you **test your emails before sending them** to avoid such ridiculous situations. But are you certain that your email testing flow is comprehensive and smooth enough?

{{% feature-panel %}}

## What Should You Test For Different Sorts Of Emails?

We have already mentioned the difference between marketing and transactional emails. Their purpose, sending method, and performance vary, and so should the testing flow.

However, the goals of testing are common for all types of email sequences &mdash; ensure deliverability, content excellence, and engagement. That’s why there is a list of aspects that you should test for any kind of email.

### Universal Email Testing Aspects

1. [**Email sending infrastructure.**](https://learn.g2.com/email-infrastructure)  
Even when you use a dedicated email marketing service, you need to check whether all integrations work perfectly fine, especially, when it is first set up.
  - Make sure you use the proper **domain** for sending emails. A mistake could be made when you work with several projects/websites.
  - Check whether necessary **authentication** methods are set &mdash; SPF and DKIM are required, while DKIM is highly recommended, but it’s still optional.
  - Test your **SMTP connection** (there are tools both for developers and marketers &mdash; we will take a look at them later in this article).
  - Examine all other additional settings, such as using dedicated or shared **IP**, **feedback loops**, and so on.

2. **Email template.**  
No matter what the message’s purpose is, it should be correct and visually appealing for every recipient.
  - Every company email, from a small notification to a detailed tutorial or newsletter, should be built with an [**HTML template**](https://www.smashingmagazine.com/2021/04/complete-guide-html-email-templates-tools/). It is important to make sure that your message looks as designed for all your recipients. The trick is that different email clients use different rendering engines &mdash; this means that there is no standard for processing email templates. Even if you included a small PNG picture, there’s no guarantee that it will be properly displayed across all email clients and devices &mdash; let alone more complex elements, such as video or animation.
  - Needless to say, the email message must not contain any mistakes or typos. **Email copy** also needs testing, to be clear, concise, and correct.
  - All the **links and buttons** should be valid and lead to the right destinations. Pay special attention to automatically generated personal links &mdash; for example, account confirmation, password reset, personal offer, etc.
    - **Personalization and/or dynamic content.**  
    Today almost all messages contain at least a tiny bit of personalization. When using merge mechanisms, make sure that emails are sent to the right addresses and that dynamic variables are generated correctly (e.g. username, location, behavior in the app, and so on). Otherwise, you risk not only offending your customers by calling them a wrong name (Hello %FirstName%!), but also disclosing personal information. All in all, it may result in a low [conversion rate](https://blog.appsumo.com/conversion-rate-formula/) for your campaigns.

3. **Email headers and subject.**  
The sender’s name and the email subject line are the first two things the recipient sees and considers when clicking your message to open it or to route it to a spam folder. Add more focus here!
  - **From, To, and Cc** are three well-known headers. Make sure they are technically correct, and also don’t be afraid to experiment &mdash; changing the “From” address can also impact the email open rate. 
    - **The subject line** is also a header, and much has been said about it &mdash; there are special subject line checkers, various lists of “100 words that you shouldn’t use in subject lines”. Besides, the email subject is the first thing used in email A/B testing. So we won’t focus on it a lot. Let’s talk instead about the **pre-header**, the third thing you see in your email inbox after the sender's name and subject line. Pre-header is often neglected, but it’s a preview text that should explain the quintessence of your message and nudge a recipient to open it. If you don’t set it, the first characters of your email will be used by default. Why should you waste those precious 50-100 characters for “Hey #name something”?  
    **Tip**: *Use the [`&nbsp`](https://mailtrap.io/blog/nbsp/) trick to set a pre-header if your email sending tool doesn’t offer such functionality, and then test how it will look for your recipients.*
  - **Technical headers or metadata.**  
  There is message metadata that can help you debug messages or track them. For example, some providers allow adding categories to the X-SMTPAPI header of the emails, which is useful for email performance tracking. Checking the raw message data can provide you with helpful information if you are an advanced SMTP email user.

4. **Spam checks.**  
Would you like to have a list of precise criteria that cause emails to be marked as spam? Everyone would, especially spammers. That’s why you can only follow some general rules and use dedicated services that analyze the reputation of your sending IP, the content of your email headers, the correctness of your HTML, whether you use certain phrases, and so on. Transactional emails can get classified as spam, too.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74221054-cc79-4035-85fd-cf422116631c/universal-email-testing-aspects.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74221054-cc79-4035-85fd-cf422116631c/universal-email-testing-aspects.png" width="800" height="533" sizes="100vw" caption="Universal email testing aspects (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74221054-cc79-4035-85fd-cf422116631c/universal-email-testing-aspects.png'>Large preview</a>)" alt="Universal email testing aspects" >}}

### Peculiarities Of Transactional Email Testing

When you [send triggered emails](https://www.smashingmagazine.com/2018/06/guide-transactional-email/), especially from your own application or online service, you should take care of a few more aspects.

1. Test your sending script. Here are two important aspects:
  - Test whether your **code works** and sends emails in the right way.
    - Check whether it seamlessly works with triggers: when a user completes a specific action, they should receive an appropriate email notification. It’s efficient to cover this part of your app functionality with **automated tests** &mdash; perform user acceptance testing.

2. If you are launching a large-scale system, it’s important to perform **email app load testing**. What if 2,000 users simultaneously click “reset password”? What happens next? How soon will they receive an email confirmation?

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bb19aee-5956-4fad-88fb-b0a3d653639e/1-email-testing-flow.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bb19aee-5956-4fad-88fb-b0a3d653639e/1-email-testing-flow.png" width="800" height="433" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bb19aee-5956-4fad-88fb-b0a3d653639e/1-email-testing-flow.png'>Large preview</a>)" alt="transactional email testing" >}}

### Marketing Emails Testing Focus

When you use a [bulk email service](https://www.sendinblue.com/bulk-email-service/), in most cases, you have built-in automation and basic testing functionality.

However, there are a couple of moments that require manual checking. They may seem obvious, but are still often overlooked.

- Make sure that the **right database is selected** (or the right list of contacts in your email marketing service). There are many cases when test emails are sent to customers, or a customer segment receives an offer that is not valid for them. 
Our favorite real story is about the US embassy in Australia accidentally sending out a test email known as a “Cookie Monster cat email”. It had “Meeting” in the subject line and a picture of a cat in blue pajamas holding a plate of cookies in the content. They were testing some new email sequences and selected their real email database instead of a testing list.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dc18897-9869-44dc-bd4f-6537079b7c29/4-email-testing-flow.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dc18897-9869-44dc-bd4f-6537079b7c29/4-email-testing-flow.png" width="800" height="452" sizes="100vw" caption="Have you heard about the Cookie Monster cat email incidence? (Image source: <a href='https://www.stuff.co.nz/oddstuff/107858968/us-embassy-apology-after-cat-pyjama-invite'>Stuff</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dc18897-9869-44dc-bd4f-6537079b7c29/4-email-testing-flow.png'>Large preview</a>)" alt="A photo of pajama-wearing cat featured in the email from the US embassy in Australia." >}} 

This email failure quickly [became popular on Twitter](https://twitter.com/usembassynz/status/1051674111712186368). Dozens of cat memes on social media are obviously funny, but this is not always the type of PR activity you expected to be part of. 
Take care of the proper naming for your clients’ lists &mdash; in some tools, they can be visible for your customers when they double opt-in or unsubscribe.

- **Check Bcc and Cc** to not reveal any email addresses. It is not recommended, but sometimes Bcc is still used for sending small batches of emails. Just a couple of years ago one online media for software developers sent a digest to its subscribers by listing them in a Cc field. Therefore, everyone on that list could see the email addresses of other recipients &mdash; obviously, the Cc and Bcc fields were just confused in that message.

## Common Email Testing Mistakes

Everyone has received an email sent by mistake at least once. Wrong links sent in promo campaigns don’t cause much harm, but what if your broken email script can lead to a data breach or a system crash? With strict data privacy guidelines, such as [GDPR](https://www.smashingmagazine.com/2021/03/state-gdpr-2021-cookie-consent-designers-developers/) and CCPA, unintentional emailing to unsubscribed users or using email addresses of people who have never subscribed to your communication can lead to conflicts or penalties.

There are two main types of email testing mistakes:

1. Important email aspects being ignored or
2. The email testing infrastructure being set improperly.

In many teams, the email testing process is limited to sending a few test emails to your own or colleagues’ inboxes. Alternatively, public email inboxes for testing are used not to flood personal inboxes.

What can such an approach inform you about? Well, you can learn that your email sending service is functioning and that your email content is displayed correctly in your recipients’ email clients (or in a web browser). You can also ask your colleagues to click links and read the email copy. But what about other [email clients](https://www.liveagent.com/blog/email-alternatives/) and, even more importantly, deliverability?

Another point is **testing 5 emails out of 5,000**. When you have a robust email-related system, you have to make sure that it functions correctly. We have mentioned the importance of merging mechanisms, so here’s the case &mdash; can you be certain that the billing information of Mr. Bluesky & Co. doesn’t go to Bluebird & Bluebird because of a tiny mistake in your database? The most efficient way is to run a set of automated tests (for example, with [Selenium](https://www.smashingmagazine.com/2018/04/feature-testing-selenium-webdriver/)) and check the content of each email.

## Correct Email Testing Process

A smooth email testing process is based on simple principles:

- **Use a checklist** to cover all important email aspects.
- **Automate** everything you are able to in order to minimize human error.
- **Limit access to your sending servers** and deployment processes.
- **Run all tests in a staging environment** and use a fake SMTP to avoid sending test emails to real users. Some developers tend to use [/dev/null fake SMTP server](https://pypi.org/project/nullsmtp/) for email testing, but this is not efficient as it doesn’t imitate production. If you run tests in a production environment, be ready to reveal test data to real users.
- **Use server monitoring tools.** They can help you indicate the abnormal activity and quickly take action if something goes wrong.

{{% ad-panel-leaderboard %}}

## Email Testing Toolkit

There is no ubiquitous email testing flow because the process of testing depends on the type of email campaign you send, the method you use (whether it’s an [email marketing service](https://wordable.io/best-email-newsletter-tools/) or your custom email functionality in your application), and the team you work with.

Development and QA teams who build transactional email sequences usually run automated tests by integrating testing frameworks and tools, such as [Selenium](https://www.smashingmagazine.com/2018/04/feature-testing-selenium-webdriver/).

For marketing campaigns, it’s more common to <strong>create an email testing checklist</strong>. I’d recommend creating a custom email testing list based on the aspects explained in the “<a href="#test-diff-sorts-emails">What should you test for different sorts of emails?</a>” section and competing it with the tools of your choice.

When you select an email tool, especially a paid one, pay attention to those services that offer wide functionality and can be used by both marketing and development teams.

We have talked about the general rules of successful and painless email testing. Now let’s go into detail about each type of test, with examples of tools.

### How To Test Sending Infrastructure

This type of testing is usually used by developers, but there are tools that can come in handy for marketers as well.

In general, you should test your mail server when you establish a new integration, change your setup, or **maintain your own email sending infrastructure**.

Telnet is a computer protocol that provides communication with a remote server. It’s also a command-line utility available in most common computer systems, including Windows, Mac, Linux, and more. It can help you test server connection, ports open for email communication, supported SMTP commands, relaying specific email addresses or domains.

To use this utility for testing, you will need to run a set of SMTP commands in a telnet client (which is pre-installed on the majority of systems).

[Wormly](https://www.wormly.com/) is an uptime monitoring service that also has an SMTP/Mail Server Test. It can help you test whether your SMTP server is configured correctly by sending a test message to your email server. Wormly will log the SMTP conversation for you so you can **check and debug errors or exceptions** if there are any to be found.

It’s super simple to use: you just need the address of your sending server, a recipient email address, and a port. You can also share the results of your team with a shareable link. Here is the case of how a marketer can use it &mdash; run a test in Wormly, proceed if no errors were thrown, and, if any were found, send a link to your dev team for troubleshooting help.

Wormly can be also useful for SMTP server monitoring, which I’ve mentioned in the <a href="correct-email-testing-process">Correct Email Testing Process</a> section.

[Gmass](https://www.gmass.co/) is an email marketing service inside Gmail. It also has a mail merge functionality and cold email sending options. The tool is a paid service, but it has a few helpful free tests:

- SMTP tester,
- Email tester (SPF, DKIM, blacklisting),
- Inbox, Spam, or Promotions (inbox placement),
- Email verifier (contact list),
- Email deliverability wizard (stats for a list of campaigns via any Google account within the last 24 hours that had at least 1,000 recipients).

If you expect high loads on your email server, it will also be good to perform load testing with a tool like [Apache JMeter™](https://jmeter.apache.org/) or an email sandbox service.

{{% ad-panel-leaderboard %}}

### How To Test Email Content

In this category, you have the widest choice of tools. We will name a few to provide you with a starting kit.

#### Email Template Checkers

When building an HTML email template with a special [template builder](https://www.activecampaign.com/email-templates) or using a drag-and-drop editor in your email sending tool, you will have a preview option. It will display how your template is rendered and, in most cases, **how it looks on different devices**.

If you need a separate solution for HTML preview, you can use a tool like [PilotMail](https://www.pilotmail.io/). It provides an email builder, layout viewer, and a test email sending to 10 addresses. There is a free plan, but the paid one costs just $3/month.

With no rendering standards for email clients, it’s important to perform email client testing to make sure that your email will look perfect in any of the recipient’s email clients. The most popular tools in this category are [Litmus](https://www.litmus.com/) and [Email on Acid](https://www.emailonacid.com/). They generate previews for a list of email clients and **allow you to manually compare them and look for issues**. You can experiment with both of them on a 7-day free trial, while further usage starts at $73/month.

Another approach for email client testing is used in [HTML Email Check](https://www.htmlemailcheck.com/) and [Mailtrap](https://mailtrap.io/) (As a friendly disclaimer, I actually work there.) These tools analyze your email template for HTML and CSS validity and provide you with an actionable list of errors for each email client. Free plans are available for both tools, and their paid subscription plans start at $10/month.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7476cd-ad17-4a92-8804-9ceea207948b/3-email-testing-flow.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7476cd-ad17-4a92-8804-9ceea207948b/3-email-testing-flow.png" width="800" height="626" sizes="100vw" caption="HTML Check feature in Mailtrap displaying the email market support score and listing possible errors. (Image source: <a href='https://mailtrap.io'>Mailtrap</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7476cd-ad17-4a92-8804-9ceea207948b/3-email-testing-flow.png'>Large preview</a>)" alt="HTML Check feature in Mailtrap displaying the email market support score and listing possible errors." >}}

#### Email Content Checks

Spell checkers and content testing tools are helpful for emails as well. [Grammarly](https://app.grammarly.com/) or [ProWritingAid](https://prowritingaid.com/Free) can help you check your email copy for errors and typos (both have free plans). [Hemingway Editor](https://hemingwayapp.com/) can give you tips on improving readability and if you’re struggling with writing, [Conversion.ai](https://www.conversion.ai/) can actually write you an email copy.

#### The Subject Line And Preheader

Email marketing services usually provide options to preview the subject line and preheader. You can also play with [TESTSUBJECT](https://zurb.com/playground/testsubject) by Zurb that displays email subject and preheader previews for a few types of mobile devices. [Preheader Testing Tool](https://codepen.io/mtthlbg/pen/mVjPrd) also provides similar functionality.

[Subject Line Tester](https://coschedule.com/email-subject-line-tester) by CoSchedule and [Send Check It](https://sendcheckit.com/email-subject-line-tester) can help you optimize your subject line for driving more opens.

#### How To Test Email Deliverability

Finally, we’ve made it to our favorite, but the most complicated, point &mdash; [email deliverability](https://mailtrap.io/blog/email-deliverability/). A whole set of factors impact your spam score: sender reputation, authentication, and email content.

There are a few tools that test your email against all the criteria.

You can start with [Mail Tester](https://www.mail-tester.com/). It’s free, but it provides a number of important tests. You can view your message and its source code after sending your email to a provided test address, get a SpamAssassin score, authentication check, message body analysis (it also shows HTML size), blacklisting report, link validation, and more.

Free Spamcheck by Postmark offers similar functionality. You can use it without sending a test message &mdash; just paste your HTML code with all headers and get an instant result. You can also integrate Spamcheck with your app via their JSON API and run automatic spam checks for all emails you send.

If you need a more robust solution, there is [GlockApps](https://glockapps.com/). It has a 14-day free trial and then offers subscription plans starting at $79/month. By the way, their website states that:

<blockquote>“On average 51% of emails never reach the inbox! So where do they go? 26% go to the spam or junk folder and 25% are never delivered.”</blockquote>

GlockApps is known for its powerful reports available for registered users. It provides inbox placement, reputation check, DMARC analytics, bounce analytics, automatic tests, monitoring and alerts, and template editor. In addition, there are a few useful separate free tools: domain checker, inbox email tester, inbox insight, DMARC analytics, and uptime monitor.

Deliverability tests are also included in many full-featured email sending and testing tools.

## Summary And Main Takeaways

The main purpose of this article was to prompt you to take email testing seriously, run it as a separate project, and pay attention to every important aspect. **Email is not just another line in someone’s inbox** &mdash; it’s a part of the user experience of your app, website or blog. It’s ideal to be able to have a team of marketers, developers, product managers, and QAs who can work together on spotless email sequences. But even if you are running a small project or have limited time and resources, you have a great list of handy tools that can do the job for you.

For any type and scale of the email-related project, it is worth allocating time to establish an email testing workflow and to **experiment with tools**. This will save you time and improve the quality of your campaigns at every iteration. And of course, you are very welcome to share your email testing stories and approaches in the comments!

### <span class="rh">Related Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'A Complete Guide To HTML Email'" href="https://www.smashingmagazine.com/2021/04/complete-guide-html-email-templates-tools/" rel="bookmark">A Complete Guide To HTML Email</a></li>
<li><a title="Read 'Design Your Mobile Emails To Increase On-Site Conversion'" href="https://www.smashingmagazine.com/2019/06/design-mobile-emails-increase-on-site-conversion/" rel="bookmark">Design Your Mobile Emails To Increase On-Site Conversion</a></li>
<li><a title="Read 'Level-Up Email Campaigns With Customer Journey Mapping'" href="https://www.smashingmagazine.com/2017/11/email-customer-journey-mapping/" rel="bookmark">Level-Up Email Campaigns With Customer Journey Mapping</a></li>
<li><a title="Read 'Everything You Need To Know About Transactional Email But Didn’t Know To Ask'" href="https://www.smashingmagazine.com/2018/06/guide-transactional-email/" rel="bookmark">Everything You Need To Know About Transactional Email But Didn’t Know To Ask</a></li>
<li><a title="Read 'HTML Email with Rémi Parmentier'" href="https://www.smashingmagazine.com/2019/11/html-email-webinar/" rel="bookmark">HTML Email with Rémi Parmentier</a> (webinar/video)</li>
</ul>

{{< signature "vf, yk, il" >}}
