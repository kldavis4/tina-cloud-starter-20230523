---
title: 'Making Time: Redesigning A Calendar Experience For Android'
slug: redesigning-a-calendar-experience-for-android
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df8e1f17-234a-4374-ae24-9fab9c99d99f/00-making-time-opt.png
date: 2015-07-24T21:55:40.000Z
author: guentherbeyerninorapin
description: >-
  In UX design, few things are more intricate than time and personal time
  management — only a good arsenal of mobile design patterns and information
  architecture principles can save you. This is the **story of redesigning the
  UX for a popular calenda tool on Android**: Business Calendar. We’ll cover
  designing systems, interaction design problems, scaling across screens and
  platforms, research, and big business decisions and their outcomes.

  Business Calendar started out as a side project, a one-man show, and is now
  run by a team of eight in Berlin. The app was very successful right from the
  time Android entered the mainstream market, and it now has an active user base
  of 2 million. But instead of modernizing the design and usability regularly,
  the developers focused on implementing user requests and customization
  options.
categories:
  - Coding
  - UX
  - Case Studies
  - Android
---
In UX design, few things are more intricate than time and personal time management — only a good arsenal of mobile design patterns and information architecture principles can save you. This is the <strong>story of redesigning the UX for a popular calendar tool on Android</strong>: Business Calendar. We’ll cover designing systems, interaction design problems, scaling across screens and platforms, research, and big business decisions and their outcomes.</p>

## The Onset

Business Calendar started out as a side project, a one-man show, and is now run by a team of eight in Berlin. The app was very successful right from the time Android entered the mainstream market, and it now has an active user base of 2 million.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Designing For A Maturing Android</span>](https://www.smashingmagazine.com/2013/05/brave-new-world-designing-for-a-maturing-android/)
*   [Mobile Design Practices For Android](https://www.smashingmagazine.com/2012/07/android-design-tips/)
*   [How To Simplify Networking In Android](https://www.smashingmagazine.com/2017/03/simplify-android-networking-volley-http-library/)
*   [Bringing Your App’s Data To Every User’s Wrist](https://www.smashingmagazine.com/2017/01/bringing-app-data-every-user-wrist-android-wear/)

{{% feature-panel %}}

But instead of modernizing the design and usability regularly, the developers focused on implementing user requests and customization options. Outdated design and new features stuffed in had made the app heavy and complex — full of features, hard to maintain for the team, hardly accessible for new users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12536864-a317-43d3-8995-21eb69f68c87/01-before-redesign-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0cc0ffa-7160-4534-88f7-25fea0611810/01-before-redesign-opt-small.png" alt="Business Calendar before the redesign: it still looks and works like in the days of Android 2.x" /></a><figcaption>Business Calendar before the redesign: It still looks and works like in the days of Android 2.x. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12536864-a317-43d3-8995-21eb69f68c87/01-before-redesign-opt.png">View large version</a>)</figcaption></figure>

Knowing they needed a redesign but having few resources themselves, the team approached Opoloo to get design and interaction on the same level as the development. For the task, we delineated goals to attract new users and keep the existing user base satisfied:

*   **Improve user experience**.  Strip down and reorganize the user interface to revive the simple, fast, efficient work process of a productivity tool.
*   **Improve accessibility**.  Keep old users happy, lower the barriers for new ones.
*   **Incorporate task management**.  Integrate tools that users need every day to create more value.
*   **Apply modern design standards**.  Address the main criticism: “Could be prettier.”
*   **Extensive tablet support**.  Improve the tablet experience as a first step to ubiquity.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5b5337-2bdf-4358-9cbb-1af2737785a6/02-paper-prototypes-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbf4215e-b2c3-43d4-8fae-cb7ad70a361a/02-paper-prototypes-opt-small.jpg" alt="Working with paper prototypes to test concepts and iterate quickly" /></a><figcaption>Working with paper prototypes to test concepts and iterate quickly. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5b5337-2bdf-4358-9cbb-1af2737785a6/02-paper-prototypes-opt.jpg">View large version</a>)</figcaption></figure>

## Interface Design: Presentation

The hardest part of any mobile calendar’s interface is the density of information, with each little piece fighting for attention: grids, events, time indicators, text labels, colors and other elements to interact with, manipulate and customize. Finding the right balance is what makes for an accessible calendar UI. Below are a few tricks we pulled with the presentation of data (i.e. how pieces of information are consumed, searched for and compared).</p>

### Favorite Bar

Although an iconic and heavily used feature of Business Calendar, the favorite bar was barely accessible: It became too small and too crowded to use as the number of calendars grew. Our solution was to use Android’s black system bar as an optical trick: The favorite bar now feels much taller and easier to tap, due to the black-in-black design. Additionally, we improved touch targets, made visible and invisible states clearer, and implemented a scrolling pattern to house more calendars.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b146b969-0f5c-411b-a02f-531c54d8e912/03-design-favorites-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/571221d7-5d99-4192-aae9-92c2af68cae3/03-design-favorites-opt-small.png" alt="One of the distinct features of Business Calendar is the favorite bar. Here is the old and new version for comparison." /></a><figcaption>One of the distinct features of Business Calendar is the favorite bar. Here is the old and new version for comparison. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b146b969-0f5c-411b-a02f-531c54d8e912/03-design-favorites-opt.png">View large version</a>)</figcaption></figure>

### View Selector

Most calendars use a spinner in the top-left corner to change views, but this can be difficult on a 4-inch+ screen, especially when you’re on the run. A navigation drawer that opens with a swipe from the left edge made switching views much easier, no matter how large the screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8312f3b5-3660-4165-8346-837f55a4b79d/04-design-navigation-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d02a6bc-ec95-4e31-8a95-41b0c66482f0/04-design-navigation-opt-small.png" alt="The view selector is turned from a spinner into a navigation bar, according to Android's standards for accessibility and consistency." /></a><figcaption>The view selector is turned from a spinner into a navigation bar, according to Android’s standards for accessibility and consistency. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8312f3b5-3660-4165-8346-837f55a4b79d/04-design-navigation-opt.png">View large version</a>)</figcaption></figure>

### Day View

“Where do I have to be today? What needs to get done? Oh, and do I need to bring an umbrella?”

This is what most people want their calendar to tell them first thing in the morning, and the old app didn’t answer these questions. This small detail makes the day view much more valuable to any user.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e059fff-52a4-4d71-93ff-bc5353cd657b/05-design-day-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f359187-0050-4271-bb8a-e016f4398c31/05-design-day-opt-small.png" alt="Focusing on the very basics of what you need to get through the day makes the day view unique and accessible. This is the day view reimagined: events, tasks and weather." /></a><figcaption>Focusing on the very basics of what you need to get through the day makes the day view unique and accessible. This is the day view reimagined: events, tasks and weather. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e059fff-52a4-4d71-93ff-bc5353cd657b/05-design-day-opt.png">View large version</a>)</figcaption></figure>

