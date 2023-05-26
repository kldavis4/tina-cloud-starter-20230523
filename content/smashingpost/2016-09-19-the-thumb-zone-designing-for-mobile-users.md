---
title: 'The Thumb Zone: Designing For Mobile Users'
slug: the-thumb-zone-designing-for-mobile-users
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/190a7e11-24c2-4bd2-acd0-530662e259b2/swipe-movements-500-opt.png
date: 2016-09-19T17:28:26.000Z
author: samanthaingram
summary: >-
  If there is one thing that will stand the test of time, it’s thumb placement on mobile devices. This makes consideration of the "thumb zone", a term coined in Steven Hoober’s research, an important factor in the design and development of mobile interfaces.
description: >-
  If there is one thing that will stand the test of time, it’s thumb placement on mobile devices. This makes consideration of the "thumb zone", a term coined in Steven Hoober’s research, an important factor in the design and development of mobile interfaces.
categories:
  - Usability
  - iOS
  - UX
  - Android
---
Have you ever interacted with a mobile website or app that <strong>simply didn’t play nice with your thumbs</strong>? Perhaps you’ve had to stretch to get to an important menu, or swiping turned into a battle with multiple swiping elements. Mishaps such as these reveal poor consideration of the thumb zone.

In this article, I will share the knowledge I’ve acquired about the thumb zone and how to apply its rules to navigation, cards and swipe gestures.

## Learning From The Best

As mentioned, Steven Hoober researched and wrote about the thumb zone in <em>Designing Mobile Interfaces</em>. This is where I first encountered the notion that it might be important to consider thumbs while developing.

Along with Hoober, Josh Clark has recorded in-depth information on how people hold their devices in his book <em>Designing for Touch</em>. You can read an <a href="https://alistapart.com/article/how-we-hold-our-gadgets">excerpt on A List Apart</a>.

Using Hoober and Clark’s study of how thumbs interact on devices, I performed user testing on wireframes that varied the location of design elements. My tests ran with navigation elements on the top and bottom of the screen, cards with buttons in different locations, and gesture areas outside and inside the thumb zone.

My test results validated Hoober and Clark’s research, while providing solid evidence of what works and what doesn’t in design. Below, I’ll share my findings on the design elements I tested. Let’s get started!

{{% feature-panel %}}

## Thumbs Vs. Touchscreens

Opposable thumbs are nice to have, aren’t they? In addition to making us way cooler than jellyfish, thumbs are also key to how we interact with our mobile touchscreen devices. Hoober’s research shows that 49% of people hold their smartphones with one hand, relying on thumbs to do the heavy lifting. Clark took this even further and determined that 75% of interactions are thumb-driven.

With this understanding of hand placement, we can conclude that certain zones for thumb movement apply to most smartphones. We’ll define them as easy-to-reach, hard-to-reach and in-between areas.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/496f7bc0-4c6c-4159-b731-ec3adcf91105/thumb-zone-mapping-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/496f7bc0-4c6c-4159-b731-ec3adcf91105/thumb-zone-mapping-opt.png" alt="Thumb-zone mapping of left- and right-handed users." width="650" height="420" /></a><figcaption>Thumb-zone mapping for left- and right-handed users. The "combined" zone shows the best possible placement areas for most users. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/496f7bc0-4c6c-4159-b731-ec3adcf91105/thumb-zone-mapping-opt.png">View the large version</a>).</figcaption></figure>

The trick is to design for the flow of the thumb zone. This provides a framework for making better design decisions, creating human-friendly experiences and getting fewer headaches. Through user testing and experimentation, I’ve discovered a few ways to use this knowledge in everyday development.

### Problems With Navigation

We all remember a time when mobile navigation was simply a dropdown list of links. It wasn’t pretty, but it got the job done. Today, we see endless examples of <a href="https://www.nngroup.com/articles/mobile-navigation-patterns/">navigation patterns</a>. What’s the best fit for the thumb zone?

