---
title: 'Breaking The Rules: A UX Case Study'
slug: breaking-the-rules-a-ux-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/573d7c2c-0cb2-41ab-ba85-80c71757a7d5/rules1.jpg
date: 2011-08-17T13:00:59.000Z
author: laura-klein
summary: >-
  Design guidelines aren’t one size fits all. Find how sometimes you can improve a process by breaking a few rules.
description: >-
  Design guidelines aren’t one size fits all. Find how sometimes you can improve a process by breaking a few rules.
categories:
  - UX
  - Usability
  - UX
  - Case Studies
---

I read a lot of design articles about best practices for improving the flow of sign-up forms. Most of these articles offer great advice, such as minimizing the number of steps, asking for as little information up front as possible, and providing clear feedback on the status of the user’s data.

If you’re creating a sign-up form, you could do worse than to follow all of these guidelines. On the other hand, you could do a lot better. Design guidelines aren’t one size fits all. Sometimes you can improve a process by breaking a few rules. The trick is knowing which rules to break for a particular project.

{{% feature-panel %}}

Recently, I did a project for <a href="https://www.outright.com">Outright</a>, a product aimed at simplifying accounting and tax preparation for small businesses. The product automates accounting tasks for sole proprietors and online product sellers so that they don’t have to do things like categorize receipts and generate profit and loss reports.

<figure><a href="https://www.smashingmagazine.com/2011/08/17/breaking-the-rules-a-ux-case-study/"><img loading="lazy" decoding="async" class="107221" title="Break the Rules" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/573d7c2c-0cb2-41ab-ba85-80c71757a7d5/rules1.jpg" alt="" width="500" height="350" /></a><figcaption>Image credit: <a href="https://www.beforethecoffee.com">Ferrell McCollough.</figcaption></figure>

To get the most value out of the product, new users have to hook up one or more of their own accounts, so that their business finances can be automated.

### The Original Design Rules

When first designing its user set-up process, *Outright* followed some very reasonable design rules:

*   It kept the process to one page in order to reduce the number of steps users had to go through.
*   It allowed new users to easily quit the set-up process, so that they could explore the interface before committing.
*   It provided constant feedback about the status of each account as it was being updated.

Then we did a redesign, broke every single one of those rules and decreased the cancellation rate by 20%.

Why did breaking those rules help in this particular case? Let’s look at them one at a time.

## Rule #1: Reduce The Number Of Screens In The Set-Up Process

This rule is normally great, because requiring a lot of unnecessary clicks just slows the user down as they try to sign up for your product. But in some cases, combining too many different concepts onto one screen can complicate things.

In the old version of the application, the user saw only one search box, in which they could enter the name of a bank, a credit card or one of several e-commerce partners, such as eBay.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53dfd926-d37e-4cdf-af58-88fd5efcd931/old-step-1-cropped1.png"><img class="106902" title="Old Add Account" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53dfd926-d37e-4cdf-af58-88fd5efcd931/old-step-1-cropped1.png" alt="Original Add Account Screen" width="550" height="290" /></a><figcaption>Putting everything on one screen can be overwhelming.</figcaption></figure>

During the preliminary user research, we found that this was a little overwhelming for new users. It made them wonder which piece of information they should add first. There was occasionally a rather dramatic pause as they tried to process what was being asked of them.

By breaking the process down into three explicit steps, we freed users from having to decide which information to input at any point. This made the whole process seem much simpler, because users always knew what was expected of them.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3986cba-00c3-4552-9e05-b79e9ac26463/step-2-cropped.png"><img class="106903" title="New Add Account" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3986cba-00c3-4552-9e05-b79e9ac26463/step-2-cropped.png" alt="The Updated Version of the Add Account Screen" width="550" height="238" /></a><figcaption>Keeping each screen focused reduced confusion.</figcaption></figure>

Of course, we have not required users to input something at every step. They can skip ahead if, for example, they don’t have a business credit card. But still, the only decision they ever have to make is whether to enter the requested information.

**When to break rule #1:** Adding steps can simplify the experience, if it makes each individual step very clear.

{{% ad-panel-leaderboard %}}

## Rule #2: Allow Users To Test Drive Before Making Them Submit Data

For many products, allowing users to play around before entering any information is a great tactic.

Think of <a href="https://www.yelp.com/">Yelp</a>. I must have read hundreds of reviews before getting around to reviewing anything myself. The same goes for online shopping; I’ll often visit a website several times before making a purchase.

But other products don’t make much sense without personalized content. Social networks, for example, are significantly more useful once you connect with friends on them.

This is certainly true with Outright. The experience for users who plug into a financial data source is so much better than for users who don’t. Letting people test drive the product before importing their account information simply doesn’t make sense. Users won’t understand the value of the product until they see and manipulate their own data.

**When to break rule #2:** While letting people explore before committing can be useful for some types of products, assess whether your product can be fully understood without personalized content.

## Rule #3: Always Provide Feedback On Status

Don’t you hate it when you’re trying to import or export data and you don’t get any feedback on how long it will take or whether any errors have occurred? Everyone does. That’s why Outright kept users informed as their data was being imported.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ea3f4c6-fc98-49e6-971e-6e5901d66a2e/old-final-cropped1.png"><img class="106904" title="Old Final Screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ea3f4c6-fc98-49e6-971e-6e5901d66a2e/old-final-cropped1.png" alt="The Original Final Screen" width="550" height="227" /></a><figcaption>Providing too much feedback caused confusion.</figcaption></figure>

The problem was, when users imported data from more than one account, the status messages started cluttering up the screen. This distracted them from adding more accounts.

Now, instead of showing constant feedback about the status of each data import, we simply let users know that they have successfully connected to their data source and then move them on. If there are errors, we provide a place at the end of the process for the user to recover.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c67f4b0-e0b4-4c01-bdf2-58c4a7d8b018/success.png"><img class="106905" title="Updated Success Screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c67f4b0-e0b4-4c01-bdf2-58c4a7d8b018/success.png" alt="Updated Success Screen" width="550" height="173" /></a><figcaption>Giving just enough feedback helps users move on.</figcaption></figure>

**When to break rule #3:** Feedback is often good, but too much can overwhelm users, especially if it distracts them from moving on to the next task. If the user can’t do anything with the feedback or if moving on is more important, consider not giving constant status updates.

## Rules That We Did Follow

Of course, we didn’t break every rule. Rules exist for a reason. We followed a lot of best practices, with great results. For example:

*   We made sure to have a single, clear, primary call to action for each screen, so that users always know what they’re supposed to do.
*   We kept each screen focused on a single task.
*   We made sure that users always know which step of the process they’re on and how many more they have left to go.

I’d love to be able to say that breaking certain rules and following certain others will improve the sign-up flow of your product, but design isn’t like that. You need to figure out which rules apply to your product and users. And once you’ve figured that out, don’t be afraid to break a few of the ones that don’t apply, just to see if that makes things better.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [10 Useful Usability Findings and Guidelines](https://www.smashingmagazine.com/2009/09/10-useful-usability-findings-and-guidelines/)
*   [30 Usability Issues To Be Aware Of](https://www.smashingmagazine.com/2007/10/30-usability-issues-to-be-aware-of/)
*   [10 Useful Usability Findings and Guidelines](https://www.smashingmagazine.com/2009/09/10-useful-usability-findings-and-guidelines/)
*   [10 Principles Of Effective Web Design](https://www.smashingmagazine.com/2008/01/10-principles-of-effective-web-design/)

{{< signature "al, mrn" >}}