### Evaluation and Learning

If you’re pressed for space and clarity, using black for general interaction works well because it integrates in the system bars and lets you focus on the content, especially when the colors are defined by the user. Also, focusing on the user’s physical abilities and mindset is paramount for a good experience.

One thing we underestimated, despite intense research and good progress on the presentation side, was the hardcore user’s need to customize their calendar experience down to the tiniest detail (for example, changing the font’s transparency). Only after this initial UI exploration did we realize how much work would be needed — not only to implement the design suggestions, but also to customize everything.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/243ae7a5-df82-4b77-ab64-16d83830392a/06-design-device-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfb250ad-bece-4c52-a772-1faa91869479/06-design-device-opt-small.jpg" alt="The calender app on a mobile device" /></a><figcaption>The calender app on a mobile device. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/243ae7a5-df82-4b77-ab64-16d83830392a/06-design-device-opt.jpg">View large version</a>)</figcaption></figure>

## Interface Design: Dialogs

Unlike the presentation, <strong>interaction with data deals with all of the dialogs</strong>, customizations and preferences and their influence on the interface. While we usually see the month or week views of our calendars, the real magic always happens in the dialogs. Being able to quickly find the right time slot, creating an event, setting all of its parameters (such as attendees or location) and, finally, getting reminders that are perfect for you — all of these are what make a calendar useful.</p>

### Research and Constraints

