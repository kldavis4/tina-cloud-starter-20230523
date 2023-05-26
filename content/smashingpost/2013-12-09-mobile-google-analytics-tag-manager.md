---
title: How To Simplify Mobile App Data With Google Analytics And Tag Manager
slug: mobile-google-analytics-tag-manager
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee876b6-05f9-46dd-a542-3566ff3bbc97/mobile-analytics-app-illu.jpg
date: 2013-12-09T13:41:17.000Z
author: andrew-thomas
description: >-
  Information about customers has never been available on the scale it is today.
  Businesses are learning new ways to leverage data to improve themselves on a
  daily basis. They’re realizing that data collection and data analysis have a
  measurable return on investment, and decision-makers are asking to see them.
categories:
  - Mobile
  - Apps
  - Marketing
  - Analytics
  - Analysis
---
Information about customers has never been available on the scale it is today. Businesses are learning new ways to leverage data to improve themselves on a daily basis. They’re realizing that data collection and data analysis have a measurable return on investment, and decision-makers are asking to see them.

As a developer, business owner or marketer, you need to know how to gather data and how to do it efficiently and in a scalable way. Furthermore, <strong>you need to understand what that data means</strong> and how to present it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Is Your Responsive Design Working? Google Analytics Will Tell You](https://www.smashingmagazine.com/2014/08/responsive-web-design-google-analytics/)
*   [A Guide To Google Analytics And Useful Tools](https://www.smashingmagazine.com/2009/07/a-guide-to-google-analytics-and-useful-tools/)
*   [Keep Your Analytics Data Safe And Clean](https://www.smashingmagazine.com/2012/04/keep-your-analytics-data-safe-and-clean/)
*   [Enabling Multiscreen Tracking With Google Analytics](https://www.smashingmagazine.com/2014/11/enabling-multiscreen-tracking-with-google-analytics/)
*   [How To Use Analytics To Build A Smarter Mobile Website](https://www.smashingmagazine.com/2014/03/how-to-use-analytics-to-build-a-smarter-mobile-website/)

Two free tools to know about are Google Analytics and Google Tag Manager. When used together, they put the power in the hands of the marketers and data geeks, while freeing developers from the burden of constant marketing-driven updates.

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0323b872-5845-4173-9a90-73e1c5170a44/mainanalyticsscreenshot-large-opt.png"><img loading="lazy" decoding="async" class="size-large wp-image-139648" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9b8a934-4cd7-4bdc-bf14-827faf34c3c0/mainanalyticsscreenshot-500-opt.png" alt="Main Analytics Screenshot" width="500" height="262" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0323b872-5845-4173-9a90-73e1c5170a44/mainanalyticsscreenshot-large-opt.png">View large version</a>)</em>

Google Analytics is a widely known and well-respected system for gathering user data. Almost all developers have come across it, and all marketers have at least heard of it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29c30339-86c0-40f8-8894-a9c62e0fa507/maintagmanagerscreenshot-large-opt.png"><img loading="lazy" decoding="async" class="size-large wp-image-139649" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c9a5fff-adc4-458e-ae58-d7567d9ac382/maintagmanagerscreenshot-500-opt.png" alt="Main Tag Manager Screenshot" width="500" height="262" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29c30339-86c0-40f8-8894-a9c62e0fa507/maintagmanagerscreenshot-large-opt.png">View large version</a>)</em>

Google Tag Manager is a relatively new system in which all of the different Google code snippets for a website or mobile application can be organized and controlled through a drag-and-drop interface in a Web browser. In the time it normally takes to add Analytics tracking code to a mobile application, developers can add Tag Manager code instead, and then the Tag Manager’s “container” may be updated with any code snippets and tracking services that Google offers individually.

For this article, we’ll talk about adding Google Analytics to a mobile application, using the very future-proof Google Tag Manager to implement it.</p>

## Before We Begin

Google Analytics and Google Tag Manager are two separate services, each complex. Understanding the difference between the two and being clear on how they work together is important.</p>

### What Are the Tags We’ll Be Managing?

We can track a lot of things in applications right now. Beyond Analytics, we have AdWords conversions and AdWords remarketing, as well as the configurations and customizations of each service.

Traditionally, each service and customization has required new code to be implemented, but Tag Manager allows you to control all of that through an interface in a Web browser. This just makes sense for everyone’s workflow. Google hopes it will soon be the industry standard.

In short, tags are the different kinds of tracking that you might want to add, remove, try out or tweak, and they’re all controlled through the Tag Manager container.</p>

### Google Analytics Is A Tag

Google Tag Manager is what you would add to your application, but you’d still need to create a Google Analytics account to track and organize all of that information about the app and its users.

You’ll need to add your Analytics account as a tag within Tag Manager. Then, in the future, you (or anyone else) can add or tweak any additional tags or settings that you want.</p>

### Wait, Why Is This Important?

Imagine that you’re the head of marketing and your company is launching a new product or service. Your app has been updated and is awaiting approval from the app store, and marketing materials have been queued and are waiting to get pushed out to your customers. On launch day, your boss asks how the new feature is performing. You pull up the analytics and find that something is wrong with the data. It could be a little tracking nuance that you didn’t account for, data that doesn’t paint a complete picture or even a development bug. With a traditional analytics setup, you’re at the mercy of your development team and all of the various app stores that need to approve changes to code. With Tag Manager, you can make that fix instantly and get your reporting squared up in minutes instead of days.

Likewise, if your boss unexpectedly asks which search ads are driving the most downloads, you can add the AdWords tag through Tag Manager and start seeing results right away. To put it simply, <strong>Tag Manager enables marketers to be agile</strong>.

Let’s get started.</p>

## Set Up Analytics

If you’re totally new to Analytics, then there’s a lot to learn and read. We won’t cover that here, but I do want to be thorough and complete, and a few tips will save you headaches down the road. <a href="https://www.google.com/analytics/learn/index.html">Google has more information</a> on getting started.

When setting up Analytics, be aware of general best practices for tracking application data through the service.

One concept that is good to understand initially is how to work with client accounts and multiple users. An analytics account has an owner, but it’s shared with various users. So, create the Analytics property through your client’s Google account (if you have a client), and add yourself and anyone on your team as users.

Setting up your app property correctly for future growth is also important. <a href="https://support.google.com/analytics/answer/2587087">Google shares some best practices.</a>

Now, if you haven’t done so already:

1.  Create a Google account.
2.  Go to Google Analytics, and click or tap “Access Analytics.”
3.  Create a new account. Accounts may hold many properties, and users of an account will have access to all properties in that account.
4.  Create a property in the account (make sure it’s a “mobile app” property, not a “website” property).
5.  Go to the “Admin” section and, in the “Property” column, click “Property Settings.”
6.  Find and record that tracking ID (you’ll need it for Tag Manager).</p>

## Set Up Tag Manager

Separate from the Analytics account, we need to create a Tag Manager account. Here are the steps:

1.  Go to [Google Tag Manager](https://www.google.com/tagmanager), and sign in with your Google account.
2.  Click or tap “New Account,” and name it something related to your app.
3.  Create a container. You’ll need one container per app, and you would add a new one only if you made a significant update that changes the tracking data.

Now that both services are set up, it’s time to connect them and start tracking. First, make sure your application is set up with all of the initial Tag Manager stuff. Google offers an SDK and instructions for both iOS and Android that include all of the Tag Manager code and files that you’ll need, with additional Analytics stuff built in. Just follow the instructions.

*   [Google Tag Manager SDK for iOS](https://developers.google.com/analytics/devguides/collection/ios/v2/)
*   [Google Tag Manager SDK for Android](https://developers.google.com/analytics/devguides/collection/android/v2/)

## Get Everything Talking to Each Other

The next step is to add a tag for Analytics in the Tag Manager interface. This is actually several steps.</p>

### Create the Tag

First, navigate to the <a href="https://www.google.com/tagmanager/">Tag Manager interface</a>. We’ll create the tag for Analytics — that is, we’ll add Analytics to our Tag Manager container, which will interact with the app through that initial code that you implemented with the Tag Manager SDK. When you drill down into your container in the Tag Manger interface in a Web browser, you’ll start off with a message telling you that you have no tags and to “click here” to create one. Either click there or click the tag icon near the top right in the row of icons.

Enter a name, like “Analytics App View” (which is to say, basic analytics tracking), select “Universal Analytics” from the drop-down menu, and enter the tracking ID from the Analytics configuration a minute ago. Set the “Track Type” drop-down menu to “App View.”

You can save now, and your tag will be created. But we’re not done yet. So far, <strong>we have a tag, but it will never fire unless we tell it when to fire</strong>, using a rule.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e0ce551-765e-42a4-9a39-95fcc48eed1d/tagmanager-tag-large-opt.png"><img loading="lazy" decoding="async" class="size-large wp-image-139521" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cbb6816-c89f-464f-854f-f316eabf51e2/tagmanager-tag-500-opt.png" alt="" width="500" height="262" /></a><br>
<em>(<a>View large version</a>)</em>

### Create a Rule

Tag Manager for apps comes with one rule built in. It’s called “Always,” which basically means “when true equals true” — in other words, always. We’ll set the Analytics App “View” tag to fire “always.”

If you’re not already looking at your newly created Analytics tag, click the tag name to edit it. A little ways down, you’ll see “Firing Rules.” Click to add one, and choose Google’s prebuilt “Always” rule. Now your tag is ready to fire.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e71926d-1849-415b-9f61-f488f78bd1c1/tagmanager-firingrule-large-opt.png"><img loading="lazy" decoding="async" class="size-large wp-image-139522" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e464848-f83d-4cea-9be3-04204f80602f/tagmanager-firingrule-500-opt.png" alt="" width="500" height="262" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e71926d-1849-415b-9f61-f488f78bd1c1/tagmanager-firingrule-large-opt.png">View large version</a>)</em>

### Publish

We’re almost there. The last step is to publish to your container — that is, to let the application know that you’ve made changes to the tags that Tag Manager is managing.

First, click or tap that “Create a Version” button in the top-right corner. This will “lock in” your current configuration and archive it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11f45056-75bf-4da7-b785-46d42c4924b8/tagmanager-createversion-large-opt.png"><img loading="lazy" decoding="async" class="size-large wp-image-139529" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8f67856-d375-4979-89ed-57427acbdc82/tagmanager-createversion-500-opt.png" alt="Tag Manager Create Version" width="500" height="262" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11f45056-75bf-4da7-b785-46d42c4924b8/tagmanager-createversion-large-opt.png">View large version</a>)</em>

Now that your version has been created, you’ll see that the “Create a Version” button has become a “Publish” button, and a “Preview” button has appeared to the left of it. Google’s preview is pretty advanced, so try it out. It’s pretty self-explanatory.

If you like what you see in the preview, hit “Publish.” If everything has gone off without a hitch, then <strong>you’re now tracking Analytics data from your application</strong>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b9dabfb-5d27-4524-868b-0e96eb764919/tagmanager-publish1-large-opt.png"><img loading="lazy" decoding="async" class="size-large wp-image-139530" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11fad9ea-15c1-46b3-bd84-bd739e2bbdca/tagmanager-publish1-500-opt.png" alt="Tag Manager Publish" width="500" height="262" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b9dabfb-5d27-4524-868b-0e96eb764919/tagmanager-publish1-large-opt.png">View large version</a>)</em>

## Now For The Data!

Now that you have Tag Manager in place and you’ve added Analytics to your Tag Manager container, you’re finally ready to start analyzing all of that data that you’ll be collecting. Below is a quick explanation of the main information that Google Analytics offers.

We’ll start with the default “App Overview” screen.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dac3906-f869-4a98-9ba5-5004d3601368/analytics-appoverview-large-opt.png"><img loading="lazy" decoding="async" class="size-large wp-image-139534" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bd6ee05-ee2c-4182-a745-28d28ca70243/analytics-appoverview-500-opt.png" alt="Analytics App Overview" width="500" height="698" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dac3906-f869-4a98-9ba5-5004d3601368/analytics-appoverview-large-opt.png">View large version</a>)</em>

First, access your <a href="https://www.google.com/analytics/">Analytics account</a> and click through to your property. Once you get to your dashboard, you’ll see a few key metrics, organized for you by Google. This is your “App Overview.” Default report shortcuts include “New Users,“ “Active Users,” “Country / Territory,” “Top Device Models,” “Engagements,” “Screens,” “Goals” and “In-App Revenue.”

<strong>Initially, the most interesting data will be about the users.</strong> Analytics shows you how many users have installed and come back to your app, which screens of your app they see and which devices they use. If this is the first time you’re using Analytics, then you’re finally seeing exactly how people use your app! Amazing!

### New Users

The “New Users” section shows not only new users, but active users and user sessions. Users are broken down by operating system (you can track the same app across multiple operating systems in one Analytics property), app version and geography.

If you’re just getting used to viewing Analytics data, then this particular section will be one of the most useful. It makes it easy to tell what’s going on with your app’s usage at a glance.</p>

### Active Users

Active users are similar to new users, but the metrics here dive a little deeper and there are more of them. You’ll see some high-level information about screens and more about sessions.

I spend a lot of time in this section, especially early on. Here it’s easy to tell what’s going on with your app. Before you get into more advanced tracking through conversion funnels and specific events, you should <strong>get a broad picture of what users do with your app</strong>. The concepts and terminology are simple, but the implications and insights are huge.

Similar to a page view in Analytics for websites, a screen view can generate an immense amount of information about users and how they use your application. A “screen” represents a literal screen or view in your app, and Google knows how to track screens automatically, without additional configuration on the developer’s part (beyond implementing the original Tag Manager and Analytics code).

The reason I mention that Google knows how to track screens automatically is that Analytics goes far beyond tracking common data with a predetermined interface. But that’s another topic. For now, we’ll stick to the built-in tracking.

A session is similar to a visit in website analytics, and it represents the duration of the user’s session across one or many screens. <strong>By analyzing sessions, you will know when and where users are getting confused</strong>, at which points you should add sales messaging or ads, and what your most popular features are.

Below the screen and session data, on the left side of the main content area, lies a submenu that’s easy to miss. I missed it at first myself. (Google Analytics’ interface is always improving, and understanding the product is a challenging undertaking and so will take a little getting used to.) The submenu starts off with “Language” selected, but check out the other options in the list for some more high-level data about users.

At this point, you’re probably already making some interesting connections and assumptions from your data. I’ll keep going through the other default reports, and then I’ll touch on the exciting next steps you can take to more advanced tracking.</p>

### Country / Territory

“Country / Territory” gives geographical information via a heat map that shows where your most active users are concentrated. With the drop-down menu in the upper-left corner, which defaults to “Sessions,” you can display any other metric on the map by geographic density.

I’ve noticed that in the business world, the “suits” seem to love this sort of graphical analysis. In an instant, it “tells a story.” Screenshots of this kind of graphic-based data go a long way in internal and external presentations.</p>

### Top Device Models

This one’s pretty self-explanatory, but clicking through gives you insight into more than just device models. It touches on screen resolution, whether the user’s device is a touchscreen, and device branding. It also includes a donut graph for at-a-glance analysis.

Depending on the type of application, your users and their habits, and your own goals for your application, “Top Device Models” could be extremely relevant or completely useless.

It will be <strong>relevant if you want to know which devices to focus development on</strong>. Knowing whether you’re getting more sales from tablets or from phones is important.

It’s much less useful if your app is only on the iPhone. Sure, you’d see which iPhones your users have, but that might not matter all that much to your return on investment.</p>

### Engagements

“Engagements” shows you more information about screens and sessions, but with some valuable additional metrics, such as crash reports and events. Crash reports are self-explanatory and invaluable if your app crashes. Events are likely the next thing you’ll learn about once you understand all of Analytics’ basics.

The things you can do with events is where Analytics starts to get really fun.</p>

### Screens

“Screens” gives you detailed metrics for each screen. Of course, a lot of the information we’ve been looking at relates to screens anyway, but that’s because screens are the basis for most basic tracking. It makes sense that screen views permeate Analytics’ entire interface. In the screens report, you’ll see things such as which screens are the most viewed, how long users spend on each screen and which screens cause users to exit.

If you want to really tailor the user experience, then the details in this view are important. You can and should control every aspect of your application, and with this information, you can start to visualize how people flow through your application and where to optimize and guide that process.</p>

### Goals

You can do so much with Analytics, and goal reporting is just the beginning. Because goals are very specific to your company and your mobile application, a broad explanation wouldn’t do this section justice. At a very basic level, goals involve setting up event listeners and then combining the tracking of those events into “funnels.” A funnel normally ends with a conversion, such as a purchase or registration, and by tracking events that lead to conversions, you can <strong>get a great idea of whether and where users are getting confused</strong> or discouraged. This requires additional configuration, but you’ll get some powerful insight by tracking non-screen-change actions as events. By chaining them together into conversion funnels, the sky is the limit on the insight you can gain.</p>

### In-App Revenue

“In-App Revenue,” like goals, gets a bit specific to each mobile app. Some apps, such as brand-building apps, don’t generate any type of revenue, and so this section wouldn’t be relevant. If your app has any type of sales or e-commerce, though, then you can track and analyze many more metrics, some of which will truly improve your bottom line.</p>

### Time Frames

Once you understand the meaning of all of these numbers and graphs, you’ll probably want to know the period of time covered by a given set of data. In the top-right corner, the date-range selector defaults to the last month, not including today.

Select any date range you want. Choose from presets such as “Today” and “Last Week,” or select a range manually. Once you click “Apply,” the time period will carry through to all of the reports until you change it or close the window.</p>

## What’s Next?

Those are the basics, but keep exploring. The next things to learn about are events, shortcuts and dashboards.</p>

### Events

Events and goal-tracking are the next logical step after screen-tracking, because events enable you to track more specific actions. Get started on the <a href="https://support.google.com/analytics/answer/1033068?hl=en">help page for Google Analytics events</a>.</p>

### Shortcuts

Shortcuts are saved snapshots of reports that you can customize or create from scratch. After you get used to the reports that Google provides, you’ll find yourself changing the same things every time you need to see data that is specific to your business. This means that it’s time to create a shortcut. Just press the “Shortcut” button in the top toolbar of the report that you want to save, and then you’ll be able to access that report at any time in the future.</p>

### Dashboards

Dashboards, then, are collections of reports and/or shortcuts. Similar to the “App Overview” screen, here you can create your own custom dashboard layouts and save them. Better yet, you can share these custom dashboards with members of your team. Create a board for your CEO with big-picture metrics, and create a separate view for developers that focuses on crashes and errors. Share them with the people who need the information. They’ll thank you for the data and the interface’s ease of use.</p>

## Moving Into The Future

As with any complex undertaking, understanding the basics of Analytics and starting with a smart configuration can make learning faster and easier. In this article, we wanted to give you insight into Google Analytics for apps but, more importantly, to present an efficient and versatile configuration and workflow, so that once you understand the main concepts, you’ll be set up to grow.

Google Tag Manager and similar products are the way of the future. Because Tag Manager enable us to add code to our application only once, <strong>anyone with account access can change tags and tracking information on the fly</strong>, without modifying the original code. This means that changes in a data collection system can be made more quickly and more easily. It also means that A/B testing happens faster and with less pushback, and that last-minute campaigns can be tracked at will.

Before Tag Manager, developers had to change the tracking code for every update to Analytics, and then app stores had to approve those changes. Thus, changes were infrequent, and sometimes mistakes wouldn’t get corrected for a week. That all changed with Tag Manager for apps.

Take advantage of it.

{{< signature "al, ea" >}}

