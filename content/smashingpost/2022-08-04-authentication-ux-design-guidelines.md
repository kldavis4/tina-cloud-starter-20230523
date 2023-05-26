---
title: 'Rethinking Authentication UX'
slug: authentication-ux-design-guidelines
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb887d40-c454-4b48-be73-44e903492deb/magic-links-authentication.jpg
date: 2022-08-04T13:30:00.000Z
summary: >-
  Nobody wakes up in the morning hoping to finally identify crosswalks and fire hydrants that day. Yet every day, we prompt users through hoops and loops to sign up and log in. Let’s fix that.
description: >-
  How to improve authentication UX, with magic links, 2FA, better password recovery and relaxed rules for secure, accessible and usable passwords.
categories:
  - Authentication
  - Usability
  - Design Patterns
  - UX
disable_panels: true
---

**Authentication** is a tricky subject. There are so many terms floating around us, from **2FA to MFA to OTP** — and it might be difficult to make sense of what we need and when we need it. But authentication is everywhere, and sometimes it’s extremely frustrating, and sometimes it’s seamless. Let’s explore a few patterns to create experience that are a bit more seamless than frustrating.

Now, nobody wakes up in the morning hoping to *finally* identify **crosswalks and fire hydrants** that day. Yet every day, we prompt users through hoops and loops to sign up and log in, to set a complex enough password or recover one, to find a way to restore access to locked accounts and logged-out sessions.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e68f8fc-3edf-4a14-a03a-f5b64ecbd971/2-authentication-ux.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e68f8fc-3edf-4a14-a03a-f5b64ecbd971/2-authentication-ux.jpeg" width="800" height="563" sizes="100vw" caption="Because CAPTCHAs don’t work any longer, we have to solve tasks that are difficult enough for machines. That’s not user-friendly but secure. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e68f8fc-3edf-4a14-a03a-f5b64ecbd971/2-authentication-ux.jpeg'>Large preview</a>)" alt="Examples of CAPTCHAs" >}}