Business Calendar was stuffed with dialogs, some of them essentially doing the same job, but without consistency. Every dialog led to another, and most had multiple versions, each with subtle variations and advanced options. Still, few of them did exactly what you’d expect.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da2e581c-7cff-4e72-a0a0-45d0af4df969/07-dialog-all-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4deacb61-5525-48f4-8b9d-afe3a6031cce/07-dialog-all-opt-small.png" alt="A huge variety of dialogs in the old version: date pickers, time pickers, color pickers, number pickers; lists with single selection, multiple selection; lists with options; lists with additional features; and any other kind of list you can imagine." /></a><figcaption>A huge variety of dialogs in the old version: date pickers, time pickers, color pickers, number pickers; lists with single selection, multiple selection; lists with options; lists with additional features; and any other kind of list you can imagine. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da2e581c-7cff-4e72-a0a0-45d0af4df969/07-dialog-all-opt.png">View large version</a>)</figcaption></figure>

### Design and Implementation

To keep the number of dialogs manageable and consistent, while holding on to most of the features, we divided them into four groups:

*   calendars and colors,
*   times and days,
*   history and templates,
*   special dialogs.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606cb97e-6980-4223-9045-58e27026d2e0/08-dialog-test-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20a7efb9-96d5-4c47-aa51-397446c1d37e/08-dialog-test-opt-small.png" alt="Calendars and colors worked as our experimental set. While revisiting every action with use cases, sketches and wireframes, we played with different colors, typography and styles." /></a><figcaption>Calendars and colors worked as our experimental set. While revisiting every action with use cases, sketches and wireframes, we played with different colors, typography and styles. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606cb97e-6980-4223-9045-58e27026d2e0/08-dialog-test-opt.png">View large version</a>)</figcaption></figure>

For each individual dialog, we then asked, what do our users expect here? Can we make it better? Can we cover its functionality with a basic system dialog? Or do we need a custom solution, as we did with the tasks below?

### Pick a Day or Range of Days

Picking a day or range of days (for example, a vacation period) is usually done by selecting a month and then a numerical value with a spinner. But really, the user wants to select not an abstract number, but rather a concrete time frame. The result is a month-like view, with a swipe selection for multiple days.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4b20d4-57fc-4360-b6a8-359010420b9a/09-dialog-range-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3f67e5a-578c-4f78-86b5-0992c084e463/09-dialog-range-opt-small.png" alt="Picking a day or range of days reveals a plethora of use and edge cases, all of which we had to map out for a fluid experience." /></a><figcaption>Picking a day or range of days reveals a plethora of use and edge cases, all of which we had to map out for a fluid experience. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4b20d4-57fc-4360-b6a8-359010420b9a/09-dialog-range-opt.png">View large version</a>)</figcaption></figure>

### Go to Year and Month

When selecting a day far into the future, you had to tediously swipe from month to month. We needed an option for the user to easily navigate to a month <em>and</em> a year, without having to select each individually. What could have unravelled as a complex series of dialogs turned into a simple list — years and months are separated visually and navigated with a fast swipe.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e03593e6-70ce-4478-b200-9325c56e76a9/10-dialog-goto-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bd88128-9695-4192-9fd9-323e70469e92/10-dialog-goto-opt-small.png" alt="Switching between month and year to quickly set and edit events. From left to right: the old view picker, a quick sketch, and the redesigned version." /></a><figcaption>Switching between month and year to quickly set and edit events. From left to right: the old view picker, a quick sketch, and the redesigned version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e03593e6-70ce-4478-b200-9325c56e76a9/10-dialog-goto-opt.png">View large version</a>)</figcaption></figure>

### The Result: A Modular Design System

We not only reduced the number of dialogs, but made sure that each dialog was part of a consistent system, defined by the actions that a user wants to complete. The idea of the modular design system that we formed when working on the dialogs is that the developers are capable of creating solid interaction patterns based on defined building blocks, without the need for constant design feedback. This accelerated development tremendously and kept communication overhead to a minimum.

In reality, this works for most cases. But depending on how complex you build your guiding system, eventually an edge case or contextual setting might break something, especially with a highly customizable app, in which case you would have to create a dedicated solution.

Dialogs are hard, especially with a complex set of customizable data, but they are where the lion’s share of time is spent. Your effort to get the most out of every single option is ultimately what sets a great productivity app apart, and every millisecond will help to take some stress out of every user’s day.</p>

