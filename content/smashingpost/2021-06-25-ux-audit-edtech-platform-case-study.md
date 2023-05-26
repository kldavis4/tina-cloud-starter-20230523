---
title: 'How To Run A UX Audit For A Major EdTech Platform (Case Study)'
slug: ux-audit-edtech-platform-case-study
author: mark-lankmilier
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5116c31-3d66-47b0-aa81-1a6759c68b92/ux-audit-edtech-platform-case-study.jpg
date: 2021-06-25T10:00:00.000Z
summary: >-
  This article is a case study of how a UX audit affects a UI. It explains how a famous educational platform can be analyzed <a href="https://www.edx.org/">edX</a> against Jakob Nielsen’s <a href="https://www.nngroup.com/articles/ten-usability-heuristics/">usability guidelines</a>. To get started, Mark Lankmiller shares all of the criteria and metrics he used for his UX audit.
description: >-
  This article is a case study of how a UX audit affects a UI. It explains how a famous educational platform can be analyzed <a href="https://www.edx.org/">edX</a> against Jakob Nielsen’s <a href="https://www.nngroup.com/articles/ten-usability-heuristics/">usability guidelines</a>. To get started, Mark Lankmiller shares all of the criteria and metrics he used for his UX audit.
categories:
  - Case Studies
  - User Experience
  - Product Strategy
---