The natural movement of the user is the first thing I learned to take into account. Ask questions: "Does my app have a long list of links?" "Do I need to mix menus?" "What goes well with my website design?" The answers to these questions will help you determine where to place navigational triggers and hooks.

If your app has a long list of links, then you’ll probably want to use a <a href="https://speckyboy.com/2014/08/12/fullscreen-responsive-menus/">full-screen overlay</a> menu. This type of menu affords space for you to organize the list, social buttons and other useful content. The pattern scales well between desktop and mobile devices, and the menu provides an opportunity to align clickable elements within the thumb zone.

<a href="https://www.hugeinc.com/">Huge</a> has always made great use of full-screen overlay menus on mobile devices:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/301bb91b-9d4b-4fe3-a8e2-cbbbf7b99a5c/huge-full-screen-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef6cfd4d-0cef-4abd-8132-14d87d5fa23a/huge-full-screen-500-opt.png" alt="Huge’s full-screen overlay menu" width="250" height="" /></a><figcaption>Huge uses a full-screen overlay menu. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/301bb91b-9d4b-4fe3-a8e2-cbbbf7b99a5c/huge-full-screen-opt.png">View large version</a>)</figcaption></figure>

On the flip side, if your app does not have a long list of links, then a sticky menu might be best. This type of menu attaches to the top or bottom of the screen and provides real estate for many links, depending on the design.

<a href="https://www.airbnb.com/mobile">Airbnb’s mobile app</a> has a sticky menu, attached to the bottom of the screen, providing easy access to important booking, messaging and listing information:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b60ab8ba-659a-4df5-8a74-14b96563b85f/airbnb-app-fixed-nav-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abe6c232-979a-4fdd-8c68-1180f4d84306/airbnb-app-fixed-nav-500-opt.png" alt="Airbnb mobile app fixed footer menu" width="250" height="" /></a><figcaption>Airbnb’s mobile app has a fixed footer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b60ab8ba-659a-4df5-8a74-14b96563b85f/airbnb-app-fixed-nav-opt.png">View large version</a>)</figcaption></figure>

If you have a large website, mixing menus might work. Because mixing menus can get complex, it’s helpful to prioritize menu links based on their importance in the app. Sticky menus are great for commonly visited links, whereas full-screen and drawer menus come in handy for important but not high-priority links.

Consider <a href="https://www.facebook.com/mobile/">Facebook’s mobile app</a>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ac5b12b-5852-4861-8515-c75fdde337a2/facebook-app-combined-menus-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0c33e6a-4073-4699-9181-67fb3cca321a/facebook-app-combined-menus-500-opt.png" alt="Thumb zone mapping of left- and right-handed users." width="250" height="" /></a><figcaption>Facebook’s mobile app combines multiple fixed menus and drawers. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ac5b12b-5852-4861-8515-c75fdde337a2/facebook-app-combined-menus-opt.png">View large version</a>)</figcaption></figure>

Facebook mixes menus based on the size of content within them. In the screenshot above, we see two sticky menus, each containing valuable links for the user. The top sticky menu is in the stretch zone, but just low enough on the page that it feels natural. The bottom sticky menu items are organized to provide comfortable tapping of popular links.

By gathering user data, practicing good design and leveraging the thumb zone, Facebook is owning sticky menus. The next time you’re trolling your friend’s posts, remember the series of decisions that have made your trolling experience that much better.

Remember that in addition to keeping important navigation items within the thumb zone, placing links outside of the friendly zone is acceptable at times. The general rule is to keep frequently used links in the easy-to-reach zone and to keep infrequently used links in the hard-to-reach zone.

{{% ad-panel-leaderboard %}}

### Keeping Cards Friendly

Next, we’re going to review how a well-designed card pattern can work for your app. The <a href="https://thenextweb.com/dd/2015/11/16/why-cards-are-dominating-mobile-design">card pattern</a> has been widely used for a while now. Cards are quick, easy and predictable; they provide bursts of information in small doses, making it easy to deliver the right content at the right time.