## Settings

Settings are a huge deal for frequent calendar users. About 60 are at hand to give users full dominion over their calendars. Most of them open new dialogs and subsetting screens, like vibration time and vibration intervals. The sheer number can be unsettling. A conflict arises: fast access versus detailed customization.</p>

### Research and Constraints

Originally, all of the settings were on the same screen, which ensured accessibility. But as new features and customizations were created, the settings became less usable: Organic growth made them confusing, inconsistent and cumbersome.

Android’s settings seemed like a perfect blueprint for consistency and accessibility, being fairly extensive, complex and adequately deep. By sticking to the guidelines suggested by the native settings, we would also stay close to what users have already been exposed to.</p>

### Design and Implementation

Still, there was the hard work to be done: We had to take everything apart. On three huge whiteboards, we listed all of the settings, along with their exact functionality, where they occurred and what actions followed from them.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1732381b-b6df-4ffa-9814-11ee8e669fc8/11-settings-process-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8387874b-1795-4ae3-a764-84fedf34452b/11-settings-process-opt-small.jpg" alt="Dissecting the settings architecture was done by hand on whiteboards, and then detailed reviews, discussions and problem-solving were done in spreadsheets." /></a><figcaption>Dissecting the settings architecture was done by hand on whiteboards, and then detailed reviews, discussions and problem-solving were done in spreadsheets. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1732381b-b6df-4ffa-9814-11ee8e669fc8/11-settings-process-opt.jpg">View large version</a>)</figcaption></figure>

The problem with having many settings, generally, is that changes arising from adjustments are revealed only when you actually try them. That might work, but it makes for terrible interaction design. Labeling adequately and precisely is paramount for good settings, so we regrouped and relabeled most of the settings to give the user a more relevant context for their actions. A good label gives you an idea of what you’re going to set <em>before</em> you set it.</p>

### Evaluation and Learning

Because we couldn’t reduce the number of settings, we split them into “General Settings” and “Views,” which correlate with the app’s architecture. A layered approach follows from that: The user first selects the settings group, then the setting, then the input. So, rather than being presented with everything in a large cluttered panel, where you’d have to wander and jump around, you have an entry point to drop into a setting, adjust it and then hop back up again. What might sound like unnecessary taps actually makes the user’s actions much more intentional: They spend less time searching and can adjust the settings undisturbed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c0815a9-72de-4d63-944f-c619436ace69/12-settings-settings-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ae693f-106e-48e2-a37a-7af15e232af9/12-settings-settings-opt-small.png" alt="A view of the huge settings panel in the old calendar, versus the newly rethought settings." /></a><figcaption>A view of the huge settings panel in the old calendar, versus the newly rethought settings. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c0815a9-72de-4d63-944f-c619436ace69/12-settings-settings-opt.png">View large version</a>)</figcaption></figure>

## Brand And Character Through Systematic Design

Branding is primarily used to orient people and, ideally, supports a person’s decision of which product is right for them in an ever-so-crowded market. A brand must tell a quick, delightful story that would otherwise take much longer. Our challenge was to come up with branding that doesn’t get in the way of productivity but still tells a unique product story.</p>

### Research and Constraints

The magic of Business Calendar was hardly visible from the outside. What made the app special and loved by its millions of users was the extensive feature set and attention to interaction detail. We wanted to communicate this much earlier in the process.

There were some constraints. With an interface so densely packed with information, people care about their content — not about the app itself. And we had to allow for a highly customizable interface; elements that usually carry branding could easily be hijacked by users who are prone to changing colors, typefaces and sizes altogether. So, instead of placing branding cues in the interface, we subtly turned the interface into a brand that would be clearly associated with Business Calendar.</p>

### Design and Implementation

Because we couldn’t touch colors, which were important for recognition and customization by the user, we were left to work with black and white. So, we made this constraint our primary branding element.

From there, the concept of white paper on a black background emerged. We laid out the user’s content in white areas, while restricting navigation and interaction with the app itself in black boxes. Likewise, all events would be displayed in their respective color in a white month grid.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ef1ea57-244f-40b7-b656-87eb547e6e35/13-brand-paper-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef7b1a51-b178-4d9d-a267-8d4527cc308f/13-brand-paper-opt-small.png" alt="Content in white, interaction and navigation in black." /></a><figcaption>Content in white, interaction and navigation in black. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ef1ea57-244f-40b7-b656-87eb547e6e35/13-brand-paper-opt.png">View large version</a>)</figcaption></figure>

