---
title: How To Build Honest UIs And Help Users Make Better Decisions
slug: how-to-build-honest-uis-and-help-users-make-better-decisions
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b0eaac0-08e3-4720-8d32-2d99279909b5/google-disguised-ads-500-opt.png
date: 2016-10-19T18:05:16.000Z
author: graemefulton
description: >-
  Many apps today, such as Google Now, Spotify and Amazon, make assumptions
  about user preferences based on personal data. They may even use this
  information to make decisions on our behalf, without any direct input from us.
  For example, Facebook tailors your news feed and Amazon recommends products 
  —  both hiding "irrelevant" information and only showing what they _think_ you
  will like.

  This type of design pattern, where user choice is removed, has recently been
  coined "anticipatory design". Its aim is to leverage data on user behavior to
  automate the decision-making process in user interfaces. The outcome lowers
  the excessive number of decisions people currently make, thereby reducing
  decision fatigue and improving decisions overall.
categories:
  - UX
  - UX
  - UI
  - Design Patterns
  - Web Design
  - Best Practices
---
Many apps today, such as Google Now, Spotify and Amazon, make assumptions about user preferences based on personal data. They may even use this information to make decisions on our behalf, without any direct input from us. For example, Facebook tailors your news feed and Amazon recommends products — both hiding "irrelevant" information and only showing what they _think_ you will like.

