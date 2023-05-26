---
title: Best Practices For Animated Progress Indicators
slug: best-practices-for-animated-progress-indicators
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70d6992a-fa76-4ba6-af93-a3bab968af12/adorable-kitten.gif
date: 2016-12-07T19:29:17.000Z
author: nickbabich
description: >-
  Visibility of system status is one of the most important principles in user
  interface design. Users want to feel in control of the system they’re using,
  which means they want to know and understand their current context at any
  given time, and especially when a system is busy doing work. A wait-animation
  progress indicator is the most common form of providing a system status for
  users when something is happening or loading.

  While an instant response from an app is the best, there are times when your
  app won’t be able to comply with the guidelines for speed. A slow response
  could be caused by a bad internet connection, or an operation itself can take
  a long time (e.g. install an update for OS). For such cases, in order to
  minimize user tension, you must [reassure users that the app is working on
  their
  request](https://www.smashingmagazine.com/2015/12/performance-matters-part-3-tolerance-management/)
  and that actual progress is being made. Thus, you should provide feedback to
  the user about what is happening with the app within a reasonable amount of
  time.
categories:
  - UX
  - User Interaction
  - Performance
  - UX
  - Sponsored Content
---
Visibility of system status is one of the most important principles in user interface design. Users want to feel in control of the system they’re using, which means they want to know and understand their current context at any given time, and especially when a system is busy doing work. A wait-animation progress indicator is the most common form of providing a system status for users when something is happening or loading.

To get a better understanding of how your UI designs can benefit from animated progress indicators, it will help to sketch out your (app) ideas. A few months back, Adobe introduced a new design and wireframing app called Experience Design (or Adobe XD), designed for creating interactive wireframes and user interfaces. The app is still in public beta, with features added on a regular base, and you can [download and try it out for free](https://adobe.ly/2hej6U0). In this article, we'll explore the main types of animated progress indicators and provide recommendations on when and how to use each type.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How Functional Animation Helps Improve User Experience](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/)
*   [In-App Gestures And Mobile App User Experience](https://www.smashingmagazine.com/2016/10/in-app-gestures-and-mobile-app-user-experience/)
*   [Best Practices For Animated Progress Indicators](https://www.smashingmagazine.com/2016/12/best-practices-for-animated-progress-indicators/)
*   [Animated Microinteractions In Mobile Apps](https://www.smashingmagazine.com/2016/08/experience-design-essentials-animated-microinteractions-in-mobile-apps/)

## Good Interaction Design Provides Feedback

While an instant response from an app is the best, there are times when your app won’t be able to comply with the guidelines for speed. A slow response could be caused by a bad internet connection, or an operation itself can take a long time (e.g. install an update for OS). For such cases, in order to minimize user tension, you must reassure the users that the app is working on their request and that actual progress is being made. Thus, you should provide feedback to the user about what is happening with the app within a reasonable amount of time.

{{% feature-panel %}}

### Always Give Some Type of Immediate Feedback

A user’s wait time begins the moment they initiate an action, and the worst case is when they don’t have any indicator the system has received it. When an app fails to notify users that it’s taking time to complete an action, users often think the app didn’t receive the request, and they try again. Plenty of extra clicks and taps have resulted due to a lack of feedback.

Any action, such as clicking a button or pulling to refresh, should have an immediate reaction. It’s essential to give some visual feedback immediately after receiving the request from the user to indicate that the process has initiated.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a943661d-3763-4e66-b22f-f5196d6d6718/pull-to-refresh-action.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a943661d-3763-4e66-b22f-f5196d6d6718/pull-to-refresh-action.gif" width=“600" height="450" alt="Pull-To-Refresh action. Image credit: Behance" /></a><figcaption>Pull-To-Refresh action Image credit: <a href="https://www.behance.net/gallery/24541501/Gear-Powered-Pull-to-Refresh-UI-animation">Behance</a> </figcaption></figure>

## Use A Progress Indicator For Any Action That Takes Longer Than One Second

When the app takes more than 0.1 second but less than one second to respond to user input, it feels like the app is causing the result to appear. Although users notice a short delay, they stay focused on their current task. After one second, the user’s attention begins to wander, and they notice that they’re waiting for a slow app to respond.

In order to reduce a user’s uncertainty, offer a reason to wait with a progress indicator for any action that takes longer than about _one second_ (Note: the use of animation isn’t recommended for anything that takes less than one second to load, because users might feel anxious about what just flashed on the screen). Animated progress indicators mitigate the negative effects of waiting and prolong the user’s attention on the site or in the app.</p>

## Types Of Progress Indicators

Progress indicators tell users that the app needs more time to process the last user action. The simplest form of process indicator is _indeterminate_ — these types of indicators request users to wait while something finishes, but they don’t indicate how long it will take.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc60a4a-8ba9-4791-b49c-007e797254d6/infinite-looped-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc60a4a-8ba9-4791-b49c-007e797254d6/infinite-looped-animation.gif" width=“600" height="300" alt="" /></a><figcaption>Infinite looped animation offers feedback that the system is working, but doesn’t provides any information about how long the user will have to wait. Image credit: <a href="https://www.behance.net/gallery/18484593/Loader-App-(Gifs)">Behance</a></figcaption></figure>

As a general rule, you should use this type of progress indicator for fast actions (2–10 seconds). Making the user stare at a spinning wheel or infinite linear animation longer can increase bounce rates for your website or cause people to close your app.

Another type of progress indicators tell _how long an operation will take_ (approximately or exactly). These types of indicators are called _determinate._ They are the most informative type of wait-animation feedback since they show the current progress, how much has already been accomplished, and how much is left. A visual indicator that progresses towards completion puts the user at ease and increases their willingness to wait.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25aa6961-dece-4e11-aa8b-54b0d26dba6d/indeterminate-indicators.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25aa6961-dece-4e11-aa8b-54b0d26dba6d/indeterminate-indicators.gif" width=“780" height="" alt="Indeterminate indicators visualize an unspecified wait time, while determinate indicators display how long an operation will take." /></a><figcaption>Indeterminate indicators visualize an unspecified wait time, while determinate indicators display how long an operation will take. Image credit: <a href="https://material.google.com/components/progress-activity.html#progress-activity-types-of-indicators">Material Design</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25aa6961-dece-4e11-aa8b-54b0d26dba6d/indeterminate-indicators.gif">Large preview</a>)</figcaption></figure>

## Two Most Popular Animated Progress Indicators

There are two popular types of animated progress indicators — _looped animation_ and _percent-done indicator_.</p>

### Looped Animation

Since the majority of looped animation is indeterminate and serve a variety of types of delays, including long ones, this type of progress indicator tends to have negative connotations.  For example, a default loading icon in Apple iOS (spinner of gray lines radiating from a central point area) serves a variety of operating system functions, indicating the status of everything from device boot to problems connecting to network or loading data. Because of that, users don’t like to see only a loading spinner with no indication of progress or time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd528521-85ef-4261-a052-186fb23e1f7f/loading-spinner.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd528521-85ef-4261-a052-186fb23e1f7f/loading-spinner.gif" width=“600" height="204" alt="Watching a loading spinner is like watching the clock tick down — when you do, time seems to stop" /></a><figcaption>Watching a loading spinner is like watching the clock tick down &mdash; when you do, time seems to stop. Image credit: <a href="https://www.appance.com/">appance</a></figcaption></figure>

### Percent-done Indicator

A percent-done indicator is a determinate progress indicator that fills from 0% to 100% and never decreases in value. Both linear and circular progress indicators may be percent-done.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03adf8c0-7cd3-4bca-a7fc-6fe23457de51/linear-percent-done-progress-indicator-opt.jpeg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03adf8c0-7cd3-4bca-a7fc-6fe23457de51/linear-percent-done-progress-indicator-opt.jpeg" width=“780" height="" alt="Loading bar" /></a><figcaption>Linear percent-done progress indicator Image credit: <a href="https://stock.adobe.com/stock-photo/progress-loading-bar-flat-style-vector-set-of-ten/84209613">Adobe Stock</a></figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5695b1f4-157c-4e43-b60e-ed7c6cae5374/percentdone-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5695b1f4-157c-4e43-b60e-ed7c6cae5374/percentdone-opt.jpg" width=“600" height="400" alt="Circular percent-done progress indicators" /></a><figcaption>Circular percent-done progress indicators Image credit: <a href="https://stock.adobe.com/stock-photo/progress-loading-bar-flat-style-vector-set-of-ten/84209613">Adobe Stock</a></figcaption></figure>

As a general rule of thumb, you should use a percent-done animation for longer processes that take 10 or more seconds. Based on Jakob Nielsen’s [research about response times](https://www.nngroup.com/articles/response-times-3-important-limits/),  10 seconds is a limit for users to keep their attention on a task, after this time users quickly grow impatient if they don’t have enough information on how long they have to wait for the result.</p>

## Tips For Progress Indicators

You should always try to make the wait more pleasant if you can’t shorten the line.</p>

### Explain Why User is Waiting

Many times, if users are informed, they may be more patient. It can be helpful to add additional clarity by including text that tells the user what is happening or explains why the user is waiting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daa26a4a-cc9b-4bc3-8cee-67233e6e58e8/skyscanner-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daa26a4a-cc9b-4bc3-8cee-67233e6e58e8/skyscanner-opt.png" width=“697" height="49" alt="Skyscanner tells users it’s searching the best flights by checking all available providers" /></a><figcaption><a href="https://www.skyscanner.net/">Skyscanner</a> tells users it’s searching for the best flights by checking all available providers.</figcaption></figure>

### Provide a General Time Estimate for Time-Consuming Tasks

Don’t try to be exact, a simple, “this might take five minutes” can be enough for the users and encourage them to wait it out.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a65cc45-9a87-420e-80ed-1ee385dd1ef9/software-update-estimation-in-apple-ios-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a65cc45-9a87-420e-80ed-1ee385dd1ef9/software-update-estimation-in-apple-ios-opt.png" width=“510" height="300" alt="Software update estimation in Apple iOS" /></a><figcaption>Software update estimation in Apple iOS</figcaption></figure>

### Show Absolute Amount of Work Done

For time-consuming operations where it’s unknown in advance how much work has to be done, it may be impossible to use a percent-done indicator, but you still can provide running progress feedback regarding the absolute amount of work done. In this case, consider showing the number of steps, because knowing the number of steps helps users at least form an approximate estimate.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8956488-511f-4503-b7fe-e764407b822d/installed-field-module-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8956488-511f-4503-b7fe-e764407b822d/installed-field-module-opt.jpg" width=“570" height="90" alt="When the progression can’t be monitored accurately consider showing the number of steps instead of percent number." /></a><figcaption>When the progression can’t be monitored accurately, consider showing the number of steps instead of percent number.</figcaption></figure>

### Don’t Stop a Progress Bar

A progress bar makes users develop an expectation for how fast the action is being processed. As a result, any unexpected freezes will be noticed and will impact user satisfaction. The worst possible case is when progress bar approaches 99% and suddenly stops. Most users will be frustrated by this behavior because it makes them think the app is frozen. Hopefully, there is a simple solution  — you can disguise small delays in your progress bar by moving it instantly and steadily.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f5a6c85-1e88-40fc-8cd4-eaa1a9a3799d/progress-bar-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f5a6c85-1e88-40fc-8cd4-eaa1a9a3799d/progress-bar-opt.gif" width=“540" height="540" alt="Image credit: Behance" /></a><figcaption>Image credit: <a href="https://www.behance.net/gallery/8490779/Progress-bar">Behance</a></figcaption></figure>

### Make Progress Bars Feel Faster to Users

Keep in mind that perception can be just as important as raw speed. In order to [make a progress bar](https://johnnyholland.org/2008/11/the-effect-of-the-progress-bar/) [_feel faster_](https://johnnyholland.org/2008/11/the-effect-of-the-progress-bar/) to users you can start the progressive animation slower and allow it to move faster as it approaches the end. This way, you give users a rapid sense of completion time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0cab7cf-73ed-4f29-9128-97f00e204fe4/make-progress-bar-feel-faster-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0cab7cf-73ed-4f29-9128-97f00e204fe4/make-progress-bar-feel-faster-opt.gif" width=“600" height="450" alt="Image credit: Behance" /></a><figcaption>Image credit: <a href="https://www.behance.net/gallery/23015991/Freebie-Progress-Bar">Behance</a></figcaption></figure>

### Offer a Visual Distraction

Creative progress indicators can reduce a user’s perception of time. If an app gives users something interesting to look at while waiting, this makes users pay less attention to the wait itself. Thus, to ensure people don’t get bored while waiting for something to happen, offer them a distraction. For example, this can be something fun…

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e69352d-ab98-4a0c-9a42-74e651f11e9b/visual-distraction-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e69352d-ab98-4a0c-9a42-74e651f11e9b/visual-distraction-opt.jpg" width=“780" height="" alt="Image Credit: Behance" /></a><figcaption>Image Credit: <a href="https://www.behance.net/de_martin">Behance</a></figcaption></figure>

Or something adorable…

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70d6992a-fa76-4ba6-af93-a3bab968af12/adorable-kitten.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70d6992a-fa76-4ba6-af93-a3bab968af12/adorable-kitten.gif" width=“400" height="300" alt="Image credit: Vimeo" /></a><figcaption>Image credit: <a href="https://vimeo.com/44251833">Vimeo</a></figcaption></figure>

Or something unexpected that catches users’ attention long enough for your app to load.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06d9da74-7240-4e84-8d20-0ad2e7f1bcd8/fine-animations.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06d9da74-7240-4e84-8d20-0ad2e7f1bcd8/fine-animations.gif" width=“598" height="511" alt="Fine animations can distract your visitors and make them ignore long loading times. Image credit: Behanc" /></a><figcaption>Fine animations can distract your visitors and make them ignore long loading times. Image credit: <a href="https://www.behance.net/gallery/19040507/Round-iPhone-app">Behance</a></figcaption></figure>

## Skeleton Screens: A Great Alternative To The Traditional Progress Indicators

As you’ve just learned, when things are going to take a while, we let people know that using progress indicators. However, while the intentions behind progress indicators are good, the end result can turn out to be bad. As Luke Wroblewski mentioned in his [article](https://www.lukew.com/ff/entry.asp?1797): “Progress indicators by definition call attention to the fact that someone needs to wait. It’s like watching the clock tick down — when you do, time seems to go slower.” With the introduction of progress indicators to our UIs, designers often make people watch the clock. While it’s better than nothing, when you design UIs you should always try to make the wait more pleasant.

Hopefully, there’s a good alternative of progress indicators, the technique that lets people have a great experience while they are waiting. And this technique has a name, _skeleton screen_. Skeleton screens (a.k.a temporary information containers) are essentially a blank version of a page into which information is gradually loaded. Rather than show a loading indicator, skeleton screens focus on _actual progress_ and create anticipation of what is to come. This creates the sense that things are happening immediately as information is incrementally displayed on the screen and people think that the application is acting while they wait.

Medium uses this trick, showing a simple wireframe as a placeholder, while the actual content loads. The load screen also makes the user familiar with the overall structure of the content being loaded.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8e87b0-ad0b-468b-ac5b-57c9c820fc09/medium-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e0c8f12-bfc2-4eb5-b5f7-df5fb98f9aba/medium-600px-preview-opt.png" width="600" height="428" alt="Medium" /></a><figcaption>Medium focus on content being loaded, not the fact that it's loading. Image Source: <a href="https://twitter.com/merhl/status/694259963225587712">merhl</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8e87b0-ad0b-468b-ac5b-57c9c820fc09/medium-large-preview-opt.png">Large preview</a>)</figcaption></figure>

## Conclusion

No matter how fast we make our app and sites, there will often be something that takes time to process. Wait animations, such as loading spinners and percent-done indicators, reduce uncertainty by informing users of the current working state and increase the likelihood that the user will stay and wait for the information to load. A rule of thumb is to use a looped indicator or skeleton screens for reasonably fast operations taking between two and ten seconds, and a percent-done indicator for operations taking more than about ten seconds. When choosing between looped animation and skeleton screens, it’s probably a good idea to favor latter because they contain one important advantage — they can improve the feel of any action taking longer than a few milliseconds.</p>

<blockquote>This article is part of the UX design series sponsored by Adobe. The newly introduced <a href="https://adobe.ly/2hej6U0">Experience Design app</a> is made for a fast and fluid UX design process, creating interactive navigation prototypes, as well as testing and sharing them — all in one place. <br /><br />You can check out more inspiring projects created with Adobe XD on <a href="https://adobe.ly/1U9LS0E">Behance</a>, and also visit the Adobe XD blog to stay updated and informed. Adobe XD is being updated with new features frequently, and since it's in public Beta, you can <a href="https://adobe.ly/2hej6U0">download and test it for free</a>.</blockquote>

{{< signature "il, ms, vf, aa" >}}