This black and white paper concept scaled down to the dialogs, scaled up to the <a href="https://www.businesscalendar.de/">website</a> and applied to almost every area of Business Calendar. It felt like the right dose of character, without interfering with personal colors and highlights.

But all of that changed when we got to onboarding. The user’s experience before installing the app felt dull and emotionless.

So, we brought back more branding and color into the mix. But something was still missing. Discussing the overall brand, we talked a lot about philosophies and influences. The Business Calendar team is based in Berlin, and we all care a lot about our hometown. This became the last piece of the branding puzzle for areas where we had plenty of space to work with and little text.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57a5d9d8-6bab-44cb-92cb-0e0768dd5ddc/14-brand-photos-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98c3acc5-9aa0-4f1a-825e-b13b53205031/14-brand-photos-opt-small.jpg" alt="Great background photographs of Berlin were the missing link in the branding experience." /></a><figcaption>Great background photographs of Berlin were the missing link in the branding experience. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57a5d9d8-6bab-44cb-92cb-0e0768dd5ddc/14-brand-photos-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5e99605-7450-42d9-b242-a7fd7d741301/15-brand-logo-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a86fd7-d734-4aa4-9107-32151402428d/15-brand-logo-opt-small.png" alt="Logo redesign, from concepts and ideas to exploration to the final design." /></a><figcaption>Logo redesign, from concepts and ideas to exploration to the final design. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5e99605-7450-42d9-b242-a7fd7d741301/15-brand-logo-opt.png">View large version</a>)</figcaption></figure>

### Evaluation and Learning

Bringing brand recognition to an app that is already used by millions of people is anything but usual, and it was a real challenge for us.

To avoid alienating existing users, we first looked at every element outside of the user’s control (such as the Google Play store promotion and the onboarding experience). From there, we carefully pushed small branding details into the core experience. It doesn’t seem like much in the finished app, but all of that exploration and effort to make sure each decision covered every user-customized edge case was relatively expensive. We learned that every application developer should invest in a solid, flexible brand system early on.

A last note. When we started the redesign, Google’s material design guidelines weren’t even introduced yet. We took their heavy focus on the paper metaphor as a sign that we were on the right track with our design decisions.</p>

## Distribution, Launch, Revenue

There are just two ways to develop software: publish a new product or update an existing one. New territory brings excitement and suspense: Whom are we addressing? How many people will use the product? What will the general perception be?

When relaunching a product, distinct questions come into play. How many new users will we reach, and how many existing ones will we lose? How will users perceive the changes? Will they love or hate the update? This pressure is especially high if you’ve dramatically updated the whole app, rather than just fixed a couple of bugs. So, how do you launch a redesign that minimizes risks <em>and</em> generates sufficient revenue?

### The Double-App Model

For the last four years, Business Calendar had been distributed through Google’s Play store as two apps: a free version and a pro version with a more extensive feature set. It’s an established model, but it became a burden to update two apps all the time.

So, what does a relaunch model that reaches a sufficient number of new users look like? Could we convert free users to support our development by paying for pro features? The problem is that solid numbers on app publishing are very hard to come by, so we had almost nothing to build on besides our own judgment and experience.</p>

### Strategy and Implementation

We considered three scenarios.

The first was to publish Business Calendar 2.0 as a classic update for the free and pro version.

*   **Pro**: We would keep the current publishing schedule, and existing users would be familiar with the process. The app would keep its high ranking in the Play store.
*   **Con**: We would still need to update two apps regularly. Users who don’t like the redesign would be left out.

The second scenario was to replace the free and pro version with Business Calendar 2.0, but add upgrades via in-app purchases.

*   **Pro**: We would simplify the release and support process immensely, offering more options to monetize development in the long run.
*   **Con**: Existing users might not like the new version and leave Business Calendar for an alternative.

The third scenario was to keep both versions in the Play store for a while and release Business Calendar 2.0 separately, with in-app purchases.