This type of design pattern, where user choice is removed, has recently been coined "anticipatory design". Its aim is to leverage data on user behavior to automate the decision-making process in user interfaces. The outcome lowers the excessive number of decisions people currently make, thereby reducing decision fatigue and improving decisions overall.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why User Experience Cannot Be Designed](https://www.smashingmagazine.com/2011/03/why-user-experience-cannot-be-designed/)
*   [Effectively Planning UX Design Projects](https://www.smashingmagazine.com/2013/01/effectively-planning-ux-design-projects/)
*   [25 User Experience Videos That Are Worth Your Time](https://www.smashingmagazine.com/2010/01/25-user-experience-videos-that-are-worth-your-time/)
*   [Better User Experience With Storytelling](https://www.smashingmagazine.com/2010/01/better-user-experience-using-storytelling-part-one/)
*   [10 Principles Of Effective Web Design](https://www.smashingmagazine.com/2008/01/10-principles-of-effective-web-design/)

Despite the good intentions imbued in anticipatory design, though, automating decisions can implicitly raise trust issues — especially at a time when trust has been eroded through the use of [dark patterns](https://www.darkpatterns.org) in user interfaces. Therefore, in contrast to the deceitful dark patterns that are meant to trick users, this article will look at how we can give people confidence in the decisions made for them by using "light patterns," which ensure that user interfaces are honest and transparent, while even nudging users to make better decisions for themselves.

{{% feature-panel %}}

## First, Why Decide For Your User?

In today's online world, consumers face more options than ever before. For example, consider shopping in marketplaces such as Amazon and eBay. Even when we know exactly what we want (replacement Apple headphones, for example), the choice can still be overwhelming:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0f4a71-fce1-4959-8d80-109028256aac/1-a9vsf2gio4k005khhkooqg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9597eb8d-36ce-43b2-b7c4-64ea7e750217/1-a9vsf2gio4k005khhkooqg-500-opt.png" width="500" height="166" alt="Amazon and eBay overwhelming product choice" /></a><figcaption>The overwhelming number of options for the exact same product on Amazon and eBay (Images: <a href="https://amazon.co.uk">Amazon</a> and <a href="https://ebay.co.uk">eBay</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0f4a71-fce1-4959-8d80-109028256aac/1-a9vsf2gio4k005khhkooqg-opt.png">View large version</a>)</figcaption></figure>

Another example is all-you-can-eat music services, such as Spotify, which put huge amounts of music at our fingertips, with no extra cost to listen to more. The additional choices quickly add up:

<figure><div class="aspect-ratio">{{< vimeo 183290441 >}}<figcaption>The overwhelming choice of music on Spotify. (Image: <a href="https://spotify.com">Spotify</a>)&gt;</div></figure>

While more choice is welcome, too much can create a daunting experience for the user, because then actually making a decision becomes difficult. This problem has been highlighted extensively before, most notably by Barry Shwartz's paradox of choice and Hick's Law:

*   [Barry Shwartz's paradox of choice](https://www.ft.com/cms/s/9cebd444-cd9c-11de-8162-00144feabdc0,Authorised=false.html?siteedition=uk&_i_location=http%3A%2F%2Fwww.ft.com%2Fcms%2Fs%2F0%2F9cebd444-cd9c-11de-8162-00144feabdc0.html%3Fsiteedition%3Duk&_i_referer=&classification=conditional_standard&iab=barrier-app)  
    "Lots of choice makes people less likely to choose anything, and less happy when they do choose."
*   [Hick's law](https://www.smashingmagazine.com/2012/02/redefining-hicks-law/)  
    "Every additional choice increases the time required to take a decision."

Both studies suggest that by reducing the amount of choice in a user interface, we can improve a user's ability to make decisions, thereby reducing frustration and making the user experience better.

Articles about "decision fatigue" back this up, stating that making high numbers of decisions can cause people to be less effective at making the important decisions in life. That's why Mark Zuckerberg [wears the same style of clothes](https://www.independent.co.uk/news/people/why-mark-zuckerberg-wears-the-same-clothes-to-work-everyday-a6834161.html) every day:

<blockquote>
<p>I really want to clear my life to make it so that I have to make as few decisions as possible about anything except how to best serve this community.</p>
</blockquote>

## How To Reduce Choice

Reducing the number of choices for a user has, therefore, become the focus for many of today's apps. This has been done in a number of ways, two of which we'll discuss now.</p>

### Make Options More Relevant

Many products are personalized to individual preferences, limiting options only to those deemed relevant to the current user. This has been done famously by Amazon, both on its website and through tailored email recommendations based on data collected on customers:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39bb8afb-3801-4f6e-ad21-4e6168df4a9e/amazon-choice-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f6b6a9b-7c40-4fc0-8d67-6a6fc170ab15/amazon-choice-500-opt.png" width="500" height="221" alt="Tailored recommendations by Amazon" /></a><figcaption>Tailored recommendations by Amazon (Image: <a href="https://amazon.co.uk">Amazon</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39bb8afb-3801-4f6e-ad21-4e6168df4a9e/amazon-choice-opt.png">View large version</a>)</figcaption></figure>

### Anticipate Decisions

Recommendations such as those above might not be enough to reduce the difficulty of choice, because users are still faced with the many relevant options that have been filtered through. This is where products can go a step further by making decisions on the user's behalf, totally removing the burden of choice.

For example, apps such as [Google Now](https://www.google.co.uk/landing/now/) are increasingly carrying out actions for users, without any direct user input:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1560780-49a2-478d-866e-c7764f7060ff/google-now-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e22f194-6070-4e39-a770-d3ab65804808/google-now-500-opt.png" width="500" height="261" alt="Google Now anticipatory design examples" /></a><figcaption>Examples of anticipatory design in Google Now (Image: <a href="https://google.co.uk">Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1560780-49a2-478d-866e-c7764f7060ff/google-now-opt.png">View large version</a>)</figcaption></figure>

Google Now makes a _lot_ of decisions in the background, from finding out where you've parked your car to searching for football scores — and notifying you at the right time without even having to be asked:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bf8765e-783b-4c5e-b6f8-69ed0cb8d56d/google-now-overview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9be5becb-c426-48c5-962a-c3b11ccc8854/google-now-overview-500-opt.png" width="500" height="188" alt="Google Now overview" /></a><figcaption>Google Now: "What you need, before you ask." (Image: <a href="https://www.google.co.uk/landing/now/">Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bf8765e-783b-4c5e-b6f8-69ed0cb8d56d/google-now-overview-opt.png">View large version</a>)</figcaption></figure>

Spotify shows another instance of this type of assumptive approach by creating playlists for users before they even think to:

<blockquote>
<p>It's like having your best friend make you a personalised mixtape every single week.</p>
</blockquote>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/792cf45f-8612-49b0-8f85-d07c0dce8506/spotify-discover-weekly-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c2d5464-ccd1-4728-bfde-3fcb02cf1119/spotify-discover-weekly-500-opt.png" width="500" height="115" alt="Spotify Discover Weekly" /></a><figcaption>Spotify Discover Weekly's personlized playlists (Image: <a href="https://spotify.com">Spotify</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/792cf45f-8612-49b0-8f85-d07c0dce8506/spotify-discover-weekly-opt.png">View large version</a>)</figcaption></figure>

The task of searching for new music and deciding which tracks to add to a playlist are carried out for you.

This notion of making decisions for users has been called "[anticipatory design](https://www.smashingmagazine.com/2015/09/anticipatory-design/)" and has become a topic of debate because of the ethics involved in making decisions on behalf of users.</p>

## Creating Trust In Anticipatory Design

In the process of reducing choices and making decisions for people using the approaches outlined above, one could be accused of being presumptuous about what users want. This can create distrust if the app doesn't do what the user expects, especially at a time when many apps have been exposed for exhibiting [dark patterns](https://alistapart.com/article/dark-patterns-deception-vs.-honesty-in-ui-design), tricking users into doing things they don't want to do.

Consequently, the higher the number of decisions an app makes for users, the more transparent it should be in order to maintain trust. This can be done by avoiding certain dark behaviors and instead favoring transparency through "light patterns," which keep users informed and in control, even when anticipatory design is used. Let's explore a few light patterns.</p>

### Avoid Limiting Information

When options are filtered away to show users more of what they might like (through app personalization and recommendation systems), an inherent problem can be created whereby users begin to see more and more of the same type of content:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d564cbc5-8754-4e50-8884-027c1aaf82aa/amazon-lamps-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6aaf440-af43-49d9-a1bd-63b43fbf72ea/amazon-lamps-500-opt.png" width="500" height="154" alt="Amazon browsing history recommendations" /></a><figcaption>Amazon browsing history recommendations (Image: <a href="https://amazon.co.uk">Amazon</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d564cbc5-8754-4e50-8884-027c1aaf82aa/amazon-lamps-opt.png">View large version</a>)</figcaption></figure>

This can making discovery of new things tricky. It is evident not only on e-commerce websites such as Amazon, but also on social media websites such as Facebook. As [Time magazine states](https://time.com/3950525/facebook-news-feed-algorithm/):

<blockquote>
<p>Facebook hopes to show more links to people who click lots of links, more videos to people who watch lots of videos and so forth.</p>
</blockquote>

Many users might not be happy with this because they don't want brands to determine what they see. For instance, Joel Spolsky, CEO of Stack Overflow, [accuses Facebook of hiding information](https://www.techworld.com/social-media/facebook-makes-me-angry-stack-overflows-ceo-joel-spolsky-on-developers-ethical-choices-3644318/):

<blockquote>
<p>Facebook is not showing all posts. It is choosing what to show you. An interesting question is to what extent does the Facebook algorithm tend to reinforce your preconceptions? Because that's what it has been trained to do.</p>
</blockquote>

### Give the User Control

One way to avoid limiting information is to make it easier for users to improve the assumptions that are made about them, through feedback mechanisms.

This can be done in different ways, from obvious (and, therefore, easier) mechanisms to less obvious ones:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc6381c6-228c-4743-a3b8-3c453deead6b/feedback-mechanisms-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02544c43-62e4-464e-8df1-970be15e1f67/feedback-mechanisms-500-opt.png" width="500" height="383" alt="Feedback mechanisms used by Google, Facebook and Amazon" /></a><figcaption>Feedback mechanisms used by Google, Facebook and Amazon (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc6381c6-228c-4743-a3b8-3c453deead6b/feedback-mechanisms-opt.png">View large version</a>)</figcaption></figure>

*   Google Now (top left) prompts users directly underneath its Now cards to check that the information shown is relevant.
*   Facebook (top right) is slightly less obvious, employing a dropdown caret in the top right of each news item. Clicking the caret reveals options to hide news you don't want to see.
*   Amazon (bottom) makes it even more difficult to tailor recommendations. You need to navigate to "Your Account" → "Your Recommendations" → "Improve Recommendations" to adjust what it shows you.

Of these three examples, Google offers the most transparent feedback mechanisms, giving multiple obvious interactions for users to provide feedback on cards, ensuring that the user is in control:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/382060a9-e955-47bc-9f6d-0c87fc7557fd/google-control-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69637c6c-4543-4592-980e-f6b821863d24/google-control-500-opt.png" width="500" height="221" alt="Google Now: You're in control" /></a><figcaption>Google Now: "You're in control." (Image: <a href="https://www.google.com/search/about/learn-more/now/#cards">Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/382060a9-e955-47bc-9f6d-0c87fc7557fd/google-control-opt.png">View large version</a>)</figcaption></figure>

As well as swiping cards, you can also access customization settings from the menu icon on each card:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/573cbca7-61b6-496f-8178-d9920fc29c31/google-control-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/573cbca7-61b6-496f-8178-d9920fc29c31/google-control-animated.gif" width="320" height="326" alt="Customizing Google Now" /></a><figcaption>Customizing Google Now (Image: <a href="https://www.google.com/search/about/learn-more/now/#cards">Google</a>)</figcaption></figure>

In the case of Facebook and Amazon, even though users can provide feedback to tailor what they see, the underlying news feed and recommendation algorithms have greater control, as [outlined by Joel Spolsky](https://www.techworld.com/social-media/facebook-makes-me-angry-stack-overflows-ceo-joel-spolsky-on-developers-ethical-choices-3644318/).</p>

### Avoid Disguising Ads as Content

Disguising ads as content is a [common dark pattern](https://darkpatterns.org/disguised-ads/), and it can happen when actions are carried out without the user's explicit consent.

As an example, Google Now recently partnered with brands such as Lyft, Airbnb, Uber and Instacart to prompt users with services available from those apps, at the time it thinks you need them. While cards from third-party services can be useful, when the cards are for paid services, it can almost seem like another form of advertising:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7ca0ad-efd9-4833-acbc-e5bd42676cf5/google-now-services-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f54f5c06-9a7b-4978-9621-3b55db70da89/google-now-services-500-opt.png" width="500" height="420" alt="Google Now partner services" /></a><figcaption>Google Now partner services (Image: <a href="https://www.google.com/search/about/learn-more/now/#cards">Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7ca0ad-efd9-4833-acbc-e5bd42676cf5/google-now-services-opt.png">View large version</a>)</figcaption></figure>

When similar dark shades of design can be seen in related products, the motivation behind anticipatory decisions becomes more suspect. Google Maps is a good example of this, appearing to [disguise ads as pins](https://thenextweb.com/google/2016/05/24/youll-soon-see-promoted-pins-google-maps-searches/#gref) on map search results:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/784f8e3f-562b-466c-9ce8-2e16dd3021a3/google-disguised-ads-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b0eaac0-08e3-4720-8d32-2d99279909b5/google-disguised-ads-500-opt.png" width="500" height="314" alt="Google Maps disguised ads" /></a><figcaption>Google Maps disguises ads as pins (Image: <a href="https://thenextweb.com/google/2016/05/24/youll-soon-see-promoted-pins-google-maps-searches/#gref">The Next Web</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/784f8e3f-562b-466c-9ce8-2e16dd3021a3/google-disguised-ads-opt.png">View large version</a>)</figcaption></figure>

### Make Use of Existing User Input

When making assumptions about users, it's important that they be accurate. A tried and tested way to do this is to make use of previous user input, as seen in web browsers features such as pre-populated forms, or by remembering credit-card details and passwords in anticipation of future use:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb90a482-997e-41fd-956b-4af4ead8ff17/browser-autocomplete-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb90a482-997e-41fd-956b-4af4ead8ff17/browser-autocomplete-opt.png" width="331" height="314" alt="Google Chrome autocomplete" /></a><figcaption>Google Chrome pre-populated forms</figcaption></figure>

This saves users from having to repeat the same tasks. The same principle can be applied when making more complex assumptions that combine multiple streams of data. [Campaign Live](https://www.campaignlive.com/article/brands-show-cards-google/1332234#wMhCR4FsQU1PWOG7.99) highlights an example of this when it discussed how the taxi service Hailo's "Now card" combines time, geolocation and previous user input to rebook taxis in Google Now:

<blockquote>
<p>Let's say you come into London and you book a Hailo cab, and you go into a particular area between 7am and 10am. If you're still there at 5pm, there's an assumption you may want to leave and that's when the Google Now card would prompt you to book a cab.</p>
</blockquote>

The assumption is likely to be more accurate in this case (and will appear less like a disguised ad) because the offer is based on a previous booking made by the user via the same service, within a reasonable time period:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47631935-1609-44c5-80bc-9f39a3f082f1/hailo-card-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47631935-1609-44c5-80bc-9f39a3f082f1/hailo-card-opt.png" width="250" height="" alt="Hailo card promtps user based on previous actions" /></a><figcaption>Hailo card prompts user based on related action (Image: <a href="https://www.google.co.uk/landing/now/">Google</a>)</figcaption></figure>

### Let Users Opt Out

Despite being able to customize the recommendations given to them, sometimes people don't want apps to make decisions for them at all. In this case, opting out must be easy. Even though you can't delete the Google Now app, you can disable Now cards in the settings:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ca34234-f2d1-4d76-b121-87e46301a4a4/google-turn-off-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ca34234-f2d1-4d76-b121-87e46301a4a4/google-turn-off-opt.png" width="250" height="" alt="Disable cards in Google Now" /></a><figcaption>Google Now lets users disable Now cards. (Image: <a href="https://www.google.co.uk/landing/now/">Google</a>)</figcaption></figure>

In contrast, there is **no way to turn off Amazon recommendations**, unless you log out completely — which makes sense (for Amazon) because [35% of product sales](https://venturebeat.com/2006/12/10/aggregate-knowledge-raises-5m-from-kleiner-on-a-roll/) are a result of recommendations, according to Venture Beat.

A question remains, therefore, as to whether features that record and make use of user data in these ways should be opt-in by default. There is a big difference between opt-in by choice and presumed consent, as shown in this example of organ donors from [Dark Patterns](https://darkpatterns.org/):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0020171-a44b-42d1-893b-d1d61886d2de/dark-patterns-opt.jpeg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0020171-a44b-42d1-893b-d1d61886d2de/dark-patterns-opt.jpeg" width="500" height="" alt="Dark patterns chart: Opt-in by choice" /></a><figcaption>The difference between opt-in by choice and presumed consent for organ donors (Image: <a href="https://darkpatterns.org/">Dark Patterns</a>)</figcaption></figure>

Basically, when opt-in is the default, consent to be an organ donor is nearly 100%, whereas when the decision to opt-in is not presumed, the consent percentage is very low.</p>

## Use Dark Patterns To Help People

It's evident that companies use dark patterns to advance their own agendas, and it's even easier today with the tools that help companies make decisions on behalf of users. However, what if similar methods could be used to help people make better decisions for themselves? Currently, many of us make poor decisions due to human frailties such as lack of self-control or a focus on short-term gains.</p>

### Nudge People to the Right Option

In their book [_Nudge: Improving Decisions About Health, Wealth, and Happiness_](https://en.wikipedia.org/wiki/Nudge_(book)), Richard Thaler and Cass Sunstein suggest creating an ethical "[choice architecture](https://en.wikipedia.org/wiki/Choice_architecture)" that nudges the user towards choosing the best overall option in the long run.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80551bcd-0742-4087-aec6-560144383a26/nudge-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80551bcd-0742-4087-aec6-560144383a26/nudge-opt.jpg" width="326" height="500" alt="Nudge: Imporving Decisions About Health, Wealth and Happiness" /></a><figcaption>Nudge: Improving Decisions About Health, Wealth and Happiness (Image: <a href="https://en.wikipedia.org/wiki/Nudge_(book)">Wikipedia</a>)</figcaption></figure>

In this vein, the techniques we have seen being used to create dark patterns can also be used to form light patterns that nudge users to make better choices.</p>

### Auto-Enrolment

For example, as life expectancy has increased, it's become important for people to save for old age through pension plans such as the US' [401(k)](https://en.wikipedia.org/wiki/401(k)). However, as explained by Thaler and Sunstein, even though these plans offer "free money," many people still don't choose to enroll. Possibile solutions suggested by Thaler and Sunstein to help people save for old age include:

*   automatically enrolling people (similar to the organ donor example),
*   forcing people to make a simple yes or no decision on whether to enroll.

These approaches are examples of light patterns because they serve to benefit users, pushing people to take action and to make good long-term decisions. Even though the latter approach forces people to decide, it simplifies the decision to an easy binary choice, which encourages people to participate.</p>

### Create Good Behavioral Patterns

[Alan Shapiro suggests](https://www.fastcodesign.com/3045039/the-next-big-thing-in-design-fewer-choices) that anticipatory apps could actually encourage behavioral patterns in users. By being constantly advised where to go and what to buy, people could become conditioned by app notifications and the decisions made on their behalf.

This could make for some scary scenarios, such as when a company is primarily interested in selling you products, because it's more likely to instill behavior that favors impulse purchases and the use of its services. For instance, Amazon's new Prime Pantry service is full of shady patterns, starting with its Pantry Boxes, which encourage people to buy more than they intended:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af758893-75fe-4c61-9d82-ca0d876bd95c/amazon-pantry-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30243820-441a-4ffa-b59b-912222011ee0/amazon-pantry-500-opt.png" width="500" height="280" alt="Amazon Pantry: Buy more" /></a><figcaption>Amazon Pantry Box encourages purchasing habits (Image: <a href="https://redefinedmom.com/how-does-amazon-prime-pantry-work/">redefined mom</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af758893-75fe-4c61-9d82-ca0d876bd95c/amazon-pantry-opt.png">View large version</a>)</figcaption></figure>

As [put by Matt Crowley](https://medium.com/@mwcrowley/the-sketchy-ux-decisions-behind-amazons-prime-pantry-f7cf12878c17#.8lhlf42sv), head of product at Circadia:

<blockquote>
<p>Amazon has shifted the conversation away from "do I need this?" to "what else do I need to fill up this box?"</p>
</blockquote>

Amazon has even gone as far as filing patents for a system that leverages user data to predict and deliver products _before_ the customer has even placed an order. Amazon calls it [anticipatory shipping](https://www.forbes.com/forbes/welcome/?toURL=https://www.forbes.com/sites/onmarketing/2014/01/28/why-amazons-anticipatory-shipping-is-pure-genius/&refURL=&referrer=#14fea58d2fac):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6a918e3-dd31-4feb-b65c-c897c8857cbb/amazon-anticipatory-shipping-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e231f9ee-1987-40ab-b65f-6dbf2384e5b2/amazon-anticipatory-shipping-500-opt.png" width="500" height="327" alt="Amazon anticipatory shipping patent diagram" /></a><figcaption>Amazon's anticipatory shipping patent diagram (Image: <a href="https://techcrunch.com/2014/01/18/amazon-pre-ships/">Tech Crunch</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6a918e3-dd31-4feb-b65c-c897c8857cbb/amazon-anticipatory-shipping-opt.png">View large version</a>)</figcaption></figure>

Putting these motives aside, what if the same tactics could be used to help people form good behaviors and habits? There are plenty of examples of this today, with the emergence of many self-improvement and habit-forming apps.

For example, [stickK](https://www.stickk.com/) [helps you](https://www.stickk.com/tour) kick bad habits by using "the psychological power of loss aversion and accountability to drive behavior change."

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67078f8f-ec67-40ff-a05c-76b2baa628a1/stick-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec73048c-c275-45d8-b511-0b8a33413035/stick-500-opt.png" width="500" height="309" alt="stickK helps you kick bad habits" /></a><figcaption>stickK helps you kick bad habits. (Image: <a href="https://stickk.com/">stickK</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67078f8f-ec67-40ff-a05c-76b2baa628a1/stick-opt.png">View large version</a>)</figcaption></figure>

[Duolingo](https://www.duolingo.com/) reminds you to practice your new language every day, helping you to form a beneficial habit.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcf380de-634e-4d5a-a862-8ec735091dea/duolingo-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcf380de-634e-4d5a-a862-8ec735091dea/duolingo-opt.png" width="250" height="" alt="Duolingo notifications" /></a><figcaption>Duolingo helps you form language-learning habits. (Image: <a href="https://upquire.com">Upquire.com</a>)</figcaption></figure>

From what we see above, the benefits people get from decisions being made on their behalf in anticipatory design are largely determined by the ethics of the company behind the app. How willing is a company to exploit customer data for its own purposes, and how much data are users willing to trade for convenience?

As explained throughout, giving users control and staying transparent are key to maintaining trust. What do you think about dark patterns used in anticipatory design? Do light patterns really exist, and who is in control when design assumptions are made?

{{< signature "il, yk, al" >}}

