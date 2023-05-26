---
title: 'Preventing Spam: Bulletproof Solutions'
slug: preventing-spam-bulletproof-solution
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11fd16f0-39b7-4a4b-ad88-1d472a4829cf/illuemail.gif
date: 2006-12-14T15:25:28.000Z
author: vitaly-friedman
description: >-
  Spam is probably one of the most difficult problems we have to deal with.
  E-Mail-filters, such as those used in GMail, provide accurate results, but not
  every company is willing to use extern services for its private mails. The
  problem occurs when web-developers have to display e-mail-addresses on a
  web-page.
categories:
  - Workflow
  - Emails
---
Spam is probably one of the most difficult problems we have to deal with. E-Mail-filters, such as those used in GMail, provide accurate results, but not every company is willing to use extern services for its private mails. The problem occurs when web-developers have to display e-mail-addresses on a web-page.

How can you make sure that not a single spam mail will find its path to the <a href="https://www.smashingmagazine.com/2013/04/rise-your-email-above-inbox-noise/">inbox</a> of your client? Or, speaking in more concrete terms, the question is, <strong>how should you display e-mails on a web-page in order to minimize spam attacks</strong>? Let's take a look at some modern and bulletproof solutions and techniques which will help you to prevent spam in your mailbox or the mailbox used by your clients. 

## Avoid stereotypes

Sometimes web-developers tend to rewrite the original e-mail, so spam-bots can't recognize it. This method might solve the problem, but <strong>spam-bots might catch on this sooner or later</strong>. Besides, many users might have problems decoding it - unless you provide some instructions how to decode the text. Most popular approaches are:

*   Replace dots with "d-o-t", "@" with [at] and as many spaces as possible. **Example:** e-mail@office.com -> e-mail [at] office [d-o-t] com
*   Insert some characters before and after the "@"-symbol. **Example:** e-mail@office.com -> e-mail {!@!} office.com.
*   Avoid stereotypes - e-mails like info@domain.com, service@domain.com, admin@domain.com are likely to be spammed anyway.

{{% feature-panel %}}

## Replace text with images

Apparently, most spam-bots don't scan images on the web (yet?), so it seems reasonable to <strong>place the text inside of an image</strong> without referring to it as an e-mail-address. There are free web-tools which generate images "on the fly", so the only thing you have to do is to place them on web-pages.

