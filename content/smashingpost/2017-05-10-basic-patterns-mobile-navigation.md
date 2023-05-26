---
title: 'Basic Patterns For Mobile Navigation: Pros And Cons'
slug: basic-patterns-mobile-navigation
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b93180-b77e-4058-9d88-ff7de3d9966f/youtube-large-opt.png
date: 2017-05-10T19:00:34.000Z
author: nickbabich
description: >-
  Once someone starts using your app, they need to know where to go and how to
  get there at any point. Good navigation is a vehicle that takes users where
  they want to go. But establishing good navigation is a challenge on mobile due
  to the limitations of the small screen and the need to prioritize content over
  chrome.

  Different navigation patterns have been devised to solve this challenge in
  different ways, but they all suffer from a variety of usability problems. In
  this article, we’ll examine five basic navigation patterns for mobile apps and
  describe the **strengths and weaknesses of each** of them. If you’d like to
  add some patterns and spice up your designs, you can download and test Adobe
  XD for free and get started right away.
categories:
  - Coding
  - Mobile
  - Navigation
  - Sponsored Content
---
Different navigation patterns have been devised to solve this challenge in different ways, but they all suffer from a variety of usability problems. In this article, we’ll examine five basic navigation patterns for mobile apps and describe the **strengths and weaknesses of each** of them. If you’d like to add some patterns and spice up your designs, you can download and test [Adobe XD](https://adobe.ly/2q0pi6P) for free and get started right away.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Design Better Buttons](https://www.smashingmagazine.com/2016/11/a-quick-guide-for-designing-better-buttons/)
*   [The Golden Rules Of Bottom Navigation Design](https://www.smashingmagazine.com/2016/11/the-golden-rules-of-mobile-navigation-design/)
*   [How To Design Error States For Mobile Apps](https://www.smashingmagazine.com/2016/09/how-to-design-error-states-for-mobile-apps/)
*   [How Functional Animation Helps Improve User Experience](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/)

## Hamburger Menu

Screen space is a precious commodity on mobile, and the hamburger menu (or side drawer) is one of the most popular mobile navigation patterns for helping you save it. The drawer panel allows you to hide the navigation beyond the left edge of the screen and reveal it only upon a user’s action.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b89fee9-9312-4f6d-829e-3dbf52aebb22/hamburger-menu-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a41e333-86e4-4504-9f28-6a21dba54d4a/hamburger-menu-780w-opt.png" width="780" height="663" alt="" /></a><figcaption>In its default state, the hamburger menu and all of its contents remain hidden. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b89fee9-9312-4f6d-829e-3dbf52aebb22/hamburger-menu-large-opt.png">View large version</a>)
</figcaption></figure>

## When To Use

The main downside of the hamburger menu is its [low discoverability](https://thenextweb.com/dd/2014/04/08/ux-designers-side-drawer-navigation-costing-half-user-engagement/), and it’s not recommended as the main navigation menu. However, this pattern might be an appropriate solution for secondary navigation options. Secondary navigation options are destinations or features that are important for users only in certain circumstances. Being secondary, they can be relegated to less prominent visual placement, as long as users can quickly find a utility when they need it. By hiding these options behind the hamburger icon, designers avoid overwhelming users with too many options.

Uber uses a hamburger icon for this purpose. Because everything about the main screen of the Uber app is focused on requesting a car, there’s no need to display secondary options such as “Payment,” “History” or “Settings.” The normal user flow doesn’t include these actions, and so they can be hidden behind the hamburger icon.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69e603b5-8475-4e7e-88a5-d00f06565ebb/uber-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69e603b5-8475-4e7e-88a5-d00f06565ebb/uber-preview-opt.png" width="415" height="720" alt="" /></a></figure>

### Pros

*   **Large number of navigation options**  
    The main advantage of the navigation menu is that it can accommodate a fairly large number of navigation options in a tiny space.
*   **Clean design**  
    The hamburger menu allows the designer to free up screen real estate by shifting options off screen into a side menu. This pattern can be particularly useful if you want the user to focus on the main content.</p>

### Cons

<ul><br>
<li><strong>Less discoverable</strong><br>
What’s out of sight is out of mind. When navigation is hidden, users are less likely to use it. While this type of navigation is becoming standard and many mobile users are familiar with it, many people still simply don’t think to open it.</li>

<li><strong>Clashes with platform navigation rules</strong><br>
The hamburger menu has become almost a standard on Android (the pattern has the name “<a href="https://material.io/guidelines/patterns/navigation-drawer.html">navigation drawer</a>” in material design), but in iOS it simply cannot be implemented without clashing with basic navigation elements, and this could overload the navigation bar.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02f31ee1-394f-460a-be5a-534954ca64ec/navigation-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02f31ee1-394f-460a-be5a-534954ca64ec/navigation-preview-opt.png" width="640" height="88" alt="" /></a><figcaption>(Image: <a href="https://lmjabreu.com/post/why-and-how-to-avoid-hamburger-menus/">lmjabreu</a>)
</figcaption></figure>

</li>

<li>The hamburger icon hides context. The hamburger menu doesn’t communicate the current location at a glance: <a href="https://www.nngroup.com/articles/hamburger-menus/">Surfacing information</a> about the current location is harder because it’s only visible when the person clicks on the hamburger icon.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6d01706-0179-4fdc-a4f3-beda1df9334b/the-hamburger-icon-hides-context.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6d01706-0179-4fdc-a4f3-beda1df9334b/the-hamburger-icon-hides-context.gif" width="320" height="568" alt="" /></a><figcaption>Out of sight, out of mind. The hamburger menu hides the user’s current location in the app.</figcaption></figure>

</li>

<li>Extra action is required to move to the target destination. Reaching a particular page usually takes at least two taps (one tap on the menu icon and another on the target option).</li>
</ul>

### Tips

<ul><br>
<li>Prioritize the navigation options. If the navigation is complex, hiding it won’t make it user-friendly. A lot of practical examples clearly show that exposing menu options in a more visible way <a href="https://www.lukew.com/ff/entry.asp?1945">increases engagement and user satisfaction</a>. Ask yourself, What’s important enough to be visible on mobile? Answering that question will require an understanding of what matters to your users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86c13574-29ef-4a60-965c-3e3870e85cfe/navigation-options-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86c13574-29ef-4a60-965c-3e3870e85cfe/navigation-options-preview-opt.png" width="750" height="400" alt="" /></a><figcaption>Redbooth’s move from a hamburger menu to a bottom tab bar resulted in <a href="https://redbooth.com/blog/hamburger-menu-iphone-app?utm_campaign=iOS_Dev_Weekly_Issue_181&utm_medium=email&utm_source=iOS%2BDev%2BWeekly">increased user sessions.</a> (Image: <a href="https://twitter.com/lukew/status/562297190735806464">LukeW</a>)
</figcaption></figure>

</li>

<li>Consider using tabs or a tab bar if you have a limited number of high-priority navigation options.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b93180-b77e-4058-9d88-ff7de3d9966f/youtube-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7565c867-6716-4e64-85d1-bce1514dfeba/youtube-780w-opt.png" width="780" height="438" alt="" /></a><figcaption>YouTube makes the main pieces of core functionality available with one tap, allowing rapid switching between features. (Source: Luke Wroblewski) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b93180-b77e-4058-9d88-ff7de3d9966f/youtube-large-opt.png">View large version</a>)
</figcaption></figure>

</li>

<li>Review your information architecture. Good apps are highly focused. So, if you have one complex app, you could split its functionality into two (or more) simple apps. Facebook released its Messenger app in order to <a href="https://www.businessinsider.com/why-is-facebook-messenger-a-separate-app-2014-11">solve the problem of complexity</a>. The reduced functionality results in a reduced set of menu options, and less need for a hamburger menu.</li>
</ul>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cb50738-5f9d-4158-8129-05161b964ca9/facebook-800-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f438b8d4-f29a-4a1c-ba5e-651823804133/facebook-780w-opt.png" width="780" height="408" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cb50738-5f9d-4158-8129-05161b964ca9/facebook-800-opt.png">View large version</a>)
</figcaption></figure>

## Tab Bar

The tab bar pattern is inherited from desktop design. It usually contains relatively few destinations, and those destinations are of similar importance and require direct access from anywhere in the app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d2ed102-fdcf-46b6-a582-1ad205e495ac/tab-bar-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d2ed102-fdcf-46b6-a582-1ad205e495ac/tab-bar-preview-opt.png" width="512" height="" alt="" /></a><figcaption>The tab bar doesn’t hide navigation, but allows direct access and presents feedback on the icon it’s related to.
</figcaption></figure>

## When To Use

Tabbed navigation is a great solution for apps with relatively few top-level navigation options (up to five). The tab bar makes the main pieces of core functionality available with one tap, allowing rapid switching between features.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af12de18-f89e-4d8b-8def-01b1777125b5/tab-bar-in-twitter-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af12de18-f89e-4d8b-8def-01b1777125b5/tab-bar-in-twitter-preview-opt.png" width="338" height="" alt="" /></a><figcaption>The tab bar in Twitter lets the user navigate directly to the screen associated with the item.
</figcaption></figure>

### Pros

<li>The tab bar fairly easily communicates the current location. Properly used visual cues (icons, labels and colors) enable the user to understand their current location at a glance.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/031254ce-e593-4e5c-91a6-ad022d32e579/tab-bar-pros.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/031254ce-e593-4e5c-91a6-ad022d32e579/tab-bar-pros.gif" width="780" height="" alt="" /></a><figcaption>(Image: <a href="https://ramotion.com/">Ramotion</a>)
</figcaption></figure>

</li>

<li>Tab bars are persistent. The navigation remains in sight no matter what page the user is viewing. The user has clear visibility of all the main app views and has single-click access to them.</li>

<li>With a thumb zone, the bottom navigation is easier to reach with the thumb when the device is held in one hand.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21491084-1bfe-402b-9860-14b7de148af8/thumb-zone-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fda19be0-4db2-4145-86ca-ef1ed57e3e3d/thumb-zone-780w-opt.jpg" width="780" height="560" alt="" /></a><figcaption>Ideal placement of navigation for the thumb zone, according to <a href="https://uxmag.com/articles/excerpt-from-the-new-book-the-mobile-frontier">UXmag.</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21491084-1bfe-402b-9860-14b7de148af8/thumb-zone-large-opt.jpg">View large version</a>)
</figcaption></figure>

</li>

### Cons

<li>The navigation options are limited. If your app has more than five options, then fitting them in a tab or navigation bar and still keeping an optimum touch-target size would be hard.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e815352-9653-4837-a552-7f5f735c17c6/tab-bar-cons-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e815352-9653-4837-a552-7f5f735c17c6/tab-bar-cons-preview-opt.jpg" width="720" height="" alt="" /></a><figcaption>Don’t use more than five options in a tab bar.
</figcaption></figure>

</li>

<li>The location and logic of the tab bar options on iOS and Android are different. Platforms have different rules and guidelines for UI and usability, and you have to take them into consideration when designing a tab bar for a particular platform. Tabs appear at the top of the screen on Android and at the bottom of the screen on iOS. This happens presumably because Android’s control bar at the bottom is hardware. Please note that this rule doesn’t apply to mobile websites, because the experience with them should be consistent regardless of the device used to browse them (Android or iOS).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/674a517a-5330-4524-a6b2-9b6d4fb1475f/tab-bar-cons-1-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/674a517a-5330-4524-a6b2-9b6d4fb1475f/tab-bar-cons-1-preview-opt.png" width="620" height="" alt="" /></a><figcaption>Proper location and logic will help to maintain a consistent experience with other apps on the platform and prevent confusion between actions and view-switching. (Image: <a href="https://design.google.com/articles/design-from-ios-to-android/">Google</a>)
</figcaption></figure>

</li>

## Tips

<ul><br>
<li>Make touch targets big enough to be easily tapped or clicked. To calculate the width of each bottom navigation action, divide the width of the view by the number of actions. Alternatively, make all bottom navigation actions the width of the largest action.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c8d72fd-5b14-49cc-86e3-7874fecfe6e5/touch-targets-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c8d72fd-5b14-49cc-86e3-7874fecfe6e5/touch-targets-preview-opt.jpg" width="320" height="" alt="" /></a><figcaption>Most users can comfortably and reliably hit a 10 &#215; 10-millimeter touch target. (Image: <a href="https://uxmag.com/articles/excerpt-from-the-new-book-the-mobile-frontier">UXmag</a>)
</figcaption></figure>

</li>

<li>Order the navigation options. Users expect to see a certain order in the tab bar. The first tab item has to be the home screen of the app, and the order of tabs should reflect their priority or the logical order in the user flow. One of the tabs should always be active and <a href="https://www.nngroup.com/articles/tabs-used-right/">visually highlighted</a>.</li>

<li>Test your icons for usability. As you can see in the example below, app designers sometimes hide functionality behind icons that are pretty hard to recognize. To prevent this from happening, <a href="https://www.nngroup.com/articles/icon-usability/">test your icons with the five-second rule</a>: If it takes you more than five seconds to think of an appropriate icon for something, then it is unlikely that an icon can effectively communicate that meaning.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/503ef466-737f-4f6e-a1e2-184edf27db9f/bloom.fm-app-preview-opt"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/503ef466-737f-4f6e-a1e2-184edf27db9f/bloom.fm-app-preview-opt" width="639" height="" alt="" /></a><figcaption>Bloom.fm app has a tab bar full of abstract icons.
</figcaption></figure>

</li>

<li>If an icon fails the five-second rule (i.e. <a href="https://www.smashingmagazine.com/2016/10/icons-as-part-of-a-great-user-experience/">isn’t self-evident</a>), it needs a text label. It’s pretty rare in the offline world that we rely on iconography alone to represent ideas &mdash; and for good reason. Due to the <a href="https://www.nngroup.com/articles/icon-usability/">absence of a standard usage</a> for most icons, text labels are necessary to communicate meaning and reduce ambiguity. Users should understand what exactly will happen before they tap on an element.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c20ba7b5-5bf8-4bf6-84a8-b98d0e9bab1b/bottom-navigation-icons-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd8cecfa-7895-4a7c-8e30-ca462814b6a9/bottom-navigation-icons-780w-opt.png" width="780" height="262" alt="" /></a><figcaption>Use text labels to provide short, meaningful definitions to bottom navigation icons. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c20ba7b5-5bf8-4bf6-84a8-b98d0e9bab1b/bottom-navigation-icons-large-opt.png">View large version</a>)
</figcaption></figure>

