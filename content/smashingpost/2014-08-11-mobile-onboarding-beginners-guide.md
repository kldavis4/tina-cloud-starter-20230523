---
title: 'Mobile Onboarding: A Beginner’s Guide'
slug: mobile-onboarding-beginners-guide
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ca518b1-a593-47b3-8183-bcfa1216bb6d/welcome-illu-play-button.jpg
date: 2014-08-11T21:39:08.000Z
author: germainesatia
description: >-
  Nowadays, displaying onboarding screens to first-time users has become a
  common practice in mobile apps. The purpose of these onboarding screens — also
  referred to as walkthroughs — is to introduce the app and demonstrate what it
  does.

  Given that these are often the first set of screens with which users interact,
  they also set the users’ expectations of the app. Therefore, it is essential
  that those involved in creating the product — product managers, designers,
  developers — take the time to evaluate whether onboarding is necessary for the
  app and, if so, to determine the best way to implement it.
categories:
  - UX
  - Mobile
  - Workflow
  - Techniques
  - UX
---
Nowadays, displaying onboarding screens to first-time users has become a common practice in mobile apps. The purpose of these onboarding screens — also referred to as walkthroughs — is to introduce the app and demonstrate what it does.

Given that these are often the first set of screens with which users interact, they also set the users’ expectations of the app. Therefore, it is essential that those involved in creating the product — product managers, designers, developers — take the time to evaluate whether onboarding is necessary for the app and, if so, to determine the best way to implement it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Roadmap To Building A Delightful Onboarding Experience](https://www.smashingmagazine.com/2016/06/complete-roadmap-building-delightful-onboarding-experience-mobile-app-users/)
*   [<span class="headline">The Role Of Empty States In User Onboarding</span>](https://www.smashingmagazine.com/2017/02/user-onboarding-empty-states-mobile-apps/)
*   [Refining Your Mobile Onboarding Experience Using Visual Analytics](https://www.smashingmagazine.com/2014/11/refining-your-mobile-onboarding-experience-using-visual-analytics/)
*   [Smart Transitions In User Experience Design](https://www.smashingmagazine.com/2013/10/smart-transitions-in-user-experience-design/)

In this article, we’ll provide <strong>some good tips on how to approach onboarding</strong>, some common implementations, alternative techniques, as well as resources to help you provide the best experience for users.

{{% feature-panel %}}

## To Onboard Or Not To Onboard?

In recent years, we’ve seen plenty of discussion on the usefulness of onboarding in mobile apps. A popular <a href="https://blog.maxrudberg.com/post/38958984259/if-you-see-a-ui-walkthrough-they-blew-it">argument against</a> onboarding is that if an app needs it, then it is fundamentally flawed, lacking the cardinal elements of simplicity and user-friendliness. While this line of thought does have logic, it’s too sweeping a conclusion.

The digital design world has plenty of rules and best practices, which is good. These rules save designers and developers from having to reinvent the wheel every time they work on a product. More importantly, they <strong>save users from stressing out whenever they use a new app</strong>; instead, they can rest assured knowing that the editing function will be represented by a pencil icon and that a “thumbs up” icon means “like.” Rules are good.

But the reality is that every app is unique in what it does, how it does it and who uses it. These variations make onboarding a reliable, pragmatic and user-friendly feature in certain instances. Let’s consider some use cases.</p>

### Use Case 1: Unfamiliar Interaction

If you are releasing an app that supports interaction methods that most users would not have been exposed to on a regular basis — particularly a gesture-driven app — then onboarding is essential. Gesture-driven apps are still in the experimental and exploratory phase. As such, developers need to guide users on how to interact with them, clearly presenting each gesture and its corresponding function.

For example, the alarm clock Timely, indicates to the user that tapping a particular part of the screen will add or subtract five minutes from the clock.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be51e03b-0631-4641-af7f-577b0864c66c/01-timely-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c50e0ea2-85fb-4be5-b57f-452eabf170c6/01-timely-opt-500.jpg" alt="Guide users towards each gesture and the expected result." width="500" height="350" /></a><figcaption><a href="https://play.google.com/store/apps/details?id=ch.bitspin.timely">Timely</a> guides users to each gesture and the expected result. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be51e03b-0631-4641-af7f-577b0864c66c/01-timely-opt.jpg">View large version</a>)</figcaption></figure>

### Use Case 2: Empty State

An app whose default state is empty and requires users to go through one or more steps to populate it with content is also well suited to onboarding. Even if the onboarding process consists of just one step, the guidance will reassure users that they are doing the right thing.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bace554-b333-4620-8bd6-7117db9da630/02-feedly-umano-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/175202b8-ca5e-4cfa-b463-ad9ff2a145d7/02-feedly-umano-opt-500.jpg" alt="Show users how to retrieve their first set of content." width="1000" height="800" /></a><figcaption><a href="https://play.google.com/store/apps/details?id=com.devhd.feedly&amp;hl=en">Feedly</a> shows users how to retrieve their first batch of content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bace554-b333-4620-8bd6-7117db9da630/02-feedly-umano-opt.jpg">View large version</a>)</figcaption></figure>

### Use Case 3: Suite of Products

If your app is part of a suite of products — say, with desktop and web companions — then onboarding could greatly improve the user’s experience, especially if the mobile app doesn’t have all of the functionality of the other versions. This is especially important in complex business apps, many of which have a variety of user roles, each with specific access rights and security restrictions.

Very often the web and desktop versions will support full functionality (such as for creating, viewing, editing and deleting content), while the mobile app limits it (such as viewing only). In such cases, <strong>a brief presentation explaining what the app does</strong> would help existing users understand how the mobile app fits into the suite of products.

### Use Case 4: Personal Information

If your app relies on personal information (such as age, weight, gender, marital status), then collect and store this information via onboarding. Guide the user step by step so that they are clear on why this information is being requested. And be sure to allow the user to change this information whenever they want (usually from the settings screen).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69b0ec59-6b5a-4fe3-a8bc-fd64a89e8145/03-fibit-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d7adde4-f926-4622-a401-c66855b39b10/03-fibit-opt-500.jpg" alt="Tell users why their personal information is needed and guide them." width="500" height="350" /></a><figcaption><a href="https://itunes.apple.com/en/app/fitbit/id462638897?mt=8">Fitbit</a> tells users why their personal information is needed and guides them. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69b0ec59-6b5a-4fe3-a8bc-fd64a89e8145/03-fibit-opt.jpg">View large version</a>)</figcaption></figure>

Even if your app doesn’t fit any of the examples above, your users might still benefit from onboarding. Keep in mind that <strong>anyone who interacts with a product will at least want to know how the product will benefit them</strong>. You can present this information in onboarding, as we’ll discuss later in the section on function-oriented onboarding.

Sure, our primary responsibility is to design products that are intuitive and easy to use. However, we shouldn’t dismiss onboarding because when it provides value to the user, it makes for a much more pleasant experience.</p>

### Which Technique to Use?

These three techniques are the most common:

*   benefits-oriented onboarding,
*   function-oriented onboarding,
*   progressive onboarding.

We’ll look at each in turn and review some general guidelines for implementing them.</p>

## Technique 1: Benefits-Oriented Onboarding

This is pretty self-explanatory. With this technique, you present the benefits (i.e. the value) of the app, communicating one or more of the following to the user:

*   _What_ does the app do?
*   _How_ can the user integrate it into their life?
*   What _value_ will this integration provide?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f3db755-dd01-4b8e-bb65-44e4369263ac/04-evernote-food-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c790ae3-c98c-4630-b5f9-f698ea70db7c/04-evernote-food-opt-500.jpg" alt="Highlight what the user will gain from using your app." width="500" height="350" /></a><figcaption>Evernote Food highlights what the user will gain from using the app. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f3db755-dd01-4b8e-bb65-44e4369263ac/04-evernote-food-opt.jpg">View large version</a>)</figcaption></figure>

When implementing this technique, consider the following principles:

### Present a Maximum of Three Key Benefits

This number is not based on hard science, but because the point is to give the user a quick overview of the app, three is a safe number (excluding the title screen). This way, the user gets to learn about the app without getting bored or slowed down by too much information.</p>

### Apply the “One Slide, One Concept” Rule

Think back to presentations from which you retained the most information. The slides with a clear, focused message probably had the greatest impact on you and were the most memorable. The same goes for onboarding screens. The “one slide, one concept” rule helps the user to focus on and digest every little piece of information. Presenting everything at once would be visually noisy and distract the user from your key message.</p>

### Prioritize, Prioritize, Prioritize

Resist the urge to show off everything cool about your app. Always return to your user data and remind yourself of the problem that the user is facing and what they need. Then, figure out how to reassure them through onboarding that the app does indeed answer their need.</p>

### Use Consistent Vocabulary

Evernote Food, mentioned above, uses verbs to quickly grab attention and communicate its key benefits. The approach is effective, efficient and succinct. If you can’t boil things down to a few high-impact verbs or adjectives, then a short phrase or two would suffice. Just be sure to stick with it all the way through. A harmonious and coherent presentation, both in visuals and terminology, will help to kick off the user’s experience on a positive note.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7028555f-bd1b-40ad-b471-e0ffbd089222/05-nytnews-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fde707d-aee5-47b4-a078-bfeb2a453b8f/05-nytnews-opt-500.jpg" alt="Use clear, brief descriptions to communicate your app’s benefits and value." width="500" height="350" /></a><figcaption><a href="https://itunes.apple.com/us/app/nyt-now/id798993249?mt=8">NYT Now</a> uses clear, brief descriptions to communicate its benefits and value. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7028555f-bd1b-40ad-b471-e0ffbd089222/05-nytnews-opt.jpg">View large version</a>)</figcaption></figure>

### Onboard Before Registration

Because onboarding is meant to be an overview, present it before the user signs up for or logs into the service. Once they decide to log in, the user will be ready to explore the app and should not be interrupted by reminders on the benefits of the app.</p>

### Keep It Brief

Perhaps you’re wondering whether onboarding really is necessary. After all, doesn’t it just repeat the description in the app store? Not at all. App store descriptions come in all shapes and sizes, whereas onboarding has to be succinct and, as such, <strong>focus on the absolute essentials</strong>. In addition, many people skip the app store description, preferring instead to dive right into the experience. So, a brief presentation once they’re engaged with the app could help them understand what the app does.</p>

### What Not to Do

<a href="https://play.google.com/store/apps/details?id=com.readability&amp;hl=en">Readability</a> is a wonderfully practical app that, unfortunately, is inconsistent across platforms. This is particularly evident in the onboarding in the Android version, which makes several missteps:

*   The user has to digest a total of seven slides and corresponding messages.
*   The text for some slides runs a bit long. For example, the slide about sharing could have been simplified by showing icons of the social networks on which content may be shared.
*   One slide encourages the user to install a Firefox plugin, which seems misplaced given that it’s a mobile platform. Plus, the previous slide already tells the user that “Readability is a web and mobile app.” Onboarding in the mobile app should not serve as a catch-all for marketing the full suite of products, but rather should be relevant to the mobile platform.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85abd13c-6792-4ef8-84b5-89d90cf3a9a3/06-readability-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df6c4600-6b85-447c-a779-57798f0d63dc/06-readability-opt-500.jpg" alt="Avoid having too many slides and content; keep the content relevant to the platform." width="500" height="350" /></a><figcaption>Avoid many slides, and keep the content relevant to the platform. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85abd13c-6792-4ef8-84b5-89d90cf3a9a3/06-readability-opt.jpg">View large version</a>)</figcaption></figure>

## Technique 2: Function-Oriented Onboarding

Another option is to forgo a presentation on benefits and to focus instead on the app’s key functionality. This is sometimes referred to as <a href="https://mobilepatterns.wikispaces.com/Coach+Marks">coach marks</a>. If you take this approach, communicate the following:

*   _What_ is the key functionality (for example, how to get started or what actions are most common);
*   _When_ to use the functionality (for example, when viewing search results);
*   _How_ to use the functionality (for example, tapping or swiping left).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea632802-d882-4823-bc51-cf21c9c7baa1/07-carousel-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b784d15-559a-4f1f-9a67-2224005e6807/07-carousel-opt-500.jpg" alt="Introduce key functions immediately." width="500" height="350" /></a><figcaption><a href="https://itunes.apple.com/fr/app/carousel-by-dropbox/id825931374?mt=8">Carousel</a> introduces key functionality immediately. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea632802-d882-4823-bc51-cf21c9c7baa1/07-carousel-opt.jpg">View large version</a>)</figcaption></figure>

When putting together function-oriented onboarding, keep the following in mind:

### Don’t Explain the Obvious

Since the dawn of the Internet, from desktop apps to the web to mobile apps, the “x” has consistently represented closing, exiting or cancelling. So, unless that icon has a different purpose in your app, including it in your onboarding won’t provide any value to users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2bf78a6-6024-44b1-9bc0-214c1a5b4683/08-adobe-kuler-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f18e845-7c3c-4597-82ee-388b9c68988b/08-adobe-kuler-opt-500.jpg" alt="Don’t show obvious actions." width="500" height="450" /></a><figcaption><a href="https://itunes.apple.com/app/adobe-kuler/id632313714">Adobe Kuler</a> doesn’t show obvious actions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2bf78a6-6024-44b1-9bc0-214c1a5b4683/08-adobe-kuler-opt.jpg">View large version</a>)</figcaption></figure>

### Three Slides, One Function Per Slide

If you are explaining the functionality in a slideshow, then follow the same principle that we covered with benefits-oriented onboarding: a maximum of three slides (excluding the title slide), presenting one function per slide.</p>

### Help the User Get Started

If your app is empty by default, focus on this in your onboarding. Don’t let the user face a blank screen the first time they open the app. Include a quick note to show them how to get started, so that they don’t wonder — even if only for a second — whether the blank screen is a bug or a feature.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c3305ff-6310-45b4-b04e-7c01e209d7a8/09-spendee-opt.jpg" alt="Reassure users by telling them how to get going." width="480" height="598" /><br>
<figcaption><a href="https://play.google.com/store/apps/details?id=com.cleevio.spendee&amp;hl=en">Spendee</a> reassures users by telling them how to get started. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c3305ff-6310-45b4-b04e-7c01e209d7a8/09-spendee-opt.jpg">View large version</a>)</figcaption></figure>

### Onboard Before Log-In or Sign-Up

As with the last technique, onboard users before they sign up for or log into your service.</p>

### What Not to Do

Photography showcase app <a href="https://itunes.apple.com/en/app/500px-discover-photos-from/id471965292?mt=8">500px</a> boasts some amazing content and a rich set of functionality to go along with it. However, the onboarding process for the iPhone app commits some faux-pas:

*   The navigation bar and its functionality are showcased. Telling users that they can navigate via the navigation bar falls under the category of obvious.
*   Some slides show buttons such as for liking, favoriting and sharing. All three of these functions are represented by icons that are universally associated with them, so explaining them in the onboarding is unnecessary. Let’s suppose, for the sake of argument, that a portion of 500px’s target audience is not familiar with these icons. In this case, progressively onboarding these users by presenting the functions in context would better serve them (for example, when the user is viewing a picture and might want to “like” it).
*   One slide shows the “flow,” a timeline that showcases the activity of people whom the user is following. Because you can only benefit from the flow once you have followed others, progressively onboarding the user by telling them about this feature after they’ve followed at least one person would have been better.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e43b314a-020f-4d45-8665-74f0c35f8891/10-single-slide-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c12f4b-e2a5-4b82-85bf-c0fe365a5f36/10-single-slide-opt-500.jpg" alt="Avoid showing several functions on a single slide, save details for later." width="500" height="350" /></a><figcaption><a href="https://itunes.apple.com/en/app/500px-discover-photos-from/id471965292?mt=8">500px</a> could have avoided showing several functions on a single slide, saving some details for later. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e43b314a-020f-4d45-8665-74f0c35f8891/10-single-slide-opt.jpg">View large version</a>)</figcaption></figure>

## Technique 3: Progressive Onboarding

In general, people learn best by doing. This probably explains the popularity of progressive onboarding, which is a true walkthrough in that it presents information to users as they use the app. For example, when the user is on the dashboard, they would see only dashboard-related information; when they’re viewing search results, they would be shown only functions related to search results.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bf83775-4d3e-4ef0-a809-e7179c177454/11-feedly-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/504c1dac-221a-4bf3-a966-9f91b59c1761/11-feedly-opt-500.jpg" alt="Display hints as user goes through app." width="500" height="350" /></a><figcaption><a href="https://play.google.com/store/apps/details?id=com.devhd.feedly&amp;hl=en">Feedly</a> displays hints as users go through the app. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bf83775-4d3e-4ef0-a809-e7179c177454/11-feedly-opt.jpg">View large version</a>)</figcaption></figure>

Here are a few things to keep in mind when progressively onboarding:

### Save for Complex Workflows

If your app has a fairly complex workflow or handles complex tasks (such as finances), then progressive onboarding is a good choice. You would feed the user information only when it’s appropriate and logical in the workflow, giving the user time to digest it.</p>

### Use for Hidden Functionality

When developing mobile apps, we’re always focused on efficiently using the small screen, which sometimes requires menus and functions to be hidden, visible only via, say, a double tap or long press. In this case, walk the user through those hidden functions.

For example, take the app <a href="https://itunes.apple.com/us/app/pocket-save-articles-videos/id309601447?mt=8">Pocket</a>, shown below. In it, functions are available for each item in the reading list, but the user has to swipe left in order to access them. Because the user has to populate the app with content, a nice touch would have been to wait until the user has added at least one item to the reading list, and then immediately point out that a left swipe reveals the hidden functions.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9c9524b-8f4f-4f76-8cbb-e491206302cf/12-pocket-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80bf0324-a6b6-4eef-8148-e860faa66c1d/12-pocket-opt-500.jpg" alt="Progressive onboarding could have been used to point out hidden functions." width="500" height="350" /></a><figcaption><a href="https://itunes.apple.com/us/app/pocket-save-articles-videos/id309601447?mt=8">Pocket</a> could have progressively onboarded users by pointing out hidden functionality. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9c9524b-8f4f-4f76-8cbb-e491206302cf/12-pocket-opt.jpg">View large version</a>)</figcaption></figure>

### Ideal for Gesture-Driven Apps

If your app is strictly gesture-driven, then this hands-on approach is best. Getting the user to take action over time as functionality is introduced will help the information stick.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09dfa88d-9a88-4244-b2ad-957dd87b4a6f/13-solar-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/737beb4d-56c4-4456-b050-403497258fdf/13-solar-opt-500.jpg" alt="13-solar-opt-500" width="500" height="350" /></a><figcaption><a href="https://itunes.apple.com/en/app/solar-weather/id542875991?mt=8">Solar</a> presents each gesture and helps the user learn by doing. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09dfa88d-9a88-4244-b2ad-957dd87b4a6f/13-solar-opt.jpg">View large version</a>)</figcaption></figure>

### Make It Persistent

For gesture-driven apps, provide a shortcut to a list of gestures and their corresponding actions, perhaps in the settings screen.

Remember that the more gestures you have, the more the user has to memorize. And the more gesture-driven apps a user has installed on their device, the more confused they can get, trying to remember the difference between a double-tap in one app and a double-tap in another. Making the information permanently accessible adds an extra layer of comfort.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f221144f-0a83-4e01-a72b-8148036b5c8a/14-beats-music-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2645f6c9-e79d-40db-b9b2-bb450cbd731c/14-beats-music-opt-500.jpg" alt="Provide permanent, quick access to the list of gestures in case user needs a reference." width="500" height="350" /></a><figcaption><a href="https://itunes.apple.com/en/app/beats-music/id781817640?mt=8">Beats Music</a> provides permanent, quick access to a list of gestures. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f221144f-0a83-4e01-a72b-8148036b5c8a/14-beats-music-opt.jpg">View large version</a>)</figcaption></figure>

### What Not to Do

Because progressive onboarding complements a user’s exploration of an app, the biggest risk is that incessant hints as the user moves from screen to screen will ruin the experience of an otherwise wonderful app. So, take even greater care with this technique to show only the most useful information.

Also, avoid highlighting features on every screen. Give the user some breathing room so that they get some satisfaction from exploring your app. A walkthrough is not a substitute for poor design. It should simply enhance the experience.</p>

## Alternative Solutions

The techniques presented above are the most popular. But you <em>do</em> have other options to play with!

### Alternative 1: Hybrid

A hybrid approach — blending one, two or all three techniques — is sometimes viable, as <a href="https://itunes.apple.com/en/app/flink-mode-street-des-meilleures/id798552697?mt=8">Flink</a> shows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52530dee-cc02-456e-b613-dc454bd5f1ac/15-flink-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e33dd820-bf55-4c7a-8436-04e82553d155/15-flink-opt-500.jpg" alt="ombine benefits and functions onboarding if necessary." width="500" height="350" /></a><figcaption>Flink combines onboarding techniques. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52530dee-cc02-456e-b613-dc454bd5f1ac/15-flink-opt.jpg">View large version</a>)</figcaption></figure>

### Alternative 2: Video

Video onboarding is used in some apps and is worth looking into. This can be taken in different directions, with some videos being more practical, like a tutorial, while others are basically advertisements. As with videos on websites, playing them automatically would be invasive and jarring for the user. And the user might be in a public space, where blasting sound from a mobile device would be inappropriate.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d82d9d-b292-414b-b082-c1f197d7dbd0/16-paper-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/657f8f8c-163b-4111-b359-98f5d6579e6b/16-paper-opt-500.jpg" alt="Use the power of sound and visual to present your product." width="500" height="350" /></a><figcaption>Fifty-Three uses the power of sound and visuals to present its app <a href="https://itunes.apple.com/en/app/paper-by-fiftythree/id506003812?mt=8">Paper</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d82d9d-b292-414b-b082-c1f197d7dbd0/16-paper-opt.jpg">View large version</a>)</figcaption></figure>

### Alternative 3: Sample Data

Providing some sample data for the user to play with might also be worthwhile. This is particularly helpful in apps that handle sensitive data, such as finances and human-resources data. If the app is preloaded with sample data, the user will feel comfortable experimenting, making mistakes and learning how the app works, and they will feel better prepared to input real data.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84571d48-6b8e-4d5a-9530-c1779ee4e330/17-xero-opt.jpg" alt="Give users sample data to manipulate and learn how your app works." width="480" height="598" /><br>
<figcaption><a href="https://play.google.com/store/apps/details?id=com.xero.touch&amp;hl=en">Xero</a> gives users sample data to learn how the app works. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84571d48-6b8e-4d5a-9530-c1779ee4e330/17-xero-opt.jpg">View large version</a>)</figcaption></figure>

## Conclusion

The guidelines and examples in this article will jumpstart your onboarding project; however, as always, the user is at the heart of all of this. So, as you evaluate which technique to use, remember to revisit your personas, user scenarios and any user data you have, whether from analytics or market research.

If you’re still unsure about which technique to go with, test one or two techniques on users and <strong>analyze the feedback to see what works and what doesn’t</strong>. No solution is one-size-fits-all, so, as always, use the data on hand to make the most informed decision.

As you take your first steps, monitor what other developers are doing. The following websites provide a variety of onboarding patterns to draw inspiration from:

*   [Pttrns](https://www.pttrns.com/)
*   [Mobile Patterns](https://www.mobile-patterns.com/)
*   [UX Archive](https://uxarchive.com/)
*   [Pinterest](https://www.pinterest.com/)

If you’re interested in platform-specific guidelines, then check out <a href="https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/StartingStopping.html">Apple’s</a> and <a href="https://developers.google.com/live/shows/6727337534029824">Google’s</a>.

{{< signature "cc, ml, al, il" >}}