*   **Pro**: Old and new users would be able to choose which app to use, and no one would be left behind.
*   **Con**: We would have to update all three apps for a period of time, and users would possibly be overwhelmed and not understand the differences. Also, this strategy could result in losing a high spot in the ranking and search results.

Debating on all of these and other strategies for weeks, we ultimately decided on option three, even though it meant additional work. Because we had worked on almost every aspect of the app, the possibility of alienating existing users was just too high.

With that decision made, we created a framework to support in-app purchases and the support websites. We created four packages for our users to select from:

*   dark theme and extended customization,
*   advanced event management,
*   tasks,
*   all of the above and some extras.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3dc6977-45cd-4ad7-bf71-04f14b82b922/19-launch-iap-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0227f50d-3c80-4692-af40-45c3b1a2a74f/19-launch-iap-opt-small.png" alt="In-app purchases allowed us to concentrate on and maintain only one app, instead of a free and pro version." /></a><figcaption>In-app purchases allowed us to concentrate on and maintain only one app, instead of a free and pro version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3dc6977-45cd-4ad7-bf71-04f14b82b922/19-launch-iap-opt.png">View large version</a>)</figcaption></figure>

We froze features, leaving four weeks to test the product, with an extensive open beta through Google+. The feedback was positive throughout, but the more we got, the more bugs emerged. Still, we wanted to keep the deadline before Christmas. So, Business Calendar 2.0 launched worldwide in the Play store on December 24th.</p>

### Evaluation and Learning

We realized that launching in late December wasn’t the perfect decision, but we certainly underestimated how little people care about new apps, especially calendars, around Christmas. The download and update numbers after launch could have been better, as could have the various rankings in the Play store.

Additionally, the forced release date brought along plenty of bugs, which annoyed new users, who in return made their voices heard on the various comment and rating platforms — understandably. We clearly realized that a slightly longer development cycle would have been the smarter decision — for the development team and for users alike.

Fortunately, the bad numbers climbed quickly in early 2015, as the team kept improving the app and squishing bugs. Business Calendar 2 reached much better positions in the Play store, resulting in higher downloads and conversion numbers.</p>

### Some Numbers

No one usually shares these, but we’ll do it anyway:

*   A month before the new release, there were 170,000 downloads in Germany. A month after the release, downloads increased to over 250,000.
*   As of June 2015, almost 46,000 pro users have installed upgrade packages to support development, although they were offered a free upgrade.
*   Sales increased by 59% in the last six months (compared to six months before the release). Without taking the upgrades into account, the sales are significantly lower.
*   Influence in Play store rankings is something to consider when launching a new app with a different model. A day before the relaunch, the old app ranked 6 in a search for “calendar.” One month after the relaunch, the new app came in at 71 (that’s despite 250,000 downloads, 32,000 on the first day alone).</p>

## Conclusion

All too often we forget that applications are built by real people with opinions, ideals and fears. When a whole company is formed around a single product that’s about to get relaunched, there’s a lot of tension — after all, these people rely on that product’s success for their own financial security.

As of now, we won’t say that the relaunch strategy of Business Calendar 2 was a clear success. Six months in, the numbers are solid for a new release, but the next twelve will show whether all of the work proved valuable for this particular product.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61f22a15-8087-4f6b-a329-c24d1eaf3815/20-conclusion-desk-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/011ad9fd-6b40-43ce-a7e8-68f38c9550c5/20-conclusion-desk-opt-small.jpg" alt="The redesign was complex and protracted, because we deliberately did things the long, hard, stupid way" /></a><figcaption>The redesign was complex and protracted, because we deliberately did things the long, hard, stupid way. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61f22a15-8087-4f6b-a329-c24d1eaf3815/20-conclusion-desk-opt.jpg">View large version</a>)</figcaption></figure>

This redesign was complex and protracted, in part because we deliberately did things the <a href="https://vimeo.com/59384516">long, hard, stupid way</a> in order to get the best results. Then, there were all the parts of the redesign and development that we left out of this article: the redesign of task management, the finer interaction details, the onboarding process, the website development, and the intricate multi-part support system, to name a few. We’re sharing this story because everyone’s standing on the shoulders of giants and this is our small contribution to better information design thinking. We hope we’ve learned enough in this project to make you a little smarter, so that you can make us smarter in turn. Thank you.

{{< signature "da, ml, al" >}}

