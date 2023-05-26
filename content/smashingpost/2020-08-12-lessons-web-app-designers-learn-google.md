---
title: '4 Lessons Web App Designers Can Learn From Google'
slug: lessons-web-app-designers-learn-google
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eac1975-cebe-4b97-8d13-01e212282245/lessons-web-app-designers-learn-google.png
date: 2020-08-12T10:30:00.000Z
summary: >-
  There’s a reason why Google dominates market share for things like search engines, web browsers, email clients and cloud storage services. It knows exactly what consumers want and it has designed simple, intuitive, and useful solutions for them. If there’s one company whose product features you should be mirroring, it’s Google.
description: >-
  Google knows exactly what consumers want and it has designed simple, intuitive, and useful solutions for them. This article explains why it’s a company whose product features you should be mirroring.
categories:
  - UX
  - Product Strategy
  - Apps
  - UI
---

Whenever I’m curious about what more we could be doing to improve our users’ experiences, the first place I look to is Google. More specifically, I go to the Google Developers site or Think with Google to pull the latest consumer data. 

But I was thinking today, *“Why don’t we just copy what Google does?”*

After all, Google *has* to walk the walk. If not, how would it ever convince anyone to adhere to its SEO and UX recommendations and guidelines? 

The only thing is, Google’s sites and apps aren’t very attractive. They’re practical and intuitive, that’s for sure. But designs worth emulating? Eh. 

That doesn’t really matter though. The basic principles for building a good web app exist across each of its platforms. So, if we’re looking for a definitive answer on what will provide SaaS users with the best experience, I think we need to start by dissecting Google’s platforms.

## What Google Teaches Us About Good Web App Design

What we want to focus on are the components that make Google’s products so easy to use time and time again. By replicating these features within your own app, you’ll effectively reduce (if not altogether remove) the friction your users would otherwise encounter. 

{{% feature-panel %}}

### 1. Make the First Thing They See Their Top Priority

When users enter your dashboard, the last thing you want is for them to be overwhelmed. Their immediate impression whenever they enter your app or return to the dashboard should be: 

*“I’m exactly where I need to be.”*

Not: 

*“What the heck is going on here? Where do I find X?”*

Now, depending on the purpose of your app, **there are usually one or two things your users are going to be most concerned with.**

