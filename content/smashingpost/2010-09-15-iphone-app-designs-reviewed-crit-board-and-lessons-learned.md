---
title: 'iPhone App Designs Reviewed: Critique Board and Lessons Learned'
slug: iphone-app-designs-reviewed-crit-board-and-lessons-learned
image: null
date: 2010-09-15T12:51:22.000Z
author: alex-komarov
description: >-
  Some time ago I started a mobile app design review section on our company's website. The idea behind this "Crit Board" was simple: if mobile developers want to create apps that people want to buy, they'll need help with design and usability. But most of the time they can't afford it. Developers can send us their mobile apps (iPhone apps, Android apps, Blackberry apps) along with questions and problems, and we (free of charge) will pick apart key usability issues,
  illustrate our design recommendations and post our findings.
categories:
  - Mobile
  - Apps
  - iPhone
  - Design Patterns
---
The only condition to get free criticism from us is that you agree for it to be made public, which is why I am able to share several case studies with Smashing's readers right now. It's hard to imagine something more relevant: these are real problems facing real developers. I hope these problems and the proposed solutions will benefit others who have similar issues and will be generally relevant to those working in the field.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Thinking Like An App Designer](https://www.smashingmagazine.com/2015/04/thinking-like-an-app-designer/)
*   [iPhone Apps Design Mistakes: Disregard Of Context](https://www.smashingmagazine.com/2009/11/iphone-apps-design-mistakes-disregard-of-context/)
*   [iPhone App Design Trends](https://www.smashingmagazine.com/2009/10/iphone-app-design-trends/)

{{% feature-panel %}}

## 1\. Foobi

<em>"Alex,</em>

<em>I am the lead designer and developer of <a href="https://tapplox.com/apps-foobi.html">Foobi</a>. Foobi was designed to track your diet in a different way; instead of tracking calories and tapping on many drilled-down lists, it works by simply tracking servings per food group and providing an overview of your food intake balance.</em>

<em>Although I have tried really hard not to over-design it by tracing Apple's footsteps while building custom UI control elements, I would love to hear from you about this subject.</em>

<em>— Remy"</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/601ab1f3-c966-41fa-8da9-333ac47571c9/foobi-1-new.png" alt="" />

Your app is beautiful indeed. And it is also usable and easy, exactly as you describe it: if user knows how to flick, he is already an expert. An expert in what, though?

As stated in the iTunes description, the purpose of this app is to "track and balance your diet." I understand the two main user goals as follows:

1.  To record what food they consume,
2.  To make sure they stay on the right path with their nutrition, and to have a clear guide to balancing their diet if they veer off that path.

Your app does a good job of fulfilling the first goal: users can easily record what they eat just by selecting the right food group and adding the amount of "servings" consumed.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/770833ce-06e7-4f16-a01c-1faaadd79d9a/foobi-2-new-updated1.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63106" title="_Foobi_2_new_updated" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/770833ce-06e7-4f16-a01c-1faaadd79d9a/foobi-2-new-updated1.png" alt="" width="545" height="518" /></a>

But what about the second more important goal of tracking progress and adjusting one’s diet? Does the app help customers achieve this goal? Not very well. There is room for big improvement.

There are two main problems with this part of the app.</p>

### Summary Information Is Hidden

To access the summary chart, you have to flip the iPhone to the side and view it in landscape mode. But this feature is not communicated through the app's design, so a user will discover it only by accident. When we talk about fulfilling a major user goal, it is important never to rely on accidents to communicate functionality.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29851635-9a63-42fa-8ad4-37ce384b9151/foobi-3-new-updated.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63107" title="_Foobi_3_new_updated" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29851635-9a63-42fa-8ad4-37ce384b9151/foobi-3-new-updated.png" alt="" width="550" height="342" /></a>

### Summary Information Is Not Well Designed

Additionally, the summary is not informative enough.

The summary chart doesn't offer too much to the viewer. Here are the main problems:

*   It's not clear what the different colors mean, and there is no legend to help.
*   The scale is not flexible. You can view the information only by week, which does not allow users to easily see their big-picture eating habits. (Tip: consider incorporating the pinch gesture to allow users to scale in and out.)
*   Tracking consumption of a particular food group is not possible with this chart but would be valuable to users.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b60174-243d-4ef3-bedd-175b0c4718f9/foobi-4-new-updated.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63109" title="_Foobi_4_new_updated" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b60174-243d-4ef3-bedd-175b0c4718f9/foobi-4-new-updated.png" alt="" width="480" height="380" /></a>

Information design is a vast topic. There are a million ways to address the problems that I've highlighted and to increase the visibility of useful information for your audience. I recommend reading Edward Tufte's books, particularly <em>The Visual Display of Qualitative Information</em>.

And here’s an inspiring display of a lot of information. Of course, it’s not tailored to mobile use, but it has a few great ideas:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ab3d4be-ed23-4e5f-a1ee-ae1ace08818e/4-foobi.jpg" alt="" /><br>
<em>From <a href="https://www.google.com/finance">Google Finance</a>.</em>

### One More Thing

When I purchased and downloaded your app, I didn’t quite understand why it was taking so long to download… until I realized that it had already downloaded. I was fooled by the app icon, which makes it look like it is still downloading:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/569a6e00-89b0-432e-a43b-7c3902f90c7c/5-foobi-updated.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63101" title="_5_foobi_updated" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/569a6e00-89b0-432e-a43b-7c3902f90c7c/5-foobi-updated.png" alt="" width="314" height="129" /></a>

## 2\. Budget Planner

<em>"Alex, please take a look at my app Budget Planner. I have tried everything, and it keeps going up and down. The major issues that people complain about are intuitiveness and slowness. People don't understand what the software does. But people who do learn it love it.</em>

<em>— Alex Sabonge"</em>

The basic idea of this app is very good, and the App Store description shows off its functionality well:"Budget Planner tracks your bills, budget, calendar and transactions by displaying your balance in a calendar view, letting you know how much money you will actually have on any particular day. Like a balance forecaster."

Here’s an <strong>overview</strong> of how Budget Planner works:

1.  Users input their monthly salary info and plug in their fixed monthly expenses (utilities, phone, car payment, etc).![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/140d69d8-74a8-4ba4-934d-19dc6012ed80/budget-planner-1-new.png)
2.  Using this data, the app allows users to track their cash flow and predict the amount they’ll have in the bank on any given day.![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/561631b2-89c5-4619-9bfe-dcd27272aee9/budget-planner-2-new.png)

Most folks would find this extremely useful. So, why are people complaining about the app? Why does it have an average rating of 2.5 out of 5 stars, and why are sales lower than you had hoped?

Let’s look at the main sources of the problem. For now, we’ll set aside lesser (though important) usability factors, such as not following the iPhone UI guidelines and using the standard controls improperly. Let’s start at the beginning. Humans invented money to buy things, right? Your core audience’s main goal is to know what they can afford and when they can afford it, whether it’s a new pair of shoes, a new car or a solid retirement plan.

People don't prepare a budget just for fun. They make the effort because they hope it will help them make better purchasing decisions (read: buy more stuff that they like), without their rent check bouncing. Your app is getting there. But several key factors are getting in the way of a great user experience. Let’s take a closer look at the app’s “landing screen,” the calendar, the main element that differentiates this app from other budget apps.

First of all, I think the calendar is a great idea. It’s much better than the categorized lists that many other apps have. The calendar is all about how much money you have or will have in future. A list only shows how much you’ve spent. Knowing that your money is gone doesn’t really help achieve a financial goal (purchasing a shiny new laptop, for example).

Here are some <strong>downsides</strong> to the calendar view:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ca474e3-a24d-43f5-a871-74a08af552d3/budget-planner-3-new-updated2.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63289" title="_Budget_planner_3_new_updated2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ca474e3-a24d-43f5-a871-74a08af552d3/budget-planner-3-new-updated2.png" alt="" width="541" height="754" /></a>

I believe there's a way to visualize information in the current design so that users are able to uncover "invisible" patterns. Uncovering the details and patterns behind their spending habits enables users to get new ideas, make informed decisions and achieve their financial goals (and praise your app in the process). Users will better understand their bad habits and be able to take steps to correct them.

A graph <strong>could provide richer possibilities for visualizing financial information</strong>. It’s much more flexible and scalable then a calendar. Using a graph for the landing screen could dramatically increase the density of meaningful data, while reducing visual noise. Here are some ideas we came up with; this is merely a draft we put together to illustrate our points and to get your ideas flowing—it is not a proposal for a final design:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4d1f33a-ec0a-43d5-bb43-aba37d754e73/budget-planner-4-new-updated.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63103" title="_Budget_planner_4_new_updated" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4d1f33a-ec0a-43d5-bb43-aba37d754e73/budget-planner-4-new-updated.png" alt="" width="550" height="570" /></a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df35420c-5dfe-43d7-ba37-f00b2ae0d27d/budget-planner-5-new-updated.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63104" title="_Budget_planner_5_new_updated" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df35420c-5dfe-43d7-ba37-f00b2ae0d27d/budget-planner-5-new-updated.png" alt="" width="549" height="326" /></a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c2675b9-e683-4a8d-a27c-d7ab09d4b25e/budget-planner-6-new-updated.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="63105" title="_Budget_planner_6_new_updated" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c2675b9-e683-4a8d-a27c-d7ab09d4b25e/budget-planner-6-new-updated.png" alt="" width="550" height="326" /></a>

### Next Steps

People love apps that help them achieve their goals. What if your app allowed users to input and compare different financial scenarios, shown through several overlaid graphs?

This capability could help users think through their options:

*   If I put my child through this private school, would I still be able to afford the Beemer I’ve always dreamed of?
*   How many hours of overtime would I need to work to be able to afford both?

These are few examples of questions that people ask themselves. If your app can help them get the answers, I think it’ll really catch on, and you’ll soon be driving a shiny new Beemer yourself.</p>

## 3\. Units United

<em>"Unit conversion app, <a href="https://itunes.apple.com/us/app/id333198406?mt=8">Units United</a>. Yep, yet another one… ;) Can you please review it?</em>

<em>— Meils Dühnforth"</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da3fc03f-db22-4061-b120-7c5bb240ab7c/units-united-1-new.png" alt="" />

The biggest problem with almost every unit converter I have seen is that they require users to submit their query in a format that the computer (or iPhone in this case) can understand. Most unit converters force people to make double the effort to get what they want.

Consider the following scenario: you’re from the US, and you are recounting yesterday’s baseball game to your Icelandic friend. During their last at bat, the Phillies hit a 456-foot home run. Amazing! You punch the value into your unit converter app, but to get an answer you must translate the query into a format that the application understands:

1.  Go to “Categories,”
2.  Select meters for the “To” unit,
3.  Select feet for the “From” unit,
4.  Type in 456 on the number pad,
5.  Double-check that you are converting 456 feet into metres and not vice versa.

Are all these steps necessary? You just wanted to know “What is 456 feet in meters?” But you had to ask the question in robo-speak. You had to select options from a list to be understood. Good software speaks your language. Among the innumerable unit converters, only Google does it right, allowing you to ask your question in plain English:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13559880-0e82-4361-ad35-eca1e426977d/units-united-2-new.png" alt="" />

Using speech recognition technology is another good idea. Sometimes your hands aren't free when you need to convert a unit. Say your Icelandic friend is driving on a US highway and needs to convert the 55 miles-per-hour speed limit into kilometers.

Implementing everything described above, your app might look something like this (this quick draft is meant to illustrate the point and is not a design proposal):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/087ee8c3-4a5b-46c7-91a8-ca3746c6f278/units-united-3-new.png" alt="" />

This application is much easier to use because there's no more robo-talk: it doesn't force users to browse categories and sub-categories, and it accepts questions in everyday language.</p>

## Send Your App For A Free Review!

Mobile developers are always welcome to send me their apps for a free review. Just use this form. Please remember that your content will be featured on our Crit Board, allowing developers, designers and users worldwide to join the conversation. If you prefer to speak privately about your design, please feel free to contact us directly.

{{< signature "al" >}}
[twcount]

