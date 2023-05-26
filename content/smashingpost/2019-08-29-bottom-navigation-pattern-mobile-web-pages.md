---
title: 'Bottom Navigation Pattern On Mobile Web Pages: A Better Alternative?'
slug: bottom-navigation-pattern-mobile-web-pages
author: arthur-leonov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53cbd3db-8aa1-4a3d-8874-3215c36caec9/bottom-navigation-pattern-mobile-web-pages.png
date: 2019-08-29T13:30:59+02:00
summary: >-
  As our phones are getting bigger, we need to adjust how we build and design our websites. Is there something to learn from app design and tap bars? Can we fix the mobile navigation of our websites to have a lower interaction cost? In this article, we’ll find out.
description: >-
  As our phones are getting bigger, we need to adjust how we build and design our websites. Is there something to learn from app design and tap bars? Can we fix the mobile navigation of our websites to have a lower interaction cost? In this article, we’ll find out.
categories:
  - Responsive Design
  - Mobile
  - Navigation
  - Design Patterns
  - Web Design
  - Best Practices
---
Whenever you hear of “mobile navigation”, what’s the first thing that comes to mind? My guess would be the hamburger slide-out menu. This design pattern had been in use since the first responsive design days, and even though a lot has changed since then, this particular pattern has not. Why is that?

How did we start using the top navigation with the hamburger menu in the first place? Is there a better alternative? In this article, I will try to explore these questions.

## The History Of The Top Navigation And The Hamburger