The business world today is obsessed with user experience (UX) design. And for good reason: [Every dollar invested in UX brings $100 in return](https://www.forbes.com/sites/forbestechcouncil/2017/01/23/how-ux-is-transforming-business-whether-you-want-it-to-or-not/?sh=f938047580e6). So, having some free time in quarantine, I decided to check whether one of the [most evolving industries right now, education technology](https://www.eu-startups.com/2020/09/how-has-the-pandemic-changed-the-face-of-edtech/) (EdTech), uses this potential of UX.

My plan was to choose one EdTech platform, audit its UX, and, if necessary, redesign it. I first looked at some major EdTech platforms (such as edX, Khan Academy, and Udemy), read user feedback about them, and then narrowed my scope to [edX](https://www.edx.org/). Why did I choose edX? Simply because:

- it’s non-profit,
- it has more than 20 million users,
- its UX has a lot of [negative reviews](https://www.trustpilot.com/review/www.edx.org).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8161ba6a-6292-4e4f-94d6-aab636f73f5a/edx-reviews-on-trustpilot.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8161ba6a-6292-4e4f-94d6-aab636f73f5a/edx-reviews-on-trustpilot.jpg" width="800" height="631" sizes="100vw" caption="edX reviews on TrustPilot (<a href=’https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8161ba6a-6292-4e4f-94d6-aab636f73f5a/edx-reviews-on-trustpilot.jpg’>Large preview</a>)" alt="" >}}

Even from my quick UX check, I got an overview of the UX principles and UI solutions followed by global EdTech platforms right now (in my case, edX).

Overall, this UX audit and redesign concept would be of great use to UX designers, business owners, and marketing people because it presents a way to audit and fix a product’s most obvious usability issues. So, welcome to my edX audit.

{{% feature-panel %}}

## Audit Structure

- <a href="#part-1">Part 1</a>: Audit for user needs
- <a href="#part-2">Part 2</a>: Audit for [10 usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)

This audit consists of two parts. First, I surveyed edX users, learned their needs, and checked whether the platform meets them. In the second stage, I weighed edX’s website against the [10 usability heuristics identified by Jacob Nielsen](https://www.nngroup.com/articles/ten-usability-heuristics/). These heuristics are well-recognized UX guidelines &mdash; the bible, if you will, for any UX designer.

Ideally, a full-fledged UX audit would take weeks. I had a fixed scope, so I checked the platform’s **home page, user profile, and search page**. These are the most important pages for users. Just analyzing these few pages gave me more than enough insight for my redesign concept.

## Part 1: Audit for User Needs

Good UX translates into satisfied users.

That’s where I started: identifying user needs. First, I analyzed statistical data about the platform. For this, you can use such well-known tools as [Semrush](https://www.semrush.com/dashboard/) and [SimilarWeb](https://www.similarweb.com/) and reviews from [Trustpilot](https://www.trustpilot.com/), [Google Play](https://play.google.com/store), and Apple’s [App Store](https://www.apple.com/app-store/).

Take SimilarWeb. The [tool analyzes edX’s](https://www.similarweb.com/website/edx.org) rank, traffic sources, advertising, and audience interests. “Computer Electronics” and “Technology” appear to be the most popular course categories among edX students.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ce81ac6-45aa-4f09-b7e7-8e3207669178/similarweb-analytics-about-edx-platform.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ce81ac6-45aa-4f09-b7e7-8e3207669178/similarweb-analytics-about-edx-platform.png" width="800" height="471" sizes="100vw" caption="<a href='https://www.similarweb.com/website/edx.org'>SimilarWeb</a> analytics for the edX platform (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ce81ac6-45aa-4f09-b7e7-8e3207669178/similarweb-analytics-about-edx-platform.png'>Large preview</a>)" alt="" >}}

For user feedback on edX, I went to Trustpilot (Google Play and the App Store are relevant only for analyzing mobile apps). I found that most users praise edX’s courses for their useful content, but complain about the platform’s UX &mdash; most often about the hard and time-consuming verification process and poor customer support.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df4e3b9a-d1cb-4ff5-9fff-50b9d80fc322/edx-user-review-on-trustpilot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df4e3b9a-d1cb-4ff5-9fff-50b9d80fc322/edx-user-review-on-trustpilot.png" width="800" height="429" sizes="100vw" caption="edX user review on Trustpilot (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df4e3b9a-d1cb-4ff5-9fff-50b9d80fc322/edx-user-review-on-trustpilot.png'>Large preview</a>)" alt="" >}}

Done with the analytical check, I moved on to user interviews. I went to design communities on Facebook and LinkedIn, looking for students of online courses, asking them to answer some of my quick questions. To everyone who responded, I sent a [simple Google Form](https://docs.google.com/forms/d/e/1FAIpQLSdHiA75LV7RV0f8PwFUMF9p3HTS8U1nyzXxD-i13IW6_4QsXw/viewform?usp=sf_link) to capture their basic needs and what they value most when choosing an education platform.

Having received the answers, I created two user profiles for edX: potential user and long-time user. Here’s a quick illustration of these two types:  

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60ab2992-0fe6-4d02-8ddd-327771f30728/1st-user-profile-for-edx.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60ab2992-0fe6-4d02-8ddd-327771f30728/1st-user-profile-for-edx.png" width="800" height="230" sizes="100vw" caption="Two user profiles for edX (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60ab2992-0fe6-4d02-8ddd-327771f30728/1st-user-profile-for-edx.png'>Large preview</a>)" alt="" >}}

I identified these two kinds of users based on my survey. According to my findings, there are two common scenarios for how users select an educational course.

Learner 1 is mainly focused on choosing between different education platforms. This user type doesn’t need a specific course. They are visiting various websites, looking for a course that grabs their attention.

The second kind of learner knows exactly what course they want to take. Supposing they’ve chosen edX, they would need an effective search function to help them locate the course they need, and they’d need a convenient profile page to keep track of their progress.

Based on the edX user profiles, their needs, and the statistical data I gathered, I have outlined the five most common problems that the platform’s customers might face.

### Problem 1: “Can I Trust This Website?”

Numerous factors determine a website’s credibility and trustworthiness: the logo, reviews, feedback, displayed prices, etc. [Nielsen Norman Group covers the theory](https://www.nngroup.com/reports/ecommerce-ux-trust-and-credibility/) of it. Let’s focus on the practice.

So, what do we have here? edX’s current home page displays the logos of its university partners, which are visible at first glance and add credibility to the platform.

At the same time, the home page doesn’t highlight benefits of the platform or user feedback. This is often a deciding factor for users in choosing a platform.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64f5d09a-6833-46df-bf74-a5eec95d3584/edx-homepage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64f5d09a-6833-46df-bf74-a5eec95d3584/edx-homepage.png" width="800" height="689" sizes="100vw" caption="<a href='https://www.edx.org/'>edX</a> home page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64f5d09a-6833-46df-bf74-a5eec95d3584/edx-homepage.png'>Large preview</a>)" alt="" >}}

#### Other approaches

It’s good to learn from competitors. Another EdTech platform, [Khan Academy](https://www.khanacademy.org/), demonstrates quite a different approach to website design. Its home page introduces the platform, talks about its benefits, and shows user feedback:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1525b8-41b6-4211-9cbf-9dc505284985/screens-of-khan-academy-homepage.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1525b8-41b6-4211-9cbf-9dc505284985/screens-of-khan-academy-homepage.jpg" width="800" height="423" sizes="100vw" caption="Screens of <a href='https://www.khanacademy.org/'>Khan Academy</a> home page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1525b8-41b6-4211-9cbf-9dc505284985/screens-of-khan-academy-homepage.jpg'>Large preview</a>)" alt="" >}}

### Problem 2: “Do I Have All of the Information I Need to Choose a Course?

Many a time, users just want to quickly scan the list of courses and then choose the best one based on the description.

edX’s course cards display the course name, institution, and certificate level. Yet, they could also provide essentials such as pricing, course rating, how many students are enrolled, start date, etc.

Proper description of elements is an essential part of UX, as mentioned in [Jacob Nielsen’s sixth heuristic](https://www.nngroup.com/articles/recognition-and-recall/). The heuristic states that all information valuable to a user should always be available.

#### Other approaches

Looking at another EdTech platform, [Udemy](https://www.udemy.com/)’s course cards display the course name, instructor, rating, number of reviews, and price.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c22fbadc-9a53-454d-b76a-470aae4dcefd/edx-course-cards-udemy-course-cards.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c22fbadc-9a53-454d-b76a-470aae4dcefd/edx-course-cards-udemy-course-cards.jpg" width="800" height="620" sizes="100vw" caption="edX and Udemy course cards (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c22fbadc-9a53-454d-b76a-470aae4dcefd/edx-course-cards-udemy-course-cards.jpg'>Large preview</a>)" alt="" >}}

### Problem 3: “Can I Sign Up Easily?”

According to a [study by Mirjam Seckler](https://research.google/pubs/pub42513/), completion time decreases significantly if a signup form follows basic usability guidelines. Users are almost twice as likely to sign up in their first try if there are no errors.

So, let’s have a deeper look at edX’s forms:

1. They do not let you type your country’s name or your date of birth. Instead, you have to scroll through all of the options. (I am in the Ukraine, which is pretty far down the list.)
2. They do not display the password you’ve inputted, even by request.
3. They do not send an email to verify the address you’ve entered.
4. They do not indicate with an asterisk which fields are required.

Speeding up the registration process is yet another crucial UX principle. To read more about it, look at Nielsen Norman Group’s [usability guidelines for website forms](https://www.nngroup.com/articles/web-form-design/).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c96cdf1f-b9d2-492e-9c43-60230c0cd357/screens-of-edx-signup-image1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c96cdf1f-b9d2-492e-9c43-60230c0cd357/screens-of-edx-signup-image1.png" width="800" height="650" sizes="100vw" caption="Screens of edX’s signup (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c96cdf1f-b9d2-492e-9c43-60230c0cd357/screens-of-edx-signup-image1.png'>Large preview</a>)" alt="Screens of edX’s signup" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffac591-cf40-4e81-b244-c81d964365b4/screens-of-edx-signup-image2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffac591-cf40-4e81-b244-c81d964365b4/screens-of-edx-signup-image2.png" width="800" height="410" sizes="100vw" caption="Screens of edX’s signup (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffac591-cf40-4e81-b244-c81d964365b4/screens-of-edx-signup-image2.png'>Large preview</a>)" alt="Screens of edX’s signup" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/486e3df6-e143-46c5-83b8-cd94b40751d3/screens-of-edx-signup-image-3.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/486e3df6-e143-46c5-83b8-cd94b40751d3/screens-of-edx-signup-image-3.jpg" width="800" height="" sizes="100vw" caption="Screens of edX’s signup (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/486e3df6-e143-46c5-83b8-cd94b40751d3/screens-of-edx-signup-image-3.jpg'>Large preview</a>)" alt="Screens of edX’s signup" >}}

#### Other approaches

Many websites let users enter data manually to speed up the application process. Another EdTech website, [Udemy](https://www.udemy.com/), has an option to show and hide the inputted password by request:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a7997bb-4409-41ca-a6ca-ffe70d31182e/udemy-signup.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a7997bb-4409-41ca-a6ca-ffe70d31182e/udemy-signup.png" width="800" height="324" sizes="100vw" caption="Udemy’s signup (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a7997bb-4409-41ca-a6ca-ffe70d31182e/udemy-signup.png'>Large preview</a>)" alt="Udemy’s signup" >}}

### Problem 4: “Is On-Site Search Helpful?”

Search is one of the most used website features. Thus, it should be helpful, simple to use, and fast. [Numerous usability studies](https://www.nngroup.com/articles/intranet-usability-the-trillion-dollar-question/) show the importance of helpful search for massive online open courses (MOOCs).

In this regard, I’ve analyzed edX’s search. I started from page loading. Below is a screenshot from [Google PageSpeed](https://developers.google.com/speed), which shows that the platform’s search speed has a grade of 12 out of 100.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db316f8c-529b-49bf-bbf0-0019babbb438/edx-analysis-on-google-page-speed.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db316f8c-529b-49bf-bbf0-0019babbb438/edx-analysis-on-google-page-speed.png" width="800" height="466" sizes="100vw" caption="edX analysis on Google PageSpeed (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db316f8c-529b-49bf-bbf0-0019babbb438/edx-analysis-on-google-page-speed.png'>Large preview</a>)" alt="edX analysis on Google PageSpeed" >}}

Let’s now move to searching in a specific category. In its current design, edX has no filtering. After choosing a category (for example, electronics courses), users need to scroll through the list to find what they want. And some categories have more than 100 items.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb9b8a06-8c03-4840-9327-5ea9eb5fe5c8/electronics-courses-category-page-on-edx.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb9b8a06-8c03-4840-9327-5ea9eb5fe5c8/electronics-courses-category-page-on-edx.png" width="800" height="396" sizes="100vw" caption="Category page for electronics courses on edX (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb9b8a06-8c03-4840-9327-5ea9eb5fe5c8/electronics-courses-category-page-on-edx.png'>Large preview</a>)" alt="Category page for electronics courses on edX" >}}

#### Other approaches

EdTech platform [Coursera](https://www.coursera.org) has visible filtering on its website, displaying all of the options to filter from in a category:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2501cb54-3b8e-4480-87c1-2864efe01c00/business-category-page-on-coursera.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2501cb54-3b8e-4480-87c1-2864efe01c00/business-category-page-on-coursera.png" width="800" height="324" sizes="100vw" caption="Business category page on Coursera (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2501cb54-3b8e-4480-87c1-2864efe01c00/business-category-page-on-coursera.png'>Large preview</a>)" alt="Business category page on Coursera" >}}

### Problem 5: “Should I Finish This Course?”

[Researchers don’t stop stressing](https://journals.sagepub.com/doi/pdf/10.1177/2158244015621777) that EdTech platforms have, on average, higher retention rates than other websites. Therefore, tracking user progress and motivation is critical for online courses. These principles are pretty simple yet effective.

That is what edX’s user profile looks like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f552b40-f61b-4210-b8f0-5eca767bcca1/edx-personal-cabinet.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f552b40-f61b-4210-b8f0-5eca767bcca1/edx-personal-cabinet.png" width="800" height="270" sizes="100vw" caption="edX’s user profile (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f552b40-f61b-4210-b8f0-5eca767bcca1/edx-personal-cabinet.png'>Large preview</a>)" alt="edX’s user profile" >}}

#### Other approaches

[Khan Academy](https://www.khanacademy.org/)’s user profile displays various statistics, such as join date, points earned, and longest learning streak. It might motivate the user to continue learning and to track their success.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acd22512-31d1-435f-8aa6-25fcadc3462e/khan-academy-personal-cabinet.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acd22512-31d1-435f-8aa6-25fcadc3462e/khan-academy-personal-cabinet.jpg" width="800" height="321" sizes="100vw" caption="Khan Academy’s user profile (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acd22512-31d1-435f-8aa6-25fcadc3462e/khan-academy-personal-cabinet.jpg'>Large preview</a>)" alt="Khan Academy’s user profile" >}}

{{% ad-panel-leaderboard %}}

## Part 2: Audit for 10 Usability Heuristics

We’ve finished analyzing the most common user needs on edX. It’s time to move to the [10 usability criteria](https://www.nngroup.com/articles/ten-usability-heuristics/) identified by Nielsen Norman Group, a UX research and consulting firm trusted by leading organizations worldwide.

You can do a basic UX checkup of your website using the 10 heuristics even if you aren’t a UX designer. Nielsen Norman Group’s website gives a lot of examples, videos, and instructions for each heuristic. [This Notion checklist](https://www.notion.so/Do-It-Yourself-UX-audit-16ef65f920c4403686c2f74b9f57411f) makes it even more convenient. It includes vital usability criteria required for any website. It’s a tool used internally at Fulcrum (where I work), but I thought it would be good to share it with the Smashing Magazine audience. It includes over a hundred criteria, and because it’s in Notion, you can edit it and customize it however you want.

### Heuristic 1: [Visibility of System Status](https://www.nngroup.com/articles/visibility-system-status/)

The first heuristic is to always keep users informed. Simply put, a website should provide users with feedback whenever an action is completed. For example, you will often see a “Success” message when downloading a file on a website.

In this regard, edX’s current course cards could be enhanced. Right now, a card does not tell users whether the course is available. Users have to click on the card to find out.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df726796-2890-45c5-a824-66fde38f6088/edx-mechanical-engineering-courses-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df726796-2890-45c5-a824-66fde38f6088/edx-mechanical-engineering-courses-page.png" width="800" height="530" sizes="100vw" caption="edX page for mechanical engineering courses. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df726796-2890-45c5-a824-66fde38f6088/edx-mechanical-engineering-courses-page.png'>Large preview</a>)" alt="edX page for mechanical engineering courses." >}}

#### Possible approach

If some courses aren’t available, indicate that from the start. You could use bright labels with “available”/“not available” messages.

### Heuristic 2: [Match Between System and the Real World](https://www.nngroup.com/articles/match-system-real-world/)

The system should speak the user’s language. It should use words, phrases, and symbols that are familiar to the average visitor. And the information should appear in a logical order.

This is the second criterion of Jacob Nielsen. edX’s website pretty much follows this principle, using common language, generally accepted symbols, and familiar signs.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c515c7-e0d7-4d27-8e1e-122aa93a40a7/edx-electronics-courses-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c515c7-e0d7-4d27-8e1e-122aa93a40a7/edx-electronics-courses-page.jpg" width="800" height="450" sizes="100vw" caption="edX page for electronics courses (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c515c7-e0d7-4d27-8e1e-122aa93a40a7/edx-electronics-courses-page.jpg'>Large preview</a>)" alt="edX page for electronics courses" >}}

#### Possible approach

Another good practice would be to break down courses by sections, and add easy-to-understand icons.

### Heuristic 3: [User Control and Freedom](https://www.nngroup.com/articles/user-control-and-freedom/)

This heuristic stresses that users always should have a clear way out when they do something by mistake, something like an undo or return option.

edX makes it impossible to change your username once it’s been set up. Many websites limit the options for changing a username for security reasons. Still, it might be more user-friendly to make it changeable.  

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cd80c79-43ed-4722-8298-09a1e608aa20/edx-account-settings.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cd80c79-43ed-4722-8298-09a1e608aa20/edx-account-settings.jpg" width="800" height="307" sizes="100vw" caption="edX account settings (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cd80c79-43ed-4722-8298-09a1e608aa20/edx-account-settings.jpg'>Large preview</a>)" alt="edX account settings" >}}

#### Possible approach

Some websites allow users to save data, a status, or a change whenever they want. A good practice would be to offer customers alternative options, like to add or remove a course or to save or edit their profile.

### Heuristic 4: [Consistency and Standards](https://www.nngroup.com/videos/usability-heuristic-consistency-standards/)

According to this fourth UX criterion, design elements should be consistent and predictable. For example, symbols and images should be unified across the UI design of a platform.

Broadly speaking, there are two types of consistencies: internal and external. Internal consistency refers to staying in sync with a product (or a family of products). External consistency refers to adhering to the standards within an industry (for example, shopping carts having the same logic across e-commerce websites).

edX sometimes breaks internal consistency. Case in point just below: The “Explore” button looks different. Two different-looking buttons (or any other elements) that perform the same function might add visual noise and worsen the user experience. This issue might not be critical, but it contributes to the overall UX of the website.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/735a3c1f-6f7d-4b24-93b8-ace44c2af1ff/explore-courses-buttons-on-edx.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/735a3c1f-6f7d-4b24-93b8-ace44c2af1ff/explore-courses-buttons-on-edx.jpg" width="800" height="269" sizes="100vw" caption="The “Explore Courses” buttons on edX (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/735a3c1f-6f7d-4b24-93b8-ace44c2af1ff/explore-courses-buttons-on-edx.jpg'>Large preview</a>)" alt="The “Explore Courses” buttons on edX" >}}

### Heuristic 5: [Error Prevention](https://www.nngroup.com/articles/slips/)

Good design prevents user error. By helping users avoid errors, designers save them time and prevent frustration.

For instance, on edX, if you make a typo in your email address, it’s visible only after you try to verify it.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd5c468-98ce-48a1-a04f-8c4bda858301/creating-edx-account.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd5c468-98ce-48a1-a04f-8c4bda858301/creating-edx-account.png" width="800" height="561" sizes="100vw" caption="Creating an edX account (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd5c468-98ce-48a1-a04f-8c4bda858301/creating-edx-account.png'>Large preview</a>)" alt="Creating an edX account" >}}

#### Possible approach

Granted, live validation is not always good for UX. Some [designers consider it problematic](https://adamsilver.io/blog/live-validation-is-problematic/), arguing that it distracts users and causes confusion. Others believe that live validation has a place in UX design.

In any case, whether you’re validating live or after the “Submit” button has been clicked, keep your users and their goals in mind. Your task is to make their experience as smooth as possible.

### Heuristic 6: [Recognition Rather Than Recall](https://www.nngroup.com/articles/recognition-and-recall/)

Users should not have to memorize information you’ve shown them before. That’s another UX guideline from Nielsen Norman Group. Colors and icons (like arrows) help users process information better.

edX’s home page displays university logos, but not the universities’ full names, which illustrates this point. Also, the user profile page doesn’t tell you which courses you’ve completed.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f552b40-f61b-4210-b8f0-5eca767bcca1/edx-personal-cabinet.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f552b40-f61b-4210-b8f0-5eca767bcca1/edx-personal-cabinet.png" width="800" height="270" sizes="100vw" caption="edX user profile (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f552b40-f61b-4210-b8f0-5eca767bcca1/edx-personal-cabinet.png'>Large preview</a>)" alt="edX user profile" >}}

#### Possible approach

The platform’s UX could be improved by showing courses that users have already done and recommending similar ones.

### Heuristic 7: [Flexibility and Efficiency of Use](https://www.nngroup.com/articles/flexibility-efficiency-heuristic/)

According to this UX principle, speed up interaction wherever possible by using elements called accelerators. Basically, use any options or actions that speed up the whole process.

edX doesn’t provide filtering when users search for a course. Its absence could increase the time and effort users take to find the course they need.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf3516c4-759e-4730-8312-c1f7695dd491/edx-search-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf3516c4-759e-4730-8312-c1f7695dd491/edx-search-page.png" width="800" height="436" sizes="100vw" caption="edX search page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf3516c4-759e-4730-8312-c1f7695dd491/edx-search-page.png'>Large preview</a>)" alt="edX search page" >}}

#### Possible approach

Search is one of the critical stages of user conversion. If users can find what they want, they will be much closer to becoming customers. So, use filters to help users find courses more quickly and easily.

### Heuristic 8: [Aesthetic and Minimalist Design](https://www.nngroup.com/videos/aesthetic-and-minimalist-design/)

[This heuristic](https://www.nngroup.com/videos/aesthetic-and-minimalist-design/) tells us to “remove unnecessary elements from the user interface and to maximize the signal-to-noise ratio of the design” (the signal being information relevant to the user, and the noise being irrelevant information).

Simply put, every element should tell a story, like a mosaic. Designers communicate, not decorate.

Comparing the current design of edX’s home page to the previous one, we can see a huge improvement. The main photo is now much more relevant to the platform’s mission. edX also added insights into how many users and courses it has.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ff152ad-4775-4dd9-86bc-3b5e88f86cd1/edx-s-previous-current-homepage-photos.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ff152ad-4775-4dd9-86bc-3b5e88f86cd1/edx-s-previous-current-homepage-photos.png" width="800" height="375" sizes="100vw" caption="edX’s previous and current home page photos (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ff152ad-4775-4dd9-86bc-3b5e88f86cd1/edx-s-previous-current-homepage-photos.png'>Large preview</a>)" alt="edX’s previous and current home page photos" >}}

### Heuristic 9: [Help Users Recognize, Diagnose, and Recover From Errors](https://www.nngroup.com/videos/usability-heuristic-recognize-errors/)

This heuristic states that errors should be expressed in simple, explanatory language to the user. It’s also good to clearly explain why an error occurred in the first place.

edX’s 404 page serves its purpose overall. First, it explains to the user the problem (“We can’t seem to find the page you’re looking for”) and suggests a solution (giving links to the home page, search function, and course list). It also recommends popular courses.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f3f43d1-3f77-40e5-b99f-a82d8649da61/edx-404-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f3f43d1-3f77-40e5-b99f-a82d8649da61/edx-404-page.png" width="800" height="420" sizes="100vw" caption="edX 404 page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f3f43d1-3f77-40e5-b99f-a82d8649da61/edx-404-page.png'>Large preview</a>)" alt="edX 404 page" >}}

### Heuristic 10: [Help and Documentation](https://www.nngroup.com/articles/ten-usability-heuristics/)

This last heuristic is about the necessity of support and documentation on any website. There are many forms of help and documentation, such as onboarding pages, walkthroughs, tooltips, chats, and chatbots.

edX has links to a help center hidden in the footer. It’s divided into sections, and users can use a search bar to find information. The search does a good job of auto-suggesting topics that might be useful.

Unfortunately, users can’t go back to the home page from the help center by clicking the logo. There is no direct way to get back to the home page from there.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/327d2c1e-4af4-4a00-953e-549adc8f3289/edx-helpcenter.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/327d2c1e-4af4-4a00-953e-549adc8f3289/edx-helpcenter.png" width="800" height="368" sizes="100vw" caption="edX help center (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/327d2c1e-4af4-4a00-953e-549adc8f3289/edx-helpcenter.png'>Large preview</a>)" alt="edX help center" >}}

#### Possible approach

Enable users to return to the home page wherever they want on the website.

{{% ad-panel-leaderboard %}}

## eDX Redesign Concept

Based on my UX findings, I resdesigned the platform, focusing on the **home page, user profiles, and search** results page. You can see full images of the [redesign in Figma](https://www.figma.com/file/ZdBMZBQ41EsjIkBiv9kqY5/edX-redesign?node-id=0%3A1).

### Home Page

#### 1. Signal-to-Noise Ratio

First things first: To meet [usability heuristic 8](https://www.nngroup.com/videos/aesthetic-and-minimalist-design/), I’ve made the whole page more minimalist and added space between its elements.

edX has the grand mission of “education for everyone, everywhere”, so I decided to put this on the home page, plain and bold.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c66fc7fc-6edc-4f48-8786-b2d8b322b387/edx-mission.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c66fc7fc-6edc-4f48-8786-b2d8b322b387/edx-mission.png" width="800" height="262" sizes="100vw" caption="edX’s mission (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c66fc7fc-6edc-4f48-8786-b2d8b322b387/edx-mission.png'>Large preview</a>)" alt="edX’s mission" >}}

I also switched the images to better reflect the story presented in the text. I expressed the mission with these new illustrations:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31161dd4-f5bc-47c6-a239-edf26b496246/edx-mission-redesigned.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31161dd4-f5bc-47c6-a239-edf26b496246/edx-mission-redesigned.jpg" width="800" height="394" sizes="100vw" caption="edX’s mission redesigned (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31161dd4-f5bc-47c6-a239-edf26b496246/edx-mission-redesigned.jpg'>Large preview</a>)" alt="edX’s mission redesigned" >}}

#### 2. Course Cards

The “New Courses” section below highlights the latest courses.

I also added some details that edX’s cards currently do not display. This made the cards more descriptive, showing essential information about each course.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c32f32c6-4eeb-4c72-9f6a-bc89422f3d95/edx-redesign-new-courses-popular-subjects.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c32f32c6-4eeb-4c72-9f6a-bc89422f3d95/edx-redesign-new-courses-popular-subjects.jpg" width="800" height="603" sizes="100vw" caption="edX redesign: new courses and popular subjects (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c32f32c6-4eeb-4c72-9f6a-bc89422f3d95/edx-redesign-new-courses-popular-subjects.jpg'>Large preview</a>)" alt="edX redesign: new courses and popular subjects" >}}

I also used icons to show the most popular subjects.

#### 3. Credibility and Trust

I added a fact sheet to show the platform’s credibility and authority:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c2dbffa-b073-4dea-9bbd-c49d9ee5027e/edx-redesign-facts-sheet.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c2dbffa-b073-4dea-9bbd-c49d9ee5027e/edx-redesign-facts-sheet.jpg" width="800" height="557" sizes="100vw" caption="edX redesign: fact sheet (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c2dbffa-b073-4dea-9bbd-c49d9ee5027e/edx-redesign-facts-sheet.jpg'>Large preview</a>)" alt="edX redesign: fact sheet" >}}

In addition, I freshened up the footer, reshaping the languages bar to be more visible to users.

### Helpful Search

#### 1. Search Process

In edX’s current design, users don’t see the options available while searching. So, I designed a search function with auto-suggestion. Now, users just need to type a keyword and choose the most relevant option.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205ffedc-94a6-4b28-96d3-da9e1bbd4318/edx-redesign-search.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205ffedc-94a6-4b28-96d3-da9e1bbd4318/edx-redesign-search.jpg" width="800" height="584" sizes="100vw" caption="edX redesign: search (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205ffedc-94a6-4b28-96d3-da9e1bbd4318/edx-redesign-search.jpg'>Large preview</a>)" alt="edX redesign: search" >}}

#### 2. Search Filters

I added a left sidebar to make it easy to filter results. I also updated the UI and made the course cards more descriptive.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f012730f-783d-4d83-9e62-6ee2497eb1bd/edx-redesign-search-filters.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f012730f-783d-4d83-9e62-6ee2497eb1bd/edx-redesign-search-filters.jpg" width="800" height="446" sizes="100vw" caption="edX redesign: search filters (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f012730f-783d-4d83-9e62-6ee2497eb1bd/edx-redesign-search-filters.jpg'>Large preview</a>)" alt="edX redesign: search filters" >}}

### User Profile

As mentioned in the audit section, it’s essential to motivate users to continue studying. Inspired by Khan Academy, I added a progress bar to user profiles. Now, a profile shows how many lessons are left before the user completes a course.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66ed59de-ccd9-499e-9106-6d06eb08ebea/edx-redesign-user-cabinet-with-progress-bar.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bb79bb3-264e-4786-a308-b54aecdc8c04/edx-redesign-user-cabinet-progress-bar.jpg" width="800" height="569" sizes="100vw" caption="edX redesign: user profile with progress bar (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66ed59de-ccd9-499e-9106-6d06eb08ebea/edx-redesign-user-cabinet-with-progress-bar.jpg'>Large preview</a>)" alt="edX redesign: user profile with progress bar" >}}

I put the navigation above so that it can be easily seen. Also, I updated the user profile settings, leaving the functionality but modifying the colors.

## Conclusion

A UX audit is a simple and efficient way to check whether design elements are performing their function. It’s also a good way to look at an existing design from a fresh perspective.

This case presented me with several lessons. First, I see that the websites in one of the most topical industries right now could have their UX updated. Learning something new is hard, but without proper UX design, it’s even harder.

The audit also showed why it’s crucial to understand, analyze, and meet user needs. Happy users are devoted users.

{{< signature "vf, il, yk, al" >}}