Often, we couple cards with actions: send, save, done, close, etc.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0da4b2af-fada-4631-a35f-f57ed96819a8/poncho-card-actions-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0cf86c8-de3a-4897-9987-945f8fac1757/poncho-card-actions-500-opt.png" alt="Poncho weather app card with actions" width="250" height="" /></a><figcaption>Ponch: Wake Up Weather’s card pattern (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0da4b2af-fada-4631-a35f-f57ed96819a8/poncho-card-actions-opt.png">View large version</a>)</figcaption></figure>

In this example we see the <a href="https://poncho.is/">Poncho: Wake Up Weather</a> app. This is a great example of placing actionable links within a card: The weather report doesn’t require a thumb tap, so it’s placed way inside the unreachable zone. The action item — in this case, a share button — is placed directly in the natural zone.

On the other side, Poncho places its "location search" and "use current location" links far inside the hard-to-reach zone. This is acceptable: A user would use those features infrequently, because the app remembers your location from the last time it was open.

On the flip side, there are times when card patterns don’t utilize the thumb zone. A prime example of this is <a href="https://www.etsy.com/mobile/">Etsy’s mobile app</a>. During checkout, Etsy provides a form in a popup card for the user to enter their shipping information:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3742b839-a1bf-40dd-aeb8-8cb28ff17a0d/etsy-card-actions-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f66d34bd-ebda-4123-8e57-393f5be5b8ec/etsy-card-actions-500-opt.png" alt="Esty checkout flaws" width="250" height="" /></a><figcaption>Etsy’s checkout flaws in the card pattern. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3742b839-a1bf-40dd-aeb8-8cb28ff17a0d/etsy-card-actions-opt.png">View large version</a>)</figcaption></figure>

At first glance, this use of a card seems appropriate and design-savvy. Digging deeper, we see flaws. The first problem is the "Cancel" link in the top-left corner. Does that link close the card or cancel the checkout process (if I'm confused, others surely will be, too). Also, The "x" is at the edge of the thumb zone, forcing the user to stretch to reach it.

Here’s a dilemma: Adding a close button to a top corner of a card is a common pattern, but it goes against the thumb zone rubric. If you’re breaking out of the thumb zone to meet a user’s expectations, look for an alternative solution. We could experiment by adding a close button at the bottom of the card, or — since cards are best when delivering short bursts of content — we could try limiting the length of content in cards.

As the card design fad takes hold, it’s a good idea to run designs through the thumb zone map to ensure that most elements are easily accessible and not confusing. Avoid following trends; instead, make human-oriented decisions throughout the design and development of your app.

{{% ad-panel-leaderboard %}}

### Gestures and Movement

<a href="https://thenextweb.com/dd/2015/11/09/how-to-implement-gestures-into-your-mobile-design">The gesture</a>: tap, double-tap, swipe, drag, pinch and press. These are the icing on the smartphone cake. Gestures enable us to engage with technology through our sense of touch.

You might be able to guess where this going. Keep gestures within the thumb zone. More importantly, allow the user to perform gestures naturally. This seems obvious, but to really pull off a comfortable experience, it’s important to calculate where the gesture should happen.

Let’s focus on the swipe interaction. Through <a href="https://blog.blakesimpson.co.uk/read/51-swipe-js-detect-touch-direction-and-distance">swipe-tracking scripts</a>, I found some really interesting movement data.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d29ee60-dbfe-4575-a282-21e250d870a9/swipe-movements-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d29ee60-dbfe-4575-a282-21e250d870a9/swipe-movements-opt.png" alt="Map of swipe movements" width="650" height="413" /></a><figcaption>Visualization of swipe-gesture data found during user testing. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d29ee60-dbfe-4575-a282-21e250d870a9/swipe-movements-opt.png">View large version</a>)</figcaption></figure>

In the map above, circles represent taps, and arrows represent swipes. The data that I collected from tests show that users usually swipe somewhere from the device’s edge towards the middle, diagonally downward. I also found that users generally swipe in the natural area of the thumb zone.