</li>

</ul>

## Priority+ Pattern

The "[Priority+](https://justmarkup.com/log/2012/06/19/responsive-multi-level-navigation/)" pattern was coined by Michael Scharnagl to describe navigation that exposes what’s deemed to be the most important navigation elements and hides away less important items behind a “more” button.</p>

### When to Use

This pattern might be good solution for content-heavy apps and websites with a lot of different sections and pages (such as a news website or a large retailer’s store). [The Guardian](https://www.theguardian.com/) makes use of the priority+ pattern for its section navigation. Less important items are revealed when the user hits the “All” button.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/048983a9-93f1-42b9-b062-6370b9461deb/bradfrost.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/048983a9-93f1-42b9-b062-6370b9461deb/bradfrost.gif" width=“780" height="" alt="" /></a><figcaption>The Guardian employs the Priority+ pattern for its section navigation.  Image credit: <a href="https://bradfrost.com/blog/post/revisiting-the-priority-pattern/">bradfrost</a><br>
</figcaption></figure>

### Pros

*   This pattern prioritizes navigation options. It surfaces the most frequently accessed navigation options.
*   It makes use of available screen space. As space increases, the number of exposed navigation options increases as well, which can result in better visibility and more engagement.
*   This menu is very adaptive. You can scale it quite nicely across screen sizes without having to transform the pattern.</p>

### Cons

*   It might hide some important navigation options. The priority+ pattern requires designers to assume the relative importance of navigation items. Be aware that the items you prioritize to be visible might not be the same ones users are looking for most.</p>

## Floating Action Button

Shaped like a circled icon floating above the UI, the floating action button changes color upon focus and lifts upon selection. It’s well known by all Android users and is a distinct element of material design. Floating above the interface of an app, it promotes user action, [says Google](https://material.io/guidelines/components/buttons-floating-action-button.html#).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f6e089-a827-43fe-986b-4c80a9f57d74/action-button-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f6e089-a827-43fe-986b-4c80a9f57d74/action-button-preview-opt.png" width="720" height="" alt="" /></a><figcaption>Floating action button
</figcaption></figure>

### When to Use

The design of the floating action button hinges on the premise that users will perform a certain action most of the time. You can make this “hero” action even more heroic by reinforcing the sense that it is a core use case of your app. For example, a music app might have a floating action button that represents “play.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d12ce354-77a7-43b0-bf47-f22706ce4e2c/fab-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d12ce354-77a7-43b0-bf47-f22706ce4e2c/fab-preview-opt.png" width="720" height="" alt="" /></a><figcaption>Use the floating action button for actions that are strongly characteristic of your app. Playback tells users that this is a music app.
</figcaption></figure>

The button is a natural cue to users for what to do next. In user research, [Google found](https://youtu.be/dZqzz5lZFvo?t=23m9s) that users understand it as a wayfinding tool. When faced with an unfamiliar screen, as many users are regularly (like when running an app for the first time), they will use the floating action button to navigate. Thus, it is a way to prioritize the most important action you want users to take.</p>

### Pros

*   It’s a signpost of what’s important. It’s a good way to prioritize the most important action you want users to take.
*   It takes up little screen space. Compared to the tab bar, it doesn’t take up an entire row.
*   A visually pleasing UI element such as this might not improve usability. However, emotion is a factor in user experience. If a user is pleased to use an app because they find it visually attractive, then that would create positive UX effects.
*   It also improves effectiveness. A study by [Steve Jones demonstrates](https://stevejones.io/img/projects/honors-thesis/SteveJones-Honors-Thesis.pdf) that a floating action button slightly impairs usability when users first interact with the button. However, once users have successfully completed a task using the element, they are able to use it more efficiently than a traditional action button.</p>

### Cons

<ul><br>
<li>A floating action button can distract users from content. It is designed to stand out &mdash; it is colorful, raised and grid-breaking. Its design is meant to draw the user's attention. But sometimes its presence can distract the user from the main content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5581af6-9a94-428c-9c2c-76d3b62ca1e5/red-fab-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a89eb45e-fd29-4e63-a611-b6dad4582791/red-fab-780w-opt.jpg" width="780" height="585" alt="" /></a><figcaption>A red button stands out from the background and focuses user attention. (Image: <a href="https://dribbble.com/PaulVanO">Paul van Oijen</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5581af6-9a94-428c-9c2c-76d3b62ca1e5/red-fab-large-opt.jpg">View large version</a>)
</figcaption></figure>

</li>

<li>It can block content. Take Google’s Gmail app for instance. In the example below, you can see that it blocks the “favorite” star, as well as the time stamp for the last row. Additional scrolling is needed whenever the user wants to see this information.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/217643d0-f2bb-4135-ac43-08a59400aa85/gmail-app-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/217643d0-f2bb-4135-ac43-08a59400aa85/gmail-app-preview-opt.png" width="506" height="" alt="" /></a></figure>

</li>

<li>It is also icon-only navigation. By design, the floating action button is a circle containing an icon. It’s an icon-only button, with no room for text labels. The problem is that <a href="https://uxmyths.com/post/715009009/myth-icons-enhance-usability">icons are incredibly hard to understand</a> because they’re so open to interpretation. Even a simple action icon like the pencil in the example below can mean different things in different apps.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af60c190-3607-4dd8-90c0-8d6ccd75fa63/icon-only-navigation-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac9cffa5-67bf-4777-b103-2bb04623c0fe/icon-only-navigation-780w-opt.jpg" width="780" height="678" alt="" /></a><figcaption>Same icon, different meanings: “Compose” in the Gmail and Inbox apps, but “Edit” in the Snapseed app. Here, context helps to explain the action. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af60c190-3607-4dd8-90c0-8d6ccd75fa63/icon-only-navigation-large-opt.jpg">View large version</a>)
</figcaption></figure>

</li>

</ul>

### Tips

<ul><br>
<li>Because it is so prominent and intrusive, use only one per screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cddcb2a-3aa4-4967-b30f-d4246bc4281c/multiple-fabs-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4606f754-f3d4-4596-9778-cc43399f4a13/multiple-fabs-780w-opt.png" width="780" height="635" alt="" /></a><figcaption>Multiple floating action buttons should never appear on screen at one time because that would confuse the visual hierarchy. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cddcb2a-3aa4-4967-b30f-d4246bc4281c/multiple-fabs-large-opt.png">View large version</a>)
</figcaption></figure>

</li>

<li>Not every screen should have one, simply because not every screen has an action of such importance.</li>

<li>The floating action button is strongly <a href="https://material.io/guidelines/components/buttons-floating-action-button.html#buttons-floating-action-button-floating-action-button">associated with positive actions</a>. Because it is full of character, it’s generally taken to be a positive action, like create, favorite, navigate, search and so on. Don’t use it for destructive actions, like delete.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1398832-7b7b-4d30-a788-fa6ffeb05f0d/fab-1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea719399-6152-406f-ad82-9bd081e83f96/fab-1-780w-opt.png" width="780" height="217" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1398832-7b7b-4d30-a788-fa6ffeb05f0d/fab-1-large-opt.png">View large version</a>)
</figcaption></figure>

</li>

<li>The floating action button could be replaced with a sequence of more specific actions. This would help to surface a set that doesn’t really belong at the top but is still important. Apps such as Evernote simplify the controls by using a floating action button for the most important user actions.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bc60f7f-b8ad-4532-84c1-7bcb483c58e9/fab.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bc60f7f-b8ad-4532-84c1-7bcb483c58e9/fab.gif" width="336" height="" alt="" /></a></figure>

</li>

<li>It can improve transitions between screens, too. The floating action button is not just a round button; it has some transformative properties that you can use to ease users from screen to screen. It can expand, morph and react.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94e729c0-d6bb-4d14-a419-07f160f289b3/fab-1.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94e729c0-d6bb-4d14-a419-07f160f289b3/fab-1.gif" width="780" height="" alt="" /></a><figcaption>(Image: <a href="https://dribbble.com/anish_chandran">Anish Chandran</a>)
</figcaption></figure>

</li>

</ul>

## Full-Screen Navigation

While with other patterns mentioned in this article, you’d be struggling to minimize the space that the navigation systems take up, the full-screen pattern takes the exact opposite approach. This navigation approach usually devotes the home page exclusively to navigation. Users incrementally tap or swipe to reveal additional menu options as they scroll up and down.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb272f2-35d3-40f2-8967-587a2f35cc14/full-screen-navigation-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b26011f3-4a65-4a36-92c4-f5d4863e4a3e/full-screen-navigation-780w-opt.png" width="780" height="268" alt="" /></a><figcaption>(Image: <a href="https://www.smashingmagazine.com/2014/10/wayfinding-for-the-mobile-web/">Smashing Magazine</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb272f2-35d3-40f2-8967-587a2f35cc14/full-screen-navigation-large-opt.png">View large version</a>)
</figcaption></figure>

### When to Use

This pattern works well in task-based and direction-based websites and apps, especially when users tend to limit themselves to only one branch of the navigation hierarchy during a single session. Funnelling users from broad overview pages to detail pages helps them to home in on what they’re looking for and to focus on content within an individual section.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e37e54-c6de-41d3-a49d-17525ca11c86/yelp-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e37e54-c6de-41d3-a49d-17525ca11c86/yelp-preview-opt.png" width="600" height="" alt="" /></a><figcaption>Full-screen navigation options in Yelp
</figcaption></figure>

### Pros

*   The full-screen navigation pattern is best for achieving simplicity and coherence. You can organize large chunks of information in a coherent manner and reveal information without overwhelming the user; once the user makes their decision about where to go, then you can dedicate the entire screen space to content.</p>

### Cons

*   Prime real estate will be wasted on chrome. You won’t be able to display any content except the navigation options.</p>

### Tips

<ul><br>
<li>Use a hamburger menu to hide secondary functionality and keep the focus on the main experience.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45e19595-e560-43e8-9097-b5131eefb7bc/cookly-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45e19595-e560-43e8-9097-b5131eefb7bc/cookly-preview-opt.png" width="640" height="" alt="" /></a><figcaption>(Image: Cookly via <a href="https://dribbble.com/shots/1353546-Mobile-Self-Service-Support-Communities/attachments/192600">Dribbble)</a><br>
</figcaption></figure>

</li>
</ul>

## Gesture-Based Navigation

29 June 2007 was a game changer. From the moment Apple launched the first fully touchscreen smartphone on the market, mobile devices have been dominated by touchscreen interaction.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9336a118-b104-4a4a-9839-0ad0f36b09ec/touch-gestures.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9336a118-b104-4a4a-9839-0ad0f36b09ec/touch-gestures.gif" width="780" height="" alt="" /></a><figcaption>(Image: <a href="https://dribbble.com/areus">Aaron Wade</a>)
</figcaption></figure>

Gestures immediately became popular among designers, and many apps were designed around experimenting with gesture controls.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87247a8a-97ad-4295-b259-524db6dbfbfb/gesture-driven-to-do-app-clear-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87247a8a-97ad-4295-b259-524db6dbfbfb/gesture-driven-to-do-app-clear-preview-opt.jpg" width="575" height="" alt="" /></a><figcaption>Gesture driven to-do app Clear
</figcaption></figure>

In today’s world, the success of a mobile app can largely depend on how well gestures are implemented in the user experience.</p>

### When to Use

This pattern is good when users want to explore the details of particular content easily and intuitively. Users will spend more time with content than they will with navigation menus. So, one of the reasons to use in-context gestures instead of a standard menu is that it’s more engaging. For example, as users view page content, they can tap on a card to learn more.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/494ad921-5d29-4935-b7e0-30c30fe337b5/github.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/494ad921-5d29-4935-b7e0-30c30fe337b5/github.gif" width="400" height="" alt="" /></a><figcaption>This type of navigation takes users on a journey of what they’re interested in. Menus simply don’t have this engaging effect. (Image: <a href="https://www.ramotion.com/">Ramotion</a>)
</figcaption></figure>

### Pros

*   It removes UI clutter. Building gestures into the heart of your design allows you to make your interfaces more minimal and to save screen space for valuable content.
*   The UI is more natural. Luke Wroblewski talks about a [study](https://www.lukew.com/ff/entry.asp?1197) in which 40 people in 9 different countries were asked to create gestures for 28 different tasks, such as deleting, scrolling and zooming. He found that the gestures tend to be similar across culture and experience. For example, when prompted to “delete,” most people — regardless of nationality — tried dragging the object off screen.
*   Gestures can be a distinctive feature of a product. Tinder has massively popularized the concept of gesture-based navigation and basically made those swipes a product-defining gesture.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2c9cf83-0650-494a-a6ce-f147415edbc5/tinder-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4105349-ac49-4e6a-8ad1-49fe4c63485d/tinder-780w-opt.png" width="780" height="" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2c9cf83-0650-494a-a6ce-f147415edbc5/tinder-large-opt.png">View large version</a>)
</figcaption></figure>

### Cons

<li>The navigation is invisible. One important rule in designing a UI is visibility: Through the menus, all possible actions should be made visible and, therefore, easily discoverable. An invisible UI can be seductively beautiful, but because it’s invisible, it will likely have <a href="https://www.jnd.org/dn.mss/gestural_interfaces_a_step_backwards_in_usability_6.html">many usability issues</a>.</li>

<li>User effort increases. Most gestures are neither natural nor easy to learn or remember. When designing gesture-based navigation, be aware that every time you remove UI clutter, the application’s learning curve goes up; and without proper visual hints and cues, users could get confused about how to interact with the app.</li>

### Tips

<ul><br>
<li>Make sure you don’t have to teach people a whole new way to interact with an interface. Design a familiar experience. In order to design good gesture-based navigation, start by looking at the current state of gestures in the mobile world. For example, if you’re designing an email app, you could use a swipe instead of an email gesture, because there’s a strong possibility that the gesture would be familiar to many users:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4afb130-8236-43d9-a5af-8e96c4af17c5/gmail-inbox-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4afb130-8236-43d9-a5af-8e96c4af17c5/gmail-inbox-preview-opt.png" width="600" height="" alt="" /></a></figure>

</li>

<li>Educate in context to teach people how to interact with your interface. Avoid long static up-front tutorials. Instead, show only the information that is relevant to the user’s current activity.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/404ea3d6-1eec-4e06-986a-f119144d4da0/pudding-monsters.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/404ea3d6-1eec-4e06-986a-f119144d4da0/pudding-monsters.gif" width="360" height="" alt="" /></a><figcaption>Pudding Monsters uses an animated hand to present a new scenario to users.
</figcaption></figure>

</li>

</ul>

## 3D Touch

3D Touch is a subtle touch mechanism that was first introduced in Apple’s iPhone 6s and 6s Plus. It allows for some new interactions, which Apple defines in two main categories:

<ul><br>
<li><strong>Quick actions</strong><br>
The iOS home screen isn’t just a grid of apps anymore, because 3D Touch allows users to perform actions specific to an app outside of the app, right from the home screen. Pressing firmly on an app icon presents a short list of quick actions: Jump right into taking a selfie from the Camera icon, or immediately navigate to your favorite contacts from the Messages app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6bfee0-a8d7-471e-adde-ef6a33360ee6/3d-touch-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60f5f141-cb6d-4653-937b-3be0a41fcec2/3d-touch-780w-opt.jpg" width="780" height="492" alt="" /></a><figcaption>3D Touch quick-action shortcuts for the camera, messages and maps apps (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6bfee0-a8d7-471e-adde-ef6a33360ee6/3d-touch-large-opt.jpg">View large version</a>)
</figcaption></figure>