The first hamburger menu icons started appearing in the '80s. It was designed by [Norm Cox](https://www.coxhall.com/bio.html) for the Xerox Star &mdash; the world’s first graphical user interface. He also designed the document icon for the same interface.  This piece of history was uncovered by [Geof Allday](https://www.evernote.com/shard/s207/client/snv?noteGuid=022f2237-4b4f-4096-87f2-053acd228c2d%C2%ACeKey=ede2672bc3f39a1b0232f84e01ca0a83&utm_campaign=buffer&utm_medium=social&sn=https%3A%2F%2Fwww.evernote.com%2Fshard%2Fs207%2Fsh%2F022f2237-4b4f-4096-87f2-053acd228c2d%2Fede2672bc3f39a1b0232f84e01ca0a83&title=The%2Borigin%2Bof%2Bthe%2Bhamburger%2Bicon&utm_content=buffer84840&utm_source=twitter.com) (who actually emailed Norm Cox). You can read the whole email response by [clicking here](https://www.evernote.com/shard/s207/client/snv?noteGuid=022f2237-4b4f-4096-87f2-053acd228c2d&noteKey=ede2672bc3f39a1b0232f84e01ca0a83&utm_campaign=buffer&utm_medium=social&sn=https%3A%2F%2Fwww.evernote.com%2Fshard%2Fs207%2Fsh%2F022f2237-4b4f-4096-87f2-053acd228c2d%2Fede2672bc3f39a1b0232f84e01ca0a83&title=The%2Borigin%2Bof%2Bthe%2Bhamburger%2Bicon&utm_content=buffer84840&utm_source=twitter.com). Later, it was seen on [Windows 1](https://disq.us/url?url=https%3A%2F%2Fyoutu.be%2FxnudvJbAgI0%3Ft%3D517%3AX7KggVkynoPbUxYhv8CFGXKquno&cuid=2647992) &
and [DOS](https://twitter.com/ftrain/status/724440969697984512).

The current mobile navigation &mdash; as we know it &mdash; was popularized by Ethan Marcotte’s “Responsive Web Design” book back in 2011. Since then, the top navigation and the hamburger became the industry’s standard.

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/61556918#t=1265s" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

## The Mobile Phone Screen Size Doubled In 10 Years

Since the original iPhone, mobile sales [have been increasing year after year](https://www.statista.com/statistics/271491/worldwide-shipments-of-smartphones-since-2009/). 2019 is the first year that the market reached saturation point and the sales have started to decrease. But that doesn’t mean people are not using phones. By 2020, we will spend 80% of our time on the Internet on mobile phones, [reports Quartz](https://qz.com/1116469/we-now-spend-70-of-time-online-on-our-phones/) and [Ciodive](https://www.ciodive.com/news/70-of-internet-traffic-comes-from-mobile-phones/510120/). Compare that to 2010, when only a fourth of Internet users were phone-based.

**As phone sales increased, screen sizes have more than doubled, too.** The average screen size of smartphones has increased from 3.2 inches all the way to 5.5 inches. In 2017, device makers started to adopt the taller 18:9 aspect ratio with 5.7-inch and 6-inch 18:9 displays. Now, we are starting to see 6-inch 18:9 displays become the new standard in flagships as well as in the mid-range price segments, as they have more screen area than 5.5-inch 16:9 displays, [XDA-Developers reports.](https://www.xda-developers.com/consumers-spending-more-time-larger-devices/)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23c5a28-9809-446c-8778-4c6d8f5073d9/1-screen-size-trends-bottom-navigation-pattern.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23c5a28-9809-446c-8778-4c6d8f5073d9/1-screen-size-trends-bottom-navigation-pattern.jpg" sizes="100vw" caption="An overview of how the mobile screen sizes have changed (Image source: <a href='https://www.scientiamobile.com/smartphone-screen-size-trend/'> ScientiaMobile) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23c5a28-9809-446c-8778-4c6d8f5073d9/1-screen-size-trends-bottom-navigation-pattern.jpg'>Large preview</a>)" alt="An overview of how the mobile scren sizes have changed" >}}

Basically, the mobile phone screen size is getting bigger and bigger. That’s fine, but how do we adapt our design patterns to reflect these changes?

{{% feature-panel %}}

## Thumb-Driven Design

I first heard of the term “thumb-driven design” from Vitaly Friedman. It’s based on the [Steven Hoober](https://www.uxmatters.com/mt/archives/2017/03/design-for-fingers-touch-and-people-part-1.php)'s and [Josh Clark](https://alistapart.com/article/how-we-hold-our-gadgets/)’s research on how people hold their devices.

The gist of it is that in nearly every case, three basic grips were most common. 49% held their phones with a one-handed grip, 36% cradled the phone in one hand and jabbed with the finger or thumb of the other, and the remaining 15% adopted the two-handed BlackBerry-prayer posture, tapping away with both thumbs, states Josh Clark. Steven Hoober had found that 75% of users touch the screen with only one thumb. Hence, the term *thumb-driven design*.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f0815c0-6891-4de2-b932-fbe1b0804130/2-phone-grip-bottom-navigation-pattern.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df58fba6-21c8-4b45-956d-57b9064279da/phone-grip-bottom-navigation-pattern-2.jpg" sizes="100vw" caption="There are three main ways in which we hold our phones. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f0815c0-6891-4de2-b932-fbe1b0804130/2-phone-grip-bottom-navigation-pattern.jpg'>Large preview</a>)" alt="There are three main ways in which we hold our phones" >}}

In 2016, Samantha Ingram wrote an article named “[The Thumb Zone: Designing For Mobile Users](https://www.smashingmagazine.com/2016/09/the-thumb-zone-designing-for-mobile-users/)” which further explores these ideas. She defined *easy-to-reach*, *hard-to-reach* and *in-between* areas.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c6eb97b-25f0-4bc7-8c33-1e6364f753d9/3-thumb-zone-mapping-bottom-navigation-pattern.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c6eb97b-25f0-4bc7-8c33-1e6364f753d9/3-thumb-zone-mapping-bottom-navigation-pattern.png" sizes="100vw" caption="Thumb-zone mapping <a href='https://www.smashingmagazine.com/author/samanthaingram/'>explained by Samantha Ingram</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c6eb97b-25f0-4bc7-8c33-1e6364f753d9/3-thumb-zone-mapping-bottom-navigation-pattern.png'>Large preview</a>)" alt="Thumb-zone mapping explained by Samantha Ingram" >}}

However, I would argue, that with increasing phone sizes, the mapping has shifted a bit:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e059ce1c-665f-4b0b-8d7e-571ffcc8d8d8/4-new-thumb-zone-mapping-bottom-navigation-pattern.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e059ce1c-665f-4b0b-8d7e-571ffcc8d8d8/4-new-thumb-zone-mapping-bottom-navigation-pattern.jpg" sizes="100vw" caption="New thumb-zone mapping adjusted to larger screen sizes (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e059ce1c-665f-4b0b-8d7e-571ffcc8d8d8/4-new-thumb-zone-mapping-bottom-navigation-pattern.jpg'>Large preview</a>)" alt="New thumb-zone mapping adjusted to larger screen sizes" >}}

When the phones were small, most areas were easy to reach. As our screens got bigger, the top part became virtually impossible to touch without adjusting your phone. From the example above, we can see where the most expensive screen real estate is. Yet, it’s often neglected on web pages. **How can we fix this?**

## Bottom Navigation Pattern

Every now and then, bottom navigation pattern pops up on the web. The idea itself is quite simple: **move the navigation bar further down**.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb56153-96e4-4a03-a385-9e2d05bcbb9f/5-slack-bottom-nav-bottom-navigation-pattern.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb56153-96e4-4a03-a385-9e2d05bcbb9f/5-slack-bottom-nav-bottom-navigation-pattern.jpg" sizes="100vw" caption="Slack web page navigation reimagined with new thumb-zone mapping (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb56153-96e4-4a03-a385-9e2d05bcbb9f/5-slack-bottom-nav-bottom-navigation-pattern.jpg'>Large preview</a>)" alt="Slack web page navigation reimagined with new thumb-zone mapping" >}}

Positioning the navigation bar at the bottom makes it easier for users to click on the menu icon, while secondary items can be moved to the top. Basically, you simply switch the order. Mobile apps have been using this logic with the tap bar pattern. It’s not a new idea in itself, but it’s still not as popular in web design as it is in app design.

This is not a foolproof solution since it raises a few critical questions, but it’s a worthy alternative. Let’s explore some of the questions that may come up.

{{% ad-panel-leaderboard %}}

## Primary And Secondary Items

As the top of the screen is becoming hard to reach, placing the primary menu items closer to the bottom is a better alternative. But what about the other things that are just as important?

I propose two ideas to tackle this problem:

1. Placing the search bar or any non-primary items to the top;
2. CTA buttons should remain at the bottom next to the menu items as it is a vital part of the navigation.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8f3080-80a5-4693-8022-b7594e0b894c/6a-primary-secondary-nav.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8f3080-80a5-4693-8022-b7594e0b894c/6a-primary-secondary-nav.jpg" sizes="100vw" caption="A wireframe of reimagined primary and secondary navigation items (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8f3080-80a5-4693-8022-b7594e0b894c/6a-primary-secondary-nav.jpg'>Large preview</a>)" alt="A wireframe of reimagined primary and secondary navigation items." >}}

## How Will This Affect Scrolling With Large Menus?

Some websites have extensive menus, submenus and everything in between.  Naturally, there will be scrolling involved.  How does flipping the primary/secondary items work in this scenario?

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbfeaae5-7ad0-4e19-9213-4af2d25743e3/7b-large-menu-wireframe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbfeaae5-7ad0-4e19-9213-4af2d25743e3/7b-large-menu-wireframe.jpg" sizes="100vw" caption="A wireframe of a reimagined large menu (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbfeaae5-7ad0-4e19-9213-4af2d25743e3/7b-large-menu-wireframe.jpg'>Large preview</a>)" alt="A wireframe of a reimagined large menu" >}}

Make the primary and secondary items (menu link, logo, search input) fixed while leaving the menu list scrollable. That way, your users will be able to reach the critical things they need.

## Where Do You Place The Logo?

You might have concerns about the logo placement. There are two ways to go about it:

- Placing the logo at the bottom might be a bit awkward, however, the thumb will most likely not obstruct it. It can be missed, though, as we tend to scan top to bottom.
- A more reasonable option is to keep the logo at the top of the page, but not to have it fixed. Make it a part of the content so it goes away as you scroll. That way, people will still be able to see it perfectly.

As you can see, I used the menu label in the wireframe. Kevin Robinson had found that [putting a label next to the icon increased engagement by 75%](https://medium.com/decoding-digital/optimising-mobile-web-navigation-2-recent-successes-8132c715f516):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21f4d17d-001c-4d18-81af-f1a16e017125/8a-logo-placement-wireframe.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21f4d17d-001c-4d18-81af-f1a16e017125/8a-logo-placement-wireframe.jpg" sizes="100vw" caption="A wireframe of the logo placed at the top while the menu can be found at the bottom. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21f4d17d-001c-4d18-81af-f1a16e017125/8a-logo-placement-wireframe.jpg'>Large preview</a>)" alt="A wireframe of the logo placed at the top while the menu can be found at the bottom" >}}

## How Does This Work With Handlebars?

Some operating systems and browsers tend to use the bottom area of the screen for their own purposes. [iOS handlebars ](https://webkit.org/blog/7929/designing-websites-for-iphone-x/)can get in the way of bottom navigation. Make sure the navigation is spacious enough to accommodate the iOS safe area.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c92750-8268-4144-97ac-65dbab93b06a/9a-ios-safe-area.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10eb560a-e42a-48a0-94f2-c5abb85caf57/9b-ios-safe-area.jpg" sizes="100vw" caption="iOS Handlebars and safe areas (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c92750-8268-4144-97ac-65dbab93b06a/9a-ios-safe-area.jpg'>Large preview</a>)" alt="iOS Handlebars and safe areas" >}}

If you place the logo dead in the center, the link might clash with the handlebar functionality. A bit of padding will do the trick.

## Will The Users Adjust To This Pattern Or Find It Disorentating?

As I was writing this article, I kept thinking of whether this would turn out into a big redesign or a simple usability improvement for users navigating through your website. After all, according to [Jakob’s Law](https://lawsofux.com/jakobs-law), users spend most of their time on other sites. This means that users prefer your site to work the same way as all the other sites they’re already familiar with.

As a counter-argument to Jakob’s Law, I would like to propose [Fitts Law](https://lawsofux.com/fittss-law). It argues that the time to acquire a target is a function of the distance and size of the target. Basically, the smaller and further away the target is, the higher the interaction cost. NN/g has a wonderful [video](https://www.nngroup.com/videos/fittss-law/) explaining this in more detail:

<figure class="video-container break-out"><iframe loading="lazy" src="https://www.youtube.com/embed/M-9FbUJk6tI" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<blockquote>“A bottom hamburger menu icon will have a much lower interaction cost compared to the top menu icon because it’s closer. By placing the menu CTA near the thumb, we are allowing the user to reach it’s end goal faster. Would the users find the feature disorientating if it lowers their interaction cost? Probably not.”</blockquote>

## How Will This Integrate With The Tap Bar Pattern?

A tap bar patterns lists three to five most common first-level actions to click on a single row. You may have seen it in popular apps and some websites:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d81602d-df47-4342-a30a-11fd4050b562/10-tap-bar-mengyuan-sun-bottom-navigation-pattern.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d81602d-df47-4342-a30a-11fd4050b562/10-tap-bar-mengyuan-sun-bottom-navigation-pattern.gif" width="800" alt="iOS Tap bar design by Mengyuan Sun" /></a><figcaption>Tap bar design by <a href="https://dribbble.com/shots/5309578-Tap-bar-animate">Mengyuan Sun</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d81602d-df47-4342-a30a-11fd4050b562/10-tap-bar-mengyuan-sun-bottom-navigation-pattern.gif">Large preview</a>)</figcaption></figure>

Hamburger menus have sparked *a lot* of controversy over the years. Just take a few moments to read [this article](https://lmjabreu.com/post/why-and-how-to-avoid-hamburger-menus/), and [this](https://uxplanet.org/alternatives-of-hamburger-menu-a8b0459bf994) one, and [this](https://techcrunch.com/2014/05/24/before-the-hamburger-button-kills-you/?guccounter=1) one, and most importantly, [this](https://www.nngroup.com/articles/hamburger-menus/) one. You’ll then understand why the tap bar became the preferred navigation pattern in mobile app design.

Nielsen argues that hidden navigation (hamburger menu) significantly [decreases user experience both on mobile and desktop](https://www.nngroup.com/articles/hamburger-menus/). On mobile, people used the hidden navigation in 57% of the cases, and the combo navigation in 86% of the cases, i.e. 1.5 times more! The combo navigation that Nielsen refers to is a tab bar pattern combined with a hamburger menu &mdash; here’s an example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc83b4a-76d6-4487-9788-83bd06baa158/11-tap-bar-with-hamburger-menu-bottom-navigation-pattern.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc83b4a-76d6-4487-9788-83bd06baa158/11-tap-bar-with-hamburger-menu-bottom-navigation-pattern.png" sizes="100vw" caption="The Samsung app example from Rizki Rahmat Ridha for <a href='https://medium.muz.li/3-good-reason-why-you-might-want-to-remove-that-hamburger-menu-from-your-product-69b9499ba7e2'>Muzli</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc83b4a-76d6-4487-9788-83bd06baa158/11-tap-bar-with-hamburger-menu-bottom-navigation-pattern.png'>Large preview</a>)" alt="Samsung app example from Rizki Rahmat Ridha for Muzli" >}}

It might seem like the tap bar is the perfect solution, but it has its problems too. [Fabian Sebastian](https://uxplanet.org/tab-bars-are-the-new-hamburger-menus-9138891e98f4) raised a good point that it only works on top-level views. It does not work with secondary navigation items. To solve this problem, a hamburger/tap bar hybrid was born. If you pay attention to the Samsung app, you’ll see that the last item on the menu is the “More” button which calls up the hamburger menu.

In essence, the bottom navigation pattern integrates quite well into the tap bar pattern if you want to combine both of them. The best place to look for good examples is in the mobile app world.

{{% ad-panel-leaderboard %}}

## Some Popular Websites Reimagined

I opened up Photoshop and did a quick mockup of a few popular websites in order to explain that **changing the navbar to go bottom-up is not that difficult**.

Let’s first take a look at [Bloomberg](https://www.bloomberg.com/):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cae96c3-e0ec-4a93-a602-f8fd583528db/12a-bloomberg-example.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cae96c3-e0ec-4a93-a602-f8fd583528db/12a-bloomberg-example.jpg" sizes="100vw" caption="The <a href='https://www.bloomberg.com/'>Bloomberg website</a> with a reimagined bottom navigation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cae96c3-e0ec-4a93-a602-f8fd583528db/12a-bloomberg-example.jpg'>Large preview</a>)" alt="Bloomberg website with a reimagined bottom navigation" >}}

Next, let’s take a look at [Invision](https://www.invisionapp.com/):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f76132c-07a7-4a89-a947-32766b4e45a0/13a-invision-example.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f76132c-07a7-4a89-a947-32766b4e45a0/13a-invision-example.jpg" sizes="100vw" caption="The <a href='https://www.invisionapp.com/'>Invision website</a> with a reimagined bottom navigation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f76132c-07a7-4a89-a947-32766b4e45a0/13a-invision-example.jpg'>Large preview</a>)" alt="Invision website with a reimagined bottom navigation" >}}

Last but not least, the good ol’ [Reddit](https://www.reddit.com/):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec449d40-5558-4681-8744-3613f7f6a631/14a-reddit-example.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec449d40-5558-4681-8744-3613f7f6a631/14a-reddit-example.jpg" sizes="100vw" caption="The Reddit website with a reimagined bottom navigation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec449d40-5558-4681-8744-3613f7f6a631/14a-reddit-example.jpg'>Large preview</a>)" alt="The <a href='https://www.reddit.com/'>Reddit website</a> with a reimagined bottom navigation" >}}

Yes, this idea does raise questions, but it’s simple enough to be adapted to the web. It does make a usability difference as the interaction cost is much lower.

## That Sounds Great, But How Do I Convince My Clients?

You, as the designer, might see the potential of this pattern, but what if your client or your boss doesn’t? I would answer this problem with a couple of arguments:

<ul>
	<li>Mobile apps have been placing valuable menu items to the bottom <em>for years</em> already. Just send them these two articles for starters:</li>
	<ul>
		<li>“<a href="https://www.smashingmagazine.com/2016/11/the-golden-rules-of-mobile-navigation-design/">The Golden Rules Of Bottom Navigation Design</a>,” written by <em>Nick Babich</em></li>
		<li>“<a href="https://www.nngroup.com/articles/mobile-navigation-patterns">Basic Patterns For Mobile Navigation: A Primer</a>,” written by <em>Raluca Budiu</em></li>
	</ul>
	<li>I had noticed cases in which popular mobile apps started to shift important bits to the bottom. A good example is <a href="https://www.uber.com/">Uber</a>. For them, the search bar is one of the most important items on the screen. In the old design, its position was at the top. Now, they’ve shifted it to the bottom. Could we be on to something here?</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d73bd6b0-73cf-4737-a05c-1ea810b577a2/15-old-new-uber-bottom-navigation-pattern.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d73bd6b0-73cf-4737-a05c-1ea810b577a2/15-old-new-uber-bottom-navigation-pattern.jpg" sizes="100vw" caption="The old and new Uber search bar design (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d73bd6b0-73cf-4737-a05c-1ea810b577a2/15-old-new-uber-bottom-navigation-pattern.jpg'>Large preview</a>)" alt="Old and new Uber search bar designs" >}}

Shifting important navigation items to the bottom is not a new thing in mobile app design. It’s just that &mdash; for some reason &mdash; the web industry has not caught up on this just yet.

## Summary

The facts are quite clear: Phones are getting bigger, and some parts of the screen are easier to interact with than others. Having the hamburger menu at the top provides too big of an interaction cost, and we have a large number of amazing mobile app designs that utilize the bottom part of the screen. Maybe it’s time for the web design world to start using these ideas on websites as well?

I understand that all of this is not a foolproof solution for all use cases, but it’s worth a shot. It helps make the experience just a tad bit better. I’m interested in hearing your thoughts below!

### Useful Reading Resources

- “[Why Not Have The Hamburger Menu At The Bottom?](https://ux.stackexchange.com/questions/67755/why-not-have-the-hamburger-menu-at-the-bottom),” Stack Overflow (Nov. 2014)
- “[The Genius — And Potential Dangers — Of The Hamburger Icon (Flyout Menu)](https://vtldesign.com/web-strategy/website-design-development/hamburger-icon-flyout-menu-website-navigation/),” Jesse Rand, Vital Design
- “[To Hamburger Or Not To Hamburger?](https://medium.com/digital-experience-design/to-hamburger-or-not-to-hamburger-aad8b4a07576),” Dan Nessler, Medium
- “[A Brief History Of The Hamburger Icon](https://blog.placeit.net/history-of-the-hamburger-icon/),” Antonio, Placeit blog
- “[Design For Fingers, Touch And People (Part 1)](https://www.uxmatters.com/mt/archives/2017/03/design-for-fingers-touch-and-people-part-1.php),” Steven Hoober, UXMatters
- “[Designing For Thumbs: The Thumb Zone](https://blog.usabilla.com/designing-thumbs-thumb-zone/),” Oliver McGough, Usabilla blog
- “[Why Mobile Menus Belong At The Bottom Of The Screen](https://uxmovement.com/mobile/why-mobile-menus-belong-at-the-bottom-of-the-screen/),” Anthony, UX Movement
- “[One-Handed Mobile Interface](https://medium.com/@konsav/-55aba8ed3859#.mf1j05vv7),” Konstantin Savchenko, Medium
- “[How Do Users Really Hold Mobile Devices?](https://www.uxmatters.com/mt/archives/2013/02/how-do-users-really-hold-mobile-devices.php),” Steven Hoober, UXmatters
- “[Facebook Paper’s Gestural Hell](https://scotthurff.com/posts/facebook-paper-gestures),” Scott Hurff
- “[Designing For Large Screen Smartphones](https://www.lukew.com/ff/entry.asp?1927),” Luke Wroblewski

### Further Related Resources

- [Windows1 (1985) PC XT Hercules](https://www.youtube.com/watch?v=xnudvJbAgI0&feature=youtu.be&t=517), the hamburger menu on Windows 1 (video)
- [Hamburger menu in DOS](https://twitter.com/ftrain/status/724440969697984512), as tweeted by Paul Ford
- “[Check The Thumb](https://thumbzone.co/)”, created by Nicolás J. Engler and Antonela Debiasi

{{< signature "cc, il" >}}