Originally, I had the misconception that users swipe horizontally across, which created problems when measuring thumb areas for swipe gestures. My design specifications did not provide enough room to swipe without triggering another swipe area simultaneously. As with most mobile design elements, consider the thumb space required for swiping. I’ve found an appropriate size of swipe areas to be at least 45 pixels tall and wide.

With all of this information, we can conclude that it’s better to place swipe-gesture actions in easy-to-reach areas, while also allowing enough space to prevent accidental inputs.

A great example of the swipe gesture is <a href="https://itunes.apple.com/us/app/inbox-by-gmail-new-email-app/id905060486?mt=8">Google’s Inbox app</a>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/510c8257-e179-4b47-beba-08ba62633e17/swipe-zone-google-inbox-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49e8fe73-9257-421d-94a8-50ab8aa37f76/swipe-zone-google-inbox-500-opt.png" alt="Google Inbox swipe areas" width="250" height="" /></a><figcaption>Google Inbox supports swipe gestures in the right places, with the right amount of space. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/510c8257-e179-4b47-beba-08ba62633e17/swipe-zone-google-inbox-opt.png">View large version</a>)</figcaption></figure>

The smart decisions here are:

*   keep swipe gestures out of hard-to-reach areas;
*   provide enough tapping space;
*   allow swipes to start anywhere in each email block element.

With all of this, gestures feel natural and comfortable, making email management faster and less complicated. Keep on keepin' on, Google!

## Summary

What have we learned? Hopefully, you better understand why the thumb zone is important. Remember these points:

*   Mobile devices and languages will change, but as long as there are touchscreens, the thumb zone will remain a critical part of design.
*   Navigational design is thumb-friendly when important links are in the easy-to-reach zone and unimportant links are in the hard-to-reach zones.
*   Cards are a powerful design asset when content and actions are thumb zone-friendly.
*   Determining swipe gesture areas becomes simpler when we consider how a person thumb swipes against a glass screen.

### Useful Links

I’ll leave you with this: Keep reading! There is much to learn from other people in the industry. Below are a few links on the subject of designing for humans:

*   [Thumb zone template](https://smashingmagazine.com/provide/thumb-zone-psd.zip) (PSD)
*   [_Designing for Touch_](https://abookapart.com/products/designing-for-touch), Josh Clark
*   [_Designing Mobile Interfaces_](https://shop.oreilly.com/product/0636920013716.do) Steven Hoober
*   "[Designing for Thumbs – The Thumb Zone](https://blog.usabilla.com/designing-thumbs-thumb-zone/)," Oliver McGough
*   [Check the thumb!](https://thumbzone.co/) Nicolás J. Engler & Antonela Debiasi
*   "[One-Handed Mobile Interface](https://medium.com/@konsav/-55aba8ed3859#.mf1j05vv7)," Konstantin Savchenko, Medium
*   "[How Do Users Really Hold Mobile Devices?](https://www.uxmatters.com/mt/archives/2013/02/how-do-users-really-hold-mobile-devices.php)," Steven Hoober, UXmatters
*   "[Facebook Paper’s Gestural Hell](https://scotthurff.com/posts/facebook-paper-gestures)" Scott Hurff
*   "[Designing for Large Screen Smartphones](https://www.lukew.com/ff/entry.asp?1927)," Luke Wroblewski

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Mobile-First Is Just Not Good Enough: Meet Journey-Driven Design](https://www.smashingmagazine.com/2017/02/mobile-first-is-just-not-good-enough-meet-journey-driven-design/)
*   [<span class="headline">Designing Card-Based User Interfaces</span>](https://www.smashingmagazine.com/2016/10/designing-card-based-user-interfaces/)
*   [Beyond The Button: Embracing The Gesture-Driven Interface](https://www.smashingmagazine.com/2013/05/gesture-driven-interface/)

{{< signature "da, yk, al, il" >}}