</li>

<li><strong>Peek and pop</strong><br>
3D Touch allows users to preview content and perform related actions within an app before deciding whether to view the full content. When users press firmly on a piece of content &mdash; such as a mail message in a list &mdash; 3D Touch opens a preview of what that content contains.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24a2a0fc-e168-4929-8f1e-b68388cec59f/3d-touch.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24a2a0fc-e168-4929-8f1e-b68388cec59f/3d-touch.gif" width="636" height="" alt="" /></a><figcaption>3D Touch immediately previews an email, which disappears when the user removes their finger. (Image: <a href="https://gizmodo.com/the-10-best-things-to-do-with-3d-touch-and-the-things-1733554205">Gizmodo</a>)
</figcaption></figure>

</li>

</ul>

### When to Use

Using 3D Touch, you can make the most frequent actions the most accessible. Think of 3D Touch like keyboard shortcuts on a desktop computer: They enable people to do repeated tasks more quickly. You can use 3D Touch to help users skip a few steps or to avoid unnecessary steps altogether.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a2dc842-7dff-427b-95f5-f51e075016de/3d-touch-1.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a2dc842-7dff-427b-95f5-f51e075016de/3d-touch-1.gif" width="636" height="" alt="" /></a><figcaption> From the home screen, the camera lets users access common features: taking a selfie, recording video or taking a normal photo. (Image: <a href="https://gizmodo.com/the-10-best-things-to-do-with-3d-touch-and-the-things-1733554205">Gizmodo</a>)
</figcaption></figure>

