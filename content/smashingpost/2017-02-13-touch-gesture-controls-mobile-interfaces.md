---
title: 'To Use Or Not To Use: Touch Gesture Controls For Mobile Interfaces'
slug: touch-gesture-controls-mobile-interfaces
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deeb6184-e6d4-4398-8671-6bfda9638487/slide-to-unlock500.jpg
date: 2017-02-13T19:31:32.000Z
author: kylesanders
description: >-
  Many criticize gestural controls as being unintuitive and unnecessary. Despite
  this, widespread adoption is underway already, and the UI design world is
  burning the candle at both ends to develop solutions that are instinctively
  tactile. The challenges here are those of novelty.

  Even though gestural controls have been around since the early 1980s and have
  enjoyed a level of ubiquity since the early 2000s, designers are still in the
  beta-testing phase of making gestural controls intuitive for everyday use.
categories:
  - Mobile
  - Usability
  - Interfaces
  - Interaction Design
---
Even though gestural controls have been around <a href="https://adage.com/article/on-design/a-history-gestural-interfaces/139976/">since the early 1980s</a> and have enjoyed a level of ubiquity since the early 2000s, designers are still in the beta-testing phase of making gestural controls intuitive for everyday use.

This article will explore the benefits and drawbacks of gestural controls for mobile UIs, as well as offer advice on effective implementation that avoids the gap in user familiarity.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [The Thumb Zone: Designing For Mobile Users](https://www.smashingmagazine.com/2016/09/the-thumb-zone-designing-for-mobile-users/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)
*   [Beyond The Button: Embracing The Gesture-Driven Interface](https://www.smashingmagazine.com/2013/05/gesture-driven-interface/)
*   [A Guide To Designing Touch Keyboards (With Cheat Sheet)](https://www.smashingmagazine.com/2013/08/guide-to-designing-touch-keyboards-with-cheat-sheet/)

{{% feature-panel %}}

## General Gestures

Gestures come in all shapes and sizes. The most common are listed in the graphic below. These are the conventional controls to which most active mobile device users are accustomed. These are the most used across platforms and, in that regard, the most intuitive. At least that’s the case with people who have significant experience using gestural controls.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12bf2405-ce45-4f41-a29a-9b089acd4d55/touch-chart-large-opt.jpg"><img loading="lazy" decoding="async"  class="alignnone" title="Mobile Gestures - Gestural-Touch-Chart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0061c8d-2295-4c87-8340-2fb3613c9a35/touch-chart-preview-opt.jpg" alt="mobile gestures" width="780" height="689" /></a><figcaption>Chart of gestural controls (Image credit: Touch Gesture Reference Guide) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12bf2405-ce45-4f41-a29a-9b089acd4d55/touch-chart-large-opt.jpg">View large version</a>)</figcaption></figure>

This level of intuition can’t be applied, however, to the diminishing population who are flying blind when confronted with a mobile interface. According to an <a href="https://www.lukew.com/ff/entry.asp?1197">oft-cited study</a> by Dan Mauney, there are a great deal of similarities in the way people expect a mobile interface to work. This study asked participants from nine countries to create a set of 28 actions using a gestural interface.

The results were stunningly similar. There wasn’t a ton of variability between actions. Most people expected certain actions to work the same. Deleting, for example, was most often accomplished by dragging an element off of the screen. Menus were constantly consulted — despite warnings not to do this. People often drew a question mark to indicate help functionality.

Oddly enough, the standard set of controls used across most apps were these:

*   tap,
*   double-tap,
*   drag,
*   flick,
*   pinch,
*   spread,
*   press,
*   press and tap,
*   press and drag,
*   rotate.

These didn’t always account for the intuitive gestures most people in the study created when left to their own devices. This presents a big question: How intuitive are gestural interfaces? Not only that, but what are the pros and cons of implementing a gestural interface?

Regardless of the drawbacks, one thing is clear: Gestural interfaces aren’t going anywhere. That’s why it’s vital for today’s designers to firmly grasp the underlying concepts that make gestural controls effective. Otherwise, the chance that the usability of their work will suffer increases dramatically.</p>

## Benefits Of Gestural Controls

Gestural controls are popular because of two major factors:

*   the meteoric rise of mobile devices with touchscreens,
*   the movie Minority Report.

Kidding. It’s just about the mobile devices. The Minority Report HUD display is such a fantastic example, however, that it’s become somewhat of a trope to discuss it in conversations about touch interfaces, but we’re still a ways off from interacting with holographic projections.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f471629-3358-45aa-8138-c3be27768829/minority-report-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b623ccab-6b07-491b-b24c-06fa6420f1ec/minority-report-preview-opt.jpg" alt="Minority-Report" width="780" height="350" /></a><figcaption>(Image credit: <a href="https://www.youtube.com/watch?v=7SFeCgoep1c">YouTube</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f471629-3358-45aa-8138-c3be27768829/minority-report-large-opt.jpg">View large version</a>)</figcaption></figure>

Even so, this foreboding Tom Cruise vehicle did a great job of showing what will eventually be possible with UI design. And the important part of that is getting something that’s usable and intuitive. Let’s examine how that’s possible in our first tangible benefit of gestural control.</p>

### Gestures Are Easy to Learn

Touch UIs only feel intuitive when they approximate interaction with a physical object. This means that tactile feedback, and the ability to manipulate the UI elements, has to work as an abstraction of a real object in order to be truly intuitive.

Even poorly designed interfaces only take a little experimentation to figure out, at least for power users. Think about how often you’ve skipped a tutorial to just interact with an app’s interface. You might miss some fine details, but it’s fairly easy to discover the primary controls for most interfaces within a few minutes of unguided interaction. Still, there’s a serious limiter on user delight if there’s no subtle guidance from the designer. So, how do you teach your users without distracting them from the application?

The best approach to creating intuitive touch-based interaction is through a process called <strong>progressive disclosure</strong>. This is a process by which a user is introduced to controls and gestures as they proceed through an interface’s flow. Start by showing users only the most important options for interaction. You can do this with visual cues, or through a tutorial-like “get started” process. I favor the former, because many users (myself included) will <a href="https://blog.maxrudberg.com/post/38958984259/if-you-see-a-ui-walkthrough-they-blew-it">usually skip a tutorial</a> to start interacting with an app right away.

Slight visual cues and animations that give instant feedback in response to touch are the perfect delivery method for progressive disclosure. A fantastic example of this is visible in Apple products’ “slide to unlock” commands, although the feature has since been removed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deeb6184-e6d4-4398-8671-6bfda9638487/slide-to-unlock500.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deeb6184-e6d4-4398-8671-6bfda9638487/slide-to-unlock500.jpg" alt="Slide-unlock" width="500" height="375" /></a><figcaption>Slide to unlock (Image credit: <a href="https://c1.staticflickr.com/5/4025/5166412211_65bf5c1aee.jpg">Flickr</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0703e67c-17d5-47a1-ba28-f784d8f5b35c/image05.gif">View large version</a>)</figcaption></figure>

The interface guides you with text, indicates the direction with an arrow and offers immediate feedback action with animation. You can take this same concept and draw it out further with more multifaceted applications.

In his 2013 <a href="https://www.smashingmagazine.com/2013/05/gesture-driven-interface/">article about gestural interfaces</a>, Thomas Joos, contributor to Smashing Magazine, covers this process thoroughly, pointing to YouTube’s Capture application as an example.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77cfb4fc-1b9d-4a4c-ac42-c60e2d218553/smashing-mag-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12146d75-9a53-4284-be63-7eee5eba5230/smashing-mag-preview-opt.jpg" alt="Gesture-driven-interface" width="780" height="822" /></a><figcaption>“Beyond the Button: Embracing the Gesture-Driven Interface” (Image credit: <a href="https://www.smashingmagazine.com/2013/05/gesture-driven-interface/">Smashing Magazine</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77cfb4fc-1b9d-4a4c-ac42-c60e2d218553/smashing-mag-large-opt.jpg">View large version</a>)</figcaption></figure>

Both progressive disclosure and the tutorial techniques offer guidance should a user require it. The disclosure method, however, has the added benefit of respecting the user enough to expect they can figure out a process.

Because they’re completing a task with minimal guidance (achieving goals, as it were), they feel a sense of accomplishment. The design is adding to their delight in interacting with the app. This can help to create habits and obviously makes it much easier to learn related or increasingly complex operations within the application. You’ve established a pattern of minimal guidance; all you have to do is repeat it as the functions layer on in complexity.

The important thing to remember when teaching users how to use your interface is the three-part process of habit formation:

1.  trigger,
2.  action,
3.  feedback.

The trigger is the inciting action, such as a push notification reminding a user to interact with the app. The action is where you leave your subtle clue as to how the user should gesticulate in order to complete the goal. Then comes the feedback, which works as a sort of reward for a job well done.

This habit-formation process is a form of user onboarding, or a way of ensuring that new users are successful when they start using your application, and then converting casual visitors into enthusiastic fans. A great example of this process (specifically, <a href="https://www.appcues.com/user-onboarding-academy/intro-to-user-onboarding/">the third step</a>) can be seen in the Lumosity app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa6dfe0f-15fa-4728-882a-4eb6b3a84d74/luminosity-app.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa6dfe0f-15fa-4728-882a-4eb6b3a84d74/luminosity-app.jpg" alt="luminosity-app" width="747" height="" /></a><figcaption>(Image credit: <a href="https://play.google.com/store/apps/details?id=com.lumoslabs.lumosity&amp;hl=en">Lumosity</a>)</figcaption></figure>

The Lumosity app is a game-based brain-training application. It allows users to set up their own triggers, which manifest as push notifications.

It then progresses to the actions, the games themselves. These games are gesture-based, and each is introduced by a quick, easy, simple tutorial.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c81be07-e79b-49fc-b775-b78884a7266b/luminosity-app2.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c81be07-e79b-49fc-b775-b78884a7266b/luminosity-app2.jpg" alt="luminosity-app" width="748" height="" /></a><figcaption>(Image credit: <a href="https://play.google.com/store/apps/details?id=com.lumoslabs.lumosity&amp;hl=en">Lumosity</a>)</figcaption></figure>

Note the succinct instructions. A quick read and the performance of the instructions provide instant feedback on user actions.

Finally, after the user has finished each exercise, the feedback is offered — then again, when they’ve finished a set number of exercises in a given day.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f01b34f-bc73-4350-a376-f817786bc18b/luminosity-app3.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f01b34f-bc73-4350-a376-f817786bc18b/luminosity-app3.jpg" alt="luminosity-app" width="756" height="" /></a><figcaption>(Image credit: <a href="https://play.google.com/store/apps/details?id=com.lumoslabs.lumosity&amp;hl=en">Lumosity</a>)</figcaption></figure>

Providing these stimuli to the user reinforces their satisfaction from performing their tasks, as well as their memory of how to perform them. Gestural controls are a skill, like any other. If you can make learning them fun, then the curve for retention will decrease significantly.

Of course, easy learning is only one benefit of a gestural UI. Another big one is the fact that it promotes a minimalist aesthetic.</p>

### Touch UIs Free Up Screen Space

Screen real estate on a mobile device is a big deal. Your space is limited, and you have to use it wisely — especially if you have an abundance of features. That’s why so many interfaces are resorting to the hamburger menu icon to hide navigation controls.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a6800b-2e20-473b-a068-682918a31119/mobile-menu.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a6800b-2e20-473b-a068-682918a31119/mobile-menu.jpg" alt="mobile-menu" width="780" height="" /></a><figcaption>Hamburger menu icon hides navigation controls (Image credit: <a href="https://upload.wikimedia.org/wikipedia/commons/b/b8/Editing_Wikipedia_mobile_screenshot_p_16,_Penny_Cyclopaedia_with_menu.png">Wiki Commons</a>)</figcaption></figure>

Using gestures for navigation of a website might be a bit of a tradeoff in usability, but it makes an app look pretty slick. Just take a look at the Solar app, which is highly minimalist and offers those subtle cues we talked about earlier.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cade2be-a53c-43dc-b26a-02d80922778f/solarscreen.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cade2be-a53c-43dc-b26a-02d80922778f/solarscreen.jpg" alt="mobile-menu" width="640" height="" /></a><figcaption>Minimalist app with subtle cues (Image credit: <a href="https://itunes.apple.com/us/app/solar-weather/id542875991?mt=8">Solar</a>)</figcaption></figure>

Though the clarity of the actions a user is meant to take is decreased slightly, the look and feel of the app are boosted in a tangible way. Plus, delight is increased because the user is given more autonomy to figure out what to do on their own. Speaking of delight…

### User Delight

Something that’s easy to use and easy on the eyes is also easy to enjoy. Gestural controls enable a tactile experience for users, and that’s downright enjoyable. Using haptic feedback to indicate a successful interaction, for example, can give users a subtle sense of accomplishment. This could be as simple as a confirmative vibration upon muting the phone (as in the case of both Apple and Android products).

Basically, in addition to the visual and audio appeal of a product, designers can now begin incorporating touch sensations as a way to engage users. The folks over at Disney are <a href="https://www.engadget.com/2013/10/07/ultrahaptics-3d-touch-displays/">exploring this concept</a> with no lack of zeal.</p>

### Room to Explore

That brings us to our final point. This is unexplored territory — a whole new world of interaction for designers to bring to life in living color! While usability and industry best practices should always be considered and consulted, this is a chance to break creatively from convention. While it might not always work out to be revolutionary, experimentation in this field can’t help but be exciting.</p>

## Disadvantages Of Gestural Controls

Oddly enough, with all of the futuristic appeal and hype paid to gestural controls, the trend isn’t universally beloved. In fact, there’s a sizeable camp in the design world that considers gestural controls to be a step back in usability.</p>

### Thoughtless Gesticulation

At least part of this pushback is due to the rush to implement. Many designers working on gestural interfaces are ignoring the standard UX caveats that have been shown to measurably improve a product’s usability. Moreover, the inclination towards conformity in design is always pretty high. You’re reading what is essentially a “best practices” article, after all. And it’s one of thousands.

This means that people are using the same techniques and design patterns across any number of applications and interfaces, even when they don’t make sense, due to “conventional wisdom.”

Designers sometimes duplicate the same usability problems in their work that you find in other popular gestural interfaces employed by industry big boys, such as Google and Facebook — for example, the preference for icons over text-based links. In an effort to save space, designers use pictures rather than text. This, in itself, isn’t exactly a cardinal sin, and it can be very helpful in moderation.

The problem is that it isn’t exactly super-intuitive. Pictures are subjective. They can mean different things to different people, and assuming that your users will know what an obscure icon is supposed to do is quite the gamble.

Check the interface of music app Bloom.fm.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8bbfe29-b506-4b80-887d-995e6566cf2b/bloomfm.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8bbfe29-b506-4b80-887d-995e6566cf2b/bloomfm.jpg" alt="bloom-fm" width="487" height="" /></a><figcaption>Image credit: <a href="https://play.google.com/store/apps/details?id=fm.bloom.android&amp;hl=en">Bloom.fm</a></figcaption></figure>

There’s a lot going on here. What’s the raindrop supposed to be? Is that a warning for a snowstorm in the bottom left? A musical note overlaying a hamburger menu in the top right, right across the screen from a regular hamburger menu? What am I looking at?

Granted, some users can hit the ground running with these interfaces and learn a lot as they go. But the point is that nothing about this interface gives you a sense of immediate apprehension. It’s not intuitive.

To address this, Bloom.fm might be better served by removing these dissonant symbols from the main screen entirely. Put these functions (whatever they are) in the hidden menu. After all, if you’re on a music player screen, what more do you really need than play, pause, fast forward and rewind?

### Unfamiliarity Breeds Discontent

This brings us to my next point, which is the overarching problem with gestural interfaces: All of the controls and gestural functions are always hidden. You’re depending on a user’s prior familiarity with basic gestural concepts to get along.

This means that any departure from convention will be seen as unfamiliar. Even more problematic is that there’s no industry standard for gestural controls. It’s like the Wild West, but with more tapping and less shooting. Double-tapping might mean one thing in one app and something completely different in another.

Gestural controls can even change between iterations of an application. For instance, the image-sharing application Imgur used the double-tap gesture for zooming in an old version, but an update to the interface changed the gesture to something different entirely. Now it’s used to “upvote” a post (i.e. increasing its popularity and giving the poster fake Internet points).

Which leads to another problem: The learning curve, depending on your attention to usability detail, can be quite steep. While picking up gestural skills is usually pretty easy, as discussed above, the greater room to explore and implement new design patterns means that touch UIs can be highly variable. Variability is roughly equivalent to unpredictability, and that’s the opposite of intuitive.

To combat this, well-designed touch UIs stay in their lane for the most part, relying on visual cues (particularly animations) and text-based explanations in some cases, to establish a connection between a gesture and a function in the user’s mind.</p>

## The Bottom Line

As stated at the beginning of this article, despite any deficiencies that may or may not be innate in the basic concepts of gestural interfaces, the touch UI is here to stay. Its flexibility and mild learning curve (for the basics anyway) practically ensure it.

The bottom line of this whole thing is that, regardless of the benefits and disadvantages, touch is the dominant interface of the future. In other words, you’ll have to find a way to make it work. Proceed with caution, and stick with the familiar whenever possible. The best advice I can give is to keep it simple and test with users above and beyond what’s required. It’s in your best interest to figure out how and when to introduce new controls, to make sure you’re not an example in someone else’s article about UI usability.

If you’d like to learn more about the implementation of touch gestures, check out these helpful resources:

*   “[How to Implement Gestures Into Your Mobile Design](https://thenextweb.com/dd/2015/11/09/how-to-implement-gestures-into-your-mobile-design/),” Carrie Cousins, The Next Web
*   “[Touch Gestures and Events](https://developer.mozilla.org/en-US/Apps/Fundamentals/User_input_methods/Touch_Gestures_and_Events),” Mozilla Developer Network
*   “[Multi-Touch Web Development](https://www.html5rocks.com/en/mobile/touch/),” Boris Smus, HTML5 Rocks
*   “[Touch Events: W3C Editor’s Draft](https://dvcs.w3.org/hg/webevents/raw-file/tip/touchevents.html#methods),” W3C
*   “[Gesture Navigation-Multitouch Gestures for Above Android 4.0.3+](https://repo.xposed.info/module/ind.fem.black.rayyan.xposed.gesturenavigation),” Xposed Module Repository

{{< signature "da, vf, al, il" >}}