Of course **security matters**, yet too often, it gets in the way of usability. As Jared Spool [said once](https://www.youtube.com/watch?v=Jxwgoy4Itxw), “If a product isn’t usable, it’s also not secure.” That’s when people start using private email accounts and put passwords on stick-it-notes because they forget them. As usual, Jared hits the nail on the head here. So what can we do to improve the **authentication UX**?

<p style="background-color: #e8f5ff;
border: 1px solid #dbeaff; border-radius: 11px; padding: 1.35rem 1.65rem;">This article is part of our ongoing series on <a href="/category/design-patterns">design patterns</a>. It’s also a part of the upcoming <a style="font-weight: bold" href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-ux/">4-weeks live UX training</a>&nbsp;🍣 and will be in our recently released <a href="https://smart-interface-design-patterns.com/">video course</a> soon.</p>

## 1. Don’t Disable Copy-Paste For Passwords

It appears only reasonable to block copy-paste for password input to avoid brute-force attacks. Yet when we do so, we also block users who copy-paste passwords from **password managers** and text documents. As a result, they need to repeatedly retype complex, lengthy, cryptic strings of text — and it’s rarely an exciting adventure to embark on.

In fact, that’s slow, annoying and frustrating. In her talk on [Authentication UX Anti-Patterns](https://youtu.be/u9j7_KuqJdg?t=238), Kelly Robinson explains that this is a common **anti-pattern**, often causing way more frustration than remedy, and hence best to be avoided.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78bcc76c-c07c-454b-b4c0-bfbdc80093ad/6-authentication-ux.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78bcc76c-c07c-454b-b4c0-bfbdc80093ad/6-authentication-ux.jpeg" width="800" height="233" sizes="100vw" caption="We can make it easier for people to use secure passwords, rather than coming up with one on spot. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78bcc76c-c07c-454b-b4c0-bfbdc80093ad/6-authentication-ux.jpeg'>Large preview</a>)" alt="An example of autocomplete with a secure auto-generated password on the left and html with the attribute autocomplete='new-password' on the right" >}}

Also, double check that your password fields include the attribute `autocomplete="new-password"`, so browsers can prompt a **strong auto-generated password**. And the best bit: users without password managers don’t have to come with a password of their own — because usually that’s a recipe for disaster.

## 2. Don’t Rely on Passwords Alone

[Passwords are problematic](https://www.security.org/digital-safety/password-manager-annual-report/). For example, only [34% of users in the US](https://bitwarden.com/resources/world-password-day/) use a password manager, and everybody else relies on their good ol’ memory, sticky notes, and text files on the desktop.

**Good passwords are hard to remember**. As a result, users often choose easy-to-guess passwords instead, including [names of their pets and loved ones](https://www.blog.google/technology/safety-security/password-checkup/), their birthdates, and their wedding dates. That’s far from secure, of course.

{{< rimg breakout="true" href="https://www.blog.google/technology/safety-security/password-checkup/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea4b37b-6e39-4664-8ecf-5a0764cc864e/4-authentication-ux.jpeg" width="800" height="462" sizes="100vw" caption="<a href='https://www.blog.google/technology/safety-security/password-checkup/'>The state of passwords</a> doesn’t look very promising. If we could avoid passwords only, we should. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea4b37b-6e39-4664-8ecf-5a0764cc864e/4-authentication-ux.jpeg'>Large preview</a>)" alt="Visualization of Google's survey of a nationally representative sample of U.S. adults to understand beliefs and behaviors around passwords and online security" >}}

Still, we often **forget our passwords**, sometimes recovering passwords 4-5 times a week. So no wonder many of us still reuse the same password across multiple accounts, often favoring convenience over data safety. In fact, allowing users to choose their own passwords is a recipe for trouble. To fix that, what if we **nudge users away from passwords**?

Any kind of [2-Factor Authentication](https://authy.com/what-is-2fa/) is better than passwords, and ideally, we could use a cookie that users can opt-in for to avoid frequent log-ins. Data-sensitive sites might want to log out users automatically after every visit (e..g online banking), but simpler sites might be better off **avoiding aggressive log-outs** and allowing users to stay logged in for 30 days or even longer.

{{% feature-panel %}}

## 3. Drop Strict Password Requirements

Since users are very good at **twisting and bending password rules** (just to forget them shortly after the task is done), what if we change our strategy altogether? What if we do support lengthy and complex passwords with all the special characters unique delimeters but keep rules relatively friendly?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/111edd3e-76c0-4521-8beb-0bf7ac73e42b/7-authentication-ux.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/111edd3e-76c0-4521-8beb-0bf7ac73e42b/7-authentication-ux.jpeg" width="800" height="" sizes="100vw" caption="<a href='https://login.mailchimp.com/signup/'>Mailchimp</a> with very simple password rules. Most password managers &mdash; in-browser and external ones &mdash; would easily meet them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/111edd3e-76c0-4521-8beb-0bf7ac73e42b/7-authentication-ux.jpeg'>Large preview</a>)" alt="A screenshot of Mailchimp password rules" >}}

This surely would come at the cost of security, of course. So to protect user’s data on their behalf, we use `new-password` to prompt secure passwords to be generated during sign-up, and nudge users aggressively towards a 2FA setup, e.g., providing **30% off for the first month for turning 2FA on**.

The only thing required would be to connect the account with a **mobile phone** or Google Authenticator, type in a verification code, or verify with a Touch-ID, and that would be it. Thus, we avoid [endless and expensive password resets](https://bioconnect.com/2021/12/08/are-password-resets-costing-your-company/), which often cause abandonment and frustration.

## 4. Social Sign-In Isn’t For Everyone

The more sensitive the data stored, the more attention users expect from the interface to security. Usability sessions hint that **log-in hurdles** seem to be accepted as long as they are considered to be *“reasonable”*. But what’s reasonable to us, as designers, isn’t necessarily what’s reasonable to our customers.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f5d95b6-2293-4531-83e8-8a202bbf8618/1-authentication-ux.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f5d95b6-2293-4531-83e8-8a202bbf8618/1-authentication-ux.jpeg" width="800" height="" sizes="100vw" caption="We can highlight previously used option to make it easier for customers to find out what they’ve signed up with last time. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f5d95b6-2293-4531-83e8-8a202bbf8618/1-authentication-ux.jpeg'>Large preview</a>)" alt="A screenshot with a highlighted previously used option of sign-in" >}}

**Social sign-in** is a good example of that. Some users love it because it’s so fast, yet others are generally opposed to it due to **privacy concerns**. Plus, we need to comply with GDPR, CCPA, and similar legislation when using them.

Also, remember that some **users forget what they signed up with last time**, so it’s a good idea to indicate their previous choice based on their previous log-in (as illustrated above). Essentially, social sign-in is a great option for people who just want to get things done, but it can’t be the only option that we provide.

{{% ad-panel-leaderboard %}}

## 5. Replace Security Questions With 2FA

In an ideal world, security questions &mdash; like the ones we are being asked by a bank on the phone to verify our identity &mdash; should help us prevent fraud. Essentially, it’s a second layer of protection, but it **performs remarkably poorly** both in terms of usability and security. Questions about favorite pets, maiden names, and the first school can easily be discovered by scrolling a Facebook stream long enough.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135f0158-e531-4689-83fa-bd3c189a01de/5-authentication-ux.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135f0158-e531-4689-83fa-bd3c189a01de/5-authentication-ux.jpg" width="800" height="562" sizes="100vw" caption="<a href='https://mcusercontent.com/16b832d9ad4b28edf261f34df/images/aeef7b17-cd58-80ec-092c-f2801835d867.jpg'>PayPal</a> still uses security questions to verify user’s identity. This isn’t particularly user-friendly or secure. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135f0158-e531-4689-83fa-bd3c189a01de/5-authentication-ux.jpg'>Large preview</a>)" alt="Examples of PayPal’s Security questions" >}}

Knowing that, users sometimes reply to these questions with the **very same answer** (e.g., their birthday or a location of birth) and sometimes even use the same password that they’ve entered initially. This isn’t really helping anybody. Magic links and push notifications are much more secure, and there is no need to memorize the answers at all.


## 6. Users Need Options For Access Recovery

Nothing can be more frustrating than being **locked out** at just the wrong moment. As designers, we can pave deliberate ways out in our interfaces with multiple alternate ways to restore access (**access recovery stacks**) and avoid these issues for good.

We often think of **password recovery** to help users restore their access, but perhaps thinking about *recovering access* is a better perspective to look at the issue. If a user can’t log in at a given moment, they aren’t really interested in defining a brand new secure password, or finding an email or special characters that they haven’t used before. They just need to log in. And we need to help them do just that.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb887d40-c454-4b48-be73-44e903492deb/magic-links-authentication.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb887d40-c454-4b48-be73-44e903492deb/magic-links-authentication.jpg" width="800" height="509" sizes="60vw" caption="<a href='https://mcusercontent.com/16b832d9ad4b28edf261f34df/images/24daa7ec-c7b5-f0cb-914d-8dba5def4846.jpg'>Magic links</a> are fantastic to recover access, but sometimes users might not have access to their email. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb887d40-c454-4b48-be73-44e903492deb/magic-links-authentication.jpg'>Large preview</a>)" alt="A screenshot with a 'Send magic link' button" >}}

Of all the techniques for access recovery, surely, [magic links](https://workos.com/blog/a-guide-to-magic-links) will be a part of the access recovery stack. Users seem to appreciate just how fast they can get back in once they are locked out. Usually they **work flawlessly** unless the email doesn’t arrive, or the account is linked to an outdated email, or the email inbox or phone aren’t available.

Still, to use magic links, users need to **switch context**, jumping from browser to the mail client and then back to the browser. It might have been faster to prompt users to type in a code on their phone to get in instead. One way or the other, to avoid lock-outs, we **provide multiple options** to guarantee a speedy recovery, and a mix of options works best:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f47188-9295-494f-bf55-f5d5a335dd9c/password-access-recovery-authentication-ux-default.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f47188-9295-494f-bf55-f5d5a335dd9c/password-access-recovery-authentication-ux-default.jpg" width="764" height="485" sizes="100vw" caption="We need to help users recover access quickly. To be resilient, we can use an entire access recovery stack. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f47188-9295-494f-bf55-f5d5a335dd9c/password-access-recovery-authentication-ux-default.jpg'>Large preview</a>)" alt="A screenshot with a 'Send magic link' button" >}}

1. **Send a magic link for log-in via email**.  
Don’t require users to retype a password, or set a new one. Users might not have access to email, or it could be hacked.

2. **Send a magic link for log-in to a secondary email**.  
Unfortunately, the secondary email is often outdated, or the user might have no access to it.

3. **Send an SMS verification URL/code to a mobile phone**.  
This option won’t work for users who have purchased a new phone, or don’t have access to their SIM-card (e.g. when travelling abroad).

4. **Send a push notification via OTP/2FA**.  
This option won’t work for users who have purchased a new phone and haven’t set up [OTP](https://www.cm.com/glossary/what-is-one-time-password/)/2FA just yet, or don’t have access to their old phone.

5. **Biometric authentication via a dedicated app/Yubikey**.  
This option won’t work for users who don’t have an OTP/2FA setup yet, or have purchased a new phone/Yubikey.

6. **Type backup recovery codes**.  
Not every user will have backup recovery codes nearby, but if they do, they should always override account lock-out. Sometimes backup recovery codes are sent via a postal service, but they could be lost/stolen.

7. **Phone call verification**.  
Users could be called on their (new) phone, and they’d need to answer a few questions to verify their idemtity. Ideally, it would be something that *they know* (e.g. latest transactions), something that *they have* (e.g. credit card) and something that *they are* (e.g. face recognition via a video call).

8. **Customer support inquiry**.  
Ideally, users could restore access by speaking to an agent via live chat, WhatsApp/Telegram, video call or email (which is usually the slowest).

It’s **not a good idea** to send randomly generated passwords via email and require a new password setup when a user finally manages to log in. That’s not secure, and it’s always a hassle. Instead, yet again, nudge users towards a [2FA](https://authy.com/what-is-2fa/) setup, so they can recover access by accessing a code from the app installed on their phone or SMS (which is [less secure](https://www.enisa.europa.eu/news/enisa-news/beware-of-the-sim-swapping-fraud), however.)

{{% ad-panel-leaderboard %}}

## Wrapping Up

**Authentication is always a hurdle**. Yet when the interface is difficult to deal with, users become remarkably creative in bending the rules to make it work and forget the password the moment they complete a transaction.

Perhaps we should give our users at least a chance to get to know our website or app before creating too many barriers for them. Ideally, we need a 2FA setup for everyone, but we need to get there first. And a path there is paved with a **seamless, good authentication UX** &mdash; without complicated rules and restrictions, and preferably the one that users won’t even notice.

## Meet “Smart Interface Design Patterns”

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Design patterns and guidelines on everything from mega-dropdowns to complex enterprise tables &mdash; with 5 new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 1rem"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin-top: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.</p>


### Useful Resources

- [The Current State of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)  
A great article by Drew Thomas on many ways to reliably authenticate users – not just passwords. 
- [Sign-In Best Practices](https://web.dev/sign-in-form-best-practices/)  
A thorough overview of cross-platform browser features to build sign-in forms that are secure, accessible and easy to use, by Sam Dutton.
- [Fixing the Failures of Authentication](https://www.youtube.com/watch?v=Jxwgoy4Itxw) by Jared Spool  
A very insightful talk about the various hurdles we put our users through when we make authentication more difficult than it should be.
- [App login design: Choosing the right user login option for your app](https://uxmag.com/articles/app-login-design-choosing-the-right-user-login-option-for-your-app)  
An article by Joseph Russell on how to decide on your app’s login method, with some options and the pros and cons of each.
- [Passwordless Authentication Methods for SaaS Web Applications](https://www.uxmatters.com/mt/archives/2022/02/passwordless-authentication-methods-for-saas-web-applications.php)  
Perhaps we don’t need passwords after all. Armantas Zvirgzdas is looking at what we can do to nudge users away from passwords towards authentication methods that don’t require passwords.

### Related Articles

If you find this article useful, here’s an overview of **similar articles** we’ve published over the years &mdash; and a few more are coming your way.

- [Designing Effective Pricing Plans UX](https://www.smashingmagazine.com/2022/07/designing-better-pricing-page/)
- [Designing A Perfect Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Designing Perfect Breadcrumbs](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/)
- [Designing A Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Perfect Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Perfect Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Designing A Perfect Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Designing A Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)
- “[Form Design Patterns Book](https://www.smashingmagazine.com/printed-books/form-design-patterns/),” written by Adam Silver

{{< signature "yk" >}}