However, just like keyboard shortcuts, essential features shouldn’t be exclusive to 3D Touch. Users must be able to operate your app normally without it.</p>

### Pros

*   With its shortcut actions, 3D Touch has the potential to save users a lot of time by skipping several taps within an app.
*   By simplifying an interface, 3D Touch enables quick, lightweight interaction. It gives designers and developers new opportunities to simplify their interfaces, while surfacing enhanced functionality for users.</p>

### Cons

*   Users have to remember which apps have quick actions. 3D Touch still isn't ubiquitous on iOS. Some apps have it, others don't. Users sometimes expect 3D Touch shortcuts for apps that don’t have them.</p>

## Innovative Navigation Patterns

People are shifting to larger-screen phones. Large smartphones don’t surprise anyone anymore. But the bigger the display is, the [less easily accessible](https://scotthurff.com/posts/how-to-design-for-thumbs-in-the-era-of-huge-screens) most of the screen is, and the more necessary it is to adapt the design (and navigation, in particular) to improve the user experience.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c66aba5-d4d7-4b0d-a723-981e28cad2f2/innovative-navigation-patterns.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c66aba5-d4d7-4b0d-a723-981e28cad2f2/innovative-navigation-patterns.png" width="780" height="" alt="" /></a><figcaption>(Image: <a href"https://www.lukew.com">LukeW</a>)
</figcaption></figure>

To solve this problem, designers are forced to look for new solutions to navigation. A couple of interesting innovative solutions can be found in the recently published article “[Bottom Navigation Interface](https://blog.prototypr.io/bottom-navigation-interface-fa4bff52065f).” One solution can be found in a health app named [Ada](https://ada.com). This app’s interface layout is a mirror image of a basic interface with a hamburger menu: Everything that’s usually at the top is conveniently at the bottom, in the easy-to-access zone.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62f34dad-9a95-459f-bb5f-53f08f567a4d/ada.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62f34dad-9a95-459f-bb5f-53f08f567a4d/ada.png" width="780" height="" alt="" /></a><figcaption>The start screen in Ada for iOS
</figcaption></figure>

The second solution is a concept for a calling app that applies one-handed navigation principles. The method feels good for calling and messaging apps because users tend to use one hand for dialing and texting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/479a00b1-cf87-43e0-89cb-2e3b6850b3ef/cuberto.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/479a00b1-cf87-43e0-89cb-2e3b6850b3ef/cuberto.gif" width="780" height="" alt="" /></a><figcaption>(Image: <a href="https://dribbble.com/shots/2934372-Android-UI">cuberto</a>)
</figcaption></figure>

## Conclusion

Helping users navigate should be a high priority for every app designer. Both new and returning users should be able to figure out how to move through your app with ease. The easier your product is for them to use, the more likely they’ll use it.</p>

<blockquote style="border-radius: 8px;">This article is part of the UX design series sponsored by Adobe. The newly introduced Adobe Experience Design CC (Beta) tool is made for a <a href="https://adobe.ly/2q0pi6P">fast and fluid UX design process</a>, as it lets you go from idea to prototype faster. Design, prototype and share — all in one app.
You can check out more inspiring projects created with Adobe XD on <a href="https://www.behance.net/galleries/adobe/5/Experience-Design">Behance</a>, and also visit the <a href="https://blogs.adobe.com/creativecloud/design/">Adobe XD blog</a> to stay updated and informed. Adobe XD is being updated with new features frequently, and since it’s in public Beta, you can <a href="https://adobe.ly/2q0pi6P">download and test it for free</a>.</blockquote>

{{< signature "ms, vf, al, yk, il" >}}