*   [E-Mail Icon Generator](https://services.nexodyne.com/email/index.php) for GMail, Hotmail, MSN, Yahoo!, AOL and many more.
*   [Signature Generator](https://www.signaturegenerator.net/) does basically the same as E-Mail-Icon Generator.
*   [Safe Mail](https://safemail.justlikeed.net/) creates your own email image in three steps.</p>

## Replace text with ASCII and Javascript-coded text

Another popular approach is to represent e-mail-adresses as ASCII code or Javascript-coded text. Users don't see any difference in e-mail-presentation, but <strong>spam-bots won't find the e-mail</strong> analyzing the source code - well, not yet. Some web-tools to convert e-mail links to ASCII code:

*   [Online Email Protector](https://www.iconico.com/emailProtector/): to use, simply type you email address below and then click in either of the textboxes. You can use the simple link code, or the more complicated Javascript link.
*   [Email Riddler](https://www.dynamicdrive.com/emailriddler/) is an online tool that encrypts and transform your email address into a series of numbers when displaying it, making it virtually impossible for spam harvesters to crawl and add your email to their list.
*   [Advanced Email Link Generator with Anti-Spam Encoder](https://www.willmaster.com/possibilities/demo/aelgwase.html): this tool will generate mailto: links you can copy and paste into your web pages and emails. The Anti-Spam Encoder is an encoding scheme designed to cloak email addresses from spammer's email harvesting robots, yet be visible and readable for your site visitors.</p>

## Bulletproof Solution

A simple solution I've been using for my recent project turned out to be the most effective I ever had. The most important rule to avoid spam is <strong>never</strong> mention it somewhere in the Web. So what I've suggested to do is to <strong>create two e-mail-accounts</strong> - the one for business contacts, which will be used only for communication with partners and serious clients and the second one, which will be decoded and published on the Web for any other purposes.

Once a potential client has written at the e-mail-address mentioned on the Web, the company will continue its communication via the first, "business" e-mail. On the other hand, brief questions or some small remarks will be responded via "open" e-mail, published online. Once the "open" e-mail gets included in spam databases and the company starts to get junk mail, it will be replaced by a new one.

This way your primarily, business contacts will always stay in touch with you via your business account and you <strong>reduce the amount of received spam to 0%.</strong>

## Using GMail spam-filters externally

Another useful technique to minimize the amount of spam-mails ending up in your inbox is letting it through gmail-filters. Unfortunately, GMail doesn't have a function which would enable users to use Google's filter directly. However, you can forward all the mails coming to your e-mail-box to your GMail account, and set your GMail account to forward the filtered messages to your private "clean" e-mail-account. The results aren't always accurate, but you'll see the difference immediately.

Have your e-mails already <strong>been flagged as spam</strong>, although you've sent a seemingly legitimate proposal to your client? Have you ever wondered why the efficiency of your newsletter campaigns suddenly dropped down? In both cases you deal with a problem which is harder to get done with than you think it is: bulletproof e-mail delivery.

The main problem with undelivered mails is that both sides — sender and recipient — don't really know what happened. Was the e-mail sent? Is the task done? Was the e-mail delivered? Most recipients will never know that an e-mail flagged as spam was sent to them — they just don't receive the e-mail. And most senders will never know that an e-mail flagged as spam wasn't delivered — they just don't get a response.

This article suggests <strong>over 20 bulletproof techniques, best practices and related services you can use to ensure best e-mail and newsletter delivery rates</strong>.

## Where Do We Stand?

E-mail is a primarily mean of communication in the Web. Instant messaging supplements e-mail, however it's a choice when it comes to communication with people you know well and/or you have a regular contact with. So where do we stand? And what is the main problem with e-mail delivery? And why do we have to deal with it?

1.  **Spam-filters calculate "spam score" to detect junk mail.** To determine whether a given e-mail is spam or not most spam filters consider a number of different attributes, such as content, length, percentage of text, use of images, number of recipients, headers etc. Usually they calculate the so-called "spam score" for every e-mail which passes the server.If the mail's score exceeds a certain threshold the mail is blocked and lands in the spam folder. The level where the threshold is set is defined by the mail server configuration. By default, this spam filter flags messages with a score greater than 5 as spam.
2.  **Spam filters aren't perfect.** Over the last years the efficiency of spam filters used by e-mail software clients and web-based e-mail-services has improved dramatically. However, since the strength level of anti-spam-algorithms has increased, it's inevitable that also more legitimate e-mails don't get through them. The result is that these filters, in order to block a good percentage of spam mails, block a good percentage of "suspicious" — in reality non-spam — messages as well.
3.  **Newsletters remain important, RSS-feeds haven't made the breakthrough yet.** In its recent usability study Nielsen Norman Group [found out](https://www.nngroup.com/reports/newsletters/summary.html "Email Newsletter Usability") that news feeds are definitely not for everybody, and they’re not a replacement for email newsletters. Apparently, "feeds are a cold medium in comparison with email newsletters. Feeds don’t form the same relationship between company and customers that a good newsletter can build.[..] Given that newsletters are a warmer and much more powerful medium, it is probably best for most companies to encourage newsletter subscriptions and promote them over feeds on their website." Therefore it's important to be aware of some sound techniques to pass through anti-spam-filters and thus guarantee a good newsletter delivery.
4.  **E-mail delivery is tricky.** The fact is that in most cases you never really know whether your first e-mail adressed to someone who doesn't know you and/or isn't expecting your e-mail will come through mail filters. And since the recipient doesn't expect your mail he/she won't be able to take it into consideration. Therefore it's necessary to be aware of some techniques to ensure the delivery of your e-mails.</p>

## Best Practices For E-Mail Delivery

According to latest studies, your <a title="Content isn't major reason ISPs filter legitimate email marketing mails into the spam folder" href="https://www.lyris.com/news/pr/pr-052907.html">reputation determines your email delivery more than your content</a>. So if you meet the expectations of your readers / recipients and don't send irrelevant information you improve the delivery rates of your e-mails. Apparently, "most delivery challenges are due to subscriber feedback; such feedback typically takes the form of complaints by recipients who mark the message as "spam" in their respective email clients and problematic traffic patterns such as bounces and spam trap hits."

However, it's not always enough. Let's take a look at the best practices for optimal e-mail delivery rates.

1.  **Avoid follow-ups, ask for a brief feedback — one word "soon" is enough.** Since you don't know whether your e-mail is delivered or not, don't assume that it is delivered. However, don't send a follow-up in doubt; follow-ups which usually include the copy of an original e-mail aren't effective and get on recipients' nerves. Instead ask the recipient in the first message to send you a brief note that your e-mail was received. For instance, ask to write back "soon", "got it" etc. once they've received the e-mail — indicate that no further comment or instant reply to your mail is necessary.
2.  **Don't attach large files to your first e-mail** (unless specified by the employer). Instead provide the detailed information on where the your CV and portfolio can be found on your personal web-site. Or simply copy and paste your resume in your e-mail. Compressed files (.zip, .tar etc.) and images are still strong signals for spam detection algorithms.
3.  **Use a consistent senders' name and email.** Make it easier for your recipient to recognize you. Don't change from "Max Mutermann" to "Developer's team". Don't change your e-mail suddenly. Once your recipient has mistakenly considered and reported your message as spam you are likely to never be able to contact them again.
4.  **Never put a link before important information.** Once the recipient has clicked upon the link you've provided and landed on some page he/she has no information about, you're lost. Many recipients might not get back to your message and report you as spam.
5.  **Snail mail is bulletproof.** If possible, follow-up on your e-mail with a "snail mail" version sent to the real postal address. This is a great way to establish contact and stay in touch with a person! Reference the e-mailed version you sent (including the date, time, and subject if possible). [[Source](https://www.job-hunt.org/article_antispam.shtml)]
6.  **Avoid fictional or irrelevant sender's name.** Communicate with your recipient personally. Instead of nicknames or company titles use your first and last name. Notice that spam-filters award e-mails without sender's name (or with an empty name) with spam score points. The sender's name shouldn't include numbers or symbols rather than your actual name. Instead of "no-reply@yourdomain" or "admin@yourdomain" provide your readers with concrete **and short** contact information, e.g. "Max Mustermann" <max_mustermann@yourdomain.com>. The "reply-to" field shouldn't be empty.</p>

## Best Principles For Bulletproof Newsletter Delivery

Since newsletters are still an important part of marketing campaigns, to achieve the highest response rate you'd like to ensure the highest delivery rate. The principles and rules listed below might help you to increase the delivery rate of your newsletters.

1.  **Send newsletters regularly.** Let your subscribers know when your emails are coming. If you offer a subscription to your newsletter from your web site then tell each and every subscriber exactly when to expect your newsletter.
2.  **Tuesday / Wednesday 2-3pm = Increased Response.** Your subscribers will come to "expect" your email to arrive in their inbox on the same day at the same time every week, meaning that they want to read your content and are generally more receptive to any special offers or promotions you may include. This means that they are less likely to misunderstand your newsletter and report it as spam.
3.  **Slow down your newsletter delivery.** Instead of using tools which boost your newsletter through mail servers to achieve "instant delivery" prefer "slow" delivery tools. Avoid sending mails to multiple (dozens or even hundreds) recipients using CC:-attribute. Use professional newsletter software or professional e-mail-delivery services. "When ISPs detect a flood of email, it looks like the work of a virus or a spammer." [[Source](https://www.imediaconnection.com/content/6806.asp)]
4.  **Use a tag line at the beginning of the subject line.** Mark your newsletters as such. Make it easier for your readers to recognize your newsletter. E.g. '[SM Newsletter] Nr. 297, 16.10.2007 — Usability Glossary — Splash Pages — Big Typography'. Remain consistent. Otherwise your readers might consider your e-mails as spam and report it.
5.  **Always insert the current date in the content.** A correct date which indicates when the newsletter was sent is more important than you probably think it is. If the date isn't mentioned or is provided incorrectly, the newsletter is given spam score points.
6.  **HTML is OK, but only if MIME-Multipart is used.** When sending newsletters as HTML make sure that also the plain text version is attached. Messages sent in MIME-Multipart-Format are automatically sent in a way that subscribers without active HTML-Viewer still get a decently formatted e-mail. It is important that both plain text and the HTML-version have the same or very similar content. The percentage of text should be higher than the percentage of HTML or images. Keep your message size between 20 and 40 Kb.
7.  **Use CSS sparingly.** In most cases it is better to use inline CSS-styling in HTML instead of referring to CSS-file in HTML. However, referring to external CSS-files is better than sending them with newsletter.
8.  **Avoid graphics and complex HTML-elements.** Spam-filters consider a number issues related to HTML. For instance, if the newsletter has too many closed tags, too many graphic (images) or structural (tables) elements it gets just as many spam score points. Besides, many readers use software (e.g. Outlook) which automatically blocks images; if users don't understand what the mail is about they'll report is as spam. Complex HTML (particularly if more than 50% of HTML-code are HTML-tags) is generously awarded with many spam score points — keep it simple. Colorful backgrounds, tables, JavaScripts and web forms shouldn't be in newsletters.
9.  **Motivate your users to add you to their whitelists.** To ensure the bulletproof e-mail-delivery ask your readers to add you to whitelists. You can [create Email whitelist instructions in seconds](https://www.keywebdata.com/?page_id=28) — for a number of e-mail applications.
10.  **Screen your advertisers and partners.** If your newsletter includes a link to a blacklisted web site you might get a whole bunch of spam score points. Verify the sites and e-mails you are linking to; check if they are already blacklisted or were reported as spam (or spam sources) before placing their advertisements in your newsletter. Even if the company is legitimate, it is possible that spammers have used their accounts for sending out spam mails.
11.  **Monitor new subscribers.** Monitor new subscribers in your lists. Set suspicious "spamflag" addresses such as "abuse@", "nospam@", "postmaster@", "marketerspam@" as inactive subscribers. [Source]
12.  **Verify your subscribers with signup confirmation.** Always make your mailing lists double opt-in. This means that when a user subscribes to your mailing list, they will be sent an email with a link that they must click on to confirm their subscription. This is very important because many people can accidentally enter an incorrect email address, or even the email address of someone else on purpose. When that person receives a newsletter they did not subscribe to, they will assume they have been spammed, and your newsletter (and possibly your web server) will be reported as spam.It also keeps invalid email addresses off of your list, which reduces the volume and percentage of undeliverable messages that you send. Since undeliverable rates also factor into filtering rules, keeping invalid email addresses from being subscribed to your list will help you to avoid content filtering. [[Source](https://www.aweber.com/blog/email-deliverability/isp-content-filtering.htm)]
13.  **Test your newsletters before sending them out.** Always check the "spam score" of your newsletters with [SpamCheck](https://spamcheck.sitesell.com) and further tools (most of them are listed below).