Let’s say you have an app like [Google Translate](https://translate.google.com/) that has a clear utilitarian purpose. There’s absolutely no excuse for cluttering the main page. They’ve come here to do one thing: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdc4495-d28d-4b6b-907a-904bd9301130/google-translate-dashboard.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdc4495-d28d-4b6b-907a-904bd9301130/google-translate-dashboard.png" sizes="100vw" caption="Google Translate users don’t have to hunt around for the translator tool. (Source: <a href='https://translate.google.com/'>Google Translate</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdc4495-d28d-4b6b-907a-904bd9301130/google-translate-dashboard.png'>Large preview</a>)" alt="Google Translate translator tool" >}}

So, don’t waste their time. Place the tool front and center and let all other pages, settings or notices appear as secondary features of the app. 

Something else this example teaches us is how you should configure your tool for users. Google could easily just leave this open-ended, but it defaults to: 

**Default Language —> English**

Google’s data likely shows that this is the most popular way users use this app. 

Although you can’t see it in the desktop app, you can see it on mobile. The formula goes like this: 

**Default Language —> Recent Language**

I suspect that, for first-time users, Google will set the translation to the user’s native language (as indicated in their Google user settings).  

If you have the data available, use it to configure defaults that reduce the number of steps your users have to take, too.

Not every web app provides users with a hands-on tool for solving a problem. In some cases, apps enable users to streamline and automate complex processes, which means their primary concern is going to be how well those processes are performing. 

For that, we can look at a product like [Google Search Console](https://search.google.com/search-console/about), which connects users to data on how their sites perform in Google search as well as insights into problems that might be holding them back. 

It’s no surprise then that the first thing they see upon entering it is this: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04a7228f-1fa6-473d-9e65-c24756b20dd9/google-search-console-overview.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04a7228f-1fa6-473d-9e65-c24756b20dd9/google-search-console-overview.png" sizes="100vw" caption="The Google Search Console overview page shows users stats on Performance and Coverage. (Source: <a href='https://search.google.com/search-console/about'>Google Search Console</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04a7228f-1fa6-473d-9e65-c24756b20dd9/google-search-console-overview.png'>Large preview</a>)" alt="Google Search Console overview - Performance and Coverage stats" >}}

Performance (the number of clicks in Google search) and Coverage (number of pages indexed without error) are above the fold. Below it is another chart that displays recommended enhancements to improve core web vitals, mobile usability and sitelinks searchbox visibility. 

Bottom line: The Overview page isn’t littered with charts depicting every data point collected by Google Search Console. Instead, it displays only the top priorities so users can get a bird’s-eye view of what’s going on and not get lost in data they don’t need at that time. 

{{% ad-panel-leaderboard %}}

### 2. Create a Useful and Simple Navigation Wherever Relevant

This one seems like a no-brainer, but I’ll show you why I bring it up. 

[Zoom](https://zoom.us/) is a great video conferencing app. There’s no arguing that. However, when users want to schedule a meeting from their browser, this is what they see:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee382bb-43e2-45d6-8682-3509a06c9cb8/zoom-navigation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee382bb-43e2-45d6-8682-3509a06c9cb8/zoom-navigation.png" sizes="100vw" caption="The Zoom web app complicates things with multiple menus. (Source: <a href='https://zoom.us/'>Zoom</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee382bb-43e2-45d6-8682-3509a06c9cb8/zoom-navigation.png'>Large preview</a>)" alt="Zoom in-browser web app with multiple menus to choose from" >}}

The “Join Meeting” and “Host Meeting” options are fine as they both eventually push the user into the desktop app. However, the “Schedule Meeting” in-browser experience isn’t great because it leaves the website navigation bars in place, which only serves as a distraction from the app’s sidebar on the left.

Once your users have created a login and have access to your app, they don’t need to see your site anymore. Ditch the website navigation and let them be submersed in the app. 

Or do as [Google Hangouts](https://hangouts.google.com/) does. Lay your app out the way users expect an app to be laid out: 

- Primary navigation along the left side, 
- Hamburger menu button and/or More (...) button contain the secondary navigation,
- Wide open space for users to play in the app.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a6af75-68b2-443f-88be-114fe115fe91/google-hangouts-simple-navigation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a6af75-68b2-443f-88be-114fe115fe91/google-hangouts-simple-navigation.png" sizes="100vw" caption="A look inside Google Hangouts and its distraction-free interface and navigation. (Source: <a href='https://hangouts.google.com/'>Google Hangouts</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a6af75-68b2-443f-88be-114fe115fe91/google-hangouts-simple-navigation.png'>Large preview</a>)" alt="Google Hangouts distraction-free interface and simple navigation" >}}

But Google Hangouts doesn’t do away with the google.com website completely. For users that want to quickly navigate to one of Google’s other products, they can use the grid-shaped icon in the top-right corner. So, if you feel it’s necessary for your users to be able to visit your website once again, you can build it into the app that way. 

This example also demonstrates how important it is to keep your navigation as simple as possible. 

Google Hangouts’ primary navigation uses symbols to represent each of the app’s tabs/options: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35f0a643-816f-4949-bf51-6d886e9b19d0/google-hangouts-main-navigation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35f0a643-816f-4949-bf51-6d886e9b19d0/google-hangouts-main-navigation.png" sizes="100vw" caption="Google Hangouts uses icons to represent the tabs of its primary navigation. (Source: <a href='https://hangouts.google.com/'>Google Hangouts</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35f0a643-816f-4949-bf51-6d886e9b19d0/google-hangouts-main-navigation.png'>Large preview</a>)" alt="Google Hangouts primary navigation design - icons only" >}}

While I think it’s okay for Google Hangouts to get away with this icon-only menu design, be careful with this approach. Unless the icons are universally understood (like the hamburger menu, search magnifying glass, or the plus sign), you can’t risk introducing icons that create more confusion. 

[As NNG points out](https://www.nngroup.com/articles/icon-usability/), there’s a difference between an icon being recognizable and its meaning being indisputable. 

So, one way you can get around this is to make the outward appearance of the menu icon-only. But upon hover, the labels appear so that users have additional context for what each means.

As for any secondary navigation you might need &mdash; including a Settings navigation &mdash; you can write out the labels since it will only appear upon user activation. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/812581ce-773d-4db6-9d73-f78d2db6902f/google-hangouts-seconary-navigation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/812581ce-773d-4db6-9d73-f78d2db6902f/google-hangouts-seconary-navigation.png" sizes="100vw" caption="The Google Hangouts secondary navigation uses an icon and label for each tab. (Source: <a href='https://hangouts.google.com/'>Google Hangouts</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/812581ce-773d-4db6-9d73-f78d2db6902f/google-hangouts-seconary-navigation.png'>Large preview</a>)" alt="Google Hangouts secondary navigation design - icons and labels" >}}

Although some of the icons would be easy enough to identify, not all of them would instantly be recognizable (like “Invites” and “Hangouts Dialer”). If even one tab in your secondary navigation is rarely seen across other apps, spell them all out. 

One last thing: The divider lines in this menu are a great choice. Rather than jam 10 tabs/options into this navigation bar together, they’re logically grouped, making it easier for users to find what they’re looking for. 

{{% ad-panel-leaderboard %}}

### 3. Provide Users with Predictive Search Functionality

Every app should have a search bar. It might be there to help users sift through content, to find the contact they’re looking for from a long list, or to ask a question about something in the app. 

The more complex your app is, the more critical a role internal search is going to play. But if you want to improve your users’ search experience even more, you’ll want to power yours with predictive search functionality. 

Even though I’m sure you have a Support line, maybe a chatbot and perhaps an FAQs or Knowledgebase to help users find what they need, a smart search bar can connect them to what they’re really looking for (even if they don’t know how to articulate it).

Google has this search functionality baked into most of its products. 

You’re familiar with autocomplete within the Google search engine itself. But here are some other use cases for smart search capabilities. 

[Google Drive](https://drive.google.com/) connects users to documents (of all types &mdash; Docs, Sheets, Slides and more) as well as collaborators that match the search query. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a602f8-a203-44a4-b1eb-c237f8daac2c/google-drive-search-matches.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a602f8-a203-44a4-b1eb-c237f8daac2c/google-drive-search-matches.png" sizes="100vw" caption="An example search for 'speed' within Google Drive. (Source: <a href='https://drive.google.com/'>Google Drive</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a602f8-a203-44a4-b1eb-c237f8daac2c/google-drive-search-matches.png'>Large preview</a>)" alt="Google Drive search for 'speed'" >}}

Users can, of course, be taken to a full search results page. However, the search bar itself predicts which content is the most relevant for the query. In this case, these are the most recent pieces of content I’ve written that include the term “speed” in the title. 

[Google Maps](https://www.google.com/maps/) is a neat use case as it pulls data from a variety of connected (Google) sources to try and predict what its users are looking for. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e31cc9a-7764-47c5-a72b-22b6cf38ab17/google-maps-predictive-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e31cc9a-7764-47c5-a72b-22b6cf38ab17/google-maps-predictive-search.png" sizes="100vw" caption="Google Maps pulls from a variety of sources to predict where users want to travel to. (Source: <a href='https://www.google.com/maps/'>Google Maps</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e31cc9a-7764-47c5-a72b-22b6cf38ab17/google-maps-predictive-search.png'>Large preview</a>)" alt="Google Maps predictive search example 'Alicia'" >}}

In this example, I typed in “Alicia”. Now, Google Maps knows me pretty well, so the first result is actually the address of one of my contacts. The remaining results are for addresses or businesses within a 45-mile radius containing the word “Alicia”. 

It doesn’t just pull from there though. This is one of those cases where the more enjoyable you make the in-app experience, the more your users will engage with it &mdash; which means more data. 

For example, this is what I see when I search for “Three”: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8955d41-7aca-489e-88a2-d2bc9e8009fd/google-maps-search-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8955d41-7aca-489e-88a2-d2bc9e8009fd/google-maps-search-example.png" sizes="100vw" caption="Google Maps will provide 'Favorite' locations in search results when relevant. (Source: <a href='https://www.google.com/maps/'>Google Maps</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8955d41-7aca-489e-88a2-d2bc9e8009fd/google-maps-search-example.png'>Large preview</a>)" alt="Google Maps displays a 'Favorite' location when a user searches for 'three'" >}}

The very first thing it pulls up is a restaurant called Three Sisters (which is a fantastic restaurant in the city of Providence, by the way). If you look just above the center of the map where the red heart is, that’s the restaurant. This means that I’ve added it to my Favorite places and Google Maps actually calls it out as such in my search results. 

Imagine how much more your users would love your app if it wasn’t always a struggle to get to the content, data or page they were looking for. *Or* to perform a desired action. When you give your users the ability to personalize their experience like this, use the information they’ve given you to improve their search experience, too. 

### 4. Enable Users to Change the Design and Layout of the App

As a designer, you can do your best to design a great experience for your users. But let’s face it: 

You’re never going to please everyone. 

Unlike a website, though, which is pretty much what-you-see-is-what-you-get, SaaS users have the ability to change the design and layout of what they’re interacting with &mdash; if you let them. And you should. 

There are many different ways this might apply to the app you’ve built. 

[Google Calendar](https://calendar.google.com/), for example, has a ton of customization options available. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b47be41-e1b7-4a82-a728-b1a36682263a/google-calendar-customization.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b47be41-e1b7-4a82-a728-b1a36682263a/google-calendar-customization.png" sizes="100vw" caption="Google Calendar allows users to customize the look and view of their calendars. (Source: <a href='https://calendar.google.com/'>Google Calendar</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b47be41-e1b7-4a82-a728-b1a36682263a/google-calendar-customization.png'>Large preview</a>)" alt="Google Calendar - view customizations" >}}

On the far left is a list of “My calendars”. Users can click which calendars and associated events they want to see within the app. 

In the bottom-right corner is an arrowhead. This enables users to hide the Google apps side panel and give them more room to focus on upcoming events and appointments. 

In the top-right, users have two places where they can customize their calendar: 

- The Settings bar allows them to adjust the color and density of the calendar. 
- The “Month” dropdown allows them to adjust how much of the calendar is seen at once.

These customizations would all be useful for any sort of project management, planning or appointment scheduling app.

For other apps, I’d recommend looking at [Gmail](https://mail.google.com/). It’s chock full of customizations that you could adapt for your app. 

Previously, if users clicked the Settings widget, it would move them out of the app and into the dedicated settings panel. To be honest, it was annoying, especially if you just wanted to make a small tweak. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eed3901-40d8-4e54-9577-cf769ff31882/gmail-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eed3901-40d8-4e54-9577-cf769ff31882/gmail-settings.png" sizes="100vw" caption="Gmail’s Settings reveals a list of design and layout customization options. (Source: <a href='https://mail.google.com/'>Gmail</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eed3901-40d8-4e54-9577-cf769ff31882/gmail-settings.png'>Large preview</a>)" alt="Gmail Settings panel - design and layout customization options" >}}

Now, the Settings button opens this panel within Gmail. It enables users to adjust things like: 

- Line spacing, 
- Background theme, 
- Inbox sorting priorities,
- Reading pane layout,
- Conversation view on/off.

This is a recent update to Gmail’s settings, which probably means these are the most commonly used design customizations its users actually use. 

For any customizations users want to make that they can’t find in this new panel, they can click “See all settings” and customize the in-app design and layout (among other things) even further.  

Other customizations you might find value in enabling in your app are: 

- Keyboard control, 
- Dark mode, 
- Color-blind mode,
- Text resizing, 
- List/grid view toggling, 
- Widget and banner hiding,
- Columns displayed.

Not only do these design and layout controls enable users to create an interface they enjoy looking at and that works better for their purposes, it can also help with accessibility. 

## Wrapping Up

There’s a reason why Google dominates market share with many of its products. It *gets* the user experience. Of course, this is due largely to the fact that it has access to more user data than most companies. 

And while we should be designing solutions for our specific audiences, there’s no denying that Google’s products can help us set a really strong base for any audience &mdash; if we just pay attention to the trends across its platforms. 

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Is Your Website Stressing Out Visitors?'" href="https://www.smashingmagazine.com/2020/06/website-stressing-out-visitors/" rel="bookmark">Is Your Website Stressing Out Visitors?</a></li>
<li><a title="Read 'Equivalent Experiences: Thinking Equivalently'" href="https://www.smashingmagazine.com/2020/06/equivalent-experiences-part2/" rel="bookmark">Equivalent Experiences: Thinking Equivalently</a></li>
<li><a title="Read 'Accessible Images For When They Matter Most'" href="https://www.smashingmagazine.com/2020/05/accessible-images/" rel="bookmark">Accessible Images For When They Matter Most</a></li>
<li><a title="Read 'How To Convince Others Not To Use Dark Patterns'" href="https://www.smashingmagazine.com/2020/05/convince-others-against-dark-patterns/" rel="bookmark">How To Convince Others Not To Use Dark Patterns</a></li>
</ul>

{{< signature "ra, yk, il" >}}
